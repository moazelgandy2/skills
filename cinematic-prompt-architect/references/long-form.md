# Long-Form — Planning Past One Clip's Ceiling

Every engine caps a single generation. The finished video's length is a separate number from any clip's length — ask it first, then route. Three numbers matter per engine: native cap, extended cap, and the catch.

## Ceilings (Aug 2026 — verify before mission-critical work, caps move fast)

| Engine | Native single generation | Extended maximum | The catch |
| --- | --- | --- | --- |
| Veo 3.1 | 4 / 6 / 8s | 148s via +7s extends (up to 20×) | Extensions 720p-only, Veo-source-only, 2-day storage timer; 1080p/4K = single 8s only |
| Sora 2 (API) | 4–20s (steps of 4) | 120s via 6 chained extensions | API sunsets Sept 2026 — don't architect pipelines on it |
| Kling 3.0 | 15s (multi-shot: 6 labeled shots) | ~3min via ~4–5s steps, paid | Drift past ~2min; quality sweet spot under 30s |
| Seedance 2.5 | 30s native (longest single pass) | Extend twice officially | Stingiest extension allowance; plan shots, not chains |
| Runway Gen-4.5 | ~10s | Short extensions | Route to it for control, not length |

## The routing decision (ask total length in Step 0.6, then pick)

- **Total ≤ native ceiling** → single generation. Never chain what fits in one pass (Sora 20s request = one 20s prompt, not three clips).
- **Total ≤ ~60s AND one continuous take** → Extend route: base clip + continuation segments, each with its own next-beat prompt.
- **Total > ~60s OR multi-scene OR multi-angle** → Assembly route (default): N shots at native length, shared anchors, joined in the editor. Cuts are cheaper than continuity — this is how real long-form AI work gets made.

## Extend-route rules

- **Base clip first, and make it perfect.** Every extension inherits clip one — spend generations on the opener before chaining anything.
- **Each segment prompt = SAME blocks re-stated + next beat only.** Identity, light, camera, grade, audio bed repeated verbatim every segment (the model remembers nothing); then one new action. Never contradict the last frame (facing left stays facing left unless the beat is the turn).
- **Short segments for complex motion (4–6s), longer for ambient (8–12s).** More decision points = less accumulated drift.
- **Endpoint discipline.** End each segment on a stable frame: subject fully visible, lighting settled, camera NOT mid-whip. Seams land on neutral motion — never on faces, logos, or reveals (pin those mid-clip, or via Frames-to-Video).
- **2–3 candidates per segment, keep least drift.** Check continuity every 2–3 segments; regenerate the bad segment, never rebuild the chain. Fix drift early — it's cheaper than discovering it five clips later.
- **Carry the audio bed across.** Same ambience, same voice; a soundtrack that jumps at each seam screams stitched. State the resolution tradeoff up front (Veo extend = 720p).

## Assembly-route rules (30s ad = 4–8 shots)

Standard spine: hook (2–3s) → problem (3–5s) → intro/reveal (3–5s) → demo (5–8s) → result (3–5s) → CTA (3–5s). Size beats to clips: dialogue 3–5s, emotional close-up 2–4s, action 2–3s, setup 3–5s. Shot list BEFORE generation (single line each: size + intent); each shot gets its own full prompt with shared anchors; transitions + J-cuts + grade-match planned in post. Approve beats first, generate in short modules — re-generate single weak shots, never the series.

## Interview trigger

Step 0.6 asks TWO numbers, one question at a time: total finished length, then per-clip/engine fit. If total exceeds the native ceiling, state the route (Extend vs Assembly), the clip count, and the tradeoff (resolution / drift / edit work) in two lines before proceeding — the user approves the plan, then you write clip-by-clip prompts, each complete and runnable alone.
