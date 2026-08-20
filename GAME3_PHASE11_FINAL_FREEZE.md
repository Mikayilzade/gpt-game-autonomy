# GAME #003 — BORROWED COLLISION — PHASE 11 FINAL SPECIFICATION FREEZE

Last updated: 2026-08-20
Factory run: **15**
Phase: **11 — Specification Freeze**
Status: **FINAL CANONICAL FREEZE / DESIGN COMPLETE**
Production implementation started: **NO**

This file closes the design stage for Game #003. It reconciles the complete Phase-3..10 specification, makes the Phase-9/10 repairs authoritative, separates gameplay canon from implementation freedom, and records a fresh implementation-readiness audit.

---

# 1. Final decision

- Product thesis internally consistent: **YES**
- Mechanical architecture deterministic enough to implement: **YES**
- Content architecture bounded/data-driven: **YES**
- UX/input/accessibility paths specified: **YES**
- Economy/progression/commercial boundaries specified: **YES**
- Technical/persistence architecture specified: **YES**
- Whole-game simulation complete: **YES**
- Adversarial review complete: **YES**
- P9-R1 reconciliation incorporated: **YES**
- P10-R1..P10-R16 incorporated: **YES**
- Phase-10 persistence/simultaneous-collision/chain-ceiling tightenings incorporated: **YES**
- Fresh-session implementation-readiness audit: **PASS — 40/40**
- Remaining uncertainty limited to explicit empirical gates: **YES**
- Specification freeze: **YES**
- **DESIGN COMPLETE: YES**
- Dedicated implementation repository migration: **NOT YET — NEXT GATE**
- Production implementation started: **NO**

The factory may proceed to migration, but Game #003 files must remain here until the dedicated repository has been populated and verified.

---

# 2. Final authority order

For implementation-sensitive conflicts, use this precedence:

1. `GAME3_PHASE11_FINAL_FREEZE.md`
2. `GAME3_ADVERSARIAL_REVIEW.md` — especially P10-R1..P10-R16 and Phase-10 persistence/collision/chain tightenings
3. `GAME3_MECHANICAL_ARCHITECTURE.md`
4. `GAME3_CONTENT_ARCHITECTURE.md`
5. `GAME3_UX_PRESENTATION_ARCHITECTURE.md`
6. `GAME3_ECONOMY_COMMERCIAL.md`
7. `GAME3_TECHNICAL_SPEC.md`
8. `GAME3_PRODUCT_THESIS.md`
9. `GAME3_WHOLE_GAME_SIMULATION.md` as validation/experience evidence
10. tournament/research files as historical selection evidence only

Where a later repair narrows earlier wording, the later repair wins. Tournament examples never override frozen mechanics.

---

# 3. Frozen product identity

Working title: **Borrowed Collision**.

One-sentence hook:

> **Steal the force from one crash and spend it somewhere else: harvest collisions as portable impacts, route them through physical sockets, and reuse those consequences on carts, doors, cargo — or yourself.**

Non-negotiable differentiation rule:

> **A resolved physical consequence becomes a portable resource, and the world-state that created and receives that consequence must continue to matter.**

The game is a premium single-player systemic causal puzzle / stylized physics puzzle for PC/Steam first. It is not a rigid-body sandbox, trajectory editor, vector-programming game, combat game, inventory RPG, factory game, open world, live service or platformer-first product.

---

# 4. Frozen impact grammar

A portable impact contains only:
- one of 8 snapped compass directions;
- one magnitude band: WEAK / MEDIUM / STRONG;
- source lineage/provenance;
- transform history for explanation;
- availability state.

It contains no numeric force/vector components, elements, rarity, durability, upgrades, random affixes or hidden modifiers.

Transform families are exactly:
1. QUARTER_TURN;
2. REVERSE;
3. MIRROR with visible fixed axis;
4. DAMPER, which reduces magnitude exactly one band and never increases it.

No free-angle rotation/aiming exists in baseline play.

Portable-impact capacity is **2 by default**. Capacity **3** is case-authored only, late, rare and subject to P10-R11. It is never a profile upgrade.

---

# 5. Authoritative physical model

Borrowed Collision uses a deterministic authored body/lane/collision-boundary graph, not engine-contact physics as gameplay truth.

Canonical bodies exist on authored nodes/boundaries and carry discrete:
- direction;
- magnitude band;
- mass class;
- durability/status flags;
- active lineage ancestry when applicable.

Presentation may interpolate attractive motion between canonical boundaries, but frame delta, tween position, collision callbacks, float contact ordering, scene-tree ordering and renderer state never decide gameplay.

Every reachable same-step collision state must compile to exactly one deterministic registered outcome.

---

# 6. Canonical collision / transaction semantics

One accepted domain-changing command resolves atomically through the frozen ordering:

1. validate semantic command against exact pre-state/revision/hash;
2. commit selected domain action exactly once;
3. build movement intents from one shared start-of-step state;
4. form simultaneous collision groups before mutation;
5. resolve each group through registered deterministic outcome rules;
6. apply body state;
7. emit eligible lineage-bound harvest output;
8. apply receiver/world triggers;
9. evaluate objectives/invariants/mastery-relevant facts;
10. continue bounded movement chain while active bodies remain;
11. settle or enter deterministic chain-limit safe state;
12. persist only the full committed transaction checkpoint;
13. release presentation/control.

A body may not belong to two separately resolved collision groups in the same canonical step. Stable IDs may serialize already-disjoint groups but may not choose physical outcomes.

Hard chain ceiling remains **24 canonical movement steps**. Known shipped solutions should not depend on reaching it. If a legal command does reach it, the result is deterministic `CHAIN_LIMIT_REACHED`; no half-applied group may persist.

---

# 7. Harvest / lineage / donor generation freeze

Eligible collision output becomes a **stable world pickup**. There is no reflex catch mechanic.

Each collision lineage emits at most one portable impact. Animation replay, duplicate commands, save/load, room transitions, Pause/Step and UI retries cannot emit a duplicate.

Donor regeneration classes are exactly:
- EXHAUSTIBLE;
- RESETTABLE;
- CYCLIC_WEAK;
- CHAIN_GENERATED.

RESETTABLE donor generation increment, its visible reset world-state consequence, and any later emitted lineage derived from that generation must be transactionally coherent. There is no save boundary where generation advanced but the reset consequence did not.

CYCLIC_WEAK may regenerate indefinitely only when its sustainably repeatable net harvest envelope remains WEAK. Renewable escalation to unbounded MEDIUM/STRONG without bounded visible cost is invalid content.

RESETTABLE stronger regeneration is valid only when each reset imposes a strategically material visible world-state/access/routing/receiver/body consequence. A free ammo button is invalid mature content.

---

# 8. Receiver / transform families

Base mechanical family ceiling remains **R1–R8**:
- R1 Ordinary Mover;
- R2 Fragile Receiver;
- R3 Band-Window Mechanism;
- R4 Converter Socket;
- R5 Damper;
- R6 Self-Launch Receiver;
- R7 Chain-Producing Body;
- R8 Anchored Trigger / Impact Door.

A body normally exposes at most two materially relevant family semantics at once.

Legal-but-adverse spends commit and teach. Examples: STRONG breaks a fragile receiver, WEAK undershoots, correct direction causes an undesirable route. Structurally incompatible spends reject before mutation/consumption with exact reason.

Transforms preserve impact identity/source lineage and never duplicate. Required known baseline solutions normally use <=2 transforms between material world-state events; >2 requires transform topology itself to be the causal lesson. No baseline fixture may require >4 consecutive transforms without a material state event.

---

# 9. Self-launch and moving-window freeze

Self-launch is ordinary consequence-transfer grammar, not a second platforming system.

Every self-launch exposes a finite authored set of legal outcomes before commit, mapping direction/band to an authored launch lane/landing/collision boundary. No analog aim, fine power adjustment, air control, double jump or frame-timed release exists.

Moving receive windows are canonical discrete states. Required baseline play must expose inspectable window/state information. Spend legality is checked against canonical window state, never animation interpolation.

Pause, Step and slowdown are legitimate presentation/accessibility tools and never invalidate completion, mastery or ordinary achievements. If Step trivializes a case because reaction speed was the challenge, the content is invalid.

---

# 10. Undo / Redo / history freeze

Undo restores an exact canonical pre-transaction checkpoint, including body state, impacts, donor generations, emitted-lineage records, objectives, inventory and history cursor. It is not inverse simulation.

Redo restores/replays the exact stored transaction only while the branch remains valid. A new accepted action after Undo truncates active Redo history.

Raw Undo, failed probes, restarts, Pause/Step, slowdown, elapsed time and input device are not baseline/mastery scoring dimensions.

---

# 11. Mature-content identity repairs — P10-R1..R16

## P10-R1 — provenance/world-state dependency
Every C15–C34 case and remix must make at least two world-state/provenance dependencies materially relevant, with at least one tied to donor availability/reset/source distinction/receiver aftermath/secondary lineage. If anonymous direction+band tokens preserve the same dominant solution reasoning, the content fails.

## P10-R2 — impact identity hierarchy
Default visual priority is direction -> magnitude -> provenance -> transform-history detail.

## P10-R3 — capture-source affordance budget
Capture-enabled sources use one consistent bounded affordance family. Capture state must be clear without turning the world into glowing loot markers.

## P10-R4 — renewable escalation
Bounded validator search classifies sustainably repeatable output of every RESETTABLE/CYCLIC_WEAK cycle. Infinite stronger output without material bounded cost is invalid.

## P10-R5 — strong-choice distribution
From C15 onward, each five-case window must include meaningful WEAK-preferred and MEDIUM-preferred baseline reasoning. STRONG cannot become a monotonic heuristic.

## P10-R6 — meaningful reset
Every strategically repeated RESETTABLE source must change meaningful access/routing/receiver/body/protected/future-donor state.

## P10-R7 — transform meaningfulness
Normally <=2 transforms between material events; no >4 consecutive transforms in known baseline fixture without material state event.

## P10-R8 — solved-route traversal compression
Presentation may compress retrieval only when the entire already-visited canonical route is state-inert, has no unresolved moving/window interaction, and executing individual traversal commands would produce the same canonical final player/pickup state. Compression never teleports impacts across unresolved dependencies.

## P10-R9 — self-launch authored outcomes
Self-launch uses finite snapped outcomes; mastery measures causal allocation/lineage, not dexterity.

## P10-R10 — moving-window legibility
Canonical state/window is visible/inspectable; Pause/Step/slowdown remain fully valid.

## P10-R11 — three-slot justification
Capacity 3 requires explicit data justification and genuine simultaneous-lineage ordering. Phase-10 target: <=4 main campaign cases unless a later canonical amendment proves need.

## P10-R12 — causal presentation budget
Default relevant causal ribbon <=5 material nodes and <=2 visible sibling branches. It may collapse inert movement and consecutive transform detail, but never source collision, lineage change or selected final consequence.

## P10-R13 — deterministic authored focus graph
Every room compiles a semantic focus graph independent of zoom, animation interpolation, scene/hash order or float-nearest ambiguity. Required interactables are keyboard/controller reachable; author overrides resolve ambiguous auto-neighbors.

## P10-R14 — reasoning-isomorphism audit
Every C15–C34 known solution character records an abstract causal skeleton. No consecutive 3-case window may share one dominant skeleton; no 5-case window may contain fewer than 3 materially distinct skeleton families.

## P10-R15 — mastery distinction
Every mastery stores `mastery_distinction_note` and a known mastery fixture showing a materially different causal character through source, lineage, preservation, allocation, compression or real temporal state.

## P10-R16 — remix dependency proof
Each remix stores source/remix dominant skeleton plus changed causal dependency. Direction/band/start/theme/threshold changes alone do not constitute remix novelty.

---

# 12. Campaign / progression freeze

Main campaign target: **34 authored cases, C01–C34**.

Pre-freeze tolerance from Phase 5 is no longer a casual production option after this final freeze. Implementation/content production should target 34; changing the count requires a documented canonical amendment with pacing/value evidence.

Teaching order remains:
- C01 collision -> portable impact;
- C02 direction;
- C03 quarter-turn;
- C04 magnitude categories;
- C05 strong can be wrong / fragility;
- C06 reverse/mirror;
- C07 secondary lineage;
- C08 two-token ordering;
- C09 exhaustible provenance;
- C10 meaningful RESETTABLE;
- C11 damper;
- C12 self-launch;
- C13 CYCLIC_WEAK;
- C14 moving receiver;
- C15+ no new primitive grammar.

Campaign unlock graph is the exact Phase-7 graph. C34 remains reachable with zero mastery and zero remix completion.

There is no XP, currency, lives, skill tree, impact upgrade, rarity, permanent inventory upgrade or grind gate.

---

# 13. Remix reconciliation — P9-R1

1.0 contains exactly **10 target remix cases** using the later Phase-7 three-pack structure:
- R01–R03 unlock when C14 is cleared;
- R04–R07 unlock when C28 is cleared;
- R08–R10 unlock when C34 is cleared.

This supersedes Phase-5 historical two-pack wording only. Phase-5 remix validity/data requirements remain in force, strengthened by P10-R16.

Every pack must represent materially different reasoning skeletons; R01–R03 must all differ materially.

---

# 14. Mastery / hints / retention freeze

Mastery families remain:
- Causal Compression;
- Preservation;
- Resource Discipline;
- Stable Causality.

Mastery is optional, never unlocks power, never gates C34 and never scores raw Undo/time/accessibility use.

Hints change information only:
- H1 Rule Reminder;
- H2 Causal Conflict Focus;
- H3 Directional Guidance at family/room/causal-category level;
- H4 explicit opt-in authored Solution Guidance.

Hints do not alter collision/token/lineage/receiver/deterministic rules. No default no-hints prestige achievement exists.

Retention excludes dailies, streaks, login rewards, rotating challenges, FOMO, energy, battle pass, ads, microtransactions and endless filler.

---

# 15. Demo freeze

The demo uses exactly five authored demo nodes:
1. DEMO01 — collision -> portable impact;
2. DEMO02 — physical direction transform;
3. DEMO03 — magnitude suitability / stronger is not automatically better;
4. DEMO04 — provenance/source availability and self-launch/physical consequence;
5. DEMO05 — deliberate secondary collision/new lineage that is reused.

Target remains 15–25 minutes. Demo is invalid if the player does not experience all five commercial proof conditions before the end.

Demo-to-full import requires an explicit versioned mapping table. Import is monotonic and idempotent. Compatible settings may transfer independently. No equivalence is inferred from names alone.

---

# 16. UX / accessibility freeze

All required baseline play must be completable through:
- mouse + keyboard;
- keyboard-only;
- controller-only;
- Steam Deck built-in controls at 1280×800 target layout.

There is no mandatory hover, right-click, mouse wheel, free-angle analog aim, drag-only precision, timed catch, frame-perfect spend, audio-only state or color-only state.

Impact identity must remain legible at Deck size, grayscale/no-audio/reduced motion. Direction is the strongest visual signal; magnitude uses redundant chevrons/body treatment/text; provenance remains inspectable.

The physical world remains the dominant play surface. Inventory remains a compact 2–3 slot impact belt, never a modal RPG inventory.

Causal explanation stays available after animation so success/failure does not depend on perceptual memory.

---

# 17. Persistence / Cloud / demo import freeze

Persistent domains remain separated conceptually into settings, profile progress and active case/recovery state.

Canonical rules:
- versioned save envelopes;
- checksum/hash validation;
- primary/temp/backup recovery generations;
- full domain transaction boundary persistence;
- no half-collision-chain save;
- no half-consumed impact save;
- donor generation/reset consequence/harvest emission stay transactionally coherent;
- duplicate commands idempotent;
- stale revision/hash rejected before mutation;
- profile clears/tutorial tags/mastery/remix facts merge monotonically when compatible;
- divergent active-case branches never synthesize a hybrid state;
- Steam/platform outage never blocks offline local play/save/completion.

Cloud is a platform adapter, not gameplay authority.

---

# 18. Technical direction freeze

Implementation target:
- **Godot 4.7.1-stable** pinned initially;
- standard build;
- GDScript-first;
- 2D Control/Canvas presentation;
- Compatibility renderer unless measured presentation needs justify Mobile;
- deterministic Domain Core separated from Application Services, Presentation and Platform Adapters;
- no engine physics contacts as domain truth;
- no scene transforms/frame timing/randomness/hash iteration as gameplay inputs;
- semantic action/input layer;
- localization-token-based content;
- deterministic content compiler/validator;
- headless replay/fixture harness from the start.

A later engine patch upgrade is implementation-flexible only after a recorded compatibility pass. It may not silently alter deterministic behavior.

---

# 19. Required validator families

Implementation must provide validation sufficient to cover:
- stable IDs/references;
- room/lane/collision graph structure;
- simultaneous collision-group completeness;
- collision-table registration;
- donor regeneration/generation contracts;
- one-harvest lineage invariant;
- renewable escalation search;
- receiver compatibility/band/window contracts;
- transform graph and transform-cycle report;
- known baseline solution replay;
- objective/invariant/mastery evaluation;
- progression/tutorial prerequisite graph;
- deterministic focus-graph reachability;
- three-slot justification;
- reasoning-transformation diversity;
- reasoning-isomorphism/causal-skeleton report;
- remix dependency comparison;
- localization/presentation required-token coverage;
- persistence/idempotency/fault-injection fixtures.

Arbitrary per-case gameplay callbacks/scripts are forbidden.

---

# 20. Fresh implementation-readiness audit — 40/40

1. Product fantasy unambiguous: **PASS**
2. Primary repeated player verb defined: **PASS**
3. Impact identity fully bounded: **PASS**
4. Transform families bounded: **PASS**
5. Receiver/device families bounded: **PASS**
6. Donor regeneration classes bounded: **PASS**
7. Authoritative state source defined: **PASS**
8. Motion representation defined: **PASS**
9. Collision grouping/resolution order defined: **PASS**
10. Same-step ambiguity handling defined: **PASS**
11. Chain ceiling behavior defined: **PASS**
12. Harvest eligibility/pickup semantics defined: **PASS**
13. Lineage/one-emission semantics defined: **PASS**
14. Renewable escalation constraint defined: **PASS**
15. Receiver legal/adverse/illegal semantics defined: **PASS**
16. Transform identity/history semantics defined: **PASS**
17. Self-launch semantics defined: **PASS**
18. Moving-window semantics defined: **PASS**
19. Inventory capacity semantics defined: **PASS**
20. Undo/Redo/history semantics defined: **PASS**
21. Objective/invariant evaluation families available: **PASS**
22. Campaign count/teaching order defined: **PASS**
23. Campaign unlock graph defined: **PASS**
24. Mastery families/validity defined: **PASS**
25. Remix count/unlock/changed-dependency rule defined: **PASS**
26. Demo content/proof boundary defined: **PASS**
27. Hint/assist rules defined: **PASS**
28. Mouse+keyboard path defined: **PASS**
29. Keyboard-only path defined: **PASS**
30. Controller/Deck path defined: **PASS**
31. Accessibility semantics defined: **PASS**
32. Causal explanation compression defined: **PASS**
33. Focus navigation determinism defined: **PASS**
34. Save/recovery transaction boundary defined: **PASS**
35. Cloud branch/merge boundary defined: **PASS**
36. Demo import safety defined: **PASS**
37. Content schema/validator obligations defined: **PASS**
38. Technical architecture and implementation order defined: **PASS**
39. Failure/recovery/idempotency edge cases defined: **PASS**
40. Remaining unknowns are empirical rather than missing rules: **PASS**

A fresh implementation session should not need to invent important gameplay to begin Phase 12A.

---

# 21. Empirical gates retained after freeze

The following remain prototype/playtest/release validation, not missing design:
- E10-01 mature players reason in source/world-state terms, not only arrows;
- E10-02 direction/magnitude/capture-source readability at Deck/grayscale/no-audio/reduced motion;
- E10-03 strongest-impact dominance remains below inherited failure threshold;
- E10-04 solved-room pickup retrieval is not dominant friction;
- E10-05 self-launch reads as authored consequence transfer, not missing platformer controls;
- E10-06 Pause/Step preserves causal challenge and removes reflex interpretation;
- E10-07 compressed causal UI explains lineage/failure;
- E10-08 controller/keyboard dense-room focus is predictable;
- E10-09 hour-3/hour-10 cases feel causally distinct;
- E10-10 persistence/idempotency/fault-injection passes;
- E10-11 demo communicates full hook and release-time value supports final price.

These gates may cause content cuts, UX repair or documented canonical amendment during implementation. They do not justify invention of new token properties or mechanics.

---

# 22. Implementation-flexible choices

A fresh implementation team may choose these without design reopen, provided frozen behavior remains identical:
- internal file/folder/class names;
- exact GDScript object organization inside the frozen architecture boundaries;
- JSON vs Resource-like human-readable source format for case authoring, if canonical compiled schema/validation remains equivalent;
- exact canonical hash algorithm, if versioned and stable;
- compression/delta strategy for history/save storage, if exact restore is preserved;
- exact animation curves/timings, if they never alter domain result;
- non-authoritative world interpolation/splines;
- art style details inside the frozen stylized/discrete presentation thesis;
- exact audio assets;
- platform SDK wrapper choice;
- Steam Cloud Auto-Cloud vs explicit adapter details, provided conflict/recovery semantics remain safe;
- internal test framework/library;
- exact implementation of semantic focus auto-generation before authored overrides;
- performance optimization strategy after equivalence tests exist;
- release-time price within or outside the design-time hypothesis after current-market/perceived-value review.

These choices may not introduce new gameplay authority.

---

# 23. Explicit non-goals at freeze

Do not add for 1.0 without canonical reopen:
- continuous physics sandbox;
- free-angle vectors;
- numeric force programming;
- combat/enemy AI campaign;
- elemental impacts;
- impact rarity/upgrades;
- crafting/equipment;
- large inventory;
- profile capacity progression;
- procedural infinite campaign;
- multiplayer/co-op;
- Workshop/UGC dependency;
- leaderboards as required value;
- proprietary online account;
- live-service retention;
- open world;
- mandatory reflex capture/timing;
- arbitrary per-case scripts.

---

# 24. Migration gate

Intended dedicated repository name: **`Mikayilzade/borrowed-collision`**.

As of the freeze run, targeted repository search did not find an existing repository with that exact intended name.

Before factory cleanup:
1. create/use `Mikayilzade/borrowed-collision` with `main`;
2. copy all canonical Game #003 files and selection/validation history;
3. preserve final-freeze content hash/SHA where practical;
4. copy/rename prepared handoff files to destination root;
5. add destination README pointing first to `IMPLEMENTATION_START_HERE.md`;
6. verify `GAME3_PHASE11_FINAL_FREEZE.md` content-identical to factory source;
7. verify authority chain is self-contained in destination;
8. update `IMPLEMENTATION_STATUS.md` to migration complete / Phase 12A next;
9. update factory `GAME_INDEX.md` with title/repository;
10. only then delete all `GAME3_*` files from factory and reset `STATUS.md` for Game #004.

Until verification passes, the factory remains the authoritative home of Game #003.

---

# 25. Final phase decision

**Phase 11 Specification Freeze: COMPLETE.**

**DESIGN COMPLETE = YES.**

Production implementation remains **NOT STARTED**.

The only next step is safe dedicated-repository migration and autonomous implementation handoff verification; not additional design expansion.