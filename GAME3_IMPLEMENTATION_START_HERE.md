# BORROWED COLLISION — IMPLEMENTATION START HERE

Status: **DESIGN FROZEN / IMPLEMENTATION NOT STARTED**
Intended destination: `Mikayilzade/borrowed-collision`

This repository/package is the complete design handoff for Borrowed Collision. Implementation must follow frozen design rather than inventing or simplifying gameplay for convenience.

## Required read order
1. `GAME3_PHASE11_FINAL_FREEZE.md`
2. `GAME3_ADVERSARIAL_REVIEW.md`
3. `GAME3_MECHANICAL_ARCHITECTURE.md`
4. `GAME3_CONTENT_ARCHITECTURE.md`
5. `GAME3_UX_PRESENTATION_ARCHITECTURE.md`
6. `GAME3_ECONOMY_COMMERCIAL.md`
7. `GAME3_TECHNICAL_SPEC.md`
8. `GAME3_PRODUCT_THESIS.md`
9. `GAME3_WHOLE_GAME_SIMULATION.md`
10. tournament/research files only when historical rationale is needed

When files disagree, obey the authority order in `GAME3_PHASE11_FINAL_FREEZE.md`.

Before creating or modifying GitHub Actions, read `CI_NOTIFICATION_POLICY.md` in the dedicated repository.

## Autonomous implementation protocol
A continuation prompt means:
1. read `IMPLEMENTATION_STATUS.md`;
2. read the frozen files needed for the exact current subsystem;
3. perform one substantial, recoverable implementation increment;
4. run the most relevant deterministic/headless/local checks available;
5. save coherent working changes to GitHub;
6. update `IMPLEMENTATION_STATUS.md` with completed work, tests, blockers, canonical contradictions and exact NEXT ACTION;
7. never leave meaningful project state only in chat.

Do not report `IMPLEMENTATION COMPLETE = YES` until Phase 12A–12H completion gates are all satisfied.

---

# Phase 12A — Technical Bootstrap

Build the smallest deterministic project foundation.

Required:
- pin Godot 4.7.1-stable initially;
- project boots to a minimal non-gameplay shell;
- Domain Core separated from presentation;
- stable ID/content-version types;
- canonical serialization/hash;
- semantic command envelope with command ID + expected revision/hash;
- minimal `CaseDefinition`/`CaseState` data model;
- one authored movement lane/collision boundary representation;
- deterministic test/headless command;
- save-envelope skeleton with temp/primary/backup validation;
- semantic input-action registry;
- no production content beyond tiny fixtures.

Exit gate:
- repeated identical fixture command sequence yields identical canonical hash;
- headless tests run without presentation scenes;
- stale/duplicate command skeleton is testable;
- no engine-physics contact is gameplay authority.

# Phase 12B — Vertical Slice

Build a DEMO01–DEMO03-like complete loop:
- one collision -> stable impact pickup;
- collect;
- direction/magnitude display;
- one transform;
- one R1/R2/R3 receiver path;
- legal adverse spend;
- exact Undo/Redo;
- causal lineage explanation;
- mouse+keyboard and controller semantic input;
- durable checkpoint/recovery.

Exit gate:
- tiny slice is playable end-to-end and deterministic;
- lineage emits once;
- duplicate Collect/Spend cannot duplicate state;
- presentation speed/reduced motion does not change domain hash.

# Phase 12C — Core Systems Complete

Implement all frozen core grammar:
- 8 directions / 3 bands;
- R1–R8;
- QUARTER_TURN/REVERSE/MIRROR/DAMPER;
- EXHAUSTIBLE/RESETTABLE/CYCLIC_WEAK/CHAIN_GENERATED;
- simultaneous collision grouping;
- bounded chain resolution and safe chain-limit state;
- self-launch authored outcomes;
- moving receive windows;
- 2-slot default / justified 3-slot case capacity;
- world pickups/multi-room traversal;
- objectives/invariants/mastery predicates;
- all P10 authoring/validation constraints representable.

Exit gate:
- canonical mechanics acceptance suite passes;
- no arbitrary case gameplay callbacks exist;
- same-step ambiguous physical state is rejected by content compiler.

# Phase 12D — Content Population

Build validated data-driven content:
- C01–C34;
- DEMO01–DEMO05;
- R01–R10;
- known baseline solution fixture for every main/demo/remix case;
- known mastery fixture where mastery exists;
- prerequisite/tutorial graph;
- causal-skeleton metadata;
- reasoning-isomorphism report;
- renewable escalation checks;
- remix changed-dependency proof;
- three-slot justification where used.

Exit gate:
- every shipped case compiles and known fixture completes;
- C34 reachable with zero mastery/remix requirement;
- no P10-R1..R16 content violation remains.

# Phase 12E — UX / Accessibility / Controller / Deck

Complete all required player paths:
- world-first in-case layout;
- impact identity hierarchy;
- capture-source affordance;
- donor/receiver/lineage inspect cards;
- causal ribbon <=5 material nodes / <=2 siblings by default;
- deterministic authored focus graph;
- mouse+keyboard, keyboard-only, controller-only;
- 1280×800 Deck target;
- remapping + Reset Controls;
- scalable UI;
- no color/audio-only information;
- reduced motion/flash;
- Pause/Step/slowdown;
- no reflex catch/aim requirement;
- localization/pseudolocalization pass.

Exit gate:
- required cases completable without pointer input;
- Deck/default UI remains readable;
- accessibility settings cannot change deterministic outcomes.

# Phase 12F — Adversarial QA

Attack:
- duplicate commands;
- stale revision/hash;
- save crash at every transaction stage;
- lineage duplication;
- donor reset/generation atomicity;
- renewable stronger-output cycles;
- transform cycles;
- simultaneous collisions;
- chain ceiling;
- Undo branch/Redo truncation;
- world-pickup recovery;
- divergent Cloud active branches;
- demo import replay/idempotency;
- focus graph reachability;
- controller ambiguity;
- accidental max-force dominance.

Exit gate:
- no known state corruption/duplication exploit;
- every failure reproduces from a deterministic replay/support bundle.

# Phase 12G — Empirical Gates

Run the retained E10-01..E10-11 playtest/prototype gates.

Critical product kill/repair questions:
- do mature players reason about source/world-state, not only arrows?
- is direction/magnitude/source readable at Deck/grayscale/no-audio?
- is STRONG non-dominant?
- is retrieval/backtracking acceptable?
- does self-launch read as authored consequence-transfer rather than missing platformer controls?
- does Pause/Step preserve challenge?
- does causal UI explain lineage/failure?
- is dense controller focus predictable?
- do Acts III–V feel cognitively distinct?
- does persistence fault injection pass?
- does demo communicate the full hook and support perceived value?

If a gate fails, apply the smallest documented canonical amendment. Do not invent token types to patch repetition.

# Phase 12H — Release Candidate

Required before completion:
- all main/demo/remix content passes regression;
- performance budgets verified on target reference hardware;
- save migrations/recovery verified;
- Steam Cloud/Achievements/demo integration verified or explicitly removed with documented release-safe reason;
- controller/Deck/localization regression passes;
- demo-to-full import validated;
- release build packaging/export smoke tests pass;
- known empirical gate failures resolved/accepted explicitly;
- final implementation status records `IMPLEMENTATION COMPLETE = YES` only after all completion checks.

---

## Canonical amendment rule
Implementation may repair a proven contradiction only by:
1. documenting the contradiction and reproduction;
2. identifying the smallest affected frozen section;
3. preferring clarification/narrowing/cut over feature addition;
4. updating tests/content data together;
5. recording the amendment in implementation status/changelog.

Never redesign the game silently for implementation convenience.
