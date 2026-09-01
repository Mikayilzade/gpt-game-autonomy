# GAME #013 — PHASE 2 CONCEPT TOURNAMENT

Date: 2026-09-01
Status: ROUND A COMPLETE — 12 -> 5 survivors; no winner selected.

## Method
Round A uses equal destructive evidence, not pitch scores. Every candidate gets: a smallest exact rule kernel, two concrete state examples, bounded search-space estimate, dominant-strategy/brute-force attack, content/tutorial/readability test, and portfolio-collision test. Examples are diagnostic microcases, not canonical levels. A candidate survives only if the same small vocabulary plausibly supports qualitatively different deductions.

Search-space counts below count naive legal action combinations before target predicates prune them. They are intentionally small enough to expose whether play degenerates into enumeration.

---

## A. Carbon Copy — SURVIVE
### Minimal kernel
Three aligned 3x3 sheets A/B/C. Each sheet has visible carbon cells and writable cells. A press action chooses one stamp footprint and a top sheet. A marked cell transfers downward through consecutive carbon-enabled contact cells; the first non-carbon cell receives the mark and stops that ray. Existing marks do not move. Sheet order is fixed in the microkernel; later families may allow one bounded reorder before pressing. Goal predicates inspect exact/categorical marks separately per sheet.

### Case A1 — depth by stopping layer
A/B/C are 2x3. Carbon columns on B = {1,3}; C has no carbon. One horizontal 1x2 stamp may be pressed on A at starts 1 or 2. Target: B must receive exactly one mark; C exactly one; A receives both stamp marks. Start 1 sends col1 through B to C while col2 stops on B; start2 reverses which columns penetrate. Two legal placements, both satisfy counts but only one satisfies target labels B:{2}, C:{1}. Deduction is visible ray stopping, not arithmetic.

### Case A2 — coupled two presses
3x3; B carbon at center plus NW/SE diagonal, C carbon only center. Two domino stamps, one horizontal and one vertical, each used once. Target requires B marks at N,W and C mark at center while forbidding duplicate-mark cell E. Naive placements: 6 horizontal x 6 vertical = 36 ordered pairs. Because the shared center penetrates two layers while its neighbors stop on B, placement choices couple across sheets; target can be reasoned from required receiving layers before testing positions.

### Attack
- Enumeration surface: modest authored boards can reach hundreds/thousands, but visible required receiving layer provides inverse deductions.
- Collapse risk: if every column has a fixed transfer depth, puzzle becomes independent per-cell lookup. Content gate must require overlapping multi-cell stamps, shared target cells, limited stamp inventory or bounded pre-order choices.
- Tutorial: mark -> carbon pass-through -> stop is explainable in one animation.
- Visual: excellent exploded-stack GIF; screenshot needs layer tabs/exploded view.
- Content families: transfer depth, stamp footprint coupling, overlap/no-duplicate, bounded sheet reorder, positive/negative target predicates.
- Portfolio: distinct from #009 because no folding/nesting/final permutation; state transform is pressure transfer through aligned layers.

Verdict: SURVIVE. Strong causal hook; must later prove it does not become a transfer-depth matrix.

---

## B. Margin Call — SURVIVE
### Minimal kernel
A printed rectangular grid has immutable symbols. Player crops by choosing final top/bottom/left/right boundaries, each moving inward only. After cropping, a cell qualifies by visible local context relative to the NEW boundary: examples EDGE, CORNER, HAS-N-VISIBLE, row/column run. Goal predicates count or identify qualifying labeled cells. Removed cells cease to exist; no movement.

### Case B1 — globally coupled boundaries
4x4 labels at (1,2)=A, (2,2)=B, (3,3)=C, (4,3)=D. Choose a 3x3 crop (4 possible windows). Target: A must be EDGE, C INTERIOR, D absent. Only rows1-3/cols1-3 works: A is top edge, C bottom/right? Here C at (3,3) is corner, so target deliberately fails; replacing target C=CORNER gives unique window. The diagnostic shows all four boundaries jointly determine role; no independent threshold solution.

### Case B2 — local-neighbor reinterpretation
5x5 with marked cells P(2,2), Q(2,4), R(4,2), S(4,4), blocker X(3,3). Choose any crop retaining >=3x3. Target: exactly two of P/Q/R/S are boundary cells, X remains interior, and P/S share boundary status. There are at most 15 row intervals x 15 column intervals =225 rectangles before size/retention pruning. P/S coupling plus X interior prevents solving four edges independently.

### Attack
- Brute force: rectangle choice is O(r^2 c^2), dangerously enumerable on small boards.
- Required anti-collapse gate: never use only absolute retain/remove predicates. Every authored case must include >=2 boundary-relative/local-context predicates coupled across both axes; later cases need labels spanning multiple edges.
- Tutorial: extremely low burden.
- Visual: crop frame changing symbol roles is legible in a GIF; static screenshot can show before/after role badges.
- Content families: boundary identity, corner status, visible-neighbor/run changes, grouped labels, exact retained populations, fixed-aspect crops.
- Portfolio: no prior game uses destructive frame/context reinterpretation.

Verdict: SURVIVE narrowly. Round B must prove a hard case where deduction beats testing rectangles.

---

## C. Pallet Proof — KILL
### Minimal kernel
Discrete 3D crate stack, choose one of four orthographic viewing directions; only first visible crate per ray contributes its label/color to manifest predicates.

### Cases
C1: 2x2x2 stack with four occupied rays; choose N/E/S/W so visible labels contain exactly one red and label A. Four choices only: trivial enumeration.
C2: two bounded stack swaps plus final view. With 4 legal swaps x 4 views =16 states, occlusion deductions exist but immediately resemble projection/silhouette puzzles.

### Attack
Depth requires adding stack rearrangement or multiple simultaneous views, which raises 3D presentation/content burden and moves toward familiar orthographic/projection CSP. A static image advertises crates, not the novel rule. Label predicates decorate rather than transform the familiar reasoning object.

Verdict: KILL — projection familiarity + disproportionate 3D burden.

---

## D. Seal Break — SURVIVE
### Minimal kernel
A cabinet has compartments separated by seams. A seal spans a listed set of seams. Opening a compartment breaks every intact seal crossing any seam that compartment must traverse; broken seals stay broken. Player may place K seals from finite sockets, then must execute a fixed or partly chosen opening sequence. Goal is an evidence signature: specified seals intact/broken after each checkpoint, not merely final count.

### Case D1 — temporal evidence
Three compartments L/M/R. Seal sockets sLM crosses L-M, sMR crosses M-R, sALL crosses both. Place two of three. Open L then R. Target after L: exactly one broken; after R: both broken. Choosing {sLM,sMR} works; {sLM,sALL} breaks two at L; {sMR,sALL} leaves? sALL breaks at L and sMR at R, also works on counts, so identity checkpoint sLM broken after L and sMR intact makes unique {sLM,sMR}. 3 placements choose2 =3.

### Case D2 — order coupling
Four compartments in a 2x2 cabinet; six candidate seals each spans one or two door seams. Choose 3 seals and choose whether checkpoint opens NW->SE or SE->NW before mandatory NE. Naive <= C(6,3)*2=40 setups. Target identities require one seal broken only at checkpoint2, one survives all, and one breaks at checkpoint1. A seal spanning both first-open routes is therefore forbidden despite matching final evidence, producing temporal deduction rather than set-cover alone.

### Attack
- If only final broken-set matters, it is set cover in costume. Mandatory gate: every substantive case has >=2 temporal checkpoints or conditional opening choices whose order changes evidence.
- Brute force remains small, but intermediate evidence gives backwards reasoning.
- Tutorial: place seal, open, tear is immediate.
- Visual/GIF: exceptionally strong.
- Content families: shared seams, nested doors, fixed vs chosen opening order, limited seal inventory, checkpoint identity, seals spanning multiple seams.
- Portfolio: destructive evidence state is new; not #011 deletion because player creates evidence constraints before deterministic destructive events.

Verdict: SURVIVE. Round B must prove temporal system scales without becoming scheduling CSP.

---

## E. Overprint — KILL
### Minimal kernel
Choose/order two sparse binary masks on aligned cells. Later print replaces earlier color on opaque cells; special overlap may mix to a third visible class. Windows judge final colors.

### Cases
E1: two 2x2 masks, 4 offsets each x 2 orders =32 states. A target requiring one mixed and one top-color cell is solvable by inspecting overlap.
E2: three windows with exact color counts couples offsets, but solution procedure becomes boolean convolution/offset testing.

### Attack
The rule kernel is clean but every state is a cellwise function of mask occupancy + order. Human deductions are mostly overlap algebra; increasing depth means more masks, offsets or special ink exceptions. This directly competes with Wax Witness for the same 'layered final impression' fantasy and is the weaker tactile/semantic version.

Verdict: KILL — boolean-grid collapse and overlap with Wax Witness; do not keep both.

---

## F. Shared Fuse — KILL
### Minimal kernel
Discrete circuit; activating device adds fixed load to every fuse on its path. If cumulative live load exceeds fuse rating, fuse opens permanently and downstream devices lose power. Player sequences activations to target final live/dead signature.

### Cases
F1: two 2A devices share 3A fuse; one has alternate 1A branch. Sequence determines which branch survives. <=6 action sequences.
F2: three devices across two shared fuses gives 3!=6 activation orders; target can require intentional first overload.

### Attack
Reasoning is load arithmetic plus sequence search. More depth adds conventional circuit topology and ratings. This also approaches #005's conserved/shared-network load identity even though failure is destructive rather than redistributive.

Verdict: KILL — arithmetic/circuit familiarity and substantive portfolio collision with #005.

---

## G. Counterweight Clerk — KILL
### Minimal kernel
Discrete beam hooks at integer distances. Hang fixed-weight labeled parcels. Beam orientation is sign(total torque); orientation exposes/hides stamps behind flaps. Goal judges exposed labels after placements.

### Cases
G1: weights 1,2 on hooks ±1,±2: 12 ordered placements; target balance plus one exposure is solved by torque equality.
G2: three parcels and a flap threshold produce <=60 arrangements but still reduce to weighted sums and threshold comparisons.

### Attack
The physical metaphor is strong, but exact solving is equations/knapsack with cosmetic exposure predicates. Avoiding arithmetic would require simulated physics, violating scope safety.

Verdict: KILL — arithmetic is the mechanic, not a hidden source of spatial depth.

---

## H. Wax Witness — KILL (wins comparison over Overprint aesthetically, still fails depth gate)
### Minimal kernel
Place/order dies on a small wax grid. A press writes ridge class; later presses flatten conflicting ridge orientations while matching ridges deepen. Goal inspects final ridge classes.

### Cases
H1: two 1x2 dies, horizontal-ridge vs vertical-ridge, 6 placements each x2 order <=72; overlap yields FLAT while non-overlap preserves ridge.
H2: add a ring die and target one DEEP, one FLAT region; deductions use overlap identity, but per-cell state is still a finite overwrite table.

### Wax Witness vs Overprint
Wax has a more distinctive physical fantasy and symmetric conflict (flatten) rather than simple later-ink precedence. However both share the same computational skeleton: aligned footprints + order + per-cell composition table -> final window predicates. Keeping either would require proving non-cellwise interactions. Wax's proposed 'ridge persistence' does not do that; it merely enlarges the cell alphabet.

Verdict: KILL both. Wax beats Overprint as presentation, but neither passes the second-order-depth test without adding exceptions.

---

## I. Cut Here — KILL on portfolio boundary
### Minimal kernel
Stack 2D cards with independently chosen quarter-turn orientations. Choose one straight cut in stack coordinates; each card receives that same cut transformed into its local coordinates. Targets judge which printed regions on each card are intersected/separated.

### Cases
I1: 3 cards x 4 orientations each x 6 cut lines ~=384 configurations; inverse reasoning from a required local cut can constrain orientation.
I2: two cuts chosen from 8 lines gives <=28 cut pairs times orientation choices; shared cuts couple all layers strongly.

### Attack / #009 comparison
As a standalone puzzle this is excellent: one action transformed across layers, strong GIF, deterministic and content-efficient. But #009 Binder's Imposition is already a flat-sheet/signature puzzle whose core mastery is predicting how source coordinates/orientations transform through deterministic fold/flip/nest/trim operations into final constraints. Cut Here removes bookbinding but preserves too much of the portfolio-level reasoning identity: independently oriented flat layers + shared physical transform + local-coordinate consequences + trim/cut semantics. The user explicitly requires substantive reuse to die, not merely a reskin distinction.

Verdict: KILL — strong concept, unacceptable #009 portfolio collision.

---

## J. Blind Staple — SURVIVE
### Minimal kernel
Packet contains 3–5 visible card layers. Player chooses their order and then one staple socket from a finite grid. Staple has fixed penetration depth D: it pierces the first D layers at that cell. A pierced layer is bound to its immediate pierced neighbor; printed keep-out zones may forbid puncture and target predicates require specified layer pairs bound/unbound. Layer contents and depth are fully visible in exploded preview before commit; no hidden information.

### Case J1 — order deduction
Layers A,B,C; D=2; one socket intersects safe zones on A/C but forbidden zone on B. Goal bind A-C while B unpunctured. Only orders with A,C in top two and B third can work: 2 valid permutations of 6; socket choice then fixes which orientation of A/C is legal. This is adjacency-through-depth, not generic stack permutation alone.

### Case J2 — two staples, conflicting adjacency
Four layers A-D, D=3. Two sockets X,Y. At X safe set {A,B,C}; at Y safe set {B,C,D}. Use both staples; target A-B bound at X, C-D bound at Y, A-D never directly bound. 24 layer orders x bounded 2-staple placement choices. Required participation at opposite sockets constrains outer layers, while shared B/C must occupy penetrating middle positions. Human deduction can infer relative stack bands before permutation.

### Attack
- Factorial brute force is the primary danger. Hard ceiling should remain <=6 layers; authored cases must include visible per-layer socket compatibility so deductions eliminate position bands.
- Avoid arbitrary staple depths per level; 2 then 3 is enough vocabulary.
- Visual: packet cross-section + staple penetration is instantly legible in GIF; screenshot can use exploded layers.
- Content families: one/two staples, depth2/3, keep-out regions, required pair binding, forbidden puncture, bounded rotations only if later proven necessary.
- Portfolio: unlike #009, no fold/permutation-to-final-book transform; core is depth-limited binding adjacency through an ordered packet. Still watch flat-layer aesthetic similarity.

Verdict: SURVIVE. Strongest risk is factorial enumeration; Round B must prove deduction-rich 5-layer case.

---

## K. Transfer Window — SURVIVE
### Minimal kernel
Two cyclic strips A/B each have binary holes over N positions and token tracks. Player may shift one strip by one step left/right, then optionally TRANSFER. On transfer, at positions where both strips have holes, a token present on exactly one side moves to the other; positions without coincident holes do nothing. Tokens are conserved. Shifts change alignment but not token coordinates on their own. Goal judges final token ownership and optionally requires a transfer budget.

### Case K1 — conservation deduction
N=5. A holes {0,2}, B holes {0,1}; A token at0, B token at2. One shift of B in {-1,0,+1}, then transfer. Target both tokens on B. Only alignment making B holes coincide with A's token0 while NOT coinciding with B-token2 can satisfy; three offsets, direct deduction from desired transfer/non-transfer.

### Case K2 — two-transfer sequencing
N=6. A holes {0,3}, B holes {0,2}; tokens A:{0,4}, B:{3}. Two shifts each in {-1,+1} with transfer after each: only 4 direction sequences before considering start offset. Target ownership A:{3}, B:{0,4}. First transfer must move token0 A->B while preserving B3; second must move B3->A without returning token0. This requires reasoning about future coincidence and conservation, not counts.

### Attack
- If only one transfer, puzzle is offset enumeration. Mandatory depth gate: substantive cases require >=2 transfers where an alignment good now can undo a prior transfer later.
- Modular arithmetic is visible but should not be required numerically; render physical holes/tokens.
- State graph can be brute-forced cheaply by implementation/certifier; player-facing cases need inverse token-ownership deductions.
- Content families: asymmetric hole patterns, transfer budgets, forbidden return, fixed intermediate checkpoint, 2 vs 3 strips only if two-strip depth proves insufficient.
- Visual: very strong sliding-strip GIF.
- Portfolio: not conveyor permutation (#010): tokens conserve identity and cross ownership tracks only at coincident windows; no fixed gantry relabeling.

Verdict: SURVIVE. Round B must prove it does not become 'try each offset sequence.'

---

## L. Dry Run — KILL on lineage + generic cellular propagation
### Minimal kernel
Grid has dry absorbent strips. Activating a source wets adjacent connected dry material exactly one step per tick; newly wet cells become impermeable to later flow. Player orders sources/strip placements to target wet/dry signature.

### Cases
L1: two sources around a T junction; source order decides which branch is claimed first. Two orders: trivial.
L2: three sources and two strip placements create <= dozens of sequences; competition fronts can be interesting but are essentially flood-fill timing/territory.

### Attack / Ink-Bleed lineage
The defining proposal is propagation through absorbent material followed by saturation becoming a barrier. That is materially the same conceptual lane previously rejected as Ink Bleed during #012 exploration: wet/ink propagation with state change blocking later propagation. Renaming liquid/strip geometry does not establish independence. Even without portfolio history, scaling trends toward generic cellular flood simulation and sequence search.

Verdict: KILL — substantive rejected-lineage reuse plus familiar flood-fill search.

---

# Round A comparison

| Candidate | Hook | Deduction source | Main collapse risk | Portfolio | Verdict |
|---|---|---|---|---|---|
| Carbon Copy | excellent | receiving-layer constraints + footprint coupling | transfer-depth matrix | clean | SURVIVE |
| Margin Call | excellent | boundary-relative role coupling | rectangle enumeration | clean | SURVIVE |
| Pallet Proof | good | occlusion | projection CSP | clean but familiar | KILL |
| Seal Break | excellent | temporal evidence checkpoints | set cover/scheduling | clean | SURVIVE |
| Overprint | excellent | footprint overlap | boolean grid algebra | clean | KILL |
| Shared Fuse | good | overload sequence | arithmetic/circuit search | #005 risk | KILL |
| Counterweight Clerk | excellent | torque | weighted-sum arithmetic | clean | KILL |
| Wax Witness | excellent | footprint composition | finite per-cell overwrite algebra | clean | KILL |
| Cut Here | exceptional | shared transformed cut | configuration enumeration | substantive #009 collision | KILL |
| Blind Staple | exceptional | penetration bands + layer adjacency | factorial permutation | watch #009 aesthetic only | SURVIVE |
| Transfer Window | exceptional | conservation + reversible coincidence | offset sequence enumeration | distinct from #010 | SURVIVE |
| Dry Run | good | competitive propagation | flood-fill sequencing | rejected Ink-Bleed lineage | KILL |

## Round A survivors — 5
1. **Carbon Copy**
2. **Margin Call**
3. **Seal Break**
4. **Blind Staple**
5. **Transfer Window**

No winner is selected. The Phase-1 score leader Cut Here is deliberately killed because portfolio independence is a hard gate, demonstrating that tournament evidence supersedes pitch score.

## ROUND B NEXT
Build one substantially harder, machine-enumerable diagnostic puzzle for EACH of the five survivors under a comparable action-space budget (target naive space ~100–10,000 states where the mechanic permits). For each:
1. define exact state/action semantics without relying on prose ambiguity;
2. enumerate or exhaustively reason solution count and shortest/allowed solution structure;
3. document at least three human deductions that reduce search before guessing;
4. derive 5–8 plausible content families and identify which are genuinely new reasoning rather than parameter inflation;
5. test whether a 6-case demo can escalate using the same vocabulary;
6. attack Carbon Copy's transfer-depth matrix collapse, Margin Call's rectangle enumeration, Seal Break's set-cover/scheduling collapse, Blind Staple's factorial permutation, and Transfer Window's offset-sequence brute force;
7. reduce to 2–3 finalists only if evidence is decisive; otherwise kill weak candidates rather than force a quota.

Production implementation remains forbidden. Throwaway enumeration scripts/calculations are allowed only as tournament evidence.