# GAME #010 — PHASE 5 CONTENT VALIDATION PASS

Date: 2026-08-31
Status: **DEMO FINALE EXACT / GAP FAMILY UNDER ADVERSARIAL VALIDATION**

Authority: previous active Game #010 authorities -> `GAME10_CONTENT_MAP.md` -> this file.

## 1. Exact DEMO-07 instance

The relationship-only finale from `GAME10_CONTENT_MAP.md` has now been instantiated exactly without adding mechanics.

### Definition
- N=5, pickup S0
- K=1 adjacent swap/tick
- tick_limit=7
- labels: `L=[R,B,G,Y,P]`
- bags:
  - Q = round / stripe
  - R2 = round / dot
  - R1 = round / dot
  - S = square / dot  *(scarce square)*
  - T = triangle / star
- initial occupancy `O=[Q,R2,R1,S,T]`
- passengers:
  - P1 = `LABEL=R AND MARK=dot`
  - P2 = `LABEL=G AND SHAPE=round`
  - P3 = `LABEL=R AND SHAPE=square`

Initial future arrivals are T, S, R1, R2, Q, then the surviving second circuit.

### Hand trace
1. Before tick 1, adjacent SWAP S1<->S2: `[R,B,G,Y,P] -> [R,G,B,Y,P]`. This is a non-pickup stage. ADVANCE: T arrives under R but MARK=star, so P1 misses naturally.
2. SWAP S0<->S1 -> `[G,R,B,Y,P]`. ADVANCE: S(square/dot) arrives. It would satisfy P1's MARK but fails LABEL, so the scarce square intentionally survives.
3. SWAP S0<->S1 -> `[R,G,B,Y,P]`. ADVANCE: R1(round/dot) arrives under R, serves P1 and is removed.
4. SWAP S0<->S1 -> `[G,R,B,Y,P]`. ADVANCE: R2(round/dot) arrives under G, serves P2 and is removed.
5. SWAP S0<->S1 -> `[R,G,B,Y,P]`. ADVANCE: Q(round/stripe) arrives; P3 needs square, miss.
6. ADVANCE: T arrives; P3 misses.
7. ADVANCE: S returns under R; P3 matches R+square and is removed. WIN exactly on final tick.

### Counterfactual checks
- **Earliest-service policy fails:** if S is served to P1 on tick 2 under R, no square bag remains for P3. Thus the tick-2 miss is strategically required in the intended family.
- **Pickup-only swap policy fails:** exhaustive bounded reasoning/search found no solution if swaps on edges not incident to S0 are forbidden. A non-pickup stage is therefore required somewhere in every winning family; `STAGING_SIGNIFICANT = true`.
- The shown line demonstrates the stage before the scarce-bag miss; another valid winning trace may stage G later, so the authored lesson must teach the dependency rather than falsely claim the shown action order is unique.
- No unrestricted swap is used; seam adjacency remains legal but unnecessary in this instance.

This exact instance replaces the relationship-only DEMO-07 placeholder in `GAME10_CONTENT_MAP.md` for subsequent authority consolidation.

---

## 2. Gap-family adversarial audit

A second formal pass was applied before inventing six F7 cases.

### Proven limitation
With canonical movement `O_after[(i+1) mod N]=O_before[i]` and no compression, replacing a consumed bag with GAP cannot alter any other surviving bag's future socket index. Therefore:
- GAP is not a spacing operation on surviving bags;
- it cannot advance/delay another bag;
- it cannot change label inheritance of another bag except indirectly through player decisions made on a blank tick;
- a removal GAP's native effects are exactly **absence of the consumed bag on later circuits** plus a guaranteed no-pickup opportunity whenever the GAP reaches S0.

### Consequence for content taxonomy
F7 remains potentially useful, but only as **empty-phase / second-circuit scheduling**, not as an independent “phase shift” system. A strong F7 case must prove at least one of:
1. a returning GAP creates a guaranteed blank tick used for a required local label stage/repair that would be unsafe or impossible on the corresponding occupied trace;
2. the identity/phase of the removed bag determines which later circuit position is guaranteed empty, and that absence changes a later service family under finite ticks;
3. two existing/created GAPs produce materially different sequences of guaranteed blank pickup ticks that interact with label-locality constraints.

Merely showing a gap, having fewer bags, or saying that the gap changed arrival timing is insufficient.

### Redundancy warning
F7 overlaps F3/F4 because “which bag is absent later” is also a consumption/substitution decision. To preserve F7 as a separate counted family, accepted F7 representatives must contain a counterfactual where the **blank tick itself**, not just loss of the consumed trait class, changes the local-swap schedule. Otherwise retag the case F3/F4 and do not count it toward the F7 minimum.

### Campaign consequence
The provisional minimum `F7 >= 6` in `GAME10_CONTENT_MAP.md` is **not frozen yet**. Before Phase 5 closes, exact instances must prove that at least six non-duplicate blank-tick scheduling relationships exist. If they do not, Act D is to be reduced/rebalanced toward F3/F4/F6 synthesis without adding mechanics, exactly as the map's repair rule permits.

---

## 3. Current Phase-5 conclusion

The demo path now has an exact multi-passenger finale and the adjacency staging promise survives destructive validation. The remaining uncertainty is narrower and explicit: whether GAPs deserve a six-case primary family or should be demoted to a modifier of consumption/staging cases.

**NEXT VALIDATION TARGET:** generate/hand-construct at least three exact F7 candidates where a returning blank pickup tick is causally necessary to a winning local-label schedule, then compare normalized traces. If three materially distinct proofs cannot be produced without contrivance, demote F7 and rebalance the 42-slot map rather than rescuing it with new mechanics.

**PHASE 5 ACTIVE. DESIGN COMPLETE = NO.**