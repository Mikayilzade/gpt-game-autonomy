# GAME #017 — PHASE 4 MECHANICAL ARCHITECTURE

Date: 2026-09-04
Selected concept: **THE QUEUE KNOWS**
Status: PHASE 4 COMPLETE
Authority: below `START_HERE.md`, `STATUS.md`, `GAME_INDEX.md`, `GAME17_RESEARCH.md`, `GAME17_TOURNAMENT.md`, `GAME17_ROUND_B.md`, `GAME17_ROUND_C.md`, `GAME17_PRODUCT_THESIS.md`.

This file turns the locked product thesis into deterministic executable rules. It does not contain production implementation code.

---

## 1. Mechanical design goals
The mechanic must satisfy all of these simultaneously:
1. customer choice is deterministic and explainable;
2. hidden type inference uses only visible candidate sets + observed actions;
3. player interventions alter both information value and later queue state;
4. queue motion never determines logic;
5. authored cases can be exhaustively validated over hidden worlds and legal actions;
6. multiple solutions are accepted when valid;
7. no campaign case requires statistical guessing, real-time reaction, pathfinding luck, or arbitrary NPC exceptions.

The canonical mental model is **intervene -> resolve -> observe -> infer -> repeat -> commit**.

---

# 2. Canonical state model

## 2.1 CaseState
A case state contains:
- `case_id`
- `tick` — integer >= 0
- `cohort_index` — current cohort to admit/resolve
- `phase` — `INSPECT | INTERVENE | RESOLVE | OBSERVE | COMMIT | TERMINAL`
- `interventions_remaining`
- `checkpoint_id`
- `counters[]`
- `customers[]`
- `cohorts[]`
- `evidence[]`
- `objective`
- `constraints[]`
- `hidden_world` — fixed actual type assignment, never shown before allowed reveal
- `candidate_worlds` — all hidden worlds still consistent with public evidence
- `history[]` — canonical logical events, independent of animation
- `terminal_result` — null or `SUCCESS | CONSTRAINT_FAIL | DIAGNOSIS_FAIL | INFORMATION_DEAD_STATE`

No other hidden mutable variable may affect customer decisions.

## 2.2 CounterState
Each counter has:
- `counter_id`
- `open` boolean
- `opens_at_tick` integer or null
- `fee` integer in authored bounded range 0..3
- `service_category` from a case-declared finite set
- `privacy_level` integer 0..2
- `walk_cost` integer 0..3
- `service_time` integer ticks per customer, 1..4
- `capacity` integer simultaneous service slots, normally 1; max 2
- `familiarity_tag` optional public tag
- `queue_slots[]` ordered front -> back
- `in_service[]` entries `{customer_id, remaining_ticks}`

A counter never has free-form speed or continuous geometry.

## 2.3 Queue slots
A queue is a fixed ordered list of logical positions. Occupancy is discrete. Visual characters may animate between slots, but the logical occupancy transition happens atomically at resolution boundaries.

Queue length means:
`waiting_count + in_service_count` only when a heuristic explicitly uses total completion prediction. UI may separately show waiting vs in-service.

## 2.4 CustomerState
Each customer has:
- `customer_id`
- `arrival_cohort`
- `candidate_types` — visible non-empty subset of the five canonical heuristics
- `actual_type` — one member of `candidate_types`, hidden until reveal policy allows
- `required_category` — public if case says service need is known; otherwise inferred through type/goal schema
- `familiar_counter_id` — public when Routine is a candidate
- `privacy_sensitive_category` — public marked category when Privacy is a candidate
- `candidate_set_current` — starts equal to `candidate_types`, then only shrinks through exact inconsistency
- `choice_history[]`
- `status` — `NOT_ARRIVED | WAITING | IN_SERVICE | COMPLETED | EXITED`
- `chosen_counter_id` current/last
- `arrival_order` — total order within cohort

Customers never have patience, mood, hidden speed, random noise, or changing preferences.

## 2.5 Cohort
A cohort is an authored ordered list of customer IDs admitted together at one intervention boundary. A cohort defines:
- `cohort_id`
- `customer_ids` in deterministic arrival order
- `admit_tick`
- optional `post_cohort_service_ticks` — number of service ticks that advance after all cohort choices resolve before returning control

Normal cases use 1–3 cohorts; hard ceiling 4.

## 2.6 Evidence record
Each observed choice creates one immutable evidence record:
- `event_id`
- `tick`
- `customer_id`
- `pre_choice_public_state_hash`
- `available_counters`
- `chosen_counter_id`
- `observed_choice_features` — concise public facts, not hidden type
- `candidate_eliminations[]` — `{type, contradiction_reason}`

Evidence is never deleted by later state changes. Later congestion cannot retroactively reinterpret an earlier choice because the exact pre-choice public state is retained.

---

# 3. Canonical predicted completion

For a customer evaluating counter `c` immediately before their choice:

`predicted_completion(c) = availability_delay(c) + queued_work(c) + own_service_time(c)`

Where:
- `availability_delay(c) = max(0, opens_at_tick - current_tick)` if closed but scheduled to open and the case permits joining-before-open; otherwise the counter is infeasible while closed.
- Default campaign rule: **customers may not join a closed counter**. Therefore normal `availability_delay = 0` for feasible counters.
- `queued_work(c)` is computed from current `in_service` remaining work plus waiting customers ahead under capacity.
- With capacity 1: `queued_work = sum(remaining service of in-service customers) + sum(service_time for waiting customers in slot order)`.
- With capacity 2: compute the deterministic two-lane finish schedule by assigning each queued service job in slot order to the earliest-free service slot, tie -> lower slot index. The candidate customer's own job is appended last and predicted completion is its finish time relative to current tick.
- `own_service_time(c)` is the public service-time preset applicable to this customer at counter c. Unless a case explicitly declares category-dependent service time, it equals counter `service_time`.

No heuristic may estimate completion by visual distance or animation duration.

---

# 4. Five canonical customer evaluators

All evaluators operate only on counters that are **feasible** for the customer's required service category and currently open. If exactly one feasible counter exists, every type chooses it. If none exists, the choice event is `NO_FEASIBLE_COUNTER`; authored campaign cases must either make that an explicit allowed outcome or validator rejects the state.

## 4.1 Global final tie-break order
Whenever a type-specific comparator remains tied after all of its semantic keys:
1. lower `predicted_completion`;
2. lower `fee`;
3. lower `walk_cost`;
4. lower stable `counter_id` lexical/order index.

Type-specific keys listed below come before this global fallback. This total order guarantees one choice.

## 4.2 PRICE
Semantic rule: choose the lowest visible fee.
Comparator keys:
1. `fee` ascending;
2. `predicted_completion` ascending;
3. global remaining fallback.

Canonical short reason: `lowest fee -> [counter]`; if tied: `same fee -> sooner completion -> [counter]`.

## 4.3 URGENT
Semantic rule: choose shortest predicted completion, ignoring fee as a preference.
Comparator keys:
1. `predicted_completion` ascending;
2. `walk_cost` ascending;
3. stable `counter_id`.

Fee is not consulted before stable final order. Reason: `soonest completion -> [counter]`.

## 4.4 ROUTINE
Each Routine-candidate customer has public `familiar_counter_id` and authored visible threshold `routine_threshold` in ticks, integer 1..4. Threshold is attached to the case/customer card and is not hidden.

Let `F` be familiar feasible counter and `B` be best non-familiar counter under `predicted_completion` then global fallback.
- if F is infeasible, choose best feasible counter by predicted completion/global fallback;
- else compute `disadvantage = predicted_completion(F) - predicted_completion(B)`;
- if `disadvantage <= routine_threshold`, choose F;
- if `disadvantage > routine_threshold`, choose B.

This includes equality in “stay familiar.” Reason examples:
- `familiar A is only +2 ticks (threshold 2) -> A`
- `familiar A is +3 ticks (>2) -> B`.

## 4.5 PRIVACY
A Privacy-candidate customer has one public `privacy_sensitive_category` marker. Each counter exposes a public binary `public_exposure(customer,counter)` derived from `service_category` signage and `privacy_level`:
- exposure = 0 when counter privacy level >= case-declared required privacy for that category;
- exposure = 1 otherwise.

Comparator keys:
1. `public_exposure` ascending;
2. `predicted_completion` ascending;
3. global remaining fallback.

Privacy never chooses an infeasible counter merely for privacy. Reason: `avoids public [category] exposure -> [counter]`.

## 4.6 CONVENIENCE
Comparator keys:
1. `walk_cost` ascending;
2. `predicted_completion` ascending;
3. `fee` ascending;
4. stable `counter_id`.

`walk_cost` is an authored discrete cost shown directly by hall layout/steps icon. No pathfinding calculates it. Reason: `fewest steps -> [counter]`.

---

# 5. Choice resolution and congestion

## 5.1 Single canonical resolution order
When player presses Resolve for a cohort:
1. freeze intervention controls;
2. apply any scheduled opening/lever state changes whose effective tick is current tick;
3. admit cohort customers in authored `arrival_order`;
4. for each arriving customer, one at a time:
   a. snapshot current public hall state;
   b. enumerate feasible counters;
   c. evaluate their **actual hidden type** with canonical evaluator;
   d. atomically append customer to chosen counter's back queue slot;
   e. write logical choice event and evidence snapshot;
   f. update queue occupancy immediately before next customer's evaluation;
5. after every customer in cohort has chosen, run candidate inference against all recorded choices from this cohort;
6. if `post_cohort_service_ticks > 0`, advance exactly that many service ticks using section 5.2;
7. evaluate service constraints and objective predicates that are defined at this boundary;
8. enter `OBSERVE` phase and return player control unless terminal.

Therefore later arrivals in the same cohort see congestion created by earlier arrivals. This is the canonical confound mechanism.

## 5.2 Service tick order
For each service tick:
1. increment global `tick` by 1;
2. decrement `remaining_ticks` for all in-service customers simultaneously;
3. complete all entries reaching 0, ordered by counter_id then service-slot index for event log only;
4. remove completed customers;
5. at each counter, fill empty service capacity from queue front, preserving queue order; starting service does not consume an extra tick on that same boundary — the new service gets full remaining service_time and first decrements on next tick;
6. apply any scheduled public counter-state transition effective at the new tick;
7. check hard service constraints that are defined continuously.

Customers do not voluntarily switch queues after choosing unless a future content family explicitly declares a public `RECHOICE_EVENT`. Phase 4 baseline has **no re-choice**. This keeps evidence causality bounded. Later content must not silently introduce switching.

## 5.3 Waiting time
For constraints, a customer's waiting time is `service_start_tick - arrival_tick`. Completion time is `completion_tick - arrival_tick`. A case must state which metric its ceiling uses. Product default phrasing `wait <= N ticks` refers to waiting time, not completion.

---

# 6. Fixed-slot movement semantics

Logical movement is atomic:
- on choice, customer occupancy changes from `NOT_ARRIVED` to exact queue slot immediately;
- on service promotion, occupancy changes from queue front to service slot immediately;
- on completion, status changes immediately.

Animation reads the event log and may interpolate characters afterward. Input may be temporarily presentation-locked during a short animation, but simulation state is already final. Skipping/fast-forwarding animation cannot alter outcomes.

The UI may show ghost arrows before resolution as hypothetical comparison aids only if they reveal no hidden truth; it may not preview actual hidden-type choice.

---

# 7. Intervention system

## 7.1 Canonical intervention actions
A case exposes a subset of four lever families:
1. **Fee/Sign** — set a counter fee to one of declared discrete values, commonly 0/1/2 or toggle `FREE` (fee 0 vs baseline).
2. **Opening** — choose whether a counter is open for the next cohort, or choose from authored discrete opening presets. Normal campaign customers cannot queue at closed counters.
3. **Service/Privacy flag** — choose one of declared service-category/privacy configurations for a counter.
4. **Capacity/Service-time preset** — choose among authored presets such as `1 slot @1 tick` vs `2 slots @2 ticks`; never continuous sliders.

## 7.2 Legality and timing
- interventions occur only in `INTERVENE` phase;
- each atomic lever change costs 1 intervention unless case says a named preset costs 0 as starting setup;
- changing the same lever twice before Resolve costs only for each committed change; player may freely preview values before confirming the intervention set;
- once Resolve begins, current cohort cannot be interrupted;
- after Observe, if another intervention window exists, unchanged lever values persist by default;
- a case may mark a lever `RESET_EACH_COHORT`; this is public in brief and validator schema;
- no hidden cooldowns.

## 7.3 Intervention budget
Normal campaign: 1–3 paid changes per case, hard ceiling 4. A “configuration” can consist of multiple lever changes if budget allows. Budget is part of the logical state and exhaustive solver.

---

# 8. Candidate inference

For every customer choice evidence record E:
1. for each type `t` in the customer's current candidate set, replay the canonical evaluator using E's exact pre-choice public state;
2. if evaluator(t) != observed chosen counter, eliminate t;
3. otherwise retain t;
4. append explicit contradiction reason for eliminated t, such as `Urgent would choose B because completion 2 < 4; observed A`.

Candidate sets only shrink. No Bayesian weights exist.

## 8.1 UI reveal boundary
Before final commit, UI may show:
- current candidate types;
- which types were eliminated by an observed choice;
- the public comparison that caused elimination;
- counter state snapshot used by that evidence.

It may **not** show:
- actual hidden type if more than one candidate remains;
- a reason sentence generated specifically from the actual hidden type unless the same sentence is valid for all surviving candidate types.

Therefore the generic observed trace should be phrased as facts + elimination, e.g. `A chosen while B was 2 ticks faster` and chips update. When only one candidate remains, UI can state `Type proven: Routine` because that is logically deduced, not leaked.

---

# 9. Hidden worlds

A hidden world is a full assignment of one actual type to every customer, each drawn from their initial candidate set, optionally constrained by public case rules such as `exactly one Urgent among C1,C2,C3`.

The validator enumerates every world satisfying these public constraints. At runtime one authored world may be fixed, or a case may select one world at start from a deterministic seed for replay variety, but **campaign solvability must hold across every allowed world** if the player is expected to succeed without knowing which world was selected.

Random selection is presentation/content variation only; inference remains exact. Default campaign is fixed authored world per case unless Phase 5 explicitly designates a replayable variant.

---

# 10. Objectives and success

A case objective is one or more exact predicates from these families:

1. **IDENTIFY** — specified customers must have singleton candidate sets and final submitted labels must match.
2. **EXCLUDE** — prove specified customer is not one or more listed types; candidate set must exclude them before commit.
3. **SEPARATE** — after a specified cohort, customers satisfying a hidden/public target predicate must be queued only at allowed counter(s), while prohibited types are absent there.
4. **POOL_ALLOWED** — identify/isolate target category while non-targets may remain unresolved.
5. **SERVICE** — satisfy a queue/service state, e.g. `medical-priority customers reach C`.
6. **HYBRID** — deduction predicate plus service constraints.

A case must state whether the final operational condition must hold in **all remaining candidate worlds** or only the actual world. Default is all remaining candidate worlds before commit; this prevents lucky routing based on unresolved hidden state.

## 10.1 Commit
Player explicitly presses Commit when objective requires diagnosis/claim. Commit is irreversible for that attempt.

On commit:
- validate submitted claim against actual hidden world;
- validate required proof predicate from evidence/candidate worlds;
- if correct, success;
- if incorrect, `DIAGNOSIS_FAIL`, reveal actual hidden world and shortest available contradiction explanation;
- player may restart/checkpoint afterward.

Operational-only cases may auto-succeed at a boundary if no diagnosis entry is needed, but at least one information objective is mandatory in every campaign case per product thesis.

---

# 11. Constraint failure

Hard constraints are exact predicates such as:
- max waiting time;
- no target type at forbidden counter;
- intervention budget;
- all customers eventually feasible for service;
- counter occupancy cap if explicitly authored.

A hard constraint failure triggers immediately at the specified evaluation boundary and records exact violating event. No score-based soft failure is required for campaign completion.

---

# 12. Exhaustive information dead-state certification

An information dead state exists only if, from current full public logical state:
- objective is not yet guaranteed/satisfied; and
- for **every** legal future player action sequence within remaining intervention/cohort budget, there exists at least one pair of remaining hidden worlds requiring different final answers but producing identical future observable evidence under that sequence, or the hard objective becomes impossible.

Validator/runtime solver may certify this by exhaustive search over:
`public state x remaining candidate worlds x legal intervention sequences x deterministic observations`.

The UI must never announce dead state from local heuristic or “no candidate changed recently.”

If the search proves impossibility, terminal result may be `INFORMATION_DEAD_STATE` with concise explanation such as `C2 remains {Urgent,Routine}; no remaining lever creates a state where their choices differ before commit.`

---

# 13. Reset, checkpoint, undo and replay

Mechanical policy:
- **Restart Case**: always available outside unskippable transition; restores case initial public/hidden state exactly.
- **Checkpoint**: canonical checkpoint exists at the start of each `INTERVENE` phase after prior cohort evidence has been accepted. Reloading it restores the exact same hidden world and evidence history.
- **Undo lever edits before Resolve**: free; because no information has been generated yet.
- **Undo after Resolve**: not allowed as a state rewind button. Use checkpoint reload instead.
- **Replay Observation**: allowed; replays animation/event visualization from stored logical event records and cannot alter state, RNG, candidate sets, budget or history.
- **Fast-forward**: presentation-only.

This prevents information gained from one future branch from coexisting canonically with a rewound state while still making experimentation cheap.

---

# 14. Difficulty knobs and hard ceilings

Canonical knobs:
- customers: 3–10 individually relevant; hard ceiling 10 visible simultaneously;
- counters: 2 normal, 3 late; hard ceiling 3;
- core heuristic families: exactly 5 for shipped base design;
- initial candidate types per customer: 2–4 normal, hard ceiling 5;
- interventions available: 1–3 normal, hard ceiling 4;
- cohorts: 1–3 normal, hard ceiling 4;
- service times: 1–4 ticks;
- Routine threshold: 1–4 ticks;
- privacy levels: 0–2;
- fee values: 0–3;
- walking costs: 0–3;
- simultaneous service capacity: 1 normal, 2 maximum;
- public global cardinality constraints: max 2 per case (example: exactly one Urgent among three customers), to avoid logic-grid overload.

Difficulty should rise primarily through:
- overlap of candidate behavior under current state;
- sequential congestion;
- limited lever budget;
- partial-identification objectives;
- interaction between operational constraint and information value.

It should not rise through tiny numeric differences, more than five heuristic families, huge crowds, or deep rule exceptions.

---

# 15. State invariants

Every legal state must satisfy:
1. each customer occupies at most one location/status;
2. queue slot order is total and duplicate-free;
3. every actual type is in initial candidate set;
4. current candidate set is non-empty and subset of initial set;
5. actual type is never eliminated by correctly computed evidence;
6. all evidence snapshots reference immutable prior public state;
7. intervention budget >=0;
8. only open/feasible counters receive choices unless case explicitly permits `NO_FEASIBLE_COUNTER`;
9. same state + same hidden world + same action yields same next state;
10. animation state is not an input to logical simulation;
11. every resolved customer choice has exactly one selected counter or explicit no-feasible outcome;
12. tick never decreases inside an attempt;
13. candidate-world set equals worlds consistent with all retained evidence/public cardinality constraints;
14. if success is declared, objective predicate and every hard constraint are true under required world quantifier;
15. if dead-state is declared, exhaustive search certificate exists.

---

# 16. Authored-case validator obligations

For every campaign/mastery case, tooling must be able to prove:
1. schema validity and all invariants;
2. at least one allowed hidden world;
3. all initial candidate sets reflect exactly the public allowed worlds;
4. every customer evaluator produces total deterministic choice for every reachable state;
5. no hidden variable outside schema influences choice;
6. at least one successful player strategy exists from start for every allowed hidden world under the case's information contract;
7. if the intended objective requires unique identification, success cannot be achieved without evidence sufficient to guarantee that identification;
8. all accepted multi-solution routes satisfy constraints; validator does not require designer-intended action sequence;
9. dead states discovered by exhaustive solver can be certified;
10. no required strategy exceeds intervention/cohort hard ceilings;
11. candidate elimination explanations are generated from the same comparator/evaluator;
12. hidden-world pairs that remain observationally equivalent at completion are permitted only when objective explicitly allows pooling.

Validator should emit diagnostics:
- reachable state count;
- successful strategy count or representative strategies;
- shortest successful depth;
- dead-state count;
- candidate-separation matrix per intervention;
- world pairs never distinguished;
- hard-constraint failure fronts.

---

# 17. Six canonical demo-case simulations

These are mechanical proofs of the Round-C demo claims, not final Phase-5 content prose.

## QK01 — SELF-SELECTION
Setup:
- counters A,B; both service_time 1, walk 0, fee baseline 1;
- A familiar for Routine candidates;
- three customers C1,C2,C3 candidate set `{PRICE, ROUTINE}`; authored hidden types P,R,P;
- player has one FREE sign intervention.

Player sets B fee 0, A fee 1.
Arrival order C1,C2,C3.
- C1 Price: B fee0 < A1 -> B.
- C2 Routine: familiar A. At choice predicted completion A=1, B has C1 waiting =>2. A is not disadvantaged -> A.
- C3 Price: B fee0 despite B predicted completion2 vs A2 -> B.
Evidence replay:
- C1 choice B eliminates Routine because Routine would choose A.
- C2 choice A eliminates Price because Price would choose B.
- C3 same as C1.
Result: exact clean split. PASS.

## QK02 — IDENTICAL UNTIL TESTED
Setup:
- C1 candidate `{URGENT, ROUTINE}`, familiar A threshold2;
- A and B initially both fee1/service1/walk0, empty. Stable tie makes both types choose A (Urgent stable tie -> A; Routine familiar -> A), so passive observation is non-diagnostic.
Intervention preset slows A service_time from1 to4 while B remains1.
At C1 choice: predicted A=4, B=1.
- Urgent -> B.
- Routine disadvantage A-B=3 > threshold2 -> B also: still non-diagnostic. This reveals a contradiction in the naive Round-C wording: merely slowing A too much does not separate these types.
Repair: use A predicted completion=3, B=1 and Routine threshold2. Equality rule says disadvantage2 <= threshold -> Routine stays A; Urgent -> B.
Canonical QK02 therefore uses A service_time3, B1.
Result: divergent exact test. PASS after repair.

## QK03 — EXPERIMENT CHANGES MEASUREMENT
Setup:
- A fee0, B fee1 after player FREE intervention on A;
- service_time both1; five customers in one cohort arrival order C1..C5;
- C1 Price, C2 Price, C3 Urgent, C4 Routine(familiar B, threshold1), C5 Urgent.
Choices resolve sequentially.
C1 Price -> A (A queue1).
C2 Price -> A (A predicted own finish2).
C3 Urgent sees A predicted3, B1 -> B.
C4 Routine familiar B: B currently contains C3 => predicted2; A predicted3; familiar B -> B.
C5 Urgent sees A predicted3, B predicted3; tie -> walk/stable; if equal walk and A stable -> A.
Observation: same FREE intervention that cleanly attracts Price customers also changes queue lengths enough that later Urgent C5 chooses A. A final location alone is not equivalent to Price. Evidence snapshots still distinguish: C5's surviving candidate set can retain Urgent because at its exact pre-choice state A/B were tied.
Result: congestion confound is real and exactly explainable. PASS.

## QK04 — SEQUENTIAL COHORT
Setup:
- two cohorts: early E1,E2 then late L1,L2;
- counters A,B, both fee1/service1;
- E1/E2 candidates allow player to infer whether early congestion will persist;
- one intervention available after cohort1: set B FREE or leave fees equal.
Mechanical proof sequence:
Cohort1 resolves, then one post-cohort service tick. Evidence is retained. Player enters checkpoint/intervention phase with exact current queues. If early cohort leaves A occupied for next tick, setting B FREE can separate Price from Routine among late customers; if B already carries residual work, the same sign may pool Urgent with Price. Because current state is fully observable and checkpointed, late action is conditioned on early observation without real-time control.
Result: sequential observe/control contract works. PASS.

## QK05 — POOLING IS ENOUGH
Setup:
- target objective: `ensure every PRIVACY customer is at C and no non-PRIVACY customer is at C`; identification of other types unnecessary.
- three counters A,B,C; C has privacy_level2 and fee1; A/B privacy0; all feasible.
- customers have candidate sets `{PRIVACY, PRICE}` or `{URGENT, ROUTINE}` etc.
Player configures C so it is the only non-exposing route for marked category but deliberately gives C higher walk cost. Privacy chooses C; Price/Convenience/Urgent need not be uniquely classified if their evaluators all choose A/B under current public state.
Validator success criterion quantifies over remaining worlds: every remaining world places Privacy at C and all non-Privacy away from C. Candidate singletons for non-target customers are not required.
Result: pooling objective is mechanically supported. PASS.

## QK06 — CONSTRAINED DIAGNOSTIC SERVICE
Setup:
- 8 customers, 3 counters A/B/C, candidate types drawn from Price/Urgent/Routine/Privacy;
- 2 intervention budget;
- wait constraint <=4 ticks;
- first cohort4, second cohort4;
- service_time A1,B1,C2 initially.
Strategy pattern validated conceptually:
1. intervention1 changes one fee/privacy flag before cohort1 to create a partial split;
2. cohort1 choices generate evidence and congestion;
3. one post-cohort service tick advances state;
4. intervention2 adjusts capacity/service preset or sign for cohort2 based on surviving worlds;
5. second cohort produces final separation while wait constraint checked continuously.
Required validator condition: authored numerical instance must be rejected unless exhaustive search proves at least one policy contingent on cohort1 observations succeeds for all allowed worlds and no customer's wait exceeds4.
The Phase-4 contract supports this directly; exact final authored QK06 numbers belong to Phase 5 because they require content balancing rather than new mechanics.
Result: architecture supports the synthesis case without rule exception. PASS.

---

# 18. Contradictions found and repaired in Phase 4

1. **Routine separation edge case.** Round-C language implied “make familiar counter sufficiently slower” would distinguish Routine vs Urgent. If slowed beyond Routine threshold, both switch. Canon now locks equality behavior and a bounded threshold so diagnostic states can be authored deliberately.
2. **Reason-trace leakage.** Showing `actual type -> reason` after every choice would leak truth. Canon now exposes public state + eliminations; actual-type-specific explanation appears only when logically deduced or post-commit.
3. **Queue switching ambiguity.** Round-C mentioned customers switching in descriptive market language. Baseline mechanic now forbids spontaneous re-choice; sequential congestion comes from later arrivals observing earlier queues. Any future re-choice would require explicit later design review, not accidental implementation.
4. **Opening delay ambiguity.** Normal customers cannot join closed counters. Opening is a pre-cohort availability lever, avoiding speculative waiting behavior.
5. **Wait vs completion ambiguity.** Wait ceilings use service-start minus arrival unless case explicitly states completion ceiling.
6. **Checkpoint/information contamination.** No post-observation undo that retains learned evidence. Checkpoint reload restores entire state/evidence branch.

---

# 19. Phase-4 acceptance result

Complete canonical answers now exist for:
- state model;
- five deterministic evaluator formulas;
- total tie-break order;
- predicted completion;
- cohort and service tick ordering;
- congestion causality;
- fixed-slot movement independent of animation;
- intervention actions, legality, persistence and budgets;
- exact candidate elimination and evidence retention;
- reveal boundaries that avoid hidden-truth leakage;
- objective families;
- commit, success and failure;
- exhaustive dead-state certification;
- restart/checkpoint/replay semantics;
- difficulty knobs and hard ceilings;
- state invariants;
- authored-case validator obligations;
- six demo-case mechanical simulations and contradiction repairs.

**PHASE 4 MECHANICAL ARCHITECTURE = COMPLETE.**

No production implementation has begun.

---

# NEXT DESIGN STEP
Proceed to **Phase 5 — Content Architecture**.

Phase 5 must define:
1. campaign chapter structure and exact case families built only from the locked mechanics;
2. target/minimum case counts and pacing across ~36 campaign + 12 mastery cases;
3. data schema for authored cases/customers/counters/objectives/constraints;
4. which content is authored versus safely parameterized/procedural;
5. reusable intervention templates and population-composition templates;
6. hidden-world construction rules and anti-combinatorial ceilings;
7. validator-driven content authoring workflow and rejection criteria;
8. tutorial/demo six-case content in final mechanical form;
9. anti-repetition rules for hours 1/3/5/8;
10. chapter unlock dependencies and optional mastery placement;
11. expansion boundaries, including explicit rule that a sixth core heuristic is not normal content expansion.

Fresh web research is not required merely to write Phase 5 unless external content/market expectations become material.