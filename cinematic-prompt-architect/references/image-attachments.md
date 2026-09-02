# Attached Images — Read First, Assign Roles, Never Re-describe

When the user attaches images, the images — not the prose — are the source of truth for what things look like. Text supports the reference; it never replaces it (prompt-only consistency holds ~1 in 3 shots vs ~4 in 5 with a locked reference). This file is the full protocol.

## 0. The upload gate (mandatory — "yes I have some" is not assets)

"I have a logo photo" with nothing attached = no assets. The moment the user claims assets, end the turn with an explicit send-request naming exactly what to upload ("Send them now — upload the logo photo and the face photo here before we continue. I work from pixels, not descriptions or filenames."). If the next reply still contains no images, ask once more and name the files — do NOT drift into engine/camera/technical questions, and do NOT draft anything. Only two exits exist: images received (→ analyze below), or an explicit "no assets, proceed prose-only" waiver (→ continue with a logged drift warning + a reference-mechanism recommendation). Silence about missing uploads is the failure mode this gate exists to kill.

## 1. Read first, deconstruct into layers

Actually LOOK at every attached image before any question or prompt. Never work from filenames, never invent unseen details, never proceed on an image you haven't seen — ask for the upload first. Deconstruct each image into these layers, in this order:

1. **Identity** — face shape, age range, hair (cut/color/volume), eyes, build, expression
2. **Wardrobe** — each garment, colors, materials, accessories, how they sit
3. **Skin** — tone + undertone as visible, texture level (feeds `color-and-skin.md`)
4. **Palette** — 3–5 anchors sampled FROM the image (these become the identical-token anchors)
5. **Lighting** — source, direction, temperature, shadow behavior
6. **Composition** — shot size, angle, subject position in frame, foreground/midground/background
7. **Environment** — location, surfaces, props, depth cues
8. **Text/logos** — transcribe exactly, note position/scale (verify frame-by-frame later; never trust it blindly)
9. **Style/grade** — grain, contrast, color science, photo vs illustrated register

State back the 2–3 most decision-relevant observations in one line ("Reading your still: cobalt bottle center-frame, warm left key, teal tile midground — locking those as anchors") so the user can correct a misread before it propagates.

### Analyze-on-receipt: the 4-pass protocol (run the moment images land, interview pauses)

When images arrive mid-interview, STOP the question flow and analyze before anything else — never "nice, got it" and move on. Four passes, in this order (each pass answers different questions, so don't blend them):

1. **Composition pass** — technique (thirds, symmetry, leading lines, negative space, frame-in-frame), focal point + what draws the eye to it, subject position, foreground/midground/background layers, depth of field, what to keep vs crop out.
2. **Lighting pass** — source direction + quality (soft diffused / hard direct), temperature, shadow behavior, exposure; across multi-refs, flag lighting mismatches immediately (warm golden face + cool fluorescent kitchen = mush — pick a winner).
3. **Color pass** — dominant + accent colors by descriptive name ("deep slate blue with a hint of teal", not "blue"), palette type, mood contribution. These become the identical-token anchors — sample them FROM the image, never from memory.
4. **Materials + details pass** — surface behavior (fabric weave, glass refraction, skin texture level, metal speculars), text/logos transcribed exactly with position/scale, faces (identity, hair, wardrobe), depth/spatial relationships, anomalies to exclude or fix.

Then: report the findings compactly (one line per image + the anchors extracted), assign each image its ONE role, and only then resume the interview where it paused. Analysis is the deliverable of that turn — not a preamble to the next question.

## 2. One image, one job (role assignment)

Every attached image gets exactly ONE role, stated explicitly: first-frame anchor · face/identity ref · wardrobe ref · product/object ref · style/grade ref · composition ref · environment ref · motion/driving ref · audio ref. The prompt then binds each role (`@Image1` inline on Seedance; Elements/Ingredients slots elsewhere) and protects the rest.

**Triple-duty flag:** one photo doing face + outfit + location duty cannot hold all three across shots. Flag it and ask for splits: a face crop (or neutral master: front + 3/4, neutral expression, clean background, even light), a wardrobe shot, and the scene plate. For series work, build the neutral master BEFORE styling — lock design, then style it.

## 3. First-frame discipline (image-to-video)

The image owns composition, subject, lighting, and style — the prompt owns ONLY motion + camera. Kling's own guidance: **15–40 words of pure movement for I2V** (vs 60–100 for text-to-video); over-describing the supplied still creates contradictions the model resolves by drifting. Template: `[shot anchor] + [small visible subject motion] + [one camera move at named speed] + [keep-X-unchanged protect clause] + duration/aspect`. Never re-describe static content; never re-state what the frame already shows.

## 4. Multi-reference fusion rules

- **3–5 focused refs beat 9 random ones.** Each must add new information or it is noise: who (identity) → what it looks like (style) → how it's framed (composition) → where (environment) → what moves (motion ref).
- **Same visual register.** All-photo or all-illustrated; mixing photo faces with illustrated mood boards sends mixed style signals.
- **Lighting must match across refs.** Warm golden face + cool fluorescent kitchen = the model splits the difference into mush. Flag conflicts explicitly and ask which wins (or normalize first).
- **Full subject, clean background.** Waist-up minimum for character refs; products with breathing room; 720p floor (1080p preferred); PNG/JPEG without heavy compression.
- **Faces stay large.** Below ~20% of frame area the model invents a generic face — keep identity beats medium/close, never wide-to-closeup jumps inside one consistency chain.
- **Two characters = two slots.** Dedicated reference + spatial language per actor, or features bleed across them.

## 5. Identity block (verbatim fragment)

Distill identity + wardrobe into one short locked fragment, pasted UNCHANGED at the top of every prompt in the series, scene lines below it. Never rephrase or reorder it — token order matters. One reference image + one frozen identity block is the whole continuity system; document filename + model + seed per shot so reshoots don't start from zero.

## 6. Chain discipline

Single-pass long generations beat chained clips where supported. When chaining: last frame of clip N becomes the start frame of clip N+1; trim unstable head/tail frames; color-match across shots; hide cuts inside motion (see `transitions.md` occlusion). Never swap in a "sharper" new reference mid-series — regenerate the affected shots instead.

## 7. Honesty rails

A reference is guidance, not a copy command — the model interprets, never replicates pixel-perfectly; frame-exact needs go to post compositing. Verify text/logos frame by frame. Real faces need the platform's consented mechanism (never promise unconsented likeness). Consent + provenance note goes in the run header when identity refs are used.
