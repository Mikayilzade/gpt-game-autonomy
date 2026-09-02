# GAME #014 — PHASE 2 CONCEPT TOURNAMENT

Date: 2026-09-02
Status: Round A complete; 6 semifinalists retained; no final winner selected.
Authority: `START_HERE.md` -> `STATUS.md` -> `GAME_INDEX.md` -> `GAME14_RESEARCH.md` -> this file.

## Round A purpose
Attack all 12 Phase-1 survivors at the level of exact toy rules rather than aesthetics. Every concept receives: minimal state/action/goal, one valid micro-instance, one hostile instance, deduction families, certifier/content/UX assessment, and a kill/retain judgment. The threshold is not merely solvability: the human route must contain deductions better than blind enumeration, the certifier must be deterministic, and the idea must support several hours without parameter inflation.

## A — Negative Casting — RETAIN
### Minimal model
Discrete 2D side-view board. Two fixed point-lights L1/L2 project axis-aligned opaque blockers onto two finite target strips W1/W2. Player places/rotates 2–4 blockers in discrete sockets. Each wall cell stores shadow bit pair `(s1,s2)`. Objectives use only derived negative-shadow classes: BOTH, L1_ONLY, L2_ONLY, LIT.

### Tiny valid instance
W1 has cells a,b,c. Required classes: `a=BOTH, b=L1_ONLY, c=LIT`. Two sockets each admit one of two blocker orientations. Socket P can affect L1 on {a,b} or {b}; socket Q can affect L2 on {a} or {a,c}. Since c must remain LIT, Q cannot use {a,c}; therefore Q->{a}. Then BOTH at a forces P to include a, selecting P->{a,b}; b becomes L1_ONLY exactly.

### Hostile instance
Four blockers each independently flip one wall interval and the target accepts many symmetric placements. If no clue couples projections, play collapses to rotation spam.

### Human deduction families
1. forbidden-light elimination from required LIT cells;
2. BOTH decomposition forcing one contribution from each light;
3. exclusive-shadow attribution (`L1_ONLY` forbids every L2-causing placement covering that cell);
4. cross-wall coupling: one blocker projection choice simultaneously constrains W1 and W2;
5. interval endpoint reasoning: required transition boundaries constrain blocker extent before identity;
6. support-count reasoning: a target cell with exactly one remaining producer forces that placement.

### Certifier / burden
Finite socket/orientation CSP; trivial deterministic exhaustive certifier. Human UI can preview static ray incidence per blocker but must not preview combined target correctness. Low bespoke asset burden; content authored as sockets, blocker projection masks, wall targets.

### Judgment
Retain. Unlike generic silhouette packing, the promising core is *multi-channel negative classification across multiple projection surfaces*. Round B must prove at least three campaign families that do not reduce to interval exact-cover.

---

## B — Museum of Wrong Labels — KILL
### Minimal model
N fixed exhibits each expose 2–3 observable behaviors. N movable law-name labels map one-to-one onto hidden rule definitions. Captions assert relations such as “the exhibit labelled X reacts before the exhibit labelled Y”. Player permutes labels until all captions are true.

### Tiny valid instance
Three exhibits E1/E2/E3. Observations leave E1 compatible with Heat or Magnetism, E2 with Magnetism or Pressure, E3 with Heat or Pressure. Caption: “Heat and Pressure are not adjacent in display order”; display order E1,E2,E3. This forces Magnetism=E2, then Heat/Pressure resolve by a second caption.

### Hostile instance
Each exhibit has a nearly unique behavior fingerprint; then the puzzle is ordinary one-to-one matching. Conversely if fingerprints are heavily ambiguous, captions become an arbitrary logic-grid clue system detached from the exhibits.

### Human deduction families
Compatibility elimination, bijection/last-label, relational clue chaining, contradiction. These are valid but mostly generic CSP operations; the physical exhibit layer does not create a new second-order reasoning grammar.

### Judgment
Kill. Strong theme, weak mechanical novelty. The best instances become a dressed permutation/logic-grid puzzle, and content burden grows through bespoke semantic captions and behaviors.

---

## C — Counterfeit Window — KILL
### Minimal model
Small fixed frame of cells, 2–4 rigid colored pieces with front/back boundary masks. Player assigns pieces to fixed slots and optional flips. Front inspection sees front mask; back inspection reverses slot order and uses back mask. Lead boundaries occlude selected color adjacencies.

### Tiny valid instance
Two slots, pieces A/B. Front requires red-red continuity across center; back requires a break. A-front right edge=red and A-back left edge=lead; B-front left=edge red and B-back right=edge red. Only A-left/B-right satisfies both views.

### Hostile instance
Once slots become spatially free, ordinary packing dominates; if slots stay fixed, most deductions are edge compatibility plus flip selection.

### Deduction families
front/back edge implication, flip parity, slot exclusivity, continuity/break constraints. These remain close to two-sided edge matching and do not yet justify the stained-glass production surface.

### Judgment
Kill. Fixed-slot version lacks depth; free-placement version becomes packing/search. It loses the sibling comparison to False Bottom, whose hidden legality layer creates stronger asymmetric reasoning.

---

## D — The Missing Reflection — RETAIN
### Minimal model
Discrete top-down orthogonal room. Mirrors occupy fixed wall sockets with orientation chosen from a tiny set (normally `/` or `\` equivalent on a 45-degree ray grid). Objects occupy fixed cells. Named observation ports emit finite rays. Goal specifies, per port, objects that must be seen at least once and objects forbidden from every reflected path. No continuous camera or free-angle placement.

### Tiny valid instance
Two ports P,Q, two mirrors M1,M2, objects A,B. P must see A but never B; Q must see B. M1 orientation x lets P ray terminate at A while orientation y sends it to B, immediately forcing x. That redirected geometry causes Q's first segment to miss B unless M2 takes orientation y; M2 is then forced.

### Hostile instance
Many mirror sockets with long multi-bounce rays and only positive goals; brute-force orientation search wins and visual tracing becomes bookkeeping.

### Human deduction families
1. forbidden-ray pruning from negative visibility;
2. first-divergence reasoning: the earliest mirror where two candidate ray paths split can be forced;
3. unique-source visibility: only one mirror state can expose a required object;
4. shared-mirror coupling across ports;
5. occlusion ordering / nearer-hit elimination;
6. path impossibility propagation after one forced reflection.

### Certifier / burden
Finite ray-state simulation and exhaustive orientation certifier are straightforward. Content can stay 2D/2.5D and deterministic. Major burden is legibility of reflected paths; controller can select a port and step through currently known physical ray segments without revealing solution correctness.

### Judgment
Retain. Negative-information fantasy is strong and mechanically distinct. Round B must cap bounce count and prove the game remains insightful rather than ray bookkeeping at hour 3.

---

## E — Ink Debt — RETAIN
### Minimal model
Finite pixel/cell canvas. Each stamp has a fixed binary mask, discrete transform, and ink identity. Applying a stamp toggles any currently inked overlapped cell to blank and paints only previously blank cells with the new stamp's ink? **Rejected ambiguity:** that rule creates involutive XOR-like behavior. Round-A canonical candidate is simpler and more physical: a stamp deposits its ink on blank cells and erases pre-existing ink on overlap, leaving overlap blank. Thus after action S: blank∩mask -> S-color; occupied∩mask -> blank; outside unchanged. Player chooses a bounded sequence from known stamps; final colored/blank pattern is judged.

### Tiny valid instance
Canvas cells 1..4. Stamp A covers {1,2}; B covers {2,3}; C covers {3,4}. Target: cell1=A, cell2=blank, cell3=B, cell4=C. C must occur after any stamp touching 4? Only C touches 4, so C is used. To leave 3 as B, B must be after C at cell3, but then C's cell4 survives. A and B overlap at2 and must both be used, forcing whichever is second to erase 2. Sequence A,C,B satisfies target.

### Hostile instance
Five stamps with nearly disjoint masks. Then order barely matters and the game is simply stamp selection; opposite extreme of dense masks creates factorial search.

### Human deduction families
1. unique-color provenance: a colored final cell forces the last effective stamp touching it;
2. required-blank overlap: final blank can prove an even/paired interaction or force a later eraser;
3. forced-late / forced-early relations from unique surviving colored cells;
4. overlap graph chains where one precedence forces another;
5. irrelevant-order equivalence classes for disjoint stamps;
6. contradiction by resurrecting/erasing a protected final cell.

### Certifier / burden
Small deterministic sequence-state engine; certifier can enumerate permutations/subsets and quotient commuting actions. Visual feedback is immediate and cheap. Authoring requires controlled overlap graphs, not bespoke narrative assets.

### Judgment
Retain, but Round B must attack whether its deduction grammar is truly richer than precedence/topological sorting. Need demonstrable blank-state reasoning and non-pairwise overlap interactions.

---

## F — False Bottom — RETAIN
### Minimal model
A drawer is a fixed grid of vertical columns. Each item has a visible top footprint/color and a hidden support footprint one layer below; player assigns 2–5 items to fixed candidate positions and chooses support orientation. Inspection judges only top cells, while legality requires every occupied top cell to be supported and hidden supports must obey collision/forbidden-zone rules. Crucially, no freeform packing: positions are socketed.

### Tiny valid instance
Three top slots A,B,C; two objects X,Y. Required visible tops at A and C, B empty. X at A can support through hidden cells {A,B} or {A}; Y at C can support {B,C} or {C}. Hidden cell B is forbidden to double-occupy and must contain exactly one support. Thus X/Y cannot both choose narrow variants if B must be occupied, and cannot both choose wide variants due collision; one must be wide. A second hidden clue “support under A forbidden” forces X narrow, therefore Y wide.

### Hostile instance
If hidden support simply mirrors visible footprint, it is ordinary placement. If supports have dozens of arbitrary shapes, content becomes packing-search and unreadable.

### Human deduction families
1. visible-slot forcing independent of hidden legality;
2. hidden support coverage constraints;
3. collision/exclusive-support reasoning;
4. top-equivalent / bottom-different ambiguity resolved by global support clues;
5. forced orientation from hidden forbidden zones;
6. resource-style support-count reasoning without numeric optimization.

### Certifier / burden
Finite socket assignment CSP; deterministic. Content can be rendered as dollhouse/drawer cutaway with toggleable x-ray for *current* supports, not future legality oracle. Low-to-moderate art burden.

### Judgment
Retain. Beats Counterfeit Window because top appearance and hidden structural truth create genuinely asymmetric state, not merely two-sided edge matching. Round B must prove hidden-layer reasoning stays central instead of becoming decorative constraint checking.

---

## G — Shared Alibi — KILL
### Minimal model
Actors assigned to fixed room positions/facings; static occluders. Clues state who could/could not see whom. Player reconstructs positions/facings.

### Tiny valid instance
Three actors, four sockets. A cannot see B; B can see C; C cannot see A. Occluder splits two lanes, forcing one assignment chain.

### Hostile instance
With enough actors/facings, solving is a generic assignment CSP. Pairwise visibility tables can be precomputed and the spatial fantasy disappears into a logic grid.

### Human deduction families
visibility incompatibility, socket exclusivity, facing elimination, occluder-mediated pair constraints. All compile cleanly to pairwise CSP edges; little irreducible geometry remains.

### Judgment
Kill. The failure hypothesis holds: a logic-grid solver representation is more natural than the purported room tableau.

---

## H — Casting Call — RETAIN
### Minimal model
Actors occupy fixed stage marks. Several audience seats emit discrete horizontal/diagonal sight rays. 2–4 movable stage flats slide among fixed tracks/positions. Each seat has an exact required visible actor subset. Flats are blockers only; actors never move.

### Tiny valid instance
Actors A,B,C on depth lanes. Seats S1,S2. S1 requires {A,C}, S2 requires {B,C}. Flat F1 has two positions: p blocks B only from S1; q blocks A only from S2. Flat F2 can block A from S1 or B from S2. To keep A visible at S1, F2 cannot first position; to keep B visible at S2, F2 cannot second — hostile? This reveals an unsatisfiable two-flat layout, useful as authoring rejection. Revised valid toy: F1 p blocks B/S1 only; q blocks A/S2 only. F2 p blocks A/S2 only; q blocks B/S1 only. Required sets force one flat into a B/S1 blocker and one into an A/S2 blocker while preserving C; two equivalent assignments expose symmetry that an extra track-occupancy rule can break.

### Hostile instance
Every flat affects one seat/actor pair independently. Then the puzzle is a bank of binary switches. At the other extreme, arbitrary polygon blockers create geometric brute force.

### Human deduction families
1. required-visible actor forbids every flat position covering that sightline;
2. forbidden-visible actor requires at least one blocker among a known set;
3. blocker-sharing: one flat position can satisfy multiple seat exclusions;
4. interval/depth dominance: a nearer flat can subsume multiple far block opportunities;
5. track exclusivity couples otherwise independent visibility clauses;
6. exact-set complement reasoning across seats.

### Certifier / burden
Finite flat-position CSP with precomputed visibility masks. Extremely controller-friendly and trailer-readable. Content cost is low if flats/tracks are data-driven.

### Judgment
Retain. It is the cleaner theatrical visibility concept. Stage Directions is killed below because its added lighting predicates multiply semantics without enough extra deduction.

---

## I — Palette Witness — KILL
### Minimal model
Three fixed light channels R/G/B, neutral objects, discrete occluder sockets. Surface samples display surviving channel subset; redundant symbols can encode subsets independent of color.

### Tiny valid instance
Sample x requires RG (B blocked), y requires G only, z requires RGB. Two occluders have known per-light shadow masks; z forbids any choice covering it, y forces R and B blockers, etc.

### Hostile instance
Once channel subsets are symbolized for accessibility, the problem becomes multi-channel shadow set-cover very close to Negative Casting but with more rendering complexity. In 3D, ambiguous penumbra/occlusion presentation worsens the problem.

### Judgment
Kill in sibling comparison. Negative Casting preserves the same useful deduction core—channel-specific occlusion and overlap—while having lower rendering/accessibility risk and a cleaner negative-space hook.

---

## J — Misprint Press — RETAIN
### Minimal model
Canvas cells; each plate has color, mask, optional discrete rotation. Printing is first-claim only: a plate colors only cells still blank; occupied cells never change. Player chooses/order all required plates to match a final multicolor print.

### Tiny valid instance
A(red) covers {1,2}; B(blue) covers {2,3}; C(green) covers {1,3,4}. Target colors: 1=red,2=red,3=blue,4=green. Cell4 uniquely forces C to be used. Cell1 red means A precedes C; cell3 blue means B precedes C; cell2 red means A precedes B. Thus A<B<C is forced without trying permutations.

### Hostile instance
If each overlap merely contributes one pairwise precedence edge, every puzzle is just reading a DAG/topological sort. Rotations that only add more edges do not rescue it.

### Human deduction families
1. unique-provenance plate forcing;
2. winner-at-cell precedence;
3. loser exclusion (a target color proves all competing plates later);
4. transitive chains;
5. rotation coupling: one chosen rotation changes precedence obligations at several cells;
6. subset-use coupling if optional plates are allowed.

### Certifier / burden
Deterministic, tiny. Strong print animation and cheap assets.

### Judgment
Retain narrowly. Round B is existential: must find non-pairwise reasoning produced by rotation/plate-selection coupling. If every hard instance compiles to a simple precedence DAG after rotations are chosen, kill it.

---

## K — Stage Directions — KILL
### Minimal model
Actors fixed; lights chosen from sockets/orientations; seat predicates classify each actor as LIT, SILHOUETTED or HIDDEN.

### Tiny valid instance
Two actors, two seats, two lights; target requires A lit at S1 and silhouette at S2 while B hidden at S1. Solving requires both illumination and seat occlusion states.

### Hostile instance
A single actor-seat state depends on light incidence, actor occlusion, seat visibility and possibly silhouette background. The predicate vocabulary becomes difficult to teach/certify and authored cases need many exceptions.

### Judgment
Kill in sibling comparison. Casting Call yields the strongest part—multi-seat inverse visibility—using one blocker grammar. Lighting adds state dimensions and production burden faster than it adds qualitatively new human deductions.

---

## L — Edge of Evidence — KILL
### Minimal model
Fragments expose discrete boundary ports tagged by painted-stroke properties: color/class, tangent direction, whether stroke terminates at break, and optional width. Player joins compatible fragment edges into a plate; objective is one connected reconstruction.

### Tiny valid instance
Four fragments in a ring. Two local joins share identical color/tangent signatures, but choosing the wrong one forces a painted line to terminate twice even though its endpoint count rule requires zero interior terminations; global continuity resolves it.

### Hostile instance
Rich edge signatures make each local join unique, yielding trivial jigsaw matching. Weak signatures produce enormous arrangement search whose difficulty is spatial assembly rather than deduction.

### Deduction families
edge compatibility, endpoint-count parity, loop/chain continuity, global fragment-degree constraints. Promising, but much of the player activity is still physical jigsaw placement and orientation search.

### Judgment
Kill for this slot. It could be a good separate restoration game, but Round A does not prove enough reasoning distance from exact-cover/jigsaw assembly to justify surviving a strong field.

---

# Sibling comparisons

## Negative Casting vs Palette Witness
Both are channel-specific occlusion CSPs. Palette Witness's accessible non-color encoding removes much of its unique color fantasy while retaining 3D/rendering burden. Negative Casting has the same useful deductions in a cheaper, more legible two-wall negative-space system and stronger monochrome accessibility. **Negative Casting survives; Palette Witness dies.**

## Casting Call vs Stage Directions
Both use stage/audience multi-view constraints. Casting Call has one crisp state variable—visible or blocked—and gains depth from shared flats/tracks across seats. Stage Directions adds illumination/silhouette/hidden semantics that increase rules and authoring cases without a correspondingly new reasoning family. **Casting Call survives; Stage Directions dies.**

## Counterfeit Window vs False Bottom
Counterfeit Window's strongest toy model is two-sided edge compatibility; allowing free placement reintroduces packing. False Bottom has two coupled but asymmetric truths: visible inspection and hidden structural legality, with top-equivalent placements that only hidden constraints can disambiguate. **False Bottom survives; Counterfeit Window dies.**

# Round-A cut
## Retained semifinalists — 6
1. **Negative Casting** — best immediate visual hook; must prove depth beyond interval exact-cover.
2. **The Missing Reflection** — strong negative-information optics; must defeat ray-bookkeeping risk.
3. **Ink Debt** — elegant destructive composition; must prove more than precedence/order enumeration.
4. **False Bottom** — strongest hidden-vs-visible asymmetric state; must keep hidden layer central.
5. **Casting Call** — cleanest multi-view visibility architecture; must prove campaign variety beyond blocker clauses.
6. **Misprint Press** — excellent physical clarity and certifier; survives only if Round B proves non-DAG reasoning.

## Killed in Round A — 6
- Museum of Wrong Labels — dressed permutation/logic-grid CSP.
- Counterfeit Window — packing/edge-matching dilemma.
- Shared Alibi — compiles too naturally to generic pairwise CSP.
- Palette Witness — dominated by Negative Casting at lower complexity.
- Stage Directions — dominated by Casting Call at lower semantic burden.
- Edge of Evidence — jigsaw/search activity remains too central.

# Cross-semifinal concern map
- **Negative Casting vs Casting Call vs Missing Reflection:** all touch visibility/occlusion, so Round B must compare their *reasoning* rather than themes. Negative Casting = channel overlap/classification; Missing Reflection = redirected path constraints + negative targets; Casting Call = shared blockers across exact visible subsets.
- **Ink Debt vs Misprint Press:** both are ordered 2D imprint systems. Ink Debt is destructive overlap with blank as an information-bearing state; Misprint Press is monotone first-claim precedence. They may not both survive Round B.
- **False Bottom** is currently the most mechanically isolated survivor, but its commercial hook is less instantly spectacular than Negative Casting/Missing Reflection and must prove demo clarity.

# Round B protocol / harder failure hypotheses
Round B should not add features merely to save a weak concept. For each semifinalist construct a *family* of 5–8 abstract cases at increasing complexity and classify the shortest human solve path.

1. **Negative Casting:** KILL if all hard cases reduce after preprocessing to interval/set exact-cover with the same attribution deductions. Must show at least 3 qualitatively distinct case families across multi-wall coupling, exclusive-channel reasoning and boundary inference.
2. **The Missing Reflection:** KILL if useful puzzles require >2 bounces routinely, manual ray tracing dominates, or negative visibility does not materially outperform brute-force orientation search. Prove a bounded optics grammar suitable for controller/handheld.
3. **Ink Debt:** KILL if every case is explainable as pairwise stamp precedence plus permutation enumeration. Must demonstrate blank-state deductions, commuting equivalence and at least one genuinely non-pairwise overlap motif.
4. **False Bottom:** KILL if visible assignment can be solved first and hidden supports merely validated afterward. Need cases where hidden constraints force visible choices early, plus at least 3 structural support motifs.
5. **Casting Call:** KILL if each required/forbidden sightline acts as an independent Boolean clause. Need shared blockers, track exclusivity, depth dominance and exact-set complement to produce different solve families.
6. **Misprint Press:** KILL if choosing plate transforms followed by a DAG/topological sort is always the complete puzzle. Need rotation/selection coupling that forces transforms through global color provenance before order becomes known.

Round B target: cut 6 -> **3**, not a winner. Then Round C should attack hour-3 repetition, campaign/content economics, tutorial/demo arc, technical risk and market/product thesis before selecting one concept.

# Round-A result
Phase 2 Round A = **PASS**. Six concepts remain. No final concept selected. No production implementation started.
