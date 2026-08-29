# GAME #006 — STITCHSPACE — CONTENT ARCHITECTURE

Last updated: 2026-08-29
Factory run: **6**
Phase: **5 — Content Architecture**
Selected concept: **G6C01 Stitchspace**
Product thesis: **LOCKED**
Mechanical architecture: **COMPLETE ON PAPER**
Content architecture: **COMPLETE ON PAPER**
Production implementation started: **NO**
DESIGN COMPLETE: **NO**

This file is the canonical Phase-5 content contract for Stitchspace. It implements `GAME6_PRODUCT_THESIS.md` and `GAME6_MECHANICAL_ARCHITECTURE.md` without adding a new primary verb. If a content idea needs a new seam power, hidden socket rule, free placement, timing challenge, portal modifier, gravity trick, new traversal ability or bespoke physics exception to become interesting, that content is invalid for the frozen 1.0 design unless an earlier phase is explicitly reopened.

---

# 1. Content goals

The campaign must prove that adjacency replacement remains interesting after the tutorial. Content succeeds only if the player repeatedly reasons about **what connection is lost as well as what connection is created**.

The content architecture therefore optimizes for:
1. early legibility of replacement rather than portal placement;
2. useful disconnection as a positive tool;
3. orientation as visible spatial consequence rather than bookkeeping;
4. alternating topology edits with physical use of the world;
5. state-dependent rewiring after player/object movement;
6. bounded one-/two-seam reasoning with rare justified three-seam synthesis;
7. multiple abstract solution skeletons instead of cosmetic socket permutations;
8. discrete deterministic authoring that remains solver-auditable;
9. compact rooms and low asset burden;
10. a representative demo that reaches the true product hook before ending.

---

# 2. Campaign target and release tolerance

## 2.1 Main campaign

Frozen design target: **34 main cases, C01–C34**.

Acceptable pre-freeze production cut range: **30–36** only if pacing/novelty review proves that a smaller or slightly larger set is stronger. Phase 11 should freeze one exact count. The current Phase-5 authoring architecture is built around 34.

Target first clear: **5–8 hours**, with ~4 hours treated as the lower commercial warning threshold rather than a content target.

## 2.2 Demo

Exactly **5 representative demo cases: DEMO01–DEMO05**.

The demo is not simply C01–C05 copied. It may share tutorial logic/content atoms, but the sequence must compress the commercial proof into **15–25 minutes** and end only after useful disconnection and state-dependent replacement have been experienced.

## 2.3 Remix / mastery

Target **8 remix cases, R01–R08**.

Acceptable range: 6–10 only if later anti-isomorphism review proves each one materially changes reasoning.

Main cases may expose optional mastery predicates. Remix cases are separate content only when they change a causal dependency or dominant solution skeleton; they are never socket recolors or harder geometry alone.

---

# 3. Campaign bands and teaching order

## Band A — C01–C06: Learn replacement

Goal: destroy the portal mental model before it forms.

### C01 — Existing seam / first crossing
Teach one persistent seam and ordinary crossing. No endpoint move until the player has physically used the existing adjacency.

### C02 — Move one endpoint
First `MOVE_SEAM_ENDPOINT`. The old adjacency disappearing must be mechanically necessary to continue, not just visual feedback.

### C03 — One seam, two sequential destinations
Route an object through the seam, then relocate the same endpoint for the player. Teaches scarce reuse.

### C04 — Orientation
A deterministic rolling/commandable object must emerge into the correct local lane. The correct seam target is selected by visible boundary orientation, not distance.

### C05 — Useful disconnection
Allow a moving blocker/object to cross, then relocate the endpoint so the old route disappears. The disconnection itself produces safety/access.

### C06 — First loop
One seam plus ordinary passages creates/breaks a small cycle. The case cannot be solved by simply connecting current room to goal.

Band A constraints:
- 2–3 rooms normal;
- 1 seam only;
- <=6 exposed legal sockets;
- <=2 relevant entities;
- no occupancy-lock lesson yet beyond normal settled crossing;
- every case should be explainable in one sentence after completion.

## Band B — C07–C14: Replacement becomes default reasoning

Goal: combine the primitive ideas while preserving readability.

### C07 — Lost return route
A useful endpoint move strands a previous route and requires planning a different return path through an ordinary passage.

### C08 — Object-before-player ordering
One seam, object and player need different adjacency states. Crossing order is the puzzle.

### C09 — Isolation objective
A required body/region must end disconnected from another region after the useful crossing.

### C10 — Orientation + cut
The correct exit orientation creates a later need to destroy that same adjacency.

### C11 — State-dependent rewire
The best target socket changes after an entity has crossed/moved. Static initial graph matching is insufficient.

### C12 — Occupancy lock introduction
A deterministic mover occupies a seam for one canonical crossing step. The player cannot relocate the occupied endpoint until settlement. Pause/Step-style presentation is later Phase 6; mechanically no reflex timing is required.

### C13 — First two-seam case
Introduce seam #2 only as a temporary preservation bridge while seam #1 is relocated.

### C14 — Two-seam swap
Two room pairings must be changed while one critical route remains available.

Band B constraints:
- 2–4 rooms;
- C07–C12 one seam;
- C13–C14 exactly two seams;
- <=8 legal sockets normal;
- <=3 relevant entities;
- at least 4/8 cases must use disconnection/isolation/old-route loss as a positive dependency.

## Band C — C15–C24: Mature topology grammar

Goal: no new primitive mechanic. Difficulty comes from topology state and entity consequences.

Dominant families distributed across the band:
- temporary cycle creation;
- graph cut/isolation;
- orientation-dependent routing;
- preserve-one/cut-one with two seams;
- object/player crossing order;
- state-dependent endpoint relocation;
- occupancy and deterministic mover sequencing;
- alternate solution character.

Representative blueprints:

### C15 — Temporary cycle / one seam
Create a cycle, use it to approach a socket from a useful local side, then break it for completion.

### C16 — Two-region isolation
Move a blocker/object into a region, cut its adjacency, then reuse the same seam elsewhere.

### C17 — Two seams / preserved lifeline
One seam must remain fixed while the other is repeatedly reused, then their roles reverse.

### C18 — Orientation relay
One object crosses two distinct seam states; the first crossing changes which orientation is useful for the second.

### C19 — Alternate skeleton case
At least two validated baseline solutions: one based on isolation, another on orientation/reuse. Both materially differ in causal skeleton.

### C20 — Mover occupancy without timing
Automatic mover follows a deterministic finite route. Endpoint relocation is allowed only after canonical settlement. Puzzle is ordering, not reaction.

### C21 — Cut before connect
The first useful action is to destroy an existing adjacency even though it temporarily reduces reachability.

### C22 — Two-seam room-pair permutation
Swap which room pairs touch while preserving entity separation constraints. Brute-force endpoint permutations must not be shortest reasoning.

### C23 — State-dependent two-seam rewire
An object crossing changes later reachability so the same endpoint placement has different value before and after the crossing.

### C24 — Midgame synthesis
4 rooms, 2 seams, one ordinary loop, player plus one object/mover, >=2 solution skeletons, and direct current-room-to-goal shortcut audit must pass.

Band C constraints:
- 3–5 rooms;
- 1–2 seams; at least 7/10 use two seams;
- <=10 legal sockets normal;
- <=4 relevant entities;
- no new globally meaningful socket family;
- every case requires a documented `lost_adjacency_dependency`.

## Band D — C25–C31: Causal compression and mastery

Goal: deeper reasoning from the same vocabulary, not larger maps.

### C25 — One edit, two consequences
One endpoint move both routes an entity and isolates another route. Baseline solution rewards causal compression but does not score raw move count.

### C26 — Preserve/cut inversion
The seam that looked like the stable lifeline becomes the one that must be sacrificed later.

### C27 — Two valid topology plans
Two distinct complete approaches with comparable length but different skeletons.

### C28 — Mover + orientation + isolation
A deterministic mover crosses, changes facing/room state, then must be disconnected from a previous region before the player can exploit the new route.

### C29 — Three-way objective conjunction
At most three material objective predicates: player position, object state/location and connection/disconnection relation.

### C30 — Rare third seam #1
First allowed three-seam case. Must include explicit `three_seam_justification` proving the third seam represents simultaneous preservation of two relationships while a third is being rewritten; removing one seam must fundamentally change the problem, not merely make it harder.

### C31 — Late alternate-solution audit
At least three solver-confirmed valid solution paths, but only if they fall into >=2 materially distinct skeleton families. Many permutations of one plan do not count.

Band D constraints:
- 3–5 rooms;
- 2 seams default;
- <=1 three-seam case in this band unless later review proves exceptional need;
- <=10 sockets preferred, 12 hard pre-freeze ceiling;
- <=4 relevant entities;
- solver reachable-state budget must remain inside Phase-5 thresholds below.

## Band E — C32–C34: Final synthesis

### C32 — Cut/loop synthesis
Use a temporary cycle, break it deliberately, then reuse the freed endpoint to complete a second dependency.

### C33 — Rare third seam #2 or strongest two-seam case
Default is a difficult two-seam case. A third seam is allowed only if the explicit justification passes and three-seam campaign budget remains <=3.

### C34 — Capstone
4–5 rooms preferred, two seams default, rare third only with exceptional proof. Must combine:
- useful lost adjacency;
- state-dependent rewiring;
- orientation or loop dependency;
- physical use between edits;
- at least two solution skeleton families if tractable;
- no direct current-room-to-goal shortest shortcut;
- no timing/dexterity requirement;
- no new rule introduced in the finale.

The capstone should feel like mastery of adjacency replacement, not a maximal-size graph.

---

# 4. Allowed content vocabulary ceiling

## 4.1 Rooms
Normal: **2–5 rooms**. Six-room case requires explicit readability justification and should be rejected unless it creates a materially new topology relation that cannot be expressed more clearly with five.

## 4.2 Edge sockets
- authored legal attachment points only;
- <=10 exposed legal sockets normal mature target;
- <=12 hard pre-freeze ceiling;
- no one-off socket powers;
- meaningful differences are room, location, local orientation, enabled state where already globally defined, crossing class and occupancy.

## 4.3 Ordinary passages
Use fixed passages to create stable loops/cuts/reference topology. They are not decorative extra doors. A passage should normally participate in reachability or orientation reasoning.

## 4.4 Seams
- 1 seam teaching baseline;
- 2 seams mature norm;
- 3 seams rare ceiling;
- target <=3 main-campaign three-seam cases;
- each 3-seam case requires `three_seam_justification` and solver-state review.

## 4.5 Entities
Allowed baseline gameplay entity roles:
1. PLAYER;
2. deterministic pushable/commandable object;
3. deterministic automatic mover;
4. hazard/blocker represented by the same discrete occupancy/movement rules.

No inventory items, keys, combatants, physics projectiles, free NPC AI or bespoke per-case movement systems are added merely for variety.

Normal mature cases: <=4 materially relevant entities including the player. More requires explicit necessity review.

---

# 5. Canonical case schema

Every authored main/demo/remix case must serialize the following data or equivalent typed fields.

## Identity/version
- `case_id`
- `content_version`
- `title_key`
- `campaign_band`
- `case_kind` = MAIN / DEMO / REMIX
- `prerequisite_case_ids`

## World
- `rooms[]`
- room-local nodes/lanes
- `edge_sockets[]`
- `ordinary_passages[]`
- socket orientation/crossing metadata
- socket enabled-state source where globally supported

## Seams
- `seams[]`
- stable seam IDs
- initial endpoint A/B socket IDs
- directionality class
- legal endpoint destination set if intentionally narrowed
- `three_seam_justification` when seam count = 3

## Entities
- `entities[]`
- class
- initial room/node/facing
- deterministic movement rule if automatic
- occupancy class/capacity interactions
- objective-relevant flags

## Goals/invariants
- `mandatory_objectives[]`
- `hard_invariants[]`
- `soft_protected_conditions[]`
- completion settlement requirements

## Solution evidence
- `known_baseline_fixtures[]`
- semantic command sequence or deterministic fixture representation
- expected final canonical hash/state predicate
- `baseline_solution_skeleton`
- optional alternate skeletons
- `lost_adjacency_dependency`
- `direct_goal_shortcut_audit`
- `physical_use_between_edits_proof`
- `state_dependent_rewire_proof` when required by band

## Mastery/remix
- optional `mastery_predicates[]`
- `mastery_distinction_note`
- `known_mastery_fixture` where mastery exists
- remix source case ID
- `changed_causal_dependency`
- source/remix skeleton tags

## Validation metadata
- expected reachable-state estimate
- solver budget tier
- transform/reasoning tags
- ambiguity/content-warnings accepted only with explicit reviewed reason
- author notes that do not override global mechanics

No arbitrary script/callback field may alter global seam, crossing, movement, orientation or Undo semantics.

---

# 6. Solution fixture contract

Every shipped case must have at least one known baseline solution fixture that:
1. starts from canonical initial state;
2. uses only semantic legal commands;
3. settles deterministically after every transaction;
4. reaches required completion predicates;
5. records expected final canonical hash or equivalent exact state proof;
6. records an abstract solution skeleton;
7. records which lost adjacency was materially useful or costly;
8. proves physical use/state change occurs between topology edits wherever required by campaign band.

A case with alternate solutions should retain at least one representative fixture per materially distinct skeleton family where practical.

Known fixtures are tests, not the only accepted player solutions.

---

# 7. Abstract solution-skeleton taxonomy

The anti-repetition system uses skeleton families, not raw move counts.

Canonical initial taxonomy:

- **S1 ROUTE_THEN_REPLACE** — create adjacency, cross/use it, relocate same endpoint because old route is no longer wanted.
- **S2 OBJECT_FIRST / PLAYER_SECOND** — route another entity under one topology, then reuse seam for the player.
- **S3 INVITE_THEN_CUT** — permit entity/hazard to cross, then deliberately remove adjacency to isolate it.
- **S4 ORIENTATION_ROUTE** — socket pairing selected primarily for exit-facing/lane consequence.
- **S5 CREATE_LOOP_THEN_BREAK** — create a cycle for access/orientation, use it, then remove it.
- **S6 PRESERVE_ONE / REWIRE_ONE** — with two seams, maintain a critical adjacency while relocating the other.
- **S7 SWAP_PAIRINGS** — move multiple endpoints to exchange which room pairs are adjacent.
- **S8 STATE_DEPENDENT_REWIRE** — later endpoint target is useful only because an entity/world state changed after earlier traversal.
- **S9 OCCUPANCY_ORDER** — deterministic crossing/occupancy order constrains when an endpoint may move.
- **S10 CAUSAL_COMPRESSION** — one adjacency replacement produces two material beneficial consequences.
- **S11 CUT_FIRST** — deliberately reduce connectivity before creating the useful final route.
- **S12 MULTI_SOLUTION_DIVERGENCE** — case intentionally supports materially different families such as orientation-first vs isolation-first.

Phase 9/10 may refine/merge labels but must not use labels to disguise isomorphic puzzles.

## Anti-isomorphism rules
From C15 onward:
- no consecutive **3-case window** may have the same dominant skeleton family for all three;
- every **5-case window** must contain at least **3 materially distinct dominant skeleton families**;
- simple room/socket renaming, orientation reflection, start/goal swap or adding one redundant endpoint does not make a new skeleton;
- every case must record a short `skeleton_distinction_note` explaining what causal decision differs from nearby cases.

A solver-generated canonical graph isomorphism check may assist, but final distinction is causal reasoning, not graph labels alone.

---

# 8. Lost-adjacency dependency proof

This is the main anti-portal content gate.

For **C07 onward**, every main case must identify at least one meaningful lost-adjacency consequence. For **C15 onward**, that consequence must be material to the known baseline solution and preferably to shortest solver solutions.

Accepted material consequences:
- old route no longer reachable;
- entity becomes intentionally isolated;
- blocker/hazard loses access;
- loop is broken/created;
- orientation opportunity disappears or changes;
- seam resource is freed for another relation;
- preserving an old adjacency becomes the central reason to use a second seam;
- entity movement makes the old relation strategically harmful;
- a future required route is only possible because the previous relation was removed.

Not accepted:
- purely cosmetic old seam animation;
- old adjacency disappears but was never useful/reachable;
- arbitrary rule saying the previous socket must be empty at finish without physical/topological consequence;
- merely forcing extra endpoint moves.

Validator output should classify each known solution as:
- `LOST_ADJACENCY_REQUIRED`;
- `LOST_ADJACENCY_MATERIAL_BUT_ALTERNATIVE_EXISTS`;
- `LOST_ADJACENCY_INCIDENTAL`;
- `UNKNOWN`.

C15+ content may not ship with `INCIDENTAL` or `UNKNOWN` without explicit Phase-10 amendment.

---

# 9. Direct-current-room-to-goal shortcut audit

For every C07+ case, solver/validator checks whether a legal seam endpoint move can directly create adjacency between the player's current area and a goal-area socket.

If yes, search whether that direct connection:
- immediately completes;
- is part of a shortest solution;
- bypasses the case's intended lost-adjacency/state dependency.

From C15 onward, a direct current-room-to-goal seam must **not** be the shortest valid solution in the known initial state when such socket pairing is structurally available, unless the real causal problem remains after that crossing and the shortcut therefore is not actually a shortcut.

Cases failing this audit are repaired by topology/objective/state design, not by adding arbitrary forbidden socket pairs solely to block the obvious solution.

---

# 10. Solver / validator pipeline

Required design-time pipeline:

1. **Schema validation** — required fields/types/IDs/version.
2. **Structural graph validation** — rooms/nodes/passages/sockets exist and references resolve.
3. **Seam legality validation** — exactly two endpoints, no shared sockets, unique orientation mapping.
4. **Entity validation** — deterministic node/lane states and movement rules.
5. **Ambiguity rejection** — contested same-boundary/same-node movement states with no global outcome are invalid.
6. **Known fixture replay** — deterministic baseline completion and expected hash/state.
7. **Reachability search** — bounded BFS/A* over endpoint placements + discrete entity state.
8. **Dead-state sample/report** — identify obvious unrecoverable states for authoring/hints, not player oracle.
9. **Direct-goal audit** — section 9.
10. **Lost-adjacency audit** — section 8.
11. **Physical-use-between-edits audit** — mature known solution cannot collapse into detached seam editing.
12. **Skeleton extraction/report** — abstract solution family plus neighboring-case comparison.
13. **Two-/three-seam state-space audit** — reject permutation bloat.
14. **Moving-entity contention audit** — prove no required solution depends on incidental resolution order.
15. **Remix/mastery distinction audit**.

## Quantitative complexity guardrails

These are Phase-5 authoring targets, not runtime performance promises:
- tutorial/early cases: preferably **<=5,000 reachable canonical settled states** under bounded solver action set;
- normal mature cases: target **<=50,000 reachable settled states**;
- late/complex cases: soft warning above **100,000**;
- any case above **250,000 reachable settled states** requires explicit review and should normally be simplified;
- three-seam case above **100,000** should be presumed overcomplicated until proven otherwise.

State count alone does not measure puzzle quality. A case with 80,000 states and a clear novel dependency may be better than one with 8,000 meaningless permutations. But growth caused mainly by extra sockets/seams/entities without new causal structure is a cut signal.

Solver may use symmetry reduction/canonicalization where it preserves exact solution distinctions.

---

# 11. Two-seam content budget

Two seams appear only after one-seam replacement, disconnection, orientation and reuse are understood.

Target main campaign distribution:
- C01–C12: one seam only;
- C13–C14: introductory two-seam;
- C15–C24: roughly 7 two-seam / 3 one-seam cases;
- C25–C34: mostly two-seam, with up to 2–3 justified three-seam cases.

Two seams must introduce one of:
- preserve-one/cut-one;
- temporary bridge;
- swapped room pairing;
- simultaneous topology commitments;
- entity-specific route ordering.

Invalid use: “same one-seam puzzle but with more possible endpoint combinations.”

---

# 12. Rare three-seam content budget

Hard Phase-5 target: **<=3 main cases**.

A three-seam case is valid only when `three_seam_justification` answers all:
1. What simultaneous relationship must be preserved that two seams cannot express without changing the intended reasoning?
2. What new causal decision appears, rather than merely more permutations?
3. Does solver state remain inside acceptable budget?
4. Is the topology still readable without an abstract graph becoming the main play surface?
5. Can one seam be removed and the case simplified without losing its unique lesson? If yes, use two seams.

Three seams are never an unlock/progression upgrade.

---

# 13. Moving-entity authoring contract

Automatic movers exist to create **state-dependent topology**, not timing tests.

Allowed:
- finite authored lane/node route;
- deterministic one-step advance after a semantic trigger/transaction;
- deterministic boundary crossing when active adjacency exists;
- visible stop/settle nodes;
- one canonical crossing-step occupancy lock;
- Pause/Step-compatible state later in UX.

Forbidden:
- frame-time windows;
- hidden speed races;
- continuous free physics;
- two movers contending for one boundary where stable ID decides winner;
- dependence on animation duration;
- requiring the player to relocate a seam while an endpoint is canonically occupied.

Every moving-entity case must have validator proof that the known baseline fixture encounters no unresolved contention state.

Normal case should use <=2 automatic movers; >2 requires explicit readability/necessity review.

---

# 14. Mastery contract

Mastery is optional and must represent a different causal quality, not punishment for experimentation.

Allowed mastery families:
- **Causal Compression** — achieve same physical goals with a topology plan where one endpoint move serves multiple material consequences.
- **Preservation** — complete while keeping an optional route/entity relation intact.
- **Isolation Discipline** — end with a specific harmful access relation cut while still satisfying main goals.
- **Topology Elegance** — satisfy a declared final adjacency relation in addition to baseline goal.

Not allowed:
- no Undo;
- no restart;
- speedrun time;
- no Pause/inspection;
- hidden minimum click count unless that count corresponds to a materially documented causal plan;
- dexterity/timing restrictions.

Every mastery-bearing case requires:
- `mastery_distinction_note`;
- known mastery fixture;
- evidence that mastery changes causal character or final topology, not only subtracts one redundant action.

---

# 15. Remix contract

A remix must change at least one **causal dependency** from its source case while using frozen mechanics.

Valid changes:
- the adjacency that must be preserved becomes the one that must be cut;
- orientation-first source becomes isolation-first remix;
- one-seam source becomes a two-seam preserve/rewire dependency with materially different skeleton;
- ordinary passage topology changes so a former loop strategy no longer dominates;
- mover/object starting state makes endpoint usefulness state-dependent in a new way;
- objective changes from connection to separation while keeping the physical setting recognizable.

Invalid remix changes:
- mirror/rotate room layout only;
- change socket labels/colors;
- move goal one node;
- add more endpoint options without new dependency;
- require one extra seam move;
- make the same solution longer;
- add time pressure.

Each remix records source and remix dominant skeleton plus `changed_causal_dependency`.

---

# 16. Demo sequence

The demo must prove the commercial thesis in five compact cases.

## DEMO01 — Rooms can become neighbors
Existing seam -> crossing -> first endpoint move. Show old adjacency visibly disappearing.

Commercial proof: this is room adjacency, not a teleport projectile.

## DEMO02 — Orientation
Route one deterministic object so the chosen destination edge determines its useful exit direction.

Commercial proof: which edges touch matters, not merely source/destination room.

## DEMO03 — Scarce reuse
One seam serves object then player. Endpoint replacement makes the previous route unavailable.

Commercial proof: seam is persistent scarce relationship, not an unlimited portal pair.

## DEMO04 — Useful disconnection
Invite a blocker/object/hazard through and deliberately move the endpoint away afterward.

Commercial proof: destroying adjacency is a positive verb.

## DEMO05 — State-dependent synthesis
Three rooms, one seam plus fixed passages or two seams if readability is proven. An entity crosses; its new state changes which adjacency should be created next; solution ends with a deliberate cut/reuse.

Commercial proof: mature play alternates physical world state and topology edits.

Demo exclusions:
- 3 seams;
- more than 4 rooms;
- dense automatic-mover contention;
- late mastery complexity;
- abstract graph UI dependence;
- any mechanic not already in frozen vocabulary.

The demo is invalid if a player can finish all five while describing the mechanic only as “put entrance/exit portals in useful places.”

---

# 17. Representative late solution traces

These are content-shape proofs, not canonical exact level layouts.

## Trace A — isolation-first
1. seam connects R1↔R3; blocker in R3;
2. player opens object route by moving opposite endpoint to R2;
3. blocker crosses into R2;
4. player uses ordinary passage to return to R1;
5. endpoint is moved away from R2, isolating blocker;
6. same seam is reused to connect R1↔R4 goal path.

Material lost adjacency: R1/R2 relation is destroyed specifically to strand blocker.
Skeleton: S3 INVITE_THEN_CUT + S1 ROUTE_THEN_REPLACE.

## Trace B — orientation-first
1. object must enter receiver from west-facing lane;
2. closest room pairing emits wrong orientation;
3. player creates a temporary cycle so object reaches a different source socket;
4. object crosses seam with correct exit facing;
5. seam endpoint is moved, breaking cycle and opening player route.

Material lost adjacency: temporary cycle must be removed to free seam and prevent incorrect return route.
Skeleton: S4 ORIENTATION_ROUTE + S5 CREATE_LOOP_THEN_BREAK.

## Trace C — preserve-one/rewire-one
1. seam A preserves player lifeline;
2. seam B routes object into remote room;
3. object state enables a different useful crossing orientation;
4. seam B becomes temporary lifeline;
5. seam A is now relocated to final goal relation.

Skeleton: S6 PRESERVE_ONE/REWIRE_ONE + S8 STATE_DEPENDENT_REWIRE.

These traces demonstrate hour-scale depth without adding seam powers.

---

# 18. Content exclusions / expansion boundary

1.0 content may not introduce:
- free-surface seam placement;
- momentum/flying/trajectory puzzles;
- room folding/rotation/scaling;
- player gravity manipulation;
- seam colors/elements/rarity/upgrades;
- time clones/time rewind as a mechanic separate from Undo;
- property transfer;
- physics stacking or precision platforming;
- combat encounters;
- procedural infinite campaign;
- level editor required for perceived value;
- hidden one-off socket rules;
- narrative locks requiring bespoke dialogue logic to solve topology.

Potential post-1.0 expansion should first explore new **arrangements of existing topology grammar**. A genuinely new primitive family requires a separate product/design review rather than being slipped into DLC because content ran thin.

---

# 19. Phase-5 content risk gates

## C5-R1 — Portal collapse
Gate: in C15–C34, every known baseline fixture must classify lost adjacency as REQUIRED or MATERIAL; anti-portal shortcut audit must pass.

## C5-R2 — Puzzle isomorphism
Gate: no C15+ three-case window shares one dominant skeleton across all three; every five-case window has >=3 skeleton families.

## C5-R3 — Two-seam permutation explosion
Gate: normal mature reachable-state target <=50k, warning >100k, review required >250k; complexity must be causal, not combinatorial noise.

## C5-R4 — Three-seam readability
Gate: <=3 main cases and explicit justification; default is to cut back to two seams.

## C5-R5 — Stranding busywork
Gate: content review rejects solutions dominated by restoring already-understood routes merely to walk back and forth.

## C5-R6 — Moving-entity timing drift
Gate: known fixtures contain no reflex window and no ambiguous contested boundary state.

## C5-R7 — Direct-goal trivialization
Gate: C15+ direct current-room-to-goal adjacency is not a shortest bypass of the case's causal dependency.

## C5-R8 — Demo miscommunication
Gate: DEMO01–05 include replacement, orientation, scarce reuse, useful disconnection and state-dependent rewire before ending.

---

# 20. Phase-5 acceptance tests

## Campaign/schema
- **C5-01** Main campaign architecture supports C01–C34 without adding a new primary verb.
- **C5-02** Every case has stable ID/version and valid campaign kind/band.
- **C5-03** Every case references only existing rooms/nodes/sockets/passages/seams/entities.
- **C5-04** No case-level callback overrides global seam/crossing rules.
- **C5-05** Normal case stays within 2–5 rooms unless explicit six-room readability justification exists.
- **C5-06** Normal mature case stays <=10 exposed legal sockets; >12 is rejected pre-freeze.

## Solutions / anti-portal
- **C5-07** Every shipped case has at least one deterministic known baseline fixture.
- **C5-08** Every known baseline fixture reaches completion and expected canonical state/hash.
- **C5-09** C07+ records a lost-adjacency dependency.
- **C5-10** C15+ lost-adjacency audit is not INCIDENTAL/UNKNOWN.
- **C5-11** Mature known solution normally alternates topology edit and physical world use/state change.
- **C5-12** C15+ direct-current-room-to-goal audit cannot expose a shortest causal bypass.
- **C5-13** Mature content cannot be solved as a detached sequence of endpoint edits followed by one traversal.

## Skeleton diversity
- **C5-14** Every C15+ case records dominant abstract solution skeleton.
- **C5-15** No consecutive three C15+ cases all share the same dominant skeleton family.
- **C5-16** Every consecutive five C15+ cases contain at least three materially distinct skeleton families.
- **C5-17** Mirroring/renaming/socket permutation alone cannot satisfy skeleton distinction.
- **C5-18** Alternate solutions count as distinct only when causal skeleton differs materially.

## Seam budgets
- **C5-19** C01–C12 use one seam only.
- **C5-20** C13–C14 introduce two seams through preserve/rewire or swap reasoning.
- **C5-21** Two-seam mature cases justify the second seam through a material simultaneous topology dependency.
- **C5-22** Main campaign uses at most three three-seam cases unless later canonical amendment proves need.
- **C5-23** Every three-seam case includes complete `three_seam_justification`.
- **C5-24** Removing a redundant third seam triggers simplification rather than difficulty compensation.

## Solver/complexity
- **C5-25** Structural validator rejects unresolved IDs, duplicate socket occupancy and ambiguous orientation mappings.
- **C5-26** Validator rejects same-boundary movement contention with no global deterministic outcome.
- **C5-27** Solver can replay baseline fixtures from canonical initial state.
- **C5-28** Solver can report direct-goal shortcut status.
- **C5-29** Solver can report lost-adjacency materiality for known/shortest paths where tractable.
- **C5-30** Reachable-state warning triggers above 100k and explicit review above 250k.
- **C5-31** Three-seam case above 100k reachable states is presumed overcomplex pending explicit review.
- **C5-32** State-space growth caused mostly by redundant sockets/seams/entities is a content-cut signal.

## Movers/entities
- **C5-33** Automatic mover uses finite deterministic lane/node rule only.
- **C5-34** No baseline solution depends on animation duration or frame timing.
- **C5-35** Known mover fixture contains no unresolved endpoint/destination contention.
- **C5-36** Normal case uses <=2 automatic movers unless explicit necessity/readability proof exists.
- **C5-37** Endpoint relocation is never required while that endpoint is canonically crossing-occupied.

## Mastery/remix
- **C5-38** Mastery never scores raw Undo/restart/time/Pause usage.
- **C5-39** Every mastery has distinction note and known mastery fixture.
- **C5-40** Every remix records source skeleton, remix skeleton and changed causal dependency.
- **C5-41** Cosmetic mirroring/socket relabeling alone cannot create a remix.

## Demo / content identity
- **C5-42** DEMO01 visibly proves new adjacency replaces old adjacency.
- **C5-43** DEMO02 proves crossing orientation matters physically.
- **C5-44** DEMO03 proves scarce seam reuse.
- **C5-45** DEMO04 proves disconnection is useful.
- **C5-46** DEMO05 proves state-dependent rewire after entity movement.
- **C5-47** Demo contains no three-seam or late dense content.
- **C5-48** Demo can be completed without timing/dexterity mechanics.

## Expansion / implementation readiness
- **C5-49** Campaign does not rely on free placement, folding, momentum, gravity, seam powers or other excluded primitives.
- **C5-50** A fresh Phase-6/implementation session can determine campaign order, schema, solver audits, seam budgets, demo shape and content-validity rules without inventing new game design.

---

# 21. Phase-5 closure

- Main campaign target and cut tolerance defined: **YES**
- Demo target defined: **YES**
- Remix target defined: **YES**
- C01–C34 teaching/campaign bands defined: **YES**
- Representative blueprints from onboarding to capstone defined: **YES**
- Room/socket/entity vocabulary ceiling defined: **YES**
- Complete case schema defined: **YES**
- Baseline/mastery fixture contract defined: **YES**
- Solver/validator pipeline defined: **YES**
- Quantitative state-space guardrails defined: **YES**
- Lost-adjacency dependency proof defined: **YES**
- Direct-to-goal shortcut audit defined: **YES**
- Solution-skeleton taxonomy defined: **YES**
- Anti-isomorphism rules defined: **YES**
- Two-seam budget defined: **YES**
- Three-seam budget defined: **YES**
- Moving-entity constraints defined: **YES**
- Mastery/remix validity defined: **YES**
- DEMO01–DEMO05 commercial proof sequence defined: **YES**
- Expansion/content exclusions defined: **YES**
- Phase-5 risk gates defined: **YES**
- Phase-5 acceptance tests: **50**
- Production implementation started: **NO**
- Content Architecture: **COMPLETE ON PAPER**
- DESIGN COMPLETE: **NO**

## NEXT PHASE

**Phase 6 — UX / Presentation Architecture.**

The next run must freeze how Stitchspace makes changing remote adjacency understandable on desktop and Steam Deck without turning the game into an abstract graph editor. It should define:
- application/screen hierarchy and first-session flow;
- world/camera representation and how multiple stable rooms remain recognizable;
- seam/endpoint/socket visual language and replacement animation;
- old-adjacency-loss + new-adjacency preview boundaries;
- orientation/crossing preview without compass bookkeeping;
- physical endpoint selection/edit flow for mouse+keyboard, keyboard-only and controller-only;
- deterministic focus/navigation graph;
- compact topology overview that explains but does not become the primary editor;
- entity/mover/occupancy visualization;
- causal explanation after edits/crossings;
- Undo/Redo/history presentation;
- accessibility, reduced motion, no-audio, color independence and scalable UI;
- Steam Deck 1280×800 target;
- demo onboarding/presentation flow;
- Pause/Step semantics for deterministic movers if used;
- save/recovery messaging boundaries;
- numbered Phase-6 acceptance tests and empirical readability gates.
