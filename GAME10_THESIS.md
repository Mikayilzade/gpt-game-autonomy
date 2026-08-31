# GAME #010 — PHASE 3 PRODUCT THESIS

Date: 2026-08-31
Status: **PHASE 3 COMPLETE / PRODUCT THESIS LOCKED**
Selected concept: **Luggage Carousel Zero** *(internal working title; not storefront commitment)*

Authority: `START_HERE.md` -> `STATUS.md` -> `GAME_INDEX.md` -> `GAME10_RESEARCH.md` -> `GAME10_TOURNAMENT.md` -> `GAME10_ROUND_B.md` -> `GAME10_ROUND_C.md` -> this file.

## 1. Product identity
PC/Steam-first, premium, single-player, offline deterministic systemic puzzle game.

**Hook:** Swap the labels, not the luggage: shape a moving baggage carousel so every passenger gets the right bag — sometimes by making them wait.

The player edits fixed socket labels while bags move through those sockets. A successful pickup consumes one bag and the front passenger, creating a persistent circulating gap. The strategic identity is planning **which bag is consumed, when it reaches pickup, and which fixed label it inherits there**.

This is not airport management, hidden deduction, real-time sorting, inventory play, conveyor construction or direct bag manipulation.

## 2. Target player and mastery promise
Primary audience: players of compact deterministic thinky games who enjoy 2–6-turn planning, public information, explainable failure and small-rule/high-recombination systems. Secondary: controller/Steam Deck players and optimization-minded players who revisit solved cases for cleaner solutions.

**Mastery promise:** novice play asks “what reaches pickup next?”; intermediate play asks “which bag should this passenger consume?”; expert play coordinates consumption order, moving gaps, label phase and scarce edits several ticks ahead. Difficulty must deepen through interaction density, not a growing rule vocabulary.

Typical first solve: ~3–12 minutes. Early teaching cases may be shorter; late mastery cases may exceed this. A session may be one case or 3–5 cases. No run loss, grind, energy, daily obligation or live-service cadence.

## 3. Campaign arc
Target full product: **36–48 certified strong cases**, grouped into a compact campaign rather than an upgrade tree.

- **Act A — Ownership (6–8):** fixed labels versus moving bags; simple label predicates; one-swap planning.
- **Act B — Identity (7–9):** bag traits + labels; substitutable versus scarce bags.
- **Act C — Consequence (7–9):** passenger queue coupling; intentional misses; consumption changes future feasibility.
- **Act D — Gaps (7–10):** removal-created circulating gaps become timing/phase objects.
- **Act E — Mastery (9–12):** bounded combinations of all prior relationships, duplicate labels, tighter tick/swap budgets and longer dependencies.

Acts describe reasoning emphasis, not newly unlocked mechanical families. Previously learned vocabulary remains sufficient throughout.

Demo target: 6–8 cases reaching the first intentional miss and first gap consequence, ending on a compact multi-passenger dependency.

## 4. Canonical loop
1. READ bags, gaps, fixed socket labels, pickup, public passenger queue and budgets.
2. PLAN future consumption and label phase.
3. SWAP two socket labels, subject to current per-tick allowance; repeat if allowance >1.
4. PREVIEW exactly the next simultaneous movement and visible predicate inputs, not a solved future trace.
5. ADVANCE one tick.
6. Every bag/gap moves one socket clockwise simultaneously.
7. Evaluate the bag now at the sole pickup against the front passenger using immutable bag traits and the pickup socket's current label.
8. On match, remove that bag and passenger; the vacated moving occupancy becomes a gap. On non-match, both remain.
9. Evaluate win, exhausted budget and certified dead state; continue, undo or restart.

## 5. Public predicate vocabulary ceiling
Predicates are always fully visible and use **positive equality clauses only**. Canonical grammar:

`Predicate := Clause | Clause AND Clause | Clause AND Clause AND Clause`

`Clause := LABEL = value | BAG_SHAPE = value | BAG_MARK = value`

Frozen ceilings:
- maximum **3 clauses** per passenger;
- at most one clause from each dimension;
- no OR, NOT, XOR, numeric comparisons, adjacency, history, passenger-specific exceptions, hidden clauses or arbitrary scripting;
- canonical trait dimensions are exactly **shape** and **mark**, plus the socket **label** dimension;
- each case may use a subset; values are case data, not new mechanics;
- visual values require redundant icon/text/pattern support where color is involved.

This ceiling is deliberately restrictive. Content must find depth in permutation/consumption/phase, not Boolean complexity.

## 6. Exactly one pickup
Canonical Game #010 has **exactly one pickup socket in every case**. Multiple pickups are rejected: they multiply simultaneous evaluation/order semantics, weaken the clean queue story and act mainly as a difficulty lever rather than a new fantasy. They are out of scope, not a late-game unlock.

The pickup socket is fixed and cannot be relabeled as a location; its socket-owned gameplay label may be swapped like any other socket label unless case data explicitly freezes a socket for onboarding only. Frozen sockets are tutorial affordances, not a mastery mechanic and should disappear after early teaching.

## 7. Budget knobs
Canonical challenge knobs are:
- **ticks remaining**: per-case finite limit;
- **swaps allowed before each tick**: case-static integer, normally 1, occasionally 0 for teaching/forced observation or 2 for selected mastery cases.

**No total-swap budget** in canonical play. A second cumulative edit currency adds bookkeeping and creates two overlapping scarcity systems. Tick count already prices waiting, while swaps-per-tick prices intervention bandwidth.

A player may ADVANCE without spending all available swaps. Unused swaps do not bank.

## 8. Success, failure, dead state and recovery philosophy
**Success:** all required passengers served before/at the final allowed tick. No score requirement is needed for basic completion.

**Budget failure:** ticks reach zero with passengers remaining.

**Logical dead state:** from the exact current state, no legal sequence within remaining ticks/per-tick swap allowance can serve all remaining passengers. The authored-case solver is authoritative for this determination.

Player-facing philosophy:
- never punish experimentation with irreversible campaign loss;
- provide unlimited Restart and stepwise Undo within a case;
- dead-state detection may immediately flag “No completion remains from here” but must not force-exit; player may inspect, undo or restart;
- explain the latest pickup by clause-level MATCH/MISS feedback;
- do not expose a complete solution, optimal next move or future solver verdict beyond dead/alive status;
- optional hint policy is deferred to UX/commercial phases, but hints may not be required for completion.

## 9. Presentation and scope ceiling
One primary screen; carousel dominates. Labels must look physically bolted to fixed socket gantries while bags visibly travel beneath them. Pickup is unmistakable; gaps are visible occupancies; passenger predicates use icons + text/pattern redundancy. 1280×800 is first-class and core cases target <=8 sockets.

Production scope: stylized 2D/2.5D, no networking, voiced narrative requirement, massive story, procedural-art dependency, Workshop promise, DLC/live-service dependency, money/upgrades/staff, inspection/contraband, physics handling, conveyor construction, free roaming, real-time timers, hidden preferences, roguelike progression, multiplayer or rule-zoo unlocks.

`Luggage Carousel Zero` remains an **internal working title only** until commercial/storefront review. Design documents may use it for continuity; no branding effort is authorized now.

## 10. Empirical gates carried forward
Before specification freeze, prototype/playtest must verify:
1. labels-belong-to-sockets / bags-move is understood by case 2;
2. intentional waiting feels clever rather than arbitrary;
3. 6–8 socket expert cases remain readable at 1280×800/controller distance;
4. simultaneous movement and persistent gaps are understood after onboarding;
5. at least 30 strong cases exist without predicate/rule soup or trace repetition;
6. swap -> movement -> pickup consequence communicates in ~10 seconds;
7. three-clause maximum is readable without turning passenger cards into worksheets.

## 11. Phase-3 acceptance checklist
- [x] One-sentence product identity frozen.
- [x] Target player and mastery promise frozen.
- [x] Session and campaign arc bounded.
- [x] Public predicate grammar ceiling frozen.
- [x] Exactly one canonical pickup frozen.
- [x] Tick and swaps-per-tick budgets frozen; cumulative swap budget rejected.
- [x] Success/dead-state/recovery philosophy frozen.
- [x] Working title explicitly non-commercial.
- [x] Scope ceiling and empirical gates explicit.
- [x] Another session can enter mechanics without redefining the product.

**PHASE 3 COMPLETE. DESIGN COMPLETE = NO.**

Next authority: `GAME10_MECHANICS.md`.