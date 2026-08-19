# GAME #003 — BORROWED COLLISION — MECHANICAL ARCHITECTURE

Last updated: 2026-08-19
Factory run: **8**
Phase: **4 — Mechanical Architecture**
Product thesis: **LOCKED**
DESIGN COMPLETE: **NO**

This file is the canonical Phase-4 mechanical specification for Borrowed Collision. It converts the Product Thesis into deterministic rules for authoritative body state, collision resolution, impact harvesting, token lineage, receiver compatibility, converters, self-launch, moving-body timing, objectives, recovery, history and causal ancestry. Production implementation is not started here.

When this file conflicts with a tournament example, this file wins unless Phase 4 is explicitly reopened. `GAME3_PRODUCT_THESIS.md` remains authoritative for product identity and scope ceilings.

---

# 1. Mechanical contract

The non-negotiable invariant is:

> **A resolved physical consequence becomes a portable resource, and the world-state that created and receives that consequence must continue to matter.**

Borrowed Collision is not a continuous rigid-body sandbox. It is a stylized deterministic causal puzzle in which moving bodies use discrete motion classes and authored collision relations. Every important result must be reproducible from canonical state without frame timing, floating-point contact order, free-angle aiming or hidden randomness.

Player reasoning must primarily concern:
- where a useful collision comes from;
- what that collision does to its donor world-state;
- the harvested impact's direction and magnitude band;
- how fixed physical devices can transform it;
- which receiver can safely/usefully accept it;
- what receiver aftermath creates next;
- whether an impact is better spent on self, cargo or environment;
- whether a secondary collision creates a more valuable future consequence.

---

# 2. Authoritative state model

A case owns one immutable `CaseDefinition` and one mutable `CaseState`.

## 2.1 Stable identity

Every body, capture source, receiver socket, converter, damper, route node, objective, invariant and impact lineage has a stable ID.

Names, art variants and display labels are never identity.

## 2.2 Canonical body state

Each body has:
- `body_id`;
- `body_family` from the reusable body/receiver registry;
- `location_id` on an authored lane/node/collision-boundary graph;
- `motion_direction` in `{N, NE, E, SE, S, SW, W, NW, NONE}`;
- `motion_band` in `{ZERO, WEAK, MEDIUM, STRONG}`;
- `mass_class` in `{LIGHT, STANDARD, HEAVY}`;
- `durability_class` where relevant;
- explicit boolean/status flags such as `BROKEN`, `OPEN`, `LATCHED`, `SPENT`, `CAPTURE_ARMED`, `SETTLED`;
- optional authored receiver/source tags;
- active lineage reference if its current motion arose from a spent portable impact or prior collision.

No canonical body exists between authored collision boundaries. Presentation may animate between boundaries, but the domain state advances boundary-to-boundary.

## 2.3 Motion graph

Cases use authored motion lanes and collision boundaries rather than unrestricted free-space simulation.

A lane defines:
- start boundary/node;
- end boundary/node;
- legal direction(s);
- body-class compatibility;
- optional one-way state;
- optional crossing/occupancy relation;
- presentation path only as non-authoritative geometry.

Bodies travel one logical lane segment per movement step unless a family rule says they settle earlier.

This allows curved-looking rails, ramps, falls or cart tracks in presentation while preserving deterministic state transitions.

## 2.4 Portable impact state

A portable impact contains exactly:
- `impact_id`;
- `direction` — one of 8 compass directions;
- `magnitude_band` — WEAK / MEDIUM / STRONG;
- `source_lineage_id`;
- `source_event_id`;
- `transform_history[]` for causal explanation;
- `availability_state` in `{WORLD_PICKUP, HELD, STORED, IN_TRANSFORM, CONSUMED}`.

Portable impacts do **not** contain:
- numeric force;
- velocity components;
- elemental type;
- rarity;
- durability;
- arbitrary modifiers.

## 2.5 Player inventory

Baseline portable-impact capacity: **2**.

Absolute 1.0 late-game ceiling: **3**.

Inventory is ordered only for player selection convenience; order has no mechanical effect.

If capacity is full, a new harvestable impact remains as a world pickup at its capture point until capacity exists, unless the capture source definition explicitly says `AUTO_DISCARD_AFTER_RESOLUTION = YES`. Base campaign default is **NO auto-discard**.

A world pickup does not block movement unless its authored presentation object occupies a non-gameplay overlay; it is not a physical body.

---

# 3. Direction and magnitude semantics

## 3.1 Direction

Direction is always one of 8 compass directions.

Opposites:
- N <-> S
- NE <-> SW
- E <-> W
- SE <-> NW

Quarter-turn clockwise:
- N->E->S->W->N
- NE->SE->SW->NW->NE

Quarter-turn counterclockwise is the inverse.

Mirror transforms are authored with a visible axis:
- horizontal mirror: N/S unchanged; E<->W; NE<->NW; SE<->SW;
- vertical mirror: E/W unchanged; N<->S; NE<->SE; NW<->SW.

No arbitrary 45-degree/free rotation is allowed unless using another canonical fixed transform device explicitly visible in the room; Phase 4 does not define such a fifth transform family.

## 3.2 Magnitude bands

Magnitude is categorical:
- WEAK
- MEDIUM
- STRONG

The player never needs numeric values.

Band order matters only where a rule explicitly compares strength. STRONG is not universally beneficial.

## 3.3 Damper

A damper changes magnitude exactly one band downward:
- STRONG -> MEDIUM
- MEDIUM -> WEAK
- WEAK -> WEAK

A damper never increases magnitude.

Passing an already-WEAK impact through a damper is legal but produces WEAK. Content should avoid requiring pointless damping unless the route itself matters.

---

# 4. Deterministic collision resolution

## 4.1 Collision event eligibility

A collision occurs when one or more active bodies enter the same authored collision boundary relation during the same movement step, or when a moving body reaches an anchored collision surface/body.

Collision topology is authored; presentation geometry does not create accidental contacts.

## 4.2 Collision input tuple

Resolution uses only canonical values:
- body A mass class;
- body A incoming direction/band;
- body B mass class;
- body B incoming direction/band or anchored state;
- authored collision relation type;
- explicit body-family collision tags.

No frame delta, interpolation velocity or animation location is consulted.

## 4.3 Collision output

Every collision table entry returns a deterministic `CollisionOutcome` containing:
- post-collision motion direction/band for each involved body;
- settle/break/latch/open/trigger flags;
- zero or one **harvestable impact output** for the collision relation unless an explicit chain-source family allows a different bounded rule;
- causal parent references;
- optional generated secondary world-state event.

The harvestable impact is based on the **resolved transferred consequence**, not raw incoming velocity.

## 4.4 Canonical baseline table semantics

The exact content-facing collision table is data-driven but must obey these global semantics:

### Moving body into anchored ordinary receiver
- receiver remains at its authored position unless its family is movable;
- moving body normally settles or rebounds according to relation;
- emitted impact direction is the direction of transferred consequence into the receiver;
- emitted magnitude is derived by the mass/band lookup.

### Moving movable body into settled movable body
- outcome depends on relative direction and mass classes;
- identical canonical tuple always yields identical output;
- no hidden restitution coefficient exists.

### Head-on simultaneous collision
If bodies approach the same boundary from opposite lanes in the same step, resolve as one multi-body collision event using the simultaneous table, not sequential low-ID impacts.

### Same-direction rear collision
If a faster/higher-band body reaches a slower body at a shared boundary, use the rear-collision table. Stable IDs do not decide physics except as a final tie-break when two otherwise identical optional consequences require ordering.

## 4.5 Harvestable impact derivation

The output band uses a small table based on source movement band and mass relationship. Phase-5 content may choose exact authored donor setups, but implementation may not improvise per-case exceptions.

Canonical default transfer table for one moving body into an anchored STANDARD capture surface:
- LIGHT + WEAK -> WEAK
- LIGHT + MEDIUM -> WEAK
- LIGHT + STRONG -> MEDIUM
- STANDARD + WEAK -> WEAK
- STANDARD + MEDIUM -> MEDIUM
- STANDARD + STRONG -> STRONG
- HEAVY + WEAK -> MEDIUM
- HEAVY + MEDIUM -> STRONG
- HEAVY + STRONG -> STRONG

Other mass-pair relations compile from the same bounded lookup registry. Content must not require players to compute mass multiplication. The resulting band is previewable/inspectable after collision and learned through repeated consistent visual rules.

The first campaign cases should use obvious standard-body donors; unusual mass interactions belong later.

---

# 5. Collision transaction ordering

One accepted player action that starts or applies motion creates one deterministic `ResolutionTransaction`.

Observable order:

1. **Command validation** — verify receiver/source/action legality and exact pre-state.
2. **Authoritative action commit** — consume/spend/trigger exactly the selected action.
3. **Movement intent build** — all active bodies compute next boundary intent from the same start-of-step state.
4. **Simultaneous conflict grouping** — collisions sharing a boundary/time-step are grouped before mutation.
5. **Collision resolution** — groups resolve in deterministic authored boundary order, with independent groups allowed to resolve conceptually simultaneously.
6. **Body-state apply** — post-collision positions/motion/status commit.
7. **Harvest-output emission** — eligible collision output creates one lineage-bound portable impact pickup if not already harvested.
8. **Receiver/world triggers** — switches, doors, breakage, latches and authored non-motion consequences update.
9. **Objective/invariant evaluation** — current case state recalculates.
10. **Chain continuation** — if active moving bodies remain, repeat steps 3–9 for the next bounded movement step.
11. **Settle / chain termination** — when no bodies are active or a hard chain ceiling is reached.
12. **Presentation release** — control returns; causal chain remains inspectable.

No player input changes an already-running transaction except explicit Pause/Step presentation controls defined below.

---

# 6. Lineage and one-harvest rule

## 6.1 Collision lineage

Every harvest-eligible collision event gets a stable `collision_lineage_id` derived from:
- case/session lineage namespace;
- causal parent event lineage;
- donor source state generation;
- collision event ordinal within that generation.

Exact encoding is technical implementation work; semantics are frozen here.

## 6.2 One harvest per lineage

One collision lineage may create at most one portable impact output.

Once its output has been emitted, that lineage is `HARVEST_EMITTED` even if the pickup is not immediately collected.

Repeated UI interaction, pause/step, animation replay, leaving/re-entering the room, save/load or duplicate commands may not emit another impact from the same lineage.

## 6.3 Undo

Undo restores the exact earlier canonical checkpoint, including lineage generation and harvest state. Therefore Undo may legitimately return the world to a state before a collision existed; re-performing the collision then creates the corresponding restored lineage again as part of the restored history branch. This is not duplication because the later branch no longer exists canonically.

## 6.4 Donor regeneration classes

Every donor/capture source is exactly one of:

### EXHAUSTIBLE
After its defining collision/state is consumed, it cannot be recreated within the current case except by Undo/Restart.

### RESETTABLE
A visible authored reset action/state can recreate the donor generation. Reset increments the donor generation, so a new collision can legitimately emit a new lineage.

Reset must have a meaningful world consequence or route requirement; a free button next to a strong donor is invalid mature content.

### CYCLIC_WEAK
A visible system repeatedly generates a WEAK donor as part of case grammar. This is allowed only when renewable weak output is explicitly intended and cannot be escalated into an accidental infinite strong-token factory.

### CHAIN_GENERATED
A collision caused by a spent portable impact creates a new donor event. Its lineage includes the spent token/source ancestry.

No hidden fourth/fifth regeneration model is allowed without Phase-4 reopen.

---

# 7. Harvest legality and pickup semantics

A collision output is harvestable only if:
- collision relation is capture-enabled;
- lineage has not emitted before;
- output band is not ZERO;
- source is not marked `NON_HARVESTABLE` by a reusable family rule;
- case is not already in terminal completion transition.

The player does not need frame-timed button presses to capture a collision.

Default capture model:
- eligible collision automatically condenses its output into a stable world pickup;
- player collects it later through ordinary interact/focus action;
- optional visual `catch` animation is presentation only.

This replaces the tournament's ambiguous “standing in capture zone” idea and removes reflex capture as a baseline requirement.

---

# 8. Spending legality

A portable impact can be spent only on a compatible **impact receiver**.

Every receiver declares:
- `receiver_family`;
- valid incoming snap directions;
- accepted magnitude bands;
- current enabled/disabled state;
- whether receiver can accept while moving;
- resulting body/world action;
- whether oversize impact causes breakage/overshoot;
- whether undersize impact produces a harmless partial/no-op legal result.

## 8.1 Legal-but-bad spends

A spend is structurally legal if the receiver accepts that direction/band according to its visible rules, even if it creates an undesirable result.

Examples:
- STRONG breaks a fragile actuator;
- WEAK moves a cart only one segment and strands it;
- correct direction launches the player into a dead-end.

These spends commit and can be undone.

## 8.2 Structurally illegal spends

Rejected before consumption:
- receiver incompatible with impact input at all;
- direction not in receiver's authored snap set;
- receiver currently disabled/blocked and its rule says it cannot receive;
- trying to spend same consumed impact twice;
- trying to target a body not exposed as an impact receiver;
- stale command against changed state.

Rejected spend leaves impact and world byte/semantically unchanged.

## 8.3 Moving receivers

A moving receiver may accept an impact only at authored `receive_windows` tied to canonical movement-step states, never interpolation timing.

Pause/Step can reveal these states. No frame-perfect hit is required.

---

# 9. Reusable receiver / device families

Phase 4 freezes a ceiling of **8 mechanical families**. Phase 5 may theme them but may not create bespoke physics scripts per case.

## R1 — Ordinary Mover
Accepts allowed impact; moves body along compatible authored lane according to direction/band. May settle at first boundary or continue by family rule.

## R2 — Fragile Receiver
Has visible safe-band set. An excessive accepted band causes `BROKEN`. Breakage is persistent until Undo/Restart or an explicitly visible reusable repair rule; base campaign should rarely add repairs because they can dilute consequence.

## R3 — Band-Window Mechanism
Responds only usefully to a declared band/set. An accepted wrong band may fail harmlessly or overshoot according to visible family semantics.

## R4 — Converter Socket
Receives a portable impact as an item transformation, not as body motion. Applies exactly one fixed direction operation: quarter-turn, reverse or mirror. Does not change lineage identity; appends transform history. It does not consume the impact except while `IN_TRANSFORM`, then returns transformed impact.

## R5 — Damper
Transforms magnitude down one band and preserves direction/lineage. Same non-consumptive item-device semantics as converter.

## R6 — Self-Launch Receiver
Applies impact to player traversal state using authored launch lane. Direction/band selects from visible legal self-launch outcomes. Player becomes a moving body for the bounded transaction.

## R7 — Chain-Producing Body
When moved/struck, can collide at another authored boundary and create a new harvestable lineage according to ordinary collision rules. It is not a magic token duplicator; the new token exists only if a real secondary collision occurs.

## R8 — Anchored Trigger / Impact Door
Receives impact without moving as a body and changes one visible state such as OPEN/LATCHED/ACTIVATED. May have band/direction requirements and may itself be fragile if themed through R2-compatible composition.

Families may be composed only where their combined rule remains visible and data-driven. A body should normally expose at most two relevant family semantics at once.

---

# 10. Converter-chain rules

A portable impact may pass through multiple converter/damper devices before spending.

Rules:
- transform chain may not branch or duplicate one impact;
- lineage remains the same source lineage;
- transform history records each device in order;
- converter/damper is deterministic and non-random;
- no transform increases magnitude;
- transform graph may contain loops physically, but applying a loop repeatedly is just repeated deterministic transformation and cannot create extra impacts;
- content validation must reject a required solution whose only difficulty is tedious repeated converter cycling with no world-state consequence.

A transformed impact remains one inventory/world item.

---

# 11. Self-launch semantics

The player can be a receiver through explicit self-launch sockets/stances.

## 11.1 Launch

Spending an impact on self:
1. consumes portable impact;
2. records source lineage parent;
3. sets player motion direction/band to the receiver's visible authored launch mapping;
4. runs player as an ordinary moving body through the bounded movement/collision transaction;
5. on safe landing, player settles at authored node;
6. on collision with a capture-enabled landing surface/body, the landing collision may create a **new chain-generated impact lineage** under ordinary collision rules.

Thus the same impact cannot survive self-launch and also be harvested again; only a genuinely new landing collision can produce another impact.

## 11.2 Self-launch failure

A legal launch may:
- land safely;
- overshoot to a bad node;
- break a fragile landing object;
- create a trapped/dead-end case state;
- generate a useful secondary impact.

No health/combat damage system is introduced. If a launch would conceptually be fatal, presentation uses a stylized local failure/reset state rather than health simulation.

## 11.3 Self-launch into donor

If player collides with a donor/capture surface, resolve exactly as any other body collision. If capture-eligible, a new lineage can emit. The player's source launch impact is already consumed and remains an ancestor, preventing duplication ambiguity.

---

# 12. Time model and moving-body states

Borrowed Collision uses discrete deterministic **movement steps**, not real-time gameplay truth.

The player may inspect indefinitely while no transaction is running.

## 12.1 Running transaction

During a movement chain:
- domain advances in discrete steps until settled;
- presentation may animate at normal/fast/reduced speed;
- player cannot alter receivers/tokens mid-step unless a future explicitly authored mechanic reopens Phase 4; 1.0 baseline has no mid-flight editing.

## 12.2 Pause and Step

Pause/Step are presentation/accessibility controls over transaction reveal.

Canonical outcome is already determined by the committed action and start state. `Step` reveals one canonical movement/collision step at a time; it does not allow new commands between steps.

Therefore pause/step cannot be exploited to change collision outcomes.

## 12.3 Chain ceiling

Every case declares `max_resolution_steps`, default 12, hard 1.0 ceiling **24**.

Content validation must prove known valid solutions settle below the ceiling.

If a transaction reaches the ceiling with active motion, this is a content/implementation error in valid shipped content, not an ordinary player fail. Debug/validation must reject chain loops before shipping.

---

# 13. Simultaneous collisions

## 13.1 Independent collisions same step

If two collision groups occur at different boundaries and share no body, resolve from the same pre-step snapshot. Their world-state outputs are applied together before objective evaluation.

Presentation may order them by stable boundary ID but that order cannot affect result.

## 13.2 Shared-body conflict

If one body is claimed by multiple collision relations in the same step, the case topology must define one canonical multi-body collision group. The domain resolves the whole group with one deterministic table entry.

Content with an unregistered ambiguous multi-contact state is invalid and must fail validation.

## 13.3 Two harvest outputs same step

Independent collision groups may each emit one portable impact pickup in the same step. Inventory capacity does not suppress creation because outputs appear as world pickups. The player can collect them later.

---

# 14. Fragility and breakage

Fragile state exists to make stronger-not-better intrinsic.

Rules:
- fragile receivers display safe/unsafe bands before spend once the family has been taught;
- excessive accepted impact commits and causes `BROKEN`;
- broken object remains in canonical world state and may alter routes/objectives;
- ordinary baseline has no hidden durability points;
- breakage is binary unless Phase 4 is explicitly reopened;
- no random break chance;
- Undo restores exact pre-break state.

If breakage creates a dead end with no remaining legal recovery, the UI may flag `Case cannot currently be completed` after deterministic proof or authored dead-end condition, but it must still allow Undo/Restart.

---

# 15. Objectives and protected invariants

All case requirements are deterministic predicates over canonical state.

Phase-4 objective families:

## O1 — Body Position / Delivery
Specified body/player/cargo ends at required node/zone.

## O2 — Mechanism State
Door/latch/switch/receiver reaches OPEN/ACTIVE/other authored binary state.

## O3 — Preservation
Specified fragile/protected body remains unbroken / unmoved / within allowed state.

## O4 — Donor Preservation
Specified donor remains available/unspent at completion.

## O5 — Impact Availability / Reservation
A particular lineage class or at least one impact of declared band/direction remains available at completion only when narratively/mechanically meaningful. Do not turn inventory retention into arbitrary checklisting.

## O6 — Causal Chain Requirement
Completion state proves a specified receiver/result was reached through an actual secondary collision/lineage relation, used sparingly when chain creation is the lesson.

## O7 — Multi-Object Final State
Several bodies/mechanisms satisfy final states simultaneously.

## O8 — Safe Band / No Overshoot
A receiver must reach target state without break/overshoot; this is normally represented as O2 + O3 rather than a hidden scoring rule.

## O9 — Traversal / Self Position
Player must reach exit/inspection position using canonical traversal including self-launch where relevant.

## O10 — Final Causal Compression Mastery
Optional mastery only: satisfy baseline while using a bounded count of final harvested/spent lineages or preserving an extra donor. Raw Undo/history is never scored.

Phase 5 may package these into themed case requests but should not invent new machine predicate families casually.

---

# 16. Completion, temporary failure and dead ends

## 16.1 Baseline completion

A case completes when:
- every required objective is true;
- every protected invariant is true;
- no active movement transaction remains;
- player is in a legal settled state;
- no required unresolved impact transformation is pending.

## 16.2 Temporary failure

A legal bad action normally leaves the case active in an unsatisfied state.

Examples:
- cart overshot switch;
- strong token broke fragile actuator;
- player launched to wrong platform;
- scarce donor was exhausted too early.

The game should explain the resulting state; it does not immediately force restart.

## 16.3 Proven dead end

A dead end may be declared only if:
- an authored terminal flag was triggered, or
- deterministic state analysis can prove no baseline completion remains under current finite state.

The player still chooses Undo/Restart. Dead-end detection is a convenience, not a punishment.

## 16.4 Reset

Restart restores exact canonical initial state and clears current history branch after confirmation if needed.

Donor regeneration through Restart is not an in-world resource action and does not count toward mastery.

---

# 17. Undo / Redo / history semantics

Undo is exact checkpoint restoration.

## 17.1 History unit

One accepted player command that changes canonical state is one history transaction:
- collect world impact pickup;
- drop/store impact at an authored storage interaction if Phase 5 includes such nodes;
- transform impact through converter/damper;
- spend impact on receiver;
- trigger an authored donor reset action;
- other canonical interact action explicitly defined by content architecture.

Pure inspection/focus/pause animation controls create no history entry.

## 17.2 Movement consequence nesting

One spend/trigger command plus all bounded movement steps, collisions, breakage, new pickups, receiver/world consequences and objective changes caused by it are one atomic history transaction.

Undo restores the exact pre-command state including:
- bodies;
- player location/motion;
- portable-impact inventory/world pickups;
- lineage emission state;
- donor generation state;
- receiver states;
- objectives/invariants;
- causal graph;
- history cursor.

## 17.3 Redo

Redo restores/replays the exact deterministic transaction if history branch is unchanged. New accepted command after Undo truncates redo branch.

## 17.4 No Undo penalty

Raw Undo/Redo count does not affect baseline or mastery.

---

# 18. Causal event ancestry

Every meaningful world change belongs to a directed acyclic causal graph.

Canonical event classes:
1. `PLAYER_COMMAND_COMMITTED`
2. `DONOR_RESET`
3. `BODY_MOTION_STARTED`
4. `BODY_MOVED_STEP`
5. `COLLISION_RESOLVED`
6. `HARVEST_OUTPUT_EMITTED`
7. `IMPACT_PICKED_UP`
8. `IMPACT_TRANSFORMED`
9. `IMPACT_SPENT`
10. `RECEIVER_STATE_CHANGED`
11. `BODY_BROKEN`
12. `SECONDARY_COLLISION_CREATED`
13. `OBJECTIVE_CHANGED`
14. `INVARIANT_CHANGED`
15. `CASE_COMPLETED`

Every event stores stable subject IDs, before/after facts and ordered material parent IDs.

The minimum explanation chain the UX must be able to present is:

`donor collision -> harvested impact -> transform(s) -> spend -> receiver motion/state -> secondary collision(s) -> objective/invariant result`.

If a secondary impact is later spent, ancestry can traverse multiple generations back to the original donor.

The UX need not show every movement-step bookkeeping event; material ancestry may collapse identical lane-step events.

---

# 19. Anti-dominant-strategy architecture

## 19.1 Anti-max-force

STRONG is not a universal upgrade because reusable rules create costs:
- fragile breakage;
- band-window receivers;
- overshoot on movers;
- strong donor exhaustion;
- dampers consume route/opportunity position;
- some desirable secondary collisions exist only from weaker outcomes.

Content validation must flag mature case families where always selecting the strongest available impact is a winning default.

## 19.2 Anti-donor-factory

Every donor has a regeneration class. Mature content rejects accidental zero-cost repeatable strong sources.

A RESETTABLE strong donor is valid only if reset changes position/state, consumes another scarce world opportunity, or requires a meaningful traversal/action sequence.

## 19.3 Anti-token-permutation

Receivers expose legal snap directions and known family rules; difficulty should not be guessing compatibility.

Mature cases must make at least two of these matter:
- donor preservation;
- receiver aftermath;
- future donor creation;
- converter topology;
- magnitude suitability;
- self versus environment allocation;
- route/traversal consequences;
- inventory capacity/order.

If a case can be solved as detached matching among visible arrows/sockets while world provenance is irrelevant, it fails content review.

## 19.4 Multiple valid solutions

Baseline objectives accept any canonical final state satisfying requirements. No hidden exact designer map/sequence is required unless the case is an explicit teaching micro-case and even then the rule must be visible.

---

# 20. Balancing knobs

Primary knobs:
- number of active bodies;
- number of donors and regeneration classes;
- donor output direction/band;
- number of portable impacts simultaneously available;
- inventory cap 2/3;
- converter topology and orientation;
- receiver accepted directions;
- receiver safe/useful magnitude sets;
- fragile object placement;
- lane connectivity;
- moving receiver windows in canonical steps;
- chain depth;
- number of simultaneous objectives/invariants;
- self-launch availability;
- reset action cost/topology;
- whether secondary collisions are harvestable;
- mastery final-lineage/harvest/preservation thresholds.

Difficulty should rise through **causal distance, ordering pressure and interaction density**, not finer angles, faster reactions, hidden physics or larger inventories.

---

# 21. Phase-5 authoring constraints inherited from mechanics

Content architecture must obey:
- every moving/collision state is representable on the authored graph;
- every possible multi-contact state has a canonical collision entry or is structurally impossible;
- every donor has one explicit regeneration class;
- every harvest output has one lineage;
- every receiver uses R1–R8 family semantics or documented composition of at most two;
- every transform uses quarter-turn/reverse/mirror/damper only;
- no required free-angle aim;
- no required mid-flight player command;
- known valid solutions settle under `max_resolution_steps <=24`;
- mature cases should normally require provenance/world-state reasoning beyond token shape;
- no accidental strong-token factory;
- no chain loop that can run indefinitely;
- no mastery scoring raw experimentation;
- no case-specific script that silently changes collision tables.

---

# 22. Key edge-case decisions

## E1 — Two collisions same beat
Independent groups resolve from same step snapshot; shared-body contacts require one canonical multi-body table entry.

## E2 — Source already harvested
Same lineage emits no second pickup. Collection state does not reset emission.

## E3 — Inventory full at harvest
Impact remains stable world pickup by default; it is not lost or duplicated.

## E4 — Token spent on moving receiver
Allowed only during authored receive-window canonical state; no interpolation timing. Otherwise structurally rejected before token consumption.

## E5 — Converter chain
One impact remains one item. Transforms append history; no duplication; loops are deterministic and cannot increase magnitude.

## E6 — Fragile breakage
Breakage is binary, deterministic and persistent on current branch. Undo/Restart restores.

## E7 — Self-launch into donor
Player collision is ordinary collision. New landing impact may emit with new chain lineage; original spent token stays consumed.

## E8 — Secondary collision creates same direction/band as parent
Still a distinct impact because lineage/event is distinct. It is not considered duplication if a real new collision occurred.

## E9 — Chain loop
Shippable content must validate that no reachable transaction exceeds chain ceiling. If loop appears in authored state search, case fails validation.

## E10 — Reset while bodies active
Not allowed. Restart/Undo/domain-changing reset command can execute only when current movement transaction is settled. Pause is presentation-only and does not make state editable.

## E11 — Collect pickup while another identical-looking impact is held
Legal if capacity exists. IDs/lineage remain distinct even if direction/band visuals match.

## E12 — Drop impacts
Baseline inventory does not support arbitrary floor dropping because this adds logistics clutter and duplication edge cases. Phase 5 may define rare authored storage sockets, but free drop-anywhere is out of scope.

## E13 — Receiver consumes weak impact but does nothing useful
If family rules visibly accept WEAK, this is a legal bad spend and token is consumed. If WEAK is incompatible, reject before consumption. Family presentation must distinguish these states.

## E14 — Broken receiver later hit again
Broken objects use a visible inert/broken rule. They do not secretly repair, produce new effects or become infinite donors unless their reusable family explicitly defines a post-break collision relation.

## E15 — Case completes while uncollected impacts remain
Allowed unless an objective explicitly concerns them. Completion does not require cleaning inventory/world pickups.

---

# 23. Mechanical acceptance tests

## State / identity
- **M4-01** Every canonical body/object has stable identity independent of art/name.
- **M4-02** Presentation interpolation coordinates cannot alter collision result.
- **M4-03** Same canonical initial state + same commands produces identical final body state.

## Direction / magnitude
- **M4-04** All impacts resolve to exactly one of 8 directions and 3 nonzero bands.
- **M4-05** Quarter-turn, reverse, horizontal mirror and vertical mirror mappings are deterministic.
- **M4-06** Damper maps STRONG->MEDIUM, MEDIUM->WEAK, WEAK->WEAK and never increases band.

## Collision
- **M4-07** Same collision input tuple yields identical `CollisionOutcome` across repeated runs.
- **M4-08** Collision output uses resolved consequence rather than raw presentation velocity.
- **M4-09** Head-on same-step collision is resolved as one simultaneous group, not sequentially by body ID.
- **M4-10** Independent same-step collisions cannot affect each other's result through processing order.
- **M4-11** Ambiguous unregistered multi-contact content is rejected before play.

## Harvest / lineage
- **M4-12** Eligible collision lineage emits at most one portable impact.
- **M4-13** Replaying animation/pause/load without state rollback cannot emit duplicate impact.
- **M4-14** Undo to pre-collision checkpoint restores lineage state exactly and allows legitimate re-execution on restored branch.
- **M4-15** EXHAUSTIBLE donor cannot regenerate without Undo/Restart.
- **M4-16** RESETTABLE donor creates new generation only through its visible reset rule.
- **M4-17** CYCLIC_WEAK source cannot accidentally escalate into infinite strong output under canonical transforms.
- **M4-18** Full inventory does not suppress/duplicate output; pickup remains in world by default.

## Spend / receivers
- **M4-19** Structurally illegal spend consumes no token and mutates no world state.
- **M4-20** Legal harmful spend commits and can break/overshoot/fail objectives.
- **M4-21** Moving receiver accepts only at authored canonical receive-window state, never frame interpolation.
- **M4-22** Converter/damper preserves source lineage and cannot duplicate impact.
- **M4-23** Receiver family behavior is data-driven from R1–R8, not dossier-specific hidden script.

## Self-launch / chains
- **M4-24** Self-launch consumes source impact before motion begins.
- **M4-25** Landing collision may create a new impact only as a distinct collision lineage.
- **M4-26** Source impact cannot survive self-launch and also be harvested as itself.
- **M4-27** Secondary collision ancestry links back through spent impact to source donor.
- **M4-28** Known valid case transactions settle below hard 24-step ceiling.
- **M4-29** Reachable infinite motion/collision loops fail content validation.

## History / recovery
- **M4-30** One spend command plus all resulting movement/collisions is one atomic history transaction.
- **M4-31** Undo restores exact bodies, impacts, lineage, donors, receivers, objectives and causal graph.
- **M4-32** Redo reproduces exact post-state on intact branch.
- **M4-33** New command after Undo truncates redo branch without affecting restored state.
- **M4-34** Pause/Step does not change canonical outcome or permit mid-transaction edits.

## Objectives / anti-exploit
- **M4-35** Baseline completion never depends on raw Undo count.
- **M4-36** Multiple valid final states are accepted when predicates are satisfied.
- **M4-37** Mature content validation can identify accidental zero-cost repeatable strong donor loops.
- **M4-38** Mature content review explicitly checks strongest-impact dominance.
- **M4-39** Mature case cannot be approved if provenance/world-state is irrelevant and play reduces to detached token matching.

## Accessibility determinism
- **M4-40** Mouse+keyboard, keyboard-only and controller-only can select impact, receiver and valid orientation without free-angle aim.
- **M4-41** Direction/magnitude can be identified without color or audio.
- **M4-42** Reduced motion/presentation speed does not alter domain result.

---

# 24. Internal coherence review

## Quantized rules versus physics fantasy
Resolved: the world is intentionally stylized causal physics. Authored lanes/boundaries and categorical bands are part of the fiction/presentation language. The game does not promise realistic rigid-body simulation.

## Collision harvesting versus ammo
Resolved by mandatory lineage, finite donor generations, receiver aftermath and content rejection if provenance is irrelevant.

## Stronger force versus progression
Resolved: magnitude is suitability, not power progression. Fragility, overshoot and band windows make STRONG situational.

## Self-launch versus platformer identity
Resolved: self-launch is one receiver use of the same portable-impact grammar, not a separate dexterity system. No free-angle or reflex requirement.

## Free Undo versus donor scarcity
Resolved: scarcity matters inside the current branch; Undo remains learning/recovery. Mastery judges final causal result, not experimentation history.

## Pause/step versus moving receivers
Resolved: receive windows are canonical step states and player cannot inject commands mid-transaction. Pause/step reveals reasoning but cannot alter outcome.

## Chain generation versus duplication
Resolved: each genuinely new collision gets distinct lineage; an impact cannot copy itself without a new physical collision event.

---

# 25. Open empirical gates carried forward

These are prototype/playtest obligations, not undefined rules:
1. <=20% ordinary failures primarily from direction/magnitude misunderstanding.
2. strongest available impact is not chosen at every meaningful decision in >=50% of mature successful solutions.
3. blind token permutation remains below ~35% of mature successful actions.
4. majority of testers can explain donor -> impact -> transform -> receiver -> secondary collision without numeric vectors.
5. players describe impacts as stored/reused collision consequences rather than generic ammo/arrows.
6. categorical collision rules feel predictable enough despite intentionally non-realistic physics.
7. self-launch feels integrated rather than an awkward secondary platforming mode.

Failure of these gates during implementation may require the smallest canonical amendment, but does not justify expanding to continuous physics by default.

---

# 26. Phase-4 closure decision

- Authoritative body/world state: **DEFINED**
- Stable identity: **DEFINED**
- 8-direction × 3-band semantics: **DEFINED**
- Collision input/output and ordering: **DEFINED**
- Harvest derivation: **DEFINED**
- Lineage / one-harvest / duplication prevention: **DEFINED**
- Donor regeneration classes: **DEFINED — 4 classes**
- Inventory / pickup / full-capacity behavior: **DEFINED**
- Spend legality / receiver compatibility: **DEFINED**
- Receiver/device families: **DEFINED — R1..R8 ceiling**
- Converter/damper semantics: **DEFINED**
- Self-launch / landing harvest semantics: **DEFINED**
- Moving-body time / pause / step / chain ceiling: **DEFINED**
- Simultaneous collision handling: **DEFINED**
- Objectives/invariants/completion/dead-end recovery: **DEFINED**
- Undo/Redo/history checkpoints: **DEFINED**
- Causal ancestry: **DEFINED**
- Anti-max-force / donor-factory / token-permutation architecture: **DEFINED**
- Balance knobs and Phase-5 authoring constraints: **DEFINED**
- Requested edge cases: **RESOLVED**
- Mechanical acceptance tests: **42**
- Production implementation started: **NO**
- Phase 4 Mechanical Architecture: **COMPLETE ON PAPER**
- DESIGN COMPLETE: **NO**

## NEXT PHASE

**Phase 5 — Content Architecture.**

The next run must define the campaign/content structure without adding mechanics: target case count and acts, exact introduction/recombination order for collision harvesting, magnitude, transforms, donor classes, self-launch, chain generation and moving receivers; canonical case data schema; reusable body/receiver theme families; objective/invariant distribution; multi-room progression; known-solution and content-validation requirements; anti-repetition transformation tags; demo slice; mastery/remix rules and hard 1.0 content ceilings. It must explicitly protect the product from becoming arrow-matching content by requiring provenance/world-state relevance in mature cases.