# GAME #018 — PHASE 4 MECHANICAL ARCHITECTURE

Date: 2026-09-06
Game: **LOCAL TIME**
Status: PHASE 4 COMPLETE — CONTENT ARCHITECTURE NEXT
Production implementation: NO
Authority: product identity and exclusions remain locked by `GAME18_PRODUCT_THESIS.md`; this file is canonical for executable mechanical semantics.

## 1. Mechanical thesis
LOCAL TIME is a deterministic finite-state puzzle. A case alternates between a **planning configuration** and an atomic **Resolve**. Clock labels are semantic values, not elapsed time. Clock placement determines current local-time predicates. Resolve snapshots those predicates, applies public irreversible transitions once, then performs public handoffs. Moving a clock after Resolve can change current conditions but never reverses a completed milestone.

## 2. Canonical state
### CaseState
- `case_id`
- `beat_index`: completed Resolve count, integer >=0
- `placement_moves_used`: committed clock relocations since case start
- `placement_move_limit`: optional authored ceiling
- `resolve_limit`: authored maximum Resolve count
- `clocks[]`, `sites[]`, `objects[]`
- `object_location`: object -> site/carrier/removed
- `milestones`: monotonic set of earned milestone IDs
- `lockouts`: monotonic set of permanent bad-state IDs
- `carrier_state[]`: deterministic carrier positions/payloads
- `objective_state`: derived, never independently mutated
- `last_resolve_trace`: presentation record only

### SiteState
- `site_id`, landmark/type
- one or more authored `footprint_cells`
- `current_local_time`: derived from coverage, not persisted
- `process_state`: finite enum when the site owns a process
- `current_predicate_rules[]`
- `transition_rules[]`
- optional `carrier_endpoint`
- optional permanent `disabled/locked` flag only when a public rule can set it

### ObjectState
- `object_id`, type
- finite `process_state` (e.g. RAW/RISEN/BAKED)
- monotonic milestone flags where needed
- `location`
- optional `collected/consumed` terminal flag
No hidden age or elapsed-time field exists in baseline mechanics.

### ClockZone
- `clock_id`
- immutable authored `time_label` for baseline campaign cases
- immutable authored footprint shape
- `socket_id` current placement
- `movable` boolean
- legal socket set
Clocks never tick during a case unless a future frozen content rule explicitly introduces a public discrete label transition; base campaign does not require this.

## 3. Sockets, footprints and overlap
Logical placement is socketed. Each socket maps a clock footprint to an exact authored set of covered site footprint cells. The preview shows that set before commitment.

A clock placement is legal iff: clock permits the socket; no authored hard occupancy rule forbids it; and every footprint cell is in the case board. Clocks may geometrically overlap. A site may be covered by multiple clocks only if the case explicitly declares its `multi_cover_policy`.

Baseline policy is **UNAMBIGUOUS**: a logically relevant site may receive at most one time label. If two zones overlap visually but cover different site cells, both are valid. If two different labels would cover the same relevant site, the configuration is illegal unless that site uses a public `REQUIRES_SET` coupled predicate that explicitly consumes multiple labels. There is no priority-by-layer, latest-placement-wins or hidden tie-break.

Decorative geometry has no logical collision semantics.

## 4. Discrete local-time semantics
A label such as `08:05` is an enum-like authored symbol with familiar clock presentation. It does not imply five minutes of simulation after `08:00`. Ordering comparisons such as before/after are forbidden unless a specific public rule declares an ordered label set; baseline rules use equality/membership only.

At any planning configuration, `LocalTime(site)` is derived from clock coverage or a fixed authored local-time field. If neither applies, value is `NONE`. Current predicates can inspect this value without mutating history.

## 5. Exact rule grammar
All campaign logic must compile to the following bounded families.

1. **CURRENT**: `LocalTime(S) in T -> Predicate P is true this configuration.` Example bridge OPEN.
2. **ADVANCE_ONCE**: at Resolve snapshot, `state=X AND current condition C -> state=Y`; X never returns because of clock movement.
3. **ORDERED_CHAIN**: repeated ADVANCE_ONCE rules over a finite acyclic chain, e.g. RAW->RISEN->BAKED. At most one transition per entity per Resolve.
4. **PERMANENT_LOCKOUT**: snapshot condition C sets monotonic lockout/terminal state, e.g. FLOWER_OPEN -> WILTED. Lockout transitions have explicit precedence over beneficial transitions on the same entity unless a case rule says the conditions are mutually exclusive.
5. **ACCEPT**: persistent object at endpoint + current predicate -> object/site receives persistent accepted milestone or object is consumed.
6. **DISPATCH**: current predicates plus required persistent prerequisites -> dispatch milestone; may enqueue a carrier movement.
7. **CARRIER_HANDOFF**: after transition evaluation, a carrier executes one public deterministic route step/handoff if its departure was enabled by the snapshot/transition result as declared by its rule.
8. **COUPLED_CURRENT**: a predicate is true only when a small explicit set of sites simultaneously satisfy public current conditions in the same pre-Resolve snapshot.

No arbitrary scripts, hidden timers, randomness, per-prop exceptions or retroactive edits are canonical.

## 6. Canonical Resolve order
Resolve is atomic logically; animation merely visualizes this sequence.

0. Validate placement configuration and remaining Resolve budget.
1. Derive coverage and `LocalTime` for every relevant site.
2. Freeze **Snapshot0** of all current predicates, object/site states, locations, milestones and lockouts.
3. Evaluate all permanent-lockout candidates from Snapshot0.
4. Evaluate all beneficial ADVANCE/CHAIN candidates from Snapshot0. An entity can earn at most one process-state transition this Resolve. A lockout candidate on that entity suppresses incompatible beneficial transition.
5. Evaluate ACCEPT/DISPATCH/coupled candidates from Snapshot0 plus already-existing persistent prerequisites only, unless the rule explicitly declares `same_resolve_prerequisite=true`. Default is false, preventing accidental multi-hop cascades.
6. Commit all non-carrier transitions simultaneously in deterministic entity-ID order only for trace stability; outcome cannot depend on ID order.
7. Execute each enabled carrier/handoff exactly one authored step, then commit resulting locations. Newly arrived cargo cannot be accepted until a later Resolve unless the endpoint rule explicitly declares `accept_on_arrival=true` and that behavior is taught/public.
8. Recompute current predicates from unchanged placement; evaluate objectives and certified terminal failure conditions.
9. Increment `beat_index`; store reason trace and post-Resolve checkpoint.

A Resolve with no logical change is legal unless the case explicitly budgets beats; it never secretly accumulates progress.

## 7. Action and budget accounting
Planning inspection/preview is free. Repositioning a movable clock from its current socket to another legal socket and committing the placement costs one **placement move**. Re-selecting/cancelling before commit costs zero. Moving several clocks requires one move each. Resolve costs one **beat** and does not itself cost a placement move.

Cases may constrain moves, beats, or both. Tutorial cases should avoid tight budgets until causality is learned. Runtime success is predicate-based, never dependent on matching an intended move count unless the objective explicitly includes a budget.

## 8. Objectives, success and failure
Objectives are Boolean expressions over public current predicates, persistent milestones, terminal object states, locations, lockout absence/presence and budgets.

Success is checked after Resolve and, for purely current final arrangements, may also be checked after a committed placement only when the case marks `placement_completion_allowed=true`. Default: after Resolve.

Immediate hard failure occurs only for an authored monotonic fatal lockout or exhausted hard budget with unmet objective. Otherwise the UI may label a state **DEAD** only when the exact case solver proves no legal continuation to success under remaining budgets. Heuristics may offer hints but may not claim impossibility.

## 9. Undo, restart, replay and checkpoints
- Every completed Resolve produces a canonical post-Resolve checkpoint.
- `Undo planning move` restores the previous uncommitted/committed planning configuration without touching completed history.
- `Undo Resolve` restores the exact pre-Resolve checkpoint including placements, move/beat counters, milestones, lockouts, carrier locations and trace. This is ordinary puzzle undo, never fictionally presented as time rewind.
- Replay replays `last_resolve_trace` presentation only and mutates nothing.
- Restart restores authored initial state.
- Save/load serializes canonical checkpoint state, not animation state.
- Undo stack is case-local and discarded when leaving unless implementation later elects to serialize it; correctness never depends on it.

## 10. Invariants
1. Same canonical state + same committed placement + Resolve => identical canonical next state.
2. Persistent milestones and lockouts are monotonic unless a rule explicitly models consumption as a separate terminal transition; clock movement never reverses them.
3. No entity advances more than one ordered-chain state per Resolve.
4. Current predicates derive solely from current public placement/fixed time and public state prerequisites.
5. Animation, frame rate and input timing cannot affect results.
6. No relevant site has ambiguous local time.
7. No hidden elapsed-time accumulation.
8. Carrier movement is finite and deterministic.
9. Objective truth is derived from canonical state.
10. Every state mutation emits a public reason-trace entry.

## 11. Difficulty knobs and ceilings
Normal campaign hard targets: <=3 movable clocks, <=8 logically relevant sites, <=10 universal semantic process families, <=5 Resolve beats for normal cases. Mastery may exceed five beats only after proof of readability; it must not exceed 8 relevant sites or 3 clocks without formally reopening scope.

Difficulty comes from: footprint overlap; harmful exposure; dependency order; simultaneous current predicates; persistent cargo handoff; move/beat scarcity; choosing which useful transition to defer; and composition of already taught families. It must not come from hidden information, many timestamps, continuous arithmetic, tiny visual differences or exception-heavy buildings.

## 12. Authored-case validator obligations
Before a case is shippable, tooling/authoring review must establish:
- initial state satisfies all schemas/invariants;
- all placements have unambiguous coverage;
- finite reachable state graph under declared budgets;
- at least one solution exists;
- exact shortest solution length(s) are known for QA, but never required as player truth;
- fatal/dead-state claims are solver-certified;
- no accidental same-Resolve cascade violates declared prerequisite policy;
- no solution depends on iteration order;
- after tutorial, case has a written **human causal proof**: a small set of necessities/constraints that eliminate substantial alternatives before enumeration;
- late cases are rejected if their main difficulty is simply trying every socket/order;
- alternate valid solutions are retained unless they break a stated objective.

Recommended authoring metadata: `introduced_family`, `required_insight`, `human_proof`, `solution_witnesses`, `dominant_strategy_attack`, `anti_enumeration_reason`, `accessibility_notes`.

## 13. LT01–LT06 exact simulations
### LT01 — Breakfast at Eight
Sites: Bakery, Bridge. One movable 08:00 zone; sockets cover either Bakery or Bridge, not both. Dough RAW. Bridge current OPEN iff Bridge=08:00. Goal: dough RISEN and bridge OPEN.

Beat 1: place 08:00 on Bakery, Resolve -> RAW->RISEN. Move zone to Bridge. Because final objective includes a current predicate, either Resolve Beat 2 or an explicitly authored placement-completion check may finish. Canonical demo uses Resolve Beat 2: no process transition; bridge current OPEN; RISEN persists; success. This deliberately proves that repeated Resolve alone does nothing.

### LT02 — Five Minutes Later, Somewhere Else
Fixed safe baseline 07:55; movable 08:05. Bread begins RISEN and advances to BAKED when Bakery=08:05. Flower OPEN permanently becomes CLOSED if Flower=08:05 before `PICKED`. Sockets are authored so Bakery-only exposure exists and a tempting Bakery+Flower footprint exists. Correct placement covers Bakery only; Resolve -> BAKED, flower remains OPEN. No chronological relation between 07:55 and 08:05 is simulated.

### LT03 — Shared Shadow
Two zones: 08:00 and 08:05. Bridge current OPEN iff 08:00; Station dispatch requires Station=08:05 AND Bridge OPEN in Snapshot0. Legal sockets allow simultaneous non-ambiguous coverage. Configure both, Resolve -> DISPATCH milestone. If 08:05 also covers protected Flower, lockout occurs and objective fails. This proves coupled simultaneous predicates.

### LT04 — Handoff
Bread RISEN at Bakery. 08:05 exposure -> BAKED on one Resolve. A public carrier endpoint can load BAKED parcel on a later Resolve under its declared load condition; carrier then moves one step after transitions. Destination ACCEPT requires parcel already present at Snapshot0 and Destination=08:10. Therefore arrival and acceptance are separate beats by default. This repairs the vague Round-C phrase “sequence three clock placements”: authored LT04 must budget enough Resolve beats for bake, handoff/arrival and accept, and must display those stages. No hidden transit time exists.

### LT05 — Bad Shortcut
Four sites, two zones, hard flower lockout. The tempting footprint simultaneously gives Bakery its useful required label and exposes unpicked Flower to its harmful label. Because lockout and beneficial transition are evaluated from the same snapshot, both occur; later clock movement cannot reopen the flower. The valid solution first earns the pickup/protection prerequisite, then uses the broad footprint. Exact sockets/content are Phase-5 authored data, but no rule exception is needed.

### LT06 — Little Town, Different Times
Two movable zones plus one fixed zone; Bakery chain, Bridge current predicate, Station dispatch, Greenhouse persistent milestone. Goal requires two persistent milestones and two simultaneous current predicates. At least one authored solution must use: (a) an earlier Resolve to earn a milestone, (b) relocation that removes its former local time without reversing it, and (c) a final configuration with distinct simultaneous labels. Validator must prove >=2 valid solutions if the demo copy promises multiple solutions; otherwise remove that promise.

## 14. Contradictions repaired from earlier phases
1. **LT04 carrier timing:** made explicit; newly created/arrived cargo does not silently chain through multiple stages in one Resolve.
2. **Clock overlap:** overlap is visually allowed but never creates ambiguous local time; coupled multi-label sites must opt in explicitly.
3. **Repeated Resolve:** cannot accumulate invisible duration; no-change Resolve is a true no-op except budget consumption.
4. **Current-only completion:** default remains Resolve-boundary success so the demo teaches one consistent rhythm; placement-only completion is explicit per case.
5. **Hazard precedence:** simultaneous harmful and beneficial exposure cannot exploit update order.

## 15. Anti-enumeration / human-proof gate
Public information remains complete; difficulty cannot be protected by hiding outcomes. From the first synthesis chapter onward, each case must include at least one authored causal necessity such as: “Flower must be protected before any broad 08:05 exposure,” “Dispatch requires bridge and station labels simultaneously,” or “Cargo must already be at destination before acceptance beat.” The validator compares reachable-state size and solution witnesses, while human review rejects cases whose practical method is scanning every legal socket sequence. Preview may show coverage and current predicates; it does not reveal multi-beat futures.

## 16. Phase acceptance
The universal model now specifies finite canonical state, placement/overlap semantics, discrete labels, bounded transition grammar, exact Resolve ordering, budgets, success/failure, solver-certified dead states, undo/checkpoint semantics, invariants, validator obligations and executable interpretations of LT01–LT06 without rewind or continuous time.

**PHASE 4 MECHANICAL ARCHITECTURE = COMPLETE.**

# NEXT DESIGN STEP — PHASE 5 CONTENT ARCHITECTURE
Define the reusable process/content families and data fields; chapter dependency ladder; exact 36-campaign + 12-mastery target with minimum quality floor; authored-case templates; case-family matrix; reuse/variation rules; art/content kit boundaries; human-proof metadata; anti-repetition gates; representative early/mid/late case proofs; and rules for cutting content rather than adding exceptions. Preserve <=3 clocks, <=8 relevant sites and the mechanical grammar above. Do not start production implementation.