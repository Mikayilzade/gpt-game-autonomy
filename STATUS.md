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
**Game #008 — PHASE 7 ECONOMY / RETENTION / COMMERCIAL MODEL COMPLETE / PHASE 8 READY.**

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

## This run completed
- Read the factory authority chain and every active Game #008 file named by the prior `STATUS.md`, then resumed exactly from Phase 7 NEXT ACTION.
- Created `GAME8_COMMERCIAL_MODEL.md` as complete Phase-7 authority without changing puzzle grammar.
- Fresh Steam market reconnaissance anchored the value band: current examples include Piece by Piece at $12.99, A Little to the Left at $14.99, Patrick's Parabox and The Roottrees are Dead at $19.99, and the substantially larger Blue Prince at $29.99.
- Locked working price hypothesis at **$17.99 USD** with an empirical **$14.99–$19.99** pre-release review band tied to validated case count, actual campaign duration, tactile polish, accessibility/platform completeness and replay value rather than competitor parity.
- Explicitly defined **no gameplay economy**: no currency, XP, energy, paid hints, star gating, grind, lives, consumables or metagame power.
- Defined tutorial-safe campaign unlock flow: C01–C06 linear, then bounded small choice clusters where Phase-5 tutorial dependencies permit, with optional mastery never gating progression.
- Defined post-solve mastery/replay through Clean Bench, Measured Cuts/Tests, eligible Final Coverage and validated Alternate Partition badges; no time/dexterity/hint-shaming mastery.
- Defined solved-review motivation around causal history, alternate partitions and cleaner solutions rather than randomized dailies/endless mode.
- Defined a working **20-achievement** set inside an 18–24 target, with explicit bans on repetitive farming, no-hint requirements, all-case no-Undo perfection, timed dexterity, external accounts and accessibility-hostile tasks.
- Locked D01–D06 demo commercial role, completion CTA, feedback route and safe demo→full recognition/import boundaries.
- Fresh official Steamworks documentation confirms demos are separate App IDs, can share Cloud storage with the full app to reduce upgrade friction, and Valve recommends disabling achievements in demos and reconciling them in the full game.
- Fresh official Next Fest guidance confirms demos must be live for participation, should be live before the press-preview list cutoff for press access, and should be clearly exposed on the base store page.
- Platform targets: Steam Achievements, Steam Cloud, full controller path and Steam Deck target; Rich Presence/basic Stats optional low-burden only; leaderboards, Workshop/editor, live events and mandatory external accounts rejected.
- Localization-ready architecture is required, but non-English release languages remain a production/commercial hypothesis pending real word count, QA/support budget and market validation.
- Froze hard monetization boundaries: premium purchase baseline; no MTX, premium currency, paid hints/Undo/power, ads, battle pass, FOMO, timers, streaks or accessibility DLC; no gameplay DLC is promised.
- Added **80 commercial/progression acceptance tests**.

## Retained migration state
### Game #006 — Stitchspace
DESIGN COMPLETE = YES; preferred repo `Mikayilzade/stitchspace`; migration pending, non-blocking.

### Game #007 — Last Known Shape
DESIGN COMPLETE = YES; preferred repo `Mikayilzade/last-known-shape`; migration pending, non-blocking.

## NEXT ACTION — GAME #008 PHASE 8 TECHNICAL IMPLEMENTATION SPECIFICATION
Build the implementation authority without starting production code:
1. research current stable engine/runtime options and choose/freeze an initial implementation baseline appropriate for tactile 3D/2.5D bench presentation, deterministic discrete domain state, PC/Steam/controller/Deck and small-team scope;
2. define strict Domain Core vs Presentation vs Platform Services boundaries so animation/physics never decide fit, knowledge or puzzle outcome;
3. define conceptual state/data model for cases, blanks, locks, accepted sets, access predicates, knowledge facts/deductions, history, mastery and campaign progress;
4. define deterministic transition/reducer ordering for FILE, TEST, OPEN/access effects, Undo/Redo/Restart and solved transition;
5. define solver/validator architecture, canonical state keys, symmetry handling, information-respecting fairness search, softlock budgets and runtime-vs-authoring separation;
6. define persistence schema/versioning, atomic save/recovery, action-history storage, settings, Cloud conflict behavior, demo/full namespaces and safe demo recognition/import;
7. define Steam-service abstraction for achievements/Cloud/controller glyph/platform availability with offline graceful degradation;
8. define input/focus abstraction matching Phase 6 and target-device constraints;
9. define localization-ready string/data boundaries and font/layout assumptions without promising languages;
10. define performance/memory/loading budgets appropriate to 3 blanks/6 locks/6 columns and Steam Deck target; avoid speculative optimization;
11. define deterministic test hooks, headless domain tests, validator fixtures, save corruption/migration tests and presentation-authority tests;
12. define implementation order for future dedicated repo from bootstrap through vertical slice, systems, content, UX/platform and empirical gates;
13. write >=60 technical acceptance tests.

If Phase 8 closes cleanly, continue into Phase 9 whole-game simulation only if there is enough run budget to perform a meaningful end-to-end paper simulation rather than a status microstep.

## Blockers
**NONE for Game #008 design.**
Game #006/#007 migrations remain pending and explicitly non-blocking.