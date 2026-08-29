# GAME #006 — STITCHSPACE — ECONOMY / RETENTION / COMMERCIAL MODEL

Last updated: 2026-08-29
Factory run: **8**
Phase: **7 — Economy / Retention / Commercial Model**
Selected concept: **G6C01 Stitchspace**
Product thesis: **LOCKED**
Mechanical architecture: **COMPLETE ON PAPER**
Content architecture: **COMPLETE ON PAPER**
UX / Presentation Architecture: **COMPLETE ON PAPER**
Economy / Retention / Commercial Model: **COMPLETE ON PAPER**
Production implementation started: **NO**
DESIGN COMPLETE: **NO**

This file is the canonical Phase-7 commercial/progression contract for Stitchspace. It cannot introduce power progression, currencies, grind, login retention, FOMO, consumables, monetized hints, content withholding, mechanical difficulty penalties for accessibility use, or any system that makes the player stronger rather than more knowledgeable.

Where this file conflicts with the frozen Product Thesis / Mechanics / Content / UX architecture, those earlier mechanical/product authorities win unless explicitly amended later.

Current market/platform references checked 2026-08-29:
- `A Little Perspective` — $14.99, released 2026-04-03, 200+ authored spatial/non-Euclidean puzzles, free Steam demo: https://store.steampowered.com/app/3485300/A_Little_Perspective/
- `Patrick's Parabox` — $19.99, systemic spatial puzzle with 350+ authored puzzles and free Steam demo: https://store.steampowered.com/app/1260520/Patricks_Parabox/
- `Chants of Sennaar` — $19.99 and free Steam demo: https://store.steampowered.com/app/1931770/Chants_of_Sennaar/
- Steam hardware recommendations — single-player content should remain offline accessible; automatic cloud saves are recommended; graphics settings should stay per-device: https://partner.steamgames.com/doc/steamhardware/recommendations
- Steam Deck/Machine compatibility — full default controller access required for Verified, Deck-native 1280×800 preferred, readable text floor 9 px and ~12 px recommended where practical: https://partner.steamgames.com/doc/steamhardware/compat
- Steam demos documentation — demo players should have clear routes back to the full game/store/wishlist: https://partner.steamgames.com/doc/store/application/demos

These are market/platform anchors only. They do not turn Stitchspace into any referenced game.

---

# 1. Commercial product position

Stitchspace is a **compact premium single-player systemic spatial puzzle**.

The value proposition is:
- one highly legible unusual verb;
- 34 main authored cases targeted at 5–8 hours first clear;
- no filler/grind required for campaign completion;
- 8 materially distinct optional remixes if anti-isomorphism validation passes;
- optional mastery conditions that reward deeper causal understanding rather than speed or low Undo count;
- polished controller/Deck/accessibility support;
- free representative demo if the product hook survives implementation empirical gates;
- offline play and durable local saves as baseline expectations.

Stitchspace must not attempt to justify value through hundreds of near-duplicate rooms, collectible padding, narrative bloat, a progression currency, cosmetic unlock farming or procedural filler.

The product succeeds commercially if players perceive:

> **“This mechanic keeps producing genuinely different spatial aha moments.”**

It fails if players perceive:

> **“This is a five-dollar portal gimmick stretched into 34 rooms.”**

---

# 2. Design-time price band

## 2.1 Frozen working target

Working US list-price target at design freeze:

**$17.99 USD**

Decision band retained for release review:

**$14.99–$19.99 USD**

This is a design-time commercial assumption, not a promise to ship at exactly $17.99.

## 2.2 Price reasoning

### $14.99 is defensible when
- first-clear content lands near 4–5 hours;
- audiovisual production is deliberately minimal;
- remix/mastery retention is thinner than target;
- demo conversion is good but perceived scale remains modest.

### $17.99 is preferred when
- first clear reliably lands around 5–7 hours for target puzzle players;
- 30+ main cases remain materially non-isomorphic;
- the final third contains real causal depth without new-rule bloat;
- controller/Deck/accessibility polish is strong;
- demo demonstrates replacement/lost-adjacency rather than only impossible-door spectacle.

### $19.99 is defensible only when
- first clear is closer to 6–8 hours without padding;
- optional remixes/mastery create meaningful post-clear value;
- visual/audio identity feels commercially finished rather than graybox-minimal;
- demo/wishlist tests and player value interviews support the ceiling;
- no major empirical readability or repetition gate remains weak.

Price may move outside this band only with fresh release-window market evidence and explicit Phase-11 amendment.

## 2.3 No price justification by raw puzzle count

Puzzle count is not the pricing metric.

A 34-case campaign at high causal density may be stronger value than 100 repetitive rooms. Marketing/store language should communicate:
- compact authored campaign;
- escalating recombination;
- multiple solution character where real;
- optional remixes/mastery;
- no filler.

Do not advertise `34 levels` as the primary commercial headline.

---

# 3. Campaign progression graph

Progression is knowledge-gated by completed main cases, never currency/mastery gated.

## 3.1 Main campaign unlock structure

Main cases are grouped into five visible chapters/bands aligned with Content Architecture.

### Chapter I — RESEAM
Cases: **C01–C06**
Initial availability:
- C01 unlocked at new profile.
- C02 unlocks after C01.
- C03 unlocks after C02.
- C04 and C05 unlock after C03 and may be completed in either order.
- C06 unlocks after both C04 and C05.

Purpose: ensure replacement, orientation and useful disconnection are all learned before broad branching.

### Chapter II — ROUTES THAT VANISH
Cases: **C07–C14**
Unlock:
- C07 and C08 unlock after C06.
- C09 unlocks after either C07 or C08.
- C10 requires C07.
- C11 requires C08.
- C12 requires C09.
- C13 requires C10 + C11.
- C14 requires C12 + C13.

Purpose: allow limited choice while preserving occupancy/two-seam teaching dependencies.

### Chapter III — TOPOLOGY AT WORK
Cases: **C15–C24**
Unlock:
- C15, C16, C17 unlock after C14.
- C18 requires any 2 of C15–C17.
- C19 requires C15 + C16.
- C20 requires C17.
- C21 requires C18.
- C22 requires C19 + C20.
- C23 requires C21.
- C24 requires C22 + C23.

Purpose: create a small fan-out so a player temporarily stuck on one mature reasoning family can continue elsewhere without bypassing necessary concepts.

### Chapter IV — CAUSAL COMPRESSION
Cases: **C25–C31**
Unlock:
- C25, C26 unlock after C24.
- C27 requires either C25 or C26.
- C28 requires both C25 + C26.
- C29 requires C27.
- C30 requires C28 + C29.
- C31 requires C30.

### Chapter V — FINAL RESEAM
Cases: **C32–C34**
Unlock:
- C32 unlocks after C31.
- C33 unlocks after C32.
- C34 unlocks after C33.

Main-campaign completion requires **C34 baseline clear only**.

No mastery, remix, achievement, hint restriction, speed condition, low-Undo requirement or collectible may gate C34.

## 3.2 Chapter completion

A chapter is visually marked complete when all its main cases are baseline-cleared.

Chapter completion may unlock:
- the next chapter;
- appropriate remix pack(s);
- optional gallery/dev-note-style non-gameplay extras if later desired.

It may not unlock mechanical power.

---

# 4. Mastery system

Mastery is optional evidence that the player found a stronger or differently structured causal solution.

## 4.1 Allowed mastery families

Every mastery predicate must fit one of these families:

1. **Useful Disconnection** — satisfy a target using an explicitly meaningful cut/isolation dependency.
2. **Topology Compression** — achieve the goal with a materially more compressed sequence of topology states, but never score raw Undo count.
3. **Preservation** — finish while preserving a specified ordinary route/seam relation/entity accessibility condition.
4. **Entity Order** — complete with an authored causal crossing/order constraint.
5. **Alternate Skeleton** — finish through a materially different solution skeleton validated by the content solver/audit.

## 4.2 Forbidden mastery dimensions

Mastery may not depend on:
- real-time completion time;
- Pause/Step use;
- slowdown/accessibility settings;
- total Undo/Redo count;
- failed attempts/restarts;
- mouse vs keyboard vs controller;
- hidden inputs/actions;
- no-hint purity by default;
- frame precision;
- speed of reading/decision-making.

## 4.3 Mastery visibility

Before baseline clear:
- mastery may be hidden or described only at high level when revealing it would spoil the core case.

After baseline clear:
- mastery predicate becomes explicit;
- player may replay immediately from initial state;
- known mastery status is stored as monotonic profile progress.

Mastery does not change campaign path difficulty or content availability except optional cosmetic/completion records.

---

# 5. Remix retention

Target 1.0 remix count: **8 cases, R01–R08**.

Remixes must pass Phase-5 `changed_causal_dependency` and anti-isomorphism requirements. A remix that only changes socket positions, orientation labels, room art, path length or one numerical threshold is invalid.

## 5.1 Remix packs

### REMIX PACK A — AFTER C14
Unlock: C14 baseline clear.
Cases: **R01–R02**.
Purpose:
- one-seam/two-seam reinterpretation of early concepts;
- prove useful disconnection and orientation can combine without late-game density.

### REMIX PACK B — AFTER C24
Unlock: C24 baseline clear.
Cases: **R03–R05**.
Purpose:
- mature alternate skeletons;
- state-dependent rewiring;
- entity/order variation.

### REMIX PACK C — AFTER C34
Unlock: C34 baseline clear.
Cases: **R06–R08**.
Purpose:
- post-campaign synthesis;
- strongest two-seam patterns;
- at most one rare three-seam remix if Phase-5 three-seam justification passes.

Remix completion is never required to unlock main cases.

## 5.2 No retention treadmill

There is no:
- daily puzzle obligation;
- streak;
- rotating FOMO challenge;
- season;
- weekly reward;
- login bonus;
- energy;
- randomized challenge feed required for completion;
- leaderboard dependency.

If a future free puzzle-of-the-week/community feature is explored, it is post-1.0 optional scope and must not carry exclusive rewards or affect the frozen campaign.

---

# 6. Hint / assist information ladder

Hints change **information only**, never game state or mechanics.

## H0 — No hint
Default normal case presentation.

## H1 — Rule Reminder
Restates the relevant global concept already taught, e.g.:
- `Moving this endpoint removes its old connection.`
- `Crossing orientation follows the socket pair shown in preview.`

No case-specific target is highlighted.

## H2 — Causal Conflict Focus
Highlights one currently relevant fact without stating an action:
- old adjacency that is preventing isolation;
- entity that must cross before a route disappears;
- ordinary passage that keeps a loop alive;
- crossing orientation mismatch.

No target socket is selected for the player.

## H3 — Directional Guidance
States the next causal category/goal family, not the exact move, e.g.:
- `Get the crate across before removing its current seam route.`
- `You need this region disconnected at completion.`
- `The next useful topology state must preserve a return path.`

May frame 1–2 relevant rooms/entities but not give a full command sequence.

## H4 — Solution Guidance
Explicit opt-in after a second confirmation.
May provide:
- one next semantic action;
- then progressive next actions on repeated request;
- eventually a full known baseline fixture if the player explicitly requests it.

H4 is not shame-marked and does not invalidate baseline campaign completion.

## 6.1 Hint timing

No automatic timer says `need a hint?` merely because the player thinks slowly.

The UI may make Hint accessible persistently after onboarding. A subtle optional reminder may appear after repeated restarts without progress, but never based only on elapsed real time.

## 6.2 Hint achievements

There is **no default achievement for completing the campaign without hints**. This avoids punishing accessibility/cognitive support use and prevents the hint system from being treated as failure.

A later achievement could recognize discovering an optional alternate solution independently only if it does not infer hidden hint purity.

---

# 7. Difficulty and accessibility relationship

Stitchspace has one canonical mechanical ruleset.

Difficulty adjustment is primarily through:
- information presentation;
- optional preview persistence;
- hint depth;
- Pause/Step availability;
- high-clarity labels;
- reduced motion;
- input remapping;
- UI scale;
- optional camera/navigation conveniences.

These do not alter:
- topology legality;
- endpoint replacement semantics;
- crossing orientation;
- occupancy;
- mover rules;
- solution state.

## 7.1 No punitive `easy mode`

There is no need for a separate mechanically easier campaign at design freeze.

If implementation playtests prove a specific case has excessive branching rather than productive reasoning, repair/cut the content before adding a rule-changing assist.

## 7.2 Optional high-clarity assists

Allowed:
- keep OLD and NEW adjacency preview visible longer;
- label rooms/sockets persistently;
- stronger focus outlines/patterns;
- show orientation ghost until commit/cancel;
- keep topology overview pinned while paused;
- let player Step deterministic movers one canonical movement unit at a time.

Use of these assists never blocks ordinary achievements/mastery unless a mastery explicitly requires a causal fact that an assist would literally solve for the player; default rule is still **do not invalidate mastery for accessibility settings**.

---

# 8. Achievement boundaries

Target launch achievement count: **14–20**, recommended initial design set: **16**.

Achievements exist to mark progression/interesting understanding, not to force grind.

## 8.1 Proposed achievement set

### Campaign milestones — 6
1. Clear C06 / Chapter I.
2. Clear C14 / Chapter II.
3. Clear C24 / Chapter III.
4. Clear C31 / Chapter IV.
5. Clear C34 / campaign.
6. Clear all 34 main cases.

### Understanding / optional feats — 6
7. First mastery predicate completed.
8. Complete mastery in one case from each campaign band that has mastery available.
9. Clear a validated alternate-skeleton case using two distinct accepted skeleton families across separate runs.
10. Complete a case whose first useful topology change reduces reachability (`cut before connect`).
11. Complete a rare justified three-seam case if one ships.
12. Complete a state-dependent mover/occupancy case while using Pause/Step at least once — explicitly normalizing accessibility tools rather than stigmatizing them.

### Remix — 3
13. Clear Remix Pack A.
14. Clear Remix Pack B.
15. Clear Remix Pack C / all shipped remixes.

### Discovery / full understanding — 1
16. Reach a documented optional topology state/alternate route that content intentionally supports and can detect deterministically without hidden dexterity.

Exact names/flavor copy remain implementation/presentation freedom.

## 8.2 Forbidden achievements

Do not ship achievements for:
- zero Undo;
- zero restarts;
- no hints;
- no Pause/Step;
- real-time speedruns as baseline platform achievements;
- controller-only or mouse-only play;
- repeated grinding/total endpoint move counts;
- launching game X days in a row;
- daily/weekly participation;
- inaccessible hidden input sequences.

Community speedrunning remains welcome, but is not built into campaign progression requirements.

---

# 9. Demo commercial contract

The free demo is strongly preferred if the implemented hook passes empirical gates.

Target duration: **15–25 minutes** for a first-time target player.

Exactly five authored commercial-proof cases:
- DEMO01: existing seam -> physical crossing;
- DEMO02: endpoint replacement and visible old-route destruction;
- DEMO03: orientation consequence;
- DEMO04: useful disconnection / entity-before-cut;
- DEMO05: state-dependent replacement synthesis that cannot be summarized as `place exit near goal`.

## 9.1 Demo must prove

Before the demo ends, the player should have personally experienced:
1. seam adjacency is physical, not teleport UI;
2. moving an endpoint destroys the old adjacency;
3. disconnection can be useful;
4. crossing orientation matters physically;
5. topology is reused after entity state changes;
6. Undo/Redo supports experimentation;
7. the game is not about dexterity.

If DEMO05 has not demonstrated state-dependent replacement, the demo is commercially incomplete even if it looks visually impressive.

## 9.2 Demo endpoint

End screen includes:
- concise recap of what the player did, not feature-count marketing;
- `Wishlist / View Full Game` primary platform action where Steam supports it;
- Continue/Replay demo cases;
- settings/accessibility retained;
- no artificial `buy now to see the answer` cliffhanger.

The demo should stop after a satisfying complete aha moment.

---

# 10. Demo -> full transition and import

Demo and full game use distinct app/content identity but compatible versioned progress mapping.

## 10.1 Importable state

May import:
- accessibility settings;
- input remaps where compatible;
- audio settings where safe across devices;
- DEMO01–DEMO05 clear facts;
- tutorial concept flags that exactly map to full-game concept IDs.

Should not import:
- device-specific resolution/render settings through Cloud;
- active mid-case demo transient state into an unrelated campaign case;
- inferred main-case clears merely because a demo case resembles C01–C06.

## 10.2 Explicit mapping table

Implementation must define a versioned table:
`demo_content_version + demo_fact -> full_profile_fact`.

Import is:
- monotonic;
- idempotent;
- safe to repeat;
- never removes full-game progress;
- never grants a main case clear unless explicitly version-mapped as the same canonical case (default: demo cases are distinct, so no main-case clear mapping).

## 10.3 First full-game boot after demo

Offer:
- `Start Campaign` (recommended) while honoring tutorial familiarity;
- settings/import explanation only if an import actually occurred.

The full campaign should not dump a returning demo player into C07. C01–C06 pacing may shorten tooltips based on imported tutorial flags, but core cases remain playable because they teach campaign-specific causal structure.

---

# 11. Steam / Deck feature scope

## 11.1 Required/targeted for 1.0

- Windows PC Steam release baseline.
- Full mouse+keyboard.
- Full keyboard-only.
- Full controller-only.
- Steam Deck 1280×800 target layout.
- Offline access to all single-player campaign/demo content after normal Steam installation/licensing behavior.
- Local durable saves independent of Cloud availability.
- Steam Cloud strongly targeted for profile/progress save transfer.
- Steam Achievements if implementation overhead remains modest and deterministic.
- controller glyph switching appropriate to active input.
- store/demo linking compliant with current Steam demo flows.

## 11.2 Steam Cloud boundary

Cloud is transport, never authority for game rules.

Clouded:
- profile progression;
- baseline/mastery/remix facts;
- compatible active-case canonical checkpoint if conflict-safe architecture supports it;
- input remaps only if cross-device semantics are safe (implementation may choose local-only remaps if device conflicts are likely).

Prefer local-only/per-device:
- graphics resolution;
- display mode;
- performance preset;
- device-specific rendering options;
- controller glyph override when hardware-specific.

On Cloud conflict:
- monotonic profile facts may merge if version-compatible;
- divergent active-case states must not synthesize a hybrid topology;
- preserve both/recover newest valid branch using Phase-8 persistence policy rather than inventing topology from partial state.

## 11.3 Offline guarantee

Loss of Steam network/Cloud must not block:
- boot after normal installed entitlement context;
- loading local progress;
- playing/clearing cases;
- earning local pending achievement facts;
- saving locally;
- replay/remix/mastery.

Platform achievement submission may retry later.

No mandatory publisher account.

---

# 12. Monetization exclusions

1.0 monetization model: **one premium purchase**.

Explicitly excluded:
- ads;
- microtransactions;
- paid hints;
- consumables;
- paid seam skins as launch economy;
- loot boxes;
- battle pass;
- premium currency;
- energy/lives;
- subscriptions;
- boosters;
- paid retries/Undo;
- paid challenge keys;
- time gates;
- pre-order mechanical power;
- deluxe edition with withheld core puzzles/mechanics;
- NFT/blockchain ownership systems;
- telemetry-driven dynamic monetization.

A soundtrack/artbook/supporter bundle may be considered later because it does not alter gameplay, but it is outside frozen 1.0 gameplay scope.

---

# 13. Post-1.0 expansion boundaries

Post-launch paid expansion is allowed only if 1.0 already feels complete.

Valid expansion directions:
- a new authored case pack using the same primitive grammar;
- genuinely distinct remix/synthesis cases;
- optional visual/thematic district with same mechanical rules;
- new campaign branch only if it explores a causal topology family not exhausted in 1.0.

Default invalid expansion strategy:
- invent many seam powers/elements to manufacture DLC;
- withhold core two-seam/three-seam reasoning from 1.0;
- sell solution hints;
- convert remixes into recurring paid challenge drops;
- add multiplayer/live-service solely for retention;
- make free update content required to understand the base campaign ending.

A new primitive mechanic belongs in an expansion only after the base grammar is proven and only if it creates a real second-order design space rather than feature inflation.

---

# 14. Retention thesis

Retention comes from unresolved curiosity, not obligation.

Desired reasons to continue:
- `I now understand cuts; what happens with two seams?`
- `There must be a cleaner topology plan.`
- `I solved it through orientation; can I solve it through isolation?`
- `I want to see the final synthesis.`

Not desired:
- `I need more currency.`
- `I lose my streak.`
- `I have to grind 3 stars.`
- `The next case is time-gated.`
- `I must replay easy rooms to unlock C34.`

The Case Board may show:
- main clear;
- optional mastery mark;
- optional alternate-solution/remix status;
- chapter completion.

It must not look like a mobile progression economy dashboard.

---

# 15. Commercial and perceived-value risks

## C7-R1 — `Portal clone` interpretation
Risk: impossible adjacent rooms are marketed visually before the atomic loss/replacement rule is understood.

Mitigation:
- trailer/store/demo must show OLD connection disappearing in the same beat as NEW connection appears;
- show an object/player stranded or protected by the removed route;
- avoid portal-gun language/color-pair imagery.

Gate:
- after demo, clear majority of representative testers should explain that a seam endpoint is **moved/reused**, not spawned as another independent portal.

## C7-R2 — low perceived content volume
Risk: 34 compact cases look thin next to puzzle games advertising 100–350 puzzles.

Mitigation:
- sell causal density, not count;
- target 5–8 real hours;
- strong chapter escalation;
- optional remix/mastery;
- polished physical-world presentation.

Gate:
- value interviews after 60–90 minute prototype/content sample should not predominantly predict a sub-$10 product if final polish/content targets are explained accurately.

## C7-R3 — repetition after one seam aha
Risk: player understands endpoint replacement and subsequent cases feel like socket permutations.

Gate:
- mature C15–C34 reasoning-isomorphism audit must satisfy Phase-5 window constraints;
- playtesters should identify materially different reasoning categories (cut/isolate, preserve, orientation, entity order, loop, state-dependent rewire) without being prompted with those labels.

## C7-R4 — price ceiling unsupported
Risk: $19.99 is chosen because references charge it, while Stitchspace lacks comparable duration/polish.

Gate:
- retain $17.99 working target; move to $19.99 only after first-clear duration, demo value perception and production polish support it.

## C7-R5 — demo gives away entire trick
Risk: demo proves endpoint replacement but full campaign appears to offer only more complex versions of the same exact puzzle.

Mitigation:
- demo demonstrates core hook but not two-seam mature grammar;
- store/trailer may tease two-seam consequence without teaching solutions;
- full-game value is recombination, not secret mechanics.

Gate:
- demo exit survey/observation should produce curiosity about `what happens with two seams / moving entities / harder cuts`, not `I think I've seen the whole game` as dominant response.

## C7-R6 — optional content becomes grind
Risk: mastery/remix marks become implicit requirements for completionism and exhaust players.

Gate:
- C34 reachable with zero mastery/remix;
- no profile power attached;
- remix count remains <=10 unless anti-isomorphism proves more genuine value.

## C7-R7 — hints stigmatized
Risk: achievements/UI imply hints are cheating, reducing accessibility.

Gate:
- no-hint campaign achievement absent;
- baseline completion unaffected;
- H4 requires explicit consent but no shame language.

## C7-R8 — Deck promise without quality
Risk: marketing says Deck-friendly but focus/readability/controller ambiguity remains.

Gate:
- Phase-6 U6 gates + physical-device validation before `Deck-friendly/Verified` promotional claim;
- do not claim Verified before Valve's actual compatibility result.

## C7-R9 — Cloud dependency harms offline product
Risk: sync failure blocks local campaign or corrupts topology progress.

Gate:
- local save remains authoritative for offline session;
- Cloud disabled/unavailable test passes all single-player flows;
- divergence never creates hybrid active-case state.

## C7-R10 — expansion pressure contaminates 1.0
Risk: core grammar is deliberately underused to reserve ideas for DLC.

Gate:
- C34 must deliver full frozen 1.0 synthesis;
- post-1.0 roadmap cannot remove any Phase-5 required campaign reasoning family from base game.

---

# 16. Commercial telemetry boundaries

Optional privacy-respecting product telemetry may measure aggregate, non-essential facts only if implementation/legal review supports it:
- demo completion rate;
- case completion funnel;
- hint tier requested;
- restart/Undo aggregates;
- controller/input category;
- crash/performance data.

Telemetry must not be required for offline play.

Do not use telemetry to:
- dynamically alter prices;
- manipulate difficulty per individual spending behavior;
- monetize frustration;
- create hidden player scores affecting content availability.

The game remains fully functional with analytics disabled/unavailable.

---

# 17. Phase-7 acceptance tests

## Product / price
- **C7-01** Product is one-time premium single-player with no gameplay microtransaction economy.
- **C7-02** Working design-time US list price is $17.99 with explicit $14.99–$19.99 release-review band.
- **C7-03** Price is not justified solely by raw puzzle count.
- **C7-04** $19.99 requires documented duration/polish/value evidence rather than analogue copying.
- **C7-05** First-clear target remains 5–8 hours; ~4 hours remains a commercial warning threshold.

## Campaign progression
- **C7-06** C01 is available on a new profile.
- **C7-07** Every main-case prerequisite in the Phase-7 graph is acyclic.
- **C7-08** C14 cannot unlock before the occupancy/two-seam teaching prerequisites required by Content Architecture.
- **C7-09** C24 requires mature two-seam/state-dependent prerequisites.
- **C7-10** C34 requires main-campaign predecessors only.
- **C7-11** C34 is reachable with zero mastery completions.
- **C7-12** C34 is reachable with zero remix completions.
- **C7-13** No currency/XP/collectible total gates a main case.
- **C7-14** Chapter branching gives at least one temporary alternate case path where specified without bypassing primitive teaching order.

## Mastery
- **C7-15** Every mastery predicate maps to an allowed mastery family.
- **C7-16** No mastery uses raw real-time completion time.
- **C7-17** No mastery uses raw Undo/Redo/restart count.
- **C7-18** Pause/Step/slowdown/accessibility use does not invalidate ordinary mastery by default.
- **C7-19** Mastery status is monotonic profile progress.
- **C7-20** Mastery never grants mechanical power or permanent seam capacity.

## Remix
- **C7-21** 1.0 target remix count is 8 and remains inside Phase-5 anti-isomorphism rules.
- **C7-22** R01–R02 unlock from C14 main clear only.
- **C7-23** R03–R05 unlock from C24 main clear only.
- **C7-24** R06–R08 unlock from C34 main clear only.
- **C7-25** Remix completion never gates main-campaign progression.
- **C7-26** Every remix records a changed causal dependency, not cosmetic socket/geometry difference only.

## Hints / difficulty
- **C7-27** H1 provides rule reminder only.
- **C7-28** H2 highlights a causal conflict/fact without choosing the exact action.
- **C7-29** H3 provides directional causal guidance without full command sequence.
- **C7-30** H4 explicit solution guidance requires deliberate opt-in.
- **C7-31** Hints do not mutate topology or game rules.
- **C7-32** Baseline campaign completion remains valid after any hint tier.
- **C7-33** No automatic hint prompt is triggered solely by elapsed thinking time.
- **C7-34** No separate mechanically easier ruleset is required at design freeze.

## Achievements
- **C7-35** Launch achievement target remains bounded around 14–20; proposed set is 16.
- **C7-36** No achievement requires zero Undo/restarts.
- **C7-37** No achievement requires no hints.
- **C7-38** No achievement penalizes Pause/Step/accessibility.
- **C7-39** No achievement requires a particular input device.
- **C7-40** No achievement requires daily streak/login/grind counts.
- **C7-41** Achievement facts are deterministic and may queue offline for later platform submission.

## Demo
- **C7-42** Demo has exactly five authored commercial-proof cases at target scope.
- **C7-43** Demo reaches useful disconnection before ending.
- **C7-44** Demo reaches state-dependent replacement before ending.
- **C7-45** Demo communicates old adjacency loss in the same core loop as new adjacency creation.
- **C7-46** Demo includes a clear full-game/wishlist navigation path supported by Steam configuration.
- **C7-47** Demo ends after a completed aha, not an answer-withheld purchase cliffhanger.
- **C7-48** Demo does not need to expose mature two-seam campaign depth as playable content.

## Demo import
- **C7-49** Demo import is versioned and explicit.
- **C7-50** Demo import is monotonic and idempotent.
- **C7-51** Demo import never deletes newer full-game progress.
- **C7-52** Demo clears do not infer main-case clears by similarity.
- **C7-53** Compatible tutorial familiarity/settings may transfer without skipping required campaign structure.

## Steam / Deck / offline
- **C7-54** All single-player campaign content remains playable without active network connection after normal installation/licensing context.
- **C7-55** Steam Cloud outage does not block local load/save/clear.
- **C7-56** Device-specific graphics settings are not required to roam through Cloud.
- **C7-57** Full controller access remains a 1.0 target consistent with Phase 6.
- **C7-58** 1280×800 Deck target remains supported.
- **C7-59** Game does not claim Steam Deck Verified before an actual Valve compatibility result.
- **C7-60** Divergent active-case Cloud states cannot be merged into a synthetic hybrid topology.

## Monetization / retention
- **C7-61** No ads/microtransactions/premium currency/energy/lives/battle pass/loot box exist in 1.0.
- **C7-62** No paid hints or paid Undo/retries exist.
- **C7-63** No daily/weekly/FOMO content is required for campaign or completion records.
- **C7-64** No core mechanic/campaign reasoning family is withheld to manufacture DLC.
- **C7-65** Optional soundtrack/artbook/supporter products, if any, never change gameplay.
- **C7-66** Post-1.0 case packs may extend authored content only after base game is complete.

## Commercial empirical gates
- **C7-67** Demo testers predominantly describe endpoint reuse/replacement rather than independent portal placement.
- **C7-68** Mature-content testers can distinguish multiple reasoning families beyond socket permutation.
- **C7-69** Demo exit feedback does not predominantly say the entire game has already been exhausted conceptually.
- **C7-70** Final price selection records observed duration, perceived value and polish evidence.
- **C7-71** Offline fault test proves local single-player remains functional with platform/cloud unavailable.
- **C7-72** Deck-friendly marketing wording is used only after actual representative-device validation.

---

# 18. Phase-7 closure

- Premium purchase model: **FROZEN**
- Working price target / decision band: **FROZEN — $17.99 / $14.99–$19.99**
- Campaign unlock graph: **FROZEN**
- C34 zero-mastery/remix gating: **FROZEN**
- Mastery families/boundaries: **FROZEN**
- Remix packs/unlock pacing: **FROZEN**
- Hint ladder H0–H4: **FROZEN**
- Difficulty/accessibility relationship: **FROZEN**
- Achievement boundaries / proposed set: **FROZEN**
- Demo commercial contract: **FROZEN**
- Demo -> full import semantics: **FROZEN**
- Steam/Deck/offline/Cloud scope: **FROZEN**
- Monetization exclusions: **FROZEN**
- Retention thesis: **FROZEN**
- Post-1.0 expansion boundaries: **FROZEN**
- Commercial empirical gates: **10 explicit risks/gates**
- Phase-7 acceptance tests: **72**
- Earlier phase reopened: **NO**
- Production implementation started: **NO**
- Phase 7 complete on paper: **YES**
- DESIGN COMPLETE: **NO**

## NEXT PHASE

**Phase 8 — Technical Implementation Specification.**

Phase 8 must now freeze the implementation architecture without starting production code: engine/version direction, deterministic Domain Core, canonical state/command transactions, typed content schema/compiler, movement/crossing resolution, canonical serialization/hash, Undo/Redo checkpoints, local persistence/temp-primary-backup recovery, Steam Cloud adapter boundary, demo import mapping, profile progression graph, semantic input/focus architecture, presentation-domain separation, solver/test hooks, performance budgets, localization readiness, support/replay bundle and implementation order through 12A–12H.