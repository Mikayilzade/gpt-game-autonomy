# GAME #012 — PHASE 7 COMMERCIAL / RETENTION MODEL

Date: 2026-09-01
Status: **PHASE 7 COMPLETE**
Product: **OPENWORK** *(provisional working title)*
Authority: commercial positioning, campaign progression, demo/full continuity, assistance, achievements, replay posture and platform-feature promises. Exact rules remain in `GAME12_MECHANICS.md`; campaign architecture remains in `GAME12_CONTENT.md`; interaction/accessibility remains in `GAME12_UX.md`.

## 1. Fresh 2026 market / platform check
The current compact puzzle market supports a deliberately modest premium price, but content quantity alone cannot justify the price. Relevant live Steam examples checked 2026-09-01:
- `Outpacked` (2026-04-01): $7.99, 61 handcrafted levels, demo, achievements, Workshop/editor.
- `Dot Art Logic` (2026-02-10): $9.99, 3,000+ nonograms, demo, achievements, Cloud.
- `A Little Perspective` (2026-04-03): $14.99, 200+ authored puzzles plus hub/narrative, demo.
- `E9uations` (2026-05-27): $14.99, demo and 20 achievements.
- `Fugaz` (2026-07-07): $5.99, explicitly short puzzle experience, demo, achievements and Cloud.
- `DIGDLE` (2026-06-29): $9.99, 300+ puzzles, demo and Cloud.

The lesson is not “price per puzzle.” OPENWORK has only a 30-floor/36-target campaign and deliberately rejects editor/Workshop/endless filler, so it should not price as though it has 100–300 levels or a narrative wrapper. Its value proposition must be dense authored deduction, strong presentation, accessibility and a polished demo.

Steamworks documentation checked 2026-09-01 also confirms:
- demos are separate appIDs and can appear directly on the base game's store page;
- achievements are persistent Steam-account features and may be localized;
- Steam Cloud is a standard fit for cross-device saves / Deck continuity;
- launch discounts are supported, while later custom discounts are subject to cooldown rules.

Research references:
- https://store.steampowered.com/app/4012320/Outpacked/
- https://store.steampowered.com/app/4297410/Dot_Art_Logic/
- https://store.steampowered.com/app/3485300/A_Little_Perspective/
- https://store.steampowered.com/app/3345810/E9uations/
- https://store.steampowered.com/app/4389170/Fugaz/
- https://store.steampowered.com/app/4817390/DIGDLE/
- https://partner.steamgames.com/doc/store/application/demos
- https://partner.steamgames.com/doc/features/achievements
- https://partner.steamgames.com/doc/features/cloud
- https://partner.steamgames.com/doc/marketing/discounts

## 2. Price / monetization freeze
### Recommended list price
**USD $8.99** provisional launch list price.

Acceptable final release band after demo/playtime testing: **$7.99–$9.99**. Do not move above $9.99 unless the frozen product materially grows beyond the current 30–36 authored-case promise or empirical playtime/value evidence is unusually strong.

Recommended launch discount: **10%** if commercial timing supports it. This is marketing policy, not a gameplay dependency, and may change near release without reopening game design.

### Monetization exclusions
Launch product has:
- one premium purchase;
- free demo;
- no ads;
- no consumable hints;
- no paid puzzle packs required to make the base campaign feel complete;
- no battle pass, streak currency, premium currency, boosters, loot boxes or subscription;
- no cosmetic store dependency;
- no “deluxe” gameplay advantage.

A soundtrack or genuinely substantial future expansion may be sold separately later, but neither is part of the launch design promise.

## 3. Campaign progression / unlock policy
The six-act structure remains, but progression is **gated branching rather than strict linear lockstep**.

Rules:
1. Act I cases 1–3 are sequential because they teach the scored object, markers and enclosure.
2. After case 3, the remaining cases of the current unlocked act may be attempted in any order.
3. The next act unlocks when the player solves **4 of the current act's 6 cases**.
4. Unsolved cases remain available permanently; unlocking the next act never marks them solved.
5. Act VI unlocks only after Act V's 4/6 gate and at least **24 total campaign cases** solved, preventing a path that skips too much foundational material.
6. The finale case (`R12` role) unlocks after **4 of the other 5 Act-VI cases** are solved.
7. Campaign completion is credited when the finale is solved. 100% completion means every shipping case solved.

Why: a compact thinky game should not strand a player behind one mental blind spot, but unrestricted global access would weaken onboarding/pacing. The 4/6 gate gives two-case skip tolerance per act without requiring a separate skip currency.

No stars, grades, par moves, speed medals, no-undo badges or move counts gate progression.

## 4. Demo scope and full-game carry-over
The protected demo remains **six authored cases**, selected from early campaign material but packaged as a coherent mini-arc. Target first-play demo duration: roughly **20–40 minutes**, with individual variance expected.

### Carry-over identity
Demo and full game use compatible versioned progress/settings schemas. Demo save records provenance explicitly (`source_product = demo`, demo content/rules versions).

On first full-game boot, if compatible demo data exists:
- offer one clear `Import Demo Progress` action;
- default recommendation is Import, but never import silently if doing so could overwrite newer full-game progress;
- imported solved case IDs that exactly match full-game case IDs + compatible content versions become solved in full game;
- imported settings map only through a whitelist of shared settings keys;
- achievements are recomputed from authoritative imported solved-state after import rather than blindly trusting demo achievement flags;
- imported cases are not forced to replay.

If a demo case was revised incompatibly before release, its solved flag is not imported; the UI explains that the puzzle changed. Settings may still import independently.

### Merge rule if both saves exist
Never replace newer full-game progress wholesale with demo data. Merge monotonic facts where safe:
- solved-case set = union of compatible solved IDs;
- glossary/tutorial-seen flags = union;
- accessibility/settings = keep current full-game values unless user explicitly chooses `Use Demo Settings`;
- current selected case / navigation state = full-game value.

Phase 8 must make this transaction crash-safe and idempotent.

## 5. Hint / assistance stance
OPENWORK ships **without a solution-directed hint ladder**. The anti-oracle boundary is a product feature.

Allowed assistance:
- predicate natural-language explanation;
- topology inspect overlay for current committed state;
- glossary/tutorial replay;
- accessibility options;
- unlimited undo/reset/reposition;
- campaign skip tolerance via 4/6 unlocks;
- optional `Reasoning Primer` cards unlocked after repeated unsolved engagement, but these may describe only general reusable concepts already taught, e.g. “An enclosed pocket cannot touch any outer edge” or “Two placements can create the same number of spaces but different sizes.” They may **not** refer to coordinates, piece roles, candidate zones, articulation points on the current board, remaining solution counts, or whether the current partial state is extendable.

The primer is not counted as a hint used; there is no hint-shame badge/stat. No achievement depends on avoiding assistance.

If later playtesting proves case-specific hints necessary, that is a Phase-10/implementation empirical gate and must obey: conceptual nudge only, never candidate-cell highlighting or certifier-derived state pruning.

## 6. Achievement set
Target: **12 Steam achievements**, all monotonic, accessibility-neutral and reconstructable from authoritative progress. No hidden speed/no-undo/no-hint conditions.

1. **First Opening** — solve first campaign case.
2. **See the Void** — complete Act I gate (>=4 Act-I cases).
3. **Inside / Outside** — solve all six Act-II cases.
4. **Shared Space** — solve all six Act-III cases.
5. **False Openings** — solve all six Act-IV cases.
6. **Coupled Cuts** — solve all six Act-V cases.
7. **Openwork** — solve the finale.
8. **Every Opening** — solve every shipping campaign case.
9. **Pocket Maker** — solve any certified case whose target includes a hole predicate after hole onboarding is available.
10. **Edges Matter** — solve any certified case whose target includes boundary signatures/touch semantics.
11. **Together, Apart** — solve any certified case containing both SAME and DIFFERENT marker relations.
12. **Three Consequences** — solve a curated mastery case tagged for >=3 materially necessary predicate classes.

Achievements 9–12 are tied to solving curated cases/content metadata, not telemetry such as number of retries or action style. They reward encountering the game's reasoning vocabulary, not grinding.

Demo achievement policy: demo may show in-game milestones but should not require a duplicate Steam achievement set. Full game awards eligible achievements after safe import/reconstruction.

## 7. Replay / post-completion posture
OPENWORK does not pretend to be endless.

After finale:
- case select clearly shows unsolved cases;
- 100% goal remains every case solved;
- any solved case can be replayed instantly;
- optional `Clear Placement and Replay` never erases the solved record;
- a postgame `Openwork Set` may expose the hardest already-shipping cases as a convenient filter, not new content;
- player may inspect which reasoning-family icon(s) a solved case exercised only after solving it, as a retrospective taxonomy rather than a pre-solve hint.

Explicitly no:
- daily puzzle/streak;
- randomized filler advertised as infinite;
- score attack;
- leaderboards;
- speedrun timer as product feature;
- par-move grades;
- no-undo medals;
- procedural challenge treadmill;
- live-service events.

Replay is secondary. The commercial promise is a finite high-quality deduction object.

## 8. Steam / platform feature posture
### Required release targets
- **Steam demo:** YES.
- **Steam Achievements:** YES, 12-target set above.
- **Steam Cloud:** YES for full-game progress/settings; demo import architecture must not create cross-app overwrite hazards.
- **Full controller support:** YES; store claim only after complete menu/gameplay regression with controller.
- **Steam Deck:** design and test toward **Verified**, but never advertise Verified until Valve status exists. Internal release gate is comfortable 1280x800 play, controller glyph correctness, text/readability, no launcher dependency and Cloud continuity.
- **Keyboard/mouse:** YES.
- **Offline play:** YES after installation; no server dependency for rules/progress.

### Localization posture
Because gameplay copy is small and predicate language is structured, architecture must be localization-ready at launch. Provisional commercial target: **English plus at least 7 additional interface languages** if budget/QA permits, prioritizing Simplified Chinese, Japanese, Korean, French, German, Spanish (Spain or LATAM chosen consistently) and Brazilian Portuguese. Russian is a strong additional candidate. Exact shipping-language list is a production/business decision and must not be promised until translation + UI QA are funded.

All predicate text, tutorial text, achievement strings, settings and case titles use localization keys; board logic never depends on rendered language.

### Store-page promise discipline
Do not claim before verified:
- exact playtime;
- “36 puzzles” if quality curation ships 30–35;
- Deck Verified;
- a specific localization count;
- Workshop/editor;
- procedural/infinite replayability.

Safe product promises once implemented: handcrafted finite campaign; deterministic deduction; controller support; demo; no timers/reflex requirement; unlimited undo; objectives concern remaining open space.

## 9. Retention / commercial acceptance gates
Phase 7 is accepted only with these gates carried forward:
1. **Price-value gate:** if final accepted campaign is only 30 cases and median blind first-play completion is <3 hours, reassess toward $7.99 rather than padding content.
2. **Demo conversion gate:** demo must contain the inversion/coupling aha, not merely six tutorials; do not lengthen demo just to quote a larger level count.
3. **Progression gate:** 4/6 branching must not allow a player to reach late acts without understanding holes, marker grouping and boundary contact; whole-game simulation must test plausible skip paths.
4. **No coercive retention:** no streaks, FOMO, grind currencies or replay requirements may be introduced to improve engagement metrics.
5. **Achievement neutrality:** every achievement must remain obtainable with remapping, reduced motion, high contrast, text scaling, unlimited undo and any permitted reasoning primer.
6. **Hint boundary:** assistance cannot inspect certifier solution sets at runtime.
7. **Cloud/import safety:** imported/demo/cloud progress may never silently erase a larger solved-case set.
8. **Feature honesty:** store features are promises only after implementation/release gates pass.
9. **Content-burden gate:** no commercial feature may require recurring authored content after launch.
10. **Finite-product gate:** if replay additions make the game materially harder to implement/QA than the 30–36 case campaign, cut the replay feature.

## 10. Phase-7 freeze statement
Commercial identity is now coherent with the mechanical/UX design:
- premium one-time purchase, provisional **$8.99**, acceptable $7.99–$9.99;
- six-act campaign with 4/6 per-act skip tolerance and no grading economy;
- six-case demo with safe optional progress/settings import;
- no solver-directed hints; general reasoning primers only;
- 12 accessibility-neutral achievements;
- finite postgame replay/100% completion, no live-service retention;
- Steam demo + achievements + Cloud + full controller as release targets; Deck Verified is a target, not a claim;
- localization-ready architecture, final language count deferred to production validation.

**PHASE 7 = COMPLETE.**

Next: Phase 8 Technical Implementation Specification. It must define a deterministic shared rules core, data model/schema versioning, runtime/certifier authority boundary, scene/state architecture, placement/history model, save transactions + Cloud conflict semantics + demo-import idempotency, Steam abstraction, input abstraction, localization keys, performance budgets, test fixtures, telemetry/privacy posture, and implementation order. No production code is to be written in the factory.