# GAME #003 — BORROWED COLLISION — PRODUCT THESIS LOCK

Last updated: 2026-08-19
Factory run: **7**
Phase: **3 — Product Thesis Lock**
Concept: **Borrowed Collision**
Product thesis locked: **YES**
DESIGN COMPLETE: **NO**

This file freezes the identity of Game #003. Later phases may refine exact mechanics, content counts, balance, implementation and presentation, but they must not quietly turn the game into generic physics puzzles, trajectory editing, projectile combat, vector arithmetic, inventory logistics, or a sandbox.

---

# 1. Working title and naming constraints

## Working title
**Borrowed Collision**

The title remains the factory working title because it expresses the core fantasy: one impact can be taken from where it happened and used elsewhere.

Fresh targeted exact-title searches on 2026-08-19 did not surface a current Steam game whose title/product identity obviously conflicts with `Borrowed Collision`. This is **not** trademark clearance. Final store-name, trademark and domain review belong to release work.

## Naming constraints
Any replacement title should preserve at least two of these ideas:
- collision/impact/consequence;
- borrowing/stealing/carrying/reusing;
- the fact that force is moved between places rather than merely redirected locally.

Avoid names that imply:
- realistic physics simulation;
- guns/projectiles/combat as the primary fantasy;
- numerical vector programming;
- time travel as the central mechanic;
- generic momentum platforming.

---

# 2. Target player

Primary audience:
- players of compact systemic puzzle games;
- players who enjoy causal reasoning, physical logic and finding elegant multi-step solutions;
- players who like mechanics that can be understood visually but deepen through recombination;
- PC/Steam players comfortable with 10–25 minute focused puzzle sessions;
- players who appreciate optional mastery and alternative solutions without punishment for experimentation.

Secondary audience:
- action-puzzle players attracted by self-launching and short moving-body sequences;
- controller/Steam Deck players if causal selection and snapping remain fully readable without mouse precision;
- players who enjoy lightly absurd stylized physical worlds even without narrative-heavy framing.

Not a primary target:
- players seeking realistic rigid-body simulation or a physics sandbox;
- reflex/action players expecting combat depth;
- programming-puzzle players who want numeric vector control;
- open-world/exploration audiences;
- players seeking procedural endless progression or live-service retention.

---

# 3. Platform / commercial frame

- **PC/Steam first.**
- Premium single-player.
- Controller support required; mouse cannot be mandatory.
- Steam Deck compatibility is a design target.
- A playable demo is strongly preferred because the hook should prove itself within 15–20 minutes.
- No F2P economy, ads, consumable retries, gacha, battle pass, server dependency or live-service requirement.
- Current design-time price neighborhood remains broadly **$14.99–$19.99**, with likely center nearer **$14.99–$17.99** if first-clear scope lands around 5–8 strong hours. This is a commercial hypothesis, not a frozen release price.

---

# 4. Genre framing

Primary genre:
**systemic causal puzzle / stylized physics puzzle**.

Supporting descriptors:
- deterministic;
- spatial;
- consequence-transfer;
- compact authored challenges;
- light action/traversal;
- multi-solution where feasible;
- low-pressure baseline play.

Do not market as:
- realistic physics simulator;
- sandbox;
- trajectory editor;
- vector-programming game;
- platformer first;
- combat game;
- inventory game;
- automation/factory game.

---

# 5. One-sentence hook

**Steal the force from one crash and spend it somewhere else: harvest collisions as portable impacts, route them through physical sockets, and reuse those consequences on carts, doors, cargo — or yourself.**

The sentence may be polished later for store copy, but its meaning is canonical.

---

# 6. Core fantasy

The world treats a collision consequence as something that can be captured, carried and reassigned.

A crate crashes into a bumper. The event is over — but its resolved impact can be harvested as a compact physical token. The player can take that consequence elsewhere, transform its direction through visible machinery, and apply it to a different receiver. A crash that happened in one room can become movement, access, traversal or the source of another collision in another room.

The fantasy is **not** controlling force abstractly. It is **reusing a consequence that genuinely happened**.

The intended player thought is:

> “That collision is useful somewhere else.”

Later mastery becomes:

> “I can engineer one collision whose consequence replaces several obvious ones.”

---

# 7. Non-negotiable differentiation rule

**A resolved physical consequence becomes a portable resource, and the world-state that created and receives that consequence must continue to matter.**

This rule protects the concept from collapsing into colored-arrow inventory.

A mature challenge is invalid if it can be reduced to:
`collect direction/magnitude token -> match it to socket`
while ignoring:
- how the donor collision was created;
- whether the donor can be recreated;
- what harvesting/spending changes in the world;
- receiver aftermath;
- magnitude suitability/fragility;
- resulting secondary collisions;
- whether the player uses the consequence on self versus environment.

If later design can remove collision provenance and world-state dependency without changing play, the product identity has been diluted.

---

# 8. Canonical player-facing core loop

1. **Read the physical problem** — identify goals, receivers, dangerous/fragile states and available donor events.
2. **Cause or observe a collision** — using already-defined world interactions rather than freeform simulation chaos.
3. **Harvest the resolved impact** — capture a visible directional/magnitude-banded consequence from an eligible collision.
4. **Carry / route it** — keep a tiny bounded inventory and move the token through visible fixed-direction transforms where useful.
5. **Spend it** — apply the token to a compatible object, mechanism, cargo or self-launch receiver.
6. **Watch deterministic consequence** — motion resolves through bounded collisions and state changes.
7. **Inspect causality** — understand source lineage, transformation, receiver result and any secondary collision created.
8. **Revise** — Undo/reset freely or continue from the new state.
9. **Complete the case** — satisfy all baseline objectives/invariants.
10. **Optionally master it** — use cleaner causal compression, preserve scarce donors, avoid breakage or meet another transparent final-state mastery condition.

There is no long submit/watch phase. Feedback follows each committed action quickly.

---

# 9. Session structure

Typical authored case:
- roughly 5–20 minutes first clear;
- one compact causal problem or tightly linked room packet;
- immediate retry/Undo/reset;
- baseline solution permits experimentation;
- optional mastery after or alongside baseline completion.

Typical play session:
- 20–60 minutes;
- usually 2–6 cases depending on complexity.

Working campaign target carried from tournament:
- approximately **30–36 authored main cases**;
- optional **8–12 remix/mastery cases** only if they change causal structure rather than pad count;
- target first-clear duration roughly **5–8 hours**, subject to Phase-5 content/pacing validation.

Counts are design targets, not permission to compensate for repetitive reasoning with raw volume.

---

# 10. Canonical primitive vocabulary ceiling

Phase 3 freezes a deliberately small player-facing vocabulary. Phase 4 must define exact semantics, but it may not casually multiply token properties.

## 10.1 Impulse identity
A portable impact has only:
- **direction** — working model: 8 snapped compass directions;
- **magnitude band** — working model: weak / medium / strong;
- **source lineage/provenance** for rules/causal explanation;
- consumed/available state.

No player-facing numeric vector components are required.

## 10.2 Physical direction transforms
Maximum 1.0 transform-family target:
1. quarter-turn;
2. reverse;
3. mirror;
4. damper.

Phase 4 may remove/merge one if redundant, but should not add a broad modifier inventory.

Transforms are physical world devices with fixed visible behavior. The player does not freely rotate a token to any angle.

## 10.3 Donor / receiver behavior ceiling
Target maximum: **6–8 reusable behavior families** across sources and receivers.

Examples that may be formalized later:
- exhaustible/resettable donor;
- ordinary receiver;
- fragile receiver;
- magnitude-window receiver;
- anchored/converter device;
- self-launch receiver;
- moving receiver;
- chain-producing collision source.

These are a ceiling direction, not permission for every case to invent bespoke exceptions.

## 10.4 Inventory ceiling
Working baseline: **2 portable impacts**.
Absolute late-game ceiling: **3**.

The product must not become inventory management.

---

# 11. Progression and hour-10 depth thesis

The player should understand almost the entire primitive vocabulary early. Progression comes from **causal composition**, not unlock inflation.

Early game:
- harvest one obvious collision;
- spend it on one receiver;
- learn direction transforms;
- learn that strong is not always better;
- learn self-launch;
- learn donor scarcity/provenance.

Midgame:
- two-token ordering;
- resettable versus exhaustible donors;
- chained collisions that create new impacts;
- source world-state changes future availability;
- receiver aftermath alters future route/state;
- self versus cargo/environment allocation;
- multi-room transport.

Late game / hour-10 mastery:
- engineer collisions deliberately for later reuse;
- recognize one collision can produce a better downstream chain than several obvious donor events;
- preserve scarce source state while solving another objective;
- combine weak impacts instead of assuming maximum force;
- use converter topology and receiver aftermath to create causal compression;
- find alternate valid solutions and transparent final-state mastery.

**No new primary verb is required at hour 10.**

If later content freshness depends on adding fine-grained vector manipulation, dozens of impulse elements, elemental force types, combat abilities or token rarity, the design has failed its depth thesis.

---

# 12. Failure, Undo, reset and experimentation philosophy

Experimentation is part of learning and must remain cheap.

Rules locked at thesis level:
- ordinary wrong-but-legal actions commit and show their consequence;
- Undo/reset is fast and does not consume a resource;
- baseline completion never penalizes raw Undo count;
- no lives, energy, retry currency or irreversible campaign punishment;
- a fragile object breaking may make the current case state unsatisfied/dead-ended, but recovery is transparent and immediate;
- a spent/exhausted donor is a world-state consequence, not a hidden punishment;
- hard failure should be rare and limited to clearly terminal local case states, with instant restart/Undo.

Brute force must be beaten through meaningful branching, source/receiver interactions and causal understanding — not by charging for experimentation.

---

# 13. Donor exhaustion / duplication philosophy

A harvested collision is not generic renewable ammo unless the case explicitly contains a renewable donor as part of its visible system.

Core thesis:
- one collision lineage yields at most its defined harvest result;
- harvesting/spending cannot duplicate an impact through UI tricks, rewind artifacts or repeated trigger overlap;
- resettable donors must have a meaningful visible reset rule/cost/state;
- strong endlessly repeatable donor loops are invalid mature content unless the loop itself is the explicit puzzle resource;
- provenance should remain inspectable enough that the player can tell **where this impact came from**.

Phase 4 must freeze exact lineage, collision and reset semantics deterministically.

---

# 14. Presentation thesis

Visual identity should make the causal transfer unmistakable in screenshots and motion.

Required visual sequence:
1. collision happens;
2. its resolved consequence condenses/pops into a chunky portable impact representation;
3. the token retains directional and magnitude identity;
4. the player visibly carries/routes it;
5. spending the token produces a matched receiver impulse;
6. secondary collisions visibly connect back to the spent source through short causal feedback.

The world should look intentionally stylized and discrete enough that quantized rules feel native rather than like a broken realistic physics engine.

Avoid:
- photorealistic rigid-body expectations;
- thin engineering-vector diagrams as the default fantasy;
- dense numeric telemetry;
- particle spectacle that obscures cause/effect.

A screenshot should ideally show donor collision lineage, a carried impact, and a receiver/transform in one readable composition.

---

# 15. Audio / causal feedback thesis

Audio reinforces impact identity but never carries unique information.

Direction must be visual. Magnitude must use redundant icon/shape/animation/text signals, not loudness alone.

Suggested language for later UX design:
- weak / medium / strong impacts have distinct visual mass and short sound character;
- harvesting has a recognizable `consequence captured` cue;
- transform devices communicate their fixed operation before commit;
- receiver failure/breakage identifies whether the problem was direction, magnitude, incompatibility or world-state consequence;
- causal lineage can be inspected after resolution without replaying the whole animation.

---

# 16. Terminology rule — avoid vector homework

Internal implementation/design language may use **impulse token**, because it is mechanically precise.

Player-facing language should default to more intuitive terms until testing proves otherwise. Candidate vocabulary:
- **impact**;
- **stored hit**;
- **captured impact**;
- **borrowed force**;
- **crash charge** only if tone supports it.

`Impulse` may appear in advanced glossary/help if playtests find it natural, but onboarding should not require understanding the physics term.

The UI must teach:
- arrow direction;
- weak / medium / strong;
- source lineage;
without exposing `x/y vector`, velocity components or Newtonian equations.

---

# 17. Input thesis

All required baseline play must be possible through:
- mouse + keyboard;
- keyboard-only;
- controller-only;
- Steam Deck controls.

Core constraints:
- no free-angle precision aiming for ordinary completion;
- directions snap to authored valid orientations;
- compatible nearby receivers can be focused/cycled deterministically;
- token selection fits a 2-slot baseline / 3-slot maximum inventory;
- inspect/causal-lineage action exists independently of hover;
- no essential right-click, wheel or drag-only command;
- no ordinary frame-perfect capture/spend timing.

Action moments may feel physical, but baseline puzzle success must remain causal rather than dexterity-gated.

---

# 18. Accessibility thesis

Required design constraints:
- direction conveyed by arrow geometry + optional compass/text labels;
- magnitude conveyed through at least two of size/chevrons/pattern/text, never color alone;
- color never carries unique donor/receiver compatibility information;
- reduced motion disables camera shake and excessive impact motion while preserving before/after state;
- all essential sound cues have visual equivalents;
- pause/step or strong slowdown is available for moving-body reasoning where timing otherwise creates a barrier;
- no mandatory rapid input, freehand precision or analog-only aim;
- remappable controls;
- scalable UI and Deck-readable labels;
- causal explanation remains available after animation so players do not need perfect perceptual recall.

Accessibility settings must not silently change core deterministic outcomes unless a separately authored assist rule is explicitly visible and later frozen.

---

# 19. Scope ceiling / explicit 1.0 exclusions

## In scope
- compact authored deterministic cases;
- stylized bounded 2D body/collision system;
- portable impact harvesting and spending;
- fixed visible direction transforms;
- self-launch as part of the same grammar;
- chained secondary collisions;
- bounded multi-room causal puzzles;
- optional final-state mastery/remixes;
- lightweight thematic framing;
- demo.

## Explicitly out of scope for 1.0
- unrestricted realistic rigid-body physics sandbox;
- free-angle vector editor;
- numeric force programming;
- projectile combat campaign;
- enemies requiring combat AI;
- open world;
- procedural infinite puzzle generation as value pillar;
- multiplayer/co-op;
- online leaderboards as design dependency;
- user-generated level editor / Workshop dependency;
- crafting/equipment/loot economy;
- dozens of elemental or modifier token types;
- token rarity/upgrade tiers;
- large inventory management;
- narrative branching/cutscene-heavy campaign;
- photorealistic asset target;
- server/backend requirement;
- generative-AI dependency for content.

A future feature that violates these exclusions requires an explicit design reopen, not implementation convenience.

---

# 20. Product-level empirical gates carried into implementation

These are not missing design rules. They are prototype/playtest obligations inherited from the tournament.

A primitive prototype must demonstrate after one tuning pass:
1. repeated identical state + command sequences produce identical collision/harvest results;
2. ordinary completion requires no unsnapped aiming or reflex timing;
3. **<=20%** of ordinary failures are primarily caused by misunderstanding direction/magnitude presentation;
4. mature play does not use the strongest available impact at every meaningful decision in **>=50%** of successful solutions;
5. blind token permutation stays below approximately **35%** of successful mature actions in observed tests;
6. most representative testers can explain a secondary collision chain without requesting numeric vector UI;
7. players describe the core as reusing/storing collision consequences, not generic arrow matching or generic physics puzzles;
8. source world-state and receiver aftermath remain decision-relevant in mature content;
9. controller/keyboard-only interaction remains substantially as legible as mouse input;
10. quantized physics reads as intentional rules, not unpredictable fake simulation.

If the prototype fails because players cannot understand the metaphor even after a reasonable presentation pass, the concept should be killed/reopened rather than hidden behind more tutorials or finer physics.

---

# 21. Anti-repetition product test

Every later major content band must be able to answer:

> “What changed in the reasoning besides a different room layout?”

The current allowed reasoning axes are:
- choose the right source collision;
- preserve/exhaust a donor intentionally;
- transform direction physically;
- choose an appropriate magnitude band;
- allocate one scarce impact between self/cargo/environment;
- make one collision create another useful collision;
- account for receiver aftermath;
- transport consequences across rooms;
- compress several obvious impacts into one elegant chain.

Phase 5 must reject a campaign that repeatedly asks only `find token of correct arrow and carry it to receiver`.

---

# 22. Product success / failure definition

Success feels like:

> “I needed an upward hit, but instead of hunting for an up-arrow I realized I could use the cart crash downstairs, turn it through the wall socket, launch myself, and make my landing become the hit that opens the exit.”

Failure feels like:
- “I matched arrows to sockets.”
- “I guessed angles until physics worked.”
- “Strong is always best.”
- “I farmed the same collision repeatedly.”
- “I needed a calculator.”
- “The game pretends to be a sandbox but everything behaves inconsistently.”

Later phases must optimize toward the first experience and actively test against the others.

---

# 23. Phase-3 acceptance decision

- Working title retained with naming constraints: **YES**
- Target / non-target player frozen: **YES**
- Platform/commercial frame frozen enough for design: **YES**
- Genre framing frozen: **YES**
- One-sentence hook frozen: **YES**
- Core fantasy frozen: **YES**
- Core player-facing loop frozen: **YES**
- Session structure frozen: **YES**
- Non-negotiable differentiation rule frozen: **YES**
- Primitive vocabulary ceiling frozen enough for Phase 4: **YES**
- Progression/hour-10 depth thesis frozen: **YES**
- Failure/Undo/reset philosophy frozen: **YES**
- Donor exhaustion/duplication philosophy frozen: **YES**
- Presentation/audio/causal-feedback thesis frozen: **YES**
- Player-facing terminology direction frozen: **YES**
- Input/accessibility thesis frozen: **YES**
- Scope ceiling / exclusions frozen: **YES**
- Empirical prototype gates carried forward: **YES**
- Production implementation started: **NO**
- Product Thesis lock: **YES**
- DESIGN COMPLETE: **NO**

## NEXT PHASE
**Phase 4 — Mechanical Architecture.**

The next substantial run must freeze the deterministic gameplay rules that make this thesis implementable without guessing: canonical world/body state, exact collision table semantics, what qualifies as harvestable resolved impact, lineage/duplication/reset rules, donor generation/regeneration classes, token inventory/state, spend legality, receiver and converter families, self-launch semantics, bounded collision-chain resolution order, moving bodies/timing model, objectives/invariants, Undo/Redo/checkpoints, causal ancestry, win/fail/dead-end recovery, balancing knobs, anti-bruteforce structure and a concrete mechanical acceptance-test index. It must preserve 8 directions × 3 bands as the working quantized model unless a documented Phase-4 contradiction proves a smaller vocabulary is necessary; it must not expand toward continuous free-angle physics or numeric vectors.