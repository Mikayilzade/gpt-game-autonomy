# GAME #010 — PHASE 4 MECHANICAL ARCHITECTURE

Date: 2026-08-31
Status: **PHASE 4 ACTIVE — deterministic core locked**
Game: Luggage Carousel Zero *(working title)*

Authority: `START_HERE.md` -> `STATUS.md` -> `GAME_INDEX.md` -> Game #010 tournament history -> `GAME10_THESIS.md` -> this file.

This phase refines mechanics only. It may not broaden the product thesis.

## 1. Exact case state
A case contains immutable definition data and mutable play state.

### Definition
- `N`: ring socket count; design target 3–8, hard canonical ceiling 8.
- sockets `S0..S(N-1)` clockwise; exactly one `pickup_socket`, canonical display normally S0.
- label multiset: one label token per socket; values may repeat.
- bags: stable IDs, immutable `shape` and `mark` values.
- initial occupancy: exactly N slots, each containing one bag ID or GAP; every bag appears exactly once.
- ordered passengers, each with 1–3 legal equality clauses under thesis grammar.
- `tick_limit >= 1`.
- `swaps_per_tick ∈ {0,1,2}`; 1 is normal baseline.
- optional early-tutorial `swappable_socket_mask`; mastery content defaults all sockets swappable.

### Mutable state
- occupancy vector `O[0..N-1]` of bag IDs/GAPs;
- label vector `L[0..N-1]`;
- `passenger_index` = first unserved passenger;
- `ticks_remaining`;
- `swaps_remaining_this_tick` reset after each resolved Advance;
- undo history of committed player actions/state snapshots;
- terminal status: PLAYING / WON / BUDGET_FAILED / DEAD (DEAD remains inspectable/recoverable).

Invariant: ring positions never disappear. A pickup replaces a bag occupancy with GAP; there is no compression.

## 2. Label-swap action
`SWAP(a,b)` is legal iff:
- state is PLAYING or DEAD-inspectable after undo has returned to a live state;
- swaps_remaining_this_tick > 0;
- a != b;
- both sockets are allowed by tutorial swappable mask.

Resolution is atomic: exchange `L[a]` and `L[b]`, decrement swaps remaining by 1, recompute preview/dead-state cache. Swapping two equal-valued labels is mechanically legal but is a no-op state transition; UX should warn/avoid accidental spend, and content solver canonicalizes it away.

Labels do not move on ADVANCE. They are socket-owned.

## 3. Advance ordering — authoritative
On `ADVANCE`:
1. Capture pre-advance state for Undo.
2. Simultaneously rotate occupancy one socket clockwise: `O_after[(i+1) mod N] = O_before[i]` for every i. Labels remain unchanged.
3. Inspect occupancy at `pickup_socket`.
4. If GAP: no passenger evaluation succeeds; record GAP PASS.
5. If bag and passenger remains: evaluate the front passenger predicate against `(bag.shape, bag.mark, L[pickup_socket])`.
6. If every clause matches, remove the bag by replacing pickup occupancy with GAP and increment passenger_index exactly once. No second passenger can be served on the same tick.
7. If any clause misses, bag remains at pickup and passenger_index does not change.
8. Decrement ticks_remaining by exactly 1.
9. If passenger_index == passenger_count: set WON, regardless of unused ticks.
10. Else if ticks_remaining == 0: set BUDGET_FAILED.
11. Else reset swaps_remaining_this_tick to case `swaps_per_tick`, then exact-solver check current feasibility; if none, flag DEAD, otherwise PLAYING.

There are no chained pickups, movement reactions, compression, bag collisions or passenger impatience.

## 4. Predicate evaluation
For current front passenger P and candidate bag B at pickup:
- LABEL clause compares required value to `L[pickup_socket]`;
- BAG_SHAPE compares to `B.shape`;
- BAG_MARK compares to `B.mark`.

All clauses use equality and AND. Empty predicate is invalid content. Repeated dimensions are invalid content. Evaluation is order-independent; UI may display clauses in stable order LABEL -> SHAPE -> MARK.

Passengers never inspect future sockets, bag history, gap count or previous misses.

## 5. Tick semantics and waiting
ADVANCE is always allowed while nonterminal and ticks remain, including with unused swaps. This is the canonical WAIT: the player does not press a separate wait button. Intentional non-service emerges by advancing into a non-match or gap.

There is no cost besides consuming one tick. Unused swaps expire on Advance and reset; they never accumulate.

## 6. Preview contract
Preview is deterministic and limited to the **next Advance only**. It may show:
- ghost destination of every current bag/gap after one rotation;
- which occupancy will arrive at pickup;
- current pickup label (fixed);
- clause-by-clause result that would occur for the front passenger after that movement;
- whether that immediate pickup would consume the bag/passenger.

Preview must not show: solver-selected swap, multi-tick path, future passenger outcomes after a hypothetical pickup, global solvability, optimality or solution count. Dead-state feedback is a separate post-action feasibility signal.

## 7. Undo / restart semantics
Unlimited Undo within a case. Undo restores the exact prior committed state including labels, occupancy, passenger index, ticks and per-tick swaps. Both SWAP and ADVANCE are undoable atomic actions; a swap can therefore be individually reversed without rewinding a whole tick.

Restart restores exact initial state. No penalty, score loss or campaign resource.

After WON/BUDGET_FAILED/DEAD, Undo and Restart remain available. DEAD does not force a modal exit. A player may not Advance from BUDGET_FAILED or WON; DEAD may allow inspection but not forward play unless UX testing demonstrates value—mechanical baseline freezes forward actions in DEAD and offers Undo/Restart.

## 8. Exact solver state and legal search
Canonical solver node:
`(O, L, passenger_index, ticks_remaining, swaps_remaining_this_tick)`.

Edges are legal non-no-op SWAPs and ADVANCE. For feasibility/dead-state certification, search ends success at all passengers served; exhaustion at ticks=0 is failure.

Safe reductions:
- bags with identical `(shape,mark)` are interchangeable only if no other system references stable bag identity; canonical solver may normalize their IDs by occupancy order;
- equal label values are indistinguishable tokens; state key stores values by socket, not token IDs;
- equal-label swaps omitted;
- when swaps_remaining=0 only ADVANCE branches;
- a sequence of swaps before one Advance is canonicalized by resulting label vector: different swap sequences reaching identical `(L, swaps_remaining)` state dedupe naturally.

Do **not** quotient rotational symmetry because pickup S0 breaks ring symmetry.

## 9. Dead-state definition
A state is DEAD iff passenger queue remains, ticks_remaining > 0, and exhaustive legal search from the current solver state has no winning path under the case budget. DEAD is therefore exact, not heuristic.

For responsive UX, authored cases may ship a precomputed reachable-state table or use bounded cached search. Technical choice deferred to Phase 8; semantic result must match exact solver.

## 10. Win optimality and mastery metrics
Basic completion requires only WON. Solver may additionally certify:
- minimum ticks to win from initial state;
- minimum number of effective swaps among minimum-tick solutions;
- number of distinct viable first resulting label states;
- whether any solution requires an intentional non-match while a different immediately matching intervention existed;
- served-bag trait sequence;
- gap-at-pickup sequence;
- label-at-pickup sequence.

These are content/optional mastery metrics, not extra currencies. Phase 7 decides which are surfaced.

## 11. Content invariants / rejection rules
A canonical authored case is invalid if:
- >8 sockets;
- not exactly one pickup;
- passenger predicate violates grammar/3-clause ceiling;
- hidden/random trait exists;
- direct bag movement is required;
- total-swap currency exists;
- a solution depends on ambiguous simultaneous ordering;
- initial state is unsolvable within budget unless explicitly a tutorial counterexample not counted as campaign completion;
- success requires more than one pickup in a tick;
- label ownership is not visually representable as socket-fixed.

Strong-case certification later should reject trivial filler, long forced waiting and reasoning-trace duplicates even when solvable.

## 12. Mechanical architecture acceptance completed this increment
- [x] Exact state variables.
- [x] Atomic swap semantics.
- [x] Authoritative simultaneous movement/pickup ordering.
- [x] Predicate grammar execution.
- [x] Budget reset/wait semantics.
- [x] One-step preview boundary.
- [x] Unlimited exact Undo/Restart baseline.
- [x] Solver state and safe symmetry reductions.
- [x] Exact dead-state definition.
- [x] Core invariants and invalid-content rules.

## 13. Remaining Phase-4 work
Next increment must pressure-test the locked core with explicit state traces and finish mechanical architecture:
1. hand-simulate at least 10 microcases covering pickup, misses, gaps, duplicate labels, identical bags, 0/1/2 swaps-per-tick, undo and final-tick success;
2. derive hard feasibility bounds and identify any solver-state explosion at N=8;
3. freeze difficulty knobs and which combinations are allowed by campaign act;
4. define content quality metrics for intentional miss, gap significance, bag scarcity/substitutability and nontrivial label staging;
5. attack degenerate strategies: swap-at-pickup-only, rotate-and-wait, duplicate-label no-op, excessive dead-state oracle use, and Undo information leakage;
6. resolve whether DEAD should hard-stop forward Advance or merely warn, using puzzle-experimentation philosophy;
7. write Phase-4 acceptance checklist and close Phase 4 only if no ordering ambiguity remains.

**DESIGN COMPLETE = NO.**