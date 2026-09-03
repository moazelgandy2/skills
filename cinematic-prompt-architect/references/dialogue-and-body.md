# Dialogue, Body & Facial Micro-Expressions Encyclopedia (FACS & Acoustic Cadence)

This guide provides deep behavioral and anatomical standards for directing human dialogue, genuine facial micro-expressions, authentic laughter/giggles, vocal cadences, and body-language synchrony in AI video generation.

---

## 1. The Root Causes of "Weird & Bad" AI Speech and Acting

Why does AI speech, facial expression, and laughter frequently look uncanny, robotic, or creepy?
1. **Mood Adjectives instead of Muscle Actions**: Writing "he smiles warmly" or "she laughs happily" triggers generic stock footage training data resulting in mannequin grins or gaping unhinged mouth openings.
2. **Missing Involuntary Micro-Expressions (FACS)**: Genuine smiles require the *Orbicularis Oculi* (cheek lift + eye crinkling / crow's feet, AU6) along with *Zygomaticus Major* (lip corner pull, AU12). Without eye involvement, the smile looks like a psychotic mask.
3. **Simultaneous Speech and Laughter**: AI models cannot synthesize speech while laughing simultaneously (it turns into garbled guttural noises). Real humans laugh in distinct rhythmic exhalations *before* or *after* phrases, or chuckle through nasal airflow.
4. **Literate vs Spoken Syntax**: Writing formal, grammatically complete sentences ("I cannot believe that you have done this") forces stiff, un-human cadence. Real human speech consists of contractions, breath pauses, asymmetric phrase fragments, and pitch inflections.
5. **Decoupled Lip-Sync Cadence**: Without specifying breath intakes, glottal stops, and stressed word syllables, the mouth opens and closes like a mechanical puppet independent of the audio waveform.

---

## 2. Anatomical Facial Action Coding System (FACS) Reference

Direct faces using anatomical muscle movements (Action Units) rather than subjective emotion labels:

| Expression / Emotion | Involuntary Muscle Movement (FACS Action Units) | Anatomical Prompt Description |
| :--- | :--- | :--- |
| **Genuine Joy / Duchenne Smile** | AU6 (Cheek Raiser) + AU12 (Lip Corner Puller) | `Eyes slightly narrowed with authentic crow's-feet crinkling at the outer corners, cheeks lifted upward, lip corners pulled diagonally up, teeth naturally parted without jaw tension.` |
| **Sarcastic / Smug Half-Smirk** | Asymmetric AU12 (One-sided Lip Pull) + AU14 (Dimpler) | `Single-sided left lip corner tightens and curls upward slightly into a restrained smirk, left cheek faintly bunching, right side of mouth relaxed and immobile, steady unblinking gaze.` |
| **Nervous / Polite Smile** | AU12 (Mouth Only) + AU20 (Lip Stretcher) | `Mouth corners stretch horizontally wide while the upper face and eyes remain tense and uncrinkled, rapid tight eyelid blink, subtle swallow.` |
| **Subtle Dread / Anxiety** | AU1 (Inner Brow Raise) + AU4 (Brow Lower) + AU20 | `Inner eyebrows pulled upward and drawn slightly together forming faint vertical forehead furrows, lower eyelids tight, nostrils subtly flaring on a sharp nasal breath.` |
| **Suppressed Rage / Cold Anger** | AU4 (Brow Lowerer) + AU7 (Lid Tightener) + AU23 | `Eyebrows drawn hard downward into a furrowed V, lower eyelids tightened, lips pressed into a thin bloodless horizontal line with jaw muscle flexing at the mandible angle.` |
| **Genuine Surprise** | AU1 + AU2 (Full Brow Raise) + AU5 (Upper Lid Raise) + AU26 (Jaw Drop) | `Eyebrows arch high in uniform elevation, upper eyelids retract exposing white above the iris (sclera), jaw falls open naturally into relaxed oval aperture (not a wide scream).` |
| **Grief / Heartbreak** | AU1 (Inner Brow Raise) + AU15 (Lip Corner Depressor) + AU17 | `Inner corners of eyebrows angled sharply upward, chin muscle (mentalis) subtly bunching and trembling, lip corners drooping downward, glistening lower eyelid meniscus.` |

---

## 3. The Laughter & Giggle Anatomy Protocol

Laughter is an acoustic and physical respiration event. Direct it as structured temporal stages:

### The 4 Types of Human Laughter

1. **The Suppressed Chuckle / Snort (Micro-Laughter)**:
   - *Acoustic*: Sharp, muffled exhalation through closed lips or nostrils (`"pfft"` or `"hnngh"`), followed by a brief breath recovery.
   - *Physical*: Shoulders hitch upward 2cm, head drops downward 15 degrees, lips purse together fighting an upward curl, eyes crinkle tight.
   - *Prompt Syntax*: `At 3.2s, subject suppresses an involuntary laugh: lips purse tight fighting a smile as cheeks bunch upward, head dips downward with a single muffled nasal breath snort, shoulders giving a quick rhythmic bounce.`
2. **The Melodic Giggle (High-Register Chuckle)**:
   - *Acoustic*: 3 to 4 short, rhythmic, breathy staccato vocal bursts (e.g. `[giggle: high pitch, rapid decay]`), followed by a bright vocal delivery.
   - *Physical*: Head tilts slightly to one side, hand instinctively touches chest or collarbone, eyes narrow into crescent folds (AU6), mouth opens into a relaxed smile.
   - *Prompt Syntax*: `Subject breaks into a light, natural giggle: head tilts 10 degrees screen-left, eyes crinkle into happy crescents, emitting three quick breathy vocal giggles before speaking with a smiling vocal register.`
3. **The Uncontrolled Belly Laugh (Full Laugh)**:
   - *Acoustic*: Deep diaphragmatic explosive exhalation (`"HA-ha-ha-ha"`), decaying into a breathy wheeze or deep inhalation sigh.
   - *Physical*: Torso rocks backward into chair backrest, jaw drops wide and loose, eyes squint shut, hands open or slap thigh, chest heaves with rapid respiration.
   - *Prompt Syntax*: `At 5.0s, subject erupts into a full belly laugh: head falls back against the chair, eyes crinkled completely shut, torso heaving with four rhythmic diaphragmatic chuckles decaying into an audible breathy sigh.`
4. **The Bitter / Dry Chortle (Sardonic Laugh)**:
   - *Acoustic*: A single, dry, hollow vocalized bark (`"Heh."`), dead-flat pitch, followed by immediate deadpan drop.
   - *Physical*: Lip corners twitch up for 0.3s and instantly drop flat; eyes remain cold, unblinking, and dead-eyed.
   - *Prompt Syntax*: `Subject emits a single dry, sardonic chortle ("Heh") with a sharp breath puff, one lip corner curling for a split second before her face resets to stone-cold stillness.`

---

## 4. Spoken Dialogue Cadence, Phonetics & Line-Craft

Transform text from written prose into natural, speakable dialogue:

### Rule 1: Conversational Syntax & Contractions
- **Ban Formal Un-contracted Grammar**: Never write `"I did not want to see you"` $\rightarrow$ write `"Didn't want to see you."`
- **Use Sentence Fragments**: Real people speak in half-thoughts: `"Three orders. In an hour. Never stops."`
- **Natural Disfluencies (Max One per Beat)**: An authentic restart or hesitation: `"Look, I... I thought we had a deal."` or a small filler `"Um, yeah."`

### Rule 2: The Pitch Arc & Operative Stressed Words
For every dialogue line, mark:
1. **The Operative Word (CAPS)**: The single word carrying the sentence stress (e.g. `"You knew I WOULDN'T."` vs `"YOU knew I wouldn't."`).
2. **The Pitch Trajectory**:
   - *Inquisitive Rise*: Pitch lifts on final syllables.
   - *Definitive Fall*: Pitch drops down to flat baseline at period, handing off the conversation.
   - *Breath Anchor*: Explicitly place the inhale: `"Sharp breath intake, then fast clipped consonants..."`

### Rule 3: Attributed Tone Labels & Dialogue Format
- **Veo / Kling / Seedance Syntax**: Attribute line in prose with emotional delivery verb and phonetic cue:
  - *Good*: `A woman breathless and agitated gasps, "They change the order three times! It never stops!" with rapid clipped consonants and an audible sharp exhalation.`
- **Sora Syntax**: In the `AUDIO` section, format with actor name, pitch spec, and delivery speed:
  - `Elena (Dialogue, agitated high-mid register, stressed on 'NEVER'): "They change the order three times! It never stops!"`

---

## 5. Body-Language Synchrony & Physical Gestures

A gesture must never float independently of the voice.

### The Synchrony Rules
1. **The Stroke Lands on the Stressed Syllable**:
   - The apex of the hand gesture (open chop, finger point, table slam) must hit its highest velocity on the exact stressed syllable of the dialogue.
2. **The Three-Keyword Body Spec**:
   - For every character: `[Posture + Weight Distribution + ONE Hand Action]`.
   - Example: `"Slouched at 30-degree recline, weight shifted to left hip, right forefinger tapping cigarette body."`
3. **Active Listener Micro-Reactions**:
   - While Character A speaks, Character B's body must not freeze like a wax figure. Direct listener feedback:
     - `Subtle head tilt (5 degrees), chin tuck, slight double blink, weight transfer to rear heel.`
4. **Decoupled Face and Neck Movements**:
   - Head turns precede eye saccades by 0.1s, or eyes glance first before the neck swivels. Robotic actors move head and torso like a single solid block.
