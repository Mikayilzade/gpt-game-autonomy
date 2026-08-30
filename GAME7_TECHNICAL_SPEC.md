# GAME #007 — LAST KNOWN SHAPE — TECHNICAL IMPLEMENTATION SPECIFICATION

Last updated: 2026-08-30
Phase: **8 — Technical Implementation Specification**
Selected concept: **G7C02 Last Known Shape**
Production implementation started: **NO**
DESIGN COMPLETE: **NO**

`GAME7_PRODUCT_THESIS.md` governs product identity. `GAME7_MECHANICAL_ARCHITECTURE.md` governs exact puzzle semantics. `GAME7_CONTENT_ARCHITECTURE.md` governs case data/diversity/validation. `GAME7_UX_PRESENTATION_ARCHITECTURE.md` governs player-facing interaction/accessibility. `GAME7_ECONOMY_COMMERCIAL.md` governs commercial/progression/platform promises. This file is authoritative for implementation architecture only where it does not alter those contracts.

---

# 1. Runtime direction and version policy

## Initial engine pin
Initial production target: **Godot 4.7.2-stable, standard build, GDScript-first**.

Fresh check on 2026-08-30:
- Godot 4.7.2-stable released 2026-08-18 and is the current stable Godot 4 release;
- Godot 4.8 is still development-only (`4.8-dev4`, 2026-08-26), therefore it is not an implementation baseline;
- Godot 4.7 remains supported under current Godot release policy.

The dedicated implementation repository must pin the exact engine version in project documentation and CI/tooling. An engine upgrade is allowed only after:
1. full domain/headless validation passes;
2. save compatibility fixtures pass;
3. representative rendering/input/Deck regression passes;
4. a rollback point exists in version control.

No gameplay rule may rely on an engine bug, scene-tree callback ordering, physics frame timing, renderer visibility result, or unstable preview-engine feature.

## Language / native extensions
- GDScript is the default implementation language.
- C# is unnecessary for baseline scope.
- GDExtension/native code is forbidden unless profiling proves a specific validated bottleneck that cannot reasonably be solved in GDScript.
- Solver/tooling may use optimized data structures but must call the same domain transition semantics as runtime.

---

# 2. Hard architecture split

The project is divided into three authority layers.

## 2.1 Domain Core — gameplay authority
Pure/discrete gameplay state and transitions. It owns:
- canonical case state;
- semantic commands;
- legality/rejection reasons;
- candidate form computation;
- observation commit/end semantics;
- slot-based object movement;
- receiver/mechanism resolution;
- win predicate;
- deterministic event ordering;
- revision/idempotency/history;
- canonical serialization/hash;
- solver transitions.

Domain Core must run headlessly without rendering, audio, Steam, input devices or scene-tree geometry.

## 2.2 Presentation — non-authoritative world/UI
Owns:
- 3D/2D scene visuals;
- camera;
- mesh/form animation;
- particles/audio;
- world-space Frame presentation;
- HUD/panels/tutorial text;
- controller/mouse visual focus;
- cosmetic interpolation;
- accessibility presentation modes.

Presentation consumes canonical snapshots/events and emits semantic player intent. It may never decide candidate form, collision affordance, receiver activation, legal movement, puzzle success, or solver state from pixels/physics callbacks.

## 2.3 Platform Adapter — optional external services
Owns:
- Steam initialization/API wrappers;
- achievements;
- Cloud transport/integration;
- platform input glyph/device metadata;
- build/package metadata;
- optional telemetry only if later explicitly adopted.

Offline Domain + Presentation correctness is mandatory when Steam/platform services are unavailable.

Dependency direction:
`Presentation -> Domain API`
`Platform Adapter -> narrow Profile/Persistence interfaces`
`Domain Core -> no Presentation/Platform imports`.

---

# 3. Canonical identifiers and schema/versioning

All gameplay IDs are stable UTF-8 ASCII-safe symbolic identifiers, not scene-tree paths or array indices.

Required namespaces:
- `case_id`: `C01`..`C34`, `DEMO01`..`DEMO06`, optional `R01`..`R06`;
- `object_id`: case-local stable ID, e.g. `obj_a`;
- `object_definition_id`;
- `form_id`;
- `pose_slot_id`;
- `frame_id`;
- `transform_rule_id`;
- `mask_id`;
- `receiver_id`;
- `mechanism_id`;
- `goal_predicate_id`;
- `hint_fact_id`;
- `presentation_theme_id`.

Never serialize engine instance IDs as durable authority.

Every persisted/data-bearing root includes:
- `schema_family`;
- `schema_version` integer;
- `content_version` string/hash where applicable.

Schema migration is explicit `N -> N+1`; no heuristic deserialization. Unknown future mandatory fields reject rather than silently defaulting puzzle authority.

Case content is data-driven. Case scripts may not define private gameplay callbacks. Global registries map IDs to vetted domain rule implementations.

---

# 4. Canonical case state

Conceptual state structure:

```text
CanonicalCaseState
  schema_version
  case_id
  content_version
  revision
  player_region_id
  player_interaction_locus_id|null
  objects: sorted map<object_id, ObjectState>
  mechanisms: sorted map<mechanism_id, MechanismState>
  receivers: only if non-derivable; otherwise derived
  world_flags: bounded declared canonical flags only
  committed_observation: object/frame facts only where mechanically active
```

`ObjectState`:
```text
object_id
pose_slot_id
remembered_form_id
physical_form_id
direct_observation_state  # UNOBSERVED | COMMITTED_OBSERVED where canonical
active_frame_id|null
```

Preview target, mouse hover, camera, candidate ghost, animation progress and focus highlight are not canonical puzzle state.

Derived facts such as receiver claims, movement lock explanations and frame legal-target lists are recomputed deterministically unless persistence is required for an explicit semantic reason.

All maps serialize in ascending stable ID order.

---

# 5. Semantic command envelope

Canonical accepted gameplay commands use an envelope equivalent to:

```text
SemanticCommand
  command_id          # globally unique within save branch
  command_type
  expected_revision
  payload
```

Authoritative command families:
- `COMMIT_OBSERVATION(frame_id, object_id)`;
- player semantic move/leave-frame command that may trigger END_OBSERVATION;
- `MOVE_OBJECT(object_id, from_slot_id, to_slot_id)`;
- globally defined `INTERACT(target_id)` where retained;
- `RESTART_CASE` handled as history/branch operation, not a hidden domain mutation.

`BEGIN_PREVIEW`/`CANCEL_PREVIEW` are session/presentation requests. Candidate computation is pure and may be queried without changing revision/history.

## Validation / transaction contract
For each mutating command:
1. compare `expected_revision` with canonical revision;
2. check command-id ledger;
3. validate against one immutable pre-state;
4. compute direct semantic delta;
5. resolve all deterministic consequences in stable order;
6. assert invariants;
7. compute child canonical state/hash;
8. append one history transaction;
9. increment revision exactly once;
10. expose presentation event bundle.

No partial canonical mutation may escape on rejection/exception.

---

# 6. Idempotency and revision ledger

Maintain a bounded branch-local `command_id -> {payload_digest, result_revision, result_hash, result_code}` ledger sufficient for duplicate delivery/retry protection.

Rules:
- unseen ID + current expected revision: evaluate normally;
- same ID + identical payload digest: return recorded result, no second mutation;
- same ID + different payload: reject `DUPLICATE_COMMAND_ID_PAYLOAD_MISMATCH`;
- stale expected revision: reject before mutation;
- rejected commands never create gameplay history children.

The ledger is operational metadata and excluded from solver-state equivalence, but persistence must retain enough information to make immediate retries idempotent after recovery.

---

# 7. Deterministic candidate / consequence evaluation

`CANDIDATE(frame_id, object_id, canonical_state)` is implemented in Domain Core as a pure function.

Allowed inputs are exactly those declared by Phase 4/5 case/global data: transform rule, object pose/identity, fixed mask, named canonical occluder inputs and explicitly declared mechanism state.

Forbidden inputs:
- rendered pixels/depth buffer;
- camera transform;
- physics collision result order;
- raycast visibility unless raycast merely visualizes a result already determined semantically;
- animation progress;
- frame delta/wall clock;
- audio state.

Preview and commit query the same function. Any mismatch from the same canonical revision is an assertion-level defect.

Deterministic immediate resolution follows Phase-4 order: direct delta -> receiver claims -> receiver priority/id -> mechanism consequences -> access predicates -> invariants -> finalized child.

---

# 8. Canonical serialization and hash

Canonical state encoding must be independent of dictionary insertion order and engine object identity.

Recommended representation:
- explicit versioned dictionary/record converted to canonical UTF-8 bytes;
- stable field order;
- sorted ID collections;
- integers/booleans/enums/IDs only for puzzle authority where practical;
- no renderer floats in authoritative state.

Hash: a stable cryptographic digest such as SHA-256 over canonical bytes.

`state_hash` is used for:
- Undo/Redo exactness fixtures;
- persistence integrity;
- solver duplicate detection if suitable, with collision-safe equality fallback where needed;
- deterministic regression snapshots;
- migration verification.

Revision is excluded from solver equivalence and may be excluded from semantic state hash if the implementation maintains a separate operational hash; the project must name these two concepts clearly. Preferred split:
- `semantic_hash`: puzzle-equivalence state, excludes revision/history;
- `snapshot_hash`: durable exact committed snapshot, includes schema/case/content/revision as needed.

---

# 9. Undo / Redo representation

Baseline implementation favors immutable canonical snapshots or copy-on-write equivalents because case state is deliberately bounded.

Each history node stores:
- parent node ID;
- accepted semantic command summary;
- exact canonical child snapshot or deterministic delta plus verified child hash;
- semantic hash;
- revision;
- optional presentation-safe human label.

Hard behavior:
- Undo activates exact parent snapshot;
- Redo activates exact selected child while branch is intact;
- accepting a new command after Undo discards Redo descendants from the active branch;
- preview/cancel has no history node;
- save only committed stable nodes.

Memory optimization may later checkpoint/delta history only if exact hash restoration remains proven by tests. Unlimited ordinary Undo/Redo is a product contract; optimization may not impose a visible shallow cap.

---

# 10. Solver architecture

Solver is a headless client of Domain Core, not a parallel reimplementation.

## State key
Use Phase-4 causally relevant semantic state only. Exclude history ancestry, presentation, camera, cursor, animation and save metadata.

## Transition generator
Generate legal semantic actions from Domain Core:
- frame/object observation commits reachable from current semantic interaction state;
- player semantic navigation transitions;
- legal object slot moves;
- global interactions.

Preview is not a solver action because it is non-mutating.

## Search
Default exact search: BFS for shortest semantic command distance on ordinary cases unless profiling proves another complete deterministic strategy more practical. Tooling may add A*/bidirectional modes only with admissible/documented behavior; shippable validation must remain reproducible.

Metrics required per Phase 5:
- canonical states visited;
- transitions expanded;
- duplicate states pruned;
- shortest semantic command length;
- solution count up to configured cap;
- termination reason;
- wall-clock diagnostic time;
- peak frontier size / approximate memory;
- shortcut-bot outcome set.

Initial authoring budget profile:
- ordinary target <=150,000 states;
- <=1,500,000 transitions;
- <=5 s optimized headless target on CI-class hardware;
- named late/capstone profile may use <=5x ordinary only after review.

The time target is instrumentation guidance, not a rule that changes puzzle semantics.

---

# 11. V1–V8 validator pipeline

One headless command must be able to validate one case, a band, demo, or all content.

## V1 Schema
Resolve all IDs/types/versions; reject undeclared/private callbacks and invalid form/pose/frame dependencies.

## V2 Reachability
Validate initial state and authored required frame/region/object reachability over at least one canonical solution.

## V3 Candidate determinism
Enumerate reachable relevant frame/object states within budget; same canonical inputs must yield same candidate/rejection.

## V4 Solver termination/instrumentation
Run exact solver and emit required metrics/budget status.

## V5 Shortcut policies
Run Phase-5 declared cheap-policy bots and authored policy assertions.

## V6 Causal diversity
At campaign aggregation level calculate family-window quotas, causal skeleton vectors and near-isomorphism flags.

## V7 Accessibility lint
Data/presentation metadata may not encode mandatory state only by color/audio or require precision free-camera/pointer semantics.

## V8 Presentation-dependency lint
Reject gameplay data references to renderer visibility, pixels, camera transforms, animation frame or physics callback order.

Validation output is machine-readable JSON plus concise human report. Non-zero exit status on hard failure. No email/notification behavior exists in validator/CI.

---

# 12. Persistence model

Persistence is generation-based and committed-boundary-only.

Recommended files:
- `profile_A.dat` / `profile_B.dat` or equivalent alternating generations;
- optional tiny manifest identifying preferred generation;
- settings separated from active case branch when useful;
- backup generation retained until newer generation verifies.

Each durable generation contains:
- format/schema version;
- monotonic save generation number;
- build/content compatibility metadata;
- profile progression facts;
- current case committed canonical branch/head snapshot;
- required Undo/Redo branch data within chosen persistence scope;
- command retry/idempotency metadata needed after recovery;
- checksum/hash over payload.

## Atomic write sequence
1. serialize immutable committed snapshot to temp/new generation;
2. flush/close file;
3. read back and verify format + checksum/hash + invariants;
4. atomically promote/rename where platform semantics permit;
5. update small manifest only after verified generation exists;
6. retain prior verified generation as backup.

A half-written newer generation is never accepted merely because its timestamp is newer.

## Recovery
On boot/load:
- enumerate recognized generations;
- validate from newest generation number downward;
- select newest fully verified compatible committed generation;
- if primary/preferred fails and backup succeeds, recover backup and surface Phase-6 plain notice;
- never combine pieces of two active puzzle generations into one topology/state/history branch.

---

# 13. Fault-injection persistence suite

Implementation must support deterministic test faults at:
- before temp write;
- mid-write/truncated payload;
- after write before flush/close;
- after verify before promotion;
- after promotion before manifest update;
- during manifest write;
- corrupted checksum;
- syntactically valid but invariant-invalid state;
- unsupported future schema;
- missing primary with valid backup.

Every fault must recover either exact earlier committed state or exact later fully committed state, never a hybrid.

Save writes must never capture `PREVIEWING` presentation-only state or in-between transformation animation.

---

# 14. Steam Cloud divergence policy

Steam Cloud is an optional transport of verified local save files, not authority over puzzle merge semantics. Current Steamworks documentation confirms Cloud/Auto-Cloud replicate configured files around sessions; the game must therefore make its local files independently safe and cross-platform compatible.

Hard rule: **never structurally merge two divergent active puzzle history branches.**

On divergence where two verified generations descend from different active case heads:
- compare explicit generation/build/profile metadata;
- merge only separately declared monotonic/commutative profile facts (e.g. union of case-clear IDs, tutorial acknowledgements, accessibility-independent achievement facts) when safe;
- do not union/replay active case commands from both branches;
- retain one active branch chosen by a transparent conflict policy/UI or safest newer known generation, preserving the other as recoverable conflict copy where feasible;
- if conflict handling cannot be made reliable for release, ship offline/local saves without promising Cloud, as Phase 7 explicitly permits.

Machine-specific graphics settings are excluded from Cloud synchronization. Input/accessibility settings may sync only when device-safe; device-specific bindings must not leave another device unrecoverable.

---

# 15. Demo -> full import

Demo and full campaign are different content identities; no active demo puzzle state becomes a campaign branch.

Versioned import payload may contain only:
- language;
- accessibility settings;
- safe input remaps;
- tutorial acknowledgement facts;
- demo completion/achievement-compatible facts;
- `demo_veteran` monotonic flag.

Import rules:
1. detect compatible demo profile;
2. show/perform documented one-time import path as platform product flow permits;
3. normalize values through current full-game schema;
4. merge only whitelisted monotonic/settings categories;
5. record import source/version and idempotency token;
6. repeated import produces no duplicate side effect;
7. any malformed/incompatible category is skipped safely;
8. full-game C01 begins as uncleared unless actually cleared in full campaign.

Import failure can never block New Game.

---

# 16. Input abstraction / semantic focus

Raw devices map to semantic actions before gameplay/UI logic.

Action vocabulary includes:
- `MOVE_*` / navigation;
- `CAMERA_*` presentation-only look;
- `INTERACT_CONFIRM`;
- `CANCEL_BACK`;
- `TARGET_PREV` / `TARGET_NEXT`;
- `INSPECT_MEMORY`;
- `UNDO`;
- `REDO`;
- `RESTART_CASE`;
- `PAUSE`.

Domain receives semantic intents/IDs, never raw scancodes, pixels or analog-stick coordinates for puzzle authority.

Each Observation Frame exposes a deterministic authored semantic target ordering filtered by current legality. Controller/keyboard cycling uses that list. Pointer selection resolves screen hit to an already-known semantic object ID and must produce the same domain action.

Steam Input may be supported as platform-level convenience; native gamepad/keyboard paths remain complete. Current Steam Deck docs support major input APIs and recommend game-appropriate controller/trackpad/gyro use; Last Known Shape does not require Deck-specific precision controls.

Remap validation enforces recoverable Confirm, Cancel, navigation and Pause bindings before accepting a configuration.

---

# 17. Presentation synchronization

After a domain transaction commits, Presentation receives an ordered semantic event bundle such as:
- `memory_committed`;
- `observation_ended`;
- `physical_form_changed`;
- `receiver_changed`;
- `mechanism_changed`;
- `access_changed`;
- `case_won`.

Presentation may animate these sequentially for comprehension, but the canonical post-state already exists at the stable boundary. Skipping animation jumps to exact final representation.

Reduced-motion mode uses alternate presentation recipes only; it never changes event ordering or timing of semantic availability.

If Presentation crashes/reloads mid-animation, rebuilding from canonical snapshot must recreate the correct final world without replaying gameplay mutation.

---

# 18. Content and localization architecture

Gameplay definitions are separated from localized/presentation resources.

Recommended directories conceptually:
```text
domain/global_rules/
content/cases/
content/object_defs/
content/forms/
content/frames/
content/receivers/
presentation/themes/
localization/
tests/fixtures/
tools/validator/
platform/
```

All player strings referenced by localization keys. Case data stores `hint_fact_id`/teaching IDs, not embedded English as authority.

Localization build lint verifies:
- key existence;
- placeholder compatibility;
- no gameplay-critical text baked only into textures;
- glossary canonical terms;
- layout test fixtures at +40% expansion for critical Frame comparison surfaces.

Content loading fails loudly in development/CI on unresolved gameplay IDs; shipping build must never silently substitute a gameplay form/rule due to missing content.

---

# 19. Performance / memory targets

The game is reasoning-heavy, not simulation-heavy. Performance priorities are stable frame pacing and instantaneous semantic response.

Baseline targets for representative 1280x800 Deck-class hardware:
- 60 fps target during ordinary play where presentation scope supports it;
- never below a stable 30 fps fallback due to required gameplay simulation;
- semantic command validation/commit normally <16 ms excluding optional cosmetic animation and autosave I/O;
- preview candidate query normally <4 ms;
- Undo/Redo state restore normally <50 ms;
- autosave performed without blocking ordinary input for a visually noticeable period; target <100 ms main-thread blocking, with serialization/write strategy adjusted if exceeded;
- ordinary loaded case canonical state <<10 MB; domain state should normally be orders of magnitude smaller;
- history memory budget target <=64 MB per active ordinary case before optional compression/checkpointing;
- no runtime solver is required for normal play/hints, avoiding solver spikes on Deck;
- loading a case should target <=2 s on Deck-class storage after initial shader/cache warm state, subject to prototype profiling.

These are engineering targets, not promises that justify changing puzzle rules. Representative scene/render budgets are set during vertical slice from measured GPU/CPU data.

---

# 20. Headless test / CI hooks

Required CLI/headless operations:
- validate all case schemas;
- run one/all V1–V8 pipelines;
- run domain acceptance fixtures;
- replay deterministic command fixture and compare semantic hashes;
- run Undo/Redo branch fixture;
- run save fault-injection matrix;
- run demo-import idempotency fixtures;
- output machine-readable validation metrics;
- exit non-zero on hard failure.

CI policy for eventual dedicated repository:
- run on pushes/PRs as appropriate;
- cache engine/tool assets where safe;
- archive concise failing validator report when useful;
- **no test emails, Gmail messages, release notifications or noisy success notifications**;
- external notification actions are manual unless a future repository policy explicitly says otherwise.

Golden deterministic fixtures must not rely on wall-clock timestamps in semantic hashes.

---

# 21. Implementation order for dedicated repository

## 12A1 — Domain bootstrap
Version pin, pure state records, ID registries, canonical encoding/hash, command envelope, revision/idempotency.

## 12A2 — Core observation vertical core
One object, two forms, one Frame: candidate preview query -> commit -> leave -> physical authority. No polished art required.

## 12A3 — History/persistence skeleton
Exact Undo/Redo, stable snapshots, generation saves, recovery/fault tests.

## 12B — Tiny playable vertical slice
C01-like through a preserve/overwrite mini-sequence with controller + keyboard semantic focus and full causal presentation.

## 12C1 — Remaining mechanics
Object slot moves, receivers/mechanisms, masks/declared occluders, two-object order.

## 12C2 — Solver/validator
Shared Domain transition API, V1–V8, cheap-policy bots, metrics.

## 12D — Content population
Author/import full cases only after domain/validator/presentation empirical gates pass. Never bulk-author around an unproven observation interaction.

## 12E — UX/accessibility/Deck
Full input/remap, Inspect, tutorials/hints, localization, 1280x800/readability, reduced motion/high contrast.

## 12F — Adversarial QA
Persistence/cloud conflicts, malformed content, idempotency, platform failure, performance, accessibility and deterministic replay.

## 12G — Empirical gates
EG7/EV7 gates from prior specs: hook comprehension, form prediction, mature variety, two-object readability, reduced-motion/non-audio causality, duration/value/demo proof.

## 12H — Release candidate
Packaging, achievements/platform integration, optional Cloud only if safe, demo/full import, regression, final price/content review.

Production implementation remains outside this factory.

---

# 22. Technical acceptance suite — 72 checks

T8-01 Engine baseline is pinned to a stable release, not 4.8-dev preview.
T8-02 Engine upgrade requires regression and rollback point.
T8-03 Domain Core can run headlessly without Presentation/Steam.
T8-04 Domain imports no scene-tree/render authority.
T8-05 Presentation cannot mutate canonical state directly.
T8-06 Platform outage cannot block offline campaign.
T8-07 Durable IDs are symbolic/stable, not engine instance IDs.
T8-08 Every persisted root is versioned.
T8-09 Unknown incompatible schema cannot silently default gameplay authority.
T8-10 Case gameplay has no private script callback semantics.
T8-11 Canonical object state stores pose/remembered/physical form exactly.
T8-12 Preview/camera/focus are excluded from puzzle canonical state.
T8-13 Canonical collections serialize in stable ID order.
T8-14 Candidate is a pure Domain function.
T8-15 Candidate never samples framebuffer/pixels.
T8-16 Candidate never depends on free camera transform.
T8-17 Candidate never depends on animation/frame delta.
T8-18 Preview and commit on identical revision return identical candidate.
T8-19 Mutating command validates immutable pre-state.
T8-20 Rejection cannot leak partial canonical mutation.
T8-21 Accepted command increments revision once.
T8-22 Deterministic immediate consequences belong to same transaction boundary.
T8-23 Receiver/mechanism ordering is stable by declared priority/ID.
T8-24 Same command ID + same payload is idempotent.
T8-25 Same command ID + different payload hard-rejects.
T8-26 Stale revision rejects before mutation.
T8-27 Solver equivalence excludes revision/history ancestry.
T8-28 Semantic hash excludes presentation state.
T8-29 Canonical hash is stable across repeated identical runs.
T8-30 Undo restores exact parent semantic hash.
T8-31 Redo restores exact child while branch exists.
T8-32 New command after Undo truncates active Redo descendants.
T8-33 Preview/Cancel creates no history node.
T8-34 Unlimited ordinary Undo is not replaced by a tiny visible history cap.
T8-35 Solver calls shared Domain transitions rather than duplicate rules.
T8-36 V1 rejects unresolved IDs/private callbacks.
T8-37 V2 checks intended authored reachability.
T8-38 V3 checks deterministic candidate results.
T8-39 V4 emits states/transitions/duplicates/solution metrics/termination.
T8-40 V5 executes declared cheap-policy checks.
T8-41 V6 computes campaign diversity/near-isomorphism.
T8-42 V7 can fail accessibility-invalid metadata.
T8-43 V8 rejects renderer/camera/animation authority.
T8-44 Ordinary over-budget case is simplified/cut, not given bespoke semantic pruning.
T8-45 Save occurs only at committed stable boundary.
T8-46 Save generation has integrity hash/checksum.
T8-47 New generation is verified before becoming preferred.
T8-48 Prior verified generation survives until newer promotion succeeds.
T8-49 Truncated newest save recovers older verified generation.
T8-50 Corrupt checksum cannot become active state.
T8-51 Invariant-invalid syntactically valid save rejects.
T8-52 Recovery never hybrids two generations.
T8-53 Mid-animation load reconstructs from canonical committed state.
T8-54 Cloud transport never structurally merges divergent active puzzle branches.
T8-55 Cloud may merge only explicitly commutative/monotonic profile facts.
T8-56 Graphics/device-specific settings are not blindly Cloud-synced.
T8-57 Game can ship without Cloud if conflict safety is unproven.
T8-58 Demo import never marks C01–C06 clear by inference.
T8-59 Demo import is versioned and idempotent.
T8-60 Demo import failure cannot block New Game.
T8-61 Raw pointer/analog coordinates never decide candidate form.
T8-62 Controller target cycle uses deterministic semantic target list.
T8-63 Keyboard-only path reaches every core action.
T8-64 Remap validator prevents unrecoverable Confirm/Cancel/navigation/Pause loss.
T8-65 1280x800 target does not require runtime solver/UI table for puzzle reasoning.
T8-66 Localization keys are separate from gameplay authority.
T8-67 +40% critical-text expansion has automated/manual layout fixtures.
T8-68 Reduced motion changes presentation only, not semantic event order.
T8-69 Headless validation returns non-zero on hard failure.
T8-70 CI test harness sends no email/Gmail notifications.
T8-71 Production content population waits until vertical observation/readability gate passes.
T8-72 No production implementation is started inside the factory repository.

---

# 23. Phase-8 result

**PHASE 8 — TECHNICAL IMPLEMENTATION SPECIFICATION: COMPLETE ON PAPER.**

The implementation path is deterministic and bounded: Godot 4.7.2-stable initial pin; GDScript-first; strict Domain/Presentation/Platform separation; canonical versioned state and stable hashes; atomic semantic transactions; exact history/idempotency; shared-domain solver/validator; verified generation persistence; non-merging Cloud policy; safe demo import; semantic input/focus; localization; Deck-class targets; headless CI hooks; and 72 technical acceptance tests.

No paper-level technical blocker prevents Phase 9.

## NEXT ACTION
Phase 9 — Whole-Game Simulation on Paper. Walk the frozen game from first boot through C34/post-clear plus hostile legal/error/recovery/platform states. Simulate at minimum: first 10 minutes; overwrite literacy; C11 dynamic input; C16–C19 two-object teaching; C23+ mature preservation chains; C34 capstone; blind-enumeration player; excessive Undo/Redo; stale/duplicate command delivery; crash at each save boundary; corrupt newest generation; Cloud-divergent devices; demo->full import/re-import; controller-only/keyboard-only; Deck 1280x800 + text expansion; reduced-motion/non-audio; localization expansion; solver-budget exceedance. Record contradictions as explicit P9 repairs and do not advance to Phase 10 until reconciled.