# GAME #018 — PHASE 3 PRODUCT THESIS LOCK

Date: 2026-09-06
Selected concept: **LOCAL TIME**
Status: PRODUCT THESIS LOCKED — MECHANICAL ARCHITECTURE NEXT
Production implementation: NO
Authority: below `START_HERE.md`, `STATUS.md`, `GAME_INDEX.md`, `GAME18_RESEARCH.md`, `GAME18_TOURNAMENT.md`.

## 1. Product identity
**Working title:** LOCAL TIME

**Genre frame:** single-player deterministic spatial scheduling / causal puzzle in compact diorama towns.

**Platform baseline:** PC / Steam first; full mouse and controller support; Steam Deck readability is a baseline constraint.

**Target player:** players who like compact systemic puzzles, visible cause-and-effect, planning and “aha” causal chains, but do not want dexterity, time-loop execution, programming syntax, large simulations or hidden-rule guessing.

**One-sentence store hook:**
> Move pockets of local time around a tiny town, lining up bakeries, bridges, flowers and trains that all need different times at once.

## 2. Core fantasy
The town does not share one clock. You physically move small clock-zones over buildings and processes so neighboring places can simultaneously experience different public times.

The fantasy is not “rewind time.” It is: **“Put the right piece of town at the right local time, then carry the consequence forward.”**

The satisfying beat is a causal chain: an 08:00 zone rises bread, then moves away to open a bridge; the bread remains risen because that milestone already happened, while another zone gives the station 08:05 and a train departs.

## 3. Core differentiator and causality contract
The game combines two state classes:

1. **Current local-time predicates** — true only while a site/object is currently covered by a clock-zone showing the required time. Example: bridge OPEN while under 08:00.
2. **Persistent process milestones** — once a valid transition completes at a Resolve boundary, it never reverses merely because the clock-zone moves away. Example: dough RAW -> RISEN after valid 08:00 exposure.

This distinction is the product's core reasoning language.

Locked causality principles:
- no global rewind;
- no retrocausality;
- moving a clock never rolls an object's completed state backward;
- no object secretly accumulates elapsed time unless a later mechanical spec explicitly defines a public discrete counter;
- all state changes occur at deterministic Resolve boundaries;
- all rules that can affect a result are public and inspectable;
- identical state + clock placement + action produces identical result.

## 4. Core loop
1. **Brief:** inspect exact goal, move budget and relevant rule cards.
2. **Inspect:** view sites, current process states, clock-zone times/footprints and legal sockets.
3. **Plan:** move/reposition allowed clock-zones among discrete legal placements.
4. **Resolve:** one deterministic beat evaluates current coverage and applies legal process transitions in canonical order.
5. **Observe:** animation shows current predicates and newly earned persistent milestones; concise reason traces explain changes/failures.
6. **Repeat:** use consequences of prior beats to set up later conditions/handoffs.
7. **Complete:** success when all final predicates/milestones/constraints hold at a valid boundary.
8. **Restart/checkpoint:** cheap recovery; no execution punishment.

No real-time reaction is required for campaign completion.

## 5. Core player verbs
Canonical high-level verbs:
- inspect a site/object and its public rule/state;
- inspect a clock-zone's displayed time and footprint;
- preview which sites a legal placement covers;
- move a clock-zone to a legal socket/placement;
- confirm configuration;
- Resolve the next beat;
- inspect exact state-change reasons;
- replay the last Resolve animation without changing logic;
- restart case / reload checkpoint.

Phase 4 must define exact low-level legality, overlap rules, evaluation order and move accounting.

## 6. Session and case targets
Typical play session: 15–45 minutes.

Case targets:
- onboarding: 2–5 min;
- normal: 5–12 min;
- late synthesis: 10–20 min;
- mastery may run longer because of planning depth, not waiting or real-time execution.

Target content remains **36 campaign + 12 optional mastery cases**, subject to later anti-repetition/playtest gates.

First-completion target is provisionally 6–8 hours; Phase 7 must re-research and lock commercial sizing.

## 7. Clock and town scope ceiling
Normal campaign baseline:
- 1–3 movable clock-zones;
- each clock displays one authored discrete time label at a case state; baseline labels use five-minute-style readable values such as 07:55 / 08:00 / 08:05, but they are semantic states, not continuous simulation;
- 2–8 logically relevant sites/objects;
- discrete legal clock placements/sockets;
- overlapping footprints allowed when explicitly visible;
- roughly 8–10 reusable process rule families across the whole base game;
- 1–5 Resolve beats normal; late mastery may exceed only if Phase 4 proves readability;
- no free physics placement;
- no open-world town;
- no continuous day/night simulation;
- no NPC schedules requiring hidden AI.

## 8. Process vocabulary thesis
Content should reuse a small set of visible process families rather than invent bespoke time magic per level.

Provisional semantic families for Phase 4 to formalize:
- **CURRENT OPEN/CLOSED** at a required local time;
- **ONE-SHOT ADVANCE** such as RAW -> RISEN;
- **ORDERED CHAIN** such as RAW -> RISEN -> BAKED;
- **PERMANENT HAZARD/LOCKOUT** such as flowers WILT/CLOSE if exposed too early;
- **CURRENT GATE + PERSISTENT CARGO** handoff;
- **ACCEPT/DISPATCH** when a persistent item arrives under a required current time;
- **CARRIER/HANDOFF** moving an already-earned milestone between sites after Resolve;
- **COUPLED TRIGGER** requiring two public current conditions simultaneously.

These are semantic families, not permission for hidden exceptions. Phase 4 must reduce them to a small exact state-transition grammar.

## 9. Progression thesis
Campaign progression expands causal composition, not time vocabulary.

Chapter direction:
1. current predicate vs persistent milestone;
2. two different local times and harmful exposure;
3. overlapping clock footprints and simultaneous predicates;
4. process handoffs / persistent cargo;
5. multiple zones with constrained move order and coupled conditions;
6. synthesis using the same bounded rule families.

Difficulty must not rise by adding dozens of timestamps, tiny timing arithmetic or exception-heavy buildings.

## 10. Demo promise
Target demo: 25–35 minutes, six cases LT01–LT06 from Round C.

It must prove in order:
1. clock-zone placement changes a current condition;
2. a completed process milestone persists after the clock leaves;
3. neighboring sites can experience different times simultaneously;
4. persistent output can be handed to a later time condition;
5. an obvious useful exposure can create an irreversible bad consequence;
6. multiple clock-zones compose into one readable town-wide causal solution.

Demo succeeds only if a new player can explain approximately:
> “You move local-time zones around. Things react to the time covering them, but completed steps stay completed.”

If players primarily describe it as a time-rewind/time-loop game, presentation/onboarding has failed.

## 11. Fairness and information contract
Every puzzle is deterministic and fully reasoned from public state.

Locked principles:
- all legal clock placements are visible;
- footprint is visible before commitment;
- each site/object exposes the rule relevant to its current state;
- Resolve cannot trigger a hidden schedule or random outcome;
- failures identify the exact public rule/transition responsible;
- the game never requires guessing an unknown rule;
- newly introduced rule families receive a safe teaching case before synthesis;
- multiple solutions are accepted whenever they satisfy exact predicates;
- no authored “intended action sequence” is runtime truth.

## 12. Preview / anti-oracle thesis
The player may preview:
- legal clock position;
- exact footprint/covered sites;
- currently visible rule cards that are relevant to covered sites;
- which current predicates would be true under that placement before Resolve.

The baseline preview must **not** automatically simulate an entire future multi-beat solution, rank placements, or reveal future consequences through several unresolved transitions.

Immediate one-beat consequence preview remains an empirical UX question for Phase 6. It may be allowed if needed for readability, but it cannot become a solver oracle.

## 13. Failure / dead-state thesis
Failure should be causal and cheap.

Categories:
1. **Hard invalid state:** a required object/site becomes permanently impossible under public rules.
2. **Move-budget failure:** remaining legal moves/beats cannot satisfy the objective.
3. **Final predicate failure:** player commits/completes while required current conditions or milestones are false.
4. **Certified dead state:** only if a future solver can prove no legal continuation succeeds.

No heuristic “you seem stuck” detector may claim impossibility.

Restart is instant. Phase 4/6 define checkpoints and undo boundaries.

## 14. Presentation thesis
The screen should read as a charming miniature town, not a timeline editor.

Primary visual language:
- buildings/sites are strong landmarks;
- clock-zones are translucent physical discs/patches with large readable clock faces/labels;
- footprint edges and overlaps are unmistakable without relying on color;
- current-time-dependent state uses active visual feedback (bridge open, station clock lit);
- persistent milestones use durable object/state changes (risen loaf shape, baked parcel, germinated tray);
- Resolve animations follow already-computed logic and never determine outcome;
- reason trace is short causal prose/icons, e.g. `08:00 covers Bakery -> RAW dough advances to RISEN`.

No visual language should imply that moving a zone backward in clock label rewinds history.

## 15. Controller / Steam Deck thesis
Fully playable without pointer precision.

Baseline:
- focus cycles among clock-zones, legal sockets/sites and objective panel;
- selecting a clock enters placement mode and highlights legal sockets;
- left/right or directional navigation selects socket; confirm places; cancel restores planning state;
- Resolve is a dedicated action;
- site details expose current state + relevant rule in one compact panel;
- camera is fixed/lightly panning/zooming, no free 3D navigation required;
- core puzzle state remains readable at 1280x800 without opening multiple nested panels.

## 16. Commercial thesis — provisional
Premium single-player puzzle game, PC/Steam first.

No ads, microtransactions, consumable hints, daily energy, live-service dependency or procedural grind.

A free demo is part of the product plan because the core distinction is easier to understand through the six-case causal sequence than through the phrase “time manipulation.”

Price and final campaign length are Phase-7 decisions after fresh market research.

## 17. Explicit scope exclusions
Out of scope unless a later contradiction repair formally reopens design:
- time travel;
- rewind/fast-forward of completed object history;
- past-self clones/echoes;
- continuous timers;
- real-time dexterity;
- global day/night simulation;
- free clock dragging over arbitrary geometry as logical state;
- physics-based zone collisions;
- hidden NPC schedules;
- dialogue-heavy narrative campaign;
- economy/tycoon layer;
- factory throughput optimization;
- procedural infinite town as core content;
- dozens of process rule families;
- rule exceptions attached to individual decorative props;
- runner-up mechanics from ONE MORE CHAIR or AFTERIMAGE DELIVERY.

## 18. Empirical gates intentionally deferred
1. Can first-time players distinguish “current condition” from “persistent milestone” by LT02 without verbal over-explanation?
2. Does moving an earlier-looking time label over a completed object falsely communicate rewind?
3. Are overlapping zone footprints readable on Steam Deck at 1280x800?
4. Can 8–10 reusable process families sustain 6–8 hours without bespoke exceptions?
5. Does immediate consequence preview aid comprehension without reducing puzzles to scanning sockets?
6. Are socketed clock placements visually embodied enough to preserve the fantasy rather than look like abstract switches?

Repairs should first simplify visual language/content, not add time-travel complexity.

## 19. Product-thesis acceptance result
Locked:
- target player/platform/genre;
- one-sentence hook and core fantasy;
- exact no-retrocausality identity;
- current predicate vs persistent milestone state classes;
- case loop and player verbs;
- session/content targets;
- clock/town/process scope ceilings;
- progression and six-case demo promise;
- fairness/preview/failure contracts;
- presentation/controller thesis;
- premium commercial direction;
- explicit exclusions and empirical gates.

**PHASE 3 PRODUCT THESIS = LOCKED.**

# NEXT DESIGN STEP — PHASE 4 MECHANICAL ARCHITECTURE
Define exact executable rules: canonical CaseState/SiteState/ObjectState/ClockZone state; legal placement and footprint overlap; discrete time-label semantics; process-transition grammar; Resolve ordering; current predicates vs milestone transitions; hazards/lockouts; carrier/handoff ordering; simultaneous-condition evaluation; move/beat budgets; objectives/win/fail/dead-state certification; checkpoint/undo semantics; difficulty knobs and hard ceilings; state invariants; validator obligations; and exact mechanical simulations of LT01–LT06. Do not start production implementation.