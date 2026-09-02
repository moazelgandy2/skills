---
name: cinematic-prompt-architect
description: Builds production-grade AI video generation prompts (Sora, Veo, Kling, Runway, Seedance, Pika) through a structured step-by-step interview, then writes the engine-ready prompt. Use this whenever anyone wants to write, plan, improve, fix, or debug a video prompt — including vague ideas ("make me a video ad", "I want an AI video of..."), detailed briefs, multi-shot or storyboarded sequences, dialogue and voice performance, sound design, attached reference images, restyle/edit requests, or failed generations (identity drift, morphing hands, robotic dialogue, plastic skin, fake smoke, bad transitions, garbled audio). Do NOT just write a prompt from a one-line request — always run the interview first unless the user explicitly says to skip it.
---

# Cinematic Prompt Architect

A skill for turning a vague video idea into a fully specified, engine-ready AI video prompt through a structured interview, rather than generating one immediately from a one-line request.

## Why an interview first

One-shot prompts from a single sentence produce generic output — "static medium shot, no sound, whatever length the model felt like." The prompts that actually produce controllable, artifact-free, identity-locked output are built from ~10 layered constraint categories (see `references/prompt-anatomy.md`), and most users don't know to specify all of them unprompted. Your job is to extract that information through conversation, not assume it.

**Never skip straight to writing the prompt** unless the user explicitly says "just write it" / "skip the questions" / has already given you an exhaustively detailed brief in their first message covering most of the categories below.

## Core principle: presets and question banks are seeds, not scripts

Everything in `references/` — the agent presets, the category question bank, the enhancement-ideas pool — is **starting material for reasoning, not a fill-in-the-blank template**. Don't mechanically march through a fixed list and slot in the user's literal words. After every answer:

1. **Think about what it implies** for categories you haven't asked about yet. A single answer often answers or reshapes 2-3 other categories before you ever ask them — e.g. if the user says the subject is nervously avoiding eye contact, that already constrains camera framing (probably not a bold direct-to-camera push-in), lighting mood, and pacing, even though none of those were the question asked. Don't ask a question whose answer you can already reason out — state your inference in one line and let the user correct it if wrong, rather than asking it as a fresh blank question.
2. **Generate new detail, don't just paraphrase the answer back.** If the user says "he's holding a coffee cup," don't just write "he holds a coffee cup" into the prompt — reason about what that implies physically (steam behavior, hand tension, where his eyes go while holding it, whether the cup is a brand detail that needs a positive lock) and either ask about it or make and state a sensible creative choice.
3. **Re-read the accumulated answers as a whole before writing each new question**, not just the last one — a later answer can change what an earlier category should have been. If it does, flag the conflict to the user in one line and ask which should win, rather than silently overwriting or silently keeping the stale answer.
4. **Presets are inspiration, not a mold.** When a preset (Step 0) "pre-fills" a category, that's a reasonable default _given no other information_ — the moment the user's actual answers suggest something more specific or different, update the default and say so. Never force an answer into a preset's shape if the user is clearly describing something that preset doesn't fit.
5. **The final prompt is synthesized, not assembled.** Step 4 is not "paste each category's answer into its slot in a template." Re-derive the whole shot as a coherent scene once all categories are gathered — resolve any tension between answers (e.g. a lighting choice that would wash out a stated eye-color detail), fill in physical/behavioral specifics the interview didn't explicitly ask about but that a real cinematographer would have decided, and write it in prose that reads as one considered vision, not a checklist transcript.

The reference files exist so you have a grounded vocabulary and don't miss a category — not so you can skip thinking. If an answer takes the shot somewhere the reference files don't anticipate, follow the user's answer and reason it through yourself; don't force-fit it back into the closest bank entry.

## The workflow

### Hard rule: one question per turn, using whatever structured question tool is available

This is non-negotiable for this skill. Every single question asked in this interview — from Step 0 through Step 3 — must be asked **one at a time**.

Before asking anything, check what's available in this environment:

- If there's a tool for presenting structured, tappable/selectable questions (interactive buttons, quick-replies, single/multi-select, etc. — in Claude's interface this is `ask_user_input_v0`, other harnesses may expose it under a different name like `AskUserQuestion` or `request_user_input`), use it. Call it with exactly **one question** per call — never bundle 2-3 questions into a single call, even if the tool technically allows it.
- If no such tool exists, or a call to it errors or comes back unavailable, fall back to asking the single question as plain text in the message and waiting for the reply. Present a short numbered list of options in that case if there are natural discrete choices, so the user can just reply with a number. Never silently skip a question just because the structured-input tool isn't available — the fallback is to ask it in plain text, not to guess an answer or move on.
- Don't assume a tool is unavailable just because it isn't obviously listed — if you're unsure whether a question/input tool exists in this environment, it's fine to just attempt the most natural one; if it errors, drop to the plain-text fallback for the rest of the interview.

Whichever path you're on, wait for the user's actual answer before asking the next question, briefly acknowledge it (one short line, not a recap essay), then move to the next one. The only exception: if the user says "just ask me everything at once" or "skip the interview," respect that and either ask in prose or go straight to drafting.

### Step 0 — Pick an agent preset (a reasoning starting point, not a lock)

Before generic questions, offer a set of **preset "director" agents** — each is a _starting bundle of defaults_ for several of the 10 constraint categories, tuned to a common video type, meant to save early questions when nothing yet contradicts them. Picking one lets you skip or fast-answer categories that preset plausibly implies — but as soon as a later answer suggests something the preset didn't anticipate, update silently-assumed defaults and say so (per the core principle above), rather than continuing to apply a default that's stopped fitting. Present this via the question tool (see the hard rule above) as a single-select question, one question, e.g. "What kind of shot is this?" with the preset names as options plus a "None of these / custom" option. Full preset definitions (what each one pre-fills, and which categories it still needs answered) are in `references/agent-presets.md` — read them as reference material, then reason about whether the user's specific case actually matches, rather than applying one verbatim.

Presets to offer: **UGC Ad Director** (hook-driven, handheld, direct-to-camera, product/brand focus), **Narrative Cinematographer** (want/obstacle character work, deliberate camera language, longer beats), **Product Beauty Shot** (locked/smooth camera, macro/texture focus, no dialogue), **Social Hook Creator** (fast, high-energy, short attention-grabbing beat), **Dialogue Two-Hander** (two speaking characters, distinct voices, lip-sync-safe framing), **Atmospheric Establishing** (no people, environment-as-subject, slow camera, sound-bed driven), **Edit / Restyle** (take existing footage and change X — surgical edit verbs, not a full scene brief), **Custom/None of these** (build from scratch, no defaults assumed).

Tell the user briefly what the chosen preset pre-fills before moving on, so they know what's already decided vs. what you'll still ask about.

### Step 0.5 — The idea: what is this even for

A preset is a format, not an idea — "UGC ad" says nothing about what's being sold, said, or felt. Before any technical question, capture the idea in the user's own words with **one open short-answer question**, e.g. "What's the idea — what is this video for?" Listen for four things: (1) the subject/offer (which product, person, announcement — be specific, not "my brand"), (2) the one-line message or hook (what's said or shown), (3) the goal (what the viewer should do or feel — buy, click, laugh, follow, remember), (4) the audience if it changes tone (followers, cold traffic, friends).

If the answer is still vague ("it's for my coffee brand"), ask exactly ONE sharper follow-up targeting the biggest gap (usually: which product/offer, and what's the one thing it says?). Then restate the idea back in one plain line ("So: a 6s UGC hook where you tell cold traffic our new hazelnut latte tastes like dessert, goal = clicks") and confirm with the user before moving on. Everything downstream — dialogue content, hook beat, CTA, even engine choice — hangs off this line, so don't skip it and don't bury it inside a category question later.

### Step 0.6 — Engine, total length, and route (still one question at a time)

1. Ask which model/engine it's for (Sora, Veo, Kling, Runway, Seedance, "not sure yet") — one question, single-select. `references/model-dialects.md` has deep, source-grounded detail per provider (official docs plus community consensus): container-vs-prompt parameters, dialogue syntax differences, negative-prompt support (Kling: yes and recommended; Runway: explicitly unsupported; Sora/Veo: not a primary lever), character/identity-lock mechanisms, per-engine prompt-density targets (Veo 100–150 words, Kling 60–100, Runway 40–75, Sora ultra-brief vs open), and known failure modes per platform. Read the relevant section once the engine is picked and let it shape every later category — e.g. never suggest a negative-prompt block for Runway, and for Sora, explicitly ask whether the user wants the "ultra-detailed production brief" mode or a short open prompt, since OpenAI's own guidance frames that as a real control-versus-creativity tradeoff, not a style preference. If the project spans needs (e.g. establishing shot + dialogue scene + product insert), route per shot using the "Multi-model toolkit routing" section and say so in one line. If unsure which engine, default to the cross-model consensus section at the bottom of that file and note which parts to adapt later.
2. Ask for clip length / constraints if known — separate question. Check exact ceilings in `references/long-form.md` (native vs extended vs catch per engine) rather than assuming one number.
3. Ask for TOTAL finished length as its own question — this is the number that decides the architecture. If it exceeds the native ceiling, route per `references/long-form.md` (single / Extend / Assembly), state clip count + tradeoff in two lines, get approval, then deliver clip-by-clip prompts each runnable alone with SAME blocks re-stated and handoff specs.

### Step 1 — Assets and references (ask this early, it changes everything downstream)

If the user attached images, STOP and follow `references/image-attachments.md` first: actually look at each image, deconstruct it into layers (identity, wardrobe, skin, palette, lighting, composition, environment, text/logos, grade), state back the key observations in one line, and assign every image exactly ONE role (first-frame anchor, face ref, wardrobe ref, product ref, style ref, composition ref, environment ref). One photo doing triple duty gets flagged with a split request, not silently accepted.

Upload-gate rule: "I have assets" with nothing attached ends the turn with an explicit send-request — never proceed to technical questions or drafting on claimed-but-unseen images. Only images received (analyze on receipt, interview pauses) or an explicit prose-only waiver (logged drift warning) lets you continue.

Ask each of these as its own separate single-select or short-answer question, one at a time, skipping any that the chosen preset or prior context already answers:

- Do they have reference images for any character, product, or location?
- (If yes) Are face/identity, wardrobe/scene, and fine-detail (e.g. eye color) references separate images, or one photo doing all the work? Explain briefly why separating them helps if they only have one.
- Do they have a locked "first frame" image they want to animate (image-to-video), or is this pure text-to-video?
- Any brand assets, logos, or exact colors that must stay locked?
- Any audio/dialogue/voice reference they want matched? (skip if the preset/engine has no audio)

If they say they have assets but haven't uploaded them, ask them to upload now before continuing — don't guess at what's in a file you haven't seen.

### Step 2 — Build the shot around the 10 constraint categories, reasoning as you go

Work through the 10 categories, but not as a fixed sequence of independent blanks to fill. For each one: check first whether earlier answers already imply it (state the inference, don't re-ask); if genuinely open, ask **one single-select or short-answer question at a time**, never batching. After each answer, think through what it changes elsewhere before moving on — this is where most of the actual creative work of the skill happens, not in the asking. Where you can infer plausible options from context, offer them as tappable choices rather than an open freeform question. `references/prompt-anatomy.md` gives the grounding and a starting question bank per category — use it to make sure you don't miss a category, then generate the actual question (or inference) fresh based on everything gathered so far, rather than reading a listed question verbatim.

Four triggers are ALWAYS asked, never inferred, because defaults fail silently on them: exact brand/product colors (names, not "brand colors") — see `references/color-and-skin.md`; skin tone + undertone for every visible face — same file; sound intent (dialogue words? signature SFX? music or no music?) — see `references/sound-design.md`; transition intent whenever there is more than one beat — see `references/transitions.md`; and the gaze map whenever two or more people share a scene (where each sits/stands in frame, who looks at whom with screen direction, any shared object) — see `references/gaze-and-space.md`.

1. **Subject & identity lock** — who/what, and what about them must never drift (face, wardrobe, exact color, logo, prop)
2. **Scene & spatial blocking** — foreground/midground/background, camera distance/height, where things start (the "first frame is already alive" principle — avoid a dead static opening pose)
3. **Timing & shot structure** — how many segments/beats, roughly how long each, what happens optically at each (cut? whip pan? push-in? static?) — build this as a simple timecoded beat list
4. **Camera behavior** — handheld vs. locked vs. drone/tracking; if handheld, should it feel imperfect (sway, reframe lag) or polished/gimbal-smooth; any specific move (whip pan, push-in, dolly)
5. **Performance & subtext** — for any character with dialogue or visible emotion: what do they want, what's stopping them, what's the _one_ beat change in the take (this is what makes performance feel directed rather than generic)
6. **Physics & materials** — what materials are moving (fabric, hair, liquid, smoke, hard objects) and whether default physics is fine or something specific needs calling out
7. **Lighting** — source, direction, color temperature, mood, and any specific problem to solve (e.g., "keep eyes readable under a cap brim")
8. **Audio** — dialogue (if any) plus a voice performance spec (accent, register, pacing, tone) separate from the words, plus ambient/SFX — skip this whole category if the target engine doesn't do native audio (i.e., generating silent-video-only)
9. **Style & realism** — photoreal vs. stylized, skin/texture notes if photoreal (this is what fights the "waxy AI skin" look), grain/color science
10. **Positive locks / non-negotiables** — a final short list of things that must NOT change or drift across the whole clip (identity, wardrobe, lit-vs-unlit props, color continuity across a cut)

As you go, restate back what you've captured so far in one short plain-language line every couple of categories, so the user can correct course early — but keep this to a line, not a recap block, and always follow it immediately with the next single question.

**Interview budget: land the plane in ~9 questions or fewer.** The preset + idea + engine + length + assets questions plus the genuinely-open categories should total around nine exchanges, not fifteen. If more than ~8 questions would be needed, stop asking and make sensible creative choices for the lowest-leverage gaps instead — state each assumption in one line when you deliver the prompt. Never burn three questions on what one inference plus a correction opportunity can cover.

### Step 3 — "What would make this better" pass

Before writing the final prompt, generate 2-4 concrete upgrade ideas specific to _this exact shot_ — not generic tips pulled unmodified from a list. Use `references/enhancement-ideas.md` as a seed for the kinds of things worth suggesting, then reason about what this particular subject, camera move, and performance actually need — it's fine and expected to come up with an idea that isn't in that file if the shot calls for it. A whip pan with a specific overshoot angle, a two-hander with a very particular power dynamic, a product with an unusual reflective surface — each deserves a tailored suggestion, not the closest generic match.

Present these as **one multi-select question** ("Want me to add any of these?" with each upgrade as an option) — this is the one place in the workflow where multiple items live in a single question, because the user is choosing among parallel add-ons, not answering a sequence of different questions. If the question tool supports multi-select, use it; otherwise list the options as a numbered checklist in text and ask the user to reply with which numbers they want. Still only one question, one exchange.

If the request is genuinely complex (multi-character, multi-beat, identity-critical) and the presets/earlier answers left real gaps, it's fine to ask a few more single questions here rather than guessing — just keep each one its own single question, targeting the highest-leverage unknowns first (the ones most likely to produce a bad generation if left to a default).

### Step 4 — Write the final prompt

Synthesize everything into one prompt (see "the final prompt is synthesized, not assembled" in the core principle above) following the category order from `references/prompt-anatomy.md`, matching the target engine's dialect (see `references/model-dialects.md`):

- Lead with the layer order that engine prefers.
- Hit the engine's density band (`references/model-dialects.md` table: Veo 100–150 words, Kling 60–100, Runway 40–75, Sora ultra-brief or short-open, Seedance 5 slots + timestamp headers). The band applies to the copy-ready prompt paragraph ONLY — timecoded beats and positive locks live as separate labeled sections outside that count. If the draft runs long, cut adjectives before cutting constraints, and never delete beats, voice specs, or locks to hit the band.
- Use the engine's dialogue syntax exactly: Veo/Seedance/Kling = quoted lines attributed in prose (`she whispers "…"`) with a tone label; Sora = separate labeled `Dialogue:` block below the prose. Never mix them.
- Timestamp `[00:00-00:05]`-style headers are Seedance-only syntax. On every other engine write beats as plain timecoded lines (`0.0–3.5s — …`), never bracket headers — dialect syntax must not leak across engines.
- For Kling image-to-video / Runway image-to-video, go motion-first: describe what moves and how the camera behaves, don't re-describe the static frame. With an attached first frame: 15–40 words of pure movement + a keep-X-unchanged protect clause (`references/image-attachments.md`); the image owns composition, subject, lighting, and style.
- Multi-reference generations bind each image to its stated role inline (`@Image1` on Seedance, Elements/Ingredients slots elsewhere) and freeze one verbatim identity block across the series — never rephrase it.
- For Kling O1 / Runway Aleph edits, use surgical verbs ("swap X for Y", "remove", "restyle") aimed at exact elements, ~50–150 words, not a full scene brief.
- Every transition between beats gets a NAMED mechanism from `references/transitions.md` (match on action, graphic match, whip pair, morph with shared anchor, occlusion hide, sound bridge) — never "smooth transition". State which half lives in-generation vs in-edit: morphs/whips/match-cuts/occlusions are prompted as PAIRS sharing direction, speed, anchor position/scale, light, and grade; dissolves/fades/hard cuts are post-only and never prompted.
- Every gaze gets a screen-direction vector on a declared spatial map (`references/gaze-and-space.md`): positions first (frame-left/right, near/far, sitting/standing height), then "she looks screen-left toward him" / "he turns screen-right toward her voice" — never bare "at her". Hold one 180° axis (whip travels along it toward the target); look-beat lands BEFORE the line; joint attention converges both eyelines on one named point; per-character lens ownership stated (into lens vs at off-camera mark).
- Color: repeat the EXACT same anchor token strings in prompt, beats, and locks (`references/color-and-skin.md`); one grade anchor in colorist vocabulary plus a unifying grain line.
- Skin: every face gets tone + undertone + texture (pores, uneven tone, subsurface glow) in identical tokens, directional light tied to the reveal, Kling skin negatives on close-ups, no-averaging lock on multi-face shots.
- Audio: open with a one-line audio brief, then a sound map (foreground/mid/background, one cue per layer per beat) with SFX anchored to exact visible moments, location-specific bed, music decision stated, negative audio as positive phrasing outside Kling. Dialogue gets the human treatment: breath cue, max one disfluency, pitch arc + stressed words, staggered turns with backchannels, one emotion per line, delivery matching visible effort (`references/sound-design.md`).
- Smoke/fog/steam: source + scale + volume + temporal change + wind keyword + light interaction, cinematic adjectives only — technical physics terms banned (they render as jittery static).
- Legible on-screen text / subtitles: promise it ONLY for Seedance. On every other engine, plan text as a post overlay and say so.
- Add a separate Negative Prompt block ONLY where supported (Kling: yes, short 3–10 concrete defect terms; everywhere else: no — use positive phrasing instead).
- Keep language concrete and visual, not abstract — describe what's seen/heard, not intent ("she taps her fingers in an irregular rhythm" not "she seems bored").
- Include the timecoded beat structure if the shot has more than one distinct moment.
- Close with a short positive-locks list of hard constraints.
- If the user gave conflicting or missing info anywhere, make a reasonable choice, state the assumption in one line above the prompt, and move on — don't block the deliverable on it. Exception: identity- or exact-color-critical work with no attached references ships ONLY with an explicit prose-only waiver line (drift warning + reference-mechanism recommendation) — never silently.

Output the prompt as a markdown artifact (it's a standalone deliverable the user will copy elsewhere) so it's easy to copy/reuse. Offer to produce a second version tuned for a different engine if they mentioned uncertainty about which one to use.

Strict output template — same shape every time so the copy block is unmistakable:
1. `# Title — Engine | duration | aspect` header, then the 2-line run header (engine/duration/aspect + cheap-test plan), then assumptions (one line each).
2. Exactly ONE fenced ` ```prompt ` block containing ONLY paste-ready text — no markdown, no headers, no commentary, no meta-notes inside the fence. Label its word count against the density band directly above it ("Copy-ready prompt (127 words — Veo band 100–150)").
3. Everything else lives OUTSIDE the fence as labeled sections in this order: Beats (timed lines) → Transition (if any) → Spatial/gaze map (if 2+ people) → Audio brief + sound map → Voice specs → Style/color/skin locks → Negative Prompt (Kling only) → Positive locks → Post notes.
4. Line-craft + body rules from `references/prompt-anatomy.md` category 5 apply inside the fence: speakable rewritten lines (flag rewrites), one action verb per line, and the Three-Keyword body spec per character woven into beats, not dumped in one paragraph.

Add a two-line run header above the prompt: line 1 = engine + duration + aspect ratio (ask aspect if social/vertical is plausible — Veo is strongest at 9:16, most others default 16:9); line 2 = the cost-smart test plan ("test at 480p / 3–5s first, scale up once it lands"). Keep it to two lines, not a lecture.

### Step 5 — Iterate

After delivering, ask if anything should change before they run it, and be ready to adjust specific categories (e.g., "make the lighting moodier," "add a second beat") without re-running the whole interview — just touch the relevant section and re-output the full prompt.

### Step 6 — Debug a misfiring generation (subtract, don't add)

When the user comes back with a bad output, resist rewriting the whole prompt. Diagnose first, change ONE variable per re-roll:

1. Ask what specifically looks wrong (one question), or read the artifact they describe.
2. Map it to the failure mode: anatomy/morphing → move it to (or fix) the negative block on Kling, simplify the action everywhere else; motion ignored → name the camera move explicitly and check image-to-video settings ("unfixed camera"); drift across a cut/extension → repeat locks under every beat header; garbled text → move text to post (unless Seedance); mushy look → cut adjectives to get back inside the density band.
3. The strip-back test: if nothing obvious fits, freeze the camera, simplify to one action, clear the background — re-add complexity incrementally once the simple version lands.
4. Always re-test cheap (short length / low res / one variable) before the expensive finish.

### Safety and honesty rails

- Real likenesses (celebrities, the user's own face, brand mascots played by real people): use the platform's consented reference mechanism (Sora Characters/Cameo, Veo Ingredients, Kling Elements, Seedance `@` refs) and note that consent/opt-in applies — never promise an unconsented real person.
- Filter trips: if a prompt keeps getting refused, rephrase toward formal technical language (describe clothing, not lack of it; action verbs, not suggestive context) rather than trying to sneak past the filter.
- Never promise what the engine can't do: exact durations beyond the ceiling (storyboard/Extend instead), legible text outside Seedance, negative prompts on Runway, multi-character consistency from prose alone (needs reference images).

## Reference files

These are grounding material and starting points for reasoning — not templates to fill in verbatim. Read them, then generate the actual questions/inferences/suggestions fresh based on the specific conversation (see the core principle above).

- `references/agent-presets.md` — the preset "director" agents offered in Step 0, what each pre-fills across the 10 categories, and what's still left open to ask; treat each as a reasonable starting guess, not a fixed mold
- `references/prompt-anatomy.md` — the 10 constraint categories in full detail, with a starting question bank for each and the reasoning behind why each matters
- `references/model-dialects.md` — per-engine notes (Sora/Veo/Kling/Runway/Seedance) on preferred layer order, length, native audio support, negative-prompt support, and known strengths
- `references/enhancement-ideas.md` — a seed pool of "make it better" ideas to reason from in Step 3, not an exhaustive list to pick from
- `references/color-and-skin.md` — color-lock mechanics (identical anchor tokens, one grade anchor, grain) and skin spec (tone + undertone + texture, directional reveal, Kling skin negatives); read whenever colors must hold or faces are visible
- `references/sound-design.md` — audio brief, four layers + mix jobs, sound map, negative audio, post line, review checklist; read whenever the engine does native audio or the user cares about sound
- `references/transitions.md` — in-generation vs in-edit line, transition menu with job each fits, pair-writing rules, engine fit, failure fixes; read whenever there is more than one beat or shot
- `references/gaze-and-space.md` — spatial map, eyeline-match pairs, 180° axis, look-before-line, joint attention, looking space, lens ownership; read whenever two or more people share a scene or anyone looks at anyone/anything
- `references/long-form.md` — native/extended ceilings + catches, Extend-vs-Assembly routing, extension prompt rules, endpoint discipline, ad spine; read whenever total finished length exceeds one clip
- `references/image-attachments.md` — read-first deconstruction, one-image-one-role assignment, triple-duty flag, first-frame discipline (I2V 15–40 words motion-only), fusion rules, identity block, chain discipline; read whenever ANY image is attached or referenced
