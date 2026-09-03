# SFX Engineering & Film Scoring Master Guide

This reference provides production-grade principles for designing cinematic sound effects (SFX), tactile Foley, physical air displacement, and film scores in AI video generation and post-production workflows. It bridges the gap between what models generate natively and what Hollywood sound editors and composers execute.

---

## Table of Contents
1. [The 5-Point Component Layering Architecture](#1-the-5-point-component-layering-architecture)
2. [Exhaustive Foley Engineering & Material Contact Matrices](#2-exhaustive-foley-engineering--material-contact-matrices)
3. [Kinematic Audio & Air Displacement (BPT Dynamics)](#3-kinematic-audio--air-displacement-bpt-dynamics)
4. [Film Scoring Paradigms & Compositional Palettes](#4-film-scoring-paradigms--compositional-palettes)
5. [Micro-Music Theory for Sound Designers](#5-micro-music-theory-for-sound-designers)
6. [Dramatic Spotting & Structural Architecture](#6-dramatic-spotting--structural-architecture)
7. [Stem Hierarchy, Frequency Carving & Loudness Standards](#7-stem-hierarchy-frequency-carving--loudness-standards)

---

## 1. The 5-Point Component Layering Architecture

Single-sample sound effects sound flat, synthetic, and weightless. Professional cinematic sound effects are engineered by stacking five distinct acoustic components across the time and frequency spectrum:

```
[0ms] ─── Attack Transient (0–30ms) ───────────► [High-Frequency Snap & Edge]
[15ms] ───── Resonant Body (30–300ms) ─────────► [Acoustic Mass & Material Core]
[20ms] ────── Sub-Bass Weight (20–80Hz) ───────► [Visceral Physical Air Displacement]
[30ms] ─────── Mechanical Sweetener ───────────► [Granular Friction, Debris & Grit]
[100ms] ──────── Acoustic Tail (300ms–3s+) ────► [Environmental RT60 Dispersion]
```

### 1. Attack Transient (0–30ms)
- **Role**: High-frequency, high-velocity spike that pierces the mix and commands immediate neurological attention.
- **Physical Meaning**: Defines material hardness and edge sharpness at the microscopic point of impact (e.g. steel sear click, stiletto tip meeting stone, knuckle striking jawbone).
- **Acoustic Profile**: 2.5 kHz – 8 kHz, zero decay, extreme crest factor.

### 2. Resonant Body (30–300ms)
- **Role**: The fundamental frequency and acoustic resonance of the vibrating mass.
- **Physical Meaning**: Tells the listener the size, volume, and material density of the object (e.g. the hollow pitch of a wooden crate, the low ring of a structural steel I-beam, the dense squelch of wet clay).
- **Acoustic Profile**: 150 Hz – 1.2 kHz, moderate sustain.

### 3. Sub-Bass Weight (20–80Hz)
- **Role**: Visceral, physical low-frequency pressure wave felt in the chest rather than heard in the ear canal.
- **Physical Meaning**: Communicates massive kinetic energy, planetary scale, or psychological dread (e.g. vault door seal locking, explosive shockwave compression, cinematic superhero landing).
- **Acoustic Profile**: 25 Hz – 75 Hz sine/sub-harmonic energy with rapid envelope decay to avoid masking.

### 4. Mechanical Sweetener (High-Frequency Micro-Texture)
- **Role**: Organic or synthetic granular layers that inject tactile personality, grit, and hyper-realism.
- **Physical Meaning**: Micro-debris scattered by the collision (e.g. powdered glass falling, hydraulic oil hiss, dry leather stretching, tobacco burning, brass cartridge case bouncing).
- **Acoustic Profile**: 4 kHz – 16 kHz granular detail.

### 5. Acoustic Tail / Environmental Release (300ms–3s+)
- **Role**: The reverberant bloom, flutter echo, or open-air dissipation that locks the event into its physical space ($RT_{60}$).
- **Physical Meaning**: Eliminates digital cutoff; informs the brain whether the impact occurred inside a dry padded booth or a cavernous stone cathedral.

---

## 2. Exhaustive Foley Engineering & Material Contact Matrices

Foley is the tactile soul of the physical world. Grounding objects with specific material interactions eliminates the weightless, uncanny feel of synthetic video.

### Footwear × Substrate Matrix
Never prompt generic "footsteps". Specify the sole compound, walking cadence, and exact substrate:

| Footwear | Substrate | Sonic Profile & Prompting Tokens |
| :--- | :--- | :--- |
| **Hard Italian leather brogues** | Wet polished marble | Sharp 4kHz transient slap, high specular reflection, zero cushion, damp suction squeak on heel turn. |
| **Worn rubber skate shoes** | Cracked asphalt with loose gravel | Granular gritty scrape, soft rubber damping, hollow 250Hz pavement thud, rolling stone clicks. |
| **Heavy lug-sole combat boots** | Damp forest loam & rotting pine mulch | Muffled organic squash, deep 90Hz spongy soil compression, wet twig fracture, zero slapback. |
| **Bare dry feet** | Sun-baked cracked red clay | Crisp powdery grit crunch, dry epidermal friction, flat acoustic deadness, warm low-mid tap. |
| **Pointed steel stilettos** | Wet diamond-plate steel catwalk | Piercing 6kHz metallic transient ping, hollow structural steel tube ring, immediate open-air dissipation. |
| **Felt-soled slippers** | Antique creaking oak parquet floor | Whispering textile sweep, sudden sharp 800Hz wooden floorboard groan, flexing timber cavity resonance. |
| **Spurred leather cowboy boots** | Weathered saloon pine floorboard | Hard heel thud, loose brass spur ring (jingle-clink sweetener), hollow dry chamber under-deck rumble. |
| **Treated rubber gumboots** | Thick tidal mud (marshland) | Deep vacuum suction squelch, liquid bubble pop on foot extraction, thick viscous slosh. |
| **Cleated athletic shoes** | Damp synthetic turf | Springy plastic-rubber squeak, granular crumb-rubber spray, resilient synthetic rebound. |
| **Stocking / Sock feet** | Polished maple dancefloor | Continuous silky friction hiss, muted heel pulse, delicate static microfiber glide. |
| **Heavy winter mukluks** | Fresh sub-zero powder snow | High-frequency styrofoam squeak, crisp crystal compaction, hyper-dry acoustic absorption. |
| **Cracked work boots** | Broken tempered glass on concrete | Piercing crystalline grinding, sharp brittle crunches, sharp shards skittering across screed. |
| **Espadrilles (rope soles)** | Sun-warmed terracotta roof tiles | Coarse abrasive rasp, dry hollow clay tap, warm acoustic bounce with zero flutter. |
| **Bare wet feet** | Steamy glazed swimming pool tile | High-pitched rubbery friction squeals, wet heel slap, splash droplets landing on standing water. |
| **Tactical assault boots** | Broken drywall & mortar rubble | Powdery chalk puff, chalky masonry crunch, crumbly mineral fracturing under full body weight. |
| **Soft moccasins** | Dry autumn oak leaves on hard earth | Explosive brittle foliage crackle, papery tearing transients, dry earthy undertone. |

### Cloth & Wardrobe Movement Pass ("The Moves")
Clothing friction reveals posture, muscular tension, and emotional anxiety:
- **Raw Heavy Selvedge Denim (16oz)**: Coarse, abrasive scraping between thighs during walking; stiff mechanical creases snapping when sitting.
- **Crisp Starched Cotton Poplin**: Whispering, high-register papery flutter; crisp, dry fabric rustle during rapid upper-body turns.
- **Heavy Waxed Canvas / Barn Jacket**: Dry, groaning friction squeak; stiff, wind-resistant flapping with hollow mid-frequency thuds.
- **Worsted Wool Tailored Suiting**: Soft, muted, muffled microfiber slide; elegant, low-amplitude brush with zero harsh high-frequency noise.
- **Heavy Oiled Motorcycle Leather**: Rich, organic leather groaning and squeaking under joint tension; heavy, dense folds creasing with tactile grain.
- **Silk Charmeuse / Evening Satin**: Liquid-smooth, delicate high-frequency sheen; frictionless whisper accompanying effortless movement.
- **Tactical Ripstop Nylon**: Sharp, synthetic swish-swish cadence with subtle plastic zipper-pull jingling.

### Prop Mechanicals & Tactile Micro-Interactions
- **Firearms & Mechanisms**:
  - Never generic "gunshot". Break down pre-firing mechanics: cold steel slide rack (metal-on-metal oily friction + spring compression + sharp lock click), sear reset (crisp 3.5kHz micro-click), and spent brass casing ejection (ringing brass bouncing on concrete with 3-bounce decay).
- **Antique Lock & Skeleton Key**:
  - Heavy iron key sliding into unlubricated keyway (mineral scraping transient), tumblers lifting (staggered dual brass clicks), heavy iron bolt throwing (deep mechanical clack and door jamb shudder).
- **Vintage Mechanical Camera**:
  - Heavy brass mirror slap (sharp mechanical snap), dual-curtain cloth shutter whirr (1/60s friction zip), spring-loaded gear escapement ticking down.
- **Glassware & Barware**:
  - Heavy crystal tumbler placed on raw mahogany (dry wooden clunk + delicate crystal chime ring at 4.2kHz), dense ice sphere clinking against leaded glass, carbonated effervescence fizzing on an inhale.
- **Cigarette & Lighter**:
  - Butane lighter thumb wheel strike (coarse flint rasp + instant butane hiss + soft flame ignition "woof"), slow drag (intimate dry tobacco crackle on deep inhalation + paper combustion).
- **Fluid Pours**:
  - Hot steaming black coffee into ceramic mug: pitch ascending as fluid column rises, warm aerated froth hiss, liquid boundary lap.

### Biological & Human Bio-Acoustic Foley
- **Pre-Speech Glottal Clicks**: Microscopic separation of the tongue from the soft palate and moist lips unsticking 100ms before phonation.
- **Swallowing Under Extreme Fear**: Audible pharyngeal constriction, dry gulp with audible Adam's apple displacement.
- **Cardiac Pulse (Internal Subjective)**: Muffled 40Hz–60Hz double-thump (lub-dub) with low-pass filtered resonance.
- **Joint / Tendon Friction**: Subtle dry knuckle pop, cervical vertebra click on a slow neck roll, taut tendon snap.

---

## 3. Kinematic Audio & Air Displacement (BPT Dynamics)

Fast camera motion, weapon arcs, and physical speed require motivated air displacement governed by the **BPT (Buildup, Peak, Tail)** envelope:

```
[0.0s – 0.3s] Buildup: Filtered air suction, pitch rising, reverse compression
[Apex Blur]   Peak: Velocity saturation, mid-frequency air tear, low sub-bass displacement
[+0.2s]       Tail: Centrifugal air vortex dissipating, room reverberation bloom
```

### Motion-Specific BPT Applications:
- **Whip Pan (Fast Camera Re-frame)**:
  - *Buildup*: Low-pass filtered pink noise sweeping upward from 200Hz to 2kHz.
  - *Peak*: Loud tearing air displacement across stereo horizon matching camera pan direction.
  - *Tail*: Spatial bloom dissipating into the arrival location's acoustic room tone.
- **Crash Zoom (0.2s Snap Punch-In)**:
  - *Buildup*: High-velocity air suction pull, sudden drop in surrounding ambient level.
  - *Peak*: Piercing vacuum snap transient at frame stop.
  - *Tail*: Heavy sub-bass thud (50Hz) anchoring the subject into close-up framing.
- **Heavy Bladed Weapon Swing**:
  - Sharp high-frequency blade whistle (fluting air over steel bevel) + low-mid air tearing body + sudden dead stop on impact.

---

## 4. Film Scoring Paradigms & Compositional Palettes

Music must possess a clear narrative function and distinctive acoustic signature. Never prompt "epic cinematic music" — specify the orchestration, harmonic tension, and aesthetic school:

### 1. Hybrid Orchestral (The Hans Zimmer Paradigm)
- **Aesthetic**: Colossal scale, seismic weight, relentless forward kinetic drive.
- **Instrumentation**: Low-brass clusters (contrabass trombones, cimbassi, tubas), distorted cello ensembles, massive modular analog synthesizers (Moog sub-oscillators), hybrid taiko/gran cassa percussion, and iconic **BRAAAM** brass-synth hybrid blasts.
- **Application**: Sci-fi epics, psychological thrillers, high-stakes military action.

### 2. Textural / Electroacoustic Minimalism (The Jóhann Jóhannsson / Hildur Guðnadóttir Paradigm)
- **Aesthetic**: Haunting, organic, desolate, emotionally raw and avant-garde.
- **Instrumentation**: Prepared acoustic cello, halldorophone (electro-acoustic resonant cello), vintage tape loops running through degrading reel-to-reels, pump organ drones with audible foot-pedal mechanics, sub-harmonic saturation, and microtonal choir glissandos.
- **Application**: Bleak crime thrillers, alien encounters, psychological trauma (*Arrival*, *Sicario*, *Chernobyl*).

### 3. Industrial Glitch & Dark Ambient (The Trent Reznor & Atticus Ross Paradigm)
- **Aesthetic**: Claustrophobic, abrasive, alienated, neurotically detailed.
- **Instrumentation**: Distorted analog synthesizer pulses, felt-damped upright piano recorded with ultra-close microphones (capturing wood creaks and felt hammer thuds), granular noise beds, polyrhythmic clockwork ticks, and bit-crushed electronic textures.
- **Application**: Modern drama, dystopian tech, corporate espionage, cyber thrillers (*The Social Network*, *Gone Girl*).

### 4. Neoclassical Chamber (The Max Richter / Philip Glass Paradigm)
- **Aesthetic**: Melancholic beauty, repetitive emotional hypnotism, existential intimacy.
- **Instrumentation**: Intimate string quartet (dry, close-mic placement with audible bow rosin), arpeggiated piano motifs, gentle woodwind breathing, and warm analog tape warmth.
- **Application**: Period drama, grief, romantic obsession, poetic arthouse narratives.

### 5. Retrospective Analog / Sci-Fi Synthwave (The Vangelis / Disasterpeace Paradigm)
- **Aesthetic**: Cosmic nostalgia, neon-lit melancholy, shimmering retro-futurism.
- **Instrumentation**: Yamaha CS-80 expressive synth brass, Prophet-5 arpeggios, rich analog chorus, lush Lexicon 224 digital reverb tails, and rolling sub-bass pulses.
- **Application**: Cyberpunk, neo-noir, retro-futuristic mysteries (*Blade Runner*).

### 6. Diegetic Source Music (In-World Audio)
- Source tracks (jukebox, radio, club sound system, neighbor's apartment):
  - Must reflect the **cabin physics** and acoustic transmission: low-pass filtered through closed doors/windows, muddy bass panel vibrations, room flutter, and mono/stereo collapsed imaging.

---

## 5. Micro-Music Theory for Sound Designers

### Pitch Alignment: Tuning SFX to the Score
Unintentional harmonic clashes between sound effects and musical score destroy production value. Professional sound designers tune diegetic sounds to the root, fifth, or octave of the musical key:
- An engine drone idling at 110Hz (A2) harmonizes cleanly with an A-minor musical cue.
- Sirens, industrial hums, and telephone rings should be pitched to complement the cue's tonal center.

### Dissonance & Roughness Intervals
When aiming to evoke psychological terror or biological alarm:
- **Minor Second (1 semitone)** & **Tritone (augmented 4th / diminished 5th)**: Create intense acoustic dissonance.
- **Acoustic Beating / Roughness**: Two pure frequencies spaced 15 Hz – 30 Hz apart generate rapid physical interference beats that stimulate the human amygdala, triggering nausea and immediate panic.

### Rhythmic Tempo-Locking (BPM to Video Framerate)
Locking music tempo to video framerate creates subconscious rhythmic perfection:
- At **24 fps**:
  - **120 BPM** = exactly 2 beats per second (1 beat = 12 frames).
  - **144 BPM** = exactly 2.4 beats per second (1 beat = 10 frames).
  - **96 BPM** = exactly 1.6 beats per second (1 beat = 15 frames).
- Landing visual cuts, whip pans, and punch impacts on these mathematically aligned beat frames maximizes perceptual punch.

### Counterpoint Scoring vs. Mickey-Mousing
- **Mickey-Mousing (Parallel Scoring)**: Music directly mimics every physical motion on screen (e.g. rising strings on standing up, thumps on falling down). Use sparingly outside animation.
- **Counterpoint Scoring**: Music contradicts the emotional tone of the physical action (e.g., a serene, mournful Bach cello suite playing over a violent, slow-motion riot). The stark cognitive dissonance forces the audience into deep emotional introspection.

---

## 6. Dramatic Spotting & Structural Architecture

Every cue must have an explicit dramatic in-point, structural job, and exit:

### Cue Functions
1. **The Tension Bed**: Low-frequency pedal drone (30–60Hz) grounding the scene, leaving the mid-range open for dialogue.
2. **The Pacing Motor**: Damp pizzicato strings, muted clockwork ticks, or subtle polyrhythmic percussion driving narrative urgency without masking speech.
3. **The Transition Swell**: Reverse cymbals, bowed metal scrapes, or rising synth sweeps leading directly into a cut, whip, or visual reveal.
4. **The Sonic Logo / Brand Mnemonic**: A 2–4 note signature sound mark (e.g. acoustic chime + sub drop) concluding a sequence.

### Structural Hit-Points & The Drop
- **The Stinger**: An abrupt full-orchestra or sub-bass hit landing synchronously with a terrifying visual reveal.
- **The Pre-Drop (Silence as a Weapon)**: The score builds into a furious crescendo, and then **cuts to absolute, dead zero-dB silence** 200ms before a gun fires, a punch lands, or a devastating word is spoken. The sudden vacuum makes the following event hit with explosive force.

---

## 7. Stem Hierarchy, Frequency Carving & Loudness Standards

Professional sound design delivers clean separation across five master stems:

```
┌─────────────────────────────────────────────────────────────┐
│ MASTER AUDIO MIX                                            │
├──────────────┬──────────────┬──────────────┬────────────────┤
│ DX (Dialogue)│ FO (Foley)   │ FX (Hard SFX)│ BG (Ambience)  │ MX (Music)
│ Lead Voice   │ Feet, Cloth  │ Impacts, Guns│ Room Tone, Wind│ Score, Drones
└──────────────┴──────────────┴──────────────┴────────────────┘
```

### Frequency Slotting & Spectral Carving
To prevent acoustic masking, assign dedicated frequency lanes:
- **Sub-Bass (20 Hz – 60 Hz)**: Sub drops, seismic booms, kick drum fundamentals, deep drone anchors.
- **Low-Mids (200 Hz – 350 Hz)**: The "mud" zone. Cut music and ambience here by 2–4 dB to preserve vocal warmth and clarity.
- **Vocal Intelligibility Pocket (1 kHz – 3 kHz)**: The sacred human speech zone. Dynamically carve a 3 dB – 6 dB pocket in all music and ambient beds whenever dialogue is active (sidechain ducking).
- **Presence & Sibilance (5 kHz – 8 kHz)**: Consonant bite, transient attack clicks, metal pings.
- **Air & Sheen (10 kHz – 20 kHz)**: Room tone breath, delicate fabric friction, open sky ambience.

### Industry Loudness Compliance Standards
- **Web & Social Delivery (YouTube, TikTok, Reels, Instagram)**:
  - Integrated Loudness: **−14 to −16 LUFS**.
  - True Peak: **−1.0 dBTP**.
  - Dynamic Range: Moderate compression to ensure intelligibility on mobile phone speakers.
- **Cinematic & Theatrical Delivery**:
  - Integrated Loudness: **−24 LUFS**.
  - True Peak: **−2.0 dBTP**.
  - Dynamic Range: Massive dynamic range (+18 to +22 dB crest factor), allowing whispers at −35 LUFS and explosions at −4 LUFS.

