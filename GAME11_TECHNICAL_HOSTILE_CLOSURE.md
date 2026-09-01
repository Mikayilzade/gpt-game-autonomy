# GAME #011 — MISSING STEP — PHASE 8 HOSTILE CLOSURE

Date: 2026-09-01
Status: **PHASE 8 HOSTILE CLOSURE COMPLETE**
Authority: `START_HERE.md` -> `STATUS.md` -> `GAME_INDEX.md` -> active Game #011 design files -> `GAME11_TECHNICAL_SPECIFICATION.md` -> this closure file for resolved hostile interface/persistence examples.

This file adds concrete payload/behavior proofs to the Phase-8 architecture. It does not change the frozen puzzle rules or start production implementation.

---

## 1. Exact canonical single-delete payload + cursor + trace

Representative canonical payload, equivalent to content witness C01:

```json
{
  "case_id": "g11_c01_first_closure",
  "case_data_version": 1,
  "case_rules_version": 1,
  "act_id": "ACT_I",
  "ordinal": 1,
  "title_key": "case.g11_c01.title",
  "teaching_tags": ["loop_closure", "recurrence"],
  "challenge_family_tags": ["F1"],
  "tracks": [
    {
      "track_id": "A",
      "start_token_id": "A1",
      "tokens": [
        {"token_id": "A1", "opcode": "PUSH"},
        {"token_id": "A2", "opcode": "TURN"},
        {"token_id": "A3", "opcode": "STAMP"}
      ]
    }
  ],
  "initial": {"lane": 0, "orientation": "N", "clamp_active": false},
  "horizon_ticks": 4,
  "edit_contract": {
    "type": "SINGLE",
    "editable_tracks": ["A"],
    "eligible_token_ids_by_track": {"A": ["A1", "A2", "A3"]}
  },
  "target": [
    {"kind": "FINAL_LANE", "eq": 0},
    {"kind": "FINAL_ORIENTATION", "eq": "N"},
    {"kind": "STAMP_COUNT", "eq": 1},
    {"kind": "BLOCKED_PUSH_COUNT", "eq": 0}
  ],
  "certificate_ref": "cert:g11_c01:v1"
}
```

Selected edit: delete `A2`.

Post-edit A is `[A1 PUSH, A3 STAMP]`. `start_token_id=A1` survives, therefore initial cursor resolves to `A1`; no numeric-index reinterpretation occurs.

Expected exact trace:

| tick | clamp at start | executed | lane after | orientation | stamps | blocked |
|---:|---|---|---:|---|---:|---:|
| 1 | false | A1 PUSH | 1 | N | 0 | 0 |
| 2 | false | A3 STAMP | 1 | N | 1 | 0 |
| 3 | false | A1 PUSH | 0 | N | 1 | 0 |
| 4 | false | A3 STAMP (lane-0 no-op) | 0 | N | 1 | 0 |

Final target = PASS.

Exhaustive candidates:
- delete A1 -> `(lane0,N,stamps0,blocked0)` FAIL;
- delete A2 -> `(lane0,N,stamps1,blocked0)` PASS;
- delete A3 -> `(lane0,N,stamps0,blocked0)` FAIL.

Certificate band = `UNIQUE`. A1/A3 happen to share the same final tuple, but neither succeeds; this does not compromise solution uniqueness. Full-trace hashes still distinguish them if their event traces differ.

### Deleted-start-anchor fixture
A separate mandatory unit fixture deletes the authored start token. Example A `[A1 PUSH,A2 TURN,A3 STAMP]`, start `A1`, delete `A1`: cursor resolves clockwise to `A2`, not to post-edit array index inherited accidentally from serialization. This remains a rules test even though C01's successful edit does not delete its anchor.

---

## 2. Exact two-track mastery payload + exhaustive certificate structure

Canonical mastery witness C09 / Round-C M-C4:

```json
{
  "case_id": "g11_c09_two_absences_i",
  "case_data_version": 1,
  "case_rules_version": 1,
  "tracks": [
    {"track_id":"A","start_token_id":"A1","tokens":[
      {"token_id":"A1","opcode":"PUSH"},
      {"token_id":"A2","opcode":"PUSH"},
      {"token_id":"A3","opcode":"TURN"},
      {"token_id":"A4","opcode":"STAMP"}
    ]},
    {"track_id":"B","start_token_id":"B1","tokens":[
      {"token_id":"B1","opcode":"PUSH"},
      {"token_id":"B2","opcode":"CLAMP"},
      {"token_id":"B3","opcode":"PUSH"},
      {"token_id":"B4","opcode":"TURN"}
    ]}
  ],
  "initial":{"lane":0,"orientation":"N","clamp_active":false},
  "horizon_ticks":12,
  "edit_contract":{
    "type":"TWO_NAMED_TRACKS",
    "editable_tracks":["A","B"],
    "eligible_token_ids_by_track":{"A":["A1","A2","A3","A4"],"B":["B1","B2","B3","B4"]}
  },
  "target":[
    {"kind":"FINAL_LANE","eq":0},
    {"kind":"FINAL_ORIENTATION","eq":"N"},
    {"kind":"STAMP_COUNT","eq":4},
    {"kind":"BLOCKED_PUSH_COUNT","eq":0}
  ]
}
```

Legal candidate count = 4×4 = 16, below the frozen 36-pair ceiling.

Exhaustive final tuples `(lane,orientation,stamps,blocked)`:

| A delete | B1 | B2 | B3 | B4 |
|---|---|---|---|---|
| A1 | `0,N,0,0` | `0,N,2,0` | `0,N,0,0` | `0,N,0,4` |
| A2 | `0,N,0,0` | `0,N,2,0` | `0,N,0,0` | `0,N,0,4` |
| A3 | `0,N,0,4` | `0,N,0,0` | `0,N,2,0` | **`0,N,4,0`** |
| A4 | `0,N,0,4` | `0,N,0,0` | `0,N,0,0` | `0,N,0,0` |

Unique success = `{A3 TURN, B4 TURN}`.

Post-edit loops:
- A `[PUSH,PUSH,STAMP]`;
- B `[PUSH,CLAMP,PUSH]`.

Successful trace repeats a 3-tick cadence four times:
- ticks 1/4/7/10: A PUSH to lane1, then B PUSH to lane0;
- ticks 2/5/8/11: A PUSH to lane1, B CLAMP schedules next tick;
- ticks 3/6/9/12: clamp active; A STAMP succeeds at lane1; B PUSH exits lane1->0 and is therefore never blocked.

Final = lane0 / N / stamps4 / blocked0.

Certificate structure must store all 16 candidate edit IDs and trace hashes, not merely the winner. Case summary:

```text
legal_edit_set_count = 16
raw_successful_edit_set_count = 1
behaviorally_distinct_successful_trace_count = 1
solution_edit_sets = [["A3","B4"]]
uniqueness_band = UNIQUE
equivalence_groups = computed across full traces, including failures
```

This proves the mastery certifier does not require heuristic search; exhaustive enumeration is the authority.

---

## 3. Corrupt-primary + valid-backup recovery

Hostile disk state:
- `save.json` exists but is truncated / fails parse or required-field validation;
- `save.prev.json` exists, parses, has supported version and sequence 184;
- no in-memory profile has yet been created.

Required load transaction:
1. read primary bytes without modifying either file;
2. parse + validate primary -> INVALID;
3. read backup bytes;
4. parse + validate + migrate backup -> VALID;
5. instantiate in-memory profile from backup;
6. expose non-alarming `Recovered previous save` notice;
7. only after a later genuine save checkpoint, use the ordinary atomic writer to create a new validated primary; keep a valid recovery generation throughout rotation.

**Forbidden:** `load primary -> fail -> construct defaults -> autosave defaults -> only then inspect backup`. That destroys the recovery path.

Recovery proof: there is no write operation anywhere in steps 1–6. Empty/default state can be created only after both primary and backup are independently rejected.

Additional implementation rule: after backup recovery, the corrupt primary is not promoted into the previous-valid slot. The next atomic write must preserve the recovered valid generation until the new primary validates.

---

## 4. Explicit N-1 -> current migration + future refusal

Current save format for this design package: conceptual v3.

Example v2 payload used a single `text_scale` scalar and lacked per-setting provenance:

```json
{
  "save_format_version":2,
  "completed_case_ids":["g11_c01_first_closure","g11_c02_longer_echo"],
  "current_case_id":"g11_c03_which_stamp",
  "settings":{"text_scale":1.5,"reduced_motion":true},
  "last_write_sequence":40
}
```

Migration v2 -> v3:
- preserve completed IDs/current case/planning selections verbatim when IDs remain canonical;
- map `text_scale` -> `settings.ui_scale`;
- preserve `reduced_motion`;
- add `settings_user_modified_keys`. Because v2 cannot prove which settings were manually changed, migrated non-default values are conservatively marked user-modified; exact default-valued fields may remain unmarked;
- initialize missing `demo_import_receipt = null`;
- set `achievement_reconciliation_version` to 0 so reconciliation reruns;
- do **not** infer/store act unlock booleans, ending or mastery from old cached flags; derive them from canonical completed IDs + current campaign manifest after migration;
- write the migrated save only through the normal atomic path after successful validation.

### Future-version refusal
If runtime supports through v3 and reads `save_format_version:4`:
1. do not run a downgrade migration;
2. do not parse unknown fields into a v3 object and rewrite it;
3. preserve both files unchanged;
4. show recoverable `This save was created by a newer version of the game` state with Retry/Back/Quit as appropriate;
5. campaign must not auto-create an empty profile at the same path.

This protects progress after accidental game downgrade / branch mismatch.

---

## 5. Demo import into partially progressed full save

Full save before import:

```text
completed = {C01,C02,C03,C05,C09}
settings.ui_scale = 1.25   [user-modified]
settings.reduced_motion = false [untouched default]
tutorial_seen = {loop_closure, recurrence}
demo_import_receipt = null
```

Supported demo export:

```text
completed = {C01,C02,C03,C04,C06,C07,UNKNOWN_OLD_DEMO_ID}
settings.ui_scale = 1.50
settings.reduced_motion = true
tutorial_seen = {loop_closure, recurrence, clamp_next_tick, duplicate_position}
export_hash = H1
```

Import result:
- intersect demo IDs with current canonical manifest -> `{C01,C02,C03,C04,C06,C07}`;
- completion union -> `{C01,C02,C03,C04,C05,C06,C07,C09}`;
- `UNKNOWN_OLD_DEMO_ID` ignored, logged diagnostically, never becomes an unlock key;
- `ui_scale` remains 1.25 because full-game user modified it;
- `reduced_motion` becomes true because the full-game value was untouched default and demo accessibility preference may safely carry over;
- tutorial flags union -> `{loop_closure, recurrence, clamp_next_tick, duplicate_position}`;
- derive quotas/unlocks from the union completion set;
- achievement reconciliation runs from canonical full-game progress;
- receipt records supported import version + H1 + import schema version.

Repeated import of identical H1 produces exactly the same semantic state. It may no-op early from the receipt but correctness must also hold if the merge runs again.

### Contradiction found and repaired: settings precedence needed provenance
The earlier abstract rule said “full-game existing user changes win; otherwise import demo values,” but the prior save schema had no reliable way to distinguish an untouched default from a user-selected value equal to a default.

**Repair:** persistence schema adds `settings_user_modified_keys: set<SettingKey>` (or behaviorally equivalent per-setting provenance). Settings UI marks a key when the user deliberately changes it. Demo import consults this set. Migration from older saves uses conservative rules described above. This is implementation architecture, not a gameplay mechanic.

---

## 6. Certificate mismatch hostile cases

### A. Content changed, rules unchanged
Suppose certificate was generated for C01 hash `HC1`, then an author changes horizon 4 -> 5 or edits a token while leaving `certificate_ref` unchanged. Normalized case hash becomes `HC2 != HC1`.

Load/release gate result:
- certificate rejected before case enters playable manifest;
- no attempt to “trust close enough” certificate metadata;
- development build identifies content-hash mismatch;
- release content verification fails closed; malformed/mismatched case is not silently playable;
- author recertifies the exact new payload.

### B. Rules version changed, content bytes otherwise same
Suppose case declares `case_rules_version=1`, certificate generated under rules v1, but runtime changes PUSH/CLAMP semantics and current content now declares rules v2.

Required result:
- v1 certificate cannot certify v2 semantics even if serialized track data is byte-identical;
- certificate identity includes rules version and stable Rules Core semantic identifier/version;
- all cases admitted under v2 require v2 recertification using the same v2 Rules Core used by runtime;
- golden traces explicitly surface unintended semantic drift.

No “certificate migration” is allowed across a semantic rules change; recertification is required.

---

## 7. Preview cannot become an oracle through normal UI API

A prose rule is insufficient; enforce the boundary structurally.

### Player-facing Rules facade
Planning UI receives only:

```text
PlanningRulesFacade {
  validate_edit_selection(case_id, edit_ids) -> EditSelectionValidity
  preview_schedule(case_id, edit_ids) -> PreviewScheduleDTO
  begin_run(case_id, edit_ids) -> RunPlaybackDTO
}
```

`PreviewScheduleDTO` contains only:
- surviving token IDs/opcodes by track;
- resolved first token/anchor;
- per-tick opcode alignment;
- cycle-boundary markers;
- clamp-active-at-start schedule derivable from CLAMP tokens.

It has **no** fields for future lane/orientation/stamps/blocked counts, target result, solution count, candidate rank or alternate edit sets.

### Separation
- `ValidatorCertifier` is a development/content service and is not referenced by normal planning UI.
- full `simulate()` is not directly exposed to planning widgets;
- `begin_run` is the explicit experiment boundary: after the player commits RUN, the application may simulate once and return immutable playback trace/result data;
- presentation may cache the current RUN trace for replay, never alternate candidate traces from certification.

### Required tests
1. serialize Preview DTO for every canonical case; assert forbidden field names/types cannot appear;
2. UI planning integration test runs with a facade mock that has no solver/certifier methods;
3. search/dependency test ensures presentation package does not import validator namespace/module;
4. before RUN, target card receives current target specification only, not `TargetResult`;
5. changing selected deletion can call `preview_schedule`, never enumerate alternatives.

This is stronger than “do not show oracle data”: normal UI does not possess it.

---

## 8. Second contradiction found and repaired: derived progression vs persisted booleans

Earlier SaveData sketch included `ending_reached` and `mastery_complete` while Campaign Service correctly defined progression as derived from canonical completed IDs + campaign manifest. Persisted authoritative booleans can become stale after content migration/quota changes.

**Repair:** authoritative save state does not require persistent `ending_reached`, `mastery_complete`, act-unlocked flags or all-cases-complete flags. Derive these on load/checkpoint from `completed_case_ids` and the current versioned manifest. If UI caches such booleans in memory, they are disposable derived values. If historical analytics/one-time presentation needs “ending has been shown,” store a distinct presentation flag such as `ending_sequence_seen`, never confuse it with eligibility/completion truth.

---

## 9. Phase-8 closure verdict

Hostile gates:
- exact single-delete payload/cursor/trace: PASS;
- exact <=36 mastery enumeration/certificate shape: PASS (16 candidates, unique success);
- corrupt-primary + valid-backup recovery without default overwrite: PASS;
- explicit N-1 migration: PASS;
- future-version refusal without destructive downgrade: PASS;
- partial full-save demo merge: PASS after adding per-setting provenance;
- repeated demo import idempotency: PASS;
- content-change certificate mismatch: PASS;
- rules-change certificate mismatch: PASS;
- Preview non-oracle architectural boundary: PASS;
- stale progression-cache contradiction: REPAIRED by deriving completion/unlocks.

**PHASE 8 COMPLETE.**

No gameplay mechanic, fifth opcode, second workpiece, hidden rule or production implementation was added.

## Handoff
Proceed directly to Phase 9 whole-game simulation. Walk first boot through ending/completion/mastery and hostile lifecycle paths using the now-concrete persistence/demo/platform contracts. Repair any cross-phase contradictions before Phase 10.