# FACTORY STATUS

Last updated: 2026-08-30
Repository: `Mikayilzade/gpt-game-autonomy`
Branch: `main`

## Factory state
- Reusable factory rules: **YES**
- Games #001–#005: **DESIGN COMPLETE / migrated**
- Game #006 Stitchspace: **DESIGN COMPLETE / migration pending / retained non-active safety archive**
- Game #007 Last Known Shape: **DESIGN COMPLETE / migration pending / retained non-active safety archive**
- Current design slot: **Game #008**
- Selected Game #008 concept: **G8C02 Locksmith's Margin**
- Production implementation inside factory: **NO**

## Continuity / active-canon rule
Only Game #008 files named below are active game canon. `GAME6_*` and `GAME7_*` remain frozen non-active safety archives and must not contaminate Game #008. Rejected Game #008 concepts are tournament history only.

## Current phase
**Game #008 — PHASE 8 TECHNICAL IMPLEMENTATION SPECIFICATION COMPLETE / PHASE 9 READY.**

## Active authority for Game #008
1. `START_HERE.md`
2. `STATUS.md`
3. `GAME_INDEX.md`
4. `GAME8_RESEARCH.md`
5. `GAME8_TOURNAMENT.md`
6. `GAME8_TOURNAMENT_RUN2.md`
7. `GAME8_TOURNAMENT_FINAL.md`
8. `GAME8_PRODUCT_THESIS.md`
9. `GAME8_MECHANICAL_ARCHITECTURE.md`
10. `GAME8_CONTENT_ARCHITECTURE.md`
11. `GAME8_UX_PRESENTATION.md`
12. `GAME8_COMMERCIAL_MODEL.md`
13. `GAME8_TECHNICAL_SPECIFICATION.md`

## This run completed
- Read `START_HERE.md`, prior `STATUS.md`, `GAME_INDEX.md`, and every active Game #008 authority file named by prior status; resumed exactly from Phase-8 NEXT ACTION.
- Created `GAME8_TECHNICAL_SPECIFICATION.md` as complete Phase-8 implementation authority without starting production code.
- Fresh engine research on 2026-08-30 confirmed **Godot 4.7.2-stable (released 2026-08-18)** remains current stable 4.x while **Godot 4.8-dev4 (2026-08-26)** is still preview/development; froze initial implementation baseline at **Godot 4.7.2-stable / GDScript-first**.
- Defined strict **Domain Core / Presentation-Application / Platform Services** boundaries; animation, mesh geometry, physics and Steam callbacks cannot decide fit, knowledge, access or solve state.
- Defined conceptual immutable case data and authoritative runtime models for cases, blanks, locks/accepted bitsets, access predicates, puzzle state, knowledge observations, action records, campaign progress and settings.
- Defined deterministic reducer ordering for FILE, TEST+OPEN/access effects, solve commit, Undo/Redo and Restart, including idempotent repeated-open/achievement behavior.
- Defined omniscient and information-respecting solver modes, canonical future-state/knowledge keys, safe blank symmetry, runtime proof-only softlock semantics, authoring validator stages and duplicate/isomorphism signatures.
- Defined versioned persistence with atomic temp/backup replacement, complete current-case action history, corruption recovery, explicit schema migrations, case-content mismatch handling and local-first Cloud conflict semantics.
- Defined separate allowlisted demo->full transfer rather than importing arbitrary demo PuzzleState; import and achievement reconciliation are idempotent.
- Defined Steam/platform abstractions for achievements, Cloud and glyph/platform availability with full offline graceful degradation.
- Defined semantic input/focus architecture, localization-ready string/font/layout boundaries, Steam Deck-class performance constraints and non-authoritative background solver requirements.
- Defined future dedicated-repo implementation sequence 12A–12H from headless bootstrap through vertical slice, systems/content, UX/platform, adversarial QA, empirical gates and RC.
- Added **120 technical acceptance tests** covering authority, FILE/TEST, knowledge, access, history, solver, persistence, Cloud, demo import, input/accessibility, localization/performance and regression.

## Retained migration state
### Game #006 — Stitchspace
DESIGN COMPLETE = YES; preferred repo `Mikayilzade/stitchspace`; migration pending, non-blocking.

### Game #007 — Last Known Shape
DESIGN COMPLETE = YES; preferred repo `Mikayilzade/last-known-shape`; migration pending, non-blocking.

## NEXT ACTION — GAME #008 PHASE 9 WHOLE-GAME SIMULATION ON PAPER
Perform one substantial end-to-end hostile paper simulation and repair contradictions in their owning authority files:
1. simulate first boot/profile creation, settings/accessibility/controller detection and C01 entry;
2. simulate D01–D06 as a fresh demo player, including first failed TEST, first FILE preview/commit, Undo, same-key multi-lock payoff, completion CTA and demo transfer;
3. simulate C01–C06 tutorial campaign with both intended and wasteful/repetitive TEST behavior;
4. simulate C07–C12 partition/diagnostic play, including a player who specializes too early, Undo/Redo branches and knowledge-ledger correctness;
5. simulate C13–C19 master branches/wear, especially BETWEEN_BRANCHES and broad tolerance readability without hidden accepted-set leakage;
6. simulate C20–C26 access-order/diagnostic conversion, including reopening locks, gating changes and identical-vector/different-history blanks;
7. simulate C27–C32 late synthesis and the maximum normal 3 blanks/6 locks/6 columns state; verify no UI/domain/content ceiling contradiction;
8. simulate solved review, mastery replay, alternate partition, achievements and case unlock clusters with idempotency;
9. simulate save after every meaningful state boundary, crash during FILE/TEST animation, corrupted primary save, backup recovery, stale content migration and long Undo/Redo history;
10. simulate Steam unavailable, Cloud conflict, delayed achievement reconciliation and demo/full import repeated twice;
11. simulate keyboard+mouse, controller hot-swap, Steam Deck 1280x800, reduced motion, high contrast, numeric labels and localization text expansion;
12. simulate runtime softlock SOLVABLE/UNSOLVABLE/UNKNOWN outcomes and hint requests without clairvoyance;
13. simulate hostile behavior: max-depth spam, inaccessible TEST spam, identical TEST spam, rapid Undo/Redo, new action after Undo, repeated solve/replay, quitting at transaction boundaries;
14. create `GAME8_WHOLE_GAME_SIMULATION.md` with the trace, contradictions found, repairs made and remaining empirical gates;
15. update the owning Phase 3–8 authority files for every real contradiction rather than leaving fixes only in the simulation file;
16. add a Phase-9 regression checklist/tests sufficient to make the repaired whole-game state reproducible.

If Phase 9 closes cleanly and remaining run budget allows a genuinely destructive review rather than a microstep, continue into Phase 10; otherwise stop with exact Phase-10 NEXT ACTION.

## Blockers
**NONE for Game #008 design.**
Game #006/#007 migrations remain pending and explicitly non-blocking.