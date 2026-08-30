# GAME #009 — PHASE 2 CONCEPT TOURNAMENT

Status: **RUN 1 COMPLETE / 10 -> 5**
Date: 2026-08-31
Active slot: **Game #009 only**
Selected concept: **NONE**
Production implementation: **FORBIDDEN in factory**

Authority order for this run:
1. `START_HERE.md`
2. `STATUS.md`
3. `GAME_INDEX.md`
4. `GAME9_RESEARCH.md`
5. this file

Games #001–#008 are exclusion/portfolio history only. No mechanic from those frozen games becomes Game #009 canon through comparison language here.

---

## 1. Run objective

Destroy weak concepts before product-thesis lock. Every Phase-1 top-10 entrant receives the same questions:
- what does a mature case actually feel like minute to minute?
- where is the hour-8 depth rather than tutorial novelty?
- what happens if the player brute-forces, greedily optimizes or exhaustively searches?
- can a solver/validator prove authored cases are legal, solvable and nontrivial?
- what is the content and asset burden?
- can a 15–30 minute demo show premise, twist and mastery without spoiling the whole game?
- what current analogue owns nearby market language?
- does the decision structure collide with Games #001–#008 even if the theme differs?
- what empirical result would kill the concept during prototype/playtest?

Run 1 does **not** reward novelty alone. Ties are broken by implementation safety + durable depth + demo strength.

---

## 2. Fresh market / analogue refresh — 2026-08-31

This is not a sales forecast. It is collision evidence used to make the tournament harsher.

### Craft / workshop is legible but occupied
- Double Fine's `Kiln` launched its pottery fantasy in 2026 and explicitly makes crafted pot shape affect play. That makes "pottery, but game" a poor differentiator even though our G9C03 proposed kiln-neighbor logic is mechanically different. Source: https://news.xbox.com/en-us/2026/01/22/kiln-developer-direct-double-fine-hands-on-preview/
- `Bookbinding – Dark Cozy Sim` released 2026-07-24 on Steam and foregrounds book craft, customers and cover creation. Binder's Imposition therefore cannot sell as a generic bookbinding fantasy; it must sell the sheet-order/fold consequence puzzle. Source: https://store.steampowered.com/app/3555780/Bookbinding/
- `A Stitch In Time` foregrounds cutting/sewing garments in a tailor shop; `The Great Couturier` foregrounds garment design and pattern placement. Tailor's Grain must be visibly a constraint puzzle about one finite cloth, not a fashion or sewing sim. Sources: https://store.steampowered.com/app/3365300/A_Stitch_In_Time/ and https://store.steampowered.com/app/2850970/The_Great_Couturier/
- `Darkroom` (2025) uses a photographic darkroom as atmospheric horror, not as a systemic exposure puzzle. Darkroom theme alone is therefore not free market whitespace, but G9C25's proposed mask/exposure mechanics remain distinguishable. Source: https://store.steampowered.com/app/3832600/Darkroom/
- `Virtual Foundry` released 2026-03-20 and presents mold preparation/casting as educational simulation. Mold Release therefore needs a visibly abstract geometry-puzzle identity and must avoid accidental vocational-training expectations. Source: https://store.steampowered.com/app/4430750/Virtual_Foundry/

### Visual-theme collisions are not necessarily mechanical collisions
- `Glass Masquerade` remains a highly rated stained-glass-inspired jigsaw puzzle. Stained Glass Noon must lead with one window satisfying multiple time-indexed projected targets; piece-fitting alone would look derivative. Source: https://store.steampowered.com/app/511470/Glass_Masquerade/
- `Impresario – Theater Tycoon` explicitly advertises live control of lighting, scenery and performer entrances during performances. Stage Cue Machine therefore sits closer to an occupied fantasy than Phase 1 suggested, even though its finite legality-changing cue stack differs. Source: https://store.steampowered.com/app/3713600/Impresario__Theater_Tycoon/
- Puppet/theater aesthetics are also active through games such as `Once Upon A Puppet`; this does not directly collide with Paper Automata, but means physical-theater imagery itself is not a hook. Source: https://store.steampowered.com/app/1904880/Once_Upon_A_Puppet/
- The name `Coin Strike` already collides with unrelated games/slot language. More importantly, the concept must survive structural comparison to Game #008 rather than rely on minting novelty. Sources include https://store.steampowered.com/app/3075700/CoinForge/ and current web results for Coin Strike titles.

### Market conclusion for Run 1
The safest surviving lane is **not** "cozy craft simulator." It is a compact premium systemic puzzle in which the craft apparatus makes a precise rule visible. The concept must still read if all shop management, narrative customers, economy, avatar walking and realistic vocational procedure are removed.

---

## 3. Equal destructive scoring rubric

Each dimension is 1–5 after attack, maximum 50.

| Code | Dimension | 5 means |
|---|---|---|
| H | Hook legibility | one sentence + one GIF communicates the unique decision |
| M | Mature-case quality | a non-tutorial case creates several interacting decisions |
| D | Hour-8 depth | new reasoning emerges from recombination, not merely larger numbers |
| A | Anti-dominant-strategy resilience | no obvious always-best ordering or exhaustive ritual trivializes play |
| SV | Solver/validator feasibility | exact validation is practical at intended state sizes |
| I | Implementation safety | discrete deterministic authority can avoid fragile continuous simulation |
| C | Content efficiency | strong cases can be authored/recombined without huge bespoke asset volume |
| Demo | 15–30m demo strength | premise -> twist -> mastery arc fits cleanly |
| Market | Differentiation | adjacent current games do not own the same store-page promise |
| Portfolio | Games #001–#008 distance | decision structure is clearly distinct, not a noun swap |

Automatic kill conditions override score:
1. core fun requires production-scale continuous physics before validation;
2. mature play collapses into repetitive exhaustive checking with no meaningful cost/ordering choice;
3. reliable solver/validator is disproportionate to factory scope;
4. concept materially reproduces a frozen portfolio decision structure;
5. the demo cannot expose the second-order system within 30 minutes.

---

# 4. Entrant destruction tests

## G9C01 — Ink Trap Press

### Mature-case walkthrough
One sheet has four target regions and two forbidden contamination zones. The player owns three plate masks, two ink classes and a bounded pressure choice. Each pass transforms the sheet rather than merely adding a flat color: exposed wet cells may spread one adjacency step under high pressure; an existing dry ink can resist, receive, mix, or block a later ink according to a tiny visible interaction table; one mask covers geometry but also delays drying in covered cells for the next pass. The target asks for final color classes in some regions, clean paper in others, and one registration edge that must remain sharp.

A mature solution is not "paint red, then blue." The player may need to print a sacrificial resist first, use a low-pressure pass to create a boundary, exploit temporary wetness on one region, then deliberately cover a nearly-correct area while printing elsewhere. Order changes legality and future spread.

### Minute-to-minute loop
1. inspect final target and current sheet state;
2. preview one plate/mask/ink/pressure pass;
3. compare predicted changed cells and wet/dry consequences;
4. commit pass;
5. observe crisp physical transformation;
6. revise plan under a small pass budget or material constraint;
7. finish and compare against target tolerances.

Preview must not become a full future oracle. It may show the direct next-pass result, not recursively solve later spread chains.

### Hour-8 depth claim
Depth comes from interaction vocabulary, not more colors: drying windows, negative-space preservation, overprint classes, pressure-dependent spread, registration offsets, masks that protect now but alter later wetness, and objectives that constrain intermediate as well as final states. Late cases can require the same small rule set to satisfy multiple image regions with fewer passes than independent treatment would allow.

### Dominant-strategy / exhaustive-search attack
**Attack:** if preview is free and every action has a small branching factor, the player may try every plate/ink/pressure combination from every state and choose any locally improving result.

**Defense requirement:** local improvement must not be monotonic. Some correct moves temporarily worsen target similarity while preparing resist or preserving future wetness. Mature case validation must include at least one case where every greedy target-similarity move fails and at least two first-pass candidates look locally plausible. Previewing one next state is allowed; full lookahead is not supplied by UI.

**Residual risk:** if state sizes are too tiny, a human can brute-force. That is acceptable only if the resulting search tree still requires conceptual pruning; case design cannot rely on obscurity.

### Solver / validator feasibility
High if authority is a finite cell grid (for example 8x8–16x16 logical cells), finite ink states, finite wetness timer classes, finite masks and <=6–8 committed passes. State transitions are deterministic. A BFS/A*/IDA* or bounded DFS can validate solvability, minimal/near-minimal pass count, multiple solution traces and greedy traps. Exact pixel rendering stays presentation-only.

### Content / asset model
Content is data: target grid, starting sheet, available plates/masks, ink interaction subset, pass budget and optional objectives. Visual assets can reuse paper/ink shaders and generic plate geometry. Authored cases need puzzle reasoning, not bespoke environment art.

### 15–30 minute demo spine
- Case 1: one plate, direct print; tactile promise.
- Case 2: second ink shows overprint.
- Case 3: high pressure spreads into a forbidden edge.
- Case 4: mask/resist teaches a move that initially looks worse.
- Demo capstone: three passes, two inks, one temporary wetness dependency; shows why order matters.

### Nearest-current-analogue differentiation
Current art/craft sims and marbling games emphasize creation, physics or workshop fantasy. Ink Trap Press must present **deterministic constrained overprinting** rather than free painting or shop management. `Ebru Artist Simulator` is specifically physics-based marbling and workshop management, reinforcing the need for our finite-state puzzle identity rather than realistic fluid simulation.

### Portfolio collision attack
Closest structural concern is #008 because commits can irreversibly narrow future options. Difference is material: #008 edits persistent vectors against multiple acceptance sets; C01 transforms a 2D substrate under temporal material interactions, with masks and spread creating spatial state. It must not reduce to "increment cells until targets accept." Keep multi-region spatial interactions and order-dependent blocking central.

### Empirical kill gate
Kill if a prototype of 12 representative cases shows either: (a) >=70% can be solved by always choosing the preview with best immediate target similarity, or (b) players describe the game as trial-and-error paint-by-numbers rather than planning interactions.

### Run-1 verdict
**SURVIVE.** Richest compact state transformation in field; good solver fit; excellent visual causality.

---

## G9C02 — Binder's Imposition

### Mature-case walkthrough
A requested 16-page booklet must be produced from two duplex sheets. Each sheet has front/back slots tied by flip orientation. The player places page faces, chooses one of a few allowed fold signatures, nests sheets, chooses binding edge, then trims. Folding remaps slots into leaf order; duplex orientation mirrors/reverses one face; nesting changes adjacency; trim may remove intentionally sacrificial registration bands. The final book must read 1..16, preserve two specified facing-page spreads and place one color insert as an outer leaf.

A mature case can deliberately make the obvious sequential page placement impossible. The reasoning object is the transformation from flat sheet coordinates to final leaf order.

### Minute-to-minute loop
1. inspect requested final booklet constraints;
2. choose signature/fold template;
3. place or swap page faces on sheet slots;
4. fold-preview the physical sheet into a compact mockup;
5. inspect resulting page sequence/facing relationships;
6. adjust placement/orientation/nesting;
7. commit bind + trim once satisfied.

The fold preview is not hidden-information gameplay; the challenge is constructing the permutation.

### Hour-8 depth claim
Depth sources: multiple signature sizes, duplex tumble/work-and-turn-like abstract orientation modes, nesting order, partial signatures, inserts, gatefold-like bounded exceptions, facing-spread constraints, page groups that must stay on one sheet, trim-loss zones and production limits such as "two inks only on sheet B." Do not simulate real print-shop minutiae; each added rule must change the permutation/constraint problem.

### Dominant-strategy / exhaustive-search attack
**Attack:** a knowledgeable player may derive a fixed imposition formula and apply it mechanically to every booklet.

**Defense requirement:** authored cases must vary fold graph, sheet count, nesting, orientation and secondary constraints enough that no single formula solves all. The UI may teach mappings, but late cases need constraint intersections where page order alone has multiple valid layouts and another requirement selects among them.

**Attack 2:** brute-force all page permutations is combinatorial and impossible manually, but solver can do it; human play could become tedious swapping.

**Defense:** provide structured operations (pairs/quads, rotate sheet, swap leaf pair) after tutorials without automating the reasoning. Avoid 32-page busywork; mature depth should arise at 8–20 logical page faces.

### Solver / validator feasibility
Excellent. Model each fold/signature as a deterministic permutation plus orientation transform. A case is a constraint satisfaction problem over page assignments, sheet selection and nesting. Exact solver can enumerate legal layouts, count solution classes, test uniqueness where desired and detect redundant constraints. No physics required.

### Content / asset model
Very efficient. Page faces can use icons, numbers, color blocks and small motif families rather than bespoke readable text. Cases are data. One table-scale 3D/2.5D apparatus can animate folding for presentation.

### 15–30 minute demo spine
- 4-page single sheet: discover that flat order is nonintuitive.
- duplex orientation twist.
- 8-page nested signature.
- facing-spread constraint.
- capstone: two sheets, one insert requirement, more than one order-correct arrangement but only one satisfying all constraints.

### Nearest-current-analogue differentiation
`Bookbinding – Dark Cozy Sim` uses book craft as setting with cover decoration, customers and narrative. Binder's Imposition must explicitly market **"lay out the flat sheets so the folded book becomes correct"**, preferably with a GIF that alternates flat sheet -> fold -> readable sequence. Generic bookbinding visuals alone are collision-prone.

### Portfolio collision attack
No prior game centers a known permutation produced by fold/nest transforms. There is no property transfer, topology rewiring, remembered form, hidden audio geometry or destructive key-vector authority. Safe.

### Empirical kill gate
Kill if first-time players still cannot predict a simple fold's result after 15 minutes with physical animation, or if mature play degenerates into repeated fold-preview/swap without players forming a mental model.

### Run-1 verdict
**SURVIVE.** Probably the field's safest exact mechanical puzzle; tutorial burden is its main risk.

---

## G9C03 — Kiln Stack

### Mature-case walkthrough
Six ceramic pieces occupy a small kiln rack. Each has glaze family, support requirement and heat band. A three-step firing schedule changes heat class by rack region. Nearby pieces can shade heat, supports conduct a bounded class, and some glaze classes migrate to adjacent exposed surfaces under the high-fire step. Objectives demand final finish class and defect avoidance on every piece.

### Minute-to-minute loop
Pack pieces/supports, choose schedule, preview coarse heat classes, fire, inspect deterministic transformations, adjust.

### Hour-8 depth claim
Could add refractory shelves, support contacts, glaze compatibility, multi-stage heat schedules and sacrificial test pieces. However, each layer trends toward a multi-object cascade simulator.

### Dominant-strategy / exhaustive-search attack
If all outcomes can be previewed before firing, the puzzle risks becoming arrangement enumeration. If preview is restricted, failure feels opaque because heat/glaze interactions are spatial and delayed. Adding uncertainty would violate desired deterministic authority.

### Solver / validator feasibility
Possible only after aggressive discretization: fixed rack cells, discrete heat propagation, finite schedule cards, categorical glaze migration. But once discretized enough for solver safety, much of the pottery fantasy becomes a thematic skin on a neighborhood cellular system.

### Content / asset model
Rack/pieces are reusable, but convincing pottery shape/glaze/fire presentation requires more 3D/material work than several rivals. Content variety also pressures bespoke shapes.

### 15–30 minute demo spine
Packing -> heat shadow -> support conduction -> glaze migration. It can work, but needs more explanation than its GIF suggests.

### Nearest-current-analogue differentiation
Double Fine's `Kiln` makes pottery highly visible in 2026 and ties pot shape to gameplay. Our puzzle is different, but the store-page comparison would force immediate explanation. Generic VR `Pottery` also simulates forming/firing/glazing. Theme is therefore occupied.

### Portfolio collision attack
High concern with #001 Organism Cargo: arrange multiple entities in a constrained chamber, commit a process, then deterministic local interactions/cascades resolve across neighbors. The nouns differ but the planning rhythm is dangerously similar.

### Empirical kill gate
Would require a prototype proving players perceive kiln-specific strategic reasoning rather than "Organism Cargo with ceramics" and that discrete heat rules remain intuitive.

### Run-1 verdict
**KILL.** Automatic portfolio-collision concern plus greater presentation/validation burden. Do not rescue by adding more simulation.

---

## G9C05 — Stained Glass Noon

### Mature-case walkthrough
A fixed window lattice has 10–16 slots. The player owns glass pieces with discrete hue/transmission classes and optional one-step prism direction. At three named sun positions (morning/noon/evening), each slot projects onto a deterministic floor-cell offset. Overlapping projected colors combine through a tiny lookup table. The same installed window must produce a red emblem at morning, leave a central aisle bright at noon, and create a blue border at evening. Some thick glass shifts the projected cell one extra step at shallow sun angles.

### Minute-to-minute loop
1. inspect the three target tableaux;
2. scrub sun position among authored checkpoints;
3. place/swap/rotate glass pieces in the fixed lattice;
4. watch deterministic projection update instantly;
5. compare all checkpoints, not only current time;
6. commit when every checkpoint satisfies its target.

### Hour-8 depth claim
Depth comes from one placement serving several time-indexed outputs. Later vocabulary: discrete transmission, overlap mixing, one-step refractive offset, opaque lead-frame blockers, paired pieces, limited stock, cells that must be lit at one time and dark at another. Keep sun positions discrete authored checkpoints; no continuous ray-tracing puzzle authority.

### Dominant-strategy / exhaustive-search attack
**Attack:** optimize each time target independently.

Fails by construction because one physical arrangement produces all times. Mature cases must have placements that improve one time while harming another.

**Attack 2:** brute-force all pieces in all slots.

State count can be large, but human trial-and-error may still dominate if feedback is only final images. UI should show per-time mismatches and let players scrub instantly; the intellectual task is reconciling conflicts, not waiting for animation.

### Solver / validator feasibility
Strong if represented as discrete projection matrices. Each slot/piece/orientation contributes deterministic outputs at K time checkpoints; overlap resolves by finite table. Exact-cover/SAT/CP-SAT or DFS with constraint propagation can validate cases and count solutions. Rendering can use richer lighting while logical authority remains a grid.

### Content / asset model
One reusable window frame, glass material palette, projection plane and motif library. Targets can be procedural/geometric rather than bespoke illustration. Case data: lattice, inventory, time checkpoints, targets, allowed piece traits.

### 15–30 minute demo spine
- direct one-time color projection;
- second time reveals the same pane lands elsewhere;
- overlap mixing;
- thick pane shifts shallow-angle projection;
- capstone requires satisfying three times simultaneously.

### Nearest-current-analogue differentiation
`Glass Masquerade` owns stained-glass jigsaw imagery but not multi-time light projection. The store promise must be **"one window, several shadows/images across the day"** rather than assemble-a-pretty-window.

### Portfolio collision attack
No previous factory game uses one static arrangement evaluated under multiple externally indexed transforms. Avoid turning thick glass into a generic transferable property or topology system. Safe.

### Empirical kill gate
Kill if players solve representative mature cases by focusing on one time completely and then making only trivial swaps, or if discrete projection cannot look visually convincing without mismatching logical authority.

### Run-1 verdict
**SURVIVE.** Excellent GIF, clear second-order constraint, solver-friendly after deliberate discretization.

---

## G9C11 — Stage Cue Machine

### Mature-case walkthrough
A compact cue stack controls curtain A/B, two lifts and three light states. Each cue fires a bounded set of actions; physical state can enable/disable later cue types. The player must arrange/parameterize cues so six beat checkpoints match a script: actor reveal, blackout, platform raise, curtain cross, finale. One cue's effect can persist and make a later cue illegal.

### Minute-to-minute loop
Arrange cue cards -> scrub/rehearse timeline -> inspect checkpoint mismatch -> reorder/parameterize -> replay.

### Hour-8 depth claim
Interlocks, persistent stage states, simultaneous cues, reset/no-reset devices, conditional legality. But this quickly becomes a visual programming/state-machine puzzle.

### Dominant-strategy / exhaustive-search attack
The natural optimal behavior is repeatedly replaying the whole timeline after each edit. If the UI shows full deterministic timeline state, the player can reason—but the interaction becomes schedule debugging. If it hides state, debugging becomes tedious. Depth increasingly comes from program length rather than a fresh physical insight.

### Solver / validator feasibility
Excellent as finite-state planning, but that is also the warning: the theme may simply dress a generic planning/programming problem.

### Content / asset model
Reusable theater assets are manageable, but strong case identity may require bespoke mini-scenes/scripts/choreography, increasing presentation burden relative to pure data puzzles.

### 15–30 minute demo spine
Curtain + light -> persistent lift -> interlock -> multi-cue finale. Mechanically understandable, but visually the demo may read as "program the theater show."

### Nearest-current-analogue differentiation
`Impresario – Theater Tycoon` already advertises controlling lighting, scenery and entrances in real time. Professional cue software such as CueCart also makes cue-grid language familiar. Our finite puzzle differs, but fantasy differentiation is weaker than Run-1 leaders.

### Portfolio collision attack
No direct frozen-game clone. However, as abstraction increases it approaches the generic circuit/programming lane already identified as crowded in Phase 1.

### Empirical kill gate
Would need prototype players to describe the central fun as manipulating physical dependencies rather than debugging a sequence/program.

### Run-1 verdict
**KILL.** Safe to implement but insufficiently differentiated once stripped of theater spectacle; hour-8 depth trends toward generic programming.

---

## G9C15 — Mold Release

### Mature-case walkthrough
A stylized 3D object has required surface patches and forbidden seam patches. The player chooses 2–4 mold sections by assigning surface regions and withdrawal directions. Every required surface must be captured; each section must be able to move along its direction without intersecting the part or another still-locked section. Removing one section can free another, so release order matters.

### Minute-to-minute loop
Rotate object, place/adjust parting boundaries, assign pull direction, simulate extraction, inspect collision/undercut overlay, revise.

### Hour-8 depth claim
Multi-part molds, removable inserts, ordered extraction, protected seam regions, shared boundaries, asymmetric pull directions. There is genuine geometry depth.

### Dominant-strategy / exhaustive-search attack
Potential dominant strategy: make many tiny mold pieces, each with easy extraction. Must cap section count and impose seam constraints. Even then, player may search pull directions mechanically unless shapes teach reusable geometric reasoning.

### Solver / validator feasibility
This is the largest problem. A robust exact validator for arbitrary 3D region partition + continuous withdrawal collision is disproportionate. Restricting shapes to voxels and pull directions to six axes improves safety but substantially weakens the mold fantasy. Pre-authored surface patches plus finite candidate parting sets would be safer, yet then player agency becomes selecting designer-provided answers.

### Content / asset model
Every strong case needs a readable 3D object whose undercuts are intentional. Procedural generation is difficult to curate; authored geometry burden is materially higher than grid/permutation rivals.

### 15–30 minute demo spine
One-piece impossible mold -> split two ways -> extraction order -> seam restriction. Strong aha possible, but camera/3D literacy consume demo time.

### Nearest-current-analogue differentiation
`Virtual Foundry` now gives foundry/mold preparation an educational simulation presence. G9C15 would need to avoid realism claims while still teaching geometric release concepts—an awkward positioning boundary.

### Portfolio collision attack
No direct clone, but if implemented as region adjacency/partition editing it risks drifting toward topology manipulation; if implemented as directional property assignment it risks other portfolio abstractions. Not an automatic collision, just less clean.

### Empirical kill gate
Prototype must prove finite/discrete authority can produce the undercut aha without arbitrary 3D collision edge cases and without players demanding freeform mold geometry.

### Run-1 verdict
**KILL.** Great intellectual seed, wrong implementation/content risk for this factory cycle.

---

## G9C21 — Tailor's Grain

### Mature-case walkthrough
One finite patterned cloth rectangle contains a repeating motif and visible grain axis. The order requires four garment panels represented as compact polygons. Constraints: two panels are mirrored; all must align grain within allowed orientation; a pocket motif must center on a flower; two seam edges must meet with stripe phase alignment; one pair may be cut on bias but consumes a scarce bias allowance. Waste minimization is secondary, not the whole objective.

The player lays, flips only allowed patterns, rotates within grain rules, and chooses cut placement. Once all parts fit, a seam-preview pairs specified edges and exposes pattern continuation.

### Minute-to-minute loop
Inspect garment-piece constraints -> place/rotate/flip patterns on cloth -> toggle seam preview -> detect motif/grain conflicts -> repack -> cut/submit.

### Hour-8 depth claim
Grain classes, directional nap, mirrored pairs, stripe/check phase at seams, motif placement, limited bias exceptions, fold-cutting, cloth defects, pieces that must share motif phase, and small remnants that must remain usable for a specified accessory. Important: never turn game into raw bin-packing leaderboard.

### Dominant-strategy / exhaustive-search attack
**Attack:** pack largest pieces first or minimize waste greedily.

Mature cases must invalidate this through motif/seam/grain constraints. Some cases should have a lower-waste layout that fails the actual order and a slightly higher-waste correct layout.

**Attack 2:** grid-search every placement.

Use snap lattice and finite orientations so solver can validate, but cloth/piece sizes should make blind enumeration unpleasant enough that constraint reasoning dominates. UI should surface violated constraints immediately after placement, not after final cutting.

### Solver / validator feasibility
Good if logical geometry is orthogonal/polyomino-like or low-vertex polygons on a finite snap grid. Exact-cover/packing with orientation and edge-phase constraints is tractable at modest counts. Avoid freehand curves and arbitrary floating coordinates as authority.

### Content / asset model
Reusable cloth motif generators and a modest library of abstract panel silhouettes. Content cases mostly combine data constraints. Full clothing visualization is optional reward presentation, not required puzzle geometry.

### 15–30 minute demo spine
- grain-only placement;
- mirrored pair;
- stripe phase across seam;
- motif-centered pocket;
- capstone where perfect waste packing is wrong because seam phase conflicts.

### Nearest-current-analogue differentiation
`A Stitch In Time` and `The Great Couturier` occupy sewing/fashion fantasy, while `Sewing Stuff` foregrounds stitching tasks. Tailor's Grain survives only if its first GIF shows **pattern pieces competing for one patterned cloth under grain + motif + seam constraints**, not avatar tailoring or fashion customization.

### Portfolio collision attack
Potential weak resemblance to spatial packing in #001, but no post-commit entity cascade exists; layout is evaluated through geometric/material alignment constraints. Keep packing as substrate, not identity. Do not add transport, living objects or adjacency cascades.

### Empirical kill gate
Kill if representative players summarize optimal play as "Tetris to reduce waste" after the first hour, or if realistic garment-shaped pieces make exact snap-grid interaction feel visually dishonest.

### Run-1 verdict
**SURVIVE.** Strong constraint stack and low technical risk; differentiation must foreground grain/motif/seam, not sewing.

---

## G9C25 — Darkroom Layers

### Mature-case walkthrough
A print grid begins unexposed. The player has three masks, two exposure intensities and a limited sequence of passes. Exposure accumulates by cell; development maps accumulated exposure bands into tonal classes. Masks preserve selected regions while dodging/burning operations alter only bounded areas. The target needs several tonal regions while keeping one highlight below a threshold.

### Minute-to-minute loop
Choose mask -> preview covered region -> expose -> inspect accumulated exposure map -> swap mask/intensity -> continue -> develop/compare.

### Hour-8 depth claim
Mask composition, partial exposure, developer curves, local dodge/burn operations, paper grades and region protection. In principle deep, but all are variants of accumulated scalar field manipulation.

### Dominant-strategy / exhaustive-search attack
Once the development mapping and masks are known, many cases reduce to solving a monotone additive coverage problem. A player can often compute desired exposure per cell and decompose it into available mask passes. Irreversibility creates tension but does not necessarily create new interaction types.

Adding chemical cross-effects could solve this but would make C25 converge toward Ink Trap Press while retaining a less visually legible rule set.

### Solver / validator feasibility
Excellent: finite additive grid, masks, intensity values, pass budget. Unfortunately this also exposes thinness; solver form is close to bounded integer linear combination/set-cover.

### Content / asset model
Excellent and cheap. Target images/masks can be geometric.

### 15–30 minute demo spine
Direct exposure -> mask -> cumulative overexposure -> capstone. Clean but second-order twist is weaker than C01.

### Nearest-current-analogue differentiation
`Darkroom` (2025) uses development as narrative horror rather than systemic puzzle, so there is market space mechanically. Yet the darkroom fantasy has less immediate visual transformation than colored overprinting unless presentation is exceptional.

### Portfolio collision attack
More importantly, irreversible scalar accumulation under acceptance thresholds drifts uncomfortably toward #008's destructive-edit logic if target regions behave as finite acceptance bands. It is not a clone, but the structural distance is weaker than C01.

### Empirical kill gate
Would need evidence that late cases produce qualitative planning beyond additive mask decomposition without importing Ink Trap Press's interaction table.

### Run-1 verdict
**KILL in favor of G9C01.** Strong standalone seed, but internally redundant tournament lane; C01 contains the richer order-dependent material interaction and stronger GIF.

---

## G9C31 — Paper Automata

### Mature-case walkthrough
A hand-cranked paper drum has 12 angular ticks and four follower lanes. At each tick, each lane reads one of a finite surface states: low, high, ramp-up, ramp-down, or hole/drop. Followers drive four visible paper figures. The requested animation score specifies poses/events at selected beats plus transition restrictions: bird rises on beat 3, moon remains high beats 4–7, drummer strikes exactly on 2/6/10, fox ducks while bird crosses. Some punch/lobe shapes occupy adjacent ticks, so one choice constrains neighboring beats. A limited set of cutouts must be placed on the drum without illegal overlap.

### Minute-to-minute loop
1. inspect desired beat timeline and current drum;
2. place/remove/rotate one cam strip or punch element on a lane;
3. crank or scrub the drum;
4. watch followers and paper characters animate;
5. compare per-beat mismatches;
6. revise until the loop performs correctly.

### Hour-8 depth claim
Coupled followers, multi-tick cam elements, phase offsets, shared axle transforms, followers that invert or delay signals, sparse "must not move" beats, one actuator driving two characters through a small linkage, cyclic wrap-around constraints. Keep vocabulary finite and physical; do not become a general-purpose logic computer.

### Dominant-strategy / exhaustive-search attack
**Attack:** solve each lane independently from its target timeline.

Defense: mature cases include shared elements, spatial overlap on drum, phase budget or coupled linkage so lanes cannot be solved independently.

**Attack 2:** if every target beat translates directly into high/low cells, puzzle is just waveform painting.

Defense requirement: multi-tick element footprints and linkages must create indirect consequences; at least one mature family needs the correct actuator state to differ from the visible desired pose because linkage inversion/delay transforms it.

### Solver / validator feasibility
Excellent. Drum is cyclic finite grid; elements have footprints and state outputs; linkages are deterministic finite transforms. Constraint solver/DFS can validate existence, solution classes, independent-lane triviality and minimum number of shared/coupled decisions.

### Content / asset model
Very efficient mechanically. One drum rig and reusable paper-character parts. New puzzles mostly need target beat scripts and element inventories. Cosmetic automata can be composed from a small modular set rather than fully bespoke animations because the mechanism itself drives motion.

### 15–30 minute demo spine
- one lane/high-low follower;
- multi-tick ramp element;
- cyclic wrap-around;
- second follower sharing drum space;
- capstone introduces one linkage inversion so solving visible pose directly fails.

### Nearest-current-analogue differentiation
Current puppet games (`Once Upon A Puppet`, `Myrmidon`) use puppetry in platform/adventure contexts, not cam-drum construction. Broad mechanical-puzzle games exist, so store language must show the paper drum causing a looping performance in the same shot.

### Portfolio collision attack
Potential generic-programming risk: drum = program, followers = outputs. This is not a prior frozen-game collision, but Phase 1 already marks generic programming as saturated. Survival condition is that physical footprints, cyclic geometry and coupled linkages remain the reasoning substrate; avoid conditional logic, gates, variables or textual code.

### Empirical kill gate
Kill if mature prototypes can be solved lane-by-lane or players describe the drum as merely "a programming grid with cute animation." At least half of mature cases must require cross-lane/cyclic physical reasoning.

### Run-1 verdict
**SURVIVE.** Very strong implementation/content profile and demo spectacle; generic-programming drift is the key Run-2 attack.

---

## G9C33 — Coin Strike

### Mature-case walkthrough
A coin blank is represented by finite relief cells. Several die faces each add/compress relief in a known footprint; rotation changes footprint alignment; strike strength chooses one of discrete transformation magnitudes. A later strike can flatten earlier raised detail in overlapping regions. Target requires relief bands plus protected details.

### Minute-to-minute loop
Select die -> rotate -> choose strength -> preview direct footprint -> strike -> inspect relief -> repeat under strike budget.

### Hour-8 depth claim
Multi-stage obverse/reverse interactions, anneal-like resets, edge constraints, overlapping relief and protected microdetails could add complexity.

### Dominant-strategy / exhaustive-search attack
Finite die/rotation/strength branching makes bounded search straightforward. To prevent greedy play, later strikes must damage earlier work. But that exact fix makes the structural resemblance to #008 stronger: irreversible discrete edits under acceptance ranges, where each commit can destroy future feasibility.

### Solver / validator feasibility
Excellent finite grid/vector transition system.

### Content / asset model
Efficient. Relief targets/dies are data and shader/mesh displacement can present results.

### 15–30 minute demo spine
One strike -> overlap damage -> rotation -> capstone with protected earlier relief. Strong tactile spectacle.

### Nearest-current-analogue differentiation
Minting/crafting titles exist and the name itself is noisy (`CoinForge`, multiple "Coin Strike" results). A new title could solve naming, but not the portfolio issue.

### Portfolio collision attack
**Fatal.** The core decision rhythm is too close to Game #008: choose a discrete irreversible transformation on a persistent object, observe target acceptance/damage, and preserve enough remaining option space for later requirements. Replacing key depth columns with relief cells and files with dies is not enough structural distance.

### Empirical kill gate
Not needed; portfolio exclusion is decisive.

### Run-1 verdict
**KILL — portfolio collision with #008.** Preserve only as exclusion history.

---

# 5. Run-1 comparative score after destruction

| ID | Concept | H | M | D | A | SV | I | C | Demo | Market | Portfolio | Total / 50 | Verdict |
|---|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---|
| G9C01 | Ink Trap Press | 5 | 5 | 5 | 4 | 5 | 4 | 5 | 5 | 5 | 4 | **47** | **SURVIVE** |
| G9C02 | Binder's Imposition | 5 | 5 | 5 | 4 | 5 | 5 | 5 | 5 | 4 | 5 | **48** | **SURVIVE** |
| G9C03 | Kiln Stack | 5 | 4 | 4 | 3 | 3 | 3 | 4 | 4 | 2 | 1 | **33** | KILL |
| G9C05 | Stained Glass Noon | 5 | 5 | 5 | 4 | 5 | 4 | 5 | 5 | 4 | 5 | **47** | **SURVIVE** |
| G9C11 | Stage Cue Machine | 4 | 4 | 4 | 3 | 5 | 5 | 4 | 4 | 3 | 5 | **41** | KILL |
| G9C15 | Mold Release | 5 | 5 | 5 | 4 | 2 | 2 | 2 | 4 | 4 | 4 | **37** | KILL |
| G9C21 | Tailor's Grain | 5 | 5 | 5 | 4 | 5 | 5 | 5 | 5 | 4 | 4 | **47** | **SURVIVE** |
| G9C25 | Darkroom Layers | 5 | 4 | 3 | 3 | 5 | 5 | 5 | 4 | 4 | 3 | **41** | KILL |
| G9C31 | Paper Automata | 5 | 5 | 5 | 4 | 5 | 5 | 5 | 5 | 5 | 5 | **49** | **SURVIVE** |
| G9C33 | Coin Strike | 5 | 4 | 4 | 3 | 5 | 5 | 5 | 5 | 3 | 1 | **40** | KILL |

Scores are decision support, not arithmetic canon. C11 scores respectably but is killed because its durable depth trends toward generic programming and its theater fantasy has a fresh adjacent market occupant. C25 is killed as an internally redundant weaker lane beside C01. C33 is killed despite technical strength because the portfolio collision is structural.

---

# 6. Exactly five survivors

## S1 — G9C31 Paper Automata
Why alive: best combined solver safety, content efficiency, physical spectacle and mature coupling potential. Biggest remaining threat: it may secretly be a programming grid.

## S2 — G9C02 Binder's Imposition
Why alive: precise transformation puzzle, unusually strong validation model, very low production risk. Biggest remaining threat: tutorial opacity / specialist-domain feel and fixed-formula mastery.

## S3 — G9C01 Ink Trap Press
Why alive: richest compact irreversible/spatial interaction and excellent tactile feedback. Biggest remaining threat: free preview + small branching could make play feel like trial-and-error; must prove anti-greedy cases.

## S4 — G9C05 Stained Glass Noon
Why alive: one arrangement evaluated across multiple sun checkpoints is a clean second-order hook with excellent GIF potential. Biggest remaining threat: discrete logical optics may look less convincing than rendered optics or cases may decompose too easily.

## S5 — G9C21 Tailor's Grain
Why alive: multiple intuitive constraints can defeat pure packing and produce strong finite solver cases. Biggest remaining threat: player perception collapses to "fabric Tetris" or store page reads as generic sewing/fashion sim.

Killed in Run 1:
- G9C03 Kiln Stack — #001 structural collision + current `Kiln` market pressure + sim burden.
- G9C11 Stage Cue Machine — generic-programming depth and current theater cue/management adjacency.
- G9C15 Mold Release — disproportionate 3D validator/content burden.
- G9C25 Darkroom Layers — additive thinness and internal redundancy versus Ink Trap Press.
- G9C33 Coin Strike — fatal structural collision with Game #008.

No killed concept is canon for Game #009.

---

# 7. Run-2 requirements — 5 -> 3

The next run must not simply rescore these five. Build one representative mature-case specification for each, then attack it concretely.

For **every survivor**, Run 2 must produce:
1. exact finite state vocabulary and proposed authority representation;
2. one tutorial case and one hour-8 mature case with all data small enough to hand-simulate;
3. at least two complete legal player traces for the mature case (one can fail), showing why decisions matter;
4. explicit greedy/exhaustive baseline and whether it trivializes the case;
5. estimated solver search size and pruning strategy;
6. content-family sketch with at least 6 distinct case families that are not mere parameter inflation;
7. 20–30 minute demo beat sheet and first store-GIF claim;
8. implementation prototype spike needed to falsify the concept, but **no production implementation in factory**;
9. market-position sentence that does not use profession/craft theme as the sole hook;
10. portfolio-exclusion re-check.

### Specific attacks
- **Paper Automata:** prove cross-lane coupling is intrinsic enough that it is not waveform painting/programming.
- **Binder's Imposition:** prove players can build a mental model without memorizing one imposition formula or drowning in page-orientation bookkeeping.
- **Ink Trap Press:** prove deterministic one-step preview does not make brute-force/greedy play dominant.
- **Stained Glass Noon:** prove multi-time constraints create planning rather than simply independent target matching.
- **Tailor's Grain:** prove grain/motif/seam constraints dominate waste-packing identity.

Run 2 should reduce **5 -> exactly 3 finalists**. Product Thesis remains unlocked until after finalists receive a final head-to-head unless evidence makes one concept decisively superior and the status explicitly records why.

---

## 8. Run-1 conclusion

**PHASE 2 TOURNAMENT RUN 1 COMPLETE: 10 -> 5.**

Survivors: `G9C31 Paper Automata`, `G9C02 Binder's Imposition`, `G9C01 Ink Trap Press`, `G9C05 Stained Glass Noon`, `G9C21 Tailor's Grain`.

Selected Game #009 concept remains **NONE**.
