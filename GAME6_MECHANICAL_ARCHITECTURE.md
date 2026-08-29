# GAME #006 — STITCHSPACE — MECHANICAL ARCHITECTURE

Last updated: 2026-08-29
Factory run: **5**
Phase: **4 — Mechanical Architecture**
Selected concept: **G6C01 Stitchspace**
Product thesis: **LOCKED**
Mechanical architecture: **COMPLETE ON PAPER**
Production implementation started: **NO**
DESIGN COMPLETE: **NO**

This file is the canonical mechanical contract for Stitchspace. It refines `GAME6_PRODUCT_THESIS.md` without adding a new primary verb. If convenience conflicts with the Product Thesis, the Product Thesis wins unless explicitly reopened.

The game is not a portal-placement simulator. Its mechanical center is the atomic replacement of one room-boundary adjacency by another using a scarce persistent seam.

---

# 1. Mechanical design goals

The mechanics must preserve five properties:

1. **Adjacency replacement is the repeated verb.** Moving a seam endpoint creates one adjacency and destroys the previous adjacency atomically.
2. **World state matters after topology changes.** Player/object location, orientation, isolation, occupancy and future reachability make the same seam useful in different ways over time.
3. **All authoritative state is discrete and deterministic.** Frame delta, renderer state, animation interpolation and physics-contact order never decide gameplay.
4. **Legal mistakes are observable and reversible.** Bad but structurally valid edits commit; illegal edits reject before mutation.
5. **The game remains physically readable.** Solver/state representation may be graph-like internally, but the player acts on rooms, seams and visible edge sockets.

---

# 2. Canonical world model

## 2.1 Case

A `CaseDefinition` contains:
- stable `case_id` and content version;
- 2–5 normal rooms, exceptionally 6 only if later content validation proves readability;
- room-local traversal nodes/lanes;
- ordinary passages;
- edge sockets;
- 1–2 seams normally, rare authored 3-seam ceiling;
- discrete entities;
- initial entity state;
- initial seam endpoint state;
- objectives and protected invariants;
- allowed endpoint destinations if narrower than global structural legality;
- known baseline solution fixtures;
- optional mastery predicates;
- authoring metadata/solution-skeleton tags.

No case-level gameplay callback may override global seam/crossing semantics. Case data chooses instances and initial state, not new laws.

## 2.2 Room

A room has:
- stable `room_id`;
- authored local traversal graph;
- zero or more edge sockets;
- zero or more ordinary passages;
- deterministic local orientation frame;
- optional static tags needed by objectives/presentation.

Rooms do not rotate, scale, fold, merge or overlap mechanically. Their local identity and coordinate frame are stable for the entire case.

## 2.3 Local traversal node / lane

Entities occupy authored logical nodes or lanes rather than free continuous coordinates for gameplay authority.

A node stores:
- stable ID;
- owning room;
- local facing/orientation metadata if relevant;
- adjacency to other local nodes;
- optional socket/passsage boundary association;
- occupancy class/capacity where needed.

Presentation may interpolate motion between nodes.

## 2.4 Edge socket

An edge socket is the only legal attachment point for a seam endpoint.

A socket stores:
- stable `socket_id`;
- owning room;
- boundary side / visible local facing (`N/E/S/W` in a 2D/cutaway representation or equivalent finite authored orientation in later presentation);
- local entry node;
- local exit node if distinct;
- supported crossing classes;
- enabled/disabled state source if stateful;
- authored compatibility tags only when globally meaningful;
- deterministic focus order metadata.

Baseline sockets do not possess unique one-off powers. Their meaningful difference is location, orientation and current structural availability.

## 2.5 Ordinary passage

An ordinary passage is a fixed authored adjacency between two local boundary nodes/rooms.

Properties:
- never consumes a seam;
- cannot be moved by the player;
- may be traversed by compatible entities;
- orientation mapping is authored and visible;
- may participate in loops/cuts alongside seams.

Ordinary passages exist to provide stable topology against which seam replacement becomes meaningful.

## 2.6 Seam

A seam is a persistent scarce adjacency resource with exactly two endpoints, A and B.

A seam stores:
- stable `seam_id`;
- endpoint A socket;
- endpoint B socket;
- endpoint occupancy locks;
- crossing directionality class (`BIDIRECTIONAL` baseline; authored `A_TO_B` / `B_TO_A` allowed only when visibly represented and justified);
- derived orientation mapping;
- active/inactive structural validity state;
- provenance/history information for explanation only.

A seam is not two independently created portals. It is one persistent relationship whose endpoint can be relocated.

## 2.7 Entity

Baseline entity classes are deliberately small:
- `PLAYER`;
- `PUSHABLE_OR_COMMANDABLE_OBJECT` only where local deterministic movement is needed;
- `AUTOMATIC_MOVER` such as a rolling body using authored lanes;
- `HAZARD_OR_BLOCKER` represented through the same discrete movement/occupancy contracts when it must move.

An entity stores:
- stable `entity_id`;
- class;
- current room/node/lane;
- local facing/orientation;
- movement state (`SETTLED`, `CROSSING`, `LOCAL_MOVE_PENDING`, etc.);
- if crossing, exact source socket, seam/passage, destination socket and canonical crossing phase;
- objective-relevant flags;
- deterministic collision/occupancy relation if applicable.

There is no authoritative rigid-body velocity, momentum vector or free trajectory in baseline mechanics.

---

# 3. Seam orientation mapping

## 3.1 Finite mapping

Every socket has a visible outward boundary direction. Crossing a seam maps local facing according to the two connected socket frames.

The canonical rule is finite and geometric:

1. entity approaches source socket from the room interior toward the source boundary;
2. crossing conceptually moves through the seam into the destination boundary;
3. entity emerges from the destination boundary into that destination room;
4. its local forward/facing is the destination socket's inward direction, with any lateral lane index mapped by an authored finite socket-lane mapping.

For four-direction rooms this means a crossing from any source side to any destination side has one of a finite set of visible quarter-turn/half-turn/straight mappings. No arbitrary numeric rotation exists.

## 3.2 Player-facing preview

Before a seam edit commits, the game can preview:
- source endpoint that will be removed;
- target socket;
- new paired socket relation;
- the resulting finite crossing orientation at both ends.

The UI may show arrows/room-edge geometry but never requires compass arithmetic.

## 3.3 Entity facing transform

Entities that care about facing adopt the canonical exit-facing defined by destination socket. Local carried state is preserved unless another globally defined entity rule says otherwise.

No seam changes magnitude/speed/resource properties. Seam crossing changes adjacency and orientation only.

---

# 4. Core command — MOVE_SEAM_ENDPOINT

Canonical command:

`MOVE_SEAM_ENDPOINT(seam_id, endpoint_selector, target_socket_id, expected_revision, command_id)`

Endpoint selector is exactly `A` or `B`.

## 4.1 Validation order

Validation is performed against one immutable pre-command canonical state:

1. command envelope is well formed;
2. `command_id` has not already been accepted for another result;
3. `expected_revision` / expected canonical hash matches current state;
4. seam exists and selected endpoint exists;
5. target socket exists and is enabled;
6. target socket is not already occupied by another seam endpoint unless a later explicit global swap command exists — baseline has no such command;
7. target socket is not the socket currently occupied by the opposite endpoint of the same seam;
8. selected endpoint is not occupancy-locked by an in-progress crossing;
9. target socket is not occupancy-locked by an in-progress crossing or incompatible settled entity state where the socket itself has bounded occupancy;
10. seam directionality/compatibility permits the resulting pair;
11. case-authored legal-destination restriction, if any, permits the target;
12. resulting connection has a unique finite orientation/lane mapping;
13. structural invariant checks pass.

If any structural validation fails, command rejects with no domain mutation and exact reason.

## 4.2 Atomic commit

If valid, commit is atomic:

1. capture pre-transaction checkpoint/history parent;
2. remove adjacency between selected endpoint's old socket and opposite endpoint socket;
3. detach selected endpoint from old socket;
4. attach selected endpoint to target socket;
5. create new seam adjacency between target and opposite endpoint socket;
6. recompute derived orientation/lane mapping;
7. update any reachability/objective facts that are defined as immediate topology facts;
8. increment revision;
9. persist/store the resulting canonical transaction checkpoint according to later technical spec;
10. hand result to presentation.

There is no observable canonical state in which both old and new adjacencies exist, and none in which the seam has only one endpoint.

## 4.3 Same-socket no-op

Moving an endpoint to its current socket is structurally legal only as a rejected `NO_CHANGE` command, not an accepted history mutation. It does not increment revision.

## 4.4 Legal but strategically bad edit

A move that strands the player, isolates a needed object, breaks a protected route that is not itself a hard invariant, or makes the current state unsolvable may still be legal and commit.

The player learns by consequence and can Undo.

## 4.5 Structural illegality

Examples that reject before mutation:
- target socket already owns another seam endpoint;
- endpoint is locked by a crossing;
- target cannot produce unique finite lane/orientation mapping;
- edit violates a hard authored protected invariant explicitly defined as `must never become false`;
- target is disabled by current world state;
- command is stale/duplicate-invalid.

A structural rejection never consumes an Undo history entry.

---

# 5. Crossing model

## 5.1 Canonical crossing transaction

A seam or ordinary-passage crossing is a discrete domain action/resolution, not a renderer event.

For a player-controlled entity, a crossing begins when a valid semantic move/interact command chooses a boundary transition.

For an automatic mover, crossing begins when its deterministic local movement step reaches a compatible boundary transition.

Canonical crossing sequence:

1. validate source entity/node and active adjacency from one pre-step state;
2. reserve source boundary and destination boundary occupancy needed for this crossing;
3. set entity to `CROSSING` with exact source/destination relation;
4. lock relevant seam endpoint(s) for the canonical crossing duration;
5. resolve one canonical crossing step;
6. place entity at destination local entry node with mapped orientation;
7. release crossing locks;
8. evaluate immediate local occupancy/objective consequences;
9. settle entity or continue a bounded deterministic automatic movement chain.

Presentation may make this visually continuous; authority remains discrete.

## 5.2 When an endpoint is movable

An endpoint is movable only if:
- no entity currently has a crossing transaction whose active boundary includes that endpoint;
- no source/destination reservation for the current canonical step includes that endpoint;
- target socket is structurally free.

The player cannot cut a seam out from under an entity during an authoritative crossing.

## 5.3 Occupancy duration

Baseline crossing occupies endpoints for exactly one canonical crossing step. Later content may use long visual travel but not longer hidden mechanical timing.

If an automatic mover begins crossing during an accepted transaction, topology cannot change until that crossing step settles. No reflex race exists.

## 5.4 Simultaneous crossing

Baseline content should avoid same-seam ambiguous simultaneous crossing unless the global rule resolves it deterministically.

Global resolution:
- collect all crossing intents from the same start-of-step state;
- if intents use disjoint seam/passage endpoint resources, they may resolve as one simultaneous group;
- if two intents contend for the same endpoint or destination node and the content has no unique authored compatibility outcome, the state is invalid content and must be rejected by the content validator;
- stable ID ordering may serialize already independent results for storage but cannot decide who “wins” a physical contention.

---

# 6. Deterministic movement

## 6.1 Player movement

Player moves between authored local nodes and through active passages/seams using semantic commands. Baseline challenge does not depend on speed, free steering, jumping precision or reaction time.

## 6.2 Automatic movers

An automatic mover has a finite deterministic rule, e.g.:
- advance to the next node on an authored lane when unblocked;
- cross the active adjacency if the lane terminates at a compatible boundary;
- settle/stop at an authored stop node;
- trigger a globally defined blocker/hazard consequence.

Each automatic movement chain is bounded. Content cannot require indefinite background simulation.

## 6.3 Pushable/commandable objects

If objects are moved by player interaction, their command is discrete: select object + legal adjacent node/transition. No free pushing physics is gameplay authority.

The exact interaction surface can be chosen in Phase 6, but the domain result must be finite and predictable.

## 6.4 Movement resolution order

One accepted domain command resolves:

1. validate semantic command against pre-state revision/hash;
2. commit direct requested state change (topology edit or local entity move);
3. build automatic movement/crossing intents from the resulting shared canonical state;
4. form non-conflicting simultaneous groups;
5. resolve crossings/local movements;
6. apply occupancy/blocker/objective consequences;
7. repeat automatic movement steps while globally defined active movers remain and chain ceiling not reached;
8. settle;
9. evaluate completion/invariants/mastery facts;
10. record one transaction checkpoint.

Frame time and scene order are irrelevant.

## 6.5 Chain ceiling

A single accepted action may cause at most **24 canonical automatic movement/crossing steps** before a safe deterministic `CHAIN_LIMIT_REACHED` state.

Known shipped baseline solutions must not rely on reaching the ceiling.

---

# 7. Seam counts and ordering rules

## 7.1 One seam

One seam is the teaching baseline and remains mechanically rich through:
- endpoint replacement;
- orientation;
- useful disconnection;
- loops with ordinary passages;
- object/player ordering;
- occupancy.

## 7.2 Two seams

Two seams are the normal mature ceiling. They may create:
- temporary bridge while another seam is relocated;
- swapped room pairings;
- preserve-one/cut-one decisions;
- loop/cut interactions;
- entity-specific route ordering.

## 7.3 Rare third seam

A case may use 3 seams only if content data includes a `three_seam_justification` proving the third seam introduces genuine simultaneous-topology reasoning rather than more search space.

Phase-5/10 review should keep such cases rare; default target <=3 main campaign cases unless evidence proves strong value.

## 7.4 Ambiguity rejection

Content is invalid if:
- two seam endpoints can occupy one socket;
- crossing mapping is not unique;
- two simultaneous interactions contend for the same boundary with no globally defined outcome;
- a target socket's enabled state depends on unordered side effects from the same step;
- a solution depends on event iteration/hash/scene order.

---

# 8. Objectives and invariants

## 8.1 Objective predicates

Objectives are declarative predicates over canonical state, e.g.:
- player at goal node;
- object X at target node/room;
- entity Y isolated from region Z under current active adjacency;
- required rooms connected/disconnected under a stated relation;
- specific entity facing at receiver node;
- all protected entities in allowed set of rooms;
- sequence-completion flag produced by globally defined interaction.

A case may require conjunctions of a small number of meaningful predicates.

## 8.2 Protected invariants

Two kinds:

### Hard invariant
May never be violated. A command that would violate it rejects structurally.
Examples should be rare and obvious: a seam cannot attach to a destroyed/disabled socket; an entity may not overlap an impossible occupied node.

### Soft/protected objective condition
May become false through a legal bad move. The move commits and the UI explains the consequence. This is preferred for puzzle experimentation.

## 8.3 Completion

Case completes when all mandatory completion predicates are true in a settled canonical state.

Completion is not evaluated during an unresolved crossing/movement chain.

## 8.4 Dead end / unsolvable state

The game does not need to prevent every legal unsolvable state. Instead:
- exact Undo/Restart must recover immediately;
- solver tooling may mark `KNOWN_DEAD_END` for hint/UI purposes only where proof is cheap;
- baseline tutorial cases avoid invisible irreversible traps before Undo/replacement is taught;
- content review rejects tedious strand/recover loops that add no reasoning.

The normal player UI should not automatically announce “unsolvable” if that would become a solution oracle.

---

# 9. Undo / Redo / history

## 9.1 Transaction boundary

One accepted semantic player action plus all deterministic automatic consequences it triggers is one history transaction.

Examples:
- one endpoint move and resulting immediate automatic mover chain;
- one player/object movement command and resulting crossings;
- one explicit interact command and its deterministic consequences.

Derived movement steps are nested in the parent transaction, not separate Undo presses.

## 9.2 Undo

Undo restores the exact canonical pre-transaction checkpoint:
- seam endpoints;
- socket states;
- all entity room/node/facing/movement state;
- occupancy/reservations;
- objective/invariant facts;
- revision/history cursor;
- deterministic auxiliary flags.

It is state restoration, not inverse animation/simulation.

## 9.3 Redo

Redo reapplies/restores the exact stored transaction result while its branch is intact.

A new accepted domain-changing command after Undo truncates the active Redo branch.

Rejected commands do not alter history.

## 9.4 No experimentation penalty

Undo count, restart count, thinking time, Pause/inspection use and input method are not baseline scoring dimensions.

---

# 10. Canonical state and hash

A canonical case-state serialization includes, in stable sorted order:
- case/content version;
- revision;
- each seam ID with endpoint A/B socket IDs and directionality;
- every stateful socket enabled/disabled state;
- every entity ID with room/node/facing/movement state and any canonical flags;
- active crossing reservations/occupancy locks if state may persist at a checkpoint;
- objective-relevant flags;
- history branch/cursor identifiers only where needed for persistence, excluded from pure gameplay-equivalence hash if technically separated later.

It excludes:
- animation/tween progress;
- camera state;
- selected UI focus unless selection itself is a domain command (baseline: no);
- frame/tick time unrelated to canonical movement;
- floating-point renderer transforms;
- audio state;
- particle effects.

Canonical hash is computed from deterministic stable serialization. Same case version + same semantic command sequence from same initial state must produce the same gameplay hash.

---

# 11. Solver state / bounded search assumptions

The intended solver state is finite:
- seam endpoint placement combinations over finite sockets;
- discrete entity nodes/facing;
- finite stateful socket/entity flags;
- bounded automatic movement state;
- no continuous velocity or timers.

## 11.1 Search actions

A design-time solver may enumerate:
- legal endpoint moves;
- legal player/object movement/interact commands;
- automatically resolved deterministic consequences.

## 11.2 Search purpose

Solver/validator is used for:
- prove at least one baseline solution fixture;
- detect direct-to-goal shortcut routes;
- detect accidental trivial solution after seam move;
- find obvious dead states;
- compare shortest/known solution skeletons;
- test whether lost adjacency ever materially matters;
- estimate state-space blowup before shipping dense two-/three-seam cases.

The solver is not a player-facing auto-solve feature.

## 11.3 Search bounds

Normal authored cases should target a reachable canonical state count that is comfortably enumerable offline by tooling. Phase 5 may set quantitative thresholds after sample content exists.

If a case's solver state explodes mainly because of extra rooms/sockets/seams rather than meaningful reasoning, the content should be simplified instead of raising tooling complexity.

---

# 12. Difficulty / balance knobs

Allowed global knobs:
- number of rooms;
- number of exposed legal sockets;
- number of seams (1, 2, rare 3);
- amount/topology of ordinary passages;
- number of relevant entities;
- number of material objective predicates;
- orientation importance;
- whether occupancy matters;
- number of required topology state transitions;
- number of materially distinct viable solution paths;
- visibility distance/overview complexity as presentation only;
- hint information level, later Phase 7.

These are not new mechanics.

Forbidden “difficulty” inflation:
- reflex timing;
- hidden socket rules;
- arbitrary per-case seam powers;
- tiny precision selection;
- random movement;
- longer animation waits;
- excessive room count;
- merely increasing endpoint permutation count without new causal structure.

---

# 13. Anti-portal mechanical authoring contracts

From the first mature campaign band onward, valid content must satisfy all applicable rules:

## M4-AP1 — Replacement consequence
At least one required endpoint move must make the lost old adjacency materially change later reachability, entity state, orientation opportunity, isolation, loop structure or ordering.

## M4-AP2 — Physical use between edits
A known baseline solution may not consist of a long detached series of endpoint edits followed by one final traversal. Mature solutions must normally alternate topology changes and physical entity use/state change.

## M4-AP3 — Direct-to-goal defense
For representative mature cases, directly joining current-room and goal-area sockets cannot be the shortest valid solution whenever such a pair exists.

## M4-AP4 — Disconnection as positive action
A material portion of campaign cases must use disconnection/isolation/cut as a benefit, not merely a cost.

## M4-AP5 — Orientation is spatial, not numeric
Known solutions must be reasoned from visible socket geometry; no case may require remembering arbitrary hidden rotation tables.

## M4-AP6 — State-dependent rewire
Mid/late cases must include endpoint decisions whose usefulness changes because an entity has already crossed/moved, preventing the whole game from becoming static graph matching.

## M4-AP7 — Seam scarcity
Adding another seam is not the default way to repair content. If a puzzle only becomes interesting with extra seam inventory, first attempt to improve topology/state consequence.

## M4-AP8 — No portal physics
Momentum, projectile trajectories, free-angle placement and recursive portal optics may not become required mechanical authority.

---

# 14. Mechanical edge-case matrix

| Edge case | Canonical result |
|---|---|
| Move endpoint to its current socket | Reject `NO_CHANGE`, no history mutation |
| Target socket already has endpoint | Reject before mutation |
| Move endpoint while entity crossing it | Reject `ENDPOINT_OCCUPIED` |
| Target socket is crossing-occupied | Reject `TARGET_OCCUPIED` |
| Old adjacency is player's only return route | Legal unless explicit hard invariant; commit and allow Undo |
| New seam isolates required object | Legal bad state unless hard invariant; commit |
| Both seam endpoints would become same socket | Reject |
| Crossing requested after adjacency already moved away | Validate against current state; reject stale/invalid crossing |
| Duplicate accepted command ID retried | Idempotently return prior result, do not duplicate mutation |
| Stale revision/hash | Reject before mutation |
| Two movers request same seam endpoint simultaneously | Invalid/contested state unless unique global non-conflicting rule; authored content must avoid/reject |
| Two independent crossings on disjoint seams | Resolve as one deterministic simultaneous group |
| Automatic chain exceeds 24 steps | Enter deterministic `CHAIN_LIMIT_REACHED`; no partial unresolved step |
| Completion becomes true mid-chain | Wait until settled state, then evaluate completion |
| Undo during presentation interpolation | Restore prior canonical transaction state; presentation reconciles |
| Redo after new branch action | Redo branch is truncated |
| Renderer/camera differs | No domain-state difference |
| Reduced motion/slow presentation | No domain-state difference |

---

# 15. Mechanical acceptance tests

## World/data integrity
- **M4-01** Every room/socket/seam/entity has stable unique ID.
- **M4-02** Every seam has exactly two endpoints in every valid settled state.
- **M4-03** No two seam endpoints occupy the same socket.
- **M4-04** Every active seam pair has one unique finite crossing/orientation mapping.
- **M4-05** Ordinary passages remain immutable under endpoint moves.

## Endpoint move semantics
- **M4-06** Valid `MOVE_SEAM_ENDPOINT` removes old adjacency and creates new adjacency atomically.
- **M4-07** No canonical intermediate state exposes both old and new adjacency.
- **M4-08** No canonical intermediate state leaves a one-ended seam.
- **M4-09** Same-socket request produces no revision/history mutation.
- **M4-10** Structurally illegal target rejects before any mutation.
- **M4-11** Strategically bad but structurally legal endpoint move commits.
- **M4-12** Endpoint move cannot commit while selected endpoint is crossing-occupied.
- **M4-13** Target socket cannot receive an endpoint while crossing-occupied.
- **M4-14** Duplicate command retry cannot duplicate/stack topology changes.
- **M4-15** Stale revision/hash rejects before mutation.

## Crossing/orientation
- **M4-16** Crossing through every allowed socket-pair orientation produces the defined local exit facing.
- **M4-17** Crossing result is independent of animation speed/frame delta.
- **M4-18** Entity cannot be canonically resident in two rooms during one settled state.
- **M4-19** Endpoint occupancy lock covers exactly the canonical crossing step.
- **M4-20** Moving endpoint after crossing settles affects future crossings only, never retroactively relocates the crossed entity.
- **M4-21** One-way seam direction rejects incompatible crossing without consuming movement state.

## Movement/resolution
- **M4-22** Identical initial state + semantic command sequence yields identical canonical hash.
- **M4-23** Independent simultaneous movement groups produce identical final state regardless of serialization order.
- **M4-24** Contested same-boundary movement cannot be resolved by incidental stable-ID priority unless an explicit global rule exists.
- **M4-25** Automatic chains settle or enter `CHAIN_LIMIT_REACHED` within 24 canonical steps.
- **M4-26** Case completion is evaluated only after transaction settlement.

## Objectives/failure/history
- **M4-27** Hard-invariant violation rejects before mutation.
- **M4-28** Soft/protected objective may be broken by a legal action and remain observable.
- **M4-29** Undo restores exact pre-transaction seam/entity/objective state.
- **M4-30** Redo restores exact stored transaction while branch intact.
- **M4-31** New accepted action after Undo truncates Redo branch.
- **M4-32** Rejected commands do not create history entries.

## Solver/content identity
- **M4-33** A case fixture can be represented entirely by finite discrete solver state.
- **M4-34** Every shipped case has at least one validated known baseline solution fixture.
- **M4-35** Mature case validator can determine whether a lost adjacency changes reachability/state along known/shortest solution paths.
- **M4-36** Representative mature cases can be tested for direct current-room-to-goal seam shortcuts.
- **M4-37** Rare 3-seam cases require explicit justification metadata.
- **M4-38** Content with ambiguous simultaneous boundary contention is rejected.
- **M4-39** No baseline fixture requires free-angle aiming, momentum/flinging or frame timing.
- **M4-40** A fresh Phase-5/implementation session can implement the domain rules without inventing seam/crossing/Undo ordering.

---

# 16. Mechanical risk gates carried forward

## M4-R1 — Portal-like collapse
Risk: the mechanics technically replace adjacency but optimal solutions still feel like place-entrance/place-exit.
Evidence gate: Phase-5 representative mature cases must demonstrate lost-adjacency dependence across multiple solution skeletons.

## M4-R2 — Orientation bookkeeping
Risk: finite mapping is deterministic but cognitively unpleasant.
Evidence gate: Phase-6 presentation and implementation prototype must keep orientation misunderstanding under Product Thesis threshold.

## M4-R3 — Two-seam state explosion
Risk: solver/content burden rises sharply.
Evidence gate: Phase 5 must quantify representative reachable state counts and refuse complexity whose value is mostly permutations.

## M4-R4 — Stranding busywork
Risk: topology scarcity becomes repeated recovery traversal.
Evidence gate: content review must distinguish insight-producing cuts from mere route restoration chores.

## M4-R5 — Graph-UI takeover
Risk: mechanical clarity encourages solving from an abstract map.
Evidence gate: Phase 6 must keep endpoint editing/world state physically grounded; overview may explain but not become a detached graph editor.

## M4-R6 — Moving-entity contention
Risk: automatic movers introduce ambiguous or timing-heavy simultaneous crossings.
Evidence gate: Phase 5 must author bounded deterministic movement patterns and reject ambiguous contention states.

---

# 17. Phase-4 closure

- Room state model defined: **YES**
- Edge-socket model defined: **YES**
- Ordinary-passage model defined: **YES**
- Seam/endpoint model defined: **YES**
- Entity state model defined: **YES**
- Endpoint replacement validation defined: **YES**
- Atomic old-adjacency removal/new-adjacency creation defined: **YES**
- Finite orientation mapping defined: **YES**
- Crossing/occupancy timing defined: **YES**
- Deterministic movement/resolution order defined: **YES**
- Legal-bad vs illegal edits defined: **YES**
- 1/2/rare-3 seam constraints defined: **YES**
- Objective/invariant/dead-end policy defined: **YES**
- Undo/Redo transaction semantics defined: **YES**
- Canonical state/hash defined: **YES**
- Solver-state assumptions defined: **YES**
- Global difficulty knobs defined: **YES**
- Anti-portal authoring contracts defined: **YES**
- Edge-case matrix defined: **YES**
- Mechanical acceptance tests: **40**
- Production implementation started: **NO**
- Mechanical Architecture: **COMPLETE ON PAPER**
- DESIGN COMPLETE: **NO**

## NEXT PHASE

**Phase 5 — Content Architecture.**

The next run must define a complete data-driven campaign/content contract without adding new primary verbs. It should specify:
- exact teaching order and campaign bands;
- target main/demo/remix counts;
- representative case blueprints from onboarding through late synthesis;
- allowed entity/room/socket vocabulary ceiling;
- case schema/data fields;
- known baseline/mastery fixture requirements;
- solver/validator pipeline and quantitative complexity guardrails;
- lost-adjacency/provenance-like dependency proof for mature cases;
- solution-skeleton taxonomy and anti-isomorphism rules;
- direct-to-goal shortcut audit;
- two-seam/three-seam content budgets;
- moving-entity authoring constraints;
- remix/mastery validity rules;
- demo content proof of useful disconnection;
- expansion boundaries;
- numbered Phase-5 acceptance tests.
