# GAME #010 — PHASE 4 MECHANICAL CORRECTION

Date: 2026-08-31
Status: **AUTHORITATIVE CORRECTION / PHASE 4 REGRESSION REPAIRED**
Game: Luggage Carousel Zero *(working title)*

Authority: this file overrides conflicting swap-legality, solver-branching, staging, duplicate-label-position and K=2 statements in `GAME10_THESIS.md`, `GAME10_MECHANICS.md` and `GAME10_CONTENT.md`. All non-conflicting rules remain unchanged. Before Phase 11, this correction must be folded into the final consolidated specification.

## 1. Defect discovered during Phase 5 campaign mapping
The original rule allowed `SWAP(a,b)` between **any two sockets**. Passenger LABEL clauses are evaluated only at the single pickup socket S0, labels do not move on ADVANCE, and labels have no history effect on bags.

Therefore unrestricted swaps collapse the intended label-position game.

### Formal collapse
For any state with K>=1 before ADVANCE:
- only `L[S0]` can affect the next passenger predicate;
- if a desired label value exists anywhere on the ring, one unrestricted transposition can place it at S0;
- the ordering of label values in S1..S(N-1) affects no bag movement, predicate, pickup, gap or passenger state;
- the non-pickup label multiset is merely storage and is invariant except for which value is exchanged with S0.

Thus states differing only by permutation of S1..S(N-1) are behaviorally equivalent. The advertised `label phase` is mostly fictitious.

Consequences under the old rule:
1. **F6 Label staging** is not a robust content family: there is usually no reason to prepare a label away from pickup because any needed value can be brought to S0 next tick in one action.
2. **F8 Duplicate-label flexibility** loses positional meaning: duplicate locations outside S0 are equivalent storage.
3. **F9 K=2 bandwidth** does not enlarge the set of pickup label values achievable on a tick; a second arbitrary transposition is generally future-storage bookkeeping, not a new causal lever.
4. Several Round-C claims about spatial label phase were therefore overstated.

This is a design-level defect, not a content-authoring problem. Filling 42 slots without repairing it would create fake diversity.

## 2. Canonical repair — swaps are LOCAL ADJACENT transpositions
The player verb remains **SWAP two socket labels**, but legality is now spatially local.

`SWAP(a,b)` is legal iff all are true:
- state is PLAYING;
- `swaps_remaining_this_tick > 0`;
- `a != b`;
- sockets are adjacent on the ring: `b = (a+1) mod N` or `b = (a-1+N) mod N`;
- both sockets pass any tutorial-only `swappable_socket_mask`.

Resolution remains atomic: exchange `L[a]` and `L[b]`, decrement swaps remaining by 1, recompute one-step preview and exact feasibility cache.

Equal-value adjacent swaps remain legal user no-ops but are warned against and omitted by the solver.

**Labels still do not move on ADVANCE. Bags still move one socket clockwise. Exactly one pickup remains. No new verb, predicate, currency, pickup, bag trait or hidden rule is introduced.**

## 3. Why locality repairs the intended system
With local swaps, label position becomes mechanically meaningful:
- K=1 can move a particular label at most one ring edge before the next ADVANCE;
- a label two or more edges from S0 cannot simply teleport to pickup;
- a non-pickup swap can stage a future label closer to S0 while preserving the current pickup label;
- moving one label toward S0 necessarily displaces neighboring values, creating future consequences;
- duplicate labels at different ring distances are not equivalent in time, even though token identity remains irrelevant;
- K=2 can move one label two edges in a tick or perform two distinct local repairs, which is genuinely stronger than K=1.

The product hook remains truthful: the player rearranges fixed gantry labels while luggage moves beneath them, but now the **spatial arrangement of all gantries matters**.

## 4. Corrected solver graph
Solver node remains:
`(O, L, passenger_index, ticks_remaining, swaps_remaining_this_tick)`.

Only legal adjacent non-no-op swaps generate edit edges.

Tick-boundary certification remains preferred: enumerate distinct label vectors reachable with 0..K legal adjacent swaps, then resolve one ADVANCE.

Simple upper bounds before duplicate-value collapse:
- K=1 on an N-socket ring: at most `1 + N` label vectors (do nothing plus one swap on each ring edge), versus the old unrestricted `1 + C(N,2)`.
- K=2: crude safe upper bound `1 + N + N^2`; exact distinct vectors are lower after inverse/repeated paths and duplicate values dedupe.
- At N=8 this crude K=2 bound is 73, far below the old unrestricted 351 two-transposition bound.

Existing conservative authoring envelopes remain valid:
- standard: N<=8, K=1;
- K=2 mastery: N<=6, ticks<=8 until Phase-8 benchmarks;
- K=0 teaching only.

The repair therefore **improves solver branching** while restoring actual positional depth.

## 5. Regression microcases
Pickup is S0; ring adjacency includes edge S(N-1)<->S0.

### R1 — old teleport is now illegal
N=5, `L=[R,B,G,Y,P]`, K=1. Passenger needs G on the next incoming matching bag. Old rule allowed S0<->S2 in one action. New rule forbids it because S2 is distance 2 from S0. The player must have staged G earlier through S1 or S3/S4.

### R2 — away-from-pickup staging is genuinely useful
N=5, `L=[R,B,G,Y,P]`, K=1. Current incoming bag satisfies P1 under R, so changing S0 would lose immediate service. P2, arriving next tick, needs G. G starts at S2. Before serving P1, swap adjacent S1<->S2: labels become `[R,G,B,Y,P]`; ADVANCE serves P1 under unchanged R. Next tick swap S0<->S1 -> `[G,R,B,Y,P]`; ADVANCE can serve P2 under G. Without the first away-from-pickup stage, G cannot reach S0 in one remaining swap.

### R3 — staging has displacement cost
Same ring. Staging G from S2 to S1 pushes B to S2. If P3 later needs B under tight timing, the stage that rescued P2 may damage P3. Thus label planning is a permutation problem rather than a free menu choice.

### R4 — duplicate positions matter without token identity
N=6, `L=[R,B,G,R,Y,P]`, K=1. Both R values are identical tokens semantically, but one sits at distance 1 from S0 through S5? Here R at S3 is distance 3 while R at S0 is already active. If current service requires preserving S0=B after a previous move and a future R must be restored, the nearer occurrence can matter by ring distance. Solver still stores values only, not R-token IDs.

### R5 — K=2 earns its slot
N=5, `L=[R,B,G,Y,P]`, K=2. To make G the pickup label this tick from S2, perform S1<->S2 -> `[R,G,B,Y,P]`, then S0<->S1 -> `[G,R,B,Y,P]`. K=1 cannot achieve G at S0 in this tick. Therefore K=2 now changes reachable pickup outcomes rather than merely rearranging storage.

### R6 — corrected Undo example
N=4, K=1, `L=[R,B,G,Y]`. Legal SWAP S0<->S1 -> `[B,R,G,Y]`, swaps remaining 0. Undo restores `[R,B,G,Y]` and swaps remaining 1. The old M10 example S0<->S2 is superseded because it is no longer legal.

### R7 — ring-edge adjacency is explicit
N=4, `L=[R,B,G,Y]`. S3<->S0 is legal because the carousel is a ring; `[Y,B,G,R]` is reachable in one swap. UI must visually show adjacency across the seam so this never feels like teleportation.

### R8 — pickup-only policy is now defeatable
Construct any two-passenger case where current P1 must retain L0=R this tick and P2 next tick needs G currently at S2. The only winning line performs S1<->S2 before serving P1, then S0<->S1 next tick. A policy that swaps only edges incident to S0 cannot win. This is now an exact measurable F6 condition.

## 6. Revised content-family proof metrics
The following Phase-5 tags are valid only under local adjacency:

### `STAGING_SIGNIFICANT`
True iff at least one winning solution requires an effective swap on an edge **not incident to S0**, and forbidding all non-pickup-adjacent swaps makes the case unsolvable within budget.

### `DUPLICATE_POSITION_SIGNIFICANT`
True iff repeated label values exist and collapsing their ring positions to a non-spatial multiset/free-choice model changes solvability, minimum ticks, or winning service family.

### `K2_SIGNIFICANT`
True iff the case is solvable with K=2 but unsolvable under the identical state/budget with K=1, or K=2 is required to preserve the intended certified family under the same tick limit. Merely shortening an already-trivial line does not earn F9.

### `LOCAL_DISPLACEMENT_SIGNIFICANT`
Optional analysis metric: a required stage moves a neighboring label away from a useful position and that displacement affects a later service decision. This may support F6/F10 evidence but is not a new family.

## 7. UX implication carried to Phase 6
Locality must be visually obvious:
- selectable swap targets are only the two neighboring gantries;
- focus navigation follows ring edges;
- the S(N-1)<->S0 seam must be visually continuous;
- preview after a local swap shows resulting label layout and next bag movement, not multi-tick advice;
- no drag gesture may imply arbitrary long-distance swapping.

## 8. Regression verdict
The defect is repaired without broadening the thesis: one existing verb gained the spatial constraint required for the already-promised phase-planning identity.

Phase-4 acceptance is restored subject to this amendment. Phase 5 must discard any candidate map/demo case that depended on unrestricted swaps and continue under **adjacent-only swap canon**.

**PHASE 4 COMPLETE AGAIN. DESIGN COMPLETE = NO.**
