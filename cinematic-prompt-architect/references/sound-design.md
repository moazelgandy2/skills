# Sound Design — Principles for Prompts That Sound Real

Bad AI-video audio is almost never a model limit — it is an underspecified layer. Half the perceived production value of a clip lives in sound, and sound actively covers visual artifacts by anchoring the viewer in a believable world. This file turns "add sound" into a design discipline.

## The audio brief (write it first, one line)

Before any audio prompting, state: the audio should make the viewer feel [emotion] and understand [message] through [layers]. If a layer doesn't serve the brief, delete it — restraint is the whole game. One clear line of dialogue + one primary SFX + one ambient bed beats a crowded soundscape every time.

## The four layers and their mix jobs

1. **Dialogue (foreground, ~60% of attention)** — formula: Speaker: [identity]. Line: "[exact words, 4–10 for short clips]". Delivery: [tone, pace, accent]. Timing: [when it starts]. Short lines lip-sync; long speeches desync. Stagger multi-speaker turns ("A says…, then B replies…"), never crosstalk.
2. **SFX + Foley (mid, ~25%)** — every visible action that would make sound needs one, anchored to the exact moment ("bag rustle syncs to the handoff", "brakes squeal as the front wheel stops"). One SFX per beat; Foley (cloth, footsteps by surface, handling) stays subtle — if consciously noticed, it's too loud. Layer compound sounds (thud + crack) rather than single thin hits.
3. **Ambience / room tone (background, ~15%)** — never digital silence: even quiet rooms hum. Location-specific bed (market chatter, HVAC, rain on awning) that CHANGES when the location changes — the ambience cut tells the audience they moved. Keep one descriptor so it never masks dialogue.
4. **Music (use sparingly, post preferred)** — mood/texture words only ("minimal pulse, low under voice"), never a competing melody over dialogue. For brand work the default is: generate clean (dialogue + SFX + bed) and score licensed music in post.

## Sound map per beat

Foreground / midground / background, one cue per layer per beat, written against the timecoded beats: what is heard first, what stays subtle, what must stay silent. Reverb must match the space (tiled room echoes, furnished room doesn't) — mismatched space breaks immersion instantly.

## Negative audio

State what is NOT heard: "no music, only natural diegetic sound", "no extra speech", "bed stays low under the voice". On engines without negative-prompt support this lives as positive phrasing, never a Negative block (see dialects).

## In-generation vs post line

Native audio is the ambient floor and the synced moment, not the final mix. Plan from the start which parts get replaced: beat-perfect music, surgical SFX character, loudness normalization (~−14 to −16 LUFS for web), EQ/de-ess — those are NLE/DAW jobs. Say so in the run notes so a good visual never gets discarded over fixable audio.

## Human voice naturalness (why generated dialogue sounds robotic)

Flat median pitch, metronome pacing, pauses at punctuation instead of breaths, perfect grammar, and zero listener behavior — that combination is the robot tell. Real speech is built from these, and every one of them is promptable:

- **Breath first.** Audible inhalation before long phrases, exhale under laughter, breath placed by sentence length ("natural breath before the line", "laughs on the exhale"). No breath = no body.
- **One disfluency per clip, max.** A single "um… so", restart ("I— I mean"), or filled pause buys more humanity than any adjective — but each one eats lip-sync budget, so exactly one, placed at a turn exchange, never mid-word.
- **Pitch arc + stress, not adjectives.** Questions rise across the phrase; statements fall to yield the turn; stress lands on content words ("TEN thousand", not "ten THOU-sand"). Write the arc ("voice lifts through the question, lands flat on the number"), not just "emotional".
- **Turn-taking like humans.** ~200ms gaps, staggered turns, listener backchannels DURING speech (laugh-through-nose, soft "mhm", head nod) rather than silence. Never overlap voices in-generation — overlap breaks lip-sync on every engine; stage interruptions as staggered beats or dub in post.
- **One emotion per line.** Calm-adjacent baselines (warm, dry, tired) sound more human than big swings; ping-ponging excited→sad→angry in one turn reads unstable. Laughter gets its own beat ([laughter] tag where supported), never folded inside a word.
- **Voice-body coherence.** Delivery must match visible effort — no whispering while sprinting, no calm monologue mid-sob. If the body is extreme, simplify the line or move it to VO.
- **Format for the ear.** Short turns, punctuation as pacing (commas breathe, periods land), line breaks where breaths go. A page-perfect sentence is usually an ear-wrong one.
- **Clean voice refs.** Audio references must be single-speaker, no overlap, no music — the model extracts tone from the ref, garbage in carries over.
- **Dub fallback.** Anything complex (overlaps, interruptions, songs, long speeches) goes to post VO/lip-sync tools; native dialogue is for short, clean, visible-mouth lines. Say so rather than forcing it.

## Review checklist (score the generation)

Dialogue exact and intelligible · lip timing acceptable for shot size · SFX lands on its visual · ambience fits without masking · no stray speech or random sounds · music (if any) supports, never competes · clip still works trimmed · captions can cut cleanly over it. If close-but-off, keep the picture and replace the audio — don't re-roll a good visual for a fixable mix.

## Interview triggers

Always ask when audio matters: is there dialogue (exact words?), what are the 1–2 signature sounds tied to visible actions, and music or no music? If the user says "just add good sound", run the brief + four layers yourself and state the choices.
