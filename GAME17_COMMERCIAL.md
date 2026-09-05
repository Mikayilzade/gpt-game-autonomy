# GAME #017 — THE QUEUE KNOWS — PHASE 7 COMMERCIAL MODEL

Date: 2026-09-05
Status: PHASE 7 COMPLETE
Production implementation: NO
Authority: active Game #017 authority through `GAME17_UX_PRESENTATION.md`.

## 0. Commercial thesis

THE QUEUE KNOWS is a compact premium PC/Steam deduction puzzle whose sellable promise is not “manage queues” but **change a public system so people reveal themselves through deterministic choices**.

Commercial design must preserve that identity. There is no grind economy, live-service loop, consumable hint currency, battle pass, daily task, paid power, random pack, or retention system that pressures play.

The product earns its price through a legible original mechanic, 36-case campaign, 12 optional mastery cases, polished explanation/recovery UX, controller/Steam Deck support and a strong free demo.

---

# 1. Fresh market read — 2026-09-05

Current logic/puzzle pricing spans a wide range. Fresh Steam/market checks show examples around $8.99–$14.99 for smaller logic titles, $19.99 for established substantial puzzle/deduction products, and higher prices for larger adventure/presentation-heavy games. Current examples found include Train45 at $10.99, Squeakross at $14.99, The Artisan of Glimmith at $12.99, Human Resource Machine at $14.99, The Roottrees are Dead at $19.99, Patrick's Parabox at $19.99 and Botany Manor at $24.99.

Commercial inference: THE QUEUE KNOWS should not price as a tiny minimalist puzzle toy, but its current 6–8 hour first-completion target and moderate asset scope also do not justify a $19.99+ assumption before playtest/polish evidence.

Steam currently permits launch discounts from 10% to 40% for 7–14 days. The product should use a modest launch discount rather than train buyers to expect deep discounting immediately.

Research basis:
- SteamDB Logic tag snapshot, checked 2026-09-05: https://steamdb.info/tag/6129/
- Steamworks discounting rules, checked 2026-09-05: https://partner.steamgames.com/doc/marketing/discounts
- Steam demos documentation, checked 2026-09-05: https://partner.steamgames.com/doc/store/application/demos
- Steam achievements documentation, checked 2026-09-05: https://partner.steamgames.com/doc/features/achievements
- Steam Cloud documentation/API, checked 2026-09-05: https://partner.steamgames.com/doc/features/cloud

These references inform commercial/platform constraints, not sales forecasts.

---

# 2. Price lock

## Base MSRP
**$12.99 USD** is the canonical planning MSRP.

Acceptable pre-release adjustment band: **$11.99–$14.99**, only after empirical review of:
- actual median first-completion time;
- final case count after cuts;
- presentation polish;
- demo response;
- comparable market pricing near release.

Moving outside that band is a commercial-design reopen, not a routine implementation choice.

## Launch discount
Canonical plan: **10% launch discount for 7–14 days**.

Allowed test alternative: 15% if pre-release marketing data suggests price friction, but do not assume it improves conversion without evidence.

No 20%+ launch discount is planned. Deeper discounts are post-launch decisions based on actual sales lifecycle and Steam event strategy.

## Regional pricing
Use Steam's current regional-pricing tooling/recommendations as the operational baseline near release, then review outliers manually. Do not hard-code a 2026 regional table into design authority because currency/purchasing-power guidance can change.

---

# 3. Length/value contract

Canonical target from product/content authority remains:
- **first campaign completion: 6–8 hours** median target;
- **completionist campaign + mastery: 9–13 hours** target;
- individual sessions: 15–40 minutes;
- demo: 25–35 minutes.

These are empirical targets, not promises to pad content.

Commercial guardrails:
- never add filler cases merely to reach an hour count;
- if playtesting shows the strongest campaign is 30–32 cases and ~5.5–7 hours, preserve quality and reconsider MSRP within the allowed band rather than pad;
- if final polished campaign naturally exceeds 8 hours, do not inflate price automatically;
- store copy must avoid exact hour claims until measured on external players.

---

# 4. Free demo strategy

## Demo boundary
The free Steam demo is exactly the canonical **QK01–QK06** first chapter/demo arc, targeting 25–35 minutes.

It must demonstrate all six product proof beats:
1. visible self-selection;
2. active diagnostic intervention;
3. deliberately worsening a line for information;
4. congestion contaminating later evidence;
5. sequential observe/control;
6. first synthesis.

The demo ends after QK06 success and a concise causal recap, then presents:
- Continue in Full Game / wishlist-store CTA as platform permits;
- chapter map preview showing five later campaign chapters and optional mastery without spoiling cases;
- accessibility/settings retained.

No demo-exclusive mechanic, currency, cosmetic or grind reward.

## Save carryover
**Desired:** full game recognizes compatible demo progress and offers `Continue from Chapter 2`, while allowing `Replay Chapter 1` at any time.

Technical Phase 8 must choose a robust implementation because Steam demos use a separate appID. Carryover must never be required for ownership/play; if unavailable or unsafe, the full game starts normally and QK01–QK06 remain quick replayable content.

Demo achievements are disabled. Steam's current demo guidance recommends disabling achievements in demos; full-game achievements begin in the paid app.

## Demo marketing role
The mechanic is easier to understand hands-on than from genre labels, so demo conversion is a central empirical gate. The demo is also the preferred Next Fest/showcase build if timing fits release plans.

The demo must have a direct feedback route during pre-release testing, but no mandatory account creation or mailing-list gate.

---

# 5. Progression and retention without grind

Retention comes from curiosity and mastery, not habit pressure.

Canonical progression:
- campaign chapter structure from Phase 5;
- 4-of-6 local chapter flexibility where already specified, with foundation prerequisites preserved;
- two optional mastery cases per chapter;
- mastery never blocks campaign;
- no XP;
- no currency;
- no unlock shop;
- no daily/weekly challenges;
- no login streak;
- no energy/lives;
- no randomized rewards.

The player returns because the next cases create a new causal reasoning problem.

Case-select UI may show:
- completed / uncompleted;
- optional mastery completion;
- best self-imposed challenge badges where applicable;
- no global star score required for progression.

---

# 6. Difficulty and accessibility

Accessibility settings never reduce achievements, progression or narrative access.

Base campaign has one authored logical difficulty. Difficulty is managed through case order, hints and optional mastery rather than separate Easy/Normal/Hard versions that multiply validation burden.

Canonical help ladder:
- normal evaluator/rule inspection;
- evidence review;
- Phase-6 non-answer hint tiers;
- checkpoint/restart.

Optional **challenge modifiers** are allowed only post-campaign or on mastery cases and only when they reuse validator-supported constraints. Candidate families:
- one fewer intervention where a certified solution exists;
- stricter wait ceiling where certified;
- no hint use badge;
- solve with specified lever family unavailable only if certified.

Modifiers:
- never gate campaign endings/content;
- never alter customer heuristics;
- never create exclusive story/reward pressure;
- are not required for base achievements except a small explicit mastery subset.

No speedrun/time-pressure difficulty is canonical.

---

# 7. Achievements

Target: **18–24 Steam achievements**, primarily milestones and alternative reasoning behavior rather than chores.

Families:

## Campaign milestones — ~7
- finish QK01;
- finish demo/chapter 1;
- finish chapters 2–5 at selected milestones;
- finish campaign.

## Mechanic-understanding — ~6
Examples:
- prove a type after deliberately creating a slower queue;
- succeed while at least one non-target remains ambiguous;
- use congestion evidence to eliminate a candidate;
- complete a contingent-policy case where second intervention differs by observed branch;
- prove an all-remaining-world operational guarantee;
- recover from a certified information-dead branch and solve after checkpoint reload.

## Mastery — ~5–8
- first mastery case;
- clear one mastery pair;
- clear all mastery cases;
- selected certified low-budget challenge achievements.

Rules:
- no achievement for repetitive counts such as “resolve 1,000 customers”;
- no missable narrative achievements requiring save manipulation;
- no achievement requiring accessibility options to be disabled;
- hidden achievements only for genuine spoiler protection, not obscurity;
- demo achievements disabled.

---

# 8. Replay incentives

The game does **not** promise procedural endless replay.

Replay value comes from:
- optional mastery cases;
- replaying solved cases to discover alternate certified policies;
- finite pre-certified hidden-world variants in selected mastery/replay cases if Phase 8 supports them cleanly;
- optional certified challenge modifiers;
- evidence/proof understanding rather than score optimization.

A solved case may show `Alternative policies exist` only if validator data proves at least two materially distinct certified policy classes. It must not reveal the alternative action sequence.

No leaderboard is planned. The core game is thoughtful, checkpoint-friendly deduction; global speed rankings would distort the fantasy and accessibility posture.

---

# 9. Steam platform feature scope

Required/strongly targeted:
- Steam Achievements in full game;
- Steam Cloud for campaign/settings save portability;
- full controller support with dynamic glyphs;
- Steam Deck compatibility target already defined in Phase 6;
- Steam Input-compatible semantic action mapping where implementation stack permits;
- demo attached to base product;
- demo-to-full save carryover if robustly implementable;
- localized store page and achievement strings for supported languages.

Not required:
- leaderboards;
- Workshop;
- trading cards at design stage;
- inventory/items;
- multiplayer/social backend;
- mandatory account system.

Cloud conflict handling and demo-save import are Phase-8 technical contracts, not excuses to change game rules.

---

# 10. Monetization and DLC boundaries

Base game: one premium purchase.

Forbidden:
- microtransactions;
- paid hints;
- consumable currency;
- paid heuristic/rule unlocks inside campaign;
- loot boxes/randomized purchases;
- ads;
- subscription requirement;
- day-one puzzle packs carved from the planned 36+12 scope.

Allowed post-launch paid expansion only after base game is complete and received well:
- a substantial authored case pack using the existing five heuristics and frozen rule language;
- new hall visual theme bundled with meaningful new cases;
- soundtrack/artbook as non-gameplay optional purchase.

A sixth heuristic is **not normal DLC**. It requires a design reopen because it changes inference vocabulary, tutorial burden, validator scope and UX.

Free updates may add accessibility, quality-of-life, certified challenge variants and a small number of bonus cases.

---

# 11. Commercial positioning

## Primary category sentence
**A deterministic deduction puzzle about designing the experiment.**

Avoid leading with `queue management`, `tycoon`, `simulation management` or `automation`, because those create the wrong purchase expectation.

## Store short-description direction
`Change signs and counter rules, watch customers choose their own queues, and use those choices as evidence. A deterministic deduction puzzle where the best experiment may make the line worse on purpose.`

## Visual/capsule thesis
The capsule should communicate:
- tiny public service hall;
- visibly different A/B/C counters/signs;
- customers splitting into queues;
- one strong changed sign/lever;
- readable title;
- no spreadsheet UI and no tycoon-money imagery.

A static screenshot should imply “why did these people split?” rather than “how efficiently can I serve them?”

## Trailer proof beats — target 45–70 sec
1. 0–6s: baseline crowd chooses similarly; hook text: `They won't tell you what they need.`
2. 6–14s: player flips FREE/sign/service rule.
3. 14–22s: crowd splits; candidate chips eliminate.
4. 22–32s: `The queue is evidence.` Show immutable snapshot/reason trace.
5. 32–44s: deliberately worse queue creates a useful distinction; later customer behaves unexpectedly because congestion changed.
6. 44–55s: three-counter/two-cohort synthesis and second intervention based on evidence.
7. end: title + `Change the system. Watch what they choose. Deduce why.` + demo/wishlist/release CTA appropriate to campaign stage.

Do not spend trailer time on chapter menus, generic walking animation or a list of 20 features.

---

# 12. Major commercial risks and mitigations

## Risk A — mistaken for queue/tycoon management
Severity: high.
Mitigation: store taxonomy, capsule, first trailer beat, demo QK01 wording and no throughput HUD all emphasize deduction/experiment design.

## Risk B — mechanic looks abstract or academic
Severity: high.
Mitigation: physical signs, tiny hall, character movement, immediate causal split and plain-language reason traces. Avoid marketing term `mechanism design` as the only consumer-facing explanation.

## Risk C — content appears thin for $12.99
Severity: medium/high.
Mitigation: 36+12 target, 6–8h measured campaign target, polished demo, mastery, alternate certified solutions. Cut price within allowed band rather than pad weak cases.

## Risk D — deduction audience assumes story-heavy detective game
Severity: medium.
Mitigation: clearly show systemic puzzle interaction and case structure; do not promise narrative mystery investigation.

## Risk E — demo teaches the whole trick and reduces purchase desire
Severity: medium.
Mitigation: QK01–QK06 prove the identity but later chapter map explicitly shows escalation into congestion, partial proof, contingent policies and three-counter synthesis. Demo ends after first synthesis, not after every late-game reasoning family is exhausted.

## Risk F — puzzle difficulty creates abandonment
Severity: medium/high.
Mitigation: checkpointing, evidence history, Type Lens, non-answer hints, 4-of-6 flexibility and optional mastery. No penalty for hints/accessibility.

## Risk G — weak visual differentiation in crowded puzzle market
Severity: medium.
Mitigation: strong service-hall diorama, physical public-rule props and queue split as the signature GIF/trailer moment; art direction must prioritize legibility and charm over asset volume.

---

# 13. Empirical commercial gates

No sales or wishlist number is forecast as fact. Measure these during prototype/store/demo stages.

## Hook comprehension gate
After viewing a 10–20 sec clip, target qualitative result: most representative testers describe changing the setup to learn from customer choices, not managing throughput.

If they say “queue manager/tycoon,” revise positioning/visual proof before adding features.

## Demo comprehension gate
After QK06, players should be able to explain that interventions create diagnostic behavior and congestion can contaminate evidence.

## Demo completion gate
Track QK01 start -> QK02 -> QK03 -> QK06 completion. Do not set a fabricated universal percentage target before external sample data; investigate sharp drop-offs case-by-case.

## Wishlist/store gate
Track store-page visits -> wishlist and demo installs -> wishlist/purchase where Steam data permits. Compare creative variants and external benchmarks available near campaign time; do not freeze a universal conversion threshold in design authority.

## Price gate
Before release, compare $12.99 against current comparable puzzle titles and measured completion/polish. Adjust only inside $11.99–$14.99 without design reopen.

## Content-value gate
External players should not report material repetition before Chapter 5. If repetition appears earlier, cut/rework cases before increasing count.

## Deck gate
Steam Deck/controller usability must not be marketed as a strength until target-device testing passes Phase-6 acceptance criteria.

---

# 14. Phase-7 acceptance result

Locked:
- premium $12.99 planning MSRP with $11.99–$14.99 empirical adjustment band;
- 10% launch discount baseline;
- 6–8h campaign / 9–13h completionist targets subject to measurement;
- QK01–QK06 free demo and desired save carryover;
- progression without XP/currency/grind/live-service chores;
- 18–24 achievement philosophy/families;
- one authored campaign difficulty plus optional certified mastery modifiers;
- finite replay incentives without procedural promise;
- Steam achievements/cloud/controller/Deck/demo feature targets;
- premium-only monetization and DLC boundaries;
- positioning/capsule/trailer proof beats;
- explicit commercial risks and empirical gates without fabricated forecasts.

**PHASE 7 COMMERCIAL MODEL = COMPLETE.**

No production implementation has begun.

# NEXT DESIGN STEP — PHASE 8 TECHNICAL IMPLEMENTATION SPECIFICATION

Using all active authority through this file, define an implementation-ready technical contract without starting production code:
1. engine/runtime recommendation and alternatives;
2. deterministic simulation architecture and authoritative state boundaries;
3. exact serialized CaseDefinition / save / evidence schemas;
4. hidden-world handling and no-leak boundaries;
5. evaluator/comparator APIs and event ordering;
6. exhaustive validator/solver architecture and proof artifacts;
7. UI presentation-event separation and Type Lens query contract;
8. input abstraction/controller/Deck implementation contract;
9. persistence, checkpoint, Steam Cloud conflict and demo-save import strategy;
10. localization/accessibility data boundaries;
11. performance budgets for 10 customers / 3 counters and solver offline/runtime separation;
12. test hooks, golden traces, property tests and determinism checks;
13. implementation phase order for the dedicated repository;
14. explicit empirical gates that require a prototype but do not reopen mechanics by default;
15. save canonical `GAME17_TECHNICAL_SPEC.md`, update STATUS/GAME_INDEX, and advance to Phase 9 if complete.
