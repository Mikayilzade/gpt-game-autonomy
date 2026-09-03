# GAME #016 — PHASE 8 TECHNICAL IMPLEMENTATION SPECIFICATION

Date: 2026-09-03
Status: PHASE 8 COMPLETE
Working title: **ONE-WAY WORKSHOP**
Authority: all prior active Game #016 files, especially `GAME16_MECHANICS.md`, `GAME16_CONTENT.md`, `GAME16_UX.md`, and `GAME16_COMMERCIAL.md`.

## 0. Purpose
This file converts the frozen product/design into a buildable deterministic technical contract for a future dedicated implementation repository. It does **not** begin production implementation inside the factory.

The implementation must preserve one rule above all others:

> **Puzzle truth is a finite deterministic model. Scene graphs, meshes, animation, sound, frame rate, physics, and platform APIs may present that truth but may never define or mutate it implicitly.**

---

# 1. Engine / runtime direction

## 1.1 Frozen engine direction
**Use Godot 4.7 stable, GDScript-first, desktop PC/Steam-first.**

If implementation begins after a newer stable Godot 4.x release exists, upgrading is allowed only after a clean deterministic-core test run and an explicit compatibility note in the dedicated repo. Do not track development/master builds for production.

Why Godot 4.7 fits this product:
- the game is a bounded single-scene 3D tabletop, not a streaming/open-world problem;
- controller and Linux/Steam Deck support are required and Godot 4.x has current SDL3-backed controller support on desktop platforms;
- data-driven authored jobs map cleanly to Resources/JSON-like data and deterministic script logic;
- the project benefits from fast iteration, low licensing complexity, and a lightweight small-team toolchain;
- no product requirement depends on engine-specific high-end rendering, networking, real-time physics correctness, or a massive commercial middleware ecosystem.

Use C# only if a measured implementation bottleneck or tooling need justifies it later; do not introduce a mixed-language architecture by default.

## 1.2 Steam integration boundary
Use the Steamworks SDK through a thin platform adapter in the dedicated repo. The game logic must run without Steam present for local tests.

Platform adapter responsibilities only:
- achievements;
- Steam Input action/glyph integration where used;
- Steam Cloud file transfer/integration;
- app/demo identity checks;
- optional overlay hooks.

The adapter must not own campaign truth, unlock logic, attempts, or job validation.

## 1.3 Rendering mode
Use standard forward/mobile-compatible 3D rendering suitable for low-end PC and Steam Deck. The visual target is stylized tabletop readability, not photorealism.

No gameplay requirement may depend on:
- real-time rigid-body settling;
- physically simulated saw/drill trajectories;
- collision tolerance as a success rule;
- shader timing;
- animation state machine timing.

---

# 2. Architectural layers

The dedicated implementation must separate at least these conceptual layers:

1. **Domain / Puzzle Core** — pure deterministic state transitions, validation, certifier, dead-state reachability, unlock evaluation.
2. **Content Data** — 24 canonical jobs + D1, capability definitions, cut sockets, operations, hints, localization keys, authoring metadata.
3. **Application / Session** — current job attempt, command dispatch, save checkpoints, restart/certify flow, profile progression.
4. **Presentation** — Godot scenes, meshes, animations, VFX, audio, camera, focus graph, UI, Trace View.
5. **Platform** — Steam achievements, Steam Cloud, demo/full discovery, controller glyph origin, filesystem paths.
6. **Tooling / Validation** — offline content validator, exhaustive/finite search tools, golden traces, schema migration tests.

Dependencies point inward. Presentation and platform call application/domain services; the domain never queries scene nodes, frame time, controller devices, or Steam APIs.

---

# 3. Stable identifiers and canonical data model

All persistent and trace-relevant identifiers are stable strings, never engine instance IDs or array positions.

Recommended naming:
- jobs: `OW01`…`OW24`, demo capstone `D1`;
- root stocks: `S1`, `S2`, `S3` inside a job;
- cut sockets: job-local stable IDs such as `S1_CUT_A`;
- operations: `OP_DRILL_1`, etc.;
- jig stations: `JIG_SPACER_A`;
- part slots: `PART_RAIL`;
- requirements: `REQ_BRACE_ANGLE_A`;
- profile ID: opaque UUID generated once;
- attempt ID: opaque UUID per restart/new attempt.

## 3.1 `JobDefinition`
Conceptual schema:

```text
JobDefinition {
  schema_version
  job_id
  title_key
  reasoning_family
  root_stocks[]
  cut_socket_defs[]
  jig_station_defs[]
  operation_defs[]
  part_slot_defs[]
  certification_requirements[]
  prerequisite_job_ids[]
  hint_set
  presentation_refs
  validator_metadata
  solution_family_signatures[]   // optional, only for recognized alternate-family achievements
}
```

`JobDefinition` is immutable at runtime.

## 3.2 `WorkpieceState`

```text
WorkpieceState {
  piece_id
  root_stock_id
  lineage_path
  geometry_token
  capabilities[]
  witnesses[]
  availability_state
  part_slot_id?
  jig_station_id?
  generation
}
```

`piece_id` is deterministic within an attempt and derived from lineage, not random. Example: `OW14:S1/L/R`.

## 3.3 `CutSocketDefinition`

```text
CutSocketDefinition {
  socket_id
  allowed_geometry_token
  family                  // STRAIGHT | DIAGONAL
  visible_anchor_ref
  child_left_geometry
  child_right_geometry
  child_capability_rules
  prerequisite_predicate?
  jig_station_requirement?
  presentation_ref
}
```

## 3.4 `JigStationDefinition`

```text
JigStationDefinition {
  station_id
  requirement_predicate
  occupancy_mode          // TEMPORARY | CONSUME_ON_OPERATION
  enabled_operation_ids[]
  required_orientation?
  presentation_ref
}
```

## 3.5 `OperationDefinition`

```text
OperationDefinition {
  operation_id
  family                  // GUIDED_DRILL | GUIDED_MARK | GUIDED_SPACING | GUIDED_DIAGONAL | ASSEMBLE
  target_predicate
  jig_station_id?
  prerequisite_witnesses[]
  deterministic_effect
  jig_resolution          // RELEASE | CONSUME | NONE
  target_resolution       // STAYS_LOOSE | PART_DOCKED | LOCKED
  irreversible
  presentation_ref
}
```

## 3.6 `PartSlotDefinition`

```text
PartSlotDefinition {
  slot_id
  acceptance_predicate
  required_witnesses[]
  reversible_before_certification
  presentation_ref
}
```

## 3.7 Requirement expression
Baseline final certification remains AND-composition only.

Supported leaf predicates:
- `PART_PRESENT(slot_id)`
- `WITNESS_PRESENT(slot_id, witness_type, parameter)`
- `PAIR_RELATION(slot_a, slot_b, token)` where physically visible
- `JIG_RELEASED(station_id)`
- `OPERATION_DONE(operation_id)`

No arbitrary script callback may define hidden job truth.

---

# 4. Authoritative runtime state ownership

## 4.1 `AttemptState`
Only the domain-owned `AttemptState` is authoritative during a job.

```text
AttemptState {
  runtime_schema_version
  job_id
  attempt_id
  commit_index
  workpieces_by_id
  jig_occupancy_by_station
  part_occupancy_by_slot
  completed_operations
  certification_state
  trace_events[]
  dead_state_evidence?
}
```

Presentation objects are projections of this state. They may cache transforms/animations but may never become the only source of availability, witness, lineage, station occupancy, operation completion, or certification truth.

## 4.2 `CampaignProfile`

```text
CampaignProfile {
  profile_schema_version
  profile_id
  cleared_jobs: set<job_id>
  demo_capstone_seen
  tutorial_flags
  revealed_hints_by_job
  accessibility_settings
  control_preferences
  achievement_reconciliation_flags
  import_receipts[]
  last_played_job?
  profile_revision
}
```

Unlock state is **derived**, not stored as authority.

## 4.3 Separation of settings
Split settings into:
- portable gameplay/accessibility/input preferences;
- machine-local graphics/display/audio-device preferences.

Machine-local display resolution, monitor choice, renderer fallback, and similar device-specific graphics settings are not part of the cloud-merged profile.

---

# 5. Deterministic command and event model

All puzzle mutations occur through semantic commands processed serially.

Core command set:
- `CommitCut(piece_id, socket_id)`
- `DockJig(piece_id, station_id)`
- `UndockJig(station_id)`
- `DockPart(piece_id, slot_id)`
- `UndockPart(slot_id)` where reversible
- `CommitOperation(operation_id, target_piece_id)`
- `Certify()`
- `RestartAttempt()`

Inspection, camera, hover, Trace View and preview commands do not mutate puzzle truth.

## 5.1 Atomic cut transaction
A cut transaction must execute as one domain transaction:
1. validate command against current state;
2. derive two children and deterministic IDs;
3. create a new immutable/cloneable state result;
4. mark parent spent;
5. update occupancy if a cut prerequisite jig resolves;
6. append one semantic trace event;
7. recompute reachable actions/dead-state evidence;
8. emit a domain event packet for presentation;
9. persist only after the transaction is fully committed.

No save may contain “parent already removed but children not created”.

## 5.2 Guided-operation transaction
Equivalent rule:
1. validate target, witnesses and station/jig;
2. calculate exact effect;
3. atomically add witness/effect;
4. release/consume jig as defined;
5. update target role if defined;
6. append trace event;
7. recompute dead-state evidence;
8. persist completed transaction.

## 5.3 Event ordering
Within one command, the domain uses fixed explicit ordering. Presentation receives the resulting event list only after truth is complete.

Animation callbacks may signal **presentation completion** only. They never authorize the actual cut, witness grant, consumption, unlock, achievement or save.

If an animation is skipped, reduced-motion mode is enabled, the window loses focus, or FPS drops, the final puzzle state is identical.

---

# 6. Deterministic lineage / trace contract

A child identity is derived from parent lineage and branch label:
- root `S1`;
- first cut children `S1/L`, `S1/R`;
- cutting `S1/R` produces `S1/R/L`, `S1/R/R`.

A trace event contains stable semantic data, not scene references:

```text
TraceEvent {
  trace_schema_version
  ordinal
  event_type
  job_id
  attempt_id
  input_piece_ids[]
  output_piece_ids[]
  operation_or_socket_id?
  station_id?
  witness_delta[]
  availability_delta[]
  requirement_snapshot_hash
}
```

The implementation should be able to replay a golden trace into an initial job state and obtain the exact same canonical state hash.

Canonical state hashing excludes presentation-only fields and timestamps.

---

# 7. Preview contracts

Preview is pure calculation.

`PreviewCut(piece_id, socket_id)` returns:
- both exact child geometry tokens;
- base capabilities/witness inheritance;
- current visible compatible stations/part slots;
- any required jig/prerequisite for that cut.

It must not:
- mutate state;
- run future branch search and label a cut good/bad;
- expose hidden solution-family data;
- change hint timers;
- create trace events.

Operation preview similarly returns exact immediate witness/consumption/release effects only.

---

# 8. Certifier contract

`Certify(AttemptState, JobDefinition)` evaluates final requirements in stable authored order.

Result:

```text
CertificationResult {
  success
  requirement_results[]
  first_failed_requirement_id?
  local_failure_reason?
  causal_trace_anchor_ids[]
}
```

The runtime certifier never compares against an intended move sequence.

A case succeeds if and only if its frozen predicates are satisfied, regardless of which validated solution family produced the state.

For `Another Way`, separately calculate a coarse validator-recognized **solution-family signature** from semantic ancestry/resource allocation facts defined in job metadata. The achievement system must never compare raw exact move strings or require a minimum move count.

---

# 9. Dead-state detector

The dead-state detector must satisfy the Phase-4 requirement:

> **Zero false positives.** It may miss some dead states, but it must never label a reachable/live state dead.

## 9.1 Runtime detector
Use optimistic reachability over each current eligible piece:
- enumerate remaining authored cuts/operations reachable from its current geometry/witness state;
- ignore competition between separate future resource uses;
- allow compatible temporary resources optimistically where doing so cannot make reachability smaller;
- compute a superset of capabilities/witnesses the remaining state could still produce;
- mark a requirement impossible only when no optimistic producer exists.

Competition-based death that needs exact global search may remain undetected at runtime.

## 9.2 Authoring validator
Offline validation is stricter. For each canonical job, perform exhaustive finite-state search where feasible under frozen ceilings (<=3 roots, <=6 committed operations, <=8 loose children, <=5 cut sockets/current piece).

Validator outputs:
- at least one certifying state exists;
- all content IDs/predicates resolve;
- no state transition creates duplicate occupancy/impossible identity;
- known authored solution families certify;
- runtime dead-state detector has **no false positives** against exhaustive ground truth;
- hint/certifier referenced requirement IDs exist;
- progression and achievement metadata are valid.

False negatives from runtime detector are counted for tuning but are not correctness failures.

---

# 10. Content loading, schema versioning and validation

## 10.1 Authoritative content format
Use externalized data assets loaded into typed runtime definitions. Recommended approach:
- Godot Resource or JSON-like source data for individual jobs;
- a generated/validated manifest listing all canonical jobs and D1;
- schema validation before packaging.

Do not hand-code case logic inside scene scripts.

## 10.2 Versions
Maintain separately:
- `content_schema_version` — structure of job definitions;
- `campaign_content_version` — shipped content revision;
- `profile_schema_version` — profile/save format;
- `attempt_schema_version` — in-progress attempt state;
- `trace_schema_version` — semantic trace format.

A content patch may change presentation, text or validated data, but must not silently reinterpret an old in-progress attempt. If a patch changes a job's logical data incompatibly, mark that job definition with a new content revision and either migrate the attempt explicitly or discard only that attempt with a clear recovery message while preserving campaign clears.

## 10.3 Package-time gate
Release builds fail validation if:
- any of OW01–OW24 or D1 is missing;
- a stable ID collides;
- a referenced geometry/station/operation/part/requirement is missing;
- a job exceeds a hard scope ceiling;
- a canonical job has zero known certifying states;
- runtime detector produces any false-positive dead state in exhaustive fixtures;
- required hint/localization keys are missing;
- prerequisite graph is cyclic or differs from Phase 7.

---

# 11. Exact campaign unlock evaluator

Unlocks are a pure function of `cleared_jobs`.

Rules:
- if no clears: only `OW01` unlocked;
- `OW01` clear => `OW02`, `OW03` unlocked;
- `OW02 OR OW03` clear => `OW04` unlocked;
- `OW04` clear => `OW05` unlocked;
- later trays use exact chain:
  - A clear => B and C;
  - B AND C clear => D;
  - D clear => next tray A.

Concrete later graph:
`OW05 -> {OW06,OW07} -> OW08 -> OW09 -> {OW10,OW11} -> OW12 -> OW13 -> {OW14,OW15} -> OW16 -> OW17 -> {OW18,OW19} -> OW20 -> OW21 -> {OW22,OW23} -> OW24`.

Important import consequence: a recorded clear does not imply its upstream prerequisite became cleared. An imported `OW05` clear is preserved but only affects downstream unlocks when `OW05` is actually reachable through the retail prerequisite chain.

Implementation strategy: compute `reachable_unlocked` iteratively from start using cleared prerequisite predicates rather than unioning downstream edges from every clear flag blindly.

Campaign complete iff `OW24` is cleared; because reaching OW24 requires every prior tray gate, normal retail progression implies all 24 clears. A profile integrity checker may also assert all 24 flags when granting final completion achievement.

---

# 12. Local persistence

## 12.1 File classes
Use separate files/concepts:
- `profile.json` (or compact binary equivalent with inspectable development representation): monotonic campaign progress, tutorial, hints, portable accessibility/control preferences, import receipts;
- `attempt.json`: current in-progress retail attempt only;
- `settings_local.json`: device-local graphics/audio-display details not cloud-merged;
- `profile_backup_<n>` rotating small backups;
- optional `attempt_backup` for crash recovery.

The demo uses a separate demo save root/package namespace and its own `demo_profile` file.

## 12.2 Atomic save procedure
For every persisted domain commit:
1. serialize to temp file;
2. write schema/version/checksum;
3. flush/close;
4. read back or validate checksum where practical;
5. atomically replace destination on supported filesystem;
6. retain last known-good rotating backup.

Never save during the middle of a cut/operation animation because presentation timing is irrelevant to truth.

Stable attempt save points:
- initial attempt creation;
- after every irreversible fabrication commit;
- after reversible docking only if needed for convenience, but these saves are not required for correctness;
- after successful certification/profile clear;
- after explicit safe exit/pause transition.

If the process crashes after domain commit but before presentation completes, load the committed result and present the bench in its post-commit stable state.

## 12.3 Corruption recovery
On load:
1. verify schema and checksum;
2. validate stable IDs against installed content revision;
3. if primary profile invalid, try newest valid profile backup;
4. never destroy a valid older profile until replacement is confirmed;
5. if attempt invalid but profile valid, discard/restart only the attempt;
6. if profile recovery fails entirely, offer explicit recovery/new-profile path and preserve unreadable files for support rather than overwriting immediately.

---

# 13. Save migrations

Migrations are explicit one-way functions:

`profile_vN -> profile_vN+1`

Rules:
- migration starts from a verified backup;
- every migration is idempotent or guarded by resulting version;
- cleared job flags may never be silently dropped;
- unknown future fields are ignored/preserved where format supports it;
- failed migration leaves the old save intact;
- attempt migration may be stricter than profile migration because attempts depend on exact content revision.

Tests must include fixtures from every shipped profile schema version after launch.

---

# 14. Demo discovery and import

## 14.1 Discovery
Retail startup uses a platform/filesystem adapter to locate a compatible demo profile from the expected demo namespace for the same platform/account context.

Detection is read-only until the player chooses Import.

A missing, incompatible or corrupt demo file never blocks retail boot.

## 14.2 Import receipt
Each compatible demo profile has stable `profile_id` + relevant content/schema version. Retail stores an import receipt such as:

```text
ImportReceipt {
  demo_profile_id
  imported_demo_revision
  merged_clear_flags_hash
  imported_at_profile_revision
}
```

Repeated import of the same unchanged demo produces no new state change.

## 14.3 Exact merge
Demo-to-retail clear mapping:
- demo OW01 => retail OW01 clear;
- demo OW03 => retail OW03 clear;
- demo OW05 => retail OW05 clear record;
- D1 => `demo_capstone_seen=true` only;
- tutorial flags => OR;
- settings => explicit player choice;
- in-progress demo attempt => never imported;
- demo achievements => none.

After merge:
1. write pre-import retail backup;
2. apply monotonic OR merge;
3. recompute retail unlocks from the retail graph;
4. reconcile achievement eligibility idempotently;
5. write new retail profile atomically;
6. retain pre-import backup until at least one later successful retail save.

## 14.4 `Start fresh` and `Decide later`
`Start fresh` dismisses the current detection without deleting demo data. The product may expose a later `Import Demo Progress` option until an import receipt exists or the player explicitly disables future prompting.

`Decide later` leaves import available and should not prompt every boot aggressively; use a persistent menu affordance plus bounded reminder policy.

---

# 15. Retail-first / cloud-conflict merge

Steam Cloud is transport/storage, not the authority that understands game semantics.

## 15.1 Clouded files
Cloud-sync:
- retail `profile` and its safe small backup(s);
- portable accessibility/control preferences if stored separately but merge-safe.

Do **not** cloud-merge arbitrary simultaneous in-progress attempts. The simplest baseline is either:
- keep `attempt` local-only; or
- cloud it as a single opaque file with explicit newest/conflict recovery and never semantic-merge two attempts.

Recommended baseline: **cloud the profile, keep active attempt local by default**. Losing an unfinished job on another machine is preferable to corrupting irreversible branch truth. Revisit only if cross-device attempt continuation proves important in testing.

Do not cloud machine-specific graphics resolution/display settings.

## 15.2 Monotonic profile merge
When two valid profile versions differ:
- `cleared_jobs` = set union;
- tutorial flags = OR;
- revealed hints = union / maximum reveal level per job;
- `demo_capstone_seen` = OR;
- import receipts = union by receipt identity;
- achievement reconciliation flags = OR;
- portable settings use a deterministic last-user-edit policy only when edit metadata is trustworthy; otherwise prefer local and show conflict choice for materially different accessibility/control settings.

Never choose a profile solely because its file timestamp is newer if that would discard clear flags.

## 15.3 Profile revision
Every successful profile mutation increments `profile_revision` and stores an optional logical edit counter/hash. Use this for diagnostics, not as a substitute for set-union semantics.

## 15.4 Cloud conflict recovery
Before accepting an externally synchronized profile:
1. parse/validate both local and incoming versions;
2. create local backup;
3. compute merge preview;
4. if merge is monotonic and unambiguous, merge automatically;
5. if settings/conflicting schema require user decision, preserve both and present `Use local settings / Use cloud settings` while still unioning monotonic progress;
6. never overwrite the only valid profile with a corrupt incoming file.

---

# 16. Achievements reconciliation

Achievements are consequences of profile/current validated state, never the authority for progress.

On retail profile load/import/cloud merge:
1. evaluate all 12 achievement predicates from profile + supported state facts;
2. query platform adapter for already-granted achievements when available;
3. grant missing eligible achievements;
4. record local reconciliation flag only after platform success or maintain retryable pending state;
5. repeated reconciliation is safe.

Demo grants none.

Milestone achievement eligibility from imported clears is allowed only when the corresponding retail state is loaded/reached per Phase 7. Do not use the platform's achievement state to unlock cases.

`Another Way` requires persistent recognized solution-family signatures for OW16 or OW20, e.g. per job a set of validator-defined family tokens witnessed on completed clears.

`Trace the Work` stores one boolean after the player opens a complete cleared-case causal recap OW09+ through all commit nodes.

---

# 17. Input abstraction and controller glyphs

## 17.1 Internal action map
The application consumes semantic actions only, matching Phase 6:
- Navigate Focus
- Select / Pick Up
- Cancel / Put Back
- Inspect
- Toggle Requirement Overlay
- Cycle Compatible Targets
- Rotate Piece Left / Right
- Zoom In / Out
- Camera Orbit / Pan
- Preview Cut
- Confirm Commit
- Restart Job
- Certify
- Pause

Godot input mappings and Steam Input action sets map devices to these actions.

## 17.2 Focus graph
Focus graph nodes are semantic object IDs. Presentation derives visible/focusable node instances each frame/state change, but adjacency is generated from stable logical relations, not animated screen position.

Automated UX tests should be able to drive every campaign command using semantic focus/action events without a mouse cursor.

## 17.3 Glyph contract
UI requests glyphs by semantic action from `InputGlyphService`.

Priority:
1. Steam Input origin glyph when Steam Input is active;
2. detected controller-family glyph set;
3. keyboard/mouse glyph/text fallback.

Changing active device must update prompts without resetting focus or action state.

---

# 18. Accessibility persistence

Persist portable accessibility values in profile or a merge-safe portable settings object, including at minimum:
- text/UI scale;
- reduced motion;
- camera easing;
- auto-frame;
- commit confirmation mode / hold duration;
- Persistent Guidance;
- Hints always available;
- overlay density;
- compatible-target emphasis;
- control remaps where platform representation permits safe portability;
- audio/visual cue accessibility preferences.

Persist device-local values separately:
- resolution/window mode;
- monitor;
- render scale/quality preset;
- output audio device.

Accessibility use never changes puzzle truth, clear labels, or achievement eligibility.

---

# 19. Presentation separation from truth

## 19.1 Projection model
After each domain transaction, presentation receives a stable `PresentationSnapshot` or events describing:
- pieces and roles;
- current dock/slot occupancy;
- witnesses/capabilities;
- requirement state;
- trace deltas;
- certification/dead-state result.

Meshes/scene nodes are recreated or repaired from this projection if needed.

## 19.2 Animation rule
For a cut:
1. domain transaction completes;
2. durable save checkpoint completes or is queued safely from completed truth;
3. presentation animates blade/split from old visual pose to new state;
4. callback only releases player input / starts optional next presentation beat.

If animation is skipped, children appear directly in their canonical post-cut presentation sockets.

## 19.3 Physics
Use collision/raycasting for selection and visual contact as convenient. Do not use rigid-body simulation to decide whether a jig fits, a part satisfies a slot, or a cut succeeds.

All docking uses authored snap transforms keyed by stable IDs.

---

# 20. Localization boundaries

Every player-visible string uses a localization key. Job data stores IDs and localization keys, not English prose as logic.

Externalize:
- job titles;
- requirement labels/reasons;
- station/capability names;
- tutorial prompts;
- all H1/H2/H3 hints;
- dead-state/certifier messages;
- menu/settings/accessibility strings;
- achievement title/description text;
- demo import/cloud recovery copy.

Never parse localized text to drive logic.

Layout assumptions:
- support at least ~35–50% text expansion for common European localization;
- avoid fixed-width button labels where wrapping/auto-size is reasonable;
- support CJK glyph/font fallback architecture;
- support Cyrillic;
- do not encode DIAGONAL A/B, PASS/FAIL or state purely with Latin letters/colors; physical icons/patterns remain canonical visual redundancy.

Launch localization list remains a commercial/budget decision; architecture must not require code redesign for FIGS, Brazilian Portuguese, Russian, Simplified Chinese, Japanese or Korean.

---

# 21. Performance / memory / load budgets

These are design budgets for future implementation validation, not claims that optimization is already done.

Target hardware floor: low-end contemporary PC and Steam Deck-class hardware at 1280×800.

## 21.1 Runtime target
- gameplay target: stable 60 FPS at 1280×800 on Steam Deck default quality where practical;
- acceptable fallback: locked stable 40 FPS only if visual polish needs it and no interaction/puzzle correctness changes;
- domain command processing: typically <5 ms; hard authoring gate <16 ms for ordinary commands on target CPU excluding presentation;
- runtime dead-state optimistic check: target <10 ms after a commit; if a rare job exceeds 25 ms, optimize/cache without weakening correctness contract;
- no frame-rate-dependent logic.

## 21.2 Memory
Target total working-set design budget: **<=1.5 GB RAM** on Deck/low-end PC in normal gameplay, with a preferred substantially lower actual footprint.

One job need only load:
- one workbench scene;
- its stock/child geometry kit;
- reusable station kit;
- UI/audio/shared assets;
- current job data.

Do not preload the entire 24-case 3D asset set if unnecessary.

## 21.3 Loads
Targets:
- cold boot to title/first playable flow: <=10 s on SSD-class target;
- case restart: <1 s logical reset and target <1.5 s until interactive;
- case-to-case transition: target <=3 s;
- save operation should not create visible hitch >50 ms; asynchronous file I/O may be used after immutable state snapshotting, but completion ordering must remain crash-safe.

## 21.4 Geometry/render ceilings
Because correctness uses discrete tokens, visual scenes should remain simple:
- reusable low/moderate-poly stock meshes;
- <=8 loose children visible plus docked parts/stations;
- no large particle systems, expensive GI dependency, cloth, destructible physics, or high-cost postprocessing needed for readability.

---

# 22. Test hooks and deterministic fixtures

## 22.1 Domain API testability
The future repo must support headless/domain-only tests capable of:
- load job;
- list legal commands;
- apply semantic command;
- inspect canonical state;
- certify;
- run dead-state detector;
- serialize/deserialize state;
- compute canonical state hash;
- replay trace.

No Godot scene rendering should be required for most puzzle correctness tests.

## 22.2 Golden job tests
Every canonical job + D1 gets:
- schema/load test;
- at least one golden valid trace;
- expected certification success;
- at least one known invalid/dead branch where appropriate;
- expected dead-state detector behavior;
- scope ceiling assertion;
- stable solution-family signature tests where used;
- hint and requirement key resolution.

OW16/OW20 require at least two recognized valid family fixtures.

OW24 requires multiple hostile serialization/replay checkpoints across its full six-commit path.

## 22.3 Deterministic replay tests
For a trace:
- same initial job + same semantic events => same final canonical state hash across repeated runs;
- serialize/load between any two commits => same eventual hash;
- presentation frame timing does not appear in trace or affect result.

## 22.4 Dead-state oracle tests
For tractable exhaustive job state spaces:
- enumerate reachable states;
- classify whether any certifying continuation exists;
- compare runtime detector;
- assert `runtime_dead => oracle_dead` for every state.

This is the zero-false-positive release gate.

---

# 23. Hostile persistence/import/cloud tests

Required automated/manual fixture classes:

1. crash after domain cut commit before animation completes;
2. crash while temp save file is being written;
3. corrupted primary profile with valid backup;
4. corrupted attempt with valid profile;
5. old profile schema migration;
6. content revision changed while an old attempt exists;
7. demo profile complete, retail empty;
8. demo complete, retail partially progressed;
9. repeated identical demo import;
10. demo corrupt/incompatible;
11. retail local has clears A, cloud has disjoint clears B => union A∪B;
12. cloud profile newer timestamp but fewer clears => no regression;
13. local/cloud settings disagree => progress union preserved while settings choice is explicit/deterministic;
14. corrupt cloud incoming file => valid local retained;
15. achievement API unavailable during eligible state => retry later without duplicate side effects;
16. Steam unavailable/offline => local progress fully functional;
17. active attempt on machine A and unrelated profile progress on B => profile merge does not semantic-merge attempt branches;
18. Reset Campaign Progress is explicit/local intent and must not be accidentally reversed/duplicated by stale cloud data without confirmation/recovery strategy.

For #18, campaign reset should create a new profile/reset generation token rather than merely clearing bits in-place; cloud merger must recognize deliberate reset as a destructive user action requiring explicit conflict semantics. It must never silently resurrect old clears or silently erase newer progress.

---

# 24. Hints implementation contract

Hint availability is application/session metadata, not puzzle truth.

Per uncleared case track:
- elapsed active reasoning time since first fabrication commit in current attempt;
- restart count while case remains uncleared;
- highest hint level revealed.

Availability:
- after 3 active minutes from first fabrication commit OR 2 restarts;
- immediate if `Hints always available`.

Pause/menu/background time does not advance the 3-minute timer.

Revealed hints persist for the profile and are not revoked on restart. Using hints has zero effect on certification/achievements.

Hints contain localization keys only and are validated so every case has H1/H2/H3.

---

# 25. Trace View implementation contract

Trace View is generated from semantic trace + current/historical workpiece state.

It may answer:
- parent/child ancestry;
- which committed operation added a witness;
- where a consumed/spent producer branch ended;
- which currently available piece already satisfies an inspected requirement;
- the player's own completed winning sequence after clear.

It may not expose:
- uncommitted future producing cuts;
- solver-ranked current actions;
- exhaustive future route;
- hidden canonical solution.

Late-case display budget remains <=6 commit/event nodes and 3 root lanes in the primary view, with irrelevant ancestry collapsible.

---

# 26. Demo vs retail package boundary

Demo and retail share:
- domain/core code;
- common content schema;
- shared geometry/station kit;
- common save/import compatibility library;
- common input/accessibility architecture.

Demo content manifest exposes only OW01, OW03, OW05 and D1.

Retail must not assume demo AppID/package exists. Demo must not contain hidden retail progression as unlockable content.

Keep profile namespaces distinct so demo cannot accidentally overwrite retail save files.

---

# 27. Security / tamper posture

This is a single-player puzzle game; anti-cheat is unnecessary.

However saves must be robust against malformed/tampered input:
- validate schema/types/bounds before loading;
- reject unknown job IDs from active attempt;
- recompute unlocks rather than trusting stored unlocked arrays;
- recompute achievements from valid progress;
- never execute scripts/code from content/save data.

Player-edited local saves may grant themselves clears; this is not a product threat worth invasive DRM. Protect correctness and corruption recovery, not leaderboard integrity that does not exist.

---

# 28. Future dedicated-repo implementation order

No production code is written here. The future dedicated repository should implement in this order:

## 12A — Bootstrap / deterministic core
1. Godot 4.7 project shell + CI/headless test path.
2. Typed IDs, capability/witness predicates, immutable job definitions.
3. `AttemptState`, command processor, cut transaction, operation transaction.
4. state hash / trace replay.
5. certifier + optimistic dead-state detector.
6. content loader/validator with one tiny fixture.

Exit gate: headless golden trace deterministically certifies without any 3D presentation.

## 12B — Vertical slice
Build **OW01** end-to-end:
- bounded bench scene;
- one root stock;
- visible cut preview/commit;
- child split presentation;
- spacer station;
- guided operation;
- part dock/certification;
- restart;
- mouse + controller semantic focus path;
- local attempt/profile save.

Exit gate: cold playable OW01 proves direct socket manipulation and restart/certifier loop.

## 12C — Core systems complete
Add remaining frozen capability grammar:
- SPAN/EDGE/FACE/PAIR;
- HOLE/MARK/SPACING/ANGLE;
- temporary/consuming jigs;
- cross-stock lineage;
- derived witness qualification;
- Trace View;
- hints/dead-state diagnostics.

## 12D — Authoring / validator
Before bulk content:
- full job schema tooling;
- exhaustive finite-state validator;
- golden trace fixtures;
- scope ceiling lints;
- solution-family signatures;
- localization/hint key validation.

Prove OW16/OW20 alternate families and OW24 ceiling in data before final content polish.

## 12E — Persistence / platform
- versioned profile + attempt save;
- backups/migrations;
- demo discovery/import;
- profile monotonic cloud merge;
- achievement adapter/reconciliation;
- Steam Input/glyph adapter;
- machine-local vs portable settings separation.

## 12F — Full content
Author/finalize OW01–OW24 + D1 through the validator, not ad hoc scene scripts.

## 12G — UX / accessibility / target-device
- full controller path;
- 1280×800 Deck readability;
- focus graph tests;
- text scaling;
- reduced motion;
- commit alternatives;
- localization stress layouts.

## 12H — Adversarial QA / empirical gates / release candidate
- hostile persistence/import/cloud tests;
- zero false-positive dead-state oracle pass;
- performance budgets;
- demo→retail transfer on clean and existing profiles;
- controller/Deck cold play;
- playtest empirical gates from Phases 3/6/7;
- packaging and regression.

Do not reorder full content population ahead of the validator/persistence foundations in a way that creates 24 brittle scene-coded cases.

---

# 29. Implementation-flexible details
These may be decided by the dedicated implementation session without reopening design, provided frozen behavior remains unchanged:
- exact Godot node hierarchy;
- exact Resource vs JSON source representation;
- ECS/object-oriented/internal functional coding style;
- file extension / text vs compact binary save encoding;
- exact visual tween library/animation organization;
- exact Steamworks wrapper library;
- editor tooling UI;
- shader/material specifics;
- internal naming conventions not exposed in saved/content IDs.

These are **not** flexible:
- deterministic domain ownership;
- stable semantic IDs/lineage;
- transaction ordering;
- state-based certifier;
- zero-false-positive dead-state rule;
- exact campaign unlock graph;
- demo merge semantics;
- monotonic progress cloud merge;
- no semantic merge of competing in-progress attempts;
- frame-rate/physics independence of correctness;
- capability/content ceilings and frozen puzzle truth.

---

# 30. Phase-8 acceptance checklist
Phase 8 is complete when the following are fully specified:

- engine/runtime direction: **YES**;
- domain vs presentation/platform separation: **YES**;
- Job/Workpiece/Cut/Jig/Operation/Part/Requirement schemas: **YES**;
- deterministic atomic mutation/event ordering: **YES**;
- stable IDs/lineage/trace replay: **YES**;
- certifier/dead-state contracts: **YES**;
- 24 jobs + D1 loading/version/validator gate: **YES**;
- exact campaign unlock evaluator: **YES**;
- profile/attempt persistence/crash recovery/migrations: **YES**;
- demo discovery/import/idempotency: **YES**;
- cloud file boundaries and monotonic merge: **YES**;
- achievement reconciliation: **YES**;
- input/focus/glyph abstraction: **YES**;
- accessibility persistence: **YES**;
- rendering/animation separation from truth: **YES**;
- localization boundaries: **YES**;
- Deck/low-end budgets: **YES**;
- headless/golden/oracle/hostile tests: **YES**;
- future implementation order: **YES**.

No production implementation has been started.

## Phase-8 conclusion
**PHASE 8 TECHNICAL IMPLEMENTATION SPECIFICATION COMPLETE.**

The game is now technically specified enough that a fresh implementation session can build the frozen systems without inventing state ownership, save/import semantics, event ordering, validation rules, unlock logic or platform boundaries.

NEXT: **Phase 9 — Whole-Game Simulation on Paper.** Run the full product through first boot, demo, import, early campaign, midgame, late game, replay/alternate solution, hints, dead lineage, controller/Deck, persistence/cloud conflict, crash recovery, and hostile/unusual behavior. Repair contradictions in existing authority files rather than adding new mechanics.