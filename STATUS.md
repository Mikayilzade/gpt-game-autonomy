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
**Game #015 — PHASE 7 COMMERCIAL MODEL COMPLETE / PHASE 8 TECHNICAL SPECIFICATION NEXT.**

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

## This run completed — Game #015 Phase 7
- Re-read factory authority and every active Game #015 file named by prior STATUS.
- Performed fresh September-2026 research on Steam demo carry-over, Steam Cloud/Deck continuity, Community feature eligibility and current puzzle-demo packaging.
- Created `GAME15_COMMERCIAL_MODEL.md` as Phase-7 authority.
- Froze finite-premium positioning: 24 dense handcrafted cases, no retention-service drift.
- Set revisable launch-price hypothesis at US$9.99–14.99 with $12.99 current center; final price remains an empirical release decision.
- Froze progression as family-based 2-of-3 relief with mandatory concept-introduction gates so players can bypass one stuck case but cannot bypass essential grammar.
- Froze a seven-case ~20–30 minute real-campaign demo, shared rules/save schema, no time limit, and required idempotent demo-to-full progress carry-over unless Phase 8 discovers a platform blocker.
- Froze achievement philosophy at roughly 10–14, targeting 10–12 meaningful learning/completion milestones; no no-hint/no-undo/speed/grind/accessibility penalties.
- Froze Steam feature scope: achievements, cloud, controller/Deck and demo carry-over IN; leaderboards/workshop/inventory OUT; Trading Cards conditional on platform eligibility.
- Froze hints/accessibility as free parity features, never monetized or stigmatized.
- Defined localization architecture expectations and provisional launch-language priorities without overpromising un-QA'd languages.
- Defined store/trailer/screenshot communication around stack -> spray -> rearrange -> spray -> unpack, not simulator imagery.
- Kept `FRESH COAT` explicitly provisional and added title-clearance gate before public store identity freeze.
- Froze launch/update/expansion boundaries and permanent exclusions: no ads, paid hints, consumables, FOMO, battle pass, loot boxes, paid skips or retention grind.
- No production implementation, test email or Gmail action performed.

## Frozen migration note
Games #006–#014 remain migration-pending NON-ACTIVE archives. Their missing repositories are non-blocking. Migrate each independently if/when its dedicated repository becomes available; verify handoff/integrity before deleting only that game's retained safety files.

## NEXT ACTION — GAME #015 PHASE 8 TECHNICAL IMPLEMENTATION SPECIFICATION
Re-read all active Game #015 authority, then specify implementation contracts without writing production code.

Required work:
1. choose/freeze engine/runtime direction or explicitly engine-agnostic boundaries, justified by 3D discrete geometry, controller/Deck, Steam integration and small-team scope;
2. define exact runtime data/state model and authority boundaries between authored source, derived certified data, save state and renderer;
3. define deterministic exposure-precompute pipeline for semantic atomic regions, including partial-region rejection/subdivision and renderer-vs-truth divergence tests;
4. define authoring/certifier architecture, legal arrangement enumeration, A->B transition enumeration, solution/equivalence/symmetry handling and repetition-signature validation;
5. define runtime arrangement/spray/reveal state machine with atomic transactions, undo/checkpoints and interruption recovery;
6. define versioned persistence schema, corrupt-save fallback, Steam Cloud conflict policy, Dynamic Cloud Sync handling, demo import/merge and achievement idempotency;
7. define input abstraction, Steam Input/device glyph integration boundaries, UI/game-state separation and localization-ready string/data contracts;
8. define performance assumptions/targets for desktop and Steam Deck, asset/runtime budgets and deterministic loading behavior;
9. define automated test hooks, content validation gates, golden-case tests and debug tooling that never leaks into shipping player UI;
10. define telemetry/privacy boundary (prefer none/minimal unless justified), build/package boundaries for demo/full game, and recommended implementation order for the dedicated repository;
11. explicitly attack renderer-vs-truth divergence, partial exposure, invalid content, symmetry bugs, corrupt saves, cloud/demo duplication and interrupted Spray/undo transactions.

If Phase 8 resolves cleanly, Phase 9 Whole-Game Simulation is next. Do not start production implementation.

## Blockers
**NONE for factory continuation.** Pending migrations #006–#014 are non-blocking.

DESIGN COMPLETE = NO (current active Game #015; Phase 8 next).