# GAME #010 — PHASE 8 TECHNICAL IMPLEMENTATION SPECIFICATION CLOSURE

Date: 2026-08-31
Status: **PHASE 8 COMPLETE**
Game: Luggage Carousel Zero *(working title)*

Authority: all prior active Game #010 authorities -> `GAME10_TECHNICAL.md` -> this file. This file resolves remaining schema, DEAD/Undo, certificate, manifest and migration ambiguity.

## 1. Canonical complete case example
The following is a valid logical instance of Demo-03 / A07 under adjacent-only swap canon. Field names are normative at semantic level; serialization syntax may vary.

```json
{
  "schema_version": 1,
  "case_id": "A07",
  "act_id": "A",
  "campaign_order": 7,
  "title_key": "case.a07.title",
  "n_sockets": 5,
  "pickup_socket": 0,
  "labels_initial": ["RED","BLUE","GREEN","YELLOW","PURPLE"],
  "bags": [
    {"bag_id":"A","shape_id":"TRIANGLE","mark_id":"DOT"},
    {"bag_id":"B","shape_id":"ROUND","mark_id":"STAR"},
    {"bag_id":"C","shape_id":"TRIANGLE","mark_id":"STRIPE"},
    {"bag_id":"D","shape_id":"SQUARE","mark_id":"DOT"},
    {"bag_id":"E","shape_id":"ROUND","mark_id":"DOT"}
  ],
  "occupancy_initial": ["A","B","C","D","E"],
  "passengers": [
    {"clauses":[
      {"dimension":"LABEL","value_id":"RED"},
      {"dimension":"BAG_SHAPE","value_id":"ROUND"}
    ]},
    {"clauses":[
      {"dimension":"LABEL","value_id":"GREEN"},
      {"dimension":"BAG_SHAPE","value_id":"SQUARE"}
    ]}
  ],
  "tick_limit": 2,
  "swaps_per_tick": 1,
  "swappable_socket_mask": null,
  "reasoning_tags": ["F1","F6","STAGING_SIGNIFICANT"],
  "tutorial_callout_ids": [],
  "certificate_id": "A07-cert-v1",
  "display_tokens": {
    "labels": ["RED","BLUE","GREEN","YELLOW","PURPLE"],
    "shapes": ["TRIANGLE","ROUND","SQUARE"],
    "marks": ["DOT","STAR","STRIPE"]
  }
}
```

Authoritative winning trace: SWAP S1<->S2; ADVANCE serves E to P1; SWAP S0<->S1; ADVANCE serves D to P2. Forbidding non-S0-incident swaps makes the case unsolvable, satisfying `STAGING_SIGNIFICANT`.

## 2. Hostile transition walkthroughs

### 2.1 SWAP -> DEAD -> Undo
Start in PLAYING with K=1. Commit one legal adjacent SWAP. Rules Core creates the new state, decrements swaps to 0, then exact feasibility is checked. If infeasible, terminal becomes DEAD. Presentation may animate the swap first and then show DEAD, but forward SWAP/ADVANCE are disabled. Undo restores the exact pre-swap labels, prior `swaps_remaining_this_tick`, terminal PLAYING, ticks, occupancy, passenger index and last-result state. No solver side effect survives Undo.

### 2.2 successful ADVANCE -> Undo
Pre-Advance snapshot/action-boundary state is retained. ADVANCE rotates occupancy, evaluates pickup, removes at most one bag/passenger, decrements tick, checks WIN before budget failure, then feasibility. Undo restores the entire pre-Advance committed state atomically, including resurrecting a consumed bag and passenger and restoring prior tick/swap values. Platform achievements and profile completion are emitted only after a committed case win is accepted by progression; they are never embedded in PlayState and never need reversal inside case Undo.

### 2.3 final-tick win
With `ticks_remaining=1`, a successful final pickup increments passenger_index to passenger_count, then tick becomes 0. WON is selected before BUDGET_FAILED. Save/progression records the win. This ordering is invariant across normal, fast and reduced-motion presentation.

### 2.4 K2 two-swap turn
For K=2, first adjacent SWAP commits a new state with swaps=1; exact feasibility may flag DEAD immediately. If alive, second adjacent SWAP commits swaps=0. Undo once restores the state after first swap with swaps=1; Undo twice restores turn start with swaps=2. ADVANCE after one swap is legal; unused bandwidth expires and resets to K after a nonterminal Advance.

### 2.5 active-case resume
`active_case` stores `case_id`, `content_manifest_version`, committed PlayState, and the Undo snapshot stack/action log needed for continued stepwise Undo. Load validates case identity, manifest compatibility and all state invariants before presenting play. If compatible, presentation is rebuilt from logical state; animations are not resumed mid-transition. Saves occur only at committed boundaries, never halfway through an animation.

### 2.6 repeated demo import
Demo import is keyed by explicit `demo_import_version` plus stable case IDs. Re-running the same import performs set union for completion, `min()` for valid best ticks, first-import-only settings merge unless full-game preference already exists, and deterministic progression recomputation. It cannot duplicate achievements, consume skips, unlock acts from demo-only flags or regress records.

## 3. Exact DEAD authority and fallback
Runtime DEAD is always an exact semantic verdict. There are only two permitted backends:
1. precomputed exact feasibility artifact keyed from canonical logical state; or
2. exact memoized search using the same Rules Core.

A heuristic may be used only as a search prune when it is one-sided safe; it may never directly declare DEAD. If runtime exact search exceeds the release performance budget for a shipped case, that case must receive precomputed support or be simplified/rejected. Presentation may temporarily keep controls input-locked during an already-resolving committed action, but may not expose an approximate alive/dead state.

Precompute lookup miss policy: fall back to exact runtime search. If both exact mechanisms fail unexpectedly because of corrupted/mismatched artifacts, fail safe by withholding the DEAD hard-stop and log the integrity problem for development builds; release packaging must treat missing/mismatched required certificate artifacts as build failure, not silently ship uncertain semantics.

## 4. Certificate artifact contract
Each shipped campaign case must have a certificate record containing at minimum:
- `certificate_schema_version`;
- `certificate_id`;
- `case_id`;
- `case_content_hash` over canonical normalized case definition;
- `rules_semantics_version`;
- `solver_version`;
- `content_manifest_version`;
- `solvable` boolean (must be true for canonical campaign cases);
- `minimum_ticks`;
- `minimum_effective_swaps_at_min_ticks` when computed;
- `viable_first_label_state_count` or canonical set/hash;
- required family-counterfactual booleans/results for the slot;
- optional exact reachable/feasibility artifact hash when precomputed DEAD data ships;
- generation timestamp/tool metadata as non-semantic audit fields.

The certificate is invalid if any of `case_content_hash`, `rules_semantics_version` or required artifact hashes mismatch runtime content. Runtime may still play a development case without a certificate in dev builds, but release build validation must reject it.

## 5. Rules and certificate version compatibility
`rules_semantics_version` changes only when logical state transitions/evaluation change. Presentation-only changes do not bump it.

Compatibility rule:
- same case hash + same rules semantics -> certificate may be reused even if solver implementation version changes, provided regression tests confirm equivalent outputs;
- changed case hash -> recertify;
- changed rules semantics -> recertify every affected case and invalidate exact-feasibility artifacts;
- solver-version-only change may improve tooling but cannot change certified truth without triggering review and regenerated certificates.

Historical player `best_ticks` remain raw records. Efficient Route is recomputed against the current valid certificate minimum and is never stored as sole truth.

## 6. Content manifest authority
`content_manifest_version` identifies the shipped set/order of canonical cases and references exact case/certificate hashes. A manifest contains at minimum:
- manifest version;
- ordered base-campaign case IDs by act;
- demo-path case IDs;
- case content hash + certificate ID/hash per case;
- current rules semantics version;
- schema minimums required to load the package.

Progression recomputation uses the current manifest plus stable completion IDs. Unknown completion IDs from older/removed content are preserved in an `orphaned_progress` compatibility area or ignored for current unlock calculation, never reassigned to another case.

## 7. Save-schema migration authority
Profile saves are migrated by explicit monotonic schema functions `vN -> vN+1`; skipping versions is implemented by chaining known migrations. A migration must be deterministic, idempotent at its target version and covered by fixture tests.

Rules:
- never reinterpret one stable case ID as a different case;
- preserve completed IDs and valid best ticks whenever the case still exists;
- recompute act unlock/frontier/skip-derived state from canonical source fields when possible rather than trusting stale cached booleans;
- keep at most one `skipped_open_case_id` per act and validate it belongs to that act;
- malformed optional fields fall back to safe defaults; malformed core progression first tries previous-good backup;
- an incompatible active-case state is discarded/restarted with a one-time notice while profile progress survives;
- settings migrations preserve accessibility intent, not obsolete physical-device IDs.

## 8. Release validation gates for Phase 8
Before an implementation build can claim the technical spec:
- every case passes schema/invariant validation;
- every canonical campaign case has matching certificate/hash;
- Phase-4 M1–M12 and correction R1–R8 are automated regression tests;
- tests cover SWAP-DEAD-Undo, Advance-win-Undo, final-tick win, K2 partial/full Undo, repeated demo import, corrupted active-case fallback and save migration fixtures;
- solver/gameplay semantic equivalence is tested on representative randomized bounded states;
- release packaging fails on missing/mismatched mandatory content/certificate artifacts;
- no Steam/platform call is needed to advance local gameplay/progression;
- controller-only and 1280x800 technical acceptance remain mandatory.

## 9. Phase-8 acceptance
- [x] complete canonical schema example exists;
- [x] state/action mapping is implementable without inference;
- [x] DEAD backend/fallback is exact and bounded;
- [x] Undo across swap/advance/terminal/K2 is exact;
- [x] active-case resume boundary is exact;
- [x] demo import is idempotent and monotonic;
- [x] certificate artifact fields/hashes frozen;
- [x] rules/certificate compatibility frozen;
- [x] content manifest authority frozen;
- [x] save migration authority frozen;
- [x] release build validation gates frozen.

**PHASE 8 COMPLETE. DESIGN COMPLETE = NO.**

Next authority: `GAME10_PHASE9_SIMULATION.md`.