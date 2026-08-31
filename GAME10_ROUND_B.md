# GAME #010 — CONCEPT TOURNAMENT ROUND B

Date: 2026-08-31
Status: COMPLETE — 5 -> 3
Final concept selected: NO

Authority: `START_HERE.md` -> `STATUS.md` -> `GAME_INDEX.md` -> `GAME10_RESEARCH.md` -> `GAME10_TOURNAMENT.md` -> this file.

Round B uses only vocabulary already admitted in Round A. No candidate receives rescue mechanics.

## B1 — Stencil Orchard — ADVANCES

### Minimal deterministic state
Board W×H, each cell has age 0..2. A case defines target predicates, remaining Steps, and reusable stencil shapes with legal rotations. A stencil placement produces a COVERED bitset. One Step resolves: (1) validate placement; (2) preview covered/exposed cells; (3) Commit; (4) every exposed age increments by 1, capped at 2; covered cells hold; (5) decrement Steps; (6) evaluate target predicates. No hidden randomness, autonomous growth, species, death, or reset is admitted.

### Three-situation onboarding
1. `[0,1,0] -> [1,1,1]`: cover the middle cell; teaches COVER = HOLD.
2. `[1,0,0]`, two Steps, target `[1,2,2]`: same correct cell must remain covered twice; teaches temporal protection.
3. 2×3 with an L stencil and two target windows: rotation that protects one mature corner also exposes two young cells; teaches one placement can satisfy competing phase requirements.

### Expert microcase
Board ages:
`1 0 1 / 0 1 0 / 1 0 1`, two Steps, target corners=1, edges=2, center=2. Available stencil is a five-cell plus shape. Step 1 cover four corners plus center is impossible with plus; instead cover the four corners by a hollow-corner stencil already in inventory while center/edges advance => corners1, edges1, center2. Step 2 cover corners+center; edges advance to2. The reasoning is schedule/phase protection across disconnected regions, not larger arithmetic. A case is valid only if its inventory actually contains the stated masks; content validator rejects mismatched prose/data.

### Solver/certification
State key = packed ages + remaining Steps; stencil inventory is case-static. Branches = legal anchor×rotation placements. Core bounds target 3×3–6×6, <=3 stencil shapes, <=4 rotations, <=8 Steps. Duplicate placements producing identical cover bitsets are canonicalized. BFS/A* can certify solvability, shortest solution and number of first-step alternatives. Generated cases are admitted only after exact certification and reasoning-skeleton dedupe.

### Demo / hour 8
10–20 min demo can teach hold, repeated protection, rotation, disconnected targets, then one multi-window case. Hour-8 depth comes from mask geometry × phase schedules × target-window interaction, not new cell types. Risk remains repetition if targets become arbitrary age paintings; content must use recognizable regions/windows and solver-derived counterfactuals.

### UX attack
Excellent at 1280×800: board, stencil tray, Step counter, target strip. Controller snaps anchors and rotates. Failure can show which cells over/under-aged and which prior Step first made the target unreachable. Strongest compact candidate.

## B2 — Luggage Carousel Zero — ADVANCES

### Minimal deterministic state
N fixed sockets form a ring, one designated pickup socket. Each socket owns one visible label. Bags occupy sockets or are absent and have immutable visible traits. Passenger queue contains public predicates over bag traits + current socket label. Player action is SWAP LABELS between two sockets, bounded per tick; ADVANCE is explicit.

Exact ADVANCE ordering: (1) finish label swaps; (2) all bags move simultaneously one socket clockwise into the next fixed socket; (3) evaluate the bag now at pickup against front passenger predicate using the pickup socket's current label plus bag traits; (4) if match, remove bag and passenger; otherwise neither changes; (5) empty sockets remain empty and circulate as gaps; there is NO compression; (6) evaluate win/fail/remaining ticks. This removes Round-A ambiguity.

### Three-situation onboarding
1. Three bags, passenger wants RED label: swap RED onto the socket that will be pickup after movement.
2. Passenger wants RED + SQUARE: teaches label is socket-owned while shape is bag-owned.
3. Two passengers with different predicates and four bags: serving the first with the unique future label alignment can strand the second; teaches queue planning.

### Expert microcase
Six sockets, pickup S0, labels `[R,B,G,R,B,G]`, bags at S1..S5 with shapes `[square,round,square,round,triangle]`, two gaps including S0. Queue: P1 accepts R+round; P2 accepts B+square; P3 accepts G+triangle; four ticks, one label swap before each tick. A greedy R placement for the nearest round serves P1 but moves B away from the square's pickup phase. The winning line first swaps B onto the square's future pickup socket, deliberately lets P1 miss one pass, then uses the second R for P1 and preserves G for triangle. Same vocabulary creates temporal permutation planning and intentional delay.

### Solver/certification
State key = bag permutation including gaps + socket-label permutation + passenger index + ticks + swaps remaining this tick. Bounds: N<=8 core, <=6 bags, <=3 labels, <=5 passengers, <=8 ticks, <=2 swaps/tick. Symmetry reduction canonicalizes bags identical in all predicate-relevant traits. Exact BFS/IDA* is feasible for authored certification; generated cases require unique/low-branch opening and no long forced waiting.

### Demo / hour 8
Demo: label-only pickup -> trait+label -> gaps -> two-passenger dependency -> compact finale. Hour-8 source is permutation × gaps × predicate overlap × queue ordering, without hidden traits or real-time play. It naturally creates stories ('let this passenger wait so the blue square survives').

### UX attack
Carousel motion is the explanation. Preview ghosts next socket positions and highlights only the front passenger's public predicate. Controller selects two socket labels then swaps. 1280×800 remains readable at <=8 sockets. Failure log can say exactly which bag reached pickup, which clauses matched, and what was missing. Strong identity and low production risk.

## B3 — Photocopier Garden — ELIMINATED

### Minimal state / ordering tested
Age grid 0..2, source rectangle, empty destination rectangle, one-turn source freeze. COPY validates equal-size empty destination, freezes source for next generation, creates destination cells at source age+1 capped2, then global generation advances all non-frozen pre-existing cells; copied cells do not advance again on creation turn.

### Onboarding / expert attempt
The first three cases teach copy, freeze, then overlap of timing. An expert 4×4 case requiring a mature pair while preserving a young source can be solved by choosing the smallest rectangle containing the desired motif and sequencing copies around frozen cells. Across attempted variants, the main reasoning repeatedly becomes 'choose rectangle footprint that freezes exactly the cells that must not age while duplicating desired ages.' Larger boards add bookkeeping more than a new strategic relationship.

### Solver
Finite and easy to certify, but destination choice makes branch factor large while meaningful solution structure stays narrow. Restricting destinations repairs search but weakens the copy fantasy.

### Direct comparison: Stencil Orchard vs Photocopier Garden
Both manipulate a discrete age field by selectively preventing advancement. Photocopier adds duplication, but its strongest consequence is still source HOLD plus copied phase offset. Stencil Orchard exposes the temporal decision more cleanly, has fewer state exceptions, clearer controller preview, lower visual clutter, and stronger solver/content canonicalization. Photocopier's spatial multiplication is visually attractive but did not prove a distinct hour-8 reasoning structure without overlap/copy-size exceptions. **CUT.** Do not revive this Game #010 cycle as a reskin or 'advanced Stencil Orchard mechanic.'

## B4 — Inventory Eclipse — ADVANCES

### Minimal deterministic state
Pack is a bounded grid. Each item has fixed occupied footprint, allowed rotations, one activation cell, and fixed shadow offsets relative to orientation. Items may overlap shadows but occupied cells may not overlap. An item is ACTIVE iff its activation cell is not shadowed by any other item. Items never shadow themselves. Compact world is a linear/branching sequence of nodes; each transition has a public requirement: named item ACTIVE or INACTIVE. Repacking is allowed only at designated safe nodes; world transitions do not use free movement.

Ordering: (1) place/rotate item; (2) validate occupied-cell collision/bounds; (3) recompute all shadows simultaneously from geometry; (4) recompute ACTIVE states simultaneously; (5) update visible world affordances; (6) when player chooses a transition, evaluate its requirement; (7) on success move to node and apply only the node's explicitly listed deterministic item transform/unlock, then recompute.

### Three-situation onboarding
1. One slider shadows crowbar; move it to activate crowbar and open gate.
2. Gate requires magnet INACTIVE; teaches absence is a positive requirement.
3. Two consecutive nodes require rope ACTIVE then magnet INACTIVE, with one repack point before both; teaches capability schedule rather than per-door packing.

### Expert microcase
2×4 pack with Rope R, Magnet M, Lamp L and a 1×2 Shade whose orientation changes its two-cell shadow vector. Route nodes A->B->C: A requires R active; crossing A activates a world vine that makes B require L active; B requires M inactive simultaneously; C requires M active, with no repack between A/B but a repack at B/C. One arrangement must expose R+L while shadowing M for A/B; at B/C rotate Shade to uncover M while preserving L. Same four rules produce planning over future requirements. The world is therefore not decoration: requirements couple multiple inventory states across repack boundaries.

### Solver/certification
Pack arrangement states are finite canonical placements/orientations plus world node. Core bounds <=4×5, <=6 items, <=4 orientations/item, <=10 nodes. Precompute legal pack arrangements and their active-bit vectors, then solve world progression over `(node, arrangement, acquired transforms)`. This is much smaller than searching raw drag sequences. Certification can demand at least one node where ACTIVE and INACTIVE requirements coexist and at least one multi-node commitment between repack points, preventing pure packing levels.

### Demo / hour 8
Demo teaches active, inactive, passive world effect, then two-node commitment. Hour-8 depth comes from capability schedules, orientation-dependent shadows, repack-point scarcity and deterministic footprint transforms already declared by nodes. No loot rarity, weight, Tetris scoring, combat, free exploration or inventory capacity economy.

### UX attack
Strongest trailer/GIF candidate: move one object, shadow sweeps across tool, tool phases out, world mechanism changes. Split screen can keep compact node strip beside pack. Controller grid snap is safe. Main risk is two-surface cognitive load, but explicit ACTIVE/INACTIVE icons and node preview keep causality inspectable.

## B5 — Consensus Machine — ELIMINATED

### Minimal state / ordering tested
<=5 agents, <=6 binary public facts, fixed visibility edges, fixed public vote cards, majority/quorum and at most one veto role. Player toggles visibility edge; votes recompute simultaneously; Commit resolves veto then quorum/majority then machine action.

### Onboarding / expert attempt
Cases teach hide one fact to flip a vote, selective ignorance to avoid veto, then a five-agent case where the same WATER/TOXIN facts must produce OPEN while inspector does not see TOXIN. The expert reasoning is valid but representation becomes the problem: either every agent displays visible-fact icons and a vote card—effectively a truth table—or information is hidden behind focus states, making failure explanation worse. Keeping only 3–4 agents preserves elegance but sharply limits combinatorial texture; adding roles/fact memory would be rule soup forbidden by Round B.

### Solver
Excellent boolean solver feasibility, but that is not enough: the play surface itself increasingly resembles satisfiability bookkeeping. Controller edge editing is also less tactile than the other finalists.

**CUT.** Mechanically sound, product-experience risk too high. Do not rescue by adding voter classes, stale tokens, dialogue personalities or hidden facts in Game #010.

# ROUND B RESULT — EXACTLY THREE FINALISTS

1. **Stencil Orchard** — best pure compact puzzle system; safest implementation/content certification; remaining threat is long-tail repetition and abstract age-painting.
2. **Luggage Carousel Zero** — best moving permutation system; strongest temporal stories from tiny vocabulary; remaining threat is whether label/predicate planning stays readable at expert density.
3. **Inventory Eclipse** — best world-facing/trailer hook and strongest capability-state fantasy; remaining threat is scope/UX from coupling pack and world.

Eliminated in Round B: **Photocopier Garden** (reasoning overlap with Stencil Orchard; duplication failed to earn distinct long-tail depth) and **Consensus Machine** (truth-table/product-experience risk despite excellent formal depth).

## Round-C comparison board
| Finalist | Hook/GIF | same-vocabulary hour-8 depth | deterministic certification | failure explanation | content efficiency | implementation safety | product identity |
|---|---:|---:|---:|---:|---:|---:|---:|
| Stencil Orchard | 5 | 4 | 5 | 5 | 5 | 5 | 4 |
| Luggage Carousel Zero | 5 | 5 | 5 | 5 | 5 | 5 | 5 |
| Inventory Eclipse | 5 | 5 | 4 | 5 | 5 | 4 | 5 |

No winner is forced in Round B.

# NEXT ROUND PROTOCOL — ROUND C (3 -> 1)
For each finalist, build a compact product proof rather than adding mechanics:
1. simulate first 20 minutes, hour 2 and hour 8 with explicit decisions;
2. define 12 representative content-case skeletons and cluster them by reasoning type to expose repetition;
3. estimate authored-content burden for a credible premium product and demo;
4. run a dominant-strategy/adversarial pass against the frozen minimal vocabulary;
5. define one screenshot, one 10-second GIF and one storefront sentence; attack whether each is legible without explanation;
6. compare controller/1280×800 cognitive load and accessibility;
7. compare solver/validator implementation burden and prototype empirical gates;
8. select exactly one winner only if it clearly dominates as a product; otherwise run a bounded tiebreaker between the top two.

Round C must end by selecting Game #010 or documenting the exact bounded tiebreaker. No production implementation.