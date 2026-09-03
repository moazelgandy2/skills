# Long-Form & Multi-Shot Architecture — Continuity, Routing & Durations

This reference governs how long-form and multi-shot projects are planned, structured, and prompted across all major video models.

---

## 1. Engine Native Single-Shot Ceilings (NEVER Under-Allocate)

Never split a prompt into tiny 2s–3s micro-fragments if the user’s scene fits inside the engine's native single-shot generation window. Doing so fragments action, breaks lip-sync, causes camera stutter, and destroys physics continuity.

| Engine | Native Single-Shot Window | Preferred Single-Pass Duration | Extension Capability |
| :--- | :--- | :--- | :--- |
| **Sora 2 / Sora 2 Pro** | 4s, 8s, 12s, 16s, 20s | **10s – 20s** | Up to 120s via chained extensions |
| **Veo 3.1** | 4s, 6s, 8s | **8s** | Up to 148s via +7s extends (720p) |
| **Kling 3.0** | 5s, 10s, 15s | **10s – 15s** | Up to 3 minutes via chained passes |
| **Seedance 2.0 / 2.5** | 5s to 30s | **15s – 30s** | Chained multi-shot passes |
| **Runway Gen-4.5** | 5s, 10s | **10s** | Chained single shots |

### The Golden Rule of Clip Duration
- **If Total Duration ≤ Engine Native Ceiling**: Generate **ONE single continuous master prompt** utilizing the full duration (e.g. a 10s Sora shot or 8s Veo shot). **NEVER split into 2s or 3s micro-shots.**
- **If Total Duration > Engine Native Ceiling**: Split into logical **full-length native shots** (e.g., three 8s Veo shots or two 10s Sora shots) joined by clear narrative or editorial transitions.

---

## 2. Multi-Shot Continuity: Holding the Vibe, Palette & Music

When a project spans multiple shots (or chained extensions), models suffer severe continuity drift if prompts are written in isolation. Use the **Four Anchor Protocol** across every shot prompt:

### Anchor 1: Acoustic Continuity & Music Bed Stems
- **The Audio Bridge Rule**: Music and ambient room beds must never abruptly reset between shots.
- **Identical Stem Descriptors**: Every shot prompt in a multi-shot sequence must repeat the **exact same music and room tone descriptors**:
  - *Music Score*: Repeat the identical BPM, key, instrumentation, and mix level (e.g., `"Low 45Hz sub-bass bowed cello drone and sparse Rhodes piano chords, -18dB under dialogue"`).
  - *Diegetic Ambience*: Repeat the identical ambient bed (e.g., `"Continuous light summer breeze rustling through lawn ryegrass, distant cicadas at 4kHz, zero urban noise"`).
- **J-Cuts / L-Cuts in Post**: Explicitly instruct which audio element bleeds across the transition seam to glue the visual cut together.

### Anchor 2: Visual Style, Grain & Grade Tokens
- **Permanent Grade Token String**: Pick one colorist grade definition and repeat it verbatim across all shots:
  - `"Warm Kodachrome 35mm film stock, lifted organic shadows, golden-hour 3200K sunlight, unifying fine optical grain, zero digital sharpness filter."`
- Never vary style adjectives between shots (e.g., do not switch between "cinematic warm" and "golden glow").

### Anchor 3: Wardrobe & Material Consistency
- Repeat the exact material definitions: `"oversized white raw-linen button-down shirt with rolled cuffs"` and `"cherry-red cotton baseball cap with matte brass buckle"`.

### Anchor 4: Environmental Lighting Coordinates
- Lock the sun angle, shadow direction, and color temperature across all shots: `"Low 3200K raking key light from camera-left at 15-degree elevation, casting long directional shadows screen-right."`

---

## 3. On-Screen Text, Wall Signage & Phone Screens

AI video models fail notoriously on detailed typography. Follow these strict engineering protocols:

### The Text Reality Hierarchy
1. **Seedance 2.0**: The **only** engine that reliably renders on-screen subtitles, lower thirds, and clean typography directly from prompt instructions.
2. **Sora, Veo, Kling, Runway**: Rendering small text (phone screens, text messages, books, small wall posters) directly in the video generates warped pseudo-letters, illegible glyphs, and flickering artifacts.

### The 4 Rules for Text & Screens

1. **Move Intricate Text to Post-Production Overlay**:
   - For phone screens, text message notifications, computer monitors, and UI graphics: Prompt the physical device with a clean matte screen showing abstract ambient glow or blank interface, and explicitly designate the text as a post-production graphical overlay:
     - `"The actor stares down at a sleek modern smartphone; the screen casts a soft cool blue glow onto her face. [Post Note: Composite UI text message overlay in post-production]."`
2. **Environment Signage Must Be Massive, Simple, and Iconic**:
   - If text must exist in the environment (neon signs, storefront banners, street signs), limit it to **1–2 short, bold words** in high contrast:
     - Good: `"A glowing vertical neon sign reading 'BAR' in bold red sans-serif tubes."`
     - Bad: `"A café menu board listing espresso prices and opening hours."` (guaranteed gibberish).
3. **Screen Blocking for Mobile Devices**:
   - Keep the phone screen angled away from direct macro camera alignment, or frame the shot over-the-shoulder where the exact screen content is obscured or cast in soft glow.
4. **Foreign Language Characters (Kanji, Cyrillic, Arabic)**:
   - Unless using Seedance or verified image references, prompt for `"atmospheric neon signage"` or `"weathered urban storefront signs"` rather than specifying exact non-Latin sentences to avoid garbled alien characters.
