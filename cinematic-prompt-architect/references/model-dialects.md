# Model Dialects (deep reference)

Grounded in official provider docs (OpenAI Cookbook, Google Cloud Blog/DeepMind, Runway Help Center) plus cross-checked community consensus (Reddit, Discord, practitioner guides) as of the research date. Platforms iterate fast — treat specifics (exact char limits, exact clip lengths) as "true as of this research," and note to the user that it's worth a quick doc-check for anything mission-critical. Use this file to reason from, not to quote verbatim into a prompt.

---

## Sora 2 / Sora 2 Pro (OpenAI)

**Container parameters are NOT promptable** — resolution, duration (seconds: 4/8/12/16/20), and character references are set in the API call itself, not in prose. Telling the model "make it longer" in text does nothing; this must be surfaced to the user as a note if they're API-integrating, not just prompting through a UI.

**Prompt-length philosophy — this is the single most important Sora-specific insight**: OpenAI's own guide states shorter prompts give the model more creative freedom and produce surprising/varied results, while longer, more detailed prompts restrict creativity — the model tries to follow guidance but may not always do so reliably. This is a real tradeoff to surface to the user explicitly: ask whether they want _control_ (detailed, ultra-specific prompt, professional-production-brief style) or _creative surprise_ (short, open prompt, let the model improvise details like time of day, wardrobe, camera angles).

**"Ultra-detailed" mode exists and is officially sanctioned** — for complex cinematic shots, OpenAI's guide shows going far beyond a simple structure into full production-brief format: Format & Look (duration, shutter angle, capture emulation, grain, halation), Lenses & Filtration, Grade/Palette (broken into highlights/mids/blacks), Lighting & Atmosphere (named sources with clock-time and bounce/negative-fill setups), Location & Framing (foreground/midground/background, explicit "avoid X" exclusions), Wardrobe/Props/Extras, Sound (diegetic-only calls, LUFS levels for background elements), a timecoded shot list with camera focal length and _purpose_ stated per shot, Camera Notes (why the shot reads the way it does), and Finishing notes (grain overlay, LUT, poster-frame description). This maps almost exactly onto the reference shot this skill was originally built from — Sora is the dialect best suited to ultra-detailed, timecoded, physically-grounded briefs like that one.

**Motion/timing rule**: each shot should have one clear camera move and one clear subject action, described in beats or counts. "Actor walks across the room" is weak; "Actor takes four steps to the window, pauses, and pulls the curtain in the final second" is strong — concrete, countable beats outperform vague verbs.

**Lighting/palette rule**: name 3-5 specific color anchors (e.g. "amber, cream, walnut brown") rather than vague mood words — this is what keeps a multi-shot sequence visually consistent when cut together.

**Style sets everything else**: naming a style early ("1970s film," "16mm black-and-white," "epic IMAX-scale") frames how the model interprets every other instruction that follows — establish it first, then layer specifics.

**Dialogue**: goes in its own labeled `Dialogue:` block below the prose description, not folded into narrative sentences — this helps the model separate visual description from spoken lines. Keep exchanges short enough to fit the clip (a 4s shot roughly one short line; 8s roughly a couple of lines); long speeches desync from pacing. Label speakers consistently across multi-character scenes.

**Character consistency**: Sora's Characters API lets a short reference clip (2-4s) become a reusable character ID, reused across generations — more reliable than re-describing appearance in prose each time, and the officially recommended approach when identity lock matters. Max 2 characters per generation.

**Image input**: an input image anchors the first frame (composition, subject, lighting, style); the text prompt then only needs to describe what happens next, not re-describe what's already in the image.

**Editing philosophy**: treat video edits as one controlled change at a time ("same shot, switch to 85mm" / "same lighting, new palette: teal, sand, rust") rather than a full re-roll — pin a close result as a reference and describe only the delta.

**Iteration expectation**: identical prompts produce different results each time by design — this is stated as a feature, not a bug, so multiple generations of the same prompt is a normal, expected workflow, not a sign something's broken.

---

## Veo 3 / Veo 3.1 (Google DeepMind / Google Cloud)

**Native audio is the defining feature** — dialogue, precisely timed sound effects, and ambient noise are all generated natively alongside the video, guided entirely by the prompt. This is present across Veo's advanced features (Ingredients-to-Video, Frames-to-Video) as well as plain text-to-video.

**Official recommended element set**: subject, action, scene/context, camera, visual style, audio, negative prompts — not every element is needed every prompt, but understanding what each does lets you add them intentionally rather than by default.

**Dialogue syntax**: enclose spoken lines in quotation marks and attribute to a speaker directly in prose — e.g. `A woman says, "We have to leave now."` — rather than a separate labeled block (this differs from Sora's separate-block convention). Keep lines short enough to say naturally in one breath given the clip length (roughly 8s clips fit one short line comfortably).

**Audio direction**: use separate sentences for sound effects, ambience, and dialogue rather than folding them together — e.g. describe the dialogue line, then a separate sentence for ambient sound, then a separate sentence for any specific SFX cue.

**Camera choreography**: Veo 3.1 handles complex, continuous camera moves well — e.g. a described 180-degree arc shot that transitions from one framing to another over the course of the clip. Precise camera language (framing terms, lens/focus terms) is rewarded more than vague mood words.

**Multi-shot dialogue workflow**: for scenes with consistent characters across multiple angles, the officially demonstrated workflow is to first generate reference images of characters/setting (e.g. via an image model), then use "Ingredients to Video" or "First/Last Frame" features to anchor those references before prompting the dialogue and motion in text.

**Clip length**: variable, roughly 4/6/8 seconds — shorter than Sora's ceiling, so dialogue and action beats need to be more compressed and front-loaded.

**Known community risk**: if audio is left undefined, clips can produce mismatched ambience, rushed delivery, or unwanted subtitle-like text artifacts in some UIs — explicitly specifying the audio layer, even briefly, avoids this rather than leaving it to a default.

---

## Kling (3.0 and later, including O1 edit mode)

**Official five-part structure** (this is Kling's own verified structure, distinct from the generic "5 P's" mnemonic circulating in less rigorous guides): Subject, Subject Movement, Scene, Camera Language, Lighting with Atmosphere. For image-to-video specifically, the rule is to describe motion and camera, not the picture — the starting frame already has the visual detail, so the prompt should lead with what moves and how the camera behaves relative to it.

**Director's Mindset**: the single biggest practitioner-community correction is to stop prompting like a photographer (describing a static look) and start prompting like a director of photography — describing how things move through time and space, not just how they look at one instant. Vague mood words ("cinematic movement") map to nothing specific in training data; concrete camera language ("slow dolly-in," "low angle") does.

**Negative prompts are strongly recommended and well-supported** — unlike some competitors. Community and vendor consensus converges on keeping the negative-prompt list short and specific rather than long: guidance ranges from roughly 3-5 terms (to avoid over-constraint / paradoxical effects) up to 10-20 short specific terms depending on source, but all agree the terms should be concrete failure modes, not vague quality words. Common, well-tested negative terms for realistic human video: blurry, distorted face, warped hands, extra fingers, extra limbs, deformed face, sliding feet, unnatural morphing during motion, sudden cut, flicker, low quality, shaky camera, cartoon/anime (if photoreal is the goal), text, watermark. Community reports confirm negative-prompting for "fast movements" and "unnatural movements" measurably improved realism and reduced a CGI-like look in human motion shots.

**Character/scene locking**: "Elements 3.0" lets reference images lock character consistency across a generation — analogous to Sora's Characters API and Veo's Ingredients-to-Video; all three major providers now converge on image-reference-based identity lock being more reliable than prose re-description.

**Native audio and lip-sync**: Kling 3.0 supports assigning dialogue and emotional tone per character with native lip-sync, and natively supports longer single-prompt narratives (community-reported up to roughly 15s) than Veo's ceiling, enabling multi-beat scenes in one generation without stitching.

**Language**: prompting in English yields more reliable adherence to complex cinematic terminology, even though Kling handles Chinese-language prompts natively — worth surfacing if the user is working in a non-English language and cares about precise camera-language adherence over natural-language fluency.

**Kling O1 (edit mode, not from-scratch generation)**: works on existing footage, not a blank generation. Prompts must be surgical — explicit action verbs ("swap," "replace," "add," "remove," "restyle") pointing at exact elements ("swap the blue shirt for a red dress") rather than a full scene re-description. Structure subject-first, then layer motion/camera behavior, then anchor style specifics; community guidance suggests keeping these prompts to roughly 50-150 words for consistent professional output across its four editing modes.

**Prompt length ceiling**: Kling's API caps prompts around 2,500 characters and negative prompts at a separate 2,500 characters — but practitioner consensus is that a tight 60-100 word prompt reliably outperforms one that maxes out the character budget. More text is not more control past a certain density.

---

## Runway (Gen-4 / Gen-4.5, Aleph, Gen4 Ref, Avatar)

**Image-to-video is the primary control mechanism, and the prompt's job shifts almost entirely to motion once an image is provided.** Runway's own guide is explicit: for image-to-video, describe motion and camera work almost exclusively — the input image already conveys subjects, composition, colors, lighting, and style, so re-describing those visual elements in the prompt adds little and can occasionally work against you by competing with what's already visually established. Refer to elements from the image with general language ("the woman," "the car") to isolate them for motion description rather than re-describing their appearance.

**Simplicity beats complexity for a single scene.** Runway's own before/after example is instructive: a single-scene prompt chaining multiple large transformations (character morphs species, forest changes season each leap, camera does a 360, environment swaps entirely) is flagged as the wrong approach; describing one continuous, physically plausible motion for one scene is the right approach. This is a stronger and more explicit warning against overloading a single Runway prompt than most other providers give.

**No negative prompts** — Runway's Gen-4 Image guide explicitly states negative prompting ("no clouds in the sky") is not supported and can produce the opposite of the intended effect if attempted; this differs sharply from Kling. Don't carry Kling-style negative-prompt habits into a Runway-targeted prompt.

**Natural language over conversational phrasing** — Runway's models are described as designed to thrive on visual detail, not conversational natural language; a request phrased as a question ("can you please generate...") is explicitly called out as weaker than a direct visual description ("cinematic photograph of..."). This is a notable contrast with providers like OpenAI, where conversational framing is more tolerated.

**Camera motion vocabulary**: locked, handheld, dolly, pan, tracking-a-subject vs. moving independently through an environment, and shifts in focus are the core vocabulary Runway's own Camera Terms guide recommends drawing from.

**Style descriptors are separable**: broad style/motion-speed descriptors (e.g. "smooth animation," "stop motion," motion speed) can be appended to a prompt when refining results, distinct from the core scene/motion description — useful for iterating tone without rewriting the whole prompt.

**Duration guidance**: roughly 2-10 seconds; prompts describing multiple sequential actions benefit from choosing a longer duration in that range rather than compressing several actions into a short clip.

**Aleph (video-to-video/restyle)** and **Gen4 Ref (reference-image-driven generation)** exist as separate modes for different jobs — restyling existing footage vs. generating fresh footage anchored to reference images — worth distinguishing when the user's task is "take this clip and change X" vs. "generate new footage that looks like this reference."

---

## Cross-model consensus (from official docs plus community convergence)

- **Structured, section-bounded prompts consistently outperform unstructured prose of similar or greater length** — every provider's own docs independently converge on some version of subject, action/motion, camera, lighting, style, audio, even though the exact labels and order differ slightly per platform.
- **Image references for identity lock now beat prose re-description across every major provider** — Sora's Characters API, Veo's Ingredients-to-Video, Kling's Elements 3.0, and Runway's image-to-video/Gen4 Ref all independently arrived at the same solution to the same problem: drift in character identity across a generation.
- **Negative-prompt support is not universal — check before relying on it.** Kling supports and recommends it; Runway explicitly does not support it and warns against attempting it. Sora and Veo's official guides don't foreground negative prompts as a primary lever at all, leaning instead on precise positive description. Don't assume a negative-prompt block will help, or even be interpreted, on every platform.
- **Concrete, countable, physically specific language beats mood words everywhere.** "Four steps to the window, pauses, pulls the curtain in the final second" (Sora); "slow dolly-in, low angle" versus "cinematic movement" (Kling); precise framing/lens terms versus vague cinematic language (Veo, Runway) — this single principle is the most consistently repeated piece of advice across every provider and every community source found.
- **Simplicity per single generation is a recurring warning, not just a stylistic preference.** Sora's own guide notes overly detailed prompts can reduce reliability of adherence; Runway explicitly warns against chaining too many large transformations into one shot. The instinct to cram more detail in is not always correct — sometimes the fix for a misfiring generation is to strip complexity back (freeze camera, simplify action, clear background) and re-add it incrementally, which is Sora's own explicitly recommended debugging approach and generalizes well to other platforms.
- **Prompt-language philosophy differs on the control-versus-creativity axis.** Shorter, more open prompts trade control for creative surprise (most explicit in Sora's docs, but the tension is real everywhere); this is worth surfacing to the user as an explicit choice early in the interview rather than assuming maximal detail is always the goal.
