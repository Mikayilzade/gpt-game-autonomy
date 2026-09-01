# GAME #012 — PHASE 4 MECHANICAL ARCHITECTURE

Date: 2026-09-01
Status: **PHASE 4 COMPLETE**
Product: **OPENWORK** (provisional working title)
Authority: exact gameplay rules. Where older tournament examples differ, this file controls.

## 1. Board truth
A case is a finite rectangular orthogonal grid with integer coordinates `(x,y)`, origin upper-left, x increasing east and y increasing south.

Every in-rectangle cell has one immutable base kind:
- `OPEN`: may remain void or receive a player piece;
- `FIXED_SOLID`: permanently occupied and never part of evaluated void.

The infinite area outside the rectangle is `EXTERIOR`. Exterior is not a playable cell and never contributes area. For enclosure testing only, an OPEN cell on a rectangle edge is cardinally adjacent to EXTERIOR across that edge.

After placements, an OPEN base cell is either:
- `REMAINING_OPEN`, if unoccupied by a player piece; or
- `PLACED_SOLID`, if occupied by a piece.

Only REMAINING_OPEN cells are evaluated by topology predicates. FIXED_SOLID and PLACED_SOLID are both impermeable separators, but their provenance remains distinct for rendering, undo and certificates.

Connectivity is cardinal/4-neighbour only. Diagonals never connect cells and never seal a diagonal leak.

## 2. Markers
A marker is immutable metadata attached to exactly one OPEN base cell. Marker IDs are unique within a case.

A marker cell is **protected from placement**: no player piece may occupy it. Therefore every marker always belongs to exactly one remaining-open component after any legal complete placement.

Markers have no collision, movement, weight or simulation effect. They exist solely for predicates and visual reference.

## 3. Piece instances and shapes
A case supplies 1–4 required piece instances. Every instance must be placed exactly once to submit a complete solution.

Frozen launch vocabulary:
- monomino `1x1`;
- domino `1x2`;
- straight triomino `1x3`.

Bars may be authored as either:
- `FIXED_H`;
- `FIXED_V`; or
- `ROTATABLE`, allowing H/V.

Rotation is discrete 90-degree orientation choice; no reflection concept exists because all frozen shapes are straight bars. A case may mix orientation policies across instances.

No L/T/polyomino catalogue is part of the frozen core. Adding a new shape is a post-freeze design change, not ordinary content authoring.

## 4. Placement legality
A piece placement is `(piece_instance_id, anchor_cell, orientation)`. Anchor is the topmost/leftmost occupied cell. The shape footprint is deterministic from anchor + orientation.

A placement is legal iff every footprint cell:
1. lies inside the board rectangle;
2. has base kind OPEN;
3. contains no marker;
4. is not occupied by another placed piece;
5. uses an orientation allowed by that instance.

Pieces may touch each other or fixed solids cardinally/diagonally. There is no gravity, support, adjacency bonus or placement-order effect.

Placement order has **zero semantic effect**. The evaluated state is the final set of occupied cells plus instance/orientation metadata. Undo order is UX history only.

## 5. Partial states, submit, undo/reset
The board may be evaluated visually after any placement for feedback, but a partial state can never win. Objective badges may show the truth of predicates against the current partial void, clearly labelled as live/current rather than final success.

A complete state has every required instance placed. It wins immediately when all target predicates evaluate true. A complete legal state that does not satisfy all predicates is simply unsolved, not a destructive fail state; player may undo/reposition.

Illegal placements are rejected before mutation.

`UNDO` removes the most recent placement action. Repositioning is represented as remove + place in history. `RESET` removes every player placement. Neither changes immutable case data.

## 6. Deterministic evaluation order
For any legal state:
1. build `R`, the set of REMAINING_OPEN cells;
2. compute 4-connected components of R;
3. assign deterministic component IDs by sorting each component's minimum `(y,x)` cell lexicographically and numbering from 0;
4. for each component compute area, marker set and touched board boundaries;
5. compute enclosed holes using exterior flood semantics below;
6. compute hole areas and deterministic hole IDs;
7. evaluate every objective predicate independently against this derived topology;
8. complete state wins iff logical AND of all predicates is true.

No objective changes simulation/evaluation of another objective.

## 7. Components
A remaining-open component is a maximal cardinally connected subset of R.

Component area = number of cells in it.

Boundary-contact set is a subset of `{N,E,S,W}`:
- N if component contains y=0;
- S if y=height-1;
- W if x=0;
- E if x=width-1.

A component may touch any number of boundaries including all four.

Marker `A` and marker `B` are `SAME` iff their cells have the same component ID; `DIFFERENT` otherwise.

## 8. Enclosed holes
Hole semantics deliberately distinguish an enclosed void pocket from the ordinary remaining-open regions being played on.

Construct the complement-within-rectangle `S = FIXED_SOLID ∪ PLACED_SOLID`. To classify open regions, flood from EXTERIOR into every REMAINING_OPEN edge cell, then through cardinal REMAINING_OPEN adjacency. Any remaining-open cell reached by this exterior flood is exterior-connected. Any remaining-open component not reached is an **enclosed hole**.

Therefore, under the frozen board model, holes are a subset of remaining-open components: specifically components with an empty boundary-contact set. This avoids contradictory dual definitions.

Hole area = component area. Hole count = number of remaining-open components with no boundary contact.

A diagonal corner gap does not connect a pocket to exterior.

This formalization means a target may simultaneously say `components = 3` and `holes = 1`; the hole is one of those three components.

## 9. Predicate grammar
Shipping authored cases may use only the following atomic predicate families.

### Global counts
- `COMPONENT_COUNT == n`
- `HOLE_COUNT == n`

### Component-area multiset
- `COMPONENT_AREAS == [a1,...,ak]` where list is sorted ascending; or
- `ALL_COMPONENT_AREAS_IN [lo,hi]`

### Hole-area multiset
- `HOLE_AREAS == [a1,...,ah]` sorted ascending; or
- `ALL_HOLE_AREAS_IN [lo,hi]`

### Marker relations
- `SAME(markerA, markerB)`
- `DIFFERENT(markerA, markerB)`

### Marker-component boundary relation
- `MARKER_COMPONENT_TOUCHES(marker, boundary_set, mode)` where mode is `EXACT`, `INCLUDES`, or `AVOIDS`.

### Global boundary-signature multiset
- `COMPONENT_BOUNDARY_SIGNATURES == [set1,...,setk]`, canonicalized by boundary bitmask N=1,E=2,S=4,W=8 and sorted numerically.

No path length, perimeter, shape matching, diagonal connectivity, symmetry, arithmetic expression language, named component identity or hidden predicate is launch canon.

A case target is an unordered finite set of atomic predicates combined by logical AND only. No OR/NOT nesting. Negative intent is expressed by explicit predicates such as DIFFERENT/AVOIDS or exact counts.

Authoring ceiling: normally 2–5 atomic predicates; hard launch ceiling 6. Redundant predicates may be rejected by curation even if technically valid.

## 10. Win and solution identity
A solution is the complete final placement assignment satisfying all target predicates.

For gameplay, two solutions are equivalent when they occupy the same cells with the same orientation-class footprints after quotienting permutations of **interchangeable piece instances**.

Two instances are interchangeable iff they share identical shape and orientation policy and have no instance-specific rule (the frozen core has no such rule). Their IDs are ignored for solution counting.

Canonical solution representation:
1. convert each placed instance to `(shape, orientation, sorted footprint cells)`;
2. sort tuples lexicographically;
3. serialize the sorted tuple list.

Thus swapping two identical domino IDs does not create a second solution. Distinct shape/orientation footprints remain distinct even if total occupied-cell union coincidentally matched (normally impossible under non-overlap).

## 11. Offline certifier/search contract
The certifier is exhaustive, deterministic and not a runtime hint oracle.

For each case it must:
1. validate schema and frozen ceilings;
2. enumerate every legal placement for every instance/orientation;
3. canonicalize interchangeable instances so permutations are not re-enumerated/count-multiplied;
4. enumerate every non-overlapping complete assignment;
5. derive topology using exactly the gameplay evaluator;
6. evaluate the AND target;
7. collect canonical satisfying solutions;
8. report raw legal complete assignments, canonical assignment count and canonical solution count;
9. reject zero-solution cases;
10. by default reject >1-solution cases unless the case explicitly carries `allow_multiple=true` and a human design review approves it. Campaign default is unique solution.

Runtime rules core and offline certifier must share golden topology fixtures so hole/component semantics cannot drift.

### Deterministic acceptance payload
Every accepted authored case stores or generates a certificate containing at minimum:
- `case_id`;
- `rules_version`;
- canonical case-data hash;
- dimensions;
- counts of base OPEN/FIXED_SOLID/markers;
- piece-instance descriptors;
- predicate descriptors;
- `raw_complete_assignments`;
- `canonical_complete_assignments`;
- `canonical_solution_count`;
- canonical witness solution(s), at least one;
- derived topology tuple for each witness;
- certifier version/hash.

Any case-data or rules-version change invalidates its certificate.

## 12. Hard mechanical ceilings
To preserve handheld readability and cheap exact certification:
- board rectangle: normal <=9x9; hard launch ceiling **9x9**;
- required pieces: **1–4**;
- shapes: only 1x1, 1x2, 1x3 straight;
- markers: normal 0–5; hard ceiling **6**;
- predicates: normal 2–5; hard ceiling **6**;
- connectivity: cardinal only;
- no case-specific simulation rules.

A content case that cannot become good inside these ceilings is discarded rather than expanding the core.

## 13. Difficulty knobs
Preferred difficulty growth, roughly strongest first:
1. **predicate coupling** — locally correct move for one predicate harms another;
2. **false articulation / false ring candidates** — several visually plausible critical zones;
3. **marker partition coupling** — cuts constrained by routes that must survive;
4. **boundary signature coupling** — topology must split while preserving/denying exits;
5. **area exactness/bands** — distinguishes otherwise topologically similar cuts;
6. **piece-role ambiguity** — different shapes could apparently serve the same local job;
7. **orientation ambiguity** for a small number of rotatable bars;
8. modest board irregularity.

Weak knobs that must not carry late difficulty: simply making boards larger, adding more pieces, hiding information, slowing retries, adding many shapes or stacking six unrelated predicates.

## 14. Challenge-family proof under one vocabulary
The following families all use the exact frozen rules above. They are content patterns, not new mechanics.

### F1 — Articulation cut
5x5 irregular open field, one 1x1. Two markers. Target: COMPONENT_COUNT=2 + DIFFERENT(A,B) + HOLE_COUNT=0. The player closes a true articulation cell.

### F2 — Seal without severing exterior
6x6 near-ring, two fixed-orientation dominoes. Target: HOLE_COUNT=1, HOLE_AREAS=[1], while two exterior markers remain SAME. Correct pieces complete an enclosure without breaking their shared exterior component.

### F3 — Marker partition with false necks
7x6 irregular field, one domino + one monomino, four markers. Target: A/B SAME, C/D SAME, A/C DIFFERENT, COMPONENT_COUNT=2. Several one-cell necks exist; most violate the required partition.

### F4 — Boundary signature sculpting
7x7 field, two bars. Target component-boundary signatures exactly `[N|W, E|S]`, no holes. The useful deduction is about which exits each resulting void must retain, not merely number of regions.

### F5 — Area-balanced split
7x7 irregular field, one 1x3 + one 1x1. Target COMPONENT_AREAS=[18,24] (illustrative authored totals must match actual board) plus marker relation. Candidate cuts producing two components are numerous; exact area eliminates the obvious neck heuristic.

### F6 — Coupled hole + partition
7x7, H domino + V domino + monomino, markers A-D. Target one enclosed area-1 hole, three total components, A/C/D SAME, B DIFFERENT from A, and exact boundary signatures. This is the Round-C mastery pattern: different predicates constrain different spatial zones.

### F7 — Preserve-the-neck inversion
A board exposes an obvious articulation cell, but target requires one component and one hole with an area band. Occupying the neck immediately fails. Player must identify a less salient near-ring instead. This explicitly weaponizes learned articulation heuristics.

### F8 — Same topology, wrong sizes
Several placements yield identical component/hole counts and marker partition, but only one yields the required component-area multiset. The challenge is distinguishing topologically equivalent-looking outcomes by quantitative void allocation.

## 15. Anti-"find the neck" content gate
Phase 5 must reject a campaign that overuses articulation closure.

For the target campaign:
- no more than **25%** of cases may have their principal deduction be "occupy a single articulation cell";
- at least **50% of cases from the middle third onward** must couple >=2 predicate classes such that satisfying either class alone leaves >=2 plausible assignments or points to a wrong assignment;
- every act after onboarding must contain at least one case where occupying the visually strongest neck is wrong;
- at least four of F2–F8 must each support >=4 quality authored cases before the 30-case floor is accepted;
- blind-retry dominance is an empirical Phase-10 gate, but Phase 5 must already record canonical assignment counts and solution uniqueness for representative cases.

## 16. Mechanical acceptance / Phase-4 conclusion
The product thesis survives formalization without new nouns. The same small vocabulary supports at least eight materially different challenge patterns: cutting, enclosing, partitioning, boundary signatures, area allocation, coupled constraints, heuristic inversion and topologically similar decoys.

Important repair versus loose tournament language: **an enclosed hole is formally a remaining-open component with zero board-boundary contact**. Component counts therefore include holes. All future authored targets must respect this exact meaning; old witness numbers are evidence only and must be re-certified if reused.

No production implementation begins here.

**PHASE 4 = COMPLETE.**

Next: Phase 5 Content Architecture must turn these families into a 30-floor/36-target campaign, define case schema and authoring/certification pipeline, build a representative certified-case matrix, progression/act dependencies and repetition gates. Any reused Round-C witness must be checked against the frozen hole semantics rather than assumed valid.