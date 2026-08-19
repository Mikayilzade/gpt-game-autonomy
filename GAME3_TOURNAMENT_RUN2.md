# GAME #003 — CONCEPT TOURNAMENT — RUN 2 FINALIST FALSIFICATION

Last updated: 2026-08-19
Factory run: **5**
Phase: **2 — Concept Tournament / Finalist Falsification**
Final concept selected: **NO**

This round resumes exactly from `STATUS.md`. It converts the four finalists from attractive product pitches into sufficiently explicit rule systems that their dominant strategies, implementation burden, control grammar and hour-10 evolution can be attacked before any Product Thesis lock.

Fresh market checks were repeated on the refined verbs. They materially confirm two warnings:
- `LeiLei` explicitly steals properties from objects and injects them into others. Single-Pixel Kingdom therefore cannot claim generic property transfer as whitespace; its only defensible center is **the avatar physically carrying state through a route, with donor absence and carrier interference making transport itself the puzzle**.
- circuit/platform precedent remains broad (`Wired`, `ReWire`, current hacking/parkour hybrids such as `R2R: Rewire to Revolt`). No exact current analogue was found for mid-motion conserved-power rewiring as traversal, but Fusebox Parkour's differentiation still lives primarily in feel/input execution rather than a scarce rules concept.
- existing mass games such as `The GoD Unit` reinforce that Bureau of Lost Weight is defensible only as **conserved redistribution**, not generic light/heavy manipulation.
- targeted impulse/collision searches still found action games using impulse and momentum, but no close primary loop where a resolved collision output is harvested as a portable consumable resource and spent elsewhere.

Current references checked 2026-08-19:
- https://store.steampowered.com/app/2920670/LeiLei/
- https://store.steampowered.com/app/885470/Wired/
- https://store.steampowered.com/app/2114100/ReWire/
- https://store.steampowered.com/app/3535160/R2R_Rewire_to_Revolt/
- https://store.steampowered.com/app/1204440/The_God_Unit/
- https://store.steampowered.com/app/1753760/Impulse/
- https://store.steampowered.com/app/811270/Impulsion/

The purpose of these references is market differentiation, not imitation.

---

# 1. Uniform falsification frame

Each finalist must now answer the same implementation-sensitive questions:
1. exact canonical conceptual state;
2. exact repeated command and state transition;
3. deterministic resolution order;
4. 8-scenario graybox packet with expected solution structure;
5. brute-force/dominant-strategy attack;
6. hour-3 and hour-10 depth without expanding the primitive vocabulary;
7. controller grammar;
8. keyboard-only grammar;
9. accessibility consequence;
10. strongest negative Steam review;
11. smallest canonical repair that could answer that review without changing the product into another game;
12. small-team burden and primary kill gate.

A finalist is cut if its strongest defense requires either arbitrary level-specific exceptions or production craftsmanship disproportionate to its product advantage.

---

# 2. G3C15 — BORROWED COLLISION

## 2.1 Canonical conceptual state

The game is built on a bounded 2D deterministic body graph rather than unrestricted continuous rigid-body chaos.

Each body has:
- stable ID;
- position on authored movement lanes/nodes or bounded continuous coordinates snapped at interaction boundaries;
- velocity represented by **8 directions × 3 magnitude bands** (`weak`, `medium`, `strong`), plus `zero`;
- mass class (`light`, `standard`, `heavy`) used only for deterministic collision table lookup;
- receiver tags: `ordinary`, `fragile`, `anchored`, `socket-compatible`, `capture-source`, `player`;
- optional one-bit state such as `spent`, `broken`, `latched`, `opened`.

A harvested impulse token contains only:
- direction: N, NE, E, SE, S, SW, W, NW;
- magnitude: weak / medium / strong;
- source lineage ID for duplication validation;
- consumed/not-consumed.

No numeric vectors are exposed to the player.

## 2.2 Collision resolution

When two moving/anchored bodies collide at an authored collision boundary:
1. identify donor event from the collision table using incoming direction, magnitude and mass classes;
2. resolve ordinary body consequences deterministically;
3. if the collision surface/body is capture-enabled and the event is harvestable, emit exactly one impulse token corresponding to the **resolved outgoing transfer impulse**, not raw pre-collision velocity;
4. mark that collision lineage harvested so rewinding/retriggering without restoring/resetting the donor cannot duplicate the token;
5. update world state;
6. presentation animates the already-decided result.

The player may carry a bounded inventory of **2 impulse tokens baseline, 3 late-game ceiling**. This prevents hoarding from becoming a generic inventory game.

## 2.3 Spending a token

A token can be stamped only onto visible compatible receiver sockets/objects.

Resolution:
1. choose receiver;
2. choose one of its authored valid snap orientations;
3. if a direction-converter socket is used, transform direction by a visible fixed rule (90-degree turn, reverse, mirror); converters never alter magnitude unless explicitly a `damper`;
4. apply impulse deterministically;
5. consume token;
6. run bounded resulting collisions until all active bodies settle or an authored chain ceiling is reached;
7. expose causal chain.

No free-angle aiming exists in baseline play.

## 2.4 Dominant-strategy guardrails

### Maximum-force farming
Strong impulses are not universally superior because:
- fragile receivers break on strong;
- some catches/pressure gates accept weak/medium only;
- overshoot can move a body past an authored receiver window;
- strong donor sources are finite-state and require meaningful world reset to recreate;
- token inventory is tiny.

### Brute-force direction testing
Each receiver exposes valid snap directions before spending. The puzzle is choosing causal use/order, not guessing angle. Undo/reset is free, so content must beat enumeration through branching interactions rather than punishment.

### Donor-factory exploit
A donor that can be repeatedly triggered with no world cost is invalid mature content unless repeated weak impulse generation is itself the intended authored resource. Validation tags source regeneration cost and rejects accidental infinite strong-source loops.

## 2.5 Eight-scenario graybox packet

### BC01 — Consequence as resource
One crate hits wall -> harvest EAST weak -> stamp onto cart -> cart reaches switch.
Expected insight: collision output can be moved across space.
Kill signal: tester thinks token is arbitrary ammo rather than the stored crash.

### BC02 — Direction transformation
Harvest SOUTH medium; use visible quarter-turn socket to launch EAST.
Expected insight: physical devices transform stored consequence; player does not rotate vectors freely.

### BC03 — Strong is harmful
Strong token breaks fragile bridge actuator; medium token succeeds.
Expected insight: magnitude band is semantic, not score/power tier.

### BC04 — Preserve scarce source
Two receivers, one strong donor, one weak renewable donor. Strong is needed later; spending it early creates dead-end but remains reversible.
Expected insight: token provenance/availability matters.

### BC05 — Self launch
Spend weak/medium impulse on player receiver to cross gap, then harvest landing collision into second token.
Expected insight: action and puzzle share the same grammar.

### BC06 — Chain causality
Impulse on cart -> cart hits crate -> second collision emits a new differently directed impulse -> door.
Expected insight: consequences can create future consequences without arbitrary modifier items.

### BC07 — Two-token ordering
Inventory cap 2; player must use one token to move socket orientation before harvesting another.
Expected insight: bounded resource/order puzzle.

### BC08 — Mature synthesis
Three donor events, two converters, one fragile receiver, one self-launch, two valid baseline solutions.
Expected solution structure: 4–6 spends/harvests, at least one non-maximum choice, no precision timing.

## 2.6 Quantitative graybox kill gates

Kill or radically reopen if after one tuning pass:
- >20% of ordinary failures are caused by misunderstanding direction/magnitude display;
- >50% of BC06–BC08 successful solutions use the strongest available impulse at every decision;
- any baseline solution requires frame-perfect collision timing or unsnapped aiming;
- repeated runs from same state/command sequence produce different capture tokens;
- >35% of successful mature actions are blind token permutations with no stated causal hypothesis;
- testers repeatedly request numeric vectors because visible bands/arrows are insufficient.

## 2.7 Hour-3 evolution

No new primary verb. Depth adds:
- converter topology;
- fragile/threshold receiver semantics;
- self-launch as ordinary tool;
- 2-token inventory pressure;
- collisions that create secondary donor events;
- route choice where spending an impulse changes the future donor layout.

Representative hour-3 case: harvest a medium west impulse from a falling counterweight, reverse it to move an elevator mass, self-launch using a weak token, then capture the elevator stop as the impulse that safely opens a fragile exit.

## 2.8 Hour-10 evolution

Still the same vocabulary. Mature cases use:
- multi-room donor economy;
- 2–3 token capacity;
- one-way converter topology;
- resettable vs exhaustible donors;
- chained impact ancestry;
- optional minimal-harvest / no-break mastery;
- moving receiver windows that are deterministic and pause/step compatible.

Hour-10 skill is causal compression: recognizing that one carefully engineered collision can replace several obvious token generations.

## 2.9 Controls

### Controller
- left stick/D-pad: move/focus player on authored traversal;
- A: interact / harvest when standing in capture zone;
- X: open 2-slot token wheel;
- stick/D-pad chooses token/receiver snap orientation;
- A confirm spend;
- B cancel;
- Y inspect causal lineage;
- LT/RT cycle valid nearby receivers when direct movement focus would be awkward.

### Keyboard-only
- arrows/WASD movement;
- Enter interact;
- Q/E token cycle;
- Tab cycles nearby compatible receivers;
- arrows select snap orientation;
- Space confirm;
- Escape cancel;
- I inspect lineage.

No mouse-only or analog-angle requirement.

## 2.10 Accessibility consequences

- magnitude is encoded with icon size/chevrons + text token, never color only;
- direction uses arrow shape + textual compass name when inspected;
- optional pause/step during moving-body states;
- generous auto-focus for harvest windows;
- no haptic/audio-only information;
- reduced motion replaces camera shake with static causal highlights;
- ordinary completion has no reflex timing requirement.

## 2.11 Strongest negative review

> “Great premise, but it becomes vector bookkeeping: collect arrows, rotate arrows, put the right arrow in the right socket.”

### Smallest canonical repair
Do **not** add more token properties. Keep 8 directions/3 bands, but ensure every mature dossier contains at least one decision where **source world-state consequence** matters in addition to token shape: harvesting/spending changes donor availability, receiver state, route, fragility or future collision chain. If puzzles can be represented as detached arrow inventory without caring where the impact came from, content fails review.

## 2.12 Production burden

Art 2/5 | UI 4/5 | domain simulation 4/5 | content 4/5 | QA 5/5 | input feel 3/5.

The burden is high but primarily deterministic/systemic, not animation/asset craft. A primitive prototype can falsify the core cheaply.

**RUN-5 RESULT: ADVANCES — strongest current contender.**

---

# 3. G3C30 — SINGLE-PIXEL KINGDOM

## 3.1 Canonical conceptual state

The world is a tile/node graph. The player avatar is one pixel-sized logical actor occupying exactly one node/cell.

Exactly **six state families maximum** are allowed in the base design candidate:
1. `SOLID` — collision-support state;
2. `HOT` — heat interaction state;
3. `HEAVY` — pressure/gravity interaction state;
4. `CONDUCTIVE` — circuit interaction state;
5. `ALIVE` — biological/agent interaction state;
6. `COLOR_IDENTITY` — symbolic faction/key state, always paired with shape/icon and never color-only.

The avatar carries at most **one state at a time**.

Every transferable donor state is either:
- **borrowed**: donor loses the state while the pixel carries/hosts it;
- **copied-temporary**: explicitly marked exceptional family behavior with a short deterministic expiry.

Default is borrowed. This is critical differentiation from generic property-shooting.

## 3.2 Transfer command

When pixel enters an interactable donor:
1. if carrying no state and donor exposes a transferable state, absorb it;
2. donor immediately enters its defined `state_absent` behavior;
3. pixel now carries the state and changes traversal compatibility;
4. when pixel touches a compatible receiver, player may deposit;
5. receiver gains state and pixel becomes empty;
6. state remains there until borrowed again or an explicitly authored deterministic expiry occurs.

There is no remote shooting/transfer. **Every transfer path must be physically traversed by the state-carrying avatar.**

## 3.3 Carrier interference rules

These are global, not per-level exceptions:
- SOLID pixel cannot pass through mesh/intangible-only channels;
- HOT pixel cannot traverse coolant/water cells without losing HOT at the first such cell;
- HEAVY pixel cannot use lift/air-current nodes;
- CONDUCTIVE pixel activates live hazards as well as useful circuits;
- ALIVE pixel attracts biological hazards and can use organic gates;
- COLOR_IDENTITY changes symbolic gates/agents but has no universal movement benefit.

This prevents one best state while making route and state inseparable.

## 3.4 LeiLei differentiation test

`LeiLei` performs property stealing/injection at range with a projectile on compact logic boards. Single-Pixel survives only if its game can be truthfully summarized as:

> **You are the courier, and the property is your body state while you physically move it through a route that the state itself changes.**

If prototype play mostly consists of deciding donor A -> receiver B independent of the route between them, the concept is too close to occupied property-transfer territory and should be killed.

## 3.5 Eight-scenario graybox packet

### SP01 — Borrow SOLID
Remove SOLID from donor platform; become SOLID; deposit into ghost bridge. Donor route disappears behind.
Expected insight: transfer has physical absence cost.

### SP02 — Carrier blocks route
SOLID allows bridge but prevents passing mesh. Player must deposit before mesh and recover later.
Expected insight: carried state changes traversal.

### SP03 — HOT coolant loss
Carry HOT toward frozen gate; direct route crosses coolant and strips state. Need alternate route.
Expected insight: property path matters.

### SP04 — HEAVY lift conflict
HEAVY activates pressure receiver but prevents air lift. Use intermediate receiver as state cache.
Expected insight: receivers can be logistics nodes, not only goals.

### SP05 — CONDUCTIVE risk
Conductive opens powered door but energizes hazard corridor while carried.
Expected insight: helpful state has collateral route cost.

### SP06 — Two-state swap
Need SOLID in room B and HOT in room A, but avatar carries one. A neutral relay receiver enables order-dependent swap.
Expected insight: one-slot logistics.

### SP07 — Moving receiver intercept
Receiver follows deterministic loop. Pixel must choose route and state compatible with interception; pause/step available.
Expected insight: motion adds routing, not twitch precision.

### SP08 — Mature three-room synthesis
Four state families present; player completes 6–8 transfers. At least two baseline solutions; no universal first state.
Expected insight: state transport network rather than property guessing.

## 3.6 Dominant-strategy attacks

### SOLID universal state
Global interference already makes SOLID incompatible with mesh and certain transport. Content validator flags if one state is first move in >50% of mature authored cases.

### State-cache trivialization
Unlimited neutral cache objects would turn one-slot carrying into inventory with extra clicks. Neutral cache nodes therefore are rare authored infrastructure; most receivers have their own active world consequence when holding state.

### Brute-force donor/receiver enumeration
Because the route changes while carrying and donor loses state, testing one transfer changes traversal topology. Still, if state graph can be solved purely by permutation search with no route reasoning, mature content fails the concept's differentiation test.

## 3.7 Hour-3 evolution

- all six families introduced by roughly hour 2–3;
- multi-room relays;
- donors whose absence matters remotely;
- moving carriers/receivers;
- one-slot state logistics;
- return-path restoration;
- optional minimal-transfer mastery.

No seventh state family is used to manufacture freshness.

## 3.8 Hour-10 evolution

Depth comes from topology, not new properties:
- 3–5 room state networks;
- borrowed state temporarily disabling donor infrastructure;
- state caches with consequences;
- multi-agent/door responses to ALIVE/COLOR identity;
- moving deterministic receivers;
- route restoration after objective completion;
- optional mastery where a state is routed through fewer hosts.

Hour-10 question: `How can one state trip accomplish two world changes while preserving my return route?`

## 3.9 Controls

### Controller
D-pad/left stick moves on logical graph. A interacts/absorbs/deposits. X previews current carried-state rule and affected nearby donor/receiver. Y toggles route/correspondence overlay. B cancel/back. No virtual cursor.

### Keyboard-only
WASD/arrows movement; Enter interact; I inspect current state; Tab cycle visible relevant state endpoints; R reset; Z Undo where puzzle mode permits.

The avatar itself is the cursor, so input burden is extremely low.

## 3.10 Accessibility

- state identities use shape/icon/pattern/text redundancy;
- COLOR_IDENTITY is never hue-only;
- movement can be turn/grid-based or speed-adjustable;
- moving receivers have pause/step assist;
- no precision platforming required for baseline;
- high-contrast single-pixel avatar may upscale into an accessibility halo without changing logical size;
- optional trail shows recent route and state pickup/drop points.

## 3.11 Strongest negative review

> “This is just another property-transfer puzzle with a tiny player dot. You ferry the obvious attribute from the obvious donor to the obvious target.”

### Smallest canonical repair
Do not add new properties. Require mature content validation to tag a **carrier-route transformation**: every dossier after the introductory band must contain at least one required decision where the carried state's traversal interference or donor absence changes the route/order. A case solvable as remote donor->receiver matching is invalid content.

## 3.12 Production burden

Art 1/5 | UI 4/5 | simulation 2/5 | content 4/5 | QA 4/5 | feel 2/5.

This remains the best scope-to-identity ratio, but market collision is real and makes content architecture unusually strict.

**RUN-5 RESULT: ADVANCES — but only as embodied state-logistics, never generic property transfer.**

---

# 4. G3C12 — BUREAU OF LOST WEIGHT

## 4.1 Canonical conceptual state

Use a discrete deterministic physics abstraction, not a general continuous rigid-body sandbox.

Objects have:
- stable ID;
- location/node;
- certified mass value chosen from authored integer certificates (e.g. 5, 10, 20, 40 kg-equivalent units);
- support relation;
- capacity threshold;
- buoyancy class;
- motion/inertia track when dynamic;
- receiver compatibility for certificates;
- break/compress/float states.

Total certified mass in a dossier is invariant unless an explicit external reservoir is part of the initial definition. There is no mass creation/destruction.

## 4.2 Transfer command

Player moves one whole visible certificate from host A to host B through a transfer action/station.

Resolution order:
1. validate both hosts and certificate availability;
2. remove exact certificate from A;
3. add to B;
4. recompute static support/capacity/buoyancy facts;
5. resolve deterministic dynamic motion on authored tracks;
6. resolve threshold effects/breakage;
7. evaluate goals/invariants;
8. present causal chain.

Certificates are discrete; the player never types mass values.

## 4.3 Global physical contracts

- support fails when total supported certified mass exceeds visible capacity;
- buoyancy uses discrete class thresholds rather than fluid simulation;
- carts on tracks gain one of three inertia bands based on mass and authored drive impulse;
- pressure devices activate at visible minimum bands;
- counterweights compare certified totals across linked sides;
- breakage is deterministic threshold state, not chaotic fracture physics.

This is intentionally puzzle physics.

## 4.4 Mass-sink exploit attack

Every compatible host has at least one globally understandable mass consequence. However, requiring every host to be always strategically important would feel contrived.

Canonical design test instead:
- mature scenarios must contain at least **two simultaneously relevant mass destinations**;
- no static host may absorb unlimited mass: all have visible capacity or a meaningful movement/buoyancy consequence;
- a deliberately designed `ballast reservoir` may exist, but its capacity is finite and its opportunity cost visible.

If arbitrary `this object cannot accept mass` flags become common, kill.

## 4.5 Eight-scenario graybox packet

### BW01 — Basic transfer
Lighten crate to move it; mass placed on pressure plate opens door.

### BW02 — Buoyancy
Move certificate to/from float platform to cross water-equivalent gap using discrete up/down state.

### BW03 — Capacity
Shelf accepts 20 but fails at 30. Need distribute across two supports.

### BW04 — Useful inertia
Heavy cart crosses resistance zone; lighter cart stops early. Strongest mass is useful here but costly elsewhere.

### BW05 — Counterweight
Two linked lifts require mass difference band, not exact free-form physics.

### BW06 — Sink trap
Obvious anchor can hold spare mass only up to capacity; overload blocks return path.
Expected insight: parking has collateral consequence.

### BW07 — Mid-route custody
A carrier can transport only <=10; certificate must be handed between hosts across facility.
Expected insight: mass itself has logistics topology.

### BW08 — Mature distribution
Six objects, four certificates, support + buoyancy + inertia + transport. At least two valid final distributions and no irrelevant sink.

## 4.6 Kill gates

Kill/reopen if:
- >40% of mature solutions converge on one ballast host;
- >2/5 testers describe deterministic threshold physics as arbitrary after visual tuning;
- ordinary completion depends on collision timing rather than state reasoning;
- >35% of decisions are blind certificate permutations;
- content repeatedly needs custom receiver prohibitions to stop dumping;
- visual mass/capacity feedback cannot explain outcomes without dense numbers.

## 4.7 Hour-3 evolution

- support and capacity;
- buoyancy;
- discrete inertia;
- counterweights;
- transport capacity;
- finite ballast;
- 4–6 certificates over 6–8 hosts.

The rules are all manifestations of one conserved quantity.

## 4.8 Hour-10 evolution

No new physics family beyond the frozen ceiling. Complexity comes from:
- mass temporarily being in transit;
- linked supports;
- moving ballast hosts;
- multi-stage return requirements;
- simultaneous threshold windows;
- optional final-distribution elegance.

Representative hour-10 solution: redistribute 40 total units so a float platform rises, then move 10 through a limited carrier to create counterweight, use the remaining 30 as cart inertia, and restore support before exit.

## 4.9 Controls

### Controller
Logical object focus with D-pad/stick; A select source certificate; shoulder buttons cycle certificates if host has multiple; D-pad/tab-like neighbor focus chooses receiver; A confirm; B cancel; X inspect capacity/mass consequences; Y toggle causal overlay.

### Keyboard-only
Tab/Shift-Tab object focus; arrows spatial focus; Enter select/confirm; Q/E certificate cycle; Escape cancel; I inspect. Mouse optional but not required.

No dragging precision.

## 4.10 Accessibility

- kg/unit text paired with 1/2/3/4-weight icon stacks;
- capacity uses matching icon slots + text;
- buoyancy/support changes are shown with stable before/after states, not animation alone;
- pause/step on moving track interactions;
- no color-only weight bands;
- reduced motion preserves state transitions.

## 4.11 Strongest negative review

> “The conservation gimmick sounds clever, but every puzzle is still make-this-light/make-that-heavy, with arbitrary shelves breaking so you can’t dump the spare weight.”

### Smallest canonical repair
Do not add more physics. Authoring must tag each mature dossier with a **mass-role transformation** and require at least two of: transport, support, buoyancy, inertia, counterweight, pressure. A scenario whose only meaningful transformation is `lighten target / park mass elsewhere` fails content review.

## 4.12 Production burden

Art 2/5 | UI 3/5 | simulation 4/5 | content 4/5 | QA 5/5 | feel 2/5.

Technically more predictable than free physics if the abstraction stays strict, but alternate-solution and exploit QA remain expensive.

**RUN-5 RESULT: ADVANCES — third contender; strongest conserved-resource puzzle but higher QA than Single-Pixel.**

---

# 5. G3C29 — FUSEBOX PARKOUR

## 5.1 Canonical conceptual state

The level is an authored traversal graph plus an electrical graph.

Electrical state:
- 1–3 power sources with integer capacity units;
- powered edges connect source to load nodes;
- each traversal surface/load consumes fixed 1–3 units;
- one temporary capacitor can store a bounded 1–2 units and decays after a fixed time/distance window;
- a moving player-carried load may hold one unit while in motion.

Traversal state:
- player has standard move, jump, wall-run and ledge-grab only;
- surfaces are `solid when powered` or `actuated when powered`;
- no combat required;
- movement uses forgiving authored geometry, not physics-sandbox behavior.

## 5.2 Rewire command

Holding rewire enters slowdown, not full pause by default.
1. eligible circuit nodes around current traversal region appear;
2. controller/keyboard focus snaps between nodes;
3. select source branch, then target branch;
4. proposed capacity result previews immediately;
5. confirm commits electrical topology;
6. powered geometry updates instantly and deterministically;
7. player motion continues under slowdown.

An accessibility option may increase slowdown to near-pause; underlying capacity rules remain identical.

## 5.3 Anti-safe-terminal architecture

The previous round proposed moving loads/decaying buffer. This round tests whether it genuinely preserves the identity.

Canonical candidate rule:
- the player can carry exactly one **live charge token** while leaving a powered anchor zone;
- that charge powers one selected forward branch for a fixed **traversal-distance budget**, not wall-clock precision;
- rewiring it behind/ahead is possible while moving;
- stopping is allowed, but the distance budget means the entire route cannot be solved from one safe room.

This is better than a timer because accessibility slowdown does not trivialize the resource.

## 5.4 Eight-scenario graybox packet

FP01 power floor to cross.
FP02 steal floor power to wall ahead; floor behind vanishes.
FP03 two loads exceed capacity; choose route.
FP04 carry live charge beyond anchor and spend before distance budget expires.
FP05 capacitor stores one unit through a powerless gap.
FP06 midair reroute between two snap nodes with generous coyote/ledge recovery.
FP07 recovery route after wrong reroute without forced death.
FP08 mature 40-second chain: 5 surfaces, two capacity choices, one alternate safe route, one mastery route.

## 5.5 Kill gates

Kill if after tuning:
- >40% of active play is spent in overlay/focus rather than traversal;
- controller causes >2 unintended node selections/minute after tutorial;
- near-pause accessibility mode removes almost all meaningful route decisions;
- safe-stop play clears >40% mature stages without interacting with charge-distance rule;
- players describe circuit work as interruption between platforming rather than traversal itself;
- camera/geometry tuning dominates development burden more than the electrical system.

## 5.6 Hour-3 / hour-10

Hour 3 adds branch capacity, moving charge, capacitor and alternate routes.

Hour 10 can add denser chains and route mastery, but it remains fundamentally an execution game. New depth without new movement mechanics is less certain than in the three puzzle-system contenders. Increasing complexity likely means harder movement/circuit multitasking rather than qualitatively new reasoning.

## 5.7 Controls

Controller feasibility exists: hold LT rewire; left stick/D-pad snaps circuit nodes; A select/confirm; release LT returns full speed. Movement remains left stick + A jump + shoulder wall-run/interaction as needed. Keyboard equivalent uses Shift hold + arrows/WASD focus and Space/Enter.

The concern is not missing bindings; it is cognitive/context switching at speed.

## 5.8 Accessibility

- configurable slowdown up to near-pause;
- distance-based charge budget instead of timer;
- broad ledge/coyote assists;
- optional route-preview arrows;
- no color-only circuit state;
- keyboard/controller remapping.

If preserving challenge requires limiting slowdown or removing recovery aids, the design fails its own accessibility thesis.

## 5.9 Strongest negative review

> “It’s two games fighting each other. The parkour feels best when I ignore the circuits, and the circuit puzzle feels best when I stop moving.”

### Smallest canonical repair
The smallest repair is already the moving charge/distance-budget rule, because it makes power itself a traversal object. If the graybox still produces the quoted review, there is no smaller paper repair: the concept should be killed rather than adding combat, abilities or more circuit types.

## 5.10 Production burden

Art 3/5 | UI 4/5 | simulation 3/5 | content 3/5 | QA 5/5 | movement/input feel **5/5 existential**.

The product advantage depends on craft quality that this factory cannot specification-freeze away.

**RUN-5 RESULT: CUT TO RESERVE.** Strong portfolio diversification, but its existential risk is implementation feel and context-switching, while the three remaining contenders are more cheaply falsifiable through deterministic grayboxes and have stronger paper depth.

---

# 6. Cross-finalist brute-force / depth comparison

| Test | Borrowed Collision | Single-Pixel Kingdom | Bureau of Lost Weight | Fusebox Parkour |
|---|---|---|---|---|
| Core resource | resolved impulse | carried world state | conserved mass | conserved electrical capacity |
| Primary action inseparable from movement/world | high | **very high** | medium | high if feel works |
| Generic market collision | low | **high due LeiLei** | medium-high mass precedent | medium circuit/parkour precedent |
| Best anti-dominant rule | source exhaustion + receiver bands | carrier interference + donor absence | finite meaningful hosts/capacity | moving distance-budget charge |
| Brute-force risk | medium | medium-high | medium-high | low logic / high execution retry |
| Hour-10 paper depth | **high** | high if route-first | high | medium-high, feel-dependent |
| UI abstraction risk | arrows/bands | state identity | mass/capacity | live overlay at speed |
| Deterministic implementation | medium-hard | easiest | medium-hard | medium + feel |
| QA burden | very high | high | very high | very high |
| Tiny-prototype falsifiability | **excellent** | excellent | excellent | good but feel tuning expensive |
| Asset burden | low | **minimal** | low | medium |

---

# 7. Final three after falsification

## #1 — G3C15 Borrowed Collision
Current leader. It has the cleanest genuinely unusual verb and the strongest relationship between a compact rule vocabulary and long-term causal depth. Its biggest danger—vector bookkeeping—can be attacked with quantized directions/bands and source-world relevance without adding feature bulk.

## #2 — G3C30 Single-Pixel Kingdom
Advances despite `LeiLei`, but under a much narrower identity: **embodied one-slot state logistics where the carrier's route changes because of the carried state and the donor's state is absent while borrowed**. It has extraordinary scope efficiency. Any drift toward remote/simple property matching is a market-collision failure.

## #3 — G3C12 Bureau of Lost Weight
Advances as the strongest conserved-resource puzzle. The conservation law creates forced collateral cost, but the concept faces familiar mass-manipulation imagery and heavy alternate-solution QA. It remains viable because the physics can be discrete rather than chaotic.

## Reserve — G3C29 Fusebox Parkour
Cut from the final three. The design can be made coherent on paper, but its key question is whether rewiring and movement feel like one continuous pleasure. That is a higher-variance implementation bet than the remaining contenders and cannot be solved by further specification.

---

# 8. Phase-2 state after Run 5

Phase 2 is **not yet complete** and no Product Thesis is locked.

The final three now have explicit enough rules for a true selection duel. The next round should not re-expand the candidate field unless a fatal market collision appears.

## NEXT ACTION — Final Selection Duel
For each of the three contenders:
1. freeze one exact one-sentence Steam pitch and 10-second muted trailer beat;
2. write the exact first 20 minutes and first 2 hours, not just feature lists;
3. define minimum shippable scope and realistic first-clear duration;
4. define content-production method and validation tooling burden;
5. define the one-week prototype plan day-by-day and the binary decision at its end;
6. run a fresh final market/analogue check using the now-exact mechanics;
7. attack likely Steam review sentiment and perceived-value risk;
8. compare pricing/value positioning only as a hypothesis, not a lock;
9. compare implementation schedule risk qualitatively under the same solo/small-team assumption;
10. choose exactly one Game #3 concept if the evidence is decisive; otherwise document why a two-prototype duel is genuinely necessary.

Only after that decision may Phase 3 Product Thesis Lock begin.