# FACTORY STATUS

Last updated: 2026-09-03
Repository: `Mikayilzade/gpt-game-autonomy`
Branch: `main`

## Factory state
- Reusable factory rules: **YES**
- Games #001–#005: **DESIGN COMPLETE / migrated**
- Games #006–#015: **DESIGN COMPLETE / migration pending / retained NON-ACTIVE safety archives**
- Current design slot: **Game #016**
- Selected concept: **ONE-WAY WORKSHOP**
- Production implementation inside factory: **NO**

## Continuity / active canon
Game #016 is the only active design slot. Games #001–#015 are exclusion/portfolio history only. Frozen archives #006–#015 are NON-ACTIVE and must not leak canon into #016. Round-C losers Unpacking Order and Margin of Error are rejected/exclusion history, not active mechanics.

## Current phase
**Game #016 — PHASE 7 ECONOMY / RETENTION / COMMERCIAL MODEL COMPLETE / PHASE 8 TECHNICAL IMPLEMENTATION SPECIFICATION NEXT.**

## Active authority for Game #016
1. `START_HERE.md`
2. `STATUS.md`
3. `GAME_INDEX.md`
4. `GAME16_RESEARCH.md`
5. `GAME16_ROUND_A.md`
6. `GAME16_ROUND_B.md`
7. `GAME16_ROUND_C.md`
8. `GAME16_PRODUCT_THESIS.md`
9. `GAME16_MECHANICS.md`
10. `GAME16_CONTENT.md`
11. `GAME16_UX.md`
12. `GAME16_COMMERCIAL.md`

## This run completed — Game #016 Phase 7
- Re-read the complete active Game #016 authority chain and resumed exactly from `NEXT ACTION`.
- Fresh-checked Sep-2026 premium puzzle pricing/demo context and current Steam discount rules; treated all market evidence as directional rather than sales prediction.
- Created `GAME16_COMMERCIAL.md` as Phase-7 authority.
- Locked working MSRP at **$12.99**, adjustable pre-release within $9.99–14.99 from empirical value evidence; baseline launch discount 10% / 7 days, with 10–15% allowed.
- Locked value gate: target median first-clear 5–7h, $12.99 floor evidence >=4.5h; never add filler/grind to defend price.
- Frozen exact campaign progression: six work-order trays with bounded branching; OW01 -> {OW02,OW03} -> OW04, then each later family A -> {B,C} -> D; OW24 implies all 24 canonical cases cleared.
- Frozen demo path OW01 -> OW03 -> OW05 -> D1 and deterministic demo-to-retail import semantics: clear flags merge by OR, retail prerequisite graph is recomputed, D1 never clears OW13, import is non-destructive/idempotent, in-progress demo attempts never import.
- Defined safe import into existing retail progress, settings-choice behavior, corruption recovery and requirement that manual file copying is never the intended user path.
- Frozen three-level authored hint ladder (goal focus -> conflict class -> proof boundary), unlock timing, always-available accessibility override and strict ban on naming the correct cut/sequence.
- Rejected move/time/material pars, grades, daily/random challenges, leaderboards and grind. Replay is case replay, alternate validated solution families and completed causal recap only.
- Locked no difficulty modes that alter puzzle truth; accessibility/information assists carry no punishment and never block achievements.
- Defined 12-achievement baseline with seven campaign milestones, meaningful state/lesson achievements, one validated alternate-solution replay achievement and one Trace View discovery achievement; no speed/no-hint/dexterity/grind achievements.
- Frozen Steam assumptions: achievements, retail Steam Cloud, full controller, Deck target, separate demo/import, localization-ready strings; no baseline Workshop/editor/leaderboards/trading-card-driven design.
- Frozen monetization exclusions and post-launch boundary: complete premium base game, no MTX/live-service economy; paid expansion only after base value proof and normally 8+ dense authored cases.
- Defined eight commercial/demo empirical gates covering comprehension, demo length, price perception, campaign value, hint integrity, Deck/controller, import/cloud reliability and store first-read.
- No production implementation, Gmail or email action performed.

## NEXT ACTION — GAME #016 PHASE 8 / TECHNICAL IMPLEMENTATION SPECIFICATION
Re-read all twelve active authority files and convert the frozen product into a buildable deterministic technical contract without starting production code.

Required substantial increment:
1. choose/freeze engine/runtime direction and justify it against small-team 3D tabletop, controller/Deck, data-driven authored content and deterministic tests;
2. define authoritative runtime state ownership and exact conceptual schemas for JobDefinition, Workpiece, CutSocket, JigStation, Operation, PartSlot, requirements, trace and campaign profile;
3. define deterministic transform/event ordering, stable IDs/lineage, cut/operation atomicity and certifier/dead-state contracts;
4. specify content loading/versioning and validation pipeline for all 24 jobs + D1, including exhaustive finite-state checks where feasible and zero false-positive dead-state detector requirement;
5. specify campaign unlock evaluator exactly from Phase 7;
6. specify versioned persistence, stable atomic attempt save points, crash recovery and save migration;
7. specify demo save discovery/import/merge/idempotency and retail-first/cloud-conflict recovery, including achievements reconciliation;
8. specify Steam Cloud conceptual file boundaries and monotonic progress merge rules without assuming cloud APIs can safely merge arbitrary in-progress attempts;
9. specify input abstraction/focus graph/controller glyph contracts and accessibility settings persistence;
10. specify rendering/presentation separation from puzzle truth, animation completion callbacks and no-frame-rate-dependent correctness;
11. specify localization-ready string/data boundaries and text expansion assumptions;
12. set performance/memory/load budgets appropriate to Deck/low-end PC and the bounded workbench;
13. define test hooks, deterministic replay/trace fixtures, golden job tests and hostile persistence/import tests;
14. define implementation order for the future dedicated repo (bootstrap -> deterministic core -> one vertical slice -> authoring/validator -> persistence/platform -> full content -> QA), while writing no production code here;
15. create `GAME16_TECH_SPEC.md` and update `STATUS.md`/`GAME_INDEX.md`.

Do not begin Phase 9 until another implementation session could build all frozen systems without inventing state ownership, save/import semantics, event ordering or validation rules.

## Blockers
**NONE for factory continuation.** Pending migrations #006–#015 remain non-blocking.

DESIGN COMPLETE = NO (current active Game #016; Phase 8 next).