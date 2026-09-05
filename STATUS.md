# FACTORY STATUS

Last updated: 2026-09-05
Repository: `Mikayilzade/gpt-game-autonomy`
Branch: `main`

## Factory state
- Reusable factory rules: **YES**
- Games #001–#005: **DESIGN COMPLETE / migrated**
- Games #006–#016: **DESIGN COMPLETE / migration pending / retained NON-ACTIVE safety archives**
- Current design slot: **Game #017**
- Selected concept: **THE QUEUE KNOWS**
- Production implementation inside factory: **NO**

## Continuity / active canon
Game #017 is the only active design slot. Games #001–#016 are exclusion/portfolio history only. Frozen archives #006–#016 are NON-ACTIVE and must not leak canon into #017. Game #017 runner-ups and killed candidates are tournament history only and do not supply canon to the selected game.

## Current phase
**Game #017 — PHASE 8 TECHNICAL SPECIFICATION COMPLETE / PHASE 9 WHOLE-GAME SIMULATION NEXT.**

## Active authority for Game #017
1. `START_HERE.md`
2. `STATUS.md`
3. `GAME_INDEX.md`
4. `GAME17_RESEARCH.md`
5. `GAME17_TOURNAMENT.md`
6. `GAME17_ROUND_B.md`
7. `GAME17_ROUND_C.md`
8. `GAME17_PRODUCT_THESIS.md`
9. `GAME17_MECHANICS.md`
10. `GAME17_CONTENT.md`
11. `GAME17_UX_PRESENTATION.md`
12. `GAME17_COMMERCIAL.md`
13. `GAME17_TECHNICAL_SPEC.md`

## This run completed — Game #017 Phase 8 Technical Specification
- Re-read required factory authority and all active Game #017 files.
- Performed fresh engine/platform verification.
- Created canonical `GAME17_TECHNICAL_SPEC.md`.
- Locked the implementation stack, deterministic simulation boundaries, serialized data/save contracts, evaluator/event ordering, offline validator, Type Lens contract, persistence/platform strategy, controller/Deck input abstraction, accessibility/localization boundaries, deterministic testing and implementation order.
- No production implementation was started.

## NEXT ACTION — GAME #017 PHASE 8 / TECHNICAL IMPLEMENTATION SPECIFICATION
Use the full active Game #017 authority through `GAME17_COMMERCIAL.md`. Do not import runner-up mechanics.

Perform one substantial implementation-specification increment without starting production code. At minimum:
1. engine/runtime recommendation and alternatives;
2. deterministic simulation architecture and authoritative state boundaries;
3. exact serialized CaseDefinition / save / evidence schemas;
4. hidden-world handling and no-leak boundaries;
5. evaluator/comparator APIs and event ordering;
6. exhaustive validator/solver architecture and proof artifacts;
7. UI presentation-event separation and Type Lens query contract;
8. input abstraction/controller/Deck implementation contract;
9. persistence, checkpoint, Steam Cloud conflict and demo-save import strategy;
10. localization/accessibility data boundaries;
11. performance budgets for 10 customers / 3 counters and solver offline/runtime separation;
12. test hooks, golden traces, property tests and determinism checks;
13. implementation phase order for the dedicated repository;
14. explicit empirical gates that require a prototype but do not reopen mechanics by default;
15. save canonical `GAME17_TECHNICAL_SPEC.md`, update STATUS/GAME_INDEX, and advance to Phase 9 if complete.

Fresh web research is required only where current engine/platform/tool constraints materially affect the specification.

## Blockers
**NONE for factory continuation.** Pending migrations #006–#016 remain non-blocking.

DESIGN COMPLETE = NO (current active Game #017; Phase 9 next).
