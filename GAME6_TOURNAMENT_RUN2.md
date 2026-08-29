# GAME #006 — CONCEPT TOURNAMENT — RUN 2 FINALIST FALSIFICATION

Last updated: 2026-08-29
Factory run: **3**
Phase: **2 — Concept Tournament / finalist falsification**
Final concept selected: **NO**
Production implementation started: **NO**

This run executes the exact falsification packet required by `STATUS.md` for the four surviving finalists: **Stitchspace, The Short Circuit, Signal in Flight, Common Shaft**. The goal is to turn each pitch into the smallest exact rule system that could be grayboxed, attack dominant/static solutions, compare hour-10 depth without new primary verbs, and reduce the field only where evidence warrants it.

Fresh exact-mechanic market checks on 2026-08-29:
- `Portal 2` remains the unavoidable portal-comparison baseline and still has enormous recognition/review volume. `Folding Dungeon` (2026) explicitly folds/connects space. Stitchspace therefore survives only as **replacement of room-boundary adjacency with scarce persistent seams**, never generic entrance/exit placement or folding.
- `Short Circuit VR` is explicitly an electronics construction/lab product; `Lighton` asks players to assemble circuits and treats a short as failure/explosion. The Short Circuit remains differentiated only if **deliberately causing a bounded fault to invoke a deterministic protection/fallback state** is the core repeated action.
- `The Signal State` is a successful modular-signal patching puzzle. Signal in Flight must not become pre-run cable construction; its identity is **editing a machine after commands have already entered execution**, where pulse history/position matters.
- `Gear Combination` (2025) explicitly centers on arranging gears to hit target rotational speed. Common Shaft therefore cannot market or design around target RPM/gear-ratio reasoning. Its only defensible identity is **membership in one forced shared motion state and collateral synchronization**.

References:
- https://store.steampowered.com/app/620/
- https://store.steampowered.com/app/4576650/Folding_Dungeon/
- https://store.steampowered.com/app/970800/Short_Circuit_VR/
- https://store.steampowered.com/app/1328570/Lighton
- https://store.steampowered.com/app/1577620/The_Signal_State/
- https://store.steampowered.com/app/3737430/Gear_Combination/

---

# 1. Uniform falsification rules

Every finalist must now answer the same questions:
1. smallest exact primitive/state vocabulary;
2. exact state-changing command semantics;
3. eight graybox cases and expected solution skeletons;
4. dominant/static/trivial strategy attack;
5. first 20 minutes and first two hours;
6. hour-10 reasoning without new primary verbs;
7. content compiler/validator burden;
8. alternate-solution search burden;
9. one-week prototype plan and binary thresholds;
10. direct portfolio-distance test against Games #001–#005.

A concept is cut if its strongest defense requires feature accretion, arbitrary per-level exceptions, real-time dexterity that defeats Pause/Step accessibility, or a repeated reasoning skeleton too close to an earlier factory game.

---

# 2. G6C01 — STITCHSPACE

## 2.1 Exact primitive vocabulary

World:
- 2–5 compact rooms;
- each room has stable identity and 2–6 authored **edge sockets** on its boundary;
- 1–3 **seams** exist in a case;
- a seam always connects exactly two currently legal edge sockets;
- ordinary authored doors/passages may also exist and are not seams;
- entities occupy room-local nodes/lanes and have stable orientation.

A seam has only:
- endpoint A socket;
- endpoint B socket;
- orientation mapping from crossing side A to side B;
- occupancy state: empty / entity currently crossing;
- optional directionality class: bidirectional or authored one-way. No portal colors, momentum preservation mechanics, recursive views, arbitrary free-surface placement or physics flinging.

Core command:
`MOVE_SEAM_ENDPOINT(seam_id, endpoint, target_socket)`.

Validation:
1. target socket is exposed/legal;
2. endpoint is not locked by an entity mid-crossing;
3. resulting seam graph is structurally valid;
4. endpoint replacement commits atomically;
5. adjacency graph updates immediately;
6. ordinary traversal/object commands then use the new graph.

The important rule is **replacement**: moving endpoint A away from socket X removes the previous seam adjacency at X at the same instant it creates the new one. A seam never creates unlimited extra doors.

## 2.2 Eight graybox cases

### SS01 — Replace, do not add
Two isolated rooms and one seam. Move endpoint once to reach target, but doing so removes return adjacency.
Skeleton: connect -> cross -> replace -> recover route.

### SS02 — Orientation matters
Rolling body enters south-facing edge and must emerge west-facing to reach a lane receiver.
Skeleton: select endpoint pair by orientation mapping, not shortest route.

### SS03 — Shared seam logistics
Player and crate need different destinations using one seam.
Skeleton: route object first -> move endpoint -> route self -> restore.

### SS04 — Disconnect as action
An enemy/hazard/rolling body is safely isolated only by moving a seam endpoint away after it crosses.
Skeleton: invite crossing -> cut adjacency -> exploit isolation.

### SS05 — Loop creation
Two ordinary passages plus one seam can create a topological cycle required to approach one edge from a different local side.
Skeleton: create cycle -> traverse transformed orientation -> break cycle.

### SS06 — Occupancy lock
A long object/transport platform occupies seam crossing for one canonical step; endpoint cannot be moved until clear.
Skeleton: schedule crossing order from deterministic occupancy, not reflex timing.

### SS07 — Two seams / swapped adjacency
Four rooms, two seams. Goal requires exchanging which pairs are adjacent while preserving one route.
Skeleton: temporary bridge -> rewire first pair -> reuse second seam -> final swap.

### SS08 — Mature synthesis
Four rooms, two seams, one rolling body, one player objective, one edge whose disconnection matters, and two valid solutions.
Required skeletons differ: one uses orientation; one uses temporary isolation. A pure `entrance near me -> exit near goal` solution must fail.

## 2.3 Dominant/static attacks

**Direct-to-goal portal exploit:** authored edge sockets alone are insufficient defense if goal socket is always reachable. Mature cases therefore require at least one material **replacement consequence**: the adjacency removed by moving a seam must affect route, object, hazard, orientation, or later access.

**Solve graph statically before moving:** acceptable in some cases, but mature play must contain state-dependent rewiring after entity movement. At least one required seam move from C-midgame onward must depend on which room/object state has already changed.

**Orientation becomes bookkeeping:** orientation must be visible on socket geometry and crossing preview. If players need compass tables, kill/repair.

**Stranding creates restart spam:** Undo is immediate; compiler rejects authored baseline paths with unavoidable hidden strand traps before the mechanic is explicitly taught.

## 2.4 First 20 minutes
0–4: stitch two exposed edges; cross.
4–7: move one endpoint and see old adjacency vanish.
7–10: orientation mapping with rolling object.
10–13: same seam must serve object then player.
13–16: deliberately disconnect something after it crosses.
16–20: first 3-room synthesis with two valid solutions and one loop.

## 2.5 First two hours
0:20–0:45: two ordinary routes + one seam, explicit adjacency replacement, first loop/isolation cases.
0:45–1:15: second seam introduced, seam occupancy, orientation combinations, object/player order.
1:15–2:00: 3–4 room cases where seam movement changes future reachability and at least two distinct solution skeletons exist. Primitive vocabulary is effectively complete by hour 2.

## 2.6 Hour-10 reasoning
No new primary verb is necessary. Mature depth can come from:
- graph cut vs graph connection;
- orientation under adjacency replacement;
- scarce seam reuse;
- state-dependent endpoint movement;
- temporary cycles;
- isolating or exposing entities by cutting adjacency;
- two-seam dependency order;
- causal compression: one seam move solving both routing and isolation.

Existential condition: at hour 10, player language must sound like `I need these rooms adjacent only until the crate crosses`, not `put portal here, then portal there`.

## 2.7 Content compiler / solver burden
Compiler must validate:
- unique sockets/room IDs;
- seam endpoint legality;
- deterministic orientation mapping;
- no simultaneous occupancy ambiguity;
- reachability for known baseline fixture;
- no forbidden free placement;
- no baseline soft-lock without Undo/recovery contract;
- transformation tags: connect, disconnect, orientation, loop, occupancy, scarce-reuse.

Alternate-solution search is **medium-high but bounded**: room graph is small and discrete. A BFS/A* over seam endpoint graph + entity states is feasible for graybox/content auditing.

## 2.8 One-week prototype
Day 1 room/socket graph and one seam.
Day 2 player crossing + exact orientation.
Day 3 movable endpoint + replacement visualization + Undo.
Day 4 deterministic rolling object and occupancy lock.
Day 5 SS01–SS04.
Day 6 SS05–SS08 + bounded solver.
Day 7 naive tests and portal-comparison interview.

PASS only if:
- >=75% naive testers can explain within 10 minutes that moving a seam **replaces adjacency** rather than placing a teleporter pair;
- orientation misunderstanding causes <20% ordinary failures after tutorial;
- >=5/8 grayboxes materially require the lost/replaced adjacency, orientation, occupancy or disconnection consequence;
- mature solver solutions produce >=4 abstract skeleton families across SS04–SS08;
- no baseline solution requires dexterity/timing;
- short mute clip communicates remote room adjacency changing without explanatory text.

## 2.9 Portfolio distance
- Organism Cargo: no logistics economy/organism system; only tiny object routing overlap generic to puzzle games.
- False Map Department: topology is physical game truth, not representation/authority bureaucracy.
- Borrowed Collision: no portable consequences/resources.
- HEARWALL: no listening primary interface.
- Tension Budget: no conserved scalar allocation or shared-load budget.

**PORTFOLIO DISTANCE: STRONG.**

**RUN-2 RESULT: ADVANCES.** Strongest scope/depth ratio; main risk remains market communication against portals/folding.

---

# 3. G6C05 — THE SHORT CIRCUIT

## 3.1 Exact primitive vocabulary

World is a stylized deterministic protection network, not an electronics simulator.

Each case has:
- 1–3 low-voltage source buses;
- 3–7 devices;
- fixed authored exposed **fault contacts**;
- 1–3 protection devices/fuses/breakers;
- each device has exactly `NORMAL` plus one authored **FALLBACK** state initially; a small late-game ceiling of two fallback modes is allowed only if globally defined.

Core command:
`BRIDGE_FAULT(contact_a, contact_b)` using a visible insulated fault probe/jumper.

A valid bridge creates a bounded **fault zone**. Resolution order:
1. validate the pair is an authored bridgable contact pair;
2. identify affected protection domain;
3. apply immediate local fault side effect from a small global family;
4. affected devices enter their deterministic fallback/safe-loss state;
5. protection trips and isolates the domain;
6. resulting mechanical/electrical fallback world state persists until an authored reset action;
7. fault bridge is removed/neutralized after trip unless the case explicitly uses a latched physical shunt.

Global fallback families are capped at four:
- `DROP` — powered latch releases / gravity-rest state;
- `SPRING_RETURN` — actuator returns to mechanical default;
- `COAST` — motor loses drive and advances/settles one authored state;
- `FAILOVER` — alternate passive/backup path becomes active.

No current/voltage arithmetic, breadboards, resistance values, free wiring, component catalogue or shock-combat system.

## 3.2 Eight graybox cases

### SC01 — Wrong is useful
Deliberate short trips latch power and opens a gravity door.
Skeleton: identify protection domain -> fault -> use fallback.

### SC02 — Domain collateral
Same trip opens one latch but also releases a platform needed later.
Skeleton: prepare mechanical state -> fault -> exploit one fallback while recovering another.

### SC03 — Protection selectivity
Two possible fault contact pairs trip different bounded domains.
Skeleton: choose *where* to fail, not whether to fail.

### SC04 — Spring return chain
Fault removes power from actuator; spring-return position physically pushes an object.
Skeleton: stage object -> trigger failure -> use passive motion.

### SC05 — Coast window
Motor loses power and coasts to one deterministic next stop; fault timing is command-step/state based with Pause/Step, not reflex.
Skeleton: set motor phase -> fault -> coast into useful state.

### SC06 — Failover path
Faulting primary domain activates a normally-unused backup route but disables another device.
Skeleton: configure downstream -> trip primary -> route through fallback -> reset.

### SC07 — Reset consequence
Reset restores power but mechanically re-latches one earlier path, so fault/reset order matters.
Skeleton: fault A -> use fallback -> reposition -> reset -> fault B.

### SC08 — Mature bounded-failure synthesis
Three protection domains, four devices, two legal fault pairs, one reset, one passive mechanical consequence, two valid solutions. No normal-circuit rewiring action exists.

## 3.3 Dominant/static attacks

**Short everything:** only authored exposed fault contacts are bridgeable; every trip has visible collateral consequence. However this cannot become arbitrary lockout. Each contact exists because the machine physically exposes a test/service point.

**Trial every fault pair:** small pair count plus Undo means brute force is always possible. Mature content must therefore make predictions readable and solution depth come from *preparing world state before the trip* and *ordering fallback consequences*, not hiding which pair works.

**Ordinary circuit puzzle drift:** if player spends meaningful time routing valid power, assembling wires, selecting resistors or satisfying normal current paths, concept fails immediately.

**Electrical simulation expectation:** visual language must openly stylize protection domains and mechanical fallback rather than promise real circuit engineering.

## 3.4 First 20 minutes
0–4: one obvious fault causes a useful latch drop.
4–7: collateral device also loses power.
7–10: choose between two fault domains.
10–13: spring-return mechanical consequence.
13–16: reset restores some states and re-locks another.
16–20: first two-fault synthesis with preparation before trip.

## 3.5 First two hours
0:20–0:45: DROP/SPRING_RETURN/COAST global families.
0:45–1:15: protection-domain selection, first failover, reset ordering.
1:15–2:00: cases combine two fallback families and world preparation. Full primitive vocabulary should be complete by ~90 minutes.

## 3.6 Hour-10 reasoning
Mature play can remain within the same verb if cases ask:
- which failure domain to invoke;
- which world state to prepare before failure;
- how collateral fallback harms/help other devices;
- when to reset;
- how a passive fallback creates the precondition for a second bounded fault;
- how to preserve one powered state while intentionally losing another.

The danger is content repetition: all cases may still read as `trip breaker, use thing that drops`. The four fallback families must produce distinct physical causal skeletons, not cosmetic animations.

## 3.7 Content compiler / solver burden
Compiler validates:
- protection-domain membership;
- legal authored fault pairs;
- deterministic trip ordering;
- fallback transition table;
- reset transition table;
- no unbounded fault loops;
- no hidden electrocution/damage simulation;
- known baseline solution;
- transformation tags for prepare/trip/collateral/reset/failover/passive-motion.

Alternate-solution search: **medium**. State space is discrete and generally smaller than Signal in Flight. Automated search can discover `fault everything then reset` trivializations.

## 3.8 One-week prototype
Day 1 domain/fault/fuse state machine.
Day 2 DROP + reset + one mechanical latch.
Day 3 SPRING_RETURN/COAST.
Day 4 FAILOVER + causal preview.
Day 5 SC01–SC04.
Day 6 SC05–SC08 + brute-force solver.
Day 7 naive test: ask players to predict consequences before confirming fault.

PASS only if:
- >=70% testers describe the core as `using failures/fail-safes on purpose`, not `wiring circuits`;
- at least 4/8 cases require meaningful pre-fault world preparation;
- at least 3 fallback families appear in non-isomorphic solution skeletons;
- brute-force `trip every available domain` is not the shortest solution in >=6/8 cases;
- no numeric electronics knowledge is needed;
- failure consequences are predictable from visible protection-domain/fallback language after tutorial.

## 3.9 Portfolio distance
No direct overlap with prior games' resource systems. Some `use a harmful state as tool` philosophy resembles Borrowed Collision's adverse spends, but there is no portable consequence. It is also distinct from False Map Department because failure is physical system state, not semantic authority.

**PORTFOLIO DISTANCE: STRONG.**

**RUN-2 RESULT: ADVANCES, but as #3 provisional.** Novel physical fantasy is strong; long-term content breadth is less proven than Stitchspace/Signal.

---

# 4. G6C03 — SIGNAL IN FLIGHT

## 4.1 Exact primitive vocabulary

World:
- 2–5 command pulses at once;
- fixed directed track graph;
- authored junctions;
- actuators/receivers;
- optional queues/gates;
- global canonical tick/step, always Pause/Step compatible.

Pulse state contains only:
- stable pulse ID;
- current edge/node;
- one of three command classes: `TRIGGER`, `SET_A`, `SET_B`;
- age/order index for deterministic queue resolution.

Core player commands are restricted to:
- `TOGGLE_JUNCTION(junction_id)` — changes future outgoing edge state;
- `HOLD_RELEASE_GATE(gate_id)` — holds/releases pulses at a visible queue gate;
- `INTERCEPT_SWAP(interceptor_id)` — swaps destination branch for the next pulse crossing that interceptor according to one fixed global rule.

No free wire drawing, programming syntax, arbitrary boolean gate construction, pulse speed upgrades or timing reflexes.

Canonical step order:
1. accept player topology/gate command only at step boundary;
2. freeze current graph state for that step;
3. move eligible pulses one edge simultaneously;
4. resolve arrivals in stable pulse-ID-independent queue rule: arrival lane priority authored and visible, then age;
5. actuators mutate state;
6. resulting actuator state may change named track permissions for next step;
7. pause for next command/step as requested.

## 4.2 Eight graybox cases

### SF01 — Change after release
One pulse passes a junction; player toggles after it passes so second pulse takes another route.
Skeleton: observe history -> change future topology.

### SF02 — Order-dependent actuator
SET_A then TRIGGER succeeds; reverse order fails.
Skeleton: route by arrival order.

### SF03 — Hold one, pass one
Queue gate holds pulse A while B takes newly opened track.
Skeleton: temporary queue -> topology edit -> release.

### SF04 — Pulse opens route for later pulse
First pulse toggles physical gate; second must be redirected only after route exists.
Skeleton: execution creates future graph.

### SF05 — Anti-synchronization
Two pulses must not arrive same step; use hold/release without real-time precision.
Skeleton: separate arrivals by canonical step.

### SF06 — Synchronization
Two command classes must arrive same step from different path lengths.
Skeleton: alter one route after launch + queue other.

### SF07 — Interceptor state
One interceptor can affect only the next crossing pulse before resetting.
Skeleton: choose which pulse consumes transient routing state.

### SF08 — Mature execution edit
Four pulses already moving when player gains control; two junctions, one queue, two actuators alter later track state. At least two valid solutions with distinct queue-vs-reroute emphasis. No single pre-run graph configuration solves it.

## 4.3 Dominant/static attacks

**Pause makes it static:** Pause is fully allowed. The concept survives because pulse position/history is canonical state; even at zero real-time speed, the player is editing an execution already in progress. Every mature case must be impossible to solve solely by selecting one initial static wiring configuration.

**Replay spam:** direction previews show next-edge destination under current topology; history strip shows pulse order. If player must repeatedly run blind to learn deterministic routes, UI failed.

**Signal State/Zachtronics drift:** no patch cables, open-ended module construction, score histograms or code optimization. This is authored stateful execution editing.

**Visual overload:** hard ceiling of five simultaneous pulses in baseline 1.0; most cases use 2–4. Pulse command classes require shape/text redundancy, not color only.

## 4.4 First 20 minutes
0–4: release one pulse and watch one edge per step.
4–7: toggle junction after first pulse passes.
7–10: two pulses/order.
10–13: hold/release queue.
13–16: first pulse opens route for second.
16–20: synchronization/anti-synchronization synthesis, all Pause/Step friendly.

## 4.5 First two hours
0:20–0:45: SET_A/SET_B/TRIGGER classes and deterministic receiver state.
0:45–1:15: queue gates and transient next-pulse interceptor.
1:15–2:00: actuator changes later track permission; 3–4 pulse cases with two valid execution edits. Primitive ceiling reached by hour 2.

## 4.6 Hour-10 reasoning
Without new verbs, mature reasoning can transform through:
- history-sensitive junction edits;
- queue ordering;
- route state created by prior command;
- same-step synchronization;
- deliberate separation;
- transient interceptor consumption;
- multiple pulses sharing one mutable topology;
- causal compression: one edit changing outcomes for several already-moving commands.

Unlike ordinary static circuits, a solution is a **policy over evolving execution state**, not a finished graph.

## 4.7 Content compiler / solver burden
Compiler validates:
- directed graph and stable IDs;
- all junction states;
- deterministic simultaneous step resolution;
- queue priority;
- no pulse ambiguity/collision loss;
- command-class receiver legality;
- known baseline solution;
- explicit max-pulse bound;
- proof that mature case is not solvable by a single pre-run static configuration;
- skeleton tags: reroute-after-pass, queue-order, sync, anti-sync, transient-consumption, actuator-opens-route.

Alternate-solution search is **high but tractable** at the small ceilings. Breadth-first search over graph state + pulse positions + receiver states is feasible but grows faster than Stitchspace/Short Circuit. Strong solver tooling should begin before bulk content.

## 4.8 One-week prototype
Day 1 directed graph/ticks/pulse movement.
Day 2 junction toggle + Pause/Step + history.
Day 3 two pulse classes + actuator state.
Day 4 queue/hold-release + sync resolution.
Day 5 SF01–SF04.
Day 6 SF05–SF08 + static-configuration solver attack.
Day 7 naive prediction/readability tests.

PASS only if:
- >=75% testers correctly predict the next destination of selected pulses after tutorial;
- <=20% ordinary failures come primarily from pulse-identity/order confusion;
- all SF04–SF08 require at least one post-launch state-dependent edit;
- >=4 distinct reasoning skeleton families appear across eight cases;
- Pause/Step does not remove the puzzle, only the reaction burden;
- UI remains readable with four simultaneous pulses at 1280×800 target;
- testers describe the game as `changing commands while they are already running`, not `building a circuit`.

## 4.9 Portfolio distance
Strong. No previous game centers temporal execution editing. It is neither conserved allocation nor portable consequence, and representation is not the thematic authority layer.

**PORTFOLIO DISTANCE: VERY STRONG.**

**RUN-2 RESULT: ADVANCES — #2 provisional.** Strong hour-10 transformation and excellent portfolio distance; UI/state-space burden is the main existential risk.

---

# 5. G6C08 — COMMON SHAFT

## 5.1 Exact primitive vocabulary

World:
- exactly one shared shaft per ordinary case;
- 3–7 device clutches;
- one drive with discrete direction `FORWARD/REVERSE` and speed band `LOW/MID/HIGH`;
- each coupled device contributes one discrete load class `LIGHT/MEDIUM/HEAVY`;
- optional one global brake;
- optional one-way clutch family late.

Core command:
`SET_CLUTCH(device_id, ENGAGED/DISENGAGED)`.

When membership changes:
1. collect all engaged devices;
2. derive resulting shared shaft band from a fixed authored lookup based on drive state + aggregate load class;
3. every engaged device receives the same direction/band simultaneously;
4. device-local mechanical state advances/holds according to its global family table;
5. disconnected devices retain or return state only according to globally visible family behavior.

No gear ratios, tooth counts, free belt routing, torque numbers, electrical power economy or arbitrary shaft network.

## 5.2 Eight graybox cases
CS01 one device coupling.
CS02 second load slows first into useful band.
CS03 detach device to accelerate another.
CS04 direction conflict with one-way device.
CS05 shared brake freezes two useful phases.
CS06 device state persists only while coupled, preventing solve-one-at-a-time.
CS07 transient heavy load used as governor while another machine crosses a band.
CS08 four devices, one brake, one reverse state, two valid ordering solutions.

Expected skeleton families: membership/load-band, synchronization, isolation-before-reverse, transient governor.

## 5.3 Dominant attacks

**Solve one device at a time:** live-coupling state retention rule partly prevents it, but this is structurally close to Tension Budget's `temporarily allocate shared conserved mechanical condition so several loads land in valid states`.

**Fastest state dominant:** receiver/device families need LOW/MID/HIGH-specific useful states. This is mechanically sound but again resembles banded conserved tension/load reasoning.

**Gear-puzzle expectation:** removing ratios/tooth counts helps, but shaft/gear imagery still invites target-speed reasoning already represented by products such as `Gear Combination`.

**Feature repair danger:** adding phase, flywheel, freewheel, clutch wear or multiple shafts would create differentiation by accretion, violating scope discipline.

## 5.4 First 20 minutes / two hours
The first 20 minutes are excellent and tactile: engage, collateral slow, detach, reverse, brake. The problem appears after ~60–90 minutes: to create genuinely different reasoning, the concept increasingly depends on persistence/synchronization/phase rules rather than the pure shared-shaft verb.

By hour 2 it can still be fun, but hour-10 breadth relies on exactly the kind of load-band/resource topology already frozen for Tension Budget.

## 5.5 Content/solver burden
Discrete solver is manageable. Compiler would validate clutch membership, derived band, device family transitions and known solutions. Technically this finalist is safe.

That is not enough: production efficiency cannot outweigh portfolio duplication.

## 5.6 One-week gate if ever revived
Prototype only if a future factory cycle can state an hour-10 repeated question that is not representable as allocation of one shared conserved/banded mechanical quantity among loads. If five mature grayboxes can be abstracted to `shared budget -> attach loads -> hit bands`, kill immediately.

## 5.7 Direct portfolio-distance test vs Tension Budget
Tension Budget frozen identity already includes:
- one local physical tension carriage;
- 3–5 snap bands;
- 2–4 active loads;
- one fixed conserved budget;
- deterministic authored distribution paths;
- causal puzzle play around which loads share the available physical condition.

Common Shaft changes rope/tension into shaft speed/coupling, but its strongest mature skeletons still reduce to:
`select active loads -> shared physical state changes -> each attached load receives a band -> preserve/alter downstream states`.

Direction and synchronization add flavor, but not enough to justify spending Game #006 on a near-neighbor when Stitchspace, Signal in Flight and The Short Circuit are much more portfolio-independent.

**PORTFOLIO DISTANCE: FAIL.**

**RUN-2 RESULT: CUT TO RESERVE.** Good standalone concept, wrong choice for this portfolio immediately after Tension Budget.

---

# 6. Cross-finalist comparison after falsification

Scale 1–10, higher is better. `Implementation predictability` = lower schedule risk.

| Criterion | Stitchspace | Signal in Flight | The Short Circuit | Common Shaft |
|---|---:|---:|---:|---:|
| 10-second mute hook | 9 | 9 | **10** | 9 |
| Exact repeated-verb distinction | **9** | 9 | 9 | 7 |
| Hour-10 depth without new verbs | **9** | **9** | 8 | 7 |
| Controller viability | 9 | 8 | 9 | **10** |
| Graybox falsifiability | **10** | 9 | **10** | **10** |
| Small-team asset efficiency | **10** | 10 | 9 | 9 |
| UI/readability risk | 7 | 6 | 8 | **9** |
| Solver/content QA manageability | 8 | 6 | 8 | 8 |
| Market-comparison resilience | 7 | 8 | **9** | 6 |
| Portfolio independence | **10** | **10** | 9 | **4** |
| First-20-minute escalation | 9 | 9 | **10** | 9 |
| Demo proves full hook | 9 | 9 | **10** | 9 |
| **Total /120** | **106** | **102** | **109** | **97** |

The raw total does not choose a winner. The Short Circuit scores extremely well on clip/demo/falsifiability but still has the largest content-exhaustion question. Stitchspace has the best systemic topology depth/scope ratio but a serious Portal/folding communication tax. Signal in Flight has the clearest hour-10 transformation and strongest portfolio distance but the hardest UI/solver burden.

---

# 7. Final three after Run 2

## A — G6C01 STITCHSPACE
**Advance.** Best scope/depth ratio and strongest discrete solver-friendly systemic structure. Must prove in final selection that adjacency replacement/disconnection is commercially legible enough to overcome portal/folding comparisons.

## B — G6C03 SIGNAL IN FLIGHT
**Advance.** Best temporal reasoning transformation and exceptional portfolio independence. Must prove four-pulse readability and that authored execution editing is more pleasurable than watching signals crawl.

## C — G6C05 THE SHORT CIRCUIT
**Advance.** Best surprise fantasy and strongest 10-second commercial beat. Must prove 4 fallback families generate enough mature causal variety without turning into either ordinary circuit work or repeated `trip breaker -> thing drops` cases.

## Reserve — G6C08 COMMON SHAFT
**Cut from final three due portfolio collision.** Standalone quality remains high, but mature abstraction overlaps too closely with Tension Budget's shared banded physical-resource/load reasoning. Preserve as a future reserve only after sufficient portfolio distance or a genuinely different mutation.

---

# 8. Phase-2 state after Run 2

Phase 2 is **not complete**. No Game #006 winner is selected.

The three finalists are now explicit enough for one true **Final Selection Duel** rather than another broad scoring round.

## NEXT ACTION — PHASE 2 RUN 3 FINAL SELECTION DUEL
For Stitchspace, Signal in Flight and The Short Circuit:
1. freeze one exact one-sentence Steam pitch and 10-second mute trailer beat;
2. write exact first 20 minutes and first two hours at product pacing level;
3. define minimum shippable commercial scope and plausible first-clear duration;
4. perform a final current market/analogue check on the exact frozen mechanic wording;
5. define content-production throughput and validation-tooling plan;
6. define perceived-value and likely negative Steam review case;
7. compare implementation schedule risk under the same solo/small-team assumption;
8. define one-week prototype plan and binary decision using measurable thresholds;
9. explicitly compare `why this game, why now, why not the other two`;
10. select exactly one Game #006 winner **only if evidence is decisive**. If not, document a two-prototype duel with explicit reason.

Only after that selection may Phase 3 Product Thesis Lock begin.
