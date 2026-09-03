# Agent Presets

Each preset pre-fills defaults across several of the 10 constraint categories (see `prompt-anatomy.md`) so the interview needs fewer questions. When a user picks one, state the pre-filled defaults in one short line, then only ask about the categories still marked "open" below. The user can always override any default if they push back on it later — presets are a starting point, not a lock.

---

## Commercial Campaign Strategist (Creative Subagent Active)

Full-funnel commercial ideation, brand positioning, and performance ad creation. Automatically activates the internal **Creative Strategist Subagent** to interrogate product DNA, perform live competitor/category research, mine consumer pain points, and draft a complete 5-beat Campaign Blueprint before cinematic prompt execution.

Pre-fills:
- **Strategy Engine**: Executes Stage 1 (Product Interrogation & "So What?" drill), Stage 2 (Autonomous Live Market & Competitor Ad Mining), and Stage 3 (Single-Minded Proposition & 5 Awareness Stages).
- **Creative Routes**: Generates 3 contrasting angles (Contrarian Problem-First, Emotional Human Truth, Visceral Demonstration).
- **Deliverable**: Outputs a master 5-beat Scamp Blueprint before moving to camera kinematics, FACS performance, and audio design.

Still open: Product mechanism, target audience, business goals, selected creative route, and target engine.

---

## UGC Ad Director (Creative Subagent Active)

Hook-driven, handheld, direct-to-camera, product/brand focus. Automatically engages the **Creative Strategist Subagent** to interrogate the product benefit and generate high-converting 0–3s hooks.

Pre-fills:
- **Strategy & Hook**: Mines high-CTR scroll-stopping hooks (Nobody Warns You, Pain Confession, Contrarian Reversal) via `references/campaign-blueprints.md`.
- **Camera behavior**: handheld, visibly imperfect (sway, reframe lag), not gimbal-smooth.
- **Performance & subtext**: direct-to-camera address, conversational/thrown-away delivery rather than performed/salesy.
- **Style & realism**: photoreal, natural skin texture, light film grain.
- **Timing**: short (5-10s), built around one hook line and one payoff beat.

Still open: product core benefit, target audience, selected hook variation, scene/blocking, audio/dialogue, and brand locks.

---

## Narrative Cinematographer

Character-driven short film beat. Prioritizes performance depth and deliberate camera language over speed/energy.

Pre-fills:

- **Performance & subtext**: always asks for want/obstacle explicitly, expects at least one beat change within the shot
- **Camera behavior**: deliberate, motivated moves (not random handheld energy) — push-ins, holds, slow reveals tied to the emotional beat
- **Style & realism**: photoreal or filmic grade, cinematic lensing

Still open: subject/identity, scene/blocking, timing/beat count, lighting, audio, physics/materials, positive locks.

---

## Product Beauty Shot

Locked or smooth camera, macro/texture focus, no dialogue — built for showing off a product or material.

Pre-fills:

- **Camera behavior**: locked or smooth/gimbal move, no handheld imperfection
- **Audio**: skip dialogue entirely; ambient/SFX only or silent
- **Performance & subtext**: not applicable, skip this category
- **Physics & materials**: high priority — always ask about the specific material behavior (liquid, reflective surface, fabric, powder, etc.)

Still open: subject/identity (the product itself + brand lock), scene/blocking, timing, lighting, style/realism, positive locks.

---

## Social Hook Creator

Fast, high-energy, built to stop a scroll in the first second.

Pre-fills:

- **Timing**: very short (3-6s), front-loaded — the strongest visual/hook happens in the first beat, not built up to
- **Camera behavior**: energetic, can include a hard cut or whip pan/snap zoom
- **Style & realism**: high contrast, punchy color, not necessarily photoreal

Still open: subject/identity, scene/blocking, lighting, audio, physics/materials, positive locks.

---

## Dialogue Two-Hander

Two speaking characters, one continuous take. Built for Veo/Seedance native audio and Kling lip-sync.

Pre-fills:

- **Performance & subtext**: always asks for each character's want, staggers them for contrast, expects the beat change where the dynamic flips
- **Audio**: dialogue-first — exact lines + per-speaker voice spec (register, pacing, accent, emotional coloring) + lip-sync-safe framing (mouths visible, stable medium or closer)
- **Timing**: short enough that every line fits in one breath at the clip length (8s ≈ two short lines max)

Still open: subject/identity (reference stills strongly recommended — prose alone won't hold two faces), scene/blocking, camera, lighting, positive locks.

---

## Atmospheric Establishing

No people, environment-as-subject. Establishing shots, location reveals, mood plates.

Pre-fills:

- **Performance & subtext**: not applicable, skip
- **Camera behavior**: slow, single move (drift, rise, arc) — one move, not three
- **Audio**: sound-bed driven — ambience + 1 signature SFX, explicit "no music" unless scored in post
- **Timing**: front-load the reveal or the grade shift; longer ceilings welcome (Sora up to ~25s)

Still open: subject/environment, scene/blocking, lighting/palette anchors (name 3–5 specific colors), style/realism, positive locks.

---

## Edit / Restyle (Kling O1 · Runway Aleph)

The user has existing footage and wants to change X — not a fresh generation.

Pre-fills:

- **Workflow**: surgical edit verbs ("swap X for Y", "remove", "add", "restyle") aimed at exact elements, ~50–150 words, subject-first then motion/camera then style anchors
- **Everything else**: inherits the source clip — don't re-brief the scene, describe only the delta

Still open: the exact element(s) targeted, the replacement spec, which edit mode (swap / remove / add / restyle), positive locks on everything that must NOT change.

---

## Custom / None of these

No defaults assumed — ask through all 10 categories from scratch, one question at a time, using context clues from whatever the user has already described to skip only what they've explicitly already told you.
