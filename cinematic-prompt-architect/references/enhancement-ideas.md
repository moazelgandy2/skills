# Enhancement Ideas Pool

Pick only the ones that actually apply to the shot at hand — present as options, don't force all of them in.

**If there's a fast camera move (whip pan, snap zoom, crash push-in):**

- Describe the blur physics explicitly (acceleration/deceleration, what's readable at peak speed) rather than just naming the move.
- Add a slight overshoot-and-correct on the landing, the way a real operator finds a subject — reads as more human than a mechanically precise stop.

**If there are 2+ speaking characters:**

- Give each a distinct voice register/pacing spec so they don't sound cloned from one TTS voice.
- Stagger who "wants" what — contrast is what makes a two-hander feel directed rather than two people reciting lines.

**If going for UGC/social realism:**

- Add imperfection: handheld sway, a stray hair, an unconscious gesture unrelated to the dialogue, a slight squint in bright light.
- Avoid "presenting to camera" energy in blocking — real UGC rarely holds a perfectly centered, perfectly composed pose the whole time.

**If it's a product/brand shot:**

- Add an explicit positive-lock line for exact brand colors/logo — these are the first thing to drift in a generation.
- Consider whether the product needs its own separate reference image from the person holding/wearing it.

**If skin/faces are prominent and photoreal is the goal:**

- Add specific texture notes (pore detail, subsurface scattering at ear/nostril edges, matte vs. sheen) — this is the single biggest lever against the "waxy AI skin" look.
- Add fine film grain across the whole frame (not just skin) to unify realism rather than making skin look separately processed from the background.

**If there's a cut or hard transition:**

- Explicitly lock continuity items across the cut (light direction, shadow direction, wardrobe, prop state) — transitions are where identity/continuity most commonly breaks.

**If dialogue exists:**

- Separate the literal words from a voice performance spec (accent, register, pacing, emotional coloring) — without this the read tends to default to flat and even.

**If the idea is longer than the target engine's clip ceiling:**

- Flag this and suggest storyboarding it as 2+ chained shots with consistent reference assets, rather than one over-length prompt.

**General polish, offer sparingly:**

- A short negative-prompt list, but only for platforms that actually support it — check `references/model-dialects.md` first. Kling supports and recommends this (common effective terms: warped hands, extra fingers, sliding feet, unnatural morphing, flicker, sudden cut). Runway explicitly does not support negative prompts and warns it can backfire. Sora and Veo don't foreground negative prompts as a lever at all. Never offer this upgrade for a Runway-targeted prompt.
- A one-line "positive locks" closer even for simple shots — cheap to add, catches drift on re-runs.
- If identity/character consistency matters and the platform supports it, suggest the platform's own reference/character-lock mechanism (Sora Characters API, Veo Ingredients-to-Video, Kling Elements 3.0, Runway Gen4 Ref/image-to-video) over prose-only re-description — every major provider has converged on this being more reliable.
- If the user seems unsure whether to go maximally detailed or leave room for the model to improvise, surface that as an explicit choice rather than assuming — this tradeoff is real and documented, most explicitly by Sora's own guidance.
