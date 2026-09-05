# GAME #017 — THE QUEUE KNOWS — PHASE 5 CONTENT ARCHITECTURE

Date: 2026-09-05
Status: PHASE 5 COMPLETE
Authority: below `START_HERE.md`, `STATUS.md`, `GAME_INDEX.md`, `GAME17_PRODUCT_THESIS.md`, and `GAME17_MECHANICS.md`
Production implementation: NO

## 0. Content mandate

This file turns the locked Phase-4 rules into a finite, authorable campaign. It does not add a sixth heuristic, continuous sliders, spontaneous queue switching, hidden cooldowns, score-grind, or runtime-only exceptions.

Target shipped content:
- **36 campaign cases** in 6 chapters of 6;
- **12 optional mastery cases**, 2 attached to each chapter;
- **48 total authored cases** at target;
- minimum acceptable launch content after empirical cuts: **30 campaign-equivalent cases**, provided every reasoning family and the full six-case demo remain represented.

The base game stays within the mechanical ceilings already frozen: 10 visible customers, 3 counters, 5 heuristic families, max 4 interventions, max 4 cohorts.

---

## 1. Campaign chapter architecture

### Chapter 1 — READ THE LINE (QK01–QK06)
Purpose: prove that a queue is evidence, not merely congestion.

Primary content:
- Price vs Routine clean splits;
- identical passive behavior that diverges under one diagnostic intervention;
- immutable pre-choice snapshots;
- first congestion confound;
- first two-cohort observation;
- first pooling objective.

Required concepts by end:
1. customers choose deterministically;
2. the same visible choice can support different types in different pre-choice states;
3. player changes the hall to create information;
4. evidence only eliminates candidates when the evaluator contradicts the observation.

Chapter gate: clear QK01–QK06. These six are the canonical demo.

### Chapter 2 — TEST, DON'T GUESS (QK07–QK12)
Purpose: make intervention selection itself the puzzle.

Primary content:
- choose among 2–3 possible diagnostic presets;
- Price/Urgent and Urgent/Routine separations;
- familiarity-threshold equality cases;
- Convenience introduced as a candidate competitor;
- first explicit intervention budget tradeoff;
- first case where a locally informative test creates worse congestion.

No new mechanics. Difficulty comes from selecting the state that partitions the surviving worlds best while preserving service constraints.

### Chapter 3 — THE CROWD IS PART OF THE TEST (QK13–QK18)
Purpose: treat sequential congestion as a causal instrument.

Primary content:
- arrival order matters;
- early customers alter predicted completion for later customers;
- an intervention that diagnoses one cohort changes the test seen by the next;
- 2 cohorts become normal; 3 cohorts appear once;
- service-time/capacity preset becomes a diagnostic lever;
- first hybrid IDENTIFY + wait/service objective.

Mandatory anti-bookkeeping rule: every case must have at least one useful conclusion obtainable from a class-level comparison, not from simulating every hidden world one by one.

### Chapter 4 — ENOUGH TO ACT (QK19–QK24)
Purpose: teach that full identification is often unnecessary.

Primary content:
- EXCLUDE;
- SEPARATE;
- POOL_ALLOWED;
- Privacy becomes operationally central;
- “all remaining worlds” operational guarantees;
- global cardinality constraint appears, max one in early chapter and max two only at chapter capstone.

This chapter must include at least two solutions where some non-target customers remain intentionally ambiguous at success.

### Chapter 5 — DESIGN THE HALL (QK25–QK30)
Purpose: combine diagnosis and mechanism design under tight budgets.

Primary content:
- 3 counters standard in several cases;
- 2–3 intervention budgets;
- 2–3 cohorts;
- multiple levers can be legal, but only some preserve future information;
- deliberate use of an apparently unattractive counter to create a separating state;
- two hidden-world branches may require different second interventions after cohort-1 evidence.

At least half the chapter must admit multiple valid policies, not one designer-scripted action sequence.

### Chapter 6 — THE QUEUE KNOWS (QK31–QK36)
Purpose: capstone synthesis without adding rules.

Primary content:
- 7–10 relevant customers;
- all five heuristics may appear in initial candidate sets, but individual customers normally start with 2–4 candidates;
- 3 counters;
- up to 4 cohorts only in the final two cases;
- max 4 interventions only in final two cases;
- hybrid diagnosis + service constraints;
- no hidden information that cannot be represented by the locked world schema.

QK36 must require contingent policy: player cannot precommit the entire solution before seeing cohort evidence.

---

## 2. Mastery architecture — MQK01–MQK12

Two optional mastery cases unlock after each chapter.

Mastery cases may:
- use the upper end of customer/intervention/cohort ceilings;
- demand shorter intervention budgets than the campaign analogue;
- require partial-world guarantees rather than singleton identification;
- combine two public cardinality constraints;
- accept multiple certified policies.

Mastery cases may **not**:
- add a sixth heuristic;
- introduce new queue movement behavior;
- require arithmetic precision beyond the public integer scales;
- hide a rule;
- depend on animation timing;
- punish hint use through content lockout.

Suggested distribution:
- MQK01–02: pure separation efficiency;
- MQK03–04: threshold/equality reasoning;
- MQK05–06: congestion as instrument;
- MQK07–08: pooling and world-quantified service guarantees;
- MQK09–10: contingent two-stage policies;
- MQK11–12: full synthesis.

---

## 3. Reasoning-family quota

Every shipped 36-case campaign must contain at least:
1. **Direct behavioral split** — 5 cases.
2. **Counterfactual diagnostic state selection** — 6 cases.
3. **Congestion-mediated evidence** — 6 cases.
4. **Threshold/equality reasoning** — 4 cases.
5. **Pooling / partial identification** — 4 cases.
6. **Operational guarantee across remaining worlds** — 4 cases.
7. **Contingent multi-cohort policy** — 4 cases.
8. **Cardinality-assisted deduction** — 3 cases.

Cases can count toward at most two quota families. This prevents one motif from satisfying the whole content target on paper.

---

## 4. Canonical authored-case schema

Each case record contains:

```
case_id
chapter
display_name_key
brief_key
tutorial_flags[]
demo_included
mastery
initial_tick

counters[]:
  counter_id
  stable_order
  open
  fee
  service_time
  capacity
  privacy_level
  walking_cost_by_customer_or_group
  familiar_for_customer_ids[]
  feasibility_tags[]
  mutable_levers[]
  reset_each_cohort_flags[]

customers[]:
  customer_id
  arrival_cohort
  arrival_order
  initial_candidate_types[]
  authored_actual_type
  routine_threshold_if_applicable
  public_tags[]
  feasibility_tags[]

cohorts[]:
  cohort_id
  arrival_customer_ids[]
  post_cohort_service_ticks
  intervention_window_after

intervention_catalog[]:
  intervention_id
  lever_family
  target_scope
  allowed_values_or_named_presets[]
  intervention_cost
  timing_windows[]

starting_intervention_budget
max_intervention_budget
public_world_constraints[]
objective_predicates[]
hard_constraints[]
commit_required
world_quantifier
checkpoint_policy_id
hint_route_ids[]
validation_expectations
```

No content file may store an authored “correct action” as runtime truth. Intended routes are validation/proof metadata only.

---

## 5. Hidden-world construction rules

### 5.1 Default
Campaign cases use one authored actual world at runtime, while the validator reasons over the full public allowed-world set.

### 5.2 Initial candidate cardinality
- chapter 1: normally 2 candidates/customer;
- chapters 2–3: 2–3;
- chapters 4–6: 2–4 normal;
- 5 candidates only for rare mastery use.

### 5.3 World-space ceiling
Raw Cartesian world count before public constraints:
- campaign target: <= 4,096;
- late campaign exceptional ceiling: <= 16,384;
- mastery hard ceiling: <= 32,768.

If a case exceeds the ceiling, reduce candidate breadth or add a **public, meaningful** composition constraint. Never add a fake cardinality rule solely to make tooling faster.

### 5.4 Cardinality constraints
Examples:
- exactly one Urgent among C1,C2,C3;
- at most two Privacy among a named group.

Max 2 per case. They must be readable in one sentence and logically relevant to the puzzle.

### 5.5 Observational-equivalence rule
If two worlds remain observationally equivalent under all legal future actions:
- reject the case if objective requires distinguishing them;
- accept only if objective explicitly permits pooling and both worlds satisfy the same required final answer.

---

## 6. Reusable population-composition templates

Templates are starting points for authors, not procedural runtime generation.

- **PAIR SPLIT**: 3–4 customers, each {Price,Routine} or {Urgent,Routine}; one intervention.
- **TRIAD TEST**: 4–5 customers, 3 heuristic families distributed in overlapping pairs.
- **CONGESTION LADDER**: 5–7 customers in fixed arrival order where early type changes late predicted completion.
- **PRIVACY POOL**: 4–6 customers; Privacy mixed with one competitor; operational isolation target.
- **TWO-STAGE BRANCH**: cohort 1 reveals which of two cohort-2 interventions is safe.
- **THREE-COUNTER COMPASS**: 6–8 customers; each heuristic has a distinct attractive dimension but no counter is universally dominant.
- **COMPOSITION PUZZLE**: small candidate sets plus one public exactly/at-most constraint.
- **CAPSTONE MIX**: 8–10 customers, 3 counters, 2–4 cohorts, but candidate breadth kept narrow enough for human reasoning.

A template must be materially transformed before shipping: different behavioral conflict, intervention choice, objective, and proof route.

---

## 7. Reusable intervention templates

All use locked Phase-4 levers.

1. **PRICE GAP** — one counter fee changes by a named discrete step.
2. **OPEN/CLOSE** — availability chosen before cohort.
3. **SERVICE PRESET** — e.g. 1 slot @1 tick vs 2 slots @2 ticks.
4. **PRIVACY SIGN** — public privacy/exposure property toggled between authored levels/presets.
5. **DIAGNOSTIC PAIR** — two legal one-change options that split different type pairs.
6. **CONGESTION SACRIFICE** — a test gains information but worsens queue state.
7. **RECOVERY PRESET** — second-window action that depends on observed cohort-1 evidence.

No intervention template may secretly change the evaluator formula itself.

---

## 8. Authored versus parameterized content

### Authored
- case topology and counter count;
- customer identities and arrival/cohort order;
- candidate sets;
- actual hidden world;
- public cardinality constraints;
- allowed intervention families/presets;
- objectives/hard constraints;
- tutorial messaging;
- hint proof route;
- chapter/mastery placement.

### Safely parameterized
- display names/skins;
- non-logical room art;
- voice/text flavor;
- exact integer values within certified preset ranges;
- which equivalent authored world is used in a replayable mastery variant, only if every allowed world is already certified.

### Not procedurally generated for base campaign
- candidate-set structures;
- hidden-world constraints;
- objective combinations;
- intervention availability;
- proof obligations.

The base game is authored deduction content, validated exhaustively. Procedural generation is not required for commercial scope.

---

## 9. Validator-driven authoring workflow

For every new case:

1. schema/invariant validation;
2. enumerate allowed hidden worlds;
3. enumerate legal interventions and reachable public states;
4. verify evaluator totality;
5. compute observation partitions;
6. search contingent policies through all allowed worlds;
7. verify objective/hard constraints for every required world;
8. detect information dead states;
9. emit shortest successful depth and representative policies;
10. emit candidate-separation matrix;
11. emit indistinguishable world pairs;
12. compare intended human proof route against actual mechanical facts;
13. run anti-triviality and anti-bruteforce checks;
14. only then mark `CONTENT_CERTIFIED`.

Reject a case if:
- luck can satisfy an all-world objective;
- the solver finds a zero-information dominant route;
- intended deduction depends on a fact not exposed publicly;
- the case has only bookkeeping growth over an earlier case;
- raw search is easier to explain than the intended reasoning;
- a hard constraint can fail for reasons the UI cannot attribute;
- the human proof uses actual hidden type before it is deduced;
- world count breaches ceiling without design justification.

---

## 10. Final six-case demo instantiation

The demo contains QK01–QK06 and must end after a genuine synthesis, not a teaser-only tutorial.

### QK01 — SELF-SELECTION
Counters:
- A: fee1, service1, privacy0, walk0;
- B: fee1 initially, service1, privacy0, walk0.
Customers:
- C1 {Price,Routine}, actual Price;
- C2 {Price,Routine}, actual Routine, familiar A, threshold2;
- C3 {Price,Routine}, actual Price.
One free pre-cohort PRICE GAP preset: B fee0.
Objective: IDENTIFY all 3.
Validator expectation: B/A/B observations make all candidate sets singleton. No alternative intervention needed.

### QK02 — IDENTICAL UNTIL TESTED
Counters A/B initially identical service1.
C1 {Urgent,Routine}, actual Routine, familiar A, threshold2.
One free SERVICE PRESET: A service3, B service1.
Objective: IDENTIFY C1.
Expected split:
- Urgent -> B;
- Routine -> A because disadvantage=2 is within threshold.
Validator must verify passive equal state is non-diagnostic and preset creates exact partition.

### QK03 — EXPERIMENT CHANGES MEASUREMENT
A fee0 after free preset; B fee1; both service1.
C1 Price, C2 Price, C3 Urgent, C4 Routine(familiar B, threshold1), C5 Urgent.
Public candidate sets are authored overlapping pairs that include each actual type and at least one confound.
Objective: identify C1,C3,C5, with no requirement to singleton every customer.
Hard constraint: none beyond feasibility.
Validator expectation: later C5 choosing A must remain consistent with Urgent because its immutable snapshot contains tied predicted completion.

### QK04 — SEQUENTIAL COHORT
Two cohorts of 2.
After cohort1, exactly one intervention remains: B may be set FREE or left equal.
Objective: EXCLUDE Price or Urgent from named late customers according to the authored world.
Case authoring requirement: validator must prove the correct second-stage choice depends on cohort1 evidence; a single blind fixed policy cannot satisfy all allowed worlds.

Final values for QK04 are certified during implementation-data entry from this contract; content is invalid if the branch-dependence proof fails.

### QK05 — POOLING IS ENOUGH
Counters A/B privacy0; C privacy2, slightly worse walk/fee.
4–5 customers; target candidates include {Privacy,Price}; others use {Urgent,Routine}.
Objective:
- every Privacy customer queues at C;
- no non-Privacy customer queues at C;
- non-target singleton identification not required.
World quantifier: ALL REMAINING WORLDS.
Validator expectation: at success, target routing is guaranteed while at least one non-target candidate set remains size>1.

### QK06 — CONSTRAINED DIAGNOSTIC SERVICE
8 customers; 3 counters A/B/C; 2 cohorts of 4; 2 intervention budget; wait ceiling <=4 ticks.
A service1, B service1, C service2 initially.
Allowed intervention families: one Price/Privacy sign adjustment before cohort1; one service/capacity or sign preset after cohort1.
Objective: HYBRID — required target separation/identification plus wait constraint.
World quantifier: ALL ALLOWED WORLDS.
Validator expectation:
- at least one contingent policy succeeds for every allowed world;
- at least two distinct cohort1 observation partitions lead to different optimal/safe second interventions;
- no customer's wait exceeds4;
- no blind two-intervention script succeeds across all worlds.

QK04 and QK06 intentionally defer exact final customer/type tables to certified data authoring; their **logical obligations are final**. Data that fails them is rejected rather than changing mechanics.

---

## 11. Pacing and unlocks

Campaign chapters unlock linearly by default:
- Chapter N+1 unlocks after 4 of 6 cases in Chapter N;
- chapter capstone case #6 unlocks after 4 of first 5;
- final campaign completion requires all 36 campaign cases;
- mastery never gates campaign progress.

Why 4-of-6:
- one difficult case cannot hard-stop the player;
- optional skipping does not erase tutorial foundations because tutorial-critical cases are explicitly mandatory below.

Mandatory foundation cases:
- QK01, QK02, QK03, QK04, QK05, QK06;
- QK13 first congestion-instrument case;
- QK19 first all-world pooling/operational guarantee case;
- QK25 first contingent mechanism-design case.

A mandatory foundation case must be cleared before the chapter whose later content assumes it, even if the numeric 4-of-6 threshold has otherwise been met.

Mastery pair for Chapter N unlocks when its campaign capstone is cleared.

---

## 12. Anti-repetition checks

### Hour ~1
Player must have encountered at least:
- direct split;
- non-diagnostic passive state;
- congestion confound;
- pooling.
If the first hour reads as “change sign, see who moves” repeatedly, reorder/cut cases.

### Hour ~3
At least three different intervention families and four objective families must have appeared. No more than two adjacent cases may share both the same main candidate pair and same objective family.

### Hour ~5
At least one-third of recent cases must succeed without full identification. At least two cases must use contingent second-stage policies.

### Hour ~8 / completionist path
Mastery difficulty must come from tighter information/service tradeoffs, not larger numbers. Any case requiring exhaustive manual world listing by the player fails the human-solvability gate.

Portfolio-wide content freshness gates:
- no three consecutive cases share same counter count + cohort count + objective family;
- no reasoning family supplies >30% of campaign;
- no exact intervention-template sequence repeats more than twice;
- late cases must change **why** an intervention is useful, not merely increase customer count.

---

## 13. Human-solvability gate

For every QK13+ campaign case and every mastery case, author supplies a short proof route in plain language:
- 2–6 major deductions for campaign;
- 3–8 for mastery.

A proof step must eliminate a class of worlds/types or establish a service guarantee. “Enumerate all remaining worlds” is not a valid proof step.

Reject if:
- the shortest natural explanation is brute-force simulation;
- a player must track >3 simultaneous numeric comparisons per decision without a grouping shortcut;
- the intended proof relies on remembering an unstored prior queue state;
- the UI cannot expose every premise needed for the proof.

---

## 14. Content reuse and asset boundaries

Reusable visual assets:
- one service-hall environment family with chapter variants;
- 3 counter shells;
- sign/preset modules;
- customer silhouettes/portraits reused independently of logic;
- queue slot markers;
- evidence/type chips;
- small set of service animations.

Case identity must come from logical setup, not bespoke art.

No chapter may require:
- a new physical room simulation;
- a new customer AI model;
- bespoke cinematic logic;
- unique animation timing as a rule;
- more than five core type icons.

---

## 15. Expansion boundaries

Safe post-launch expansion:
- new authored cases using the same five evaluators;
- new public integer/preset combinations inside existing ceilings;
- new objectives assembled from existing predicate families;
- new mastery packs;
- cosmetic hall themes.

Requires explicit design reopening:
- sixth customer heuristic;
- spontaneous re-queueing;
- probabilistic behavior;
- freeform counter placement;
- real-time intervention;
- continuous pricing/service sliders;
- economics/tycoon layer;
- persistent metagame upgrades;
- online multiplayer.

A sixth heuristic is **not** normal DLC content. It changes the inference language and must be treated as a new-system design decision.

---

## 16. Phase-5 acceptance result

Phase 5 now defines:
- 36 campaign + 12 mastery target;
- six chapter purposes and progression;
- reasoning-family quotas;
- canonical case/customer/counter/cohort/objective/intervention schema;
- hidden-world construction and ceilings;
- population/intervention templates;
- authored vs parameterized boundaries;
- validator authoring pipeline and rejection gates;
- final logical contracts for demo QK01–QK06;
- unlock dependencies and mandatory foundations;
- hour 1/3/5/8 anti-repetition checks;
- human-solvability gates;
- content reuse/asset limits;
- explicit expansion boundaries.

**PHASE 5 CONTENT ARCHITECTURE = COMPLETE.**

No production implementation has begun.

# NEXT DESIGN STEP

Proceed to **Phase 6 — UX / Presentation Architecture**.

At minimum define:
1. controller/mouse/Steam Deck interaction model;
2. hall overview, counter inspector, customer/evidence inspector and intervention planning layout;
3. exact pre-choice/post-choice evidence presentation without hidden-truth leakage;
4. queue-state/predicted-completion readability without turning UI into an oracle;
5. cohort Resolve / Observe / Intervene pacing, skip/fast-forward/replay;
6. candidate-type chips and contradiction explanations;
7. tutorial flow across QK01–QK06;
8. commit/diagnosis/failure/restart/checkpoint UX;
9. accessibility: color-independent type/counter language, text scale, motion reduction, input remap;
10. 1280x800 handheld and controller-only acceptance;
11. hint UX that teaches a comparison/proof premise without naming the hidden type or action;
12. first-session and late 10-customer readability walkthroughs.
