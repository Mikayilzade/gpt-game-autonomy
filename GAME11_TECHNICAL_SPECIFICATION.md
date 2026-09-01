# GAME #011 — MISSING STEP — PHASE 8 TECHNICAL IMPLEMENTATION SPECIFICATION

Date: 2026-09-01
Status: **PHASE 8 SUBSTANTIAL INCREMENT — CORE ARCHITECTURE FROZEN**
Authority: `START_HERE.md` -> `STATUS.md` -> `GAME_INDEX.md` -> `GAME11_PRODUCT_THESIS.md` -> `GAME11_MECHANICAL_ARCHITECTURE.md` -> `GAME11_CONTENT_ARCHITECTURE.md` -> `GAME11_UX_PRESENTATION_ARCHITECTURE.md` -> `GAME11_COMMERCIAL_RETENTION_MODEL.md` -> this file for implementation architecture.

This document specifies implementation boundaries only. It does not start production code and does not change frozen game rules.

## 1. Runtime direction
Preferred implementation baseline: **Godot 4.7.2 stable + GDScript**.

Fresh 2026 check:
- Godot 4.7.2 stable released 2026-08-18;
- Godot 4.8 was still in dev builds at the end of August 2026;
- 4.7 is a supported stable branch.

Sources:
- https://godotengine.org/article/maintenance-release-godot-4-7-2/
- https://godotengine.org/download/preview/
- https://docs.godotengine.org/en/latest/about/release_policy.html

Why this fits:
- deterministic low-state puzzle logic does not require a heavier engine;
- Control/UI tooling suits controller-first one-screen layout;
- PC/Linux/Steam Deck export path is appropriate;
- GDScript is sufficient for bounded exhaustive enumeration and deterministic simulation at launch ceilings.

Engine choice is implementation-direction authority, not a gameplay rule. A later implementation session may upgrade to a newer stable Godot patch/minor only after regression tests prove identical rules/certificates.

## 2. Architectural rule: one pure Rules Core
Gameplay truth must live in a presentation-independent deterministic module.

Conceptual layers:
1. **Rules Core** — case state, edit application, phase-anchor resolution, tick simulation, targets, trace production.
2. **Validator/Certifier** — exhaustive legal edit enumeration, certificate production/verification, duplicate/equivalence analysis.
3. **Case Repository** — loads immutable canonical case data and matching certificates.
4. **Campaign Service** — progression quotas, completed IDs, unlocks, ending/mastery flags.
5. **Persistence Service** — versioned local saves, migrations, demo import, atomic write/recovery.
6. **Platform Adapter** — Steam achievements/cloud/input features behind optional interface.
7. **Presentation/UI** — planning, Preview, RUN playback, result explanation, accessibility.

Forbidden architecture:
- opcode semantics in animation scripts;
- target truth calculated separately by UI;
- campaign unlock logic encoded in scene paths;
- case-specific scripts overriding rules;
- solver behavior used directly as normal-player recommendation logic.

## 3. Canonical enum/value types
Conceptual strongly bounded values:

```text
Opcode = PUSH | TURN | STAMP | CLAMP
TrackId = A | B | C | D
Lane = 0 | 1
Orientation = N | E
EditContractType = SINGLE | TWO_NAMED_TRACKS
TargetKind = FINAL_LANE | FINAL_ORIENTATION | STAMP_COUNT | BLOCKED_PUSH_COUNT
UniquenessBand = UNIQUE | EQUIVALENT_MULTI | TRACE_MULTI | UNSAT
```

Use integer/string serialized representations only through explicit versioned codecs. Never depend on engine enum ordinal remaining stable across versions.

## 4. Canonical case schema
Runtime schema mirrors Phase 5 and is the only gameplay input.

Minimum normalized object:

```text
CaseData {
  case_id: string
  case_data_version: int
  case_rules_version: int
  act_id: string
  ordinal: int
  title_key: string
  teaching_tags: [string]
  challenge_family_tags: [string]
  tracks: [TrackData]
  initial: InitialStateData
  horizon_ticks: int
  edit_contract: EditContractData
  target: [TargetClauseData]
  presentation: PresentationMetadata
  certificate_ref: string
}

TrackData {
  track_id: A..D
  start_token_id: string
  tokens: [{ token_id: string, opcode: Opcode }]
}
```

Load-time hard validation rejects malformed case data before gameplay:
- duplicate case/token IDs;
- invalid track count/ID/order;
- token count outside ceilings;
- missing start anchor;
- edit that could create track length <2;
- invalid eligible token ID;
- horizon outside authored bounds;
- target outside frozen grammar;
- mastery contract naming absent/duplicate tracks;
- certificate hash/version mismatch.

Release builds must fail closed on malformed content: show a recoverable content-error screen/log entry rather than improvising semantics.

## 5. Rules Core API contract
Conceptual pure functions:

```text
validate_case(case) -> ValidationResult
apply_edit(case, edit_set) -> EditedCase
resolve_initial_cursors(case, edit_set) -> CursorVector
simulate(case, edit_set) -> RunTrace
evaluate_target(case, run_trace.final_state) -> TargetResult
first_monotone_failure(case, run_trace) -> optional FailureEvent
preview_schedule(case, edit_set) -> PreviewSchedule
```

`preview_schedule` may derive only the information allowed by Phase 4/6: surviving loop/token schedule, cycle boundaries, resolved anchors and CLAMP-active-at-start ticks. It must not call target evaluation on future workpiece state for player presentation.

Internally the validator may call the full simulator for every legal edit; UI access to those results is prohibited by layer boundary.

## 6. Tick-state structure
Canonical state during simulation:

```text
SimulationState {
  tick: int
  lane: Lane
  orientation: Orientation
  successful_stamps: int
  blocked_pushes: int
  clamp_active_this_tick: bool
  clamp_scheduled_next_tick: bool
  cursor_by_track: map<TrackId, token_id>
}
```

Every transition uses Phase-4 exact order:
1. promote scheduled clamp;
2. clear next schedule;
3. execute A -> B -> C -> D current surviving tokens;
4. advance cursors;
5. emit immutable trace row;
6. optionally stop only on frozen monotone-hard-fail semantics.

A deterministic trace row records both before/after values and each opcode event. Animation consumes trace rows; animation never drives state.

## 7. Trace schema
Each tick trace should preserve enough data for deterministic playback and debugging:

```text
TickTrace {
  tick
  clamp_active_at_start
  events: [
    {track_id, token_id, opcode, lane_before, lane_after,
     orientation_before, orientation_after,
     stamps_before, stamps_after,
     blocked_before, blocked_after,
     scheduled_clamp_after_event}
  ]
  final_state_after_tick
}
```

The full trace is canonical debug/validator data. Shipping runtime may avoid persisting traces in save files because they are reconstructible from case+edit.

## 8. Exact certificate contract
Certificate generation must use the same Rules Core library/module as runtime simulation, not a duplicated algorithm.

Certificate identity hash input:
- canonical normalized case serialization;
- `case_rules_version`;
- validator/certificate format version;
- optionally a stable Rules Core semantic build identifier.

Certificate verifies:
- legal edit count;
- all candidate edit sets;
- final values;
- success/failure;
- full trace hash;
- first monotone fail;
- equivalence groups;
- uniqueness band;
- difficulty/duplicate fingerprints.

Runtime release gate:
- every campaign case has certificate;
- certificate case hash matches loaded case;
- rules version supported;
- designated UNIQUE cases are still UNIQUE.

Certificates are development/content-integrity artifacts, not secret DRM. Player progression never depends on hiding their existence.

## 9. Canonical serialization and hashing
Use deterministic canonical serialization for case/certificate hashing:
- fixed field order;
- UTF-8;
- normalized enum/string casing;
- stable array ordering where order is meaningful;
- no engine object IDs, timestamps, whitespace-sensitive pretty-print or dictionary iteration order in hash input.

Hash algorithm implementation choice may be SHA-256 or another stable widely supported cryptographic hash; pick one before content certification and version it. Do not rely on Godot's generic object hash for persisted authority.

## 10. Save model
Normal campaign save stores player progress, not simulation truth.

Conceptual schema:

```text
SaveData {
  save_format_version
  game_content_version
  profile_id_local
  completed_case_ids: set<string>
  current_case_id: optional string
  planning_edits_by_case: map<case_id, EditSelection>
  ending_reached: bool
  mastery_complete: bool
  tutorial_seen_flags: set<string>
  nudge_seen_case_ids: set<string>
  settings: SettingsData
  achievement_reconciliation_version
  demo_import_receipt: optional DemoImportReceipt
  last_write_sequence: int
}
```

Do not persist:
- mid-RUN mutable state;
- certificate solution sets;
- precomputed solver recommendations;
- UI animation state;
- Steam achievement cache as campaign authority.

On resume from a case, restore planning selection. RUN restarts deterministically from tick 1.

## 11. Atomic persistence / corruption recovery
Required write flow:
1. serialize to temporary file;
2. flush/close successfully;
3. validate parse + required fields if practical;
4. rotate prior valid primary to backup;
5. atomically replace primary where platform permits.

Maintain at least primary + previous-valid backup.

Load order:
1. primary if valid;
2. backup if primary invalid;
3. fresh profile only if neither is valid.

Never silently overwrite a corrupt primary with empty progress before backup recovery is attempted. If recovery occurs, inform user non-alarmingly and continue.

## 12. Save-version migration
Every save migration is explicit and monotonic.

Rules:
- old -> current through ordered migration functions;
- never mutate unknown future-version save;
- preserve unknown progress only when safe; otherwise refuse with recoverable message rather than truncating;
- canonical completed case IDs survive reordering/act quota changes;
- removed case IDs may stay in historical set but cannot unlock nonexistent content by accident;
- achievement reconciliation runs after migration.

Migration tests must include at minimum N-1 and oldest supported shipped save fixtures once releases exist.

## 13. Demo import contract
Demo is a separate product/app possibility and cannot be assumed to share Steam Cloud namespace automatically.

Define a small versioned `DemoProgressExport` local payload containing only:
- export format/version;
- demo content version;
- completed canonical case IDs;
- settings/accessibility values safe to import;
- tutorial-seen flags;
- integrity checksum/hash sufficient to detect accidental corruption, not anti-cheat security.

Full game import algorithm:
1. discover known local demo-export location(s);
2. parse supported version;
3. intersect completed IDs with full-game canonical IDs;
4. union with existing full save (never replace stronger progress);
5. merge settings only under clear precedence rule: full-game existing user changes win; otherwise import demo values;
6. record import receipt/version/hash;
7. recalculate campaign unlocks from resulting completion set;
8. reconcile achievements idempotently.

Repeated import must produce same state.

## 14. Campaign progression service
Progression must be derived from content manifest + completed case ID set, not separately stored unlock booleans where avoidable.

Functions conceptually:
```text
get_act_completion(act_id, completed_ids)
get_required_quota(act_id, campaign_manifest)
is_act_unlocked(act_id, completed_ids)
is_ending_reached_eligible(completed_ids)
is_all_cases_complete(completed_ids)
is_mastery_complete(completed_ids)
```

Mandatory onboarding IDs and quota data belong to a versioned campaign manifest. Save stores completion; derived unlock state is recomputed, reducing stale-state bugs.

## 15. Achievement reconciliation
Local progression is truth; Steam achievements are a platform mirror.

On suitable checkpoints / startup after platform initialization:
- derive all earned achievements from current canonical progress;
- query platform where available;
- set any missing earned achievements;
- never revoke Steam achievements because a save is older or temporarily unavailable;
- no gameplay progression waits on Steam callback/network.

Demo import follows same reconciliation path. Duplicate calls must be harmless.

## 16. Steam/platform abstraction
Define optional interface conceptually:

```text
PlatformService {
  is_available()
  active_input_glyph_family()
  unlock_achievement(id)
  request_achievement_state()
  cloud_sync_capability()
  notify_local_save_changed_if_needed()
}
```

Core game runs with a NullPlatformService offline/outside Steam.

Do not put Steam APIs in Rules Core, case loading or campaign logic.

## 17. Input architecture
All player actions map to semantic actions, never hard-coded device buttons:
- focus_up/down/left/right;
- track_prev/next;
- confirm;
- cancel;
- preview_toggle;
- help;
- scrub_prev/next;
- pause;
- playback_pause;
- playback_step;
- playback_speed.

UI queries active input family only for glyph presentation. Mouse motion alone should not switch glyph family; require meaningful click/button/axis threshold consistent with Phase 6.

## 18. Localization readiness
All user-facing strings use keys.

Do not serialize localized opcode names as gameplay values. Case target/rendering receives semantic enum then formats localized text.

Layout rules:
- 150% text and long-string stress fixtures;
- no text baked into art where it conveys mechanics;
- achievement names/descriptions localization-ready;
- numbers, arrows and A->D track identity remain mechanically stable across locales.

Working commercial title remains unresolved and must not be embedded as a rules/content identifier.

## 19. Presentation reconstruction contract
Planning view is derived from CaseData + selected EditSelection.
Preview is derived from `preview_schedule` only.
RUN playback is derived from immutable RunTrace.
Result card is derived from `TargetResult` + final trace state.

This separation makes pause/speed/reduced-motion safe: changing playback speed cannot alter outcome.

## 20. Performance assumptions / budgets
The game is logic/UI-light. Performance targets should therefore be strict rather than permissive.

Baseline goals:
- 60 fps presentation target on ordinary desktop/Steam Deck where practical; never below Steam Deck compatibility baseline because of game logic;
- 1280×800 first-class;
- Rules Core simulation for one edit effectively instantaneous to player;
- full <=36-candidate mastery certification should complete in development tooling fast enough for interactive authoring;
- no per-frame solver search during normal gameplay;
- no large texture/particle dependency required for correctness.

A 30 fps minimum compatibility floor is platform guidance, not a design target; Missing Step has no plausible justification for CPU-heavy runtime simulation.

## 21. Logging / diagnostics
Development builds should support deterministic compact logs:
- case ID/hash/rules version;
- selected token IDs;
- per-tick trace;
- target result;
- certificate verification result;
- save migration/recovery event;
- demo-import result.

Release logging should avoid personal data and excessive disk growth. No telemetry is required for game correctness.

## 22. Test layers
### Rules unit tests
Frozen semantic fixtures for:
- deleted start anchor;
- duplicate opcodes;
- PUSH into active CLAMP;
- PUSH lane1->0 under CLAMP;
- multiple PUSHes same tick;
- multiple CLAMPs coalescing;
- consecutive clamps;
- STAMP lane0 no-op;
- A->D same-tick order;
- final-tick CLAMP with no future effect;
- monotone early fail;
- horizon target evaluation.

### Golden trace tests
Persist expected traces for canonical witnesses C01, C03/C04, C07 and C09 or equivalent final selected representatives. Any engine/rules refactor must reproduce them byte/field-equivalently under the current rules version.

### Validator tests
- UNIQUE;
- UNSAT;
- EQUIVALENT_MULTI;
- TRACE_MULTI;
- 36-pair mastery enumeration;
- certificate mismatch rejection.

### Persistence tests
- save/load round trip;
- temp-write interruption simulation;
- corrupt primary + valid backup;
- corrupt both -> recoverable fresh-profile path;
- old-version migration;
- future-version refusal;
- case removed/reordered between content versions.

### Demo-import tests
- no demo file;
- valid import;
- repeated import;
- existing stronger full progress;
- unknown demo case IDs;
- older supported export;
- corrupt export;
- imported settings vs already-changed full settings.

### UI acceptance tests
- controller-only complete path;
- keyboard-only path;
- 1280×800;
- 150% text;
- reduced motion;
- active glyph switching;
- duplicate token positional identity;
- Preview never displays target forecast;
- RUN speed/step does not alter trace.

## 23. Implementation order for dedicated repository
When migrated, implementation should proceed approximately:

### 12A — bootstrap + deterministic core
Project, Rules Core, case parser/validator, minimal tests, persistence skeleton.

### 12B — vertical slice
One certified single-delete case end-to-end: plan -> Preview -> RUN -> result -> save completion.

### 12C — all frozen mechanics
Four opcodes, anchors, all target grammar, mastery edit contract, full trace/result behavior.

### 12D — content pipeline
Validator/certifier, campaign manifest, populate certified launch cases.

### 12E — UX/platform/accessibility
Controller/keyboard/mouse, 800p/150%, settings, Steam adapter, demo import, achievements/cloud.

### 12F — adversarial QA
Persistence corruption, versioning, certificate mismatches, progression quotas, repeated imports, input switching, hostile traces.

### 12G — empirical gates
Playtest difficulty, hint necessity, 36 vs 42 quality decision, playback pacing, demo length/conversion positioning, price recheck.

### 12H — release candidate
Packaging, performance, Deck/controller regression, demo/full compatibility and final content/certificate integrity audit.

## 24. Explicit non-goals
- production implementation in this factory;
- generic ECS architecture for four-opcode puzzle state;
- networking/server authority;
- anti-cheat infrastructure;
- procedural daily puzzle backend;
- runtime solver recommendations;
- level editor at launch;
- save slots/cloud account system beyond local+Steam baseline;
- analytics dependency;
- engine physics as gameplay truth.

## 25. Phase-8 closure still required
Core architecture is frozen, but Phase 8 should not yet be marked complete until the next run performs hostile concrete walkthroughs using actual representative serialized case/save payloads:
1. one exact canonical case JSON-like example + expected post-edit trace;
2. one mastery case + 36-or-less enumeration/certificate example;
3. save corruption/recovery walkthrough;
4. N-1 save migration example;
5. demo import into existing partial full-game progress;
6. certificate mismatch after content/rules version change;
7. verify no Preview/UI layer can accidentally obtain solver result through the proposed interfaces.

If these pass without architectural repair, mark Phase 8 complete and proceed to Phase 9 whole-game simulation.