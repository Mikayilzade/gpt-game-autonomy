# GAME #006 — CONCEPT TOURNAMENT — RUN 1

Last updated: 2026-08-29
Factory run: **2**
Phase: **2 — Concept Tournament / destructive pass**
Final concept selected: **NO**
Production implementation started: **NO**

This run executes the uniform destructive tournament defined by `STATUS.md` across all ten Phase-1 survivors. The purpose is to kill attractive but shallow, derivative, UI-heavy or production-disproportionate concepts before Product Thesis.

Fresh refined-mechanic checks on 2026-08-29 reinforced several constraints:
- `Stringate` (2026) and the broader Portal lineage confirm that generic portals/moving portals are occupied; Stitchspace survives only if seam topology, orientation and room-boundary rewiring are mechanically central rather than portal dressing.
- `Gear Combination`, `Cogs`, `Crazy Machines` and factory/gear games validate mechanical puzzle demand but make plain gear-routing visually generic. Common Shaft survives only if *shared forced synchronization and collateral coupling* is the repeated verb.
- `Short Circuit VR`, `Lighton`, `Puzzle Light: Rotate` and other electronics titles confirm that ordinary circuit construction/fault avoidance is crowded. The Short Circuit must make deliberate bounded failure states the product, not wire routing.
- falling-sand/thermal sandboxes such as `Sand in a Box` and upcoming `Powdertron` raise the expectation bar for continuous thermal simulation. Heatprint must therefore stay authored/discrete and consequence-first.
- maintenance games such as `Awaria` validate a strong repair fantasy but also show how easily machine maintenance becomes bespoke per-device content.

Market references are evidence for differentiation only, never templates to imitate.

---

# 1. G6C08 — COMMON SHAFT

## 10-second muted clip
0–2s: three idle machines flank one visibly rotating shaft. 2–4s: player clutches a lift onto it; lift rises. 4–6s: same clutch instantly slows/reverses an already-coupled fan and conveyor. 6–8s: player releases the fan, shaft accelerates and lift overshoots. 8–10s: player couples a brake at the exact stable state and all remaining devices stop together.

The clip communicates one physical fact: **everything attached must live with the same motion**.

## First 15 minutes
0–3: clutch one device; shared speed/direction is obvious. 3–6: two devices with useful but conflicting requirements. 6–9: introduce finite authored speed bands and reversal source, not numeric RPM. 9–12: teach collateral effect: solving one load changes another. 12–15: first synthesis with three devices, one optional clutch order and one deliberately harmful but legal coupling.

## Mature 30-minute session
A compact machine room contains one shaft, 5–7 attachable loads, 2–3 drive states and 1–2 brakes/freewheels. The player repeatedly changes which subsystems share motion, using one machine's unwanted load or direction as another machine's needed condition. Most actions are coupling decisions, not construction.

## 24 situations / genuine transformations
**T1 coupling membership:** lift+fan, pump+door, cutter+feed, brake+platform, flywheel+press, alternator+gate.
**T2 direction conflict:** one device needs forward while another must coast/reverse; six variations using one-way clutches, reverse drive and hold states.
**T3 load/speed collateral:** attach load to slow shaft into safe band; detach to accelerate; use heavy transient load; preserve a minimum speed elsewhere; six cases.
**T4 synchronized phase/state:** two devices must share start/stop moment, one must be isolated before next stroke, shared brake freezes multiple states, six cases.

Four genuine transformations survive without adding belts, gears inventory or factory expansion.

## Dominant exploit + smallest global counter-rule
Exploit: solve devices one at a time by disconnecting everything else.
Counter-rule: some world states are only retained while their device remains coupled or while shaft remains in a visible band. This is global `state requires live coupling`, not per-level arbitrary locks.

## Controls
Controller: left stick/D-pad moves/focuses authored clutch points; A clutch/unclutch; LB/RB cycles nearby couplings; X inspects shaft state; Y previews affected currently coupled devices; Undo/Redo dedicated. Keyboard equivalent: WASD/arrows, Enter/A, Q/E cycle, I inspect, Tab effects, Z/Y history. No virtual cursor or precision drag.

## Hour 3 / hour 10
Hour 3: one-way clutch, shared brake, flywheel/inertial hold represented discretely, reversible drive, useful load as speed governor. Hour 10: topology/order problems with the same 5–6 primitives; multi-stage causal compression where a temporary harmful coupling sets two downstream states. No factory economy, belts, ratios or free gear construction.

## Burden
Art 3/5 | UI 3/5 | simulation 3/5 | content 4/5 | QA 4/5. Deterministic banded shaft state avoids rigid-body truth.

## Negative review
“Every puzzle is attach the right machines until the speed is correct; it’s Tension Budget with gears.”
Smallest repair: require mature cases to include at least two distinct causal roles for coupling beyond resource sharing: direction/state persistence/synchronization plus load-band reasoning. If detached abstract load accounting preserves solutions, content fails.

## One-week gate
PASS only if 6–8 graybox cases produce >=3 distinct reasoning skeletons, testers naturally explain collateral coupling rather than “allocate power”, strongest/fastest shaft state is not dominant, and no real-time precision is needed.

**RESULT: FINALIST — #1 provisional.** Strongest physical readability, but portfolio overlap with Tension Budget remains the primary attack target.

---

# 2. G6C01 — STITCHSPACE

## 10-second muted clip
Player grabs the north edge of a sealed room and stitches it to the east edge of another; the seam visibly zips closed and a rolling object exits sideways into the distant room. Player moves one endpoint and the route instantly changes while geometry itself remains unfolded.

## First 15 minutes
0–3: one seam connects two otherwise sealed edges. 3–6: crossing preserves a visible orientation rule. 6–9: move one endpoint and strand/recover an object. 9–12: one scarce seam must serve two routes sequentially. 12–15: first loop where seam placement alters both player route and object route.

## Mature session
Three to five compact rooms expose 6–10 legal boundary sockets and 1–3 physical seams. The player rewires adjacency, moves through it, transports objects, temporarily creates loops and deliberately disconnects a return edge after crossing.

## 24 situations
**T1 reachability:** bypass wall, connect isolated room, route object, rescue return route, one-way orientation, two-stage seam reuse.
**T2 orientation:** rotate exit heading through chosen edges, preserve/flip local facing under explicit seam class, route gravity-lane object, six cases.
**T3 topology/loops:** create cycle, break cycle, isolate region, swap two adjacencies, temporary self-loop, avoid sealing player; six cases.
**T4 moving-state dependency:** object enters before endpoint moves, seam occupied, scarce seams shared across rooms, transport changes later adjacency, six cases.

## Dominant exploit
Exploit: always stitch current room directly to goal.
Counter-rule: only authored exposed boundary sockets are stitchable and seam count is tiny; objectives depend on what adjacency disconnects as well as connects. This is legible topology, not arbitrary “portal forbidden” surfaces.

## Controls
Controller/keyboard focus edge sockets with deterministic spatial cycle; select endpoint A, endpoint B, confirm; shoulder buttons cycle legal edges. World movement remains ordinary. No free drawing.

## Hour 3 / 10
Hour 3: two seams, orientation, objects occupying seams, loops. Hour 10: graph-state problems with 3–5 rooms and consequences of removing old adjacency; no portal colors, momentum tricks, recursive boxes or folding geometry required.

## Burden
Art 2 | UI 4 | simulation 2 | content 5 | QA 4. Main burden is level topology validation and communicating remote adjacency.

## Negative review
“Cool portal puzzle, except portals are drawn on room borders.”
Repair: forbid content whose solution reasoning is simply “place entrance/exit”. Mature cases must require an adjacency *replacement* consequence: connecting A-B must materially remove/consume/redirect another useful adjacency or change orientation/occupancy.

## One-week gate
PASS if naive testers can explain the difference from a portal within 10 minutes, orientation errors stay low, and at least 3 of 8 mature cases rely on adjacency replacement rather than shortcutting.

**RESULT: FINALIST — #2 provisional.** Excellent scope and depth, with serious marketing-comparison risk.

---

# 3. G6C06 — FLOOR PLAN SURGERY

## 10-second clip
Player slides one full wall carriage; a room shrinks while the adjacent room grows. A machine is cut off from one worker, a rolling object gains a corridor, and a pressure/containment zone changes in one visible motion.

## First 15 minutes
Teach one wall, route consequence, occupied side constraint, then two competing rooms and first machine whose reach crosses the moved boundary.

## Mature session
A floor contains 3–4 rooms and 2–4 wall carriages on fixed tracks. Moving a wall reallocates finite floor cells and changes containment, access, machine reach and sometimes zone membership.

## 24 situations
T1 route allocation (6), T2 containment/zone membership (6), T3 machine reach/clearance (6), T4 multi-wall sequencing and restoration (6).

## Exploit
Move every wall to maximum useful side. Counter-rule: every wall reallocates finite shared space and both adjacent rooms have explicit minimum functional footprint/occupied objects; no side can receive space for free.

## Controls
Select wall carriage, choose one of discrete stops, preview directly affected occupancy/reach, confirm. Controller first-class.

## Hour 3 / 10
Hour 3 can combine two walls and machine reach. Hour 10 currently mainly creates larger coupled layouts. The rule does not naturally produce as many qualitatively different causal transformations as Common Shaft/Stitchspace without adding pressure, ownership, gas, people or bespoke machine rules.

## Burden
Art 3 | UI 4 | simulation 2 | content 5 | QA 4.

## Negative review
“After the clever intro it is just sliding dividers until every room is big enough.”
The smallest repair would require multiple global consequences of wall position, but that begins to expand the vocabulary.

## Gate
PASS would require 8 grayboxes with >=3 reasoning skeletons using only route/containment/reach and no new subsystem. This looks uncertain.

**RESULT: RESERVE / CUT FROM FINAL FIVE.** Strong clip, insufficient proven hour-10 transformation without system accretion.

---

# 4. G6C03 — SIGNAL IN FLIGHT

## 10-second clip
Two bright command pulses travel down separate tracks. Player flips a junction after one pulse passes but before the second; first opens a gate, second is intercepted and redirected into a lift, with visible order dependence.

## First 15 minutes
0–3 release one pulse. 3–6 redirect while moving. 6–9 two pulses and order. 9–12 Pause/Step and intercept device. 12–15 first synchronization/anti-synchronization synthesis.

## Mature session
A small deterministic command network contains 2–5 pulses, finite tracks, queues, interceptors and actuators. The player edits topology/state while commands are already travelling rather than constructing a static circuit before Run.

## 24 situations
T1 reroute-after-release (6); T2 ordering/queue (6); T3 interception/transformation of pulse destination/state (6); T4 simultaneous/separated arrival and moving topology (6).

## Exploit
Pause immediately and solve as a static circuit. Counter-rule: Pause/Step remains allowed, but topology changes are themselves canonical actions that affect only pulses that have not crossed the relevant boundary; history/position makes the problem dynamic even when paused.

## Controls
Controller selects nearest junction/interceptor in stable authored focus order; A toggles/commits; Pause/Step dedicated; no cursor drawing.

## Hour 3 / 10
Hour 3: queues, fork timing, pulse priority, one pulse unlocking a route for another. Hour 10: schedule/topology interplay, commands changing later routing state, causal chains of 4–6 events. Vocabulary can remain tight.

## Burden
Art 2 | UI 5 | simulation 3 | content 4 | QA 5. Readability of multiple in-flight pulses is existential.

## Negative review
“It’s a circuit puzzle that makes me wait for the signals to move.”
Repair: mature puzzles must contain decisions that are impossible to express as one pre-run static wiring arrangement; at least one topology edit must depend on pulse history/position.

## Gate
PASS if >75% testers can predict next pulse destinations without replay spam, Pause/Step users still face state reasoning, and 6 mature grayboxes cannot be solved by one static preconfiguration.

**RESULT: FINALIST — #3 provisional.** Distinct enough if “editing execution” survives UI load.

---

# 5. G6C04 — HEATPRINT

## 10-second clip
A hot stamp touches a cold plate; a bright footprint remains. A wax latch softens only where printed, coolant crosses part of the footprint, and a later slider bends exactly through the remaining warm region.

## First 15 minutes
Teach persistent-but-decaying discrete heat cell, direct melt/soften consequence, coolant subtraction, overlap/merge and first delayed use.

## Mature session
Player moves one or two heat/cool tools across a small authored grid, creating temporary discrete thermal regions that affect traction, wax, bimetal devices and reveal states.

## 24 situations
T1 placement/path footprint (6); T2 decay/order (6); T3 hot/cold overlap and cancellation (6); T4 mechanisms sampling region shape/state (6).

## Exploit
Paint everything hot. Counter-rule: fixed thermal budget/decay would make it resource accounting; harmful overheating/cooling by material family is more physical but creates more rules.

## Controls
Grid/track stamping is controller viable if discrete; free painting is forbidden.

## Hour 3 / 10
Hour 3 works. Hour 10 tends either toward larger fields or adding more heat-reactive material types. That creates exactly the content/simulation catalogue the factory wanted to avoid.

## Burden
Art 4 | UI 4 | simulation 4 | content 5 | QA 5.

## Negative review
“Looks like a thermal sandbox but behaves like arbitrary colored tiles.”
The repair—richer thermal simulation—would worsen scope and readability.

## Gate
Needs testers to accept discrete thermal rules as physical while producing 3+ reasoning skeletons from <=4 reaction families. High failure probability.

**RESULT: CUT.** Attractive visual effect, wrong expectation/scope asymmetry.

---

# 6. G6C07 — CHECKPOINT MATERIAL

## 10-second clip
Player clamps a marker onto a loaded scale. Gauge visibly snaps its new zero to current load. Player removes two crates; mechanism now reads “-2 relative steps” and opens a counterbalanced door even though absolute load remains high.

## First 15 minutes
Capture reference position/load, react to deviation, move reference after world change, use one machine's baseline to make an otherwise impossible state count as zero.

## Mature session
3–6 mechanisms each compare their current discrete state against one captured local reference. Player decides *when* to checkpoint, then changes the world so relative differences trigger machines.

## 24 situations
T1 load baselines (6), T2 position baselines (6), T3 count/state baselines (6), T4 chained reference capture where one mechanism's change creates another's useful reference (6).

## Exploit
Checkpoint immediately before every desired action. Counter-rule: capturing reference has a visible physical eligibility condition and replaces the previous reference; however repeated free recapture still risks trivialization. Adding limited charges would become arbitrary resource gating.

## Controls
Select calibratable machine, hold/press capture, inspect simple before/current/reference markers. Controller easy.

## Hour 3 / 10
Hour 3 can be clever. Hour 10 risks becoming algebraic scheduling of baselines unless world consequences are rich, which would require importing many bespoke machine rules.

## Burden
Art 2 | UI 5 | simulation 2 | content 5 | QA 4.

## Negative review
“Interesting idea, but I’m basically changing zero on a bunch of gauges and doing subtraction in my head.”
Smallest repair is stronger physical visualization, not enough to solve the fantasy weakness.

## Gate
PASS only if naive testers solve mature cases using physical-language descriptions rather than numerical/calibration language, and free recapture is not dominant.

**RESULT: CUT TO RESERVE.** Elegant formal mechanic, weak tactile fantasy and demo conversion.

---

# 7. G6C36 — SERVICE WINDOW

## 10-second clip
A machine cycles visibly. During one safe open phase, player slides a service window aside, grabs an internal cam/follower into another authored slot, closes it, and the next external stroke changes while the machine never fully stops.

## First 15 minutes
Expose one internal during a deterministic paused step, reposition among 2–3 snap slots, see next cycle change, then teach that opening access itself blocks/exposes another internal.

## Mature session
A compact machine has 3–5 internally visible modules and 2–4 operating phases. The player pauses/steps, opens bounded service windows and repositions/reconnects snap-state components while external outputs continue across cycles.

## 24 situations
T1 phase-gated access (6), T2 internal slot/state changes (6), T3 one access panel hides/blocks another (6), T4 multi-cycle setup where a change made now affects later accessible phase (6).

## Exploit
Open everything while paused and configure ideal machine. Counter-rule: service windows are physical parts of the mechanism; opening one changes/block access/output states and only specific internals are exposed in each canonical cycle phase.

## Controls
Controller focus hierarchy must switch cleanly between exterior machine, service window and exposed snap slots. Pause/Step mandatory. No precision grabbing; all slots discrete.

## Hour 3 / 10
Potential depth is high if the same 4–5 module families recur across machines. But commercial fantasy strongly pushes toward unique machinery, animations and internals. Reusing the exact modules risks visual repetitiveness; bespoke modules explode content burden.

## Burden
Art 5 | UI 5 | simulation 3 | content 5 | QA 5.

## Negative review
“Every level teaches me another machine-specific panel and I spend half my time figuring out what is clickable.”
The smallest repair is a strict universal module vocabulary, but that weakens the maintenance fantasy.

## Gate
PASS requires one primitive graybox machine vocabulary to generate 8 genuinely different cases with no new module families and controller testers to navigate internals without a virtual cursor.

**RESULT: CUT.** Excellent fantasy, unfavorable asset/UI/content scaling.

---

# 8. G6C02 — LAST CONTACT

## 10-second clip
A piston touches rubber, gaining a visible short-lived rubber contact memory. Its next strike becomes soft and stops a fragile crate. Then metal touches it and the next stroke becomes hard, launching a second object.

## First 15 minutes
Teach one contact memory, replacement by last contact, one next-operation consumption, sequencing through a machine and first donor object whose physical location matters.

## Mature session
Several mechanisms remember exactly one last material-contact class; moving real donor objects through the space sets upcoming behavior. Contact state is consumed or replaced by the next valid operation.

## 24 situations
T1 set next behavior (6), T2 overwrite order (6), T3 donor routing/location (6), T4 chained contacts where one altered operation moves the next donor (6).

## Exploit
Park every donor beside its target and reapply before use. Counter-rule would require donor scarcity/location or contact consumption, but then it increasingly resembles physical property delivery previously explored in Single-Pixel/LeiLei-adjacent territory.

## Controls
Physical object movement plus interact; controller viable if authored lanes/snap carries.

## Hour 3 / 10
Hour 3 is good. Hour 10 needs more contact classes, richer donor logistics or more mechanism-specific responses. All three increase overlap or content taxonomy.

## Burden
Art 3 | UI 4 | simulation 3 | content 5 | QA 4.

## Negative review
“It’s another property-transfer puzzle except the property expires after one machine action.”
The required repair changes the identity more than it clarifies it.

## Gate
Would need testers to reason primarily about physical contact history rather than donor labels and maintain depth with <=4 contact classes.

**RESULT: CUT.** Market/portfolio collision remains too structural.

---

# 9. G6C09 — VACUUM SHAPE

## 10-second clip
Player opens a vent; a large membrane object snaps from inflated arch to collapsed wedge, lowering a platform and sealing a pipe. Close/fill causes it to snap into a rigid buoyant block and lift cargo.

## First 15 minutes
Teach two discrete shape states, one structure doing two jobs, vent network, then sequence where changing shape opens one route while closing another.

## Mature session
3–5 flexible structures each have 2–3 authored stable forms controlled by local vent/fill state. Their forms become platforms, seals, pushers, containers or blockers.

## 24 situations
T1 route geometry (6), T2 sealing/containment (6), T3 pushing/lifting/holding (6), T4 coupled vent sequencing where one pressure action changes several structures (6).

## Exploit
Toggle every structure until useful form appears. Counter-rule: visible vent topology plus finite discrete states lets players predict rather than guess, but shared vent coupling starts resembling resource/pressure network puzzles.

## Controls
Select vent/valve, choose authored state; no soft-body manipulation.

## Hour 3 / 10
Hour 3: shared vents and 3-form membranes. Hour 10 tends toward more membrane shapes/functions or pressure-network complexity. Trailer suggests soft-body simulation that design explicitly cannot safely promise.

## Burden
Art/animation 5 | UI 3 | simulation 3 | content 5 | QA 4.

## Negative review
“The inflatable stuff looks physical but everything just snaps between canned shapes.”
Repairing that perception would require exactly the soft-body simulation burden the concept rejects.

## Gate
PASS only if primitive snap animations still feel satisfying/physical and 8 cases remain interesting with <=3 global shape families.

**RESULT: CUT.** Expectation mismatch and content animation burden are too high.

---

# 10. G6C05 — THE SHORT CIRCUIT

## 10-second clip
Player bridges two exposed contacts with a fault bar. Sparks travel, a fuse isolates one branch, a motor drops into a spring-return fallback state and physically releases a door. Player removes the short before a second fallback becomes harmful.

## First 15 minutes
Teach legal intentional fault, predictable isolation, one useful fallback, collateral shutdown and first chain where a fault deliberately resets one device while preserving another.

## Mature session
A tiny deterministic electrical-mechanical panel has 4–7 devices, 2–4 faultable contact pairs and explicit fuse/fallback states. The player causes bounded faults to invoke normally undesirable safe/fail states as tools.

## 24 situations
T1 fallback activation (6), T2 isolation/topology consequence (6), T3 fault ordering/reset (6), T4 collateral mechanical consequences such as latch release/heater trip/motor coast (6).

## Exploit
Short everything and observe what helps. Counter-rule: each legal short previews direct affected branch/fuse/fallback family; puzzle is selecting collateral result, not hidden trial-and-error. Undo remains free.

## Controls
Controller focus exposed contact pairs; select first/second or choose authored bridge, confirm; inspect branch effects. No wire drawing.

## Hour 3 / 10
Hour 3: multiple fault domains, latching fuse, reset order, one mechanical consequence. Hour 10: use one fault to create a fallback state that changes which later short is possible, with 2–3 bounded fault types. Depth can come from causal sequencing rather than more components.

## Burden
Art 3 | UI 4 | simulation 2 | content 4 | QA 4.

## Negative review
“It’s still a circuit puzzle, except the correct move is intentionally making the circuit wrong.”
Repair: never let wire/path construction become the dominant activity; fixed topology, few visible faultable pairs, and every mature case must require a fallback/mechanical consequence that ordinary correct routing cannot express.

## Gate
PASS if testers can predict fault consequences after onboarding, do not describe play as circuit assembly, and 6/8 mature cases require reasoning about fail-safe state rather than connectivity alone.

**RESULT: FINALIST — #4 provisional.** Narrower hook than leaders, but surprisingly strong causal identity and cheap deterministic prototype.

---

# 11. Uniform comparison after destructive pass

Scores 1–10; higher is better. `Build predictability` means lower production risk.

| Concept | Hook | Mute clip | Depth | Market distinction | Portfolio distance | Controller | Build predictability | Content scalability | Demo | Total /90 |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| **Common Shaft** | 9 | 9 | 9 | 8 | 6 | 9 | 8 | 8 | 9 | **75** |
| **Stitchspace** | 9 | 9 | 9 | 7 | 10 | 9 | 9 | 8 | 9 | **79** |
| **Signal in Flight** | 8 | 9 | 9 | 7 | 10 | 8 | 8 | 8 | 9 | **76** |
| **The Short Circuit** | 9 | 9 | 8 | 7 | 9 | 9 | 9 | 8 | 9 | **77** |
| Floor Plan Surgery | 9 | 10 | 6 | 8 | 9 | 9 | 8 | 6 | 9 | 74 |
| Checkpoint Material | 7 | 7 | 8 | 9 | 10 | 10 | 9 | 6 | 7 | 73 |
| Service Window | 9 | 10 | 8 | 8 | 10 | 6 | 5 | 5 | 9 | 70 |
| Last Contact | 8 | 9 | 7 | 5 | 6 | 8 | 8 | 6 | 8 | 65 |
| Vacuum Shape | 9 | 10 | 7 | 8 | 9 | 9 | 5 | 5 | 9 | 71 |
| Heatprint | 9 | 10 | 7 | 7 | 9 | 8 | 5 | 5 | 9 | 69 |

The totals do not automatically select a winner. Common Shaft remains in despite lower portfolio score because its tactile collateral coupling is unusually legible. Floor Plan Surgery is excluded despite a respectable total because its hour-10 transformation currently relies on adding subsystem consequences. Checkpoint Material is excluded despite technical elegance because its core fantasy is weak and likely reads as calibration arithmetic.

---

# 12. Phase-2 finalists after Run 1

Exactly four advance:

## F1 — G6C01 STITCHSPACE
Best scope/depth/portfolio combination. Existential question: can players immediately perceive **rewired adjacency** as different from portals/folding, and can mature puzzles force adjacency replacement rather than shortcut placement?

## F2 — G6C05 THE SHORT CIRCUIT
Strongest surprise improvement. Intentionally exploiting fail-safe states is highly legible and cheap to model. Existential question: can it avoid looking like a conventional circuit puzzle with an inverted objective?

## F3 — G6C03 SIGNAL IN FLIGHT
Best temporal-state reasoning without clone/time-loop territory. Existential question: does editing execution-in-progress remain comprehensible with several pulses, or become UI/event-log management?

## F4 — G6C08 COMMON SHAFT
Strongest tactile machinery fantasy and causal collateral. Existential question: is shared synchronization/coupling genuinely distinct enough from Tension Budget's conserved-load engineering and generic gear puzzles?

### Reserves
1. **Floor Plan Surgery** — strongest reserve if the final four fail; mute clip is exceptional, hour-10 transformation unproven.
2. **Checkpoint Material** — formal depth reserve; tactile fantasy weak.

### Eliminated in Run 1
- Heatprint — expectation/simulation/content mismatch.
- Service Window — bespoke machine/UI burden.
- Last Contact — property-transfer/portfolio collision.
- Vacuum Shape — soft-body expectation and animation/content burden.

---

# 13. NEXT ACTION — PHASE 2 RUN 2 / FINALIST FALSIFICATION

Do **not** enter Product Thesis yet.

For all four finalists, next run must:
1. freeze the smallest exact primitive/state vocabulary;
2. define 8 graybox cases with expected solution skeletons;
3. attack every case for trivial/static/dominant solutions;
4. compare hour-10 reasoning with no new primary verbs;
5. run a fresh exact-mechanic analogue check, especially Stitchspace vs portals/topology, Short Circuit vs circuit/failure-state games, Signal in Flight vs live-programming/signal games, Common Shaft vs gear/load/coupling games;
6. specify first 20 minutes and first two hours precisely;
7. define content compiler/validator burden and alternate-solution search burden;
8. define one-week prototype plan with binary kill thresholds;
9. perform a direct portfolio-distance test against Games #001–#005;
10. reduce to **2–3 final contenders** only if evidence warrants it.

No Game #006 winner is selected yet.