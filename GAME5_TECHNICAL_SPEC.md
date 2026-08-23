# GAME #005 — TECHNICAL IMPLEMENTATION SPECIFICATION

Last updated: 2026-08-23
Factory run: **10 — extended pass**
Phase: **8 — Technical Implementation Specification**
Selected concept: **G5C02 — Tension Budget**
Commercial title: **TBD**
Production implementation: **NOT STARTED**

# PHASE 8 STATUS = COMPLETE

This file maps the frozen product/mechanics/content/UX/commercial canon into an implementation-ready technical architecture. It does **not** start production code inside the factory.

---

# 1. Engine / runtime direction

## 1.1 Selected baseline

**Godot 4.7.2-stable, GDScript-first, 3D project.**

Rationale:
- the game is a compact offline single-player 3D/isometric puzzle with deterministic authored state, not a simulation requiring a large custom engine;
- Godot supports Windows/Linux exports, controller input, localization/pseudolocalization and headless execution suitable for validators/tests;
- the project benefits from text-friendly scenes/resources and a small codebase another autonomous implementation session can reason about;
- gameplay does not require proprietary middleware, networking or high-end rendering features;
- 4.7.2 is the current stable maintenance release as of 2026-08-23; 4.8 is still development and is not the baseline.

Official references checked on 2026-08-23:
- Godot release archive: https://godotengine.org/download/archive/
- Godot 4.7.2 stable: https://godotengine.org/download/archive/4.7.2-stable/
- controller/gamepad docs: https://docs.godotengine.org/en/4.7/tutorials/inputs/controllers_gamepads_joysticks.html
- pseudolocalization docs: https://docs.godotengine.org/en/4.7/tutorials/i18n/pseudolocalization.html

## 1.2 Version policy

- bootstrap pins exact engine version in project documentation and CI tooling;
- maintenance upgrade inside 4.7.x may occur only after automated validation + representative scene regression;
- do not migrate to 4.8/dev merely because it exists;
- engine upgrade is an implementation decision only when it preserves frozen behavior.

## 1.3 Rendering direction

- authored stylized 3D scenes;
- elevated perspective camera;
- simple materials, restrained transparency and limited dynamic-light complexity;
- renderer choice may be Forward+ or a lighter renderer after target-device profiling, but visual effects may not become gameplay authority;
- all state-critical readability must survive effects being reduced.

---

# 2. Technical north star

Gameplay truth lives in a **small deterministic Domain Core**. Godot scene nodes present and animate that truth; they do not invent it.

The same authored definition + command sequence must always produce the same:
- revision;
- committed anchor band;
- SLACK/TAUT/HIGH load state;
- traversal permissions;
- objective/checkpoint state;
- completion state.

Rope visuals, animation interpolation, camera, audio, haptics and particles are presentation adapters only.

---

# 3. High-level project boundaries

Recommended dedicated-repo shape:

```text
project.godot
/src
  /domain
    rig_state.gd
    rig_reducer.gd
    rig_rules.gd
    checkpoint_snapshot.gd
    progression_state.gd
  /content
    encounter_definition.gd
    rig_revision_definition.gd
    load_definition.gd
    traversal_definition.gd
    content_registry.gd
  /validation
    encounter_validator.gd
    campaign_validator.gd
    signature_validator.gd
    reachability_solver.gd
  /runtime
    encounter_controller.gd
    input_router.gd
    save_service.gd
    progression_service.gd
    settings_service.gd
  /presentation
    rig_presenter.gd
    load_presenter.gd
    carriage_presenter.gd
    camera_director.gd
    feedback_director.gd
  /ui
  /tests
/content/encounters
/content/demo
/scenes
/localization
```

Exact filenames are implementation-flexible. Boundary responsibilities are not.

---

# 4. Data model

## 4.1 EncounterDefinition

One immutable definition per encounter version:

```text
EncounterDefinition
  definition_version
  encounter_id
  progression_band
  primary_signature
  secondary_signatures[]
  intended_first_solve_minutes
  budget_B
  snap_count
  initial_anchor_band
  rail_definition
  load_definitions[]
  revision_A
  optional revision_B
  objective_definition
  region_definitions[]
  traversal_edges[]
  checkpoints[]
  intended_solution_commits[]
  accepted_alternate_solution_signatures[]
  demo_eligible
  validation_tags[]
```

Preferred serialized format: typed custom `Resource` stored as text `.tres`, or another text-diffable Godot-native representation. Binary-only content definitions are discouraged.

## 4.2 LoadDefinition

```text
LoadDefinition
  load_id
  archetype: LIFT | GATE | SPAN
  stable_pose_SLACK
  stable_pose_TAUT
  stable_pose_HIGH
  transition_path
  traversal_semantics
  safety_volume_metadata
  visual_motif_id
```

The definition never stores a dynamic physics result as canonical state.

## 4.3 RigRevisionDefinition

```text
RigRevisionDefinition
  revision_id
  active_load_ids[]
  distribution_by_snap[snap_count][active_load_count]
```

Each distribution entry is integer 0/1/2 internally and maps exactly to SLACK/TAUT/HIGH.

## 4.4 Traversal definition

Authoring representation:
- `RegionDefinition` — stable semantic region IDs;
- `TraversalEdgeDefinition` — from/to region plus condition expression tied only to stable load/revision/objective state;
- no frame timing conditions;
- no hidden random conditions.

World navigation remains ordinary 3D movement. The region graph exists for validation, restart safety and automated reasoning.

---

# 5. Runtime authoritative state

Use a serializable value object equivalent to:

```text
EncounterRuntimeState
  state_schema_version
  encounter_id
  encounter_definition_version
  rig_phase
  revision_id
  committed_anchor_band
  player_region_id
  objective_state
  checkpoint_id
  completion_state
  transition_epoch
```

Derived, not independently persisted:
- active load IDs;
- load quanta;
- SLACK/TAUT/HIGH labels;
- stable traversal edges;
- visual target poses.

They are reconstructed from definition + runtime state.

`transition_epoch` monotonically changes on each commit/mutation/restart and prevents stale animation callbacks from committing old transitions after a restart.

---

# 6. Commands, reducer and events

## 6.1 Commands

Domain commands are explicit intents, for example:
- `BeginAnchorGrab`
- `CancelAnchorGrab`
- `CommitAnchorBand(target_band)`
- `ActivateObjective`
- `PlayerEnteredRegion(region_id)`
- `RequestRestart`
- `RequestExit`

Raw device input never edits rig state directly.

## 6.2 Reducer

`RigReducer.apply(state, command, definition) -> TransitionPlan`

A TransitionPlan contains:
- new authoritative state or pending state;
- old/new derived load bands;
- ordered domain events;
- presentation targets;
- collision/traversal update obligations;
- checkpoint obligations;
- validation errors if command is illegal.

The reducer must be deterministic and testable without rendering.

## 6.3 Domain events

Representative events:
- `AnchorGrabStarted`
- `AnchorCommitAccepted`
- `CableBandChanging`
- `LoadTransitionRequested`
- `StableRigReached`
- `ObjectiveActivated`
- `RigRevisionChanged`
- `CheckpointPromoted`
- `RestartBegan`
- `RestartCompleted`
- `EncounterCompleted`

Events carry semantic IDs, not scene-node references.

---

# 7. Exact update / event ordering

## 7.1 Normal frame ordering

1. Collect input into abstract actions.
2. Runtime controller maps legal action to domain command.
3. Domain reducer validates command against stable authoritative state.
4. Reducer emits TransitionPlan with new/pending state and ordered semantic events.
5. Runtime stores authoritative transition state and increments `transition_epoch`.
6. Presentation adapters animate carriage/cables/loads toward requested poses.
7. Collision/traversal adapter follows frozen per-archetype transition contract.
8. Presenter reports completion tagged with current `transition_epoch`.
9. Runtime ignores stale completion tags.
10. When all required adapters complete, reducer/runtime finalizes STABLE state.
11. Stable traversal graph is recomputed from canonical state.
12. Completion/checkpoint predicates are evaluated only after stable authority exists.

No `delta` accumulation decides puzzle truth.

## 7.2 Preview ordering

Preview is intentionally outside authoritative simulation:
- player enters `GRABBED_PREVIEW` presentation mode;
- current committed band remains collision/traversal authority;
- rail position can move continuously;
- nearest prospective band is resolved deterministically;
- presenters may show target posture/ghost cues for that prospective band;
- no region/traversal edge becomes legal from preview;
- cancel restores the original committed presentation;
- release emits exactly one `CommitAnchorBand` command.

## 7.3 Commit ordering

1. resolve nearest legal snap;
2. same-band release becomes no-op stable return;
3. safety precondition check;
4. commit semantic anchor band;
5. derive vector from current revision;
6. cable/hardware causal cue begins;
7. loads animate according to archetype;
8. gate/span permissions obey stable-state rules;
9. lift rider is carried kinematically if legal;
10. all transition adapters settle;
11. STABLE becomes authoritative;
12. traversal/exit/objective checks run.

## 7.4 Objective mutation ordering

1. objective command legal only in STABLE;
2. enter MUTATING, lock carriage/objective interaction;
3. show physical add/remove event;
4. switch revision A -> B while physical anchor band identity remains unchanged;
5. resolve revision-B vector at the same band;
6. increment transition epoch;
7. run normal cable -> load transition sequence;
8. verify stable, safe world;
9. promote C1 snapshot;
10. return control.

---

# 8. Load implementation contracts

## 8.1 Shared rule

Loads are deterministic kinematic state machines with exactly three stable poses. They may use animation curves for feel but may not use uncontrolled rigid-body/rope physics to decide final position.

## 8.2 Lift

- stable semantic dock = LOW/MID/HIGH derived 1:1 from SLACK/TAUT/HIGH;
- platform collision remains solid;
- rider is carried through deterministic parent/velocity transfer or equivalent tested method;
- legal landing traversal activates only at stable authored docks;
- transition swept volume is validator-approved and non-crushing.

## 8.3 Gate

- stable clearance = 0/1/2;
- passage conditions query stable clearance tier;
- closing prevents new entry into the unsafe swept zone before movement can trap the player;
- no partial-gap traversal;
- no frame-perfect crossing solutions.

## 8.4 Span

- only TAUT stable state supplies its traversal edge;
- preview/interpolation never creates collision authority;
- SLACK/HIGH entrance geometry communicates invalid route;
- baseline authoring forbids legal carriage commit while player occupies a span that will change.

---

# 9. Player movement / interaction architecture

- CharacterBody-style deterministic ordinary locomotion is appropriate; exact Godot node choice is implementation-flexible.
- no jump/dash/crouch/combat state machine;
- input actions: `move_left/right/up/down` or vector equivalent, `interact`, `cancel`, `restart`, `pause`, optional `rig_focus`;
- controller and keyboard/mouse feed the same action abstraction;
- carriage movement projects movement input onto the authored rail axis;
- strong snap attraction and hysteresis prevent flicker between adjacent bands;
- accessibility remapping changes input bindings, not domain commands.

No main encounter may access device-specific input directly.

---

# 10. Checkpoint reconstruction and restart

## 10.1 Canonical checkpoint snapshot

A checkpoint stores semantic state only:

```text
CheckpointSnapshot
  encounter_id
  definition_version
  checkpoint_id: C0 | C1
  revision_id
  committed_anchor_band
  objective_state
  safe_player_spawn_id
```

Do not persist:
- current tween percentage;
- cable bone transforms;
- physics velocities;
- temporary preview location;
- camera interpolation;
- audio state.

## 10.2 Restart algorithm

1. invalidate all active transition epochs;
2. block gameplay input;
3. clear preview/transient presentation state;
4. load immutable encounter definition;
5. recreate canonical runtime state from checkpoint snapshot;
6. derive active loads/distribution/traversal graph;
7. hard-set world to stable poses/collisions;
8. place player at authored safe spawn;
9. run anti-softlock assertion;
10. return STABLE/input.

Repeated restart from the same checkpoint must be idempotent.

## 10.3 App quit / resume

The baseline does not promise exact mid-transition resume.

If the player quits during an encounter, next launch resumes at latest durable C0/C1 checkpoint. This is intentional and deterministic.

---

# 11. Profile persistence and progression

## 11.1 Save domains

Separate:
- `ProfileSave` — campaign progress, completion records, unlock state, achievements metadata where appropriate;
- `CurrentRunSave` — current encounter ID + latest C0/C1 snapshot;
- `SettingsSave` — controls/accessibility/audio/video/localization preferences.

## 11.2 Profile schema

```text
ProfileSave
  schema_version
  content_version
  completed_encounter_ids[]
  unlocked_encounter_ids[]
  discovered_alternate_solution_flags[]
  optional_remix_unlocks[]
  last_selected_encounter_id
```

No gameplay currency or upgrade inventory exists.

## 11.3 Atomicity

- write to temporary file then replace/rename;
- maintain one previous known-good backup if platform/filesystem permits;
- validate schema before replacing current save;
- corrupted CurrentRunSave falls back to encounter C0, never deletes campaign completion;
- corrupted optional metadata must not invalidate the profile if recoverable.

## 11.4 Versioning

Every save includes explicit schema version and content version.

Migration policy:
- additive compatible fields get defaults;
- renamed fields use deterministic migration functions;
- unsupported future save versions fail safely with user-readable message and preserved file;
- encounter definition changes that invalidate a saved C1 checkpoint may fall back to C0 for that encounter, while preserving completed campaign progress.

---

# 12. Progression graph

The campaign remains mostly guided.

Technical baseline:
- Band A linear;
- later content may expose small 2–3 encounter branches;
- unlock rules are explicit data, not inferred from scene filenames;
- synthesis encounters can require completion of named prerequisite IDs;
- completed encounters stay replayable;
- demo has a separate progression registry and cannot accidentally unlock retail campaign state unless product design later intentionally imports completion.

A simple `ProgressionDefinition` should declare prerequisites and next nodes.

---

# 13. Data-driven authoring pipeline

## 13.1 Authoring flow

1. Designer creates/edits EncounterDefinition.
2. Static validator runs in editor or command line.
3. State-space validator enumerates every legal revision/band distribution.
4. Traversal solver enumerates reachable `(revision, band, player_region, objective)` states from C0/C1.
5. Intended solution is checked against actual graph.
6. Alternate solutions are reported, not automatically treated as defects.
7. Campaign signature validator compares structural signature to other encounters.
8. Only validator-clean content can enter a release candidate; explicit reviewed waivers must be documented, not silently ignored.

## 13.2 Content compilation

At export time, content may remain Resources or be compiled into a registry. Runtime must resolve encounter IDs through one canonical registry and reject duplicate IDs.

---

# 14. Validators V01–V18 as implementation contracts

All Phase-5 validators are executable obligations.

### V01 Budget conservation
Enumerate every revision/band; exact integer sum equals `B`.

### V02 Band bounds
Every quantum in `{0,1,2}`.

### V03 Adjacent transfer
For adjacent rail bands, vector delta contains exactly one `+1`, one `-1`, all other zero.

### V04 No duplicate bands
Unique vector per snap within a revision.

### V05 World-state distinction
Automated layer verifies distinct semantic poses/motif IDs; visual QA confirms distinction at target camera scale.

### V06 Load contract
Archetype data uses exactly canonical semantic mapping.

### V07 No transition-timing dependency
Traversal solver uses only stable states; reduced-motion/snap-complete simulation yields same solution graph.

### V08 Safe swept volume
Static safety metadata + representative runtime tests ensure legal commits cannot crush/trap.

### V09 Reachability / anti-softlock
Graph search from every reachable canonical state proves restart exists and required intended path remains viable; unreachable authored states are reported.

### V10 Post-mutation conservation
Same `B`, snap count and physical band identity across revisions.

### V11 Mature decision separation
Solver verifies intended solution contains qualifying separating event between required meaningful commits.

### V12 Safe static enumeration rejection
Compute whether all completion-critical choices can be previewed from one permanently safe anchor-access state before a separating event. Flag invalid mature definition.

### V13 Permanent best band
Search for a band that satisfies every completion-critical phase/region state without later reconfiguration.

### V14 Signature duplicate
Create normalized structural fingerprint from load multiset, snap count, mutation mode, primary signature, meaningful commit count, separating-event sequence and revision structure. Near-match threshold is a human-review flag, not an automatic gameplay kill.

### V15 Theme-only novelty
Campaign review combines V14 fingerprint with authored reasoning metadata and adjacency.

### V16 Placement ceiling
Intended completion-critical commits <=4.

### V17 Mutation ceiling
At most one completion-relevant irreversible mutation.

### V18 Archetype ceiling
Only Lift/Gate/Span in 1.0 main campaign.

## 14.1 Required preflight feasibility check

Before individual validators, the tool must verify that each revision actually has enough **distinct conserved distribution states connected by legal adjacent one-quantum transfers** to support its declared snap count.

This is mathematically implied by V01/V03/V04 but deserves a first-class diagnostic so impossible content fails with a useful message instead of a confusing cascade. Phase 9/10 must audit the existing skeleton against this constraint before final freeze.

---

# 15. Traversal / solution solver

Use a finite graph over semantic states, not world-space brute-force physics.

Conceptual node:

`SolverNode = (revision, anchor_band, player_region, objective_state)`

Edges:
- ordinary region traversal if current stable conditional edge is open;
- legal carriage commit if anchor is accessible from current region;
- objective mutation if trigger is accessible and stable;
- exit completion if conditions met.

Solver outputs:
- existence of path from C0 to win;
- shortest meaningful-commit count;
- whether C1 is reachable/valid;
- softlock states;
- permanent-best-band candidates;
- static-enumeration pattern;
- alternate solution signatures.

The solver does **not** replace human fun review.

---

# 16. Automated test architecture

## 16.1 Domain tests

Headless tests for:
- all legal/illegal FSM transitions;
- preview never mutates authority;
- same-band no-op;
- distribution derivation;
- commit idempotency where applicable;
- mutation ordering;
- transition epoch stale-callback rejection;
- C0/C1 reconstruction;
- repeated restart idempotency;
- save migration functions.

## 16.2 Property / exhaustive tests

Because domains are tiny, enumerate rather than sample where practical:
- all vectors for 2–4 loads and legal budgets;
- adjacency deltas;
- all bands/revisions in every shipped encounter;
- every reachable solver state;
- all checkpoint restore paths.

## 16.3 Presentation integration tests

Representative scenes assert:
- Lift carries rider safely;
- Gate cannot crush/precision-squeeze;
- Span transient never becomes legal route;
- reduced-motion and normal-motion reach identical stable state/collision;
- mute mode does not remove visual truth;
- optional labels do not change simulation.

## 16.4 Golden encounter tests

Keep tiny canonical fixtures:
- two-load give/take;
- three-load TAUT compromise;
- traversal-separated two-commit state;
- mutation + C1 + return inversion;
- invalid duplicate-band fixture;
- invalid budget fixture;
- invalid static-enumeration fixture.

---

# 17. Input / accessibility abstraction

`InputRouter` exposes semantic actions only.

Required device parity tests:
- keyboard-only path;
- common XInput/SDL-style controller path;
- controller disconnect/reconnect while paused or stable;
- remapped interaction/restart;
- no encounter-specific hardcoded key checks.

Settings are data-driven and persisted separately.

Reduced-motion implementation must alter only presentation durations/camera flourish; the domain reducer and traversal graph remain identical.

Optional SLACK/TAUT/HIGH labels query derived semantic state and must never query internal numeric budget for display.

---

# 18. Localization readiness

- all user-facing strings use stable localization keys from first implementation;
- no important text baked into textures;
- world labels that are purely decorative can remain nonsemantic, but objective/help/settings strings are localizable;
- use Godot localization resources/gettext-compatible pipeline as chosen by implementation;
- pseudolocalization is part of Phase 12E QA;
- UI supports text expansion and right-to-left-safe layout where practical, even if launch language list is decided later;
- gameplay itself remains readable with minimal text.

---

# 19. Performance assumptions / budgets

The game uses compact authored scenes and deterministic kinematic machinery; there is no justification for heavy simulation cost.

Release-intent targets to validate empirically:
- **60 fps target** on supported PC and handheld-class target hardware at appropriate resolution/settings;
- frame budget ~16.67 ms;
- Domain Core + traversal bookkeeping should remain comfortably sub-millisecond in representative encounters because state spaces are tiny;
- no authoritative rope solver, crowd simulation, combat AI or procedural world generation;
- active gameplay loads normally <=4;
- gameplay cables are bounded and authored;
- avoid per-frame allocation in hot gameplay paths where trivial to prevent;
- camera/visual effects expose scalable quality settings;
- memory budget should remain modest; stream/unload encounter scenes rather than keeping entire campaign resident.

Performance gates are measured in implementation; exact minimum PC specification is not frozen in design.

---

# 20. Logging / diagnostics

Development builds should support a toggled diagnostics overlay/log containing:
- encounter ID / definition version;
- revision;
- committed band;
- derived semantic load states;
- current region ID;
- checkpoint;
- validator status;
- last domain command/event sequence.

Internal quanta may appear in developer diagnostics only.

Release normal play never exposes them as required solution UI.

---

# 21. Error containment

If invalid content somehow reaches runtime:
- fail encounter load early with explicit development error;
- do not guess/correct malformed distributions silently;
- retail builds should route to safe fallback/menu and preserve save;
- never write corrupted canonical state to profile because a scene node reported an impossible transform.

Save and runtime errors must not mutate completed campaign progress destructively.

---

# 22. CI / notification-safe validation direction

Dedicated implementation repo should favor:
- fast deterministic domain/validator tests on code/content changes;
- headless representative scene tests on relevant paths;
- manual or PR-gated heavier export/device checks until stable;
- docs-only changes should not trigger expensive workflows;
- no test-email notification mechanism.

A dedicated `CI_NOTIFICATION_POLICY.md` is created at migration/freeze handoff, not here.

---

# 23. Implementation sequence — dedicated repo Phase 12

## 12A — Technical bootstrap
Deliver:
- Godot 4.7.2 project;
- Domain Core state/reducer/enums;
- EncounterDefinition/registry;
- V01–V18 + preflight feasibility skeleton;
- solver foundation;
- input abstraction;
- C0/C1 persistence skeleton;
- headless test command.

Exit: deterministic fixtures pass without requiring polished art.

## 12B — Vertical slice / empirical prototype
Build three deliberately small grayboxes:
1. give/take teaching;
2. TAUT/traversal-separated mature state;
3. mutation/return-inversion state.

Use real controller path and representative cable/load readability.

## 12G-early — mandatory empirical readability/tactility gate
Before bulk content production:
- roughly 8–12 unfamiliar testers if practical;
- >=~75% median post-teaching consequence prediction target;
- most can explain give/take without numbers/graph;
- carriage move roughly <=2–3 s once reached;
- full socket enumeration not dominant in mature fixture;
- no realistic rope simulation required for belief/readability.

**FAIL blocks 12C/12D bulk expansion.** Repair must remain bounded; feature inflation is prohibited.

## 12C — Core systems complete
- all three load adapters;
- mutation/revision;
- traversal regions;
- checkpoint/restart;
- progression/save;
- preview/commit;
- camera/feedback baseline;
- validation tooling mature enough for authorship.

## 12D — Content population
- build campaign from validator-clean data;
- maintain systemic fingerprint review;
- cut near-duplicates instead of inventing mechanics;
- demo definitions share same domain/contracts.

## 12E — UX/accessibility/controller/localization
- full remapping/settings;
- reduced-motion parity;
- muted parity;
- optional state labels;
- pseudolocalization;
- target-device readability.

## 12F — Adversarial QA
- save corruption/recovery;
- restart spam/idempotency;
- stale transition callbacks;
- controller disconnect;
- invalid content rejection;
- alternate solutions;
- softlocks;
- performance regression.

## 12G-final — empirical confirmation
Re-run empirical gates on representative polished demo/campaign slices and verify earlier fixes did not regress readability/tactility.

## 12H — Release candidate
- exports/package;
- Steam demo/full build separation;
- final performance/device regression;
- store/release checklist;
- release-save migration tests.

---

# 24. Phase 8 acceptance checklist

- [x] Current stable engine/runtime direction selected and justified.
- [x] Domain Core separated from presentation.
- [x] Exact conceptual data objects defined.
- [x] Command/reducer/event architecture defined.
- [x] Preview/commit/mutation/checkpoint ordering defined.
- [x] Load runtime contracts mapped from Phase 4.
- [x] Persistence/versioning/recovery defined.
- [x] Campaign progression representation defined.
- [x] V01–V18 mapped to implementation contracts.
- [x] State-space/traversal solver defined.
- [x] Input/controller/accessibility abstraction defined.
- [x] Localization readiness defined.
- [x] Performance assumptions defined.
- [x] Automated tests and diagnostics defined.
- [x] Phase 12A–12H implementation order defined.
- [x] Empirical gate moved before bulk content without changing its criteria.
- [x] Production implementation remains outside factory.

# PHASE 8 DECISION

**PHASE 8 TECHNICAL IMPLEMENTATION SPECIFICATION = COMPLETE.**

The specification is technically coherent enough to simulate the whole game on paper. Phase 9 must now walk the complete user/runtime lifecycle and explicitly audit the authored campaign against the finite distribution-state constraints, including any contradiction between snap count, active-load count, fixed budget and mutation revisions.