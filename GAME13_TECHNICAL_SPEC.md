# GAME #013 — PHASE 8 TECHNICAL IMPLEMENTATION SPECIFICATION

Date: 2026-09-02
Status: PHASE 8 COMPLETE — BUILDABLE TECHNICAL CONTRACT FROZEN
Selected concept: **SEAL BREAK** (working title)
Authority: Phase 4 mechanics, Phase 5 content, Phase 6 UX and Phase 7 commercial model remain authoritative. This file specifies how a future implementation repository must represent, execute, persist, validate and test those rules. It does **not** authorize production implementation inside the factory.

## 1. Phase-8 verdict
Seal Break can be implemented as a compact deterministic desktop game with one shared domain rules contract used by runtime play, replay and offline certification. No unresolved technical-design question currently requires a mechanic change.

Recommended implementation direction for the future dedicated repository:
- **Godot 4.7.x stable**, with **4.7.2 stable (2026-08-18)** the current baseline at design-freeze time;
- standard Godot desktop build, PC/Steam first;
- GDScript is the default implementation language unless the implementation session proves a concrete reason to use C# or native code;
- pure/domain resolver code must not depend on scene-tree timing, animation callbacks, rendering nodes or Steam APIs;
- Steam integration sits behind adapters so rules, saves and tests remain runnable without Steam.

This is a technical direction, not a lifetime version lock. Before production bootstrap, use the then-current supported stable Godot 4.x release unless an engine upgrade breaks required behavior. Never begin production on a preview/dev build merely because it is newer.

Fresh platform/tool evidence checked 2026-09-02:
- Godot's official archive lists 4.7.2 as stable (2026-08-18) while 4.8 is still in development;
- Godot's current release policy lists 4.7 and 4.6 as supported branches;
- Steam Cloud documentation confirms Dynamic Cloud Sync can deliver changed files during an application session and recommends handling local-file-change notifications;
- Steam Deck compatibility guidance requires the default controller configuration to expose all game functionality and correct input glyph behavior.

## 2. Architectural boundary
Future implementation is split into five conceptual layers.

### 2.1 Domain
Pure deterministic logic. No rendering, audio, animation, Steam, filesystem or wall-clock dependencies.

Owns:
- case semantic validation;
- legal-submission validation;
- canonicalization;
- deterministic resolver;
- evidence predicate evaluation;
- trace construction;
- solution/equivalence signatures;
- certifier-facing enumeration contracts.

### 2.2 Application
Coordinates player actions and runtime state transitions.

Owns:
- session state machine;
- edit transactions and undo/redo;
- commit snapshot creation;
- reveal/replay/scrub control;
- progression decisions;
- hint request state;
- save orchestration;
- demo import orchestration.

It calls Domain but never reimplements Domain rules.

### 2.3 Presentation
Godot scenes/UI/audio/animation.

Owns only visualization and interaction mapping. Presentation may stagger several same-checkpoint tear animations, but authoritative trace state is already fixed before animation begins.

### 2.4 Platform adapters
Steam achievements, Cloud notifications, input-device glyph family, filesystem paths, optional Steamworks integration. Domain and core save semantics must work when these adapters are absent.

### 2.5 Offline authoring/certifier
A headless/editor-capable tool using the same Domain resolver and schema. It may enumerate large bounded spaces, generate reports and hashes, but cannot contain a second implementation of tear rules.

## 3. Runtime state machine
Canonical top-level states:

1. `BOOT`
2. `LOAD_PROFILE`
3. `TITLE_MENU`
4. `CASE_SELECT`
5. `CASE_LOADING`
6. `CASE_EDIT`
7. `COMMIT_VALIDATE`
8. `RUN_RESOLVE`
9. `RUN_REVEAL`
10. `RUN_RESULT_SUCCESS`
11. `RUN_RESULT_MISMATCH`
12. `RUN_REPLAY`
13. `PAUSE_OVERLAY`
14. `HELP_OR_HINT_OVERLAY`
15. `SAVE_CONFLICT_GATE`
16. `FATAL_CONTENT_ERROR`

### 3.1 Boot/load
`BOOT -> LOAD_PROFILE` after platform adapter initialization. Steam absence/offline state is not fatal.

`LOAD_PROFILE` performs schema/version validation and recovery before menu presentation. If a valid profile exists, proceed to `TITLE_MENU`. If the main file is invalid but backup is valid, recover backup and write a new main file with a recovery audit marker. If neither is valid, preserve corrupt files and offer a fresh profile rather than deleting evidence silently.

Cloud/local ambiguity that cannot be deterministically merged enters `SAVE_CONFLICT_GATE` before gameplay progress can be overwritten.

### 3.2 Case entry
`CASE_SELECT -> CASE_LOADING -> CASE_EDIT`.

At `CASE_LOADING`:
- load case data;
- semantic-validate it;
- verify supported content/rules versions;
- construct immutable case model;
- build initial edit state;
- restore optional last-edit draft only if its case content hash still matches.

Shipping content failure is a development/release-blocking error. Runtime must not silently repair malformed case definitions.

### 3.3 Commit
`CASE_EDIT -> COMMIT_VALIDATE` only when player requests Commit.

`COMMIT_VALIDATE` performs structural legality only:
- placement budget/mode;
- socket enabled/existence;
- history bounds;
- required/forbidden/fixed-position/precedence constraints;
- no duplicate compartment opening.

It does not indicate whether target evidence will pass.

If legal, application freezes a `SubmissionSnapshot`, computes its canonical submission hash, clears presentation-only run state, then transitions to `RUN_RESOLVE`.

### 3.4 Resolve/reveal separation
`RUN_RESOLVE` calls the pure resolver to completion in one logical operation and produces a complete immutable `RunTrace` before any reveal animation is authoritative.

Then `RUN_REVEAL` consumes that trace. Step/1x/2x/Instant/Skip alter only presentation cursor/timing.

A skipped reveal and a fully animated reveal must finish with identical trace/result hashes.

### 3.5 Result and return
After reveal:
- all predicates true -> `RUN_RESULT_SUCCESS`;
- otherwise -> `RUN_RESULT_MISMATCH`.

Both retain the immutable trace for retrospective inspection.

`Replay` enters `RUN_REPLAY` using the exact same submission snapshot and stored trace hash. Implementation may either re-render stored trace or re-run resolver and assert equal trace hash; debug/test builds should favor the latter parity check.

`Return to Edit` restores the exact pre-commit edit submission plus its undo/redo stacks according to the Phase-6 transaction rules. No broken/intact simulation state is copied into edit state.

### 3.6 Pause/help/hints
Pause/help overlays are modal application states layered over a resumable owner state. Hints may disclose only authored hint text and hint-step state. They do not modify Domain legality or resolution.

## 4. Canonical data schema
Serialization format may be JSON, Godot resources or another deterministic text/binary representation, but the semantic schema below is frozen. Authoring source should remain diffable where practical.

### 4.1 Package/version header
Every case package contains:
- `schema_version`: integer;
- `rules_version`: stable string/integer for Domain semantics;
- `case_id`: globally stable ASCII identifier;
- `content_revision`: monotonic authoring revision;
- `title_key`;
- `act_id`, `act_position`, `campaign_position`;
- `required_for_floor`, `demo_included`;
- `prerequisite_case_ids`;
- `difficulty_band`;
- `teaching_intent`;
- `estimated_first_solve_minutes`;
- `content_hash`: generated from canonical semantic form, not manually authored.

Presentation/localization text changes that do not alter mechanics may increment package revision without changing a separately computed `mechanics_hash`.

### 4.2 Seam record
`SeamDef`:
- `seam_id`;
- `presentation_anchor_ids[]` or equivalent render geometry reference.

Semantic equality ignores decorative render data.

### 4.3 Compartment record
`CompartmentDef`:
- `compartment_id`;
- `label_key` or short label metadata;
- `traversed_seam_ids[]` sorted canonically by ID;
- `openable` (normally true);
- presentation anchor/visual reference.

Semantic validation rejects empty traversed seam sets for participating openable compartments unless a specifically reviewed tutorial exception exists; default is reject.

### 4.4 Socket record
`SealSocketDef`:
- `socket_id`;
- `covered_seam_ids[]`, unique and sorted;
- `enabled`;
- accessibility identity key/pattern/icon ID;
- presentation anchor/shape references.

`trigger_compartment_ids[]` is derived at load/certification time and must never be an independently authoritative authored field. If cached, cache is diagnostic only and must be checked against derivation.

### 4.5 Placement contract
`PlacementDef`:
- `mode`: `FIXED | CHOOSE_EXACT_K | CHOOSE_UP_TO_K | CHOOSE_FROM_GROUPS`;
- `k` where required;
- `fixed_socket_ids[]`;
- finite group definitions only where Phase-4 permits.

### 4.6 History contract
`HistoryDef`:
- `mode`: `FIXED_HISTORY | CHOOSE_FROM_AUTHORED_HISTORIES | ARRANGE_REQUIRED_SET | ARRANGE_BOUNDED_SUBSET`;
- `min_steps`, `max_steps`, and `exact_steps` when appropriate;
- `fixed_history[]`;
- `authored_history_choices[][]`;
- `eligible_compartment_ids[]`;
- `required_open_ids[]`;
- `forbidden_open_ids[]`;
- `fixed_position_constraints[]` as `(compartment_id, checkpoint)`;
- `precedence_constraints[]` as `(before_id, after_id)`.

All histories use distinct compartment IDs. No repeated opening exists in v1.

### 4.7 Evidence predicate tagged union
`EvidencePredicateDef` is a tagged union with exactly the Phase-4 vocabulary:
- `INSTALLED`;
- `NOT_INSTALLED`;
- `BREAKS_AT`;
- `BREAKS_BEFORE`;
- `BREAKS_AFTER`;
- `INTACT_THROUGH`;
- `FINAL_INTACT`;
- `FINAL_BROKEN`;
- `OPENED`;
- `UNOPENED`;
- `OPENS_AT`;
- `SAME_BREAK_STEP`;
- `BREAKS_EARLIER`.

Each carries typed IDs/checkpoints rather than free-form expressions. Unknown tags are hard errors, never ignored.

### 4.8 Certification/reasoning metadata
Preserve Phase-5 fields:
- expected certification class;
- expected solution class count;
- acceptance projection;
- legal-space estimate;
- deduction tags/count;
- setup class;
- trigger motifs;
- similarity signature;
- anti-repetition note;
- human/oracle-free review status;
- redundant-evidence review;
- generated certifier result hash/version.

Generated certification fields are build artifacts/reports, not replacements for authored semantics.

### 4.9 Localization metadata
No player-visible prose is embedded as authoritative logic. Cases reference localization keys for title/objective/evidence rendering/tutorial/hints. IDs remain stable internal values and may have short accessible display aliases.

## 5. Canonicalization, IDs, hashes and versions
Determinism requires stable normalization.

### 5.1 Stable IDs
IDs are case-sensitive ASCII tokens with a restricted safe character set `[A-Z0-9_\-]` or one documented equivalent. Runtime never depends on array insertion order for identity.

### 5.2 Set normalization
Every semantic set is normalized as unique IDs sorted by binary/ordinal ID order before hashing or comparison. Duplicate authored IDs are validation errors rather than silently deduplicated.

### 5.3 History normalization
Opening history is an ordered list and is never sorted. Its order is mechanically meaningful.

### 5.4 Predicate normalization
For hash purposes, predicate records normalize field names/tags and operand ordering only where the predicate is symmetric. `SAME_BREAK_STEP(A,B)` may canonicalize the two socket IDs; `BREAKS_EARLIER(A,B)` may not.

### 5.5 Mechanics hash
Compute `mechanics_hash` over canonical semantic case data excluding localization strings, decorative assets, estimated solve time and other presentation-only fields. Use a standard cryptographic hash available reliably in the chosen runtime/tooling (SHA-256 is the default recommendation).

### 5.6 Result hashes
Generate:
- `submission_hash` from case mechanics hash + canonical installed set + exact ordered history;
- `trace_hash` from rules version + case mechanics hash + full checkpoint trace;
- `certification_hash` from certifier version + rules version + mechanics hash + normalized solution/equivalence report.

Hashes detect drift; they do not provide security/anti-cheat guarantees.

### 5.7 Version behavior
- `schema_version`: serialization shape;
- `rules_version`: resolver semantics;
- `save_schema_version`: persistence shape;
- `certifier_version`: enumeration/report implementation version.

A change to tear ordering/predicate semantics requires a rules-version change and recertification of all shipping cases. Pure UI changes do not.

## 6. Shared deterministic resolver contract
The Domain resolver accepts only:
- immutable validated `CaseModel`;
- immutable legal `SubmissionSnapshot`.

It returns either a structural validation error or immutable `RunTrace`.

Pseudo-contract, not production code:

`resolve(case, submission) -> RunTrace`

RunTrace contains:
- `case_id`;
- `mechanics_hash`;
- `rules_version`;
- exact installed socket set;
- exact opening history;
- checkpoint 0 witness/open state;
- ordered checkpoints 1..N;
- per checkpoint: opened compartment, traversed seam set, unordered set of newly broken sockets, cumulative per-socket break state/time, cumulative opened set;
- final unopened set;
- per-predicate boolean result plus retrospective causal references where deterministically derivable;
- overall success boolean;
- submission_hash;
- trace_hash.

### 6.1 Resolution order
For checkpoint i:
1. read one compartment from history;
2. mark it opened;
3. read its traversed seam set;
4. collect every currently intact installed socket whose covered seams intersect traversed seams;
5. set all collected witnesses broken at checkpoint i atomically;
6. materialize checkpoint snapshot;
7. continue.

Never resolve same-checkpoint seals sequentially in a way that changes later same-checkpoint eligibility.

### 6.2 Break time
A witness has exactly one value from `{NEVER, 1..N}`. Once non-NEVER, it never changes.

### 6.3 Predicate evaluation
Predicates are pure functions over submission + complete trace. Comparison predicates require both witnesses to break where Phase 4 says so; e.g. `BREAKS_EARLIER(A,B)` is false if either is NEVER.

### 6.4 No frame/time dependence
Resolver receives no delta time, random generator, locale, animation speed, input device or wall-clock. Same canonical inputs and rules version must yield byte-equivalent normalized trace semantics across supported machines.

## 7. Replay representation
Replay is not a recording of animations or inputs. It is a deterministic trace of semantic checkpoints.

Canonical replay payload can store:
- `case_id` + mechanics hash;
- rules version;
- canonical submission snapshot;
- expected trace hash;
- optional cached checkpoint trace.

On load, if case mechanics hash/rules version still match, runtime may regenerate and verify. If they do not match, old replay is marked incompatible rather than force-applied to changed content.

Scrubbing selects semantic checkpoint 0..N and asks presentation to render that state. Presentation cannot insert, delete, reorder or merge checkpoints.

## 8. Offline certifier contract
The certifier uses the exact Domain validation/resolver/predicate code.

Input:
- one validated case package;
- certification policy/options;
- expected certification metadata.

Output report:
- case ID/mechanics hash/rules version/certifier version;
- legal placement count;
- legal history count;
- legal combined submission count;
- satisfying submission count;
- exact satisfying submission hashes;
- normalized solution signatures;
- equivalence groups under declared acceptance projection;
- classification: `UNIQUE_EXACT | UNIQUE_OBSERVABLE | MULTI_VALID_INTENTIONAL | INVALID_AMBIGUOUS`;
- zero-solution failure if applicable;
- redundant-evidence analysis;
- predicate discrimination report;
- trace hashes for satisfying solutions;
- search duration/memory diagnostic only;
- generated certification hash.

### 8.1 Exhaustive bounds
Shipping cases must have finite explicit action spaces. Certifier must exhaust them rather than rely on random sampling.

Recommended content gate:
- default target <= 1,000,000 legal combined submissions per case;
- soft warning above 250,000;
- hard review above 1,000,000;
- an exception may use pruning/backtracking only if completeness is proven and the algorithm remains deterministic;
- no shipping case may be accepted merely because brute-force certification “usually finds” a solution.

These are tooling/scope bounds, not player difficulty targets.

### 8.2 Enumeration order
Use canonical deterministic ordering:
1. socket combinations in lexicographic ID order;
2. histories in lexicographic/permutation order defined from canonical eligible compartment order;
3. no parallel worker ordering may alter normalized output.

Parallelism is allowed only if results are sorted/canonicalized before report/hash generation.

### 8.3 Equivalence grouping
Default solution signature follows Phase 4: installed socket set + exact history + complete break-time vector + opened/unopened set.

If `acceptance_projection` exists, certifier computes both exact and projected signatures. It must report what distinctions were ignored so an author cannot accidentally hide ambiguity.

### 8.4 Redundant-evidence analysis
For each authored predicate P:
- remove P from the conjunction;
- exhaustively recertify or reuse complete solution table;
- compare satisfying equivalence classes.

If removing P does not change the accepted class set, flag P as redundant.

Default shipping gate: redundant evidence is rejected, except documented tutorial prose/reinforcement where Phase 5 explicitly permits it. Redundancy flags do not automatically rewrite content.

### 8.5 Human-review handoff
Machine certification cannot prove fun or human deduction quality. Every shipping case report links/exports:
- expected primary/secondary deduction tags;
- legal submission count;
- number of solution classes;
- redundancy status;
- trigger motif/similarity signature;
- candidate human solve notes.

Human reviewer must mark `oracle_free_human_review = PASS` only after solving without live hypothetical-result assistance and without exhaustive manual enumeration. Late cases require the Phase-5 deduction-count/anti-repetition gates.

## 9. Persistence schema
Use small explicit files rather than one opaque monolith where practical.

Recommended logical records:
1. `profile.json` — progression, achievements mirror, hint state, per-case solved metadata;
2. `settings.json` — controls/accessibility/audio/display preferences that are appropriate to roam;
3. optional `drafts.json` — current unsolved edit drafts, non-essential and safe to discard if incompatible;
4. local-only machine configuration file for graphics/window/device-specific settings; do **not** roam machine-specific settings through Steam Cloud.

Steam's current Cloud guidance explicitly recommends avoiding machine-specific configuration in Cloud and notes smaller/separated files reduce unnecessary synchronization.

### 9.1 Profile fields
- `save_schema_version`;
- `profile_id` random stable UUID-like token;
- `profile_generation` monotonic integer;
- `created_utc`;
- `last_modified_utc` diagnostic only, not sole merge authority;
- `install_id` diagnostic source identifier;
- `campaign_content_version`;
- per case:
  - `case_id`;
  - last known mechanics hash;
  - solved bool;
  - `first_solved_utc` if known;
  - `solve_generation` monotonic per-record generation;
  - optional successful submission/trace hash for review;
  - hints opened bitset/maximum hint step;
  - demo provenance flag where relevant;
- campaign/act completion derivable from cases rather than stored as sole authority;
- achievement facts or emitted-achievement IDs;
- import ledger entries.

### 9.2 Atomic local writes
Every save mutation:
1. serialize deterministic complete new record to temporary sibling file;
2. flush/close;
3. validate parse/checksum/schema from temp;
4. rotate current valid main to `.bak`;
5. atomic rename/replace temp -> main where OS permits;
6. never overwrite both main and backup in one unverified step.

Optional checksum is corruption detection, not security.

### 9.3 Recovery
Load order:
- validate main;
- if invalid, validate backup;
- if backup valid, recover it and preserve corrupt main with timestamp/diagnostic suffix;
- if neither valid, preserve both and start conflict/recovery UX rather than silently zeroing progress.

Draft corruption may discard only drafts, never progression.

## 10. Save migration
Each save schema migration is a pure version-to-next-version transform with fixtures.

Rules:
- never skip unknown future versions;
- migrate a copy, validate, then atomically replace;
- preserve solved status for stable `case_id` whenever a mechanical content revision remains acceptance-compatible;
- if a shipped case's mechanics change incompatibly, explicit migration policy must decide whether prior completion remains grandfathered. Do not infer this from hash mismatch alone;
- removal/replacement of a case must not corrupt act/campaign completion; progression is recomputed against the installed content manifest and legacy completion retained in history if needed.

## 11. Steam Cloud and Dynamic Cloud Sync
Steam Cloud is a transport/synchronization layer, not the authority for game semantics.

### 11.1 Cloud file set
Cloud-roam:
- progression profile;
- accessibility/control preferences intended to follow the player;
- optional drafts only if proven safe and useful.

Local-only:
- resolution/window/display adapter selection;
- device-specific performance settings;
- crash logs/cache.

### 11.2 Normal startup conflict/merge
When local and Cloud versions differ, parse and validate both before writing anything.

Automatic merge is allowed only for monotonic/union-safe facts:
- solved case = OR if both records refer to compatible stable case semantics;
- highest hint step seen = max;
- achievement emitted = OR;
- earliest known first-solve timestamp = min when both credible;
- import ledger = set union;
- accessibility/settings: latest explicit per-setting generation wins, not whole-file blind overwrite.

Draft edit submissions are **not** union-merged. Pick the newer compatible draft by per-record generation or present a conflict choice if both diverged materially.

A save with an unknown future schema, invalid checksum, incompatible profile identity, or ambiguous non-monotonic state may not be auto-merged.

### 11.3 Dynamic Cloud Sync during process lifetime
Because Steam can notify the application that local Cloud-managed files changed while the game is running, future implementation must handle a platform callback/event.

On notification:
1. if in menu/case select with no unsaved edit transaction, reload/merge immediately through the normal validated merge path;
2. if in `CASE_EDIT` with unsaved draft changes, snapshot the draft locally, merge progression/settings, then restore draft only if case mechanics hash remains compatible;
3. if in committed reveal/replay/result, never mutate the active immutable run trace; queue reload until return to a safe boundary;
4. if newly synchronized data changes solved/progression status, update menus after the safe merge;
5. if an irreconcilable conflict exists, enter `SAVE_CONFLICT_GATE` before any overwrite.

Use Steam's write-batch/suspend hints where the chosen Steam integration supports them, but correctness must not depend on the hint succeeding.

### 11.4 Conflict UX
Conflict screen names the meaningful difference (`This device solved 18 cases; Cloud solved 20; both contain unique solves`) and prefers safe merge when possible. Never reduce a richer monotonic union to a timestamp winner.

## 12. Demo -> full import
Demo and full game share save-schema concepts but have distinct product namespaces/paths.

Import runs only in full game and is idempotent.

### 12.1 Import identity
An import candidate is accepted only if:
- source profile validates;
- source save version can migrate;
- a demo case maps to a full-game `case_id`;
- mechanics hash/declared acceptance contract is identical for “solved” carryover.

A demo wrapper derived from a late case but mechanically modified never marks the campaign case solved.

### 12.2 Merge semantics
- solved campaign-identical demo case -> union into full profile;
- hint usage -> max/union for same case if carried;
- supported accessibility/control preferences -> merge by explicit setting generation or first-import preference;
- never overwrite a newer full-game solution/draft with demo data;
- record `(demo_profile_id, source_generation, import_contract_version)` in import ledger;
- repeating the same import produces no additional change.

### 12.3 Import tests
Must cover: fresh full profile, already-progressed full profile, repeated import, old demo save migration, corrupted demo save, mechanically changed wrapper, same case solved on both sides, Cloud arriving before/after import.

## 13. Input abstraction
Gameplay code consumes semantic actions, not physical buttons.

Required actions include:
- `NAV_UP/DOWN/LEFT/RIGHT`;
- `PANEL_PREV/NEXT`;
- `PRIMARY`;
- `SECONDARY_OR_CONTEXT`;
- `BACK/CANCEL`;
- `UNDO`, `REDO`;
- `TOGGLE_PLAN`, `TOGGLE_EVIDENCE`;
- `COMMIT`;
- `REPLAY`;
- `RETURN_TO_EDIT`;
- `REVEAL_NEXT_STEP`;
- `REVEAL_SKIP`;
- `PAUSE`;
- `HELP_HINT`.

Controller, keyboard and mouse map into the same action layer. Mouse hover may change focus/highlight only; no mechanical information is mouse-exclusive.

### 13.1 Focus graph
Every interactive semantic item has stable `focus_id`. Workbench neighbor graph is generated from authored presentation anchors and can have explicit author overrides.

Automated validation detects:
- focus node with no inbound route when it should be reachable;
- trapped focus cycles;
- missing escape/back path;
- focus target hidden at active layout breakpoint.

Every modal remembers originating semantic focus ID and restores it when valid.

### 13.2 Glyphs
Presentation asks input adapter for current glyph family. Game functionality does not depend on glyph art. Rapid switching between keyboard/mouse/controller may update prompts without changing focus or state.

## 14. Responsive layout acceptance matrix
Minimum mandatory test surfaces:
- 1280x800 at 100%, 150%, 200% text scale;
- 1920x1080 at 100%, 150%, 200%;
- 2560x1440 at 100%, 200%;
- representative ultrawide layout as robustness check, not a special gameplay mode.

For each:
- Workbench participating labels readable;
- active rail can open/close without hiding required controls;
- no evidence meaning clipped at 200%;
- no horizontal text crawl required to understand a single evidence predicate;
- focused control remains visible after reflow;
- controller can reach all actions;
- commit legality reason remains readable;
- no UI component shrinks core text to compensate for overflow.

At high scale, switch to narrow/drawer layout rather than compressing Workbench below readability floor.

## 15. Localization/font architecture
All player-facing strings use localization keys with parameterized tokens for witness labels/checkpoint numbers. Do not concatenate grammar from fragments where word order may differ by language.

Evidence rendering uses semantic templates such as:
- `evidence.breaks_at(socket_label, checkpoint)`;
- `evidence.breaks_earlier(a_label, b_label)`.

Requirements:
- fallback locale always available;
- font stack supports every actually shipped language before that language can be enabled on store page;
- missing glyph detection in automated localization QA;
- pseudo-localization with expansion and accented/mixed-width characters;
- CJK line-break/overflow tests if those locales enter release scope;
- right-to-left architecture should avoid irreversible assumptions, but RTL is not promised unless fully tested;
- IDs never translated; display labels may be localized where required.

No language list from Phase 7 becomes a promise through this architecture.

## 16. Performance/resource assumptions
Seal Break is compact 2D/restrained 2.5D and must not require high-end hardware for simulation.

Design budgets/gates:
- Domain resolve for one normal submission: target <1 ms on a typical desktop development machine and effectively unnoticeable on handheld; release gate is no visible frame hitch, not a specific benchmark promise;
- case load/domain model build: target <50 ms excluding cold asset IO;
- UI/reveal should hold stable frame pacing at 60 Hz on Steam Deck-class hardware; optional lower refresh must remain fully playable;
- no authoritative physics simulation;
- no per-frame solver/certifier work;
- certifier runs offline/editor/headless, never during ordinary gameplay;
- bounded cabinet scene assets; texture/audio memory must be measured in vertical slice before content scaling;
- animation Skip/Instant path must not wait on visual particles/tweens to finish before semantic result is available.

Performance regressions are profiled on worst dense shipping case and at 200% text scale.

## 17. Logging and diagnostics
Debug/development logging may emit:
- case ID/mechanics hash/rules version;
- submission hash;
- trace hash;
- state-machine transition;
- save generation/migration path;
- Cloud merge decision category;
- certifier counts and classification;
- input/focus reachability failures.

Do not log localized user text as semantic authority. Release logs should avoid unnecessary personal/platform identifiers. No telemetry is required by the design.

A human-readable trace dump for a committed run should list each checkpoint, opened compartment, traversed seams, newly broken witnesses and predicate outcomes. This is a QA tool, not player oracle UI.

## 18. Test strategy
### 18.1 Golden resolver fixtures
Create small canonical fixtures for every Phase-4 edge:
- one seam/one seal;
- one seal covering multiple seams crossed same checkpoint -> one break;
- multiple seals same checkpoint -> identical break time regardless animation order;
- already-broken witness ignores later triggers;
- omitted compartment -> witness may remain NEVER;
- every history mode;
- every evidence predicate;
- same-step and earlier comparisons;
- fixed/precedence legality;
- invalid duplicate compartment/opening.

Each fixture stores expected normalized trace and trace hash.

### 18.2 Runtime-vs-certifier parity
For every shipping case and a generated sample of legal submissions:
- runtime Domain resolver trace == certifier resolver trace;
- success bool == predicate conjunction in certification;
- normalized submission/trace hashes match.

Best architecture is literally shared module/code, with parity tests still retained to catch adapter/schema differences.

### 18.3 Property/fuzz tests
Generate bounded valid/invalid case models/submissions and assert:
- resolver deterministic across repeated calls;
- no break time decreases/changes after first break;
- newly broken set is subset of previously intact installed set;
- every break at i has nonempty seam intersection with opening i;
- an intact final seal has no trigger intersection with any opened compartment's traversed seams;
- checkpoint count equals history length;
- opened set monotonically grows by exactly one each checkpoint;
- replay from canonical submission yields same trace hash;
- permutation of semantic set serialization does not change mechanics/trace hashes;
- locale/input/presentation speed do not change Domain output.

### 18.4 Persistence tests
Power-loss simulation at each atomic-write step; malformed JSON/resource; truncated main; bad backup; future version; migration chain; duplicate save generations; Cloud union; contradictory profile IDs; Dynamic Sync notification during edit/reveal; demo import repetition.

### 18.5 UI/input tests
Controller-only, keyboard-only, mouse without drag, 1280x800, 200% scale, focus restoration, glyph switching, all history modes, exact-K full budget, mismatch/replay/scrub, hint overlay, reduced motion.

Automated UI tests may assert reachability/layout bounds; manual handheld review remains required.

## 19. Content build/certification pipeline
Future implementation repository should treat authored cases as data and run a release pipeline:
1. schema parse;
2. semantic validation;
3. mechanics hash generation;
4. exhaustive certifier;
5. expected-class/count comparison;
6. redundancy report;
7. similarity/anti-repetition metadata report;
8. localization-key existence check;
9. presentation-anchor/focus-graph validation;
10. human-review status check;
11. package certified manifest.

Release build fails if a shipping case has zero solutions, unexpected ambiguity, unsupported rules version, invalid socket/trigger relation, missing required localization key, stale certification hash after mechanics change, or human-review status FAIL/PENDING where required.

## 20. Technical authority and implementation dependency order
Future dedicated repository implementation should proceed in this dependency order.

### 20.1 12A — bootstrap/domain first
- pin supported stable Godot version;
- repository/build/test harness;
- semantic schema parser/validator;
- pure Domain model;
- deterministic resolver + predicate evaluator;
- canonicalization/hash utilities;
- golden fixtures;
- headless certifier skeleton.

Gate: all Phase-4 rules executable without UI.

### 20.2 12B — vertical slice
Implement SB_01/SB_02 plus one later F2/F4-style diagnostic using placeholder presentation:
- edit state;
- commit snapshot;
- resolve/reveal separation;
- replay/scrub;
- mismatch;
- controller focus path;
- basic save.

Gate: one complete true loop, not merely resolver tests.

### 20.3 12C — core systems
All four history modes, placement modes required by floor campaign, all frozen predicates, undo/redo, hints shell, progression, robust case loading.

### 20.4 12D — content population
Import/certify the frozen campaign. Content is rejected if certifier or human anti-repetition gates fail; implementation does not invent new mechanics to rescue it.

### 20.5 12E — UX/accessibility/platform
Responsive rails, 200% text, controller/keyboard/mouse, reduced motion, high contrast, localization pipeline, Steam achievements/Cloud adapter, demo packaging/import.

### 20.6 12F — adversarial QA
Persistence corruption, Dynamic Cloud Sync, duplicate/idempotent imports, input/focus, skip/replay parity, certifier/runtime parity, save migrations, achievement idempotency.

### 20.7 12G — empirical gates
External playtests: tutorial clarity, whether non-oracular human deduction survives, content repetition, handheld evidence density, solve times, hint quality, price/content perception. These may tune presentation/content or cut cases but cannot silently alter frozen mechanics.

### 20.8 12H — release candidate
Certified shipping manifest, truthful case count, store/demo agreement, release-time engine/platform recheck, performance, packaging, regression.

## 21. Explicit implementation prohibitions
Future implementation must not:
- put authoritative tear logic in animation callbacks;
- run a solver live to color hypothetical edits;
- duplicate resolver semantics separately for runtime and certifier;
- infer trigger compartments from decorative pixels/collision physics at runtime;
- use floating-point geometry to decide seam intersection authority;
- serialize scene nodes as the only save authority;
- overwrite Cloud/local saves using timestamp alone where union-safe progress exists;
- let Dynamic Cloud Sync mutate an active committed trace;
- make mouse drag mandatory;
- add durability/randomness/partial damage/repeated opening;
- introduce production mechanics inside the factory.

## 22. Phase-8 acceptance checklist
PASS because the design now specifies:
1. supported engine/runtime direction without preview-build dependency;
2. domain/application/presentation/platform/certifier boundaries;
3. exact runtime state machine and commit/reveal transaction;
4. canonical semantic case schema;
5. stable IDs/canonicalization/hash/version contracts;
6. one shared deterministic resolver;
7. replay trace semantics independent of animation;
8. exhaustive certifier input/output, bounds, equivalence and redundancy checks;
9. human-review handoff;
10. atomic persistence/recovery/migrations;
11. deterministic Cloud conflict/merge and Dynamic Sync safe boundaries;
12. idempotent demo import;
13. semantic input abstraction/focus graph;
14. 1280x800/200%-text acceptance matrix;
15. localization/font architecture without unverified language promises;
16. compact performance assumptions;
17. logging/test/golden/property/parity requirements;
18. future implementation dependency order;
19. explicit anti-oracle and anti-drift prohibitions.

## 23. Phase verdict
**PHASE 8 PASS.** Important technical design ambiguities are resolved sufficiently to proceed to whole-game simulation on paper.

No production implementation was started.

Next phase: **Phase 9 — Whole-game simulation on paper.** Walk first boot, first five minutes, first hour, midgame, late game, completion, demo-to-full transition, return after absence, controller/handheld path, hint use, repeated mismatch, Cloud conflict/Dynamic Sync, corrupted save, content-version change, and hostile/unusual player behavior. Repair contradictions in authoritative files rather than documenting them as vague implementation problems.