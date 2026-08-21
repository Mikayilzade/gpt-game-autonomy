# GAME #004 — TECHNICAL IMPLEMENTATION SPECIFICATION

Last updated: 2026-08-21
Factory run: **12**
Phase: **8 — Technical Implementation Specification**
Working name: **HUSHLINE** (provisional / high-risk for final commercial use)
Phase status: **COMPLETE / LOCKED FOR DOWNSTREAM DESIGN**
Production implementation: **NOT STARTED**

This file defines how the locked Phase-3 through Phase-7 design can be implemented without allowing engine behavior, rendering, platform APIs or content-authoring shortcuts to become hidden gameplay rules. It does not add a new mechanic and does not begin production code.

---

## 1. Current technical direction

### 1.1 Engine baseline
Initial implementation target: **Godot 4.7.1-stable, GDScript-first**.

Current-version check performed 2026-08-21:
- Godot's official archive lists **4.7.1-stable** (2026-07-14) as the current stable 4.7 maintenance release;
- 4.7.2 is still release-candidate and 4.8 is development-only;
- Godot documents fixed-rate physics ticks independently from rendered frames and supports interpolation between them.

Therefore the dedicated implementation repository should start on **4.7.1-stable**, pin that exact editor/runtime version for bootstrap and test fixtures, and upgrade only after a deliberate compatibility pass. Do not start production on a 4.8 development build merely because it is newer.

Official references checked:
- https://godotengine.org/download/archive/
- https://godotengine.org/article/maintenance-release-godot-4-7-1/
- https://docs.godotengine.org/en/stable/tutorials/physics/interpolation/physics_interpolation_introduction.html

### 1.2 Why Godot fits this product
The locked game is a compact 2D/2.5D top-down deterministic product with modest scene complexity, custom graph logic, controller requirements, lightweight animation/VFX and no networking or free rigid-body simulation. Godot provides the needed 2D scene/UI/audio stack while allowing the gameplay rules to live outside the SceneTree.

### 1.3 Language
**GDScript-first** is the default because:
- the gameplay domain is small and data-heavy;
- engine integration and iteration are straightforward;
- no C#-only dependency is required by the frozen design;
- headless domain/content tests can remain inside one engine/toolchain.

A later hotspot may be moved to native code only after profiling proves a need. The acoustic graph sizes are too small to justify premature native optimization.

### 1.4 Rendering direction
Use Godot's 2D stack as the baseline. A 2.5D visual look may be created through layered sprites, lighting, shaders and authored perspective cues, but no 3D physics or 3D navigation dependency is required for the core game.

---

## 2. Non-negotiable architecture boundary

The implementation is split into four layers.

### Layer A — Deterministic Domain Core
Authoritative gameplay state and rules only:
- encounter state;
- canonical tick/time;
- player authoritative position/movement state and acoustic-node ownership;
- barrier rail/slot state;
- doors and graph mutations;
- moving source state;
- listeners and deterministic navigation state;
- sound event generation;
- acoustic propagation;
- listener hearing/retarget logic;
- direct-detection predicates;
- objectives/win/fail;
- checkpoints/snapshots;
- mastery counters;
- deterministic telemetry/events.

The Domain Core must not call:
- rendering APIs;
- animation/audio APIs;
- Steam APIs;
- wall-clock time;
- random functions without an explicit domain RNG state;
- SceneTree discovery to decide gameplay truth.

### Layer B — Runtime Orchestrator / World Binding
Godot-facing glue:
- converts Input actions to semantic domain commands;
- advances the fixed simulation clock;
- binds stable domain IDs to scene visuals/colliders/handles;
- sends immutable domain events/state views to presentation;
- owns checkpoint/save requests;
- handles scene loading/transitions.

Layer B may know Godot Nodes, but must not reimplement hearing, retarget, barrier attenuation or objective truth.

### Layer C — Presentation
Camera, sprites, animation, VFX, acoustic route drawing, UI, haptics and audio.

Presentation consumes authoritative domain state. It can interpolate or animate, but it cannot decide:
- whether a listener heard;
- which acoustic path is minimum;
- whether the barrier is mechanically active;
- whether a door is open for simulation;
- whether the player is detected;
- whether an objective is complete.

### Layer D — Platform Adapters
Steam/OS-specific services behind interfaces:
- achievements;
- Cloud/save availability;
- store overlay / full-game CTA;
- full-app ownership checks for demo flows;
- rich presence if implemented;
- platform input-glyph metadata.

The game must remain fully playable offline with a `NullPlatformAdapter`.

---

## 3. Authoritative state representation

### 3.1 Stable IDs
Every rule-bearing authored object receives a stable string ID at content-authoring time:
- encounter;
- node;
- edge;
- player spawn;
- listener;
- source;
- door;
- barrier;
- rail;
- slot;
- objective;
- checkpoint;
- mastery predicate;
- navigation node/edge;
- world binding.

IDs are immutable once public content/saves depend on them. Runtime collections with ambiguous iteration order must be sorted by stable ID before an ordering-sensitive operation.

### 3.2 Canonical numeric state
All rule-critical acoustic values are integers as already locked:
- strength 1–4;
- base attenuation 0–2;
- barrier addition +3;
- thresholds 1–3;
- tick counters/timers as integer ticks.

For motion state, the implementation should avoid making floating-point engine physics authoritative. Preferred bootstrap model:
- fixed-step domain positions stored in quantized integer world units (for example 1/1024 of a design unit, exact scale chosen during 12A);
- velocities/route progress represented as deterministic integer/fixed-point values;
- authored navigation paths/trigger regions compiled into deterministic domain geometry;
- presentation converts authoritative values to Godot `Vector2` for rendering.

The exact quantization scale is an empirical technical choice, not a gameplay rule. It must be fine enough that control feel is unaffected and coarse enough to make replay/state hashing stable.

### 3.3 No engine-physics authority
The baseline game has no design need for free rigid-body simulation. Therefore:
- do not rely on `RigidBody2D` outcomes for puzzle truth;
- do not derive listener hearing from physics raycasts;
- do not let a render frame determine node ownership;
- static collision/query helpers may be used as development tools, but authoritative state transitions must be reproducible by the Domain Core.

---

## 4. Fixed-step simulation contract

### 4.1 Baseline tick
Authoritative simulation target: **60 domain ticks per simulation second**.

Godot may render at any supported frame rate. Rendering interpolates between authoritative states and never feeds interpolated values back into the domain.

### 4.2 Simulation-speed assists
The UX-locked 100% / 85% / 70% / 55% assist presets change the relationship between wall-clock time and simulation time, not the rules inside a simulation tick.

Conceptually:
- the domain remains 60 ticks per simulation second;
- slower assists accumulate domain time more slowly against real time;
- player movement, listener movement, timers, moving sources, locomotion cadence and gameplay-relevant door movement all share that same domain clock;
- acoustic resolution remains instantaneous at its canonical tick;
- rendering/VFX playback may have separate cosmetic speed controls.

This preserves ordering and solution logic.

### 4.3 Per-tick order
The implementation must reproduce the Phase-4 order exactly:
1. capture semantic input for tick;
2. resolve player movement and node ownership;
3. advance barrier manipulation movement, excluding snap mutation;
4. advance physical interaction progress and collect pending mutations;
5. commit barrier snap/release;
6. commit door/object graph mutations in stable object-ID order;
7. advance moving environmental sources in stable source-ID order;
8. advance listener movement/timers and update listener node ownership;
9. generate due sound events with explicit emission snapshot semantics;
10. solve propagation for each event;
11. resolve hearing/event selection in stable listener-ID order;
12. resolve direct detection/fail;
13. resolve objective/win if no fail;
14. publish deterministic telemetry/presentation events;
15. increment tick.

No Node callback order may substitute for this explicit sequence.

---

## 5. Input command model

### 5.1 Semantic commands
Presentation/input code must convert device events to a small domain command packet per tick, for example:
- `move_axis_qx`, `move_axis_qy`;
- `fast_move_active`;
- `interact_pressed/released`;
- `cancel_pressed`;
- `preview_active` (presentation-facing, not a domain mutation by itself);
- `barrier_axis_q` while grabbed;
- `rotate_left/right` at legal station;
- `restart_requested` / `pause_requested` handled by orchestrator rather than normal domain step.

Analog axes are quantized before entering the authoritative simulation so replays do not depend on raw device float noise.

### 5.2 Godot InputMap boundary
Use Godot actions/InputMap for device abstraction and runtime remapping. Godot's stable documentation exposes adding/removing events from InputMap, but dynamic remap state is not itself a save format, so the game must persist user mappings separately.

Official reference checked:
- https://docs.godotengine.org/en/stable/classes/class_inputmap.html

### 5.3 Remap persistence
Store remaps by semantic action ID, device family and normalized binding record. On load:
1. load default project actions;
2. apply portable user remaps where valid;
3. drop invalid/missing device-specific bindings safely;
4. guarantee keyboard fallback for desktop development builds.

No gameplay save depends on a physical key code.

---

## 6. Acoustic graph implementation

### 6.1 Runtime graph
For each encounter, compile a compact immutable graph definition plus a small mutable edge-state overlay.

Immutable:
- node IDs;
- edge IDs;
- edge endpoints/direction;
- base attenuation;
- physical passage binding;
- optional door binding;
- optional barrier-slot binding.

Mutable overlay:
- enabled/disabled from door state;
- active barrier addition on exactly one snapped slot edge;
- any canonical visible mutation already allowed by the locked schema.

### 6.2 Minimum attenuation
Because normal graphs are <=12 acoustic nodes, prioritize correctness/traceability over micro-optimization.

For each sound event:
1. construct the event's graph snapshot after applying its explicit BEFORE/AFTER mutation semantics;
2. run deterministic shortest-cost propagation from source node using integer edge costs;
3. compute minimum attenuation to every reachable node;
4. derive `remaining_intensity = max(0, strength - min_cost)`;
5. determine listener hearing against persistent threshold.

Dijkstra with a stable `(distance, node_id)` queue is sufficient. An all-pairs method is also acceptable if it preserves the same result and trace contract.

### 6.3 Tied minimum routes
Do **not** choose one arbitrary shortest route for presentation.

Runtime result per relevant listener must include:
- minimum cost;
- the union/list of edges belonging to every mechanically valid minimum-cost simple route required by current content;
- a stable route/group ID representation for presentation/testing.

Preferred implementation for tiny graphs:
- compute minimum distance;
- enumerate simple paths whose cost equals that minimum, using visited-node protection;
- content validator caps route-density so enumeration remains small and presentation-readable;
- deduplicate route edge sequences and sort by stable edge-ID tuple.

A technical validator should reject pathological authored states whose tied-minimum simple-path count exceeds a reasonable tooling ceiling (provisional 16 per source→listener pair) or whose decision-relevant visual density violates the existing Phase-5 3–4-route readability ceiling. This does not change hearing math; it prevents authoring content that cannot satisfy the locked presentation contract.

### 6.4 Propagation result object
Canonical result should be a pure value object containing at minimum:
- `event_id`;
- `source_node_id`;
- `strength_band`;
- graph snapshot/version ID;
- `min_cost_by_node`;
- `remaining_intensity_by_node`;
- `minimum_route_sets_by_relevant_listener`;
- `listener_hearing_results`;
- stable reason/debug trace.

Presentation receives this object but cannot modify it.

---

## 7. Navigation and movement contracts

### 7.1 Listener navigation
Listeners use an authored deterministic navigation graph/polyline network separate from acoustic weights.

Navigation definition includes:
- stable nav node IDs;
- fixed/quantized world positions;
- directed/bidirectional nav edges;
- integer traversal cost/length;
- optional door binding;
- posted anchor and short patrol route IDs.

When an investigation begins:
- target world position and acoustic node are captured from the sound event at emission;
- deterministic A*/Dijkstra chooses a path using `(cost, nav_node_id)` stable tie ordering;
- the chosen path is stored in listener state so visual path and actual motion cannot diverge mid-route except after a canonical door/state mutation that explicitly forces replanning;
- any replan uses the same deterministic rule.

No random search wandering or engine navmesh tie-breaking is authoritative.

### 7.2 Player movement
The preferred 12A prototype uses custom deterministic kinematic movement against simple authored collision geometry rather than dynamic physics.

Requirements:
- same quantized input + same state produces the same position sequence;
- node ownership is computed after player movement at the canonical step;
- collision resolution ordering is explicit and stable;
- direct-detection queries use authoritative positions/regions, not interpolated render transforms.

If implementation evidence later shows Godot `CharacterBody2D` can satisfy all replay/checkpoint/parity gates across target platforms without hidden ordering differences, it may be used behind the same domain contract. That is an implementation substitution, not permission to relax deterministic tests.

---

## 8. Barrier implementation contract

The barrier is represented by one domain state:
- rail ID;
- last snapped slot ID;
- candidate/target slot ID;
- quantized progress along rail;
- legal orientation state;
- RESTING / GRABBED / MOVING / SNAPPING / RELEASED;
- current acoustically active edge or none.

Only `SNAPPING -> RESTING` at a fixed-step boundary activates +3 attenuation.

Between slots:
- active acoustic edge = none;
- old slot is reopened immediately after leaving its snap envelope;
- candidate preview uses a prospective candidate state and never mutates live attenuation.

Release midpoint ties return to last occupied slot exactly as Phase 4 states.

Scene animation follows domain rail progress. A visual panel overlapping a doorway early/late cannot change attenuation before domain snap.

---

## 9. Door/source/listener implementation contracts

### 9.1 Doors
Domain door state is exactly OPEN/CLOSED for baseline content. One mutation commits at its canonical step and updates both nav and acoustic connectivity from the same state record.

`emission_phase` is authored on the action/event and converted into an immutable event graph-snapshot ID. Presentation receives the same before/after fact; it never infers order from animation frames.

### 9.2 Moving sources
Moving environmental sources follow deterministic authored routes with quantized progress/tick timing. Periodic emissions reference domain ticks, not animation callbacks or audio playback time.

### 9.3 Listener state
Canonical listener record contains:
- stable ID;
- hearing threshold;
- state enum;
- authoritative position/node;
- posted anchor/patrol route progress;
- current investigation event ID;
- current investigation-causing received intensity;
- captured target position/node;
- chosen nav path + segment progress;
- search/return timers in ticks;
- direct-detection profile ID.

Retarget logic is one Domain Core function shared by gameplay and tests. Equal received intensity cannot reset an active investigation before ARRIVED/SEARCH.

---

## 10. Prediction architecture

### 10.1 One code path, two state instances
Prediction must call the **same** graph mutation, propagation and hearing functions as committed resolution.

Implementation model:
1. take a read-only canonical live state at a tick boundary;
2. create a lightweight prospective copy/copy-on-write state;
3. apply the candidate action at the same ordering phase where real action would commit;
4. generate the candidate event with the same source strength/node and emission phase;
5. solve propagation using the same function;
6. evaluate hearing using the same listener-threshold function;
7. return `PredictionResult` without committing prospective state to live domain.

No second "UI approximation" solver is allowed.

### 10.2 State copy cost
The state is intentionally small. Copying encounter-level scalar/array state for preview is acceptable. If profiling later requires optimization, structural sharing/copy-on-write may replace full copies only if test parity remains exact.

### 10.3 Preview cache
A cache may key on:
- canonical state hash/revision;
- candidate action ID;
- candidate slot/action parameters.

Cache is presentation optimization only. Any domain mutation increments the state revision and invalidates affected preview entries.

### 10.4 Parity acceptance
Automated test requirement:
For every deterministic test case, if a predicted candidate action is immediately committed from the same canonical state, predicted listener `HEARS/DOES_NOT_HEAR` booleans and route-cost result must equal actual committed resolution **100%**.

---

## 11. Content authoring and compile pipeline

### 11.1 Authoring format
Preferred source format: typed custom Godot `Resource` data (`.tres`) for encounter definitions and reusable archetypes, because Godot Resources provide editor-visible typed properties and version-control-friendly text serialization.

Official resource behavior checked:
- https://docs.godotengine.org/en/stable/tutorials/scripting/resources.html

A scene may provide visual geometry/bindings, but **rule data must not exist only as arbitrary Node properties discovered at runtime**.

### 11.2 Encounter definition resource
Phase-5 fields map directly to typed definitions:
- EncounterDefinition;
- AcousticNodeDefinition;
- AcousticEdgeDefinition;
- ListenerDefinition;
- SourceDefinition;
- DoorDefinition;
- BarrierRailDefinition / BarrierSlotDefinition;
- ObjectiveDefinition;
- CheckpointDefinition;
- MasteryPredicateDefinition;
- NavigationGraphDefinition;
- authored reference solution metadata.

### 11.3 World binding
Encounter scene contains a `WorldBinding` table mapping stable domain IDs to visual/interaction Nodes/paths.

Loader rejects:
- missing required binding;
- duplicate binding;
- a bound physical passage whose domain edge is absent;
- a barrier slot with no world pose/rail marker;
- listener/source/door IDs not present in EncounterDefinition.

Decorative Nodes require no domain ID.

### 11.4 Compile/validation step
Before an encounter can be marked production-ready:
1. load typed source data headlessly;
2. validate schema/ID/reference integrity;
3. run Phase-5 static validators V01–V16;
4. run technical invariants below;
5. run authored reference solution/replay if present;
6. emit a canonical manifest/hash used by runtime/save compatibility tests.

### 11.5 Additional technical invariants
Without changing the design, tooling must reject:
- duplicate IDs in any namespace where uniqueness is required;
- edge endpoint IDs that do not exist;
- door/slot references to unknown edges;
- a baseline encounter containing more than one active barrier instance;
- source/listener start nodes that do not exist;
- navigation route references to unknown nav nodes;
- a checkpoint scheduled mid-barrier move or mid-event;
- a door sound mutation lacking explicit emission phase when order matters;
- invalid threshold/strength/attenuation ranges;
- normal mature density above locked limits without exceptional flag;
- authored world binding missing a mechanically active passage;
- tied-route enumeration that exceeds tooling/readability ceiling;
- a reference save/replay built against a different content manifest without migration metadata.

### 11.6 Validator output
Errors should be machine-readable and human-readable:
- code (e.g. `V05_PERMANENT_BARRIER_DOMINANCE`);
- encounter ID;
- implicated IDs;
- severity ERROR/WARNING;
- concise explanation;
- optional counterexample/reference solution trace.

This makes content failures actionable without burying them in scene logs.

---

## 12. Snapshot, checkpoint and save model

### 12.1 Three persistence scopes
Separate:

**A. Machine-local settings**
- display mode/resolution;
- renderer/performance preferences;
- device-specific input preferences where needed.

Do not assume these should Cloud-sync across PCs/handhelds.

**B. Portable profile/settings**
- language;
- accessibility presentation preferences where portable;
- portable remaps where valid;
- campaign completion;
- unlocked encounters/remixes;
- mastery records;
- achievement shadow flags;
- demo completion metadata;
- optional onboarding-seen flags.

**C. Encounter checkpoint snapshot**
- exact domain state required to resume/restart deterministically.

Steam's current Deck/Cloud guidance recommends clouded saves but cautions against syncing device-specific graphics settings, which supports this split.

Official references checked:
- https://partner.steamgames.com/doc/features/cloud
- https://partner.steamgames.com/doc?q=How+to+enable+cloud+save+on+steam

### 12.2 Checkpoint snapshot fields
At minimum:
- save schema version;
- build/content manifest version/hash;
- encounter ID;
- canonical tick;
- player authoritative state;
- barrier rail/slot/progress/state;
- door states;
- moving-source states/progress/timers;
- every listener state/path/timers/current investigation data;
- objective/mastery state;
- locomotion cadence state;
- event sequence counter;
- explicit RNG state if any future allowed randomness exists (baseline none);
- checkpoint ID.

No animation/VFX/audio playback state is authoritative.

### 12.3 Serialization format
Use an explicit versioned save DTO rather than serializing arbitrary live Nodes/Objects.

Recommended disk format for player saves: compact JSON or a documented binary envelope containing explicit primitive fields. Content `.tres` auto-serialization is useful for authoring, but player saves need deliberate schema migration and corruption handling.

### 12.4 Atomic save
Required write strategy:
1. serialize to memory;
2. write `*.tmp`;
3. flush/close;
4. validate checksum/header if used;
5. atomically replace primary where supported;
6. retain one previous known-good generation (`*.bak`) for recovery.

On load:
- validate magic/schema/content compatibility/checksum;
- if primary fails, try backup;
- if checkpoint cannot migrate safely, preserve profile progress and restart the encounter from a valid authored checkpoint/start rather than silently inventing state.

### 12.5 Versioning
Every persisted file carries:
- `save_schema_version`;
- `game_build_version`;
- `content_manifest_hash`;
- optional `source_app_kind`: FULL / DEMO.

Migration functions are one-way, explicit and tested against committed fixtures.

---

## 13. Demo/full continuity

Steam's current demo documentation confirms demos use a separate App ID and can share Cloud storage with the full app; Valve recommends disabling achievements in demos and granting applicable achievements later from valid saved state.

Official references checked:
- https://partner.steamgames.com/doc/store/application/demos
- https://partner.steamgames.com/doc/features/cloud

### 13.1 Build flavors
Create data-driven build flavors:
- `FULL`;
- `DEMO`;
- `DEV/TEST`.

Domain mechanics are identical. Build flavor controls only:
- content manifest subset;
- menu/store CTA availability;
- Steam App ID/platform configuration;
- achievement publication behavior;
- optional demo completion flags.

No `if demo: hearing works differently` logic is allowed.

### 13.2 Demo content gating
Demo manifest contains exactly the curated D01–D04 package (or content-identical final replacements). It cannot load later encounter resources simply because they ship in shared depots.

### 13.3 Shared progress fields
Safe transferable fields:
- portable settings/accessibility;
- valid input remaps;
- `demo_completed`;
- per-demo encounter completion IDs;
- onboarding-seen flags;
- content-identical campaign completion only when the full build verifies matching encounter content version/hash.

If demo D01–D04 are remixed rather than content-identical, full game starts campaign normally and imports only settings/demo-completion metadata.

### 13.4 Achievements
Demo adapter never unlocks Steam achievements. It may record internal eligible achievement facts if needed. Full build may evaluate valid imported state and grant appropriate achievements after ownership/loading rules are satisfied.

---

## 14. Platform adapter contract

Define an interface equivalent to:
- `is_platform_available()`;
- `is_full_app_owned()`;
- `unlock_achievement(id)`;
- `query_achievement(id)`;
- `set_rich_presence(key, value)`;
- `open_full_game_store_page()`;
- `cloud_capability()` / save-path policy hooks;
- `current_input_glyph_family()` where platform integration supports it.

Domain code emits semantic events such as `EncounterCompleted`, `MasteryAchieved`, `DemoCompleted`; an achievement/profile service maps those to platform calls.

The Steam adapter can fail or be absent without corrupting local progress. Failed achievement sync is retried from shadow flags later; it never rewinds gameplay.

---

## 15. Localization architecture

### 15.1 Text keys, not source prose
All user-visible text uses stable localization IDs, not English strings as gameplay keys.

Godot supports key/value translation resources, CSV and gettext-based workflows; its documentation recommends unique identifiers as a scalable pattern and provides pseudolocalization for early layout testing.

Official references checked:
- https://docs.godotengine.org/en/stable/tutorials/assets_pipeline/importing_translations.html
- https://docs.godotengine.org/en/stable/tutorials/i18n/pseudolocalization.html

### 15.2 Domain/presentation separation
Domain state uses enums/IDs such as `LISTENER_HEARD`, `FAIL_DIRECT_DETECTION`, `V05_PERMANENT_BARRIER_DOMINANCE`. Presentation maps these to localized text/icons.

No localized string is parsed to decide a mechanic.

### 15.3 Layout tests
Implementation must support:
- text expansion/pseudolocalization;
- UI scale and handheld target together;
- right-to-left mirroring where applicable for UI controls;
- non-text mechanical icons remaining interpretable without English labels.

The title itself remains unresolved and cannot become a save/content namespace.

---

## 16. Accessibility data boundaries

Accessibility options are split into:

**Presentation-only**
- high contrast;
- background detail reduction;
- route line thickness;
- listener outline strength;
- explicit numeric bands;
- reduced motion;
- pulse style;
- HEARS/DOES_NOT_HEAR text labels;
- text/icon scale;
- preview hold/toggle/persistence;
- camera smoothing.

**Deterministic assist parameters**
- whole-simulation speed preset;
- legal interaction reach multiplier within frozen bounds;
- barrier snap generosity;
- direct-detection forgiveness duration/radius where allowed;
- checkpoint density/content selection when authored.

Presentation-only settings cannot enter Domain Core hashes except where a test explicitly verifies independence. Assist parameters that change deterministic timing/interaction geometry must be part of canonical state/replay metadata so a run can be reproduced honestly.

Acoustic strength, attenuation, thresholds, tied-route logic and mutation ordering are never changed by accessibility presentation settings.

---

## 17. Telemetry and event log

### 17.1 Local deterministic event stream
The Domain Core emits a structured event log suitable for tests and optional later analytics:
- tick;
- semantic event type;
- stable actor/object IDs;
- source event/route result IDs;
- old/new state where useful;
- reason code.

Examples:
- `PLAYER_NODE_CHANGED`;
- `BARRIER_LEFT_SLOT`;
- `BARRIER_SNAPPED`;
- `DOOR_STATE_CHANGED`;
- `SOUND_EMITTED`;
- `LISTENER_HEARD`;
- `LISTENER_DID_NOT_HEAR` for relevant prediction/test cases;
- `LISTENER_RETARGETED` / `RETARGET_REJECTED_WEAK`;
- `DIRECT_DETECTION_FAIL`;
- `OBJECTIVE_COMPLETED`;
- `CHECKPOINT_RESTORED`;
- `ENCOUNTER_COMPLETED`.

### 17.2 Product metrics hooks
If analytics are later enabled with appropriate privacy disclosure, aggregate hooks should be able to measure the empirical gates without changing play:
- passive-wait fraction;
- meaningful barrier edits/minute;
- slot usage distribution;
- failed hearing predictions (should be zero outside bugs);
- restarts;
- deliberate useful-hearing events;
- encounter completion time;
- muted/no-audio configuration usage;
- assist usage.

No telemetry is required for offline completion. Analytics implementation is not part of Domain Core.

---

## 18. Replay and deterministic hashing

### 18.1 Replay record
A replay fixture contains:
- build/content manifest hash;
- encounter ID;
- assist ruleset ID;
- initial snapshot/hash;
- per-tick semantic input packets;
- explicit restart/checkpoint commands;
- expected final hash and key event checkpoints.

### 18.2 State hash
Create a canonical serialization/order for rule-bearing state and hash it at selected ticks. Exclude:
- render interpolation;
- animation progress;
- audio playback;
- camera state;
- purely presentation accessibility state.

Include deterministic assist parameters.

### 18.3 Determinism gate
A golden replay run repeatedly on the same pinned engine/build must produce identical state hashes and event sequence. Cross-OS/CPU runs should be compared during 12A; if quantized domain math is implemented as specified, target identical hashes across Windows/Linux target builds.

If cross-platform drift appears, do not hide it by weakening preview/checkpoint contracts. Locate remaining float/engine-order authority and remove it from the domain path.

---

## 19. Headless test architecture

### 19.1 Test runner
The dedicated repository should provide a headless test entry point runnable with the pinned Godot executable. Avoid making a third-party test plugin a hard runtime dependency; a lightweight internal runner is sufficient if it can produce machine-readable pass/fail output.

### 19.2 Unit tests
Minimum domain units:
- graph edge enable/disable;
- strength/attenuation/threshold boundary cases;
- barrier +3 exactly once on one snapped edge;
- between-slot barrier = no attenuation;
- shortest cost;
- tied minimum routes;
- strong sound leakage through barrier;
- listener multi-event selection;
- strict-greater retarget rule;
- search/return timers;
- door BEFORE/AFTER snapshot semantics;
- moving source node ownership;
- player/listener node ownership boundary cases;
- direct detection predicates;
- win/fail ordering.

### 19.3 Property/fuzz tests
For randomly generated **small legal graphs**:
- compare production shortest-path solver with a slower exhaustive simple-path oracle;
- verify increasing one edge attenuation cannot decrease minimum path cost;
- verify disabling an edge cannot create a cheaper path;
- verify adding the barrier affects only its bound edge;
- verify listener hearing is exactly `remaining_intensity >= threshold`;
- verify stable ID reorder in source data does not change canonical result after compilation;
- verify prediction commit equivalence for random legal candidate actions.

Fuzz generators must stay inside locked value ranges and do not create new gameplay cases.

### 19.4 Golden tests
Commit small canonical fixtures for:
- one-route screening;
- tied alternate routes;
- threshold split;
- deliberate lure;
- barrier leakage strength 4;
- door-before and door-after emission;
- equal-strength retarget rejection;
- moving source;
- return-path inversion;
- exceptional three-listener case;
- checkpoint round trip;
- demo/full metadata import.

### 19.5 Content tests
Every encounter build runs:
- V01–V16;
- technical schema/reference validators;
- content manifest hash generation;
- reference solution playback when available;
- checkpoint restore comparison;
- preview/resolution parity on annotated critical actions.

---

## 20. Save/recovery tests

Required automated cases:
1. serialize→deserialize produces same canonical state hash;
2. checkpoint restore reproduces next-event prediction exactly;
3. corrupted primary falls back to backup;
4. unsupported future schema refuses safely without overwriting file;
5. old committed fixture migrates forward and preserves campaign progress;
6. content-manifest mismatch either migrates through an explicit rule or restarts the affected encounter safely;
7. interrupted temporary write leaves previous primary/backup recoverable;
8. demo metadata imports without falsely completing non-identical campaign encounters;
9. machine-local graphics settings are not required for portable Cloud progress.

---

## 21. Performance budgets

These are engineering targets for implementation validation, not player-facing promises.

### 21.1 Target hardware/profile
Primary baseline:
- ordinary contemporary PC;
- Steam Deck-class 1280×800 handheld readability/performance target;
- 60 Hz domain simulation;
- 60 FPS render target in normal encounters when hardware/settings support it.

### 21.2 Domain budget
Normal mature content (<=12 acoustic nodes, 2 listeners):
- full domain tick target: **<1.0 ms average, <2.0 ms p99** on target handheld-class CPU;
- one immediate acoustic prediction recompute target: **<0.25 ms average**;
- route enumeration must remain bounded by validator.

Exceptional 3-listener content:
- domain tick target remains <2.0 ms p99;
- if presentation becomes the bottleneck, reduce route VFX density before changing domain truth.

These numbers are deliberately generous for such small graphs and should expose accidental architecture overhead early.

### 21.3 Frame budget
At 60 FPS total frame budget is ~16.7 ms. The acoustic/domain logic should consume a small minority. Major likely costs are rendering/VFX/UI overdraw and asset complexity, not graph solving.

### 21.4 Preview churn
During barrier dragging, the candidate acoustic result may change frequently. Recompute only when authoritative/prospective state relevant to the prediction changes (slot candidate, door/source/listener node revision, targeted action), not on every render pixel of a drag.

### 21.5 Memory/loading
Encounters are small. Prefer loading one encounter plus nearby shared assets rather than a monolithic campaign scene. Quick restart must restore an in-memory checkpoint/domain snapshot, not reload all assets.

Perceived restart target remains about <=1 second and ideally much faster after the encounter is loaded.

---

## 22. Implementation order for the dedicated repository

This is the later **Phase 12** implementation order. No production code is created in the factory.

### 12A — Deterministic technical bootstrap
Deliver:
- pinned Godot 4.7.1 project;
- folder/module boundaries for domain/orchestrator/presentation/platform/content/tools/tests;
- fixed-step domain runner;
- stable IDs and canonical state hashing;
- typed EncounterDefinition skeleton;
- minimal graph solver;
- headless test runner;
- local save envelope + round-trip test;
- InputMap semantic command adapter skeleton;
- NullPlatformAdapter.

Exit gate: deterministic headless smoke replay produces identical hashes across repeated runs.

### 12B — Vertical slice / thesis kill prototype
Implement only enough for 3–4 representative encounters:
- player movement/node ownership;
- one local barrier rail;
- posted + investigating listener;
- footsteps + distraction + loud objective;
- tied routes;
- exact world prediction;
- direct detection/fail/restart;
- one door mutation;
- one selective-audibility climax;
- basic no-audio presentation.

Exit gate: one-week empirical gates can actually be measured. If the thesis fails, do not populate 34 encounters.

### 12C — Core systems complete
Add/finalize:
- listener patrol/return semantics;
- moving source;
- all locked mastery predicates;
- complete barrier state/rotation station handling;
- content compiler/validators;
- full accessibility rule boundaries;
- robust snapshot/version migration foundation.

### 12D — Content population
Build/validate E01–E34 + R01–R08 from typed data, maintaining reference solutions and validator signatures. Do not add one-off mechanics to rescue weak levels.

### 12E — UX / accessibility / controller / platform-facing support
Finish:
- acoustic route VFX and tied-route emphasis;
- barrier tactility;
- listener/failure explanation;
- full remapping/input glyphs;
- no-audio parity;
- reduced motion/high contrast/text scale;
- deterministic speed assists;
- handheld pass;
- localization/pseudolocalization;
- Steam adapter integration behind interfaces;
- demo build flavor.

### 12F — Adversarial QA
Automate and manually attack:
- prediction mismatch;
- save corruption/recovery;
- listener retarget exploits;
- nearest-door dominance;
- silence-everything collapse;
- brute-force content;
- restart/replay determinism;
- demo/full import;
- controller disconnect/remap edge cases;
- 3-listener readability.

### 12G — Empirical gates
Run the locked prototype/playtest gates from Phases 3–7 plus technical gates in this file. Cut exceptional content before expanding UI/system complexity if it fails.

### 12H — Release candidate
Freeze:
- final content manifest;
- save schema compatibility window;
- performance pass;
- full regression suite;
- Steam/demo packaging;
- achievement/Cloud behavior;
- release builds and checklist.

No phase may claim `IMPLEMENTATION COMPLETE = YES` until 12H acceptance passes.

---

## 23. CI / automation posture for later repository

The previous factory projects established an important operational lesson: unstable push-triggered CI can create notification spam without improving validation quality.

For Game #004's dedicated repo:
- headless tests must be easy to run locally and manually;
- initial GitHub Actions should prefer `workflow_dispatch` and/or pull-request validation once stable;
- documentation-only changes should not trigger heavyweight gameplay tests;
- do not enable broad every-push CI until the headless suite is consistently green and notification policy is documented;
- batch coherent implementation checkpoints rather than firing multiple speculative CI commits.

A dedicated `CI_NOTIFICATION_POLICY.md` remains mandatory at migration time per factory rules.

---

## 24. Empirical technical gates

These are intentionally unresolved until implementation/prototype evidence exists.

### T8-01 — Engine version gate
Before 12A bootstrap, recheck current Godot stable. Upgrade from pinned 4.7.1 only if a newer stable materially improves the project and migration risk is low.

### T8-02 — Quantized movement feel
The chosen fixed-point/quantization scale must be imperceptible in player control at desktop and controller input. If not, increase precision without returning rule authority to render-frame floats.

### T8-03 — Cross-platform replay
Golden domain replays should hash identically on target Windows/Linux builds. Any divergence must be isolated before content scale-up.

### T8-04 — Prediction latency
Barrier/action preview must update perceptually instantly during normal use. Target acoustic computation is far below one frame; if UI feels delayed, profile binding/VFX rather than weakening exact preview.

### T8-05 — Tied-route density
Real authored content must stay below the route-enumeration/readability ceiling. If legitimate content routinely creates >16 tied simple minimum paths, redesign representation/tooling before shipping hidden routes.

### T8-06 — Deterministic player collision
Custom kinematic/domain collision must feel as smooth as expected for the top-down game. If engine helpers are substituted, replay/hash gates remain mandatory.

### T8-07 — Handheld frame/readability
At 1280×800 target, two-listener mature content must sustain target performance while routes, motifs and barrier remain legible.

### T8-08 — Three-listener exceptional load
E28/E33/R expert case must pass both computational and visual readability. If not, cut/reduce that content class; do not create a global graph/listener table to rescue it.

### T8-09 — Save migration
At least two historical save schema fixtures must migrate correctly before release candidate, even if early schemas are synthetic development versions.

### T8-10 — Demo/full continuity
Shared Cloud/local import must never falsely mark non-identical campaign content complete. Test with separate demo/full App ID configuration before release.

### T8-11 — Steam-unavailable behavior
Full campaign save/progress must work when Steam APIs are absent/offline. Platform sync may retry later without blocking play.

### T8-12 — Localization stress
Pseudolocalization + maximum UI scale + handheld resolution must not obscure HEARS/DOES_NOT_HEAR outcomes or objective/restart controls.

---

## 25. Explicit technical non-goals

Do not implement for 1.0 unless a later formal design amendment changes scope:
- realistic wave/ray acoustic simulation;
- per-material acoustic physics outside the locked integer schema;
- microphone input;
- multiplayer synchronization/rollback;
- procedural level generation requirement;
- combat AI framework;
- dynamic destructible architecture;
- inventory/crafting backend;
- remote graph editor;
- multiple freely controlled barriers;
- generic behavior-tree AI platform;
- runtime mod/Workshop API;
- global leaderboard backend;
- server account system;
- title/lore systems built around `HUSHLINE` before name clearance.

---

## 26. Contradiction audit

Phase 8 introduces no gameplay contradiction.

Key reconciliations:
- Phase-4 fixed-step order becomes one explicit domain runner rather than relying on SceneTree callback order.
- Exact prediction uses prospective cloned domain state and the same solver as resolution.
- Tied minimum routes remain all mechanically represented; implementation enumerates bounded simple minimum routes rather than silently selecting one.
- Barrier between slots remains acoustically inactive; scene overlap never becomes authority.
- Listener navigation is deterministic and authored, preserving short predictable investigation/search/return behavior.
- Whole-simulation speed assists scale the domain clock consistently and do not change acoustic logic.
- Complete no-audio parity remains presentation architecture over identical domain truth.
- Demo/full builds share mechanics and differ only in data/platform gating.
- Steam Cloud is an adapter/persistence concern, not gameplay authority.
- Engine Resources are used for typed content authoring, while player saves use explicit versioned DTOs rather than arbitrary Node serialization.
- `HUSHLINE` is not used as a persistent namespace because final title is unresolved.

No frozen Phase-3–7 rule was changed to simplify implementation.

---

## 27. Phase-8 acceptance audit

Phase 8 is complete because:
- current engine/runtime direction is verified and pinned to Godot 4.7.1-stable for initial implementation;
- Domain Core / orchestrator / presentation / platform boundaries are explicit;
- fixed-step 60 Hz simulation and deterministic ordering are explicit;
- stable IDs, canonical integer/fixed-point state and state hashing are defined;
- acoustic graph solve, tied-route representation and propagation result contracts are defined;
- listener/player navigation authority is separated from engine/render timing;
- barrier, door, moving-source and listener implementation contracts preserve Phase-4 rules;
- prediction clones prospective state and reuses exact committed code;
- typed content Resource + world-binding + headless compile/validator pipeline is defined;
- Phase-5 validators are carried into tooling with additional reference-integrity checks;
- versioned snapshot/checkpoint/profile/settings scopes are defined with atomic recovery and backup behavior;
- demo/full build flavors and continuity fields are defined without gameplay divergence;
- Steam achievements/Cloud/store CTA are isolated behind adapters;
- localization/accessibility boundaries prevent presentation state from becoming gameplay authority;
- deterministic event logs, replay fixtures, state hashes, unit/property/golden/content tests are specified;
- performance targets cover normal <=12-node/2-listener and exceptional 3-listener content;
- later implementation order 12A–12H is explicit without production code;
- technical empirical gates are documented instead of being solved by adding mechanics.

**PHASE 8 TECHNICAL IMPLEMENTATION SPECIFICATION = COMPLETE.**

## NEXT DESIGN HANDOFF
Proceed to **Phase 9 — Whole-Game Simulation on Paper**. Create `GAME4_WHOLE_GAME_SIMULATION.md`. Walk the frozen product through first boot, D01–D04 demo, early campaign, first deliberate hearing, first selective-audibility split, midgame door/sequence logic, moving-source introduction, mature return-path inversion, exceptional three-listener content, final E34 synthesis, restart/checkpoint/save/demo-full continuity, accessibility/no-audio/simulation-speed paths, mastery/remixes and hostile player behavior. Attack contradictions between mechanics, content, UX, commercial packaging and technical contracts. Repair contradictions explicitly but do not casually add mechanics.