# Music & Sound Effects Design — Comprehensive Reference Guide

This reference provides deep, production-grade principles for designing cinematic music, sound effects (SFX), and Foley in AI video generation and cinematic workflows. It bridges the gap between what models generate natively and what professional sound design requires.

---

## 1. Core Architecture: The 4 Audio Layers & Spotting

Never dump sound into a scene as general ambient noise or an all-over score. Audio must be spotted against the visual timeline in distinct, structured layers.

### Layer 1: Spoken Dialogue & Vocalizations (Foreground, ~60% Mix Focus)
- **Vocal Delivery & Line Construction**:
  - Direct with transitive action verbs ("to soothe", "to needle", "to dismiss") rather than emotional adjectives ("angrily").
  - Spoken lines must pass the read-aloud test (short, 4–10 words per beat, contraction-heavy).
  - Explicit breath points: an audible inhale before speech, exhale on a laugh or trailing thought.
  - Exactly one operative stressed word per beat to guide pitch contour and lip cadence.
- **Physical Effort & Mic Distance**:
  - Intimate whispering requires tight proximity effect and room reflection damping.
  - Shouting requires acoustic throw, natural slapback echo, and diaphragm strain.

### Layer 2: Hard SFX & Diegetic Interactions (Midground, ~25% Mix Focus)
- **Frame-Anchored Sync**: Every visible physical movement or collision must have an explicit sonic anchor.
- **The Envelope Rule: Transient, Body, Tail**:
  - **Transient / Attack**: The initial high-frequency, high-amplitude burst of impact (0–30ms). Defines punch, snap, crispness, and clarity (e.g., shoe sole heel strike, metal latch click, knuckles meeting wood).
  - **Body / Resonance**: The fundamental frequencies and resonant acoustic mass (30–300ms). Supplies weight, thickness, and perceived physical density (e.g., hollow wooden deck, heavy wet earth, dense linen thud).
  - **Tail / Decay / Acoustic Ring**: The acoustic dispersion, release, and reverberant decay into the surrounding room or environment (300ms–2s+). Connects the object to the physics of the space.

### Layer 3: Environmental Ambience & Room Tone (Background, ~15% Mix Focus)
- **Never Pure Digital Silence**: Real environments constantly breathe. Even dead-quiet rooms have a characteristic frequency profile (air-conditioning hum, floor creaks, pipe resonance).
- **Acoustic Dimension & Depth**:
  - Foreground details: Light localized air currents, nearby foliage rustle.
  - Midground details: Neighborhood traffic, gentle surf, bird calls across a meadow.
  - Deep background: Low atmospheric rumble, distant wind shear, horizon drone.
- **Spatial Consistency**: Room tone must shift instantly when the camera moves from exterior to interior, establishing location changes before the eye even finishes processing the cut.

### Layer 4: Music & Score (Mood, Tension, and Subtext)
- **Spotting Discipline**: Music must be scored with explicit in-points, cue shifts, and out-points. Wall-to-wall continuous music washes out drama and flags amateur production.
- **Dynamic Contrast & The Drop**:
  - Dropping the music to dead silence right before an important line or reveal hits 10x harder than a musical crescendo sting.
  - Build tension through rising rhythmic density or low-end filtering, then pull the rug out for the key line.
- **Native vs. Post Rule**:
  - Native models handle tonal beds, sub-bass drones, and atmospheric textures well.
  - Complex rhythmic beats, licensed scores, and beat-synced drops belong in post-production.

---

## 2. Deep Sound Effects Design: Foley, Textures, and Dynamics

### Foley Artistry: Materials, Weight, and Contact
Foley is the tactile soul of the physical world. In AI prompts, grounding objects with specific material interactions eliminates the uncanny, weightless feel of synthetic video.

1. **Footwear & Surfaces**:
   - Never just "steps". Specify the sole material and substrate:
     - *Hard leather brogues on wet polished marble* (sharp high transient, short bright slap, zero cushion).
     - *Worn rubber skate shoes on cracked asphalt with loose grit* (granular scrape transient, muted hollow thud).
     - *Bare feet on damp lawn grass* (soft organic squash, subtle soil suction, muffled low-mid body).
2. **Cloth & Wardrobe Rustle**:
   - Fabric movement communicates posture, weight shifts, and emotional tension.
   - *Oversized heavy cotton loungewear*: Soft, muffled, dry friction against itself.
   - *Crisp starched linen*: Granular, papery scratch with dry, airy flutter in a breeze.
   - *Waxed canvas / Heavy nylon*: Low-frequency friction squeak and taut tension snaps when stretching across chair frames.
3. **Prop Handling & Micro-SFX**:
   - Jewelry: Metallic clinks, chain links sliding over collarbone skin and fabric.
   - Cigarette & Flame: The dry paper pull, soft butane hiss, crisp wheel strike, delicate micro-crackle of tobacco burning on an inhale.
   - Drinkware: Ceramic mug scraping across raw timber, cold glass sweating and sticking slightly to a tabletop.

### Whoosh & Swish Physics: The BPT Architecture
Camera transitions, rapid arm swings, and whip pans require motivated air displacement:

- **BPT Structure (Buildup, Peak, Tail)**:
  - **Buildup (0.0s – 0.3s)**: Rising filtered white/pink noise, pitch sliding upward, simulating air compression as the camera accelerates.
  - **Peak (At Blur Apex)**: Maximum velocity saturation. Low-end weight combined with tearing high frequencies as the frame smears completely.
  - **Tail / Deceleration (0.1s – 0.3s post-landing)**: Reverb bloom, trailing air vortex dissipating, settling into the new scene's ambient floor.
- **Mass & Velocity Matching**:
  - *Fast body whip pan*: Deep, chest-thumping low-mid air tear with broad stereo pan across the horizon.
  - *Subtle head turn*: Micro air swish, almost entirely high-frequency breath and hair brush.
  - *Hard crash zoom*: Piercing snap transient with sharp vacuum pull.

### Spatial Acoustics & Reverb Matching
Reverb communicates the physical boundaries of the world:
- **Tiled bathroom / Concrete underpass**: High flutter echo, long ringing decay, early reflections that hollow out dialogue.
- **Open field / Grassy lawn**: Complete lack of wall reflections; sound drops off sharply with distance (\(1/r^2\)); wind shear across the microphone capsule; warm ground bounce.
- **Furnished domestic room**: Heavy high-frequency absorption from rugs, sofas, and curtains; dry, intimate, boxy acoustic profile.

---

## 3. Music Scoring & Composition Framework

### Cue Functions (Every Cue Must Have One Named Job)
1. **The Tension Bed (Harmonic Drone / Sub-Bass)**:
   - Low-frequency pedal tone (30–60Hz) creating subconscious anxiety or grounding the scene.
   - Sparse organic textures (bowed cello, glass harmonica, tape-saturated Rhodes piano chords) that stay below 250Hz and above 3kHz to leave dialogue space open in the 1kHz–2.5kHz sweet spot.
2. **The Pacing Motor (Rhythmic Undercurrent)**:
   - Muted analog ticking, damp pizzicato strings, or subtle polyrhythmic percussion.
   - Drives narrative velocity forward without shouting.
3. **The Transition Cover / Swell**:
   - Cymbal scrape, reverse piano chord, or rising synth swell leading directly into a cut, whip, or reveal.
4. **The Sonic Brand Signature (Brand Mnemonic / Sting)**:
   - 2–4 note harmonic resolution or sound mark (e.g., custom acoustic chime + low sub drop) placed deliberately at the final card.

### Dynamic Range & Frequency Carving
- **Dialogue Space**: Never allow melodic instruments (lead synth, guitar, aggressive brass) to sit in the 1kHz to 3kHz zone while a character is speaking.
- **Loudness Standards (Reference Delivery)**:
  - Web & Social Video: Target −14 to −16 LUFS integrated, −1.0 dBFS True Peak.
  - Cinematic / Theatrical: Target −24 LUFS integrated, wide dynamic headroom for explosive peaks.

---

## 4. Prompting Template for Sound & Music

When constructing full production briefs, structure the audio section with concrete sonic tokens:

```markdown
### AUDIO & SOUND DESIGN
- **Audio Brief**: [One line capturing emotional goal, listener perspective, and primary mix focus].
- **Dialogue**:
  - [Character Name]: "[Exact words spoken]"
  - Delivery: [Vocal register, mic distance, pacing, breath cue, operative stressed word].
- **Hard SFX & Foley (Transient / Body / Tail)**:
  - [Timecode / Action]: [Attack transient description] + [Resonant body texture] + [Decay/Reverb tail].
  - [Foley Interaction]: [Specific fabric/surface contact details].
- **Ambience & Acoustic Environment**:
  - Foreground: [Immediate air, local breeze, clothing rustle].
  - Background / Bed: [Location tone, distant fauna, HVAC, traffic drone; zero wall reflections / dry open air].
- **Music & Score Direction**:
  - Entry point & Cue Function: [Where score starts and what narrative job it performs].
  - Palette & Instrumentation: [Specific instruments, BPM range, frequency profile].
  - Dynamic Arc & The Drop: [Explicit point where music attenuates or cuts to silence for dialogue impact].
- **Negative Audio**: [Explicit exclusion of unwanted sounds: no cheesy synth pads, no royalty-free ukulele, no background chatter, no digital clipping].
```
