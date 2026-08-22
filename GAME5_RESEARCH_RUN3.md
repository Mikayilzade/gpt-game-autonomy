# GAME #005 — OPPORTUNITY DISCOVERY — RUN 3

Last updated: 2026-08-22
Factory run: **3**
Phase: **1 — Opportunity Discovery**
Concept selected: **NO**
Production implementation: **NOT STARTED**

This pass is the Phase-1 completion attempt. It attacks all nine active Run-2 concepts at full-product depth, adds current nearest-neighbor pressure, and decides only which concepts deserve entry into a formal Phase-2 tournament. **No Game #005 winner is selected here.**

---

# 1. Fresh market / nearest-neighbor pressure

Fresh searches were run specifically against the remaining novelty claims rather than broad genre tags.

## 1.1 Movement-trail pressure became materially worse
`TrailRail` is a 2026 Steam action-puzzle whose explicit store pitch is that the player's movement trajectory/footsteps become materialized world-changing geometry. Its demo launched February 2026 and contains six stages / roughly 30 minutes of play.

References:
- https://store.steampowered.com/app/3846430/TrailRail/
- https://store.steampowered.com/app/4330530/TrailRail_Demo/

`Warmth` also uses a trail-of-warmth puzzle framing, although its trail comes from placed heat sources rather than the player's decaying footprint:
- https://store.steampowered.com/app/1234830/Warmth/

This does not make every thermal mechanic derivative, but it substantially weakens **G5C45 Thermal Footprint** because its most marketable sentence is still `your movement leaves a trail that changes the world`. Heat-reactive consumers would have to carry the remaining novelty, which in turn creates content inflation.

## 1.2 Orbit as a broad action vocabulary is crowded, but Tool Orbit remains narrower
Orbital games are active and familiar:
- `Orbit - Playing with Gravity` centers on launching bodies into stable orbits and even previews future trajectories: https://store.steampowered.com/app/552120/Orbit__Playing_with_Gravity/
- `Arclo` uses an orbiting tethered body and anchor-swapping as its complete control vocabulary: https://www.edcaspersen.com/arclo/guide/
- multiple 2025–2026 small orbit/gravity puzzlers continue to appear.

This means **G5C37 cannot market `orbits are cool` as novelty**. It survives only if its identity stays specific: **a carried tool becomes a persistent second moving actor on authored local orbit tracks, while the player independently traverses, catches it, and hands it between anchors**. Real orbital simulation would move the concept into a much more crowded and harder-to-control family.

## 1.3 Property transfer is established, but sequential door memory remains distinct enough for tournament pressure
`Prop Swap` is a direct precedent for swapping physical/material properties such as weight and friction between objects:
- https://yernemm.itch.io/prop-swap

No fresh targeted result found the exact proposed **door-as-one-bit-state-memory** rule where an eligible object and doorway exchange HEAVY/LIGHT state when crossing. That is not proof of uniqueness, but it is enough to keep G5C17 alive if the campaign can remain mostly one-property rather than escalating into a property catalogue.

## 1.4 Repair / logic / wiring games are crowded at the category level
`Prelogate` and many logic/programming games already make rule networks into puzzles:
- https://store.steampowered.com/app/332830/

`Dynopunk` includes gadget diagnosis/repair alongside narrative systems:
- https://store.steampowered.com/app/1596730/

The exact `one wrong physical rule cartridge -> run machine -> observe causal symptom -> replace one cartridge` loop remains narrower, but **G5C21 loses immediately if the machine becomes a circuit editor, code panel, or wiring screen**.

## 1.5 Cable/tension search still did not surface an exact conserved-tension core
Fresh targeted searches surfaced cable-connection puzzles such as `Rescue Cable`, but not an obvious commercial game whose core is **moving one anchor so a fixed tension budget redistributes simultaneously among several visible live loads**:
- https://store.steampowered.com/app/2551730/Rescue_Cable/

The market-distance claim for G5C02 therefore remains plausible but unproven. Its larger risk is not precedent; it is whether players can read tension without numbers or a detached network UI.

## 1.6 Umbrella/crowd idea has real-world plausibility, not yet product depth
Pedestrian-flow research has directly measured how holding umbrellas changes lane formation and merges/splits bidirectional pedestrian streams:
- https://arxiv.org/abs/1606.03434

This supports the visual intuition behind **G5C41 Crowd Umbrella**, but scientific plausibility does not solve the game's production problem: many agents, lane-state readability, and enough repeated depth without adding many NPC roles.

---

# 2. G5C41 — Crowd Umbrella full attack

## Smallest viable vocabulary
- player walks in a top-down public space;
- one umbrella has two states: CLOSED / OPEN;
- while open, facing may be rotated among 8 snapped directions;
- deterministic pedestrians follow authored lane fields and avoid the umbrella footprint;
- pedestrian streams may merge/split only at authored junctions;
- no individual social AI, dialogue, combat, or hidden personality model.

The concept fails if it needs free social-force simulation to look alive.

## Eight mature kernels
1. **Bottleneck Split** — open umbrella just before a narrow junction; one incoming stream divides around the player, briefly freeing the center route.
2. **Counterflow Shield** — angle the umbrella so opposing streams peel to different sides, letting the player walk upstream without collision.
3. **Merge Poison** — solving one lane creates a jam at a downstream merge; player must close/re-angle before reaching it.
4. **Crosswalk Window** — redirect pedestrians away from one crossing long enough for a service cart to pass; too much displacement blocks the player's exit side.
5. **Moving Bottleneck** — walk while open so the crowd split travels with the player; stopping in the obvious safe spot causes a queue to grow into the next junction.
6. **Two-Junction Sequence** — first angle benefits west junction but sends excess flow toward north; second move must unwind the first consequence.
7. **Platform Edge** — umbrella widens the player enough to force one lane around a column, but opening too early pushes pedestrians into the only stair approach.
8. **Return Inversion** — an event reverses one major pedestrian stream; the same umbrella angle used on entry now worsens extraction.

## Product attack
- 10-second mute clip: **excellent**. One umbrella opening and a whole crowd splitting is visually immediate.
- repeated 5–15 second action: **good in short bursts**.
- controller: **good** with snapped facing.
- 20-minute demo: **credible**.
- one-week graybox: **medium**, not cheap. Deterministic lane-field crowd behavior, avoidance, junction flow, jams and readable animation all need work before the mechanic can even be judged fairly.
- asset burden: **materially higher** than the abstract/mechanical survivors because 20–40 readable moving agents must feel intentional rather than robotic clutter.
- hour-5 defense: weak under the smallest vocabulary. Eight kernels already lean repeatedly on bottleneck, merge and reversed-flow topology.

## Dominant-strategy / failure attack
Likely dominant play is `open umbrella at the narrowest point and push forward`. Preventing that requires junction-specific crowd objectives, different destinations, vehicle/service interactions or differentiated pedestrian classes. Those are **new content/system burdens**, not depth emerging cheaply from the umbrella itself.

**RUN-3 VERDICT: CUT FROM PHASE-2 FIELD.**

The hook is excellent, but mature depth asks the team to build a crowd-simulation/content machine disproportionate to the mechanic. Preserve as historical reserve; do not tournament-test it against candidates with cheaper systemic depth.

---

# 3. G5C45 — Thermal Footprint full attack

## Smallest viable vocabulary
- WALK and FAST movement lay visible heat samples along the player's recent route;
- every heat sample decays deterministically after a short fixed lifetime;
- a target reacts when enough live trail overlaps its heat zone;
- player cannot paint from a cursor; only actual movement creates heat;
- no inventory, fire tools or temperature-management UI.

## Eight mature kernels
1. **Frozen Hinge** — circle a hinge to accumulate enough heat before the first trail segment cools.
2. **Two-Zone Relay** — warm A, then reach B while enough of A's trail remains to keep a path open.
3. **Crossing Trail** — path geometry must intersect two sensors but avoid a heat-sensitive hazard tile.
4. **Fast / Slow Choice** — FAST lays stronger/denser heat but makes turning less forgiving; WALK allows exact path shaping.
5. **Cooling Return** — player intentionally waits only through active movement elsewhere so an earlier hazardous trail cools before extraction.
6. **Moving Contact** — a deterministic moving plate crosses the player's recent trail and reacts only if timing/route align.
7. **Shared Corridor** — the route needed to warm one mechanism also warms an unwanted wax gate unless the player takes a longer geometric approach.
8. **Final Loop** — route must maintain two separated warm zones long enough to cross a third region before the first expires.

## Product attack
- 10-second clip: **strong**.
- controller: **excellent**.
- graybox: **very cheap**.
- demo: **easy**.
- systemic depth: **medium**. Most hard kernels become path-shape + decay-window problems.
- execution pressure: high; after understanding the route, success depends on reproducing it before decay.
- content inflation: to escape path-drawing repetition the concept wants wax, springs, frozen hinges, thermal sensors, moving heat consumers, hazards, etc.

## Nearest-neighbor impact
`TrailRail` now occupies a very strong 2026 `your movement trajectory becomes world-changing puzzle material` position. Thermal decay changes the rule, but the first GIF/store sentence is too adjacent. `Warmth` adds further heat-trail language pressure.

**RUN-3 VERDICT: HARD KILL.**

The candidate is producible but no longer ownable enough, and its depth trends toward timed route execution plus a growing consumer list.

---

# 4. G5C02 — Tension Budget deep full-product attack

## Exact smallest vocabulary
1. One **movable anchor** per encounter, constrained to an authored rail or 3–5 sockets.
2. A visible cable network connects the anchor to 2–4 **loads**.
3. Every socket produces a deterministic distribution of three presentation bands: SLACK / TAUT / HIGH.
4. Loads respond to bands through one physical state curve already visible in their geometry: lift height, gate counterweight, bridge sag, piston reach, or weighted arm angle.
5. No soft-body cable simulation is authoritative. Cable animation only visualizes discrete state.
6. No numeric tension values are required in normal play.
7. Mature encounters may visibly add/remove one load through an ordinary objective action; this changes redistribution but does not add a new manipulation system.

## Twelve-kernel campaign sketch
1. **Single Lift** — first anchor move visibly raises one platform.
2. **Lift / Gate Trade** — lift rises while gate drops; first collateral consequence.
3. **Sag Bridge** — enough tension flattens a cable bridge but lowers a counterweight elsewhere.
4. **Three-Load Split** — useful answer is the middle socket because all three loads need non-extreme states.
5. **Crossing While Live** — player must pass through the geometry created by one distribution to reach another socket approach.
6. **Counterweight Corridor** — move anchor twice; first clears ceiling weight, second restores floor route.
7. **Moving Winch Base State** — a deterministic machine changes one cable's base pull, so the useful socket changes after the cycle.
8. **Load Removal** — objective detaches a visible crate/counterweight; the same anchor position now redistributes differently.
9. **Partial Success Trap** — a socket opens the obvious gate but over-tensions a bridge into an unusable high state.
10. **Two-Stage Traverse** — one distribution gets player onto a central platform; from there player physically reaches a different side of the rail and changes distribution for the exit.
11. **Tied Visual Outcome** — two sockets both raise the target lift, but only one leaves enough tension to keep a distant return arm in range.
12. **Return Inversion** — objective changes load topology; extraction requires a distribution never useful on entry.

## Can tension be taught without numbers?
**Paper answer: YES, if the art treats cable state as posture rather than arithmetic.**

Required teaching grammar:
- SLACK has a clearly hanging curve and loose hardware;
- TAUT becomes straight with one visible mechanical notch/indicator;
- HIGH visibly pulls the connected spring/counterweight near its limit;
- each load animates continuously during anchor movement, but snaps mechanically to one canonical band at socket commit;
- in the first three encounters, the player never needs to compare more than two loads at once;
- no gauge is needed for correctness; a gauge may exist as secondary decoration/accessibility redundancy.

If testers ask `what is the number on this cable?` before they can predict a state, presentation failed.

## Dominant-strategy attack
Potential dominant strategy: enumerate all 3–5 sockets and choose the one that makes the obvious route open.

Defense must be **encounter structure**, not hidden data:
- mature states require a sequence of 2–4 anchor placements;
- player physical position determines which placement is useful now;
- objective/load mutations change later redistribution;
- a socket that solves the local gate can create a downstream/return problem;
- preview can remain exact without recommending the best sequence.

## 20-minute demo beat
- 0–3 min: one cable/load, drag anchor, immediate posture change.
- 3–7 min: two loads, first obvious tradeoff.
- 7–12 min: three sockets / two loads, player traverses geometry created by tension.
- 12–20 min: three-load selective compromise + objective removes one load and forces a second anchor move for extraction.

The true differentiator appears before demo end without adding a second pillar.

## Hour-5 repetition defense
Depth axes available without new mechanics:
- topology of cable/load connectivity;
- socket-to-distribution mapping;
- number of loads (2–4 only);
- physical consequence curve per already-known load family;
- player traversal relationship to those consequences;
- one visible load mutation;
- ordered sequence and return inversion.

Main risk: multiple load families can become content inflation. Tournament must test whether **3–4 reusable load archetypes** are enough for an entire game.

## Implementation ambiguity / one-week falsification
Very cheap if implemented as discrete data:
`socket -> per-cable band -> load state`.

One-week prototype can use colored lines, rectangles, 4 sockets and simple platforms. No rope solver is necessary. This is a major strength.

**RUN-3 VERDICT: PHASE-2 SURVIVOR — STRONG.**

---

# 5. G5C37 — Zero-G Tool Orbit deep full-product attack

## Exact smallest vocabulary
1. Top-down compact zero-g rooms; player movement uses simple omnidirectional thrusters with capped acceleration, not realistic inertia simulation unless feel proves necessary.
2. Player carries exactly one active tool baseline.
3. Authored **orbit anchors** expose 2–3 discrete tracks each: inner / outer, occasionally reversed direction only if visually obvious.
4. Releasing the tool inside an anchor's capture zone snaps it onto the highlighted track at a deterministic phase entry point.
5. Tool then repeats that track until caught or transferred.
6. The tool interacts only with marked world targets while orbiting: momentary strike target, blocking/interceptable hazard, catch-transfer zone.
7. Catch windows are generous/authored; pixel-perfect interception is not the puzzle.
8. Real gravity equations are explicitly unnecessary.

## Twelve-kernel campaign sketch
1. **First Orbit** — tool loops through one switch every cycle while player crosses a door.
2. **Inner / Outer** — choose track that hits A but misses B.
3. **Catch Across Room** — launch, traverse independently, catch at opposite arc.
4. **Anchor Hand-off** — catch from A and release into B without returning to start.
5. **Orbit Shield** — tool repeatedly intersects a periodic hazard line while player crosses elsewhere.
6. **Phase Window** — two targets lie on one track; player chooses release phase so the first hit opens a short player route before the second resets it.
7. **Moving Intercept** — deterministic target moves through the orbit zone; authored preview shows which track intersects it.
8. **Player / Tool Crossing** — player must move through the orbit interior after the tool passes, making the persistent tool both helper and spatial hazard.
9. **One Tool, Two Anchors** — objective requires two different periodic interactions; player must abandon the first orbit and physically recover the tool.
10. **Obstacle Mutation** — objective rotates a panel that blocks one formerly-safe orbit segment; tool must be re-caught and reassigned.
11. **Catch Under Pressure** — player position after a door crossing determines which future arc can be intercepted; no aiming precision, but route planning matters.
12. **Return Inversion** — same orbit that enabled entry now repeatedly triggers the wrong target after objective mutation; extraction requires hand-off to a different anchor.

## Authored orbit tracks vs physics
**Paper answer: authored tracks are not a compromise; they are the correct product rule.**

The interesting state is `tool is a persistent periodic actor I placed into the room`, not `I solved Keplerian mechanics`. Track preview can be a visible ring/ellipse with arrow and target intersection marks. Release should snap to a legal orbit when the tool is in a capture halo, much like snapping an object to a rail.

Controller contract candidate:
- carry tool: normal movement;
- hold Aim/Orbit Preview near anchor: nearest legal track highlights;
- left/right or stick radial choice chooses inner/outer;
- release button commits;
- catch is contextual within generous proximity.

No free-angle ballistic aiming is required in 1.0.

## Dominant-strategy attack
Potential collapse: `put tool on orbit that hits switch, then wait`.

Mature defense:
- player must exploit the periodic state while independently traversing;
- single tool means every new orbit relinquishes previous periodic function;
- catch/hand-off changes which periodic function exists;
- at least some target states are momentary, requiring active exploitation but not long patrol waiting;
- geometry/objective mutations invalidate static orbit camping.

## 20-minute demo beat
- 0–4 min: launch tool into a single obvious orbit and cross a held-open route.
- 4–8 min: inner/outer track selection.
- 8–13 min: launch then catch across room.
- 13–20 min: hand tool from anchor A to B while moving; final action uses one periodic hit to open the path and a second catch to escape.

Very strong mute-clip communication throughout.

## Hour-5 repetition defense
Available depth axes:
- anchor layout;
- track radius/direction;
- target intersections;
- tool periodic phase;
- player route relative to orbit;
- catch point;
- one-tool exclusivity;
- world mutation changing valid/valuable tracks.

Risk remains that targets become a catalogue of `things a wrench can hit`. Keep target families extremely small and make depth come from **orbit relationships**, not bespoke tool functions.

## Implementation ambiguity / one-week falsification
Cheap. Prototype can be circles/ellipses and one moving tool with deterministic phase. The real risk is **feel**, not systems complexity: catch/release must feel fast and intentional on controller.

Empirical kill gate for tournament/vertical slice: after 10 minutes, users should deliberately create/catch orbits rather than fight the snap system; failed catches should be rare outside strategic mistakes.

**RUN-3 VERDICT: PHASE-2 SURVIVOR — STRONG.**

---

# 6. G5C17 — Door Memory deep full-product attack

## Exact smallest vocabulary
The rule is now made explicit for falsification:

**Every memory door stores one binary weight state: HEAVY or LIGHT. When an eligible object crosses, the object and door SWAP weight states.**

Example:
- door memory = HEAVY;
- cart entering = LIGHT;
- cart exits HEAVY;
- door memory becomes LIGHT.

This is simpler and more deterministic than vague `remember last object and stamp next` wording.

Other baseline rules:
1. Only marked movable objects are eligible; player does not change weight in Phase-1 baseline.
2. Object weight has exactly three reusable world consequences in the candidate grammar:
   - HEAVY can depress heavy plates / weighted mechanisms;
   - LIGHT can be pushed/carried by player where HEAVY cannot;
   - HEAVY/LIGHT changes whether a simple lift/counterweight threshold is met.
3. No friction, fire, magnetism, size, color, electricity or other property family is required to enter Phase 2.
4. Doors always show their stored state physically before crossing.

## Twelve-kernel campaign sketch
1. **First Swap** — LIGHT cart crosses HEAVY door and becomes heavy enough for a plate.
2. **Get It Back** — same cart must later become LIGHT again to be moved to exit.
3. **Door Poison** — using the heavy state solves one plate but leaves the only return door LIGHT.
4. **Two Objects** — order of two carts determines which one receives the required state.
5. **Two Doors** — two memory doors hold opposite states; route/order matters more than object selection.
6. **Lift Threshold** — heavy cart lowers one counterweight lift, changing player access while the door memory flips.
7. **Carry Through / Push Back** — player can only relocate LIGHT cart manually, so crossing sequence changes both state and object mobility.
8. **State Transport** — use one cheap cart purely to carry HEAVY state from Door A into Door B, effectively moving memory through the world without a portable token UI.
9. **Intermediate Parking** — an object must end a step heavy for a plate, then later be made light to move again.
10. **Two-Door Cycle** — careless sequence returns both doors to the wrong state; intended solution uses one object to rotate the pair through a three-crossing cycle.
11. **Objective Mutation** — completing objective locks one path, so the state arrangement used on entry cannot simply be reversed.
12. **Return Inversion** — extraction needs a different object LIGHT than entry did, forcing the player to reason about door memory after each swap.

## Does one property scale?
**Paper answer: surprisingly yes for tournament entry, but not yet proven for a full game.**

The 12 kernels use only HEAVY/LIGHT plus three physical consequences. The depth comes from **state ordering and location**, not adding new property nouns. Two doors and two or three eligible objects create a compact state machine that can be understood visually.

The danger is Sokoban-style combinatorial annoyance. Object pushing/carrying must be fast and resets immediate. Levels should remain small enough that failure means `I put the weight state in the wrong place`, not `I spent two minutes hauling a box back`.

## Dominant-strategy attack
Potential strategy: cycle an object through a door repeatedly until the wanted state appears. Because swap is binary, immediate repeated crossing simply alternates states and is not itself interesting.

Encounter defense:
- physical one-way/position constraints must make crossing order meaningful;
- using a door moves the object to the other side, so state change also changes spatial availability;
- two doors/objects create state-location coupling;
- no arbitrary cooldown or crossing cost.

## 20-minute demo beat
- 0–4 min: one door + one cart, visibly swap LIGHT/HEAVY.
- 4–8 min: heavy plate then need cart light to move again.
- 8–13 min: two objects / one door ordering.
- 13–20 min: two doors with opposite memory states; final puzzle requires transporting HEAVY state through one object then restoring a movable LIGHT object for exit.

The true rule can be taught without text-heavy property systems.

## Hour-5 repetition defense
Depth axes within one binary property:
- number/location of doors (1–3 target ceiling);
- stored initial states;
- number/location of eligible objects (1–3 target);
- physical access graph;
- which heavy consequences are currently required;
- object mobility when LIGHT;
- ordering and return requirements.

Main risk: 4–8 hours may still exhaust the state grammar. Phase 2 must compare campaign ceiling against the other survivors rather than assume a second property family will rescue it.

## Implementation ambiguity / one-week falsification
Extremely cheap and deterministic. A grid/top-down prototype with two-colored door states and crates can prove the entire mechanical core in days.

**RUN-3 VERDICT: PHASE-2 SURVIVOR — STRONG.**

---

# 7. G5C21 — Broken Rule Workshop deep full-product attack

## Exact smallest vocabulary
1. One compact machine occupies the physical play space and runs a deterministic 5–12 second cycle.
2. Player can stop/reset instantly between tests.
3. Exactly one **rule cartridge** is wrong in the baseline campaign puzzle.
4. Player may remove one cartridge and insert one of a small visible spare set, then immediately RUN.
5. Rule cartridges belong to only four candidate families for Phase-2 testing:
   - DIRECTION: route left/right;
   - ORDER: A before B / B before A;
   - CONDITION: act on ON vs OFF sensor state;
   - DELAY: short vs long beat.
6. The machine itself provides evidence through moving parts and outputs; no source code, wire drawing or truth-table screen is required.
7. Machine primitives are reusable modular actuators/sensors, not bespoke scripted set pieces.

## Twelve-kernel campaign sketch
1. **Wrong Direction** — sorter routes both items into reject bin.
2. **Clamp / Press Order** — press fires before clamp; visible failure immediately identifies temporal relation but not necessarily cartridge location.
3. **Sensor Inversion** — gate opens when sensor is empty instead of occupied.
4. **Delay Collision** — two correct paths interfere only because one delay cartridge is wrong.
5. **Symptom Downstream** — visible jam occurs three modules after the bad direction rule; player must reason upstream.
6. **False Local Symptom** — replacing the cartridge nearest the jam changes behavior but does not produce valid output.
7. **Two Candidate Causes** — observed first run is consistent with two faults; player runs one controlled test configuration to discriminate.
8. **One Spare, Two Sockets** — correct cartridge type is known but location must be diagnosed from sequence.
9. **Efficiency Variant** — two repairs produce valid product, but one creates an extra cycle; optional mastery only.
10. **Parallel Branch** — fault affects only every second item due to condition state, making observation across a full cycle necessary.
11. **Reset State Trap** — one delay fault appears harmless on first item but fails after machine returns to start phase.
12. **Final Composite Machine** — 7–8 modules, one fault, two plausible hypotheses; player alters one cartridge, runs, observes and finishes in 2–4 experiments.

## Can it stay world-first?
**Paper answer: YES, but only under a strict presentation boundary.**

The machine must occupy most of the screen. Cartridges are physical objects mounted beside the actuator they govern. During RUN, the player watches actual objects move. There is no detached wiring board. A cartridge may have a simple icon pair (`left/right`, `A→B/B→A`) but never a mini programming language.

If optimal play becomes staring at cartridge labels without running the machine, the concept has failed.

## Dominant-strategy attack
Potential strategy: try every spare cartridge in every socket.

Counterstructure:
- fast experimentation remains allowed and should not be punished;
- a mature machine may have 6–8 sockets × 2–3 plausible spares, making blind search slower than interpreting behavior but still finite;
- optional mastery can reward few RUNs, but base completion never adds consumable attempts;
- controlled test outcomes should eliminate hypotheses rapidly.

The challenge must be diagnosis, not anti-brute-force friction.

## 20-minute demo beat
- 0–4 min: obvious direction fault, swap and RUN.
- 4–8 min: order fault whose visible collision explains cause/effect.
- 8–13 min: symptom occurs downstream from fault location.
- 13–20 min: two plausible hypotheses; first experimental swap changes the symptom, second fixes machine.

This is a strong demo because each RUN produces a visible story within seconds.

## Hour-5 repetition defense
Depth axes:
- machine topology;
- cartridge family combinations;
- fault location;
- symptom distance from cause;
- periodic/parallel behavior;
- ambiguity requiring controlled experiment;
- optional efficiency target.

However content authoring remains the largest risk: every puzzle needs a machine that is visually readable in multiple incorrect states. Modular authoring tools are likely mandatory.

## Implementation ambiguity / one-week falsification
Core logic is cheap. The hard part is authoring/readability, not runtime systems. A one-week graybox with 4 rule families and 5 reusable modules can test whether players actually infer faults from motion.

**RUN-3 VERDICT: PHASE-2 SURVIVOR — CONDITIONAL-STRONG.**

It survives because the repeated `change one rule -> run -> watch consequence` loop is distinct and demo-friendly, but it carries higher content-authoring burden than G5C02/G5C17.

---

# 8. G5C01 — Frame Pin deep attack

## Smallest vocabulary
- exactly one mechanism may be pinned at a time;
- pinned mechanism freezes at exact current deterministic phase and becomes normal collision/cover;
- pinning a second mechanism instantly releases the first from its stored phase;
- no rewind, fast-forward, clone, timeline or global time stop.

## Twelve-kernel sketch
1. crusher shelf;
2. elevator bridge;
3. rotor cover;
4. conveyor carrier support;
5. paired sweepers;
6. return cascade;
7. pin moving gate at partial opening;
8. release old piston so it pushes an object while new platform is pinned;
9. pin shield, traverse, then release it to expose target;
10. two moving platforms whose relative phase matters;
11. objective changes one machine cycle speed after release;
12. final handoff chain across three periodic mechanisms.

## Destructive result
The 12 kernels reveal only three recurring reasoning families:
- choose the correct phase;
- choose which one object receives the pin;
- exploit the automatic release of the previous object.

That can absolutely make a good puzzle game, but the first two are deeply familiar time-freeze language and the third is a constraint rather than a new fantasy. Mature play repeatedly trends toward `watch cycle -> freeze useful pose -> cross`.

Current object-level time-freeze precedent is strong enough that Game #005 should demand more ownable distance rather than rationalize this candidate because it is cheap to build.

**RUN-3 VERDICT: CUT FROM PHASE-2 FIELD.**

Not a bad game; simply weaker portfolio/market upside than the four survivors.

---

# 9. G5C25 — Sunpatch Garden deep attack

## Smallest vocabulary
- one reflector relocates one visible sun patch among authored regions;
- one active sun patch baseline;
- consumers react in <=2–4 seconds and reverse predictably when light leaves;
- no farming timers, inventory, resource harvesting or calendar.

## Twelve-kernel sketch
1. vine bridge grows;
2. flower blooms and pollinator moves;
3. basking creature vacates a plate;
4. wet crossing dries;
5. one angle weakly serves two consumers;
6. canopy mutation changes return path;
7. shade-loving plant opens while bright plant closes;
8. two-step pollination state;
9. sun patch must follow player route across reflector stations;
10. creature and vine compete for same patch;
11. objective permanently opens skylight, changing available patch geometry;
12. return inversion across two consumers.

## Destructive result
The concept is beautiful, controller-safe and marketable, but the kernel list demonstrates the same problem as Rain Router: **mature variety is being purchased with consumer types**.

If reduced to only vine + flower, depth shrinks rapidly. If expanded to vines, flowers, pollinators, creatures, drying, shade plants, canopies and multi-stage ecology, art/content/animation burden rises and the small-rule thesis weakens.

Compressed reactions solve waiting but make the ecology feel like switches wearing organic skins. Slower reactions preserve fantasy but violate the repeated 5–15 second action goal.

**RUN-3 VERDICT: CUT FROM PHASE-2 FIELD.**

Keep as a visually appealing reserve, but it does not beat the systemic economy of the four survivors.

---

# 10. G5C10 — Pressure Line deep attack

## Smallest vocabulary
- one portable seal moves among authored pipe junction sockets;
- pressure is discrete and deterministic;
- seal closes one branch; pressure redistributes to 2–4 visible consumers;
- consumers use a tiny known family such as piston / lift / door;
- player physically traverses the same room; no pipe-construction UI.

## Twelve-kernel sketch
1. piston stair vs door;
2. launcher vs lift;
3. parallel branch;
4. reservoir discharge;
5. moving demand;
6. objective opens bypass;
7. seal moved from entry branch to return branch;
8. overpressure holds one piston extended while another retracts;
9. two paths reach same consumer but one starves exit;
10. physical access to socket requires first pressure state;
11. objective adds/removes one consumer demand;
12. final three-stage seal sequence.

## Destructive result
The candidate is mechanically sound but conceptually loses to G5C02.

Both use one physical control to redistribute a conserved network quantity among multiple mechanisms. Tension Budget has the stronger world-space visual metaphor because **the cables and loads themselves deform simultaneously**. Pressure Line more naturally wants gauges, pipe tracing and invisible internal pressure, pushing it toward `pipe editor with an avatar`.

Existing pressure/valve/network puzzle precedent, including `ComPressure`, further weakens its discovery advantage.

**RUN-3 VERDICT: CUT FROM PHASE-2 FIELD.**

It becomes a useful comparison case for G5C02, not a separate tournament entrant.

---

# 11. Cross-candidate Phase-1 completion matrix

| Candidate | Hook / mute clip | Small-rule depth | Demo | Graybox | Controller | Hour-5 defense | Market distance | Main burden | Phase-1 result |
|---|---|---|---|---|---|---|---|---|---|
| **G5C02 Tension Budget** | Strong | **Very strong** | Strong | **Excellent if discrete** | Strong | Strong | Strong | readability without numbers | **ADVANCE** |
| **G5C37 Zero-G Tool Orbit** | **Excellent** | Strong | **Very strong** | Strong | Medium-strong | Strong | Medium-strong | feel/catch predictability | **ADVANCE** |
| **G5C17 Door Memory** | Strong | Strong | Strong | **Excellent** | **Excellent** | Medium-strong | Strong | campaign ceiling | **ADVANCE** |
| **G5C21 Broken Rule Workshop** | Medium-strong | Strong | **Very strong** | Strong | Strong | Medium-strong | Medium-strong | machine authoring/editor drift | **ADVANCE** |
| G5C01 Frame Pin | Strong | Medium | Strong | Excellent | Strong | Medium | Weak-medium | time-freeze familiarity | CUT |
| G5C25 Sunpatch Garden | Strong | Medium | Strong | Strong | Strong | Weak-medium | Medium | consumer/art inflation | CUT |
| G5C10 Pressure Line | Medium | Strong | Strong | Excellent | Strong | Medium-strong | Weak-medium | pipe abstraction | CUT |
| G5C41 Crowd Umbrella | Excellent | Weak-medium | Strong | Medium | Strong | Weak | Strong | crowd/content burden | CUT |
| G5C45 Thermal Footprint | Strong | Medium | Strong | Excellent | Excellent | Medium | **Weak after 2026 precedent** | execution/consumer inflation | **HARD KILL** |

---

# 12. Final Phase-1 survivor dossiers

Phase 2 opens with **exactly four** entrants. This is intentionally smaller than the 6–10 early pressure set because Run 3 removed candidates whose appeal depended on precedent tolerance, content inflation or expensive simulation.

## S1 — G5C02 Tension Budget
Core promise: move one physical anchor and watch a fixed tension budget redistribute across several connected loads, changing the room in multiple places at once.

Why tournament-worthy:
- collateral consequence is visually physical;
- small deterministic implementation;
- mature depth from distributions/sequences, not property catalogue;
- strong portfolio distance;
- good demo path.

Tournament kill question: **can players predict states quickly without feeling they are solving a hidden graph or wanting numeric tension gauges?**

## S2 — G5C37 Zero-G Tool Orbit
Core promise: throw one carried tool into a predictable authored orbit, let it keep acting as a persistent second actor while you move elsewhere, then catch/hand it to another orbit.

Why tournament-worthy:
- strongest action/GIF identity;
- repeated verb is tactile and controller-oriented;
- authored tracks keep technical burden low;
- player + persistent tool create second-order choreography without clone/AI systems.

Tournament kill question: **does snapped orbit/catch control feel empowering, and can late play remain more than periodic switch-hitting?**

## S3 — G5C17 Door Memory
Core promise: a doorway and crossing object swap HEAVY/LIGHT state, so every crossing changes both the object's physical role and what the doorway will give the next object.

Why tournament-worthy:
- extremely cheap deterministic prototype;
- unusual sequential-state rule;
- one binary property already supports 12 non-identical paper kernels;
- excellent controller/readability potential.

Tournament kill question: **does a full premium campaign exist without adding more property families or becoming box-hauling/Sokoban friction?**

## S4 — G5C21 Broken Rule Workshop
Core promise: change exactly one physical rule cartridge in a live machine, run it immediately, watch the causal failure, and diagnose the bad rule through experiments.

Why tournament-worthy:
- clean experiment-observe-revise loop;
- failure itself is entertaining content;
- strong 20-minute demo shape;
- deterministic and low runtime complexity.

Tournament kill question: **can reusable machine modules keep the game embodied and varied without turning into a programming editor or expensive bespoke-machine authoring project?**

---

# 13. Phase-1 decision

**PHASE 1 OPPORTUNITY DISCOVERY = COMPLETE.**

Evidence threshold for a tournament is met because:
- 60 clean-slate seeds were generated across broad territories;
- all active candidates received mature-state attacks rather than premise-only ranking;
- direct/current nearest-neighbor pressure killed attractive but less-ownable concepts;
- final entrants each have a clear 5–15 second repeated verb;
- each supports a plausible 15–25 minute demo;
- each is cheap enough to graybox before full production;
- each has an identifiable second-order depth source;
- each has a specific kill question that Phase 2 can test destructively;
- none requires reopening Games #001–#004 mechanics as canon.

No winner is selected. Production implementation remains prohibited in the factory.

---

# 14. NEXT ACTION — PHASE 2 / CONCEPT TOURNAMENT RUN 1

Create `GAME5_TOURNAMENT.md` and test **G5C02, G5C37, G5C17, G5C21** under the same destructive rubric.

At minimum:
1. Freeze one-sentence pitch and exact smallest vocabulary for each entrant before scoring.
2. Build a normal-play **10-second mute trailer trace** for each; reject explanations that require captions to reveal the core causality.
3. Build a **20-minute demo paper trace** for each with first independent decision, differentiator reveal and closing synthesis.
4. Build at least **12 mature-state kernels per entrant** or reuse/expand Run-3 kernels where valid, then classify distinct reasoning families rather than merely count levels.
5. Estimate a 4–8 hour campaign/content burden without adding rescue mechanics.
6. Attack dominant strategies, brute force, waiting, execution burden, UI abstraction, tutorial burden and controller friction.
7. Attack implementation ambiguity and define the cheapest one-week kill prototype for each.
8. Re-run nearest-neighbor/current-store pressure where the exact product positioning needs validation.
9. Score at least: hook, repeated feel, systemic depth, demo strength, market distance, production risk, content burden, accessibility/readability and portfolio distance.
10. Eliminate at least one entrant if destructive evidence supports it; do **not** force an elimination for tournament drama.
11. Do not select the final Game #005 winner until the tournament evidence is strong enough; Phase 2 may require multiple runs.
12. Do not begin production implementation.
