# GAME #003 — BORROWED COLLISION — ECONOMY / RETENTION / COMMERCIAL MODEL

Last updated: 2026-08-20
Factory run: **11**
Phase: **7 — Economy / Retention / Commercial Model**
Product thesis: **LOCKED**
Mechanical architecture: **COMPLETE ON PAPER**
Content architecture: **COMPLETE ON PAPER**
UX / presentation architecture: **COMPLETE ON PAPER**
DESIGN COMPLETE: **NO**

This file is the canonical Phase-7 commercial/progression contract for Borrowed Collision. It does not add gameplay primitives, token properties, receiver families, transforms, combat, progression stats or simulation rules. If a commercial/retention idea would require changing the frozen consequence-transfer grammar, that earlier phase must be explicitly reopened rather than silently mutated here.

---

# 1. Commercial thesis

Borrowed Collision is a **premium single-player systemic causal puzzle / action-puzzle**, not a retention service.

The product earns value from:
- the rare, immediately legible fantasy of harvesting a real collision consequence and reusing it elsewhere;
- 34 authored campaign cases with a controlled causal-complexity curve;
- optional mastery that rewards deeper causal understanding rather than punishing experimentation;
- 10 bounded remix cases that change causal dependencies rather than simply tightening thresholds;
- replay through alternate solutions, donor preservation, chain compression and cleaner use of the same small grammar;
- a 15–25 minute demo that proves the hook, not merely teaches controls;
- strong controller/Deck support and clear deterministic causality.

The game must not manufacture engagement through currencies, upgrades, rarity, daily obligations, limited-time content, grinding, ads, battle passes or recurring monetization.

---

# 2. Current price / market reference snapshot — 2026-08-20

Current US Steam list-price references checked for design positioning:

- **A Little Perspective** — $14.99; released 2026-04-03; authored puzzle game with a strong single-mechanic identity and demo.
  - https://store.steampowered.com/app/3485300/A_Little_Perspective/
- **One Move Away** — $14.99; released 2026-05-28; authored 3D puzzle game; Steam Achievements / Steam Cloud / Family Sharing.
  - https://store.steampowered.com/app/3172440/One_Move_Away/
- **The GoD Unit** — $9.99; older first-person physics-puzzle reference; useful as a lower-price precedent for smaller physics-puzzle scope.
  - https://store.steampowered.com/app/1204440/The_God_Unit/
- **Bionic Bay** — $19.99 list price; materially higher action/presentation/physics-production burden than Borrowed Collision and therefore a useful upper-neighborhood comparison rather than a direct scope match.
  - https://store.steampowered.com/app/1928690/Bionic_Bay/

Current Steamworks references checked:
- Demos: https://partner.steamgames.com/doc/store/application/demos
- Steam Cloud: https://partner.steamgames.com/doc/features/cloud
- Steam Achievements: https://partner.steamgames.com/doc/features/achievements
- Steam Deck / hardware recommendations and compatibility: https://partner.steamgames.com/doc/steamhardware/compat

Steam currently supports shared Cloud storage between demo and full-game app IDs and recommends clouded saves for games that move between Deck/PC. Steam's demo documentation also recommends not awarding demo achievements directly; compatible progress can instead be recognized after import/full-game load.

These are platform/commercial references, not gameplay authority.

---

# 3. Price-position hypothesis

## 3.1 Design-time band

**US list-price design band: $14.99–$19.99.**

**Working center hypothesis: $16.99.**

Interpretation:
- **$14.99** is the safe target if first-clear duration settles near the low end, presentation remains deliberately compact, or remixes/mastery do not materially extend value.
- **$16.99** is the preferred design center if 34 campaign cases sustain roughly 5–8 strong first-clear hours, demo conversion is healthy, causal variety survives the hour-3/hour-10 gates, and controller/Deck polish is solid.
- **$19.99** is defensible only if final audiovisual polish, case density, optional mastery/remix value and action-puzzle feel materially approach the quality expectation of stronger premium physics/action references.
- A lower launch price should not be used to excuse thin/repetitive content.

This is **not a release-time price lock**. Final price must be rechecked against actual median playtime, perceived value, reviews of comparable releases and current Steam market conditions near release.

## 3.2 Discount philosophy

No launch-discount percentage is frozen. Discount cadence belongs to release planning. The base game must feel complete and fairly priced at list price; a permanent sale is not part of the value proposition.

---

# 4. Progression economy: deliberately none

There is **no spendable progression currency** in 1.0.

Forbidden:
- coins;
- XP/levels;
- impact upgrades;
- rarity tiers;
- permanent token capacity purchases;
- crafting;
- skill trees;
- hint currency;
- energy/lives;
- consumable retries;
- resource farming between cases.

Campaign progression is based only on:
1. baseline case clears;
2. explicit tutorial/prerequisite tags;
3. milestone unlocks for optional remixes.

The player becomes stronger through causal understanding, not permanent numerical power.

The mechanical 2-slot baseline / selected late 3-slot capacity is authored **case grammar**, not a player upgrade track.

---

# 5. Exact campaign unlock graph

The campaign contains C01–C34. Progression code must consume this graph/prerequisite data rather than invent a second UI-only unlock rule.

## Act I — C01–C07
Strict teaching chain:
`C01 -> C02 -> C03 -> C04 -> C05 -> C06 -> C07`.

Reason: each case establishes a prerequisite concept used immediately by the next case.

## Act II — C08–C14
- C08 unlocks on C07 clear.
- C09 unlocks on C07 clear.
- C10 requires C08.
- C11 requires C09.
- C12 requires C10 + C11.
- C13 requires C12.
- C14 requires C12.

The first small branch allows source/order reasoning and provenance/suitability reasoning to be learned in either local order while protecting prerequisite coherence.

## Act III — C15–C21
- C15 requires C13 + C14.
- C16 requires C15.
- C17 requires C15.
- C18 requires C16.
- C19 requires C17.
- C20 requires C18 + C19.
- C21 requires C20.

## Act IV — C22–C28
- C22 requires C21.
- C23 requires C22.
- C24 requires C22.
- C25 requires C23.
- C26 requires C24.
- C27 requires C25 + C26.
- C28 requires C27.

## Act V — C29–C34
- C29 requires C28.
- C30 requires C29.
- C31 requires C29.
- C32 requires C30 + C31.
- C33 requires C32.
- C34 requires C33.

## Progression invariants

- **C34 is reachable with zero optional mastery marks.**
- Remixes never gate the campaign.
- Achievements never gate the campaign.
- Re-clearing a solved case is never required to unlock another main case.
- Tutorial tags remain additional safety constraints: content compilation must reject an unlock graph that exposes a case before all mechanics it requires have been demonstrated.
- If later Phase-9 pacing review changes a dependency, it must update this canonical graph and content prerequisite metadata together.

---

# 6. Mastery retention role

Phase 5 established four mastery directions. Phase 7 freezes their progression/commercial meaning.

## M1 — Causal Compression
Reward a final solution where one deliberately engineered collision/chain replaces multiple obvious donor uses.

Valid examples:
- complete using <=N material source lineages;
- create/use a specified downstream CHAIN_GENERATED consequence instead of consuming two independent donors;
- solve with a shorter final causal chain when the case supports meaningful alternatives.

Invalid examples:
- raw move count;
- raw Undo count;
- arbitrary time limit.

## M2 — Preservation
Preserve a visible world resource/state beyond baseline requirements.

Examples:
- keep an exhaustible donor unused;
- keep fragile cargo/receiver unbroken;
- preserve a resettable system in its ready state;
- preserve a return route or optional world-state invariant.

## M3 — Resource Discipline
Use the available consequence economy more elegantly without turning impacts into a currency.

Examples:
- finish while leaving one useful impact unspent;
- avoid consuming a scarce STRONG source;
- complete without activating the selected third inventory slot in a case where 2-slot play remains valid;
- use a renewable WEAK lineage where an obvious STRONG source would work but cause collateral cost.

## M4 — Stable Causality
Complete with an authored stronger causal-state condition that remains valid across the bounded deterministic movement state relevant to the case.

This is not a generic wait timer. The stronger condition must involve a real moving receiver, moving body, reset cycle, chain consequence or other already-defined temporal state.

## Mastery rules

- Baseline completion is never blocked by mastery.
- Raw Undo, restart count, failed probes, pause/step usage, slowdown usage, input device and elapsed thinking time are never scored.
- Accessibility settings do not invalidate mastery.
- No mastery awards stronger tools, larger permanent inventory or mechanical power.
- Mastery may award visible Case Board stamps/marks and achievement progress only.
- A campaign case should normally expose 0–2 mastery marks; late cases may expose 3 only when they represent genuinely different causal insights.
- Every mastery contract must store an internal `mastery_distinction_note` explaining how the required insight differs from baseline play. Phase-10 review must reject arbitrary threshold shaving.

---

# 7. Remix structure — exactly 10 target cases

Phase 5's target is frozen as **10 remix cases** for 1.0 unless Phase 5 is explicitly reopened.

They are permanent optional content, not rotating/daily seeds.

## Pack R-A — Reclaimed Impacts (R01–R03)
Unlock: **C14 cleared**.

Purpose: remix the fully taught early grammar before deep chain routing.

Required diversity:
- at least one source-selection/provenance remix;
- at least one magnitude/fragility remix;
- at least one self-launch / transform-topology remix.

## Pack R-B — Chain Revisions (R04–R07)
Unlock: **C28 cleared**.

Purpose: recombine Act III/IV causal chains, moving windows and regeneration classes.

At least three distinct dominant reasoning-transformation tags across the four cases.

## Pack R-C — Borrowed Department (R08–R10)
Unlock: **C34 cleared**.

Purpose: post-campaign expert cases using the full frozen grammar without adding mechanics.

At least one case must support 3+ materially different baseline solution characters (for example preservation-heavy, chain-compression-heavy, and self/cargo allocation-heavy).

## Remix validity contract

Each remix stores:
- `source_substrate_id`;
- changed initial facts;
- changed objective/invariant facts;
- `changed_causal_dependency`;
- `expected_new_reasoning_transformation`;
- at least one known valid solution fixture.

A remix is invalid if it only:
- moves starts;
- changes a numerical threshold;
- swaps art/theme;
- tightens a mastery limit;
while preserving the same dominant causal insight as the source case.

No remix is time-limited. No login/date gate exists.

---

# 8. Retention without grind

Retention means the player voluntarily wants another causal problem.

Primary retention drivers:
- 5–20 minute authored-case cadence;
- regular shifts among source selection, direction conversion, magnitude suitability, donor preservation, chain generation, self/cargo allocation, moving windows and causal compression;
- alternate valid solutions where mechanically feasible;
- transparent mastery after baseline clear;
- 10 permanent remix cases;
- returning to an earlier case with later causal understanding;
- compact systemic achievements that reward unusual legitimate consequences rather than repetition.

Explicitly forbidden:
- dailies;
- streaks;
- login rewards;
- rotating challenge windows;
- battle passes;
- FOMO events;
- energy/lives;
- push-notification engagement loops;
- endless procedural filler presented as required value;
- arbitrary cumulative edit/harvest counts.

No DAU/retention KPI may justify weakening the premium puzzle identity.

---

# 9. Hints / assist philosophy

Accessibility and puzzle assistance are separate.

## 9.1 Accessibility neutrality

All Phase-6 accessibility features remain valid at full completion/mastery legitimacy:
- UI scaling;
- remapping;
- non-color / non-audio redundancy;
- reduced motion/flash;
- pause/step;
- slowdown;
- controller/keyboard-only paths;
- high-clarity labels;
- Deck-readable layout.

These are access features, not cheats.

## 9.2 Hint ladder

Hints change **information/help only**. They do not mutate impact, collision, token, receiver, lineage or deterministic movement rules.

### H1 — Rule Reminder
Restates one already-taught canonical rule and highlights relevant objects/requirement. No move recommendation.

Example: `STRONG impacts can break fragile receivers; MEDIUM is safe here.`

### H2 — Causal Conflict Focus
Identifies the two current systems/facts in conflict and where they are located.

Example: `The exhaustible donor you used also controls the only later STRONG source.`

Does not tell the player which impact to spend where.

### H3 — Directional Guidance
May name one causal category or room worth reconsidering, such as `Look for a way to create a secondary collision rather than consuming another source.` It may identify a family, not the full sequence.

### H4 — Optional Solution Guidance
Explicit opt-in authored stepwise guidance for players who ask for it. Not automatic and not the default puzzle loop.

Rules:
- Baseline completion remains available after any hint depth.
- Mastery remains valid because it checks final causal state, not whether help was consulted.
- Ordinary achievements are not disabled by hints.
- No default `no hints` prestige achievement exists.
- Hints never expose hidden known-solution fixtures unless H4 explicitly uses authored guidance data.

---

# 10. Demo strategy and demo -> full transition

## 10.1 Demo content identity

Use the already frozen `DEMO01..DEMO05` sequence from Phase 5/6.

The demo must deliver, in order:
1. a real collision becomes a stored impact;
2. a physical direction transform;
3. magnitude suitability / strong-not-better consequence;
4. source/provenance matters;
5. a spent impact creates a deliberate secondary collision / new lineage and the player reuses that consequence.

Target: **15–25 minutes**, median near 20.

The demo ending must land on the product `aha`: `I reused a consequence created by a consequence I had already moved.`

Do not add a disconnected prologue or demo-only mechanic.

## 10.2 Demo progression transfer intent

Preferred Phase-8 contract:
- demo and full game use separate versioned application/profile envelopes;
- compatible settings transfer;
- exact compatible tutorial tags and case/demo clears may transfer only through an explicit versioned mapping table;
- import is monotonic and idempotent;
- import never removes fuller progress;
- demo achievement state is not independently authoritative;
- compatible achievement conditions may be granted by the full game after validated import/load;
- incompatible active demo case state is not synthesized into changed full-game content;
- a rules/content mismatch may still allow settings import while refusing clear-state import.

Steam currently supports shared Cloud storage between demo/full app IDs; Phase 8 may use this where robust, but the design does not depend on Steam Cloud as the only import path.

---

# 11. Steam / platform 1.0 feature scope

## Required / target features

- premium single-player Steam base game;
- full practical controller support;
- Steam Deck-targeted 1280×800 layout/control path;
- Steam Achievements;
- Steam Cloud target for progress/settings where conflict-safe persistence can be implemented;
- associated Steam demo;
- Family Sharing compatibility unless a later platform/licensing constraint prevents it;
- localization-ready UI/content architecture;
- offline play without proprietary account.

## Explicit 1.0 exclusions

- Workshop / level editor / UGC dependency;
- online leaderboards;
- multiplayer / co-op;
- Remote Play Together as a designed requirement;
- proprietary account/login;
- server backend;
- inventory/trading-market items;
- marketable cosmetics;
- paid gameplay DLC required for the base campaign conclusion;
- daily/online challenge service;
- telemetry required for progression.

Trading cards/profile items may be considered as release-adjacent platform extras only if trivial; they are not a design requirement.

---

# 12. Achievement target and philosophy

Working target: **20–24 Steam achievements**, center **22**.

Suggested families:
- 5 act-completion achievements;
- 1 campaign completion achievement;
- 4 causal-discovery/system achievements tied to meaningful first consequences (not merely clicking a tutorial action);
- 5 mastery-family achievements across Causal Compression / Preservation / Resource Discipline / Stable Causality;
- 3 remix-pack / remix completion achievements;
- 4–6 playful systemic achievements for unusual but legitimate causal outcomes.

Rules:
- no arbitrary `harvest 1000 impacts` grind;
- no achievement for repeated failure/restart/Undo farming;
- no login-day/streak achievements;
- no speedrun/timed completion requirement by default;
- no achievement requires disabling accessibility features;
- no achievement requires a particular input device;
- hidden achievements only for spoiler/discovery reasons, not obscurity for its own sake;
- achievements grant no mechanical power.

---

# 13. Monetization exclusions / expansion boundary

## 13.1 Base game

One premium purchase.

Explicitly forbidden:
- microtransactions;
- paid impact types;
- paid inventory slots;
- paid hints;
- cosmetic store;
- loot boxes/gacha;
- ads;
- subscription;
- battle pass;
- season/event pass;
- paid retry/Undo resources;
- paid progression skips;
- planned withholding of main C01–C34 cases for launch DLC.

## 13.2 Future expansion

No DLC is required for 1.0 completeness.

A future paid expansion is acceptable only if the base game proves demand and the expansion is a coherent substantial new casebook.

Preferred expansion shape:
- new authored causal cases using the existing impact/lineage grammar;
- new theme/presentation family if budget supports it;
- possibly one carefully justified new transform/receiver semantic only through an explicit canonical design reopen and only if it creates enough depth to justify system/QA cost.

Bad expansion shapes:
- one puzzle sold at a time;
- paid stronger impacts or capacity upgrades;
- consumable hint packs;
- cosmetic shop built around token rarity;
- recurring seasonal case cadence.

---

# 14. Commercial / retention risks

## C7-R1 — perceived-value mismatch
Risk: 34 cases sound substantial but may collapse if many are tutorial-thin or ask the same arrow-to-socket question.

Gate: final price review must use actual median first-clear time, causal-variety review, mastery/remix engagement and perceived-value interviews rather than case count alone.

## C7-R2 — `arrow inventory` mis-positioning
Risk: screenshots/UI make impacts look like generic colored ammunition or puzzle keys.

Gate: demo/store capture must show source collision, lineage/provenance and receiver aftermath; at least one trailer sequence must visibly generate a secondary collision and reuse it.

## C7-R3 — quantized physics expectation mismatch
Risk: players buy expecting continuous sandbox physics and call deterministic authored lanes fake/limited.

Gate: store/demo presentation intentionally shows chunky authored sockets, bands, lanes and causal clarity. Do not market `realistic physics`.

## C7-R4 — mastery becomes threshold cleanup
Risk: replay asks the same solution with one fewer impact.

Gate: every mastery contract stores `mastery_distinction_note`; adversarial review rejects marks lacking a distinct causal insight.

## C7-R5 — remix padding
Risk: 10 remixes look like recycled levels.

Gate: every remix must document a changed causal dependency and different dominant reasoning transformation.

## C7-R6 — demo teaches but does not sell
Risk: the first four nodes feel like mechanics training and the product `aha` arrives after demo exit.

Gate: DEMO05 must include deliberate secondary collision lineage reuse and an independent synthesis decision before end card.

## C7-R7 — hint system becomes solution oracle
Risk: retention improves through spoilers while the central reasoning fantasy collapses.

Gate: H1–H3 never prescribe a complete command sequence; H4 is explicit opt-in authored solution guidance.

## C7-R8 — platform feature creep
Risk: Workshop/leaderboards/online challenge systems multiply QA before the core game proves itself.

Gate: all remain excluded unless an explicit scope reopen replaces equivalent cost elsewhere.

## C7-R9 — price anchoring too high
Risk: $19.99 comparison creates expectations of Bionic Bay-level action production/visual spectacle.

Gate: working center stays $16.99; $19.99 requires measured value/polish evidence near launch.

---

# 15. Empirical commercial gates

1. **Hook comprehension:** >=80% representative demo testers can explain that a collision consequence is captured and reused elsewhere without prompting.
2. **Provenance comprehension:** >=70% can explain why two visually similar impacts may differ strategically because their source world-state matters.
3. **Demo second-order proof:** >=60% can describe one deliberate secondary-collision lineage they created/reused rather than merely matching an arrow to a receiver.
4. **Demo desire:** exit interviews show curiosity about later donor chains/self-launch/multi-room causal compression, not only satisfaction with the tutorial novelty.
5. **No grind dependency:** a fresh profile can reach C34 without replaying cleared cases for resources/mastery.
6. **Mastery distinction:** internal review can state one qualitatively different insight for every shipped mastery mark.
7. **Remix distinctness:** every remix passes changed-causal-dependency review.
8. **Store-positioning truth:** representative viewers do not primarily classify the product as a physics sandbox, shooter, vector-programming game or inventory puzzler after the core trailer/demo beat.
9. **Price fairness:** target players judge release-time price fair against actual scope/polish; exact price rechecked near launch.
10. **Platform integrity:** Cloud/demo transfer and Deck/controller support do not require a proprietary online account.

---

# 16. Phase-7 acceptance tests

## Commercial model
- **E7-01** — 1.0 monetization is one premium purchase; no gameplay microtransactions exist.
- **E7-02** — design-time price remains a hypothesis, not hard-coded release canon.
- **E7-03** — working price band is $14.99–$19.99 with center $16.99 pending release-time review.
- **E7-04** — no currency, XP, permanent impact upgrade, rarity or skill-tree progression exists.

## Campaign progression
- **E7-05** — C01–C07 follow the frozen strict teaching chain.
- **E7-06** — Act-II branch/prerequisites match section 5.
- **E7-07** — Act-III branch/prerequisites match section 5.
- **E7-08** — Act-IV branch/prerequisites match section 5.
- **E7-09** — Act-V branch/prerequisites match section 5.
- **E7-10** — C34 is reachable with zero optional mastery marks.
- **E7-11** — no main-case unlock requires replay/farming.
- **E7-12** — progression compiler rejects a case whose required tutorial tags have not been demonstrated by cleared prerequisites.

## Mastery / retention
- **E7-13** — mastery never scores raw Undo, restart, failed attempts, pause/step or elapsed thinking time.
- **E7-14** — accessibility settings never invalidate mastery.
- **E7-15** — mastery grants no mechanical power or permanent inventory increase.
- **E7-16** — every mastery contract contains a nonempty `mastery_distinction_note`.
- **E7-17** — Causal Compression mastery requires a real causal-structure difference, not arbitrary move-count shaving.
- **E7-18** — Stable Causality uses an actual temporal/moving system, never idle waiting.
- **E7-19** — no daily/streak/FOMO/energy retention system exists.

## Remixes
- **E7-20** — 1.0 target contains exactly 10 remixes unless Phase 5 is explicitly reopened.
- **E7-21** — R01–R03 unlock permanently on C14 clear.
- **E7-22** — R04–R07 unlock permanently on C28 clear.
- **E7-23** — R08–R10 unlock permanently on C34 clear.
- **E7-24** — every remix declares source substrate, changed inputs, changed causal dependency and expected new reasoning transformation.
- **E7-25** — a remix changing only starts/art/numeric threshold fails validation.

## Hints / accessibility
- **E7-26** — H1 Rule Reminder contains no move ranking.
- **E7-27** — H2 Conflict Focus identifies systems/facts but not a complete move.
- **E7-28** — H3 Directional Guidance may identify a causal family/room but not a command sequence.
- **E7-29** — H4 Solution Guidance is explicit opt-in and separately authored.
- **E7-30** — using hints never blocks baseline campaign completion.
- **E7-31** — hints do not change collision/token/receiver/deterministic simulation rules.
- **E7-32** — no ordinary achievement requires playing without hints/accessibility features.

## Demo / platform
- **E7-33** — demo necessarily shows one real collision -> portable impact -> remote spend.
- **E7-34** — demo necessarily shows strong-not-always-better/magnitude suitability.
- **E7-35** — DEMO05 necessarily includes a deliberate secondary collision/new lineage reuse before end.
- **E7-36** — demo-to-full import intent is monotonic/idempotent and version-mapped.
- **E7-37** — incompatible demo active state is never synthesized into changed full-game content.
- **E7-38** — compatible settings may transfer independently of incompatible clear state.
- **E7-39** — Steam Cloud is a target, not a requirement for offline play correctness.
- **E7-40** — controller/Deck support remains target scope; no proprietary account is required.

## Achievements / monetization scope
- **E7-41** — achievement target is 20–24 unless later commercial review records a reasoned change.
- **E7-42** — no achievement requires arbitrary high repeated harvest/edit/restart counts.
- **E7-43** — no achievement requires disabling accessibility or a particular input device.
- **E7-44** — Workshop, online leaderboards and server-backed live challenges are not 1.0 requirements.
- **E7-45** — all C01–C34 main campaign cases belong to the premium base-game scope.
- **E7-46** — paid hints, impact upgrades, inventory-slot purchases and gameplay microtransactions are forbidden.
- **E7-47** — any future paid expansion is optional substantial new casebook content and cannot sell power over base cases.

## Commercial integrity
- **E7-48** — store/demo messaging does not call the game a realistic physics sandbox.
- **E7-49** — store/demo messaging shows provenance/world-state and at least one secondary-collision chain, not detached arrow matching only.
- **E7-50** — final release price is rechecked using measured scope/polish/value rather than inheriting the design hypothesis automatically.

---

# 17. Phase-7 closure decision

- Premium commercial frame: **FROZEN FOR DESIGN**
- Exact release price: **INTENTIONALLY OPEN; working hypothesis recorded**
- Campaign progression graph: **FROZEN**
- Progression currency/power economy: **NONE**
- Mastery role: **FROZEN**
- Remix target/unlock policy: **FROZEN — 10 cases**
- Retention philosophy: **FROZEN — no grind/FOMO/live-service loop**
- Hint/assist philosophy: **FROZEN**
- Demo commercial boundary/import intent: **FROZEN ENOUGH FOR TECH SPEC**
- Steam/Deck feature scope: **FROZEN**
- Achievement target/philosophy: **FROZEN**
- Monetization exclusions: **FROZEN**
- Expansion boundary: **FROZEN**
- Empirical commercial gates: **DEFINED**
- Phase-7 acceptance tests: **50**
- Earlier gameplay phase reopened: **NO**
- Production implementation started: **NO**
- Phase 7: **COMPLETE ON PAPER**
- DESIGN COMPLETE: **NO**

## NEXT PHASE

**Phase 8 — Technical Implementation Specification.**

Phase 8 must translate the frozen product/mechanics/content/UX/commercial design into implementation contracts: engine/runtime direction, deterministic domain/presentation separation, canonical state/data model, semantic command/transaction architecture, collision-table/content compiler, lineage/idempotency rules, Undo/Redo/history checkpoints, save/profile/recovery/versioning, Steam Cloud conflict semantics, demo/full import mapping, input abstraction, localization readiness, headless validation/replay harness, performance budgets, implementation slices, failure handling and numbered technical acceptance tests. It must preserve the deliberate stylized/discrete causal-physics model and must not start production implementation.