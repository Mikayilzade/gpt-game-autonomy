# FACTORY STATUS

Last updated: 2026-09-01
Repository: `Mikayilzade/gpt-game-autonomy`
Branch: `main`

## Factory state
- Reusable factory rules: **YES**
- Games #001–#005: **DESIGN COMPLETE / migrated**
- Games #006–#011: **DESIGN COMPLETE / migration pending / retained non-active safety archives**
- Current design slot: **Game #012**
- Selected concept: **OPENWORK** *(working title; topology-of-remaining-space puzzle)*
- Production implementation inside factory: **NO**

## Continuity / active canon
Game #012 remains cleanly separated from Games #001–#011. Older games are exclusion/portfolio history only. Ink Bleed is rejected history, not parallel canon.

## Current phase
**Game #012 — PHASE 7 COMMERCIAL / RETENTION COMPLETE / PHASE 8 NEXT.**

## Active authority for Game #012
1. `START_HERE.md`
2. `STATUS.md`
3. `GAME_INDEX.md`
4. `GAME12_RESEARCH.md`
5. `GAME12_TOURNAMENT.md`
6. `GAME12_ROUND_C.md`
7. `GAME12_PRODUCT_THESIS.md`
8. `GAME12_MECHANICS.md` — exact Phase-4 rules; controls over loose tournament examples
9. `GAME12_CONTENT.md` — Phase-5 campaign/content/certification architecture
10. `GAME12_UX.md` — Phase-6 interaction/presentation/accessibility/onboarding authority
11. `GAME12_COMMERCIAL.md` — Phase-7 commercial/progression/demo/platform authority

## This run completed
### Game #012 Phase 7 — Commercial / Retention Model
- Resumed exactly from prior `NEXT ACTION`; no production implementation started.
- Performed fresh 2026 market/platform research against live Steam compact-puzzle listings and current Steamworks documentation.
- Added `GAME12_COMMERCIAL.md` as canonical Phase-7 authority.
- Froze provisional list price at **$8.99**, acceptable final range $7.99–$9.99 subject to final campaign/playtime value gate; recommended launch discount 10% remains a release marketing choice.
- Explicitly excluded ads, consumable hints, paid progression, battle pass, currencies, streaks, live-service loops and launch DLC needed to complete the base experience.
- Defined six-act progression: first three Act-I cases sequential, then current-act free order; next act unlocks at 4/6 solved, Act VI also requires 24 total solves, finale requires 4/5 preceding Act-VI cases.
- Defined six-case demo target (~20–40 min intent) and safe demo->full import semantics: provenance/versioning, compatible solved-ID union, settings whitelist, no forced replay and no blind overwrite of newer full progress.
- Froze assistance stance: no solution-directed hint ladder and no runtime certifier query; reusable general reasoning primers are allowed only if they never reference current-board candidate cells/roles/solution viability.
- Defined 12 accessibility-neutral achievements tied to campaign completion and curated reasoning vocabulary rather than speed, no-undo, retry counts or hint avoidance.
- Defined finite replay posture: 100% completion, free replay and optional hardest-case filter; no dailies, leaderboards, procedural filler, move grades or grind.
- Froze platform targets: Steam demo, achievements, Cloud, full controller, offline play; design/test toward Deck Verified but never advertise Verified before Valve status exists.
- Defined localization-ready architecture and provisional language priorities without making an unfunded shipping-language promise.
- Added price-value, demo, progression, achievement-neutrality, anti-oracle, Cloud/import, feature-honesty and content-burden acceptance gates.

### Fresh evidence recorded
Current Steam examples checked include Outpacked ($7.99/61 levels), Dot Art Logic ($9.99/3000+ puzzles), A Little Perspective ($14.99/200+ puzzles), E9uations ($14.99), Fugaz ($5.99 short-form), and DIGDLE ($9.99/300+). This supports keeping OPENWORK below the $10 threshold unless final empirical value materially exceeds the current compact 30–36-case specification.

## Frozen migration state
Game #006 Stitchspace: pending, non-blocking.
Game #007 Last Known Shape: pending, non-blocking.
Game #008 Locksmith's Margin: pending, non-blocking.
Game #009 Binder's Imposition: pending, non-blocking.
Game #010 Luggage Carousel Zero: pending, non-blocking.
Game #011 Missing Step: pending, non-blocking; final authority `GAME11_FINAL_FREEZE.md`.

## NEXT ACTION — GAME #012 PHASE 8 TECHNICAL IMPLEMENTATION SPECIFICATION
Perform one substantial technical-specification increment without writing production code.

Required work:
1. select and justify engine/runtime direction appropriate to 2D deterministic grid UI, controller/Deck target, Steam integration and low asset burden; verify current stable tool versions if version specificity matters;
2. define authority layering: immutable case data -> deterministic rules core -> derived topology -> runtime presentation, with the offline certifier using the same evaluator contract;
3. define conceptual data structures for board/case/pieces/predicates/placements/topology/certificates and exact schema/rules/content version responsibilities;
4. define application/scene/state architecture for boot, campaign map/case select, puzzle session, pause/settings, success and demo import without embedding gameplay truth in UI nodes;
5. define placement/history/reposition transaction semantics and deterministic serialization/canonicalization;
6. define persistence architecture with atomic local saves, migrations, future-version refusal, corruption recovery, Steam Cloud conflict/merge policy and idempotent demo-import transaction;
7. define Steam abstraction for achievements/Cloud/controller glyph/platform availability so non-Steam/offline play remains functional;
8. define input-action abstraction and localization-key/data boundaries consistent with Phase 6/7;
9. define performance/memory budgets for <=9x9 runtime evaluation and offline exhaustive certification; runtime must never enumerate solutions;
10. define test architecture: golden topology fixtures, predicate tests, canonical-solution fixtures, save/import/cloud conflict fixtures, controller/focus/accessibility regression and representative content certificate verification;
11. define telemetry/privacy posture: no online service required; any analytics must be optional/minimal and never necessary for puzzle truth/progression;
12. define implementation dependency order for the future dedicated repository and explicit non-goals;
13. hostile-pass the Phase-7 progression/import/achievement rules against the proposed architecture and repair contradictions now;
14. if Phase 8 closes cleanly, set exact Phase-9 whole-game simulation scenarios as NEXT ACTION.

## Blockers
**NONE for factory continuation.** Pending migrations #006–#011 are explicitly non-blocking.

DESIGN COMPLETE = NO (current active Game #012).
