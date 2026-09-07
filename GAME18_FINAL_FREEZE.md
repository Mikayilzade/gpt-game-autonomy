# GAME #018 — FINAL SPECIFICATION FREEZE

Date: 2026-09-07
Game: **LOCAL TIME**
Status: **DESIGN COMPLETE = YES / MIGRATION PENDING**
Production implementation inside factory: **NO**

## 1. Frozen product
LOCAL TIME is a premium single-player deterministic spatial causal puzzle for PC/Steam. The player moves socketed zones of semantic local time around compact diorama towns. Current predicates exist only under present clock coverage; persistent milestones earned on Resolve remain earned after clocks move. The game has no rewind, retrocausality, continuous clock simulation or real-time execution requirement.

Store hook: **Move pockets of local time around a tiny town, lining up bakeries, bridges, flowers and trains that all need different times at once.**

Launch commercial baseline: $14.99 USD, Windows/Steam first, mouse/keyboard + controller, Steam Deck readability target, Steam Cloud/achievements, offline puzzle play, free LT01–LT06 demo with compatible idempotent carryover. Campaign quality floor is 30 cases and mastery baseline is 8. Cases 31–36 and M09–M12 are conditional quality slots and must not be promised until validated.

## 2. Authority order
Implementation must resolve ambiguity in this order:
1. `GAME18_FINAL_FREEZE.md`
2. `GAME18_ADVERSARIAL.md`
3. `GAME18_SIMULATION.md`
4. `GAME18_TECH_SPEC.md`
5. `GAME18_COMMERCIAL.md`
6. `GAME18_UX.md`
7. `GAME18_CONTENT.md`
8. `GAME18_MECHANICS.md`
9. `GAME18_PRODUCT_THESIS.md`
10. `GAME18_TOURNAMENT.md`
11. `GAME18_RESEARCH.md`
12. factory-level `START_HERE.md` only for workflow, not game rules.

Later authority supersedes earlier wording only where they conflict. P9-A/P9-B/P9-C and P10-A–P10-F below are binding repairs.

## 3. Frozen mechanical contract
- Canonical gameplay is a finite deterministic state machine alternating planning and atomic Resolve.
- Clock labels such as 07:55/08:00/08:05 are semantic equality/membership tokens, not elapsed chronology.
- Logical placement is socketed; exact footprints and covered relevant sites are public before commitment.
- Relevant sites cannot receive ambiguous local time. Multi-label coupling must be explicit public COUPLED_CURRENT semantics.
- Planning changes derived NOW predicates immediately but cannot mutate persistent process history.
- Persistent mutation occurs on Resolve from Snapshot0.
- Frozen semantic families are exactly: CURRENT, ADVANCE_ONCE, ORDERED_CHAIN, PERMANENT_LOCKOUT, ACCEPT, DISPATCH, CARRIER_HANDOFF, COUPLED_CURRENT.
- No entity advances more than one ordered-chain state per Resolve.
- Lockout/hazard and beneficial candidates derive from Snapshot0; a protection earned this Resolve cannot rescue same-Resolve exposure.
- Base shipped campaign/mastery forbids `same_resolve_prerequisite=true` and `accept_on_arrival=true`. Using either requires formal reopening of mechanical design and explicit onboarding.
- Newly arrived cargo is accepted no earlier than a later Resolve by baseline rules.
- Every shipped case has a finite authored `resolve_limit`.
- Success is exact public predicate satisfaction, never matching an intended sequence.
- DEAD is claimed only for authored monotonic fatal/budget failure or exact solver certification.
- Same canonical state + action produces the same state and structured reason trace independent of frame rate, animation, input timing or collection iteration order.

## 4. Binding Phase-9 repairs
**P9-A — Persistence generation:** Undo Resolve restores puzzle state/counters but never decrements persistence metadata. Every later persisted mutation receives a newer monotonic `save_generation`.

**P9-B — Finite Resolve graph:** `resolve_limit` is mandatory for every shipped campaign/mastery case, including generous teaching cases.

**P9-C — Finite dispatch:** a carrier-starting DISPATCH consumes a public finite READY -> DISPATCHED-style stage/edge. Unchanged predicates cannot relaunch or automatically continue the same carrier. Each distinct later movement requires a distinct authored finite stage.

## 5. Binding Phase-10 rulings
**P10-A — Repetition topology:** similarity clusters ship only with the hard distinctions defined in `GAME18_ADVERSARIAL.md`; otherwise later duplicates are cut. In particular 08/19, 14/18/29, 26/27/31 and 32/33/36 are explicit review clusters.

**P10-B — Resolve budgets:** teaching/generous, reasoning and mastery-tight are distinct budget classes. Normal campaign cases cannot derive their main interest from globally shortest play.

**P10-C — No base same-beat exceptions:** base shipped content forbids same-Resolve prerequisites and accept-on-arrival.

**P10-D — Carrier ownership:** capacity, occupancy, stage and payload ownership are explicit finite state. Ambiguous simultaneous exclusive claims are invalid authored definitions, never runtime tie-breaks. Reachable unbounded carrier cycles are invalid.

**P10-E — Anti-oracle preview:** preview may expose exact footprint, NOW predicates, ambiguity and factual permanent-risk triggers. It does not automatically expose beneficial Resolve transitions, future objectives, future carrier outcomes, ranked sockets or multi-beat solutions.

**P10-F — Count promise:** 30 campaign + 8 mastery is the floor. 31–36 and M09–M12 are optional quality slots. Cut repetition before adding rules or filler.

## 6. Content and scope freeze
Normal campaign ceilings remain <=3 movable clocks and <=8 logically relevant sites. Content uses the eight frozen semantic families, a bounded reusable town kit, <=10 landmark shells target, <=8 logical object classes target and <=3 carrier shells target. <=2 simultaneous carriers belongs only in late/mastery synthesis.

Campaign dependency ladder remains six chapters: onboarding; persistent ordering; dispatch/accept/carrier; protection/risk; multi-clock spatial coordination; synthesis. LT01–LT06 are the canonical demo/onboarding sequence.

Every Chapter-2+ case requires a one-sentence required insight, written causal proof, anti-enumeration reason, solution witness, repetition signature, nearest-case comparison and cut condition. A solver-successful but humanly enumerative/repetitive case does not ship.

## 7. UX / presentation freeze
The primary visual grammar is **NOW / DONE / LOCKED OUT**. Clock identity is redundant across label + pattern/glyph + silhouette where practical; color is supplemental only. Persistent states never play reverse/rewind presentation. No ticking ambience or backward-clock visual language may imply continuous or reversible time.

Mouse and controller invoke the same domain commands. No precision dragging or pointer emulation is required. At 1280x800 all relevant landmarks, active clock labels, objective state and Resolve controls must remain usable; a board that requires camera hunting fails content review.

Resolve computes canonical result before animation. Skip/fast/motion-reduction/replay alter presentation only. Reason trace explains mutations but never gives future strategy. Undo is named Undo Resolve/Undo Move, not rewind.

## 8. Persistence / platform freeze
Saves serialize versioned canonical domain state, never scene/tween/animation authority. Writes are atomic with validation and last-known-good recovery. Definition-incompatible checkpoints are never guessed/reconstructed; preserve profile completion/settings and restart the affected case when necessary.

Demo -> full import is idempotent and monotonic. Safe profile facts may union; in-progress puzzle checkpoints are selected whole, never field-merged. Demo source saves are not deleted.

Cloud is transport, not gameplay authority. Diverged valid local/cloud generations are preserved and surfaced for explicit conflict handling; wall-clock timestamp alone cannot destructively choose a save. Corrupt cloud data cannot overwrite valid local data. Steam absence never blocks local play/save.

## 9. Dedicated-repository technical handoff
Recommended baseline remains latest stable Godot 4.7.x patch available at implementation bootstrap, GDScript, Windows/Steam first. Pin the exact engine version then. Godot handles scenes/UI/input/render/audio; the authoritative puzzle core remains pure and independent of Nodes, frame time, physics and Steam APIs.

Implementation order:
1. bootstrap + pure domain harness;
2. canonical definitions/state/coverage/hash;
3. Resolve + eight families + LT01–LT03 golden tests;
4. carriers/objectives/undo + LT04–LT06;
5. exact solver + content validator;
6. atomic persistence/migrations/demo import;
7. LT01–LT06 presentation vertical slice + controller/accessibility;
8. Steam adapter/cloud/achievements after local persistence is proven;
9. content population/tooling;
10. adversarial QA, Deck/display/localization/performance and empirical gates;
11. demo/release candidate.

Do not author the full 30–36 cases before the LT01–LT06 vertical slice proves the mechanic and UX.

## 10. Implementation acceptance criteria
A fresh implementation may call the frozen design implemented only when all are true:
1. production domain core is deterministic and scene/frame/platform independent;
2. LT01–LT06 definitions and golden witness/hash/trace tests pass;
3. shuffled storage/iteration order cannot change outcomes;
4. solver invokes the production rule core rather than duplicating mechanics;
5. validator rejects ambiguous coverage, invalid references, forbidden families/flags, unbounded carrier cycles and ambiguous ownership;
6. every shipped case has finite Resolve budget, >=1 solver witness and required human-review metadata;
7. save/load round trip preserves canonical state; interrupted/corrupt writes recover without silent profile loss;
8. Undo creates correct older puzzle state inside a newer persistence generation;
9. demo import is idempotent and cannot regress newer full-game progress;
10. cloud divergence/corruption cannot silently destroy a valid local candidate;
11. mouse/controller reach every puzzle action and target-display readability gates pass;
12. animation/replay/fast mode/motion reduction never affect canonical state;
13. localization never affects rule equality/hash and precision rule text receives terminology/layout QA;
14. all shipped campaign/mastery cases pass solver, repetition, human-proof, readability and anti-enumeration gates;
15. store/demo messaging and onboarding do not present the game as rewind/time travel.

## 11. Empirical prototype/playtest gates
These are intentionally implementation-stage evidence, not unresolved game rules:
- after LT02, target >=80% of first-time testers can explain NOW vs DONE without facilitator correction;
- testers do not primarily infer rewind/time travel from earlier-looking labels;
- LT03 overlapping/multi-clock state is legible at 1280x800 and non-color/high-contrast modes;
- controller users can reach every clock/socket/site/action without pointer emulation;
- factual risk warnings inform without being read as forbidden-move advice;
- default no-transition-oracle preview does not create unacceptable rule-memory friction; any experimental one-beat preview is rejected if it becomes socket scanning;
- LT04 arrival vs later acceptance is understood;
- LT06 works as unguided synthesis and demo feels like a complete arc rather than six tutorials;
- 30 campaign cases + 8 mastery survive novelty/human-proof review; only then validate optional 31–36/M09–M12;
- store/demo audience accepts $14.99 value proposition at actual measured scope/polish;
- bounded reusable art kit remains charming/readable rather than visibly repetitive.

Failure of an empirical gate should first repair presentation/content/cuts. It does not authorize silent new mechanics.

## 12. Explicit out of scope
No time travel, global rewind/fast-forward, past-self clones, continuous timers, global day/night simulation, hidden schedules, RNG-dependent puzzle outcomes, real-time dexterity, arbitrary free-placement logic, physics-driven gameplay state, hidden overlap priority, reverse process transitions, arbitrary per-building scripts, ninth semantic family, same-beat multi-hop cascades, routing/pathfinding gameplay, economy/tycoon layer, factory throughput layer, dialogue-heavy campaign, infinite procedural town, live service, ads, MTX, consumable hints, daily energy/grind, mandatory online play, or runner-up mechanics from Game #018 tournament.

## 13. Freeze verdict
All important gameplay rules, state transitions, information boundaries, content gates, UX semantics, persistence behavior, commercial boundaries, technical architecture and implementation acceptance criteria are specified. Remaining unknowns are empirical validation gates with predetermined repair boundaries.

A fresh implementation session should not need to invent important gameplay.

**DESIGN COMPLETE = YES.**

## 14. Migration state
Intended dedicated repository: `Mikayilzade/local-time`.

Repository lookup on 2026-09-07 returned unavailable/not found. Migration is therefore **PENDING**. Per factory continuity policy, every `GAME18_*` file remains in this factory as a frozen **NON-ACTIVE safety archive** until the dedicated repository exists and migration integrity is verified. Do not delete or treat these files as canon for Game #019.

Factory must immediately advance to Game #019 Phase 1 clean-slate opportunity discovery.