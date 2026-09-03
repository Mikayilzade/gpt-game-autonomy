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
**Game #016 — PHASE 8 TECHNICAL IMPLEMENTATION SPECIFICATION COMPLETE / PHASE 9 WHOLE-GAME SIMULATION ON PAPER NEXT.**

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
13. `GAME16_TECH_SPEC.md`

## This run completed — Game #016 Phase 8
- Re-read the complete active Game #016 authority chain and resumed exactly from `NEXT ACTION`.
- Fresh-checked current Godot and Steamworks platform guidance before freezing implementation direction.
- Created `GAME16_TECH_SPEC.md` as Phase-8 authority.
- Froze **Godot 4.7 stable / GDScript-first** as the default runtime direction for the future dedicated repo, with explicit upgrade gating to newer stable Godot 4.x only after deterministic-core regression.
- Separated deterministic puzzle/domain truth from Godot scenes, meshes, animation, physics, frame timing and Steam APIs; presentation/platform layers may project truth but never own it.
- Defined exact conceptual schemas for JobDefinition, WorkpieceState, CutSocketDefinition, JigStationDefinition, OperationDefinition, PartSlotDefinition, certification requirements, AttemptState, CampaignProfile, traces and stable IDs/lineage.
- Froze semantic command set and atomic ordering for destructive cuts and guided operations; no partial mutation may be interactable or saved.
- Froze deterministic lineage IDs and replayable semantic traces with canonical state hashing independent of presentation/timestamps.
- Specified state-based certifier and **zero false-positive** optimistic runtime dead-state detector contract, plus stricter exhaustive offline validator/oracle comparison where finite state spaces permit.
- Specified content/data versioning and package-time validation for OW01–OW24 + D1, including ID/predicate resolution, scope ceilings, known valid traces, alternate-family signatures and prerequisite graph validation.
- Froze exact campaign unlock evaluator from Phase 7, including the important rule that imported out-of-order clear records do not bypass unreached retail prerequisites.
- Specified versioned local profile/attempt persistence, atomic temp-write/replace, rotating backups, stable post-commit save points, crash recovery and explicit one-way save migrations.
- Specified demo discovery/import receipts, non-destructive OR merge, idempotency, retail-first merge, pre-import backup and D1 mapping semantics.
- Froze Steam Cloud conceptual boundaries: monotonic profile union for clear/tutorial/hint/import state, machine-local graphics excluded, and no semantic merge of competing in-progress irreversible attempts. Recommended baseline is cloud profile + local active attempt.
- Specified idempotent achievement reconciliation; achievements never own unlock truth and demo grants none.
- Specified semantic input abstraction, logical focus graph, Steam/controller glyph service, controller/mouse coexistence and portable vs machine-local accessibility/settings persistence.
- Froze rendering/animation separation from correctness: domain commits first; animation callbacks only release presentation flow; skipped animation/FPS changes cannot alter puzzle state.
- Specified localization-ready string/data boundaries and text-expansion/CJK/Cyrillic layout assumptions.
- Set Deck/low-end design budgets for FPS, memory, command/dead-state latency, restart/case transition and bounded visual complexity.
- Defined headless domain hooks, golden job traces, deterministic replay/state-hash fixtures, exhaustive dead-state oracle tests and hostile persistence/demo/cloud/achievement test matrix.
- Defined future dedicated-repo implementation order: bootstrap deterministic core -> OW01 vertical slice -> full core grammar -> authoring/validator -> persistence/platform -> full content -> UX/accessibility/target device -> adversarial QA/empirical gates/release candidate.
- No production implementation, Gmail or email action performed.

## NEXT ACTION — GAME #016 PHASE 9 / WHOLE-GAME SIMULATION ON PAPER
Re-read all thirteen active authority files and simulate the frozen game end to end without adding new mechanics.

Required substantial increment:
1. simulate first boot through OW01 with mouse and controller paths, including accessibility quick settings, first irreversible commit, restart and certification;
2. simulate the exact demo path OW01 -> OW03 -> OW05 -> D1, including expected knowledge state, hint availability and final causal recap;
3. simulate first retail boot with: no demo; completed demo + empty retail; completed demo + existing retail; corrupt/incompatible demo; verify exact unlock outcomes and achievement reconciliation;
4. simulate early campaign OW01–OW08, including bounded branch unlocks and at least one dead-lineage recovery;
5. simulate midgame OW09–OW16, including Trace View, delayed reuse, cross-root ancestry and at least one alternate valid solution-family case;
6. simulate late campaign OW17–OW24, including occupation/consumption conflict, derived witnesses, OW24 six-commit capstone and final certification;
7. simulate hints H1/H2/H3 in at least one early, one mid and one late job and verify they do not collapse into move instructions;
8. simulate replay/Another Way and completed causal recap/Trace the Work achievement semantics;
9. simulate save/load after every irreversible commit in a late case, crash before/after animation completion, attempt corruption, profile backup recovery and incompatible content revision;
10. simulate cloud/profile merge with disjoint clears, stale fewer-clear profile, conflicting portable settings, corrupt incoming profile and deliberate Reset Campaign Progress generation handling;
11. simulate controller/Deck-only traversal of hardest-case focus graph, cut/operation commit, restart, certify, hints and settings without mouse fallback;
12. simulate low-information/high-information accessibility overlays, reduced motion and single/double/hold commit variants without changing puzzle truth;
13. simulate hostile player behavior: repeated invalid docking, certification spam, restart spam, switching input devices mid-commit, quitting at transaction boundaries, repeatedly importing demo, replaying cleared cases, attempting to exploit reversible docking/consumption ordering;
14. identify contradictions, ambiguity, excessive friction or missing authority and patch the relevant existing Game #016 files rather than hiding fixes only in Phase-9 notes;
15. create `GAME16_SIMULATION.md` recording walkthroughs, failures found, patches applied and remaining empirical gates; update `STATUS.md`/`GAME_INDEX.md`.

If Phase 9 exposes no unresolved structural contradiction after patches, Phase 10 Adversarial Review may begin in the following run. Do not set `DESIGN COMPLETE = YES` before Phase 11 Specification Freeze.

## Blockers
**NONE for factory continuation.** Pending migrations #006–#015 remain non-blocking.

DESIGN COMPLETE = NO (current active Game #016; Phase 9 next).