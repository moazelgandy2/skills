# Fiction Writing Principles & Prose Engineering Bible: Reader Reward Channels, AI Failure Modes & Taste Discipline

This reference establishes the narrative craft, psychological reward systems, and linguistic disciplines required to engineer compelling fiction, dialogue, and commercial storytelling. It provides explicit diagnostic tools to identify and scrub the 10 documented failure modes common to language models.

---

## Part I: The Five Reader Reward Channels

Fiction readers do not consume stories merely for factual plots; they read to experience neurological and emotional payoffs. Effective prose simultaneously protects and activates these five overlapping reward channels:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│ THE 5 READER REWARD CHANNELS                                                │
├──────────────────────────┬──────────────────────────────────────────────────┤
│ 1. Transportation        │ Entering the narrative world; sensory immersion  │
│ 2. Aesthetic Pleasure    │ Sentence-level cadence, rhythmic variation       │
│ 3. Social Simulation     │ Modeling flawed minds; interpreting subtext      │
│ 4. Narrative Flow        │ Optimal cognitive processing; matched pacing     │
│ 5. Prediction Reward     │ Information gaps, suspense, earned payoffs       │
└──────────────────────────┴──────────────────────────────────────────────────┘
```

### 1. Transportation (World Immersion & Strict POV Horizon)
- **The Core Rule**: The reader enters the world through a single, bounded consciousness.
- **The Knowledge Horizon**: The AI’s context window holds the entire story, but the POV character only knows what they have physically experienced up to this exact second. Never let the prose leak future knowledge, omniscient summaries, or emotional evaluations the character has not earned.
- **Concrete Physical Grounding**: Anchor scenes in tangible physics—friction, gravity, temperature, fabric textures, smells, and peripheral noise.

### 2. Aesthetic Pleasure (Sentence-Level Architecture)
- **Style is a Reward, Not Decoration**: Readers derive physical pleasure from linguistic musicality, varied sentence lengths, and dynamic syntax.
- **Syntactic Cadence**:
  - *Short, staccato sentences (Parataxis)*: Accelerate tension, simulate physical shock, create visceral immediacy.
  - *Complex, layered sentences (Hypotaxis)*: Draw out psychological rumination, sensory depth, and atmospheric weight.
  - *Monosyllabic Anglo-Saxon diction vs. Polysyllabic Latinate diction*: Use concrete, punchy Anglo-Saxon roots (bone, blood, stone, harsh, cold) for grounded action; reserve Latinate abstractions for detached, clinical analysis.

### 3. Social Simulation (Theory of Mind & Subtext)
- **The Human Puzzle**: Readers enjoy reading because it exercises their capacity to simulate other human minds.
- **The Interpretive Gap**: When prose states an emotion directly, it deprives the reader of the reward of deducing that emotion. Present the external behavioral anomaly, the awkward pause, or the misdirected physical action, and let the reader’s mind leap across the gap to diagnose the pain.

### 4. Narrative Flow (Cognitive Processing Match)
- **Friction-Free Momentum**: Pacing must match the internal stakes of the scene.
- **Action beats**: Cut descriptive density; focus on verbs, spatial vectors, and immediate physical consequences.
- **Reflection beats**: Expand sensory detail and psychological friction, but halt immediately before it becomes philosophical indulgence.

### 5. Prediction Reward (Curiosity & Suspense)
- **Information Gaps**: Suspense is not created by hiding information from the reader; it is created by letting the reader see the impending collision while the characters walk toward it (Dramatic Irony), or by planting specific, unresolved narrative questions that demand answers.
- **The Earned Payoff**: Never resolve a mystery through coincidence or unearned epiphany.

---

## Part II: The 10 Documented AI Failure Modes & Deterministic Fixes

Language models are heavily trained to be helpful, polite, comprehensive, and explanatory. In creative writing and dramatic storytelling, these exact helpfulness instincts produce severe prose defects.

```
┌─────────────────────────────────────────────────────────────────────────────┐
│ THE 10 AI FAILURE MODES (DEFECT CATALOG)                                    │
├─────────────────────────────────────────────────────────────────────────────┤
│ 1. Emotion Labeling           6. Scope Over-Elaboration                     │
│ 2. The Stock-Tells Trap       7. Collapsing Ambiguity                       │
│ 3. Premature Resolution       8. Over-Intensified Purple Prose              │
│ 4. Voice Homogenization       9. Info-Dumping Mechanics                     │
│ 5. Emotional Commentary       10. Punctuation Residue (Em-Dash Crutch)      │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

### Defect 1: Emotion Labeling (Direct Naming of Affect)
- **The Defect**: Writing *"She was furious,"* *"He felt a deep sadness,"* or *"A wave of anxiety washed over him."*
- **Why It Happens**: The model's training rewarded explicit state classification and clarity.
- **Deterministic Fix**: Delete the emotion noun. Substitute a character-specific, physical action under constraint:
  - *Bad*: "He was terrified of making a mistake."
  - *Fixed*: "He held the soldering iron with two hands to keep the tip from rattling against the PCB."

---

### Defect 2: The Stock-Tells Trap (Cliché Somatic Indicators)
- **The Defect**: Falling back on statistically overrepresented rubber-stamp physical reactions:
  - Clenched fists, digging nails into palms
  - Shaky breaths, releasing a breath they didn't know they were holding
  - Averting eyes, looking at shoes
  - Tightening jaws, grinding teeth
- **Why It Happens**: These phrases appear thousands of times in online fiction corpora, making them high-probability default tokens.
- **Deterministic Fix**: Ban all four stock tells. Replace with idiosyncratic physical displacement actions (e.g. wiping down an already clean counter, adjusting glasses by the hinge, peeling the label off a beer bottle).

---

### Defect 3: Premature Tension Resolution (The Comfort Reflex)
- **The Defect**: An intense conflict or argument is immediately followed by an apology, a shared understanding, a warm chuckle, or a silver lining within the same scene.
- **Why It Happens**: RLHF heavily penalizes leaving human users in unresolved, hostile, or anxious emotional states.
- **Deterministic Fix**: Enforce the **Law of Persistent Tension**. If an argument occurs in Beat 2, forbid reconciliation. Let the scene end on an uncomfortable silence, an unresolved grievance, or a slammed door.

---

### Defect 4: Voice Homogenization (The Polite Assistant / Therapy Voice)
- **The Defect**: Every character speaks in articulate, emotionally fluent, well-reasoned prose. Street hustlers, weary soldiers, and corporate executives all sound like empathetic counselors.
- **Why It Happens**: The assistant baseline persona leaks through all character dialogue.
- **Deterministic Fix**: Asymmetric dialogue engineering:
  - Introduce evasiveness, sentence fragments, interruptions, deflected questions, and defensive sarcasm.
  - Constrain vocabulary based strictly on character socioeconomic background and education.

---

### Defect 5: Emotional Commentary & Editorial Metaphors
- **The Defect**: Appending an explanatory editorial after an emotional event:
  - *Example*: "His grandfather's watch stopped ticking. The silence was deafening, a poignant reminder that time marches forward, indifferent to human suffering."
- **Why It Happens**: The model feels compelled to explain the thematic significance of narrative events.
- **Deterministic Fix**: Enforce the **Hard Cut Rule**. Present the sensory event and cut immediately. Trust the reader to understand the weight:
  - *Fixed*: "His grandfather's watch stopped ticking. He wound the crown until the spring resisted, set it on the nightstand, and laced his boots."

---

### Defect 6: Scope Over-Elaboration (Completeness Bloat)
- **The Defect**: When tasked with a 15-second hook or a confrontation beat, the model writes the confrontation, the aftermath, the internal reflection, and a moral conclusion.
- **Why It Happens**: The model equates longer, comprehensive responses with quality and helpfulness.
- **Deterministic Fix**: Enforce strict beat boundaries. Cut the narrative at the climax of the beat without providing the aftermath.

---

### Defect 7: Collapsing Ambiguity (The Moral Clarifier)
- **The Defect**: When a narrative moment should remain ethically ambiguous or morally gray, the model subtly steers the reader toward the "correct" moral interpretation or clarifies whether a character is lying.
- **Why It Happens**: Ambiguity registers as communicative vagueness or safety risk in base training.
- **Deterministic Fix**: Keep the character's internal motives opaque. Show contradictory behaviors that allow multiple plausible interpretations.

---

### Defect 8: Over-Intensified Purple Prose (Melodrama Inflation)
- **The Defect**: Inflating mundane moments to operatic cosmic stakes:
  - *Example*: "Her soul fractured into a thousand shimmering shards of iridescent grief as the realization crashed down upon her like a tempestuous sea."
- **Why It Happens**: The model confuses high emotional stakes with extravagant vocabulary.
- **Deterministic Fix**: Apply the **Understatement Law**. Extreme emotion demands sparse, quiet, concrete language. The simpler the sentence, the harder it hits:
  - *Fixed*: "She looked at the empty coat hanger. 'He took the car,' she said."

---

### Defect 9: Info-Dumping & Technical Exposition
- **The Defect**: Pausing narrative momentum to explain world rules, technology, or corporate workflows in explanatory paragraphs.
- **Why It Happens**: The model's primary training function is answering questions and explaining concepts.
- **Deterministic Fix**: The **Leakage Protocol**. Exposition must leak through consequence, physical limitation, or mundane character frustration, never through direct explanation.

---

### Defect 10: Punctuation Tells (The Em-Dash Crutch)
- **The Defect**: Scattering em dashes (`—`) across every sentence to connect disparate clauses, creating an artificial, rhythmic cadence that screams machine generation.
- **Why It Happens**: Models rely on em dashes to branch thoughts without committing to strong grammatical subordinations.
- **Deterministic Fix**: **Zero-Tolerance Em-Dash Ban**. Delete em dashes. Restructure the sentence into clean periods, commas, semicolons, or colons.

---

## Part III: Fiction-Specific Taste Discipline

Taste in creative writing is not subjective preference; it is the deliberate practice of **restraint, negative space, and multi-purpose economy**.

```
┌─────────────────────────────────────────────────────────────────────────────┐
│ THE 4 TASTE DISCIPLINE COMMANDMENTS                                         │
├─────────────────────────────────────────────────────────────────────────────┤
│ 1. Multi-Purpose Economy    │ Every sentence must perform 2+ functions      │
│ 2. The Iceberg Principle    │ 7/8ths of the emotional mass remains subtext  │
│ 3. Objective Correlative    │ Physical objects carry the emotional load     │
│ 4. Asymmetric Cadence       │ Vary line lengths; kill predictable beats     │
└─────────────────────────────────────────────────────────────────────────────┘
```

### 1. Multi-Purpose Economy
- If a sentence only describes scenery $\rightarrow$ **Cut it.**
- If a sentence only delivers factual information $\rightarrow$ **Cut it.**
- A sentence is allowed to survive ONLY if it simultaneously advances the narrative AND reveals character psychology or emotional tension.

### 2. The Iceberg Principle (Ernest Hemingway)
- The dignity of movement of an iceberg is due to only one-eighth of it being above water.
- The writer who omits things because they do not know them creates hollow prose. But the writer who knows their world intimately and deliberately withholds 90% of the backstory creates prose that vibrates with unspoken tension.

### 3. The Objective Correlative (T.S. Eliot)
- The only way of expressing emotion in the form of art is by finding an "objective correlative"; a set of objects, a situation, a chain of events which shall be the formula of that *particular* emotion.
- Don't describe grief. Describe an untouched bowl of soup growing cold on a Formica table.

### 4. Status Transactions (Keith Johnstone)
- Every line of dialogue between two characters is a negotiation of social status.
- Characters are constantly raising or lowering their status relative to the other person through posture, gaze, tone, interruption, or deliberate silence. Static, equal-status dialogue is dead dialogue.

---

## Part IV: The Prose Engineering Checklist (Pass/Fail)

Before any script or narrative brief passes to the Creative Auditor, verify:

- [ ] **Zero Emotion Labels**: Is every emotion expressed through physical constraint and action?
- [ ] **Zero Stock Tells**: Are fists, jaws, shaky breaths, and averted eyes 100% absent?
- [ ] **Zero Em-Dash Residue**: Are there zero decorative em dashes?
- [ ] **Strict Lived-Experience POV**: Does the character speak/think only from what they know right now?
- [ ] **Persistent Tension**: Is unresolved conflict allowed to stay unresolved without quick apologies?
- [ ] **Asymmetric Sentence Rhythm**: Do sentence lengths vary widely (from 2 words to 25 words)?
- [ ] **Objective Correlative Present**: Does a concrete physical object carry the thematic weight?
- [ ] **35% Word Count Reduction**: Has every unnecessary filler word been ruthlessly pruned?
