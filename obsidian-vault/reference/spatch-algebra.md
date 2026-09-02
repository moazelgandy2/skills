# Full patch-instruction reference

This covers the complete `markdown-patch` 2.x algebra as exposed by the Obsidian Local REST API. The MCP `vault_patch` tool only ever speaks the JSON-instruction shape described in the main SKILL.md — you'll need this file only if you're working with the raw REST API directly (e.g. via `curl` or a script calling `PATCH /vault/{path}`), debugging an error code, or explaining version-migration behavior to the user.

## Instruction fields (recap, complete)

| Field | Type | Notes |
|---|---|---|
| `targetType` | `"heading"` \| `"block"` \| `"frontmatter"` | required |
| `target` | array (heading) / string (block, frontmatter) / null | required |
| `operation` | `"replace"` \| `"prepend"` \| `"append"` \| `"delete"` | required |
| `scope` | `"content"` \| `"marker"` \| `"markerAndContent"` \| `"parent"` | default `"content"` |
| `content` | string | payload option 1 |
| `value` | JSON | payload option 2 |
| `destination` | `{parent, place}` | payload option 3, only with `scope: "parent"` |
| `within` | integer | heading targets only, refines to a body block |
| `createTargetIfMissing` | boolean, default false | |
| `rejectIfContentPreexists` | boolean, default false | |
| `ifMatch` | string | document-map `version` token |

Exactly one of `content` / `value` / `destination` may be present, and which one is valid depends on `targetType`/`scope`/`operation` — not every combination in the algebra is meaningful; invalid ones return `400`.

## Scope × target details

- **`content`** on a heading = the subtree below the heading line. The heading line itself is never part of this scope — a `replace` here needs only the new body, not the heading text, or it'll get duplicated underneath the (unchanged) heading.
- **`marker`** on a heading = just the heading line's text, no `#` characters (they're taken literally, not stripped — including them turns `"## New Name"` into a literal heading rendering `## ## New Name`). On a block, the marker is its `^id`; renaming takes a new id (letters, numbers, hyphens, underscores). On frontmatter, the marker is the key; renaming takes a new key name.
- **`markerAndContent`** = both together. For a heading, this is the only scope where a `replace` can change the heading's own text *and* rebase it as a heading vs. dissolve it (if the replacement `content` has no leading `#`, the section becomes a plain paragraph — no longer addressable as a heading). `prepend`/`append` at this scope insert a new sibling section immediately before/after, not inside.
- **`parent`** — only valid with `operation: "replace"`, and only for headings. Re-parents the section using `destination: {parent: [...] | null, place}`. Levels are rebased automatically to fit the new position.

## `within`: literal splice into a body block

Every other write operation is "block-boundary safe" — the engine trims your `content`'s edge whitespace and inserts its own separating blank line, so a normal `append`/`prepend` at `content` or `markerAndContent` scope always produces a brand-new block and can never accidentally glue onto an existing paragraph or list.

`within` breaks out of that safety net on purpose: given a heading target and an index (0-based, negative from the end, isolated `^id` lines uncounted), the instruction acts on that one direct body block of the section instead of the whole section. With `scope: content` (the default), `replace`/`prepend`/`append` splice your `content` **literally** into that block — you own every character, including leading/trailing whitespace and newlines — so `append` with `"\n- item"` continues a list, and without the leading `\n` your text would instead run onto the end of the last existing line. `delete` at this scope removes the whole block. With `scope: markerAndContent`, `prepend`/`append` instead insert a new block immediately before/after the targeted one (the safe, engine-managed kind).

`within` cannot be combined with `createTargetIfMissing` (there's nothing to create — you're indexing into existing blocks), and only applies to heading targets.

Because `within` is positional, always read the document map or the section itself immediately before using it, and pair it with `ifMatch` — if the file changed in between, you want the patch to fail rather than splice into the wrong block.

## Table row writes

A `block` target addressing a table accepts a 2-D JSON array in `value`: one array of cell strings per row. `append` adds row(s) after the existing body rows; `prepend` puts them first (right below the header row); `replace` swaps all body rows for the given ones. Each row must have exactly as many cells as the table has columns, or the whole write is rejected. Cells are treated as content, not markdown table syntax — a literal `|` is escaped for you automatically, and a cell may not contain a line break (send `<br>` if you need a visual break within a cell), since a table row is one line.

## Frontmatter semantics

Frontmatter payloads always go in `value`, never `content` — even for what looks like plain text, since the engine needs to know the JSON type (string vs. number vs. list vs. object vs. null vs. boolean). `replace` sets the field outright. `prepend`/`append` **merge** into the existing value: list concatenation for arrays, dict merge for objects, string concatenation for strings. There is no built-in "remove one item from a list" operation — the standard pattern is: read the field's current value, filter/modify it in your own logic, then `replace` the whole field with the result.

## Duplicate headings and block ids

If a document has two sibling headings with identical text under the same parent, or a repeated block reference id, only the *first* occurrence keeps the plain text/id as its address. Every later occurrence gets a non-printable marker suffix appended to its key in the document map. Always copy that key verbatim from the map response — never try to type or reconstruct the marker by hand, since it isn't printable/typeable text.

## Optimistic concurrency

`vault_get_document_map` returns a `version` token (a content hash). Pass it back as `ifMatch` on a subsequent patch to make the edit conditional: if the file changed since you read the version, the patch fails with `412` and the file is left untouched, so you can safely refetch and retry rather than risk clobbering an intervening change. Use this for any multi-step read-then-write sequence where the file might change between your calls (e.g. a bulk-edit loop, or an edit based on stale context from earlier in a long conversation).

## Raw-content mode (REST API only, templating-friendly)

Not relevant to the MCP tools, which always send structured JSON — but useful if scripting the REST API directly, or if a `text/markdown`-bodied request is easier than JSON-escaping markdown content. The instruction's fields travel as URL path elements / headers, and the request body is the raw payload:

- Target via URL path: `PATCH /vault/note.md/heading/A/B` (percent-encode segments with non-ASCII or a literal `/`).
- Or via `Target-Type`/`Target` headers with an explicit `Markdown-Patch-Version: 2` (the `Target` header is percent-encoded JSON for headings, a plain id/key for block/frontmatter).
- `Operation`, `Target-Scope`, `Within`, `Create-Target-If-Missing`, `Reject-If-Content-Preexists`, `If-Match`, `Destination` all map to headers.
- Body content-type selects the payload carrier: `text/*` → `content`, `application/json` → `value`, no body → none (a delete, or a `Destination`-only move). An empty body never clears content by accident — a `replace` with an empty body is rejected as a missing carrier; send an explicit `{"content": ""}` JSON body to clear deliberately.

URL-path targeting and header-based targeting can't both be present (`422 ConflictingTargetSpecification`), and `Target-Type`/`Target` headers on a PATCH without an explicit version header fail loudly (`400 PatchHeaderTargetingRequiresExplicitVersion`) rather than guessing between raw-content mode and the deprecated 1.x format.

## Deprecated 1.x format

Superseded, removed in plugin 6.0, still reachable via `Markdown-Patch-Version: 1` in the meantime (responses carry a `Deprecation` header). Headings were `"A::B"`-delimited strings instead of arrays, renames required including the `#` characters, frontmatter values were serialized as strings instead of typed JSON, and the document map was a flat list instead of a nested tree. Only relevant if a user shows you old integration code and asks why it stopped working, or asks you to migrate a script — in which case, translate to the 2.x shape described in the main skill rather than perpetuating the old format.

## Error codes worth recognizing

- `400 InvalidPatchInstruction` — malformed instruction, or an operation×scope×targetType combination that isn't part of the algebra (e.g. a JSON body on a heading target in raw mode).
- `404` — the file, or the addressed target within it, doesn't exist and `createTargetIfMissing` wasn't set.
- `409` — `rejectIfContentPreexists` was set and the content already appears in the target span.
- `412` — `ifMatch` didn't match the current version; file untouched, safe to refetch and retry.
- `422 ConflictingTargetSpecification` — more than one targeting mechanism supplied at once.
- A `heading-depth-overflow` warning (not an error) appears in the `Markdown-Patch-Warnings` response header, percent-encoded JSON, when a rebased heading level would exceed h6 — it still writes, just flags it.
