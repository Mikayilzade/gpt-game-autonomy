# GAME #008 — ECONOMY / RETENTION / COMMERCIAL MODEL

Last updated: 2026-08-30
Phase: **7 — Economy / Retention / Commercial Model**
Selected concept: **G8C02 Locksmith's Margin**
Working title: **Locksmith's Margin**
Production implementation started: **NO**

This file is the complete Phase-7 authority. It does not change the frozen puzzle grammar. Commercial systems may motivate players to encounter and master cases, but may never distort tests, hints, cuts, information, difficulty, or campaign access into a grind/economy.

---

# 1. Commercial thesis

Locksmith's Margin is a **premium, finite, authored puzzle game**. Its value proposition is a compact tactile system with ~28–32 high-quality cases, a 6-case demo, strong physical presentation, and optional mastery/review after solving.

There is no retention treadmill. The product should be satisfying to finish and leave, while giving interested players reasons to revisit cases for cleaner reasoning and alternate solutions.

## Working USD list price
**Working hypothesis: $17.99 USD.**

**Empirical release-review band: $14.99–$19.99.** Final price is not chosen by competitor parity alone. Before release, reassess against:
- validated main-campaign first-play median;
- percentage of the 28-case quality floor actually shipping;
- demo-to-full perceived depth jump;
- presentation polish and tactile quality;
- accessibility/controller/Deck completeness;
- whether solved review/mastery meaningfully adds value;
- current puzzle-market pricing at release time.

Decision rule:
- **$14.99** is favored if the strong campaign lands near the 28-case floor, median full completion is short, or presentation remains deliberately minimal;
- **$17.99** is baseline if 28–32 cases sustain the intended depth curve with polished tactile presentation and complete UX;
- **$19.99** is justified only if playtesting validates a substantial, consistently strong campaign/replay layer and release polish compares credibly with premium systemic puzzle products.

Do not raise price because case count was padded. Do not lower price merely because the game is puzzle-focused.

## Evidence snapshot (2026-08-30)
Current Steam examples span a wide value band: *Piece by Piece* is $12.99 with 100 handcrafted levels; *A Little to the Left* is $14.99; *Patrick's Parabox* is $19.99 with 350+ handcrafted puzzles; *The Roottrees are Dead* is $19.99; the much larger puzzle-adventure *Blue Prince* lists at $29.99. These are positioning references, not direct content-equivalence claims. The $17.99 hypothesis intentionally sits between compact puzzle pricing and larger/deeper premium puzzle products.

---

# 2. No in-game economy

There is **no gameplay currency** and no resource metagame outside a case.

Forbidden:
- coins, XP, keys-as-currency, crafting materials, energy, lives;
- purchasing hints;
- paying to Undo/Restart;
- star totals required to open later campaign cases;
- daily rewards, login streaks, timers or limited attempts;
- loot, random rewards, gacha, boosters;
- permanent stat upgrades;
- consumable assistance;
- grind to bypass a puzzle.

The only progression resource is **understanding**.

---

# 3. Campaign unlock flow

## 3.1 Main path
Campaign cases unlock by **solving preceding required teaching nodes**, not by scores.

Default flow is mostly linear because the content architecture has a tutorial DAG, but after foundational teaching the player receives small bounded choice clusters:
- C01–C06: linear;
- C07–C12: two-at-a-time local availability where dependencies allow;
- C13–C19: small act clusters, normally 2–3 available cases;
- C20–C26: small clusters preserving prerequisite concepts;
- C27–C30: all become available once their prerequisite concepts are solved;
- C31 unlocks after C27–C30;
- C32 unlocks after C31.

Exact cluster membership is content-validation work; it may not violate the Phase-5 tutorial DAG.

## 3.2 Anti-frustration rule
A player should rarely be blocked from the entire campaign by one non-tutorial mature puzzle. After C06, where dependency permits, at least two unsolved required cases should normally be available.

No skip token economy. If playtests show a specific required case causes abnormal abandonment, fix/reorder the case rather than sell or meter a bypass.

## 3.3 Completion
Base campaign completion means solving C32 after all prerequisite required cases. Optional mastery never changes ending access.

---

# 4. Optional mastery and replay

Mastery is **post-solve information**, not progression power.

## 4.1 Per-case mastery badges
A solved case may expose up to three authored badges selected from:
- **Clean Bench** — solve without Undo;
- **Measured Cuts** — FILE actions at or below an authored validated threshold;
- **Measured Tests** — TEST actions at or below an authored threshold;
- **Final Coverage** — only on cases explicitly authored/validated for simultaneous final-state coverage;
- **Alternate Partition** — complete using a validated materially different key-to-lock coverage partition.

Not every case needs three badges. Thresholds must come from validator/playtest evidence, not arbitrary round numbers.

## 4.2 Mastery rules
- badges unlock only after first ordinary solve, so they do not distract from discovery;
- badges never gate campaign cases, hints, accessibility, endings, achievements required for ordinary completion, or content;
- Undo use is always allowed; `Clean Bench` is merely a replay challenge;
- no time/speedrun badge in the base design;
- no dexterity challenge;
- no `solve without hints` achievement that shames assistance use;
- no requirement to repeat trivial cases dozens of times.

## 4.3 Solved review
After solving, Review mode shows:
- final key vectors and which locks each key actually opened during the winning trace;
- action timeline;
- observed/deduced knowledge progression;
- optional comparison to authored mastery thresholds;
- discovered alternate partition count only where validator can define it honestly;
- Replay from start.

Review never reveals hidden accepted-set data beyond what the completed case is allowed to disclose. After completion, an optional `Reveal Mechanism` educational visualization may show the full fictional accepted sets **only if Phase 8 can implement it cheaply and it cannot be confused with real locksmith instruction**; otherwise omit it.

## 4.4 Replay motivation
Replay comes from:
- seeing a cleaner route after understanding the case;
- finding a different valid partition;
- preserving more margin/fewer cuts;
- completing optional authored mastery;
- revisiting physical solution history.

No randomized daily puzzle is promised. No procedural endless mode is part of launch scope.

---

# 5. Achievement authority

Target **18–24 Steam achievements**; working design uses 20. Achievements are low-maintenance flags over existing deterministic events.

## 5.1 Campaign / understanding achievements
1. **First Turn** — open first required lock.
2. **Read the Mark** — complete C02.
3. **Too Far** — encounter/understand the tutorial TOO_DEEP case by completing C03.
4. **Shared Scar** — open two required locks with the same key in one case.
5. **Margin** — complete C06.
6. **Partitioner** — complete first required multi-blank partition case.
7. **Probe** — complete C12.
8. **Two Ways Fit** — complete first master-branch teaching case.
9. **Wide Enough** — complete first wear/tolerance teaching case.
10. **Behind the Lock** — complete first access-order teaching case.
11. **Convert the Probe** — complete C25.
12. **Three Policies Fail** — complete C29.
13. **Workshop Job** — complete C31.
14. **Locksmith's Margin** — complete C32/main campaign.

## 5.2 Optional expression/mastery achievements
15. **Restraint** — solve an authored eligible case after previewing but not committing a tempting cut, using a deterministic case flag rather than inferred intent.
16. **One Key, Three Opens** — open three required locks with one persistent key in an eligible case.
17. **Second Opinion** — solve an eligible case using a validated alternate partition after previously solving it with another.
18. **Clean Work** — earn Clean Bench on any 10 eligible cases; not all cases.
19. **Measured Hand** — earn Measured Cuts on any 10 eligible cases.
20. **Workshop Mastery** — earn any 30 mastery badges total, with campaign offering materially more than 30 so perfection is unnecessary.

## 5.3 Achievement prohibitions
No achievement may require:
- every case with no Undo;
- never using hints;
- speed/timed execution;
- controller-specific dexterity;
- intentionally losing hundreds of times;
- repeating identical TESTs/actions;
- leaving the game open;
- daily/weekly attendance;
- secret irreversible chores with no readable clue;
- changing accessibility settings off;
- platform-external accounts/social posting;
- real-world locksmith knowledge.

Demo achievements are disabled. If demo completion logically satisfies an achievement, the full game may grant it after safe imported progress is recognized.

---

# 6. Demo commercial strategy

The demo is D01–D06 exactly as Phase 5/6 define it: **20–30 minutes target**, ending immediately after the first strong multi-lock partition payoff.

## 6.1 Storefront job
The demo must prove three things quickly:
1. filing feels tactile and legible;
2. failure is useful information rather than punishment;
3. the game is about preserving one key across several locks, not lockpicking.

Base store page should display the demo prominently above purchase options when commercially appropriate. For Next Fest participation, demo should be live before Valve's press-preview cutoff and have correct categories/tags.

## 6.2 Demo CTA
After D06:
- show the two solved keys physically beside the opened locks;
- one short line: `You learned the margin. The full workshop adds branching fits, worn tolerances, access-order jobs, and 28+ validated cases.`
- primary CTA: `Wishlist / View Full Game` pre-release or `Continue in Full Game` after release;
- secondary: `Replay Demo`, `Settings`, `Feedback`;
- do not show a fake locked skill tree, countdown, sale timer or manipulative urgency.

The CTA may mention only features/content actually expected under frozen scope. If release case count changes, text must update.

## 6.3 Demo save/import
Demo stores a versioned completion/progress record compatible with the full game's import path.

Full game recognition rules:
- recognize D01–D06 completion and tutorial concepts learned;
- never import demo state directly into a mismatched full campaign case;
- offer `Start full campaign with equivalent tutorials marked understood` or `Play from C01`;
- player can replay all tutorials regardless;
- settings/accessibility mappings should import when schema-compatible;
- corrupt/incompatible demo data fails safely without blocking a fresh game.

Steam's current demo documentation supports shared Cloud storage to reduce upgrade friction; exact persistence mechanism is Phase 8 authority.

## 6.4 Demo reviews/feedback
A separate demo store page is optional, not required. Use it only if the extra page/review surface is worth maintaining and all screenshots/text accurately describe demo content. Always provide an obvious feedback route from demo menu/pause during public testing.

---

# 7. Steam/platform feature target

## Required target
- Steam Achievements;
- Steam Cloud for campaign/settings where technically appropriate;
- full controller support path;
- Steam Deck target consistent with Phase 6;
- Family Sharing/default Steam platform behavior where available without custom game logic.

## Nice-to-have only if near-zero maintenance
- Steam Rich Presence: e.g. `Case 18 — Wear Bridge` or `Reviewing a solved case`, with no spoiler details;
- basic Steam Stats only where they directly back achievement counters/mastery and do not become public competitive pressure.

## Explicitly rejected for launch baseline
- leaderboards: encourages speed/optimization pressure inconsistent with thoughtful untimed play and creates cheat/maintenance concerns;
- Workshop/level editor: validator, UX, moderation and content-sharing burden is disproportionate;
- trading cards/items as a design requirement;
- multiplayer/Remote Play-specific features;
- live events/dailies;
- mandatory account linking;
- user-generated lock/key exchange;
- platform-specific gameplay content.

---

# 8. Localization / release-language hypothesis

The game is structurally localization-friendly because critical state is physical + iconographic and there is no large narrative script or voice requirement.

## Baseline production assumption
- English is source language and mandatory release language.
- Architecture must support Unicode, variable text expansion, pluralization where needed, remappable glyph substitution, and localized UI from Phase 8 onward.
- No puzzle solution may depend on English wordplay.
- No essential rule may be baked into texture art.

## Commercial localization hypothesis
At production budgeting, evaluate professional UI/subtitle localization for a compact set such as French, German, Spanish (Spain/LatAm strategy decided commercially), Brazilian Portuguese, Simplified Chinese, Japanese, Korean, and Russian, with additional languages only when cost/market/support evidence justifies them.

**This is not a promised launch-language list.** Final languages require real word count, QA budget, font/rendering checks, store demand and support capacity. Machine translation alone is not sufficient for release-critical puzzle instructions.

---

# 9. Discount, bundle and DLC boundaries

## Discounts
- no fake permanent discounting;
- launch discount, if used, should be modest and conventional rather than designed to make list price fictional;
- later discounts follow platform events/product age; no gameplay changes tied to sale participation;
- price changes must not alter existing players' content entitlement.

No exact launch-discount percentage is frozen in design; decide near release from current Steam conditions.

## Bundles
Cross-game/publisher bundles are allowed later if thematically/commercially sensible and require no game-design changes. Soundtrack bundle is allowed only if an actual soundtrack product exists and rights/production justify it.

## DLC
No gameplay DLC is promised. Launch game must feel complete at base price.

Future paid expansion is allowed only if post-launch evidence supports a genuinely substantial new authored case set that uses the frozen grammar or a clearly scoped expansion grammar. Never cut planned base-campaign cases to manufacture DLC.

Cosmetic DLC is not a production requirement. No key skins are needed to monetize.

---

# 10. Retention ethics / hard monetization boundaries

**Premium purchase is the gameplay baseline.**

Hard NO:
- MTX;
- paid hints;
- paid Undo/Restart;
- paid power/solution reveal;
- consumables;
- ads;
- battle pass;
- FOMO events/rewards;
- artificial waiting timers;
- streaks;
- loot boxes;
- premium currency;
- grind multipliers;
- pre-order gameplay advantage;
- accessibility features sold separately;
- platform-exclusive puzzle rules.

Player time is not a monetization resource.

---

# 11. Commercial empirical gates

Before release pricing/store claims freeze, production must measure:
- D01–D06 median fresh completion: target 20–30 min;
- >=80% of demo completers can explain that preserving compatibility can be better than making one lock `more exact`;
- main campaign validated count >=28 without filler;
- C01–C32 (or final shortened spine) median completion and abandonment by act;
- no single mature required case creates a disproportionate hard-stop without alternate available case/fix;
- mastery replay is treated as optional value, not necessary padding;
- store capsule/trailer tests do not primarily communicate burglary/real lockpicking;
- target players understand `premium finite puzzle game`, not endless sim;
- price review uses then-current Steam comparables and actual finished quality.

If the game ships at the 28-case floor with a materially short completion time, $19.99 is presumptively rejected unless polish/value evidence is unusually strong.

---

# 12. Commercial / progression acceptance tests

### Pricing/value
P01 working USD hypothesis is exactly $17.99 until empirical review.
P02 permitted review band is $14.99–$19.99 unless a documented pre-release market review reopens it.
P03 case-count padding may never justify a higher price.
P04 final price review includes validated campaign length and presentation quality.
P05 28-case floor does not automatically justify $19.99.
P06 price does not change puzzle rules, hint access or difficulty.

### Campaign progression
P07 C01–C06 progression is linear.
P08 post-C06 progression may branch only where tutorial dependencies permit.
P09 no star/mastery count gates a required case.
P10 no currency gates a required case.
P11 optional mastery is never required for C32.
P12 mature campaign should normally offer >=2 available unsolved cases where dependency graph permits.
P13 a blocking case with abnormal abandonment is redesigned/reordered rather than monetized.
P14 campaign completion remains based on required case solves, not score total.

### Mastery/replay
P15 mastery badges appear only after ordinary first solve.
P16 Undo remains available even when Clean Bench exists.
P17 no base mastery requires speed.
P18 no mastery requires disabling accessibility.
P19 Final Coverage exists only on explicitly validated eligible cases.
P20 Alternate Partition requires a validator-recognized materially distinct partition.
P21 mastery thresholds are authored/validated, not arbitrary.
P22 mastery rewards no gameplay power.
P23 replay has no random daily requirement.
P24 no endless/procedural mode is promised at launch.

### Achievements
P25 achievement target remains 18–24 unless implementation evidence justifies a bounded revision.
P26 achievements derive from deterministic existing state/events.
P27 no achievement requires never using hints.
P28 no achievement requires all cases without Undo.
P29 no achievement requires timed/dexterity execution.
P30 no achievement requires repetitive identical action farming.
P31 no achievement requires external account/social action.
P32 no achievement requires real locksmith knowledge.
P33 demo achievements are disabled.
P34 eligible demo achievements can reconcile once in full game without duplicate grants.
P35 optional mastery achievements can be completed without perfecting every case.

### Demo
P36 demo contains D01–D06 only under current content authority.
P37 demo target remains 20–30 minutes.
P38 demo reaches core preserve-margin hook by D05.
P39 demo ends after D06 payoff rather than teasing every later mechanic interactively.
P40 CTA never uses countdown/FOMO or fake locked progression.
P41 CTA case-count claim matches current validated release plan.
P42 demo always offers replay/settings after completion.
P43 public demo has a visible feedback route.
P44 full game can recognize demo completion without requiring import.
P45 corrupt demo data cannot block fresh full-game start.
P46 imported settings never override an unsupported/invalid full-game binding silently.
P47 demo and full-game shared Cloud strategy, if used, is versioned and namespaced safely.

### Steam/platform
P48 achievements are a launch target.
P49 Cloud is a launch target subject to Phase-8 safe conflict/persistence design.
P50 controller/Deck support is not a post-launch commercial stretch goal.
P51 leaderboards are excluded from launch baseline.
P52 Workshop/editor is excluded from launch baseline.
P53 no mandatory external account exists.
P54 Rich Presence is optional and cannot block release.
P55 Steam Stats are used only for low-burden deterministic counters if needed.

### Localization
P56 source strings are externalizable; essential prose is not texture-baked.
P57 puzzle logic never depends on English wordplay.
P58 non-English launch languages are hypotheses until budget/QA validation.
P59 machine translation alone is insufficient for release-critical puzzle text.
P60 controller glyph substitution remains independent of language.

### Monetization/discount/DLC
P61 base game is premium purchase only for gameplay.
P62 no MTX or premium currency exists.
P63 hints/Undo/Restart never cost money or consumables.
P64 no ads exist.
P65 no battle pass/FOMO/streak reward exists.
P66 no artificial wait timer exists.
P67 no accessibility feature is paid DLC.
P68 launch game is complete without promised DLC.
P69 planned base cases cannot be removed to manufacture paid DLC.
P70 bundles do not alter gameplay entitlement/rules.
P71 sale participation never creates exclusive puzzle content.
P72 no exact launch discount is frozen years/iterations ahead of release.

### Integrity
P73 commercial systems may not add a new puzzle verb.
P74 commercial systems may not reveal hidden accepted sets.
P75 commercial systems may not alter TEST cost from free.
P76 commercial systems may not punish Undo.
P77 retention telemetry, if implemented, is not used to manufacture friction.
P78 no achievement/mastery popup interrupts a TEST result before causal feedback is readable.
P79 offline core campaign remains playable without Steam services; unavailable platform achievements/cloud degrade gracefully.
P80 any later commercial-policy change that violates P61–P69 requires explicit design reopening, not silent implementation drift.

**Phase-7 acceptance suite: 80 tests.**

---

# 13. Phase-7 freeze

**PHASE 7 COMPLETE.**

Frozen commercial/progression authority:
- working price $17.99 USD, empirical review band $14.99–$19.99;
- premium finite game, no gameplay economy;
- tutorial-safe campaign unlocks with bounded post-C06 choice;
- optional post-solve mastery/review without gating or grind;
- 20 working Steam achievement designs inside an 18–24 target;
- D01–D06 demo as the main conversion surface with safe recognition/import;
- Achievements + Cloud + controller/Deck as platform targets;
- leaderboards/Workshop/live-service systems rejected;
- localization-ready architecture, but non-English release list remains a production/commercial hypothesis;
- no MTX, paid hints/power, ads, FOMO, timers or promised DLC.

Next authority: Phase 8 must specify engine/runtime direction, deterministic state/data architecture, persistence and demo/full migration, Steam-service abstraction, solver/validator integration, performance, localization implementation readiness, test hooks, and build order without changing this commercial model.