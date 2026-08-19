# GAME #003 — BORROWED COLLISION — TECHNICAL IMPLEMENTATION SPECIFICATION

Last updated: 2026-08-20
Factory run: **12**
Phase: **8 — Technical Implementation Specification**
Product thesis: **LOCKED**
Mechanical architecture: **COMPLETE ON PAPER**
Content architecture: **COMPLETE ON PAPER**
UX / presentation architecture: **COMPLETE ON PAPER**
Economy / commercial model: **COMPLETE ON PAPER**
DESIGN COMPLETE: **NO**

This file is the canonical Phase-8 technical contract for Borrowed Collision. It translates the frozen Phase-3..7 design into implementation architecture without starting production code or adding gameplay.

When technical convenience conflicts with frozen gameplay, the smallest affected earlier canonical phase wins unless explicitly reopened. A renderer, physics engine, scene graph, save library or platform API may never become gameplay authority merely because it is convenient.

Current technical references checked 2026-08-20:
- Godot release archive: https://godotengine.org/download/archive/
- Godot 4.7.1 maintenance release: https://godotengine.org/article/maintenance-release-godot-4-7-1/
- Godot stable command-line/headless documentation: https://docs.godotengine.org/en/stable/tutorials/editor/command_line_tutorial.html
- Godot `FileAccess`: https://docs.godotengine.org/en/stable/classes/class_fileaccess.html
- Godot `DirAccess`: https://docs.godotengine.org/en/stable/classes/class_diraccess.html
- Godot internationalization: https://docs.godotengine.org/en/stable/tutorials/i18n/index.html
- Steam Cloud: https://partner.steamgames.com/doc/features/cloud
- Steam Input: https://partner.steamgames.com/doc/features/steam_controller
- Steam Deck compatibility: https://partner.steamgames.com/doc/steamhardware/compat

As of 2026-08-20, Godot **4.7.1-stable** is the latest stable 4.7 maintenance release in the official archive; 4.7.2 is still release-candidate and 4.8 is development-only. Therefore the implementation handoff should pin 4.7.1 unless a deliberate pre-production upgrade is separately evaluated and recorded.

---

# 1. Technical design goals

The implementation must make the following properties structural:

1. **Deterministic causal physics is domain logic, not engine physics.** Motion, collisions, impact output, receive windows and chain resolution are computed from discrete authored state.
2. **Presentation never owns truth.** Scene transforms, animation positions, frame delta, tween completion and physics contacts cannot decide gameplay.
3. **Every portable impact has inspectable lineage.** Harvest, transform, spend and secondary collisions remain causally attributable across rooms and save/load.
4. **One collision lineage emits at most one impact.** Duplicate input, pause, load, animation replay and platform retries cannot duplicate consequences.
5. **Undo/Redo restores exact canonical checkpoints.** No inverse simulation.
6. **Content is data-driven and statically validated.** R1–R8, donor regeneration classes, transform families, collision tables, objectives, mastery and remixes must compile from bounded schemas rather than per-case gameplay scripts.
7. **Input is semantic and device-independent.** Mouse+keyboard, keyboard-only, controller and Steam Deck emit the same domain commands.
8. **Persistence is interruption-safe.** A crash cannot leave half a collision chain, half-consumed impact or hybrid lineage state as authoritative.
9. **Offline/local correctness is complete.** Steam Cloud/Achievements are adapters, never required for solving or saving a case.
10. **The deterministic headless harness is a first-class subsystem.** Every shipped case and major system is replayable without presentation scenes.

---

# 2. Engine / runtime direction

## 2.1 Frozen implementation direction

**Godot 4.7.1-stable, standard build, GDScript-first, 2D Control/Canvas architecture.**

Repository/tooling must pin the exact engine patch. Do not follow `latest` automatically. A future engine upgrade requires a recorded compatibility pass over deterministic replays, save fixtures, controller focus, rendering and export smoke tests.

## 2.2 Why Godot fits Borrowed Collision

The product needs:
- small deterministic graph/state simulation;
- strong 2D symbolic rendering;
- UI-heavy inspection, causal ribbons and focus navigation;
- controller/input remapping;
- localization and pseudolocalization;
- lightweight authored data pipelines;
- headless scripted execution;
- desktop/Steam Deck export.

It does **not** need:
- continuous rigid-body physics as gameplay truth;
- 3D navigation meshes;
- high-end 3D rendering;
- online authoritative servers;
- large-scale ECS architecture.

## 2.3 Renderer

Default target: **Compatibility renderer** for the stylized 2D presentation unless measured visual needs later require Mobile. No gameplay rule may depend on renderer, GPU, frame rate or shader precision.

## 2.4 Language boundary

GDScript is the default for domain, application and presentation because iteration speed and inspectability matter more than native throughput at this state scale.

C#/GDExtension/native code is permitted only behind an adapter when:
- a platform SDK requires it; or
- profiling proves a measured bottleneck against the frozen performance budgets.

A native rewrite for hypothetical performance is out of scope.

---

# 3. Architecture and authority boundaries

## 3.1 Layer A — Domain Core

Pure deterministic data + algorithms. It must not depend on scene nodes, rendering, audio, OS time, locale, platform identity, filesystem, Steam, frame delta or engine physics contacts.

Responsibilities:
- `CaseDefinition` compiled rules/content;
- `CaseState` canonical mutable state;
- body/lane/collision state;
- collision-group formation;
- collision-table lookup;
- impact harvest/lineage;
- transform rules;
- receiver compatibility;
- self-launch semantics;
- moving receive-window states;
- bounded chain resolution;
- objective/invariant/mastery evaluation;
- canonical serialization/hash;
- deterministic explanation/event DAG.

Domain APIs accept explicit immutable inputs and return explicit results.

## 3.2 Layer B — Application Services

Owns orchestration around Domain Core:
- active case session;
- semantic command construction/validation;
- Undo/Redo/history;
- traversal/session state coordination;
- content loading/compiler reports;
- campaign prerequisites/tutorial tags;
- profile progression/mastery/remix unlocks;
- save/checkpoint/recovery;
- schema/content migrations;
- demo import;
- localization-token lookup;
- platform achievement/cloud adapters.

Application Services cannot override collision results or receiver rules.

## 3.3 Layer C — Presentation

Godot scenes/nodes for:
- Title / first-launch setup;
- Case Board / Brief / Completion;
- world rooms;
- bodies and lanes;
- pickups/impact belt;
- receiver/converter affordances;
- inspection cards;
- causal ribbon/history;
- Pause/Step presentation;
- settings/accessibility/help.

Presentation submits semantic commands and consumes immutable snapshots / presentation plans. It may interpolate motion between canonical boundaries, but it never computes gameplay contact, impulse strength, lineage, objective truth or receive-window legality.

## 3.4 Layer D — Platform Adapters

Replaceable adapters for:
- local filesystem abstraction;
- Steam Cloud / Remote Storage strategy;
- Steam Achievements;
- Steam Input/glyph integration if selected;
- build/platform metadata.

The game must remain fully functional locally if every Steam adapter is disabled.

---

# 4. Canonical content identity

Each compiled `CaseDefinition` is immutable and identified by:
- `case_id`;
- `content_schema_version`;
- `case_content_version`;
- `ruleset_version`;
- `collision_registry_version`;
- `canonical_hash_version`;
- `content_hash`.

A running active case references an exact identity tuple. It must never silently load a changed case definition into an older active state.

Compiled content is normalized before hashing so source-file ordering and authoring whitespace do not change semantic identity.

---

# 5. Canonical `CaseDefinition` model

`CaseDefinition` contains only immutable content/rules references:

- identity/version tuple;
- act/tutorial/prerequisite tags;
- room definitions;
- route nodes and movement lanes;
- collision boundaries and simultaneous-group contracts;
- initial bodies;
- collision table/profile references;
- donor source definitions;
- receiver definitions R1–R8;
- transform-device definitions;
- initial world impacts/pickups, if any;
- inventory capacity (2 default, max 3);
- objective/invariant definitions;
- mastery contracts;
- known solution fixtures;
- reasoning-transformation tags;
- presentation/localization token references;
- `max_resolution_steps` <=24;
- deterministic authored focus/navigation graph or source data from which it compiles.

There is no arbitrary case callback, embedded gameplay script or freeform expression language capable of replacing canonical rules.

---

# 6. Canonical `CaseState` model

A mutable `CaseState` contains:

- exact case identity/version tuple;
- `session_id` for persistence/conflict identity only;
- monotonic `session_revision`;
- `player_state`;
- `body_state_by_id`;
- `impact_state_by_id`;
- `impact_inventory_ids[]`;
- world-pickup locations;
- donor generation/emission state;
- receiver/device current states;
- transform in-progress state, if any;
- objective/invariant/mastery evaluation state;
- current movement/transaction state;
- causal-event DAG for current/recent transaction;
- history cursor/branch metadata;
- completion state.

Derived caches are disposable and rebuildable from canonical state + immutable definition.

---

# 7. Player and traversal state

`PlayerState` contains:
- stable player ID;
- settled `route_node_id` when not self-launched;
- current room ID;
- motion direction/band only while participating in a canonical self-launch/movement transaction;
- settled/moving/failure status;
- current interaction/focus eligibility as derived data, not source truth.

Ordinary walking/traversal is represented by semantic node-to-node commands on the authored player traversal graph. It cannot create free-space collision contacts. Traversal may change pickup/receiver access, but it does not advance autonomous moving bodies unless the frozen case rule explicitly creates a movement transaction.

Contiguous ordinary traversal may be visually compressed, but canonical current player node must always be saveable/recoverable.

---

# 8. Canonical body state

`BodyState` fields:
- `body_id`;
- body/mechanical family references;
- `location_id` at an authored node/boundary;
- `motion_direction` in 8 directions or NONE;
- `motion_band` ZERO/WEAK/MEDIUM/STRONG;
- mass class LIGHT/STANDARD/HEAVY;
- durability class;
- binary/status flags such as BROKEN/OPEN/LATCHED/SPENT/SETTLED;
- active source-lineage ancestry if current motion was caused by a portable impact/secondary collision;
- canonical movement-step state where relevant.

No canonical body exists between lane boundaries. Animation coordinates are not serialized into domain state.

---

# 9. Movement lanes / collision relations

## 9.1 `MovementLaneDefinition`

Fields:
- lane ID;
- start/end canonical node/boundary IDs;
- permitted logical direction(s);
- compatible body/player families;
- one-way state;
- optional occupancy/crossing relation;
- authored next-step mapping;
- presentation spline/path reference only as non-authoritative metadata.

## 9.2 `CollisionRelationDefinition`

Fields:
- boundary/relation ID;
- participant lane/body-role constraints;
- collision profile/table ID;
- capture-enabled flag;
- simultaneous-group rule;
- harvestability family flag;
- deterministic outcome registry reference.

Every reachable same-step multi-contact state must map to exactly one registered deterministic group/outcome or content fails validation.

---

# 10. Portable-impact / lineage model

## 10.1 `PortableImpactState`

Fields:
- stable `impact_id`;
- direction enum;
- magnitude enum;
- source lineage ID;
- source event ID;
- ordered transform-history records;
- availability state WORLD_PICKUP / HELD / STORED / IN_TRANSFORM / CONSUMED;
- current pickup room/node or inventory slot reference;
- creation transaction/revision for diagnostics.

No numeric vector, element, rarity, durability, upgrade or hidden modifier exists.

## 10.2 `LineageState`

Each collision lineage stores:
- lineage ID;
- donor/source ID;
- donor generation;
- parent lineage/event IDs;
- collision event ordinal;
- `harvest_emission_state`;
- emitted impact ID if any.

The domain asserts one emitted impact maximum per lineage.

## 10.3 Donor state

Every donor is exactly EXHAUSTIBLE / RESETTABLE / CYCLIC_WEAK / CHAIN_GENERATED.

Mutable donor state stores:
- donor ID;
- generation counter;
- available/spent/resetting state;
- most recent emitted lineage;
- visible reset/cycle state where relevant.

Reset increments generation only through the frozen visible reset contract.

---

# 11. Receiver / transform state

## 11.1 Receiver definition/state

Definition:
- receiver ID;
- family R1..R8;
- accepted directions;
- accepted bands;
- safe/useful/unsafe sets;
- enabled condition;
- receive-window state IDs if moving;
- direct result contract;
- post-receive state changes.

Mutable state:
- enabled/disabled;
- current window/movement-step state;
- broken/open/latched/activated states as applicable;
- body relation where receiver moves with a body.

## 11.2 Transform state

Transforms are only QUARTER_TURN / REVERSE / MIRROR / DAMPER.

Converter/damper operations:
- preserve impact identity and source lineage;
- append one typed transform-history item;
- return exactly one transformed impact;
- never duplicate;
- never increase magnitude through damper;
- never consult presentation orientation.

Fixed axis/orientation is content data.

---

# 12. Objective / invariant / mastery state

Objective and invariant instances are pure deterministic predicates over canonical case state.

State stores:
- objective/invariant ID;
- family ID;
- current status;
- machine subjects/targets;
- latest material causal event IDs explaining transition;
- first failing fact when false where representable.

Mastery evaluation is separate from baseline completion and uses only frozen final causal/state contracts. Raw Undo, elapsed time, failed probes, slowdown, pause/step and input device are never fed into mastery predicates.

---

# 13. Semantic command registry

Presentation never submits cursor coordinates, animation timestamps or physics contacts. It submits typed semantic commands with stable IDs and an expected pre-state hash/revision.

Required command families:

## C8-TRAVERSE
`TraversePlayerCommand(from_node_id, to_node_id, expected_pre_state_hash)`
- legal only across an authored currently accessible player traversal edge;
- updates settled player node/room;
- does not invent body collision;
- may expose/hide interactions through derived access queries.

## C8-COLLECT
`CollectImpactCommand(impact_id, expected_player_node, expected_pre_state_hash)`
- validates pickup exists, is reachable and capacity exists;
- moves exact impact identity WORLD_PICKUP -> HELD;
- no lineage regeneration occurs.

## C8-TRANSFORM
`TransformImpactCommand(impact_id, transform_id, expected_pre_state_hash)`
- validates access/enabled state;
- applies exact fixed transform;
- same impact ID/source lineage returns with appended transform history.

## C8-SPEND
`SpendImpactCommand(impact_id, receiver_id, snap_orientation_id, expected_receive_window_state?, expected_pre_state_hash)`
- validates ownership/access, receiver compatibility, window state and current exact pre-state;
- consumes the selected impact exactly once;
- starts the full bounded deterministic resolution transaction;
- self-launch is ordinary R6 spend, not a separate physics subsystem.

## C8-RESET-DONOR
`ResetDonorCommand(donor_id, reset_action_id, expected_pre_state_hash)`
- only RESETTABLE donors;
- validates visible reset contract and settled world;
- increments generation only after successful canonical reset consequence.

## Application control commands
- Undo;
- Redo;
- Restart Case;
- Pause/Step presentation controls;
- inspect/focus/help commands.

Pause/Step/Inspect do not mutate domain outcome. Restart is an application-level replacement with canonical initial state, not an in-world donor reset.

Any later new domain-changing command family requires explicit canonical review because it may represent a hidden new player verb.

---

# 14. Command idempotency / stale input

Each domain-changing command contains:
- unique command ID for session/app idempotency;
- expected session revision;
- expected canonical pre-state hash;
- semantic stable IDs.

Rules:
1. if command ID already committed, return the stored result / `ALREADY_APPLIED` without mutating again;
2. if expected revision/hash is stale, reject before mutation;
3. structurally illegal command creates no canonical revision, history entry, lineage, pickup or save generation;
4. accepted command advances revision exactly once regardless of how many derived collisions/events occur;
5. presentation animation cannot resubmit the command as a second action.

---

# 15. Deterministic transaction architecture

## 15.1 Traversal / collect / transform

These are bounded atomic domain commands. They validate, construct new canonical state, evaluate any directly affected availability/objective facts, produce a transaction event set, then commit one revision.

## 15.2 Spend / donor-trigger transaction

A spend follows the exact mechanical ordering:
1. validate command and exact pre-state;
2. consume/commit selected impact or donor action;
3. build all movement intents from same canonical step snapshot;
4. group simultaneous collisions before mutation;
5. resolve groups using explicit registered collision tables;
6. apply body states simultaneously for the step;
7. emit at most one harvest output per eligible collision lineage;
8. apply receiver/world triggers;
9. evaluate objectives/invariants;
10. continue next step while motion remains;
11. terminate when settled or reject content during validation if hard ceiling would be reached;
12. commit one new canonical state/revision and one parent history transaction;
13. presentation receives an immutable `ResolutionPresentationPlan` after the result exists.

No player command enters an already-running chain. Pause/Step only controls reveal.

## 15.3 Two-buffer step rule

Every movement step uses:
- immutable `StepStartSnapshot`;
- intent buffer;
- simultaneous collision-group resolver;
- next-state buffer;
- post-step causal events.

No low-ID body can mutate state observed by a later body during intent calculation.

---

# 16. Collision registry implementation contract

Collision behavior is data-driven from a bounded registry keyed by explicit canonical tuples, including:
- mass classes;
- incoming direction/band;
- relation profile;
- anchored/movable roles;
- body family tags;
- registered simultaneous-group type.

The registry returns typed `CollisionOutcome` data only.

Forbidden:
- engine rigid-body restitution determining canonical result;
- float impulse calculations later quantized differently per frame;
- scene callbacks that special-case a named case/body;
- dictionary iteration deciding simultaneous contact order.

A build-time coverage report must prove every reachable authored collision tuple is defined.

---

# 17. Determinism contract

## 17.1 Forbidden domain inputs

Domain Core must not read:
- wall-clock time;
- frame delta / FPS;
- OS locale;
- controller/device identity;
- animation state;
- render coordinates;
- engine physics collision order;
- uncontrolled RNG;
- hash-map/dictionary iteration order;
- scene-tree child order;
- Steam user/account identity.

## 17.2 Numeric policy

Gameplay uses enums, stable IDs and integers.

Presentation uses floats for drawing/interpolation only. They cannot feed back into canonical state.

If a later canonical value truly needs fractional arithmetic, use documented fixed-point integer units and explicit rounding; do not introduce ambient floating-point physics.

## 17.3 Stable ordering

All result-affecting set operations explicitly sort by:
1. frozen gameplay priority;
2. authored stable boundary/group order where specified;
3. stable ID as final tie-break only when semantics permit.

Container order is never meaningful.

---

# 18. Canonical serialization / state hashing

## 18.1 Canonical form

Define a versioned canonical serialization independent of Godot object serialization:
- fixed field ordering;
- sorted stable-ID collections;
- explicit enum integer/string encoding;
- normalized UTF-8 stable tokens;
- no timestamps, localized strings, scene instance IDs or presentation coordinates;
- no unordered dictionaries without sorted-key conversion.

## 18.2 Hash

Working frozen direction: **SHA-256 of canonical UTF-8/binary canonical serialization**, labeled `canonical_hash_version = 1`.

Hash scope includes all result-relevant case state and excludes diagnostics/session timestamps/UI settings.

## 18.3 Replay fixture

A golden replay contains:
- exact case/content/rules/collision-registry identity;
- initial state hash;
- ordered semantic commands;
- expected revision/post-state hash per command;
- expected key collision/lineage events;
- expected final objective/mastery assertions.

Headless replay must reproduce every expected hash.

---

# 19. Causal-event DAG implementation

Typed event registry must cover at least Phase-4 events:
- PLAYER_COMMAND_COMMITTED;
- DONOR_RESET;
- BODY_MOTION_STARTED;
- BODY_MOVED_STEP;
- COLLISION_RESOLVED;
- HARVEST_OUTPUT_EMITTED;
- IMPACT_PICKED_UP;
- IMPACT_TRANSFORMED;
- IMPACT_SPENT;
- RECEIVER_STATE_CHANGED;
- BODY_BROKEN;
- SECONDARY_COLLISION_CREATED;
- OBJECTIVE_CHANGED;
- INVARIANT_CHANGED;
- CASE_COMPLETED.

Each event stores:
- transaction ID;
- deterministic event ordinal;
- event type;
- stable subjects;
- typed before/after facts;
- ordered material parent IDs;
- movement-step index where relevant.

The domain stores enough material ancestry for UX questions, but may omit non-material internal reads. Presentation may collapse lane-step events; it may not fabricate ancestry.

---

# 20. Undo / Redo / history checkpoint architecture

## 20.1 History unit

Every accepted domain-changing semantic command creates one canonical history transaction. Derived movement/collisions/pickups/objective changes are children of the initiating command.

Navigation/traversal transactions may be compacted in presentation history, but the canonical history/checkpoint stream still preserves the exact player node required to restore subsequent actions.

## 20.2 Snapshot strategy

Preferred 1.0 implementation: **full canonical CaseState checkpoint for every accepted command**, optionally compressed.

Reason: cases are deliberately small and exact recovery/Undo is more important than sophisticated inverse deltas.

A later internal delta representation is allowed only if metamorphic tests prove exact semantic equivalence.

## 20.3 Undo

Undo restores the exact pre-command checkpoint, including:
- player node/state;
- every body;
- inventory/world pickups;
- impact IDs/transform history;
- lineage emission state;
- donor generations;
- receiver/device states;
- objectives/invariants/mastery eligibility;
- causal graph/history cursor.

## 20.4 Redo

Redo on an intact branch may:
- restore stored post-checkpoint; or
- replay the semantic command and assert the stored post-hash.

Debug/headless validation should prefer replay+assert. New accepted command after Undo truncates redo branch.

Raw history length is never a mastery input.

---

# 21. Content source / compiler pipeline

## 21.1 Authoring source

Use human-reviewable, version-control-friendly structured content: Godot Resources, JSON-like source, or another deterministic text format. Exact syntax is implementation-flexible; compiled schema semantics are frozen.

Known solution fixtures are kept as validation data and never exposed as ordinary hint data.

## 21.2 Compiler output

For each case compile:
- normalized `CaseDefinition`;
- content hash/version identity;
- stable ID registries;
- movement/traversal graphs;
- collision coverage table;
- simultaneous-contact group registry;
- donor/receiver/transform registries;
- authored focus/navigation graph;
- objective/invariant/mastery registry;
- progression/tutorial prerequisites;
- known solution fixtures;
- anti-repetition/reasoning tags;
- validation report.

## 21.3 Structural validation

Reject:
- duplicate/missing stable IDs;
- broken room/lane/node references;
- unreachable required interactions caused by malformed topology;
- undefined reachable collision tuple;
- ambiguous unregistered multi-contact;
- impact direction/band outside frozen registry;
- inventory capacity >3;
- transform outside quarter-turn/reverse/mirror/damper;
- receiver outside R1–R8 or invalid composition;
- donor without exactly one regeneration class;
- moving receive window tied to animation time rather than canonical step state;
- chain ceiling >24;
- case exceeding Phase-5 hard body/room/donor/receiver/device ceilings;
- arbitrary gameplay callback/script hook.

## 21.4 Progression/commercial validation

Compiler validates:
- C01–C34 exact prerequisite graph from Phase 7;
- tutorial-tag prerequisites are satisfied by graph order;
- C34 reachable with zero mastery;
- remixes never gate main campaign;
- R01–R03 unlock at C14, R04–R07 at C28, R08–R10 at C34;
- no progression currency/power field exists in schema;
- no mastery contract reads raw Undo/time/accessibility/input history.

## 21.5 Reasoning diversity validation

Validate Phase-5 windows:
- every case has one dominant reasoning-transformation tag;
- from C15 no three consecutive cases share the same dominant tag across all three;
- every five-case C15+ window has >=3 distinct dominant tags;
- Act IV/V cannot rely only on direction/magnitude matching;
- mature provenance counterfactual metadata is present.

## 21.6 Mastery validation

Every mastery instance requires:
- mastery family;
- machine predicate;
- `mastery_distinction_note`;
- one known satisfying fixture/state;
- proof it does not use raw Undo/time/pause/assist/input history.

## 21.7 Remix validation

Every remix requires:
- source substrate ID;
- changed facts;
- `changed_causal_dependency`;
- expected new reasoning transformation;
- known valid fixture;
- proof source-case solution does not trivially transfer unchanged.

Parameter/art-only padding fails validation.

---

# 22. Donor/exploit validation tooling

## 22.1 Lineage uniqueness

Automated fixtures assert:
- one emission max per lineage;
- transform preserves identity;
- consumed impact cannot reappear;
- Undo restores one branch rather than retaining both.

## 22.2 Donor regeneration graph

Bounded state/search tooling flags:
- RESETTABLE donor with zero meaningful world/route cost;
- renewable net-positive STRONG loops;
- CYCLIC_WEAK -> renewable MEDIUM/STRONG escalation;
- transform/secondary-collision cycles that duplicate impact count or power.

## 22.3 Strong-force dominance report

For authored and solver-found solutions where feasible, record meaningful magnitude choices. Flag cases where strongest-available impact is universally dominant or weaker bands never create advantage.

## 22.4 Provenance counterfactual

For C15+, validator/content review stores whether removing donor world-state and handing equivalent impacts at start would preserve the primary challenge. `YES` is a mature-content failure unless the case is explicitly an early identity tutorial.

---

# 23. Known-solution / bounded-search tooling

Every campaign/remix case stores at least one exact-version known baseline solution fixture.

The harness must:
- replay fixture;
- assert hashes/collision outcomes/lineages/objectives;
- verify settlement below chain ceiling;
- verify no illegal command is embedded;
- verify mastery fixtures separately.

Bounded search is recommended for compact cases to detect:
- accidental one-action solution;
- donor-factory loops;
- max-force dominance;
- neutral pickup/storage trivialization;
- dead state mislabeled solvable;
- known solution no longer valid after content edit.

Exhaustive solving of every late case is not required if the reachable state space is too large; structural validation + known fixtures + targeted adversarial search remain mandatory.

---

# 24. Persistence domains

Use separate logical documents:

1. **settings** — accessibility, audio, language, remaps, UI/presentation preferences.
2. **profile_progress** — case clears, mastery IDs, tutorial tags, remix unlock facts, local achievement mirror, demo-import receipts.
3. **active_case** — current exact case state, history/checkpoints, active content identity.
4. **recovery_backup** — previous verified generation(s) of mutable documents.

Frequently changing active-case data should not require rewriting all lifetime progress/settings.

---

# 25. Save envelope / durable write protocol

## 25.1 Envelope fields

Every persistent document contains:
- `format_id`;
- `save_schema_version`;
- profile ID;
- document type;
- monotonic generation;
- creator build version;
- content/rules/collision version where relevant;
- canonical payload;
- payload checksum/hash;
- optional diagnostic timestamp not used for gameplay/merge authority.

## 25.2 Durable write

Required application protocol:
1. serialize next envelope to temporary file;
2. flush/close;
3. read back and validate schema/checksum;
4. preserve current valid primary as backup generation;
5. rename validated temp to primary where supported;
6. report `saved` only after primary/newest-valid generation is verifiably readable.

Do **not** assume rename is universally crash-atomic. Recovery always considers valid primary/backup/temp remnants.

## 25.3 Transaction durability boundary

An in-memory domain transaction becomes authoritative for the current process when completed, but persistence never writes a partial movement chain.

Crash outcomes:
- before complete transaction checkpoint is durably written: recover previous valid revision;
- after new complete revision is durably written but before animation finishes: recover new state; causal history explains what happened;
- no partially consumed token / partially advanced body state is recoverable as canonical.

---

# 26. Load / corruption recovery

For each document type:
1. enumerate recognized primary/backup/temp candidates;
2. reject checksum/schema/profile mismatch;
3. migrate supported schema candidates in memory;
4. choose highest valid compatible generation;
5. if equal-generation payloads differ, preserve/surface conflict rather than selecting by filename/iteration order;
6. rewrite a clean primary only after successful recovery selection.

Fallback rules:
- missing/corrupt settings -> defaults;
- missing/corrupt active case -> keep profile, return to Case Board / restart active case;
- corrupt profile with no valid backup -> Recovery UI, preserve original evidence, do not silently overwrite with zero progress.

---

# 27. Save schema / content compatibility

Save schema version and case/rules version are separate.

## 27.1 Schema migration

Every supported persistent schema change supplies monotonic `N -> N+1` migration fixtures. Migrations operate on data, not scene nodes/localized text.

## 27.2 Active-case compatibility

An active case resumes only if its ruleset/content/collision-registry identity is explicitly supported.

If incompatible:
- preserve durable profile progress;
- archive/preserve incompatible active case for diagnostics/recovery;
- explain that the unfinished case changed and must restart;
- restart from current canonical case definition if player chooses;
- never best-effort reinterpret body/lineage state under changed collision rules.

Historical clear/mastery facts remain monotonic unless an explicit migration can prove a record no longer maps to a canonical ID. Default is preservation with version tagging.

---

# 28. Steam Cloud / cross-device semantics

## 28.1 Independence

Steam Cloud is a storage adapter. The game is fully playable/saveable offline without Steam connectivity.

## 28.2 Cloud candidates

Target cloud data:
- `profile_progress`;
- portable settings excluding machine-specific display/window values;
- `active_case` only if branch-conflict/recovery testing is robust before release.

Do not cloud logs, caches, generated thumbnails or machine-specific graphics/device state.

## 28.3 Profile semantic merge

When the application can inspect both valid progress documents:
- case clear = boolean OR / compatible-set union;
- tutorial tags = union;
- mastery IDs = union only when canonical mastery definition/version is compatible; otherwise preserve historical tagged record separately;
- remix unlocks = re-derived from merged main-case clears;
- demo import receipts = union;
- achievement mirror = union, platform remains external authority for Steam achievement state;
- no currency/power conflict exists because Phase 7 forbids those systems.

Merged profile gets a new generation with parent envelope hashes for diagnostics.

## 28.4 Settings merge

Use per-setting logical revisions for portable settings. Higher setting revision wins. Equal revision with divergent values preserves current local value and records conflict; wall-clock timestamp is not sole authority.

## 28.5 Active-case ancestry merge

Auto-select one active case over another only when:
- same session ID;
- same case/content/rules/collision identity;
- one semantic command sequence is an exact prefix of the other;
- all shared checkpoint hashes match.

Then keep the strict descendant.

Divergent branches or different session IDs are never synthesized. Preserve both candidates when adapter permits and present a human-readable recovery choice. Profile progression merges independently.

If the chosen Steam integration cannot expose both conflicting candidates, document reliance on Steam conflict selection + local backups rather than pretending app-level branch merge is guaranteed.

---

# 29. Demo -> full import identity

Demo and full game use separate application IDs but the same logical progress-schema family.

`DemoImportCandidate` contains:
- demo profile ID;
- demo build/content/rules identity;
- settings subset;
- DEMO01..DEMO05 completion/tutorial facts;
- any explicitly equivalent campaign-clear/mastery facts;
- checksum;
- deterministic import receipt ID derived from candidate identity/hash.

`demo_to_full_mapping` is explicit/versioned. It may map:
- settings;
- tutorial tags;
- exact equivalent case clears only where equivalence is declared;
- compatible mastery facts only where contract identity is equivalent.

Rules:
1. validate candidate;
2. apply explicit mapping only;
3. union/merge monotonically;
4. record receipt;
5. reapplying same receipt is no-op;
6. never infer campaign clear from similar title/lesson;
7. incompatible active demo case is not synthesized into full game;
8. compatible settings may still import when clear mapping is refused.

Demo achievements are not independently authoritative; full game may grant compatible achievement conditions after validated import/load.

---

# 30. Semantic input abstraction

Use Godot `InputMap`/semantic action architecture. Domain receives semantic commands, never physical device events.

Required action families include:
- move/focus north/south/east/west;
- confirm/interact;
- cancel/back;
- inspect;
- collect;
- cycle impact previous/next;
- focus compatible receiver previous/next;
- choose snap orientation;
- transform/spend confirmation;
- Undo/Redo;
- Pause/Step;
- room overview/breadcrumb navigation;
- history/causal navigation;
- settings/help.

Physical bindings are remappable. Active-device glyph switching cannot alter focus or domain state.

---

# 31. Deterministic authored focus graph

Keyboard/controller map navigation cannot depend on runtime nearest-float guesses alone.

Each room compiles a focus graph over:
- traversal nodes;
- pickups;
- compatible receivers;
- transform devices;
- donor/reset interactions;
- relevant inspection targets.

Auto-generation may propose neighbors from authored presentation coordinates, but the compiled graph is stable data and supports author overrides.

Validation asserts:
- every required interactive target reachable from at least one normal traversal/focus path;
- no required focus island;
- directional selection stable across zoom/UI scale/layout;
- disabled targets have deterministic skip/focus semantics;
- same room state + input sequence selects same semantic target across devices.

---

# 32. Steam Deck / controller technical targets

- 1280×800 primary Deck validation resolution;
- all gameplay functions reachable through controller path;
- no mandatory text typing during cases;
- no free-angle analog precision;
- impact/receiver/focus glyphs readable without hover;
- UI honors Phase-6 44 logical-pixel target direction and text scaling;
- active input glyph family may change presentation only;
- controller disconnect/reconnect must preserve semantic focus and paused/settled domain state;
- Reset Controls remains reachable after deliberately broken remap.

---

# 33. Localization pipeline

Gameplay identity uses stable IDs/enums/tokens, never translated text.

Examples:
- `CASE_C14_TITLE`;
- `IMPACT_DIR_NE`;
- `IMPACT_BAND_MEDIUM`;
- `RECEIVER_FRAGILE`;
- `DONOR_RESETTABLE`;
- `OBJ_PRESERVE_CARGO`.

Localized strings are presentation only. Direction remains mechanical enum even when translated display label differs.

Preferred workflow: PO/gettext or another version-control-friendly Godot-supported format with runtime locale selection and pseudolocalization.

Validation fails on:
- missing source-language token;
- translated string used as gameplay key;
- invalid/missing format placeholder;
- critical UI string omitted from pseudolocalization coverage.

Layouts must preserve Phase-6 text expansion/accessibility targets. Directional UI icons that mean physical world directions are **not** mirrored by locale simply because UI reading direction changes; only navigation/back/forward interface icons should follow locale conventions where appropriate.

---

# 34. Headless deterministic test harness

Implementation repository must provide one documented command that runs domain/content tests in Godot `--headless` mode and exits nonzero on failure.

Required test families:

1. stable ID/schema/compiler tests;
2. collision table coverage/golden tuples;
3. simultaneous collision grouping;
4. lineage one-emission/duplication tests;
5. donor regeneration tests;
6. transform identity/no-duplication tests;
7. receiver safe/unsafe/illegal spend tests;
8. self-launch/landing secondary collision tests;
9. moving receive-window canonical-step tests;
10. bounded chain settlement tests;
11. objective/invariant/mastery tests;
12. Undo/Redo exact hash tests;
13. known solution fixtures for every case/remix;
14. progression/prerequisite graph tests;
15. remix changed-dependency validation;
16. save/recovery fault injection;
17. schema migration fixtures;
18. Cloud semantic merge fixtures;
19. demo import idempotency/monotonicity;
20. focus-graph/controller reachability smoke tests;
21. localization-domain independence tests;
22. golden replay state-hash fixtures.

---

# 35. Metamorphic / invariance tests

Mandatory high-value invariants:

- same initial state + same semantic command sequence -> same hash;
- locale change -> no domain-hash change;
- input device change -> no domain-hash change;
- animation speed/reduced motion -> no domain-hash change;
- scene rendering enabled vs headless -> same domain result;
- dictionary insertion order perturbation -> same domain result after stable sorting;
- Undo(Command(S)) -> exact S;
- Redo(Undo(Command(S))) -> exact post-command state when branch intact;
- duplicate committed command ID -> no second revision;
- stale pre-state hash -> no mutation;
- converter chain never changes impact count;
- damper never increases magnitude;
- one lineage never emits twice;
- full inventory changes collection availability but not whether already-emitted world pickup exists;
- interrupted presentation after durable transaction -> recovery loads committed domain state;
- forced crash before durable transaction checkpoint -> recovery loads previous complete revision.

---

# 36. Fault-injection persistence tests

Simulate process/storage failure at each durable-save stage:
- before temp creation;
- during temp write;
- after temp write before readback;
- after readback before backup;
- after backup before primary replace;
- after primary replace before UI acknowledgement.

Expected invariant: loader selects a recognized valid complete generation or reports unrecoverable corruption without overwriting all evidence.

Also inject:
- corrupted checksum;
- unsupported schema;
- unsupported active-case rules version;
- equal-generation divergent payload;
- Cloud profile divergence;
- Cloud active-case branch divergence;
- duplicate demo receipt.

---

# 37. Performance / memory budgets

Borrowed Collision is intentionally compact. Budgets prevent accidental architectural bloat.

## 37.1 Domain

Target on minimum-supported desktop / Steam Deck-class hardware:
- typical accepted non-chain command: <=5 ms p95;
- typical spend/collision transaction: <=12 ms p95 excluding presentation;
- worst authored late-game 24-step safety-bound transaction: <=50 ms p99;
- case definition compile/load validation at runtime: <=250 ms for one case after source assets loaded; shipping builds should normally consume prevalidated compiled data;
- no simulation result depends on meeting a timing budget.

## 37.2 Presentation

- target 60 FPS at 1280×800 Deck layout;
- 30 FPS remains mechanically correct/playable because domain is frame-independent;
- no case requires more than Phase-5 active-body ceilings;
- causal ribbon/history expansion should not instantiate unbounded UI nodes.

## 37.3 Memory

Targets:
- typical runtime working set substantially below 1 GB; hard design expectation comfortably under 1 GB on Deck;
- one active case full Undo/checkpoint history normally <=64 MB uncompressed-equivalent target;
- profile/settings/save documents kilobytes to low megabytes;
- causal history may prune/collapse presentation-only detail after canonical support bundle/checkpoint requirements are satisfied, but may not break Undo/provenance for current branch.

## 37.4 Save/load

- ordinary checkpoint serialization/write should not create visible multi-second stalls;
- Case Board -> ordinary case interactive target <=2 s on SSD/Deck-class storage after initial boot/assets;
- performance optimization may not weaken durable-write or deterministic checks.

---

# 38. Failure handling

## Illegal/stale command
Typed rejection; no revision/history/save generation.

## Unexpected domain assertion
Development/headless: fail loudly with case identity, command, pre-state hash, collision/group trace.

Release: cancel uncommitted transaction, preserve latest safe checkpoint, show recoverable error rather than saving partial state.

## Chain safety ceiling reached
Shipped valid content should never hit this. Treat as implementation/content error, preserve pre-command checkpoint, emit diagnostics, do not present as ordinary puzzle failure.

## Corrupt active case
Try valid backups. If none, retain profile and restart only current case.

## Corrupt profile
Never silently zero-and-overwrite. Preserve originals and enter Recovery UI if no valid backup/migration exists.

## Unsupported old active case
Archive/preserve, retain compatible profile progress, restart current canonical case only.

## Steam/platform unavailable
Local save/progression continues. Achievement/cloud reconciliation may retry later; it never blocks completion.

---

# 39. Observability / deterministic replay support bundle

Developer/support diagnostics should expose:
- build version;
- exact case/content/rules/collision versions;
- canonical state hash;
- session revision;
- recent semantic command sequence;
- collision-group trace;
- lineage graph summary;
- save candidate/generation report;
- content validation report.

A shareable QA `replay bundle` should contain:
- exact case/version identity;
- initial checkpoint/hash;
- ordered semantic commands;
- expected/observed revision hashes;
- optional causal trace;
- no unnecessary Steam account IDs, personal filesystem paths or unrelated telemetry.

Headless QA can replay this bundle to reproduce a reported final hash.

---

# 40. Implementation slices / handoff ladder

## 12A — Technical Bootstrap
Build only:
- pinned Godot project;
- Domain Core folder/module boundary;
- stable IDs/enums;
- minimal CaseDefinition/CaseState;
- canonical serialization/hash;
- one collision tuple;
- semantic command skeleton/idempotency;
- headless test command;
- local save envelope skeleton.

Exit gate: one tiny deterministic fixture repeats identical hashes across many runs, headless tests pass, no scene is gameplay authority.

## 12B — Vertical Slice / existential proof
Implement a DEMO01–DEMO03/C01–C05-sized slice:
- authored movement lane;
- real collision -> persistent impact pickup;
- collect;
- spend on Ordinary Mover;
- quarter-turn transform;
- magnitude window + fragile strong-is-bad result;
- exact Undo/Redo;
- world/belt/provenance presentation;
- mouse+keyboard and controller path;
- one save/reload fixture.

Exit gate: naive-player-facing prototype can truthfully demonstrate `collision -> stored consequence -> transform -> spend -> deterministic aftermath`; repeated identical runs hash identically.

Do **not** mass-produce content before this gate is empirically promising.

## 12C — Core Systems Complete
Add:
- full collision registry/mass relationships;
- all donor regeneration classes;
- R1–R8;
- mirror/damper;
- secondary chain-generated lineages;
- self-launch;
- moving receive windows/Pause-Step;
- 2/3-slot behavior;
- multi-room world pickups;
- all objectives/invariants/mastery predicates;
- complete causal ancestry;
- exact history.

Exit gate: all Phase-4 mechanics + system acceptance tests pass using data-driven cases only.

## 12D — Content Population
Implement compiler/validators and populate C01–C34 + R01–R10 + DEMO01–DEMO05 through data.

Exit gate: every case validates, every main/remix has known solution fixture, progression graph valid, anti-repetition/donor/strong-force/provenance reports pass.

## 12E — UX / Accessibility / Controller / Deck
Complete Phase-6 flows, all input modes, authored focus graphs, settings/help/localization scaffolding, reduced motion/flash, high-clarity labels, Deck 1280×800 QA and recovery UI.

Exit gate: all required case interactions completable keyboard-only and controller-only without free-angle precision or missing hover-only information.

## 12F — Adversarial QA
Fault injection, duplicate command/lineage attacks, donor factory search, state corruption, save migrations, branch conflicts, active-case incompatibility, dead-end detection, long-chain edge cases, performance profiling.

## 12G — Empirical Gates
Run deferred player/product gates:
- consequence-transfer comprehension;
- direction/magnitude misunderstanding rate;
- strongest-force dominance;
- blind token-permutation rate;
- provenance relevance;
- arrow-inventory mis-positioning;
- demo second-generation-lineage `aha`;
- mastery/remix distinctness;
- controller/Deck readability;
- price/value perception near release.

A failed empirical gate triggers the smallest canonical amendment, not uncontrolled feature expansion.

## 12H — Release Candidate
Final regression, exports, Steam integration, demo/full import, Cloud/achievement checks, localization/content validation, performance/package checks and release checklist.

---

# 41. CI / notification-safe implementation expectation

The later dedicated implementation repository must include a CI/email-noise policy in its handoff.

During unstable 12A/early 12B:
- headless tests should run locally in the implementation session where practical;
- remote CI should be manual (`workflow_dispatch`) if the suite is expected to fail repeatedly;
- automatic push/PR CI should be enabled only after the baseline suite is consistently green;
- a workflow producing repeated failed runs should return to manual-only until repaired;
- avoid bursts of tiny commits/pushes used only to probe CI.

This is an implementation-process guardrail, not gameplay canon.

---

# 42. Explicit technical non-goals

Do not add for 1.0:
- engine rigid-body contacts as authoritative gameplay;
- continuous free-space Newtonian simulation;
- float-angle/vector solving;
- physics-based ragdolls as mechanics;
- combat/projectile weapon system;
- procedural case generator;
- generic embedded scripting language for case authors;
- arbitrary token modifiers/elements/upgrades;
- ECS rewrite for scale;
- online authoritative backend;
- multiplayer synchronization;
- Workshop/editor architecture;
- cloud requirement for offline play;
- telemetry requirement for progression;
- AI-generated gameplay rules/content at runtime.

---

# 43. Technical risks / gates

## T8-R1 — presentation leaks into physics
Gate: interactive presentation and headless semantic replay yield identical hashes/events.

## T8-R2 — collision table incompleteness
Gate: compiler coverage proves every reachable authored tuple/group has exactly one registered outcome.

## T8-R3 — lineage duplication
Gate: duplicate command/load/pause/transform/save fixtures cannot produce a second impact from one lineage.

## T8-R4 — donor-factory exploit
Gate: bounded search/fixtures detect renewable strong escalation and zero-cost RESETTABLE factories.

## T8-R5 — traversal/history ambiguity
Gate: save/Undo/Redo fixtures restore exact player node, pickup accessibility and subsequent command legality even after multi-room movement.

## T8-R6 — Cloud branch data loss
Gate: monotonic profile merge + strict active-case ancestry test; divergent branches never synthesize.

## T8-R7 — content special-case creep
Gate: shipped case source cannot register arbitrary gameplay callbacks; all mechanics compile through frozen registries.

## T8-R8 — controller focus drift
Gate: authored focus graph deterministic across zoom/UI/device and every required target reachable.

## T8-R9 — localization changes semantics
Gate: language/pseudolocalization changes no canonical hash or impact/receiver identity.

## T8-R10 — save crash window
Gate: fault injection always finds a valid complete generation or preserves evidence without silent reset.

## T8-R11 — quantized physics expectation mismatch
Technical response: never increase precision to imitate sandbox physics; presentation and tutorial must truthfully show authored lanes/discrete impacts. Empirical gate remains Phase 12G.

## T8-R12 — content-state search explosion
Gate: late content may rely on known fixtures + targeted bounded adversarial search rather than requiring exhaustive proof; hard state ceilings remain enforced.

---

# 44. Phase-8 acceptance tests

## Engine / architecture
- **T8-01** Project pins exact stable Godot version; no ambient `latest` upgrade.
- **T8-02** Domain fixture runs headlessly without loading gameplay presentation scenes.
- **T8-03** Presentation cannot mutate canonical bodies/impacts/lineages except through semantic commands.
- **T8-04** Platform/Steam adapter absence does not block local play/save/completion.
- **T8-05** Engine physics contacts/frame delta are absent from canonical collision resolution.

## State / determinism
- **T8-06** Canonical CaseState includes exact player/body/impact/donor/receiver/lineage/objective state required to resume deterministically.
- **T8-07** Same content identity + pre-state + command sequence yields identical SHA-256 canonical hashes across repeated runs.
- **T8-08** Locale, input device, animation speed and reduced motion cannot change domain hash.
- **T8-09** Stable sorting prevents dictionary/scene insertion order from changing collision/group result.
- **T8-10** Presentation float coordinates never enter collision-table keys.

## Commands / transactions
- **T8-11** Stale expected revision/pre-hash rejects with no mutation.
- **T8-12** Duplicate committed command ID cannot advance revision twice.
- **T8-13** Structurally illegal collect/transform/spend/reset creates no history/save generation.
- **T8-14** One accepted spend increments canonical revision/history exactly once regardless of derived chain length.
- **T8-15** All movement intents for one step read the same StepStartSnapshot.
- **T8-16** Shared-body simultaneous collision uses one registered group, not sequential body order.
- **T8-17** Independent same-step collisions cannot affect each other through processing order.
- **T8-18** Self-launch is resolved through ordinary R6 spend + movement/collision rules.
- **T8-19** Moving receiver legality references canonical window-state ID, not animation time.

## Impact / lineage / donor
- **T8-20** One collision lineage emits at most one impact under duplicate UI/load/pause/replay attempts.
- **T8-21** Full inventory leaves already-emitted pickup in world rather than suppressing/duplicating it.
- **T8-22** Transform preserves impact ID/source lineage and appends deterministic history.
- **T8-23** Converter chain cannot branch/duplicate one impact.
- **T8-24** Damper never raises magnitude.
- **T8-25** EXHAUSTIBLE donor cannot regenerate without Undo/Restart.
- **T8-26** RESETTABLE generation advances only through valid visible reset command.
- **T8-27** CYCLIC_WEAK/transform/chain composition cannot create unintended renewable stronger-source loop in validated content.
- **T8-28** CHAIN_GENERATED impact has distinct new lineage whose ancestry includes parent spent impact/collision.

## Undo / history
- **T8-29** Undo restores exact pre-command hash including player location and world pickups.
- **T8-30** Redo on intact branch restores/replays exact stored post-hash.
- **T8-31** New accepted command after Undo truncates redo branch without leaving duplicate lineage/pickup state.
- **T8-32** Raw history/Undo count is inaccessible to mastery predicates.

## Content compiler
- **T8-33** Duplicate/missing stable references fail compilation.
- **T8-34** Undefined reachable collision tuple or ambiguous multi-contact fails compilation.
- **T8-35** Case exceeding frozen room/body/donor/receiver/transform/inventory/chain ceilings fails compilation.
- **T8-36** Case-specific arbitrary gameplay callback is rejected/unsupported.
- **T8-37** Every main/remix case has exact-version known baseline solution fixture.
- **T8-38** Known solution fixture reproduces expected hashes/lineages/objectives and settles below hard chain ceiling.
- **T8-39** C01–C34 prerequisite graph is acyclic and C34 reachable with zero mastery.
- **T8-40** Remix pack unlocks derive exactly from C14/C28/C34 and do not gate campaign.
- **T8-41** Reasoning-transformation window rules validate from C15 onward.
- **T8-42** Every mastery contract has distinction note + satisfying fixture and reads no forbidden experiment/accessibility history.
- **T8-43** Every remix declares changed causal dependency and proves source solution does not trivially transfer unchanged.

## Persistence / recovery
- **T8-44** Primary corrupt + valid backup loads valid backup without losing compatible profile progress.
- **T8-45** Complete valid temp/new generation can recover after interrupted replacement.
- **T8-46** Equal-generation divergent payload is surfaced as conflict/corruption, never chosen by iteration order.
- **T8-47** Unsupported active-case collision/rules version preserves profile and restarts case rather than reinterpreting state.
- **T8-48** Every supported save schema hop has deterministic migration fixture.
- **T8-49** Forced failure during an uncommitted chain cannot load a partial token/body/lineage hybrid.
- **T8-50** Platform outage cannot block safe local save.

## Cloud / demo
- **T8-51** Compatible profile merge never loses case clear/tutorial/mastery facts.
- **T8-52** Active-case auto-selection occurs only for strict command-history/hash descendant.
- **T8-53** Divergent active branches are never synthesized.
- **T8-54** Reapplying same demo receipt is idempotent.
- **T8-55** Incompatible demo clear can be skipped while compatible settings/tutorial facts import through explicit mapping.
- **T8-56** Demo similarity alone never auto-clears C01–C34 without declared equivalence.

## Input / localization / Deck
- **T8-57** Mouse+keyboard, keyboard-only and controller paths can emit every required semantic gameplay command.
- **T8-58** Same semantic command sequence from different devices yields same domain hash.
- **T8-59** Every required interactive target is reachable in compiled authored focus graph.
- **T8-60** Focus selection result is stable across zoom/UI scale/device glyph changes.
- **T8-61** Reset Controls remains reachable after broken remap.
- **T8-62** Missing source localization token fails validation.
- **T8-63** Translated strings are never gameplay identity/lookup keys.
- **T8-64** Pseudolocalization cannot change domain hash.
- **T8-65** 1280×800 Deck smoke pass keeps required controls/readability accessible without mandatory pointer/typing/free-angle aim.

## Test harness / failure / performance
- **T8-66** One documented `--headless` command runs domain/content fixtures and returns nonzero on failure.
- **T8-67** Golden replay bundle reproduces expected final hash from semantic commands only.
- **T8-68** Fault injection at each save-write phase retains a valid complete generation or preserves evidence and reports unrecoverable corruption safely.
- **T8-69** Representative late-game transaction meets performance budget on Deck-class reference hardware or triggers profiling before content expansion.
- **T8-70** Chain safety ceiling reached in a shipped-known-valid path is treated as content/implementation error, not normal puzzle fail.
- **T8-71** Replay support bundle contains enough deterministic state/command/version data to reproduce a reported result without personal account data.
- **T8-72** No automatic unstable push-CI is required for 12A/early 12B; implementation handoff can keep remote CI manual until baseline tests are green.

---

# 45. Phase-8 closure decision

- Engine/runtime direction frozen enough for implementation: **YES — Godot 4.7.1-stable, GDScript-first, deterministic 2D**
- Domain/Application/Presentation/Platform boundaries frozen: **YES**
- Canonical CaseDefinition/CaseState/body/impact/lineage/receiver models frozen: **YES**
- Semantic command / transaction / idempotency architecture frozen: **YES**
- Collision registry and discrete movement contract frozen: **YES**
- Canonical serialization/hash/replay contract frozen: **YES — SHA-256 canonical v1**
- Content compiler/validator contract frozen: **YES**
- Undo/Redo/checkpoint architecture frozen: **YES**
- Save/recovery/schema compatibility frozen: **YES**
- Steam Cloud semantic conflict policy frozen at application level: **YES, with adapter limitation explicitly documented**
- Demo/full import semantics frozen: **YES**
- Input/focus graph/Deck target frozen: **YES**
- Localization pipeline frozen: **YES**
- Headless/golden/metamorphic/fault-injection test architecture frozen: **YES**
- Performance/memory budgets defined: **YES**
- Implementation 12A–12H ladder defined: **YES**
- Technical non-goals/failure handling/observability defined: **YES**
- Phase-8 acceptance tests: **72**
- Production implementation started: **NO**
- Earlier canonical gameplay phase reopened: **NO**
- Phase 8 Technical Implementation Specification: **COMPLETE ON PAPER**
- DESIGN COMPLETE: **NO**

## Technical contradiction review

No genuine contradiction was found requiring Phase 3–7 reopening.

One implementation-sensitive clarification made here is intentionally narrow rather than a gameplay change: ordinary player traversal is represented as canonical semantic node-to-node state so save/Undo/interaction access can be exact. It does not add free-space physics or advance autonomous moving-body chains.

## NEXT PHASE

**Phase 9 — Whole-Game Simulation on Paper.**

The next run must walk the frozen product end-to-end through first boot, DEMO01..DEMO05, first 20 minutes, first 60 minutes, each campaign act, first secondary lineage, first donor-regeneration economy, first moving receive-window case, first multi-room causal-routing case, C34 synthesis, mastery/remix replay, demo->full transfer, interrupted save/recovery, Cloud divergence, all required input modes and hostile/unusual player behavior. It must identify boring loops, arrow-inventory mis-positioning, provenance loss, strong-force dominance, multi-room pickup friction, self-launch dexterity drift, moving-window ambiguity, causal-ribbon overload, persistence ambiguity and hour-10 exhaustion. Reopen only the smallest canonical phase if a true contradiction is proven.