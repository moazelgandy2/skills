# Camera Language & Kinematics Encyclopedia — Angles, Tracking, Zooms & Optics

This encyclopedia governs camera direction, spatial perspectives, tracking mechanics, lens behaviors, and optical effects for AI video generation across Sora, Veo, Kling, Runway, and Seedance.

---

## 1. Camera Angles: The Power & Psychological Axis

Camera angles establish the subconscious power dynamic between the subject, the environment, and the audience. Never prompt vague words like "good angle"; specify the exact physical perspective.

| Camera Angle | Elevation & Tilt Vector | Psychological & Narrative Impact | When to Use | Prompt Formula & Syntax |
| :--- | :--- | :--- | :--- | :--- |
| **Eye-Level Shot** | Sensor at 1.5m–1.6m, 0° tilt (parallel to ground) | Neutrality, objective realism, human-scale connection | Standard dialogue, naturalistic drama, interviews | `Camera at eye-level height of 1.55m, 0-degree tilt, parallel horizon` |
| **Low-Angle Shot** | Sensor at 0.3m–0.8m, +15° to +35° upward tilt | Dominance, heroism, intimidation, towering authority | Villains, heroic reveals, monumental architecture | `Low-angle perspective at 0.5m elevation, tilted upward at +25 degrees toward subject` |
| **High-Angle Shot** | Sensor at 2.2m–3.0m, -20° to -45° downward tilt | Vulnerability, isolation, diminution, powerlessness | Defeat, surveillance, character trapped or overwhelmed | `High-angle shot at 2.6m elevation, tilted downward at -30 degrees looking down on subject` |
| **Dutch Angle (Canted)** | Sensor tilted sideways along roll axis: 8° to 25° roll | Psychological disorientation, madness, dread, vertigo | Thrillers, panic, mental collapse, horror, unstable tension | `Dutch canted angle with a 15-degree clockwise roll off-horizontal, horizon skewed` |
| **Bird's-Eye / God's View** | Directly overhead at 90° downward nadir tilt | Absolute detachment, omniscience, fatalism, architectural layout | Crime scenes, labyrinth navigation, transit, choreography | `Overhead bird's-eye view, camera looking directly down at a 90-degree nadir plunge` |
| **Worm's-Eye View** | Ground level (0.05m–0.15m), +45° to +80° upward tilt | Extreme awe, monolithic scale, claustrophobic looming | Giant monsters, soaring skyscrapers, boots stomping mud | `Extreme worm's-eye view pinned 10cm off floor, steep +60-degree upward tilt` |
| **Shoulder-Level (Dirty OTS)** | Sensor at 1.4m behind foreground subject (20% occlusion) | Intimacy, spatial anchoring in conversations | Two-character dialogue, interrogations, confrontational beats | `Dirty over-the-shoulder frame, 25% foreground shoulder occlusion on frame-left` |

---

## 2. Camera Tracking & Motion Kinematics

Moving cameras must be physically grounded. Diffusion models produce unnatural "floating drone" drift if not constrained by physical rig mechanisms.

### The Tracking Taxonomy
1. **Lead Tracking (Push-Out / Backwards Dolly)**:
   - *Mechanics*: Camera travels backward along the Z-axis in front of a forward-advancing subject, matching their walking speed (1.0–1.3 m/s).
   - *Use*: Forces the audience to confront the subject’s face and advancing emotional momentum.
   - *Prompt Syntax*: `Camera leads subject backward along corridor central axis at 1.2 m/s, maintaining locked 45% MCU frame occupancy`.
2. **Follow Tracking (Push-In / Forwards Dolly)**:
   - *Mechanics*: Camera tracks forward behind the subject, capturing their heading and immediate environment.
   - *Use*: Suspense, exploration, stalking, entering mysterious new spaces.
   - *Prompt Syntax*: `Camera follows 1.5 meters behind subject's right shoulder, tracking forward into dimly lit chamber`.
3. **Lateral / Side Tracking (Trucking Shot)**:
   - *Mechanics*: Camera glides sideways parallel to the subject's path of motion.
   - *Use*: Profile studies, traveling alongside vehicles, walking-and-talking dialogues with passing parallax.
   - *Prompt Syntax*: `Lateral trucking shot moving parallel to subject at 1.0 m/s, capturing foreground fence posts sliding in rapid parallax`.
4. **Arc Tracking (Orbit Shot / 360° Wrap)**:
   - *Mechanics*: Camera orbits the subject along a curved or circular track while panning to hold the subject dead-center.
   - *Use*: Epiphanies, romantic vertigo, tactical standoff, dramatic realizations.
   - *Prompt Syntax*: `Camera executes a smooth 90-degree clockwise orbital arc at 1.8m radius, revolving from profile to three-quarter frontal`.
5. **Boom / Pedestal (Vertical Displacement)**:
   - *Mechanics*: Entire camera body moves straight up (Pedestal Up) or down (Pedestal Down) without tilting the lens.
   - *Use*: Revealing scale, transitioning between floor details and character faces.
   - *Prompt Syntax*: `Camera pedestals vertically upward from puddle reflection at 0.2m up to eye level at 1.6m with 0-degree tilt`.

---

## 3. Specialized Camera Rigs

Prompting specific professional rig names activates deep cinematic conditioning in modern video models:

*   **Technocrane / Telescoping Jib**: High-angle sweep that smoothly extends outward through space while booming down. Use for opening establishing shots descending into close-ups:
    *   `Technocrane sweep: high-angle 6m crane arm telescopes diagonally downward and forward, settling into a crisp 1.5m eye-level close-up`.
*   **Steadicam / Trinity Rig**: Smooth, floating, dynamic human-driven motion with subtle organic inertia and corner lean. Use for continuous walk-throughs:
    *   `Steadicam operator glide following subject through crowded bazaar, exhibiting organic 1-degree inertia damping and corner banking`.
*   **Handheld Cinéma Vérité**: Raw, visceral, shoulder-mounted camera with physical breathing sway and slight re-frame lag. Use for documentary realism, panic, action:
    *   `Handheld shoulder-mount capture, noticeable organic micro-jitter (1.2Hz frequency), tactile reframing hesitation, raw documentary urgency`.
*   **Snorricam (Chest-Mounted Rig)**: Rig bolted directly to the actor's torso facing back at them. The actor remains dead-still in center-frame while the entire background wildly sways and twists around them:
    *   `Snorricam rig strapped to subject's chest: actor's face remains locked dead-center in frame while background walls sway violently behind them`.
*   **Cable-Cam / Wire Rig**: High-speed, perfectly straight overhead or ravine tracking. Use for sports, car chases, forest pursuits:
    *   `Cable-cam tracking shot skimming 2 meters above forest canopy at 15 m/s, zero roll variance`.

---

## 4. Zoom Mechanics & Optical Illusions

Zooms change focal length; tracking changes camera position. Mixing them up creates amateurish results.

1. **Slow Optical Push-In (Creeping Zoom)**:
   - Gradual focal tightening (e.g. 50mm to 85mm) over 8 seconds without moving the camera base. Used for mounting psychological focus or dread.
   - Syntax: `Slow, barely perceptible optical zoom-in from 50mm to 70mm over 8 seconds, tightening focus onto trembling pupils`.
2. **Crash Zoom / Snap Zoom (Tarantino Zoom)**:
   - Ultra-fast, high-velocity focal burst (e.g. 35mm to 135mm in 0.3s) accompanied by transient optical motion blur. Used for shock reveals, martial arts impacts, dramatic irony.
   - Syntax: `High-velocity 0.3-second crash zoom from wide master to tight extreme close-up on villain's smirk, instantaneous snap focal lock`.
3. **Dolly Zoom / Vertigo Effect / Zolly**:
   - Camera dollies backward while the optical lens simultaneously zooms in (or vice versa). The subject remains exactly the same size in frame while the background perspective warped, stretched, or compressed.
   - *Use*: Sudden catastrophic realization, panic attack, vertigo, cosmic dread.
   - Syntax: `Motivated Dolly Zoom (Zolly): camera dollies backward 2 meters while lens zooms from 35mm to 85mm; subject remains locked at 50% MCU frame size while background perspective expands and warps outward in surreal vertigo`.

---

## 5. Lens Character & Optical Artifacts

Specify lens families to control flare, bokeh, and edge distortion:
- **Anamorphic Glass (Kowa / Cooke Anamorphic)**: Oval bokeh, horizontal blue/amber streak flares, subtle barrel distortion at edges, cinematic 2.39:1 squeeze rendering.
- **Spherical Masters (Arri Master Primes)**: Razor-sharp edge-to-edge, circular creamy bokeh, zero chromatic aberration, pristine color neutral fidelity.
- **Vintage Glass (Super Baltar / Canon K-35)**: Warm skin glow, gentle edge fall-off, organic rainbow halation around specular light sources.
- **Split-Diopter Lens**: Optical split-focus filter keeping both an extreme foreground object (15cm away) and a background subject (10m away) in simultaneous razor-sharp focus with a visible vertical boundary line.
