# Transitions — Which, When, and Where They Get Built

Fake-feeling AI transitions come from three errors: a vague "smooth transition" with no named mechanism, a transformation with no shared anchor, and prompting in the editor what belongs in post (or vice versa). This file draws the lines.

## The golden rule: in-generation vs in-edit

**Build in the generation** (needs frame-by-frame motion only the model can render): morphs, whip pans carried across a cut, match cuts (graphic / action / sound), first-to-last-frame interpolation, occlusion hides (foreground wipe, silhouette pass, lens-cover, shadow pass, dark-frame pass).

**Build in the edit, never prompt** (instant and perfect in any NLE): hard cuts, cross-dissolves, fades to/from black, washes. Prompting "then dissolves into…" buys a muddy AI dissolve and a wasted generation — write the two clean clips and dissolve in post.

## The transition menu — which for which job

- **Match on action** (default, most invisible): cut DURING a movement that continues across the cut — door opening, head turn, hand lift. Use whenever staying in one scene; choreograph the action so both halves share it.
- **Graphic match**: same shape/composition across time or place (circle → circle, skyline → skyline). Use for thematic links and time jumps; lock position + scale + framing on both halves or the cut breaks.
- **Sound bridge / J-cut / L-cut**: cheapest invisible glue — next scene's audio starts early (J) or current audio lingers (L). Use on dialogue and documentary flow; plan in the sound map, execute in post.
- **Whip pan**: energy, comedy, frantic travel, big time/space jumps. Must be motivated or it reads as a YouTube preset. Rules: SAME direction + SAME speed both halves, heavy motion blur at peak, cut at the blurriest frame, add a whoosh SFX. Models default to slow pans — override explicitly ("fast whip pan, heavy motion blur at peak").
- **Morph**: one thing becomes another (product transform, pupil → galaxy). Needs a SHARED shape or motion carried through, named explicitly — without it the morph collapses into blur. Veo handles morphs cleanly; keep it a single continuous take, no cut.
- **Occlusion / invisible cut** (1917-style): hide the cut behind a passing foreground object, a whip-blur, or a near-black frame. Use to fake one continuous take across separately generated clips; design the occluder (pillar, passerby, dark doorway) into BOTH halves.
- **Smash cut**: hard contrast for comedy/shock — pure edit, no blend, no prompt needed beyond two strong endpoints.
- **Dissolve / fade**: time passage, memory, contemplation — pure edit, never prompted.

## Pair-writing: transitions come in halves

Whips, match cuts, and occlusions are always written as PAIRS: an OUT half and an IN half sharing direction, speed, anchor position/scale, light, and grade. Generate both, cut on the matched frame (blur peak / action peak / anchor alignment). One half without the other is just a pan.

## Engine fit (2026)

Veo: morphs land cleanly. Pika: first-to-last-frame is purpose-built for defined-end transitions. Kling/Sora: camera-driven whips and match cuts (override slow defaults). Seedance: timestamp headers ARE hard cuts — use them as the edit plan. Runway: reference/first-frame stills keep both halves consistent. Luma: smooth dreamlike interpolation for dissolves you do want generated.

## Failure fixes

Muddy dissolve → you prompted an edit-side transition; re-plan as two clean clips + post blend. Morph collapsed to blur → name the shared anchor. Whip came out slow → say "fast" + "heavy blur at peak" explicitly. Halves don't match → lock position/scale/direction/light across both. Grade jump across the cut → shared palette anchors + reference stills + grade match in post. Cut still visible → switch mechanism to occlusion (pass something dark/close past the lens in both halves) or bridge it with a J-cut.
