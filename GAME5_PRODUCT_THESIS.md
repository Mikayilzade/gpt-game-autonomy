# GAME #005 — PRODUCT THESIS LOCK

Last updated: 2026-08-22
Factory run: **7**
Phase: **3 — Product Thesis Lock**
Selected concept: **G5C02 — Tension Budget**
Commercial title: **TBD** (`Tension Budget` remains an internal concept label)
Production implementation: **NOT STARTED**

# PHASE 3 STATUS = COMPLETE

This file locks the product identity that later mechanics/content/UX/technical work must preserve. It does **not** freeze detailed simulation rules beyond the selection constraints already proven in Phase 2, and it does not start production implementation.

---

## 1. Product identity

### Target player
Primary audience:
- PC puzzle players who enjoy compact systemic spatial problems;
- players who prefer understanding visible cause/effect over hidden-stat optimization;
- players who like tactile world manipulation but do not want precision platforming, combat or heavy engineering UI;
- controller and handheld users must remain first-class rather than afterthoughts.

The product should also be approachable to players who do not understand real-world cable mechanics. The game teaches its own small visual grammar; no engineering knowledge is assumed.

### Platform
**PC / Steam first.**

Baseline:
- single-player;
- fully offline-capable;
- keyboard/mouse + controller;
- handheld-readable target where practical;
- premium buy-once product unless later commercial evidence gives a strong reason to change.

No multiplayer/network dependency is part of the thesis.

### Genre framing
**Top-down / elevated-isometric systemic traversal puzzle.**

Not:
- a rope-physics sandbox;
- an engineering simulator;
- a pipe/circuit editor;
- a precision platformer;
- an automation/factory game;
- a combat game;
- a graph puzzle presented through menus.

The player remains physically inside the same machinery they are reasoning about.

---

## 2. One-sentence hook

**Move one physical tension carriage and several connected machines change at once — raising one route can sag or close another, so every traversal is about choosing the right temporary compromise.**

Short store/GIF version:

**Pull here. Something rises. Something else gives way. Cross before your next choice changes the whole rig again.**

The first sentence is the design authority; the short line is presentation shorthand only.

---

## 3. Core fantasy

The player is a **rigger moving through a stylized suspended mechanical complex**: oversized lifts, counterweighted gates and cable-supported spans are visibly tied into one shared rig.

The fantasy is not “calculate tension.” It is:

> **Put your hands on one big mechanism, feel the entire structure answer, and use that tradeoff to make a route through it.**

Fiction stays intentionally light. The player may be framed as an inspector/rigger restoring passage through dormant infrastructure, but narrative never needs to explain formulas, currencies, factions or a large lore burden.

### Presentation wrapper
The world should look deliberately constructed to make cause/effect readable:
- large exposed cables and pulleys;
- oversized anchor carriage/handle;
- readable suspended platforms, gates and flexible spans;
- strong silhouettes and mechanical travel limits;
- clean stylized industrial/civic architecture rather than realistic factory clutter.

The machinery should feel physical and satisfying, but authoritative behavior is discrete and deterministic. Visual polish may imply weight; it must not imply free rope simulation that the rules do not support.

---

## 4. Signature player verb

### Anchor form — LOCKED
The baseline anchor is a **short continuous physical rail with 3–5 authored snap bands/positions**.

Player interaction:
1. approach the anchor locally in the world;
2. grab it;
3. slide the carriage along one short axis;
4. connected cables and loads visibly preview their destination/posture while the carriage moves;
5. release into a clear snap band;
6. the selected discrete system state becomes authoritative.

Why this form wins over pure buttons/sockets:
- preserves tactile ownership and visible “pull” fantasy;
- avoids a menu/state-selector feel;
- remains controller-safe and low precision;
- allows continuous visual cause/effect preview while keeping gameplay state discrete;
- can complete a normal meaningful move in roughly 2–3 seconds once the player is in reach.

### Explicitly rejected
- remote anchor control;
- detached graph/editor screen;
- point-and-click cable rewiring;
- free rope endpoint placement;
- real soft-body rope as gameplay authority;
- numeric tension entry;
- long crank/drag animations used as difficulty.

Later phases may tune rail length, snap count, grab radius and animation timing, but not replace direct local rail manipulation without reopening Phase 3.

---

## 5. Shared tension model — product-level lock

Every encounter/system has **one visible shared tension budget** distributed across its connected loads.

Canonical cable states remain exactly:
- **SLACK**
- **TAUT**
- **HIGH**

These are gameplay bands, not real engineering units. The player reasons from visible posture and consequences, not calculations.

### Baseline load archetypes — LOCKED
Phase 3 carries forward exactly three reusable families:
1. **Lift** — occupies authored height/posture states.
2. **Counterweighted Gate** — opens/closes/changes clearance through counterweight response.
3. **Flexible Span** — changes among visibly sagged / usable / over-lifted-steep traversal postures.

Repeated instances, mirroring, spatial arrangement and load addition/removal may create later depth. A fourth load family is **not assumed**. Phase 4 may only introduce one if it proves that the core product otherwise cannot satisfy already-frozen thesis goals; adding novelty for its own sake is prohibited.

---

## 6. Minimum visual language — no numbers required

A player at normal gameplay zoom must distinguish the three cable bands without reading a value.

### SLACK
Required redundant cues:
- obvious visible cable sag/curve;
- relaxed pulley/tensioner posture;
- connected load in its slack-result silhouette/position.

### TAUT
Required redundant cues:
- cable pulled straight with ordinary working posture;
- mechanical indicator collar/tab in the middle position;
- load in its useful/mid response where applicable.

### HIGH
Required redundant cues:
- cable remains straight but fittings/tensioner visibly reach an extreme compressed/extended posture;
- a large world-space three-position mechanical tab/collar is visibly at its high extreme;
- connected load is in its high-result silhouette/position.

Color, sound and vibration may reinforce these states but may **not** be the only differentiator.

### Causal transition rule
When the player moves the anchor, connected consequences should change in a visually synchronized sequence so the eye can follow:
**anchor motion → cable posture → load motion.**

The game must not hide redistribution and later reveal it as a surprise. Difficulty comes from choosing consequences, not discovering secret rules.

---

## 7. Core loop

A normal encounter repeats this loop:
1. enter and visually read the current rig;
2. identify which temporary set of load states creates the next useful route;
3. physically reach the anchor;
4. move it and watch multiple connected consequences change together;
5. traverse the route that now exists;
6. reach a new spatial state, anchor access or objective;
7. reconfigure the same shared budget because the previous compromise is no longer useful;
8. complete the objective / load mutation;
9. re-read the changed rig and extract.

The repeated action is not simply `pick the correct socket`. Mature play must involve **temporary compromise + physical traversal + reconfiguration**.

No passive cycle waiting is required by the thesis. Loads may animate between authored states, but waiting for a moving mechanism to eventually become correct should not become a central difficulty source.

---

## 8. Differentiator

The product is not unique because cables exist. Its defended differentiator is the combination of:

1. **one local physical anchor** as the repeated tactile verb;
2. **one shared conserved budget** so helping one load visibly changes others;
3. **several simultaneous world consequences** from each move;
4. **nonnumeric physical readability** instead of graph/calculation UI;
5. **traversal-separated decisions** so the best distribution changes with player position;
6. **visible load mutation** so entry logic can invert on extraction;
7. deterministic low-execution puzzle play rather than free rope physics.

If later design turns this into “route cable power through a graph,” “solve tension numbers,” or “simulate ropes realistically,” it has lost the selected product.

---

## 9. Session structure and campaign scope

### Main campaign target — LOCKED RANGE
- **24–28 main encounters**;
- working target: **26**;
- roughly **4–6 hours** for a first completion depending on puzzle speed;
- optional mastery/remix content may exist later only if it reuses the core grammar efficiently and playtest evidence shows demand.

Do not inflate beyond the Phase-2 repetition evidence merely to increase store-hour count. Tournament analysis found roughly 18 materially distinct systemic signatures and an honest strong-content ceiling around 26–30 encounters under the frozen vocabulary.

### Encounter length
Typical mature encounter target:
- roughly **5–12 minutes** on first solve;
- shorter teaching encounters acceptable;
- late synthesis may run longer if restart/checkpoint recovery stays humane.

### Macro pacing
Campaign should broadly progress through:
1. direct cause/effect;
2. two-load give/take;
3. non-extreme TAUT compromise;
4. traversal-separated reconfiguration;
5. three-load global consequence;
6. multi-placement relays;
7. repeated-archetype interactions;
8. visible load addition/removal;
9. return inversion;
10. compact synthesis without new mechanics.

This is a product pacing promise, not yet a final level list.

---

## 10. Demo promise — LOCKED

A commercial **15–25 minute demo** must demonstrate the real product, not stop at the tutorial.

Before demo end, normal play must include all of the following:
1. one anchor move visibly changes **at least two loads at the same time**;
2. the player independently makes a meaningful give/take choice;
3. a useful solution requires **TAUT / middle compromise**, proving that max/min is not the whole game;
4. the player traverses away from the initial decision point and later reconfigures the same shared system from a materially different spatial state;
5. one visible load is added/removed or otherwise leaves/joins the shared budget through an ordinary objective event;
6. the previously useful configuration becomes wrong or insufficient for return/extraction;
7. no numeric tension display or detached diagram is required to understand why.

Preferred final demo beat:
anchor move → multiple visible load changes → player crosses → objective visibly removes a counterweight → the old distribution changes meaning → player realizes the exit now needs a different compromise.

If the demo cannot show this cleanly in 15–25 minutes, the product thesis is not ready for production regardless of later campaign plans.

---

## 11. Dominant-strategy boundary

The main known exploit is **safe static socket enumeration**: stand at one anchor, cycle all 3–5 states, visually identify the globally correct answer, commit once.

The product does **not** fight this by hiding information or punishing experimentation.

Instead mature content must separate important choices through:
- traversal commitment;
- player-location-dependent usefulness;
- later anchor access;
- visible load addition/removal;
- return inversion;
- multi-placement sequence requirements.

A future content validator must flag/reject mature encounters where all completion-critical reasoning can be solved by exhaustively previewing every anchor state from one permanently safe station before any meaningful traversal/state change.

Fast restart remains allowed and desirable.

---

## 12. Accessibility / control thesis

The selected concept's advantage is **reasoning without dexterity tax**.

Required direction:
- controller-native local grab/slide/release;
- no pixel precision;
- no reaction-time catch mechanics;
- no color-only state distinction;
- no audio-only mechanical truth;
- clear focus/highlight for the currently manipulated rig;
- reduced-motion option may shorten/snap transitions while preserving causal before/after readability;
- UI/text scaling should not obscure world-space cable/load state.

Later UX design may add optional explicit labels for SLACK / TAUT / HIGH as an accessibility aid, but the base game must remain solvable from world presentation without numeric tension values.

---

## 13. Scope ceiling / explicit cuts

### In scope
- one directly manipulated anchor system per normal encounter baseline;
- 3–5 anchor snap bands;
- 2–4 active loads;
- three canonical tension states;
- three baseline load archetypes;
- ordinary top-down traversal;
- authored load addition/removal mutations;
- deterministic checkpoints/restarts;
- lightweight fiction and stylized mechanical spaces.

### Out of scope unless Phase 3 is formally reopened
- combat;
- enemies/patrol stealth as a central pillar;
- free rope construction;
- cutting/tying knots;
- realistic rope/soft-body simulation as authoritative puzzle state;
- stress/breakage/fatigue simulation;
- numeric engineering calculations;
- detached node/graph/circuit editor;
- inventory of tension tools/gadgets;
- multiple simultaneous independently controlled anchor systems as baseline;
- factory logistics/automation economy;
- crafting/resources/currency/grind;
- large narrative/dialogue burden;
- procedural level generation as a requirement;
- co-op/multiplayer.

---

## 14. Empirical kill gate carried into implementation

Design can specify the rules, but it cannot honestly claim the core feels/readability works before graybox playtesting.

A one-week empirical prototype remains mandatory before expensive content production.

### Prototype must contain
- normal player movement;
- one short 4-position anchor rail;
- Lift + Counterweighted Gate + Flexible Span;
- SLACK / TAUT / HIGH visual states;
- one teaching encounter;
- one traversal-separated mature encounter;
- one load-removal + return-inversion encounter;
- no numeric tension UI.

### Required observations
With roughly 8–12 unfamiliar testers if practical:
- consequence-prediction accuracy after teaching;
- blind socket-enumeration frequency;
- whether players ask for numbers/gauges/graph view;
- whether they can explain the give/take idea in ordinary language;
- grab-to-intentional-release time once in reach;
- whether normal camera scale makes all relevant cable/load states distinguishable.

### Phase-3 empirical PASS target
- median post-teaching consequence prediction roughly **>=75%**;
- most players understand that redistributing pull helps some loads while changing others without numeric explanation;
- blind full enumeration is not the dominant mature-solving method;
- normal anchor move feels quick/physical, roughly **<=2–3 seconds** from grab to intentional snap once reached;
- no realistic rope simulation is needed for believable cause/effect.

### Kill/redesign trigger
- players repeatedly request numbers or detached diagrams;
- SLACK / TAUT / HIGH cannot be distinguished reliably at play zoom;
- mature puzzles are consistently solved faster by cycling all sockets than by reasoning/traversal;
- the anchor feels like a menu selector with a long animation;
- adding realistic rope physics appears necessary just to make the rule understandable.

A failed empirical gate should trigger bounded repair or concept reconsideration, not feature inflation.

---

## 15. Product thesis acceptance checklist

- [x] One selected concept only: G5C02 Tension Budget.
- [x] G5C37 stays historical reserve; no hybridization.
- [x] PC/Steam-first single-player premium baseline frozen.
- [x] Genre framed as embodied systemic traversal puzzle, not engineering sim/editor.
- [x] Core fantasy and minimal fiction wrapper frozen.
- [x] One-sentence hook frozen.
- [x] Local short-rail anchor manipulation frozen.
- [x] SLACK / TAUT / HIGH product language frozen.
- [x] Lift / Counterweighted Gate / Flexible Span baseline frozen.
- [x] Nonnumeric redundant world-space visual language frozen.
- [x] Core loop and differentiator frozen.
- [x] 24–28 main encounter range / 26 working target frozen.
- [x] 4–6 hour first-completion target frozen.
- [x] 15–25 minute demo must show full differentiator, mutation and return consequence.
- [x] Static safe socket enumeration remains an explicit content-rejection condition.
- [x] Accessibility advantage is low execution burden, no audio/color/numeric dependence.
- [x] One-week readability/tactility empirical gate remains explicit.
- [x] Production implementation remains outside factory.

# PHASE 3 DECISION

**PHASE 3 PRODUCT THESIS LOCK = COMPLETE.**

Game #005 is a compact premium embodied systemic puzzle about physically redistributing a shared tension budget across a stylized exposed rig. The player repeatedly makes temporary mechanical compromises, traverses the consequences, then reconfigures after position or load state changes.

Phase 4 may now specify exact mechanical architecture. It must not expand the product into rope simulation, engineering arithmetic, graph editing, gadget inventory or a second gameplay pillar.

## NEXT ACTION — GAME #005 RUN 8 / PHASE 4 MECHANICAL ARCHITECTURE
1. Re-read the complete active authority chain including this file.
2. Create `GAME5_MECHANICS.md`.
3. Define the exact authoritative state model for anchor positions, cable bands, shared budget allocation and load responses.
4. Specify deterministic ordering for grab/preview/commit, traversal, load transition, objective mutation and checkpoint/restart.
5. Freeze exact rules for Lift, Counterweighted Gate and Flexible Span, including collision/traversal state during transitions.
6. Define how 3–5 anchor positions map to distributions without exposing numbers to the player; content data may use internal integers if useful.
7. Define invalid/ambiguous authored states and validator rules, especially safe static socket enumeration and visually indistinguishable states.
8. Specify player movement/interactions only as needed to support the puzzle identity; do not add a movement mastery pillar.
9. Define win/fail/reset, sequencing, objective mutation, return inversion and content-level state-machine rules.
10. Separate frozen mechanics from balance knobs and empirical feel values.
11. Do not begin Phase 5 or production implementation until Phase 4 is internally coherent and implementation-ready at the rules level.