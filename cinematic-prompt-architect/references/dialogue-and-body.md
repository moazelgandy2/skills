# Dialogue & Body — How Humans Speak, Interact, and Move

Robotic delivery and mannequin bodies share one root cause: the prompt directed words and poses as separate decorations instead of one coupled human system. Speech, gesture, face, and posture are temporally locked in real humans — this file makes them locked in the prompt. (Companions: `sound-design.md` for the audio layer, `gaze-and-space.md` for eyelines, `prompt-anatomy.md` category 5 for the interview questions.)

## PART 1 — DIALOGUE: WRITE IT SPEAKABLE, DIRECT IT PLAYABLE

### 1. Line-craft (fix the words first — no delivery saves an un-speakable line)

- **Read-aloud test.** If awkward to say, rewrite. This single test catches 80% of robotic lines.
- **Contractions always, fragments over sentences.** "You need one" beats "you are in need of one"; interruptions and trail-offs welcome. Full grammatical sentences read as writing, not speech.
- **Kill on-the-nose exposition.** Never state the feeling or the plot ("Already solved three refunds while you asked" → "Handled. Three refunds. While you asked."). Suggest, don't tell; let contradiction between line and body carry subtext.
- **One line, one job, 4–10 words for AI.** Fragmentation is a feature: short lines lip-sync and leave room for breath and reaction. Long speeches get trimmed + split (Part 2 / post VO).
- **Distinct voice per character.** Vocab, rhythm, quirks, contractions-vs-precision — cover the names and the lines should still be attributable.
- **Flag every rewrite.** Show original vs rewritten so the user approves the new words.

### 2. Voice direction (action verbs, not adjectives)

- **One transitive action verb per line**, aimed at the scene partner: "to needle her", "to dismiss him", "to corner him". Same words on different verbs = different scenes. Never direct with emotion adjectives ("angrily", "sadly") — swap for what the character DOES with the feeling.
- **Emphasis map: one operative word per line.** Mark the stressed word ("stress on SUGAR"); shifting it shifts the subtext. Pitch arc rides it: questions lift across the phrase, statements fall flat to yield the turn.
- **One emotion per line.** Calm-adjacent baselines over ping-pong; laughter gets its own beat, never folded inside a word.
- **Breath + one disfluency max.** Inhale before phrases, exhale under laughter; a single "um… so" / restart / trail-off at a turn exchange. Each costs lip-sync budget — exactly one.
- **Stagger turns, backchannel the listener.** 200ms gaps, "mhm"/nod/laugh-through-nose DURING speech. Never overlap voices in-generation (breaks lip-sync everywhere) — stage cut-offs as staggered beats, dub true overlap in post.
- **Voice-body coherence.** Delivery matches visible effort; clean single-speaker voice refs; complex overlap/songs → post VO.

## PART 2 — BODY: POSTURE, GESTURE, FACE AS ONE SYSTEM

### 3. The Three-Keyword spec (per character, per clip)

`posture + weight + ONE hand action` — e.g. "erect, forward-planted, grips folder" vs "rounded, sunk, knots fingers". Max one upper-body + one lower-body action per 4–6s clip; more invites limb disconnection. Directional verbs over emotional adjectives ("listlessly drags feet", not "sad man"). Anatomical anchors (correct anatomy, limb separation, balanced weight) + negatives on risky motion. Reroll acting notes by changing the ADVERB, keeping the posture.

### 4. Gesture–speech synchrony (the science that kills the robot feel)

- **Stroke lands ON the stressed word.** The gesture's peak (fastest point) coincides with the pitch peak — hand hits apex exactly as the stressed syllable lands ("TEN [jab] thousand"). Beat gestures on emphasis; pointing/iconic strokes start just BEFORE their word, never after it.
- **Gestures tie to BEATS, never mime single words.** One intentional gesture per beat; sparse beats word-literal mime, which reads AI instantly.
- **Reaction bodies stay visible.** Posture shifts, nods, weight transfers on turns; the listener's body answers even when silent. No frozen bystanders mid-conversation.

### 5. Status, space, and face

- **Status physicality:** lean-in = connection, step-back = detachment; open vs closed; high vs low; stillness vs fidget. Towering close-high vs low-far reads hierarchy without a word. Proxemics shift with the beat (approach to pressure, withdraw to yield).
- **Face in clusters, not isolation:** brow + eyes + mouth read together; micro-leaks (half-second flicker before the mask) beat held expressions; listener micro-reactions (eyebrow flash, nostril flare with intensity) sell the line harder than the speaker's mouth.
- **Contradiction = subtext made visible:** "I'm fine" + averted gaze + fidget. Direct the mismatch deliberately — say what the face does that the words deny.

## DELIVERY CHECKLIST (run before finalizing any performance beat)

- [ ] Every line passes read-aloud; rewrites flagged
- [ ] Each line has one transitive action verb + one operative stressed word
- [ ] Breath placed; max one disfluency; staggered turns; no overlap
- [ ] Each visible character has posture + weight + one hand action
- [ ] Gesture peaks land on stressed words; gestures tied to beats
- [ ] Reaction bodies visible; status/proxemics mapped; gaze vectors set (see gaze-and-space.md)
- [ ] Face read as cluster incl. one micro-leak or listener reaction where it counts
- [ ] Reroll plan names the adverb to change, posture held fixed
