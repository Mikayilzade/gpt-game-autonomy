# GAME #010 — PHASE 4 MECHANICAL ARCHITECTURE

Date: 2026-08-31
Status: **PHASE 4 COMPLETE — destructive proof passed**
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
- state is PLAYING;
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
ADVANCE is always allowed while PLAYING and ticks remain, including with unused swaps. This is the canonical WAIT: the player does not press a separate wait button. Intentional non-service emerges by advancing into a non-match or gap.

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

After WON/BUDGET_FAILED/DEAD, Undo and Restart remain available. A player may not Advance or Swap from WON, BUDGET_FAILED or DEAD. DEAD is an inspectable hard stop with Undo/Restart only; this is now final Phase-4 canon.

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

For certification/search, implementations should additionally use a **tick-boundary macro graph**: enumerate all distinct label vectors reachable with 0..K swaps before the next Advance, then resolve one Advance. Intermediate swap states remain necessary for Undo/UX but need not multiply the certification graph.

## 9. Dead-state definition
A state is DEAD iff passenger queue remains, ticks_remaining > 0, and exhaustive legal search from the current solver state has no winning path under the case budget. DEAD is exact, not heuristic.

DEAD is evaluated only after a committed SWAP or ADVANCE has settled. If exact feasibility is false, forward play hard-stops; Undo/Restart remain available. This avoids turning repeated dead warnings into an oracle-driven exploration mode while preserving consequence-free experimentation.

For responsive UX, authored cases may ship a precomputed reachable-state table or use cached exact search. Technical choice is deferred to Phase 8; semantic result must match exact solver.

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

## 12. Deterministic core acceptance
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

# 13. Destructive mechanical proof — 12 explicit microcases
Notation: pickup is S0; occupancy lists `[S0,S1,...]`; one Advance rotates right, so pre-tick S(N-1) arrives at S0. `-` means GAP. Only the front passenger is evaluated.

### M1 — basic successful pickup, no swap
N=3. `O=[A,B,C]`, `L=[R,B,G]`; C is square/stripe. Passenger wants `LABEL=R`. ADVANCE -> `[C,A,B]`; C arrives under fixed S0 label R, matches, is removed -> `[-,A,B]`. Passenger served. Confirms labels stay fixed while bags move.

### M2 — explicit miss leaves bag in ring
Same state, passenger wants `LABEL=B`. ADVANCE -> C reaches S0 under R, misses; resulting `O=[C,A,B]`, passenger unchanged. Confirms a miss does not remove, reorder or mark the bag.

### M3 — gap pass
N=4, `O=[A,B,C,-]`. ADVANCE -> `[-,A,B,C]`; pickup sees GAP; nobody is served. The gap remains at S0 and continues on the next tick. Confirms no compression.

### M4 — pickup creates circulating gap
N=4, `O=[A,B,C,D]`, D matches. ADVANCE -> `[D,A,B,C]` then remove D -> `[-,A,B,C]`. Next ADVANCE -> `[C,-,A,B]`; gap has moved from S0 to S1 while C now reaches pickup. Confirms removal changes future phase only through a persistent occupancy hole.

### M5 — one swap before tick stages pickup label
N=3, `O=[A,B,C]`, `L=[B,R,G]`, C round/dot; passenger wants `LABEL=R AND SHAPE=round`. `SWAP(S0,S1)` -> `L=[R,B,G]`; ADVANCE -> C reaches S0 under R and is consumed. Confirms edit acts on sockets, not bag identity.

### M6 — zero swaps per tick remains valid observation/wait content
N=3, K=0, `O=[A,B,C]`, `L=[R,B,G]`; passenger wants shape of B. Tick1 ADVANCE: C reaches pickup and misses. Tick2 ADVANCE: B reaches pickup and is consumed. This is valid only as short onboarding/forced-observation material; Phase-5 quality rules prohibit long K=0 filler.

### M7 — two swaps per tick can create a permutation not reachable with one swap
N=4, `L=[R,B,G,Y]`, K=2. `SWAP(S0,S1)` -> `[B,R,G,Y]`; `SWAP(S1,S2)` -> `[B,G,R,Y]`. Result is a 3-cycle of label values; no single transposition reaches it. ADVANCE then resolves normally. Confirms K=2 is a materially larger intervention bandwidth and needs tighter authoring bounds.

### M8 — duplicate labels are values, not token identities
N=4, `L=[R,R,B,G]`. Swapping S0/S1 is a legal user no-op but solver omits it because state remains `[R,R,B,G]`. Swapping S1/S2 yields `[R,B,R,G]`, distinct. No puzzle may depend on which physical R token moved.

### M9 — trait-identical bags are solver-symmetric
N=4, A and B are both square/dot, C round/dot, D triangle/stripe. No rule references bag IDs. States `[A,C,B,D]` and `[B,C,A,D]` are equivalent under canonical normalization. If one identical bag is served, the remaining state is normalized by trait-class occupancy, not narrative identity. Content prose may not distinguish A from B.

### M10 — Undo after swap restores bandwidth as well as labels
N=4, K=1, `L=[R,B,G,Y]`. SWAP S0/S2 -> `[G,B,R,Y]`, swaps remaining becomes 0. Undo restores `[R,B,G,Y]` **and** swaps remaining=1. A subsequent different swap is legal. Confirms no hidden action debt.

### M11 — Undo after successful pickup resurrects exact bag/passenger state
N=3, one passenger, `O=[A,B,C]`, C matches. ADVANCE produces win after removing C. Undo restores pre-advance `O=[A,B,C]`, passenger_index=0, ticks, label vector and pre-tick swap remainder exactly. Win has no irreversible side effect.

### M12 — final-tick success beats budget failure
Ticks remaining=1, passenger remains, incoming bag matches. ADVANCE rotates, pickup succeeds, passenger_index reaches passenger_count, then tick decrements to 0. Ordering rule 9 checks success before budget failure: terminal is WON, never BUDGET_FAILED. If the bag misses instead, terminal is BUDGET_FAILED.

**Trace result:** all required edge classes behave consistently; no ambiguous ordering was found.

# 14. Solver burden and safe authoring envelope
A naive Cartesian upper bound is unacceptable. At N=8 with six distinguishable bag trait classes + two identical gaps, occupancy permutations alone can reach `8!/2! = 20,160`. With four duplicated label values at multiplicity 2 each, label vectors can reach `8!/(2!^4) = 2,520`. Multiplying by passenger progress, ticks and within-tick swap remainder yields billions of theoretical nodes (e.g. >11 billion under a loose 6-passenger/10-tick envelope). Therefore Phase 4 explicitly rejects “plain unrestricted BFS is cheap” as a design assumption.

The practical certification graph uses tick-boundary macro actions. With eight **distinct** labels, K=1 has at most `1 + C(8,2) = 29` distinct 0/1-swap resulting label permutations before Advance. K=2 has at most 351 permutations within two transpositions (identity + 28 transpositions + 112 3-cycles + 210 disjoint double-transpositions) before duplicate-value collapse. This is why K=2 cannot be combined freely with maximum N/tick depth.

### Frozen authoring envelopes
**Envelope A — standard campaign (default):**
- N=3..8;
- K=1;
- bags <=7; at least one gap is recommended once gaps are taught, but initial all-bag states remain legal;
- distinct label values <=4;
- passenger count <=6;
- tick_limit <=10;
- exact certification mandatory.

**Envelope B — two-swap mastery:**
- K=2 only;
- N<=6;
- distinct label values <=4;
- passenger count <=5;
- tick_limit <=8;
- no case enters content pool until exact solver runtime/memory passes Phase-8 implementation budget.

**Envelope C — zero-swap teaching/observation:**
- K=0;
- N<=5;
- tick_limit<=4;
- never used as late mastery challenge.

N=7–8 + K=2 is **non-canonical/out of envelope** unless a later implementation benchmark proves it safe and Phase-11 explicitly amends the freeze. Content generation may explore it offline, but campaign data cannot rely on it.

### Required solver pruning/representation contracts
- tick-boundary macro graph for feasibility/certification;
- canonical trait-identical bag representation;
- duplicate label values represented directly, no token identity;
- memoization keyed by `(canonical O, L, passenger_index, ticks_remaining)` at tick boundaries;
- lower bound prune: if `remaining_passengers > ticks_remaining`, state is immediately infeasible because at most one passenger can be served per tick;
- any passenger for which no remaining bag trait class can satisfy its SHAPE/MARK clauses is immediately infeasible;
- solution traces deduped by effective label state before Advance, not raw swap ordering.

These are semantic authoring constraints; Phase 8 may choose BFS, IDA*, dynamic programming or backward tables as long as exact results agree.

# 15. Frozen difficulty knobs and campaign combinations
Difficulty may change only through existing state variables and relationship density.

1. **N / ring size** — more arrival phases and socket choices.
2. **Passenger count** — longer consumption dependency.
3. **Tick slack** = `tick_limit - minimum_ticks`; low slack makes intentional misses costly.
4. **K swaps/tick** — 0 teaching, 1 baseline, 2 selected mastery.
5. **Predicate width** — 1 to 3 clauses, never new operators.
6. **Bag substitutability** — how many remaining bags satisfy each passenger's immutable bag clauses.
7. **Passenger overlap** — how many passengers compete for the same bag trait classes.
8. **Label multiplicity** — duplicate vs scarce labels.
9. **Gap count / gap phase** — timing structure created initially or by prior service.
10. **Opening ambiguity** — number of viable first macro label states.

Act A: N3–5, K0/1, 1-clause then label+one trait, high tick slack, no designed dependency on gaps.
Act B: N4–6, K1, 1–2 clauses, first scarce/substitutable bag choices, moderate passenger overlap.
Act C: N4–7, K1, 2 clauses normally, intentional miss and consumption-order dependency required in strong cases.
Act D: N5–8, K1, gaps become causally significant; at least one case family requires removal-created phase change rather than merely showing gaps.
Act E: N5–8 K1 baseline; selected N<=6 K2 cases; up to 3 clauses; tighter slack, duplicate labels, stronger overlap. No Act E case may rely only on larger N or more clauses.

# 16. Strong-case measurable criteria
A case can be solvable yet weak. Content Architecture must classify and reject filler using these metrics.

### Intentional-miss significance
For a case tagged `INTENTIONAL_MISS`, at least one minimum-tick or designated canonical solution must contain a tick where the front passenger could have been served by some legal pre-Advance label state, but every solution that serves them on that tick fails the full case. A mere unavoidable miss does not qualify.

### Gap significance
For a case tagged `GAP_SIGNIFICANT`, altering the relevant gap into a predicate-irrelevant neutral bag, or counterfactually compressing the ring after the causal pickup, must change solvability/minimum ticks/required served-bag sequence. A gap that only adds visual spacing does not qualify.

### Scarcity / substitutability
For `SCARCE_BAG`, some passenger has exactly one remaining bag trait class satisfying its immutable clauses at the decision point and a competing earlier passenger can consume that class.
For `SUBSTITUTION`, at least one passenger has >=2 candidate bag trait classes, but choosing one candidate changes downstream feasibility or minimum ticks. Cosmetic duplicates do not count.

### Nontrivial label staging
A solution demonstrates `LABEL_STAGING` only if at least one effective swap changes a label on a socket other than S0 and the benefit is realized on a later tick; furthermore an alternative policy restricted to swaps involving S0 cannot achieve the same minimum-tick win. This directly rejects pickup-only label play.

### Opening quality
Early cases may have one obvious opening. Mid/late strong cases should normally have 2–6 superficially plausible macro openings but fewer solver-certified viable openings. Cases with dozens of equivalent openings or only long forced waiting are rejected.

# 17. Degenerate-strategy attacks

## Swap-at-pickup-only
Attack: because only S0 label is evaluated, perhaps every useful swap simply changes S0 immediately before pickup.
Repair/criterion: content must include LABEL_STAGING cases where a non-S0 swap is causally required for optimal/feasible play. Fixed labels at other sockets matter because staging determines which value can be brought to S0 in later ticks under limited K. Act C onward requires regular examples; otherwise the game collapses to “choose pickup color.”

## Rotate-and-wait
Attack: unlimited harmless rotation could solve by waiting until the right bag arrives.
Repair: finite ticks already price waiting. Strong-case validation rejects long forced-wait traces and requires meaningful intervention density. Campaign cases should not contain >2 consecutive Advances with zero effective swaps unless those passes create/consume a strategically meaningful gap or intentional miss.

## Duplicate-label no-op / token tracking
Attack: duplicate labels could invite meaningless swaps or perceived hidden token history.
Repair: no token identity exists; equal-value swap is visibly warned and omitted by solver. Content never distinguishes two same-value labels.

## Dead-state oracle
Attack: player could make arbitrary swaps and use immediate DEAD to binary-search the solution.
Decision: exact DEAD remains valuable, but **DEAD hard-stops forward play**. It is checked after a committed action and offers Undo/Restart, not repeated exploration deeper from an impossible state. It still leaks one bit of feasibility—intentionally, like a strong contradiction warning—but cannot reveal which alternative is correct. Optional accessibility/hint settings may later delay the warning, but canonical semantics stay exact.

## Undo information leakage
Attack: unlimited Undo + one-step Preview lets players test candidate swaps without cost.
Decision: accepted by design. This is a deterministic reasoning game, not an information economy. There is no hidden state to protect. Mastery comes from understanding causality; reversible experimentation is a feature. Scores/achievements, if any, may record an optional clean solve separately but cannot restrict Undo for basic completion.

# 18. Phase-4 final acceptance checklist
- [x] >=10 explicit traces; 12 completed including all mandated edge classes.
- [x] Simultaneous movement and pickup ordering unambiguous.
- [x] Gap creation/circulation unambiguous.
- [x] Duplicate labels and trait-identical bag symmetry defined.
- [x] K=0/1/2 behavior defined.
- [x] Undo exactness and final-tick success proven.
- [x] Naive N=8 state explosion quantified; unrestricted BFS assumption rejected.
- [x] Safe campaign authoring envelopes frozen.
- [x] Tick-boundary macro certification contract frozen.
- [x] Difficulty knobs and per-act combinations frozen.
- [x] Strong-case metrics for intentional miss, gap significance, scarcity/substitution and label staging frozen.
- [x] Pickup-only, rotate/wait, duplicate-label, dead-oracle and Undo attacks resolved.
- [x] DEAD forward-play decision finalized: hard stop + Undo/Restart.
- [x] No production implementation added.

**PHASE 4 COMPLETE. DESIGN COMPLETE = NO.**

Next authority: `GAME10_CONTENT.md` (Phase 5 Content Architecture).