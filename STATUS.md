# FACTORY STATUS

Last updated: 2026-09-06
Repository: `Mikayilzade/gpt-game-autonomy`
Branch: `game18-phase4-mechanics` (recoverable active branch; main synchronization remains pending)

## Factory state
- Reusable factory rules: **YES**
- Games #001–#005: **DESIGN COMPLETE / migrated**
- Games #006–#017: **DESIGN COMPLETE / migration pending / retained NON-ACTIVE safety archives**
- Current design slot: **Game #018**
- Selected concept: **LOCAL TIME**
- Production implementation inside factory: **NO**

## Continuity / active canon
Game #018 is the only active design slot. Games #001–#017 are exclusion/portfolio history only. Frozen archives #006–#017 are NON-ACTIVE. Round-C runners-up remain killed for this slot.

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

## This run completed — Game #018 Phase 8
- Created canonical `GAME18_TECH_SPEC.md` after reading the complete active authority chain.
- Fresh technical research checked 2026-09-06: Godot official release/archive policy and Steamworks Cloud/demo/Deck documentation.
- Selected Godot 4.7.x stable / GDScript-first as recommended implementation direction; 4.7.2 is current stable while 4.8 is development, with implementation-time revalidation required.
- Separated canonical mutable authority, derived state and presentation state so rendering/animation/physics cannot alter puzzle outcomes.
- Defined versioned non-executable schemas for cases, sockets, footprints, clocks, sites, objects, carriers, rule instances and objectives.
- Translated the Phase-4 Resolve order into an exact deterministic implementation contract.
- Defined canonical structural state identity/hashing and symmetry restrictions.
- Defined validator + exhaustive solver using the same authoritative transition kernel, with exact DEAD certification rules.
- Defined structured reason events and replay as non-authoritative presentation.
- Defined semantic input abstraction and controller focus graph with automated no-trap checks.
- Defined versioned atomic/recoverable profile saves, backup recovery and explicit migration fixtures.
- Defined monotonic/idempotent demo->full import that cannot downgrade stronger full-game progress.
- Defined conservative Steam Cloud policy: machine-local graphics separated; Auto-Cloud preferred initially; divergent active checkpoints preserved rather than silently merged; all public promises require real Steam build validation.
- Defined localization/font/layout contracts and pseudolocalization/CJK QA.
- Defined Deck/performance targets as validation gates rather than promises.
- Defined kernel property tests, LT01–LT06 golden cases, save/cloud fixtures and UI automation.
- Defined data-driven authoring/validator workflow and future 12A–12H implementation dependency order.
- No production implementation started.

## NEXT ACTION — GAME #018 PHASE 9 / WHOLE-GAME SIMULATION ON PAPER
Read all active Game #018 authority, especially `GAME18_MECHANICS.md`, `GAME18_CONTENT.md`, `GAME18_UX.md`, `GAME18_COMMERCIAL.md`, and `GAME18_TECH_SPEC.md`.

Create canonical `GAME18_WHOLE_GAME_SIM.md`. Perform one substantial end-to-end hostile paper simulation, not a summary. At minimum:
1. first boot/accessibility and LT01–LT06 demo minute-by-minute enough to expose teaching contradictions;
2. transition from demo to full game and Case 07 progression;
3. representative full-game walks through Cases 09, 18, 24, 30, 34 and 36 using only frozen grammar;
4. mastery/replay/efficiency loop and whether it remains optional rather than grind;
5. planning/Resolve interruption, Undo Placement, Undo Turn, Restart, quit/load and replay semantics;
6. controller-only and 1280x800 Deck navigation/readability path;
7. localization/pseudolocalization stress on rule cards/reason trace/objectives;
8. demo->full import, clean install, existing full progress, repeated import, corrupted save, offline/cloud and two-device divergence;
9. hostile player behavior: socket scanning, intentional illegal conflicts, repeated Resolve/no-op attempts, brute force, animation skipping, save manipulation expectations;
10. explicitly test whether hour-5 play is still causal reasoning rather than raw socket enumeration;
11. re-evaluate the 36+12 target against Phase-5/7 quality gates; do not preserve counts for quota;
12. maintain a defect/contradiction ledger with severity, authority source and minimal repair. Any authority change must be explicit; do not silently rewrite earlier design.

End with exact targets for Phase 10 Adversarial Review. Do not start production implementation.

## Blockers
**NONE for factory continuation.** Main-branch synchronization remains pending/flaky; Phase 4–8 authority is recoverably retained on `game18-phase4-mechanics`. Do not treat older main state as newer canon.

DESIGN COMPLETE = NO (current active Game #018; Phase 9 next).
