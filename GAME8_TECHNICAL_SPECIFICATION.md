# GAME #008 — TECHNICAL IMPLEMENTATION SPECIFICATION

Last updated: 2026-08-30
Phase: **8 — Technical Implementation Specification**
Selected concept: **G8C02 Locksmith's Margin**
Working title: **Locksmith's Margin**
Production implementation started: **NO**

This document is implementation authority, not production code. It translates the Phase 3–7 design into deterministic software boundaries that a later dedicated implementation repository can execute without inventing gameplay.

---

# 1. Implementation baseline

## 1.1 Engine/runtime decision
Initial implementation baseline: **Godot 4.7.2-stable, GDScript-first**.

Reasoning:
- the game is a compact single-station 3D/2.5D tactile presentation rather than a large streaming world;
- domain state is tiny and deterministic, so a lightweight engine with strong scene/UI/input tooling is sufficient;
- controller/keyboard/mouse abstraction, desktop export and Linux/Steam Deck targets fit the scope;
- GDScript keeps iteration and test ownership simple for a small project;
- no engine physics feature is required for authoritative gameplay.

Fresh check on 2026-08-30: Godot 4.7.2 is the current stable 4.x maintenance release; 4.8 is still development (`4.8-dev4`). Therefore do **not** baseline on 4.8 preview builds.

Upgrade policy: implementation may move to a later **stable** 4.x only after a dedicated migration/regression pass proves identical domain tests, save migration, controller focus behavior and target-device performance. Never upgrade because a preview has a desirable rendering feature.

## 1.2 Rendering direction
- 3D bench and physical artifacts are presentation only.
- authoritative cut depths, lock acceptance, access, knowledge and completion are integer/data state.
- key mesh may be generated/deformed from the key vector for visual fidelity, but mesh geometry is downstream of domain state.
- lock cutaway animation reads an already-computed TEST result; it does not determine the result.
- rigid-body simulation is unnecessary for core authority. Decorative physics, if used, must be non-interactive and non-authoritative.

## 1.3 Runtime product targets
- Windows PC primary shipping target.
- Linux/Steam Deck target from project architecture, not a late port.
- macOS may be supported if release economics/QA permit; it is not required to define puzzle rules.
- offline single-player core must remain fully playable without Steam availability.

---

# 2. Architectural authority boundaries

The project must preserve three hard layers.

## 2.1 Domain Core
Pure deterministic authority. Owns:
- case static data;
- key vectors;
- lock accepted sets;
- access predicates;
- legal action calculation;
- TEST evaluation;
- FILE transition;
- opened-lock state;
- knowledge observations/deductions;
- action history snapshots/deltas;
- Undo/Redo/Restart;
- win state;
- mastery counters derived from history;
- solver/validator state representations;
- save-domain serialization.

Domain Core must be runnable headlessly with no scene tree, animation, Steam API, audio, render frame, wall clock or random source.

## 2.2 Presentation/Application layer
Owns:
- bench scenes;
- camera transitions;
- key/lock visuals;
- cutaway and filing animation;
- HUD/ledger/history/hints;
- menus/focus;
- accessibility visualization;
- audio/haptics;
- input intent routing;
- non-authoritative pacing/flourish.

Presentation submits semantic commands to Domain Core and renders returned state/events. It may never directly mutate key depth, knowledge, opened locks or access state.

## 2.3 Platform Services
Owns optional/external capabilities:
- Steam initialization/availability;
- achievements;
- Cloud synchronization adapter;
- controller glyph/platform naming support;
- Rich Presence/Stats if later enabled;
- file-system paths and platform-specific safe-storage helpers.

Domain Core never imports Steam/platform classes. Platform failures cannot prevent local play or local saves.

## 2.4 Allowed dependency direction
`Platform adapters -> Application orchestration -> Domain Core`
`Presentation -> Application orchestration -> Domain Core`

Domain Core depends only on domain data/value types and deterministic utilities.

Forbidden dependency examples:
- Domain Core asking a mesh for current notch depth;
- TEST using animation collision contact;
- solver reading UI ledger state instead of canonical knowledge state;
- Steam achievement callback directly marking a case solved;
- save loader restoring scene nodes as puzzle authority.

---

# 3. Canonical conceptual data model

Names are conceptual; implementation may rename classes but not merge authorities in ways that break contracts.

## 3.1 CaseDefinition
Static immutable record:
- `schema_version`
- `case_id`
- `campaign_slot`
- `primary_family`
- `column_count: int` (4..6 campaign)
- `depth_max: int` (3..5 campaign)
- `blanks: Array<BlankDefinition>` (1..3 campaign)
- `locks: Array<LockDefinition>` (1..6 required normal ceiling)
- `required_lock_ids`
- tutorial concept metadata
- mastery definitions
- validation metadata/signature version
- localization keys/presentation IDs that do not affect solver semantics.

## 3.2 BlankDefinition
- `blank_id: stable string/id`
- `start_vector: PackedInt32Array[C]`
- presentation variant ID only.

## 3.3 LockDefinition
- `lock_id`
- `required: bool`
- `accepted_sets[C]`, each represented canonically as a sorted unique integer collection or compact bitset over `0..D`
- `access_predicate`
- presentation variant ID only.

Accepted-set bitset is recommended because D<=5: equality, membership and canonical hashing become trivial and branch gaps remain explicit.

## 3.4 AccessPredicate
Discriminated union:
- `ALWAYS`
- `AFTER_OPEN(lock_id)`
- `AFTER_ANY(lock_ids)`
- `AFTER_ALL(lock_ids)`

No runtime script callback is permitted as an access rule in main campaign content.

## 3.5 PuzzleState
Authoritative current forward state:
- `case_id`
- `key_vectors[blank_id][C]`
- `opened_lock_bitset`
- `knowledge_state`
- `authoritative_action_index`
- derived `case_solved` may be cached but must be reproducible.

Do not store presentation selection/camera/focus in PuzzleState.

## 3.6 KnowledgeState
Must preserve exactly what the player is entitled to know.

For each `(blank_id, lock_id, column)` store a canonical set/list of observations sufficient to reproduce:
- accepted-at-depth observations;
- TOO_SHALLOW at tested depth plus LIGHT/STRONG when produced;
- TOO_DEEP at tested depth;
- BETWEEN_BRANCHES at tested depth;
- OPEN accepted observations.

Deductions are preferably derived from observations rather than persisted as independent truth. If cached, cache must be discardable/recomputable.

## 3.7 ActionRecord
Semantic authoritative action:
- stable sequence number;
- `FILE(blank_id, column, before_depth, after_depth)`; or
- `TEST(blank_id, lock_id, tested_vector_snapshot, result, emitted_observations, newly_opened_lock?, access_changes)`.

ActionRecord contains enough exact information for history display and deterministic undo/redo. Hidden case data does not need to be copied into each record.

## 3.8 CampaignProgress
Separate from current PuzzleState:
- solved case IDs;
- unlocked/eligible case IDs derived from solved prerequisites;
- per-case mastery/best stats;
- tutorial-understood flags where needed for demo import;
- achievement-event counters/flags;
- last selected case;
- current in-progress case save reference/state.

## 3.9 SettingsProfile
Separate save domain:
- input mappings if application-owned;
- UI scale;
- text size;
- contrast/reduced motion;
- discrete numeric labels setting;
- hold/toggle preference;
- audio levels;
- confirmation preference;
- controller/glyph preference only where needed.

Settings corruption must not corrupt campaign progress.

---

# 4. Deterministic command/reducer model

All puzzle mutations go through one command gateway such as `DomainSession.apply(command)`.

## 4.1 FILE ordering
For `FILE(blank, column)`:
1. validate current session/case exists;
2. validate blank exists and is currently legal for filing;
3. validate column range;
4. read current integer depth;
5. if at `D`, return `NO_OP_MAX_DEPTH` with no history entry;
6. create next vector with exactly `+1` on selected column;
7. create ActionRecord containing before/after;
8. commit PuzzleState key vector;
9. append history and clear redo tail if command follows an Undo;
10. recompute derived win/mastery-progress state if relevant (FILE itself cannot newly solve ordinary case);
11. emit deterministic domain events to application (`FILE_COMMITTED`, state snapshot/version);
12. schedule/request non-authoritative softlock analysis against the committed state.

Softlock result never changes the state automatically.

## 4.2 TEST ordering
For `TEST(blank, lock)`:
1. validate IDs;
2. evaluate access predicate from current opened-lock bitset;
3. if inaccessible, return `ILLEGAL_ACCESS` with no history and no knowledge change;
4. snapshot tested key vector;
5. evaluate columns `1..C` strictly in order against accepted sets;
6. if blocker exists, derive exactly one blocker relation and optional shallow strength;
7. produce accepted-prefix observations for columns before blocker;
8. produce blocker observation only for blocker column;
9. if no blocker, produce accepted observations for all columns and `OPEN`;
10. on OPEN, if lock was not already opened, set opened bit exactly once;
11. derive access-state changes from new opened bitset; no bespoke callbacks;
12. merge observations monotonically into KnowledgeState;
13. create/append ActionRecord even for an identical repeated legal test, because Undo/history must match player actions; however emitted **new knowledge set** may be empty and no progression/hint counter may advance from repetition;
14. evaluate `all required opened` after opening/access effects;
15. if newly solved, emit `CASE_SOLVED` exactly once for this forward timeline state;
16. clear redo tail if appropriate;
17. return semantic result/event bundle for presentation.

Repeated identical tests are authoritative actions for history/Undo but grant no extra information or achievement farming.

## 4.3 Feedback relation function
Given current depth `x` and accepted bitset `A`:
- if `x < min(A)` -> TOO_SHALLOW;
- else if `x > max(A)` -> TOO_DEEP;
- else if `x notin A` -> BETWEEN_BRANCHES;
- else accepted.

For TOO_SHALLOW:
- nearest deeper accepted `y=min{a in A | a>x}`;
- LIGHT iff `y=x+1`, else STRONG.

No floating tolerance.

## 4.4 OPEN semantics
OPEN is not a separate player command. It is a TEST result and nested effect. This prevents ordering ambiguity between `TEST succeeded`, `lock opened`, `access changed`, and `case solved`.

## 4.5 Undo
Undo applies exact inverse of the most recent ActionRecord to the prior authoritative state.

Recommended implementation: because states are tiny, maintain immutable/copy-on-write domain snapshots per action or deterministic action replay from case start with cached snapshots. Reliability outranks micro-optimization.

Undo must restore:
- key vectors;
- knowledge observations added by that action;
- opened bitset/access consequences;
- solved state;
- mastery statistics dependent on timeline.

Undo must not change campaign completion already committed by leaving a solved review into campaign progression unless the design explicitly allows reopening the solved session; campaign commit occurs at a defined boundary outside puzzle action history.

## 4.6 Redo
Redo restores the exact previously undone ActionRecord transition. It must not rerun solver-dependent or time-dependent logic. A different forward authoritative action clears redo tail.

## 4.7 Restart
Restart replaces PuzzleState/history with the exact authored initial state, retaining campaign-level solved history only if the case was previously solved in an earlier committed run. Current attempt stats reset.

## 4.8 Campaign solve commit
When current case reaches solved state:
- show solved review from current attempt;
- campaign progress may record solved/mastery immediately in a local transaction, but must be idempotent;
- repeated solve or replay may improve mastery/best stats but cannot duplicate one-time unlock/achievement events.

---

# 5. Solver and validator architecture

Solver tooling is primarily authoring/validation infrastructure. Runtime uses only bounded proof services such as softlock/hint support.

## 5.1 Two solver modes
### Omniscient solver
Knows full accepted sets. Used for:
- basic solvability;
- minimum/near-minimum action estimates;
- partition enumeration/signatures;
- final-coverage checks;
- softlock proof from current forward state.

### Information-respecting solver
Policy state includes player-visible knowledge and may choose actions only using facts/deductions legitimately available. Used for:
- fairness validation;
- hint safety;
- ensuring a case does not require clairvoyant cuts/tests.

## 5.2 Canonical future-state key
For omniscient future solvability:
- sorted/canonical multiset of key vectors when blanks are truly symmetric for future mechanics;
- opened-lock bitset;
- access state need not be separately stored if purely derived from opened bitset;
- include any future mechanic state only if frozen canon requires it (none currently).

For information-respecting search, include canonical knowledge representation and preserve blank identity whenever histories differ in player-visible information.

## 5.3 Blank symmetry
Two blanks may be swapped only when all of these match:
- current vectors equal;
- future legal actions identical;
- no blank-specific case rule exists (none expected);
- in information-respecting mode their knowledge states are equivalent under the same permutation.

Never symmetry-collapse merely because vectors match while their observation histories differ.

## 5.4 Knowledge canonicalization
Observations are normalized by `(blank, lock, column, relation, tested_depth, strength-if-any)` and duplicate observations collapse. Accepted-prefix/open facts at the same depth normalize identically.

## 5.5 Action generation
Solver actions are semantic FILE/TEST only.

Safe pruning:
- never generate FILE at max depth;
- repeated TEST with identical vector against same lock can be pruned if it adds no new observation and produces no new OPEN state;
- inaccessible TEST excluded;
- symmetry-equivalent FILE actions may be collapsed only under proven blank symmetry.

## 5.6 Runtime softlock budget
Softlock checker is proof-only:
- `UNSOLVABLE` only if exhaustive/bounded proof completes;
- `SOLVABLE` if a completion is found;
- `UNKNOWN` on timeout/budget exhaustion.

Only `UNSOLVABLE` may trigger Phase-6 warning.

Initial target budget:
- desktop background target <=100 ms typical, hard cooperative budget <=250 ms before yielding/aborting to UNKNOWN;
- Steam Deck same correctness, budget may be lower to protect frame time;
- never block animation/input waiting for softlock proof.

Exact budget is empirical implementation tuning, not puzzle rule authority.

## 5.7 Authoring validator stages
Implement Phase-5 V0+ pipeline as separate commands/tests:
- schema legality;
- access reachability;
- omniscient solvability;
- information-respecting fairness;
- softlock false-positive verification;
- cheap-policy attacks;
- solution partition extraction;
- canonical duplicate/isomorphism signature;
- pacing/action-count metrics;
- campaign-family/tutorial constraints.

Validator output should be machine-readable (JSON or structured report) and suitable for CI.

## 5.8 Duplicate/isomorphism detection
Canonical case signature should normalize at minimum:
- lock labels;
- blank labels where symmetric;
- column permutation only when the entire case transforms equivalently, including access/knowledge consequences;
- accepted-set topology;
- start vectors;
- access graph;
- objective/mastery-relevant constraints.

Signature equality flags review; it need not automatically prove experiential duplication.

---

# 6. Persistence and recovery

## 6.1 Save files
Use explicit versioned data, not serialized scene nodes/resources as sole authority.

Recommended logical files/namespaces:
- `profile.json` or equivalent compact structured binary/text: campaign progress/current case metadata;
- `attempt_<slot>.json`: current PuzzleState + complete current case ActionRecords or enough deterministic reconstruction data;
- `settings.json`;
- optional `demo_profile.json` namespace/marker.

Exact encoding may be JSON initially for transparency/testing; later compact encoding is allowed only with migration tests.

## 6.2 Save schema version
Every persisted top-level payload has:
- `format_id`;
- `schema_version` integer;
- app/game build version for diagnostics;
- payload;
- integrity checksum/hash where practical.

Case content has its own schema/content version. Save must record the case content identity/signature required to detect incompatible changed content during development.

## 6.3 Atomic local save
Write protocol:
1. serialize to temporary file in same save location;
2. flush/close;
3. validate parse/integrity of temp payload;
4. rotate current known-good file to backup where platform permits;
5. atomically rename temp to primary;
6. retain at least one previous known-good profile/attempt backup.

A crash between steps must leave either old good save or new good save recoverable.

## 6.4 Autosave boundaries
Save after:
- every authoritative FILE/TEST action or short coalesced transaction once domain commit completes;
- case solve/campaign progression commit;
- mastery improvement;
- settings changes separately.

Because state is tiny, reliability is preferred over infrequent saves. Do not save midway through an animation as if presentation were authority.

## 6.5 Load recovery order
On startup/load:
1. parse primary;
2. validate schema/integrity/case references;
3. if invalid, attempt previous backup;
4. if backup valid, restore it and inform player non-alarmingly;
5. if both invalid, preserve corrupt files for diagnostics where possible, start safe fresh profile only after explicit user choice if meaningful progress would be lost.

Never silently overwrite the last recoverable save with a fresh empty profile during failed load.

## 6.6 Migration
Migrations are explicit `vN -> vN+1` transformations with fixtures.
- migrations must be deterministic and idempotent at their target version;
- never reinterpret a stored key vector based on rendered geometry;
- if case content changed incompatibly during development, safest fallback is preserve campaign solved status/mastery while restarting only the affected in-progress case from its new authored initial state, with clear dev/release policy.

## 6.7 Cloud model
Steam Cloud is a transport/synchronization layer over local save authority, not the database of truth.

On conflict where platform provides two materially different versions:
- compare timestamps only as one signal;
- prefer progress-aware resolution UI when both are valid and neither dominates safely;
- show human-readable summaries such as solved-case count, last case, last modified device/time if available;
- never merge two in-progress attempt action histories automatically.

Safe merge may combine monotonic campaign achievements/solved case flags only if schema rules prove union cannot invent impossible state; current-attempt state must choose one side.

Offline play must remain normal. Cloud failure queues/retries externally and never blocks local save.

---

# 7. Demo/full persistence contract

## 7.1 Namespace separation
Demo and full game have distinct app/profile identity even if Steam Cloud storage is configured compatibly.

Demo export record contains only an allowlisted `DemoTransfer` payload:
- transfer schema version;
- D01–D06 solved flags;
- tutorial-understood flags derived from solved demo cases;
- compatible settings/accessibility values;
- optional non-sensitive demo feedback metadata excluded from gameplay.

Do **not** import:
- arbitrary current demo PuzzleState into Cxx campaign;
- demo action history as full campaign history;
- solver internals;
- demo-only development flags.

## 7.2 Full-game recognition
On first compatible full launch:
- detect transfer once;
- validate schema/content identity;
- offer documented choice: start C01 normally or mark equivalent tutorial explanations understood while keeping all cases replayable;
- achievements disabled in demo; full game may reconcile deterministic achievement conditions from accepted imported solved flags after user profile creation/load.

Import is idempotent. Re-import cannot duplicate achievements, progression unlocks or mastery counters.

---

# 8. Steam/platform service abstraction

Define interface-style services; application consumes capabilities, never assumes Steam exists.

## 8.1 PlatformService
Capabilities:
- `is_platform_available()`
- `get_platform_name()`
- `get_controller_glyph_family()` or map semantic actions through input layer
- optional overlay/store navigation helper.

## 8.2 AchievementService
- queue idempotent `unlock(achievement_id)`;
- local application records logical achievement eligibility independently;
- if Steam offline/uninitialized, retain pending unlocks locally and reconcile later;
- platform callback failure does not roll back game progress.

## 8.3 CloudService
- platform adapter exposes sync availability/status and conflict inputs;
- local SaveService remains authoritative writer/reader;
- CloudService never mutates Domain Core directly.

## 8.4 Graceful degradation
Without Steam:
- all campaign, hints, mastery, saves, controller input and accessibility work;
- achievements can remain locally tracked for later platform reconciliation;
- Rich Presence absent with no UX error loop;
- Cloud menu indicates unavailable rather than blocking Continue.

---

# 9. Input and focus architecture

## 9.1 Semantic actions
Use the Phase-6 canonical actions through Godot InputMap or an equivalent application abstraction. Domain commands are fewer than raw inputs:
- FILE commit;
- TEST;
- Undo;
- Redo;
- Restart.

Navigation, selection, zoom, ledger and pause remain application/presentation commands.

## 9.2 Focus model
Application maintains semantic focus object (`bench key`, `lock`, `column`, `UI control`) independent from mouse hover.

Requirements:
- every modal/screen declares default focus;
- close modal restores prior focus if legal;
- hot-plug/device switch does not clear focus;
- mouse movement alone cannot steal controller focus;
- unfocused OS window ignores controller gameplay commands;
- repeat rate/deadzone tuning affects navigation only, never FILE count.

## 9.3 Rebinding
Bindings are data/settings. Puzzle logic references semantic actions only. A remap cannot alter action ordering or create multi-commit from one press.

FILE_COMMIT must trigger once per discrete press edge. Input repeat is prohibited for FILE_COMMIT/TEST/Undo/Redo/Restart unless explicitly handled as repeated user presses.

---

# 10. Localization-ready boundaries

All player-facing strings use localization keys. No puzzle authority depends on localized text.

## 10.1 Data/string separation
Case data stores:
- title localization key;
- optional short flavor/presentation keys;
- tutorial/help localization keys.

Never store accepted-set meaning inside textual instructions.

## 10.2 Formatting
- no string concatenation that assumes English word order;
- variables use placeholders with named semantics;
- controller glyph is a token/icon, not hard-coded button letter in source text;
- pluralization/number formatting uses localization system when needed;
- discrete depth numbers are plain numeric facts and optional aids.

## 10.3 Fonts/layout
- use font assets with fallback strategy suitable for intended eventual scripts; final language set remains commercial decision;
- UI containers must tolerate at least ~30–40% text expansion without overlap at reference layouts;
- ledger rows can wrap/scroll; never shrink essential text to unreadable sizes;
- do not bake essential text into textures.

Right-to-left support is not promised at design freeze but architecture should avoid assumptions that make it impossible.

---

# 11. Performance, memory and loading budgets

The game has extremely small authoritative state; performance risk is presentation/UX, not solver-sized runtime world simulation.

## 11.1 Frame targets
Target:
- 60 fps presentation on Steam Deck-class hardware at 1280×800 under normal bench scenes;
- graceful 30 fps fallback is acceptable only as a user/platform graphics choice, never because solver blocks main thread.

## 11.2 Main-thread rules
- no exhaustive solver/validator work on rendering frame path;
- runtime softlock/hint search runs incrementally/background or cooperatively budgeted;
- save serialization should be tiny and non-janky; disk flush may be asynchronous after an in-memory transaction while preserving ordered durability guarantees.

## 11.3 Scene complexity guidance
- one bench scene, <=3 active key artifacts, <=6 locks, modest transparent/cutaway effects;
- avoid expensive real-time global illumination requirement as product dependency;
- avoid large dynamic shadow counts/volumetric smoke/etc.; they add no puzzle value;
- material/mesh variants should share resources where practical.

## 11.4 Memory target
No strict MB number is design authority before real assets exist. Implementation gate: base bench + maximum normal case must remain comfortably within Steam Deck memory budget without streaming complexity; duplicate high-resolution textures/material instances are a review smell.

## 11.5 Loading
- cold boot should reach main menu without large shader/content compilation stalls after first-run cache behavior where controllable;
- case transition target: a few seconds maximum on Steam Deck, preferably near-instant because cases reuse bench assets;
- restarting current case should not reload entire application scene.

---

# 12. Deterministic testing and instrumentation

## 12.1 Headless Domain Core tests
Must run without graphics for:
- FILE legality and +1 exactness;
- accepted-set membership;
- first-blocker ordering;
- feedback relation/strength;
- accepted-prefix observations;
- OPEN persistence;
- access predicate evaluation;
- knowledge monotonic merge;
- repeated identical test no-new-info;
- Undo/Redo exactness;
- restart exactness;
- solve transition idempotency;
- mastery counters;
- canonical hashes/signatures.

## 12.2 Golden transition fixtures
For several compact cases, store initial state + command sequence + expected state/event after every action. Run across engine upgrades and save migrations.

## 12.3 Validator fixtures
Include:
- trivially solvable case;
- unsolvable case;
- omniscient-solvable but information-unfair case;
- access-cycle invalid case;
- branch-gap feedback case;
- symmetry case with equivalent blanks;
- equal-vector/different-knowledge case that must not collapse information-respecting symmetry;
- cheap-policy-trap cases;
- near-duplicate/isomorphic pair.

## 12.4 Presentation-authority tests
Automated/integration tests or debug assertions must verify:
- rendered key depth is generated from current key vector;
- TEST animation result receives DomainResult rather than recomputing fit;
- skipping animation yields identical DomainState;
- reduced motion yields identical DomainState/history;
- physics disabled/change in frame rate cannot alter TEST/FILE result;
- controller vs mouse route produces identical command sequence for equivalent actions.

## 12.5 Persistence tests
- crash-style interrupted temp write;
- corrupted primary valid backup;
- corrupted primary+backup safe failure;
- schema migrations;
- stale case content identity;
- Cloud conflict choosing either side;
- demo import repeated twice;
- Steam unavailable at save/load;
- Unicode/settings round-trip.

## 12.6 Debug tooling
Later implementation should provide developer-only:
- dump canonical PuzzleState;
- dump player-visible KnowledgeState;
- replay action trace from initial state;
- run case validator from case ID;
- visualize accepted sets only in dev mode;
- solver result/timeout metrics;
- canonical signature display;
- deliberately corrupt a copied test save fixture, never user save.

No dev information ships accidentally into normal ledger/hints.

---

# 13. Implementation sequence for dedicated repository

This is handoff ordering, not implementation started here.

## 12A — Technical bootstrap
- Godot 4.7.2-stable project baseline;
- Domain Core module/value types;
- semantic input map;
- headless test harness;
- versioned save service skeleton;
- CI with no email-noise/test-email policy.

Exit: command-line/domain tests run; one synthetic case loads and can be driven without graphics.

## 12B — Vertical slice
Implement 3 locks / 2 blanks / 5 columns:
- bench overview;
- select key/lock;
- preview + FILE commit;
- TEST cutaway driven by DomainResult;
- accepted-prefix/TOO_SHALLOW/TOO_DEEP;
- Undo/Redo/Restart;
- tiny ledger;
- save/reload exact attempt.

Run Game-8 prototype kill gates from tournament/mechanics.

## 12C — Core systems complete
- master branch/BETWEEN_BRANCHES;
- wear accepted sets;
- access predicates;
- full knowledge/deductions/hints;
- softlock proof service;
- mastery tracking;
- solved review.

## 12D — Content pipeline/population
- declarative case loader;
- validator CLI/report;
- C01–C32 candidate spine;
- D01–D06;
- duplicate/policy/fairness validation;
- quality floor enforcement.

## 12E — UX/accessibility/platform
- complete controller/Deck focus path;
- remapping;
- accessibility suite;
- localization plumbing;
- Steam achievements/Cloud adapter;
- demo/full transfer.

## 12F — Adversarial QA
- save corruption/recovery;
- platform offline/hot-plug;
- solver timeouts;
- exploit/duplicate events;
- focus traps;
- animation/domain divergence;
- long Undo/Redo histories.

## 12G — Empirical gates
- fresh-player demo comprehension;
- tactile presentation quality;
- C01–C32 abandonment/difficulty;
- Deck readability/performance;
- store misunderstanding as burglary/lockpicking;
- price/value review.

## 12H — Release candidate
- validated >=28 strong cases;
- demo packaging;
- release build regression;
- achievement/Cloud idempotency;
- localization selected-language QA;
- performance/package/store checklist.

---

# 14. Technical acceptance tests

The following are release/implementation contracts unless explicitly marked empirical.

## Domain boundaries
T01 Domain Core can execute a complete case with no scene tree/render/audio/platform service.
T02 Presentation cannot mutate key vectors directly.
T03 Presentation cannot mark a lock opened directly.
T04 Platform callbacks cannot mark a case solved.
T05 Physics/collision never decides accepted-set membership.
T06 changing animation speed cannot change authoritative action count/result.
T07 reduced-motion mode produces identical domain traces.
T08 mesh deformation is downstream of integer key vector.

## FILE
T09 FILE changes exactly one selected column by +1.
T10 FILE at maximum depth is a no-op and creates no authoritative history record.
T11 preview changes no PuzzleState.
T12 canceling preview changes no PuzzleState/history.
T13 one physical input press cannot commit multiple FILE steps through repeat.
T14 FILE after Undo clears redo tail.
T15 filing cannot shallow a key in forward state.

## TEST and fit
T16 TEST evaluates columns left-to-right.
T17 only first incompatible column is the blocker.
T18 columns after blocker add no observation.
T19 columns before blocker add accepted-at-tested-depth observations.
T20 singleton accepted set evaluates exactly.
T21 contiguous tolerance uses integer membership only.
T22 disjoint branch accepted set uses the same membership rule.
T23 `x < minA` returns TOO_SHALLOW.
T24 `x > maxA` returns TOO_DEEP.
T25 interior non-member between branches returns BETWEEN_BRANCHES.
T26 LIGHT iff nearest deeper accepted value is exactly x+1.
T27 STRONG iff nearest deeper accepted value is >=x+2.
T28 successful TEST records accepted observations for all columns.
T29 successful first open sets opened state once.
T30 reopening an opened lock cannot duplicate completion/access effects.
T31 later filing the opening key does not clear opened state.
T32 inaccessible TEST changes no knowledge/history/state.

## Knowledge
T33 observations are monotonic inside forward timeline.
T34 duplicate identical observation collapses logically.
T35 repeated identical legal TEST may appear in action history but yields no new knowledge.
T36 repeated identical TEST cannot farm hints/progression/achievements.
T37 deductions can be recomputed solely from observations + universal rules.
T38 ledger cannot access hidden accepted sets through presentation API.
T39 equal vectors with different observation histories remain distinguishable to information-respecting solver.

## Access and solve
T40 ALWAYS is accessible initially.
T41 AFTER_OPEN uses opened bit only.
T42 AFTER_ANY activates when any referenced lock opened.
T43 AFTER_ALL activates only when all referenced locks opened.
T44 access result is deterministic for identical opened bitset.
T45 case solves iff all required locks are opened under default objective.
T46 CASE_SOLVED event is idempotent for a given transition.
T47 replaying solved case cannot duplicate campaign unlock rewards.

## Undo/Redo/Restart
T48 Undo FILE restores exact prior vector.
T49 Undo TEST removes exactly observations/effects added by that action.
T50 Undo successful first-open restores opened/access/solved state exactly.
T51 Redo replays stored transition exactly.
T52 Redo does not recompute against wall clock/randomness.
T53 new action after Undo invalidates redo tail.
T54 restart recreates authored initial PuzzleState exactly.
T55 restart clears current attempt knowledge/history.
T56 camera/menu actions never appear in authoritative Undo history.

## Solver/validator
T57 omniscient solver finds known fixture solution.
T58 omniscient solver proves known fixture unsolvable.
T59 information-respecting solver rejects a clairvoyance-only fixture.
T60 information-respecting solver solves a fair fixture without hidden accepted-set access.
T61 runtime softlock warning never appears on UNKNOWN.
T62 runtime softlock warning appears only after proof UNSOLVABLE.
T63 softlock analysis never blocks frame/input waiting for completion.
T64 repeated no-new-info TEST can be pruned in solver search.
T65 symmetric identical blanks may canonicalize only when future and knowledge equivalence hold.
T66 different-knowledge identical-vector blanks do not collapse incorrectly.
T67 invalid access cycle fixture is rejected.
T68 empty accepted-set fixture is rejected.
T69 out-of-range depth fixture is rejected.
T70 >campaign-ceiling content is rejected for main campaign unless explicitly non-campaign tooling mode.
T71 canonical duplicate signature flags a known renamed/isomorphic fixture.

## Persistence
T72 every persisted payload declares format/schema version.
T73 primary save parses after normal write/read round trip.
T74 interrupted temp write leaves prior known-good save recoverable.
T75 corrupted primary loads valid backup without overwriting backup first.
T76 corrupted primary+backup does not silently replace progress with empty profile.
T77 schema migration fixture produces expected target payload.
T78 migration never derives key state from mesh geometry.
T79 current in-progress case content mismatch is detected.
T80 settings corruption cannot corrupt campaign progress namespace.
T81 autosave occurs only after authoritative transaction commit, never mid-animation authority.
T82 long current-case history can reload and preserve full Undo capability.

## Cloud/platform
T83 Steam unavailable does not prevent local play.
T84 Steam unavailable does not prevent local save/load.
T85 failed achievement unlock does not roll back campaign progress.
T86 pending eligible achievement can reconcile when platform returns.
T87 Cloud conflict never auto-merges two current attempt timelines.
T88 choosing either valid Cloud side loads a self-consistent profile/attempt.
T89 controller glyph/platform service failure falls back without blocking input.

## Demo/full
T90 demo transfer contains only allowlisted transfer fields.
T91 demo current PuzzleState is not imported into arbitrary full campaign case.
T92 compatible demo completion can mark equivalent tutorial understanding without making cases unreplayable.
T93 demo import is idempotent.
T94 repeated demo import cannot duplicate achievements/progress counters.
T95 corrupt/incompatible demo transfer cannot block fresh full-game profile.

## Input/focus/accessibility
T96 keyboard and controller equivalent semantic command sequences produce identical domain traces.
T97 mouse hover cannot steal controller focus by itself.
T98 returning from modal restores deterministic legal focus.
T99 controller hot-plug does not lose authoritative selected puzzle state.
T100 OS-unfocused window ignores gameplay controller commands.
T101 all essential actions are reachable from default controller configuration.
T102 no mandatory hold input exists for core action.
T103 optional numeric depth labels reveal no hidden lock accepted values.
T104 colorblind/high-contrast mode changes presentation only.
T105 UI at 1280x800 keeps all max-case critical targets reachable/readable under target accessibility scale, subject to empirical visual QA.

## Localization/performance
T106 essential strings are localization keys, not embedded in texture authority.
T107 controller prompts use semantic glyph tokens rather than hard-coded English button names.
T108 text expansion does not overlap or hide required controls in supported release languages.
T109 solver/validator exhaustive work is absent from normal render-frame critical path.
T110 normal maximum case remains responsive while background softlock check runs.
T111 restart does not require full application reload.
T112 target Steam Deck bench scene reaches intended performance/readability gate empirically without changing domain rules.

## Authority regression
T113 engine upgrade requires all domain golden traces to match.
T114 save schema upgrade requires migration/corruption regression suite to pass.
T115 animation refactor requires presentation-authority tests to pass.
T116 platform SDK update cannot change local offline puzzle results.
T117 case-data tooling cannot publish generated content unless validator + authored causal review pass.
T118 no production implementation decision may introduce continuous/floating fit authority without reopening Product Thesis.
T119 no technical shortcut may expose solver-only hidden data to player ledger/hints.
T120 a fresh implementation session can identify Domain, Presentation and Platform ownership for every frozen core system from this document.

---

# 15. Phase-8 freeze decision

**PHASE 8 TECHNICAL IMPLEMENTATION SPECIFICATION = COMPLETE.**

Initial baseline is **Godot 4.7.2-stable / GDScript-first**. The central non-negotiable implementation invariant is:

> Integer/discrete Domain Core decides every cut, fit, observation, opening, access effect, Undo state and solve result; presentation and platform services may only render, route and persist those decisions.

No production code has been started in the factory.

Phase 9 should now perform a whole-game paper simulation across first boot, D01–D06, C01–C32 progression, mature diagnostic/access cases, mastery/replay, save/crash/Cloud/demo import, controller/Deck/accessibility, solver timeout and hostile user behavior. Every contradiction found must be repaired in the owning Phase 3–8 authority before Phase 10.