# GAME #014 — PHASE 8 TECHNICAL IMPLEMENTATION SPECIFICATION

Date: 2026-09-02
Status: COMPLETE — implementation contract frozen; Whole-Game Simulation next.
Working title: **NEGATIVE CASTING**
Authority: `START_HERE.md` -> `STATUS.md` -> `GAME_INDEX.md` -> Game #014 tournament record -> `GAME14_PRODUCT_THESIS.md` -> `GAME14_MECHANICAL_ARCHITECTURE.md` -> `GAME14_CONTENT_ARCHITECTURE.md` -> `GAME14_UX_PRESENTATION.md` -> `GAME14_COMMERCIAL_MODEL.md` -> this file.

## 1. Phase-8 verdict
**PASS.** The frozen design can be implemented without inventing important gameplay. The technical direction deliberately keeps puzzle truth in a small deterministic data/model layer and treats the attractive diorama renderer as a non-authoritative projection of that truth.

No production implementation begins in this factory. This document is the implementation contract a later dedicated repository must follow.

---

# 2. Engine / runtime direction

## 2.1 Frozen lead engine
**Godot 4.7.x stable, GDScript-first**, using the latest supported 4.7 patch available when implementation begins. Do not build production on a 4.8 development snapshot merely for novelty.

Rationale:
- current Godot release policy lists 4.7 (June 2026) as supported;
- the game needs lightweight 2D deterministic logic plus modest stylized 3D/2.5D presentation, not a custom renderer;
- Godot supports desktop Vulkan/Direct3D/Metal paths plus Compatibility/OpenGL for lower-end fallback;
- controller, localization, save-file and desktop export requirements are within normal engine scope;
- the puzzle certifier can share pure data/model code with runtime without binding truth to scene nodes or GPU output.

C# is not required. Native/GDExtension code is allowed only if profiling proves a real need; current frozen case maxima are far too small to assume one.

## 2.2 Supported desktop baseline
Lead release target:
- Windows 10/11 x86_64;
- Linux x86_64 / SteamOS-class environment for Steam Deck;
- macOS may be supported if release resources allow, but it is not required to define puzzle truth.

Renderer policy:
- prefer Godot Forward+ or Mobile renderer for the stylized diorama where stable on target hardware;
- maintain a Compatibility-renderer fallback if visual acceptance/performance remains adequate;
- logical puzzle truth must be bit-identical regardless of rendering backend.

Minimum product performance target is much stricter than Steam Deck compatibility minimum: **60 fps target at 1280x800 on Steam Deck-class hardware**, while **30 fps is the hard playable floor** during heavy cosmetic transitions. Puzzle-state changes themselves must settle logically in the same frame and never wait on GPU ray tracing or asynchronous visual effects.

## 2.3 Steam / Deck implementation assumptions
Current Steam Deck compatibility guidance requires the default controller path to expose all content, correct active-device glyphs, and support for Deck-native 1280x800 or 1280x720; 30 fps at 800p is the compatibility floor. The frozen UX remains more conservative than that minimum.

Use Steam Input where practical for future-proof device glyphs and action-based configuration. The game must also remain fully playable through ordinary engine gamepad events if Steam APIs are unavailable/offline.

Steam Cloud is an optional platform transport for save files, never the source of puzzle truth. Platform API failure cannot prevent offline single-player progression.

---

# 3. Architectural boundary: truth model vs presentation

The production project should be split conceptually into five layers:

1. **Core Logic** — exact rational geometry, blocker transforms, ray/polygon incidence, target evaluation, legal configuration checks, observational equivalence. Pure deterministic code; no SceneTree dependency required for tests.
2. **Content Model** — validated archetype/case schemas, stable ids, versioning, hashes, derived-cache metadata.
3. **Game State** — current blocker states, undo/redo, check result, campaign completion, hints/tutorial flags, persistence.
4. **Presentation / UX** — diorama scenes, cameras, surface cards, semantic overlays, animations, audio, controller/mouse/keyboard adapters.
5. **Platform Services** — Steam achievements/cloud/input/store hooks. Every platform call is replaceable or optional for local play.

Hard invariant: layers 4–5 may consume canonical/derived logical truth but may not feed renderer-derived collision, screen-space rays, shadow maps, physics queries or floating-point visual transforms back into the canonical solution evaluator.

---

# 4. Exact number representation

## 4.1 Authored integers and rationals
Canonical authored geometry uses signed integers for world/casting-plane coordinates. Rational sample parameters and any exact intermediate ratio use normalized pairs:

`Rational { num: int64, den: int64 > 0 }`

Normalization:
- divide by `gcd(abs(num), den)` after construction;
- zero is always `0/1`;
- denominator is always positive;
- comparison uses exact cross multiplication with overflow protection.

The frozen authored coordinate recommendation `0..32` is retained. Implementation tools may internally scale imported shapes, but the canonical saved geometry remains integer/rational.

## 4.2 Overflow policy
With the frozen maxima, signed 64-bit arithmetic is sufficient if formulas are bounded carefully. Nevertheless:
- use checked integer operations in certifier/editor validation;
- reject content if an exact intermediate exceeds the implementation's proven safe bound;
- never silently fall back to float for a truth decision.

If the selected language/runtime cannot provide safe checked multiplication conveniently, implement a tiny exact predicate helper using wider integer support or factor-reduced cross products. Do not change geometry semantics to avoid this engineering task.

## 4.3 Rational surface samples
A sample is stored as `(t_num,t_den)` and evaluated exactly:
`P = A + t*(B-A)`.

Do not pre-bake sample coordinates to float as canonical data. A derived preview may use float.

---

# 5. Exact transformed blocker polygons

## 5.1 Archetype geometry
Canonical polygon vertices are ordered simple-polygon local integer points. Winding must be normalized consistently by tooling (preferred counter-clockwise). Repeated adjacent vertices are rejected. Zero-length edges are rejected.

## 5.2 Discrete transforms
Baseline pose transforms are exact matrices from the finite 90-degree rotation set:
- 0: `(x,y)`
- 90: `(-y,x)`
- 180: `(-x,-y)`
- 270: `(y,-x)`

Then add socket integer translation. Explicit mirrored authored poses, if ever approved, are represented as named exact transform matrices with entries in `{-1,0,1}` and determinant ±1; the player is still choosing a discrete pose, not applying arbitrary reflection.

No floating-point trig belongs in canonical pose generation.

---

# 6. Exact ray segment vs polygon-interior contract

Canonical Phase-4 rule remains:

`blocked(L,P,B) = TRUE` iff the **open segment** from light `L` to sample `P` intersects the **strict interior** of transformed polygon `B`.

Pure boundary touch/tangency does not block. Any positive-length traversal through polygon interior blocks.

## 6.1 Required implementation algorithm
Use an exact segment-polygon clipping/intersection predicate, not engine physics.

For each polygon edge and the segment `Q(u)=L+u(P-L), 0<u<1`, compute exact candidate boundary-intersection parameters where non-parallel lines meet. Add `u=0` and `u=1` as partition sentinels. Handle collinear overlap as boundary contact candidates but never infer blocking from overlap alone.

Sort/deduplicate exact rational `u` values in `[0,1]`. For every consecutive pair `(u_a,u_b)` with nonzero width, choose exact midpoint `u_m=(u_a+u_b)/2`. Evaluate whether `Q(u_m)` lies strictly inside the polygon using an exact point-in-polygon predicate with boundary classified separately. If any interval midpoint is strict interior and the interval overlaps `0<u<1`, return TRUE. Otherwise FALSE.

Why this contract:
- tangent contact produces no positive-width interior interval -> FALSE;
- crossing a vertex into/out of interior is handled without epsilon rules;
- a segment running along a polygon edge is boundary-only -> FALSE unless another interval enters strict interior;
- start/end points are excluded by the open-segment rule;
- the same algorithm works for convex and approved concave simple polygons.

An optimized convex-only fast path may be added later but must be equivalence-tested against this reference predicate on all canonical content and fuzz fixtures.

## 6.2 Exact point classification
`classify_point_polygon(Q, poly)` returns exactly one of:
- `OUTSIDE`
- `BOUNDARY`
- `INSIDE`

Boundary is detected first using exact collinearity + bounding-box containment. Interior uses an exact crossing/winding rule with half-open vertex handling so a horizontal/vertex crossing is counted deterministically.

## 6.3 Degenerate rejection
Authoring validation rejects:
- self-intersecting polygons;
- zero-area polygons;
- duplicate non-adjacent edges;
- light exactly on polygon boundary/interior for any legal state;
- sample exactly on polygon boundary/interior for any legal state;
- blocker/surface overlap;
- zero-length surfaces;
- sample parameter at 0 or 1;
- duplicate sample parameters on a surface.

Tangency can mathematically exist but shipping clearance diagnostics normally reject it as unreadable.

---

# 7. Clearance / visual robustness

Exact truth alone is insufficient for human readability. Tools compute a **clearance metric** for every `(light, sample, blocker state)` ray against every polygon vertex/edge that does not logically cross interior.

Implementation may choose a normalized rational or high-precision diagnostic distance for authoring review, but this diagnostic is not canonical blocking truth.

Before content freeze, pick and document one world-space visual-clearance threshold after the actual renderer/camera exists. Any canonical state closer than the threshold to changing incidence is rejected or manually reviewed. The threshold is an empirical presentation gate and may tighten; it may never change which side exact logic calls blocked.

---

# 8. Canonical authored data schemas

Use text-reviewable data in the dedicated repository (JSON, JSON-compatible resources, or Godot Resources with deterministic export). Canonical logical fields must remain diffable and serializable independent of scene-node layout.

## 8.1 Archetype schema
Required conceptual fields:

```text
BlockerArchetype
  archetype_id: StableId
  schema_version: int
  geometry_revision: int
  display_name_key: StringKey
  local_polygon: [IntPoint]
  allowed_pose_defs: [PoseDef]
  presentation_asset_id: StableId
  presentation_footprint_revision: int
```

`presentation_asset_id` never defines truth.

Stable ids are lowercase ASCII namespaced strings, e.g. `blocker.bar_short.v1`; do not use array index as identity.

## 8.2 Case schema
Required conceptual fields:

```text
CaseDef
  case_id: StableId              # e.g. case.nc09
  schema_version: int
  content_revision: int
  display_order: int
  group_id: StableId
  required_for_floor: bool
  demo_included: bool
  difficulty_band: enum
  bounds: IntRect
  lights: {L1:IntPoint, L2:IntPoint}
  surfaces: [SurfaceDef]
  blockers: [BlockerInstanceDef]
  illegal_joint_states: [JointStateConstraint]
  initial_state: {blocker_id: pose_id}
  target: {surface_id: [TargetClass]}
  focus_surface_id: StableId
  tutorial_flags: [StableId]
  estimated_solve_band: enum/range
  human_route: HumanRouteDef
  hints: [HintTierDef]
  localization_keys: {...}
```

Each blocker instance has stable `blocker_id`, `archetype_id`, integer socket, and ordered stable `pose_id`s. Runtime save files persist ids, not list indices.

## 8.3 Surface schema

```text
SurfaceDef
  surface_id: StableId
  a: IntPoint
  b: IntPoint
  samples: [RationalT] # strictly increasing, 3..12 per Phase-4 limits
  presentation_anchor_id: StableId
```

Target array length must exactly equal sample count.

## 8.4 Human-route schema

```text
HumanRouteDef
  route_id: StableId
  route_revision: int
  intended_aha_key: StringKey
  steps: [DeductionStep]

DeductionStep
  step_id: StableId
  family: enum
  premises: [LogicalFactRef]
  subject: CandidateSubjectRef
  before_classes: [ClassRef] or count
  after_classes: [ClassRef] or count
  depends_on: [step_id]
  rationale_key: StringKey / authoring note
```

Only Phase-4 deduction families are allowed unless design is explicitly reopened.

---

# 9. Validation pipeline

Loading canonical content for shipping/tooling is two-stage:

## 9.1 Structural validation
Reject before geometry work if:
- duplicate ids;
- missing referenced archetype/pose/surface;
- malformed rational;
- samples unsorted/duplicated/outside `(0,1)`;
- target/sample length mismatch;
- blocker count/state/surface/sample ceilings exceeded without explicit design-reopen marker;
- initial state illegal;
- unknown enum/string id;
- floor/demo/group campaign metadata contradicts Phase 5;
- demo includes anything outside NC01–NC08 under the frozen base plan without explicit product revision.

## 9.2 Geometry validation
Then validate polygon simplicity, transforms, lights/surfaces/blocker separation, legal joint-state combinations, incidence, clearance, equivalence, solution existence, solution classes and human route.

Shipping build must fail CI/content packaging if any required floor case is uncertified or cache hashes do not match canonical truth.

---

# 10. Derived caches, hashing and invalidation

## 10.1 Canonical geometry hash
Serialize canonical logical geometry in a normalized order and compute a cryptographic digest (SHA-256 preferred). Include:
- schema version affecting truth;
- bounds;
- exact lights;
- exact surface endpoints/sample rationals;
- referenced archetype logical geometry revision + polygon;
- blocker sockets and legal exact pose transforms;
- joint legality constraints.

Do **not** include cosmetic asset paths, localized strings or UI layout.

## 10.2 Target hash
Separate digest over ordered `(surface_id, target classes)` plus accepted-solution policy.

## 10.3 Derived-incidence cache
Cache key includes:
`core_logic_version + geometry_hash`.

Cache payload may contain for each blocker pose:
- per-light/per-surface sample bitsets;
- global observational-equivalence partition;
- clearance diagnostics.

If key differs, discard and regenerate automatically. No manual stale-cache waiver exists.

## 10.4 Certification cache
Key includes:
`certifier_version + core_logic_version + geometry_hash + target_hash + human_route_revision`.

Payload may include solution-class summary and route verification traces. Shipping authority remains canonical data + current certifier result, never the cache file itself.

---

# 11. Runtime puzzle state machine

Recommended high-level states:
- `CASE_LOADING`
- `PLAY_READY`
- `MUTATING_POSE`
- `CHECK_FEEDBACK`
- `SOLVED_PRESENTATION`
- `CASE_MENU`
- `PAUSED`
- `LEAVING_CASE`

Logical mutation is atomic. Animation may continue after truth changes, but input buffering must not create impossible intermediate states.

## 11.1 Current case state

```text
CaseSession
  case_id
  content_revision
  blocker_pose_by_id
  selected_blocker_id
  primary_surface_id
  contribution_inspection_enabled
  undo_stack
  redo_stack
  last_check_mismatch_samples
  has_mutated_from_initial
  solved_this_session
```

Only blocker poses are puzzle truth. Selection, surface focus and inspection are UI state and do not affect target evaluation.

## 11.2 Pose mutation
On state-next/state-prev/direct pose action:
1. resolve requested next legal pose for selected blocker;
2. reject any explicitly illegal joint state before commit;
3. push prior blocker pose into one atomic undo command;
4. clear redo stack;
5. apply pose;
6. recompute current semantic sample truth from derived incidence (or reference geometry in debug);
7. clear/dismiss stale mismatch highlighting per UX rule;
8. autosave resumable state using debounce/transaction policy;
9. play presentation transition.

Do not put surface changes, focus changes or inspection toggles into puzzle undo history.

## 11.3 Undo / redo
Command is `(blocker_id, from_pose_id, to_pose_id)`. Undo/redo must revalidate ids and legality against loaded content. If content revision migration removed a pose, the resume state is migrated/reset before session begins; history is not trusted across incompatible revisions.

Undo stack need not persist across app restarts. Current blocker configuration must persist. This avoids save bloat and migration ambiguity while preserving the player’s meaningful progress.

## 11.4 Check
Check compares exact current semantic class for every sample against target.
- exact match -> solve transaction;
- mismatch -> record only mismatching `(surface_id,sample_index)` for UI.

Never calculate or surface “best blocker,” distance-to-solution, candidate solution count or correct-pose comparison in normal runtime.

---

# 12. Input abstraction

Implement the Phase-6 logical action list as engine input actions. Gameplay systems consume actions, not physical keycodes.

Required action categories:
- blocker focus prev/next;
- pose prev/next;
- surface prev/next;
- contribution inspection toggle;
- check;
- undo/redo;
- reset;
- case menu/pause;
- confirm/back;
- directional UI navigation.

Input-device tracking changes prompt glyph family only after meaningful input; passive mouse movement/trackpad noise must not constantly flip glyphs.

Steam Input integration, if used, maps to the same logical actions. Losing Steam Input falls back gracefully to standard gamepad mapping.

---

# 13. Certifier contract

A deterministic offline certifier/editor tool is mandatory before content population can be considered complete.

## 13.1 Enumeration
For a case, enumerate Cartesian blocker pose vectors in stable blocker/pose-id order and skip explicit illegal joint states. Frozen maximum ordinary raw space is at most `4^6 = 4096`, so exhaustive search is the reference algorithm; clever SAT solving is unnecessary for correctness.

For every vector:
- combine cached per-blocker incidence by OR per light/sample;
- classify target semantic state;
- compare target;
- if valid, record vector and observational solution-class signature.

A debug mode must periodically recompute incidence from exact geometry and assert cache identity.

## 13.2 Observational equivalence
For one blocker, two poses are equivalent iff:
1. their complete incidence vectors across all lights/surfaces/samples are identical; and
2. they participate identically in explicit joint-legality constraints.

Construct deterministic equivalence class ids by sorting member pose ids and hashing/serializing the set. Do not equate poses merely because rendered silhouettes look symmetric.

Complete solutions belong to the same meaningful solution class when every differing pose is within the same per-blocker observational equivalence class.

## 13.3 Solution acceptance
Runtime accepts **every** physically legal target-valid vector. It never compares against a single authored solution pose.

Certifier reports:
- raw legal configurations;
- valid physical vectors;
- meaningful solution-class count;
- each blocker's equivalence partition;
- bypass/easier solution diagnostics where computable.

---

# 14. Human-route verification

The machine certifier must verify that each documented deduction is true about candidate classes under its declared premises; it is not enough to store prose.

Reference approach:
1. begin with each blocker's case-level observational pose classes;
2. apply route premises from target semantics and previously proven class reductions;
3. for each step, mechanically test that every class eliminated by the step is inconsistent with the stated premise(s), and every retained class remains possible under the step's local claim;
4. verify dependency graph is acyclic;
5. verify claimed before/after counts;
6. verify meaningful-step count and family diversity gates by difficulty band;
7. verify residual assignment does not occur before required MID/LATE/CAPSTONE depth gate.

The verifier is intentionally conservative. If a sophisticated human argument cannot be represented, improve the authoring fact vocabulary within the same frozen mechanics; do not simply stamp the route “verified.”

Suggested logical fact references include:
- target state of named sample;
- blocker pose-class incidence on named light/sample;
- established candidate-class set for named blocker;
- set of remaining producers for named channel/sample;
- equality/inequality of incidence extent/endpoints across named pose classes;
- equivalence-on-surface / split-on-other-surface relation.

The tool may calculate richer diagnostics, but player UI never exposes route verification data automatically.

---

# 15. Renderer / logical-truth separation

## 15.1 Visual geometry
A 3D blocker mesh may be an extrusion/stylization of its canonical 2D footprint. Its floor-plane projected silhouette must agree visibly with logical polygon within an authored tolerance. Decorative detail may sit above the occluding body only when it cannot imply a materially different occlusion edge.

Authoring tooling should render/debug the canonical polygon outline over the scene mesh to catch disagreement.

## 15.2 Shadows
Visual renderer shadows are cosmetic. They may use soft edges, baked styling or custom projected textures, but target/current semantic markers derive from canonical incidence bits.

Do not sample a GPU shadow buffer to decide LIT/L1_ONLY/L2_ONLY/BOTH.

## 15.3 Semantic overlay
Each sample gets a stable presentation anchor derived from its surface parameter. UI binds:
- target canonical class;
- current canonical class;
- mismatch flag after explicit check;
- optional selected-blocker current contribution bit(s).

The overlay may animate between states but must never display an intermediate semantic class as truth.

## 15.4 Contribution inspection
Only current selected pose incidence is exposed. Implementation API should accept `(case_session, blocker_id)` and return its **current** per-light sample contribution. It must not have a normal gameplay call that requests target-ranked or future-pose comparison.

Counterfactual tooling exists only in developer/editor builds.

---

# 16. Persistence model

## 16.1 Save split
Use two conceptual files/domains:

**Progress save (cloud-eligible)**
- save schema version;
- campaign content-set/version marker;
- completed case ids + completion revision metadata;
- unlocked groups or data sufficient to derive them;
- per-case resumable blocker pose map + content revision;
- last active case;
- tutorial-seen flags;
- hint tiers opened per case;
- campaign/all-shipped completion markers (derivable but cacheable);
- pending platform-achievement reconciliation ids.

**Settings save**
- accessibility settings;
- text/UI scale;
- audio levels;
- remappable bindings where portable;
- active glyph behavior preference;
- graphics/display options.

Device-sensitive display mode/resolution/render-scale should remain local rather than blindly roam through cloud. Safe accessibility preferences may roam if implementation keeps them separate from bad cross-device display state.

## 16.2 Atomic local writes
Never overwrite the only save directly.

Reference transaction:
1. serialize deterministic new save to `progress.tmp`;
2. flush/fsync where platform permits;
3. parse + checksum/validate temp;
4. rotate valid existing primary to `progress.bak`;
5. atomic rename temp -> primary;
6. retain at least one previous known-good backup.

Include file-level checksum/hash over canonical serialized payload. A checksum is corruption detection, not security.

On load:
1. try primary;
2. if corrupt/incompatible beyond migration, try backup;
3. preserve corrupt file under diagnostic name rather than deleting immediately;
4. if both fail, start fresh with a visible recoverability message, never crash-loop.

## 16.3 Autosave points
Autosave after:
- blocker pose mutation (debounced but flushed promptly on leave/quit);
- case completion;
- group unlock/progression change;
- hint/tutorial state changes worth retaining;
- leaving a case.

Do not require manual save slots for this finite puzzle campaign.

---

# 17. Content revision and save migration

## 17.1 Case resume compatibility
A saved in-progress case stores `case_id`, `content_revision`, and pose ids by stable blocker id.

On load after content update:
- if same case revision -> restore directly after legality validation;
- if revision changed but every saved blocker id/pose id still exists and canonical migration table declares compatibility -> restore mapped state;
- otherwise reset **that case's resumable configuration only** to new initial state and tell the player briefly if they had in-progress work.

Never delete earned completion merely because geometry of an already completed case changed, unless a serious invalid-save bug requires a one-off explicitly documented migration. Completion is player history, not a revalidation benchmark.

## 17.2 Migration tables
Every save-schema or destructive content-id change requires an explicit migration function/table covered by fixtures. No heuristic matching by display name.

Old migration steps remain available for all public versions the team promises to support, or a documented minimum upgrade path converts through intermediate schema representations.

---

# 18. Demo -> full import

## 18.1 Separate namespace
Demo and full app should use separate local save roots/app ids as platform conventions require. The full game may perform a one-time import scan for the demo's explicitly exported/importable progress payload.

## 18.2 Importable data
Only import when schema/content compatibility is proven:
- NC01–NC08 completions;
- compatible current demo case pose map;
- tutorial-seen flags;
- opened hint tiers;
- safe accessibility/control settings.

Do not import graphics resolution/window mode blindly.

## 18.3 Merge rules
Import is one-way and idempotent.
- Existing full-game completion always wins over missing demo completion.
- Union completed case sets where ids are allowed demo ids.
- For one resumable case present in both, prefer the full-game state unless the full save is effectively new and import has never occurred.
- Record `demo_import_version/source_hash` so relaunch does not repeatedly overwrite progress.
- Corrupt/incompatible demo data is ignored with optional non-blocking explanation; full game starts normally.

Demo uninstallation after import must have no effect.

---

# 19. Steam Cloud boundary / conflict policy

Cloud transports **progress save + safe roaming settings**, not volatile caches, certification files, screenshots or graphics/device settings.

Preferred file strategy is a very small number of explicit stable files rather than per-case cloud files, reducing cross-device partial-state risk. Steam Auto-Cloud or explicit Remote Storage can be selected during implementation; either must respect the same local atomic-save/recovery contract.

If Auto-Cloud is used, configure platform root overrides deliberately because save roots vary by OS. Never rely on an undocumented absolute user path.

Conflict policy:
- local app maintains primary + backup regardless of cloud;
- when platform presents a cloud conflict, do not silently select by timestamp inside custom code unless platform contract guarantees the decision;
- when custom reconciliation is possible, monotonic facts such as completed cases/hints/tutorial flags may be safely unioned, while one active resumable pose state is selected from the explicitly newer valid save or presented through platform conflict UX;
- never let a corrupt remote copy delete the only local backup;
- achievement state is reconstructed/reconciled from campaign progress, not used to reconstruct puzzle saves.

Offline play always works. Cloud sync failure is non-fatal.

---

# 20. Accessibility / settings persistence

Persist at least:
- UI/text scale;
- semantic-glyph prominence;
- color-vision-safe palette selection if offered;
- contrast/background simplification;
- reduced motion;
- screen shake (default none/minimal);
- audio sliders/mutes;
- subtitle/caption settings if any voiced content exists;
- hold/toggle preferences where applicable;
- remapped keyboard/gamepad bindings;
- mouse wheel pose-cycle preference;
- reset-confirm preference only if UX implementation offers it.

No accessibility option may alter puzzle target truth or achievement eligibility.

Settings migration must clamp invalid old values and restore safe defaults per field rather than discard the entire file.

---

# 21. Localization-ready boundaries

All player-facing text uses localization keys from day one. Do not store English sentences as logic identifiers.

Localized domains include:
- menus/settings;
- tutorial copy;
- target-state glossary/labels;
- case title/flavor line;
- hint tiers;
- achievements;
- save-recovery/error messages;
- demo/store-adjacent in-game CTA copy where platform allows.

Do not localize stable ids, pose ids, schema enum values or hashes.

UI must allow text expansion without shrinking semantic glyphs below readability gates. Avoid text rendered into bespoke textures. The four target states always remain understandable through redundant glyphs even if a translation is temporarily missing.

---

# 22. Performance budgets

Frozen logical maxima are tiny. Performance risk is presentation, not solver complexity.

## 22.1 Runtime logical budget
For a pose change at maximum ordinary case size:
- derive current semantic truth from precomputed incidence bitsets in <<1 ms on normal desktop/Deck CPU target;
- reference exact-geometry recomputation may run in debug/editor, not required every frame;
- no background solver runs during normal player interaction.

## 22.2 Visual target
At 1280x800 Steam Deck-class baseline:
- target 60 fps during play;
- never below 30 fps sustained;
- surface switch and solved beauty transition may momentarily increase GPU cost but cannot block controls/save logic;
- visual shadow resolution/softness is scalable because it does not define truth.

Content ceilings remain:
- exactly 2 logical lights;
- 1–3 surfaces;
- <=12 samples/surface, floor campaign substantially below this;
- <=6 blockers ordinary hard ceiling, floor currently <=5;
- <=4 legal states/blocker ordinary hard ceiling;
- <=10 logical blocker archetypes launch ceiling.

If a visual asset requires exceeding memory/draw-call budgets, simplify the asset; never simplify canonical semantic overlays.

---

# 23. Automated test suite

## 23.1 Exact geometry unit tests
Required fixtures:
- segment clearly outside polygon -> unblocked;
- proper interior crossing -> blocked;
- pure vertex touch -> unblocked;
- edge tangency -> unblocked;
- collinear travel along boundary -> unblocked unless a later interval enters interior;
- start/end boundary-only contact under open-segment rule -> unblocked;
- concave polygon crossing with enter/exit intervals -> correct;
- all four exact 90-degree transforms;
- rational sample points with nontrivial denominators;
- point-in-polygon boundary half-open vertex cases.

Add deterministic fuzz/property testing: generate small simple polygons and integer segments, compare optimized predicate (if any) against the frozen reference interval-midpoint algorithm.

## 23.2 Incidence / semantic tests
- OR union of multiple blockers on same channel;
- one blocker may block both channels at a sample;
- exact mappings for LIT/L1_ONLY/L2_ONLY/BOTH;
- cache generation equals direct geometry;
- geometry mutation changes hash and invalidates cache;
- cosmetic mutation does not change geometry hash.

## 23.3 Equivalence / certifier tests
- identical incidence + identical legality -> equivalent;
- identical incidence + different joint legality -> not equivalent;
- symmetric-looking but different surface effect -> not equivalent;
- multiple physical solutions within one equivalence class all accepted;
- distinct solution classes reported deterministically;
- unsolvable case rejected;
- stale certification cache rejected.

## 23.4 Human-route tests
Fixtures covering every frozen counting family; reject fake step, cyclic dependency, incorrect before/after count, repeated-family MID gate violation, residual assignment too early.

## 23.5 Runtime state tests
- pose change is one undo step;
- surface/focus/inspection changes do not enter undo;
- redo clears after branched mutation;
- incorrect check preserves configuration;
- correct check records completion exactly once/idempotently;
- leave/reload restores current pose map;
- reset restores initial pose but not historical completion.

## 23.6 Save/recovery tests
- interrupted temp write leaves prior save loadable;
- corrupt primary restores backup;
- corrupt primary+backup starts clean without crash-loop;
- schema migrations deterministic and idempotent;
- removed pose resets only affected in-progress case;
- completed case stays completed across compatible content revisions;
- demo import is one-way/idempotent;
- malformed demo file cannot damage full save;
- cloud-disabled/offline path behaves identically for gameplay.

## 23.7 Input/UX automation/manual gates
Automate what is stable, manually verify:
- all gameplay functions reachable controller-only;
- keyboard-only path complete;
- glyph switching follows actual active input without passive mouse thrash;
- 1280x800, 1280x720, 1920x1080 and common ultrawide/square-ish constraints do not clip essential UI;
- increased UI/text scale does not hide target/current semantics;
- three-surface late case remains readable;
- reduced-motion mode skips/shortens camera easing without changing information.

---

# 24. Malformed-content rejection matrix

A shipping content build fails for any of the following:
- schema parse error or unknown required field/version;
- duplicate/missing stable id;
- invalid rational/geometry/polygon;
- authored incidence/mask override present;
- exact geometry exceeds frozen limits without explicit design reopening;
- invalid initial state or unreachable pose id;
- target length mismatch;
- zero solution;
- target-valid vector rejected because it differs from author's preferred pose;
- stale geometry/target/certification hash;
- human route false under current incidence;
- MID+ route below depth/family gate;
- shipping clearance below approved threshold without recorded readability approval;
- semantic state encoded color-only in its presentation test fixture;
- required demo/floor metadata contradicts campaign contract.

Warnings rather than hard errors may cover non-semantic repetition metrics, cosmetic archetype reuse counts and solve-time estimates, but floor content cannot be marked final until those reviews are resolved.

---

# 25. Developer/debug hooks

Editor/debug builds should expose:
- canonical 2D footprint overlay over rendered blocker;
- exact light-to-sample rays;
- per-blocker/per-pose derived incidence table;
- geometry/target/cache hashes;
- equivalence classes;
- exhaustive solution list/classes;
- human-route verifier trace;
- clearance heat/flag overlay;
- current target/current semantic dump;
- save schema/content revision inspector;
- force-corrupt/interrupt-save test commands.

These are development tools. Shipping player builds must not accidentally expose solver/equivalence/solution-count/debug overlays.

---

# 26. Implementation order in dedicated repository

A fresh implementation session should follow this order rather than building art first.

## 12A-1 — Pure logical kernel
- Stable ids/data primitives.
- Rational/int exact predicates.
- Polygon validation + transforms.
- Reference segment-vs-polygon-interior predicate.
- Incidence + semantic target evaluator.
- Unit/fuzz tests.

Exit: worked Phase-4 examples and edge/tangency fixtures reproduce exactly.

## 12A-2 — Content schema + certifier
- Archetype/case parser.
- Structural/geometry validation.
- Derived hashes/cache.
- Exhaustive solver/equivalence.
- Human-route verifier skeleton.

Exit: tiny synthetic cases certify deterministically and malformed content fails loudly.

## 12A-3 — Headless runtime state
- CaseSession.
- Pose actions/undo/redo/reset/check.
- Campaign completion/unlock calculations.
- Save schema + atomic recovery.

Exit: complete puzzle can be played through tests without renderer.

## 12B — Vertical slice NC01–NC03
- One casting-table scene.
- Two visual lights.
- 2–3 blocker meshes aligned with canonical footprints.
- One surface with target/current semantic cells.
- controller/mouse/keyboard actions.
- contribution inspection current-state only.
- check/mismatch/completion.
- save/resume.

Exit: someone can understand and solve NC01–NC03 with no debug overlay and truth remains independent of renderer.

## 12B+ — Demo architecture proof NC01–NC08
Before mass content, prove:
- second-surface primary/secondary UX at NC07;
- NC08 synthesis readable at 1280x800;
- tutorial skip/revisit;
- settings/accessibility baseline;
- demo->full import harness using synthetic app roots;
- Steam/standard controller glyph fallback architecture.

Only after this proof should implementation populate the full 24-case campaign.

## Later production phases
Follow repository factory template: core systems -> content population -> full UX/accessibility/platform support -> adversarial QA -> empirical playtest gates -> release candidate.

---

# 27. Empirical gates intentionally deferred to implementation

The following are not unknown mechanics; they are measurements that require a real build:
1. final world-space visual-clearance threshold for grazing rejection;
2. whether Forward+/Mobile/Compatibility renderer is best for the final art on Deck hardware;
3. exact GPU visual shadow quality budget at 60 fps target;
4. final UI text/glyph sizes above the frozen readability minimum;
5. whether Steam Input integration or a hybrid standard-gamepad layer gives the cleanest glyph switching across devices;
6. final cloud implementation choice (Auto-Cloud vs explicit API) after app ids/save roots exist;
7. median demo and 24-case completion time;
8. whether 3-surface NC17+ cases remain cognitively readable without solver-like overlays.

Failure of an empirical gate triggers implementation/presentation/content rework within frozen rules. It does not authorize arbitrary masks, third lights, new blocker powers or other excluded mechanics.

---

# 28. Frozen exclusions preserved

Phase 8 explicitly does **not** introduce:
- arbitrary authored projection masks;
- renderer/physics-derived logical truth;
- continuous blocker placement/rotation;
- moving lights;
- third logical light;
- transparency/refraction/mirrors;
- special blocker powers;
- procedural campaign;
- scores/timers/par moves/leaderboards/dailies;
- hint currency, paid hints or solution oracle;
- multiplayer/co-op;
- always-online validation/account dependency;
- color-only semantic information;
- production implementation inside the factory.

Rejected tournament concepts remain history only.

---

# 29. Phase-8 acceptance checklist

PASS requires all true:
- engine/runtime direction is concrete without binding truth to engine physics;
- canonical geometry is exact integer/rational;
- open-segment/strict-polygon-interior tie behavior is implementable without epsilon ambiguity;
- schemas have stable ids and explicit revisioning;
- derived incidence is disposable/hash-keyed;
- runtime mutable truth is only blocker pose vector plus deterministic target evaluation;
- observational equivalence and multiple valid solutions are specified;
- human-route gate is machine-checkable in principle;
- renderer/semantic overlay cannot redefine truth;
- save writes are atomic/recoverable;
- content revision and demo import rules are explicit;
- cloud is transport, not authority;
- localization/accessibility have data boundaries;
- Deck/handheld and performance budgets are stated;
- tests cover geometry, state, certification, saves and malformed content;
- implementation order reaches a vertical slice before content-scale production;
- no excluded mechanic was smuggled in.

**Result: PASS.**

---

# 30. NEXT ACTION — PHASE 9 WHOLE-GAME SIMULATION
Create `GAME14_WHOLE_GAME_SIMULATION.md` and walk the frozen product end-to-end rather than adding systems.

Required simulation passes:
1. fresh install / first boot / controller-only path / settings and accessibility;
2. NC01–NC08 first-player demo arc, including likely wrong actions, two incorrect checks, hint use, leave/resume and NC07 second-surface reveal;
3. transition from demo to full-game import and a no-demo fresh full-game path;
4. hour-1 representative MID case with connected human deductions;
5. late NC17–NC24 three-surface progression, stuck-player flow and optional hint tiers;
6. campaign unlock 2-of-3 behavior, skipped-case return and all-24 Campaign Complete semantics;
7. replay, achievement reconciliation, offline play and cloud-conflict/recovery scenarios;
8. hostile behavior: orientation spam, repeated check, reset/undo abuse, alt-tab/suspend during save, corrupt resume, content revision mismatch, rapid device switching;
9. estimate cognitive/repetition pressure across the full 24-case skeleton and repair contradictions only within frozen mechanics;
10. record every repair explicitly and hand Phase 10 a list of residual attack surfaces.

Do not start production implementation.