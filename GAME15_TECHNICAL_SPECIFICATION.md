# GAME #015 — PHASE 8 TECHNICAL IMPLEMENTATION SPECIFICATION

Date: 2026-09-03
Status: PHASE 8 COMPLETE
Working title: **FRESH COAT**
Design complete: NO

## 0. Authority and intent
This file freezes implementation contracts for the already-designed game. It does **not** begin production implementation and may not reopen Product Thesis, Mechanical Architecture, Content Architecture, UX, or Commercial Model by convenience.

Authoritative gameplay truth remains semantic and deterministic. The renderer, physics engine, particle system, camera, animation, shaders and Steam APIs are presentation/platform clients of that truth, never its source.

Fresh platform/engine research was checked on 2026-09-03. Godot 4.7.2 is the current stable Godot 4 release (2026-08-18); 4.8 is still development. Steam Deck compatibility guidance still requires a controller-complete default path and at least playable 30 fps at 800p. Steamworks still supports demo/full shared cloud storage, recommends disabling demo achievements and granting them after import into the full game, and supports Dynamic Cloud Sync for suspend/resume scenarios. GodotSteam's former GitHub repository was archived in July 2026 and moved upstream elsewhere, so this specification deliberately isolates Steam behind an adapter instead of making gameplay depend on one community binding.

Research evidence, not game canon:
- https://godotengine.org/download/archive/
- https://godotengine.org/download/archive/4.7.2-stable/
- https://partner.steamgames.com/doc/steamhardware/compat
- https://partner.steamgames.com/doc/features/cloud
- https://partner.steamgames.com/doc/store/application/demos
- https://github.com/GodotSteam/GodotSteam

---

## 1. Runtime direction

### 1.1 Engine baseline
Freeze the initial dedicated-repository implementation target as **Godot 4.7.x stable, standard build, GDScript-first**.

Rationale:
- the game is a small deterministic 3D scene with discrete transforms, modest UI and no need for high-end proprietary engine systems;
- Godot supplies desktop/Windows/Linux export, controller/input mapping, 3D rendering, localization/UI and lightweight project structure without license/runtime-fee dependency;
- GDScript minimizes toolchain burden for a small codebase whose difficult work is data correctness/certification rather than CPU-heavy simulation;
- exact puzzle truth will be stored as precomputed data, so engine floating-point physics is not needed for correctness.

Do not adopt a development/preview engine branch for the baseline. A later stable 4.x maintenance upgrade is allowed only after regression tests pass.

### 1.2 Engine-agnostic boundary
The following modules are conceptually portable and must not depend on SceneTree/node identity:
- authored case schema;
- certified exposure tables;
- arrangement legality records;
- coat-history transition rules;
- target validation;
- progression state;
- save migration/merge rules;
- certifier outputs and golden fixtures.

Godot-specific code should primarily host rendering, input, scenes, animation, platform bridge and file I/O adapters.

### 1.3 Steam integration boundary
Define a `PlatformServices` interface with capabilities rather than direct calls from gameplay:
- `cloud_available`
- `request_cloud_sync()`
- `achievement_unlock(id)`
- `achievement_is_unlocked(id)`
- `input_glyph(action, device)`
- `rich_presence_set(key,value)` optional
- `is_demo_build`
- `platform_user_scope_id` if safely available/needed

The concrete Steamworks binding is chosen during dedicated-repo bootstrap from a currently maintained Godot 4-compatible integration. The game must also run with a local/null adapter for development and non-Steam testing. Community plugin disappearance must never break puzzle-state code.

---

## 2. Authority layers and immutable data flow

Technical authority order inside a build:
1. **Authored source data** — human-edited case/object/socket/region/target definitions.
2. **Certification output** — generated exposure truth, legal-state tables, solution/equivalence/repetition metadata and source hashes.
3. **Runtime immutable case package** — only certified data allowed into a shipping build.
4. **Runtime mutable puzzle state** — current arrangement, stage, coat histories, undo/checkpoint branch.
5. **Save/profile state** — serialized mutable puzzle/progression/settings data with schema version.
6. **Renderer/UI** — a view of layers 3–5 only.

The renderer may not raycast to decide whether a semantic region is painted. Physics nodes may not decide whether a pose is legal. Runtime uses certified IDs/tables.

Every certified case package contains:
- `case_schema_version`
- stable `case_id`
- source-content hash
- certifier-version ID
- object/region/socket IDs
- per-stage legal arrangements represented by stable arrangement IDs
- exact exposure bitsets/ID sets for each legal arrangement and booth stage
- legal A->B transition adjacency where applicable
- targets
- symmetry/equivalence metadata needed at runtime only if player-facing alternate-solution recognition requires it
- debug provenance stripped or gated from release build as appropriate.

A shipping case whose source hash does not match its certified output fails build validation.

---

## 3. Geometry and exposure-precompute contract

### 3.1 Geometry role
Authored geometry exists to derive semantic truth offline and to render the same shapes at runtime. Geometry uses a constrained orthogonal vocabulary with integer/rational-grid coordinates wherever practical.

Each atomic region is a polygon or union of coplanar polygons with:
- stable region ID;
- exact plane/normal;
- exact local polygon boundary;
- owner object;
- rendered material-slot mapping.

### 3.2 Exposure precompute
For every legal arrangement and stage direction, the certifier computes exact orthographic visibility of every atomic region under the Mechanical Architecture definition.

Required procedure conceptually:
1. transform all participating solids/region polygons into exact stage-world coordinates;
2. project along the fixed booth axis into an exact 2D plane;
3. compute coverage of the candidate atomic region by blocker solids ahead of it along the ray direction;
4. classify the entire atomic region as `EXPOSED` only if no positive-area subset is blocked;
5. classify as `OCCLUDED` only if the full positive-area region is blocked;
6. if both blocked and exposed positive-area subsets exist, return `PARTIAL_INVALID`, never a percentage;
7. author must subdivide the semantic region along a stable blocker boundary or remove the offending pose; recertify.

No shipping data may contain `PARTIAL_INVALID`.

### 3.3 Exactness strategy
The certifier should prefer exact integer/rational polygon operations or an equivalent robust constructive representation. Floating-point meshes may be used for rendering, but exposure certification must not rely on raster pixels, antialiasing, GPU depth buffers, screen resolution, shadow maps or epsilon-tuned renderer visibility.

If the implementation uses a geometry library whose internal arithmetic is floating point, it must produce canonical snapped outputs on the authored grid and pass adversarial near-contact tests. Any ambiguous classification is build-failing, not rounded into gameplay truth.

### 3.4 Renderer-vs-truth divergence guard
For every arrangement included in golden validation:
- runtime semantic truth comes from the certified exposure set;
- an automated debug render produces object/region ID buffers from canonical cameras/directions;
- test tooling compares coarse expected visibility/occlusion presentation against semantic truth to detect gross art/mesh drift;
- divergence does **not** change truth: it fails asset/content QA.

Examples that must fail QA:
- renderer visibly shows a gap while certified region is fully occluded;
- decorative mesh protrusion hides a region although gameplay geometry says exposed;
- LOD changes silhouette enough to contradict masking;
- material transparency makes an occluder look non-solid.

Shipping collision/render meshes that participate visually in masking must therefore remain derived from or tightly locked to certified gameplay solids.

---

## 4. Authoring and certifier architecture

### 4.1 Pipeline separation
Use two explicit workflows:
- **Authoring source**: human-readable data + constrained geometry.
- **Certification build step**: deterministic tool reads source, rejects invalid content, emits immutable runtime package and report.

No level is hand-approved around a failing certifier.

### 4.2 Enumeration
For each stage:
- enumerate all object->socket/pose assignments allowed by authored domains;
- reject duplicate occupancy, compatibility, collision/contact and containment violations;
- canonicalize harmless symmetries to arrangement classes;
- assign deterministic stable arrangement IDs based on canonical normalized content, not enumeration order.

For two-stage cases:
- enumerate legal A arrangements;
- enumerate legal B arrangements;
- compute allowed transitions under the rearrangement contract;
- enumerate `(A_class,B_class)` solution paths only through legal transition edges.

### 4.3 Applying coats in the solver
A-stage exposure set appends A to exactly those region histories.
B-stage exposure set appends B to exactly those histories.
Targets then evaluate exact histories. No renderer invocation is part of solving.

### 4.4 Symmetry/equivalence
Symmetry metadata may declare:
- object permutations for identical geometry+targets;
- socket mirror/rotation automorphisms;
- orientation symmetries with identical exposure consequence;
- harmless parking positions.

Canonicalization must be tested against two failure modes:
1. over-collapse: two states that differ in a target-relevant future transition are incorrectly merged;
2. under-collapse: mirror/identity duplicates inflate solution count and apparent difficulty.

Two arrangements may be equivalent at stage A only if they have identical current exposure consequences **and** identical equivalence of reachable target-relevant B transition classes when B exists. Current exposure alone is insufficient for cross-stage canonicalization.

### 4.5 Repetition validator
Generate the Phase-4/5 normalized repetition signature and compare all 24 campaign cases. The tool flags isomorphic pairs; a human may waive only with a written `repetition_exception_rationale` naming the genuinely new deduction pressure.

### 4.6 Certifier outputs
Per case report:
- raw legal arrangement count per stage;
- canonical arrangement-class count;
- legal transition count;
- solution-class count;
- successful paths;
- necessary exposure/occlusion facts where derivable;
- partial-region violations;
- unreachable target histories;
- symmetry quotient summary;
- normalized repetition signature;
- source hash/certifier version;
- content budget violations.

Developer proof metadata may assist hints and review, but certifier-discovered solution data must never leak into shipping normal UI.

---

## 5. Runtime state machine

### 5.1 Top-level puzzle states
Canonical state enum:
- `LOADING_CASE`
- `EDIT_A`
- `SPRAY_A_TRANSACTION`
- `POST_A` / `EDIT_B` when second stage exists
- `SPRAY_B_TRANSACTION`
- `READY_TO_REVEAL`
- `REVEALING`
- `RESULT_SUCCESS`
- `RESULT_FAILURE`
- `PAUSED`

One-pass cases transition `EDIT_A -> SPRAY_A_TRANSACTION -> READY_TO_REVEAL`.

Presentation animation may lag behind a committed semantic transaction, but gameplay input remains locked until presentation acknowledges the new stable state.

### 5.2 Editable arrangement
The editable state stores only stable object instance IDs mapped to legal arrangement elements/arrangement ID. Object transforms in the scene are a projection of this mapping.

A placement transaction is:
`select legal destination -> resolve exact resulting arrangement -> atomically replace editable arrangement -> animate old transform to certified transform`.

If animation is interrupted, load/resume uses the committed exact arrangement, never an interpolated transform.

### 5.3 Spray atomicity
`SPRAY` is a semantic transaction:
1. verify current state is editable and arrangement ID is certified/legal;
2. construct a complete next-state payload in memory from certified exposure table;
3. append coat to exposed histories exactly once;
4. create new committed checkpoint with monotonically increasing local transaction sequence;
5. durably save checkpoint using atomic file replacement;
6. only after durable success mark semantic state advanced;
7. start/continue presentation animation;
8. unlock next stable state only after presentation completes/skips.

A crash at any point must resume either the previous durable checkpoint or the complete new durable checkpoint, never half-painted state.

### 5.4 Undo model
Maintain a bounded semantic undo journal for the current case, not arbitrary visual transforms.
- pre-spray placement edits may use lightweight in-memory undo entries and optional resume snapshot;
- each spray boundary has a full checkpoint;
- Undo from post-A returns to the exact pre-A editable state;
- Undo from post-B returns to the exact post-A/pre-B editable state with A histories preserved;
- result Undo follows Mechanical/UX rules.

Undo itself is also a transaction when persistence is updated. It must not decrement an integer separately from state replacement.

### 5.5 Transaction idempotency
Every spray/checkpoint transaction has a stable ID `(case_id, local_attempt_id, tx_seq, stage)`. Replaying a transaction after crash/import sees that the destination checkpoint already contains that ID and does nothing. No coat can be appended twice because an animation callback or cloud merge fired twice.

---

## 6. Persistence schema and recovery

### 6.1 Files
Use a small explicit profile layout, e.g. conceptually:
- `profile.json` — progression, tutorial acknowledgements, achievement ledger, latest case pointer, profile schema version;
- `puzzle_state.json` — latest in-progress case semantic state/checkpoints;
- `settings.json` — preferences/accessibility/input configuration where appropriate;
- optional previous-valid backups (`*.bak`) managed atomically.

Actual format may be JSON or another inspectable versioned serialization, but opaque engine scene serialization is forbidden for canonical saves.

### 6.2 Save envelope
Every save document includes:
- `schema_version`
- `build_content_version`
- stable profile ID generated locally
- `revision` monotonic counter
- `written_at_utc` informational only, never sole conflict authority
- checksum/hash for corruption detection
- payload

Puzzle payload includes stable case/object/region/arrangement IDs, not NodePaths or scene-instance IDs.

### 6.3 Atomic local writes
Write new save to temp -> flush/close -> validate parse/checksum -> atomically replace primary -> preserve previous known-good backup. Never modify the only valid file in place.

### 6.4 Corrupt-save policy
On load:
1. validate primary envelope/schema/checksum/semantic IDs;
2. if invalid, validate previous known-good backup;
3. if backup valid, recover and tell user succinctly that the latest state was recovered from a previous checkpoint;
4. if puzzle state alone is corrupt but profile is valid, preserve campaign completion/settings and discard only in-progress attempt;
5. if profile is corrupt but recoverable completion evidence exists in backup/cloud merge, reconstruct via monotonic sets;
6. if no safe recovery exists, move corrupt files aside for support/debug and start a new profile rather than crashing.

Never silently reinterpret unknown arrangement IDs using nearest current geometry.

### 6.5 Schema migration
Migrations are explicit pure transformations `vN -> vN+1` with fixtures. They operate on stable IDs. A migration may drop an incompatible in-progress attempt if a case's certified arrangement schema changed, but must preserve monotonic completed-case/tutorial/achievement evidence whenever safe.

No save migration may invent completion.

---

## 7. Cloud, Dynamic Cloud Sync and conflict policy

### 7.1 Principle
Cloud sync transports versioned semantic files; it does not decide gameplay truth. Local game code performs deterministic merge where multiple valid progress states can coexist.

### 7.2 Merge classes
**Monotonic sets** merge by union:
- completed case IDs;
- tutorial acknowledgements;
- unlocked family milestones;
- internal achievement-eligibility facts.

**Settings** use field-level last-user-change revision when available; otherwise current local settings win to avoid surprising control/accessibility changes from an older device.

**In-progress puzzle attempt** is not union-merged. Choose one valid branch using:
1. same case/content version: greater semantic checkpoint `tx_seq` within the same `attempt_id` wins;
2. distinct attempts or distinct cases: preserve the branch associated with the profile's selected `latest_case` when its revision is newer; otherwise prompt only if both contain material unsynchronized work that cannot be safely ordered;
3. never combine A checkpoint from one attempt with B arrangement from another.

A rare cloud conflict prompt should offer understandable choices (`This device` / `Other device`) with completion union preserved either way.

### 7.3 Dynamic Cloud Sync
Before suspend/hand-off, flush only a stable semantic checkpoint/save revision. Resume validates cloud material before loading into active runtime. Presentation animation state is never synchronized; resume reconstructs from semantic state and may replay/skip visuals.

### 7.4 No timestamp-only destructive policy
Wall-clock timestamps may be skewed. A file is not overwritten solely because its UTC timestamp is later. Schema validity, profile identity, monotonic revision and transaction lineage take precedence.

---

## 8. Demo-to-full import

### 8.1 Shared identity
Demo and full builds use the same stable case IDs, tutorial IDs and schema contracts for shared content. Build entitlement changes availability only; it does not rename content.

### 8.2 Import transaction
On first full launch where demo data is detected:
1. parse/validate demo profile with supported schema migrations;
2. create import fingerprint from demo profile ID + relevant revision/hash;
3. if fingerprint already exists in full profile's import ledger, no-op;
4. union completed shared case IDs and tutorial acknowledgements;
5. merge safe settings only if full user has not changed them or according to explicit field revisions;
6. import in-progress state only if the exact case/content package remains compatible and no newer full attempt exists;
7. derive full-game unlock state from merged facts;
8. persist atomically;
9. then evaluate achievement eligibility and issue platform unlock calls idempotently.

The demo never directly writes Steam achievements.

### 8.3 Achievement idempotency
Maintain local semantic achievement facts separately from platform acknowledgement. Unlock flow:
`eligibility true -> local pending/unlocked fact saved -> platform request -> platform confirmation when available`.
Repeated launch/import retries may resend a safe unlock request but may never duplicate reward logic or progression.

---

## 9. Input, glyph and UI/state separation

### 9.1 Input abstraction
Gameplay consumes semantic actions frozen in Phase 6, not device keycodes. Device adapters map keyboard/mouse/controller/Steam Input to actions.

A `GlyphProvider` queries active input family/platform APIs and returns presentation glyph IDs. If Steam glyph retrieval is unavailable, use a generic controller glyph set; never let missing glyph service disable actions.

### 9.2 State ownership
- `PuzzleModel`: semantic state only.
- `PuzzleController`: validates commands and executes transactions.
- `PuzzleView`: scene objects, outlines, paint materials, animations.
- `PuzzleUI`: target/stage/action/inspection presentation.
- `InputRouter`: semantic actions.
- `PersistenceService`: snapshots/migrations.
- `PlatformServices`: Steam/null adapter.

UI may request factual queries (`current exposure`, `target history`, `actual history`, `legal destinations`) through read-only model interfaces. It cannot mutate state directly.

### 9.3 Modal race guard
While a placement or spray transaction is committing, block contradictory semantic commands. Pause may pause/skip presentation but cannot interleave a second Spray, Reset or placement write. Confirmation dialogs capture input focus atomically so one controller press cannot both close a dialog and trigger the underlying Spray.

---

## 10. Localization contracts

All player-facing strings use stable localization keys from first implementation pass. No text baked into meshes, target-card textures, screenshots used as UI, or scene filenames.

Data contracts:
- case flavor title = localization key;
- region display name = localization key or icon-only stable semantic label;
- hint tiers = localization keys with bounded placeholders referencing already-known target labels;
- achievement/store strings are separate resources;
- action prompts use localized action name + glyph, never hard-coded button text.

Layouts must tolerate expansion. Target/history truth is iconically redundant so localization cannot change mechanics.

Certifier/debug proof text is developer-only and need not ship/localize.

---

## 11. Performance and loading budgets

### 11.1 Target
Steam Deck compatibility floor is 30 fps at 1280x800; Fresh Coat should target **60 fps at 1280x800 on Steam Deck-class hardware during normal puzzle interaction** because scenes are intentionally small. 30 fps remains the absolute acceptance floor for any rare transition, not the design target.

Desktop baseline target: 60 fps at 1080p on modest integrated/discrete hardware appropriate to a low-complexity stylized 3D puzzle.

### 11.2 Runtime budgets
Per puzzle typical/ceiling:
- 2–4 visible workpieces normal; 5 exceptional;
- ~16 meaningful semantic regions target budget;
- low hundreds of thousands of rendered triangles is already more than sufficient; prefer far lower;
- no real-time GI requirement;
- no gameplay physics simulation;
- minimal transparencies; object-isolation ghosting must avoid pathological overdraw;
- spray particles/material transitions are cosmetic and scalable/disableable.

### 11.3 Deterministic loading
Load order:
1. immutable certified package;
2. validate package/version/hash;
3. instantiate render scene keyed by stable IDs;
4. apply saved semantic state;
5. resolve view materials/transforms from semantic state;
6. accept input.

Input is never accepted before semantic state and view agree. Missing render asset for a required stable ID is a hard development/build validation error; release should fail gracefully to menu/support rather than invent a substitute gameplay object.

---

## 12. Automated validation and test architecture

### 12.1 Pure model tests
Required exhaustive/unit tests:
- coat-history transitions;
- target predicates;
- legal/illegal arrangement lookup;
- A->B transition legality;
- spray idempotency;
- undo checkpoint restoration;
- progression 2-of-3 + mandatory-gate logic;
- demo import union/idempotency;
- achievement eligibility idempotency;
- save migration fixtures;
- corrupt-save recovery.

### 12.2 Golden case fixtures
At minimum freeze FC01, FC07, FC10, FC14, FC18, FC21 and FC24 as golden semantic fixtures containing:
- known legal arrangements;
- known invalid arrangements;
- expected exposure sets;
- expected target result for at least one success and representative failures;
- expected solution-class count after symmetry where stable.

Any certifier/runtime disagreement on a golden fixture fails CI.

### 12.3 Geometry adversarial suite
Include fixtures for:
- flush face contact;
- zero-area edge/point contact;
- exact aperture/cavity exposure;
- multiple blockers whose union covers a region;
- partial coverage requiring subdivision;
- coplanar invalid overlaps;
- symmetric mirrored arrangements;
- near-grid-boundary authoring mistakes.

### 12.4 Transaction crash tests
Inject failure after each spray transaction step: before temp write, after temp write, after flush, after replace, before animation, during animation, before platform/cloud notification. Restart must resolve to exactly old or new checkpoint with no duplicated coat.

Repeat similarly for Undo and demo import.

### 12.5 Cloud merge matrix
Automated merge fixtures cover:
- same profile same attempt newer tx;
- divergent attempts;
- completed cases on each device;
- older demo + newer full;
- same demo imported twice;
- clock skew;
- corrupt remote + valid local;
- unsupported future schema;
- achievement pending during merge.

### 12.6 UI/input tests
Automatable smoke tests should verify every required action is reachable with controller-only navigation, modal focus does not leak, device switch changes prompts without state loss, and 1280x800 target/settings layouts stay within safe bounds.

---

## 13. Debug tooling boundary

Developer builds should provide:
- arrangement ID/state inspector;
- certified exposure overlay;
- region ID labels;
- source/certifier hash display;
- symmetry class/solution-class browser;
- transition graph viewer;
- save envelope viewer/corruption injector;
- forced platform/cloud response simulator;
- transaction crash injection points;
- input-device simulator;
- performance counters.

These tools are compiled out, hidden behind non-shipping feature flags, or otherwise inaccessible in normal release UI. The normal player exposure preview remains strictly the factual current-state feature frozen in Phase 6, not the developer solver overlay.

---

## 14. Telemetry and privacy boundary

Baseline product uses **no custom gameplay telemetry backend and no account system**.

Permitted without design reopening:
- storefront/platform aggregate analytics provided by Steam;
- local diagnostic logs that contain technical events, build version and case ID but no personal content;
- opt-in crash reporting only if a concrete service is later selected with clear disclosure and minimal data.

Do not transmit arrangement attempts, hint use, failures, controller IDs or save contents to a custom server by default. Commercial demo conversion may be assessed from platform/store statistics; gameplay must not depend on analytics connectivity.

---

## 15. Demo/full build boundaries

One codebase, shared content schema, build-time entitlement manifest.

**Full build:** FC01–FC24 plus full progression/achievements.
**Demo build:** only the approved seven-case content package and demo end/upsell surface; achievements disabled; shared/importable save contract retained.

Content packaging must ensure omitted full-game cases are genuinely absent/unreachable from demo assets if practical, while stable IDs of included cases remain identical.

No `if demo then different puzzle rules` branches are allowed in the semantic model.

---

## 16. Recommended dedicated-repository implementation order

### 12A1 — Pure deterministic core
Case schema, stable IDs, coat histories, targets, arrangement IDs, transition tables, pure PuzzleModel tests.

### 12A2 — Certifier/exposure tooling
Constrained geometry importer, exact exposure precompute, partial-region rejection, symmetry canonicalization, certified package output, golden fixtures.

### 12A3 — Runtime scene bootstrap
Godot 4.7.x project, render objects keyed to semantic IDs, socket/pose presentation, null PlatformServices.

### 12B — Vertical slice
Implement FC01 + FC07 + FC10 with complete arrange/spray/undo/reveal flow, controller path, save checkpoint, no production content expansion yet.

### 12C1 — Persistence and recovery
Atomic save envelope, migrations, crash injection, resume.

### 12C2 — Full core rules
Second pass, rearrangement, cavity/self-occlusion presentation, ordered histories, factual exposure preview.

### 12D — Content population
Certify and integrate all FC01–FC24 only after repetition/budget gates pass.

### 12E — UX/accessibility/platform
Controller remapping, glyph provider, Deck layouts, localization, hints, Steam adapter, demo package, cloud/import/achievements.

### 12F — Adversarial QA
Cloud conflicts, corrupt saves, transaction races, symmetry, partial exposure, asset/truth divergence, modal double input.

### 12G — Empirical gates
Run the existing E1–E5/C1–C6 player/release validation; repair implementation/readability without inventing new mechanics.

### 12H — Release candidate
Performance, packaging, demo/full regression, Steam Deck testing, title/price/store release decisions.

---

## 17. Explicit technical attacks and frozen resolutions

### T1 — Renderer says exposed, truth says occluded
Resolution: certified semantic exposure is authoritative; asset-ID-buffer divergence fails QA/build review. Never read paint truth from renderer.

### T2 — Atomic region partly covered
Resolution: `PARTIAL_INVALID`; author subdivision or pose removal required. No percentages/epsilon acceptance.

### T3 — Symmetry hides a future distinction
Resolution: stage-A equivalence must preserve target-relevant reachable B transition classes, not current exposure alone.

### T4 — Save crashes halfway through Spray
Resolution: complete next state constructed first, atomic file replacement, transaction ID/idempotency. Resume old or new checkpoint only.

### T5 — Animation callback fires twice
Resolution: presentation cannot append coats; model transaction already committed and duplicate tx ID is a no-op.

### T6 — Undo during Spray
Resolution: arrangement-changing commands locked during semantic commit/presentation boundary; Undo becomes available only from next stable state and restores full checkpoint.

### T7 — Demo imported twice
Resolution: import fingerprint ledger + monotonic union + idempotent achievements.

### T8 — Cloud has two branches
Resolution: union monotonic progression; never splice puzzle attempts; lineage/revision selects compatible branch or prompts on irreducible divergent attempts.

### T9 — Clock skew makes older file appear newer
Resolution: timestamp is informational; schema/profile/revision/transaction lineage dominate.

### T10 — Community Steam plugin becomes unmaintained
Resolution: platform adapter isolates dependency; core works with null/local adapter. Select supported binding during implementation bootstrap.

### T11 — Corrupt in-progress puzzle destroys campaign
Resolution: separate profile/puzzle state, known-good backup and surgical fallback; completion is preserved where valid.

### T12 — Debug solver leaks into player UI
Resolution: developer tooling separate/stripped; normal preview asks only current factual exposure.

---

## 18. Phase-8 acceptance
Phase 8 passes because a fresh implementation session can now build the deterministic core, certifier, runtime state machine, persistence, Steam boundary and QA architecture without inventing important technical gameplay behavior.

Implementation-flexible details that are intentionally **not** game-design unknowns:
- exact maintained Godot Steamworks binding selected at bootstrap;
- exact serialization library/JSON helper;
- exact polygon boolean library used by certifier if it satisfies the exactness/tests contract;
- exact scene/node class names;
- cosmetic shader/particle implementation;
- final hardware minimum spec after profiling.

No production implementation has begun in this factory.

PHASE 8 = COMPLETE
DESIGN COMPLETE = NO

## NEXT ACTION — PHASE 9 WHOLE-GAME SIMULATION
Re-read all active Game #015 authority, then simulate the entire shipped experience on paper from first boot through campaign completion and repeat/resume behavior. Walk at least: first launch/settings/controller, FC01 onboarding, first failure/undo, family unlock relief, demo-to-full import, FC10 two-pass transition, FC13 ordered-history learning, FC16 cavity inspection, FC21 role reversal, FC24 capstone, completion/achievements, suspend/cloud resume, corrupt-save fallback, replay/alternate solution, and a hostile player who brute-cycles poses. Record contradictions, friction, pacing/readability problems and repair the specification where needed. If contradictions require mechanical reopening, say so explicitly; otherwise advance to Phase 10 Adversarial Review.