# GAME #016 — PHASE 2 CONCEPT TOURNAMENT / ROUND B

Date: 2026-09-03
Status: Round B complete; **3 finalists; no winner selected**.
Authority inputs: `GAME16_RESEARCH.md`, `GAME16_ROUND_A.md`.

## 0. Method
Round B does not reward prior score. Each survivor received: (1) exact small state/action/certification model, (2) one nontrivial worked case, (3) direct attack on its named dominant strategy, (4) tutorial→mid→late verb-vocabulary test, (5) current analogue/differentiation check, and (6) proof-route / clip legibility / content scale / determinism judgment.

Fresh September-2026 searches were treated conservatively. Search absence is never uniqueness evidence. Relevant surfaced references include: **Outpacked** (Apr 1 2026: luggage packing under logical adjacency constraints, 61 levels + editor), **Packing Life** (Mar 6 2026: efficient box packing), **Room to Breathe** (Apr 24 2026: furniture layout under functional requirements), **vrkshop** (freeform VR woodworking), **Chop Chop Inc.** (Aug 7 2026: woodworking/furniture production sim), **Gear Combination** (May 29 2025: gear-ratio placement puzzle), and announced **Geareo** (freeform physics mechanical sandbox). These narrow the claims we can safely make.

---

# 1. Margin of Error — FINALIST

## Exact small model
A workpiece dimension is never stored as a secret random number. It is a certified interval `x ∈ [nominal-low, nominal+high]`. A measuring tool contributes a disclosed bias interval. A mark references either a trusted datum or a previously created uncertain feature. Correlation is represented by named error sources, not by player arithmetic.

Player verbs: **choose datum → place gauge/ruler → choose one discrete mark socket → cut/fit → inspect envelope → certify**. Certification evaluates both extremes and named shared error sources. A functional pair can specify both minimum clearance and maximum play, killing the “make everything loose” strategy.

## Worked puzzle — Forked Latch
Stock bar has trusted left face D. Ruler R reads +1 to +2 units long. Two holes must end 8–10 units apart; final bar length must be 19–21. Legal marks are 9, 10, 19 and 20 ruler units from a chosen reference. If both holes are independently measured from opposite uncertain cut faces, worst-case separation expands beyond the 8–10 band. If both are referenced from D, the shared ruler bias cancels in their separation, while final length still requires the safer nominal socket. The player sees colored physical envelopes overlap before certification; no subtraction worksheet is required.

**Human proof route:** identify the one relation whose tolerance must cancel → share a datum for that pair → satisfy the separate outer envelope.

## Dominant-strategy attack
“Use widest clearance” fails because too much play violates the upper functional bound. “Always use one datum” also fails in later jobs where independent errors are intentionally useful to avoid correlated drift in two unrelated fits. Thus datum choice remains contextual.

## Verb scalability
- Tutorial: one biased ruler, one shared-datum cancellation.
- Midgame: two named error sources, one go/no-go gauge.
- Late: 3–4 features, purchased part tolerance, mixed correlated/independent errors.
No new verb is needed; complexity comes from which uncertainty should cancel versus remain independent.

## Market / production judgment
Current searches surfaced ruler/geometry education titles (e.g. `Ecocoru`, `Compass & Straightedge`) but not a close Steam analogue centered on **tactile tolerance-stack design under disclosed uncertainty**. This remains a differentiation hypothesis, not a uniqueness claim. Major risk is category perception: screenshots can look educational unless the physical fit/reveal is foregrounded.

**Round-B verdict: FINALIST.** Strongest formal proof structure and portfolio distance. Risk is presentation, not mechanical ambiguity.

---

# 2. The Spare Room — KILL

## Exact small model
Two disclosed grid floorplans A/B share an object set. Each furniture item has occupied cells, orientation, use-zone cells, and optional facing/access predicate. One placement/orientation must satisfy no-overlap, in-bounds and use-zone predicates in both A and B.

## Worked puzzle — Sliding Studio
A 5×4 room becomes 4×5 after wall translation. Bed needs one free long-side cell; desk must face a window cell; chair needs one pull-out cell. The geometric intersection can hold all footprints, but putting everything there blocks either bed access in A or chair access in B. The valid family deliberately places the desk in a cell outside A/B intersection while its transformed counterpart remains legal in the other state.

This proves paired-state reasoning is real, but it also exposes the product problem: the solved object remains a constrained furniture layout.

## Dominant-strategy attack
Intersection packing can be defeated cleanly, as above. Solving A and B independently also fails because placement identity is shared. Mechanical proof therefore passes.

## Verb scalability
Tutorial and midgame work with place/rotate/inspect. Late novelty, however, tends to demand more furniture-specific use predicates (hinge arc, bedside reach, sightline, appliance clearance, etc.). That is one-off-rule inflation unless kept shallow.

## Market / production judgment
The space is visibly occupied. `Room to Breathe` released Apr 24 2026 as a furniture layout puzzle where accessibility, spacing, orientation and room function are explicit constraints; `BOXROOM` and `My Dream Setup` reinforce the broader room-layout/decorating surface. The two-floorplan obligation is differentiated, but the trailer/screenshot first read is likely “another room-layout game” before the state-switch hook is understood.

**Round-B verdict: KILL.** Mechanical validity is not enough; market-surface collision plus late content pressure loses to stronger candidates.

---

# 3. One-Way Workshop — FINALIST

## Exact small model
A job consists of stock pieces with a finite ordered set of **cut sockets**. A cut partitions one stock piece into exactly two deterministic children. Each child has typed observable properties from a deliberately tiny vocabulary: `length band`, `straight-reference edge`, `angle template`, `spacer width`, `hole-pattern witness`, `consumed/available`. A required product child can later be assembled; an offcut can be socketed physically into a jig station whose predicate it satisfies.

Frozen verb set for proof: **inspect plan, choose stock, choose cut socket, commit cut, place resulting child as part or jig, perform jig-gated operation, certify**. Maximum primitive families: straight cut, diagonal cut, guided drill, spacing/positioning operation, assembly, certification. No freehand geometry.

## Worked puzzle — Three Cuts, Two Tools
Blank length 12 has legal cut sockets at 3, 4, 7, 8. Final product requires rail R=7, peg-hole operation H requiring spacer width 3, and diagonal brace B requiring an angle template created by a diagonal cut.

Three plausible first cuts:
- cut at 7 → R=7 + offcut 5; product looks efficient, but no width-3 spacer can be recovered before H;
- cut at 3 → spacer 3 + stock 9; H becomes possible, but a later straight 7+2 split leaves no angle template;
- diagonal cut at 4 → product-side 8 + triangular template 4; then cut 8 at 3 to create spacer 3 + stock 5, but rail 7 becomes impossible.

The authored solution family instead begins from a second provided 10-unit narrow blank: first create the angle template while preserving the 12-unit main stock, then use the template to authorize a diagonal feature on the future rail; main stock splits 3+9, spacer 3 gates H, and the remaining 9 is cut at the certified 7 socket to produce R=7 plus waste 2. The puzzle is not “minimize waste”: it is **plan a fabrication ancestry in which byproducts are future capabilities**.

## Dominant-strategy attack
“Keep the biggest offcut” loses whenever a smaller child has the only required type/band. “Always make required product parts first” loses because doing so may destroy the only future jig lineage. The system can expose all child previews before commitment, making failure strategic rather than hidden.

## Verb scalability
- Tutorial: one cut creates a spacer required immediately.
- Midgame: choose between two useful offcut properties.
- Late: 4–6 operations, two blanks, offcut lineage crosses product branches.
Depth grows in dependency graph, not action vocabulary.

## Market / production judgment
Current woodworking references are mostly simulation/freeform (`vrkshop`) or broader production fantasy (`Chop Chop Inc.`), not discrete proof puzzles where waste becomes mandatory tooling. That supports differentiation cautiously. The critical production constraint is to resist continuous sawing: freeform cutting would explode certifiability and controller UX. Discrete visible cut sockets are therefore product-defining, not a prototype shortcut.

**Round-B verdict: FINALIST.** Best causal hook and strong clip moment: make a cut, rotate the “waste”, snap it into a jig, reveal why it mattered.

---

# 4. Unpacking Order — FINALIST

## Exact small model
A case is a finite voxel/socket volume with named apertures. Each object has a finite set of legal poses and one or more extraction vectors. Object `i` is removable along vector `v` iff its swept discrete volume to the relevant aperture intersects neither case-forbidden cells nor any remaining object's occupied cells. Target is a total or partial extraction order. During certification the player may remove only the currently requested target(s); non-target repositioning is forbidden.

Player verbs: **place, rotate among legal poses, inspect pull vectors, seal, request-extract, diagnose blocker**.

## Worked puzzle — Side Mouth
Case has top aperture T and right aperture R. Long object A can exit only R; plate B exits only T; hook C exits T but its swept column blocks A's rightward corridor while present; cube D exits either T or R. Required order is `A → B → {C,D}`.

Naive reverse packing says place C/D/B then A last. But A cannot be inserted last through R if C already occupies the crossing corridor; inserting A from T is illegal. The valid construction places A first through R into its deep socket, then C in a pose whose static body does not block A's future R sweep, then B and D. At certification A slides through the preserved side corridor, which opens B's top sweep. This is an **assembly/extraction dependency graph**, not density packing.

Two additional reverse-order failure families are mechanically available without new verbs: (1) an object whose insertion aperture differs from its extraction aperture; (2) two objects whose legal insertion corridors cross but whose final poses preserve only one future extraction corridor. These are enough to prevent “just reverse the list” from being a universal solver.

## Dominant-strategy attack
Reverse-order intuition remains useful—good tutorial knowledge—but is incomplete under aperture asymmetry and swept-volume corridors. Density maximization is irrelevant because empty corridor preservation is often mandatory.

## Human proof route
Show each target's translucent sweep corridor on demand. Player reasons backward from the first extraction: which corridor must remain empty? Which later objects have poses outside it? This produces a visible proof object. Failure identifies exact blocker and vector, never merely “doesn't fit.”

## Verb scalability
- Tutorial: one aperture, three cuboids, one obvious blocking corridor.
- Midgame: two apertures, asymmetric object vectors.
- Late: 6–8 objects, partial order, handles/corridors, still same verbs.
Content can scale through object pose/vector/corridor combinations rather than furniture-like bespoke rules.

## Market / production judgment
Market risk increased materially in 2026. `Outpacked` released Apr 1 2026 with 61 luggage-packing logic levels and Workshop; `Packing Life` released Mar 6 2026 around fitting objects efficiently into boxes. They are not the same mechanic—both emphasize packing state/constraints rather than requested **future extraction certification**—but marketing must never lead with “pack a suitcase.” The differentiator must be visible immediately: seal the case, then perform the promised extraction sequence through constrained apertures.

**Round-B verdict: FINALIST, but differentiation risk is higher than its Round-A score implied.** Mechanical proof survives strongly.

---

# 5. Lost Motion — KILL

## Exact small model
Each linkage has discrete input position, output position, direction and backlash reservoir. On a direction reversal, input travel first consumes a configured slack band; only excess travel transmits. Asymmetric element may have distinct CW/CCW slack. Update order is input step → local slack absorption → transmitted delta → next element.

## Worked puzzle — Miss the First Bell
Finite crank trace `+3, -2, +2`. Bell must remain still on first +3, move exactly one unit on -2, and move on final +2. Two serial backlash collars with asymmetric bands can satisfy this by consuming the first direction and partially resetting on reversal. Too much total slack misses the required return output; too little rings early.

## Dominant-strategy attack
Maximum slack is defeated by lower engagement windows. Mechanical algebra is deterministic.

## Why it still loses
The core variable is invisible stored travel. A good animation can show gap closure, but once two or three slack elements stack, the player must track reservoirs across direction reversals. At that point the clearest UI is effectively a motion trace/graph. Meanwhile current Steam surfaces include gear-ratio puzzles (`Gear Combination`) and broad physics/mechanical sandboxes such as announced `Geareo`; these do not duplicate backlash-as-resource, but they raise the visual bar for mechanical feel. A discrete non-physics implementation risks looking less satisfying than the fantasy promises; real physics would damage determinism.

**Round-B verdict: KILL.** Formal model passes; product communication and animation/physics expectation burden do not beat the finalists.

---

# 6. The Long Drawer — KILL

## Exact small model
Cabinet = finite set of drawers. Drawer `d` has discrete extension state 0..k, occupied depth-lane cells per state, and handles/latches exposed by predicates over other drawer states. Legal action moves one drawer exactly one stop if target occupancy is collision-free and the manipulated handle is currently reachable. Retrieval removes a requested tool from a disclosed reachable compartment.

## Worked puzzle — Cross Handle
A has states 0/1/2, B 0/1, C 0/1/2. A2 blocks B1; A1 exposes B's side handle; B1 exposes C's latch; C1 blocks A2; target sequence is tool in C then tool behind A2. Deduction path is forced by visible dependency: A1 → B1 → C1/retrieve → C0 → B0 → A2/retrieve. Blindly fully opening reachable drawers causes immediate reversible blockage.

## Dominant-strategy attack
“Open everything” clearly fails. But the more serious Round-A threat—**click every legal handle**—does not fail enough. With 3–5 drawers and reversible stops, a player can cheaply explore the small state graph. Making wrong moves costly would add arbitrary friction; making graphs larger would create BFS tedium. Hidden latches would create trial-and-error.

## Verb scalability
The same pull/push/retrieve verbs scale, but 20+ handcrafted cases need either larger state graphs or additional mechanism predicates. The first invites search; the second invites bespoke-mechanism inflation.

## Market / production judgment
No close current direct analogue surfaced in targeted searches, and clip legibility is excellent. Nevertheless the intrinsic solving object is a small reversible state graph. Unlike the finalists, Round B did not find a robust proof discipline that makes reasoning clearly easier/more pleasurable than clicking through reachable states.

**Round-B verdict: KILL.** Strong toy, weaker deep puzzle product.

---

# 7. Comparative Round-B result

| Candidate | Exact mechanics | Dominant threat defeated? | Human proof route | Market surface | Content scale | Determinism | Verdict |
|---|---|---|---|---|---|---|---|
| Margin of Error | PASS | PASS | **Excellent** | Distinct but education risk | Strong | Excellent | **FINALIST** |
| The Spare Room | PASS | PASS | Good | **Crowded room-layout surface** | Medium | Excellent | KILL |
| One-Way Workshop | **PASS** | **PASS** | Excellent lineage proof | Distinct if discrete | **Strong** | Excellent | **FINALIST** |
| Unpacking Order | **PASS** | **PASS** | **Excellent corridor proof** | Packing surface crowded | **Strong** | Excellent | **FINALIST** |
| Lost Motion | PASS | PASS | Medium | Mechanical sandbox expectation | Medium | Good if discrete | KILL |
| The Long Drawer | PASS | **FAIL vs click-search** | Weak-medium | Distinct | Medium | Excellent | KILL |

Finalists are therefore:
1. **One-Way Workshop**
2. **Unpacking Order**
3. **Margin of Error**

This ordering is provisional, not winner selection.

## 8. Why these three deserve Round C
### One-Way Workshop
Most original causal sentence and strongest “aha” clip. Round C must prove a full 20–30 minute demo arc without cut-space or lineage bookkeeping becoming menu work.

### Unpacking Order
Cleanest physical proof object and easiest failure explanation. Round C must decide whether extraction-order identity is strong enough to overcome 2026 packing-game surface competition and whether 3D readability remains bounded.

### Margin of Error
Deepest reasoning and strongest formal anti-bruteforce structure. Round C must prove non-engineers can enjoy it with almost no numeric calculation and that marketing can communicate play rather than coursework.

## 9. Exact Round-C confrontation
Do not add candidates. For each finalist, create the same product-level mini-spec:
1. one-sentence store hook and 10-second trailer beat;
2. exact first 15 minutes using only eventual canonical verbs;
3. one midgame and one late puzzle proof;
4. 24-case content architecture sketch showing at least 6 reasoning families without new-rule inflation;
5. demo promise, likely price/value band, target player and strongest/weakest screenshot;
6. implementation risk ledger and smallest prototype that could falsify the concept;
7. direct pairwise comparison: OWW vs UO, OWW vs MoE, UO vs MoE on fun-before-difficulty, explanation, depth, market readability, production ratio and portfolio value;
8. select exactly one winner unless all three fail a newly exposed hard gate.

After explicit winner selection, immediately begin **Phase 3 Product Thesis Lock** only if the Round-C evidence leaves no unresolved identity contradiction. Do not start production implementation.

## 10. Round-B conclusion
Round B reduces six survivors to **three finalists**. The Spare Room, Lost Motion and The Long Drawer are killed despite mechanically valid cores because market-surface crowding/content inflation, communication/physics expectation burden, and cheap reversible click-search respectively make them weaker products.

**No Game #016 concept is selected yet. DESIGN COMPLETE = NO.**
