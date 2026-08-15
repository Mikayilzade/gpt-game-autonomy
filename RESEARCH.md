# RESEARCH

Last updated: 2026-08-15
Research state: **initial scan complete; broad discovery still in progress**

This file contains external evidence, hypotheses, candidate concepts, comparisons, and rejected directions. It is intentionally separate from `GAME_BIBLE.md`: research can be messy and probabilistic; the Bible must eventually contain only canonical design decisions.

---

# 1. Research rules

1. Date every market-sensitive conclusion.
2. Distinguish:
   - first-party/platform data;
   - third-party measured data;
   - estimates;
   - journalism/anecdotes;
   - our own inference.
3. A successful reference game proves that a desire exists, not that copying the game will succeed.
4. A rapidly filling microgenre should usually be treated as a warning, not an invitation.
5. Favor durable player motivations over fashion:
   - mastery;
   - transformation;
   - optimization;
   - discovery;
   - collection;
   - expression;
   - risk/reward;
   - problem solving;
   - social stories;
   - visible progress;
   - surprise.
6. Market data informs concept selection but does not replace fun architecture.

---

# 2. Initial August 2026 signals

## 2.1 Steam / PC remains attractive but extremely crowded
Sensor Tower's 2026 State of Gaming report describes another record year for Steam in units, premium game revenue, and number of releases, while also noting that growth was driven primarily by larger AAA/AA publishers. This is a useful two-sided signal: premium PC demand is real, but raw availability is not enough for discovery.

Source:
- https://sensortower.com/report/state-of-gaming-2026

**Inference for this project:** a small game needs a highly legible hook and must not rely on "being a good indie game" as its discovery strategy.

## 2.2 Friend-group / creator-friendly games can outperform expectations
The same Sensor Tower overview highlights 2025 breakout PC/console titles such as R.E.P.O. and PEAK as examples of friend-group experiences rising strongly.

**Caveat:** this does not mean multiplayer is automatically the right scope for us. Multiplayer adds networking, synchronization, lobby/match flow, connection failure states, and much larger QA surface.

**Working interpretation:** borrow the *story-generating* and *watchable* qualities of social games even if the selected game remains single-player.

## 2.3 Depth appears to matter for breakout Steam indies
A Turbine Games analysis of 1,712 Q4 2025 indie Steam launches reports a strong association between longer average playtime and titles crossing its success threshold, and also reports a large multiplayer correlation.

Source:
- https://turbine.games/2026/05/27/steam-indie-success-factors/

**Caveat:** this is third-party analysis and correlation, not causal proof. Long playtime can be a consequence of success and quality rather than a standalone recipe.

**Useful design lesson:** avoid concepts that exhaust their meaningful decisions after 60–120 minutes unless their price/scope is intentionally tiny. Seek recombination and mastery.

## 2.4 Puzzle is currently strong on mobile, but mobile economics differ
PocketGamer.biz, using AppMagic estimates, reported puzzle revenue growing about 20% year over year in H1 2026 and reaching second place by global player spending across the major mobile stores.

Source:
- https://www.pocketgamer.biz/h1-2026-genre-analysis-strategy-stumbles-rpgs-fall-and-puzzle-revenue-ramps-up/

**Caveat:** mobile spending data is heavily shaped by F2P/live-ops economics and cannot be transferred directly to a premium Steam project.

**Useful design lesson:** puzzle-like clarity and repeated solvable tasks remain commercially relevant, but we should look for deeper systems rather than defaulting to match-3 or standard mobile monetization patterns.

## 2.5 Satisfying organization / transformation is a visible 2026 PC trend
PC Gamer's August 10, 2026 Steam review describes a rapid wave of games centered on sorting and tidying, citing the success of *Librarian: Tidy Up the Arcane Library!* and many fast-following titles.

Source:
- https://www.pcgamer.com/gaming-industry/steam-week-in-review-games-about-sorting-1000s-of-mundane-objects-onto-shelves-are-the-new-craze-sweeping-pc-gaming/

The article reports that *Librarian* reached a 29,469 all-time concurrent peak and more than 17,000 very positive reviews at the time, while also listing a large wave of near-term sorting-game imitators.

**Important conclusion:** the underlying desire — converting disorder into visible order — is powerful, but **plain sorting is already becoming crowded extremely fast**. We should extract the transformation satisfaction, not make another shelf-sorting clone.

## 2.6 Repair / diagnosis can create a compact, legible fantasy
Recent 2026 coverage around *ReStory* presents electronics repair as an appealing cozy task fantasy. PC Gamer also framed it as a compact puzzle about running an electronics repair shop.

Reference coverage:
- https://www.pcgamer.com/gaming-industry/steam-week-in-review-games-about-sorting-1000s-of-mundane-objects-onto-shelves-are-the-new-craze-sweeping-pc-gaming/

**Inference:** diagnosis, disassembly, testing, repair, and visible before/after transformation are promising verbs because they can be understood immediately and can support deeper rule interactions than pure placement.

## 2.7 Steam Next Fest evidence favors concepts with strong genre legibility, but estimates are noisy
A June 2026 third-party Next Fest report observes strong performance clusters around RPG, action, strategy/RTS, and co-op, while also warning that Valve does not publish game-level wishlist data and many values are estimates.

Source:
- https://llamagriffin.com/Data/Steam%20Next%20Fest%20June%202026%20Report.html

**Inference:** use such data only as directional evidence. Our project should not select a high-production RPG or survival craft game simply because the category has a high ceiling.

---

# 3. Durable design lessons extracted from the scan

The first research pass suggests the following *combination* is worth optimizing for:

1. **Instantly understandable physical or cognitive verb**
   - inspect;
   - connect;
   - repair;
   - classify;
   - route;
   - assemble;
   - transform;
   - contain;
   - optimize.

2. **Visible before/after state change**
   Players should be able to see chaos become order, broken become functional, unknown become understood, unsafe become contained, inefficient become elegant, etc.

3. **A second-order system that prevents the game from becoming a chore simulator**
   Examples:
   - hidden properties;
   - interacting rules;
   - cascading consequences;
   - scarce tools;
   - risk/reward;
   - changing constraints;
   - procedural contracts;
   - uncertain diagnosis;
   - competing objectives.

4. **Replayable combinations rather than thousands of authored levels**

5. **A screenshot/GIF-friendly spectacle**
   This can be visually modest as long as an action produces readable transformation or surprising consequences.

6. **A concept that remains fun without multiplayer**
   Multiplayer may be evaluated later as an optional multiplier, not a crutch.

---

# 4. Initial scoring framework

Each candidate is scored 1–5 on:

- **H — Hook clarity (20%)**: can the game be explained and shown quickly?
- **D — Systemic depth (20%)**: can simple rules produce mastery and varied decisions?
- **S — Scope fitness (20%)**: can a small AI-assisted project realistically finish it?
- **M — Market distinctiveness (15%)**: is it recognizably different without being incomprehensible?
- **A — Asset efficiency (10%)**: higher score = lower dependence on expensive bespoke content.
- **T — Technical feasibility (10%)**: higher score = lower implementation/QA risk.
- **C — Clipability (5%)**: can play create visually understandable moments worth sharing?

Weighted score:

`Score = 0.20H + 0.20D + 0.20S + 0.15M + 0.10A + 0.10T + 0.05C`

This is a comparison tool, not a truth machine. A candidate with a high score may still die in stress testing if its core loop is boring.

---

# 5. First-pass candidate field

These are deliberately raw product seeds, not final pitches. Names are placeholders.

| ID | Concept seed | Core verb / hook | H | D | S | M | A | T | C | Preliminary score |
|---|---|---|---:|---:|---:|---:|---:|---:|---:|---:|
| C01 | **Curse Appraiser** | Buy/test/appraise strange objects whose hidden properties can help or ruin the shop | 5 | 5 | 4 | 5 | 4 | 4 | 5 | 4.60 |
| C02 | **Impossible Repair Bench** | Diagnose and repair devices whose components obey unusual interacting rules | 5 | 5 | 4 | 5 | 4 | 4 | 5 | 4.60 |
| C03 | **Signal Operator** | Tune, isolate, route, decode, and contain signals on a tactile control desk | 5 | 5 | 4 | 5 | 5 | 4 | 4 | 4.60 |
| C04 | **Living Blueprint** | Assemble mechanisms from modular parts, then watch them physically run or fail | 5 | 5 | 4 | 4 | 4 | 3 | 5 | 4.30 |
| C05 | **Ritual Assembly Line** | Build a tiny production chain where symbolic ingredients interact by rules, not recipes alone | 4 | 5 | 4 | 5 | 4 | 4 | 5 | 4.35 |
| C06 | **Containment Clerk** | Inspect incoming objects/creatures and construct the correct containment procedure from clues | 5 | 4 | 4 | 4 | 4 | 4 | 4 | 4.15 |
| C07 | **One-Room Time Machine** | Rearrange a room; every changed object rewrites later states of the same space | 5 | 5 | 3 | 5 | 4 | 2 | 5 | 4.05 |
| C08 | **Dungeon Maintenance Shift** | Repair traps, clean damage, rebalance hazards, and prepare a dungeon before the next adventurer wave | 5 | 4 | 4 | 4 | 3 | 4 | 5 | 4.10 |
| C09 | **Mechanical Garden** | Grow self-operating mechanical organisms by connecting energy, motion, and behavior modules | 4 | 5 | 3 | 5 | 4 | 3 | 5 | 4.00 |
| C10 | **Anomaly Warehouse** | Organize inventory, but items alter nearby rules, weight, labels, space, or time | 5 | 5 | 4 | 4 | 4 | 3 | 5 | 4.25 |
| C11 | **Memory Forensics** | Reconstruct events by manipulating layered photos/audio/objects and testing hypotheses | 5 | 4 | 3 | 4 | 4 | 4 | 3 | 3.85 |
| C12 | **Micro-Factory Troubleshooter** | Diagnose why a compact factory is failing, then modify the smallest number of links to recover output | 4 | 5 | 5 | 4 | 5 | 5 | 4 | 4.65 |
| C13 | **Organism Cargo** | Pack and transport living cargo whose shapes/needs/interactions change en route | 5 | 4 | 4 | 5 | 4 | 4 | 5 | 4.30 |
| C14 | **Night Archive** | Catalog records whose contents alter each other and expose an evolving hidden system | 4 | 4 | 5 | 3 | 5 | 5 | 3 | 4.20 |
| C15 | **Rulebreaker Janitor** | Clean/restore spaces where each contaminant obeys a different physical rule | 5 | 4 | 4 | 4 | 3 | 4 | 5 | 4.10 |
| C16 | **Tiny Ecosystem Mechanic** | Repair a miniature ecosystem by changing only a few species/resources and observing cascades | 4 | 5 | 3 | 5 | 4 | 3 | 4 | 3.95 |
| C17 | **Contract Alchemist** | Fulfill strange customer requirements by combining materials with discoverable transformation laws | 4 | 5 | 4 | 4 | 4 | 4 | 4 | 4.15 |
| C18 | **Route of Echoes** | Plan routes through a compact map where each trip changes future traversal rules | 4 | 5 | 4 | 5 | 5 | 4 | 3 | 4.35 |

### Notes on strongest first-pass seeds

#### C01 — Curse Appraiser
Promising because appraisal, testing, buying/selling, collection, hidden properties, risk, and shop progression can interact. A cursed item can be both inventory and system modifier. Main danger: drifting into a dialogue-heavy shop simulator or becoming too similar to existing inspection games.

#### C02 — Impossible Repair Bench
Strong tactile fantasy plus visible transformation. Deep version would make diagnosis itself the game: components interact under consistent but discoverable laws. Main danger: requiring too many bespoke device assets and animations. Needs a modular visual system.

#### C03 — Signal Operator
Potentially excellent asset efficiency: one desk/interface can host enormous systemic variety. Signals can have frequencies, modulation, interference, routing, priority, spoofing, decay, and hidden meaning. Main danger: becoming an abstract UI spreadsheet instead of an embodied game. Needs satisfying audiovisual feedback.

#### C05 — Ritual Assembly Line
Could combine optimization with discovery and absurd emergent outcomes. Strong opportunity for reusable modules. Main danger: production-line genres already have sophisticated incumbents; the symbolic/ritual rules must fundamentally change play.

#### C07 — One-Room Time Machine
Exceptional marketing hook if interactions are clear. Reusing one room is asset-efficient, but state dependency and causality are technically dangerous. Must constrain the simulation grammar enough to remain implementable.

#### C10 — Anomaly Warehouse
Extracts the current sorting/organization appeal but adds a systemic layer: placement is not merely aesthetic because objects distort nearby rules. Risk: appearing to be just another 2026 tidy-up game unless the anomaly behavior dominates trailers and screenshots.

#### C12 — Micro-Factory Troubleshooter
Very strong scope score because it can use small discrete puzzle/simulation states and reusable visual modules. Distinguishing feature is *diagnosis and minimal intervention*, not unlimited factory construction. Could produce elegant challenges and seeded scenarios. Risk: hook may look less emotionally evocative than cursed objects or strange signals.

#### C13 — Organism Cargo
Clear spatial puzzle with potential emergent interactions. Living cargo can grow, eat, heat, infect, attract, sleep, emit, merge, or panic. Strong visual comedy and systemic combinations. Risk: physics-heavy implementation if treated too literally; could instead use grid/container rules.

#### C18 — Route of Echoes
Potentially deep with low assets if map rules mutate through travel. Risk: abstract presentation and insufficiently visceral action.

---

# 6. Early directions to treat skeptically

These are not permanent bans, but they currently have a high burden of proof.

## Plain sorting / shelf organization sim
Reason: visible August 2026 wave of fast followers after breakout success. The desire is valid; the literal format is becoming crowded.

## Generic supermarket / retail simulator
Reason: crowded and increasingly clone-like. Requires a much stronger mechanical mutation than a new theme.

## Generic Vampire-Survivors-like
Reason: easy to prototype but difficult to distinguish; much of the value rests on content/balance volume and polish after the basic loop is copied.

## Standard deckbuilder roguelike
Reason: powerful structure, but heavily explored. Any candidate would need a genuinely different information/interaction model rather than a new card theme.

## Open-world survival crafting
Reason: high market ceiling but catastrophic scope for this project's objective. World generation, building, AI, combat, inventory, progression, content, optimization, and QA multiply quickly.

## Multiplayer extraction / co-op horror by default
Reason: strong market/creator signals but networking and social infrastructure can dominate development. Keep social-story design lessons, not necessarily multiplayer implementation.

## Pure narrative adventure / visual novel
Reason: can be excellent, but depth often requires large authored writing/art volume. Only reconsider if the narrative *mechanic* itself creates reusable systemic play.

## Mobile F2P idle game
Reason: deceptively simple front-end but meaningful commercial competition requires acquisition, analytics, live operations, monetization tuning, retention content, and often ad spend.

---

# 7. Questions for the broader Phase 1 scan

The next research cycle should challenge the current field rather than simply polishing it.

1. Which successful low-budget games since 2023 create 10+ hours from a tiny ruleset?
2. Which concepts generate shareable stories without multiplayer?
3. Which recent games demonstrate strong use of a single room, desk, screen, vehicle, machine, or compact environment?
4. Which task fantasies have clear satisfaction but are not yet flooded with direct clones?
5. Which games failed because their core verb became repetitive despite strong aesthetics?
6. Which genres have deceptively high content burdens?
7. What can be made data-driven so that dozens of situations emerge from a small asset library?
8. Which candidate concepts survive when reduced to a one-week primitive prototype?
9. Which candidates still sound interesting with all lore and theme removed?
10. Which candidates can support a compelling demo without giving away most of the game?

---

# 8. Current working hypothesis

Do not lock this yet.

The most promising design territory is currently:

> **A compact workplace / machine / containment fantasy built around an immediately satisfying verb, where ordinary task logic is transformed by hidden interacting rules, producing diagnosis, optimization, visible transformation, and emergent consequences.**

This territory includes C01, C02, C03, C05, C10, C12, and C13 without forcing the final game to be any of them.

Why it is attractive:
- understandable interaction fantasy;
- strong before/after feedback;
- supports systemic depth;
- potentially low environment count;
- data-driven content is possible;
- good GIF/trailer potential;
- can remain single-player;
- does not require photorealism;
- can borrow the satisfaction of current task/organization games without cloning their literal format.

This hypothesis must be attacked in the next phase, not protected.
