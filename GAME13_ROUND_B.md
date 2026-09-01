# GAME #013 — PHASE 2 CONCEPT TOURNAMENT / ROUND B

Date: 2026-09-01
Status: ROUND B COMPLETE — 5 -> 3 finalists; no winner selected.
Authority context: `GAME13_RESEARCH.md` + `GAME13_TOURNAMENT.md` remain historical tournament evidence; this file is the Round-B authority.

## Method
Round B attacks the five survivors under finite, machine-enumerable diagnostics. The goal is not to reward the puzzle with the largest state count. A survivor must show deductions that remove large classes of actions before guessing, and must plausibly produce six escalating demo cases without introducing unrelated mechanics.

All diagnostics below are throwaway design evidence, not canonical production levels or code. Coordinates are zero-based where used. Search counts are naive legal candidate configurations before goal pruning unless explicitly stated.

## Verdict summary

| Candidate | Diagnostic space | Solution result | Human deduction quality | Six-case same-vocabulary escalation | Collapse attack | Round-B verdict |
|---|---:|---:|---|---|---|---|
| Carbon Copy | 12 x 12 x 9 = **1,296** | **1 exact configuration** | strong inverse receiving-layer + footprint deductions | PASS | transfer-depth matrix resisted only when footprints overlap/couple | **FINALIST** |
| Margin Call | **441** admissible rectangles | **1 rectangle** for diagnostic signature | real but quickly becomes boundary candidate elimination | technically PASS | core remains finite rectangle enumeration / submatrix classification | **KILL** |
| Seal Break | C(10,5) x 4! = **6,048** setups | **1 setup/order** for exact temporal signature | strong break-time / survivorship / order deductions | PASS | temporal identity defeats pure set cover | **FINALIST** |
| Blind Staple | 5! x C(6,2) = **1,800** raw configurations | **2 equivalent solutions** differing only in irrelevant bottom-two order | strong penetration-band + adjacency deductions | PASS | factorial surface collapses into position bands when authored correctly | **FINALIST** |
| Transfer Window | 5^5 = **3,125** shift sequences | **7 sequences** under two ownership checkpoints + final target | some inverse ownership reasoning, but sequence equivalence remains large | borderline | offset-history enumeration remains the natural solver | **KILL** |

Round B therefore reduces **5 -> 3**: **Carbon Copy, Seal Break, Blind Staple**.

---

# A. Carbon Copy — FINALIST

## B diagnostic A3 — three coupled footprints
Board: aligned 4x4 sheets A/B/C. Every press is made on A. For each footprint cell, the mark appears on A and travels downward. If B at that coordinate is non-carbon, B receives the mark and the ray stops. If B is carbon and C is non-carbon, C receives the mark and the ray stops. If B and C are both carbon, no lower writable sheet receives it. Marks are set-valued for this diagnostic; repeated marking does not create a new mark.

Sheet B carbon cells:
`{(0,0),(0,3),(1,1),(1,2),(2,0),(3,0),(3,2),(3,3)}`

Sheet C carbon cells:
`{(1,1),(1,2),(1,3),(2,2),(3,3)}`

Inventory, each used exactly once:
- H2: horizontal domino, 12 legal placements;
- V2: vertical domino, 12 legal placements;
- L3: cells `(0,0),(1,0),(1,1)` in its fixed orientation, 9 legal placements.

Goal lower-sheet mark sets:
- B exactly `{(0,2),(1,0),(1,3),(3,1)}`;
- C exactly `{(0,0),(3,2)}`.

Exhaustive enumeration over `12*12*9 = 1,296` placement triples yields **one** exact configuration:
- H2 = `{(3,1),(3,2)}`;
- V2 = `{(0,0),(1,0)}`;
- L3 = `{(0,2),(1,2),(1,3)}`.

## Human deductions before guessing
1. C requires `(0,0)` and `(3,2)`. A cell can reach C only where B is carbon and C is writable. This immediately turns those two coordinates into required footprint coverage while many B-target cells must instead stop one layer earlier.
2. C `(3,2)` and B `(3,1)` are adjacent on the bottom row; H2 is the only inventory footprint that can cover that exact mixed-depth pair in one placement without introducing another required lower mark. This strongly fixes H2 at `(3,1)-(3,2)`.
3. C `(0,0)` plus B `(1,0)` align vertically and force V2 to the first column. The alternative of supplying them through L3 would necessarily expose an extra neighbor footprint and conflicts with the remaining B target.
4. The remaining B targets `(0,2),(1,3)` together with B-carbon `(1,2)` match the L3 footprint at top-left `(0,2)`, forcing the final placement.

These deductions recover the unique solution by required receiving depth and inventory geometry rather than testing 1,296 triples.

## Transfer-depth-matrix attack
Failure mode remains real: if all stamps are 1x1, or if target requirements decompose by cell, each board coordinate is merely a lookup `B/C/none`. The diagnostic survives because a single multi-cell footprint must simultaneously satisfy cells that stop at different depths, and the scarce footprint inventory couples those coordinates.

**Hard content gate if selected:** every non-tutorial case must include at least two multi-cell footprints whose cells have mixed transfer outcomes, plus either overlap/no-duplicate pressure, scarce footprint identity, or one bounded sheet-order decision. A case solvable as independent per-cell depth lookup is invalid content.

## Plausible content families
1. mixed-depth footprint fitting — **real new reasoning**;
2. scarce stamp inventory where only one footprint can cover a mixed-depth pair — **real**;
3. overlap/no-duplicate targets, where two otherwise-correct stamps interfere — **real**;
4. one bounded pre-press sheet reorder among 3 sheets — **real but higher tutorial cost**;
5. required vs forbidden marks on lower sheets — useful predicate variation, **not depth by itself**;
6. larger 4x5/5x5 boards — **parameter inflation unless paired with coupling**;
7. additional stamp shapes — dangerous content inflation; only add if they create a qualitatively new footprint deduction.

## Six-case demo escalation
1. one domino, two sheets: show pass-through vs stop;
2. one domino crossing two transfer depths;
3. two different footprints, exact lower targets;
4. overlap/no-duplicate target forces ordering/placement interaction without new rule;
5. three sheets + three footprints, mixed-depth inverse deduction;
6. compact A3-style capstone with one optional bounded layer-order choice only if playtest proves readable.

Verdict: **FINALIST**. Hook, visual causality, inverse deductions and compact deterministic implementation all remain strong. Biggest threat is flat-layer presentation similarity to #009; Round C must compare portfolio identity explicitly rather than relying on theme.

---

# B. Margin Call — KILL

## B diagnostic B3 — boundary-role signature
Grid: 8x8 immutable sheet. A crop is one axis-aligned rectangle of at least 3 rows and 3 columns. There are
`sum_{h=3..8}(9-h) * sum_{w=3..8}(9-w) = 21*21 = 441`
admissible rectangles.

Labels:
- A=(1,1)
- B=(1,5)
- C=(3,3)
- D=(5,1)
- E=(5,5)
- F=(6,3)
- G=(2,6)
- H=(6,6)

Role of a retained label is CORNER if on both crop boundaries, EDGE if on exactly one, INNER otherwise; a removed label is OUT.

Target role signature in A..H order:
`INNER, EDGE, INNER, EDGE, CORNER, OUT, OUT, OUT`.

Exhaustive enumeration of all 441 admissible rectangles yields **one** crop: rows `0..5`, columns `0..5`.

## Human deductions
1. E must be CORNER at `(5,5)`, so row 5 and column 5 are both crop boundaries.
2. A and C must be INNER, forcing top <1, left <1 and bottom/right beyond their coordinates. With finite zero-based grid, top=0 and left=0.
3. F/G/H must be OUT while B/D remain EDGE; once bottom=5/right=5 from E, their status is explained without testing alternate rectangles.

## Why this still fails
The deductions are clean, but they are deductions **about the four rectangle coordinates**. Every proposed family ultimately adds predicates that narrow `(top,bottom,left,right)`. Even a larger board remains a tiny `O(r^2 c^2)` candidate set, and the player's natural fallback is to drag the crop through plausible rectangles while watching badges update.

Attempts to prevent brute force — hiding live role feedback, adding exact counts, aspect constraints, neighbor/run predicates — either make interaction less pleasant or decorate the same rectangle-enumeration object. The six-case demo can escalate rules, but hour-10 depth would depend on denser predicate bookkeeping rather than a second-order system.

## Content-family audit
1. corner/edge/interior identity — core but same reasoning;
2. retain/remove labels — simpler version of same;
3. neighbor-count after crop — new predicate, not new action interaction;
4. row/column visible-run length — more bookkeeping;
5. grouped labels sharing a role — constraint density only;
6. fixed aspect/area crops — restricts enumeration further;
7. multiple crops — would be a new mechanic and risks region/topology territory.

## Six-case demo test
A six-case demo is easy to author, but escalation would read as “more conditions on the same rectangle” by cases 4–6. That is precisely the parameter-inflation failure the tournament is designed to reject.

Verdict: **KILL**. Excellent 10-second hook and tutorial, insufficient second-order depth. Do not revive by adding many predicate types.

---

# C. Seal Break — FINALIST

## B diagnostic D3 — temporal evidence, placement + opening order
Compartments: A/B/C/D. There are 10 candidate seal sockets. A selected seal breaks irreversibly at the first checkpoint whose opened compartment belongs to that seal's crossing set.

Crossing sets:
- s1={A}
- s2={B}
- s3={C}
- s4={D}
- s5={A,B}
- s6={B,C}
- s7={C,D}
- s8={A,D}
- s9={A,C}
- s10={B,D}

Player selects exactly 5 of 10 seals and chooses a permutation in which all four compartments are opened. Raw setup space is `C(10,5)*4! = 252*24 = 6,048`.

Target temporal evidence is expressed as exact first-break checkpoints:
- s1 breaks at checkpoint 1;
- s2 breaks at checkpoint 2;
- s3 breaks at checkpoint 3;
- s4 breaks at checkpoint 4;
- s5 breaks at checkpoint 1;
- no other seal is installed.

Exhaustive enumeration yields **one** setup:
- installed `{s1,s2,s3,s4,s5}`;
- opening order `A,B,C,D`.

This exact diagnostic intentionally uses transparent crossing sets so the anti-collapse property can be inspected rather than hidden behind a decorative cabinet.

## Human deductions
1. A single-compartment seal breaking at checkpoint 4 identifies the last opened compartment immediately: s4 -> D last. Likewise s3 at checkpoint 3 forces C into position 3 after later positions are excluded.
2. s1 at checkpoint 1 and s5={A,B} also at checkpoint 1 jointly force A first: if B were first, s1 would survive checkpoint 1.
3. With A first, C third, D fourth, B is forced second and all target break times follow. The five selected seal identities are also explicit from evidence; no set-cover search remains.
4. More generally, a multi-seam seal's break time is a `min()` over the opening positions of its crossing set. Intersections between single- and multi-seam evidence produce precedence deductions rather than mere coverage counts.

## Set-cover/scheduling attack
If the target were only a final broken-set or count, the mechanic would be set cover. If the player merely permuted doors against independent deadlines, it would be generic scheduling. What survives is **identity-rich destructive evidence through time**: a seal spanning several routes records whichever qualifying opening happened first, so one witness constrains relative order of multiple compartments and interacts with other witnesses.

**Hard content gate if selected:** substantive cases must have at least two checkpoints and at least two multi-crossing seals whose break times interact with single-crossing or overlapping witnesses. Final-state-only cases are tutorial-only.

## Plausible content families
1. single + multi-crossing witness triangulation — **real**;
2. choose K seals before a fixed opening sequence — **real inverse placement**;
3. fixed seals, choose opening order — **real temporal deduction**;
4. choose both bounded seal subset and bounded opening order — **real coupling**;
5. seals sharing one seam but diverging on another — **real witness discrimination**;
6. one compartment that can be intentionally left unopened — **real survivorship deduction**;
7. larger seal counts alone — parameter inflation;
8. arbitrary seal strengths/colors — reject unless they alter a core deduction, not just alphabet size.

## Six-case demo escalation
1. one seal across one door: opening tears it;
2. two seals, one spans two compartments: first-open semantics;
3. fixed opening order, choose which seals produce a two-checkpoint evidence card;
4. fixed seals, choose among 3 opening orders;
5. overlapping multi-crossing witnesses infer relative order without trial;
6. compact choose-seals + choose-order capstone with 3–4 checkpoints.

Verdict: **FINALIST**. It kept the strongest physical/GIF hook while Round B demonstrated a true temporal reasoning object beyond set cover. Round C must check whether repeated “infer order from first break” becomes formulaic and whether evidence UI remains immediately legible.

---

# D. Blind Staple — FINALIST

## B diagnostic J3 — five-layer packet with mixed penetration depths
Layers: A/B/C/D/E, all visible before commit. Player chooses one stack permutation and an unordered pair of distinct staple sockets among U/V/W/X/Y/Z.

Socket penetration depths:
- U=2, V=3, W=2, X=3, Y=2, Z=3.

A socket is legal only if every penetrated layer is safe at that socket. Safe-layer sets:
- U: {A,B,D,E}
- V: {B,C,D,E}
- W: {A,B,C,D,E}
- X: {B,C,E}
- Y: {A,B,D,E}
- Z: {A,B,D,E}

A depth-2 staple binds positions 1–2. A depth-3 staple binds positions 1–2 and 2–3. No staple affects lower positions. Raw configuration space is `5!*C(6,2)=120*15=1,800`; 500 configurations are puncture-legal under the safety matrix.

Target:
- use U and V;
- at U, the bound pair is D-E;
- at V, bound pairs are D-E and E-B (therefore E is the shared middle layer of the depth-3 penetration chain);
- all punctures must be legal.

Exhaustive enumeration yields **2** solutions:
1. D,E,B,A,C
2. D,E,B,C,A

The two solutions differ only by swapping bottom positions 4–5, which no chosen staple reaches. They are mechanically equivalent; the meaningful top-three band is uniquely `D,E,B`.

## Human deductions
1. The V target contains two adjacent bindings sharing E. With depth 3, E must be the middle penetrated layer; D and B must occupy positions 1 and 3 in some order.
2. U is depth 2 and must bind D-E, eliminating `B,E,D` and forcing the top pair specifically to be D,E. Thus the top three are `D,E,B` before considering A/C at all.
3. Socket legality independently confirms U can puncture D/E and V can puncture D/E/B, while X cannot serve as a substitute because D is unsafe there. Large socket classes disappear from inspection, not permutation testing.
4. Bottom A/C order is provably irrelevant to the chosen staples. Treating the two exhaustive solutions as an equivalence class is a feature: the game should judge required binding/evidence, not demand arbitrary hidden order.

## Factorial-collapse attack
Raw permutations grow factorially, but good content exposes **position-band constraints**. A required depth-2 binding fixes the top pair; a depth-3 chain constrains the top three; visible safe/unsafe socket matrices rule layers out of penetration bands. The human object is therefore “which layers can occupy which penetration bands?” rather than “try 120 permutations.”

However, cases with no such band deductions are invalid even if a certifier can brute-force them.

**Hard content gate if selected:** cap at <=6 layers; every substantive case must permit at least three visible band/adjacency eliminations before any residual permutation guess. Never require arbitrary ordering of layers below all staple depths.

## Plausible content families
1. depth-2 pair binding — tutorial/core;
2. depth-3 shared-middle chain — **real new reasoning**;
3. two sockets with incompatible safety sets — **real**;
4. required and forbidden pair bindings — **real**;
5. “must remain unpunctured” layer as a band exclusion — **real**;
6. one staple socket chosen from several versus fixed sockets — **real choice coupling**;
7. 5 -> 6 layers — parameter inflation unless extra layer participates in a depth band;
8. layer rotations — reject by default; risks #009 flat-sheet transform collision and unnecessary search.

## Six-case demo escalation
1. three layers, depth 2, bind one required pair;
2. safe/forbidden puncture zones eliminate a top layer;
3. four layers, depth 3, shared-middle binding chain;
4. choose one of several sockets using visible safety sets;
5. two staples of depths 2 and 3 create intersecting top-band constraints;
6. five-layer J3-style capstone where bottom-order equivalence is accepted rather than overconstrained.

Verdict: **FINALIST**. Round B directly defeats the “factorial permutation” objection when content is authored around penetration-band deductions. Remaining risks: flat-layer aesthetic adjacency to #009, and whether staple/socket visuals can stay pleasant rather than medical/industrial.

---

# E. Transfer Window — KILL

## B diagnostic K3 — five-transfer offset history
Two cyclic strips of length N=8.
- A holes: {0,1,2}
- B local holes: {1,5,6}
- starting token ownership: token@0=A, token@1=B, token@2=A, token@7=B.

B has an alignment offset. Each of five turns chooses delta from `{-2,-1,0,+1,+2}`, updates offset modulo 8, then TRANSFER occurs automatically. At a world position where A has a hole and shifted B also has a hole, a token there switches strip ownership. Token identity/position is conserved; only owner changes.

Raw input-sequence space is `5^5 = 3,125`.

Diagnostic target uses an ownership checkpoint after transfer 2, another after transfer 4, and exact final ownership. Exhaustive enumeration found **7** satisfying delta sequences for the sampled evidence signature, including:
- `(-2,0,0,+1,0)`
- `(-2,0,+1,-1,+1)`
- `(-1,0,-1,+1,0)`
- `(-1,0,0,-1,+1)`
- `(0,0,-2,+1,0)`
- `(0,0,-1,-1,+1)`
- `(+1,0,-2,-1,+1)`

The multiplicity is not inherently a flaw, but inspection shows that distinct control sequences frequently collapse to the same useful coincidence/ownership history.

## Human deductions
1. A token that must switch owner at a checkpoint requires its coordinate to be a coincident opening at that transfer; a token that must stay must avoid coincidence. This prunes offsets directly.
2. Conservation means the only way to alter final owner is an odd number of coincidences for that token; required final ownership gives parity information about its transfer opportunities.
3. Checkpoints can prevent a locally-good transfer that would later be undone, so multi-step reasoning is real.

## Why this still fails
After those deductions, the natural remaining representation is a short sequence of modular offsets. Multiple delta sequences produce the same relevant alignment state, and adding more turns primarily increases path enumeration rather than the vocabulary of deductions. Checkpoints help only by specifying more of the desired path, which approaches scheduling-by-offset.

A UI that continuously previews coincident holes makes brute force especially tempting; hiding that feedback harms the tactile hook. Adding a third strip could create more coupling, but that is a substantial new system introduced solely to rescue depth and would increase readability burden.

## Content-family audit
1. asymmetric hole patterns — parameter variation;
2. two/three transfer budgets — sequence length variation;
3. checkpoint ownership — stronger constraint but same offset object;
4. forbidden return of a token — parity/path constraint;
5. fixed starting offset — baseline;
6. chosen starting offset — more enumeration;
7. third strip — genuine new coupling, but too large a rescue mechanic for tournament survival.

## Six-case demo test
Cases 1–3 teach alignment, transfer and conservation well. Cases 4–6 necessarily become longer offset histories/checkpoints unless a third strip appears. That is not enough same-vocabulary qualitative escalation.

Verdict: **KILL**. Excellent kinetic GIF, but the Round-B evidence confirms the feared offset-sequence brute-force identity. Do not rescue it with a third strip inside this tournament.

---

# Round-B finalist comparison

## Carbon Copy
Best qualities: most immediately magical causal transformation, clean deterministic 2D implementation, strong inverse spatial deductions, very marketable animation.
Main risk: without strict footprint coupling it is a transfer-depth matrix; visually it also lives near “stacked sheets” portfolio territory despite different mechanics.

## Seal Break
Best qualities: strongest destructive temporal storytelling, evidence states are memorable, Round B demonstrates precedence reasoning through irreversible witness break times.
Main risk: repeated cases could become the same `min(open-position)` deduction in different seam graphs; UI must communicate checkpoints without becoming a scheduling spreadsheet.

## Blind Staple
Best qualities: strongest proof that an apparently factorial problem can be converted into human band/adjacency deductions; tiny rule set, excellent certifiability, elegant acceptance of irrelevant lower-layer order.
Main risk: less broad visual appeal than Carbon Copy/Seal Break and flat packet presentation can aesthetically echo #009 even though the reasoning object is different.

# Round-B decision
**Advance exactly three finalists:**
1. Carbon Copy
2. Seal Break
3. Blind Staple

**Kill:** Margin Call, Transfer Window.

No winner is selected in Round B.

# NEXT — PHASE 2 ROUND C
Run an equal final tournament across the three finalists. Required evidence:
1. build a second hard diagnostic for each finalist that attacks the exact Round-B surviving weakness, not the same strength again;
2. compare hour-10 reasoning diversity using a 24–36-case hypothetical campaign map and reject candidates whose content families are cosmetic variants;
3. compare first-10-minute teachability and construct a six-case demo beatsheet with expected player deductions, not just rule introductions;
4. attack portfolio independence, especially Carbon Copy and Blind Staple versus #009's flat-layer identity;
5. attack Seal Break repetition by proving at least three qualitatively different temporal witness deductions beyond simple first-break ordering;
6. compare screenshot/GIF/trailer legibility, controller/Deck interaction burden, asset burden, certifier complexity and likely implementation risk;
7. choose exactly one winner only if evidence is decisive. If no finalist clears the bar, kill all three and return to a new concept field rather than forcing a weak Game #013.
8. If a winner is selected, begin Phase 3 Product Thesis Lock in the same run only if Round C is fully documented and the transition is safe. Do not start production implementation.
