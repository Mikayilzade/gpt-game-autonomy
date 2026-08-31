# GAME #010 — PHASE 8 TECHNICAL IMPLEMENTATION SPECIFICATION

Date: 2026-08-31
Status: **PHASE 8 ACTIVE — CORE TECHNICAL CONTRACT ESTABLISHED**
Game: Luggage Carousel Zero *(working title)*

Authority: all prior active Game #010 authorities -> `GAME10_PHASE7_CLOSURE.md` -> this file.

This phase specifies how another implementation session can build the frozen design. It does **not** authorize production implementation inside the factory.

---

## 1. Runtime / engine direction

### Preferred implementation target
**Godot 4.7.2 stable + GDScript**, PC/Steam-first.

Fresh check on 2026-08-31:
- Godot 4.7.2 is the current stable 4.x release, published 2026-08-18.
- Godot 4.8 is still a development branch (`4.8-dev4` published 2026-08-26), so the implementation handoff should not target preview builds by default.
- Godot provides a dedicated 2D engine and cross-platform desktop exports suitable for this one-screen deterministic puzzle product.

Sources:
- https://godotengine.org/article/maintenance-release-godot-4-7-2/
- https://godotengine.org/download/archive/

### Why Godot fits
- strong native 2D/control-node workflow for carousel + UI-heavy presentation;
- low overhead for a small offline deterministic game;
- headless/testable scripting is practical for solver/case validation;
- input actions map cleanly to the semantic controller abstraction already frozen;
- no production need for physics, networking, ECS, streaming worlds or engine-heavy 3D systems.

### Stability rule
A dedicated implementation repo may move to a later **stable** Godot 4.x release only after regression tests pass. It must not move to a dev/RC build merely for novelty.

Engine choice is implementation direction, not gameplay canon. A future implementation may use another engine only if it preserves every frozen deterministic/UX contract and does not broaden scope.

---

## 2. Architectural boundary — deterministic core first

The game must be split conceptually into four layers:

1. **Case Data** — immutable authored definition.
2. **Rules Core** — pure deterministic state transition/evaluation functions.
3. **Solver / Certification** — exact search and counterfactual tooling using the same Rules Core semantics.
4. **Presentation / Platform** — rendering, animation, UI, input, persistence, Steam integration.

No presentation object may become authoritative gameplay state.

The Rules Core must be runnable without scene animation, audio, Steam APIs or platform UI. Given the same case definition and action sequence, it must produce byte-for-byte-equivalent logical state on all supported machines.

---

## 3. Canonical runtime state model

### Immutable `CaseDefinition`
Required logical fields:
- `schema_version`
- `case_id`
- `act_id`
- `campaign_order`
- `title_key`
- `n_sockets`
- `pickup_socket` (canonical campaign cases use exactly one)
- `labels_initial[]`
- `bags[]` with `{bag_id, shape_id, mark_id}`
- `occupancy_initial[]` containing `bag_id` or `GAP`
- `passengers[]` containing 1–3 clauses each
- `tick_limit`
- `swaps_per_tick` in `{0,1,2}`
- optional tutorial `swappable_socket_mask`
- `reasoning_tags[]` authoring metadata
- `tutorial_callout_ids[]`
- `certificate_id` / certificate manifest reference
- localization/display-token references for label/shape/mark values

### Mutable `PlayState`
- `occupancy[]`
- `labels[]`
- `passenger_index`
- `ticks_remaining`
- `swaps_remaining_this_tick`
- `terminal_status` = PLAYING / WON / BUDGET_FAILED / DEAD
- `last_pickup_result` structured data or null
- `action_index`

Undo history is not part of the state identity used by the solver. It is a presentation/session stack of prior committed `PlayState` snapshots or reversible deltas.

### Invariants
At every committed boundary:
- exactly N occupancy slots and N labels exist;
- every remaining bag ID appears exactly once; removed bags appear zero times;
- GAP may appear multiple times;
- labels are values by socket and never move on ADVANCE;
- pickup remains one fixed socket;
- passenger index is monotonic except when Undo restores a prior snapshot;
- ticks never increase except Undo/Restart;
- swaps remaining lies in `0..K`;
- all states validate before persistence.

---

## 4. Pure rules API contract

The implementation should expose equivalent pure operations even if names differ:

- `validate_case(definition) -> ValidationResult`
- `initial_state(definition) -> PlayState`
- `legal_adjacent_swaps(definition, state) -> list<Edge>`
- `apply_swap(definition, state, edge) -> PlayState`
- `preview_advance(definition, state) -> PreviewResult`
- `apply_advance(definition, state) -> AdvanceResult`
- `evaluate_predicate(passenger, bag, pickup_label) -> ClauseResults`
- `is_exactly_feasible(definition, state) -> bool`
- `restart(definition) -> PlayState`

`apply_swap` and `apply_advance` must not animate, wait, read input, call Steam, localize strings or mutate UI nodes.

### Deterministic action log
For test/debug/replay purposes, an action is one of:
- `SWAP(edge_min_socket, edge_max_socket)` with explicit ring-seam normalization;
- `ADVANCE`.

A complete logical playthrough is `case_id + content_manifest_version + action sequence`. This is sufficient to replay/debug a deterministic state trajectory.

---

## 5. Adjacent ring representation

Canonical ring neighbors of socket `i`:
- clockwise: `(i + 1) mod N`
- counter-clockwise: `(i - 1 + N) mod N`

A swap edge must be stored canonically so S(N-1)<->S0 is not treated as a special teleport. Recommended canonical edge ID is the lower index of the clockwise edge origin or an explicit `{a,b}` sorted pair plus ring-adjacency validation.

The presentation layer may draw an oval/circle, but gameplay geometry is this discrete cycle graph only.

---

## 6. Advance ordering — implementation acceptance contract

The Rules Core must execute exactly:
1. rotate all occupancies one socket clockwise simultaneously;
2. inspect occupancy now at pickup;
3. if BAG, evaluate current front passenger using fixed pickup label + bag shape/mark;
4. if all clauses match, replace bag with GAP and increment passenger index once;
5. decrement tick count;
6. success check before zero-budget failure;
7. if still nonterminal and ticks remain, reset swaps to K;
8. exact feasibility check; if no winning path, set DEAD; else PLAYING.

No animation callback or scene timing may alter this ordering.

Unit tests must include every Phase-4 regression microcase plus correction cases R1–R8.

---

## 7. Predicate representation

Use structured data, never free-form condition strings.

Recommended clause record:
- `dimension`: LABEL | BAG_SHAPE | BAG_MARK
- `value_id`: stable content ID

Validation rejects:
- zero clauses;
- >3 clauses;
- duplicate dimensions;
- unknown dimensions/values;
- operators other than positive equality.

Display order is canonical LABEL -> BAG_SHAPE -> BAG_MARK regardless of authored JSON ordering.

Localization changes only display strings, never value IDs.

---

## 8. Case file format

Preferred source format: human-reviewable **JSON** or equivalent text data committed to version control. Runtime import may compile to Godot resources, but source authority should remain diffable text.

Illustrative shape only:
```json
{
  "schema_version": 1,
  "case_id": "A01",
  "n_sockets": 3,
  "pickup_socket": 0,
  "labels_initial": ["RED", "BLUE", "GREEN"],
  "bags": [
    {"bag_id":"A","shape_id":"SQUARE","mark_id":"DOT"}
  ],
  "occupancy_initial": ["A", "GAP", "GAP"],
  "passengers": [
    {"clauses":[{"dimension":"LABEL","value_id":"RED"}]}
  ],
  "tick_limit": 1,
  "swaps_per_tick": 0
}
```

Actual campaign data must match the validated content authority, not this illustrative mini-record.

### Build-time validation
CI/editor import must fail on invalid cases. Invalid content must never be silently repaired at runtime.

---

## 9. Solver / certification boundary

### One semantic engine
Solver search must call the same pure swap/advance semantics used by gameplay. A duplicated "fast approximation" implementation is forbidden unless equivalence tests prove it against the authoritative Rules Core.

### Tick-boundary macro search
For exact certification, prefer nodes at pre-Advance boundaries:
`(canonical occupancy, label vector, passenger_index, ticks_remaining)`.

For each node:
1. enumerate every distinct label vector reachable through 0..K legal adjacent swaps;
2. resolve exactly one ADVANCE;
3. canonicalize trait-identical bag IDs where safe;
4. memoize feasibility/metrics.

### Exact outputs required for shipped cases
At build/certification time produce:
- solvable within budget;
- minimum ticks;
- optional minimum effective swaps among minimum-tick solutions;
- viable first resulting-label states;
- family-specific counterfactual results needed by content authority;
- content certificate/version hash;
- any data needed for deterministic DEAD checks.

### Runtime DEAD strategy
Semantic requirement: exact result. Technical implementation may choose one of two backends behind the same interface:
- precomputed feasibility lookup for reachable campaign states; or
- exact memoized runtime solver.

The implementation must choose per benchmark, not by changing game rules.

**Performance gate:** a committed action must not freeze presentation waiting on a solver search. Target exact DEAD verdict <=100 ms p95 on target Steam-Deck-class hardware for shipped campaign cases. If a runtime backend cannot meet this, that case must ship with precomputed feasibility support or be simplified/rejected before release.

No approximate/heuristic DEAD status is allowed.

---

## 10. Solver canonicalization rules

Safe:
- trait-identical bags interchangeable because stable bag ID is not observed by gameplay;
- duplicate label token identities do not exist; only values by socket matter;
- equal-value adjacent no-op swaps omitted;
- equivalent raw swap sequences that reach the same label vector with same remaining bandwidth dedupe;
- `remaining_passengers > ticks_remaining` immediately infeasible;
- if no remaining bag trait class can ever satisfy a remaining passenger's shape/mark clauses, immediately infeasible.

Unsafe:
- rotationally quotienting the ring, because pickup S0 breaks symmetry;
- treating non-pickup label positions as a multiset, because adjacent-only swaps make spatial position causal;
- compressing GAPs;
- reordering passenger queue;
- merging distinct bags that differ in any predicate-relevant trait.

---

## 11. Persistence model

Use a versioned local save with atomic replacement semantics.

Recommended logical files:
- `profile_save.json` — progression/settings/demo migration/platform reconciliation;
- `active_case.json` — optional resumable in-progress case;
- platform cloud may synchronize these files but is not their semantic owner.

### `profile_save`
Must cover Phase-7 fields:
- schema/content versions;
- completed case IDs;
- best ticks by case;
- act skip-used/skipped-open state or canonical recomputation source;
- campaign ending state;
- demo import version;
- tutorial acknowledgements;
- settings/accessibility/input configuration;
- achievement reconciliation flags if needed.

### `active_case`
Persist enough to resume exactly:
- case ID + content manifest version;
- full committed `PlayState`;
- action/undo history sufficient for continued stepwise Undo, or explicitly persist a bounded full snapshot stack if memory size is trivial;
- last-result state if needed for presentation restoration.

If content version changes incompatibly, do not guess-migrate an active puzzle state. Preserve profile progress, discard/restart that active case with a clear one-time notice.

### Atomicity
Write temp -> flush/close -> replace target. Keep one previous-good backup where practical. A malformed save must fail safe to backup/default without corrupting content files.

---

## 12. Demo/full-game import

Steamworks current documentation allows a demo save to use shared cloud storage with the full app and recommends granting demo-earned achievements only when the full game loads qualifying progress.

Technical contract:
- demo and full game share stable case IDs and logical profile schema subset;
- import operation carries an explicit `demo_import_version`;
- merge is idempotent and monotonic;
- completion is set union;
- `best_ticks[case] = min(valid existing, valid imported)`;
- act unlock/frontier/skip state is **not trusted from demo** and is recomputed under Phase-7 progression rules;
- settings import only when no explicit full-game preference already supersedes it;
- achievement adapter evaluates after merge;
- repeated Steam Cloud sync/import cannot duplicate or regress progress.

Sources checked 2026-08-31:
- https://partner.steamgames.com/doc?q=cloud
- https://partner.steamgames.com/doc?q=achievements

---

## 13. Achievement adapter

Gameplay/progression code emits semantic events/state; a platform adapter owns Steam achievement calls.

Rules:
- local predicates for the 12 frozen achievement IDs are deterministic and testable offline;
- platform grant is idempotent;
- failure/unavailability of Steam API never blocks gameplay or local progression;
- on startup/full-game demo import, reconcile earned local predicates with platform state;
- no demo achievement calls.

Steamworks integration remains optional for non-Steam builds but the base product must preserve local trigger semantics.

---

## 14. Input abstraction

Create actions matching Phase-6 semantics, not physical button names:
- FocusPrevSocket
- FocusNextSocket
- SelectSwapOrigin
- ConfirmSwapTarget
- CancelSelection
- Preview
- Advance
- Undo
- Restart
- OpenPause
- FocusPassengerPanel
- TogglePredicateDetails

All gameplay must be completable using controller action mappings alone.

Input layer produces intents. Rules Core validates/commits actions. Holding a key/button may repeat navigation but must never accidentally repeat committed swaps/Advances without distinct confirmation semantics.

Current Steam hardware guidance still emphasizes Deck-native resolutions and controller-complete functionality; 1280x800 remains the primary certification viewport.

---

## 15. Presentation architecture

Recommended Godot separation:
- `GameSession` orchestrator owns current definition/state and invokes Rules Core;
- `CarouselView` renders sockets/bags/gaps/labels from state;
- `PassengerPanel` renders public queue;
- `HUD` renders ticks/swaps/result state;
- `InputRouter` translates device actions to semantic intents;
- `TransitionPlayer` animates a **known already-resolved logical transition**;
- `SaveManager`, `ProgressionManager`, `AchievementAdapter`, `LocalizationCatalog` remain separate services/modules.

Critical rule: resolve logical state first (or compute a transition object), then animate that transition. Animation completion must not decide whether pickup succeeds.

Reduced-motion mode uses the same transition object with different visualization.

---

## 16. Localization readiness

No gameplay logic may compare localized strings.

Use stable IDs for:
- case titles;
- act names;
- label/shape/mark values;
- predicate dimension names;
- result explanations;
- tutorial callouts;
- menus/settings/achievements.

UI containers must support wrapping/expansion rules already frozen at 125/150% scale. Avoid concatenating grammar-sensitive strings where a localized template key is safer.

Base implementation should make adding locales data-driven even if launch-language count is not frozen here.

---

## 17. Accessibility hooks

Technical implementation must expose:
- text scale 100/125/150;
- animation Normal/Fast/Instant or Reduced Motion;
- high-contrast focus;
- permanent color-redundant symbols/patterns;
- configurable bindings;
- Confirm Advance option;
- separate gameplay/ambience volume;
- dynamic glyph provider/fallback glyph set;
- semantic accessible names for focused sockets, passenger clauses and controls where the UI toolkit/platform permits.

Accessibility settings never alter puzzle certification/budgets.

---

## 18. Performance / memory budgets

This game should be CPU/GPU-light. Budgets are conservative release gates, not excuses to add effects.

On Steam-Deck-class target hardware:
- sustain 60 fps at native 1280x800 during normal/fast presentation; 30 fps fallback is not the design target;
- no gameplay transition should allocate large transient structures every frame;
- Rules Core state copy should remain tiny (N<=8); snapshot Undo is acceptable if measured memory remains trivial;
- UI input response should feel immediate (<1 rendered frame before feedback where practical);
- exact DEAD computation target <=100 ms p95 as above, never blocking animation/render thread long enough to hitch perceptibly;
- case load/save should complete comfortably below human-notice thresholds on local storage; no network dependency;
- full campaign data/certificates should remain small enough for ordinary package/save handling; any solver table explosion is a content/solver gate, not a reason to weaken exactness.

No physics simulation, particle density or 3D scene may jeopardize these budgets.

---

## 19. Test hooks / required automated suites

### Rules regression
Automate Phase-4 M1–M12 and correction R1–R8.

### Invariant fuzz
Generate legal small states/actions and verify:
- ring length preserved;
- labels never Advance;
- bags never duplicate;
- pickup removes at most one bag/tick;
- final-tick win beats budget failure;
- Undo round-trip restores exact state.

### Solver equivalence
For tiny exhaustive instances, compare:
- brute-force raw action search;
- optimized tick-boundary solver.

They must agree on feasibility and minimum ticks.

### Save round-trip
Serialize/deserialize every logical state field; exact equality required.

### Demo merge
Repeated import N times yields same final profile as one import.

### Progression
Test A01–A03 strict gate, one skip per act, all-but-one unlock, blocker return, ending vs all-cases-complete distinction.

### Accessibility/input
Controller-only scripted navigation reaches every required gameplay/menu state; text-scale layouts have no predicate truncation at canonical test locales/synthetic long strings.

---

## 20. Implementation order for dedicated repository

### 12A — Bootstrap / deterministic foundation
1. pin stable engine version;
2. create Rules Core + case schema validator;
3. implement M/R regression tests;
4. implement exact tiny solver baseline;
5. load one minimal case headlessly.

### 12B — Vertical slice
1. one N3/N4 case;
2. controller/mouse semantic input;
3. swap + preview + Advance + pickup;
4. Undo/Restart/DEAD;
5. minimal passenger/HUD presentation;
6. deterministic save/resume.

### 12C — Core systems complete
- full envelopes K0/K1/K2;
- full predicate grammar;
- progression/skip;
- solver certification backend;
- demo import contract;
- achievement-local predicates.

### 12D — Content population
- import/certify 36–48 campaign cases under Phase-5 pipeline;
- seven-case demo path;
- reject failing/duplicate cases rather than weakening validator.

### 12E — UX/accessibility/platform
- full responsive screens;
- 150% text;
- reduced motion;
- controller-only;
- Steam integration/cloud/achievements where applicable.

### 12F — Adversarial QA
- save corruption/recovery;
- cloud/demo idempotency;
- solver mismatch;
- terminal Undo;
- content-version migration;
- input hot-swap;
- localization overflow;
- performance.

### 12G — empirical gates
Playtest the carried Phase-3/6/7 gates without silently rewriting mechanics.

### 12H — release candidate
Packaging, demo/full separation, regression, storefront build checklist.

---

## 21. Explicit technical non-goals

Do not build:
- multiplayer/network gameplay;
- authoritative online backend;
- account/login service;
- physics baggage simulation;
- procedural endless runtime generator;
- level editor/Workshop pipeline;
- telemetry dependency for rules;
- ECS/service architecture disproportionate to N<=8 puzzle state;
- production code inside this factory repo.

Optional anonymous analytics may be considered later only under privacy/platform requirements and can never be required for play.

---

## 22. Phase-8 open validation before closure

Core technical architecture is specified, but Phase 8 should not close until one hostile pass proves it is internally complete.

Next pass must:
1. write a fully valid canonical sample case schema for at least one demo case and ensure every frozen field maps cleanly;
2. walk SWAP -> DEAD -> Undo, ADVANCE -> pickup -> Undo, final-tick win, K2 two-swap, demo import and active-case resume through the architecture;
3. attack solver/runtime DEAD performance fallback and certificate-version compatibility;
4. freeze exact authority for content manifest/save schema migration behavior;
5. define build-time certificate artifact minimum fields/hashes;
6. close Phase 8 only if a fresh implementation session would not need to invent state/persistence/solver/platform semantics;
7. if clean, continue immediately to **Phase 9 Whole-Game Simulation on Paper**.

**PHASE 8 ACTIVE. DESIGN COMPLETE = NO.**