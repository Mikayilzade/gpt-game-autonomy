# FACTORY STATUS

Last updated: 2026-09-06
Repository: `Mikayilzade/gpt-game-autonomy`
Branch: `main`

## Factory state
- Reusable factory rules: **YES**
- Games #001–#005: **DESIGN COMPLETE / migrated**
- Games #006–#017: **DESIGN COMPLETE / migration pending / retained NON-ACTIVE safety archives**
- Current design slot: **Game #018**
- Selected concept: **LOCAL TIME**
- Production implementation inside factory: **NO**

## Continuity / active canon
Game #018 is the only active design slot. Games #001–#017 are exclusion/portfolio history only. Frozen archives #006–#017 are NON-ACTIVE and must not leak canon into #018. Round-C runners-up ONE MORE CHAIR and AFTERIMAGE DELIVERY are killed for this slot and are not backup canon.

## Current phase
**Game #018 — PHASE 8 TECHNICAL SPECIFICATION COMPLETE / PHASE 9 WHOLE-GAME SIMULATION NEXT.**

## Active authority for Game #018
1. `START_HERE.md`
2. `STATUS.md`
3. `GAME_INDEX.md`
4. `GAME18_RESEARCH.md`
5. `GAME18_TOURNAMENT.md`
6. `GAME18_PRODUCT_THESIS.md`
7. `GAME18_MECHANICS.md`
8. `GAME18_CONTENT.md`
9. `GAME18_UX.md`
10. `GAME18_COMMERCIAL.md`
11. `GAME18_TECH_SPEC.md`

## Completed through Phase 7
Phases 1–7 complete: opportunity discovery, tournament selection, product thesis, deterministic mechanical architecture, content architecture, UX/presentation architecture and commercial model.

## This run completed — Game #018 Phase 8
- Added canonical `GAME18_TECH_SPEC.md` on `main`.
- Fresh engine research: Godot 4.7 is supported; 4.7.2 stable released 2026-08-18 while 4.8 remains development. Locked Godot 4.7.x stable/GDScript as baseline direction, with puzzle authority isolated from engine presentation.
- Defined hard Domain/Core, Content, Presentation/Application and Platform boundaries.
- Mapped Phase-4 state and Phase-5 authored schema into stable-ID `CaseDefinition`, `RunState`, and `ProfileState` contracts.
- Defined deterministic Resolve API, normalized serialization, stable state hashing, structured localizable reason traces and iteration-order invariance.
- Defined exact solver as a consumer of the production core, plus content-validator obligations and human-proof boundary.
- Locked versioned atomic saves, last-known-good recovery, definition compatibility and pure schema migrations.
- Locked monotonic/idempotent demo-to-full import that cannot overwrite newer full-game progress.
- Defined Steam Cloud divergence handling: preserve both valid candidates, no silent timestamp winner, safe union only for tested monotonic profile fields, whole-checkpoint choice for divergent in-progress state.
- Defined device-independent input actions, controller/Deck navigation, 1280x800 display target, localization boundaries and animation-vs-logic separation.
- Defined LT01–LT06 golden tests, property/invariant tests, corruption/import/cloud fixtures and fake-platform tests.
- Defined implementation order T0–T9 and technical acceptance criteria for the later dedicated repository.
- No production implementation started.

## NEXT ACTION — GAME #018 PHASE 9 / WHOLE-GAME SIMULATION
Read all active Game #018 authority, especially `GAME18_MECHANICS.md`, `GAME18_CONTENT.md`, `GAME18_UX.md`, `GAME18_COMMERCIAL.md`, and `GAME18_TECH_SPEC.md`.

Perform one substantial end-to-end paper simulation and save canonical `GAME18_SIMULATION.md`. At minimum walk:
1. first boot/settings and LT01–LT06 in exact player order;
2. representative Cases 07–36 across all six chapters, checking proof-shape escalation rather than merely family count;
3. campaign completion and 8 mastery baseline + 4 reserve decision;
4. quit/load/restart/undo/replay and animation skip/crash boundaries;
5. demo-to-full import, repeated import and older-demo/newer-full conflict;
6. Steam offline/cloud divergence/corrupt latest checkpoint recovery;
7. mouse/controller/Steam Deck navigation/readability;
8. hostile behavior: Resolve spam, socket scanning, broad-warning scanning, undo abuse and deliberate budget waste;
9. contradictions among current/persistent predicates, carrier arrival/acceptance, hazards, coupled conditions and save checkpoints;
10. whether 30–36 campaign cases still plausibly sustain distinct human proof shapes.

Repair contradictions canonically rather than handwave. If Phase 9 resolves cleanly, Phase 10 Adversarial Review is next. Do not start production implementation.

## Blockers
**NONE for factory continuation.** Games #006–#017 have pending migrations but remain frozen non-active archives.

DESIGN COMPLETE = NO (current active Game #018; Phase 9 next).
