# ORGANISM CARGO — PHASE 4 CLOSURE

Status: **CANONICAL — MECHANICAL ARCHITECTURE CLOSED**
Last updated: 2026-08-15

This file closes Phase 4 by forcing the canonical rules in `GAME_BIBLE.md`, `MECHANICS.md`, and `DECISION_ARCHITECTURE.md` through a representative vertical-slice content set, six complete contracts, two explicit paper simulations, and adversarial abuse tests.

The numeric values below are a **mechanical validation profile**, not final launch balance. They exist to prove that the architecture can generate readable, deterministic, non-degenerate play with finite integer values. Later balance passes may tune values while preserving the rules and relationships validated here.

---

# 1. Phase-4 closure criteria

Phase 4 is considered closed only if all are true:

1. the same global tick order can express every representative contract;
2. every contract contains a meaningful post-launch temporal consequence except the orientation tutorial;
3. every foundation support is sometimes useful and sometimes inferior;
4. no tested exploit becomes a universal solution;
5. every failure can be expressed through the existing causal log;
6. no representative contract requires a one-off rule outside the trait/support/hazard/predicate grammars;
7. Bronze/Silver/Gold do not reward intentional welfare degradation;
8. deterministic replay produces the same result from the same committed state;
9. the content grammar remains small enough to teach and implement;
10. no contradiction remains that blocks Phase 5 content design.

Result of this pass: **PASS**. Mechanical architecture may move to Phase 5.

---

# 2. Validation profile

## 2.1 Authoritative numeric domains

For paper validation:

- heat per cell: integer `0..20`;
- stress field per cell: integer `0..12`;
- contamination per cell: integer `0..20`;
- organism internal stress: integer `0..20`;
- contamination load: integer `0..20`;
- satiety: integer `0..12`;
- powered-support demand/capacity: integer units;
- transit length: normally `6..16` ticks in this slice.

No probability is used.

## 2.2 Validation propagation model

This profile intentionally uses simple arithmetic so the architecture can be inspected by hand.

### Heat
At Phase C sources add heat to source cells.
At Phase D each cell:
1. keeps its Phase-C value;
2. receives `floor(source_neighbor_heat / 4)` from each orthogonal neighbor using the Phase-C snapshot;
3. loses passive cooling `1`;
4. clamps `0..20`.

This is not locked as final balance math; the important architectural fact is snapshot-based local propagation.

### Stress field
Stress field is short-lived.
At Phase D:
- source cell keeps full source contribution;
- orthogonally adjacent cells receive `floor(source / 2)`;
- distance-2 cells receive nothing in the validation profile;
- all prior-tick field is discarded before the new field is built unless a future trait explicitly creates persistence.

### Contamination
Contamination persists.
At Phase D:
1. sources add to current cell contamination;
2. each cell gives `floor(value / 5)` to each orthogonal neighbor from the pre-propagation snapshot;
3. passive decay subtracts `1` only on vent ticks, otherwise `0`;
4. clamp `0..20`.

## 2.3 Meter intake

Unless a trait overrides it:

- heat exposure adds internal stress by `max(0, max_heat_on_occupied_cells - 6) / 2`, integer floor;
- stress-field exposure adds internal stress equal to `max_stress_field_on_occupied_cells`;
- contamination exposure adds contamination load `floor(max_contamination_on_occupied_cells / 3)`;
- baseline stress recovery while CALM and unexposed is `-1` per tick;
- baseline satiety metabolism for organisms tagged `METABOLIC` is `-1` every second tick, at ticks 2,4,6,...;
- all meters clamp to their domain.

These values are calibration scaffolding only.

## 2.4 Shared stress thresholds for the slice

Unless stated otherwise:

- `agitated_enter = 6`;
- `agitated_exit = 3`;
- `panic_enter = 11`;
- `panic_exit = 7`.

State transitions occur under the canonical hysteresis rules and default to next-tick start.

## 2.5 Shared contamination thresholds

Unless stated otherwise:

- `contaminated_enter = 8`;
- `contaminated_exit = 4`;
- ordinary mandatory delivery ceiling = `contamination_load <= 10`;
- critical contamination ceiling where used = `>= 16`.

---

# 3. Vertical-slice hold and fixture vocabulary

## HLD-A — Training Crate
- geometry: 5x5 all usable;
- utility fixtures: U1 at north-west edge, U2 at south-east edge;
- one bed fixture B1 center-left;
- power capacity: 3;
- zones: LEFT columns 1–2, CENTER column 3, RIGHT columns 4–5.

## HLD-B — Split Hold
- geometry: 6x5;
- blocked cells: (3,2), (3,4);
- utility fixtures: U1 left wall, U2 right wall;
- bed fixture B1 at (2,5);
- one baffle-compatible boundary between columns 3 and 4;
- power capacity: 4;
- zones: PORT columns 1–3, STARBOARD columns 4–6.

## HLD-C — Bent Hold
- geometry: 6x6 bounding box with unusable cells (5,1),(6,1),(6,2),(1,6),(2,6);
- utility fixtures U1 at (1,1), U2 at (6,6), U3 at (4,3);
- bed B1 at (2,4);
- power capacity: 4;
- zones: FORE rows 1–3, AFT rows 4–6.

These three geometries are sufficient to exercise orientation, future growth, local hazard zones, support competition, and template-break pressure without introducing a larger hold system.

---

# 4. Foundation support validation values

## S01 Cooler
- utility fixture;
- power draw 2;
- removes up to 4 heat/tick from cells at Manhattan distance <=1 from fixture;
- allocation: highest heat, then nearest, then cell coordinate order;
- no effect on stress/contamination.

## S02 Filter
- utility fixture;
- power draw 2;
- removes up to 4 contamination/tick from fixture cell + adjacent cells;
- same deterministic allocation principle;
- no direct reduction of organism contamination load.

## S03 Baffle
- cargo-cell/boundary support;
- power 0;
- blocks 75% of stress-field transmission across its declared boundary, integer floor after reduction;
- blocks directed rays if solid;
- occupies/claims its boundary footprint and may deny future growth adjacency.

## S04 Nest Pad
- bed support;
- power 0;
- one compatible linked organism;
- if stress <=7 for two consecutive ticks while on/linked to pad, queues ASLEEP next tick;
- sleeping organism stress-field intake modifier = 50%, integer floor;
- sleep ends on vibration hazard or stress >=10;
- awake-only beneficial traits are disabled while asleep.

## S05 Feed Cartridge
- cargo-cell support;
- power 0;
- capacity 6 food units;
- gives up to 2 food/tick to eligible adjacent consumers using lowest satiety then instance-ID tie-break;
- remains solid when empty.

## S06 Monitor Beacon
- utility fixture;
- power draw 1;
- no mitigation;
- contract specifies exactly what otherwise-bounded information it reveals;
- never supplies a success verdict or recommendation.

---

# 5. Vertical-slice organism compositions

The slice uses nine species definitions. No species uses bespoke simulation code.

## O01 Ember Pod
- body: Dot;
- traits: T01 Heat Emitter, T03 Alarm Emitter;
- heat: +3 while CALM/AGITATED, +4 while PANICKED;
- alarm: stress field +4 while AGITATED, +7 while PANICKED;
- metabolic: no;
- role: unstable source whose panic can cascade.

## O02 Hushling
- body: Dot;
- trait: T04 Soother;
- while CALM and awake, adjacent targets receive `-3 internal stress/tick`, capacity 1 target, highest stress then ID;
- while AGITATED/PANICKED/ASLEEP, soothing is off;
- role: narrow social stabilizer that can itself fail.

## O03 Silt Grazer
- body: Dot -> Domino on growth;
- traits: T06 Filter Feeder, T08 Growth Trigger;
- consumes up to 3 contamination/tick from occupied/adjacent cells, converting consumed 2 contamination -> +1 satiety;
- growth condition: satiety >=8 at end of two consecutive ticks;
- growth orientation follows facing; added cell is directly forward;
- on growth blocked: +3 stress and retry next tick while condition remains true;
- role: useful contamination sink whose success changes topology.

## O04 Spore Bell
- body: Dot;
- traits: T05 Spore Shedder, T10 Reactive Pulse;
- while CONTAMINATED emits +3 contamination on occupied cell/tick;
- when first becoming CONTAMINATED, one-time pulse +4 contamination on occupied cell;
- role: contamination cascade seed.

## O05 Warmback
- body: Domino;
- traits: T01 Heat Emitter, T09 Symbiotic Buffer;
- +2 heat on each occupied cell/tick;
- one adjacent tagged `FRAGILE` target receives 50% contamination intake, capacity 1;
- role: harmful thermal presence but useful narrow protection.

## O06 Cradle Moss
- body: Dot;
- traits: T04 Soother, T07 Grazer-compatible producer variant represented through the FEEDING grammar;
- while CALM/awake soothes one adjacent target by -2 stress;
- exposes 2 edible units/tick to compatible grazers; feeding does not harm Moss in this profile;
- while ASLEEP both effects are disabled;
- role: beneficial cluster anchor whose sleep can remove two benefits at once.

## O07 Pulse Mite
- body: Dot;
- traits: T03 Alarm Emitter, T10 Reactive Pulse;
- alarm as O01 but +3/+6;
- on entering PANICKED emits +5 heat once to occupied cell;
- role: converts stress cascade into thermal cascade.

## O08 Glass Larva
- body: Dot -> Corner on maturation;
- traits: T07 Grazer, T08 Growth Trigger;
- consumes compatible food up to 2/tick;
- growth when satiety >=9 for two ticks;
- mature footprint uses anchor + forward + right relative cells;
- on growth blocked: +2 stress, no arbitrary rotation;
- tagged FRAGILE;
- role: future-space planning.

## O09 Ash Sponge
- body: Domino;
- traits: T02 Heat Sink, T06 Filter Feeder;
- absorbs up to 3 heat/tick from occupied/adjacent cells, capacity shared;
- consumes up to 2 contamination/tick but gains no satiety;
- if total heat absorbed in a tick >=3, emits +2 stress field from its occupied cells next tick through an explicit scheduled reactive output;
- role: two-channel helper with a visible self-tradeoff; not universal because it can create stress.

Composition validator note: O09 is allowed because its two sinks do not create unconditional self-sustain, and heavy heat mitigation creates a new stress cost rather than a free broad aura.

---

# 6. Representative contract set

The six contracts map directly to the canonical difficulty ladder. Layout coordinates below describe one valid strategy, not the only valid solution.

## R1 — “Face Forward” — Orientation / Tier 0

### Hold / route
- HLD-A;
- 6 ticks;
- no hazards;
- no supports.

### Manifest
- O01 Ember Pod E1;
- O02 Hushling H1;
- O03 Silt Grazer G1, starting satiety 5, facing selectable.

### Mandatory
- route completed;
- no organism CRITICAL;
- G1 `GROWTH_BLOCK_COUNT == 0`.

### Silver
- H1 never AGITATED.

### Gold
- all mandatory + Silver;
- E1 final stress <=3.

### Pressure families
orientation + relationship.

### Intended learning
The player sees G1's documented future Domino cell. Orientation matters even before a hard growth contract appears.

### Valid strategy
Place H1 adjacent to E1; place G1 with its growth-forward cell empty. Because no contamination food exists, G1 does not grow in this tutorial, but the overlay teaches orientation without punishing the player.

### Plausible failure
Place E1 far from H1 and adjacent to another temporary stress demonstration source in the authored tutorial variant; E1 becomes AGITATED and H1 cannot help due to range.

R1 is the only allowed almost-static tutorial.

---

## R2 — “One Bad Neighbor” — Single Causal Link / Tier 1

### Hold / route
- HLD-A;
- 8 ticks;
- tick 3–4: thermal surge +3 heat in LEFT zone;
- supports: none.

### Manifest
- E1 O01 Ember Pod, stress 1;
- H1 O02 Hushling, stress 0;
- P1 O07 Pulse Mite, stress 2.

### Mandatory
- route complete;
- no CRITICAL;
- `NEVER_ENTERED_STATE(H1, PANICKED)`.

### Silver
- `NEVER_ENTERED_STATE(E1, PANICKED)`.

### Gold
- Silver + `NEVER_ENTERED_STATE(P1, PANICKED)`.

### Pressures
heat + social adjacency.

### Valid strategy
Keep E1 outside LEFT; put H1 adjacent to E1; keep P1 two cells away from E1 so a possible E1 alarm does not immediately push P1 over panic.

### Failure cascade
E1 placed in LEFT -> surge increases E1 stress -> E1 becomes AGITATED -> next tick Alarm raises neighboring stress -> P1 panics -> P1 heat pulse raises local heat -> H1 becomes AGITATED and its soothing turns off -> E1 escalates.

The player learns a single clear temporal chain: route hazard -> mood change -> next-tick trait activation.

---

## R3 — “Useful Dirt” — Competing Proximity / Tier 2

### Hold / route
- HLD-A;
- 10 ticks;
- tick 4–6 contamination leak +3/tick at RIGHT edge cell (5,3);
- support allowance: choose **one** of Filter or Baffle;
- power capacity 3.

### Manifest
- G1 O03 Silt Grazer, satiety 4;
- B1 O04 Spore Bell, contamination load 4;
- M1 O06 Cradle Moss;
- E1 O01 Ember Pod.

### Mandatory
- no CRITICAL;
- B1 contamination load <=10 at arrival;
- G1 growth block count ==0.

### Silver
- no organism PANICKED.

### Gold
- Silver + no powered support used.

### Pressures
contamination + feeding/growth + beneficial/harmful proximity + support choice.

### Valid strategy A
No powered support: place G1 near leak/B1 so it consumes contamination, but face its future growth into reserved space; place Moss adjacent to E1; leave enough distance that B1's contamination pulse cannot immediately bathe Moss.

### Valid strategy B
Use Filter near leak, allowing G1 farther from B1 and reducing growth timing pressure, but forfeiting Gold.

### Failure cascade
G1 placed beside B1 but growth-forward cell occupied by Moss -> contamination feeds G1 -> satiety reaches growth trigger -> growth blocks -> +3 stress repeatedly -> G1 becomes AGITATED/PANICKED -> layout loses welfare medal even though contamination control was initially correct.

This contract proves that a helpful relationship can create a future spatial hazard.

---

## R4 — “Wake Window” — Temporal Planning / Tier 3

### Hold / route
- HLD-B;
- 12 ticks;
- tick 5: vibration burst, hold-wide, +3 stress field and wakes ASLEEP;
- tick 8–9: thermal surge +3 in STARBOARD;
- support allowance: Nest Pad + one of Cooler or Feed Cartridge.

### Manifest
- M1 O06 Cradle Moss;
- L1 O08 Glass Larva, satiety 5;
- E1 O01 Ember Pod;
- H1 O02 Hushling;
- W1 O05 Warmback.

### Mandatory
- no CRITICAL;
- L1 must be MATURE at arrival;
- M1 must be AWAKE at arrival;
- L1 no growth block.

### Silver
- E1 never PANICKED.

### Gold
- Silver + use no powered support.

### Pressures
sleep/wake timing + feeding/growth + heat + support opportunity cost.

### Valid strategy
Put M1 adjacent to L1 so food drives maturation; reserve L1 Corner footprint. Use Nest Pad on E1 or H1 only if needed, not M1, because sleeping M1 disables food production. If choosing Feed Cartridge, it can replace risky Moss adjacency and earn Gold because it is unpowered; if choosing Cooler, the STARBOARD surge is easier but Gold is impossible.

### Failure cascade
Player sleeps M1 early to reduce social stress -> its food production turns off -> L1 fails to reach satiety threshold before arrival. The support improved local calm but invalidated the lifecycle objective.

This proves that sleep is not a universal safety button.

---

## R5 — “Brownout Chain” — Cascades & Scarce Mitigation / Tier 4

### Hold / route
- HLD-C;
- 14 ticks;
- tick 4–5 contamination leak +4 at AFT-right zone;
- tick 7–8 power brownout: available power drops from 4 to 2;
- tick 9 thermal surge +4 FORE;
- tick 11 vibration burst +3 stress field, wakes sleepers;
- supports supplied: Cooler, Filter, Baffle, Nest Pad; choose at most 3 by allowance; installed power demand still <=4 pre-launch.

### Manifest
- E1 O01 Ember Pod, stress 2;
- P1 O07 Pulse Mite, stress 2;
- B1 O04 Spore Bell, contamination load 5;
- G1 O03 Silt Grazer, satiety 4;
- W1 O05 Warmback;
- M1 O06 Cradle Moss;
- H1 O02 Hushling.

### Mandatory
- all organisms not CRITICAL;
- B1 contamination load <=10;
- G1 no growth block;
- route complete.

### Silver
- no organism PANICKED;
- no support brownout event affecting Filter.

### Gold
- Silver + supports used <=2.

### Pressures
all three channels + growth + brownout priority + support scarcity.

### Known valid strategy
Install Filter at AFT-right and Cooler FORE. Set **Filter priority 1, Cooler priority 2** so brownout leaves Filter active and Cooler off during ticks 7–8. Put B1/G1 in AFT with G1 facing reserved growth cell; put E1 near H1/M1 in CENTER/FORE but outside the thermal surge core; keep P1 separated by the blocked geometry. The Cooler is not essential during the brownout window because the large heat event is tick 9 after power returns.

Alternative Gold strategy: Filter + Baffle only, using H1/M1 placement to absorb heat/stress rather than Cooler.

### Plausible failure cascade
Player prioritizes Cooler above Filter -> brownout tick 7 disables Filter -> residual contamination from leak remains near B1 -> B1 crosses contaminated threshold -> reactive contamination pulse -> G1 absorbs more contamination and feeds/grows earlier than expected -> if future cell occupied, growth blocks -> stress rises -> G1/P1 become AGITATED -> P1 panic pulse adds heat -> tick 9 thermal surge stacks -> H1 becomes AGITATED and stops soothing -> E1 panics.

This is the primary Phase-4 causal-chain contract.

---

## R6 — “No Familiar Template” — Mastery Recombination / Tier 6

### Hold / route
- HLD-C rotated/mirrored authored variant with one utility fixture removed, still using the same hold grammar;
- 16 ticks;
- tick 3–4 vent cycle (extra contamination decay -2 and heat decay -2);
- tick 6 zone isolation blocks stress-field transmission between FORE and AFT;
- tick 9–10 thermal surge +3 AFT;
- tick 11–12 brownout available power 2;
- tick 13 vibration burst;
- support allowance: choose exactly 2 among Cooler, Filter, Baffle, Nest Pad, Feed Cartridge, Monitor Beacon;
- uncertain route detail: thermal surge intensity is documented as `+2..+4`; Monitor Beacon reveals exact +3 before launch.

### Manifest
- A1 O09 Ash Sponge;
- E1 O01 Ember Pod;
- P1 O07 Pulse Mite;
- L1 O08 Glass Larva, satiety 4;
- M1 O06 Cradle Moss;
- W1 O05 Warmback;
- B1 O04 Spore Bell, contamination load 3;
- G1 O03 Silt Grazer, satiety 3.

### Mandatory
- no CRITICAL;
- L1 mature at arrival;
- B1 contamination load <=10;
- G1 no growth block;
- route complete.

### Silver
- no PANICKED states;
- no organism contamination load >12 at any tick.

### Gold
- Silver + no powered mitigation support (Cooler/Filter) used; Monitor Beacon is allowed because it is informational.

### Pressures
heat/contamination/stress + two growth footprints + route timing + isolation + brownout + bounded uncertainty + support choice.

### Known valid strategy family
Use Feed Cartridge + Baffle for Gold: Cartridge feeds L1 while Moss can be positioned to soothe/serve as backup food outside the highest hazard area; Baffle limits E1/P1 stress coupling but must not cut Moss off from its intended target. Put A1 near AFT heat sources to absorb heat, but not adjacent to P1 because A1's heavy-absorption scheduled stress output can push P1 toward panic. Put G1 near B1 only if its future Domino cell remains reserved. Warmback protects B1 or L1 from contamination but creates extra heat, so place it near A1's thermal sink region rather than beside E1.

Non-Gold information strategy: Monitor Beacon + Feed Cartridge reveals thermal intensity and stabilizes L1 growth, sacrificing direct mitigation but reducing uncertainty.

### Plausible failure cascade
A1 placed centrally as a supposed universal buffer -> absorbs >=3 heat during thermal surge -> schedules stress output -> P1 receives that stress and panics -> P1 heat pulse increases local heat -> A1 absorbs even more heat next tick and schedules another stress output -> E1 becomes AGITATED and adds alarm stress -> apparent “buffer cluster” becomes an amplifier. This specifically kills the universal-buffer template.

---

# 7. Paper simulation A — R5 Brownout Chain

This paper run focuses on the canonical Phase A→I order and one failure branch. It is intentionally not a full cell-by-cell spreadsheet; it follows all state-changing events required to validate phase semantics.

## 7.1 Committed failing setup

- Filter and Cooler installed; demand 4, capacity 4.
- **wrong priority:** Cooler priority 1, Filter priority 2.
- B1 at AFT-right near leak.
- G1 adjacent to B1, facing an occupied future-growth cell.
- P1 within stress-field adjacency of G1.
- E1 adjacent to H1; H1 currently CALM.

Starting key values:
- B1 contamination load 5;
- G1 satiety 4, stress 1;
- P1 stress 2;
- E1 stress 2;
- H1 stress 0.

### Tick 4 — contamination leak begins

**A Route:** leak becomes active AFT-right, +4 contamination source. Power 4.

**B Start transitions:** none.

**C Generation:** leak +4. No B1 spore output because B1 is not yet CONTAMINATED.

**D Propagation:** contamination field builds around leak; Filter is powered and removes contamination in its later defined support action within the channel-resolution contract. Exposure near B1 is reduced but nonzero.

**E Exposure/interactions:** B1 and G1 sample contamination. G1's Filter Feeder also consumes local contamination, producing satiety gain if enough is consumed.

**F Meters:** B1 load rises moderately; G1 satiety rises.

**G Thresholds:** no contamination state transition yet; G1 has not satisfied two consecutive growth ticks.

**H Consequences/log:** records leak -> local contamination -> B1/G1 intake and G1 feeding.

**I:** continue.

### Tick 5 — second leak tick

Same ordering. B1 load approaches contaminated threshold; G1 reaches first qualifying `satiety >=8` end-tick if allocation is favorable. Growth trigger stores consecutive-condition count = 1.

### Tick 6 — leak ends, residual contamination persists

**A:** leak inactive. Power normal.

**C/D:** no new route contamination, but field persists. Filter reduces residual field.

**E/F:** G1 consumes remaining contamination and reaches second qualifying satiety tick.

**G:** G1 queues growth for next tick start.

**H:** causal log records `growth_condition_met` parented to prior contamination-consumption events.

### Tick 7 — brownout begins; growth collides

**A Route:** available power becomes 2. Priority allocation powers Cooler (2) and turns Filter OFF. Log: `BROWNOUT -> FILTER_OFF`.

**B Start transitions:** G1 executes queued growth. Future Domino cell is occupied, so growth fails. Set `GROWTH_BLOCKED`, +3 stress consequence according to O03. The architecture does not search another direction.

**C Generation:** residual contamination remains; Filter is off. If B1 crossed CONTAMINATED on prior F/G threshold, B1 now emits +3 contamination. If it crosses this tick instead, emission begins next tick under snapshot semantics.

**D Propagation:** contamination persists/spreads without powered filtering.

**E:** G1 consumes some, but capacity cannot erase the whole region; B1 and G1 take exposure.

**F:** B1 load rises; G1 satiety remains high; G1 stress receives exposure + growth-block consequences as specified.

**G:** if B1 load >=8, queue/set CONTAMINATED according to condition timing. G1 may enter AGITATED once stress >=6.

**H:** if B1 newly enters CONTAMINATED, its T10 pulse emits +4 contamination as a same-boundary reactive event for later-state accounting without retroactively changing Phase E exposure. Causal parents: brownout -> filter off -> contamination persistence -> B1 threshold -> pulse.

### Tick 8 — second brownout tick, cascade expands

**A:** Cooler remains powered, Filter off.

**B:** G1 remains/enters AGITATED from prior threshold. Growth retries because condition remains true; future cell is still occupied -> another growth-block event +3 stress.

**C:** B1 now emits +3 contamination because CONTAMINATED. Any pulse residue is present according to contamination persistence rules.

**D:** field expands.

**E:** P1 receives stress-field exposure if G1/nearby alarms are active; G1 consumes contamination but cannot fully compensate.

**F/G:** G1 can cross panic threshold; P1 can cross agitation depending exact adjacency field.

**H:** records all threshold entries independently. Same-tick threshold crossings cannot cancel one another.

### Tick 9 — power restored + thermal surge

**A:** power 4; Filter returns ON; FORE thermal surge +4 activates.

**B:** any queued PANICKED state for G1/P1 becomes active now.

**C:** P1 if PANICKED emits alarm through T03; E1 emits based on own state; thermal hazard contributes heat.

**D:** heat and stress fields propagate independently.

**E/F:** nearby organisms intake heat/stress. Filter can now reduce contamination, but cannot remove accumulated internal contamination load or undo prior stress.

**G:** H1 may cross AGITATED. If so, soothing will switch off next tick.

**H:** P1 entering PANICKED triggers its one-time +5 heat pulse. That pulse is logged with parent chain back through growth block / alarm exposure.

### Tick 10 onward

The exact values depend on positions, but architecture has already demonstrated the intended failure topology:

`wrong brownout priority`
→ `Filter off`
→ `persistent contamination`
→ `Spore Bell contaminated/pulse`
→ `Grazer accelerated feeding + blocked growth`
→ `stress escalation`
→ `Pulse Mite panic`
→ `heat pulse`
→ `later surge stacking`
→ `Hushling agitation / soothing loss`
→ possible Ember panic.

No step required random resolution, autonomous movement, same-tick recursive triggering, or hidden ordering.

## 7.2 Corrected retry

Single hypothesis-driven revision:
- set Filter priority 1, Cooler priority 2;
- reserve G1's future growth cell.

Expected consequences:
- Filter stays active ticks 7–8;
- contamination field remains bounded;
- B1 may never cross CONTAMINATED;
- G1 either grows cleanly or grows later without repeated block stress;
- P1 does not receive the downstream stress escalation;
- Cooler being off during brownout is acceptable because the major thermal surge starts after power returns.

This retry validates that the failure teaches a precise corrective model rather than demanding arbitrary rearrangement.

---

# 8. Paper simulation B — R6 No Familiar Template

This run validates scheduled secondary effects, route isolation, uncertainty, and why the two-channel Ash Sponge is not a universal answer.

## 8.1 Failing “buffer cluster” setup

- supports: Feed Cartridge + Monitor Beacon;
- Beacon reveals thermal surge = exactly +3;
- A1 Ash Sponge placed centrally adjacent to P1 Pulse Mite and E1 Ember Pod;
- M1 Cradle Moss adjacent to L1 Glass Larva;
- G1 near B1 with free growth-forward cell;
- W1 near B1 to reduce contamination intake.

### Ticks 1–2
Low pressure. L1 feeds from M1; G1 has limited contamination food. All remain CALM.

### Ticks 3–4 — vent cycle

**A:** vent event active.

**D:** extra heat and contamination decay applies after propagation. This is beneficial for contamination control but slightly reduces environmental food available to G1.

Consequence: G1 growth is delayed. This is acceptable because its maturation is not mandatory in R6; the system demonstrates that a nominally beneficial vent can alter timing.

### Tick 6 — zone isolation

**A:** isolation boundary becomes active.

**D:** stress-field transmission across FORE/AFT boundary is blocked/reduced according to route definition.

This temporarily protects one cluster but can also prevent Moss/Hushling-style benefits if they were across the boundary. No geometry moves.

### Ticks 9–10 — thermal surge AFT

A1 is positioned to overlap the hot region.

**C/D:** hazard raises heat; A1 Heat Sink consumes up to 3 heat/tick.

Because A1 absorbs >=3, its explicit trait schedules +2 stress-field output for the following tick. This is not an immediate recursive pulse.

**E/F:** A1 mitigates heat successfully; neighboring P1 receives less direct heat than it otherwise would.

**H:** log records `ASH_SPONGE_HEAT_ABSORB >=3 -> schedule stress output tick+1`.

### Tick 10 / 11 boundary

Scheduled A1 stress output becomes active in the correct later phase/tick. P1 and E1 are adjacent to A1, so they receive the field.

P1's stress rises toward AGITATED/PANICKED. E1 may become AGITATED, which activates its alarm on the next tick.

### Ticks 11–12 — brownout

Available power 2. Beacon is the only powered support in this setup (draw 1), so it remains active and the brownout itself causes no mitigation failure. This demonstrates that informational support can survive a route event without becoming a raw safety tool.

P1, however, is now near the panic threshold because A1 converted earlier heat mitigation into delayed social pressure.

### Tick 12

If P1 crosses `panic_enter`, PANICKED is queued for next tick start. E1 may also be AGITATED, adding alarm pressure.

### Tick 13 — vibration burst

**A:** vibration adds +3 stress field and wakes sleepers.

**B:** P1's queued PANICKED becomes active before later phases.

**C:** P1 now emits its panic alarm; E1 may emit alarm if AGITATED/PANICKED.

**D/E/F:** vibration + alarms stack through the canonical additive exposure path.

**H:** P1's first PANICKED entry fires one-time +5 heat pulse. A1 may absorb some heat on subsequent tick, which can again satisfy its delayed stress-output condition.

The cluster intended as a “safe center” has become an amplifier:

`thermal surge`
→ `A1 absorbs heat`
→ `A1 schedules stress`
→ `P1 stress increases`
→ `P1 panics`
→ `P1 heat pulse`
→ `A1 absorbs again`
→ `new delayed stress pressure`.

The loop is **not infinite inside one tick** because A1's stress output is scheduled and P1's panic pulse is one-time per state entry. Hysteresis prevents repeated panic-entry pulses unless the organism genuinely exits and later re-enters PANICKED.

## 8.2 Corrected family

Move A1 away from P1/E1 and place it near Warmback / AFT thermal load. Use the Baffle or spacing to separate A1's delayed stress output from sensitive alarm species. Keep food support near L1. This preserves A1's heat value while externalizing its downside into space/relationship planning.

This validates O09 as a legitimate two-channel helper rather than a universal buffer.

---

# 9. Adversarial exploit review

## 9.1 Self-sustaining food/filter loop

Attack: place Spore Bell next to Silt Grazer so B1 creates contamination, G1 consumes it for satiety, then maturation/traits create more contamination indefinitely.

Result: **blocked by architecture + composition rules**.
- B1 only sheds while contaminated; contamination is a hazard to B1 and can violate delivery limits.
- G1 converts finite environmental contamination to finite satiety; it does not emit contamination.
- growth is bounded to declared stages.
- no organism in the slice creates an unlimited food->contamination->food positive loop.
- generator rejects autonomous infinite positive-resource cycles.

Design rule carried forward: any future producer/consumer cycle must have at least one external finite input, welfare cost, capacity ceiling, or irreversible stage cap.

## 9.2 Stress-soothing cancellation loop

Attack: stack Hushlings/Cradle Moss around alarm organisms so all stress arithmetic cancels forever.

Result: **not universal**.
- Soothers have capacity 1 and target priority.
- they disable while AGITATED/PANICKED/ASLEEP.
- spatial adjacency consumed by soothers competes with feeding, growth room, and isolation.
- route vibration/heat can destabilize the soother itself.
- advanced manifests can contain multiple stress-sensitive targets exceeding total soothing capacity.

Hard reject for future content: never create an unconditional multi-target soother with range >= alarm range and no state gate.

## 9.3 Contamination farming

Attack: intentionally contaminate a Filter Feeder to accelerate satiety/growth and exploit contamination as free food.

Result: **allowed as a strategic tradeoff, not an exploit**, provided the contamination creates real risk.
- contamination can push source/consumer over delivery limits;
- growth changes footprint and may create spatial stress;
- optional medals can reward contamination control;
- vent/filter supports can reduce available “food,” creating route-dependent timing.

This is exactly the kind of useful-dangerous relationship the game wants. It becomes an exploit only if contamination has no meaningful downside. Future species validation must enforce a downside or contract conflict.

## 9.4 Power-priority exploit

Attack: install every powered support and reorder priorities to make brownouts trivial.

Result: **contained**.
- pre-launch installed demand cannot exceed normal capacity;
- contract allowance and fixture count cap installed supports;
- brownout power allocation means only some remain active;
- the player can optimize priority, but that is intended skill;
- hazards are timed so the “correct” priority may depend on which event is currently dangerous.

Future route design rule: avoid brownouts that have one globally correct support priority independent of manifest and hazard timing.

## 9.5 Growth-block abuse

Attack: deliberately block growth to keep an organism small and avoid bad adjacency while still receiving its pre-growth benefits.

Result: **partially legitimate but bounded**.
- growth-block carries stress and/or maturation failure as species-defined consequence;
- contracts can require maturation or zero growth blocks;
- blocked growth does not grant a generic benefit other than retaining footprint;
- repeated growth attempts can escalate stress.

Important design principle: some optional mastery solutions may intentionally delay/deny growth, but mandatory rules must never accidentally reward welfare degradation. If an organism can safely remain juvenile forever, that must be a documented viable biological state, not a loophole.

## 9.6 Infinite / recursive state pulses

Attack: A pulse triggers B panic; B pulse triggers A contamination; A pulse re-triggers B inside same tick.

Result: **architecturally blocked**.
- state entries use snapshot thresholds;
- state-entry effects execute in Phase H as a batch;
- they cannot retroactively change Phase-G threshold decisions;
- one-time transition pulses require actual state entry;
- content validator rejects same-tick recursive transition loops;
- scheduled delayed pulses cannot execute unboundedly because timers advance by ticks and lifecycle/event counts are finite.

## 9.7 Isolate-all

Attack: maximize spacing and baffles so harmful interactions never happen.

Result: **fails across representative set**.
- compact holds and mandatory manifests limit empty buffers;
- feeding, soothing, filtering, and symbiosis reward proximity;
- growth reserves consume space;
- Baffles can remove beneficial relationships;
- some Gold routes require low support use/compact solutions.

No additional global anti-isolation rule is needed.

## 9.8 Universal buffer species

Attack: always place Ash Sponge centrally.

Result: **explicitly killed in R6**.
- its heat/contamination mitigation is capacity-limited;
- heavy heat absorption schedules stress output;
- central placement can destabilize alarm species;
- Domino footprint consumes valuable adjacency/space.

Any future two-channel helper must carry an equally legible downside or narrow capacity.

## 9.9 Template reuse

Attack: solve every contract with “soother in center, hazards at edges, growth outward.”

Result: **broken by the contract family**.
- hazards target different zones/times;
- irregular holds change valuable cells;
- future growth directions differ;
- Baffles/zone isolation change social connectivity;
- mandatory lifecycle goals sometimes require clustering;
- brownout and support allowance alter the best mitigation;
- R6 punishes central buffering.

Phase-5 generation validator must track solution-feature diversity. If one topology solves a large share of generated candidates, reject/retune those candidates rather than adding random noise.

## 9.10 Brute-force retries

Attack: blindly try arrangements until one passes.

Result: **possible in principle, but not structurally rewarded**.
- retries are intentionally free because failure is educational;
- deterministic causal review makes informed revision faster than blind search;
- board/manifest combinatorics become large quickly;
- medals add transparent secondary constraints;
- no campaign reward exists for fewer retries, so the game does not shame experimentation.

The design does not attempt to prohibit brute force; it makes understanding the efficient path.

---

# 10. Foundation support dominance matrix

Every support must have at least one representative case where it is useful and one where it is inferior.

| Support | Clearly useful | Clearly inferior / costly |
|---|---|---|
| Cooler | R4/R5 thermal surge when social layout cannot absorb heat safely | R3 where contamination is the real constraint; powered use also loses Gold |
| Filter | R3/R5 contamination leak / Spore Bell management | R4 where growth/feeding and timing dominate; no contamination hazard |
| Baffle | R5/R6 to break stress cascades / buffer scheduled stress output | R3 when it blocks Grazer/Spore or Moss relationships and consumes future space |
| Nest Pad | R4 for targeted stabilization when its target may safely sleep | R4 on Cradle Moss specifically, where sleep disables food/soothing and can prevent Larva maturation |
| Feed Cartridge | R4/R6 to decouple growth from risky producer adjacency | R5 where contamination/power is the weak link and cargo-cell cost worsens growth spacing |
| Monitor Beacon | R6 where bounded hazard intensity is uncertain and information has strategic value | R1–R5 with fully known rules, where it consumes fixture/power/allowance without mitigation |

No support is a default auto-pick across the representative suite.

---

# 11. Medal ethics / welfare audit

The six contracts were checked against the rule that better medals must not encourage worse organism welfare.

Findings:
- Gold may require fewer powered supports, but never requires an organism to panic, contaminate, starve, or become critical.
- A low-support Gold route must still pass all mandatory welfare predicates.
- Growth-block count is never rewarded positively.
- Intentional contamination farming can be a tactic, but optional medals cap contamination rather than reward higher contamination.
- Planning time and retries do not affect medals.
- No medal rewards maximum heat/stress exposure as “efficiency.”
- Sleep is never rewarded merely for keeping organisms unconscious; where sleep is useful, arrival-state requirements or disabled beneficial traits create context.

Conclusion: current medal grammar is mechanically and tonally compatible with the product thesis.

---

# 12. Contradiction reconciliation

## 12.1 Support “contract budget” wording in MECHANICS.md

`MECHANICS.md` section 12 uses older wording saying supports may occupy “contract budget.” `DECISION_ARCHITECTURE.md` later and more specifically locks the resource as **contract support allowance, not money/currency**.

Canonical interpretation: “contract budget” in the older mechanics prose means the non-monetary support allowance. No persistent or per-contract money resource exists in the Phase-4 foundation.

A later cleanup pass may rename the older phrase, but there is no unresolved design contradiction.

## 12.2 Support phase placement

The global phase order is retained. Support channel mitigation must be implemented at the documented channel/effect phase appropriate to the support, using snapshots and deterministic capacities. This closure does not create a new global phase. Cooler/Filter behavior is part of environmental channel resolution; Nest/Feed/Baffle effects enter their relevant existing phases.

## 12.3 Immediate vs next-tick state entry

The canonical behavioral default remains `next_tick_start`. A trait can create a Phase-H reactive event on the threshold boundary only when its definition explicitly says so; that event cannot retroactively change Phase-E/F values. The R5/R6 simulations were written to preserve this rule.

## 12.4 Environmental formulas

The numeric propagation equations in this closure are a validation profile, not a replacement for the architecture statement that exact rates are balance variables. Phase 7/8 may tune formulas, but must preserve local, deterministic, snapshot-based resolution and causal explainability.

No other blocking contradiction was found.

---

# 13. Phase-4 mechanical acceptance results

### Tick model
PASS — six contracts fit A→I ordering; advanced simulations require no reordering.

### Determinism
PASS — all target selection and transitions use fixed selectors, phase boundaries, or declared schedules.

### Explainability
PASS — both advanced failure chains can be represented as parented causal events.

### Spatial consequence
PASS — growth, body orientation, baffles, fixture topology, and support cell costs materially alter layouts.

### Temporal consequence
PASS — Tier 1+ contracts cannot be solved purely from time-zero shape fit.

### State machine
PASS — CALM/AGITATED/PANICKED/ASLEEP plus orthogonal flags are sufficient for the representative set.

### Trait grammar
PASS — nine species and six contracts use the ten foundation families without bespoke code.

### Support grammar
PASS — all six supports have distinct roles and explicit inferior cases.

### Anti-dominance
PASS — isolate-all, sedate-all, universal buffer, power, growth, recursive pulse, and template attacks remain bounded.

### Contract predicates
PASS — all mandatory/Silver/Gold goals fit the existing Boolean predicate grammar.

### Welfare incentives
PASS — no medal requires worse welfare.

### Scope
PASS — one hold, discrete cells, 6–16 ticks, <10 organisms, reusable body/trait modules remain sufficient.

---

# 14. Mechanical architecture freeze

Mechanical architecture is now **complete for purposes of moving forward**.

The following are frozen unless a later whole-game/adversarial pass finds a contradiction:

- deterministic discrete transit;
- authoritative A→I tick order;
- three environmental channels only at foundation;
- three internal meters (stress, contamination load, satiety);
- four exclusive primary behavior states + orthogonal condition flags;
- bounded growth stages with predeclared footprints and no pushing;
- ten foundation trait families;
- six foundation supports;
- free reversible planning followed by hard commit;
- no future solver preview;
- power + fixture/space + support allowance resource model;
- contract predicate grammar;
- Bronze/Silver/Gold structure;
- deterministic route hazards;
- causal event log requirement;
- difficulty growth through interactions/timing rather than count/noise;
- no generic money layer inside contracts;
- no universal all-channel mitigation;
- no arbitrary organism movement during transit.

Phase 5 may add content definitions only by composing these systems. If Phase 5 discovers a content need that requires a new mechanical family, it must be treated as a formal architecture change and re-run the relevant closure tests rather than silently expanding scope.

---

# 15. NEXT PHASE HANDOFF

Proceed to **Phase 5 — Content Architecture**.

Phase 5 should define, in implementation-ready data terms:

1. launch-target counts for species, body plans, traits, holds, route hazards, supports, contracts, tutorial/milestone content, and cosmetic/flavor variants;
2. a canonical launch species roster built only from the locked grammar;
3. trait numeric parameter bands and readability templates;
4. hold families and fixture/zone grammar;
5. route families and hazard sequencing grammar;
6. campaign structure and content unlock order;
7. authored vs generated contract split;
8. generation validation rules, including solvability and anti-template diversity checks;
9. discovery/documentation content plan for undocumented traits;
10. narrative framing sufficient to make manifests memorable without large dialogue burden;
11. content naming/tone conventions;
12. minimum demo content set vs launch content set;
13. data fields required for every content family;
14. explicit out-of-scope content so Phase 5 does not reopen creature collection, breeding, ship exploration, combat, or open world.

Mechanical architecture should not be expanded during Phase 5 unless content proves a specific locked rule impossible.