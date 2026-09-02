# Color & Skin — Locking What Drifts Most

Color play and skin-tone shift are the two most common "something feels off" complaints about AI video — and both are prompt failures before they are model failures. This file gives the exact mechanics.

## Color lock

**Name 3–5 anchors, then never rename them.** Pick specific color tokens ("emerald-green glass", "matte cream label", "warm terracotta", "travertine stone") and repeat the EXACT same strings in the prompt paragraph, every beat, and the locks list. Three variants of the same anchor ("emerald bottle" / "green glass" / "rich emerald tones") read as three different instructions — this single habit causes most reported color drift. Order cues palette → lighting → camera, 2–4 core cues total.

**One grade anchor, not a mood pile.** State the grade once in colorist vocabulary: "warm editorial grade, muted restraint, lifted blacks, light 35mm grain" beats "beautiful warm dreamy cinematic golden tones" — competing adjectives pull the grade in different directions every re-roll. Restrained, natural palettes (muted tones, earthy range, soft highlights) read photographic; hyper-saturated language reads rendered.

**Grain unifies the grade.** A light film-grain line across the whole frame (not just skin) blends regions the model renders separately and hides micro color-stepping. Always include it on photoreal work.

**Reference beats prose for exact colors.** Whenever brand/exact colors matter, recommend the platform lock (Kling Elements, Sora Characters, Veo Ingredients, Seedance `@` refs, Runway Gen4 Ref / first-frame still) over prose — prose holds a palette family, only a reference holds an exact hex. For multi-shot work, pin one seed/grade still and generate every clip from it.

**If colors still drift:** tighten the palette → lighting → camera trio (fewer cues, identical tokens), lock style via reference frames, and plan the final grade pass in post rather than burning re-rolls — plus the Step 6 strip-back applies to color too.

## Skin

**Every face gets tone + undertone + texture, in identical tokens.** Format: `[tone] skin with [undertone] undertone` — e.g. "deep brown skin with warm undertone", "fair skin with cool undertone and freckles". Undertones (warm / cool / neutral / olive, plus zone notes like "warm cheeks, slight redness at nose") are what stop two faces averaging into each other and stop grades from pushing skin orange or grey. Repeat the full string identically everywhere; add a no-averaging lock on multi-face shots ("both skin tones stay distinct, no averaging or drift").

**Texture is four terms, not one.** `visible pores` + `natural uneven tone` + `soft subsurface scattering glow` + `fine lines / light blemishes` — pores alone still render waxy. Never write "flawless", "perfect complexion", or "beauty lighting" anywhere: those tokens actively trigger the retouched-photo prior. Documentary/editorial style anchors ("raw, unretouched, street-casting feel") pull the same direction.

**Light the face to reveal texture.** Directional side/raking light across the skin ("warm side sunlight rakes across real skin texture") shows pores; flat frontal light hides them and invites the plastic look. Tie the light to the skin explicitly in one clause — don't describe lighting and skin in separate sentences that never meet.

**Kling negatives for skin** (supported — always include on close-ups): `smooth skin, plastic skin, waxy, airbrushed` at minimum; add `beauty filter, porcelain skin, doll, 3d render` when the brief is beauty-adjacent. Positive texture + negative smoothing push from both sides at once.

**Consistency across shots:** identical skin strings + same reference face + same light direction every shot. Skin is an anchor element like wardrobe — it goes in the cross-shot locks, not just the first description.
