# GAME #018 — PHASE 8 TECHNICAL IMPLEMENTATION SPECIFICATION

Date: 2026-09-06
Selected concept: **LOCAL TIME**
Status: PHASE 8 COMPLETE — WHOLE-GAME SIMULATION NEXT
Production implementation: NO

## 1. Technical direction
**Recommended runtime: Godot 4.7.x stable, GDScript-first.** As checked 2026-09-06, Godot 4.7.2 is the current stable patch while 4.8 is development/pre-release. The implementation repository should pin a tested stable 4.7 patch initially and upgrade only behind full deterministic/golden regression.

Why Godot fits: compact single-player 3D/2.5D dioramas, data-driven authored content, strong UI/input needs, tiny authoritative state, no networking/physics authority, modest rendering requirements, easy headless logic tests, and low licensing/operational burden.

Alternatives: Unity is viable but adds unnecessary project/package/licensing surface for this bounded game; a custom framework would increase UI/controller/localization/tooling cost. C# in Godot is not required. The puzzle kernel must remain engine-light enough that its state/Resolve/solver tests do not depend on rendering nodes.

Fresh technical evidence checked this run: Godot official archive/release policy shows 4.7.2 stable (2026-08-18) and 4.8-dev4 as development; Steamworks documents Steam Cloud/Auto-Cloud, demo save sharing with the full app, and Deck support for major input APIs. Store promises remain conditional on real-device/build validation.

## 2. Authority boundaries
Three layers are mandatory.

### A. Canonical mutable authority
Small serializable values only: case_id, ruleset_version, beat_index, move_count, clock socket assignments, persistent site/object states, object locations, carrier payload/location states, public persistent flags, remaining budgets, terminal status, completion records and pre-Resolve checkpoint.

### B. Derived state
Never serialized as authority: effective local time per site, NOW predicates, footprint coverage, legal-placement graph, objective truth, focus graph, dead-state proof, visual highlight state. Recompute from canonical state + immutable case data.

### C. Presentation state
Never puzzle authority: scene nodes, transforms used only for art, tweens, particles, camera, animation progress, audio, hover/focus effects, reason-trace animation cursor. A crash during animation must never create a different puzzle result.

## 3. Immutable data model
Use versioned declarative resources (JSON or Godot Resources compiled from a human-reviewable source format). No arbitrary case scripts.

`CaseDef`: schema_version, ruleset_version, case_id, chapter/tier, title_key, objective_text_key, clocks[], sockets[], footprints[], sites[], objects[], carriers[], rule_instances[], objectives[], constraints, initial_state, budgets, difficulty_band, concept_ids, validator_metadata, human_causal_proof[], anti_enumeration_tags[], art_kit_id, demo/mastery flags.

`SocketDef`: socket_id, world_anchor, allowed_clock_ids/tags.

`FootprintDef`: footprint_id, per_socket_covered_site_ids. Logical coverage is explicit; runtime geometry never decides it.

`ClockDef`: clock_id, time_label_id, footprint_id, movable, move_cost, allowed_socket_ids, initial_socket_id.

`SiteDef`: site_id, presentation_anchor, base_tags, rule_instance_ids, initial_persistent_state, resident_object_ids.

`ObjectDef`: object_id, family_id, public_tags, persistent_state_enum, initial_location, hazard_tags.

`CarrierDef`: carrier_id, ordered public path, capacity baseline 1, enabling predicate/rule reference, initial payload/location.

`RuleInstance`: instance_id, family enum limited to the eight Phase-5 families, subject IDs, public params, source_state, condition AST, target_state/flag/dispatch intent, reason_string_key. Conditions may use only frozen public primitive predicates.

`ObjectiveDef`: objective_id, AST using MILESTONE/CURRENT/OBJECT_AT/FLAG/ALL/ANY/NOT/AT_MOST_MOVES/AT_MOST_BEATS, display key, required flag.

All IDs are stable strings. Validation rejects missing refs, duplicate IDs, unsupported family/version, unknown enum values and any executable/script field.

## 4. Runtime canonical state schemas
`CaseState`: schema_version, ruleset_version, content_hash, case_id, beat_index, move_count, clock_socket_by_id, persistent_site_state_by_id, object_state_by_id, object_location_by_id, carrier_state_by_id, persistent_flags, remaining/maximum budgets, terminal_status.

`PlanningState`: canonical CaseState plus unresolved legal clock relocations and move-cost delta. It is not committed across Resolve until legality passes.

`Checkpoint`: exact canonical pre-Resolve CaseState + planning baseline. Undo Turn restores this, never inverses transitions.

Use integers/enums/stable IDs; no floating point participates in puzzle logic. World transforms are presentation lookup only.

## 5. Deterministic Resolve contract
A single pure-ish kernel entry point conceptually accepts `(CaseDef, CaseState, confirmed PlanningActionSet)` and returns `(new CaseState, ReasonTrace, BoundaryResult)`.

Order is frozen:
1. validate planning legality/conflicts/budgets; illegal returns no mutation/beat;
2. freeze S0;
3. derive C0 effective times/NOW predicates;
4. evaluate all persistent/hazard/accept/dispatch/coupled intents against S0+C0 only;
5. sort intents by stable entity/rule IDs solely for reproducible trace, **not** conflict resolution;
6. reject contradictory writes as content/runtime assertion failure;
7. atomically commit compatible persistent writes;
8. carrier stage: deterministic max-one-hop dispatch/handoff; arrivals cannot accept this Resolve;
9. recompute derived truth;
10. evaluate hard failure, then success, then budget/dead-state boundary according to Phase 4;
11. increment beat for successful Resolve and emit immutable trace.

No scene callback, frame delta, animation, dictionary iteration order, random number or physics query may influence this result.

## 6. State identity and canonical hashing
Solver/test identity excludes presentation, reason trace, checkpoint, UI focus and decorative values. Canonicalize maps by sorted stable ID and serialize a fixed ordered tuple containing case/ruleset version, beat/budget values, clock sockets, persistent states, locations, carriers, flags and terminal state.

Use a stable cryptographic/content hash for diagnostics/cache keys, but equality is structural canonical-state equality rather than trusting hash collision absence.

Solver may normalize only genuinely semantically interchangeable entities explicitly marked with a validated symmetry group. Never infer symmetry from art/name/position.

## 7. Validator architecture
Validation pipeline:
1. schema/reference/enums/version validation;
2. hard-ceiling and footprint/socket legality validation;
3. static rule grammar validation;
4. reachable-state exhaustive exploration using the same Resolve kernel as runtime;
5. contradiction/determinism assertions on every reachable Resolve;
6. solver proves >=1 win and computes lexicographic best `(moves, beats)` plus useful alternate-solution metrics;
7. unreachable/initially-satisfied objective checks;
8. human-proof/anti-enumeration metadata gates;
9. content-family/variety reports across campaign.

No separate simplified solver rules. Solver and game call the same authoritative transition functions.

## 8. Exhaustive deterministic solver
Action generation enumerates legal clock relocations/configurations plus Resolve under exact remaining budgets. Search uses BFS for minimum beats where appropriate and a deterministic cost ordering for `(moves, beats)` records; visited set uses canonical structural identity/hash.

Because campaign ceilings are <=3 clocks, <=8 sites, <=5 labels and <=8 mastery Resolves, exhaustive certification is a design requirement. If a case exceeds practical state/time budgets, simplify the case rather than ship heuristic DEAD claims.

Outputs per case: solvable, shortest cost, number/range of solution families where tractable, reachable hard-fails, certified dead-state table/cache optionally generated offline, branching/state counts, dominant first-action concentration, and regression witness paths. Runtime hints do not expose solver paths.

A runtime DEAD message may use a shipped proof/cache only when its content/ruleset hash matches exactly; otherwise omit the claim or run a bounded-to-completion exhaustive proof if guaranteed safe.

## 9. Reason trace / event log
Every authoritative mutation emits a structured `ReasonEvent`: resolve_index, stage, event_type, subject_id, source_state, target_state, condition_refs, clock/site refs, localization_key, localization_args.

Trace order follows canonical Resolve stages and stable IDs. Player prose is localized from structured facts; do not store English as logic.

Reason trace is diagnostic/presentation evidence, not authority. Replay consumes trace + before/after snapshots to animate; replay cannot invoke Resolve or mutate CaseState. Save may retain the latest trace solely to replay after interruption.

## 10. Input abstraction and focus graph
Gameplay commands are semantic actions: FocusNext/Previous, DirectionalFocus, Select, Cancel, Inspect, ToggleOverview, Resolve, UndoPlacement, UndoTurn, Replay, Pause. Mouse, keyboard, controller and Steam Input map to these; puzzle code never branches on device.

Focus nodes are landmarks, clocks, legal sockets, objective rows and action-rail controls. In placement mode, graph is regenerated from legal sockets using authored/spatial neighbors with deterministic fallback. Every focus node must have a route back; automated traversal checks no traps. Pointer drag, if added, resolves to the same SelectClock -> SelectSocket -> Confirm commands.

Steam Deck target remains 1280x800 controller-only completion; Verified status is never assumed. Test on a retail Deck/representative SteamOS hardware before claims.

## 11. Profile/save model
Separate cloud-worthy progression from machine-local graphics/device preferences.

`ProfileSave`: schema_version, game_build_semver, ruleset_version, profile_uuid, monotonic_save_revision, written_utc, campaign_progress, per_case_records `{completed,best_moves,best_beats,optional_marks}`, mastery_unlocks, achievement_intents/awarded IDs, accessibility/gameplay preferences suitable across devices, current_case_checkpoint optional, latest_reason_trace optional, demo_import_receipt optional.

Machine-local file: resolution/window mode, render scale and hardware-specific graphics settings; exclude from Steam Cloud.

### Atomic write/recovery
Write new serialized data to temp; flush/close; parse+checksum/self-validate temp; rotate current valid save to `.bak`; atomically rename temp to current where platform semantics allow. On boot: validate current; if corrupt load backup; if both fail preserve corrupt files and offer new profile rather than silently overwriting evidence.

Never deserialize executable objects. Migrations are explicit pure version-to-version transforms with fixtures.

## 12. Demo -> full import
Preferred Steam setup: shared cloud/progress path or full-app cloud storage as supported by Steam demo guidance, but only after AppID/depot testing.

Import contract:
1. detect compatible demo save by signed/validated schema marker + product family ID;
2. parse and migrate demo schema without modifying source;
3. merge only LT01–LT06 completion/best records, compatible settings and glossary/progression unlock needed to enter Case 07;
4. never downgrade stronger full-game progress;
5. record source demo save ID/hash + imported revision in `demo_import_receipt`;
6. repeated import of same or older demo state is a no-op; newer demo records merge by monotonic best/progress rules;
7. preserve both source and pre-import full backup until successful post-write validation.

Test clean full install, existing full progress, repeated import, old demo schema, cloud-restored demo, corrupted demo and interrupted import. Do not advertise carryover until these pass.

## 13. Steam Cloud policy
Start with Steam Auto-Cloud for the small validated profile files unless implementation testing shows need for direct Remote Storage control. Steam documentation says Auto-Cloud syncs configured files at application start/exit; keep hardware-specific settings out.

The game cannot promise to control every Steam-client sync conflict. In-game protection therefore uses save UUID/revision/time plus backups. If the game itself sees two importable/divergent profiles, never silently merge checkpoint state. Progress records may merge monotonically (completed OR; best score = better valid score), but mutually divergent active checkpoints are preserved as recovery candidates and user chooses which to continue.

Cloud quotas/path configuration, demo/full sharing, offline->online, two-PC divergence, Deck suspend/resume and uninstall/reinstall must be tested through actual Steam builds. Dynamic Cloud Sync is not required baseline; enable only after explicit suspend/resume validation.

## 14. Localization contract
All player text uses localization keys. Rule logic references enum/time IDs, never translated strings. Structured reason events format localized templates with typed args. Time labels such as `08:05` are data formatted consistently and never parsed back from display text.

UI containers must support expansion/wrapping and 3 text sizes. Essential labels cannot be baked into textures. Font stack must cover Latin, Cyrillic, Simplified Chinese, Japanese and Korean target sets with licensed fonts; glyph coverage gets automated build checks. Pseudolocalization tests +30–40% expansion and long German/Russian strings at 1280x800. CJK line breaking and controller glyph/prose separation require manual QA.

## 15. Rendering/performance budget
Logic target is trivial relative to rendering. Diorama presentation should use a bounded camera and modular assets; puzzle-relevant outlines/clock labels are UI/readability critical.

Shipping targets to validate, not hardware promises: stable 60 fps at native 1280x800 on Steam Deck target path; optional 30 fps cap only as user power choice, never required for logic; Resolve kernel completes effectively instantaneously on shipping hardware; normal frame never waits on solver search.

Guidelines: <=8 logical sites but decorative props may be batched/instanced; bounded dynamic lights/shadows; no gameplay physics; avoid expensive transparency stacks for footprints; prewarm common shaders/particles; animation skip/reduced-motion path must reduce rather than increase cost. Establish measured GPU/CPU/frame-time budgets in vertical slice, then gate art additions against them.

## 16. Test architecture
### Kernel/property invariants
- same canonical state + action => byte/structurally identical authoritative result;
- current predicates equal recomputation and never survive as authority;
- moving clocks alone cannot reverse persistent state;
- conflicting time labels on one site never commit;
- one carrier max one hop/Resolve;
- newly arrived cargo cannot accept same Resolve;
- max one persistent advance/entity/Resolve unless explicitly frozen otherwise (baseline none);
- contradictory intents are validator/runtime assertion failures;
- undo checkpoint round-trip restores exact canonical state;
- serialize->deserialize preserves canonical identity;
- presentation frame rate/order cannot change result.

### Golden LT01–LT06
Store authored fixtures for initial state, representative valid/invalid actions, exact post-Resolve canonical snapshots and structured reason events. Include persistence proof (LT01/02), irreversible hazard (LT02/05), coupled simultaneous truth (LT03/06), conflict rejection (LT03), handoff/arrival boundary (LT04), multi-clock synthesis and alternate valid route (LT06).

### Save/cloud fixtures
Every historical schema migration; temp-write interruption; corrupted current + valid backup; duplicate demo import; older/newer demo; divergent progress merge; unsupported future schema fails safely.

### UI automation
Controller-only navigation reaches every required action; focus graph has no trap; critical 1280x800 layouts at all text sizes/pseudolocales; Resolve/skip/reduced-motion produce same authority.

## 17. Content authoring workflow
Author works in human-reviewable case data, not scene scripts. Tooling must provide:
- schema-aware case editor/importer;
- socket/footprint visualization with exact covered site IDs;
- rule/objective builder constrained to approved grammar;
- initial-state preview;
- one-click validate/solve;
- shortest-cost/state-count/branching report;
- reachable contradiction and hard-fail witnesses;
- human_causal_proof and anti-enumeration checklist;
- reason-trace preview;
- 1280x800 framing/readability preview;
- campaign variety report.

A case cannot enter shipping catalog unless validator succeeds for its exact content hash. CI validates all cases headlessly and runs golden/kernel/save tests.

## 18. Future implementation dependency order
12A bootstrap: pin stable engine; repository/CI; pure data schemas; canonical kernel; serialization; LT01 fixture; headless tests.

12B vertical slice: LT01–LT02 playable with diorama, semantic input, NOW/DONE, Resolve/reason trace, checkpoint/undo; validate mouse + controller.

12C core systems: all eight families, conflicts, carriers, objectives, solver/validator, dead certification, profile/save, focus graph.

12D content: author/validate full target catalog with automated reports; cut weak cases rather than expand grammar.

12E UX/platform: full LT01–LT06 onboarding, accessibility, localization plumbing, Steam integration, controller/Deck/readability.

12F adversarial QA: save corruption/import/cloud divergence, deterministic fuzz/property tests, exploits, interruption during Resolve, content regression.

12G empirical gates: Phase 3/6/7 comprehension, preview-oracle, Deck, content uniqueness, price/demo and localization semantic QA gates.

12H RC: performance/build/package/store/demo/full upgrade regression.

No later phase may make presentation nodes authoritative to save time.

## 19. Technical acceptance criteria
Phase 8 considers implementation sufficiently specified when a future implementation agent can satisfy all of these without inventing gameplay:
1. all case content loads from non-executable validated data;
2. headless kernel produces deterministic canonical snapshots for LT01–LT06;
3. runtime and exhaustive solver share the exact Resolve semantics;
4. every shipping case solver-proves >=1 win and no reachable ambiguous write;
5. DEAD is shown only from exact exhaustive proof matching content/ruleset hash;
6. reason trace explains every mutation from structured public causes;
7. all input devices map to semantic commands and controller path has no focus trap;
8. save writes are versioned, atomic/recoverable and migration-tested;
9. demo import is monotonic/idempotent and cannot downgrade full progress;
10. cloud/hardware-specific preferences are separated and Steam claims wait for build tests;
11. localization cannot alter rule semantics and target scripts have glyph/layout QA;
12. puzzle authority is independent of frame rate, animation, rendering and physics;
13. CI can validate all content headlessly and run golden/property/save suites;
14. 1280x800 Deck target path is readable/controller-complete on real hardware before public claim;
15. no production implementation exists in the factory repository.

## 20. Unresolved empirical/implementation gates
- Confirm current stable Godot patch at actual implementation start; do not upgrade merely because 4.8 becomes stable.
- Measure Godot 4.7 Vulkan/compatibility renderer behavior on target Deck/Windows hardware and choose renderer from evidence.
- Decide Auto-Cloud versus direct Remote Storage only after demo/full AppID/path tests.
- Verify Steam demo/full cloud sharing and carryover in real Steamworks configuration before marketing it.
- Test suspend/resume/offline/two-device divergence before considering Dynamic Cloud Sync.
- Measure exhaustive solver worst-case state counts on authored late/mastery cases; simplify cases if certification becomes slow.
- Validate fonts/licenses and CJK memory/layout footprint.
- Establish real vertical-slice frame budgets before freezing decorative rendering scope.

None of these gates changes the frozen puzzle grammar.

## 21. Phase result
Phase 8 locks engine direction, canonical/derived/presentation boundaries, data schemas, deterministic Resolve implementation contract, state identity, validator/solver, reason trace, semantic input/focus, robust saves/demo import/cloud policy, localization, rendering targets, automated testing, authoring workflow and future implementation order.

No contradiction with Phases 3–7 was found. No production code was created.

**PHASE 8 TECHNICAL SPECIFICATION = COMPLETE.**

# NEXT DESIGN STEP — PHASE 9 WHOLE-GAME SIMULATION ON PAPER
Create `GAME18_WHOLE_GAME_SIM.md`. Walk the product end-to-end: first boot/accessibility, LT01–LT06 demo, transition to full game, representative Cases 09/18/24/30/34/36, mastery, replay/efficiency, quit/load during planning and Resolve, Undo/Restart, controller-only/Deck path, localization stress, demo->full import, cloud/offline/divergent-save scenarios, and hostile player behavior. Track every contradiction/ambiguity against the authority chain; repair only with explicit minimal amendments. Stress whether hour-5 play remains causal reasoning rather than socket enumeration and whether 36+12 should survive the quality gate. End with a Phase-9 defect ledger and exact Phase-10 adversarial-review targets. Do not start production implementation.