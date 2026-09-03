# Exact Frame Matching, Geometric Anchors & Seam Interpolation

This guide provides engineering standards for achieving 95–100% exact frame consistency across AI video generations, keyframe transitions, and chained shots. When models match at only 80–85%, the failure is almost always caused by loose coordinate definitions, floating camera origins, or unanchored start/end states.

---

## 1. The Root Cause of 80–85% Frame Mismatches

Why do prompts that describe the scene well still drift 15–20% in framing?
1. **Relative vs Absolute Spatial Telemetry**: Describing "close-up on her face" gives the model a 30% margin of error in lens focal length, camera distance, and head framing.
2. **Missing Bounding-Box & Grid Coordinates**: Without explicit frame percentages (e.g., `"Subject's eyes positioned on the upper horizontal third line at 33% vertical height, centered at 65% horizontal width"`), the model re-seeds composition randomly.
3. **Camera Origin Drift**: When a camera moves or cuts, failing to specify the exact height off ground (e.g. 1.2m), tilt angle (e.g. -5° downward), and lens focal length (e.g. 50mm spherical) allows the AI to invent new perspective vanishing points.
4. **Unconstrained Start and End States**: If only the action is prompted, the model guesses the entrance frame (0.0s) and exit frame (final second). 

---

## 2. The 100% Keyframe Anchor Architecture (First & Last Frame Interpolation)

For engines supporting Start/End frames (Kling 3.0, Runway Gen-4.5, Veo Frames-to-Video, Pika 2.2):

### The FLF (First/Last Frame) Principle
- **Pre-lock the Endpoints as Still Images First**: Generate the opening frame (0.0s) and final frame (e.g. 10.0s) as pristine still images before generating video.
- **Prompt Motion as Generative Inbetweening**: The prompt must NOT describe static scene appearance (since the frames already provide it); it must describe exclusively the **vector of travel, acceleration, and intermediate transformation** between Frame A and Frame B.
- **Hold-and-Settle Padding**:
  - Always enforce 0.5s of pre-roll hold on Frame A and 0.5s of settle deceleration before Frame B to prevent models from overshooting or warping the final frame.

---

## 3. The Geometric Grid Telemetry Protocol (For Text-to-Video & Image-to-Video)

When generating without a pre-rendered end frame, enforce **Geometric Grid Telemetry** directly in `LOCATION MAP` and `FIRST FRAME / BLOCKING`:

### Frame Percentage Mapping
Every subject must be anchored using explicit Cartesian screen coordinates:
- **Horizontal Screen Position**:
  - `Frame-Left (0%–33% X)`
  - `Frame-Center (33%–66% X)`
  - `Frame-Right (66%–100% X)`
- **Vertical Screen Position**:
  - `Upper Third (0%–33% Y)` — Eyeline default for medium/close shots
  - `Middle Third (33%–66% Y)` — Torso / horizon line
  - `Lower Third (66%–100% Y)` — Ground anchor / seating plane
- **Subject Screen Occupancy**: Specify exact visual mass percentage:
  - Extreme Close-Up: `Subject fills 85%–95% of vertical frame height`
  - Medium Close-Up: `Subject head and shoulders occupy 45%–55% of vertical frame height`
  - Wide Master: `Full standing subject occupies 25%–30% of vertical frame height`

### Optical Vanishing Point & Sensor Height
Explicitly define:
1. **Camera Lens Equivalent**: Specify focal length and optical distortion: `"50mm rectilinear prime lens, zero barrel distortion, flat field curvature."`
2. **Camera Sensor Elevation & Angle**: `"Camera placed at fixed 1.4m standing eye-level, tilted downward at -4 degrees toward the subject's eyeline."`
3. **Horizon Line Pin**: `"Background horizon line bisects the frame at exactly 40% vertical height."`

---

## 4. The Seam-Matching Protocol Across Multi-Shot Chains

When shot N cuts to shot N+1 in a narrative sequence:

### Rule 1: The Verbatim End-to-Start Handoff (The Shared Frame Rule)
- Extract the literal last clean frame of Shot 1 and use it as the `First-Frame Anchor` of Shot 2.
- In prompt text, Shot 2's `FIRST FRAME / BLOCKING` must describe the exact physical posture and momentum of that handoff frame:
  - `"First frame at 0.0s is physically identical to the final frame of Shot 1: subject frozen in mid-stride with left heel touching ground, head turned 40 degrees screen-left, coat hem trailing behind."`

### Rule 2: 180-Degree Line & Screen Direction Invariance
- If a subject exits frame-right, the cut to the next angle MUST show them entering from frame-left (preserving directional momentum).
- The optical axis must never jump across the 180° line. If Subject A is screen-left looking screen-right in Shot 1, Subject A must remain screen-left in any reverse two-shot setup unless an on-screen camera move physically crosses the line.

### Rule 3: Lighting Vector Persistence
- Key light angle must remain pinned to absolute world coordinates:
  - `"Key light remains pinned at 3200K low sun from true West (camera-left in Shot 1, camera-front in reverse-angle Shot 2)."`

---

## 5. Summary Checklist for 95–100% Match Precision

| Parameter | Loose Prompt (80% Match) | Precision Telemetry (100% Match) |
| :--- | :--- | :--- |
| **Eyeline** | "She looks at him" | "Eyeline pinned at 35% vertical height, directed screen-left along a 15-degree vector" |
| **Subject Size** | "Medium shot of the master" | "Subject torso and head occupy precisely 50% of vertical frame height, centered at 30% X" |
| **Camera Pose** | "Low angle camera" | "Camera elevated at 0.4m off floor, tilted +12 degrees upward, 35mm focal length" |
| **Handoff State** | "Continuing the conversation" | "Frame 0.0s matches Shot 1 exit frame: jaw closed, right hand suspended 10cm above wheel" |
