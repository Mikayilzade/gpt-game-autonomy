# GAME #007 — LAST KNOWN SHAPE — MECHANICAL ARCHITECTURE

Last updated: 2026-08-30
Phase: **4 — Mechanical Architecture**
Selected concept: **G7C02 Last Known Shape**
Production implementation started: **NO**
DESIGN COMPLETE: **NO**

This file defines the canonical deterministic gameplay contract for Last Known Shape. It resolves all paper-level ambiguities required before content architecture. `GAME7_PRODUCT_THESIS.md` remains authoritative for product identity; this file is authoritative for domain mechanics.

---

# 1. Mechanical thesis

The player does not freely reshape objects. The player performs discrete **observation writes** from authored Observation Frames. Each legal frame/object pairing exposes one exact candidate remembered form before commit. Committing observation overwrites the object's remembered form. Once direct observation ends at the declared canonical boundary, that remembered form becomes the object's authoritative physical form and therefore its authored gameplay affordances.

Core causal sentence:

> **Preview exact form -> commit observation -> end direct observation -> remembered form becomes physical authority -> exploit or deliberately overwrite later.**

The system must be understandable without pixel interpretation, free-camera alignment, hidden ray thresholds, real-time timing, or image recognition.

---

# 2. Canonical world model

Gameplay authority is discrete and data-defined.

## 2.1 Object definition
Each transformable object has immutable authored identity plus canonical mutable state.

Immutable fields:
- `object_id` — globally stable identifier within case;
- `form_catalog[]` — allowed `form_id` values;
- `pose_slots[]` — authored discrete physical locations/orientations the object may occupy;
- `movement_profile_id` — legal ordinary relocation rules;
- `interaction_profile_id` — which player/object interactions are supported;
- `default_form_id`;
- `default_pose_slot_id`.

Mutable canonical fields:
- `pose_slot_id`;
- `remembered_form_id`;
- `physical_form_id`;
- `direct_observation_state` = `UNOBSERVED | PREVIEWING | COMMITTED_OBSERVED`;
- `active_frame_id | null`;
- `active_receiver_claims[]` derived from form + pose;
- `movement_lock_reason | null` derived from rules.

`remembered_form_id` is the persistent observation memory. `physical_form_id` is normally equal to remembered form whenever object is outside direct observation. During preview/committed observation, presentation may show source geometry plus candidate overlay, but puzzle authority never depends on interpolated visual geometry.

## 2.2 Forms
A `form_id` is a discrete authored gameplay state, not a mesh silhouette sample.

Each form defines:
- stable `form_id`;
- presentation asset reference(s);
- footprint/occupancy tags per compatible pose slot;
- receiver/contact affordance tags;
- traversal affordance tags, e.g. `BRIDGE`, `STEP`, `BLOCKER`, `FIT_NARROW`, `REACH_HIGH`;
- occluder contribution profile for explicitly declared Observation Frames;
- carry/push eligibility;
- authored incompatibilities.

Forms never acquire case-specific private physics callbacks. A case composes global affordance rules and authored data.

## 2.3 Pose slots
Object movement authority is slot-based.

A pose slot declares:
- stable `pose_slot_id`;
- which objects may occupy it;
- capacity;
- allowed entering/exiting transitions;
- compatible forms;
- receiver/contact geometry tags;
- whether it lies in an Observation Frame's declared occluder set;
- traversal/blocking consequences per form tag.

Continuous renderer coordinates may animate between slots, but solver/gameplay authority changes only at canonical command boundaries.

## 2.4 Observation Frames
An Observation Frame is an authored deterministic write station.

Immutable fields:
- `frame_id`;
- player activation locus/facing conditions expressed discretely;
- ordered list of eligible object IDs or object classes;
- `transform_rule_id`;
- optional `fixed_mask_id`;
- explicit `occluder_inputs[]` listing object IDs + qualifying pose/form predicates;
- candidate lookup/function parameters;
- frame access predicate;
- optional mutually-exclusive frame lock group.

A frame does **not** sample the camera framebuffer. Candidate form is computed from canonical state only.

## 2.5 Receivers and world mechanisms
Receivers are authored consumers of object affordances: sockets, pressure contacts, bridge spans, shutters, lifts, gates, etc.

Each receiver declares:
- `receiver_id`;
- deterministic activation predicate over canonical object form/pose/contact tags;
- resulting discrete mechanism state;
- stable priority for simultaneous consequence resolution where needed.

Receivers do not inspect meshes, collision callbacks or animation frames directly.

---

# 3. Observation candidate function

Canonical pure function:

`CANDIDATE(frame_id, object_id, canonical_state) -> form_id | rejection_reason`

The candidate may depend only on:
1. selected frame's authored transform rule;
2. selected object's canonical identity and pose;
3. fixed mask state declared by that frame;
4. explicitly listed occluder inputs in their canonical pose/form states;
5. explicit world mechanism state if and only if named as a frame input.

It may not depend on:
- free camera transform;
- screen-space pixel coverage;
- renderer visibility query;
- antialiasing/resolution;
- frame delta;
- animation timing;
- hidden physics overlap order;
- audio state;
- player mouse precision beyond semantic object selection.

For every legal pre-state, preview and commit call the same candidate function over the same canonical state snapshot.

---

# 4. Observation lifecycle

Canonical semantic commands:
- `BEGIN_PREVIEW(frame_id, object_id, expected_revision)`;
- `COMMIT_OBSERVATION(frame_id, object_id, expected_revision, command_id)`;
- `CANCEL_PREVIEW()`;
- `END_OBSERVATION(object_id)` is normally automatic when the player leaves/cancels the authored observation locus after a committed write; it is not an extra puzzle choice unless a later UX layer exposes an equivalent explicit action.

## 4.1 BEGIN_PREVIEW
Eligibility is checked against one immutable pre-command state. On success:
- set UI/presentation preview context only;
- compute exact candidate form;
- show candidate, current remembered form, and directly knowable affordance deltas;
- do **not** mutate remembered form, physical form, receivers, revision, history or solver state.

Preview state itself is presentation/session state and excluded from canonical puzzle hash except where needed to restore menu/UI continuity. Cancelling it has zero gameplay consequence.

## 4.2 COMMIT_OBSERVATION
A commit is legal only while:
- player satisfies frame activation predicate;
- frame/object pairing is eligible;
- object is not mechanically locked against observation;
- candidate computation succeeds;
- expected revision matches.

Accepted commit forms one atomic semantic transaction:
1. recompute candidate from immutable pre-state;
2. verify it matches preview result if preview is active; mismatch is a hard specification error and commit rejects;
3. overwrite `remembered_form_id` with candidate;
4. mark object `COMMITTED_OBSERVED` at that frame;
5. do **not** yet apply the remembered form as a new physical authority while direct observation remains active;
6. increment revision and record transaction.

The prior remembered form is destroyed by commit, but its current physical consequences may remain until direct observation ends. This deliberate split makes `look -> remember -> look away -> reality resolves` causally legible.

## 4.3 END_OBSERVATION / resolution boundary
Direct observation ends when the player leaves the frame's declared activation locus, deliberately switches to another legal frame target, or another explicit global condition ends observation.

At the canonical boundary:
1. object changes to `UNOBSERVED`;
2. `physical_form_id := remembered_form_id`;
3. recompute occupancy/contact/receiver claims from new form + current pose;
4. resolve deterministic immediate mechanism consequences;
5. stop at the next stable player-command boundary.

This transition and all immediate deterministic consequences belong to the same history transaction as the player action that ended observation (normally the movement/interaction command causing exit), not as an unowned asynchronous mutation.

## 4.4 Re-observation
Re-entering any frame does not itself overwrite memory. Only `COMMIT_OBSERVATION` overwrites remembered form.

A player may inspect a candidate and cancel without losing the current remembered form.

---

# 5. Physical-form authority and affordances

The puzzle never asks the engine to infer gameplay from arbitrary transformed mesh geometry.

When `physical_form_id` changes, global resolution maps authored form tags to world state:
- traversal span available/unavailable;
- receiver contacts active/inactive;
- passage blocked/unblocked;
- object fits/does not fit a compatible pose transition;
- object can/cannot be carried/pushed according to form profile;
- authored occluder predicates become true/false for named frames.

An object's remembered form persists through ordinary movement until another observation commit overwrites it.

Movement into a destination pose is legal only if the object's **current physical form** is compatible with that destination. There is no temporary shrink/stretch animation authority.

---

# 6. Authored masks and occluders

Occlusion is symbolic and explicit.

A frame may compute candidate using:
- one fixed authored mask state;
- zero or more named object occluder inputs;
- each occluder contributes a finite symbolic token based on its current canonical form + pose.

Example:
`Frame B + Object O + Occluder A=TALL@P3 -> HOOK`
`Frame B + Object O + Occluder A=COMPACT@P3 -> WIDE`

The candidate function may be implemented as table, finite rules, or pure deterministic function, but every dependency must be declared in case data and inspectable by tooling.

Forbidden:
- arbitrary third object accidentally blocking a camera ray;
- tiny pose differences outside slots;
- hidden visual overlap thresholds;
- player avatar acting as occluder unless a future global rule explicitly adds that primitive (baseline: excluded).

---

# 7. Object movement / placement

Supporting movement is intentionally bounded so Last Known Shape does not become a physics sandbox.

Allowed baseline object commands:
- `MOVE_OBJECT(object_id, from_slot, to_slot, expected_revision, command_id)` for push/carry/snap relocation where authored adjacency and form compatibility allow;
- ordinary player traversal commands among authored navigation regions;
- `INTERACT(receiver_or_mechanism_id)` only for globally defined simple devices where needed.

Object movement rules:
1. source and destination are discrete authored slots;
2. path legality is authored/global and deterministic;
3. current physical form controls compatibility;
4. moving an object can change declared occluder inputs and receiver claims;
5. movement itself does not alter remembered form;
6. no momentum, stacking simulation, emergent rigid-body authority or precision balancing is baseline canon.

---

# 8. Two-object observation semantics

Baseline mature ceiling is two simultaneously reasoning-critical transformable objects.

There is no simultaneous observation commit. Player semantic commands serialize deterministically.

If A is used as an occluder input for observing B:
- candidate for B reads A's **current canonical physical form + pose** at the start of B's commit transaction;
- changing A later does not retroactively alter B's remembered form;
- B changes only through a later explicit B commit.

This is the central preservation/order property.

If observing A causes an eventual form change that alters access to B's frame, access change occurs only at A's end-of-observation resolution boundary.

No candidate function may recursively depend on the candidate form currently being previewed for another object.

Three reasoning-critical objects are not baseline mechanical canon; Phase 5 may mark a rare optional experiment only if readability/solver bounds are proven. Main campaign must remain completable without introducing a third-object rule dependency.

---

# 9. Legality and rejection reasons

All illegal semantic commands reject before canonical mutation.

Stable reason codes include:
- `FRAME_NOT_ACCESSIBLE`
- `OBJECT_NOT_ELIGIBLE_FOR_FRAME`
- `OBJECT_NOT_AT_REQUIRED_POSE`
- `OBSERVATION_LOCKED`
- `NO_VALID_CANDIDATE`
- `PREVIEW_COMMIT_MISMATCH`
- `STALE_REVISION`
- `DUPLICATE_COMMAND_ID_PAYLOAD_MISMATCH`
- `DESTINATION_OCCUPIED`
- `FORM_INCOMPATIBLE_WITH_DESTINATION`
- `MOVE_PATH_BLOCKED`
- `OBJECT_NOT_MOVABLE_IN_CURRENT_FORM`
- `INTERACTION_PREDICATE_FALSE`

Illegal strategic choices that are still rule-legal **commit normally**. The game does not protect the player from making a bad but understandable observation overwrite.

---

# 10. Stable event ordering

All gameplay consequences resolve from canonical state, not engine callback order.

At a semantic transaction:
1. validate command against immutable pre-state;
2. compute direct semantic mutation;
3. collect changed object affordance claims;
4. recompute receivers in ascending stable receiver priority, tie by `receiver_id`;
5. collect mechanism transitions caused by receiver changes;
6. resolve globally declared mechanism consequences in stable priority/id order;
7. recompute access predicates affected by those consequences;
8. assert canonical invariants;
9. increment revision / finalize history child;
10. expose resulting presentation events.

If two receivers simultaneously demand mutually incompatible states of one mechanism, the mechanism must define one global resolution rule or the case is invalid. Case-specific callback ordering is forbidden.

There are no wall-clock autonomous gameplay changes in baseline design. If a later mechanism visually moves, semantic completion occurs at the deterministic transaction boundary; animation is presentation.

---

# 11. Undo / Redo / idempotency

Every accepted player semantic command plus all deterministic immediate consequences before the next player-command boundary is one history transaction.

Required properties:
- unlimited ordinary Undo/Redo during cases;
- Undo restores exact parent canonical state/hash;
- Redo restores exact child while branch is intact;
- new accepted command after Undo truncates Redo descendants;
- preview/cancel does not create history entries;
- duplicate `command_id` + identical payload returns recorded result without second mutation;
- duplicate `command_id` + different payload hard-rejects;
- stale expected revision rejects before mutation.

Achievements/mastery may never punish baseline Undo use.

Canonical history snapshots need not preserve renderer interpolation, camera transform or transient preview UI.

---

# 12. Win, fail, dead states and recovery

## 12.1 Win
Each case defines a deterministic `WIN_PREDICATE(canonical_state)` over authored world facts such as:
- player in goal region;
- required receivers active/inactive;
- required objects in specified pose/form states;
- optional preservation constraints if explicitly taught.

Win is evaluated after every accepted transaction reaches stable boundary.

## 12.2 Fail
Baseline cases avoid punitive real-time fail states. A hard fail exists only for explicit authored irreversible destruction if such a global primitive is later retained; Phase 4 baseline defines **none**.

Therefore ordinary bad states are recoverable through Undo/Restart.

## 12.3 Dead states
Solver/tooling may detect no-solution states. Runtime does not automatically announce dead state by default because that would become an oracle. Player always has Undo and Restart Case.

Content may optionally provide a generic hint like `Your current state may have lost a required route` only through the later hint architecture, never through hidden per-case cheat logic.

---

# 13. Canonical solver state

Solver/gameplay hash includes only causally relevant discrete facts:
- player navigation region / semantic interaction position;
- each transformable object's pose slot;
- each object's remembered form;
- each object's physical form if it can differ during committed direct observation;
- each object's observation state only where it changes legal next actions;
- relevant frame access state if not purely derived;
- receiver/mechanism states not purely derivable;
- movable non-transform object slots if any;
- revision excluded from state equivalence but retained operationally.

Excluded from solver identity:
- camera transform;
- cursor position;
- animation progress;
- particles/audio;
- preview-only candidate UI;
- Undo ancestry/history branch;
- explanatory provenance/log text;
- save metadata.

Derived receiver claims should be recomputed rather than duplicated in solver key where practical.

## State-explosion boundaries
Baseline authoring limits:
- normally <=2 transformable reasoning-critical objects;
- <=3 useful forms per object in ordinary main cases; 4 only with explicit proof;
- <=4 relevant Observation Frames per case;
- discrete pose slots, typically <=5 per object;
- no unconstrained combinatorial occluder list: each frame <=2 named dynamic occluder inputs, normally 0–1;
- no recursive candidate dependencies;
- no continuous state variables.

Every authored case must terminate under a configurable solver budget. Cases exceeding practical budget are simplified/cut rather than receiving bespoke pruning semantics.

---

# 14. Difficulty and balance knobs

Difficulty increases through causal composition, not execution speed.

Primary knobs:
1. number of useful forms/object;
2. number of frames relevant to current plan;
3. whether best current form harms later access;
4. number of preserve->overwrite cycles required;
5. whether same frame changes candidate because of explicit occluder state;
6. number of object pose relocations between observations;
7. number of reasoning-critical objects (1 -> 2);
8. observation-order dependency depth;
9. receiver coupling count;
10. whether goal requires temporarily moving away from a seemingly-good form;
11. whether a frame becomes inaccessible under one physical form;
12. number of plausible but causally inferior legal commits.

Forbidden difficulty knobs:
- tiny timing windows;
- precision camera alignment;
- hidden form thresholds;
- unreadable visual clutter;
- arbitrary increase in form count;
- dozens of receivers with bookkeeping load;
- punishing Undo.

---

# 15. Anti-dominant-strategy fixtures

Content architecture must include representative cases proving the following universal strategies fail.

## ADS-1: `Keep the largest/longest form`
Fixture: LONG bridges gap but blocks access to COMPACT frame; TALL must operate lift first, COMPACT transports, LONG comes last.

## ADS-2: `Observe every frame immediately`
Fixture: committing a convenient alternate frame early destroys a remembered bridge required to reach the next frame.

## ADS-3: `Never overwrite a working form`
Fixture: one object must switch LONG -> COMPACT -> LONG across changed pose/access states.

## ADS-4: `Solve one object completely, then the other`
Fixture: A must temporarily become TALL to alter B's candidate, B must commit and preserve HOOK, then A is overwritten COMPACT. Strict object-by-object completion fails.

## ADS-5: `Always observe the frame nearest the object/goal`
Fixture: near frame yields directly useful form that self-blocks access; distant frame yields enabling intermediate form.

## ADS-6: `Try every form until one works`
Mature case requires state-dependent future value: same form is useful in one pose/stage and harmful in another, so blind enumeration without understanding creates additional unresolved state rather than directly ending the case. Free Undo remains intact.

---

# 16. Mechanical scope exclusions

Not part of baseline 1.0 mechanics:
- free-camera silhouette capture;
- continuous perspective scaling;
- arbitrary mesh boolean operations;
- player-drawn forms;
- computer vision/image recognition;
- emergent physics stacking;
- real-time stealth/timing;
- combat;
- time rewind as a world mechanic (Undo is interface/history, not fiction system);
- clones/replays;
- portals/non-Euclidean adjacency;
- currencies/upgrades;
- procedural level generation;
- case-specific script callbacks that redefine observation semantics.

---

# 17. Mechanical acceptance tests

The implementation spec and later content validator must preserve at least these tests.

## Observation authority
**M01** Legal BEGIN_PREVIEW returns exactly one candidate form from canonical state.
**M02** BEGIN_PREVIEW mutates no canonical puzzle state or history.
**M03** CANCEL_PREVIEW after any preview leaves hash unchanged.
**M04** Camera rotation while previewing cannot change candidate.
**M05** Resolution/window-size change cannot change candidate.
**M06** An undeclared third object visually crossing the camera cannot change candidate.
**M07** A declared occluder changing from COMPACT to TALL may change candidate exactly per authored rule.
**M08** Fixed mask state affects only frames that explicitly reference it.
**M09** Preview candidate and accepted commit candidate are identical for unchanged pre-state.
**M10** Forced preview/commit mismatch rejects without mutation.

## Commit / overwrite / resolution
**M11** COMMIT overwrites remembered form atomically.
**M12** COMMIT alone does not apply a different physical form while direct observation remains active.
**M13** Ending direct observation sets physical form equal to remembered form.
**M14** Ending observation recomputes all affected receiver claims before next player command.
**M15** Re-entering a frame without commit does not overwrite memory.
**M16** Previewing a different frame and cancelling preserves prior memory.
**M17** Re-observing and committing same remembered form is legal and deterministic unless authoring explicitly suppresses no-op commands globally.
**M18** A commit that is strategically bad but legal is not auto-rejected.

## Movement / affordances
**M19** Object movement changes pose but not remembered form.
**M20** Destination incompatible with current physical form rejects before mutation.
**M21** Legal relocation updates receiver and occluder consequences deterministically.
**M22** Renderer collision glitches cannot create a legal pose transition absent authored slot transition.
**M23** BRIDGE affordance is active only in authored compatible pose/form combinations.
**M24** FIT_NARROW compatibility is determined by form data, not visible mesh width.

## Multi-object ordering
**M25** B candidate reads A's canonical physical form/pose at B commit pre-state.
**M26** Later change to A does not retroactively alter B remembered form.
**M27** Changing A can change B's *future* candidate if B frame declares A as occluder.
**M28** Preview candidate for A cannot recursively depend on B's simultaneous preview candidate.
**M29** Two object commits in opposite orders may produce different legal states only when declared causal dependencies justify it.
**M30** No engine scene-tree ordering can change two-object result.

## Event ordering / receivers
**M31** Identical pre-state + semantic input yields identical post-state/hash across repeated runs.
**M32** Simultaneous receiver changes resolve by declared global priority/stable ID.
**M33** Case with ambiguous conflicting receiver demands fails validation rather than using callback order.
**M34** Mechanism animation duration cannot alter semantic end state.

## Legality / idempotency
**M35** Stale revision rejects before mutation.
**M36** Duplicate command ID + same payload performs no second mutation.
**M37** Duplicate command ID + different payload hard-rejects.
**M38** Illegal frame/object pair rejects with stable reason code.
**M39** No-valid-candidate state rejects without overwriting remembered form.
**M40** Occupied/incompatible movement target rejects without partial relocation.

## Undo / Redo
**M41** Undo after observation commit restores exact prior remembered form.
**M42** Undo after movement that ended observation restores exact parent observation/physical state.
**M43** Redo restores exact child hash while branch intact.
**M44** New accepted command after Undo truncates Redo descendants.
**M45** Preview/cancel creates no Undo step.
**M46** Unlimited ordinary Undo does not alter case completion eligibility.

## Solver / dead-state
**M47** Solver state equivalence ignores camera, animation and history ancestry.
**M48** Solver distinguishes states with different remembered forms even if current presentation mesh has not yet resolved during observation.
**M49** Solver terminates representative one-object cases within configured authoring budget.
**M50** Solver terminates representative two-object occluder/order cases within configured budget or validator rejects/simplifies case.
**M51** Runtime does not automatically expose solver dead-state oracle.

## Dominant-strategy rejection
**M52** ADS-1 fixture cannot be solved by keeping LONG/largest form throughout.
**M53** ADS-2 fixture demonstrates that observing every available frame immediately can destroy required access.
**M54** ADS-3 fixture requires at least two deliberate overwrites of one object.
**M55** ADS-4 fixture cannot be solved by fully finishing A before first meaningful B commit.
**M56** ADS-5 fixture rejects nearest/direct-goal frame as shortest valid causal plan.

## Accessibility / causal readability mechanics
**M57** Candidate form is available through non-color shape/icon/outline information.
**M58** Audio muted changes no legal action or authoritative state.
**M59** Reduced-motion transformation preserves exact semantic boundary and consequence ordering.
**M60** Core mechanic remains solvable without reflex timing or precision pointer movement.

---

# 18. Phase-4 result

**Mechanical Architecture is COMPLETE ON PAPER.**

Resolved:
- deterministic object/form/frame/receiver data contract;
- exact preview/commit/end-observation lifecycle;
- remembered vs physical authority split;
- explicit masks/occluders with no pixel authority;
- slot-based object movement;
- two-object observation-order semantics;
- legality/rejection codes;
- stable event ordering;
- exact Undo/Redo/idempotency boundaries;
- win/dead-state recovery policy;
- bounded canonical solver state;
- difficulty knobs and anti-dominant fixtures;
- **60 mechanical acceptance tests**.

No production implementation has begun.

## NEXT ACTION
Phase 5 — Content Architecture. Define the main campaign and demo as authored data over this mechanical contract. Required: content families, teaching sequence, target/minimum case counts, case schema, form/object/frame vocabulary ceiling, authored occluder families, causal-diversity quotas, anti-isomorphism rules, solver/validator pipeline, demo structure, optional mastery/remix rules, and >=45 content acceptance tests. The campaign must prove preserve/overwrite, access self-block, frame/affordance tradeoffs, state-dependent reuse and two-object observation order without adding private observation laws.