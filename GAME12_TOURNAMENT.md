# GAME #012 — CONCEPT TOURNAMENT

Date: 2026-09-01
Status: **PHASE 2 ROUND A COMPLETE — 6 survivors**
Authority: tournament evidence only; no final winner or frozen mechanics.

## Round A method
Each of the 12 Phase-1 survivors was forced through two tiny concrete cases using the same destructive criteria from `STATUS.md`: tutorial legibility, second-case reasoning novelty without mechanic proliferation, visual readability, deterministic validator/solver feasibility, brute-force risk, theme-independent structural identity, portfolio collision, 30+ case plausibility, trailer/demo legibility and controller/Steam Deck feasibility.

This pass intentionally kills concepts that sounded attractive in prose but failed once reduced to actual player decisions.

### Fresh market sanity check — 2026-09-01
Current Steam evidence strengthens the factory's caution around generic minimalist grids. `Metanoia` (2026-02-27, $4.99) advertises only two base mechanics across 24 levels; `Netoo` (2026-03-03) is a free minimalist magnet/rotator logic game; `Symetria` (2026-04-22, $2.99) offers 150 geometry-transformation levels; and `AfterMove` (2026-08-12, $8.99) already occupies a strong "one move causes many deterministic reactions" pitch. Therefore survival here requires a causal law that is obvious in motion and structurally unlike Sokoban, generic geometry, or simultaneous-reaction grid puzzles.

Sources checked this run:
- https://store.steampowered.com/app/4293060/Metanoia/
- https://store.steampowered.com/app/4017520/Netoo/
- https://store.steampowered.com/app/4498840/Symetria/
- https://store.steampowered.com/app/4614710/AfterMove/

---

# 1. Margin of Error — KILL

**Provisional law tested:** a chain of gauges derives each next reading from the previous accepted reading; the player may place one tolerance band that makes one otherwise-invalid reading accepted, changing the downstream baseline.

### Case A — one rescue
Readings: `10 -> 11 -> 13 -> 14`. Normal tolerance is ±1. Goal: make the last reading valid by granting one ±2 tolerance at exactly one link.
- placing it on `11 -> 13` accepts 13 and lets 14 remain valid;
- placing it elsewhere fails before the end.

Good tutorial: the causal chain is understandable.

### Case B — competing rescue points
Readings: `8 -> 10 -> 9 -> 12 -> 11`; one widened tolerance and one target final band.
The intended reasoning is to decide which temporary acceptance changes the later baseline enough to rescue another transition.

**Destructive finding:** once numbers replace the mechanical theme, the puzzle is nearly a worksheet over adjacent differences. More cases require different thresholds, branches or multiple bands, all of which increase arithmetic rather than a new visual causal pattern. Tiny solver state is excellent (`O(n)` one-band placements), but that is also the problem: human reasoning and brute enumeration converge immediately.

**Verdict:** kill. Strong deterministic core, weak experiential identity and weak 30+ case confidence.

---

# 2. Negative Space Clerk — SURVIVE

**Provisional law tested:** place a limited number of opaque stamps; only the connected components, holes and boundary contacts of the remaining unstamped region matter.

### Case A — create exactly two void regions
Board: a 5×5 open sheet with two inward notches. One 1×3 stamp may be placed horizontally or vertically. Goal: visible paper must have exactly two connected regions, neither touching both left and right edges.

The useful placement is not "cover the target"; it is to sever a narrow bridge. The before/after topology is readable in one glance.

### Case B — preserve one region while creating one hole
Board: 6×6 with a pre-existing C-shaped blocked area. Two 1×2 stamps. Goal: remaining paper stays globally connected **and** contains exactly one enclosed unstamped hole of size 1.

This asks the opposite reasoning from Case A: do not sever connectivity; instead complete a ring while preserving an escape route elsewhere.

**Assessment:**
- Same vocabulary generates at least connectivity, component-count, hole-count, edge-contact, bottleneck and area-band families.
- Exact validation is trivial via flood fill / component analysis.
- Search ceiling can stay compact: e.g. 36 cells × 2 orientations × choose 2 placements is comfortably enumerable for offline certification.
- Human brute force risk is controlled if late boards offer many legal placements but objectives depend on multiple topological predicates.
- Trailer read is excellent: one stamp lands and a previously continuous negative-space silhouette splits or encloses.
- Risk remains portfolio/theme collision with False Map Department / Binder's Imposition if presented as paperwork or sheets. If advanced, retheme away from documents and avoid fold/trim semantics.

**Verdict:** survive, but identity must be explicitly topology-of-absence rather than office/paper fiction.

---

# 3. Wrong-Side Assembly — SURVIVE

**Provisional law tested:** rooted assembly tree; every component has front/back state. The player chooses which joints are made from the back. A back-made joint flips the orientation of the entire descendant subtree relative to its parent; direct component rotation is impossible.

### Case A — one downstream flip
Tree: root A with children B and C; B has child D. Initial all-front. One joint may be back-made. Goal: `D back`, `B back`, `C front`.
- flipping joint A-B flips B and D together;
- flipping B-D changes only D and fails.

The action and consequence are visually immediate.

### Case B — nested cancellation
Tree: A-B-D-E chain plus B-C branch. Two back-joints required. Goal: B back, C back, D front, E front.
A flip above B plus a nested flip above D creates cancellation on the deeper subtree. Reasoning is now about parity over ancestry, not simply "flip the wrong part".

**Assessment:**
- Exact solver is bit-parity on tree edges; exhaustive certification remains tiny for authored trees.
- Second case genuinely changes reasoning through nested parity/cancellation while keeping one verb.
- Visual identity survives theme removal: toggling an edge flips an entire colored/face-marked subtree.
- 30+ case families plausibly include single-branch flips, nested cancellation, shared-ancestor targets, constrained flip counts, forbidden joints, symmetric ambiguity and multi-goal face patterns.
- Main risk is mathematical collapse: if UI exposes all parity too plainly, advanced puzzles become XOR homework. Round B must test whether geometry/assembly shape creates human-readable but nontrivial deduction rather than pure linear algebra.

**Verdict:** strong survivor.

---

# 4. The Quiet Majority — SURVIVE

**Provisional law tested for tournament only:** devices sit on a fixed adjacency graph. Each active device votes its current ON/OFF state into every neighbor's next-state majority. A silenced device sends no vote but remains physically present and can still receive votes/state changes. Ties preserve current state. Player silences exactly N devices before a short deterministic resolution horizon.

### Case A — silence the loud center
Line of five states: `ON, ON, OFF, OFF, OFF`; neighborhoods are immediate left/right plus self for active voters. Silence one device before one update. Goal: center ends ON while both endpoints keep their initial states.

The instructive move is to silence a voter whose missing contribution changes a local majority without deleting the node itself.

### Case B — delayed cascade
Ring of six with alternating `ON/OFF` except one adjacent ON pair. Silence two devices, simulate two rounds, target exactly four ON devices at round 2.
A first-round tie can preserve a state that becomes the decisive vote in round 2, so selection is about delayed causal effect rather than immediate majority only.

**Assessment:**
- Deterministic synchronous update and exhaustive subset search are straightforward. Typical authored ceiling with 10 devices and choose-3 silence is only 120 intervention sets; 14 choose 4 is 1001, still trivial offline.
- That ceiling creates a player brute-force risk if reset/resolve is instantaneous. Any future version needs constraints that make causal prediction faster than blind testing (limited attempts is undesirable; better UI should expose vote neighborhoods and resolution trace).
- Structural identity is distinct from previous portfolio: intervention removes influence, not topology, properties, instructions or objects.
- Potential content families: immediate majority, tie preservation, delayed cascade, hub suppression, asymmetric neighborhoods, exact-count goals, protected unsilenceable nodes.
- Risk: can look like cellular automata spectacle or political-voting theme. Keep the fiction abstract/device-like and bounded; no endless simulation.

**Verdict:** survive to Round B specifically to test brute-force dominance and player explainability over 2–4 rounds.

---

# 5. Misprint Foundry — KILL

**Provisional law tested:** a finite derivation tree duplicates a shape. One chosen production node uses a mirrored plate; descendant orientation is inherited through alternating mirror relationships.

### Case A
Binary tree depth 2. Place one mirrored plate so exactly the two leaves under branch L are mirrored and R leaves are normal.

### Case B
Depth-3 uneven tree with one already-mirrored ancestor. Choose one defective node so selected grandchild returns to normal via mirror cancellation while its sibling remains mirrored.

**Destructive finding:** when stripped of factory art, this is the same underlying parity-on-tree reasoning as Wrong-Side Assembly, but with less direct player agency and weaker visual manipulation. Keeping both would waste tournament diversity.

**Verdict:** kill as inferior structural sibling of Wrong-Side Assembly.

---

# 6. Debt of Distance — KILL

**Provisional law tested:** tokens act in fixed order. Each receives a base movement allowance plus any unspent distance inherited from the previous token. Player chooses how much each spends.

### Case A
Allowances `[3,3,3]`; targets require moves `[1,5,3]`. Underspend token 1 by 2 so token 2 can spend 5.

### Case B
Four tokens with obstacles make spending extra distance sometimes harmful; player must carry 2 units across one token without consuming them, then spend later.

**Destructive finding:** useful choices reduce to budgeting a conserved scalar across a sequence. Obstacles can disguise it, but the structural heart is still resource redistribution, too adjacent to Tension Budget's portfolio identity. Adding positional movement creates a generic movement puzzle around the same conserved pool.

**Verdict:** kill for portfolio collision and abstraction risk.

---

# 7. Witness Protection — KILL

**Provisional law tested:** fixed cameras cover known sectors. Covering a camera removes all of its witness contributions. Targets demand exact witness counts.

### Case A
Three cameras cover targets with desired counts `[1,0,2]`; cover exactly one lens.

### Case B
Five cameras overlap four targets; cover two lenses so one target loses two witnesses while another must retain exactly one.

**Destructive finding:** mechanically this is a binary incidence-matrix / exact set-cover puzzle. Case 2 is larger, not qualitatively different. Visibility graphics improve presentation but not the reasoning law, and sector geometry can tempt unnecessary optics/line-of-sight complexity. Offline solving is easy, but player brute force is also easy when the number of cameras is small.

**Verdict:** kill. Familiar exact-cover structure without a convincing second-order interaction.

---

# 8. One Bad Ruler — SURVIVE

**Provisional law tested:** cuts are sequential; every next measurement starts from the previous cut. Exactly one measurement must use a ruler with one known missing tick, causing that requested length to snap to the next available tick and shifting every downstream absolute cut position.

### Case A — obvious propagated defect
Desired operations request lengths `[2,3,2]`. Bad ruler lacks tick `3`, so a requested 3 snaps to 4. Final silhouette target requires absolute cuts at `2,6,8`. Choosing the bad ruler on operation 2 uniquely creates those cuts.

### Case B — use the error to cancel a later mismatch
Requested lengths `[3,2,3,1]`; part includes two marked features judged by absolute cut positions. Bad ruler lacks tick 2 (snaps to 3). The player chooses one operation to mismeasure; an early +1 shift makes a later notch align while a late use does not.

**Assessment:**
- Clear physical causal story: one wrong measurement shifts everything after it.
- Solver ceiling is tiny (`n` candidate operations), so levels cannot rely on "which step?" alone for 30+ cases.
- To survive Round B it must prove a richer but still single-vocabulary architecture: multiple rulers with distinct missing ticks, exactly-one bad-use constraints, paired silhouettes/landmarks, or optional measurement origins may add depth—but mechanic proliferation is a danger.
- It is more visually embodied than Margin of Error and has a stronger clip: choose ruler -> cut snaps -> all downstream marks shift.

**Verdict:** survive cautiously. Round B must either prove 30+ cases without turning into arithmetic or kill it.

---

# 9. Ink Bleed — SURVIVE

**Provisional law tested:** each placed drop expands deterministically through cardinal fiber cells until blocked by walls or cells already wetted by earlier drops. A drop claims all reachable dry cells in its allowed fiber network; claimed cells become barriers for later colors. Player chooses drop positions/order from a small fixed palette.

### Case A — first color becomes a dam
A 5×5 fiber map has two chambers joined by a two-cell neck. Place red then blue. Goal: red owns left chamber; blue owns right chamber plus exactly one neck cell. Red must be placed so its spread closes one approach before blue resolves.

### Case B — deliberate containment by prior wetness
A branching 6×6 map. Three drops, fixed colors but player chooses order. Goal requires green to occupy two disconnected pockets. The only way is for earlier colors to wet connecting corridors, splitting the dry region before green spreads.

**Assessment:**
- Second case creates a genuinely different pattern: previous fill is not merely territory competition but dynamically constructs barriers for future flood fill.
- Validation is deterministic flood fill; action search stays compact for authored legal source points/order permutations.
- Visual trailer legibility is excellent: first ink floods, then visibly stops/rechannels the next color.
- 30+ case families plausibly include choke ownership, containment, deliberate disconnection, exact-area bands, protected cells, order-only cases, source-position cases and multi-color barrier chains.
- Main risk is generic "Flood-It" resemblance. Identity must be **history-dependent wet cells become future impermeable barriers**, not recoloring/area capture.

**Verdict:** strong survivor.

---

# 10. Public Secret — KILL

**Provisional law tested:** each character holds facts. Each round they transmit one fact to adjacent characters using a deterministic public priority. Player may redact a limited number of initial facts.

### Case A
Three people in a line; redact one initial fact so after two rounds the center knows A+B while endpoints each know exactly one fact.

### Case B
Five-person branch graph; a lower-priority fact can propagate only if a higher-priority fact is redacted upstream, changing what several people say later.

**Destructive finding:** causal depth exists, but the board state becomes icon/text bookkeeping very quickly. To explain why a person transmitted fact C instead of B, UI needs priority lists, inventories and round traces; trailer readability collapses compared with the stronger survivors. Structurally it is deterministic information propagation over a graph, but presentation burden is disproportionate to the mechanical novelty.

**Verdict:** kill for state-communication cost and weak 10–30 second readability.

---

# 11. Spare Chair — SURVIVE

**Provisional law tested for tournament only:** people arrive in fixed order and choose their highest-ranked currently available chair. Player removes exactly N chairs before seating begins. Goals concern final neighbor/separation relations, not chair identities alone.

### Case A — removal causes a preference cascade
Four chairs `A B C D`, three people arrive P1/P2/P3.
- P1 preference: B>A>C>D
- P2: B>C>A>D
- P3: C>D>B>A
Remove exactly one chair. Goal: P1 adjacent to P3 but P2 not adjacent to P1.
Removing B forces P1->A, P2->C, P3->D, producing a different cascade than simply deleting a seat after everyone sits.

### Case B — save a worse seat for a later person
Five chairs and four people with overlapping rankings. Goal simultaneously requires two friends adjacent and two rivals separated by at least one empty/other seat. The winning chair removal works because an early person's second choice consumes a chair that would otherwise divert a later person.

**Assessment:**
- Same rules naturally create greedy-allocation cascades, sacrifice, protecting a seat, adjacency, separation and exact-neighbor goals.
- Deterministic solver is tiny: with 10 chairs and remove 2 there are 45 initial interventions; with 14 remove 3 there are 364. Again, brute-force risk is real and Round B must compare causal deduction versus blind retries.
- Visual state can be excellent if each person's first few preferences are represented as small chair symbols/portraits rather than text lists.
- Structurally distinct from Luggage Carousel Zero: no moving permutation/gantries/service predicates; it is intervention into a stable greedy allocation outcome.
- Potential danger: "preference list homework" if too many ranks are displayed.

**Verdict:** survive to Round B; require low-information visual preference grammar and proof that 30+ cases do not need huge lists.

---

# 12. Courtesy Gap — KILL

**Provisional law tested:** objects traverse a one-dimensional encounter schedule. In normal encounters fixed right-of-way preserves order; placing a limited temporary yield gap causes exactly one encounter to invert the pair's order, changing later encounters.

### Case A
Three movers A/B/C meet in known event order. Insert one gap so B yields to C, making later A encounter C instead of B.

### Case B
Four movers, two gaps. First inversion changes which pair even reaches the second encounter, so the second gap's target is endogenous rather than pre-scripted.

**Destructive finding:** Case B is genuinely richer, but the game's identity after theme removal is still pairwise permutation via selected inversions. This sits uncomfortably close to Luggage Carousel Zero's adjacent permutation territory even though time/event semantics differ. It also risks requiring a timeline/event visualization that is harder to parse than the action itself.

**Verdict:** kill for portfolio adjacency and presentation overhead.

---

# Round A survivor matrix

| Candidate | Hook | Case-2 novelty | Visual legibility | Solver | Brute-force risk | 30+ cases | Portfolio separation | Round A |
|---|---:|---:|---:|---:|---:|---:|---:|---|
| Margin of Error | 4 | 2 | 3 | 5 | 1 | 2 | 5 | **KILL** |
| Negative Space Clerk | 5 | 5 | 5 | 5 | 4 | 5 | 3 | **SURVIVE** |
| Wrong-Side Assembly | 5 | 5 | 5 | 5 | 4 | 5 | 5 | **SURVIVE** |
| The Quiet Majority | 5 | 5 | 4 | 5 | 3 | 5 | 5 | **SURVIVE** |
| Misprint Foundry | 4 | 4 | 5 | 5 | 4 | 4 | 2 | **KILL** |
| Debt of Distance | 4 | 3 | 4 | 5 | 3 | 3 | 1 | **KILL** |
| Witness Protection | 5 | 2 | 5 | 5 | 2 | 3 | 5 | **KILL** |
| One Bad Ruler | 5 | 4 | 5 | 5 | 2 | 3 | 5 | **SURVIVE (fragile)** |
| Ink Bleed | 5 | 5 | 5 | 5 | 4 | 5 | 5 | **SURVIVE** |
| Public Secret | 5 | 5 | 2 | 5 | 4 | 4 | 5 | **KILL** |
| Spare Chair | 5 | 5 | 4 | 5 | 3 | 5 | 5 | **SURVIVE** |
| Courtesy Gap | 5 | 5 | 3 | 5 | 4 | 4 | 2 | **KILL** |

## Survivors — Round B field (6)
1. **Negative Space Clerk** — strongest topology-of-absence candidate; must retheme and avoid paper/fold identity.
2. **Wrong-Side Assembly** — strongest exact causal/parity candidate; must prove it does not collapse into XOR homework.
3. **The Quiet Majority** — strong intervention/cascade identity; must defeat blind subset enumeration and preserve explainability.
4. **One Bad Ruler** — excellent physical hook but fragile depth; must prove a 30+ case grammar without arithmetic/mechanic creep.
5. **Ink Bleed** — strongest visual simulation candidate; must prove history-dependent barrier identity beyond generic flood fill.
6. **Spare Chair** — strong greedy-allocation cascade; must prove compact visual preferences and low brute-force dominance.

## Round A kills
- Margin of Error — arithmetic worksheet / enumeration collapse.
- Misprint Foundry — inferior structural sibling of Wrong-Side Assembly.
- Debt of Distance — conserved-resource portfolio collision.
- Witness Protection — exact-cover incidence matrix with insufficient second-order depth.
- Public Secret — state communication burden overwhelms trailer/UI clarity.
- Courtesy Gap — pairwise permutation adjacency to Luggage Carousel Zero.

# NEXT ROUND RECOMMENDATION
Round B should be **destructive depth proof, not another score table**. For each of the six survivors:
1. build a 3-case mini-arc: tutorial, inversion/aha, mastery;
2. define the minimum complete rule grammar needed for those cases;
3. enumerate/estimate the actual intervention search space for mastery;
4. identify the intended human deduction shortcut and compare it against blind retries;
5. name at least five distinct content families available without adding a new core verb;
6. run a collision/saturation check against closest known games and Games #001–#011;
7. reject any candidate that needs >3 new rule nouns after its tutorial to create depth;
8. target **2–3 finalists** for Round C.

Special kill gates:
- **One Bad Ruler:** kill if depth requires multiple unrelated ruler types, freeform arithmetic, or >2 layers of numeric annotation.
- **Quiet Majority:** kill if mastery is easier to brute-force than to reason causally or if >3 simulation rounds become unreadable.
- **Spare Chair:** kill if preference lists routinely exceed 3 visible choices/person.
- **Wrong-Side Assembly:** kill if mastery reduces to obvious parity equations with no meaningful spatial/assembly reading.
- **Negative Space Clerk:** kill if differentiation depends mainly on document/stamp theme or case variety becomes generic polyomino placement.
- **Ink Bleed:** kill if objectives can be solved as ordinary flood-fill/color territory without exploiting wet-history barriers.
