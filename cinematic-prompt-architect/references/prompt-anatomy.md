# Prompt Anatomy — 10 Constraint Categories

For each category: why it matters, and questions to ask (pick 2-4 per category, don't ask all of them — infer what's already answered from context and only ask what's missing).

## 1. Subject & identity lock

Why: without a locked reference, models drift or "average" facial/wardrobe traits across a shot, especially across a cut or camera move. Splitting identity (face/hair) from scene appearance (wardrobe/props) from fine detail (eye color, tattoos, scars) into separate reference points prevents this averaging.

Ask:

- Who/what is the subject? (person, product, creature, object)
- Any reference images? If multiple people/products, are refs separate per subject?
- What must never change about them mid-clip — face, exact wardrobe color, logo, a specific prop?
- If no image reference exists, get a tight physical description (hair, build, skin tone, distinguishing features) — the more concrete, the less the model improvises.
- With references: freeze one verbatim identity block reused across every shot (never rephrase); add wardrobe as a separate ref + verbatim line, not prose improvisation (`references/image-attachments.md`).

## 2. Scene & spatial blocking

Why: models default to a flat, undirected space unless depth and distance are specified. A "dead" static first frame (arms at sides, neutral pose) reads as obviously AI-generated; describing the first frame as already mid-action avoids this.

Ask:

- What's in foreground / midground / background?
- Where is the camera relative to the subject (distance, height, angle)?
- What's the subject doing in the very first frame — already in motion, or held pose?
- Time of day / season / weather if it affects light and mood.

## 3. Timing & shot structure

Why: unstructured prompts produce one continuous unplanned action; naming beats with rough timecodes gives the model checkpoints to hit, especially for shots with more than one moment (a cut, a whip pan, a reveal).

Ask:

- How many distinct beats/moments happen in this clip?
- Roughly how long is each (as a fraction of total length, since exact seconds vary by engine)?
- Any hard transition (whip pan, cut, hard push-in) or is it one continuous move?
- What's the very last frame/beat — where does it land?
- For EVERY join between beats: which NAMED mechanism (`references/transitions.md` — match on action, graphic match, whip pair, morph with shared anchor, occlusion hide, sound bridge)? What is shared across it (anchor position/scale, direction, speed, light, grade), and which half is generated vs done in post? Never accept "smooth transition" — always force the mechanism + the shared anchor.

## 4. Camera behavior

Why: default AI camera motion is often too smooth/mechanical, which reads as artificial. Deciding intentionally whether the camera should feel human (handheld, imperfect) or engineered (gimbal, drone, locked) is a stylistic choice, not a default.

Ask:

- Handheld/imperfect, or smooth/locked/drone?
- Any specific camera move (push-in, pull-out, pan, whip pan, tracking, orbit)?
- If there's a fast move (whip pan, snap zoom), should motion blur be described explicitly?
- Lens character — wide/observational vs. tight/compressed portrait feel?

## 5. Performance & subtext (only relevant if there are people/characters)

Why: labeling an emotion ("she's annoyed") produces generic, illustrative acting. Giving a want and an obstacle, plus one specific beat change, produces a performance with an arc instead of a static expression held for the whole clip.

Ask:

- What does this character want in this moment?
- What's stopping them from getting it directly?
- Is there one specific turn/beat where something shifts (tone, posture, expression)?
- Any physical tic or unconscious gesture that should NOT be tied literally to a specific word (avoids over-literal gesture-to-word AI tells)?
- For spoken lines: breath placement, ONE disfluency max, pitch arc + stressed words, staggered turns with listener backchannels, one emotion per line, voice matching visible effort (`references/sound-design.md` naturalness section) — never overlapping voices in-generation.

## 6. Physics & materials

Why: naming the specific materials in frame (fabric type, hair, liquid, smoke, loose objects) and giving each a one-line behavior note prevents generic/floaty physics, which is one of the most common "AI look" tells.

Ask:

- What materials are visibly moving (clothing type, hair, liquid, smoke, hanging objects)?
- Is there wind/breeze, or still air?
- Anything that needs to visibly react to contact (fabric creasing under weight, grass bending, liquid rippling)?
- For smoke/fog/steam (plastic-looking when vague): name source + scale (candle wisp vs bonfire plume) + starting volume + temporal change (thinning direction, reveal target) + wind keyword (drifting, shredding, lingering) + light interaction (backlit edges, volumetric shafts) — cinematic adjectives only, NEVER technical physics terms ("turbulence", "vortices", "fluid dynamics" render as jittery static). Soft low-detail smoke refs for big motion; 3-variation reroll expectation.

## 7. Lighting

Why: vague lighting ("nice lighting") produces flat, generic output. Specifying source direction, color temperature, and how light interacts with a specific problem area (shadowed eyes, backlit hair, reflective surfaces) solves the actual visual issue instead of leaving it to a default.

Ask:

- Time of day / light source (sun, window, practical lamp, neon, overcast)?
- Direction relative to subject (key from left/right/front/back)?
- Warm or cool color temperature, and how strong/soft are shadows?
- Any specific problem to solve (e.g. face partly in shadow but must stay readable)?
- Exact brand/product color tokens (names, not "brand colors") — these become identical repeated anchors (`references/color-and-skin.md`).
- For faces: does the light rake across the skin to reveal texture, or flatten it? Tie light to skin explicitly.

## 8. Audio

Why: many engines now generate native audio; unspecified audio defaults to silence or generic ambience. Dialogue needs a voice performance spec separate from the words (accent, register, pacing, emotional coloring) or it defaults to a flat TTS-like read.

Ask (skip entirely if target engine is silent-video-only):

- Any dialogue? If so, exact words plus a voice description (age, accent, register, pacing, emotional tone).
- Ambient sound / SFX tied to visible actions (footsteps, fabric, wind, objects)?
- Music or no music?

Then build the full sound design per `references/sound-design.md`: one-line audio brief first, four layers with mix jobs, a sound map against the beats, negative audio. Never "add good sound" — always brief + map it.

## 9. Style & realism

Why: "photoreal" alone often still produces waxy skin, over-smooth textures, and generic color grading. Naming texture specifics (pore detail, fabric weave, grain) and a concrete grade/look fights this.

Ask:

- Photoreal, stylized, animated, or a specific film/photo reference look?
- If photoreal: any texture details worth calling out (skin, fabric)?
- Color grade — warm/cool/neutral, film grain or clean digital?
- Aspect ratio / resolution if they care.
- Grade anchor in colorist terms + unifying grain (`references/color-and-skin.md`); skin spec per face (tone + undertone + texture) when people are visible.

## 10. Positive locks / non-negotiables

Why: long prompts can bury critical constraints in prose; a short final checklist re-states the things that must not drift, giving the model (and the user, on review) an unambiguous checklist independent of the narrative description.

Ask (usually inferable from earlier answers — confirm rather than re-ask from scratch):

- What are the 3-6 things that must be identical from first frame to last (identity, exact colors, a held prop, a lit/unlit state)?
- Anything that must happen exactly once and not repeat or loop oddly?

---

## Global constraints (apply to every prompt, not a category)

- **Density band**: Veo 100–150 words, Kling 60–100, Runway 40–75, Sora ultra-brief or short-open, Seedance 5 slots + timestamp headers. Cut adjectives before constraints.
- **Aspect ratio**: ask when social/vertical is plausible. Veo is strongest at 9:16; most others default 16:9. Record the choice in the run header.
- **On-screen text**: only promise legible text for Seedance; everywhere else it's a post overlay.
- **Negative prompting**: Kling-only block (3–10 concrete defect terms). Everywhere else, positive phrasing only.
- **Identity across shots**: prose re-description loses to reference images on every engine — recommend the platform's lock mechanism (Sora Characters, Veo Ingredients, Kling Elements, Seedance `@` refs, Runway Gen4 Ref) whenever consistency matters.
