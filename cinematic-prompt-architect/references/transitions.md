# Transitions Encyclopedia — Mechanics, When to Use & Technical Execution

Transitions determine temporal rhythm, narrative cohesion, and spatial continuity. In AI video generation, transitions must be explicitly assigned to either **In-Generation Mechanics** (which require physics and optical rendering) or **In-Edit Decisions** (which belong in post-production).

---

## 1. The Core Law: In-Generation vs In-Edit

| Transition Mechanism | Execution Domain | Why | Prompt Handling |
| :--- | :--- | :--- | :--- |
| **Match on Action** | **In-Generation + Edit** | Motion starts in Shot A, finishes in Shot B | Prompt identical vector and speed across both shots |
| **Graphic Match Cut** | **In-Generation + Edit** | Compositional geometry matches across space/time | Prompt identical Cartesian coordinates and scale on both shots |
| **Whip Pan (Swish Pan)** | **In-Generation + Edit** | Rapid directional motion blur bridges the cut | Prompt paired OUT-blur and IN-blur with matched speed/direction |
| **Morph / Transformation** | **In-Generation ONLY** | Continuous physical interpolation of subject matter | Single unbroken take prompt with explicit anchor metamorphosis |
| **Occlusion Hide / Wipe** | **In-Generation + Edit** | Frame blocked by passing foreground object | Prompt full black-out occlusion at tail of A and head of B |
| **Light Leak / Lens Flash** | **In-Generation OR Post** | Solar flare wipes frame into new scene | Prompt high-intensity directional flare blowout |
| **Crash Zoom Transition** | **In-Generation + Edit** | Violent focal burst into subject details | Prompt 0.3s zoom burst with matched entry trajectory |
| **J-Cut / L-Cut** | **Post-Production ONLY** | Audio bridge preceding or trailing video cut | Specify in Audio Brief and Post Notes; never prompt visual fade |
| **Hard Cut / Smash Cut** | **Post-Production ONLY** | Instantaneous frame swap on timeline | Generate two pristine clips; assemble with razor cut in NLE |
| **Cross-Dissolve / Fade** | **Post-Production ONLY** | Opacity blend across timeline | **NEVER prompt "dissolves into"** (causes muddy AI artifacts) |

---

## 2. Complete Transitions Menu & When to Use

### 1. Match on Action (The Invisible Narrative Cut)
- **Concept**: Cutting from one shot to another while the subject is in the middle of a continuous physical motion.
- **When to Use**: Intra-scene continuity, changing angles during combat, entering doorways, sitting down, opening letters.
- **Rules**: The motion in Shot 1 must match the direction, velocity, and limb state in frame 0.0s of Shot 2.
- **Prompt Example**:
  - *Shot 1*: `"At 9.4s, subject initiates forward right-leg kick, foot elevating to 45 degrees as frame terminates."`
  - *Shot 2*: `"First frame at 0.0s catches right foot mid-kick at 45 degrees, continuing full kinetic arc into heavy bag impact."`

### 2. Graphic Match Cut (Thematic & Temporal Link)
- **Concept**: Transitioning between two visually disparate scenes by matching the exact shape, color, or composition of an object.
- **When to Use**: Time skips, memory triggers, thematic metaphors (e.g. spinning roulette wheel cutting into spinning jet turbine; circular eye pupil cutting into lunar eclipse).
- **Rules**: Lock the Cartesian coordinates (X/Y screen percentages) and scale of the matching shape verbatim in both prompts.
- **Prompt Example**:
  - *Shot 1*: `"Subject's round brass pocket watch fills exactly 40% of screen center (X: 50%, Y: 50%), ticking rhythmically."`
  - *Shot 2*: `"Full moon in night sky fills exactly 40% of screen center (X: 50%, Y: 50%), bathed in identical circular luminescence."`

### 3. Whip Pan (Swish / Speed Pan)
- **Concept**: The camera pans with violent angular velocity (180°–360°/sec), dissolving the image into high-speed directional motion blur streaks.
- **When to Use**: High-energy transitions, time jumps, comedic beats, rapid shifts in geographical location, frenetic montage.
- **Rules**: Must be written as a **Coordinated Pair**:
  - *OUT-half (Shot 1)*: Camera accelerates horizontally screen-right, hitting peak motion blur at the final frame.
  - *IN-half (Shot 2)*: Camera starts at peak motion blur panning screen-right, decelerating into settled focus on the new subject within 0.4s.
  - Direction and angular speed must be 100% identical.

### 4. Occlusion Hide (1917 / Hitchcock Rope Invisible Cut)
- **Concept**: The camera passes behind a massive foreground object (a dark tree trunk, concrete pillar, actor's back, or closing door) that momentarily fills 100% of the frame in darkness, masking the edit seam.
- **When to Use**: Faking an unbroken 60-second or multi-minute continuous take across separately generated 10s AI clips.
- **Rules**:
  - *Shot 1 Exit*: Camera pushes close until the dark pillar or actor's trench coat completely eclipses the entire lens (100% frame occlusion).
  - *Shot 2 Entrance*: Camera emerges from behind the same dark surface in the new environment with matching forward velocity.

### 5. Metamorphic Morph (Continuous Take)
- **Concept**: A single unbroken take where an element physically liquefies, re-organizes, or grows into another without an editorial cut.
- **When to Use**: Surreal dream sequences, sci-fi nano-technology, high-end commercial product reveals (perfume bottle transforming into blooming rose).
- **Rules**: Execute as a single prompt pass (Veo or Kling preferred). State the static anchor points that remain unchanged while the target surface morphs.

### 6. Smash Cut
- **Concept**: A sudden, violent, jarring cut between two scenes of extreme tonal, kinetic, or acoustic contrast (e.g. screaming battlefield cutting to a tranquil silent breakfast table).
- **When to Use**: Shock, waking from nightmares, comedic absurdity, sudden interruptions.
- **Rules**: Maximum acoustic and visual contrast. Zero pre-roll motion blur; instant hard cut on timeline.

### 7. Sound Bridges (J-Cuts & L-Cuts)
- **Concept**:
  - **J-Cut**: The audio of the upcoming scene (a car horn, dialogue line, or music intro) arrives 1.0–2.0s before the picture cuts.
  - **L-Cut**: The dialogue or room tone of the previous scene continues playing under the opening frames of the new scene.
- **When to Use**: Dialogue flow, conversational rhythm, smoothing hard cuts, documentary narrative momentum.
- **Rules**: Stated in the prompt's `AUDIO` specification and detailed in Post-Production Engineering Notes.

---

## 3. Pairing Protocol Checklist

When writing multi-shot sequences featuring transitions, verify:
- [ ] **Directional Symmetry**: Whip pan directions match (Right-to-Right, Left-to-Left).
- [ ] **Velocity Match**: The exit speed of Shot 1 matches the entry speed of Shot 2.
- [ ] **Scale & Coordinate Alignment**: Graphic matches share identical Cartesian X/Y percentages and subject occupancy.
- [ ] **Acoustic Bridge**: Foley whoosh dynamics (Buildup-Peak-Tail) or J/L cuts bridge the visual transition seam.
