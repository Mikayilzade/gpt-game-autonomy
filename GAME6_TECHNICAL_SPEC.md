# GAME #006 — STITCHSPACE — TECHNICAL IMPLEMENTATION SPECIFICATION

Last updated: 2026-08-29
Factory run: **9**
Phase: **8 — Technical Implementation Specification**
Selected concept: **G6C01 Stitchspace**
Product thesis: **LOCKED**
Mechanical architecture: **COMPLETE ON PAPER**
Content architecture: **COMPLETE ON PAPER**
UX / Presentation Architecture: **COMPLETE ON PAPER**
Economy / Retention / Commercial Model: **COMPLETE ON PAPER**
Technical implementation specification: **COMPLETE ON PAPER**
Production implementation started: **NO**
DESIGN COMPLETE: **NO**

This file freezes implementation architecture without starting production code. It exists to preserve Stitchspace's actual design during implementation: deterministic authored topology replacement in a physical room-stage, not free portal placement, real-time physics, scene-tree authority or presentation-driven logic.

Current engine reference checked 2026-08-29: Godot **4.7.2-stable**, released 2026-08-18, is the current stable 4.x maintenance release. Godot 4.8 remains development-only. Initial implementation therefore pins **Godot 4.7.2-stable** rather than following dev snapshots.

---

# 1. Runtime / engine direction

## 1.1 Frozen initial stack

- Godot **4.7.2-stable** pinned for initial implementation.
- Standard desktop build, PC/Steam first.
- GDScript-first unless a measured bottleneck later justifies a native extension.
- 2D `Control` / `CanvasItem`-centric presentation preferred for the first implementation because canonical gameplay is discrete room/node topology and requires strong UI/readability/Deck support, not authoritative 3D physics.
- A 2.5D/isometric/orthographic visual treatment is presentation freedom only if it preserves stable room frames, socket readability and deterministic focus.
- No physics-body contact callback, render transform, tween position, animation frame, navigation mesh or scene-tree order may decide canonical gameplay.

## 1.2 Engine upgrade rule

Changing engine version after implementation starts requires:
1. clean baseline tests before upgrade;
2. version-control checkpoint;
3. deterministic replay/hash regression before/after;
4. save migration/recovery smoke test;
5. controller/focus and 1280×800 layout regression.

Engine upgrades never silently change frozen mechanics.

---

# 2. Architecture boundaries

Implementation has three strict layers.

## 2.1 Domain Core — gameplay authority

Pure deterministic state and transitions. Owns:
- case definition/state;
- rooms/nodes/sockets/passages/seams/entities;
- topology and reachability facts;
- crossing/orientation mapping;
- occupancy reservations/locks;
- semantic commands;
- automatic mover chains;
- objectives/invariants/mastery predicates;
- transaction history;
- canonical serialization/hash;
- solver/validator-facing transition API.

Domain Core must run headlessly without scenes, audio, renderer, Steam, filesystem UI or input devices.

## 2.2 Presentation Layer — never authoritative

Owns:
- room-stage visual instances;
- camera/focus presentation;
- OLD→NEW preview;
- seam/socket animation;
- HUD, case rail, history, topology overview;
- accessibility rendering;
- audio;
- glyphs;
- animation interpolation.

Presentation receives accepted/rejected domain results and material events. It never mutates canonical state directly.

## 2.3 Platform Adapters

Own external services and device integration:
- filesystem persistence;
- Steam Cloud transport;
- achievements;
- Steam Input/device glyph mapping where used;
- demo/full product identity/import source;
- build/export/platform paths.

Platform failure must not alter gameplay truth or block offline single-player play when local storage works.

---

# 3. Canonical typed data model

All gameplay IDs are stable explicit strings or compact typed IDs; never scene paths or instance IDs.

## 3.1 Content identity

`ContentVersion`
- `schema_version`
- `gameplay_version`
- `content_pack_id`
- `content_pack_version`

`CaseDefinition`
- `case_id`
- content version
- rooms
- local nodes/lanes
- edge sockets
- ordinary passages
- seams + initial endpoint placement
- entities + initial state
- objectives
- hard invariants
- optional mastery predicates
- legal endpoint destination restrictions
- authored focus metadata
- known baseline/mastery solution fixtures
- reasoning skeleton metadata
- lost-adjacency dependency metadata
- rare-three-seam justification if applicable

## 3.2 Room / node / socket

`RoomDefinition`
- `room_id`
- local frame/orientation
- local nodes
- static presentation tags only where non-authoritative

`TraversalNode`
- `node_id`
- `room_id`
- local neighbors
- local facing/lane metadata
- occupancy capacity/class
- optional boundary association

`EdgeSocket`
- `socket_id`
- `room_id`
- boundary orientation
- entry/exit node IDs
- supported crossing class
- enabled-state source
- compatibility tags
- stable focus metadata

`OrdinaryPassage`
- `passage_id`
- endpoint socket/node relation
- fixed directionality
- finite orientation/lane mapping

## 3.3 Seam

`SeamState`
- `seam_id`
- endpoint A socket ID
- endpoint B socket ID
- directionality
- derived finite orientation mapping
- endpoint lock/reservation state

A seam always has exactly two endpoints in every persisted canonical state.

## 3.4 Entity

`EntityState`
- `entity_id`
- entity class
- current room/node
- local facing
- movement state
- current crossing reservation if any
- objective-relevant flags
- deterministic blocker/occupancy state

No authoritative transform/velocity/floating position is stored as gameplay state.

## 3.5 CaseState

Canonical state contains only deterministic facts:
- revision;
- content identity;
- seam placements;
- entity states;
- socket enabled/lock state where derived inputs require storage;
- objective/invariant facts if not cheaply derived;
- case-local globally defined interaction flags;
- emitted/consumed one-shot semantic events if idempotency requires them;
- history cursor metadata outside the hashed gameplay payload where appropriate.

Presentation selection, camera, open panels, animation progress and audio do not belong in the domain hash.

---

# 4. Semantic command envelope

Every domain mutation arrives through:

`CommandEnvelope`
- `command_id`
- `command_type`
- typed payload
- `expected_revision`
- `expected_state_hash`
- optional local monotonic client sequence for diagnostics only

Required commands include at minimum:
- `MOVE_SEAM_ENDPOINT`
- player/local entity movement commands
- explicit globally defined interaction commands
- Undo
- Redo
- Restart Case

## 4.1 Idempotency

Accepted command IDs are recorded in the active transaction/replay window. Re-submitting the same command ID with the same precondition returns the recorded result without applying it again. Reuse with conflicting payload is rejected.

## 4.2 Stale state

Revision/hash mismatch rejects before mutation with a stale-state result. UI then refreshes from canonical state.

## 4.3 `MOVE_SEAM_ENDPOINT`

Implementation must follow the exact Phase-4 validation/commit order. The transaction is indivisible:
- old adjacency removed;
- selected endpoint relocated;
- new adjacency created;
- finite orientation mapping recomputed;
- deterministic consequences resolved;
- one new committed checkpoint produced.

No save/history/render-visible gameplay state may contain both old+new adjacency or a one-ended seam.

---

# 5. Deterministic resolver

## 5.1 General transaction order

For one accepted semantic action:
1. validate envelope and immutable pre-state;
2. commit direct requested domain mutation;
3. derive automatic movement/crossing intents from one shared canonical state;
4. group disjoint simultaneous intents;
5. reject invalid authored contention rather than resolve it by object/scene/hash iteration order;
6. resolve finite crossing/orientation/occupancy effects;
7. apply blocker/objective consequences;
8. continue deterministic active movers;
9. stop at settle or 24-step chain ceiling;
10. evaluate completion/mastery in settled state;
11. produce material event list + canonical post-state/hash;
12. create one transaction checkpoint.

## 5.2 Simultaneous intent contract

Stable IDs may sort already-independent events for serialization/log readability. They may never choose a winner when two entities compete for one exclusive boundary/node. Such a reachable state is a content/compiler error unless a future frozen global rule defines the physical result.

## 5.3 Chain ceiling

Maximum automatic movement/crossing steps per accepted action: **24**.

On limit:
- finish no partial collision/crossing group;
- enter deterministic `CHAIN_LIMIT_REACHED` safe state/result;
- record reproducible diagnostics;
- shipped known solutions may not require the ceiling.

---

# 6. Canonical serialization and hash

Canonical serialization must be independent of:
- dictionary/hash iteration order;
- scene order;
- resource load order;
- locale;
- wall-clock time;
- float formatting;
- renderer state.

Rules:
1. explicit schema version;
2. UTF-8;
3. stable field order;
4. collections sorted by stable typed ID unless domain order is itself meaningful;
5. enums serialized by frozen symbolic/integer value;
6. no unnecessary floating-point gameplay fields;
7. derived presentation-only fields omitted;
8. canonical hash uses a standard cryptographic digest available consistently in runtime/tooling (SHA-256 acceptable).

Determinism gate: same CaseDefinition + same initial state + same semantic command sequence = exactly same canonical state bytes/hash and material event sequence across repeated runs on supported desktop/headless targets.

---

# 7. Undo / Redo

Undo is checkpoint restoration, never inverse simulation.

`HistoryEntry`
- parent canonical checkpoint/hash;
- accepted semantic command envelope;
- exact canonical post-checkpoint/hash;
- material event summary for presentation/debugging.

Rules:
- one accepted semantic action + all automatic consequences = one history entry;
- structural rejection creates no entry;
- Undo restores exact parent state;
- Redo restores/replays only the intact stored child transaction after pre-state/hash verification;
- new accepted action after Undo truncates Redo branch;
- Restart returns to canonical case initial checkpoint;
- raw Undo count is not mastery/scoring state.

Implementation may use snapshots, structural sharing or event-assisted snapshots, but externally observable behavior must be exact checkpoint restoration.

---

# 8. Content compiler / validator / solver hooks

Authoring data must compile into immutable runtime `CaseDefinition` data before shipping.

Compiler/validator checks include:
- unique IDs and valid references;
- 2–5 normal room budget / explicit exception handling;
- legal socket counts;
- valid finite orientation/lane mapping for every reachable seam pair;
- no duplicate endpoint occupancy;
- no same-step unresolved contention;
- no unordered side-effect dependency;
- seam count budgets and required three-seam justification;
- declarative objective/invariant validity;
- known baseline fixture exists and completes;
- known mastery fixture where mastery exists;
- C34 reachability independent of mastery/remix profile state;
- no direct-current-room-to-goal shortcut where Phase-5 data forbids it;
- `lost_adjacency_dependency` requirements;
- reasoning-skeleton / anti-isomorphism windows;
- remix changed-causal-dependency proof;
- state-space/reachable-state thresholds from Phase 5;
- no new case-local gameplay callbacks or portal-like free placement.

## 8.1 Solver API

The solver uses the same Domain Core transition functions as runtime, never a simplified second rules implementation.

Must support:
- BFS/appropriate bounded search over canonical hashes for tractable cases;
- known solution replay validation;
- shortest-path or bounded-path measurements where relevant;
- alternate-solution skeleton classification metadata;
- dead-end exploration for authoring only;
- regression fixtures saved as semantic command sequences.

Solver hints are not automatically player hints.

---

# 9. Persistence

Three conceptual persistent domains stay separated:

## 9.1 Settings
Device/user presentation settings, controls, accessibility, language and audio/display choices. Device-specific display settings should not blindly Cloud-merge across hardware.

## 9.2 Profile progress
Monotonic facts:
- main case clears;
- mastery clears;
- remix clears;
- tutorial/help discovery;
- achievements/progression facts;
- demo-import provenance/version.

## 9.3 Active case / recovery
Exact one-branch canonical checkpoint/history needed to resume the current case.

## 9.4 Save envelope

Every persisted file uses:
- magic/product ID;
- schema version;
- gameplay/content version;
- payload type;
- monotonic local save generation;
- payload length where useful;
- payload checksum/hash;
- payload.

Write protocol:
1. serialize complete candidate generation;
2. write temp file;
3. flush/close;
4. reopen/validate checksum/schema;
5. preserve previous valid primary as backup generation;
6. atomically replace/promote primary where platform semantics permit;
7. only then tell UX save succeeded.

Recovery order evaluates newest **valid** compatible generation, not merely newest timestamp. Corrupt/incompatible candidates fall back to verified backup/safe checkpoint with explicit recovery messaging.

Never persist:
- half of a seam move;
- half of a crossing group;
- unresolved automatic chain;
- a history cursor that references missing checkpoint data.

## 9.5 Fault injection

Automated persistence tests inject failure after every write/promote stage and prove recovery yields either exact previous committed state or exact new committed state, never a hybrid.

---

# 10. Steam Cloud / cross-device conflict policy

Cloud is transport, never gameplay authority.

Profile progress may merge monotonically when schema/content compatibility is proven:
- cleared = union;
- mastery/remix = union;
- tutorial/help facts = union where safe.

Active case branches do **not** merge structurally.

If two devices have diverged active-case branches:
- preserve both candidate save generations locally where possible;
- choose one active branch using explicit freshness/known-valid metadata and user-facing conflict selection when necessary;
- never synthesize seam placements/history from both branches;
- profile monotonic progress can still merge independently.

Cloud unavailable/offline: local save/load/completion continues normally.

---

# 11. Demo → full import

Demo and full product use explicit versioned mapping, not name guessing.

`DemoImportMap`
- demo product/schema version range;
- full product/schema target;
- explicit demo case/tutorial/progress fact → full equivalent fact mapping;
- compatible settings mapping;
- unsupported facts ignored with diagnostics.

Rules:
- import is monotonic;
- import is idempotent;
- replaying import cannot duplicate achievements/progress;
- no active demo case state is assumed equivalent to a full-game case unless explicitly mapped;
- settings can import independently of gameplay progress;
- a failed/incompatible import never damages existing full-game profile/save.

---

# 12. Input and deterministic focus architecture

Input devices emit semantic actions. Domain Core never reads physical key/button codes.

Minimum semantic actions:
- move/navigate player;
- Interact;
- select seam / endpoint;
- next/previous seam where relevant;
- next/previous valid target;
- Confirm;
- Cancel;
- Inspect;
- Topology Overview;
- Undo;
- Redo;
- Pause/Resume;
- Step;
- major UI navigation.

Focus graph is authored/compiled semantic data:
- required interactables reachable by keyboard/controller;
- stable authored priority + stable ID tie-break for already equivalent candidates;
- no nearest-pixel/floating-position calculation as authoritative focus order;
- camera zoom/animation/layout cannot change the semantic target cycle;
- pointer may choose a semantic target directly, but result uses the same action pipeline.

Remapping and `Reset Controls` remain available even after an unusable mapping.

---

# 13. Localization / pseudolocalization readiness

All player-facing text uses localization keys; no gameplay logic compares translated strings.

Required implementation readiness:
- UTF-8 text pipeline;
- locale-independent canonical serialization;
- dynamic layout containers instead of fixed English pixel widths where practical;
- pseudolocalization target around +30–40% expansion plus accented/wide glyph stress;
- UI-scale combinations tested with pseudolocalization at 1280×800;
- socket/seam/entity identity never depends on abbreviated English labels alone;
- controller glyphs and localized labels remain distinct data.

Initial shipped language set is a later commercial/release decision; architecture must not make English-only assumptions.

---

# 14. Performance / target budgets

These are implementation budgets, not a promise of exact hardware certification.

Target gameplay scene complexity is deliberately bounded: <=6 rooms, <=12 exposed sockets, <=3 seams, <=4 material entities in normal frozen content.

## 14.1 Runtime targets

At 1280×800 Deck-class presentation:
- target 60 FPS ordinary play;
- 30 FPS must not change deterministic outcomes;
- domain transaction excluding solver should normally complete within one frame-budget-scale on target hardware; heavy authoring solver never runs synchronously during ordinary play;
- ordinary seam preview/focus update should feel immediate;
- no unbounded background simulation.

## 14.2 Domain budgets

- no per-frame domain simulation when canonical state is settled;
- canonical resolver complexity bounded by small authored graph + 24 movement-step ceiling;
- runtime reachability checks cache safely or recompute from small graph;
- solver/state-space work is editor/headless/offline tooling except explicitly cheap hint facts.

## 14.3 Memory/loading

Cases are compact data resources. Prefer loading one active case plus lightweight Case Board metadata rather than retaining all room scenes live. No streaming/open-world system required.

Performance degradation must never be “fixed” by changing canonical rules.

---

# 15. Headless / deterministic tooling

Repository implementation should expose one documented headless test entrypoint capable of running without presentation scenes.

Required suites:
- Domain unit tests;
- canonical serialization/hash tests;
- command idempotency/stale-state tests;
- crossing/orientation table tests;
- simultaneous-intent contention tests;
- Undo/Redo exactness;
- chain-limit tests;
- content compiler validation;
- known solution/mastery fixture replay;
- anti-isomorphism reports;
- persistence fault injection;
- demo import idempotency;
- save migration fixtures;
- deterministic fuzz/property tests over small valid authored states.

Golden tests must store semantic inputs/expected hashes or structured expected facts, not screenshots as gameplay authority.

---

# 16. Reproducible support bundle

A user/dev bug-report bundle may contain:
- game/build version;
- engine version;
- platform/device class;
- case/content version;
- initial checkpoint hash;
- semantic command history since checkpoint;
- current canonical hash/revision;
- material event summaries;
- persistence generation metadata/checksum status;
- input device/action-map metadata where relevant;
- relevant settings excluding secrets/personal paths where possible.

It should exclude unnecessary personal data and never require raw Steam credentials/tokens.

A reported domain bug should be reproducible by feeding the support replay into headless Domain Core.

---

# 17. Implementation order — Phase 12A–12H

## 12A Technical Bootstrap
- pin Godot 4.7.2-stable;
- project boots to non-gameplay shell;
- Domain Core independent of scenes;
- typed IDs/content versions;
- canonical serialization/hash;
- semantic command envelope;
- minimal rooms/nodes/socket/seam/entity model;
- one endpoint replacement fixture;
- headless tests;
- persistence envelope skeleton;
- semantic input registry.

Exit: repeated identical fixture sequence = identical hash; stale/duplicate command path testable.

## 12B Vertical Slice
Implement DEMO01–DEMO03-like loop:
- room-stage;
- one seam;
- endpoint selection/move;
- OLD→NEW preview;
- physical crossing;
- orientation consequence;
- useful old-adjacency loss;
- Undo/Redo;
- keyboard/controller semantic focus;
- durable recovery.

Exit: playable end-to-end without graph editor/free portal placement; presentation cannot affect domain hash.

## 12C Core Systems
- all Phase-4 crossing/occupancy/mover rules;
- one/two/rare-three seams;
- ordinary passages;
- objectives/invariants/mastery predicates;
- Pause/Step canonical boundaries;
- chain ceiling;
- exact history.

## 12D Content Population
- C01–C34;
- DEMO01–DEMO05;
- target R01–R08;
- known solution/mastery fixtures;
- compiler/solver reports and anti-isomorphism checks.

## 12E UX / Accessibility / Controller / Deck
- all Phase-6 player paths;
- authored focus graph;
- 1280×800 readability;
- remapping/reset;
- reduced motion/high contrast;
- pseudolocalization/layout stress.

## 12F Adversarial QA
Attack duplicates/stale commands, endpoint locks, contention, save crashes, branch history, Cloud divergence, demo import, focus reachability, malformed content and accidental portal-like bypasses.

## 12G Empirical Gates
Run retained product/UX/commercial playtest gates. Human/readability/value findings remain empirical and may not be fabricated by automation.

## 12H Release Candidate
Regression, packaging/export, performance, persistence migration/recovery, demo/full integration, platform adapter and release-safe empirical decisions.

Implementation reports `IMPLEMENTATION COMPLETE = YES` only when all required gates are actually satisfied.

---

# 18. Phase-8 acceptance tests

### Engine / boundaries
- **T8-01** Initial project pins Godot 4.7.2-stable or records an explicit later approved migration.
- **T8-02** Domain Core tests run without loading presentation scenes.
- **T8-03** Renderer/tween/physics-contact order cannot mutate canonical state.
- **T8-04** Platform service failure cannot change puzzle rules.

### Data model
- **T8-05** Every gameplay object uses stable explicit IDs, never scene instance identity.
- **T8-06** A persisted seam always has exactly two endpoints.
- **T8-07** Canonical EntityState contains no authoritative free-body velocity/transform.
- **T8-08** Presentation-only state is excluded from canonical hash.

### Commands / determinism
- **T8-09** Every mutation uses a semantic command envelope with ID + expected revision/hash.
- **T8-10** Duplicate accepted command cannot apply twice.
- **T8-11** Conflicting reuse of command ID rejects.
- **T8-12** Stale revision/hash rejects before mutation.
- **T8-13** Endpoint replacement exposes no intermediate canonical one-ended or double-adjacency seam.
- **T8-14** Same fixture+commands repeated 1,000 times produces identical canonical hashes/events.
- **T8-15** Supported headless and presentation builds agree on domain hash for same replay.

### Movement / contention
- **T8-16** Crossing orientation is derived from finite authored socket frames only.
- **T8-17** Endpoint lock prevents relocation during canonical crossing reservation.
- **T8-18** Disjoint simultaneous intents have order-independent final state.
- **T8-19** Exclusive contention with no global rule is rejected as invalid content, not ID-ranked.
- **T8-20** 24-step ceiling produces deterministic safe result with no partial group persistence.

### History
- **T8-21** One semantic action + automatic consequences produces one history transaction.
- **T8-22** Structural rejection produces no history mutation.
- **T8-23** Undo restores byte-equivalent canonical checkpoint/hash.
- **T8-24** Redo restores exact intact branch.
- **T8-25** New accepted command after Undo truncates Redo branch.

### Content tooling
- **T8-26** Compiler rejects duplicate IDs/broken references.
- **T8-27** Compiler rejects non-unique reachable seam orientation mapping.
- **T8-28** Compiler rejects unresolved same-step contention.
- **T8-29** Every shipped main/demo/remix case has validated known baseline solution.
- **T8-30** Mastery content with a mastery predicate has a validating mastery fixture.
- **T8-31** Phase-5 lost-adjacency and anti-shortcut constraints are machine-checkable where specified.
- **T8-32** Reasoning-skeleton/anti-isomorphism report is generated for required campaign windows.
- **T8-33** Remix changed-causal-dependency metadata/report is enforced.
- **T8-34** Three-seam case without justification fails compile/release validation.

### Persistence
- **T8-35** Save envelope validates schema/content/checksum before use.
- **T8-36** Fault injection at every save stage recovers exact old or exact new committed generation, never hybrid.
- **T8-37** No unresolved crossing/mover chain is persisted as an accepted resume point.
- **T8-38** Corrupt newest generation falls back to verified compatible backup.
- **T8-39** UI save-success indicator occurs only after durable validation/promotion.

### Cloud / demo import
- **T8-40** Offline local save/clear works with platform services unavailable.
- **T8-41** Compatible profile clear/mastery/remix facts merge monotonically.
- **T8-42** Divergent active-case branches never synthesize a hybrid topology/history.
- **T8-43** Demo import uses explicit versioned mapping.
- **T8-44** Repeating demo import is idempotent.
- **T8-45** Failed/incompatible demo import cannot damage existing full-game progress.

### Input / localization
- **T8-46** Domain receives semantic actions, not physical key/button codes.
- **T8-47** Required keyboard/controller focus order is independent of camera geometry/animation/hash iteration.
- **T8-48** Pointer and controller activation of same target produce the same semantic command.
- **T8-49** Reset Controls remains reachable after unusable remap.
- **T8-50** Gameplay logic never compares localized strings.
- **T8-51** Pseudolocalized +40% text at 1280×800 does not hide mandatory case controls/status in supported UI-scale range.

### Performance / support
- **T8-52** Settled case performs no required per-frame domain simulation.
- **T8-53** Heavy solver/search never blocks ordinary runtime input/render path.
- **T8-54** Changing presentation FPS/speed does not alter canonical replay outcome.
- **T8-55** Support replay bundle can reproduce a domain issue headlessly from checkpoint + semantic commands.
- **T8-56** Support bundle excludes platform credentials/tokens.

### Implementation readiness
- **T8-57** A fresh implementer can identify the authoritative Domain/Presentation/Platform boundaries without invention.
- **T8-58** A fresh implementer can build Phase 12A without choosing new gameplay rules.
- **T8-59** A fresh implementer can implement persistence/Undo/Cloud conflict behavior without inventing merge semantics.
- **T8-60** No technical section grants implementation permission to add free portal placement, real-time physics authority, arbitrary room rotation, graph-editor gameplay or timing-dependent seam relocation.

---

# 19. Phase-8 closure

- engine/runtime direction frozen: **YES**
- Domain / Presentation / Platform separation frozen: **YES**
- canonical typed data model frozen: **YES**
- semantic command/idempotency contract frozen: **YES**
- crossing/orientation/occupancy/mover resolution frozen: **YES**
- canonical serialization/hash frozen: **YES**
- Undo/Redo checkpoint contract frozen: **YES**
- compiler/validator/solver hooks frozen: **YES**
- local persistence/recovery/fault boundaries frozen: **YES**
- Steam Cloud conflict contract frozen: **YES**
- demo→full import contract frozen: **YES**
- input/focus implementation contract frozen: **YES**
- localization/pseudolocalization readiness frozen: **YES**
- performance/headless testing budgets frozen: **YES**
- support/replay bundle frozen: **YES**
- Phase 12A–12H implementation order frozen: **YES**
- Phase-8 acceptance tests: **60**
- production implementation started: **NO**
- DESIGN COMPLETE: **NO**

## NEXT PHASE

**Phase 9 — Whole-Game Simulation on Paper.**

Simulate the complete experience from first boot through C34/post-clear, including hostile/legal-bad states, persistence/recovery, controller/Deck, demo→full transition, likely repetition/dominant strategies, state-space/readability pressure and commercial-value pacing. Repair contradictions with the smallest canonical amendments and preserve them explicitly for Phase 10/11.
