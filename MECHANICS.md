# ORGANISM CARGO — MECHANICAL ARCHITECTURE

Status: **CANONICAL PHASE 4 APPENDIX — FOUNDATION LOCKED**
Last updated: 2026-08-15

This file is canonical for Phase 4 mechanics and is subordinate only to the product thesis in `GAME_BIBLE.md`. It exists because the mechanical specification is large enough to deserve an implementation-oriented appendix. At specification freeze, contradictions must be reconciled and this file must remain readable as a standalone mechanical contract.

---

# 1. Mechanical objective

The central problem is not static packing. The player chooses **initial conditions** for a small deterministic ecology, commits, and then observes whether the system survives transit.

A valid contract must create at least one meaningful temporal consequence after launch. If a contract is normally solvable by checking only time-zero shape fit or time-zero adjacency, it is mechanically invalid for the core campaign except as the earliest tutorial.

The simulation must satisfy four properties simultaneously:

1. **Deterministic** — identical initial state + content version + route sequence produces identical results.
2. **Discrete** — gameplay authority uses grid cells, integer/fixed-point values, explicit ranges, and ordered events; animation never decides outcomes.
3. **Explainable** — every authoritative change has a causal event record.
4. **Composable** — organisms are data-defined combinations of reusable traits rather than bespoke scripts.

---

# 2. Hold topology

## 2.1 Grid

The authoritative hold is a 2D orthogonal grid. Typical launch holds are expected to range from roughly 5x5 to 9x7 usable cells, with blocked cells and fixtures creating shape variety.

A cell has:
- coordinate `(x,y)`;
- occupancy state;
- passable/blocked flag;
- optional fixture/support identifier;
- environmental channel values;
- optional zone tags;
- route-hazard modifiers affecting that cell.

Diagonal contact never counts as adjacency unless a trait explicitly says `diagonal`.

## 2.2 Occupancy

Every occupied cell belongs to exactly one organism or support module at authoritative resolution boundaries. Two solid entities may never share a cell.

Transient visual overlap during animation has no gameplay meaning.

## 2.3 Footprints

An organism has a footprint defined as a set of local integer cell offsets from an anchor cell. Rotation is allowed only when its body plan declares legal orientations.

Legal placement requires:
- all footprint cells inside usable hold cells;
- no overlap with other solid occupancy;
- orientation permitted by body plan;
- any fixture/zone requirements satisfied.

## 2.4 Distance

Default distance is Manhattan distance between the nearest occupied cells of two entities.

`distance(A,B) = min(|ax-bx| + |ay-by|)` over occupied cells.

Definitions:
- **adjacent** = distance 1;
- **near** = distance <= configured trait range;
- **same zone** = shares a route/fixture-defined zone tag, independent of distance.

A trait must specify which distance model it uses. No hidden Euclidean distance.

## 2.5 Line of effect

Default organism emissions do **not** require line of sight; they use range and environmental propagation rules.

Traits explicitly tagged `directed` use cardinal rays from designated emitter cells. A directed ray stops at:
1. blocking wall/fixture;
2. first solid organism if the trait is `interceptable`;
3. maximum range.

This avoids a universal line-of-sight subsystem while supporting a small number of readable directional mechanics later.

---

# 3. Authoritative time model

## 3.1 Transit ticks

Transit is resolved in integer ticks `t = 1..T`.

A normal contract should target approximately 10–24 ticks. Tutorial contracts may be shorter. Very long runs are discouraged because causal readability degrades.

The visual playback may slow, pause, or accelerate, but the authoritative simulation always advances whole ticks.

## 3.2 Snapshot rule

At the start of each phase, reads come from the state snapshot defined for that phase. Effects are accumulated into deterministic deltas or queued events and committed only at the phase boundary.

This prevents trait ordering from accidentally changing outcomes.

## 3.3 Exact tick order

Every transit tick resolves in this order:

### Phase A — Route and hold input
1. advance route timeline to tick `t`;
2. activate/deactivate scheduled route hazards;
3. compute fixture availability and hold-wide modifiers;
4. record route events.

### Phase B — Start-of-tick state transitions
1. decrement timers that expire at tick start;
2. resolve scheduled wake/recovery/maturation transitions;
3. apply transitions whose trigger was locked on the previous tick;
4. update footprint if the transition changes body stage;
5. if required growth cannot legally occupy its deterministic growth cells, apply the growth-blocked rule instead of searching arbitrarily for space.

### Phase C — Passive environmental generation
1. each organism/support computes channel output from its current state;
2. outputs are accumulated per source cell;
3. fixture and hazard channel contributions are added;
4. no organism has reacted to these values yet.

### Phase D — Environmental propagation and decay
1. local channel values propagate using the channel-specific rule;
2. decay/venting is applied;
3. cell values are clamped to channel bounds;
4. the resulting environmental field becomes the tick's exposure snapshot.

### Phase E — Exposure and direct interactions
1. each organism samples its occupied cells/environment;
2. adjacency/range trait effects are evaluated from the same snapshot;
3. feeding, soothing, agitation, contamination transfer, and other direct effects are emitted as effect records;
4. effects targeting the same variable are aggregated by the conflict rules below.

### Phase F — Internal meters
Apply aggregated changes to organism internal meters, including stress, contamination load, satiety, and trait-specific timers. Clamp values to legal ranges.

### Phase G — Threshold evaluation
Evaluate state thresholds after all Phase-F deltas are committed. State transitions are queued according to each transition's timing policy:
- `immediate_end_tick` — state changes now for scoring/end-of-tick outputs but cannot retroactively change earlier phases;
- `next_tick_start` — default for posture/behavior changes;
- `scheduled(n)` — fires after an explicit delay.

### Phase H — End-of-tick consequences
1. resolve queued immediate consequences;
2. evaluate organism critical conditions;
3. evaluate contract fail-fast conditions;
4. write causal event records;
5. take the authoritative end-of-tick snapshot.

### Phase I — Contract completion check
If `t == T` or a hard fail-fast condition ended the run, evaluate mandatory delivery conditions and optional objectives using the final authoritative snapshot plus timeline aggregates.

This ordering is canonical. Traits may add events inside a phase but may not reorder the global phases.

---

# 4. Environmental channel set

The base game uses **three spatial environmental channels**. More channels require explicit proof that they add non-redundant decisions.

## 4.1 Heat

Meaning: local thermal burden.

Why it exists:
- intuitive spatial propagation;
- creates clustering and spacing tradeoffs;
- can interact with growth, sleep, metabolism, route hazards, and supports;
- easy to visualize.

Authoritative representation: bounded integer/fixed-point `heat[cell]`.

Default propagation concept:
- sources add heat;
- each propagation step shares a configured fraction with orthogonal neighbors;
- hold walls/fixtures may alter transfer;
- passive cooling subtracts a fixed amount;
- values clamp at zero and channel maximum.

Exact rates are balance variables, not architecture.

## 4.2 Stress field

Meaning: environmental agitation perceived by nearby organisms — noise, pheromonal alarm, motion, social disturbance abstracted into one readable channel.

Why it exists:
- allows one panicking organism to create cascades;
- supports soothing organisms and barriers;
- creates meaningful social spacing without bespoke relationship tables;
- complements internal stress meter.

Distinction: **stress field** is spatial; **stress** is an organism's internal accumulated meter.

Propagation should be shorter-range and faster-decaying than heat so it behaves as local social pressure rather than a second temperature map.

## 4.3 Contamination

Meaning: spores, residue, microbes, parasites, or anomalous biological contamination present in a cell.

Why it exists:
- creates persistence and path-dependent danger;
- allows contamination to remain after a source changes state;
- supports cleaning/filter fixtures and immune/resistant traits;
- makes growth/movement-of-footprint consequences distinct from pure adjacency.

Contamination can persist longer than stress field and can be amplified or consumed by traits.

## 4.4 Channels deliberately excluded from the foundation

Not separate base channels:
- oxygen;
- humidity;
- light;
- sound;
- radiation;
- odor.

These can appear later only as route tags, binary requirements, or trait flavor unless playtesting demonstrates a unique decision space. The foundation must not become six overlapping heat maps.

---

# 5. Organism entity schema

Every organism instance contains at least:

## Identity/content
- `instance_id` — stable runtime identifier;
- `species_id` — data definition identifier;
- `body_plan_id`;
- display/flavor metadata separate from mechanics;
- ordered list of trait module IDs.

## Spatial
- anchor cell;
- orientation;
- current footprint stage;
- occupied cells derived from body plan + stage + orientation;
- deterministic growth direction priority if the body can expand.

## Internal meters
Foundation meters:
- `stress` — bounded 0..Smax;
- `contamination_load` — bounded 0..Cmax;
- `satiety` — bounded 0..Fmax.

Optional trait-local meters/timers are allowed but should be rare and visible when they affect decisions.

## State flags
An organism has one primary behavioral state plus orthogonal condition flags where needed.

Primary-state foundation:
- `CALM`;
- `AGITATED`;
- `PANICKED`;
- `ASLEEP`.

Condition flags:
- `CONTAMINATED`;
- `CRITICAL`;
- `GROWTH_BLOCKED`;
- `DELIVERY_FAILED` where contract logic marks irreversible loss.

Growth stage is not a primary mood state; it is body state (`JUVENILE`, `MATURE`, optional `ENLARGED`) because an organism can be both mature and asleep.

## Contract condition
Each organism may have delivery requirements such as:
- survive/not critical;
- stress <= threshold;
- contamination_load <= threshold;
- reach or avoid a growth stage;
- remain fed above threshold;
- never enter a forbidden state;
- finish in a required zone.

Requirements are explicit before launch unless a tutorial is intentionally introducing a rule.

---

# 6. Internal meters and transitions

## 6.1 Stress

Stress is the main short-term instability meter.

Canonical threshold pattern:
- below `agitated_enter` → CALM unless another primary state overrides;
- at/above `agitated_enter` → AGITATED;
- at/above `panic_enter` → PANICKED;
- recovery uses lower exit thresholds (`agitated_exit`, `panic_exit`) to create hysteresis and prevent flicker.

`panic_enter > agitated_enter > agitated_exit`.

Panic must materially change outputs/behavior; it cannot be a cosmetic state. Typical panic effects include stronger stress-field emission, increased heat output, refusal to feed, or activation of a panic-specific trait.

## 6.2 Contamination load

Organisms absorb contamination from occupied cells and direct contact traits. Resistance modifies intake, not the environmental value itself.

At a configured load threshold, `CONTAMINATED` becomes true. Some traits may become active only while contaminated. Recovery can require load falling below a lower threshold or a treatment/support effect.

Contamination is never random infection chance in transit. Exposure deterministically changes load.

## 6.3 Satiety

Satiety represents nutritional reserve. Baseline metabolism may consume a small deterministic amount per tick for selected organisms.

Below hunger thresholds, an organism may:
- become more stress-sensitive;
- seek/trigger feeding interactions;
- change emissions;
- fail a welfare objective.

Feeding is an interaction rule, not freeform movement. Organisms do not walk around the hold in the base design.

## 6.4 Sleep

Sleep is an explicit state with entry conditions/timers. Sleeping commonly reduces stress-field sensitivity/output and may reduce metabolism, but specific effects are trait-defined.

Sleep is not a universal safe button because:
- some contracts require organisms awake at arrival;
- some organisms cannot be sedated/slept;
- sleeping can reduce beneficial emissions;
- some hazards wake organisms;
- support capacity/space limits prevent blanket sleep strategies.

## 6.5 Critical state

`CRITICAL` means the organism has crossed a severe welfare/survival boundary. It does not automatically end every contract; contract rules decide whether criticality is immediate failure or merely destroys an optional goal.

Critical transitions must identify a primary causal meter/event in the timeline.

---

# 7. Trait grammar

Traits are small reusable rule modules. A species should normally use 1–3 mechanically significant traits at launch; more requires strong readability proof.

Every trait definition has:
- trigger phase;
- trigger condition;
- target selector;
- range/adjacency model;
- effect list;
- state gating;
- numeric parameters;
- UI summary template;
- causal-log template;
- priority only where a true non-commutative operation exists.

## 7.1 Foundation trait families

The initial grammar should support at least these ten trait archetypes:

### T01 Heat Emitter
While active, adds heat to occupied cells each tick.

### T02 Heat Sink
Reduces heat in occupied/adjacent cells up to a per-tick capacity. Capacity prevents one sink from solving the whole hold.

### T03 Alarm Emitter
When AGITATED/PANICKED, emits stress field; panic emission is stronger.

### T04 Soother
Reduces stress-field exposure or directly reduces internal stress of adjacent organisms. It has a per-tick target/capacity limit and may stop functioning while itself panicked/asleep.

### T05 Spore Shedder
While contaminated or at a defined growth stage, emits contamination.

### T06 Filter Feeder
Consumes contamination from adjacent/occupied cells and converts part of it into satiety or another beneficial outcome. This creates useful-but-risky adjacency.

### T07 Grazer
Consumes edible output from an adjacent compatible source. Feeding amount and source cost are deterministic.

### T08 Growth Trigger
When satiety/heat/other explicit condition is satisfied for `n` ticks, queues growth to a larger footprint stage.

### T09 Symbiotic Buffer
When adjacent to a compatible target, grants a narrow resistance or reduces one channel. It must be conditional and capacity-limited, never a universal all-purpose shield.

### T10 Reactive Pulse
On entering a named state (e.g. PANICKED, CONTAMINATED, MATURE), emits a one-time pulse such as heat, stress, cleansing, or food production. This supplies dramatic deterministic cascades.

These are archetypes, not final species names.

## 7.2 Trait restrictions

Foundation traits may not:
- roll random chances;
- move organisms autonomously;
- spawn arbitrary new entities without bounded placement rules;
- read future route events unless explicitly framed as prediction support outside simulation;
- silently modify another trait's parameters;
- perform hidden global searches for “best” targets.

Target selection must be explainable and deterministic.

---

# 8. Simultaneous effect resolution

## 8.1 Additive effects

Effects on meters/channels are additive within a phase unless the trait explicitly defines a cap.

Example:
- two adjacent soothers each apply `-2 stress`;
- one alarm applies `+3 stress`;
- aggregate delta = `-1` before clamping.

## 8.2 Multipliers

Multipliers are discouraged because order is less intuitive. Where required, combine all additive deltas first, then apply modifiers in a fixed category order:
1. source production modifier;
2. transmission modifier;
3. target intake/resistance modifier;
4. final clamp.

Within a category, multiplicative modifiers combine multiplicatively using fixed-point arithmetic.

## 8.3 Capacity-limited consumers

When one entity can affect only `k` targets or consume a finite amount, target allocation uses a deterministic selector declared by the trait.

Allowed selectors include:
- nearest, then lowest `instance_id` tie-break;
- highest exposure, then nearest, then `instance_id`;
- clockwise from orientation direction;
- explicit player-linked target if the support module allows a pre-launch link.

“Random target” is forbidden for authoritative transit.

## 8.4 Competing consumption

If multiple consumers claim a finite cell resource, resolve proportionally when divisible; otherwise use stable selector order documented by that resource. The UI must be able to preview the rule.

## 8.5 State-entry triggers

If multiple organisms cross thresholds on the same tick, all threshold decisions use the same committed Phase-F snapshot. State-entry pulses then execute as a batch in Phase H. A pulse cannot stop another same-tick threshold crossing retroactively.

This is crucial for reproducibility and causal review.

---

# 9. Growth and footprint change

Growth must create spatial drama without freeform pushing.

## 9.1 Predeclared growth footprints

A body plan defines discrete stages. Example:
- juvenile: `{(0,0)}`;
- mature: `{(0,0),(1,0)}` relative to orientation;
- enlarged: additional declared offsets.

## 9.2 Growth resolution

When growth triggers:
1. compute the next footprint from current anchor/orientation;
2. identify newly required cells;
3. if every required cell is legal and empty, growth succeeds at the defined transition boundary;
4. otherwise growth does **not** push neighbors or search another orientation;
5. organism receives `GROWTH_BLOCKED` and a defined consequence.

Possible body-plan consequences are data-defined but must be explicit, e.g. stress increase per blocked tick, delayed maturation, or delivery failure if maturation was required.

## 9.3 Why no pushing

Automatic pushing introduces non-local chain resolution, unclear priorities, and physics-like ambiguity. The planning problem is stronger when the player must reserve future space deliberately.

## 9.4 Shrink/retraction

If a trait later allows shrinking, vacated cells become empty at the transition boundary. No other entity moves automatically into them during transit; the benefit is environmental spacing or future growth capacity.

---

# 10. Feeding

Feeding is defined through compatibility tags and adjacency/range, not animation collision.

A producer can expose `food_type` and amount. A consumer has compatible food tags and deterministic demand.

Canonical order in Phase E:
1. compute available food outputs from source snapshot;
2. enumerate eligible consumer-source edges;
3. allocate using source's selector/capacity rule;
4. emit satiety gain and source-cost effects;
5. commit in Phase F.

Cannibalism/predation is outside the foundation because it risks changing the tone and requiring removal/death topology. It may be reconsidered only if later content design proves essential.

---

# 11. Route hazards

Route hazards are deterministic timeline modifiers known before launch unless a contract explicitly teaches partial information.

Foundation hazard families:

## H01 Thermal surge
For specified ticks, adds heat to all cells or a named zone.

## H02 Vibration burst
Adds stress-field pressure and/or wakes sleeping organisms at specified ticks.

## H03 Contamination leak
Adds contamination to a specified cell/zone for specified ticks.

## H04 Power brownout
Disables or reduces selected support fixtures for specified ticks.

## H05 Vent cycle
Increases environmental decay/venting for specified ticks; can be beneficial or harmful to organisms needing warmth/contamination as food.

## H06 Zone isolation
Temporarily changes propagation across a declared boundary or closes a fixture conduit. Geometry itself does not move.

Hazards are timeline data, not random runtime rolls.

A route may combine hazards, but normal contracts should avoid more than two new hazard concepts simultaneously.

---

# 12. Hold support modules

Supports are optional tools that occupy cells, fixture slots, power budget, or contract budget. The foundation needs enough constraints that “support everything” is not dominant.

Candidate foundation supports:

## S01 Cooler
Consumes power; removes heat locally up to capacity.

## S02 Filter
Consumes power; removes contamination locally up to capacity.

## S03 Baffle
Occupies cells; reduces stress-field transmission across its edge/zone but also blocks some beneficial proximity.

## S04 Nest pad
One organism occupying/adjacent to the pad receives sleep/recovery benefit; capacity 1.

## S05 Feed cartridge
Finite deterministic food reserve for compatible organisms; occupies a cell or fixture slot.

## S06 Monitor beacon
No direct simulation power; improves planning/review information for advanced uncertain-trait contracts. This prevents all support choices from being raw mitigation.

Supports must carry opportunity cost. The exact combination of cell occupancy, fixture slots, power, and contract-specific allowance is Phase-4/7 balance work.

---

# 13. Success and failure evaluation

## 13.1 Hard validity before launch

Launch is blocked only for structurally invalid setup:
- manifest entity unplaced;
- illegal overlap/out-of-bounds placement;
- forbidden orientation/zone;
- required fixture not connected/assigned where the contract explicitly requires it.

The game does **not** block launch merely because simulation predicts failure. Players may intentionally test a hypothesis.

## 13.2 During transit

A contract can define `fail_fast` conditions, but these should be rare. Examples:
- organism enters irreversible fatal/critical state when all organisms must survive;
- hold system reaches catastrophic threshold.

Most failures should continue to the end when useful because observing the rest of the cascade provides evidence.

## 13.3 End-of-transit mandatory evaluation

Mandatory conditions are Boolean predicates over:
- final organism states/meters;
- final positions/body stages;
- timeline facts such as `never_panicked` or `max_heat_seen`;
- support/resource usage;
- route completion.

All mandatory predicates must pass for contract success.

## 13.4 Optional scoring

Optional objectives create replay depth without blocking campaign progress. Examples:
- no organism panicked;
- contamination never exceeded X;
- use <= N powered supports;
- leave >= N cells empty;
- deliver a named organism mature;
- finish with total stress below threshold;
- use no sedating support;
- no growth-blocked events.

Scores should reward different approaches rather than a single universal “fewest moves” metric.

---

# 14. Causal event log

Every authoritative change that can affect outcome emits an event record:
- tick;
- phase;
- source entity/hazard/support;
- target entity/cell/channel;
- effect type;
- pre-value;
- delta or transition;
- post-value;
- rule/trait ID;
- optional parent event ID for cascade chains.

Example chain:
1. tick 5 thermal surge raises heat near Organism A;
2. A crosses agitation threshold;
3. tick 6 A's alarm trait emits stress field;
4. B absorbs stress and panics;
5. B's reactive pulse emits contamination;
6. C crosses contamination delivery limit.

The post-run UI must be able to reconstruct this chain without simulation-specific ad hoc text.

---

# 15. Anti-dominant-strategy architecture

## 15.1 “Isolate everything”

Countermeasures:
- holds are compact;
- beneficial adjacency exists (feeding, soothing, filtering, symbiosis);
- some organisms require compatible neighbors;
- optional objectives can reward space efficiency;
- growth requires reserved cells, making all-empty buffers expensive.

A valid advanced contract should often contain at least one reason to cluster and one reason to separate.

## 15.2 “Sedate everything”

Countermeasures:
- not all organisms can sleep;
- some must arrive awake;
- sleep suppresses useful emissions/feeding;
- vibration hazards wake organisms;
- nest/sedation support is capacity-limited and costly;
- prolonged sleep can reduce satiety or prevent growth.

No generic sedation consumable that simply removes stress from all organisms is allowed.

## 15.3 “Maximum empty space”

Countermeasures:
- every manifest organism is mandatory unless contract says otherwise;
- support modules compete for space;
- beneficial proximity and feeding can require compact layouts;
- some optional goals reward compactness;
- later holds may be irregular rather than simply larger.

## 15.4 “Universal buffer organism”

No organism may simultaneously neutralize all three environmental channels with broad range and no meaningful downside.

Buffer traits must be narrow by channel, conditional, capacity-limited, or create a cost elsewhere.

## 15.5 “One solved template for every contract”

Countermeasures:
- varying hold geometry;
- rotating/directional body plans;
- route-specific hazard zones/timings;
- manifest composition changes;
- growth timing;
- optional objectives that alter priorities.

Generation must detect if trivial template reuse solves too many challenge families.

---

# 16. Determinism invariants

The implementation must preserve these invariants:

1. Same initial serialized state + content version + route definition = bit-equivalent authoritative result where practical.
2. Entity iteration order never affects additive outcomes.
3. Where order is inherently necessary, a documented stable selector resolves ties.
4. Visual frame rate never affects simulation state.
5. Input during transit cannot alter authoritative state in the base design; transit is observation after commitment.
6. Pause/playback speed never changes outcome.
7. Loading/replaying an in-progress authoritative snapshot yields the same remaining outcome.
8. Numeric operations use deterministic integer/fixed-point arithmetic for authoritative values; avoid platform-dependent floating-point accumulation where feasible.
9. Every threshold transition is evaluated at a named phase boundary.
10. Every content definition affecting simulation carries a version/hash for save/replay diagnostics.

---

# 17. Edge-case rules

## 17.1 Simultaneous critical conditions
All are recorded; contract failure chooses a primary display reason only for UI brevity. Causal log retains every violation.

## 17.2 Entity becomes critical while emitting a beneficial effect
Effects already emitted from the phase snapshot remain for that tick. Critical-state behavior changes apply only at the next allowed phase boundary.

## 17.3 Growth and route hazard same tick
Route hazard Phase A applies first; start-of-tick growth Phase B then resolves. If growth was scheduled from previous tick, hazard activation cannot cancel it unless the hazard explicitly changes cell legality before Phase B.

## 17.4 Support loses power mid-tick
Brownout state is established Phase A, so the support is inactive for all later phases that tick.

## 17.5 Multiple threshold crossings
All thresholds derive from the same post-meter snapshot. If one organism crosses both contamination and panic thresholds, both condition changes are queued; primary behavioral state precedence is explicit in the organism state policy.

## 17.6 Exact threshold values
Comparisons are inclusive where written `>= threshold`; content definitions must never rely on fuzzy float equality.

## 17.7 Invalid content definition
The validator rejects content with impossible footprint stages, circular immediate triggers, missing target selectors, undefined tags, negative capacities, or transition loops that can execute infinitely within one tick.

---

# 18. Foundation challenge grammar

A challenge is mechanically interesting when it combines at least two pressures from different families:

- **space pressure** — footprint/growth/blocked cells;
- **environment pressure** — heat/stress field/contamination;
- **relationship pressure** — feeding/soothing/symbiosis;
- **time pressure** — hazards and delayed state transitions;
- **support pressure** — limited power/slots/capacity;
- **objective pressure** — optional conditions that favor a different layout than mere survival.

Advanced contracts should generally combine 3–4 families, not all six at once.

Difficulty comes from interactions, not opaque rule count.

---

# 19. Worked deterministic example

Hold: 5x5. Transit: 8 ticks.

Manifest:
- A: 1x1 Heat Emitter + Alarm Emitter; panic threshold 8.
- B: 1x1 Soother; works only while CALM.
- C: juvenile 1x1 Filter Feeder; grows to 1x2 after satiety condition; contamination-sensitive.
- D: Spore Shedder while contaminated.

Route:
- tick 3–4 thermal surge on left zone;
- tick 6 vibration burst.

Planning tension:
- A near B keeps A calm, but B near thermal surge may itself become agitated and stop soothing;
- C near D can eat/filter contamination, but if C grows toward occupied space it becomes growth-blocked;
- isolating D removes contamination risk but starves C of its useful filtering/feeding interaction;
- reserving a cell for C growth reduces buffer space around A.

Illustrative cascade if arranged poorly:
1. tick 3 surge raises A/B heat exposure;
2. B accumulates stress and becomes AGITATED at end tick 3;
3. tick 4 B no longer soothes; A crosses panic threshold;
4. tick 5 A panic alarm raises local stress field;
5. D becomes stressed, activates contamination shedding condition;
6. C filters contamination and gains satiety;
7. C queues growth;
8. growth at next tick is blocked by the cell the player used as an A/B spacer;
9. C gains stress/loses delivery objective;
10. vibration worsens the cascade.

A better layout may deliberately accept more heat on A while preserving B's calm state and C's future growth cell.

This is the target texture: **no single placement rule is difficult, but temporal interaction makes the initial arrangement meaningful.**

---

# 20. Foundational balance variables

Exact numbers remain tunable data. Required exposed variables include:

## Hold
- width/height;
- blocked-cell mask;
- zone definitions;
- fixture locations;
- base propagation/decay parameters per channel.

## Route
- tick count;
- hazard start/end ticks;
- hazard zone/intensity;
- support availability modifiers.

## Organism
- meter maxima;
- threshold enter/exit values;
- base meter decay/recovery;
- channel intake coefficients;
- trait output amounts;
- trait ranges;
- capacities;
- growth delays/footprints;
- feeding rates;
- delivery thresholds.

## Supports
- power cost;
- space/fixture cost;
- per-tick capacity;
- range;
- consumable reserve where applicable.

## Contract
- allowed supports;
- power/support budget;
- mandatory predicates;
- optional predicates;
- medal/score thresholds;
- information visibility rules.

---

# 21. Mechanical validation gates

Before Phase 4 can be called mechanically complete, a graybox/simulation validator must demonstrate on paper or in throwaway tests that:

1. at least three clearly different valid layouts can solve some contracts;
2. at least one contract requires planning for future footprint change;
3. at least one contract requires beneficial adjacency despite contamination/stress risk;
4. isolate-all fails or loses major optional value on representative advanced contracts;
5. sedate-all is impossible or inferior by construction;
6. a single buffer species cannot dominate all manifests;
7. a 12–20 tick cascade can be explained in <= 5 major causal steps in the UI summary while retaining full detail in the timeline;
8. changing one initial placement can create a predictable multi-step consequence rather than merely +/- score;
9. deterministic replay produces identical event logs;
10. content validator can reject unsolvable or degenerate generated contracts;
11. the system remains legible with roughly 6–10 organisms without requiring constant tooltip reading during transit;
12. environmental channels produce genuinely different layout decisions rather than acting as renamed copies.

---

# 22. Remaining Phase 4 work

The foundation is locked enough to proceed, but Phase 4 is **not complete**. Still required:

1. exact player action legality and pre-launch prediction aids;
2. support-resource model (power/slots/budget) selection;
3. full organism primary-state precedence and state-transition table;
4. species/body-plan construction grammar and restrictions;
5. contract mandatory/optional predicate language;
6. campaign difficulty curve at mechanical level;
7. formal scoring/medal model;
8. information uncertainty model for newly discovered traits;
9. support-module final foundation roster;
10. explicit mechanical acceptance tests for each trait family;
11. vertical-slice content set built from this grammar;
12. adversarial pass against degenerate loops, infinite trigger chains, unreadable cascades, and content combinations that are technically valid but not fun.

Until these are specified and later integrated with content/UX/technical architecture, `DESIGN COMPLETE` remains **NO**.
