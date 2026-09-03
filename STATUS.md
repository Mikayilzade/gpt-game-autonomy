# FACTORY STATUS

Last updated: 2026-09-03
Repository: `Mikayilzade/gpt-game-autonomy`
Branch: `main`

## Factory state
- Reusable factory rules: **YES**
- Games #001–#005: **DESIGN COMPLETE / migrated**
- Games #006–#014: **DESIGN COMPLETE / migration pending / retained NON-ACTIVE safety archives**
- Current design slot: **Game #015**
- Selected concept: **FRESH COAT (working title)**
- Production implementation inside factory: **NO**

## Continuity / active canon
Game #015 is the only active design slot. Games #001–#014 are exclusion/portfolio history only. Frozen archives #006–#014 are explicitly NON-ACTIVE and must not leak canon into #015.

## Current phase
**Game #015 — PHASE 8 TECHNICAL IMPLEMENTATION SPECIFICATION COMPLETE / PHASE 9 WHOLE-GAME SIMULATION NEXT.**

## Active authority for Game #015
1. `START_HERE.md`
2. `STATUS.md`
3. `GAME_INDEX.md`
4. `GAME15_RESEARCH.md`
5. `GAME15_ROUND_A.md`
6. `GAME15_ROUND_B.md`
7. `GAME15_ROUND_C.md`
8. `GAME15_PRODUCT_THESIS.md`
9. `GAME15_MECHANICAL_ARCHITECTURE.md`
10. `GAME15_CONTENT_ARCHITECTURE.md`
11. `GAME15_UX_PRESENTATION_ARCHITECTURE.md`
12. `GAME15_COMMERCIAL_MODEL.md`
13. `GAME15_TECHNICAL_SPECIFICATION.md`

## This run completed — Game #015 Phase 8
- Re-read factory authority and every active Game #015 file named by prior STATUS.
- Performed fresh September-2026 verification of Godot stable versions, Steam Deck requirements, Steam Cloud/demo guidance and the current GodotSteam maintenance/move situation.
- Created `GAME15_TECHNICAL_SPECIFICATION.md` as Phase-8 authority.
- Froze initial implementation direction as Godot 4.7.x stable, GDScript-first, with deterministic core data kept engine-agnostic.
- Isolated Steamworks behind a `PlatformServices` adapter so gameplay/state never depends on a particular community binding.
- Froze authority layers: authored source -> certified derived truth -> immutable runtime package -> mutable model -> versioned persistence -> renderer/UI.
- Specified exact exposure-precompute contract with `PARTIAL_INVALID` rejection/subdivision and explicit renderer-vs-truth divergence QA.
- Specified authoring/certifier enumeration, A->B transition graph, symmetry/equivalence rules, repetition validator and stable certified case packages.
- Specified runtime arrangement/spray/reveal state machine with atomic Spray checkpoints, transaction IDs, idempotency and interruption-safe Undo/recovery.
- Specified versioned save/profile layout, atomic writes, corrupt-save fallback and explicit schema migrations using stable semantic IDs.
- Specified cloud conflict policy: monotonic progress union, no cross-attempt state splicing, revision/transaction lineage over timestamps, Dynamic Cloud Sync stable checkpoints.
- Specified idempotent demo-to-full import and achievement reconciliation.
- Specified semantic input abstraction, glyph/provider boundary, UI/model separation, localization contracts and modal double-input guard.
- Set Steam Deck-class target at 60 fps / 1280x800 where practical, with platform 30 fps floor; no gameplay physics requirement.
- Defined pure-model, golden-case, geometry-adversarial, transaction-crash, cloud-merge and controller/UI test suites plus non-shipping debug tools.
- Froze baseline privacy posture: no custom gameplay telemetry backend/account system.
- Defined one-codebase demo/full packaging and dedicated-repository implementation order 12A–12H.
- Explicitly attacked renderer divergence, partial exposure, symmetry bugs, corrupt saves, cloud/demo duplication, interrupted Spray/Undo and stale Steam integration dependencies.
- No production implementation, test email or Gmail action performed.

## Frozen migration note
Games #006–#014 remain migration-pending NON-ACTIVE archives. Their missing repositories are non-blocking. Migrate each independently if/when its dedicated repository becomes available; verify handoff/integrity before deleting only that game's retained safety files.

## NEXT ACTION — GAME #015 PHASE 9 WHOLE-GAME SIMULATION
Re-read all active Game #015 authority, then simulate the complete shipped experience on paper and repair contradictions/friction rather than merely summarizing it.

Required walkthroughs:
1. first boot on desktop/Deck, input detection, settings/accessibility and FC01 entry;
2. FC01 first arrangement, factual exposure preview, first Spray, reveal, first failure and Undo/reset recovery;
3. onboarding through FC05 and transition into family-based 2-of-3 progression with mandatory concept gates;
4. exact seven-case demo flow and demo-to-full import into normal FC01–FC24 campaign order;
5. FC10 two-pass/rearrangement teaching and interruption/resume between A and B;
6. FC13 A_THEN_B introduction and failure explanation without appearance/order confusion;
7. FC16 cavity inspection and hidden-region accessibility without camera hunting/oracle leakage;
8. FC21 role reversal and FC24 capstone under four-object readability pressure;
9. campaign completion, achievements, replay and legitimate alternate solutions;
10. Steam Deck suspend -> cloud -> PC/other-device resume and an irreducible divergent-attempt conflict;
11. corrupt latest puzzle state / valid profile recovery;
12. hostile behavior: rapid pose cycling, repeated Spray/Undo, modal double input, skipping one case per family, hint use and attempted brute force.

For every walkthrough record: player-visible state, semantic state, likely confusion/friction, whether current spec already resolves it, and exact repair if not. Verify campaign pacing/unlock graph and demo carry-over do not create prerequisite contradictions. If a contradiction requires reopening mechanics/content/UX/commercial/technical rules, patch the relevant authority file explicitly; otherwise create a Phase-9 simulation file and advance to Phase 10 Adversarial Review.

## Blockers
**NONE for factory continuation.** Pending migrations #006–#014 are non-blocking.

DESIGN COMPLETE = NO (current active Game #015; Phase 9 next).