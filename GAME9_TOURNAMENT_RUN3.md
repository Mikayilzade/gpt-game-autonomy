# GAME #009 — PHASE 2 CONCEPT TOURNAMENT — RUN 3

Status: **RUN 3 COMPLETE / 3 -> 1 / WINNER SELECTED**
Date: 2026-08-31
Active slot: **Game #009 only**
Winner: **G9C02 Binder's Imposition**
Production implementation: **FORBIDDEN in factory**

Authority: START_HERE.md -> STATUS.md -> GAME_INDEX.md -> GAME9_RESEARCH.md -> GAME9_TOURNAMENT.md -> GAME9_TOURNAMENT_RUN2.md -> this file.

## 1. Method
Finalists were not rescored abstractly. Each received three fixed microcases (tutorial, midgame, hour-8), one minimum rule vocabulary, a solver/search sanity check, explanation/demo burden attack, production burden comparison, and drift/portfolio attack. Any rule repair required during a trace counted against the concept.

## 2. G9C02 Binder's Imposition — WINNER

### Minimum rule vocabulary
1. A signature exposes a finite set of flat duplex slots.
2. A chosen fold template is a deterministic bijection from flat slots to final bound-face positions plus orientation bits.
3. Nesting assigns signatures to outer/inner final-position domains.
4. Constraints inspect only final position, facing adjacency, signature membership, orientation, blank/trim survival, and bounded material role.
5. Player edits are reversible assignment/swap, signature choice, orientation, and nest order; Fold Preview reveals the deterministic result but does not solve constraints.

No real printing calibration, paper physics, customer economy, prose-layout work, or vocational trivia is authority.

### B3-T — tutorial
One 4-face duplex sheet. Transform final read order = `[F1,B0,B1,F0]`. Goal `1,2,3,4`. Exact inverse assignment: `F1=1, B0=2, B1=3, F0=4`. One coherent lesson: flat order looks wrong because folding is the permutation.

### B3-M — midgame
Two 4-face signatures, one outer and one inner. Final position domains: outer `{1,2,7,8}`, inner `{3,4,5,6}`. Constraints: pages 3 and 6 must share the blue-stock signature; page 8 must be outer; pages 4/5 must face. Blue stock exists on exactly one signature. Therefore blue must be inner, outer receives `1,2,7,8`, inner receives `3,4,5,6`, then each sheet is solved by the same inverse fold map. Wrong blue-outer choice is globally impossible regardless of local swaps. This proves sheet-role deduction, not rote local imposition.

### B3-H — hour-8
Three 4-face signatures A/B/C produce final domains outer `{1,2,11,12}`, middle `{3,4,9,10}`, inner `{5,6,7,8}`. Constraints: gold-stock pages `{4,9}` must share one signature; foldout pair `{6,7}` must be on the innermost signature and one face orientation-reversed; page 12 must be outer; page groups `{1,2}` and `{11,12}` may not share the gold signature. Exactly one signature is gold stock and exactly one permits reversed orientation.

Deduction: gold must be middle because only middle contains both 4 and 9 under correct reading order; reversed-capable signature must be inner because only inner can host 6/7; remaining signature is outer. Local fold inversion is then applied independently. A memorized four-page formula handles only the final local step; it cannot infer the role assignment. The case stays inside one mental model: choose physical roles, then invert known folds.

### Search sanity check
Raw face assignment grows factorially (8 faces = 40,320 before two nest orders; 12 faces is enormous), but fold templates predefine final-position domains. CSP validation works by propagating page-domain, signature-role, facing, orientation, and material constraints before any flat-slot permutation. Intended 8–20-face cases are therefore validator-friendly while remaining human-legible. Symmetric sheet labels can be canonicalized before solution counting.

### Explanation burden
Before a 20–30 minute capstone the player needs only: flat slot -> folded position, duplex orientation, nesting, and one secondary constraint. Secondary constraints reuse the same output book rather than create a parallel subsystem.

### Production burden
Vertical slice: one table/workbench, reusable page-face icons/numbers, 2D flat editing plus simple fold/nest animation. ~30 strong cases are mostly data and validation work, not bespoke environments or large art sets. This is the lowest production-risk finalist.

### Drift attacks
- **Rote formula:** defeated by varying signature roles/nesting/secondary constraints; local formula is intentionally a learned primitive, not the whole puzzle.
- **Orientation bookkeeping:** keep orientation binary, visible, and bounded; do not model real press jargon.
- **Generic programming:** no timeline, gates, signals, or code-like execution.
- **Portfolio collision:** none of #001–#008 centers reversible assignment through known fold permutations plus final-book constraints.

**Verdict: SELECT.** Three scales remain clean under one rule vocabulary; depth grows by constraint intersection rather than exception count.

## 3. G9C01 Ink Trap Press — KILLED IN FINAL

### Frozen minimal test vocabulary
Finite grid; cell pigment `blank/R/B/P/K`; wet bit lasts exactly one subsequent pass; exposed low-pressure ink affects only mask cells; R+B on a wet opposite color becomes P; dry K blocks later ink; high pressure adds orthogonal spread into blank cells only. No overwrite exceptions beyond those statements.

### I3-T
3x3, center-only mask, R-low, target center R. Trivial and legible.

### I3-M
1x4 strip. Masks `{0,1}`, `{1,2}`, `{2,3}`; target requires purple at 1, clean at 0/3, blue at 2 under three-pass cap. The player can create purple only by timing R/B within wet window while protecting endpoints through mask choice. This is valid but already requires state-timer explanation.

### I3-H
2x4 grid with one K-resist boundary, two color masks, one high-pressure opportunity and forbidden contamination cells. A certified non-greedy solution can be authored, but its quality depends on wet-state timing plus spread plus resist interaction. Removing any one of those leaves mostly direct mask coloring; keeping them creates three interacting rule channels before the mature case becomes interesting.

### Search / burden result
Finite BFS/IDA* is practical, but state is `pigment × wetness` per cell plus pass budget. Exact validation is not the problem. The problem is human explanation: direct next-pass preview encourages trial enumeration, while hiding it makes wet/spread failures opaque. Thirty strong cases would require careful anti-greedy certification and substantial target/mask authoring.

### Kill reason
The concept survives technically, but Binder produces comparable systemic depth with fewer temporal exceptions and substantially lower explanation burden. Ink Trap Press remains vulnerable to **paint-by-numbers / preview-and-try drift**. Final kill is comparative, not because it is unbuildable.

## 4. G9C31 Paper Automata — KILLED IN FINAL

### Frozen minimal test vocabulary
Discrete ticks; each lane has binary drum bits; outputs sample at tick start; rising edges schedule effects for the next tick only; allowed coupling families in the final test are next-tick gate and persistent inversion. Player edits punches before RUN; RUN is deterministic one cycle.

### P3-T
T=4, one lane, target `0,1,1,0`; choose punches 1 and 2. Immediate mechanical causality.

### P3-M
T=5, lanes A/B. A rising edge gates B next tick. Target A=`1,0,1,0,0`, B=`0,1,0,1,0`; choose A punches `{0,2}`, B `{1,3}`. Coupling is legible.

### P3-H
T=6, lanes A/B/C. A rising gates B next tick; B rising toggles C inversion from next tick onward. Sparse editable sites force anticipation of the inversion boundary. The trace is deterministic and solver-small, but solving requires reasoning in tick-indexed signal causality rather than primarily in physical paper form.

### Search / burden result
Validator is excellent: enumerate edit sets and simulate one cycle; even ~10^5–10^7 candidates are manageable with prefix and symmetry pruning. Yet the human burden grows faster than the solver burden. The hour-8 identity is effectively signal debugging with a cardboard renderer.

### Kill reason
Fails the final factory anti-drift question. Coupling can be made legible, but durable depth pushes directly toward **clock-signal programming/debugging**, an explicitly avoided current-market lane. Art charm does not change the reasoning substrate.

## 5. Final comparison
Binder wins because the same four primitives survive tutorial -> midgame -> hour-8 without additional timing state, exception tables, or programming semantics. It has the cleanest validator, lowest polished-slice burden, strongest 30-case content efficiency, and best portfolio distance.

Final order: 1) Binder's Imposition — SELECT; 2) Ink Trap Press — KILL comparative complexity/preview drift; 3) Paper Automata — KILL programming/debugging drift.

Phase 2 is complete. Product Thesis may now lock G9C02 only.