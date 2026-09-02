---
name: coderabbit-wsl
description: Run a CodeRabbit AI code review on this project's code via the CLI installed on WSL, scoped to the right files, and summarize the findings into a prioritized fix list. Use this whenever the user wants to review the code / working tree / a package or branch / a before-merge or before-commit pass, says "CodeRabbit" or wants an AI review or a bug/security scan ("check my changes", "scan for issues", "review before merge", "find bugs in X"). Trigger even if the user does not name the skill. Runs through the PowerShell tool on Windows → WSL.
---

# CodeRabbit Code Review (Windows → WSL)

Run the CodeRabbit CLI (installed on WSL, located dynamically — see Step 0) against this repo and turn the review into a short, prioritized, actionable list. Do not just dump the raw output.

## Two rules that matter on this machine

1. **Always execute through the PowerShell tool, never Git Bash.** This host is Windows. The Bash tool in this environment is Git Bash, which rewrites `wsl` calls and can silently mangle the embedded quotes and `&&` — producing wrong or empty reviews. Run the `wsl bash -l -c "…"` string via the **PowerShell tool** instead.

2. **Decide the scope before you run — don't review the whole repo by default.** A monorepo-wide review returns hundreds of files. If the user didn't already say what to review, either clarify or pick the least-surprising narrow scope (uncommitted work, or a single package), and encode it with a scope flag.

## Prerequisites

- CodeRabbit CLI installed somewhere in WSL and authenticated (`coderabbit auth login`; for headless/agent use `coderabbit auth login --scope`). This skill is machine-agnostic — it detects the binary location and the repo path at runtime (Step 0), so nothing is hardcoded to a user's home or a fixed mount.
- This repo must be reachable from WSL (Windows project trees live under a `/mnt/<drive>/…` mount).

## Step 0 — Resolve paths dynamically (any machine)

Don't hardcode the binary path or the repo mount. Derive both at runtime; this works for any drive letter, user, and machine.

```powershell
# 1) Convert the current Windows project folder into its WSL path (any drive letter):
$cwd = (Get-Location).Path                      # e.g. D:\projects\kallem
$WSL = ($cwd -replace '\\','/') -replace '^([A-Za-z]):/', { '/mnt/' + $_.Groups[1].Value.ToLowerInvariant() + '/' }
# (drive letter is lowercased → /mnt/d/...; validated against `wsl bash -lc "wslpath -w`"`)

# 2) Locate the CodeRabbit binary wherever it is (empty string if not resolvable):
$CR = (wsl bash -lc "command -v coderabbit").Trim()
if (-not $CR) { $CR = 'coderabbit' }            # fall back to the WSL PATH name
```

Used as: `cd "$WSL" && $CR review …`. A WSL login shell usually already has `~/.local/bin` on PATH, so `command -v coderabbit` normally resolves; `$CR` just makes the call explicit and portable. If it returns nothing and the review says `command not found`, put the binary's folder on WSL's PATH (or call its full detected path).

## Step 1 — Pick the review scope (do this first)

Ask yourself what changed / what the user cares about, then choose the tightest matching scope:

| You want to review | Flag | Example |
|---|---|---|
| One package / directory only (avoids a file explosion) | `--dir <relpath>` | `coderabbit review --dir packages/backend --agent` |
| Uncommitted (staged + tracked edits) only | `--uncommitted` | `coderabbit review --agent --uncommitted` |
| Committed changes only | `--committed` | `coderabbit review --agent --committed` |
| Include untracked, never-added files | `--include-untracked` | `coderabbit review --agent --include-untracked` |
| Against a base branch (pre-PR from main) | `--base main` | `coderabbit review --agent --base main` |
| Faster / lighter pass | `--light` | `coderabbit review --agent --light` |

Heuristics:

- "review the changes I just made" → `--uncommitted`.
- "review package X / this folder" → `--dir <X>` (this is the preferred way to avoid a large-file explosion).
- About to open/merge a PR → `--base main`.
- Flags combine: `coderabbit review --dir packages/backend --uncommitted --agent`.
- If even a narrowed scope still seems huge, prefer asking the user taming vs silently reviewing the whole tree.
- **Keep the diff under the free-plan file ceiling (~150 files).** Even `--uncommitted` can exceed it if the current branch is far ahead of the base; narrow with `--dir <pkg>` (and `--base <closer-commit>` if needed). If the CLI still says "Too many files!", copy the suggested narrower scope it prints rather than guessing.

## Step 2 — Run the review (PowerShell tool)

Run the chosen command with the PowerShell tool. A review can take 2–5 minutes, so run it in the background (`run_in_background: true`) with a generous timeout and keep working.

```powershell
wsl bash -l -c "cd '$WSL' && $CR review --agent"
wsl bash -l -c "cd '$WSL' && $CR review --dir packages/backend --agent"
wsl bash -l -c "cd '$WSL' && $CR review --agent --uncommitted"
wsl bash -l -c "cd '$WSL' && $CR review --agent --base main"
```

Note: plain text is the default output. `--agent` emits the machine-readable findings this skill wants. There is no `--plain` flag (default is already plain). The scope flags are `--committed` / `--uncommitted` (not a `-t` shorthand).

## Step 3 — Read the `--agent` output

`--agent` writes **JSON Lines** — each line an event with a `type` field. Don't treat all lines alike:

| `type` | Meaning | Act on? |
|---|---|---|
| `finding` | one review finding (severity + file + guidance) | ✅ the only lines you summarize |
| `review_context` | scope metadata — `currentBranch`, `baseBranch`, `workingDirectory` | surface branch info in your summary |
| `complete` | end event → `findings` count + `reviewedFiles` list | confirm scope + report how many files were scanned |
| `status` / `heartbeat` | progress / no-op heartbeats | ignore (noise) |

Extract every `{"type":"finding", …}` and ignore `status`/`heartbeat` lines. Each finding includes (at least):

- `severity` — critical / major / minor / trivial
- `fileName` — relative path (scoped by your `--dir` / scope)
- `description` / `codegenInstructions` — what to change and how
- `suggestions` — optional code snippets

Use the final `complete` line's `findings` count and `reviewedFiles` to confirm your scoped `--dir` covered the intended files and to state how many were scanned. Surface `review_context`'s branch info so the summary reads like a review of the current work.

Synthesize the output; don't echo the raw stream:

- Group by severity, then order critical → trivial.
- For each finding: file, severity, one–two-line summary, and the concrete fix.
- Put the critical/major findings on top and make them prominent; note explicitly when the review surfaced nothing critical.

## Step 4 — Fix and verify

1. Fix findings critical → major → minor.
2. Re-run the same scoped review to confirm those findings are gone; stop when only trivial/acceptable items remain.
3. To restate the previous run's findings without a full re-review: `wsl bash -l -c "cd '$WSL' && $CR review findings"`.
4. For a fast follow-up, `coderabbit stats` shows recent review activity.

## Why these details

- **PowerShell over Git Bash**: on this Windows host the Bash tool is Git Bash; `wsl` through it breaks quotes/`&&`, so PowerShell is the reliable interpreter.
- **Scope-first**: `--dir` + a tight scope keeps reviews fast, cheap, and focused instead of a repo-wide wall of files.
- **Synthesize, don't echo**: the user gets value from a short prioritized action list, not the raw payload.
- **Verify the fix**: re-running scoped review closes the loop and confirms the resolution before merge.

## Troubleshooting

| Symptom | Fix |
|---|---|
| `command not found` | Find it first: `wsl bash -lc "command -v coderabbit"`. If empty, the binary isn't on WSL `PATH` — add its folder to `~/.bashrc`/`~/.bash_profile`, or call it via its detected/installed absolute path |
| `Permission denied` | In WSL: `chmod +x $(command -v coderabbit)` |
| Empty result, "No changes to review" | Check `git status`; scope too narrow vs changes → add `--include-untracked` / `--base main` |
| Too many files | The diff exceeded the plan's cap (~150 files) — the CLI prints a suggested narrower scope to copy (`--dir <path>`, or `--base <closer-commit>` when the branch is far ahead). Pick one and re-run |
| Review limit reached / seat not linked | A usage/seat or rate limit — wait for the reset window, or link an assigned seat / use an Agentic API key (`--api-key` / `--region`). This is an account constraint, not a path/scope error |
| Timeout | Review can sleep 2–5 min → `run_in_background: true` + generous timeout |
| Wrong/interleaved shell output | Ensure you ran via the **PowerShell tool**, not Git Bash |
