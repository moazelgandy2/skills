# Gaze & Space — Who Looks at Whom, and From Where

A character "looking at" someone means nothing without a shared spatial map. "He turns his head toward her" with no screen direction is a coin flip the model will lose half the time — that is exactly how a man ends up staring past the woman he is answering. This file makes gaze promptable.

## 1. Spatial map first (before any gaze line)

Establish positions in frame terms: who sits/stands WHERE (frame-left foreground vs background screen-right, near vs far, sitting vs standing height). Every gaze then gets a screen-direction vector, never a bare "at her": "she looks screen-left toward him", "he turns his head screen-right toward her voice". No vector, no gaze — that is the rule.

## 2. Eyeline match pairs

Gaze works in pairs: look-shot → target. The look's height must match the target's height (looking slightly DOWN at a seated person, UP at a standing one, level across a table). For off-camera address, position the voice too: "her voice calls from off-camera screen-right (his frame), he looks toward camera — her position behind the lens — before answering."

## 3. The 180-degree axis

Draw the axis between the two people; keep the camera (and every whip, pan, and cut) on ONE side of it. A looks screen-right, B looks screen-left, always. Crossing the line makes both face the same way and the conversation reads broken. Whip-pans must travel ALONG the axis toward the target: panning left to find him means he lives screen-left, so she looks screen-left and he answers screen-right.

## 4. Look before line

Gaze leads speech: the look-beat lands first (turn head, find eyes, hold half-beat), THEN the line. Eye contact clusters at turn ends (~2s bursts, ~60–70% of conversation, with natural look-aways). Never direct a permanent unbroken stare, and never deliver the line before the head arrives.

## 5. Joint attention (two people, one object)

When both attend to the same thing, converge both eyelines on it with its position named: "both look down-center at the engine part between them". Shared gaze on one anchored point reads instantly; two independent "looking" lines drift apart.

## 6. Looking space + reaction coverage

Leave empty frame space in the direction of each look. For dialogue, plan the reaction: the listener's face must be visible (or cut to it) during the line — a punchline delivered to an empty frame feels unanswered even when the gaze is right.

## 7. Direct address discipline

State per character who owns the lens: presenter looks INTO lens (audience), guest looks AT presenter (off-camera mark), never both accidentally. An unplanned lens look reads as a fourth-wall break; a missing planned one reads as evasion.

## 8. Post fallback

Gaze-correction (eye-contact AI) tools can redirect eyes toward camera in post for direct-address work. Note it in run notes when the money beat depends on exact eye contact — don't burn generations chasing pupils.

## Interview trigger

Whenever two or more people share a scene, always map it before technical questions: where does each person sit/stand in frame, who looks at whom (with screen direction), and what shared object (if any) both attend to. One question, one map, then proceed.
