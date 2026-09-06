# GAME #018 — PHASE 8 TECHNICAL IMPLEMENTATION SPECIFICATION

Date: 2026-09-06
Game: **LOCAL TIME**
Status: PHASE 8 COMPLETE — PHASE 9 WHOLE-GAME SIMULATION NEXT
Production implementation: NO

Authority: prior active Game #018 files. This is an implementation contract, not production code and not permission to add gameplay grammar.

## 1. Runtime / engine direction

Baseline implementation direction: **Godot 4.7.x stable, GDScript, Windows/Steam first**. As of 2026-09-06 Godot 4.7 is a supported release line and 4.7.2 is the current stable maintenance release (2026-08-18); 4.8 is still development. Start a dedicated implementation repository on the latest stable 4.7 patch available at bootstrap and pin the exact version in project documentation. Do not move to a preview/dev engine for convenience.

Use Godot primarily for scene/UI/input/rendering/audio. The puzzle authority is a small pure deterministic domain layer independent of scene-node order, animation, frame time, physics and Steam APIs. This permits headless/unit-style validation and avoids making the diorama scene tree the save format.

Rendering target is deliberately modest: compact stylized 2.5D/3D dioramas, <=8 relevant sites and <=3 clocks. Prefer the least expensive renderer that preserves the final art thesis; Compatibility is acceptable if presentation survives. Do not make a renderer-specific visual effect part of logical readability.

## 2. Layer boundaries

Four hard layers:

1. **Domain/Core** — immutable-ish canonical state values, legal actions, Resolve, objectives, hashing. No Node references, tweens, wall-clock time, RNG, Steam calls or localized strings.
2. **Content** — authored case definitions compiled/loaded into validated domain definitions. No arbitrary executable gameplay scripts.
3. **Presentation/Application** — diorama nodes, HUD, animation, reason-trace rendering, input focus, menus, save orchestration.
4. **Platform** — filesystem, Steam Cloud/achievements, controller glyph source, optional telemetry. Platform failure cannot change puzzle rules.

The presentation may request a domain action and render its returned transition result; it may never mutate canonical puzzle state directly.

## 3. Canonical data mapping

### CaseDefinition (authored, immutable during play)
- schema_version, case_id, chapter, title_key, goal_key, district_skin
- site_defs[], object_defs[], clock_defs[], socket_defs[], carrier_defs[]
- transition_rules[], lockout_rules[], accept_rules[], dispatch_rules[], coupled_rules[]
- objective_expr, fatal_conditions[]
- placement_move_limit?, resolve_limit
- placement_completion_allowed=false baseline
- introduced/reinforced families
- validation metadata: required_insight, ordered human_proof, solution witnesses, shortest counts, dominant_strategy_attack, anti_enumeration_reason, repetition_signature, accessibility_notes, cut_condition

### RunState (canonical mutable play state)
- run_schema_version, case_id, definition_revision
- beat_index, placement_moves_used
- clock_socket_by_id
- site_process_state_by_id, site_terminal_flags
- object_process_state_by_id, object_location_by_id, object_terminal_flags
- sorted milestone IDs, sorted lockout IDs
- carrier position/payload state
- current committed planning placement if it differs from last Resolve checkpoint

Derived values such as LocalTime(site), current predicates, objective truth, legal socket highlights and reason prose are not persisted as authority.

### ProfileState
- profile_schema_version, install/profile UUID
- completed case IDs and optional mastery/challenge flags
- latest valid checkpoint reference per case
- settings/accessibility/control preferences
- tutorial acknowledgements
- achievement intent/outbox IDs where platform submission is pending
- monotonic save_generation and last_modified_utc for conflict UX only

No localized display text is stored as canonical gameplay state.

## 4. Stable IDs and serialization

All gameplay entities/rules use authored stable string IDs unique within a case. Never serialize scene paths, Node instance IDs, enum ordinals whose ordering may change, resource memory addresses or translated strings.

Canonical serialization uses explicit versioned fields and deterministic ordering: maps become key-sorted records for hashing; sets become sorted arrays. Unknown future fields may be ignored only when the reader explicitly supports forward-compatible handling; otherwise preserve the old save and invoke recovery rather than guessing.

Definition revisions are content hashes or monotonically versioned authored revisions. A checkpoint created against a changed definition must pass a migration/compatibility function before loading.

## 5. Deterministic Resolve core

Pure conceptual API:
`ResolveResult resolve(CaseDefinition def, RunState pre)` -> `{post_state, trace_events, objective_result, terminal_result}`.

Resolve follows Phase-4 order exactly: validate -> derive coverage -> Snapshot0 -> lockout candidates -> beneficial candidates -> accept/dispatch/coupled candidates -> simultaneous non-carrier commit -> one carrier step -> recompute current/objective -> increment beat.

Candidate evaluation is side-effect free. Commit order may be sorted by stable ID for deterministic traces, but outcome must be identical under shuffled iteration order. Tests deliberately randomize collection iteration before comparison.

No floating-point value participates in logical rules. Footprints, sockets, labels, counters and state enums are discrete. Visual world coordinates map to authored logical socket/site IDs before entering the core.

## 6. Reason-trace contract

Core emits structured `TraceEvent`, not English prose:
- event_type
- rule_id
- actor/entity IDs
- relevant clock/time label IDs
- pre_state token, post_state token
- same_resolve_group / phase
- permanent flag

Presentation maps events to localization keys and icons. Every canonical mutation must correspond to >=1 trace event; no-change Resolve emits a structured NO_CHANGE event. Trace is reproducible from the same pre-state/action and is not persisted as puzzle authority.

## 7. State hashing and replay diagnostics

Define `canonical_state_hash` over normalized CaseDefinition revision + RunState gameplay fields, excluding timestamps, settings, trace prose, animation state and platform metadata. Use a stable documented digest available in the implementation stack; never rely on language runtime `hash()`.

Record optional diagnostic tuples in development/test builds: `{case_id, pre_hash, action, post_hash}`. Golden witnesses can replay actions and assert hashes. Shipping saves need not retain an unbounded action log.

Hash equality is a debugging/solver identity tool, not cryptographic anti-cheat.

## 8. Solver architecture

The exact solver consumes the same CaseDefinition and invokes the same legality/Resolve core as gameplay. It is not a second implementation of rules.

Search node = normalized canonical RunState plus remaining budgets. Edges = legal committed clock relocations and Resolve actions under authored constraints. Planning-only inspection is absent. Deduplicate by canonical state hash plus collision-safe state equality.

Solver outputs: solvable?, shortest Resolve/move metrics, witness action sequences, reachable-state count, certified dead states when requested, alternate solution witnesses and diagnostics. A DEAD UI claim is allowed only from exact certification for the current definition/budget.

Solver is an authoring/test tool; shipping builds need not expose broad search. Runtime may include only bounded certification support if performance is proven, otherwise authored fatal rules and budget exhaustion remain the immediate failure path.

## 9. Content validator

Validation pipeline for every authored case:
1. schema/stable-ID uniqueness;
2. references resolve and states belong to declared finite enums;
3. socket footprints are in board and relevant-site coverage is unambiguous except explicit REQUIRES_SET semantics;
4. only eight frozen rule families appear;
5. dependency graph contains no illegal reverse transition/hidden timer/arbitrary script;
6. finite budgets/finite reachable graph are established;
7. solver finds >=1 solution and records shortest metrics;
8. promised alternate-solution counts are verified;
9. same-Resolve prerequisite/arrival flags are explicit, never defaulted from missing data;
10. shuffled-order determinism tests pass;
11. human-proof/repetition/anti-enumeration metadata exists from Chapter 2 onward;
12. target-display content density metadata respects <=3 clocks/<=8 relevant sites.

The validator cannot certify fun or a human proof merely because a solver succeeds. Human review remains a shipping gate.

## 10. Persistence and atomic saves

Separate profile and per-case checkpoints. Never serialize live animation/tween/node state.

Atomic local write contract:
1. serialize to a new temp file;
2. validate schema and checksum/digest by reading the temp representation;
3. flush/close;
4. preserve previous known-good file as rotating backup;
5. atomically replace/rename where supported;
6. only then advance profile pointer/save_generation.

Keep at least last-known-good profile plus previous checkpoint generation. If a write fails, continue play when safe, clearly report save failure, and do not delete the previous valid generation.

On load: validate structure, version, definition compatibility and required IDs before committing anything to live state. If latest checkpoint fails, try known-good backup; if only a case checkpoint is bad, preserve profile completion/settings and offer restart of that case. Never partially reconstruct unknown gameplay state.

## 11. Save/schema migration

Every persistent document has explicit schema_version. Migrations are pure old-document -> new-document transformations tested against fixture saves. Keep migration paths for every publicly released schema; pre-release development schemas may be deliberately invalidated only before public demo distribution.

Case-definition changes use explicit compatibility rules. Safe examples: presentation/localization-only revision; added nonlogical metadata. Unsafe examples: changed socket coverage, rule ordering, initial object state. Unsafe revision invalidates that checkpoint but must preserve completion/profile records where logically valid and offer case restart.

## 12. Demo -> full import

Demo and full game share profile schema and canonical LT01–LT06 case IDs. Full-game import is **idempotent and monotonic**:
- discover demo profile once or on explicit retry;
- parse/validate without modifying either source;
- merge completion/mastery/tutorial flags by union;
- settings use explicit user choice or full-game-current preference, not blind overwrite;
- checkpoints import only when destination has no newer/more advanced compatible checkpoint; never replace a full-game completed case with demo in-progress state;
- write merged full profile atomically;
- mark source fingerprint/import record only after successful destination write;
- repeating import produces the same result.

Never delete demo saves as part of import.

## 13. Steam Cloud conflict/recovery policy

Local disk is always a valid offline play path. Cloud synchronization is platform transport, not canonical merge logic.

For non-conflicting generations, sync newest validated generation. If both local and cloud changed since the last common sync marker, do not silently choose by wall-clock timestamp. Present a conflict choice with useful facts: device/source, save generation, last modified time, campaign completion count and latest case/checkpoint. Preserve both candidates locally before choice.

Profile-level safe monotonic fields such as completed case IDs/achievements may be union-merged only through an explicitly tested merge function. In-progress checkpoint state is never field-wise merged; choose one whole compatible checkpoint per case. A corrupt cloud candidate cannot overwrite a valid local save. Upload occurs only after local validation and atomic persistence.

Steam unavailable/offline => game starts and saves locally; achievement intents may queue idempotently for later submission.

## 14. Input abstraction

Domain actions know nothing about device. Application actions include `focus_next_clock`, `focus_prev_clock`, `enter_place`, `nav_socket(direction)`, `confirm`, `cancel`, `resolve`, `undo_move`, `undo_resolve`, `inspect`, `toggle_trace`, `replay`, `pause`, `zoom/pan`.

Mouse drag and click-place resolve to the same placement command. Controller spatial navigation uses authored/generated socket neighbor graph with deterministic fallback; no pointer emulation is required. All logical actions are remappable except unavoidable platform/system actions.

Hot-plug switches glyph presentation without changing focus/state. Simultaneous devices cannot double-submit a Resolve during transition lock. Input is disabled only while a state-changing command is being committed; skip/fast-animation cannot alter computed result.

## 15. Display / Deck assumptions

Logical state must remain readable at **1280x800** with UI scale baseline. Automated/screenshot QA should cover 1280x800, 1920x1080 and common ultrawide safe framing; ultrawide may letterbox/extend decoration rather than reveal hidden logical advantage.

Critical labels are UI overlays/vector/font-rendered, not baked English texture. High-contrast/pattern modes alter presentation only. Motion reduction and animation speed never affect logic.

Target 60 fps on modest Steam-compatible PC/Deck-class hardware, but puzzle correctness must remain identical at low frame rates. <=8 logical sites and small carrier counts mean CPU simulation should be negligible; solver work is never run synchronously every frame.

## 16. Localization pipeline

All player-facing strings use stable localization keys with parameterized placeholders for semantic values. Source English is externalized from scenes/content. Rule text is generated from bounded rule templates plus localized entity/state names; avoid concatenating grammar fragments that assume English word order.

Clock labels are semantic IDs rendered through a locale-aware display function where necessary, while canonical equality uses IDs. Numeric clock art cannot be the only representation of a gameplay condition.

Pseudo-localization, long-string expansion, missing-key checks, CJK/font coverage and right-to-left layout resilience are technical QA gates even if launch-language selection is narrower. Localized strings never influence solver equality or state hashes.

## 17. Animation / logic separation

Application sends command -> core returns complete post-state + structured events -> save checkpoint can be committed -> presentation animates the already-known result. Closing/skipping animation snaps to post-state; it cannot cancel half a logical transition.

Autosave after Resolve occurs against canonical post-state independent of whether animation finished. On crash during presentation, reload shows the committed post-state, not a half-animated scene.

Diorama actors/carriers interpolate only between canonical authored endpoints. Physics collisions, navigation agents and animation callbacks cannot trigger gameplay transitions.

## 18. Golden tests LT01–LT06

Each demo case has checked-in canonical definition fixtures plus witness sequences.

- LT01: RAW -> RISEN, relocation leaves RISEN, no-change Resolve does not advance, final Bridge NOW succeeds.
- LT02: narrow 08:05 bakes safely; broad exposure closes unprotected flower; earlier/later-looking labels never reverse BAKED/CLOSED.
- LT03: dispatch requires simultaneous Snapshot0 Bridge OPEN + Station 08:05; ambiguous overlap rejected; protected-flower failure trace exact.
- LT04: bake, handoff/arrival and acceptance are separate by default; newly arrived parcel cannot accept in same Resolve.
- LT05: harmful and beneficial candidates from same snapshot both occur where compatible; lockout precedence cannot be bypassed by iteration order.
- LT06: at least the promised solution count is solver-verified; final distinct labels and persistent milestones survive relocation.

Golden assertions include normalized post-state, structured trace event types/rule IDs and canonical state hashes.

## 19. Property / invariant tests

Generate or enumerate bounded legal micro-definitions and assert:
- same state/action => same post-state/hash/trace structure;
- shuffled entity/rule storage order => same logical outcome;
- moving clocks without Resolve never mutates persistent milestones/process history;
- a Resolve advances any ordered entity <=1 state;
- lockouts/milestones obey monotonic contract;
- no ambiguous relevant-site local time can enter a valid Resolve;
- no-change Resolve changes only budget/beat bookkeeping and trace;
- replay/animation/input glyph changes do not change state hash;
- undo Resolve exactly restores pre-state hash and counters;
- save-load round trip preserves canonical state hash;
- solver witness replay reaches objective;
- every mutation has a trace event.

## 20. Persistence/corruption tests

Fixtures cover truncated JSON/resource, bad checksum, unknown schema, missing stable ID, changed case definition, interrupted temp write, valid backup + corrupt latest, cloud/local divergence, repeated demo import, demo older than full checkpoint, full profile absent, Steam offline and queued achievement resubmission.

Pass criterion is no silent progress loss and no partial invented state.

## 21. Steam/platform adapter tests

Use a fake platform adapter in normal automated tests. Verify Cloud conflict decision data, achievement idempotency, offline startup/save, controller hot-plug and absence of gameplay dependency on Steam initialization. Real Steam integration is a later dedicated-repository acceptance pass, not factory work.

## 22. Technical implementation order for dedicated repository

**T0 Bootstrap:** pin stable Godot version; project opens; pure-domain test harness runs.

**T1 Domain model:** IDs, definitions, RunState, coverage/current predicates, legality, canonical normalization/hash.

**T2 Resolve:** all eight semantic families, Snapshot0 ordering, structured trace; LT01–LT03 golden tests.

**T3 Carrier/objective/undo:** LT04–LT06, checkpoints, solver-facing action API.

**T4 Solver + validator:** exact search, witness replay, dead certification, schema/content checks, human-review report output.

**T5 Persistence:** atomic profile/checkpoints, migrations, corruption recovery, demo import.

**T6 Presentation vertical slice:** LT01–LT06 diorama/HUD/reason trace, mouse/controller abstraction, accessibility baseline; no full content population yet.

**T7 Platform:** Steam Cloud/achievements adapter and conflict UX after local persistence is proven.

**T8 Content population/tooling:** author/validate campaign using frozen schemas and proof gates.

**T9 QA/release:** Deck/display, localization, performance, corruption, demo/full, platform packaging and empirical UX gates.

Do not build all 30–36 cases before T0–T6 prove the vertical slice.

## 23. Technical acceptance criteria

Phase-8 implementation contract is satisfied later only when:
1. core logic runs independently of scenes/frame time;
2. LT01–LT06 golden tests pass from data definitions;
3. identical inputs are deterministic and iteration-order invariant;
4. content solver invokes production core rather than duplicate rules;
5. authored invalid/ambiguous cases fail validation before runtime;
6. saves are versioned, atomic, recoverable and corruption-tested;
7. demo import is repeated safely without regressing full progress;
8. cloud conflicts never silently discard divergent valid progress;
9. every state mutation has structured localizable reason evidence;
10. mouse/controller/Deck paths map to the same commands;
11. localization and accessibility presentation cannot affect hashes/rules;
12. animation can be skipped/crashed/reloaded without logical divergence;
13. no production gameplay rule exists only in a scene script or bespoke case callback;
14. empirical gates from prior phases remain visible as tests/playtest obligations rather than being declared solved by architecture.

## 24. Phase acceptance

The technical direction now maps the frozen finite-state design to a deterministic, testable and recoverable implementation without inventing production gameplay. Engine choice is deliberately replaceable at the presentation boundary; the core contracts, data IDs, Resolve order, solver, saves, import/cloud semantics and acceptance gates are authoritative.

**PHASE 8 TECHNICAL SPECIFICATION = COMPLETE.**

# NEXT DESIGN STEP — PHASE 9 WHOLE-GAME SIMULATION

Walk the frozen product end-to-end on paper: first boot/settings -> LT01–LT06 -> chapter transitions -> representative Cases 07–36 -> mastery -> quit/load/cloud conflict -> demo-to-full -> controller/Deck -> hostile behavior (Resolve spam, socket scanning, undo abuse, repeated import, corrupted checkpoint, offline Steam). Track contradictions against Phases 3–8, repair canon rather than handwave, and determine whether content volume/proof diversity still survives. Do not start production implementation.