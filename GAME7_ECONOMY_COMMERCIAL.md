# GAME #007 — LAST KNOWN SHAPE — ECONOMY / RETENTION / COMMERCIAL MODEL

Last updated: 2026-08-30
Phase: **7 — Economy / Retention / Commercial Model**
Selected concept: **G7C02 Last Known Shape**
Production implementation started: **NO**
DESIGN COMPLETE: **NO**

`GAME7_PRODUCT_THESIS.md` governs product identity. `GAME7_MECHANICAL_ARCHITECTURE.md` governs puzzle semantics. `GAME7_CONTENT_ARCHITECTURE.md` governs case counts/diversity. `GAME7_UX_PRESENTATION_ARCHITECTURE.md` governs interaction/accessibility. This file freezes the commercial wrapper and progression incentives without adding gameplay primitives.

---

# 1. Fresh market evidence — 2026-08-30

Current Steam checks used for pricing/context:
- **A Little Perspective** — released 2026-04-03, current list price **$14.99**, 200+ authored puzzles, demo, Steam Achievements/Cloud/Family Sharing. Source: https://store.steampowered.com/app/3485300/A_Little_Perspective/
- **Piece by Piece** — released 2026-03-13, current list price **$12.99**, 100 handcrafted levels, demo. Source: https://store.steampowered.com/app/3249380/Piece_by_Piece/
- **The Artisan of Glimmith** — released 2026-03-17, current list price **$12.99**, handcrafted systemic puzzle, demo. Source: https://store.steampowered.com/app/4160210/
- **The Roottrees are Dead** — current list price **$19.99**, established premium authored puzzle/mystery product. Source: https://store.steampowered.com/app/2754380/
- Steamworks demo documentation currently supports a demo button on the base game page; a separate demo page is optional, and Steam links the demo back to the full game. Steam also exposes a one-time wishlist demo-release notification window after first making the demo playable. Source: https://partner.steamgames.com/doc/store/application/demos

Interpretation: the 2026 compact authored-puzzle market supports roughly low-teens pricing for narrower/lighter products and ~$20 for stronger premium perceived-value products. Last Known Shape targets fewer cases than 100–200-level abstract puzzle packages, but substantially higher per-case 3D presentation/systemic authoring burden and a 5–8h preferred first clear. It should not compete on raw puzzle count.

---

# 2. Commercial thesis

**Premium, single purchase, PC/Steam first.**

Working US list-price target: **$17.99 USD**.
Release-review band: **$14.99–$19.99 USD**.

$17.99 is a design-time target, not an irrevocable launch price. Final choice occurs after representative playtest evidence for:
- median first-clear duration;
- final strong case count after cuts;
- mature causal variety;
- presentation quality/readability;
- demo comprehension/conversion intent;
- optional remix/mastery value.

Price decision rule:
- bias to **$14.99** if release lands near 28 cases, ~4–5h median, limited remix value or modest presentation polish;
- preserve **$17.99** if 30–34 strong cases, ~5–7h median and hook/variety validate;
- consider **$19.99** only if 34-case package, strong 6–8h value, excellent polish/demo response and optional content materially extends depth without padding.

No price is justified by sunk development effort alone.

---

# 3. Monetization boundaries

Forbidden:
- ads;
- microtransactions;
- consumable currency;
- paid hints;
- XP boosters;
- battle pass;
- daily/weekly engagement chores;
- FOMO events;
- loot/randomized purchases;
- mandatory account;
- always-online requirement;
- paid level-skip tokens.

Allowed later only as conventional expansion product after 1.0, if genuinely substantial:
- soundtrack/artbook;
- a large authored expansion with new cases that still obeys frozen mechanics or an explicitly versioned expansion spec.

No monetization system may alter puzzle state or reward grind.

---

# 4. Campaign unlock architecture

Progression exists to preserve teaching dependencies while reducing hard-block frustration.

## C01–C10
Strict sequential unlock. These cases teach foundational semantics and their order is part of onboarding.

## C11–C15
C11 unlocks after C10. C12–C15 unlock sequentially because first dynamic occluder/state-dependent concepts require controlled teaching order.

## C16–C22
C16–C19 sequential for two-object literacy. After C19, C20/C21 may both unlock; completing either unlocks C22. Both remain available for completion.

## C23–C28
Two shelves:
- shelf A: C23, C24, C25;
- shelf B: C26, C27, C28.
C23 and C26 unlock after C22. Within each shelf, cases unlock sequentially. Completing at least **4 of C23–C28**, including at least one from each shelf, unlocks C29; all six remain available and count toward full campaign completion.

## C29–C34
C29–C33 unlock sequentially to preserve synthesis pacing. C34 unlocks after C33 **and** at least 31 total main-case clears. Therefore a player may bypass up to three earlier mature cases temporarily but must complete enough of the campaign before capstone.

`Campaign Complete` requires C34 clear. `All Main Cases` is a separate profile fact for 34/34.

No currency, stars or arbitrary score threshold controls access.

---

# 5. Case completion and mastery

Baseline clear criterion is only the authored win predicate. Undo, Restart, hints and accessibility settings do not invalidate a clear.

Optional **Insight** mastery may exist only where content metadata proves one structurally meaningful secondary challenge, such as:
- preserve a specified remembered form across an intermediate state;
- solve using an alternate validated solution family;
- avoid one explicitly taught unnecessary overwrite;
- satisfy a case-specific causal constraint already expressible in frozen mechanics.

Forbidden mastery:
- speed/time thresholds;
- no-Undo achievements as product-significant progression;
- precision movement scoring;
- hidden collectibles unrelated to core reasoning;
- arbitrary minimum-command optimization across all cases.

A case without a strong causal mastery condition simply has no mastery badge.

Mastery never gates main campaign progress.

---

# 6. Optional remix admission

Content architecture allows **R01–R06 maximum** and zero minimum.

A remix ships only if:
1. its dominant causal skeleton materially differs from its source case;
2. it changes a causal dependency, not just room art/start pose;
3. validator confirms it is not near-isomorphic under the Phase-5 vector rules;
4. it introduces no private gameplay rule;
5. representative testers perceive a different planning problem.

Remixes unlock after C22 and/or after clearing their source concept band. Exact per-remix dependency is data-authored.

No remix count is promised in store copy until validated content exists.

---

# 7. Hint economy

Hints are a usability feature, not a scarce resource.

H0–H3 from Phase 6 are available without currency, cooldown, score penalty or achievement invalidation. A case may optionally delay H2/H3 by a short period of active play to reduce accidental spoilers, but the player can disable that delay in accessibility/settings if frustration reduction requires it.

No `hint tokens`, watch-ad hints or finite campaign hint inventory.

---

# 8. Achievement philosophy

Target: **14–20 achievements**, bounded and explainable.

Recommended families:
- campaign band milestones (5–6);
- C34 / campaign completion;
- all 34 main cases;
- first deliberate overwrite milestone after tutorial;
- first valid two-object dependency solve;
- selected authored Insight/mastery milestones;
- all validated remixes/masteries if they ship;
- one or two playful mechanic-consistent discoveries that do not require pixel hunting.

Forbidden achievement design:
- `finish without Undo` as a baseline prestige axis;
- speedrun requirement;
- accessibility-option exclusion;
- daily login/streak;
- repetitive action counters (`observe 10,000 times`);
- hidden achievements whose only function is arbitrary replay grind.

Achievements never gate cases or endings.

---

# 9. Demo architecture and commercial role

Demo target remains **DEMO01–DEMO06 / ~20–30 minutes**. It must prove the game is more than one magical transformation:
1. remember/resolve hook;
2. overwrite;
3. conflicting affordances;
4. authored mask/state dependence;
5. preservation decision;
6. readable two-object/order finale.

The demo remains available after release unless operational evidence gives a concrete reason to remove it. No artificial limited-time scarcity is part of the design.

Steam's current demo tooling supports keeping a demo tied visibly to the base game and optionally giving it its own store page. A separate demo page should be used only if there are enough demo-specific assets/trailer/screenshots to maintain it well; otherwise the base-page demo button is sufficient.

The factory records **no instruction to trigger wishlist/demo notification emails automatically**. Marketing notification actions are manual release operations outside this design factory.

---

# 10. Demo → full-game continuation/import

DEMO cases are representative authored cases, not assumed byte-identical to C01–C06. Therefore demo completion does **not** silently mark main campaign cases complete.

Compatible import facts:
- accessibility/settings;
- input remaps;
- language;
- tutorial-fact acknowledgement flags;
- demo completion facts/achievements where platform-compatible;
- a `demo_veteran` profile flag.

On first full-game start with demo-veteran flag:
- campaign begins at C01;
- already-understood tutorial prompts may default to abbreviated mode;
- player can choose `Show full tutorials` at any time;
- no puzzle state or campaign win predicate is imported by guesswork.

Import is explicit, versioned, idempotent and monotonic for these profile facts. Failure to import never blocks starting the full game.

---

# 11. Replay / retention thesis

This is not a retention-maximization product. Desired post-clear behavior is voluntary mastery:
- replay unsolved main cases;
- revisit skipped mature cases before/after capstone;
- attempt validated Insight conditions;
- play causally distinct remixes;
- compare different valid solution families where the game can present them without exposing a solver oracle.

There are no dailies, procedural infinite mode, seasonal ladder, streaks or mandatory check-ins.

If players finish after one satisfying 5–8h campaign, that is a valid product outcome.

---

# 12. Difficulty / accessibility commercial boundaries

No separate `easy content SKU` or paid accessibility feature.

Baseline support includes free Undo/Redo, H0–H3 hints, reduced motion, high contrast, non-audio play, text scale and remapping. These are not treated as cheats.

If implementation later adds difficulty presets, they may only alter presentation/hint cadence or select authored optional challenge variants; they may not silently change the canonical observation rule.

---

# 13. Platform feature target

Steam-first target features:
- Achievements;
- Steam Cloud if Phase 8 persistence/branch rules prove safe;
- controller support;
- Steam Deck-friendly 1280×800 UX target;
- Family Sharing as platform-supported where applicable;
- demo;
- offline campaign.

Cloud is optional at release if branch safety cannot be proven. Offline correctness outranks Cloud convenience.

No Workshop/level editor is in 1.0 scope. User-created cases would require exposing safe authoring/validation tooling and materially expand support burden.

---

# 14. Store-positioning boundary

Store promise should foreground:
- exact remembered-form hook;
- authored observation, not free-camera perspective tricks;
- preserve/overwrite planning;
- physical exploitation of remembered form;
- later two-object order/dependency.

Do not market as:
- `200+ puzzles` volume competition;
- generic `mind-bending perspective game`;
- quantum simulator;
- physics sandbox;
- Portal-like movement game.

A trailer/demo must show at least one overwrite where losing an old useful form is visibly consequential.

---

# 15. Release-value empirical gates

EV7-01: target players understand the hook from a mute 15–30s clip.
EV7-02: median full first-clear duration is measured from representative non-expert players.
EV7-03: final main-case survivor count is >=28 and diversity quotas pass.
EV7-04: at least three mature causal families are perceived as materially different in playtest, not only validator metadata.
EV7-05: DEMO06 two-object finale remains readable and produces stronger full-game interest than ending after the first transformation gimmick.
EV7-06: $17.99 value perception is tested against final duration/polish; price moves within $14.99–$19.99 band based on evidence.
EV7-07: optional remixes are excluded from value claims until they pass causal-distinction validation.
EV7-08: Cloud is excluded from release promises until branch/recovery semantics pass Phase-8/QA tests.

---

# 16. Phase-7 acceptance suite — 48 checks

EC-01 Product is premium single purchase.
EC-02 Working list target is $17.99 with $14.99–$19.99 review band.
EC-03 Final price is empirical, not paper-locked irrespective of final content.
EC-04 No ads/MTX/currency/battle pass/FOMO exists.
EC-05 No hint currency exists.
EC-06 No mandatory account/online dependency exists.
EC-07 C01–C10 preserve teaching order.
EC-08 Dynamic-occluder introduction remains ordered through C15.
EC-09 Two-object literacy remains ordered through C19.
EC-10 Mature shelves permit bounded bypass without skipping teaching foundations.
EC-11 C34 requires C33 plus at least 31 main clears.
EC-12 Main campaign completion does not require all optional content.
EC-13 34/34 is tracked separately from C34 completion.
EC-14 Undo use never invalidates main clear.
EC-15 Hint use never invalidates main clear.
EC-16 Accessibility settings never invalidate main clear.
EC-17 Mastery never gates campaign.
EC-18 Mastery cannot be generic speedrun scoring.
EC-19 Mastery cannot require no-Undo baseline play.
EC-20 Mastery uses only frozen mechanics.
EC-21 Remix count may be zero.
EC-22 Remix admission requires causal distinction.
EC-23 Cosmetic layout changes alone cannot qualify a remix.
EC-24 Remixes never add private rules.
EC-25 Hints are free and non-consumable.
EC-26 Achievement target is bounded rather than grind-driven.
EC-27 No daily/streak achievement exists.
EC-28 Achievements never gate progression.
EC-29 Demo contains preserve/overwrite beyond tutorial gimmick.
EC-30 Demo reaches a readable two-object/order dependency.
EC-31 Demo availability is not artificially time-limited by design.
EC-32 Factory never auto-triggers Steam wishlist/demo email notifications.
EC-33 Demo completion does not guess-equate demo cases with campaign clears.
EC-34 Demo import is versioned/idempotent.
EC-35 Demo import can carry settings/remaps/accessibility.
EC-36 Demo import failure cannot block full-game start.
EC-37 Replay thesis does not require infinite/procedural mode.
EC-38 No seasonal retention system exists.
EC-39 Optional difficulty cannot alter observation semantics silently.
EC-40 Offline campaign remains baseline.
EC-41 Cloud may be cut before violating branch integrity.
EC-42 Workshop/editor is out of 1.0 scope.
EC-43 Store copy does not compete primarily on raw puzzle count.
EC-44 Store copy distinguishes authored Observation Frames from free-camera perspective manipulation.
EC-45 Trailer/demo shows consequential overwrite, not only transformation spectacle.
EC-46 Price review uses measured duration/content/polish/demo evidence.
EC-47 Unvalidated remixes do not inflate store value claims.
EC-48 No commercial system adds a new gameplay primitive.

---

# 17. Phase-7 result

**PHASE 7 — ECONOMY / RETENTION / COMMERCIAL MODEL: COMPLETE ON PAPER.**

Working commercial target is $17.99 with a $14.99–$19.99 evidence-driven release band. Campaign unlock structure, mastery/remix admission, free hints, bounded achievements, representative demo, safe demo→full profile import, replay philosophy, platform targets and strict no-grind/no-MTX boundaries are frozen.

## NEXT ACTION
Phase 8 — Technical Implementation Specification. Re-check current engine/runtime direction before pinning. Specify Domain Core / Presentation / Platform boundaries, canonical data schemas, deterministic command/event/hash contracts, solver/validator tooling, persistence/backup/recovery, Cloud/demo-import conflict rules, input abstraction, localization architecture, performance budgets, test harnesses and implementation order. Add >=55 technical acceptance tests.