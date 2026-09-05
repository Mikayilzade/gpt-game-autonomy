# GAME #017 — THE QUEUE KNOWS — PHASE 8 TECHNICAL IMPLEMENTATION SPECIFICATION

Date: 2026-09-05
Status: PHASE 8 COMPLETE
Production implementation: NO
Authority: active Game #017 authority through `GAME17_COMMERCIAL.md`.

This file is an implementation-ready technical contract. It specifies architecture, data, persistence, testing and implementation order without starting production code.

---

# 1. Engine / runtime recommendation

## Primary recommendation
Use **Godot 4.7.x stable, GDScript baseline** for the dedicated implementation repository.

Why:
- the game is dominated by deterministic state transitions, UI, fixed-slot movement and light 2D/2.5D presentation rather than high-end rendering;
- Godot 4.7.2 stable was current on 2026-08-18 and supports Windows/Linux export, matching PC/Steam and Steam Deck goals;
- GDScript keeps iteration and test harness work lightweight for a small systemic puzzle;
- the architecture below deliberately isolates simulation from scene-tree timing, so engine-specific update order cannot affect outcomes.

Do **not** depend on:
- physics for gameplay truth;
- frame delta for simulation;
- unordered node traversal;
- animation callbacks to advance logic;
- floating-point comparisons for heuristic decisions.

## Acceptable alternative
C# in Godot is acceptable if implementation maintainers prefer stronger static typing. If used, keep the same pure simulation contracts and serialized schemas.

## Not recommended by default
Unity/Unreal are not forbidden, but their heavier project/runtime footprint adds little value for this scope. Changing engine is allowed only if the dedicated implementation session preserves every deterministic/persistence/test contract below.

---

# 2. Architectural layers

The implementation must separate these layers:

1. **ContentData**
   - immutable case definitions;
   - localization keys;
   - authored hidden world;
   - validator metadata.

2. **SimulationCore**
   - pure deterministic state transitions;
   - evaluator/comparator logic;
   - intervention application;
   - cohort resolve;
   - service ticks;
   - inference;
   - objective/constraint evaluation.

3. **SolverValidator**
   - exhaustive world/action search;
   - offline certification;
   - proof artifacts;
   - no rendering dependencies.

4. **RuntimeSession**
   - owns current attempt;
   - save/checkpoint integration;
   - action dispatch;
   - produces presentation events.

5. **Presentation**
   - hall scene, UI, animation, audio, camera;
   - consumes immutable logical events;
   - never mutates authoritative logic directly.

6. **PlatformServices**
   - Steam achievements;
   - Cloud;
   - demo/full-game import;
   - controller glyphs;
   - platform-specific paths.

SimulationCore must be runnable in headless tests without loading gameplay scenes.

---

# 3. Authoritative state boundaries

Only SimulationCore owns gameplay truth.

Authoritative state:
- current case id/version;
- logical tick;
- phase;
- cohort index;
- intervention budget;
- counter logical states;
- customer logical states;
- current candidate sets;
- candidate-world representation;
- immutable evidence records;
- objective/constraint state;
- logical history;
- checkpoint snapshots;
- terminal result.

Non-authoritative:
- customer world positions;
- tween progress;
- camera;
- hover/focus;
- animation queues;
- audio state;
- screen transitions;
- particle effects;
- temporary UI prediction overlays.

Rule: deleting and rebuilding the entire presentation layer from serialized authoritative state must not change the next legal simulation result.

---

# 4. Canonical serialized CaseDefinition

Recommended versioned JSON-like schema:

```
{
  "schema_version": 1,
  "case_id": "QK01",
  "content_version": 1,
  "chapter": 1,
  "mastery": false,
  "demo_included": true,
  "display_name_key": "case.qk01.name",
  "brief_key": "case.qk01.brief",
  "tutorial_flags": [],
  "initial_tick": 0,

  "counters": [
    {
      "id": "A",
      "stable_order": 0,
      "open": true,
      "opens_at_tick": null,
      "fee": 1,
      "service_category": "GENERAL",
      "privacy_level": 0,
      "walk_cost": 0,
      "service_time": 1,
      "capacity": 1,
      "familiarity_tag": "A",
      "initial_queue": [],
      "initial_in_service": []
    }
  ],

  "customers": [
    {
      "id": "C1",
      "arrival_cohort": "K1",
      "arrival_order": 0,
      "candidate_types": ["PRICE","ROUTINE"],
      "authored_actual_type": "PRICE",
      "required_category": "GENERAL",
      "familiar_counter_id": null,
      "routine_threshold": null,
      "privacy_sensitive_category": null,
      "required_privacy_level": null
    }
  ],

  "cohorts": [
    {
      "id": "K1",
      "customer_ids": ["C1"],
      "admit_tick": 0,
      "post_cohort_service_ticks": 0
    }
  ],

  "intervention_windows": [
    {
      "before_cohort": "K1",
      "allowed_actions": ["SET_FEE_B_0"],
      "reset_each_cohort": false
    }
  ],

  "interventions": [
    {
      "id": "SET_FEE_B_0",
      "family": "FEE",
      "target_counter": "B",
      "field": "fee",
      "value": 0,
      "cost": 0
    }
  ],

  "starting_intervention_budget": 1,
  "public_world_constraints": [],
  "objective": {},
  "hard_constraints": [],
  "world_quantifier": "ALL_REMAINING",
  "checkpoint_policy": "INTERVENE_BOUNDARIES",
  "hint_route_ids": [],
  "validation_expectations": {}
}
```

Requirements:
- integer semantics only for fee/service/walk/privacy/threshold/tick;
- enum values normalized;
- stable counter/customer IDs immutable within a content version;
- unknown fields rejected in development/certification builds;
- release may ignore unknown forward-compatible presentation-only metadata but never unknown simulation fields.

---

# 5. Runtime CaseState schema

```
{
  "runtime_schema_version": 1,
  "case_id": "QK01",
  "content_version": 1,
  "attempt_id": "uuid-or-monotonic-id",
  "tick": 0,
  "phase": "INTERVENE",
  "cohort_index": 0,
  "interventions_remaining": 1,
  "checkpoint_id": "CP0",
  "counters": {...},
  "customers": {...},
  "candidate_world_ids": [...],
  "evidence_ids": [...],
  "history_event_ids": [...],
  "terminal_result": null
}
```

Do not serialize derived UI caches as truth.

Derived values that should be recomputed:
- predicted completion;
- comparator tuples;
- candidate chip display order;
- Type Lens rows;
- evidence prose;
- objective progress labels.

---

# 6. Hidden-world representation and no-leak boundary

## Runtime
The authored actual world exists only inside SimulationCore / RuntimeSession private state.

Presentation receives:
- public case data;
- candidate sets;
- public world constraints;
- observation records;
- proven singleton types;
- post-terminal reveal payload when allowed.

Presentation must never receive the full hidden assignment before reveal.

## API rule
No UI function may accept a raw `actual_type` parameter.

Allowed query:
`get_public_customer_view(customer_id)`

Forbidden query:
`get_customer_actual_type(customer_id)` before terminal/proven-singleton reveal.

## Debug builds
Developer overlays that reveal hidden truth must:
- require explicit debug flag;
- render a persistent `DEBUG TRUTH` watermark;
- be impossible in production export;
- never be used by screenshot/golden UI tests intended to validate player-facing behavior.

---

# 7. Evaluator / comparator API

Use one evaluator per type, all pure functions.

```
evaluate_choice(
  type: HeuristicType,
  customer_public: CustomerPublicState,
  hall_snapshot: PublicHallSnapshot
) -> ChoiceEvaluation
```

`ChoiceEvaluation`:
- chosen_counter_id or NO_FEASIBLE_COUNTER;
- ordered comparator facts;
- public reason atoms;
- predicted-completion facts actually used.

Type-specific comparator order is exactly Phase 4.

Suggested lower-level pure API:

```
get_feasible_counters(customer, hall) -> CounterId[]
predicted_completion(customer, counter, hall) -> int
evaluate_price(...)
evaluate_urgent(...)
evaluate_routine(...)
evaluate_privacy(...)
evaluate_convenience(...)
```

All comparator sorting must use explicit ordered tuple logic, never dictionary/hash iteration order.

---

# 8. Canonical event ordering

Runtime action `RESOLVE_COHORT` produces an ordered logical event batch.

Order:
1. INTERVENTION_LOCKED
2. scheduled lever transitions at current tick
3. for each customer in authored arrival order:
   - PRE_CHOICE_SNAPSHOT
   - CUSTOMER_CHOICE
   - QUEUE_APPEND
   - EVIDENCE_CREATED
4. INFERENCE_BATCH_APPLIED
5. for each post-cohort service tick:
   - TICK_INCREMENTED
   - SERVICE_PROGRESS_BATCH
   - SERVICE_COMPLETIONS ordered by counter stable_order then slot
   - SERVICE_PROMOTIONS
   - SCHEDULED_COUNTER_TRANSITIONS
   - CONTINUOUS_CONSTRAINT_CHECK
6. BOUNDARY_CONSTRAINT_CHECK
7. BOUNDARY_OBJECTIVE_CHECK
8. OBSERVE_READY or TERMINAL

Presentation may animate events slowly, quickly or instantly, but may not reorder them logically.

---

# 9. Evidence schema

Each immutable evidence record:

```
{
  "evidence_id": "E00012",
  "case_id": "QK03",
  "tick": 0,
  "customer_id": "C5",
  "pre_choice_public_state_hash": "sha256-or-equivalent",
  "available_counter_ids": ["A","B"],
  "chosen_counter_id": "A",
  "public_snapshot": {
    "counter_facts": {...},
    "queue_facts": {...},
    "customer_public_facts": {...}
  },
  "eliminations": [
    {
      "type": "ROUTINE",
      "reason_code": "ROUTINE_WOULD_CHOOSE_OTHER",
      "reason_args": {...}
    }
  ]
}
```

Store structured reason codes + args, not final localized prose.

Evidence snapshot must be immutable after creation.

---

# 10. Type Lens contract

Type Lens is a public counterfactual comparison tool, not an oracle.

API:

```
query_type_lens(
  customer_id,
  hypothetical_public_state,
  candidate_type
) -> PublicCounterfactualResult
```

Allowed output:
- feasible counters;
- public comparator facts;
- which counter that candidate type would choose in the hypothetical public state;
- explanation atoms.

Forbidden output:
- probability;
- hint that a candidate is the actual hidden type;
- aggregate “best test” score;
- information gain;
- solver recommendation;
- actual-world branch preview.

Type Lens may evaluate one candidate model at a time or explicitly selected visible candidate models. It must not silently run hidden-world policy search for the player.

---

# 11. Solver / validator architecture

The validator is primarily an **offline authoring tool**.

Inputs:
- CaseDefinition;
- all allowed hidden worlds;
- legal action domains;
- objective and hard constraints.

Search node:
`(public logical state, surviving hidden-world set, remaining budget, cohort position)`

World identity need not be part of player-visible state; solver internally branches by observation partition.

At an intervention decision:
1. enumerate legal action sets;
2. simulate action for every surviving world;
3. partition worlds by identical public observation result;
4. recursively search each observation partition;
5. a policy succeeds only if all required branches eventually satisfy objective under the case quantifier.

Outputs:
- `CONTENT_CERTIFIED` boolean;
- world count;
- reachable public-state count;
- shortest successful policy depth;
- representative policy tree;
- successful policy class count if tractable;
- dead-state certificates;
- indistinguishable world pairs;
- candidate-separation matrix;
- hard-constraint failure fronts;
- dominant zero-information route warning;
- content repetition metrics.

## Proof artifacts
Every certified content file should produce machine-generated artifact:
`validation/QKxx.cert.json`

It contains:
- case content hash;
- validator version;
- certification timestamp;
- metrics above;
- representative policy hashes;
- invariant/property-test summary.

Release build should refuse uncertified campaign/mastery case data in CI packaging.

---

# 12. Runtime dead-state handling

Normal gameplay should not invoke the full expensive offline search after every animation frame.

Allowed runtime approaches:
1. precomputed dead-state certificates keyed by canonical public-state hash for certified content; or
2. bounded exact solver invocation only at explicit dead-state query/checkpoint moments if performance is proven.

No heuristic “probably impossible” result.

If runtime cannot prove dead state cheaply, it simply does not announce dead state; restart/checkpoint remains available.

---

# 13. Save model

Use one account-local save document plus per-case checkpoint payloads.

```
SaveRoot
  save_schema_version
  product_id
  build_compat_version
  profile_id
  last_write_utc
  campaign_progress
  mastery_progress
  achievements_shadow_state
  settings
  current_session_ref?
  case_attempt_summaries
  demo_import_marker?
```

CurrentSession:
- case id/content version;
- authoritative CaseState;
- selected fixed hidden world identifier;
- evidence;
- checkpoint snapshots;
- no animation state required.

## Atomic writes
Write to temp file, flush, validate parse/hash, then replace primary save.
Keep one local previous-good backup.

Never overwrite a readable primary save with a failed migration result.

---

# 14. Save migrations

Every save has integer schema_version.

Migration pipeline:
`v1 -> v2 -> v3`, never direct ad-hoc field guessing.

Rules:
- migration functions are deterministic and tested with fixtures;
- unsupported future-version save opens read-only recovery/error flow rather than destructive overwrite;
- content version mismatch must map stable IDs or restart current case while preserving completed-case progress;
- player progression should survive case-data corrections whenever logically possible.

---

# 15. Checkpoint contract

Checkpoint is a full authoritative-state snapshot taken only at Phase-4 legal checkpoint boundaries.

Checkpoint stores:
- same hidden world;
- accepted evidence up to boundary;
- candidate sets/worlds;
- queues/service state;
- intervention budget;
- tick/cohort;
- objective state.

Reload checkpoint replaces whole branch state.

No merge of knowledge from discarded future branch.

UI notes may be either:
- branch-local and rewind with checkpoint; or
- purely player-authored external notes that are explicitly non-canonical.

Default: automatic logical notes/candidate marks rewind; freeform scratch notes may persist if UX implements them, but they cannot alter game logic.

---

# 16. Steam Cloud conflict policy

Preferred: one compact primary save + backup, not hundreds of per-case mutable files.

Each local save records:
- monotonic local revision;
- last_write_utc;
- completed-case set;
- current session id;
- integrity hash.

Conflict handling:
- if platform supplies a clear newer file and local has not diverged, accept newer;
- if both progressed independently, show explicit conflict UI with timestamp, campaign completion count, mastery completion count, current case;
- never silently merge current attempt state;
- optional safe merge of **completed-case union** is allowed only if both saves share compatible schema/content and no progression flags are destructive;
- settings prefer local-device settings except account-level accessibility options explicitly chosen to sync.

If uncertain, preserve both copies and ask the player which to use.

Steam Cloud is portability, not authoritative remote truth.

---

# 17. Demo -> full game save import

Because Steam demo and full game use separate app identities, implement carryover as a deliberate import, not shared-path assumption.

Demo export payload:
```
DemoCarryover
  carryover_schema_version
  source_product = "demo"
  completed_demo_cases
  chapter1_complete
  tutorial_seen_flags
  accessibility/settings subset
  checksum
```

Full game on first boot:
1. detect demo carryover in known import location/platform service path;
2. validate schema/checksum;
3. show `Import demo progress?`;
4. if accepted, mark QK01–QK06 completed as appropriate;
5. offer Continue Chapter 2 or Replay Chapter 1;
6. never import current in-progress case branch if content versions differ.

Demo carryover is optional. Failure must never block full game.

---

# 18. Input abstraction

Define semantic actions, not physical keys:
- NAV_UP/DOWN/LEFT/RIGHT
- FOCUS_NEXT_GROUP / PREV_GROUP
- CONFIRM
- BACK
- OPEN_CUSTOMER
- OPEN_COUNTER
- OPEN_OBJECTIVE
- OPEN_EVIDENCE
- OPEN_TYPE_LENS
- CYCLE_CANDIDATE_PREV/NEXT
- INTERVENTION_VALUE_PREV/NEXT
- RESOLVE
- REPLAY_OBSERVATION
- FAST_FORWARD
- PAUSE

Mouse maps to same command layer.

No gameplay code may branch on “gamepad button X” directly.

Dynamic glyphs are presentation mapping only.

Controller navigation graph must be explicit and testable; no dependence on scene-tree insertion order.

---

# 19. Steam Deck / 1280x800 contract

Technical acceptance:
- complete campaign/controller operation at 1280x800;
- no mandatory hover;
- no pointer precision interaction;
- all critical text passes chosen minimum readable scale from Phase 6;
- 10-customer stress case remains navigable by focus groups;
- modal/detail panels never require simultaneous visibility of more than the Phase-6 information hierarchy permits;
- reduced-motion mode bypasses long tweens while preserving event order.

Add automated viewport smoke tests for:
- 1280x800;
- 1920x1080;
- 2560x1440 UI scale classes.

---

# 20. Localization data boundaries

All player-facing text uses localization keys.

Never concatenate grammar-heavy explanation strings manually.

Reason traces use:
- reason_code;
- named args;
- localized template.

Example:
`reason.routine.threshold_stay` with args counter=A, disadvantage=2, threshold=2.

Numbers and counter IDs can be inserted with locale-aware formatting where needed.

Layout rules:
- support text expansion;
- no fixed-width label that can truncate critical objective/evidence text without scroll/wrap;
- type/counter meaning never color-only.

---

# 21. Accessibility implementation boundaries

Accessibility settings live outside simulation state.

Required technical hooks:
- text/UI scale;
- reduced motion;
- animation speed/instant resolve;
- color-independent icons/patterns;
- high-contrast focus;
- full remapping;
- hold/toggle alternatives;
- audio independence for all logical information;
- subtitle/caption path for optional flavor audio;
- screen-shake intensity including off.

Changing accessibility settings must not:
- change logical tick;
- alter heuristics;
- disable achievements;
- modify validator certification.

---

# 22. Performance budgets

The runtime simulation is tiny relative to rendering.

Target interactive budget:
- resolving 10-customer / 3-counter cohort logic: under 5 ms on a typical desktop debug build where practical;
- Type Lens single candidate query: effectively instant, target <1 ms average;
- loading a case/save: no noticeable multi-second stall from simulation.

Do not optimize prematurely around these exact numbers; the key contract is that runtime never performs exhaustive whole-case validation in the frame loop.

Offline validator may take seconds/minutes for late/mastery cases, but CI should cache by content hash.

If a case exceeds validation practicality, simplify world/action space before adding opaque optimization that weakens proof guarantees.

---

# 23. Determinism contract

Given:
- same CaseDefinition content hash;
- same initial hidden world id;
- same ordered player action list;

the implementation must produce:
- identical logical event sequence;
- identical evidence;
- identical candidate sets;
- identical terminal result;
- identical canonical state hashes.

Across supported platforms, simulation cannot depend on:
- wall clock;
- frame count;
- locale;
- animation speed;
- hash-map iteration;
- floating-point rounding;
- OS path;
- controller type.

Use explicit integer/state ordering.

---

# 24. Test strategy

## Unit tests
- predicted completion capacity1/capacity2;
- each heuristic comparator;
- global tie breaks;
- Routine equality threshold;
- Privacy exposure precedence;
- feasibility;
- intervention budget;
- service tick order;
- candidate elimination;
- objective predicates;
- wait vs completion constraints.

## Golden traces
For QK01–QK06 maintain canonical action -> event-log fixtures.

A golden trace stores:
- initial content hash;
- actions;
- expected state hashes after each action;
- expected evidence elimination sets;
- expected terminal status.

## Property tests
Examples:
- actual type is never eliminated by evidence generated from same evaluator;
- candidate sets only shrink;
- restart reproduces initial state;
- checkpoint reload reproduces exact prior authoritative hash;
- animation/fast-forward settings do not affect logical trace;
- sorting/counter insertion order does not alter stable-order outcome;
- serialization roundtrip preserves authoritative state;
- all certified success states satisfy every hard invariant.

## Fuzz tests
Generate bounded legal synthetic states within mechanical ceilings and check invariants/evaluator totality. Fuzz data is not shipped content.

---

# 25. State hashing

Canonical state hash should serialize fields in explicit stable order.

Use hash for:
- golden traces;
- checkpoint integrity;
- validation cache keys;
- bug reports/replays.

Exclude:
- localized strings;
- timestamps;
- UI focus;
- animations;
- platform metadata.

Evidence pre-choice hash uses public-state-only canonical serialization, not hidden truth.

---

# 26. Replay / bug reproduction

A lightweight logical replay file may contain:
- case id/content hash;
- hidden world id for developer reproduction only;
- ordered player actions;
- resulting state hashes.

Player-facing exported bug report must not expose hidden type unless case is terminal or user explicitly opts into diagnostic bundle.

This enables deterministic reproduction without video capture.

---

# 27. CI gates for dedicated repository

Required gates before merge:
1. schema validation;
2. unit tests;
3. deterministic golden traces;
4. property tests;
5. all changed content recertified;
6. no production content without validation artifact;
7. headless boot/load smoke test;
8. save migration fixture tests;
9. demo carryover fixture tests;
10. UI navigation smoke tests where automation is reliable.

CI/email policy: no test emails, no Gmail integrations, no notification spam. GitHub Actions status is sufficient.

---

# 28. Implementation order in dedicated repository

## 12A — Technical bootstrap
- Godot project;
- pure SimulationCore library;
- schema parser;
- stable IDs/enums;
- headless test harness;
- save shell;
- CI.

## 12B — Vertical slice
Implement QK01–QK02 only:
- counters/customers;
- fee/service intervention;
- Resolve;
- evidence;
- candidate chips;
- commit;
- restart/checkpoint;
- mouse/controller navigation.

Exit gate: deterministic golden traces pass and a new player can complete QK01/QK02 without hidden developer tools.

## 12C — Core systems complete
- all five heuristics;
- capacity2;
- privacy;
- multiple cohorts;
- hard constraints;
- pooling/hybrid objectives;
- Type Lens;
- dead-state support.

## 12D — Validator + content population
- offline solver;
- certification artifacts;
- QK01–QK36 + mastery;
- anti-repetition/content checks.

## 12E — UX/accessibility/platform
- final Phase-6 layouts;
- Deck 1280x800;
- full controller;
- settings/remapping;
- save/Cloud;
- achievements hooks;
- demo carryover.

## 12F — Adversarial QA
- save corruption/recovery;
- Cloud conflict;
- stale content version;
- duplicate input;
- action spam;
- focus loss;
- checkpoint branch contamination;
- all invariants.

## 12G — Empirical gates
- tutorial comprehension;
- queue-manager misread;
- 10-customer readability;
- Type Lens clarity;
- performance;
- demo comprehension;
- content repetition.

## 12H — Release candidate
- certified content only;
- packaging;
- Steam build/demo;
- full regression;
- release checklist.

---

# 29. Prototype empirical gates that do not reopen mechanics by default

The implementation prototype must test:
1. QK01–QK02 comprehension without developer explanation;
2. whether players understand evidence snapshot vs final queue;
3. whether Type Lens clarifies rather than solves;
4. controller traversal at 1280x800;
5. 10-customer late-case readability;
6. fixed-slot animation feels alive enough;
7. reason traces are concise and non-leaking;
8. offline validator practical on late-case world spaces;
9. checkpoint/restart flow feels cheap enough for experimentation;
10. demo carryover path is robust.

Default repair order:
1. UX/presentation simplification;
2. content values/order;
3. hint/explanation;
4. implementation optimization.

Do not add a sixth heuristic, management mechanics, probabilistic AI or real-time control to repair these gates.

---

# 30. Explicit out-of-scope technical complexity

Do not add by default:
- ECS framework;
- networking;
- rollback netcode;
- server backend;
- database server;
- user accounts;
- runtime procedural case generation;
- physics navigation;
- behavior trees;
- machine-learning NPC logic;
- modding API;
- scripting language for players;
- telemetry backend required for offline play.

Simple local analytics hooks for optional playtest builds are allowed if privacy-respecting and removable.

---

# 31. Phase-8 acceptance result

Phase 8 now defines:
- recommended Godot 4.7.x stable stack;
- pure deterministic simulation boundary;
- serialized CaseDefinition/CaseState/evidence/save contracts;
- hidden-world no-leak boundary;
- evaluator and event-order APIs;
- offline exhaustive solver/certification architecture;
- Type Lens anti-oracle API;
- checkpoint/save migration/Cloud/demo-import policies;
- semantic input/controller/Deck contract;
- localization/accessibility boundaries;
- runtime/offline performance separation;
- state hashing and deterministic replay;
- unit/golden/property/fuzz tests;
- CI content-certification gates;
- dedicated-repository implementation order;
- empirical prototype gates that do not reopen mechanics by default.

**PHASE 8 TECHNICAL IMPLEMENTATION SPECIFICATION = COMPLETE.**

No production implementation has begun.

# NEXT DESIGN STEP — PHASE 9 WHOLE-GAME SIMULATION ON PAPER

Perform a complete paper simulation across the entire product, not just demo mechanics:
1. first boot and first 5 minutes;
2. QK01–QK06 full first session;
3. hour ~1 transition into Chapter 2;
4. hour ~3 congestion-heavy middle;
5. hour ~5 pooling/all-world proof chapter;
6. late three-counter synthesis;
7. QK36 campaign ending;
8. mastery/replay path;
9. failure/checkpoint/dead-state/hint behavior;
10. save/resume/Cloud conflict/demo-import edge journeys;
11. controller/Deck stress journey;
12. hostile behavior: spam inputs, restart loops, committing early, pathological but legal intervention choices;
13. detect contradictions between mechanics/content/UX/commercial/technical authority;
14. repair any contradictions in canonical design files, not only in simulation notes;
15. save canonical `GAME17_WHOLE_GAME_SIMULATION.md`, update STATUS/GAME_INDEX, and advance to Phase 10 if complete.
