# GAME #014 — PHASE 2 CONCEPT TOURNAMENT — ROUND B

Date: 2026-09-02
Status: COMPLETE — six semifinalists cut to three; no winner selected.
Authority: `START_HERE.md` -> `STATUS.md` -> `GAME_INDEX.md` -> `GAME14_RESEARCH.md` -> `GAME14_TOURNAMENT.md` -> this file.

## Method
Round B attacks case-family depth rather than adding rescue mechanics. Each semifinalist gets five increasing abstract cases. `E` is the naive finite enumeration size before constraint pruning. A concept survives only if several cases have a short human route based on its distinctive grammar, not merely trying states. State counts are comparative design estimates, not implementation benchmarks.

## 1. Negative Casting — FINALIST
Canonical Round-A model: socketed opaque blockers; fixed lights and walls; target cells classify LIT/L1_ONLY/L2_ONLY/BOTH.

| Case | Structure / E | Short plausible human route | Carrying deduction |
|---|---|---|---|
| NC1 | 2 blockers x2 states; 1 wall; E=4 | LIT endpoint forbids Q-long; BOTH then forces P-long | forbidden-light -> BOTH decomposition |
| NC2 | 3 blockers x2; 2 walls; E=8 | W2 LIT removes two orientations; W1 exclusive cell identifies sole L1 producer | cross-wall pruning + unique producer |
| NC3 | 3 blockers x3; 2 walls; E=27 | target transition at wall cell 3 cannot be made by short masks; endpoint forces B2 orientation, then exclusives resolve others | interval endpoint + attribution |
| NC4 | 4 blockers x3; 2 walls; E=81 | two candidate orientations look identical on W1 but differ on W2; W2 L2_ONLY kills one equivalence class; BOTH cells force complementary L1 coverage | projection-equivalence split across walls |
| NC5 | 4 blockers x4; 3 walls; E=256 | protected LIT cells prune 7/16 local states; one wall transition fixes extent, second wall fixes light attribution, third wall resolves blocker identity | multi-surface chained deduction |

Human depth: strong. The same physical blocker participates in several projections, so the useful representation is not independent target cells. Three viable campaign families already exist without new rules: protected-negative-space cases; endpoint/extent cases; cross-wall identity cases. Later content may combine them.

False-depth attack: if every mask is arbitrary, the game becomes exact-cover. Therefore future mechanical spec must require geometrically coherent projection masks (contiguous/structured under the discrete projection model) and authored human deductions. Certifier growth is tiny: with 6 blockers x4 orientations E=4096 before pruning; deterministic exhaustive certification is practical.

Handheld/controller: strong if wall cells are large and channel class has symbol redundancy, not color-only coding. 20-minute demo can teach LIT -> exclusive -> BOTH -> second wall with 4 cases. Authoring multiplication: low-to-moderate; one blocker geometry creates masks across walls automatically.

Verdict: SURVIVE.

## 2. The Missing Reflection — FINALIST
Canonical model: discrete top-down room, fixed ports/objects, mirror sockets with 2–3 orientations, bounded deterministic rays.

| Case | Structure / E | Short plausible human route | Carrying deduction |
|---|---|---|---|
| MR1 | 2 mirrors x2; E=4 | P forbids B; first mirror state leading to B is eliminated; Q requirement fixes M2 | forbidden-ray + unique source |
| MR2 | 3 mirrors x2; E=8 | P/Q share M2; each individually allows both states, but their forbidden sets intersect only in one M2 state | shared-mirror coupling |
| MR3 | 4 mirrors x2; max 2 bounces; E=16 | two P paths share first segment; required A makes later branch impossible, forcing earliest divergence at M1; that fixes Q occlusion order | first-divergence -> nearer-hit |
| MR4 | 4 mirrors x3; E=81 | required C has one feasible reflected predecessor after forbidden D removes a whole branch; propagate impossibility backward through two mirrors | backward path impossibility |
| MR5 | 5 mirrors x3; max 2 bounces; E=243 | negative goals prune two path classes, shared mirror resolves a port pair, final positive object is unique-source | class pruning + shared coupling + unique source |

Human depth: good, but only under a strict bounce budget. Two-bounce reasoning remains inspectable; three-plus repeated bounces risks tracing bookkeeping rather than insight. Unlike Casting Call, mirror state changes *where a path goes*, so downstream feasibility can propagate backward; blockers merely remove fixed sightlines.

False-depth attack: state count itself is harmless (3^7=2187), but visual path length is the real complexity cost. Future spec should cap meaningful reflected paths at two mirror interactions for ordinary campaign cases; any capstone exception needs human-path evidence.

Handheld/controller: acceptable, weaker than Casting Call/Negative Casting. Port-select plus step-through physical ray path is mandatory; it may show current geometry but never solution correctness. 20-minute demo can teach direct forbidden path, one reflection, shared mirror, then two-bounce first-divergence. Content burden: moderate because rooms must be visually legible and path collisions authored carefully.

Verdict: SURVIVE.

## 3. Ink Debt — KILL
Rule: stamp mask deposits its color on blank cells and erases occupied overlap to blank.

| Case | Structure / E | Human route observed | Diagnosis |
|---|---|---|---|
| ID1 | A/B/C, fixed use; E=6 | unique final colors force relative order; blank overlap confirms pair interaction | precedence plus provenance |
| ID2 | 4 stamps; E=24 | protected final color forces one stamp late; two required blanks imply overlapping pairs | still pairwise precedence/parity-like bookkeeping |
| ID3 | 5 stamps, one optional; <=326 sequences | unique provenance selects subset, then precedence chain | subset choice + ordering, no new grammar |
| ID4 | 5 dense masks; E=120 | blank cells can be caused by many last-two interactions; shortest reliable route branches over candidate late stamps | factorial search begins to dominate |
| ID5 | 6 stamps; E=720 | non-pairwise-looking three-way overlaps depend on full local history; player must simulate candidate sequences | history execution, not clean deduction |

The destructive blank state does create information, but it is unstable information: a blank can be produced by many histories and later resurrected by another stamp. At low density, puzzles collapse to precedence/provenance; at high density, the player tracks full local histories. There is no clean middle family demonstrated across five cases. Quotienting commuting disjoint stamps helps the certifier, not the human grammar.

Handheld visual feedback is excellent and authoring cheap, but the 20-minute demo would teach a rule more elegantly than the hour-3 game can deepen it. Adding special inks, protected cells, or stamp powers would be rescue-feature inflation and is forbidden this round.

Verdict: KILL — fails Round-A requirement for robust blank-state/non-pairwise depth.

## 4. False Bottom — KILL
Rule: visible top assignments plus hidden support orientation/collision/forbidden zones in socketed positions.

| Case | Structure / E | Human route observed | Diagnosis |
|---|---|---|---|
| FB1 | 2 objects x2 supports; E=4 | visible slots force objects; hidden exact-one support fixes orientation | hidden layer genuinely resolves ambiguity |
| FB2 | 3 objects x2; E=8 | forbidden hidden cell eliminates one orientation; collision forces neighbor | good local support chain |
| FB3 | 4 objects x2; E=16 | top-equivalent objects swap; bottom constraints break symmetry | assignment CSP + support legality |
| FB4 | 4 objects x3; E=81 | visible arrangement can be solved first; then bottom orientations are a separate exact-cover problem | layers decouple |
| FB5 | 5 objects x3; E=243 | strongest route is enumerate top-compatible assignment, then reject hidden collisions | hidden legality becomes post-hoc validator |

The hook survives tiny cases but fails the centrality test as complexity rises. Either the top arrangement is obvious and the bottom is a second CSP, or top assignment is hard and hidden supports mostly reject completed candidates. The two layers do not produce enough alternating inference without introducing extra support semantics/resources, which would be rescue features.

Certifier is trivial, controller/handheld presentation is good with x-ray toggle, and content burden is moderate. Those strengths do not fix the reasoning split.

Verdict: KILL — Round-A risk confirmed: hidden legality trends toward post-hoc validation.

## 5. Casting Call — FINALIST
Rule: fixed actors/seats; movable flats choose discrete track positions; each position blocks a precomputed seat-actor sightline set; each seat requires an exact visible actor subset.

| Case | Structure / E | Short plausible human route | Carrying deduction |
|---|---|---|---|
| CC1 | 2 flats x2; E=4 | required-visible A forbids one F1 position; forbidden B then forces F2 | protected sightline -> required blocker |
| CC2 | 3 flats x3; E=27 | one F2 position blocks two forbidden actors for different seats; track exclusivity makes it forced | blocker-sharing + exclusivity |
| CC3 | 3 flats x4; E=64 | nearer position subsumes far blocking but also hides required C, so far position is forced; second seat resolves remaining flat | depth dominance with protected visibility |
| CC4 | 4 flats x4; E=256 | two seats demand complementary exact subsets; candidate blockers that solve S1 violate S2, leaving one shared position class | exact-set complement + cross-seat coupling |
| CC5 | 5 flats x4; E=1024 | preserve three required rays first, reducing legal positions; two forbidden rays then form a shared blocker obligation; track collision resolves final symmetry | negative pruning -> blocker-sharing -> track coupling |

Human depth: strong and extremely legible. Its deductions are monotone: flats only block; required-visible rays prune positions permanently, and forbidden-visible actors demand coverage. That makes reasoning cleaner than mirrors but potentially less deep. The key hour-3 question is whether blocker-sharing/depth/track interactions sustain variety or all cases feel like set cover.

Certifier growth remains modest (6 flats x5 positions = 15,625). Controller/handheld readability is best in field: cycle flat, move along track, select seat overlay. 20-minute demo can reach multi-seat blocker-sharing quickly. Authoring burden low because visibility masks derive from stage geometry.

Verdict: SURVIVE.

## 6. Misprint Press — KILL
Rule: first plate to touch a blank cell permanently claims it; later plates cannot overwrite.

| Case | Structure / E | Human route observed | Diagnosis |
|---|---|---|---|
| MP1 | 3 fixed plates; E=6 | each target winner yields A<B<C | pure precedence DAG |
| MP2 | 4 fixed plates; E=24 | multiple cells add precedence edges; transitive closure solves | pure DAG |
| MP3 | 3 plates x2 rotations; E=48 | target cells prune rotations, then remaining solve is DAG | discrete configuration CSP + DAG |
| MP4 | 4 plates x2 rotations; E=384 | one rotation changes several precedence obligations, giving useful coupling | SAT/CSP over rotations, then DAG |
| MP5 | 5 plates, optional one, rotations; >3000 raw | provenance chooses subset/configuration; all ordering information still decomposes into pairwise `winner before loser` edges | no irreducible non-pairwise order grammar |

This fails its explicit existential Round-A test. For any fixed set of transformed plates, every colored final cell says exactly: target-color plate must precede every differently colored plate covering that cell. The ordering problem is therefore a directed precedence graph. Rotation/selection can make choosing the graph nontrivial, but that changes the game into configuration CSP followed by topological sorting rather than producing a richer printing deduction grammar.

Excellent animation and tiny technical burden are insufficient. Adding drying, overwrite classes, pressure, or plate degradation would be rescue mechanics.

Verdict: KILL.

# Cross-semifinal comparison

## Visibility cluster: Negative Casting vs Missing Reflection vs Casting Call
All three survive because their reasoning is now demonstrably different:
- **Negative Casting:** combine multiple light-channel projections into target negative-space classes; strongest deduction is contribution attribution across surfaces.
- **Missing Reflection:** orientation redirects paths; strongest deduction is first-divergence/backward path feasibility with bounded reflections.
- **Casting Call:** blockers monotonically remove fixed sightlines; strongest deduction is protected-ray pruning plus shared coverage/track coupling.
They share a visibility theme but not a state-transition grammar. Round C must still kill any whose campaign converges into repeated set-cover.

## Ink cluster: Ink Debt vs Misprint Press
Both die, for opposite structural reasons. Misprint Press is too monotone and compiles to precedence once configurations are fixed. Ink Debt is non-monotone, but that extra state makes dense cases history-simulation rather than yielding a stable human deduction vocabulary.

## False Bottom
Dies independently: hidden supports matter in microcases but increasingly separate into legality checking after visible assignment rather than alternating with visible deductions.

# Comparative burden snapshot

| Concept | Distinct human grammar | Raw certifier growth | Handheld readability | Authoring multiplication | 20-min demo | Hour-3 risk |
|---|---|---|---|---|---|---|
| Negative Casting | HIGH | LOW | HIGH | LOW-MED | HIGH | exact-cover/set-cover convergence |
| Missing Reflection | HIGH | LOW | MED | MED | HIGH | ray-tracing bookkeeping |
| Ink Debt | MED-LOW | MED factorial | HIGH | LOW | HIGH | sequence simulation |
| False Bottom | MED | LOW | HIGH | MED | MED-HIGH | layer decoupling/post-hoc validation |
| Casting Call | HIGH | LOW | VERY HIGH | LOW | VERY HIGH | repeated blocker set-cover |
| Misprint Press | LOW-MED | MED factorial | HIGH | LOW | HIGH | DAG/toposort repetition |

# Round-B result
Field cut **6 -> 3 finalists**:
1. **Negative Casting**
2. **The Missing Reflection**
3. **Casting Call**

Killed: **Ink Debt, False Bottom, Misprint Press**.

No Game #014 winner is selected yet.

# ROUND C failure hypotheses / NEXT TESTS
Round C is a product-and-campaign tournament, not another toy-CSP pass. Give equal destructive treatment to all three finalists.

### Negative Casting — failure hypothesis
By hour 3, every puzzle may feel like the same protected-cell / coverage attribution problem with different masks. Test a 20–30 case campaign grammar: at least four mechanically distinct case families must arise from the frozen projection rule without arbitrary mask authoring. Verify that multi-wall cases remain readable and do not require color-only channel coding. Attack whether a trailer can explain BOTH/L1_ONLY/L2_ONLY without looking like a technical shadow editor.

### The Missing Reflection — failure hypothesis
The hook may be strongest but repeated two-bounce ray tracing may become visual bookkeeping, especially on handheld. Test a campaign progression under a strict ordinary-case two-reflection cap; demand at least four deduction families that recombine rather than merely longer rays. Simulate a 20-minute demo and an hour-3 case. Kill if readability requires solver-like path overlays or if absence goals dominate every solve.

### Casting Call — failure hypothesis
Monotone blocking may make the cleanest demo but the shallowest full game: after learning preserve-required-rays then cover-forbidden-rays, later puzzles may be set-cover variants. Build a 20–30 case campaign grammar using only flats/tracks/seats/actors and exact visibility sets. Demand qualitatively different families from blocker-sharing, depth dominance, track competition, multi-seat complements, and symmetry-breaking. Kill if variety requires adding lights, moving actors, timed cues, or special flat powers.

## Exact Round-C required output
1. Draft 20–30-case campaign skeleton for each finalist at family level (not 60–90 fully authored puzzles).
2. Simulate first 20 minutes, representative hour-1 and hour-3 cases for each.
3. Score hook/GIF, human insight, repetition, tutorial burden, handheld/controller UX, content burden, technical burden, portfolio distance, demo strength and commercial framing.
4. Perform fresh market/analogue check because final selection is commercially consequential.
5. Choose exactly one winner or kill/rework the whole field if none passes.
6. If a winner passes, begin Phase 3 Product Thesis in a new `GAME14_PRODUCT_THESIS.md`; do not start implementation.
