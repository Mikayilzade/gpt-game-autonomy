# GAME #009 — PHASE 2 CONCEPT TOURNAMENT — RUN 2

Status: **RUN 2 COMPLETE / 5 -> 3 FINALISTS**
Date: 2026-08-31
Active slot: **Game #009 only**
Selected concept: **NONE**
Production implementation: **FORBIDDEN in factory**

Authority order for this run:
1. `START_HERE.md`
2. `STATUS.md`
3. `GAME_INDEX.md`
4. `GAME9_RESEARCH.md`
5. `GAME9_TOURNAMENT.md`
6. this file

Games #001–#008 remain portfolio/exclusion history only. This file does not import their mechanics into Game #009 canon.

---

## 1. Run-2 method

Run 1 used abstract destructive comparison. Run 2 requires finite, hand-simulatable cases. Each survivor receives:
- an exact logical state vocabulary;
- one tutorial case;
- one hour-8 mature case;
- at least two complete legal traces for that mature case, including one failure when useful;
- a greedy/exhaustive baseline attack;
- search-size and pruning estimate;
- at least six content families that alter reasoning rather than only scale numbers;
- a 20–30 minute demo spine;
- first store-GIF claim;
- current market-position sentence;
- a prototype falsification spike;
- a portfolio-exclusion re-check.

Ties break by implementation safety + mature depth + demo strength.

---

# 2. G9C31 — Paper Automata

## 2.1 Logical authority
A case contains a paper drum with `T` discrete angular ticks and `L` follower lanes. Each lane has one follower reading a binary lobe state `0/1` at the current tick. The player punches/removes lobes from a finite drum pattern before run. A follower edge transition may actuate a small deterministic linkage rule that can affect a second lane's effective read offset or gate state on later ticks.

Canonical state tuple:
`(tick, drum[L][T], gate_bits, lane_offsets, output_trace)`.

Allowed edit verbs before RUN:
- toggle one punch at `(lane,tick)` if that site is editable;
- rotate one lane by an allowed offset token;
- set one bounded coupling card between named lanes where the case permits it.

RUN is deterministic for exactly one cycle. No continuous physics is authority; animation is presentation of the finite trace.

## 2.2 Tutorial case P-T1
`T=4`, `L=1`; target follower trace `0,1,1,0`; player toggles exactly two sites. Direct solution: punches at ticks 1 and 2. Purpose: establish drum -> repeated trace without coupling.

## 2.3 Hour-8 mature case P-M1
`T=6`, `L=3`: A, B, C.

Fixed rules:
- A directly reads its drum lane.
- Rising edge on A opens gate `g` for exactly the next two ticks.
- B output = its drum bit only while `g=1`; otherwise 0.
- Rising edge on B increases C's read offset from `0` to `+1` for the remainder of the cycle.
- C reads its lane at `(tick + offset) mod 6`.

Editable sites:
- A: ticks {0,2,4}; choose exactly 2 punches.
- B: ticks {1,3,5}; choose exactly 2 punches.
- C: ticks {0,1,2,3,4,5}; choose exactly 2 punches.

Targets:
- A output: `1,0,1,0,0,0`
- B output: `0,1,0,1,0,0`
- C output: `0,1,0,0,1,0`

### Trace P-M1-SUCCESS
Edits: A punches {0,2}; B punches {1,3}; C punches {0,4}.

Tick 0: A rises -> `g` opens for ticks 1–2. B=0. C offset0 reads C0=1, but target C0=0: this raw placement appears wrong until we account for cycle initialization rule: tick0 output is sampled before edge side-effects and C lane is defined with presentation-phase inversion? That would introduce an ugly exception, so this trace exposes a specification flaw.

**Repair made inside Run 2:** remove same-tick ambiguity by defining strict order: `read raw bits -> emit outputs -> detect rising edges -> apply effects beginning next tick`. Re-author C target to match an exact trace instead of relying on phase tricks.

Repaired target C: `1,0,0,0,1,0`.

Now:
- t0: A1, B0, C1; A rising schedules gate for t1–t2.
- t1: A0, B1, C0; B rising schedules C offset +1 starting t2.
- t2: A1, B0, C0 (reads C3); A rising schedules gate t3–t4.
- t3: A0, B1, C0 (reads C4=1 would output 1, so C placement still conflicts).

Second repair: choose C punches {0,5}.
- t0 C1.
- t1 C0.
- offset+1 from t2: reads C3=0, C4=0, C5=1, C0=1 at t5 -> output `1,0,0,0,1,1`, still one extra.

This case is becoming bookkeeping-heavy. That is useful tournament evidence rather than something to hide.

A simpler valid coupled case is therefore used for final comparison:

### P-M1R — repaired mature case
`T=5`, A/B/C.
- A rising edge opens B gate for next tick only.
- B rising edge toggles C inversion for all subsequent ticks.
- strict order: outputs first; edge effects begin next tick.
Editable punches: A choose2 of {0,2,4}; B choose2 of {1,3,4}; C choose2 of {0..4}.
Targets: A=`1,0,1,0,0`; B=`0,1,0,1,0`; C=`1,0,1,1,0`.
Solution edits: A{0,2}, B{1,3}, C{0,2}.
Trace:
- t0 raw A1/B0/C1 -> outputs 1/0/1; A rise gates B at t1.
- t1 raw A0/B1/C0 -> outputs 0/1/0; B rise toggles C inversion from t2.
- t2 raw A1/B0/C1 -> C inverted =>0, which misses target C2=1.
So choose C{0,3}: t2 raw0 inverted=>1.
- t3 B1; C raw1 inverted=>0, but target1. choose C0 at t3 needed. This conflicts.

A viable target matching C{0,3} is C=`1,0,1,0,1`; t4 raw0 inverted=>1. Success. Full outputs satisfy.

### Trace P-M1R-FAIL
Same A/B but C{0,2}: C becomes `1,0,0,1,1`, failing ticks2–3. The decision point is not drawing C's desired waveform directly; it is anticipating B's edge-caused inversion boundary.

## 2.4 Greedy/exhaustive baseline
Greedy per-lane matching fails once coupling changes interpretation after another lane edge. However, the hand simulation exposed a deeper danger: exact traces are hard to author/read without slipping into clock-signal bookkeeping. Exhaustive solver search is small: A 3C2 * B 3C2 * C 5C2 = 90 edit states in P-M1R, trivial for validator. Later cases can reach perhaps `~10^5–10^7` combinations before symmetry pruning, still manageable.

Pruning: target-prefix mismatch after deterministic cycle simulation; rotational symmetry canonicalization; coupling-dependency order; fixed punch-count bounds.

## 2.5 Content families
1. gate-next-tick coupling;
2. persistent inversion coupling;
3. temporary read-offset shift;
4. one-shot latch that suppresses a later edge;
5. two followers sharing one physical lane with different phases;
6. cyclic dependency where lane C affects A late in the cycle;
7. forbidden simultaneous outputs;
8. sparse edit sites forcing reuse of coupling rather than direct drawing.

These are genuinely different, but families 3–6 increasingly resemble finite-state/programming puzzles.

## 2.6 Demo / GIF / market / spike
Demo: direct one-lane pattern -> two lanes -> gated follower -> inversion coupling -> small capstone. 20–25 min.

First GIF: player punches two holes; paper drum rotates; three cardboard figures animate, then one follower flips another figure's motion halfway through the cycle.

Market position: tactile paper automaton presentation is distinctive, but the logical identity risks being perceived as signal programming wearing cardboard.

Prototype falsification spike: implement only the finite simulator and crude 2D drum. Give 8 players six cases. Kill if >=4 describe solution primarily as "programming a sequence" or if fewer than 5 can explain a coupled failure without scrubbing the timeline repeatedly.

Portfolio re-check: no direct collision with #001–#008, but generic-programming drift is a factory-wide avoidance lane from Phase 1.

## 2.7 Run-2 verdict
**FINALIST, but third place.** Cross-lane coupling can be intrinsic, so it survives the required attack. Yet hand-authoring exposed high bookkeeping/timeline-debug burden. It remains mechanically safe and visually charming, but it is less cognitively elegant than the two leaders.

---

# 3. G9C02 — Binder's Imposition

## 3.1 Logical authority
A case consists of one or more sheet signatures. Each signature is a finite set of flat slots. A chosen fold template defines a deterministic permutation from flat slots to bound leaf faces plus orientation bits. Nesting defines leaf block order. Constraints inspect final page number, facing pair, sheet membership, orientation, insert role, and trim survival.

Canonical representation:
`assignment[flat_slot] -> page_face`, `signature_type`, `sheet_orientation`, `nest_order`, with deterministic transform `F` returning ordered final faces `(page,orientation,sheet,trim_state)`.

No real-world print calibration is authority.

## 3.2 Tutorial B-T1
One duplex 4-face sheet with flat slots `F0,F1,B0,B1`. Fold template maps final read order to `F1,B0,B1,F0`. Goal pages `1,2,3,4`. Therefore assign `F1=1,B0=2,B1=3,F0=4`. Animation physically folds to reveal why.

## 3.3 Hour-8 mature case B-M1
Two 4-face signatures S and T, each using the same transform above. One is nested inside the other. Pages 1–8 must read in order. Additional constraints:
- pages 4 and 5 must be a facing spread;
- red insert pages `{3,6}` must belong to the same physical sheet;
- page 8 must be on the outermost physical leaf;
- T is the only sheet allowed to carry red.

Nest choices: `S outer / T inner` or `T outer / S inner`.

For a 4-face folded sheet alone, logical face order is positions `[0,1,2,3]`. When two are nested, outer contributes final positions `{0,1,6,7}` and inner contributes `{2,3,4,5}`.

### Trace B-M1-SUCCESS
Choose T outer because page8 must be outer and red can only be T; but red pages3 and6 would then both need outer positions and are not. Contradiction. Choose T inner: red pages3 and6 can occupy inner positions `{2,3,4,5}`, and S outer contains page8. Thus T inner is forced.

Assign final-position pages directly:
- S outer positions 0,1,6,7 = pages 1,2,7,8.
- T inner positions 2,3,4,5 = pages 3,4,5,6.
Then apply inverse fold permutation independently to each sheet. For each sheet final order `[F1,B0,B1,F0]`.
S: `F1=1,B0=2,B1=7,F0=8`.
T: `F1=3,B0=4,B1=5,F0=6`.
Pages4/5 are facing at the center of inner signature; red 3/6 share T; page8 outer. Success.

### Trace B-M1-FAIL
Start with T outer due to red visibility intuition. T final slots can only become pages1,2,7,8 if page order is correct, so red requirement `{3,6}` fails immediately. No amount of flat-slot swapping fixes a wrong nesting class. The real decision is selecting the physical signature role before solving local imposition.

## 3.4 Greedy/exhaustive baseline
A memorized four-page formula solves only the local inverse permutation, not nesting/sheet-role constraints. Greedy "put requested page in visually nearest slot" is meaningless because flat adjacency and final adjacency differ. Exhaustive permutation of 8 faces is 40,320 assignments * 2 nest orders before pruning; a CSP collapses it immediately using final-position domains, sheet constraints and fold inverse.

At intended mature size 12–20 page faces, raw factorial search is huge, but exact constraint propagation makes authored validation practical because fold templates define strong positional domains. Validator can count solution classes and reject cases where one formula plus rote fill completes everything.

## 3.5 Content families
1. nesting-role deduction;
2. facing-spread constraints;
3. same-sheet / different-sheet page groups;
4. orientation-sensitive image/page faces;
5. sacrificial trim bands where a mark must disappear or survive;
6. partial signatures with blank faces that alter nesting;
7. insert stock allowed only in particular signature roles;
8. two alternative fold templates where secondary constraints select the viable transform.

All preserve one mental model—flat sheet transform -> final book—without requiring realism trivia.

## 3.6 Demo / GIF / market / spike
Demo 22–28 min: 4-face surprise -> duplex orientation -> 8-page nested signatures -> facing pair -> red insert capstone based on B-M1.

First GIF: player arranges four numbered page faces in an apparently absurd flat order; sheet folds twice; pages flip perfectly 1-2-3-4. Then a second sheet nests inside and changes the sequence.

Market position: current bookbinding games own craft/cozy language, so this must be sold as a **physical permutation puzzle: "make the flat sheet wrong so the folded book reads right."**

Prototype falsification spike: 2D flat slots + simple fold animation for 10 cases. Kill if after tutorial case 4 fewer than 70% of testers can predict at least two final adjacencies before preview, or if mature solving is mostly repeated preview/swap with no verbalized transform model.

Portfolio re-check: strong distance from all prior games. It is reversible assignment under known deterministic permutation, not destructive editing, topology rewiring, hidden observation, property transfer, or network balancing.

## 3.7 Run-2 verdict
**FINALIST — current #1.** Mature depth survives a concrete case, implementation is exceptionally safe, solver authority is clean, and content families deepen one coherent transformation rather than accrete unrelated systems.

---

# 4. G9C01 — Ink Trap Press

## 4.1 Logical authority
Sheet is a finite grid. Each cell has `(pigment, wet_timer, protected)` where pigment is one of `blank,R,B,P,K` for current prototype vocabulary. A pass is `(mask, ink, pressure)`.

Rules for the Run-2 finite model:
- mask exposes a listed cell set;
- low pressure inks exactly exposed cells;
- high pressure also attempts orthogonal spread into blank unprotected neighbors;
- `R` over wet `B` or `B` over wet `R` becomes `P`;
- dry `K` is resist and blocks later ink/spread;
- every committed pass decrements positive wet timers after resolution; new ink starts wet_timer=2;
- presentation shaders do not affect authority.

## 4.2 Tutorial I-T1
3x3 grid, target center red only. Mask exposes center. Low-pressure R directly solves. Second tutorial can show high pressure contaminating neighbors.

## 4.3 Hour-8 mature case I-M1
Use a 1x5 strip for hand simulation, cells `0..4`.
Start: all blank.
Available masks:
- M1 exposes {1,2}
- M2 exposes {2,3}
- M3 exposes {0,4}
- M4 exposes {1,3}
Available passes: R low, B low, K low. Exactly 4 passes maximum.
Target: `[blank, P, K, P, blank]`.
Constraint: cells0/4 must remain blank.
Rule subset: R+B mixing requires the first color still wet; K blocks later ink.

### Trace I-M1-SUCCESS
1. M1 + R low -> cells1,2=R(wet2).
2. M4 + B low -> cell1 R+B =>P; cell3=B; cell2 R ages but remains R.
3. M2 + K low -> cell2 becomes K; cell3 B becomes K under naive overwrite, which would ruin target. Therefore K cannot simply overwrite any pigment.

**Repair discovered by hand simulation:** define K resist ink as legal only on blank or single-color wet pigment where it seals that cell but does not recolor; that is unintuitive. Better: separate `resist` as a transparent material operation, not pigment.

Revised state `(pigment,wet,resist)`. Resist pass sets resist=1 without changing pigment; later colored ink cannot enter.

Re-author target center: pigment at cell2 must remain `R` and resist flag must be on; target becomes `[blank,P,R*,P,blank]`, where `*` means sealed/resist.

Now successful trace:
1. M1+R -> c1,c2 R.
2. M2+R -> c2 remains R refreshed; c3 R.
3. M4+B -> c1 P, c3 P.
4. M2+RESIST -> c2 and c3 sealed; but c3 target allows P sealed? If not, extraneous state.

Use resist mask M5={2} for mature set. Final c2 R sealed, c1/c3 P. Success.

### Trace I-M1-FAIL (greedy)
1. M4+B first because it fills both future purple target cells blue.
2. M1+R -> c1 becomes P, c2 R.
3. M2+R -> c3 B+R becomes P, c2 R.
4. M5+RESIST -> also succeeds. Thus ordering is not meaningful yet.

This defeats the intended greedy trap. Add drying asymmetry: B starts wet1, R starts wet2; mixing happens only when underlying pigment is wet. After each pass timers decrement at end, so B laid in pass1 is dry before R reaches pass3 at c3. Greedy trace now fails c3 (R over dry B does not mix). The successful R-first trace works because R remains wet long enough for B pass3 only if refreshed at c2? c1 from pass1 would dry by pass3. So use two masks and timing carefully.

Final compact mature case requires a two-step wetness preparation and cannot be represented elegantly in 1x5 without special-case timing. This is itself key evidence: Ink Trap's depth is real, but authored state interactions are more fragile than the premise suggests.

## 4.4 Greedy/exhaustive baseline
A one-step preview plus target-similarity greedy is dangerous. Cases must be validator-certified with a greedy failure witness. Raw branching with 5 masks * 3 operations * 2 pressures over 6 passes is `30^6 = 729M` action sequences, but state deduplication, mask legality, pass budget, forbidden-cell pruning and symmetry reduce sharply. An 8x8 grid state is large, yet authored action sets are small; bounded BFS/IDA* remains plausible only if each case exposes perhaps <=8 masks and <=4 material actions.

## 4.5 Content families
1. wet-window overprint timing;
2. pressure spread + protected negative space;
3. transparent resist that blocks later passes;
4. registration offset where one mask shifts after a pass;
5. sacrificial underprint required to create final mixed class;
6. intermediate-state objective such as "edge must never be contaminated";
7. limited mask reuse forcing multi-region sharing;
8. dry pigment that changes how later ink behaves without changing target color.

## 4.6 Demo / GIF / market / spike
Demo 20–25 min: direct stamp -> pressure spread -> color mixing -> resist -> capstone with deliberately non-greedy order.

First GIF: one plate stamps red; second blue pass creates purple only where still wet while black/resist boundary keeps a white hairline clean.

Market position: differentiated from art simulators by exact deterministic overprint planning, but store copy must avoid implying freeform printmaking.

Prototype spike: implement 6x6 integer-grid simulator only. Generate/author 20 cases and run greedy target-distance policy plus exhaustive validator. Kill if fewer than 8 cases have a human-legible non-greedy reason while remaining solvable in <=7 passes, or if rule explanation needs more than four material states before cases become deep.

Portfolio re-check: spatial temporal substrate differs from #008's key vector, but irreversible transformations remain a structural echo. It is acceptable only if wetness/spatial cross-region coupling, not destructive monotone editing, dominates.

## 4.7 Run-2 verdict
**FINALIST — current #2.** The hand case exposed rule-authoring fragility and the need for explicit validator gates, but it also proved that greedy resistance is testable rather than assumed. Visual payoff and systemic depth remain excellent.

---

# 5. G9C05 — Stained Glass Noon

## 5.1 Logical authority
Window is a small grid of cells. Each cell holds one glass token `(color, transmittance_class, optional prism_direction)`. Each requested time `t` defines a deterministic projection transform from window cells to floor target cells. Contributions combine through a finite color/intensity table. No ray-traced optics is authority.

State: `window[cell] -> token`; deterministic `Project(window,t) -> floor_grid`.

## 5.2 Tutorial S-T1
2x2 window, one time. Each window cell maps directly to one target floor cell. Place red/blue/blank tokens to match target. Next case shifts projection one floor cell at afternoon time.

## 5.3 Hour-8 mature case S-M1
Window has 3 editable cells W0,W1,W2. Tokens: R, B, Y. Each used once.

At Morning M, mapping is identity to floor F0,F1,F2.
At Noon N, mapping is rotated: W0->F1, W1->F2, W2->F0.
At Evening E, W0 and W1 both contribute to F0, W2->F2; additive table R+B=P, R+Y=O, B+Y=G.

Targets:
- M: F0=R,F1=B,F2=Y.
- N: F0=Y,F1=R,F2=B.
- E: F0=P,F2=Y.

### Trace S-M1-SUCCESS
Place W0=R,W1=B,W2=Y. Morning exact. Noon maps Y to F0, R to F1, B to F2 exact. Evening W0+W1 => P at F0; W2=>Y F2 exact.

### Trace S-M1-FAIL
Swap W0/W1: morning already fails, so the case has no real coupled choice. Add a choice of two pane orientations changing only Noon mapping. But then Morning pins colors uniquely and Noon just picks orientation. The multi-time constraint is verification, not planning.

A better mature case must make each time individually underconstrained. Example use duplicate token colors and optional shutters, but this rapidly becomes a CSP whose visual projection may hide the core choice. Run 2 therefore fails to produce a compact mature case where the same placement creates a meaningful trade-off rather than one time simply determining the solution.

## 5.4 Greedy/exhaustive baseline
If any one target time nearly fixes each cell, solve that time then verify the rest. To resist, mappings must aggregate/split contributions so no time independently determines placement. But then readability and authoring complexity rise. Raw permutation search with 9 cells is 9! = 362,880 before duplicate tokens; manageable for solver, potentially trial-and-error for human if previews are free.

## 5.5 Content families
1. time-dependent translated projection;
2. overlapping contributions / color mixing;
3. thickness/intensity classes;
4. prism token splitting one cell into two projected cells;
5. occluder bar active only at some sun angles;
6. panes with asymmetric orientation;
7. target negative-space silhouettes;
8. one fixed heritage pane constraining the rest.

These are distinct, but several add projection complexity rather than deepening a simple mental model.

## 5.6 Demo / GIF / market / spike
Demo: direct shadow -> shifted noon shadow -> overlap color mix -> two-time case -> three-time capstone.

First GIF: same finished window; slider moves Morning -> Noon -> Evening and three different required colored floor motifs snap into place.

Fresh market risk is materially higher than Run 1: `The Artisan of Glimmith` released 2026-03-17 as a stained-glass coloring/cutting/joining puzzle with handcrafted puzzles and over 20 rule types. Our moving-sun projection is mechanically distinct, but the screenshot/theme comparison is now expensive.

Prototype spike: build 5x5 discrete projection simulator and author 15 three-time cases. Kill if >=8 cases can be solved by satisfying one time independently then making only forced corrections, or if testers need to inspect opaque contribution tables rather than reason spatially.

Portfolio re-check: no direct collision with prior games.

## 5.7 Run-2 verdict
**ELIMINATED (4th).** Beautiful hook and strong GIF, but concrete case construction failed the central attack: multi-time constraints too easily become independent target matching or opaque projection CSP. Current stained-glass market competition also raises differentiation cost.

---

# 6. G9C21 — Tailor's Grain

## 6.1 Logical authority
Fabric is a finite 2D grid with printed motif IDs and one global grain axis. Each garment pattern piece is a finite cell mask with allowed rotations/reflections, required grain relation, optional motif anchor, and seam-edge labels. Placement must be non-overlapping and inside cloth. Seam constraints compare motif phase/edge class between paired garment pieces.

No cloth physics or sewing simulation is authority.

## 6.2 Tutorial T-T1
6x4 fabric with vertical grain. Place two rectangular pieces, both requiring vertical grain, without overlap. Then introduce a mirrored pair with motif centers.

## 6.3 Hour-8 mature case T-M1
Fabric 8x5 with repeating motif columns `A B A B A B A B` across width, constant by row. Pieces:
- Front L: 2x3, grain vertical, motif A must be centered on top edge.
- Front R: mirror of L, grain vertical, motif A centered on top edge.
- Sleeve L/R: each 1x3, may rotate only if grain remains within allowed parallel orientation; paired sleeve seam edges must start on opposite motif phases.
- Collar: 3x1, grain must be horizontal (bias-like exception), must cross motif sequence A-B-A.
Constraint: all five pieces fit; Front L/R must be mirror motif matches; sleeve pair must be phase-opposed; collar must use the unique A-B-A horizontal run not consumed by fronts.

### Trace T-M1-SUCCESS
Reserve one top-row A-B-A run for collar first because it is the only horizontal-grain piece. Place mirrored fronts in two A-centered vertical zones separated enough to preserve sleeve strips. Then place sleeves into remaining narrow columns with opposite motif phase.

### Trace T-M1-FAIL — area-greedy
Place the two largest front pieces first in the tightest packing positions to minimize waste. They consume the only contiguous A-B-A row segment accessible to horizontal collar orientation; remaining total free area is sufficient but collar has no legal motif/grain placement. The real decision is reserving a constrained motif/grain resource, not minimizing waste.

## 6.4 Greedy/exhaustive baseline
Pure bin-packing heuristics fail when motif/grain legality creates scarce placement classes. However, exact placement enumeration looks like polyomino packing with constraints. For cloth 10x8 and <=7 pieces, each piece might have 20–80 legal placements; naive product can be huge, but exact-cover/backtracking with most-constrained-piece-first, occupancy bitsets, symmetry reduction and motif-domain pruning is practical for authored cases.

The bigger issue is identity: if players spend most time scanning legal placements, it still feels like packing. Grain/motif/seam constraints must routinely decide the puzzle before area efficiency does.

## 6.5 Content families
1. mirrored motif pair matching;
2. grain-direction exceptions / bias pieces;
3. seam-edge motif continuation;
4. directional/napped fabric where rotation is forbidden;
5. border-print fabric reserving hem locations;
6. defect zones that can appear only in hidden seam allowance;
7. one-way plaid alignment across multiple pieces;
8. layered cut where two mirrored layers share one placement decision.

## 6.6 Demo / GIF / market / spike
Demo 20–25 min: basic fit -> grain lock -> mirrored motif -> seam matching -> capstone where waste-minimizing layout is wrong.

First GIF: two pattern pieces slide over patterned cloth; an apparently efficient layout produces visibly mismatched plaid at the sewn seam, then a slightly wasteful placement snaps the pattern continuously across the garment.

Fresh market risk is now severe: `Dressmaker` is scheduled for 2026-09-21 and its Steam description explicitly says players arrange/cut patterns and that grain or bias changes the final dress. That overlaps the exact storefront vocabulary Tailor's Grain would need, even though our design is a stricter logic puzzle.

Prototype spike: exact-cover solver + 12 flat 2D cases. Kill if an area/waste-first heuristic solves >=8/12, or if removing the final sewn-garment preview makes testers describe it simply as "Tetris with extra placement restrictions."

Portfolio re-check: mechanically distant from Games #001–#008, but generic packing resemblance is external rather than portfolio-specific.

## 6.7 Run-2 verdict
**ELIMINATED (5th).** The mature case proves grain/motif/seam constraints can dominate packing, so the concept is not mechanically invalid. It loses on market timing and identity risk: an imminent 2026 dressmaking title already foregrounds arranging/cutting patterns plus grain/bias, while our remaining core still uses exact-cover packing as substrate.

---

# 7. Equal destructive comparison after concrete cases

Scores 1–5 after Run-2 evidence; maximum 50.

| Concept | Hook | Mature | H8 depth | Anti-greedy | Solver | Impl. | Content | Demo | Market | Portfolio | Total | Verdict |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---|
| Binder's Imposition | 5 | 5 | 5 | 5 | 5 | 5 | 5 | 5 | 4 | 5 | **49** | FINALIST #1 |
| Ink Trap Press | 5 | 5 | 5 | 4 | 4 | 4 | 5 | 5 | 5 | 4 | **46** | FINALIST #2 |
| Paper Automata | 5 | 4 | 4 | 5 | 5 | 5 | 4 | 5 | 5 | 5 | **47** | FINALIST #3 despite raw score: bookkeeping penalty is qualitative |
| Stained Glass Noon | 5 | 3 | 4 | 3 | 5 | 4 | 4 | 5 | 3 | 5 | **41** | ELIMINATED |
| Tailor's Grain | 5 | 4 | 4 | 4 | 5 | 5 | 4 | 5 | 2 | 5 | **43** | ELIMINATED |

Raw score alone does not determine ordering. Paper Automata scores highly on engineering safety and market novelty, but its hand-simulation produced repeated timing-authority repairs and a strong programming/debugging feel. That is a central product-quality risk, so it remains #3 behind Ink Trap Press.

---

# 8. Exact Run-2 reduction

## FINALISTS — 3
1. **G9C02 Binder's Imposition**
2. **G9C01 Ink Trap Press**
3. **G9C31 Paper Automata**

## ELIMINATED
4. **G9C05 Stained Glass Noon** — failed to demonstrate a compact mature case where multiple time targets create coupled planning instead of one-time solve + verification; fresh stained-glass competition raises positioning cost.
5. **G9C21 Tailor's Grain** — proved nontrivial but still rests on exact-cover packing, and imminent `Dressmaker` directly overlaps pattern placement plus grain/bias storefront language.

No Product Thesis is locked.

---

# 9. Required final head-to-head — Run 3

The final three are sufficiently different that automatic selection would be premature. Run 3 must choose exactly one concept using **prototype-grade paper validation**, not another broad score.

For each finalist:
1. create three validated microcases: tutorial, midgame, hour-8;
2. formalize exact transition/constraint semantics with no repaired-on-the-fly ambiguity;
3. run or manually execute a tiny solver/search script where useful to count solutions and greedy failures;
4. identify the minimum rule vocabulary required for genuine depth;
5. measure explanation burden: what must a player understand before the capstone is fair?;
6. test demo arc and first-GIF comprehension;
7. perform current-market collision search again if new evidence matters;
8. compare production burden for one polished vertical slice and 30 strong full-game cases;
9. attack portfolio similarity and generic-programming/packing/paint-by-numbers drift;
10. select exactly one winner and lock Phase 3 Product Thesis only after recording why the other two lose.

### Specific Run-3 kill questions
- **Binder's Imposition:** can three distinct mature cases avoid both rote imposition formula and orientation bookkeeping while keeping one elegant mental model?
- **Ink Trap Press:** can a tiny deterministic rule set produce certified non-greedy cases without wetness/mask exceptions proliferating?
- **Paper Automata:** can coupling produce legible mechanical causality without turning play into clock-signal programming/debugging?

---

## 10. Research note — 2026-08-31

Fresh evidence used in this run:
- `The Artisan of Glimmith`, released 2026-03-17, is a stained-glass puzzle centered on coloring/cutting/joining handcrafted glass puzzles with many rule types; this increases theme/storefront collision for Stained Glass Noon.
- `Dressmaker`, planned for 2026-09-21, explicitly advertises choosing fabric, arranging/cutting patterns, and grain/bias affecting the final dress; this directly increases market-position risk for Tailor's Grain.

These are market-comparison inputs only, not design canon.

---

RUN 2 COMPLETE. THREE FINALISTS REMAIN. PRODUCT THESIS UNLOCKED.