# ORGANISM CARGO — DECISION ARCHITECTURE

Status: **CANONICAL PHASE 4 APPENDIX — DECISION LAYER LOCKED**
Last updated: 2026-08-15

This file is canonical for the Phase-4 player-decision layer of **Organism Cargo**. It extends `MECHANICS.md` without replacing its simulation rules. If a conflict exists, the product thesis in `GAME_BIBLE.md` is highest-level authority; otherwise the more specific rule in this file governs pre-launch action legality, preview, support resources, behavioral-state precedence, species construction, contract predicates, difficulty, scoring, uncertainty, and acceptance tests.

The purpose of this layer is to make the deterministic simulation into a playable decision system rather than merely a correct ecology model.

---

# 1. Pre-launch player action legality

## 1.1 Planning state is non-punitive

Before launch, planning actions are **free, reversible, and unlimited**. There is no move counter, no real-time countdown, and no score penalty for dragging an organism several times.

Reason: the intended pressure comes from understanding a living system, not from interface dexterity or fear of experimenting with the board.

The player may:
- inspect any manifest organism;
- inspect any support module allowed by the contract;
- inspect any hold cell, zone, fixture, route hazard, objective, and known trait;
- place any unplaced organism on legal cells;
- move any placed organism to another legal position;
- rotate an organism only through orientations declared by its body plan;
- remove a placed organism back to the manifest tray;
- place/move/remove supports subject to support-specific legality;
- assign a pre-launch link/target when a support explicitly permits one;
- undo/redo planning actions;
- reset the entire setup to the contract's original state;
- save the current planning arrangement locally as the contract's working setup;
- launch any structurally valid setup even when known indicators suggest likely failure.

## 1.2 Organism placement legality

An organism placement is legal only if all are true:
1. every current-footprint cell is inside the usable hold;
2. no current-footprint cell overlaps another solid organism/support;
3. body-plan orientation is legal;
4. any explicit zone restriction is satisfied;
5. no occupied cell is blocked;
6. any contract-specific anchor/fixture rule is satisfied.

The UI may allow dragging through illegal positions visually, but the authoritative placement snaps only to a legal state. Illegal reasons must be shown specifically: `overlap`, `blocked`, `outside hold`, `orientation forbidden`, `wrong zone`, or `fixture required`.

## 1.3 Future growth is not a launch-validity rule

A setup remains structurally launchable if a future growth footprint is blocked. The player is warned when a **known** growth rule has no legal future cells, but launch is not prevented.

Reason: future-space planning is part of the game. Automatically preventing a bad future state would solve an intended decision for the player.

Exception: an authored tutorial may temporarily block launch while explicitly teaching the growth rule, but this is onboarding scaffolding, not a general mechanic.

## 1.4 Rotation

Rotation is discrete, normally 90-degree cardinal orientation changes. A body plan declares its legal orientation set.

Rules:
- symmetric orientations that create identical footprints may be collapsed in the UI;
- rotation may change directed trait rays and deterministic growth direction;
- the preview must update immediately after rotation;
- rotation cannot be performed during transit in the base game.

## 1.5 Support placement legality

Supports belong to one of three placement classes:

### Cargo-cell support
Occupies one or more ordinary hold cells and blocks organism occupancy.
Examples: baffle, feed cartridge.

### Utility-fixture support
Installs only in a declared utility fixture and does not consume cargo cells beyond the fixture's fixed footprint.
Examples: cooler, filter, monitor beacon.

### Organism-bed support
Occupies a declared bed/pad fixture or cell and may affect at most one linked/occupying organism.
Example: nest pad.

A support definition must declare exactly one class. No support silently changes class by contract.

## 1.6 Support assignment and links

A support may permit a deterministic pre-launch link only when its rule depends on a named target. The player explicitly chooses the target and the UI draws the link.

Links are invalidated if:
- target is removed from the hold;
- target no longer satisfies range/zone requirements;
- support is removed;
- contract forbids the pairing.

Invalid links block launch only when the support's definition says the link is required for functioning. Otherwise the support launches unlinked and does nothing until its rule can legally apply.

## 1.7 Undo / redo

Planning requires a normal reversible command history.

Undoable actions:
- place;
- move;
- rotate;
- remove;
- support install/remove;
- support link change;
- setup reset as a single undoable action where practical.

Undo history is cleared when transit launches. Post-run retry reconstructs the exact pre-launch setup that was committed, then starts a new planning history from that state.

## 1.8 Reset modes

Two reset actions are distinct:

- **Reset to last launch** — available after a transit; restores the exact committed layout/support setup so the player can make one targeted revision.
- **Reset contract** — restores the contract's initial empty/default planning state.

The first is the default retry behavior because the game wants hypothesis-driven revision rather than rebuilding from memory.

## 1.9 Launch validity

The launch button is enabled when:
- every mandatory manifest organism is placed;
- every placement is structurally legal;
- support use does not exceed slot/power/allowance constraints;
- all required support links/fixture assignments are valid;
- no contract-defined structural prerequisite is missing.

Launch validity does **not** require:
- predicted survival;
- predicted medal completion;
- future growth space;
- low heat/stress/contamination;
- a support module;
- a solver-confirmed solution.

The game must never present `likely failure` as `invalid setup`.

---

# 2. Prediction and preview rules

## 2.1 Preview philosophy

The pre-launch UI explains **known local rules and immediate relationships** but never runs the full future on the player's behalf.

The player should be able to understand why a plan might work without receiving a solved answer.

Three information layers are canonical:

1. **Facts** — current state and rules already known.
2. **Immediate influence preview** — direct relationships implied by the current arrangement.
3. **Transit evidence** — what actually happened on a committed run.

These layers must never be visually conflated.

## 2.2 Facts shown before launch

Always visible or inspectable when known:
- current organism meters and state;
- current footprint and legal growth footprint direction/stages;
- documented trait text;
- documented trait range/direction;
- current adjacency and compatibility;
- support effects/capacities;
- route timeline and hazards when the contract marks them known;
- mandatory and optional contract predicates;
- power/fixture/support allowance usage.

## 2.3 Immediate influence preview

The player may toggle overlays for:
- heat sources/sinks and their **current-tick local footprint/range**;
- stress-field sources/soothers and current range;
- contamination sources/filters and current range;
- feeding compatibility edges;
- symbiotic compatibility edges;
- directed trait rays;
- future body footprint for the next documented growth stage;
- support influence areas.

The preview may answer:
- `A currently affects B`;
- `B is inside this source's range`;
- `C would require these cells if it grew next stage`;
- `this cooler covers these cells`.

It may **not** answer before launch:
- `A will panic on tick 7`;
- `this arrangement will succeed`;
- `move B here to solve the contract`;
- complete future channel maps for every tick;
- a full causal chain that has not yet occurred.

## 2.4 One-tick arithmetic assistance

For documented traits, inspection may show an exact **current-state contribution** such as `+2 heat/tick while CALM` or `reduces up to 3 contamination/tick from adjacent cells`.

The UI may total direct current contributions on a selected cell/entity if doing so saves arithmetic, but it must label the value as **current-state only**. It must not account for future state transitions, route phases, or growth unless those events are already active at time zero.

This keeps the puzzle about causal prediction, not calculator transcription.

## 2.5 Route timeline preview

Known route events are shown as a compact timeline with tick windows and affected zones.

Example:
- ticks 3–4: thermal surge, port zone;
- tick 7: vibration burst, hold-wide;
- ticks 9–10: vent cycle.

If a contract intentionally withholds route information, the hidden segment is clearly marked as unknown rather than omitted deceptively.

## 2.6 No auto-solver preview

The base game has no button that:
- simulates all arrangements;
- ranks placements;
- marks a setup `safe`;
- gives a percentage success chance;
- recommends a move.

A later accessibility feature may expose more explanatory math, but it may not calculate strategic recommendations.

## 2.7 Post-attempt knowledge advantage

After a committed transit, the player may scrub the actual event timeline and inspect exact past values for that run. Retrying does not hide learned evidence.

This creates the intended loop:
**prediction → experiment → evidence → revised prediction**.

---

# 3. Locked support-resource model

The foundation uses **three distinct constraints**, each with a different purpose:

1. **physical space / fixture topology**;
2. **utility power capacity**;
3. **contract support allowance**.

There is **no generic money budget during an individual contract** in the foundation.

Reason: a fourth interchangeable currency would add bookkeeping without a unique spatial/systemic decision.

## 3.1 Physical space and fixtures

Every hold declares:
- cargo cells;
- blocked cells;
- utility fixtures;
- optional bed/pad fixtures;
- zone boundaries.

Some supports consume valuable cargo cells; others compete for scarce utility fixtures. This ensures support choice changes layout rather than functioning as a menu-only buff.

## 3.2 Power capacity

Each hold has an integer `power_capacity` for powered supports.

Each powered support has integer `power_draw`.

Pre-launch invariant:
`sum(active installed support power_draw) <= power_capacity`.

Route brownouts may lower **available transit power** after launch. The player cannot violate pre-launch power capacity, but a known brownout can temporarily disable supports according to deterministic priority rules.

## 3.3 Power priority during brownout

Before launch, each powered support receives a unique priority order when more than one is installed. Default order is installation order, but the player may reorder it freely.

When available route power drops below installed demand:
1. support power is allocated in player-declared priority order;
2. a support is either fully powered or off unless its definition explicitly permits degraded operation;
3. powered/off transitions are recorded in the causal log;
4. no random support selection occurs.

This turns brownouts into predictable planning rather than surprise punishment.

## 3.4 Contract support allowance

A contract defines which support module types and quantities are available for that shipment.

Examples:
- one cooler + one filter + one baffle;
- choose any two supports from a supplied pool;
- no powered supports;
- only one cargo-cell support.

This is a **loadout allowance**, not currency. The player cannot grind resources elsewhere to overpower a contract.

## 3.5 Why no persistent consumable stock

Feed cartridges may have finite **in-transit capacity**, but the campaign does not require buying/restocking them from a persistent economy.

Persistent consumable inventory is excluded because it creates hoarding, grind, and failure punishment that conflicts with the puzzle-learning loop.

## 3.6 Support opportunity-cost principles

Every foundation support must cost at least one of:
- cargo space;
- fixture slot;
- power;
- limited contract allowance;
- loss of beneficial propagation/proximity;
- finite in-run capacity.

No support may be universally positive with zero tradeoff.

---

# 4. Final foundation support roster

Six supports are retained. None are cut at this stage because each occupies a distinct mechanical role.

## S01 Cooler — RETAIN

Class: utility fixture.
Power: yes.
Role: local heat mitigation.

Rules:
- removes heat from declared cells/range up to a per-tick capacity;
- cannot reduce below zero;
- capacity is shared across affected cells with deterministic allocation;
- vulnerable to brownout;
- cannot simultaneously remove contamination/stress.

Decision created: power/fixture competition and local thermal planning.

## S02 Filter — RETAIN

Class: utility fixture.
Power: yes.
Role: contamination mitigation.

Rules:
- removes environmental contamination, not organism internal load directly;
- finite per-tick capacity;
- vulnerable to brownout;
- does not remove heat/stress.

Decision created: prevention vs organism-based filtering and fixture/power tradeoff.

## S03 Baffle — RETAIN

Class: cargo-cell support.
Power: no.
Role: propagation shaping.

Rules:
- occupies one or more cells/edges depending body representation;
- reduces stress-field transmission across declared boundary;
- may also block directed rays if tagged solid;
- does not erase stress already on either side;
- can block beneficial soother/social relationships and consume future growth space.

Decision created: separation has a concrete spatial cost.

## S04 Nest Pad — RETAIN

Class: organism-bed support.
Power: no by foundation default.
Role: targeted sleep/recovery assistance.

Rules:
- capacity one organism;
- linked/occupying organism gains sleep-entry or recovery benefit defined by the pad;
- does not force sleep through wake conditions;
- may suppress a beneficial awake-only trait indirectly because the organism sleeps;
- some organisms are incompatible.

Decision created: targeted calm at the cost of fixture/placement and lost awake behavior.

## S05 Feed Cartridge — RETAIN

Class: cargo-cell support.
Power: no.
Role: finite nutrition source.

Rules:
- occupies a cargo cell;
- holds finite deterministic food units;
- declares food compatibility tags;
- eligible adjacent consumers compete by documented selector;
- empty cartridge remains solid during transit unless a future content rule explicitly says otherwise.

Decision created: sacrifice space to stabilize feeding/growth timing.

## S06 Monitor Beacon — RETAIN, REDEFINED

Class: utility fixture.
Power: yes, low draw.
Role: information, not mitigation.

The beacon **does not reveal a full future simulation**.

In contracts containing intentionally uncertain route segments or undocumented organism behavior, the beacon may reveal one of the following as specified by the contract:
- exact intensity/timing of one otherwise-bounded route hazard family;
- exact numeric values for one selected organism's internal meters during transit playback/review when those values would otherwise be shown only categorically;
- exact local channel readings for cells within beacon range during playback/review.

The choice is known before launch. It never identifies the correct layout.

Decision created: spend a fixture/power/allowance slot on better evidence rather than direct protection.

## 4.1 Foundation support prohibition

Do not add a universal `shield`, global sedation system, teleport/reposition support, undo-during-transit tool, or all-channel cleanser. Such tools collapse the core commitment/prediction loop.

---

# 5. Primary behavioral-state model

An organism has exactly one **primary behavioral state**:
- `CALM`;
- `AGITATED`;
- `PANICKED`;
- `ASLEEP`.

Condition flags (`CONTAMINATED`, `CRITICAL`, `GROWTH_BLOCKED`, etc.) are orthogonal and never replace the primary state.

## 5.1 State precedence

`ASLEEP` is an exclusive behavioral override while the organism remains asleep.

An asleep organism still has an internal stress meter. Stress can rise/fall during sleep, but awake mood states are not simultaneously active.

When sleep ends, the organism's awake state is derived immediately from its current stress using the hysteresis transition rules below.

`CRITICAL` does not override the primary behavioral state; it is a condition flag so a creature can be `PANICKED + CRITICAL` or `ASLEEP + CRITICAL` if content allows the latter.

## 5.2 Required threshold ordering

For every organism using the foundation stress state machine:

`panic_enter > panic_exit >= agitated_enter > agitated_exit >= 0`.

The values may differ by species but the ordering may not.

This creates hysteresis and prevents state flicker.

## 5.3 Awake-state transition table

Transitions are evaluated at Phase G after Phase-F meter commits.

### Current CALM
- if `stress >= panic_enter`: queue `PANICKED`;
- else if `stress >= agitated_enter`: queue `AGITATED`;
- else remain `CALM`.

### Current AGITATED
- if `stress >= panic_enter`: queue `PANICKED`;
- else if `stress <= agitated_exit`: queue `CALM`;
- else remain `AGITATED`.

### Current PANICKED
- if `stress > panic_exit`: remain `PANICKED`;
- else if `stress <= agitated_exit`: queue `CALM`;
- else queue `AGITATED`.

Awake mood transitions default to `next_tick_start` so a threshold crossed from this tick's effects changes behavior on the next authoritative tick. A state-entry reactive pulse may be queued for the transition boundary according to its trait definition, but never retroactively modifies the crossing tick.

## 5.4 Entering sleep

Sleep entry is never automatic for all organisms. It requires an explicit source:
- organism trait;
- nest pad;
- starting contract state;
- route event designed to induce sleep.

A sleep-entry rule declares:
- eligibility tags;
- required conditions;
- optional maximum stress for entry;
- delay/timer;
- expected duration or wake conditions.

Sleep entry normally resolves `next_tick_start` after eligibility is satisfied.

## 5.5 While ASLEEP

Default sleep behavior modifiers may include:
- reduced stress-field sensitivity;
- reduced stress-field emission;
- reduced metabolism;
- disabled awake-only traits;
- enabled sleep-only traits.

These modifiers are data-defined and shown in trait/state UI. Sleep itself does not imply invulnerability.

## 5.6 Waking

Wake can be triggered by:
- sleep timer expiration;
- known vibration hazard;
- explicit wake trait/effect;
- organism-specific stress `wake_threshold` reached while asleep;
- contract-defined arrival wake event.

Wake is queued for the next valid Phase-B transition boundary.

On wake:
1. remove `ASLEEP`;
2. derive awake state from current stress as if entering the state machine fresh:
   - `stress >= panic_enter` -> PANICKED;
   - else `stress >= agitated_enter` -> AGITATED;
   - else CALM;
3. fire any legal wake/state-entry events in their documented later phases.

## 5.7 Same-tick sleep and wake request

If both are queued for the same next-tick boundary, **wake wins**. This prevents a vibration event or severe stress from being erased by simultaneous sleep eligibility.

The causal log records both requests and the precedence decision.

## 5.8 Condition flags

### CONTAMINATED
Enters at `contamination_load >= contaminated_enter`.
Exits only at `contamination_load <= contaminated_exit`, where `contaminated_exit < contaminated_enter`, unless a trait makes the state irreversible for the current contract.

### CRITICAL
Enters when an explicit severe condition is met. Criticality is normally sticky for the transit unless the organism/content definition explicitly supports recovery. Recovery rules must be uncommon and visible.

### GROWTH_BLOCKED
Set when scheduled growth cannot occupy required cells. It may clear if a later growth attempt is legal, but because entities do not move during transit, clearing normally requires a temporary cell-legality change rather than neighbor movement.

### DELIVERY_FAILED
Used only when a mandatory organism requirement becomes irreversibly impossible before arrival. It is a contract-evaluation flag, not a biological state.

## 5.9 State-output requirement

Every primary state must materially affect at least one of:
- emissions;
- intake/sensitivity;
- feeding eligibility;
- trait activation;
- metabolism;
- sleep/wake behavior;
- contract condition.

A state with no gameplay effect is visual flavor and must not enter the authoritative state machine.

---

# 6. Species and body-plan construction grammar

## 6.1 Species is a composition, not bespoke code

A species definition is built from:
- one body plan;
- one starting growth stage;
- legal orientations;
- base thresholds/intake coefficients;
- 1–3 mechanically significant trait modules;
- zero or more **passive readability tags** that do not introduce separate active mechanics;
- optional growth-stage transition;
- presentation metadata.

No species may require a one-off simulation subsystem unless that subsystem is promoted into a reusable trait family.

## 6.2 Trait count

Foundation campaign rules:
- introductory species: 1 significant trait;
- standard species: 2 significant traits;
- advanced species: 3 significant traits;
- more than 3 requires a formal readability exception and is excluded from generated contracts by default.

A trait with multiple state-gated outputs still counts as one trait only when the UI can explain it as one coherent rule.

## 6.3 Trait role categories

For composition validation, significant traits are tagged with roles:
- `SOURCE` — emits a channel/resource;
- `SINK` — consumes/mitigates a channel/resource;
- `SOCIAL` — soothes/alarms/symbiotic effect;
- `FEEDING` — producer/consumer relation;
- `LIFECYCLE` — growth/sleep/maturation timing;
- `REACTIVE` — state-entry pulse.

A normal species should not contain more than one trait of the same role unless the pair is state-exclusive and adds a clearly different decision.

## 6.4 Forbidden or restricted compositions

Reject by validator unless an explicit authored exception exists:

1. unconditional broad heat source + broad heat sink on the same organism when they mostly cancel;
2. unconditional alarm emitter + unconditional soother with identical range when net result is arithmetic noise;
3. spore shedder + strong contamination immunity + high-capacity filter feeder when the organism can generate and consume its own loop with no external dependency;
4. any combination that autonomously sustains infinite positive resource growth;
5. two reactive pulses that trigger each other recursively within the same tick;
6. universal multi-channel resistance together with a broad beneficial aura;
7. lifecycle rule requiring a future footprint that can never fit any legal hold in which the species may appear;
8. trait text requiring hidden target priorities not expressible by the supported selector grammar.

## 6.5 Synergy requirement for multi-trait species

A 2–3 trait species should satisfy at least one:
- one trait changes when another becomes active;
- the traits create a meaningful self-tradeoff;
- the combination makes the organism useful to some neighbors and dangerous to others;
- lifecycle changes which trait matters over time;
- the pair creates a routing/placement decision not present in either trait alone.

Simply stacking two unrelated bonuses is discouraged.

## 6.6 Body-plan foundation

Launch-oriented body-plan vocabulary is intentionally small:

### B01 Dot
Current footprint: 1 cell.
Purpose: simplest spatial actor; dense relationship puzzles.

### B02 Domino
Current footprint: 2 orthogonal cells.
Purpose: orientation and space blocking.

### B03 Corner
Current footprint: 3 cells in an L.
Purpose: irregular fit and directional adjacency.

### B04 Bar
Current footprint: 3 cells in a line.
Purpose: separation/bridge behavior and directional planning.

Additional body plans require proof that they create new decisions rather than just harder packing.

## 6.7 Footprint size ceiling

Normal launch species should occupy 1–3 cells at current stage and at most 4 cells at any later foundation growth stage.

Larger organisms are milestone content only and may not become the default difficulty lever.

## 6.8 Growth-stage ceiling

Foundation species have at most:
- starting stage + one growth transition for standard content;
- starting stage + two transitions only for rare authored advanced content.

Repeated open-ended growth is excluded.

## 6.9 Growth readability

If an organism can grow during a contract:
- next-stage footprint is inspectable before launch once the trait is documented;
- growth direction/orientation relationship is explicit;
- trigger condition is documented when known;
- the UI can overlay required future cells;
- no hidden alternate footprint selection occurs.

---

# 7. Formal contract predicate grammar

Contracts are data-defined Boolean requirements. They may not use arbitrary scripts for ordinary success/scoring logic.

## 7.1 Predicate tree

A contract requirement is an expression built from:
- `ALL(children...)`;
- `ANY(children...)`;
- `NOT(child)` only for simple atomic/event predicates;
- atomic predicates listed below.

Deep Boolean nesting should be limited for readability. Standard campaign objectives should normally fit in one sentence and use no more than two logical levels.

## 7.2 Entity selectors

Atomic predicates may target:
- `ORGANISM(instance_id)`;
- `SPECIES(species_id)`;
- `TAG(tag)`;
- `ALL_MANIFEST`;
- `ZONE(zone_id)`;
- `SUPPORT(support_id/type)`;
- `HOLD`.

Selectors resolving to multiple organisms define whether the predicate uses `ALL`, `ANY`, count, sum, min, or max explicitly.

## 7.3 Final-state atomics

Allowed foundation final-state predicates:
- `PRIMARY_STATE(selector) == state`;
- `HAS_FLAG(selector, flag) == bool`;
- `METER(selector, meter) comparator value`;
- `GROWTH_STAGE(selector) comparator stage`;
- `IN_ZONE(selector, zone_id)`;
- `AWAKE(selector)`;
- `SUPPORTS_USED(type/tag) comparator count`;
- `POWER_DRAW_INSTALLED comparator value`;
- `EMPTY_CELLS comparator value`;
- `ROUTE_COMPLETED == true`.

Comparators: `<`, `<=`, `==`, `>=`, `>` where the value domain supports it.

## 7.4 Timeline atomics

Allowed timeline predicates:
- `NEVER_ENTERED_STATE(selector, state)`;
- `NEVER_GAINED_FLAG(selector, flag)`;
- `EVENT_COUNT(event_type, selector/filter) comparator n`;
- `MAX_METER_SEEN(selector, meter) comparator value`;
- `MIN_METER_SEEN(selector, meter) comparator value`;
- `MAX_CHANNEL_SEEN(zone/cell/hold, channel) comparator value`;
- `TICKS_IN_STATE(selector, state) comparator n`;
- `GROWTH_BLOCK_COUNT(selector) comparator n`;
- `SUPPORT_ACTIVE_TICKS(type/id) comparator n`;
- `NO_EVENT(event_type, selector/filter)` as readable alias for count zero.

## 7.5 Forbidden-event objectives

A `forbidden event` is simply a timeline predicate such as:
- no panic entry;
- no contamination flag entry;
- no growth blocked;
- no support brownout;
- no organism critical;
- no named reactive pulse.

The UI must name the event before launch.

## 7.6 Mandatory vs optional requirements

Each contract contains:
- `mandatory[]` — all must pass for delivery success;
- `silver_objectives[]` — optional mastery criteria for Silver;
- `gold_objectives[]` — optional mastery criteria for Gold, evaluated in addition to Silver unless contract explicitly declares an alternative set.

Mandatory predicates should primarily protect contract delivery/welfare intent. Optional predicates shape strategy and replay.

## 7.7 Predicate design prohibitions

Do not use objectives that:
- depend on hidden rules the player could not know or intentionally discover;
- reward causing irreversible harm unless the fiction and product tone are deliberately changed later;
- require opaque weighted sums;
- punish number of retries in the campaign;
- punish time spent in planning;
- require pixel-perfect/manual speed;
- contradict another mandatory goal without explicitly presenting an alternative-objective choice.

## 7.8 Example contract expression

Mandatory:
- `ALL_MANIFEST: HAS_FLAG(CRITICAL) == false`;
- `METER(ORGANISM(C), contamination_load) <= delivery_limit`;
- `GROWTH_STAGE(ORGANISM(C)) >= MATURE`;
- `ROUTE_COMPLETED == true`.

Silver:
- `NEVER_ENTERED_STATE(ALL_MANIFEST, PANICKED)`.

Gold:
- `SUPPORTS_USED(powered) <= 1`;
- `GROWTH_BLOCK_COUNT(ALL_MANIFEST) == 0`.

This can be rendered in plain language without exposing predicate syntax to players.

---

# 8. Mechanical difficulty ladder

Difficulty increases by **relationship depth, temporal dependency, information pressure, and constrained mitigation**, not primarily by organism count.

## Tier 0 — Orientation

Purpose: teach interface and static facts.

Typical content:
- 2–3 organisms;
- one trait family;
- no hidden information;
- no route hazard;
- no support choice;
- very short transit.

A static-ish contract is permitted only here as tutorial scaffolding.

## Tier 1 — Single causal link

Purpose: prove that transit changes the answer.

Typical content:
- 3–4 organisms;
- one state transition;
- one beneficial or harmful relationship;
- one obvious future consequence;
- full trait information.

Player learns: initial adjacency is not final behavior.

## Tier 2 — Competing proximity

Purpose: force a real spatial tradeoff.

Typical content:
- 4–6 organisms;
- one reason to cluster + one reason to separate;
- two environmental/relationship families;
- optional support with simple cost.

Player learns: there is no universal spacing rule.

## Tier 3 — Temporal planning

Purpose: plan for changing footprint/state and route timing.

Typical content:
- 4–7 organisms;
- growth or sleep/wake;
- one known route hazard window;
- two-step causal chain;
- support power/space tradeoff.

Player learns: reserve future space and align behavior with timing.

## Tier 4 — Cascades and scarce mitigation

Purpose: combine familiar rules into 3–5 step causal stories.

Typical content:
- 5–8 organisms;
- 3 pressure families;
- two known route events;
- limited power/fixture/support allowance;
- meaningful Silver/Gold alternative pressure.

Player learns: protect the weak link, not every source independently.

## Tier 5 — Discovery contracts

Purpose: introduce bounded uncertainty without arbitrary failure.

Typical content:
- 4–7 organisms;
- one new/partially undocumented trait or uncertain route detail;
- forgiving mandatory welfare threshold;
- evidence-focused support option such as Monitor Beacon;
- successful observation permanently documents the rule.

Discovery tier must not require blind guessing for campaign progression.

## Tier 6 — Mastery recombination

Purpose: test model-building, not memorized recipes.

Typical content:
- 6–10 organisms, but often fewer;
- 3–4 pressure families;
- irregular hold;
- multiple state-gated traits;
- route timing/brownout interaction;
- strict but transparent optional objectives;
- no new fundamental rule required.

A Tier-6 contract is good when a veteran pauses because familiar rules interact in an unfamiliar way.

## 8.1 Difficulty prohibitions

Do not increase difficulty primarily by:
- hiding documented information;
- adding more tiny UI text;
- increasing organism count beyond readability;
- making thresholds arbitrary/noisy;
- shortening planning time;
- adding random transit outcomes;
- demanding exact arithmetic the UI could show;
- using one-off exceptions.

---

# 9. Scoring and medal model

## 9.1 Delivery success is binary

Mandatory predicates either pass or fail. There is no partial campaign completion hidden behind a score percentage.

## 9.2 Medal tiers

A successful contract grants at least **Bronze**.

- **Bronze** — all mandatory delivery predicates pass.
- **Silver** — Bronze + all contract `silver_objectives` pass.
- **Gold** — Silver + all contract `gold_objectives` pass.

A contract may omit Gold or Silver objectives only for early tutorials. Standard contracts should have one concise Silver theme and one concise Gold theme, where a theme may contain 1–2 closely related predicates.

## 9.3 No hidden weighted score in campaign

The standard campaign does not use a hidden formula combining stress, speed, supports, empty cells, and retries.

Reason: hidden weighted scoring pushes players toward unexplained optimization and can reward welfare-hostile behavior.

## 9.4 What optional objectives may reward

Good optional axes:
- welfare stability (`never panicked`, low total/final stress);
- contamination control;
- no blocked growth;
- support efficiency (`use <= N powered supports`);
- power efficiency;
- compactness/space efficiency when it does not cause harm;
- arrival state (`arrive awake`, `arrive mature`);
- constraint challenge (`no nest pad`, `no powered supports`);
- protecting a beneficial relationship throughout transit.

## 9.5 What scoring must not reward

Do not reward:
- organism death/criticality as an efficiency tactic;
- planning speed;
- fewer retries in campaign progression;
- fewer mouse moves;
- deliberate ignorance of causal review;
- sacrificing a low-value organism unless a future darker mode explicitly changes the product ethics and is separately designed.

## 9.6 Retry philosophy

Retries are unlimited for ordinary campaign contracts. The game records best medal achieved, not failure count as a punishment.

A separate challenge mode may record attempts/time for self-imposed competition only after the full product is stable; it is not required for design completion.

---

# 10. Information uncertainty and discovery

## 10.1 Two knowledge states

Mechanically relevant trait facts are either:
- **DOCUMENTED** — exact gameplay rule is available in the codex/inspection UI;
- **UNDOCUMENTED** — the player receives bounded cues but not the full rule.

Avoid a ladder of vague percentage-identification states unless later testing proves necessary.

## 10.2 What is never hidden

Even for an undocumented organism, always show:
- current footprint and orientation legality;
- current visible primary state;
- current visible condition flags;
- contract-critical welfare condition;
- whether the organism has an undocumented behavior slot;
- any immediate hard placement restriction;
- body growth possibility when physical size makes it contract-critical, though the exact trigger may be unknown in a discovery contract.

The game must never hide that a rule exists and then punish the player for not imagining it.

## 10.3 Discovery cues

An undocumented trait has 2–3 bounded clue channels chosen by content design:
- short observational sentence;
- icon/category hint (`social`, `thermal`, `feeding`, `reactive`, `lifecycle`);
- visible pre-launch behavior;
- shipping note from prior handlers;
- monitor reading category;
- known trigger but unknown magnitude, or known effect family but unknown trigger.

A discovery contract should usually hide **one relationship dimension**, not the entire trait.

## 10.4 Discovery safety rule

First exposure to a new undocumented trait in the main campaign must satisfy at least one:
- mandatory success is achievable under a conservative layout that the clues support;
- a failed first attempt cannot irreversibly cost progression/resources;
- the contract is explicitly an observation/training shipment whose Bronze condition is forgiving;
- the unknown effect becomes visible early enough that a retry is informed.

Blind 50/50 guessing is invalid content.

## 10.5 Documentation unlock

When an undocumented trait produces a clearly observable causal event during a completed/failed run, it may become documented if the observation uniquely identifies the rule family and trigger.

For authored milestone discovery, the contract may require a specific observation before documentation.

Once documented, the rule remains documented across the profile and generated mastery contracts may use it normally.

## 10.6 Unknown route information

Unknown route segments are rarer than unknown organism traits and must be bounded, e.g.:
- thermal surge will occur in one of two declared windows;
- exact contamination intensity unknown but marked low/medium/high range;
- brownout duration uncertain within a declared bounded interval.

However, authoritative transit remains deterministic per contract seed. The uncertainty is informational, not stochastic at runtime.

The base campaign should prefer exact known route timelines; uncertainty is a later-layer spice.

## 10.7 Monitor Beacon role

The Monitor Beacon may convert one bounded uncertain fact into exact evidence according to the contract. This makes information compete with mitigation without becoming an auto-solver.

---

# 11. Mechanical acceptance tests — primary states

Each state-family implementation must pass these tests before Phase 4 is considered mechanically stable.

## ST01 CALM -> AGITATED threshold
Given stress below `agitated_enter`, add a delta ending exactly at threshold. Result: AGITATED is queued according to transition timing; event log identifies the source delta.

## ST02 CALM -> PANICKED skip
Given one large same-tick stress delta from CALM to `>= panic_enter`, organism transitions directly to PANICKED at the next state boundary, not AGITATED for an artificial extra tick.

## ST03 AGITATED hysteresis
Stress falls below `agitated_enter` but remains above `agitated_exit`. Result: remains AGITATED.

## ST04 PANICKED hysteresis
Stress falls below `panic_enter` but remains above `panic_exit`. Result: remains PANICKED.

## ST05 PANICKED recovery to AGITATED
Stress becomes `<= panic_exit` but `> agitated_exit`. Result: AGITATED.

## ST06 PANICKED recovery to CALM
Stress becomes `<= agitated_exit`. Result: CALM.

## ST07 sleeping stress accumulation
ASLEEP organism receives stress and reaches wake threshold. Result: stays ASLEEP for current phase/tick, queues wake, wakes at legal boundary, derives awake state from current stress.

## ST08 simultaneous sleep/wake requests
Both requests resolve same boundary. Result: wake wins; log records precedence.

## ST09 condition orthogonality
A PANICKED organism crosses contamination threshold. Result: primary state remains PANICKED while CONTAMINATED becomes true; no state information is lost.

## ST10 critical orthogonality
An ASLEEP organism becomes CRITICAL through an allowed condition. Result: ASLEEP remains primary until wake rule; CRITICAL flag is independently visible/logged.

---

# 12. Mechanical acceptance tests — foundation traits

## T01 Heat Emitter
- active state produces exactly configured heat in source cells;
- inactive state produces zero;
- two emitters add commutatively regardless entity iteration order;
- state transition affects output only from the documented next phase/tick.

## T02 Heat Sink
- never removes more than capacity;
- never creates negative heat;
- target allocation is deterministic under equal exposures;
- two sinks cannot produce order-dependent results.

## T03 Alarm Emitter
- CALM output matches definition (normally zero/low);
- AGITATED/PANICKED outputs use correct state snapshot;
- same-tick panic transition does not retroactively emit panic-level field before legal boundary;
- source event can be traced to downstream stress intake.

## T04 Soother
- eligible targets only;
- capacity/target limit respected;
- tie-break deterministic;
- asleep/panicked gating respected;
- multiple soothers combine by additive/cap rules without ordering dependence.

## T05 Spore Shedder
- emits only under declared flag/stage condition;
- contamination persists/decays according to field rules after source stops;
- source cannot recursively re-trigger itself infinitely within a tick;
- output causality names state condition.

## T06 Filter Feeder
- consumes environmental contamination only up to available amount and capacity;
- satiety conversion exactly matches consumed amount/rule;
- competing consumers resolve deterministically;
- cannot consume negative contamination or duplicate the same units.

## T07 Grazer
- only compatible food edges eligible;
- source reserve/cost conserved;
- consumer demand capped;
- multiple consumers use declared stable allocation;
- no freeform movement occurs.

## T08 Growth Trigger
- counter increments only when trigger condition satisfied;
- reset/hold behavior is explicit when condition breaks;
- growth queues at correct boundary;
- legal future footprint succeeds;
- blocked footprint sets GROWTH_BLOCKED and never pushes/searches alternative space.

## T09 Symbiotic Buffer
- compatible target/tag required;
- range/adjacency rule exact;
- capacity target limit exact;
- effect applies only to declared channel/intake variable;
- cannot silently stack beyond defined cap.

## T10 Reactive Pulse
- fires once per eligible state-entry event;
- does not refire every tick while state persists;
- simultaneous state entries batch correctly;
- pulse event cannot retroactively cancel the state transition that triggered it;
- recursive pulse cycles are rejected or bounded by validator.

---

# 13. Mechanical acceptance tests — supports/resources

## SR01 Power capacity
Pre-launch installation above capacity is structurally invalid and launch blocked with exact reason.

## SR02 Brownout priority
Given installed draw above temporary route availability, powered supports are enabled in player-declared priority order and result is deterministic.

## SR03 Fixture exclusivity
Two utility supports cannot occupy one fixture.

## SR04 Cargo support occupancy
Baffle/feed cartridge blocks organism placement and future growth cells exactly like solid occupancy.

## SR05 Cooler capacity
Cooling cannot exceed local capacity; unavailable under brownout.

## SR06 Filter capacity
Environmental contamination removal cannot exceed capacity and does not directly delete organism contamination load.

## SR07 Baffle tradeoff
Stress transmission is reduced across declared boundary while a beneficial range effect crossing the same blocked relation follows its own explicit baffle interaction rule; no hidden exception.

## SR08 Nest capacity
Only one eligible organism receives benefit; incompatible organism produces clear pre-launch warning/invalid link.

## SR09 Feed reserve
Finite food units are conserved; empty cartridge provides no food but remains occupying space.

## SR10 Monitor information boundary
Beacon reveals only contract-declared evidence and never exposes a solved layout/full-future success prediction.

---

# 14. Mechanical acceptance tests — contracts and preview

## CP01 Structural validity vs predicted failure
A fully placed legal setup known to fail in simulation remains launchable.

## CP02 Illegal setup
Overlap/out-of-bounds/unplaced mandatory manifest disables launch and displays exact structural reason.

## CP03 Future growth warning
Known blocked future growth displays warning but does not disable launch.

## CP04 Current influence overlay
Overlay changes immediately after move/rotation and shows only documented direct current relationships.

## CP05 No future solver leak
Preview never reports a future state transition or success result not yet observed from a committed run.

## CP06 Deterministic retry
Retry from last launch reconstructs identical starting state and produces identical event log if unchanged.

## CP07 Predicate correctness
Every mandatory/Silver/Gold predicate evaluates from authoritative final/timeline data; UI text maps to exactly the same predicate.

## CP08 Medal monotonicity
Gold implies Silver implies Bronze. A failed mandatory predicate cannot produce a medal regardless optional performance.

## CP09 No retry penalty
Repeated failures do not reduce achievable campaign medal.

## CP10 Discovery transparency
Undocumented trait is visibly marked as containing unknown behavior; first observation generates causal evidence rather than an unexplained state change.

---

# 15. Content-combination validator rules

The content validator must reject or warn on mechanically legal but design-invalid combinations.

Hard reject:
- impossible current placement for mandatory manifest;
- no valid growth footprint for a required maturation objective across every legal initial placement;
- unsupported trait target selector;
- same-tick infinite trigger chain;
- power requirement impossible even with all allowed support configurations when powered support is mandatory;
- predicate referencing absent entity/trait/state;
- undocumented mandatory objective whose necessary fact cannot be inferred safely;
- mutually contradictory mandatory predicates;
- species violating hard trait-composition prohibitions.

Design warning / require authored approval:
- challenge has only one trivial static time-zero solution with no meaningful transit state change;
- more than 10 organisms in a normal hold;
- more than 3 significant traits on a species;
- more than 4 pressure families in a standard contract;
- causal summary requires more than ~5 major links to explain primary failure;
- all available supports are direct mitigation with no meaningful choice;
- Silver/Gold objective encourages worse organism welfare than Bronze;
- unknown trait causes immediate unavoidable mandatory failure on first exposure;
- one layout template solves a high fraction of generated siblings.

---

# 16. Phase-4 closure criteria after this appendix

The following Phase-4 areas are now **locked enough for implementation specification later**:
- pre-launch action legality;
- undo/reset/retry semantics;
- prediction/preview boundary;
- support resource constraints;
- foundation support roster;
- primary behavioral-state precedence;
- species/body-plan composition grammar;
- formal contract predicate grammar;
- mechanical difficulty ladder;
- medal/scoring principles;
- information uncertainty/discovery model;
- acceptance tests for state/trait/support/contract families.

Phase 4 is **not yet complete**. Remaining work should now be narrow and destructive rather than additive:

1. define the exact vertical-slice mechanical content set using the locked grammar;
2. run an adversarial mechanical review against self-sustaining loops, degenerate supports, unsolvable predicates, unreadable cascades, and one-template solutions;
3. produce several fully specified representative contracts from tutorial through mastery and paper-simulate them;
4. reconcile any contradictions across `GAME_BIBLE.md`, `MECHANICS.md`, and this file;
5. only then mark Phase 4 mechanically complete and move to Phase 5 content architecture.

No production code should begin before the later specification freeze.