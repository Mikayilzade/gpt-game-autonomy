# FACTORY STATUS

Last updated: 2026-08-20
Repository: `Mikayilzade/gpt-game-autonomy`
Branch: `main`

## Factory state
- Reusable factory rules: **YES**
- Game #1 migrated: **YES — Organism Cargo -> `Mikayilzade/organism-cargo`**
- Game #2 migrated: **YES — False Map Department -> `Mikayilzade/false-map-department`**
- Factory cleanup after Game #2: **COMPLETE**
- Current design slot: **Game #3**
- Game #3 autonomous design run count: **11**
- Game #3 concept selected: **YES — Borrowed Collision**
- Phase 1 Opportunity Discovery: **COMPLETE**
- Phase 2 Concept Tournament: **COMPLETE**
- Phase 3 Product Thesis Lock: **COMPLETE**
- Phase 4 Mechanical Architecture: **COMPLETE ON PAPER**
- Phase 5 Content Architecture: **COMPLETE ON PAPER**
- Phase 6 UX / Presentation Architecture: **COMPLETE ON PAPER**
- Phase 7 Economy / Retention / Commercial Model: **COMPLETE ON PAPER**
- Phase 8 Technical Implementation Specification: **NEXT**
- Production implementation started: **NO**

## Current phase
**Game #3 — Phase 8 Technical Implementation Specification / Phase 7 complete on paper**

## Active temporary files — mandatory recovery read
1. `GAME3_RESEARCH.md`
2. `GAME3_RESEARCH_RUN2.md`
3. `GAME3_RESEARCH_RUN3.md`
4. `GAME3_TOURNAMENT.md`
5. `GAME3_TOURNAMENT_RUN2.md`
6. `GAME3_TOURNAMENT_RUN3.md`
7. `GAME3_PRODUCT_THESIS.md`
8. `GAME3_MECHANICAL_ARCHITECTURE.md`
9. `GAME3_CONTENT_ARCHITECTURE.md`
10. `GAME3_UX_PRESENTATION_ARCHITECTURE.md`
11. `GAME3_ECONOMY_COMMERCIAL.md`

## Completed — autonomous run 11
1. Re-read `START_HERE.md`, prior `STATUS.md`, `GAME_INDEX.md`, and every active Game #3 recovery file named by status before acting.
2. Resumed exactly from Phase 7 and created canonical `GAME3_ECONOMY_COMMERCIAL.md` without starting production implementation or reopening gameplay mechanics.
3. Rechecked current Steam references on 2026-08-20: `A Little Perspective` $14.99, `One Move Away` $14.99, `The GoD Unit` $9.99, `Bionic Bay` $19.99, plus current Steamworks Demo/Cloud/Achievements/Deck documentation.
4. Froze a design-time US list-price band of **$14.99–$19.99**, working center **$16.99**, while explicitly requiring release-time market/value recheck rather than turning the hypothesis into release canon.
5. Froze **no progression currency/power economy**: no XP, upgrades, rarity, crafting, skill tree, energy/lives, hint currency or farmed retries. The player progresses through case clears and tutorial/prerequisite tags only.
6. Froze the exact C01–C34 campaign prerequisite graph. C34 remains reachable with **zero optional mastery marks**, remixes/achievements never gate the main campaign, and replay/farming is never required for progression.
7. Froze four optional mastery roles: **Causal Compression, Preservation, Resource Discipline, Stable Causality**. Raw Undo/restart/failure/time/pause/assist/input-device history is never scored; accessibility never invalidates mastery; mastery grants no mechanical power.
8. Froze exactly **10 target remix cases** into three permanent packs: R01–R03 after C14, R04–R07 after C28, R08–R10 after C34. Every remix must document a changed causal dependency and new dominant reasoning transformation; parameter/art padding fails validation.
9. Froze retention without grind/FOMO: authored case cadence, alternate solutions, mastery, remixes and causal re-interpretation only. Dailies, streaks, rotating content, push-engagement loops, energy and endless filler are explicitly excluded.
10. Froze a four-depth hint model: Rule Reminder, Causal Conflict Focus, Directional Guidance, optional explicit Solution Guidance. Hints change information/help only; they never mutate collision/token/receiver/deterministic rules and never block baseline completion/mastery legitimacy.
11. Froze demo commercial intent around `DEMO01..DEMO05`, with the demo required to end on a deliberate secondary-collision/new-lineage reuse `aha`. Demo->full transfer is intended to be version-mapped, monotonic and idempotent; incompatible active demo state is never synthesized.
12. Froze Steam/Deck 1.0 scope: practical controller support, Deck-targeted layout, Steam Achievements, Steam Cloud target, associated demo, offline play without proprietary account and localization-ready architecture. Workshop, online leaderboards, multiplayer, server backend, proprietary login and live challenge services remain out of scope.
13. Froze a working achievement target of **20–24 (center 22)** with no grind, anti-access, input-device or repeated-failure farming achievements.
14. Froze monetization exclusions: one premium purchase, no microtransactions, paid hints, paid impact types, inventory-slot purchases, cosmetic store, ads, battle pass or withheld C01–C34 launch content. Any future paid expansion must be optional substantial new casebook content and cannot sell power.
15. Recorded nine commercial/retention risks: value mismatch, `arrow inventory` mis-positioning, quantized-physics expectation mismatch, shallow mastery, remix padding, demo over-teaching/underselling, hint oracle risk, platform feature creep and over-anchoring at $19.99.
16. Added ten empirical commercial gates covering hook/provenance/demo comprehension, no-grind progression, mastery/remix distinctness, store-positioning truth, price fairness and platform-account independence.
17. Added **50 numbered Phase-7 acceptance tests (`E7-01..E7-50`)** spanning commercial model, campaign progression, mastery, remixes, hints/accessibility, demo/platform, achievements, monetization and positioning integrity.
18. Phase-7 closure: **COMPLETE ON PAPER**. Product Thesis, Mechanical Architecture, Content Architecture and UX remain locked; no new token property, transform, receiver family, combat layer or retention mechanic was added.
19. Production implementation remains **NOT STARTED**.

## Locked Game #3 thesis
**Borrowed Collision** — Steal the force from one crash and spend it somewhere else: harvest collisions as portable impacts, route them through physical sockets, and reuse those consequences on carts, doors, cargo — or yourself.

### Non-negotiable differentiation rule
**A resolved physical consequence becomes a portable resource, and the world-state that created and receives that consequence must continue to matter.**

## NEXT ACTION
Execute **Phase 8 — Technical Implementation Specification**:
1. choose and justify the engine/runtime direction for the frozen deterministic 2D causal-physics design using current stable tool/platform evidence where material;
2. define strict Domain Core / Application Services / Presentation / Platform Adapter ownership boundaries so scenes/animation never become gameplay truth;
3. freeze the canonical `CaseDefinition` / `CaseState` / body / movement-lane / collision-relation / portable-impact / lineage / receiver / transform / objective state models;
4. define deterministic semantic command and transaction architecture for collect, transform, spend, reset, self-launch, moving receive windows, chained collision resolution and idempotent stale/double-command rejection;
5. define canonical serialization/state hashing and replay fixtures independent of frame rate, locale, input device, scene-tree/hash iteration and presentation speed;
6. define the content compiler/validator for R1–R8 families, donor regeneration classes, collision tables, prerequisite graph, reasoning-transformation tags, mastery distinction notes, remix changed-causal-dependency requirements and known-solution fixtures;
7. freeze Undo/Redo/history checkpoint architecture preserving exact body/token/lineage/world-pickup/transaction state;
8. define save/profile/recovery/version migration rules, interrupted transaction recovery, corruption backup selection and active-case compatibility across changed content/rules;
9. define Steam Cloud conflict/merge semantics and demo->full mapping/import identity while keeping offline/local correctness independent of Steam;
10. define semantic input abstraction and deterministic authored focus graph for mouse+keyboard, keyboard-only, controller and Deck;
11. define localization-ready token pipeline without using translated strings as gameplay identity;
12. define headless deterministic test harness/golden replay/metamorphic/fault-injection/content-validation suites;
13. define performance/memory/load/save budgets appropriate for the compact deterministic simulation;
14. define implementation slices 12A bootstrap -> vertical slice -> full systems/content/UX/QA, with the existential causality/readability gates tested before large content production;
15. define technical failure handling, observability/replay-support bundle and explicit technical non-goals;
16. add numbered Phase-8 acceptance tests and create `GAME3_TECHNICAL_SPEC.md`;
17. do **not** start production implementation or reopen gameplay simply for technical convenience.

## Completion rule
Game #3 remains **IN PROCESS** until full design freeze, dedicated-repository migration, autonomous implementation handoff + CI/email-noise guardrail, migration verification, `GAME_INDEX.md` update and factory cleanup/reset for Game #4 are all complete.

## Recovery rule
Read `START_HERE.md`, this file, `GAME_INDEX.md`, then every file listed under Active temporary files, and execute `NEXT ACTION` exactly.
