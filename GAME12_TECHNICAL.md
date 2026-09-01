# GAME #012 — PHASE 8 TECHNICAL IMPLEMENTATION SPECIFICATION

Date: 2026-09-01
Status: **PHASE 8 COMPLETE**
Product: **OPENWORK** *(provisional working title)*
Authority: technical architecture and implementation contracts. `GAME12_MECHANICS.md` remains authoritative for gameplay truth; `GAME12_CONTENT.md` for campaign/certification; `GAME12_UX.md` for interaction/presentation; `GAME12_COMMERCIAL.md` for progression/demo/platform policy.

No production code is created by this phase.

---

## 1. Engine / runtime direction

### Decision
Use **Godot 4.x, standard GDScript build**, targeting the current supported stable branch at implementation bootstrap. As of 2026-09-01, Godot's release policy lists 4.7 as supported and 4.8 as development; Godot 4.7.2 was released 2026-08-18. The dedicated implementation repository should therefore start on **Godot 4.7.2-stable or the newest later 4.7.x patch available at bootstrap**, not a 4.8 development build.

Do not freeze the design to a patch forever. Freeze the **policy**: supported stable minor, latest patch, upgrade only after green deterministic fixtures + save compatibility tests.

### Why Godot fits OPENWORK
- native 2D/UI-first architecture without 3D production burden;
- deterministic grid logic can live in plain data/services independent of scene nodes;
- strong controller/keyboard/mouse input mapping and focus navigation;
- lightweight Windows/Linux builds suit Steam/Deck;
- localization and scalable UI are first-class enough for the small text surface;
- testable non-rendering rules code is practical;
- no engine physics, networking, ECS, animation graph or heavyweight scene system is required for puzzle truth.

### Steam integration direction
Use a thin adapter around an actively maintained Godot Steamworks binding compatible with the chosen Godot stable version, with **GodotSteam/GDExtension as the preferred candidate**, but do not allow that binding to enter the domain rules layer. Exact plugin version is an implementation dependency to pin after bootstrap compatibility verification.

Steam must be optional at runtime. If Steam initialization fails or the executable is launched outside Steam, local campaign play, settings, saves and input remain functional. Steam-only features degrade to unavailable, never to game failure.

### Fresh platform evidence
Current Steamworks guidance continues to support action-based Steam Input; in native mode the game receives logical actions rather than physical button assumptions and may request the bound action origin for correct glyph display. Current Steam Cloud documentation remains the platform integration target for cross-device save continuity. These reinforce adapter boundaries rather than direct Steam calls from gameplay/UI logic.

---

## 2. Authority layering

The runtime must have one directional truth flow:

`IMMUTABLE CASE DATA -> RULES CORE -> DERIVED TOPOLOGY -> PREDICATE RESULTS -> SESSION STATE -> PRESENTATION`

The reverse direction is forbidden. UI nodes may request an action; they may not invent legality, component IDs, holes, predicate truth or progression.

### Layer A — immutable authored content
Contains only case schema fields from Phase 5 plus localization keys and curated metadata. No cached topology is trusted.

### Layer B — deterministic rules core
Pure conceptual services/functions operating on value data:
- schema validation;
- placement footprint derivation;
- placement legality;
- final occupied-cell set construction;
- remaining-open set;
- component derivation;
- hole classification;
- marker/boundary/area derivation;
- predicate evaluation;
- canonical assignment serialization.

No scene tree, rendering object, Steam API, save file or wall clock is allowed as an input to rules truth.

### Layer C — derived topology snapshot
Immutable result for one committed board state. Runtime may cache it, but it is always reproducible from case + placements + rules version.

### Layer D — session/controller state
Selected piece, board cursor, history, temporary held/reposition state, objective focus and inspect state. These are gameplay-session convenience state, not puzzle truth.

### Layer E — presentation
Board renderer, component outlines, hole halos, cards, sound, animation and menu focus consume snapshots/events.

### Offline certifier
The certifier must call the **same rules evaluator contract** as runtime. It may enumerate assignments offline, but must never maintain a second implementation of topology semantics. The certifier adds search/certificate/reporting around the shared evaluator; runtime excludes enumeration modules from normal gameplay paths.

---

## 3. Version responsibilities

Use four distinct version concepts; never collapse them into one integer.

### `rules_version`
Changes only when mechanics/evaluation semantics change: e.g. connectivity, hole definition, predicate semantics, canonicalization. Any change invalidates all content certificates and requires golden-fixture migration/re-certification.

### `case_schema_version`
Changes when serialized authored-case structure changes while gameplay semantics may remain identical. Loader owns migrations from supported older schema versions to the current in-memory schema.

### `content_version`
Per-case authoring revision already frozen in Phase 5. A material board/marker/piece/predicate change increments it and invalidates that case certificate. It is part of demo-import compatibility.

### `save_schema_version`
Changes when persistence structure changes. Save migration must not depend on scene/UI state.

Additionally record build version for diagnostics, but build version does not determine puzzle truth.

---

## 4. Conceptual data model

Names below are conceptual, not mandatory code identifiers.

### `CellCoord`
Integer `x,y`; canonical coordinate ordering is `(y,x)` for sorting, exactly matching Phase 4.

### `BoardDefinition`
- width, height;
- canonical sorted fixed-solid coordinates.

All omitted in-rectangle cells are base OPEN.

### `MarkerDefinition`
- stable marker ID;
- cell;
- visual slot only.

### `PieceDescriptor`
- shape enum: MONO1 / BAR2 / BAR3;
- orientation policy: FIXED_H / FIXED_V / ROTATABLE.

### `PieceInstance`
- stable authored instance ID;
- descriptor.

IDs support editing/history/UI. They do not defeat interchangeable-piece quotienting.

### `Placement`
- instance ID;
- canonical anchor;
- orientation.

### `CanonicalFootprint`
- descriptor shape;
- resolved orientation;
- sorted occupied coordinates.

### `PredicateDefinition`
Tagged union corresponding exactly to Phase-4 atomic grammar. Boundary sets stored as bitmask N=1,E=2,S=4,W=8. Area multisets always normalized sorted ascending at load validation.

### `CaseDefinition`
- IDs/versions/title key/act/sequence;
- board;
- markers;
- piece instances;
- predicates;
- allow_multiple;
- family/difficulty/demo/achievement metadata.

### `TopologyComponent`
- deterministic component ID;
- sorted cell collection or compact cell mask;
- area;
- sorted marker IDs;
- boundary bitmask;
- `is_hole = boundary_mask == 0`.

### `TopologySnapshot`
- remaining-open mask;
- component list in deterministic ID order;
- cell -> component ID lookup;
- hole component IDs;
- sorted component-area multiset;
- sorted hole-area multiset;
- sorted component-boundary-signature multiset.

### `PredicateResult`
- predicate stable index/ID;
- boolean current truth;
- optional presentation-safe derived facts such as current count/current areas/current marker relation.

It must never contain candidate-solution information.

### `EvaluationSnapshot`
- placements canonicalized;
- completeness flag;
- topology snapshot;
- predicate results;
- solved flag = complete AND all predicates true.

### `Certificate`
Exactly the Phase-4 payload plus schema/content versions and canonical content hash. Shipping builds may include expected certificate metadata for integrity/regression, but runtime does not require certifier search counts to play a case.

---

## 5. Deterministic serialization / hashing

### Case canonicalization
Before hashing:
- normalize coordinates to integer arrays;
- sort fixed solids `(y,x)`;
- sort markers by stable ID and validate unique cells;
- preserve piece instance IDs for authored identity but normalize descriptor enum strings;
- sort unordered predicate set by canonical serialized descriptor because target conjunction order has no semantics;
- sort all area multisets;
- normalize boundary sets to integer bitmasks;
- omit author notes/localized rendered strings from gameplay content hash unless their change is intentionally supposed to invalidate certificate (default: no).

Hash a canonical UTF-8 representation with an implementation-standard cryptographic hash such as SHA-256. Exact JSON whitespace/object-property order must not affect the hash.

### Placement canonicalization
For active runtime history, instance identity is preserved. For solution identity/certifier counting, use Phase-4 canonical tuples and quotient interchangeable instances.

### Determinism prohibition
Rules/certificate outputs must never depend on:
- dictionary iteration order;
- scene/node order;
- frame timing;
- random number generator;
- locale;
- floating-point geometry;
- wall clock;
- Steam account state.

Grid/rules core uses integer/boolean/set semantics only.

---

## 6. Application / scene-state architecture

Recommended top-level composition:

### `AppRoot`
Long-lived composition root. Owns services, navigation and current profile state. It does not own puzzle rules truth.

### Services
- `ContentRepository` — load/validate case manifests;
- `RulesService` — deterministic evaluator facade;
- `ProgressionService` — derive unlocks from solved IDs + frozen gate rules;
- `SaveService` — atomic persistence/migrations/recovery;
- `PlatformService` — Steam/null implementation;
- `InputService` — logical actions + glyph source;
- `LocalizationService` — keys/locales;
- `SettingsService` — validated settings;
- `AchievementService` — recompute eligibility from authoritative progress;
- optional `DiagnosticsService` — local logs, never required for truth.

### Screen states
1. Boot / save recovery / platform initialization.
2. Title / Continue / New Campaign / Demo Import prompt where applicable.
3. Campaign Map / Case Select.
4. Puzzle Session.
5. Pause / Settings overlay.
6. Success transition / next-case options.
7. Credits/completion surfaces.

Menus may be separate scenes/screens. Puzzle truth remains a domain object passed into a board presenter.

### Boot ordering
1. initialize basic logging and local paths;
2. load app build/config;
3. initialize localization default;
4. load/validate content manifest;
5. load local save with migration/recovery;
6. initialize platform adapter asynchronously/defensively;
7. reconcile Cloud only through the save service policy;
8. recompute unlocks/achievements from authoritative solved state;
9. surface demo-import offer if eligible;
10. enter title/campaign.

Platform failure cannot block step 8/10.

---

## 7. Puzzle session / placement transaction semantics

### Committed state
Committed puzzle state is the ordered history of player transactions plus current placement map. The rules evaluator consumes only the resulting placements, because placement order has no semantic effect.

### Transaction types
- `PLACE(instance, new_placement)`
- `REMOVE(instance, old_placement)` if exposed as committed removal;
- `REPOSITION(instance, old_placement, new_placement)` — one user-visible transaction although internally validated as remove + legal place;
- `RESET(previous_complete_placement_map)` — one undoable transaction is optional; minimum frozen UX requires reset recovery, not necessarily undo-reset. Implementation should prefer reset as one undoable transaction unless memory/UI tests reveal confusion.

### Placement commit
1. construct candidate footprint;
2. validate against immutable case + all other committed placements;
3. if invalid: no mutation/history entry;
4. if legal: mutate placement state atomically;
5. derive one new evaluation snapshot;
6. append history transaction;
7. emit presentation event from old snapshot -> new snapshot;
8. if solved, request progression commit.

### Reposition held state
Picking up a piece creates a **temporary UI transaction state**, not a committed save state. The old placement remains authoritative until a new legal position commits. Cancel restores it with zero rules-history change. If app exits/crashes while held, reopen from last committed placement state; never serialize a half-held piece.

### Undo
Undo reverses the last committed transaction deterministically and recomputes evaluation. It does not mutate solved-history: once the campaign records a case solved, replay/undo does not unsolve it.

### Session persistence
Unsolved in-case placement state may be persisted for convenience, but is non-monotonic and lower authority than solved progression. Persist only committed placements plus case ID/content version. On content-version mismatch, discard resume placements but never discard already compatible solved progress without migration logic.

---

## 8. Progression authority

The save file must **not store unlocked acts/cases as independent truth**. Store monotonic solved case IDs with compatible content identity; derive unlocks every boot and after every solve using Phase-7 rules.

This repairs a future stale-state risk: progression rule changes or imported solved sets cannot leave contradictory cached unlock flags.

### Frozen derivation
- Act I cases 1–3 sequential.
- After C3, remaining cases in current unlocked act are free order.
- next act when current act solved count >=4/6.
- Act VI additionally requires >=24 total campaign solved.
- finale requires >=4 of other 5 Act-VI solved.
- campaign complete when finale solved.
- 100% when all shipping campaign case IDs solved.

### Hostile skip-path resolution
Potential contradiction: 4/6 gates could permit repeated skipping of the exact cases that first teach later predicate vocabulary. **Repair:** content/campaign metadata must designate tutorial prerequisites for *first introduction only*, but these are already represented by Act-I C1–C3 sequential and act ordering. A later act may not contain a predicate whose only teaching case can be skipped in the immediately previous act unless that predicate has already appeared in a mandatory earlier case. This is a Phase-9 simulation gate and content sequencing responsibility, not a new progression currency.

No case-specific unlock flags are needed beyond deterministic prerequisites encoded in campaign manifest.

---

## 9. Persistence architecture

### Save separation
Use at least:
- `profile/progress` — solved cases, tutorial/glossary seen, completion facts, last selected case, achievement reconstruction metadata;
- `settings` — accessibility/audio/input/UI preferences;
- `resume` — optional current puzzle committed placements.

They may be physically bundled, but logical separation is required so progress merge does not overwrite settings and corrupt resume never destroys solved history.

### Atomic local writes
For each save unit:
1. serialize validated new payload to temporary file in same filesystem location;
2. flush/close;
3. verify parse + checksum/hash if used;
4. rotate existing primary to bounded backup;
5. atomically rename temp to primary where platform permits;
6. retain at least one known-good backup.

Never edit the primary file in place.

### Load recovery order
1. primary validates and supported version -> use it;
2. primary corrupt -> try backup;
3. backup valid -> restore/copy as primary and notify non-blockingly;
4. neither valid -> preserve corrupt files for diagnostics, start safe empty local profile after explicit warning; do not fabricate solved progress.

### Save migrations
Migrations are pure transformations `vN -> vN+1`, chained sequentially and fixture-tested. Before migrating, preserve source copy. A migration must be idempotent at its destination version.

### Future-version refusal
If `save_schema_version > supported_current`, **do not load and do not overwrite it**. Enter a guarded state offering continue without saving / create separate older-version profile only if implementation supports it; default safest release behavior is refuse profile mutation and explain that the save was created by a newer build. Cloud upload is disabled for that profile until a capable build runs.

This is a hard anti-downgrade corruption rule.

---

## 10. Steam Cloud conflict / merge policy

### Principle
Cloud is transport, not authority over local facts. The application owns semantic merge.

### Monotonic progress merge
When local and Cloud saves are both valid and compatible:
- solved case IDs = union of compatible solved facts;
- tutorial/glossary seen = union;
- campaign completion/100% are recomputed;
- achievements recomputed;
- last-selected/navigation state chooses the newer valid profile metadata only as convenience;
- optional resume state is **not unioned**: choose newest compatible resume by commit timestamp/build metadata, or discard if ambiguous;
- settings are not silently unioned by individual timestamp unless implemented/tested. Prefer current device local settings; Cloud settings may be a separate opt-in policy.

### Version conflict
- if either side is future save version: preserve it and refuse destructive merge/upload from older runtime;
- if both supported but require migration: migrate copies locally first, then merge;
- if one side corrupt: quarantine it and retain the valid side; never upload corruption over valid data;
- if content IDs changed: only facts passing compatibility mapping survive.

### Clock distrust
Wall-clock timestamp may choose only non-critical convenience state. It must never decide which solved set wins, because clocks can be skewed. Monotonic solved union is stronger.

### Cloud write sequence
Semantic merge -> atomic local commit -> platform upload/sync. If upload fails, local progress remains valid and queues future sync. A Steam error never rolls back a solved case.

---

## 11. Demo -> full import transaction

Demo and full game have separate product/app identities. Full game reads an export/importable demo profile through an explicit compatible source path or platform-supported location; demo must never directly write the full game's primary save.

### Import identity
Record in full profile:
- stable `import_source_id` derived from demo profile identity + source product;
- demo save/schema/rules manifest versions;
- imported compatible solved IDs;
- import transaction version;
- completion marker.

### Idempotent transaction
1. discover candidate demo profile read-only;
2. validate source product/provenance and supported schema;
3. derive compatible solved IDs by exact case ID + approved content compatibility table;
4. preview what will import;
5. user confirms Import;
6. construct merged full profile in memory;
7. union compatible solved/tutorial facts;
8. settings remain full-game values unless user separately chooses `Use Demo Settings` using whitelist;
9. recompute unlocks and achievement eligibility;
10. atomic full-save commit;
11. only after successful commit record import-source completion within that same committed payload;
12. award/sync Steam achievements after authoritative local commit.

Repeating the same import produces the same solved set and no duplicate side effects. If crash occurs before atomic commit, import is offered again; after commit it is already complete.

### Achievement repair
Do not import achievement flags. Achievement service derives them from solved case IDs + curated case metadata. This ensures demo/full, offline/online and Cloud restore converge.

### Demo settings whitelist
May include text scale, reduced motion, high contrast, audio levels, language and shared remaps where action IDs match. Must exclude product-specific navigation/resume/cloud metadata.

---

## 12. Steam / platform abstraction

Define an interface-style platform facade with a null/offline implementation and a Steam implementation.

Capabilities:
- initialization / availability;
- user/platform identity only if needed for platform APIs;
- achievement read/unlock/request sync;
- Cloud availability/read/write/sync status;
- logical input-origin/glyph lookup if Steam Input is used natively;
- overlay/store hooks only if later needed;
- platform language hint as a suggestion, never rules input.

Rules, progression and saves cannot call Steam directly.

### Achievements
Achievement unlock requests occur only after local authoritative progression commit. Failure queues re-evaluation; on next platform availability, compare all 12 eligibility rules against progress and unlock missing achievements. Never relock Steam achievements.

### Controller glyphs
The UI renders glyphs from the current binding/action origin when available; otherwise engine/local generic glyph mapping. No gameplay prompt hardcodes “A/B/X/Y” as semantic truth because remapping and PlayStation/Nintendo layouts exist.

---

## 13. Input action abstraction

Canonical logical action vocabulary should cover behavior, not devices:
- `NAV_UP/DOWN/LEFT/RIGHT`
- `BOARD_PLACE`
- `BOARD_UNDO`
- `BOARD_PICKUP_REPOSITION`
- `BOARD_ROTATE_PREV/NEXT` or one rotate action if UX confirms parity
- `PIECE_PREV/NEXT`
- `TOPOLOGY_INSPECT`
- `OBJECTIVE_DETAILS`
- `CANCEL/BACK`
- `PAUSE`
- `RESET_HOLD`
- generic `CONFIRM`

Mouse maps to the same commands via pointer targeting rather than bypassing command handling.

Action labels/glyph prompts use localization/action-label keys. Physical button names never enter tutorial truth.

Focus navigation regression is required for every screen with controller-only input.

---

## 14. Localization boundaries

Rules/content store localization keys only:
- case title key;
- tutorial/callout key;
- predicate family templates;
- glossary entries;
- settings/actions/achievement strings.

Marker IDs A–F are stable puzzle symbols but presentation may localize labels only if doing so preserves exact cross-predicate identity. Default safer launch plan is icon/Latin-symbol marker identity independent of sentence grammar.

Predicate text is composed from structured templates; never parse localized text back into rules.

Numeric/area values are integer formatting only; no locale-dependent decimal logic exists.

Pseudo-localization and longest-string UI tests are required before shipping language claims.

---

## 15. Performance / memory budgets

Runtime boards are <=9x9 = <=81 cells. Performance must be designed for instant interaction, not micro-optimized prematurely.

### Runtime evaluation budget
On representative low-end target hardware/Deck-class device:
- placement legality + full topology + predicates should target **<1 ms typical, <4 ms hard engineering budget** per committed placement in release builds;
- no visible frame hitch above one 60 Hz frame due to rules evaluation;
- evaluation may simply recompute the entire <=81-cell topology; incremental graph algorithms are unnecessary complexity unless profiling proves otherwise;
- ghost movement evaluates footprint legality only, not hypothetical topology/predicates.

### Memory
A puzzle snapshot should remain tiny. Avoid retaining topology snapshot per cursor movement. History may retain transactions and optionally previous snapshots, but a 4-piece case makes memory negligible.

### Offline certifier
Certifier may enumerate all legal canonical complete assignments exhaustively. Hard design ceiling is 4 pieces on <=81 cells. Certification is an authoring/build tool and may take seconds for pathological candidates, but target accepted representative cases should certify comfortably on a developer machine.

Suggested curation engineering gate:
- accepted shipping case certification target <10 seconds on ordinary contemporary desktop for full exhaustive run;
- warn >10s;
- reject/rework >60s unless a proven deterministic pruning optimization preserves exhaustive equivalence.

These are workflow budgets, not gameplay difficulty gates.

### Critical prohibition
Runtime **never enumerates candidate solutions**, even if the board is small enough. Certifier/search modules are tooling-only.

---

## 16. Test architecture

### A. Golden topology fixtures
Minimum fixture matrix includes:
- single exterior-connected field;
- two components;
- one zero-boundary hole;
- diagonal leak that remains disconnected cardinally;
- edge opening preventing hole status;
- multiple holes;
- all four boundary signatures;
- marker membership across split;
- fixed-solid vs placed-solid provenance producing same topology.

For each fixture assert exact deterministic component IDs, areas, markers, boundary masks, hole IDs.

### B. Predicate tests
Every grammar atom tests true/false, boundary modes EXACT/INCLUDES/AVOIDS, multisets with repeats, zero holes, malformed references rejection and conjunction ordering invariance.

### C. Placement tests
Out-of-bounds, fixed-solid collision, marker protection, overlap, fixed/rotatable orientation, canonical anchor and interchangeable-piece solution quotient.

### D. Certificate/canonical-solution fixtures
Keep tiny cases with known raw assignment count, canonical assignment count and canonical solution count. Assert certificate hash invalidation on rules/content changes.

### E. Representative content verification
Every accepted shipping case must have a checked certificate matching current rules/content hash. CI/build verification fails if a case lacks a current valid certificate.

### F. Persistence fixtures
- primary valid;
- primary corrupt + backup valid;
- both corrupt;
- every supported migration chain;
- future-version refusal;
- interrupted temp write;
- resume content-version mismatch;
- old build cannot overwrite future save.

### G. Demo import fixtures
- demo only -> import;
- full only -> no import needed;
- overlapping solved sets -> union;
- incompatible revised case -> not imported;
- settings whitelist;
- repeated identical import -> no change;
- crash/restart before commit -> safe retry;
- achievements reconstructed, not duplicated.

### H. Cloud conflict fixtures
- local subset / cloud superset;
- local superset / cloud subset;
- disjoint solved sets -> union;
- skewed clocks;
- corrupt side;
- future-version side;
- resume conflict;
- upload failure after local commit.

### I. Progression fixtures
Exhaustively test plausible solved-set patterns around every 4/6 gate, 24-total Act-VI requirement and 4/5 finale gate. Derived unlocks must be stable after import/Cloud union.

### J. UX/input/accessibility regression
Controller-only navigation across all screens; remapped controls; glyph switching; mouse/controller alternation; 1280x800 9x9 + six objectives; text scale; high contrast; reduced motion; focus restoration after modal/pause/reposition; hold-reset safety.

### K. Anti-oracle regression
Static/code-boundary test where practical: runtime package/API surface must not expose certifier enumeration or functions such as remaining-solution count/candidate ranking. Ghost preview test asserts topology snapshot is not computed for uncommitted placements.

---

## 17. Telemetry / privacy posture

No account, backend or online service is required.

Default launch posture: **no custom gameplay telemetry required**. Steam aggregate/store/platform data may exist outside game logic, but puzzle truth/progression never depends on it.

If optional analytics are later added for playtest/release diagnostics:
- explicit privacy disclosure;
- minimize fields;
- no board-state stream needed for normal release;
- no personally identifying payload designed by the game;
- no third-party analytics SDK allowed merely to count session length if it meaningfully increases binary/privacy burden;
- analytics failure/offline state is invisible to progression;
- opt-out must not affect achievements/features.

Local diagnostic logs may include app version, case ID, content/rules/save versions and error codes; avoid storing Steam identifiers unless needed for platform debugging and disclosed appropriately.

---

## 18. Hostile pass: Phase-7 rules vs architecture

### H1 — “newer save” ambiguity
Phase 7 says never blindly overwrite newer full progress with demo data. Timestamp-based “newer” is unsafe for monotonic progression.
**Repair frozen here:** solved-case truth merges by compatible union; timestamps only choose non-monotonic convenience state. Future schema version always wins preservation, not overwrite.

### H2 — cached unlock flags can stale
If saves persist unlocked acts separately, demo/cloud unions can create contradictory progression.
**Repair:** save solved IDs; derive all unlocks. Cached unlock display may exist but is never authoritative.

### H3 — achievement double-award/import trust
Importing demo achievement flags could diverge from full curated metadata.
**Repair:** reconstruct all achievement eligibility after every authoritative progress merge/import. Platform unlock is idempotent.

### H4 — incompatible demo content
Case IDs can match while a puzzle was revised.
**Repair:** compatibility requires case ID plus content-version/compatibility manifest approval. No solved import on incompatible revision.

### H5 — settings merge can damage accessibility preference
“Keep newer” can replace the user's current device accessibility choice with a demo/cloud value.
**Repair:** local full-game settings win by default; demo settings require explicit action. Cloud settings policy must be separate from progress union.

### H6 — resume state and solved state conflict
Cloud may contain an old unsolved placement for a case local progress already solved.
**Repair:** solved progression is monotonic. Resume can coexist for replay but can never unsolve or block completion. If ambiguous, discard resume rather than progression.

### H7 — reasoning primers and privacy
A “repeated unsolved engagement” trigger could tempt retry telemetry or account counters.
**Repair:** primer eligibility can be computed locally from optional per-case local engagement counters; counters are non-critical, never achievements, never Cloud-required and may be omitted entirely if UX chooses simple glossary access.

### H8 — runtime certifier temptation
Small boards make it technically easy to provide “is this state still solvable?” hints.
**Repair:** certifier enumeration is tooling-only dependency. Runtime package/API does not call or expose candidate enumeration. Anti-oracle is architectural, not merely UI policy.

### H9 — Steam outage
Achievement/Cloud/platform initialization could delay boot.
**Repair:** local save commits first; platform sync is secondary/retriable. No Steam availability required for rules/progression.

### H10 — demo/full Steam Cloud cross-app collision
Separate appIDs must not point both products at the same mutable primary save path without semantic import control.
**Repair:** demo writes demo-owned provenance save; full reads/imports read-only then writes only full-owned save.

Result: Phase-7 progression/import/achievement policy is technically coherent after the repairs above; no commercial rule requires reopening.

---

## 19. Future implementation dependency order

This is a handoff order for the future dedicated repository, not work to execute in the factory.

### T1 — deterministic domain core
Case value types, schema validator, footprint legality, topology derivation, predicates, canonicalization, golden tests.

### T2 — offline certifier harness
Enumeration, interchangeable quotienting, certificate generation/verification, representative fixture counts.

### T3 — local content pipeline
Manifest/case loader, certificate integrity, localization keys, sample certified vertical-slice cases.

### T4 — puzzle session model
Placement/reposition/history/reset/evaluation snapshot; no art dependency.

### T5 — minimal board/UI vertical slice
Controller-first cursor, tray, objectives, current-state inspect, success. Validate 1280x800 early.

### T6 — save/progression
Atomic save, migration, solved-union semantics, derived unlocks, resume.

### T7 — campaign/content population
Certified cases, act gates, demo manifest, family/achievement metadata.

### T8 — accessibility/localization/input polish
Remapping, glyph abstraction, text scaling, reduced motion, high contrast, pseudo-localization, full focus regression.

### T9 — platform adapter
Steam achievements/Cloud/Input integration behind interfaces; offline/null path remains tested.

### T10 — demo/full import
After both products' save manifests are stable, implement compatibility/import fixtures and crash safety.

### T11 — adversarial QA / empirical gates
Deck/readability, save corruption, Cloud, brute-retry behavior, content exhaustion/repetition and performance.

Do not integrate Steam before the deterministic/local product works. Do not author the full 36 cases before certifier + vertical slice prove semantics and UX.

---

## 20. Explicit technical non-goals

No launch requirement for:
- networking/backend/account system;
- multiplayer;
- deterministic lockstep/replay networking;
- physics simulation;
- runtime procedural case generation;
- runtime solution solver;
- Workshop/editor;
- mod API;
- scripting language for predicates;
- user-generated content validation;
- database server;
- custom launcher;
- always-online DRM;
- mobile port architecture;
- console certification architecture;
- complex ECS;
- multithreaded topology evaluation;
- live-ops telemetry pipeline.

If future implementation complexity grows because of any of these, cut it rather than redefine the frozen product.

---

## 21. Phase-8 acceptance conclusion

The design has a clean implementation path:
- supported stable Godot 4.x, currently 4.7.2 as of 2026-09-01;
- pure integer deterministic rules independent of scenes/platform;
- one shared evaluator contract for gameplay and offline certification;
- explicit schema/rules/content/save versions;
- scene/UI never stores gameplay truth;
- placement/reposition/history transactions are deterministic;
- local save is atomic with backup/migration/future-version refusal;
- Cloud and demo progress merge monotonic compatible solved facts instead of overwriting them;
- achievements are reconstructable;
- Steam is optional and isolated;
- runtime contains no solver enumeration;
- complete fixture/test matrix covers topology, persistence, import, Cloud, input and progression;
- implementation order proves the rules core/certifier/vertical slice before content and platform expansion.

**PHASE 8 = COMPLETE.**

## NEXT PHASE — Phase 9 Whole-Game Simulation
Simulate the frozen product on paper through hostile, concrete journeys and repair contradictions. Minimum scenarios:
1. fresh keyboard/mouse first boot through first 6 onboarding cases;
2. controller/Deck first boot at 1280x800 with text scaling/high contrast/reduced motion;
3. a player repeatedly skips the two hardest cases in each act and tries to reach Act VI/finale;
4. a strong puzzle player brute-tests placements instead of reasoning in early, mid and mastery cases;
5. a struggling player uses unlimited undo, inspect and reasoning primers without case-specific hints;
6. first demo run -> partial demo completion -> install full game -> import -> achievements/unlocks;
7. existing full progress plus older/newer demo import attempt;
8. two-device Cloud conflict with disjoint solved sets and conflicting resume/settings;
9. offline solve several cases -> Steam returns -> achievement/Cloud reconciliation;
10. corrupted local primary with valid backup; both-corrupt path; future-version save opened by older build;
11. content update changes one case after it was solved and after it existed in demo;
12. late-game 9x9 / 4-piece / 5–6 predicate case on handheld for readability and interaction fatigue;
13. 30-case floor vs 36-target campaign value path and likely session/playtime shape;
14. 100% completion / replay / postgame filter without retention grind;
15. rapid input during placement animation, reposition, undo, reset-hold and success transition.

Phase 9 must record exact contradictions/repairs and carry unresolved empirical risks into Phase 10 rather than hiding them.