# GAME #010 — PHASE 5 CONCRETE CONTENT MAP

Date: 2026-08-31
Status: **PHASE 5 SUBSTANTIAL INCREMENT — 42-SLOT MAP + DEMO TRACES + LATE-GAME SKELETONS**
Game: Luggage Carousel Zero *(working title)*

Authority: `START_HERE.md` -> `STATUS.md` -> `GAME_INDEX.md` -> Game #010 tournament history -> `GAME10_THESIS.md` -> `GAME10_MECHANICS.md` -> `GAME10_MECHANICS_CORRECTION.md` -> `GAME10_CONTENT.md` -> this file.

This file uses the authoritative **adjacent-only ring swap** rule. Any older unrestricted-swap example is non-canonical.

---

## 1. Gap semantic clarification found during mapping

The 42-slot exercise exposed an imprecise phrase in earlier documents: a removal-created GAP does **not** shift the socket phase of any remaining bag. Occupancy always rotates one socket per ADVANCE with no compression. Replacing the consumed bag with GAP therefore preserves every other bag's trajectory.

What a GAP actually does is create a **persistent empty phase slot**. When that occupancy returns to pickup on a later circuit, that tick cannot serve a passenger. Under a finite tick budget, this can alter feasible service schedules and make an earlier consumption choice matter, but it never accelerates, delays, or reindexes another bag relative to the ring.

Therefore authoritative Phase-5 meaning is:
- `GAP_SIGNIFICANT`: replacing a specified GAP with a predicate-irrelevant but otherwise non-consumable dummy occupancy, or counterfactually keeping the consumed bag present, changes solvability/minimum ticks/service family because the empty phase returns at pickup;
- `REMOVAL_GAP_SIGNIFICANT`: the GAP created by a successful pickup later reaches pickup while passengers remain, and removing that blank return from the trace changes the certified family/feasibility;
- no case may claim a GAP “shifts” another bag's arrival phase.

This is a **content-language correction only**, not a mechanical change.

---

# 2. Concrete 42-slot campaign map

Notation: `N` ring sockets, `K` adjacent swaps/tick, `T` target tick-limit band, `W` maximum passenger predicate width. Tags use F1–F10 from `GAME10_CONTENT.md`.

| ID | Act | N | K | T | W | Primary tags | Slot obligation / distinct relationship |
|---|---|---:|---:|---:|---:|---|---|
| A01 | Ownership | 3 | 0 | 1 | 1 | F1 | Pure observe: fixed pickup label, incoming bag rotates under it. |
| A02 | Ownership | 4 | 1 | 1 | 1 | F1 | One adjacent S0 swap changes next pickup label; ownership test by case 2. |
| A03 | Ownership | 4 | 1 | 2 | 1 | F1,F6 | Label starts one edge beyond pickup-neighbor; stage one tick before use. |
| A04 | Ownership | 5 | 1 | 2 | 1 | F1,F6 | Required stage can use either side of ring; seam adjacency explicitly exercised. |
| A05 | Ownership | 4 | 1 | 3 | 1 | F1 | Two candidate labels, only timing distinguishes them; no trait clauses. |
| A06 | Ownership | 5 | 0 | 3 | 1 | F1 | Short K0 prediction: player forecasts exact three arrivals; no filler beyond 3 ticks. |
| A07 | Ownership | 5 | 1 | 2 | 1 | F1,F6 | Demo staging proof: current pickup label must stay, non-pickup swap required now for next passenger. |
| B01 | Identity | 4 | 1 | 2 | 2 | F1,F2 | First LABEL+SHAPE binding; bag trait stays with bag. |
| B02 | Identity | 5 | 1 | 3 | 2 | F2 | MARK replaces SHAPE; same movement grammar, new immutable dimension only. |
| B03 | Identity | 5 | 1 | 3 | 2 | F2,F3 | Two trait-equivalent candidates for P1, but only one useful later. |
| B04 | Identity | 5 | 1 | 3 | 2 | F2,F4 | Unique SHAPE class must survive an earlier broad predicate. |
| B05 | Identity | 6 | 1 | 3 | 2 | F3,F6 | Substitution choice coupled to away-from-pickup staging. |
| B06 | Identity | 6 | 1 | 4 | 2 | F4,F6 | Scarce MARK bag plus label-distance constraint; current service still straightforward. |
| B07 | Identity | 5 | 1 | 4 | 2 | F3,F4 | Three candidate bags collapse to two future-equivalence classes; choose by preservation. |
| B08 | Identity | 6 | 1 | 4 | 2 | F2,F6 | Act exam: alternating SHAPE/MARK passengers with a required two-tick label walk. |
| C01 | Consequence | 4 | 1 | 4 | 2 | F4,F5 | First exact intentional miss: serviceable scarce bag must pass and return later. |
| C02 | Consequence | 5 | 1 | 4 | 2 | F3,F5 | Immediate P1 service loses because alternate P1 bag arrives next tick and preserves P2 class. |
| C03 | Consequence | 5 | 1 | 4 | 2 | F5,F6 | Required intentional miss is achieved by staging a future label away from S0 rather than merely scrambling pickup. |
| C04 | Consequence | 6 | 1 | 5 | 2 | F4,F5,F6 | Preserve unique bag while moving required future label two edges across two ticks. |
| C05 | Consequence | 6 | 1 | 5 | 2 | F3,F5 | Two immediate-service choices exist across nearby ticks; only later one preserves queue matching. |
| C06 | Consequence | 6 | 1 | 6 | 2 | F4,F6 | Pickup-only label policy provably fails despite no required intentional miss. |
| C07 | Consequence | 7 | 1 | 6 | 2 | F3,F4,F5 | Candidate-set chain: P1 broad, P2 medium, P3 unique; earliest P1 service loses. |
| C08 | Consequence | 7 | 1 | 6 | 2 | F5,F6 | Consequence exam: non-pickup stage + one deliberate miss + seam swap later. |
| D01 | Gaps | 5 | 1 | 6 | 2 | F7 | First explicit blank-return lesson: consumed bag's GAP returns while P2 remains. |
| D02 | Gaps | 5 | 1 | 6 | 2 | F4,F7 | Scarce bag preservation must account for a future blank pickup tick. |
| D03 | Gaps | 6 | 1 | 7 | 2 | F5,F7 | Intentional miss chosen partly to avoid creating a blank return inside the critical service window. |
| D04 | Gaps | 6 | 1 | 7 | 2 | F6,F7 | Stage label during a tick whose incoming occupancy is GAP; blank tick is strategically productive, not filler. |
| D05 | Gaps | 6 | 1 | 7 | 2 | F7,F8 | Duplicate label positions allow one copy to be staged while an empty phase returns. |
| D06 | Gaps | 7 | 1 | 8 | 2 | F3,F7 | Which substitutable bag P1 consumes determines which trait-class absence later repeats as GAP. |
| D07 | Gaps | 7 | 1 | 8 | 2 | F4,F6,F7 | Required stage occurs before removal; resulting GAP return constrains the preserved scarce bag's second circuit. |
| D08 | Gaps | 8 | 1 | 9 | 2 | F7,F8 | Two GAPs at different phases plus duplicated labels; exact blank-order matters, not bag shifting. |
| D09 | Gaps | 8 | 1 | 9 | 2 | F5,F6,F7 | Act exam: intentional miss, non-pickup stage, then one removal-created blank return before final service. |
| E01 | Mastery | 5 | 1 | 6 | 2 | F3,F4,F6,F10 | Compact synthesis without gaps: substitution + scarcity + local staging. |
| E02 | Mastery | 6 | 1 | 7 | 2 | F4,F5,F6,F10 | Scarce bag, intentional miss, displacement-sensitive staging. |
| E03 | Mastery | 6 | 1 | 7 | 3 | F2,F3,F6,F10 | First justified 3-clause predicate; third clause splits an otherwise equivalent candidate class. |
| E04 | Mastery | 6 | 1 | 8 | 2 | F5,F7,F8,F10 | Intentional miss changes which duplicated-label copy is useful when blank returns. |
| E05 | Mastery | 7 | 1 | 8 | 2 | F3,F6,F7,F10 | Substitution choice changes which trait absence occupies a future blank phase; staged label must cross seam. |
| E06 | Mastery | 7 | 1 | 9 | 3 | F4,F6,F7,F10 | Unique bag + local displacement + one meaningful removal gap + selective 3-clause card. |
| E07 | Mastery | 8 | 1 | 10 | 2 | F3,F4,F5,F6,F10 | Longest K1 queue-coupling case; no third clause and no K2 to keep readability. |
| E08 | Mastery | 5 | 2 | 6 | 2 | F6,F9,F10 | First K2-significant case: needed label two edges away this tick; identical case impossible at K1. |
| E09 | Mastery | 6 | 2 | 8 | 2 | F7,F8,F9,F10 | K2 used for two spatial repairs around a returning blank; duplicate labels create alternatives. |
| E10 | Mastery | 6 | 2 | 8 | 3 | F4,F5,F6,F9,F10 | Final bounded synthesis: K2 significant, scarce-bag miss, two-edge stage, third clause changes candidate competition. |

### Map audit
- 42 slots exactly: A7 + B8 + C8 + D9 + E10.
- K0: exactly 2 early cases (A01, A06).
- K2: exactly 3 mastery cases (E08–E10), all N<=6/T<=8.
- Three-clause target: only E03, E06, E10; never used as raw difficulty padding.
- F6 staging appears throughout and every counted F6 candidate must satisfy `STAGING_SIGNIFICANT` under adjacency.
- F7 is reserved for persistent empty-phase consequences; no slot claims other bags are phase-shifted.

---

# 3. Seven exact demo cases and hand traces

All demo swaps are adjacent. `S0` is pickup. Occupancy shown `[S0..]`; ADVANCE rotates right. Bag traits not referenced by a passenger may be arbitrary but remain explicit for data completeness.

## DEMO-01 / A01 — “The Gantry Stays”
Definition:
- N=3, K=0, ticks=1
- L=`[R,B,G]`
- bags: A=square/dot, B=triangle/star, C=round/stripe
- O=`[A,B,C]`
- P1=`LABEL=R`

Trace:
1. ADVANCE -> occupancy before pickup resolution `[C,A,B]`; C arrives under fixed S0 label R.
2. P1 matches; remove C -> `[-,A,B]`; win.

Teaching proof: the bag moved; R did not. No player edit exists to confuse ownership.

## DEMO-02 / B01 — “Bag Trait Comes With It”
Definition:
- N=4, K=1, ticks=1
- L=`[B,R,G,Y]`
- A=round/dot, B=triangle/star, C=round/stripe, D=square/dot
- O=`[A,B,C,D]`
- P1=`LABEL=R AND SHAPE=square`

Trace:
1. adjacent SWAP S0<->S1 -> L=`[R,B,G,Y]`.
2. ADVANCE -> D reaches S0; D is square and S0 is R -> consume; win.

Counterfactual: ADVANCE without swap gives D under B, so LABEL fails while SHAPE still matches. This isolates socket label from bag shape.

## DEMO-03 / A07 — “Stage Before You Need It”
Definition:
- N=5, K=1, ticks=2
- L=`[R,B,G,Y,P]`
- A=triangle/dot, B=round/star, C=triangle/stripe, D=square/dot, E=round/dot
- O=`[A,B,C,D,E]`
- P1=`LABEL=R AND SHAPE=round`
- P2=`LABEL=G AND SHAPE=square`

Winning trace:
1. SWAP S1<->S2 -> L=`[R,G,B,Y,P]`. This swap is not incident to pickup.
2. ADVANCE -> E reaches S0, matches R+round, is consumed. O=`[-,A,B,C,D]`.
3. SWAP S0<->S1 -> L=`[G,R,B,Y,P]`.
4. ADVANCE -> D reaches S0, matches G+square, consumed; win.

`STAGING_SIGNIFICANT` proof:
- If swaps on edges not incident to S0 are forbidden, G begins at distance 2 from S0.
- Tick1 must preserve R at S0 to serve P1 within the 2-tick budget.
- Tick2 offers only one adjacent swap, so G cannot reach S0 from S2.
- Therefore pickup-only swapping makes the case unsolvable. Exact family condition satisfied.

## DEMO-04 / B04 — “Keep the Only Square”
Definition:
- N=4, K=1, ticks=4
- L=`[R,B,G,Y]`
- A=triangle/star, B=round/dot, C=round/dot, D=square/dot
- O=`[A,B,C,D]`
- P1=`LABEL=R AND MARK=dot`
- P2=`LABEL=R AND SHAPE=square`

Intended trace:
1. D (square/dot) is about to arrive. SWAP S0<->S1 -> pickup becomes B; ADVANCE: D arrives, MARK matches but LABEL misses; D survives.
2. SWAP S0<->S1 -> pickup R; ADVANCE: C(round/dot) arrives and serves P1. C removed -> GAP.
3. ADVANCE: B(round/dot) arrives; P2 needs square, miss.
4. ADVANCE: A(triangle/star) arrives; P2 still misses. This line does **not** yet return D within N=4, so it exposes a budget defect if ticks=4.

Repair for canonical demo data: set ticks=5.
5. ADVANCE: D returns to S0 under R and serves P2; win.

Certified relationship: P1 has multiple MARK=dot candidates, but consuming D at tick1 destroys the only square candidate for P2. The case introduces substitution/scarcity. It also contains an intentional miss, but the tutorial copy emphasizes candidate preservation rather than naming the later F5 metric.

## DEMO-05 / C01 — “The Right Bag Must Pass”
Definition:
- N=3, K=1, ticks=4
- L=`[R,B,G]`
- A=triangle/star, C=round/dot, D=square/dot
- O=`[A,C,D]`
- P1=`LABEL=R AND MARK=dot`
- P2=`LABEL=R AND SHAPE=square`

Winning trace:
1. D is immediately serviceable for P1, but is unique square. SWAP S0<->S1 -> L=`[B,R,G]`; ADVANCE: D reaches S0 under B, misses intentionally.
2. SWAP S0<->S1 -> L=`[R,B,G]`; ADVANCE: C reaches S0, serves P1; C becomes GAP.
3. ADVANCE: A reaches S0, misses P2.
4. ADVANCE: D returns to S0 under R, serves P2; win.

`INTENTIONAL_MISS` proof: the no-swap tick1 line serves D to P1 immediately; afterward no square bag remains, so P2 is impossible. Every winning family must keep D through tick1. This is a true anti-greedy lesson.

## DEMO-06 / D01 — “Empty Phase Returns”
Definition:
- N=3, K=1, ticks=5
- L=`[R,B,G]`
- A=triangle/star, B=round/dot, C=square/dot
- O=`[A,B,C]`
- P1=`LABEL=R AND SHAPE=square`
- P2=`LABEL=R AND SHAPE=round`

Trace:
1. ADVANCE: C reaches S0 under R, serves P1 -> O=`[-,A,B]`.
2. ADVANCE: B reaches S0 under R, serves P2 immediately -> win.

This trace teaches gap creation visually but does not make the return significant. Therefore it **cannot** earn F7 admission by itself. For the full-game D01 slot, the certified variant must retain passengers beyond the first circuit so the created GAP returns to pickup while service is still pending. The demo is allowed to teach the visual rule before the campaign later requires `REMOVAL_GAP_SIGNIFICANT`.

## DEMO-07 / C03+D preview finale — “Stage, Pass, Then Collect”
Definition target:
- N=5, K=1, ticks=6
- L=`[R,B,G,Y,P]`
- bag trait classes: one scarce square/dot S; two round/dot alternatives R1/R2; one triangle/star T; one round/stripe Q
- passenger queue: P1 broad `LABEL=R AND MARK=dot`; P2 `LABEL=G AND SHAPE=round`; P3 `LABEL=R AND SHAPE=square`
- initial ordering must place S as first incoming, R1 as second incoming, and R2 on a later circuit.

Canonical family requirements for the data-population pass:
1. tick1 must both preserve S through an intentional miss **and** perform a non-pickup stage that is necessary to make G reachable for P2;
2. P1 must then consume a non-square dot bag;
3. P2 must consume a round bag under staged G;
4. S must return later and satisfy P3 under R;
5. at least one removal-created GAP must be visible before completion, but demo admission does not require its later return to be significant;
6. forbidding non-pickup swaps or forcing earliest P1 service must each make the case unsolvable.

This finale is intentionally left as a **solver-populated exact instance**, not hand-waved runtime data: its relationship contract is frozen, but Phase 5 will not claim exact certification until enumeration confirms a compact state satisfying all six requirements. If enumeration fails, replace only bag/label relationships or tick slack; do not add mechanics.

### Demo trace audit
- Demos 01–05 have exact hand traces; Demo 04 required and records a concrete tick-limit repair from 4 -> 5.
- Demo 06 is deliberately visual-teaching only and explicitly does not claim F7 significance.
- Demo 07 has exact relationship/counterfactual acceptance requirements but still needs solver-backed instance population. Therefore Phase 5 is not yet closed.

---

# 4. Twelve late-game skeletons with distinct normalized families

These are relationship skeletons for E/D slots, not unverified exact case data. Each must later be solver-instantiated and deduped under value renaming.

| Skeleton | Target slots | Distinct normalized trace/counterfactual family |
|---|---|---|
| L1 Scarce-first-pass | E02 | Earliest service consumes unique future class; winning family has required miss then later return. |
| L2 Two-edge stage | E08 | Required pickup label begins distance 2; K2 reaches it same tick; identical K1 state fails. `K2_SIGNIFICANT`. |
| L3 Split repair | E09 | Two swaps are required on different ring edges in one tick; moving one label two edges is insufficient. |
| L4 Displacement debt | E01/E02 | A required non-pickup stage displaces another useful label; later service must repair that specific displacement. |
| L5 Seam migration | E05 | Winning label path crosses S(N-1)<->S0 seam; linearized adjacency policy fails. |
| L6 Duplicate near/far | D05/E04 | Same label value exists twice; which spatial occurrence is mobilized changes minimum service family. `DUPLICATE_POSITION_SIGNIFICANT`. |
| L7 Blank-return deadline | D07/E06 | Removal-created GAP returns to pickup while queue remains; one finite-budget service opportunity is blank. Counterfactual without blank return wins earlier. |
| L8 Consume-which-absence | D06/E05 | Two substitutable bags can serve P1; whichever is consumed determines which trait class is absent on its later phase, changing later queue feasibility. |
| L9 Productive blank tick | D04 | Incoming GAP means no service is possible, but the tick is used to stage a label away from pickup; banning non-pickup swaps loses. |
| L10 Three-clause split | E03 | Third clause partitions two candidates that are identical under the first two clauses; removing clause changes winning served-bag family, proving width is substantive. |
| L11 Branch-then-converge | E07 | At least two viable first label states exist, but only one service-order family preserves a scarce late candidate; not a forced-opening puzzle. |
| L12 Compound finale | E10 | Required miss + K2-significant two-edge local movement + scarce candidate + later blank return; each counterfactual independently breaks or changes the certified family. |

### Material-difference proof standard
Two skeletons do not count as distinct merely because entities or ring size differ. The accepted representative must have a different tuple over:
`(required_miss, nonpickup_stage, local_displacement, duplicate_position, k2_required, removal_gap_return, substitution_choice, scarce_class, 3clause_split, opening_branch_class)`.

The twelve skeletons above intentionally occupy different tuples; L12 combines several but does not replace the simpler representatives.

---

# 5. Family coverage freeze candidate

These are **minimum accepted-case counts** across the final 36–48 campaign, not merely tags authored on paper. A single case can satisfy multiple families.

| Family | Minimum | Target band | Admission evidence |
|---|---:|---:|---|
| F1 Alignment | 5 | 6–8 | next-arrival / fixed-label relationship materially used |
| F2 Trait binding | 7 | 8–12 | trait clause changes candidate set |
| F3 Substitution | 7 | 8–12 | >=2 candidates and choice changes later family/feasibility |
| F4 Scarcity preservation | 7 | 8–12 | unique/near-unique class must survive earlier opportunity |
| F5 Intentional miss | 6 | 7–10 | forced-earliest-service counterfactual loses |
| F6 Label staging | 10 | 12–18 | exact `STAGING_SIGNIFICANT` under adjacency |
| F7 Gap/empty phase | 6 | 7–10 | >=3 must be `REMOVAL_GAP_SIGNIFICANT`; no phase-shift claims |
| F8 Duplicate-label position | 4 | 5–8 | spatial duplicate counterfactual changes solution/min ticks/family |
| F9 K2 bandwidth | 2 | 2–3 | exact `K2_SIGNIFICANT`; never >3 campaign slots |
| F10 Synthesis | 6 | 7–10 | >=3 independently proven family relationships |

Campaign release gate: at least **30 accepted cases must be pairwise non-duplicate by normalized trace/counterfactual family**, even if the shipped total is 36–48. This preserves the Phase-3 empirical gate against apparent volume built from cosmetic variants.

---

# 6. Repetition repair rules frozen from the map

The concrete map reveals four likely repetition traps and defines relationship-only repairs:

1. **Too many 'walk label toward S0' puzzles.** Repair by coupling the stage to displacement debt, candidate preservation, a productive blank tick, or seam route. Do not add longer label distances merely to increase difficulty.
2. **Too many scarcity cases that are just 'don't use square yet'.** Repair by varying substitutable candidate sets, predicate dimension causing scarcity, and the tick on which the scarce bag becomes tempting.
3. **Gap cases falsely advertised as phase shifting.** Repair by requiring a returned empty pickup phase to change feasible schedule or by making a blank tick useful for staging. Never claim other bags were shifted.
4. **Three-clause cards as difficulty inflation.** Repair by deleting the third clause unless a counterfactual proves it changes candidate competition/service family.

If fewer than six genuine F7 cases survive exact instantiation, reduce Act D count and reallocate slots to F3/F4/F6 synthesis rather than inventing a new gap mechanic. The 42 target is subordinate to strong-case quality and 36-case release floor.

---

# 7. Expansion boundaries

Post-launch or extra campaign content may vary only:
- N within canonical ceiling;
- initial occupancy including GAP count;
- label multiset and adjacent positions;
- legal shape/mark/label values;
- passenger queue/predicate combinations under the same grammar;
- tick limit and K within frozen envelopes;
- tutorial-only socket mask only in onboarding-style content.

Expansion may **not** add multiple pickups, bag steering, label movement on ADVANCE, non-adjacent swaps, extra predicate operators, passenger impatience, score multipliers, consumable swaps, real-time execution, branching narrative rules, power-ups, blockers, conveyor construction or hidden information without reopening product/mechanical architecture.

---

# 8. Phase-5 state after this increment

Completed now:
- all 42 target slots mapped;
- adjacency-correct family distribution established;
- exact gap meaning corrected without changing mechanics;
- five demo cases fully exact and hand-traced, one visual gap-teaching case traced, one finale relationship contract frozen;
- staging demo proves `STAGING_SIGNIFICANT`;
- 12 distinct late-game skeleton families defined;
- minimum/target per-family coverage proposed at implementation-ready precision;
- repetition repair rules and expansion boundaries frozen.

Still required before Phase 5 can close:
1. instantiate/certify DEMO-07 exactly with solver or bounded exhaustive enumeration;
2. produce exact F7 variants proving at least three `REMOVAL_GAP_SIGNIFICANT` cases and validate the family is genuinely worth six campaign slots;
3. exact-check the 42-slot map for family minima after solver-populated cases begin replacing skeletons;
4. consolidate the gap clarification into `GAME10_CONTENT.md` or final spec authority;
5. if those checks pass without another mechanical contradiction, close Phase 5 and begin Phase 6 UX / Presentation Architecture.

**PHASE 5 ACTIVE. DESIGN COMPLETE = NO.**