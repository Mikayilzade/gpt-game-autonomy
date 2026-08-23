# GAME #005 — IMPLEMENTATION START HERE

This file is a migration-ready handoff template for the dedicated repository. After migration it should become `IMPLEMENTATION_START_HERE.md`.

## Source of truth
Read in this order:
1. `GAME5_PHASE11_FINAL_FREEZE.md`
2. `GAME5_ENCOUNTER_BLUEPRINTS.md`
3. `GAME5_PHASE11_READINESS_AUDIT.md`
4. `GAME5_PHASE10_AMENDMENTS.md`
5. `GAME5_TECHNICAL_SPEC.md`
6. `GAME5_UX_PRESENTATION.md`
7. `GAME5_CONTENT_ARCHITECTURE.md`
8. `GAME5_MECHANICS.md`
9. `GAME5_ECONOMY_COMMERCIAL.md`
10. `GAME5_PRODUCT_THESIS.md`

History/research files explain why decisions were made but do not override this chain.

## Implementation rule
Do not redesign frozen gameplay for convenience. If a blueprint cannot be implemented under the frozen rules, record the contradiction in `IMPLEMENTATION_STATUS.md` and stop that subsystem rather than inventing a new mechanic.

## Phase sequence
### 12A — Technical bootstrap
- pin documented Godot baseline;
- create deterministic Domain Core/data boundaries;
- implement content schema and validators V01–V20;
- implement traversal/state solver and headless test harness;
- input/persistence/settings skeleton;
- no bulk content.

### 12B — Vertical slice
Build the three empirical fixtures P-A/P-B/P-C plus minimal final-intent camera/input/presentation.

### 12G EARLY EMPIRICAL GATE — MANDATORY BEFORE BULK CONTENT
Although factory numbering lists 12G later, the readability/tactility empirical gate is intentionally executed immediately after the vertical slice. Do not populate the full campaign before this gate passes or receives a bounded documented repair.

### 12C — Core systems complete
All frozen load/carriage/mutation/checkpoint/restart behaviors, controller/accessibility parity and deterministic recovery.

### 12D — Content population
Serialize and implement the exact causal blueprints in `GAME5_ENCOUNTER_BLUEPRINTS.md`; final transforms may vary only while preserving each locked graph.

### 12E — UX/accessibility/target-device
Complete final camera, state grammar, settings, remapping, reduced motion, muted parity, localization readiness and handheld readability.

### 12F — Adversarial QA
Run V01–V20, graph/state solvers, restart/persistence corruption, stale-callback, alternate-solution, anti-enumeration and regression suites.

### 12G — Remaining empirical gates
Campaign repetition, full demo comprehension, late-game readability and representative player testing.

### 12H — Release candidate
Performance, packaging, demo/retail separation, Steam-ready build, final regression and release checklist.

## First NEXT ACTION
Create Phase 12A bootstrap only. Implement the smallest deterministic content/domain foundation capable of expressing P-A, P-B and P-C and running V01–V20 headlessly. Do not start art/content production first.

## Completion
`IMPLEMENTATION COMPLETE = YES` only after 12A–12H acceptance criteria and all mandatory empirical gates are satisfied. Design completion does not equal implementation completion.
