# GAME #010 — PHASE 3 PRODUCT THESIS

Date: 2026-08-31
Status: THESIS SKELETON LOCKED / PHASE 3 ACTIVE
Selected concept: **Luggage Carousel Zero** *(working title)*

Authority: `START_HERE.md` -> `STATUS.md` -> `GAME_INDEX.md` -> `GAME10_RESEARCH.md` -> `GAME10_TOURNAMENT.md` -> `GAME10_ROUND_B.md` -> `GAME10_ROUND_C.md` -> this file.

## 1. Product identity
**Format:** PC/Steam-first, premium, single-player, offline, deterministic systemic puzzle game.

**One-sentence hook:**
> Swap the labels, not the luggage: shape a moving baggage carousel so every passenger gets the right bag — sometimes by making them wait.

**Core fantasy:** operate a tiny impossible baggage carousel where the bags keep their identities but the meaning of each fixed position can be reassigned. You are not sorting luggage directly; you are arranging the future conditions under which moving luggage will be accepted.

**Differentiator:** the player edits **fixed socket labels** while **bags move through them**. Passengers consume matching bags at one pickup point, leaving persistent circulating gaps. Serving someone changes future permutation state; deliberately failing to serve now can be the correct strategic action.

## 2. Target player
Primary:
- players who enjoy compact deterministic “thinky” puzzle games;
- players comfortable planning 2–6 turns ahead but who do not want programming syntax or opaque hidden information;
- players attracted to strong physical/visual causality and short self-contained levels.

Secondary:
- Steam Deck/controller players seeking one-screen puzzle sessions;
- optimization-minded players who enjoy shortest/clean solution mastery after solving normally.

Not targeted:
- real-time conveyor-management players;
- airport tycoon/simulator audiences expecting economy, building or staff management;
- hidden-deduction / Papers-Please-like inspection gameplay;
- roguelike, inventory-management or automation-factory audiences.

## 3. Session promise
Typical first-solve case: approximately 3–12 minutes, with early teaching cases below that and late mastery cases potentially longer.

A normal session can be one case or a cluster of 3–5. No run loss, grind timer, energy system, daily obligation or live-service cadence.

## 4. Core loop
1. **READ** the carousel: bag traits, fixed socket labels, gaps, pickup, front passenger predicate, queue and remaining tick/swap budget.
2. **PLAN** which bag should eventually satisfy which passenger and which passengers may need to wait.
3. **SWAP** two socket-owned labels within the current bounded edit budget.
4. **PREVIEW** the next simultaneous bag movement and visible pickup predicate inputs without revealing a full future solution.
5. **ADVANCE** one tick.
6. Bags move simultaneously clockwise one socket; the pickup bag is evaluated against the front passenger using immutable bag traits plus the current pickup-socket label.
7. If it matches, bag and passenger are removed; the emptied socket remains a circulating gap. If not, neither is removed.
8. Evaluate success/failure/budget and continue.

The loop is deterministic and reversible through restart/undo policy to be frozen in later phases; no twitch execution is intended.

## 5. Win / fail thesis
A case is won when every required passenger has been served within its defined finite tick/edit budget and any case-specific public completion condition is satisfied.

Failure is explainable, never random. Typical fail reasons:
- tick budget exhausted;
- a required future match has become impossible because the only compatible bag was consumed;
- label phase cannot be repaired within remaining swaps/ticks;
- other explicitly declared finite feasibility loss.

The implementation may allow continued experimentation after logical dead state, but the game must be able to identify/certify dead states for authored content and optional player feedback.

## 6. Frozen minimal vocabulary
Canonical core vocabulary entering Phase 4:
- fixed ring sockets;
- one designated pickup socket baseline;
- socket-owned visible labels;
- bags with immutable visible traits;
- bag/gap permutation around ring;
- public ordered passenger queue;
- public predicates over bag traits + current socket label;
- bounded SWAP LABELS action;
- explicit ADVANCE action;
- simultaneous one-socket movement;
- pickup evaluation after movement;
- successful pickup removes bag + front passenger;
- no compression: empty socket becomes persistent circulating gap;
- finite case budget.

No hidden bag properties, randomness, real-time belt pressure, direct bag movement, inventory grid, combat, economy, worker placement, airport construction or passenger dialogue system is admitted.

## 7. Product-scale content thesis
Initial full-game design target: **36–48 certified strong cases**, subject to Phase-5 proof of reasoning diversity rather than raw count.

Demo target: **6–8 cases** spanning:
1. socket label ownership;
2. bag trait + label conjunction;
3. queue consumption consequence;
4. intentional passenger miss;
5. first circulating gap;
6. multi-tick label staging;
7. compact finale combining those ideas.

Full-game depth should come from combinations of:
- bag substitutability/scarcity;
- predicate overlap;
- label multiplicity;
- gap phase;
- swap budget;
- tick budget;
- consumption order;
- intentional misses;
- future label staging.

Adding a new rule family merely to inflate content is not acceptable.

## 8. Presentation thesis
One primary screen. The carousel itself is the dominant visual object.

Mandatory visual distinction:
- labels are physically/visually fixed to sockets, ideally as overhead gantries/plates;
- bags visibly move beneath/between those fixed structures;
- pickup is spatially unmistakable;
- gaps remain visible as empty moving positions;
- passenger predicate cards use icons + text and never color alone.

1280x800 is first-class. Core cases should remain readable with <=8 sockets unless later empirical testing proves a higher bound safe.

## 9. Commercial/scope thesis
Premium complete product; exact price deferred to Phase 7 market refresh.

Production scope target is deliberately small-to-medium:
- 2D or 2.5D stylized one-screen presentation;
- no networking;
- no voiced narrative requirement;
- no procedural art dependency;
- no massive campaign story;
- no level editor/Workshop promise at thesis stage;
- no DLC/live-service dependency.

The game must be worth buying because the core permutation system sustains mastery, not because it contains a large quantity of bespoke assets.

## 10. Round-C empirical gates carried forward
Before final specification freeze, prototype/playtest must verify:
1. new players understand **labels belong to sockets; bags move** by the second teaching case;
2. intentional waiting reads as clever planning, not arbitrary stalling;
3. 6–8 socket expert cases remain readable at 1280x800/controller distance;
4. simultaneous movement and persistent no-compression gaps are understood without explanation after onboarding;
5. a content corpus can sustain at least 30 strong cases without predicate/rule soup or trace-level repetition;
6. the strongest trailer/GIF can communicate swap -> movement -> pickup consequence in ~10 seconds.

These are empirical gates, not permission to leave rules undefined.

## 11. Scope ceiling / non-goals
Explicitly OUT for Game #010 unless a later phase proves a contradiction requiring reconsideration:
- multiple airports/career-management meta;
- money/upgrades/staff;
- bag inspection or contraband;
- physics luggage handling;
- direct conveyor construction;
- free-roaming character;
- real-time timers;
- hidden passenger preferences;
- procedural infinite mode as a requirement;
- roguelike progression;
- unlockable mechanical rule zoo;
- multiplayer;
- user-generated content commitment.

## 12. Phase-3 remaining work
Phase 3 is not yet fully frozen. Next run should pressure-test and lock:
- exact title status / naming strategy without spending design time on branding;
- target campaign arc and mastery promise;
- exact definition of “public predicate” and allowed predicate vocabulary ceiling;
- whether there is exactly one pickup in canonical game or if multiple pickups must be permanently excluded;
- whether swap budget is per tick, per case, or both as canonical knobs;
- explicit success/dead-state feedback philosophy;
- product thesis acceptance checklist.

Then enter Phase 4 mechanical architecture and specify exact state/action ordering, predicate grammar, budgets, undo/restart semantics, solver state and content-generation knobs.

DESIGN COMPLETE = NO.