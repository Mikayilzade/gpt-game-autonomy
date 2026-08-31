# GAME #011 — PHASE 2 CONCEPT TOURNAMENT — ROUND A

Date: 2026-09-01
Status: ROUND A COMPLETE — 12 -> 5
Authority: START_HERE.md -> STATUS.md -> GAME_INDEX.md -> GAME11_RESEARCH.md -> this file.

Purpose: equal destructive treatment of the 12 provisional candidates. No candidate is protected by its Phase-1 score. The core test is whether the same small vocabulary produces explainable hour-3/hour-8 depth without importing a mechanic zoo.

## Equal test rubric
For every candidate: (1) 20-second GIF, (2) minimal deterministic state/action order, (3) first-20-minute teaching path, (4) hour-3/hour-8 same-vocabulary depth, (5) dominant-heuristic counterexample, (6) implementation/validator burden, (7) failure explainability, controller + 1280x800 clarity, (8) content efficiency, (9) portfolio collision.

## 03 — Queue Sculptor — SURVIVE
**20s GIF:** a divider drops into a visible six-person queue. Each person has one tiny icon-rule (e.g. avoid red directly ahead / stand behind hat). The queue resolves in a clearly animated deterministic cascade; moving the same divider one slot gives a radically different stable order.
**State/order:** ordered agents + one divider position + public local preference per agent. PLACE/MOVE DIVIDER -> scan front-to-back applying one bounded relocation rule per agent -> repeat deterministic passes until stable or pass cap -> evaluate target.
**20 min:** 3 agents/one rule family; then mixed preferences; then two plausible stable-looking outcomes; finally cases where satisfying an early agent harms a later chain.
**Hour 3/8:** depth can come from heterogeneous local rules, cascade order, divider location and target predicates without adding verbs. Exact state space remains finite if agent counts/rules are capped.
**Naive heuristic attacked:** “put divider immediately before the most constrained agent.” Counterexample: A avoids red ahead, B wants hat ahead, C(red/hat) and D; divider before A can move C away, causing B to relocate and break final target, while divider after B preserves both.
**Burden:** low-medium deterministic resolver + validator; authoring can be solver-assisted. **Explainability/UI:** strong if every relocation flashes its public reason; controller excellent. **Content:** high.
**Portfolio:** queue theme superficially near #010, but structural identity is local-agent preference stabilization around a divider, not moving-object timing/label permutation/passenger service. Must avoid luggage/service presentation.
**Round-A score:** 8.5/10.

## 04 — Pressure Caption — KILL
**20s GIF:** drag a comma/parenthesis between words on a machine instruction; grouping changes and machinery executes differently.
**State/order:** token string + punctuation slots + parse tree -> EDIT -> parse -> execute machine clauses -> evaluate.
**20 min:** grouping precedence, then nested grouping, then multiple machines.
**Hour 3/8 claim:** fails cleanly. With a tiny grammar it trends toward parse-tree exercises; sustaining hours requires more operators, syntax exceptions or machine verbs — exactly the mechanic zoo constraint.
**Heuristic:** “group the two desired words” is beaten by precedence across three clauses, but repeated counterexamples become programming-language tutorial content.
**Burden:** parser/localization/accessibility high relative to game depth. Text legibility at 1280x800/150% conflicts with dense late cases.
**Portfolio:** distinct, but structural weakness is sufficient to kill.

## 05 — Fossil Forecast — SURVIVE
**20s GIF:** choose one colored sediment layer and press LITHIFY; a crisp cross-section hardens, then a time-lapse erosion pass removes exposed soft cells and reveals a route/fossil while another route disappears.
**State/order:** compact 2D cross-section cells with material, hardness, fossil/void; choose one eligible connected layer -> harden -> deterministic erosion rounds from exposed boundary -> settle/reveal -> evaluate accessibility/preservation targets.
**20 min:** exposure/erosion; shielding; preserving one fossil while revealing another; choosing when a layer becoming permanent blocks future erosion.
**Hour 3/8:** plausible through geometry, erosion fronts, hardness ordering, irreversible timing and multi-target tradeoffs using the same LITHIFY verb. Needs strict material vocabulary ceiling.
**Heuristic:** “harden the layer directly above the fossil.” Counterexample: that cap protects the fossil but also prevents side erosion needed to open its extraction path; hardening a lateral buttress lets top material erode while preventing collapse/exposure of a second fragile target.
**Burden:** medium; cellular erosion solver is deterministic but visual rules must be exact. **Explainability:** strong with erosion preview/time-lapse. **Controller:** strong. **Content:** high if authored cross-sections validated automatically.
**Portfolio:** clearly separate from #001–#010.
**Round-A score:** 8.3/10.

## 06 — Borrowed Silence — KILL
**20s GIF:** mute machine B; its scheduled pulse jumps into the next compatible machine C, changing the sequence.
**State/order:** machine cycle + compatibility + one mute -> transfer skipped action -> execute.
**Depth:** scheduling chains are viable, but the identity is explicitly transfer of a property/action from donor to recipient. This is too close to #003 Borrowed Collision's portfolio identity even if timing differs. Renaming does not fix the structural collision.
**Heuristic:** “mute the harmful action” can backfire because it lands on a worse recipient, but that is precisely the transferable-property causal lesson already represented.
**Decision:** kill for portfolio collision rather than rescue with extra semantics.

## 08 — One-Way Wallpaper — KILL
**20s GIF:** peel a continuous strip around a room; exposed wall glyphs activate while peeled glyphs appear wrapped onto the next wall.
**State/order:** cyclic strip segmentation + peel interval + exposed/wrapped symbols -> PEEL -> transfer strip -> activate exposed set.
**20 min:** peel direction/length, wrap boundary, activation combinations.
**Hour 3/8:** weak. Without adding symbol types/interactions, optimal play trends toward interval/cyclic-set selection. Extra depth would come from a growing rule zoo.
**Heuristic:** “peel until desired glyph exposed” can activate a harmful glyph around the corner, but this pattern repeats quickly.
**Burden:** continuous-strip representation and corner readability are medium-high. **Decision:** kill for same-vocabulary depth failure.

## 09 — Deferred Gravity — KILL
**20s GIF:** select blue objects, rotate their future gravity arrow, press release; current motion completes, then all blue objects fall sideways.
**State/order:** object positions/velocities/class + pending class gravity -> choose pending gravity -> resolve current motion -> commit gravity -> resolve.
**20 min:** delayed commitment, class separation, support timing.
**Hour 3/8:** collapses toward ordinary gravity/platform puzzles with delayed input. Sustaining depth needs switches, materials, hazards, multiple gravity exceptions — extra mechanics.
**Heuristic:** “set gravity toward target” fails when current settling changes the support geometry first, but this is a timing twist rather than enough identity for a full campaign.
**Decision:** kill.

## 10 — Counterfeit Shadow — SURVIVE
**20s GIF:** swap the shadow silhouettes of a tall vase and a key-shaped object; real objects stay still, but a key-shaped optical sensor opens while a weight plate still reacts to the vase's real mass.
**State/order:** objects with physical identity + assignable shadow identity; sensors declare whether they read real or shadow property. SWAP SHADOWS -> recompute projected silhouettes deterministically -> sensors resolve in fixed order -> evaluate.
**20 min:** shadow-vs-real distinction; one shadow swap; sensor conjunction; occlusion-free initial cases; later spatial projection only if exact/readable.
**Hour 3/8:** good if depth comes from two simultaneous identity layers, limited shadow permutation, sensor predicates and scarce swaps. Risk: projection geometry can explode art/solver burden; Round B must prove a discrete representation rather than physics/lighting simulation.
**Heuristic:** “give the required silhouette to the sensor-facing object.” Counterexample: swapping silhouettes satisfies optical lock but the donor's new shadow trips a second detector while its real mass is still required on a plate; correct solution moves/chooses a different pair under a swap budget.
**Burden:** medium-high; discrete shadow footprints can control it. **Explainability:** potentially excellent with split real/shadow highlights. **Controller:** good. **Content:** high if sensor grammar stays tiny.
**Portfolio:** distinct; property *transfer* risk exists, but the core is dual identity/perception. Round B must reject any version where it becomes #003-style generic property lending.
**Round-A score:** 8.0/10 conditional.

## 12 — Weather Receipt — KILL
**20s GIF:** each action prints a weather card into a visible receipt queue; the oldest card pops and changes next turn's wind/rain.
**State/order:** environment + FIFO forecast tokens; ACTION emits token -> oldest token applies -> world resolves.
**20 min:** FIFO delay, planning two/three turns, token consequence.
**Hour 3/8:** deterministic but too abstract; with a small token vocabulary it becomes queue scheduling, while richer weather/world interactions require many secondary mechanics. GIF hook is weaker than survivors.
**Heuristic:** “print the weather you need next” fails due to FIFO latency, but once learned that is bookkeeping rather than evolving mastery.
**Decision:** kill.

## 15 — Museum of Echoed Weight — KILL
**20s GIF:** put a heavy statue on pedestal A; later pedestals visibly inherit its weight number despite displaying different objects, tilting bridges/scales.
**State/order:** ordered pedestal placements + copied weight register -> PLACE -> propagate weight -> resolve load checks.
**20 min:** copy source, sequence, thresholds.
**Hour 3/8:** likely collapses to arithmetic/threshold puzzles. Avoiding that requires adding many object properties, which would become generic property-copying and increase #003 collision.
**Heuristic:** “copy the heaviest available weight” fails on upper-bound supports, but variants remain numerical constraint satisfaction.
**Decision:** kill.

## 16 — Lighthouse Arbitration — SURVIVE
**20s GIF:** three lighthouse beams point at preferred moving ships. Player drags lighthouse priority A>B>C to B>A>C; the winning beam holds its ship while losing beams visibly bend to second-choice ships, producing a different collision-free escort assignment.
**State/order:** beams each have public ranked eligible targets; global/sector priority order; ships occupy deterministic lanes. SET PRIORITY -> process beams by priority, each claims best still-eligible target -> losing/conflicted beam takes next choice -> advance one tick -> evaluate safety/coverage.
**20 min:** one contested ship; second-choice fallback; moving eligibility windows; planning priority for next tick.
**Hour 3/8:** promising from ranked preference conflicts + temporal eligibility + limited priority edits, but danger of spreadsheet feel. Must remain <=5 beams/ships and visually spatial.
**Heuristic:** “put the beam with the fewest targets first.” Counterexample: scarce beam A claims ship X, forcing flexible B to Y, but C can only serve Y next tick; ordering B first sends B to X, A to Z and preserves Y for C's future window, satisfying all.
**Burden:** medium exact assignment simulator/solver. **Explainability:** strong if fallback arcs preview. **Controller:** strong. **Content:** high.
**Portfolio:** unlike #010 because player changes arbitration priority over simultaneous ranked claims, not labels/queue/tick pickup. Avoid passenger/gantry aesthetics.
**Round-A score:** 8.2/10.

## 22 — Missing Step — SURVIVE
**20s GIF:** a four-step assembly line loops [PUSH, CUT, TURN, STAMP]. Player crosses out CUT once; downstream gears re-phase, so later cycles align two machines that previously missed each other.
**State/order:** several small periodic tracks with explicit phase; DELETE one occurrence/type under case rule -> execute simultaneous ticks in fixed machine order -> cycle boundaries compact/re-phase -> evaluate produced sequence/state.
**20 min:** one loop; two synchronized loops; deletion changes period/phase; target requires temporary misalignment before final alignment.
**Hour 3/8:** strongest abstract depth candidate if the vocabulary stays operations + one deletion and interactions arise from phase arithmetic/spatial workpieces. Exact solver straightforward for bounded periods.
**Heuristic:** “delete the step that directly causes the bad output.” Counterexample: deleting bad STAMP shortens the loop and makes PUSH coincide with another machine's clamp on later cycles; deleting an apparently useful TURN instead re-phases STAMP into a safe window and still yields target orientation through the neighboring loop.
**Burden:** low-medium; deterministic periodic simulator + BFS/A*. **Explainability:** excellent with timeline preview/ghost next cycles. **Controller/800p:** excellent if <=4 tracks. **Content:** very high.
**Portfolio:** distinct from conserved-budget #005: no conserved scalar/network; distinct from #010: no moving queue/label service. Potential generic timing-puzzle analogue risk needs Round-B market/mechanic check.
**Round-A score:** 9.0/10.

## 27 — Glass Queue — KILL
**20s GIF:** make one divider opaque/transparent; each agent reacts only to first visible object ahead and cascades positions.
**State/order:** ordered agents/dividers + visibility + reaction rules -> TOGGLE -> scan/cascade -> stabilize.
**Depth:** mechanically viable, but direct comparison exposes it as Queue Sculptor with visibility replacing divider insertion. Keeping both would waste tournament diversity. Queue Sculptor has a cleaner physical verb and easier causal explanation; Glass Queue needs more visibility edge cases.
**Decision:** kill as dominated sibling, not because the underlying family is bad.

# Round-A result — 5 survivors
1. **Missing Step (#22)** — 9.0: best deterministic same-vocabulary depth/validator ratio.
2. **Queue Sculptor (#03)** — 8.5: extremely legible cascade, needs anti-bookkeeping proof.
3. **Fossil Forecast (#05)** — 8.3: strongest thematic/visual differentiation, medium simulation risk.
4. **Lighthouse Arbitration (#16)** — 8.2: ranked-claim conflict has depth, must beat spreadsheet feel.
5. **Counterfeit Shadow (#10)** — 8.0 conditional: high GIF value, must constrain shadow representation and prove not generic property transfer.

No sixth candidate retained merely to fill a bracket.

## Fresh collision/name check notes
Fresh exact-name searches on 2026-09-01 did not surface an obvious current game using the exact working names Queue Sculptor, Pressure Caption, Fossil Forecast, Borrowed Silence, One-Way Wallpaper, Deferred Gravity, Counterfeit Shadow, Weather Receipt, Museum of Echoed Weight, Lighthouse Arbitration or Glass Queue. `Missing Step` is noisy as ordinary phrase/title language and therefore should be treated as an internal working name, not a cleared commercial title. Exact-name absence is not trademark clearance.

Mechanic analogue cautions for Round B:
- Missing Step: compare against established time/sequence manipulation puzzle vocabulary; its differentiator must be deletion-induced period/re-phasing, not generic rewind/time control.
- Counterfeit Shadow: compare against shadow/projection puzzle games; keep deterministic dual-identity sensors rather than freeform lighting.
- Queue Sculptor/Lighthouse Arbitration: explicitly test whether the visual spatial consequence prevents them becoming assignment/queue spreadsheets.
- Fossil Forecast: exact erosion must remain inspectable and avoid physics simulation.

# NEXT ROUND-B ACTION
Run a deeper tournament among these five only. For each build 3 exact microcases with complete state/action traces (teaching, deceptive midgame, mastery), estimate bounded solver state size, define a hard mechanic-vocabulary ceiling, and perform fresh direct-mechanic analogue research. Attack repetition at hour 8 and portfolio collision again. Cut to 2–3 finalists; if a candidate cannot produce three trace-distinct cases under its vocabulary ceiling, kill it.