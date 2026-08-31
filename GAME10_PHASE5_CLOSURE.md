# GAME #010 — PHASE 5 CONTENT ARCHITECTURE CLOSURE

Date: 2026-08-31
Status: **PHASE 5 COMPLETE — F7 DEMOTED, 42-SLOT MAP REBALANCED**
Game: Luggage Carousel Zero *(working title)*

Authority: all prior active Game #010 authorities -> `GAME10_CONTENT_VALIDATION.md` -> this file.

This file is an authoritative amendment over conflicting F7/GAP-family claims in `GAME10_CONTENT.md`, `GAME10_CONTENT_MAP.md`, and earlier tournament prose. It does not change mechanics.

---

## 1. Bounded F7 proof attempt — verdict

`STATUS.md` required at least three exact candidates where a returning GAP reaches pickup while passengers remain and the **blank tick itself** is causally necessary to a winning adjacent-label schedule.

That requirement cannot be honestly satisfied under the frozen mechanics.

### 1.1 Equivalence proof
At any tick, player edits occur **before** ADVANCE. Pickup resolution occurs only after movement. If the incoming occupancy is a GAP, no passenger is served. Now replace that GAP counterfactually with a bag `X` whose immutable SHAPE/MARK cannot satisfy any remaining passenger under any reachable pickup label. On every future tick until X's traits become relevant (which by construction never occurs):

- the same adjacent label swaps are legal;
- the same label vectors are reachable;
- all occupancies rotate by the same one socket per tick;
- at the pickup tick, X is guaranteed not to serve exactly as GAP is guaranteed not to serve;
- tick consumption is identical;
- passenger index is identical;
- label displacement is identical;
- solver feasibility is identical except for state identity that no rule observes.

Therefore the **blankness itself adds no scheduling affordance**. A player can stage labels on any guaranteed non-service tick, whether the pickup occupancy is GAP or an inert/nonmatching bag.

### 1.2 What removal-created GAPs actually contribute
A pickup still has an important consequence: the consumed bag is absent on later circuits. But that consequence is already captured by:
- F3 Substitution — which candidate was consumed;
- F4 Scarcity preservation — whether a future-needed trait class was consumed;
- F5 Intentional miss — whether consumption was deliberately avoided;
- F6 Label staging — whether a non-service tick was used for local label work;
- F8 Duplicate-label flexibility — spatial alternatives in label values.

The returning empty occupancy is excellent **visual consequence and timing texture**, but it does not form a mechanically independent reasoning family under no-compression movement.

### 1.3 Rejected rescue routes
Phase 5 explicitly rejects rescuing F7 by adding any of these:
- compression after pickup;
- gap-dependent swap discounts;
- special "work on gap tick" actions;
- passenger impatience;
- multiple pickups;
- bag collisions;
- gap-specific predicates;
- gap merging/splitting;
- real-time timing.

Any such repair would add mechanics to preserve a taxonomy label, which is backwards.

**VERDICT: F7 is DEMOTED from primary reasoning family to a non-counted presentation/context modifier named `BLANK_RETURN`.**

---

## 2. Canonical GAP / BLANK_RETURN language

GAP remains canonical state and must remain visually legible because successful service permanently replaces a bag occupancy with GAP.

Allowed claims:
- the consumed bag is absent on later circuits;
- the empty occupancy itself returns to pickup at its fixed ring phase;
- that tick guarantees no service;
- the player may use any non-service tick, including a GAP return, to perform label staging before ADVANCE;
- multiple gaps create a visible service rhythm with guaranteed empty arrivals.

Forbidden claims:
- a gap shifts, accelerates, delays, compresses or reindexes surviving bags;
- a gap alone changes label reachability;
- a gap grants an action unavailable on an occupied nonmatching tick;
- `BLANK_RETURN` counts as an independent proof family.

`BLANK_RETURN` is useful as a pacing/readability/content-description tag, never as justification for accepting an otherwise duplicate case.

---

## 3. Rebalanced 42-slot map

The 42 IDs and act counts remain A7/B8/C8/D9/E10. A/B/C slots are unchanged except that incidental GAP language is descriptive only. Act D is retained as a **Consequence / Empty Rhythm** act because the persistent hole is visually and narratively worth teaching, but its nine slots must earn admission through existing causal families.

### Revised Act D obligations

| ID | N/K/T band | Counted families | Context modifier | Distinct obligation |
|---|---|---|---|---|
| D01 | N5/K1/T6 | F3,F6 | BLANK_RETURN | First explicit returning empty occupancy; case earns its slot through substitution + a required local stage, not blankness. |
| D02 | N5/K1/T6 | F4,F6 | BLANK_RETURN | Preserve scarce trait while a prior consumption later produces a visible empty arrival. |
| D03 | N6/K1/T7 | F5,F6 | BLANK_RETURN | Required intentional miss plus staging; creating the earlier hole changes the story, not the proof family. |
| D04 | N6/K1/T7 | F6 | BLANK_RETURN | A guaranteed non-service tick is used for a required stage; certification compares against pickup-only swap policy, not GAP-vs-dummy. |
| D05 | N6/K1/T7 | F6,F8 | BLANK_RETURN | Duplicate label positions + local stage around a visible empty return. |
| D06 | N7/K1/T8 | F3,F4 | BLANK_RETURN | Choice of which P1 candidate is consumed changes later trait availability; hole identifies the consumed phase visually. |
| D07 | N7/K1/T8 | F4,F6 | BLANK_RETURN | Scarce-bag preservation + displacement-sensitive staging across a second circuit. |
| D08 | N8/K1/T9 | F3,F6,F8 | BLANK_RETURN | Two visible gaps and duplicate labels, but acceptance requires substitution and spatial-label proofs. |
| D09 | N8/K1/T9 | F5,F6,F8 | BLANK_RETURN | Act exam: intentional miss + non-pickup stage + duplicate-label position; one prior hole returns during the trace. |

No Act D slot is admitted merely because a GAP returns.

### Revised Act E tags
- E04: `F5,F6,F8,F10 + BLANK_RETURN` (remove F7).
- E05: `F3,F6,F8,F10 + BLANK_RETURN` (replace F7 with positional duplicate/label interaction if exact data proves F8; otherwise keep F3,F6,F10 and require another independent family before admission).
- E06: `F4,F6,F8,F10 + BLANK_RETURN` (same proof rule).
- E09: `F6,F8,F9,F10 + BLANK_RETURN`.
- all other E slots unchanged.

When exact campaign instances are populated, any slot whose stated family counterfactual fails is rewritten/replaced; slot numbering is architecture, not entitlement to ship.

---

## 4. Frozen family coverage after demotion

Family counts are coverage floors over the **accepted 36–48 campaign pool**, not simple tag counts in the planning table. One case may satisfy multiple families.

- **F1 Alignment:** minimum 7; target 9–12.
- **F2 Trait binding:** minimum 6; target 8–12.
- **F3 Substitution:** minimum 8; target 12–16.
- **F4 Scarcity preservation:** minimum 8; target 12–16.
- **F5 Intentional miss:** minimum 6; target 8–12; each requires exact anti-greedy counterfactual.
- **F6 Label staging:** minimum 14; target 18–24; each counted representative must satisfy `STAGING_SIGNIFICANT` or a stricter local-displacement proof.
- **F7:** **RETIRED / non-canonical as a counted family.** Historical references mean `BLANK_RETURN` only.
- **F8 Duplicate-label flexibility:** minimum 5; target 7–10; positional significance required.
- **F9 K=2 bandwidth:** exactly 3 target mastery slots, minimum 2 surviving strong cases; maximum 3 in base campaign.
- **F10 Synthesis:** minimum 6; target 8–12; requires at least three independently proven counted families.

This distribution deliberately concentrates the game around the system that survived destructive proof: **local label permutation + bag-consumption choice + queue coupling**.

---

## 5. Demo-path correction

The seven-case demo remains valid as a teaching sequence, with two wording changes.

1. DEMO-01 — ownership.
2. DEMO-02 — label + bag trait.
3. DEMO-03 — away-from-pickup staging; exact `STAGING_SIGNIFICANT` proof retained.
4. DEMO-04 — preserve the only square; canonical tick budget is **5**, not 4.
5. DEMO-05 — required intentional miss.
6. DEMO-06 — **visual GAP semantics only**: show that service leaves a persistent hole and the belt does not compress. It is not marketed/certified as a new strategic family.
7. DEMO-07 — exact N5/K1/T7 finale from `GAME10_CONTENT_VALIDATION.md`; it proves scarce-bag intentional miss + queue coupling + required non-pickup staging. It does **not** claim a returning-gap consequence because gaps created on ticks 3/4 cannot return by tick 7 on N=5.

This correction removes a false demo promise without weakening the actual finale.

---

## 6. Content-population contract

Another session can now populate the campaign without inventing design:

1. choose a planned slot and its counted family obligations;
2. instantiate exact N/labels/bags/queue/budget within Phase-4 envelope;
3. solve exactly under adjacent-only swaps;
4. extract normalized traces;
5. run the specific family counterfactuals;
6. reject if family proof fails, regardless of solvability;
7. reject normalized duplicates after trait/value renaming;
8. reject >2 unjustified consecutive no-effective-swap Advances;
9. review 1280x800 readability before acceptance;
10. retain `BLANK_RETURN` only as a descriptive modifier;
11. retain at least 36 strong cases; target 42; never pad to hit a target count.

### Required counterfactuals
- F3: force each plausible early candidate choice; at least one changes later feasible service family.
- F4: consume the scarce class at earliest opportunity; completion must fail or materially worsen under the intended budget.
- F5: force immediate service whenever currently possible in the critical state; all such lines fail while a delayed line wins.
- F6: forbid non-S0-incident swaps; case becomes unsolvable or loses the certified intended solution family.
- F8: replace repeated-label spatial arrangement with a canonical collapsed/free-choice abstraction; solvability/minimum ticks/service family changes.
- F9: identical case at K=1 is unsolvable under the same tick limit or loses the intended certified family.
- F10: independently establish at least three counted proofs above.

---

## 7. Expansion boundary

Future base-game content may vary only existing data and budgets inside frozen envelopes. More cases, new cosmetic luggage/airport skins, and new values for existing LABEL/SHAPE/MARK dimensions are allowed if accessibility-safe.

Not allowed as silent content expansion: new predicates/operators, new trait dimensions, multiple pickups, direct bag movement, compression, special gap actions, cumulative swap currency, real-time pressure, passenger powers, conveyor construction, item physics, random hidden state or endless procedural campaign.

---

## 8. Phase-5 acceptance

- [x] 42-slot architecture exists.
- [x] adjacency correction propagated to content logic.
- [x] seven-case demo path exists with exact finale and repaired Demo 04 budget.
- [x] >=12 late-game relationship skeletons exist in prior map authority.
- [x] false GAP phase-shift language removed.
- [x] bounded F7 validation resolved by proof, not padding.
- [x] F7 retired and Act D rebalanced without adding mechanics.
- [x] family floors/targets frozen.
- [x] exact admission/counterfactual rules frozen.
- [x] expansion boundaries frozen.
- [x] another session can populate/certify campaign data without inventing content rules.

**PHASE 5 COMPLETE. DESIGN COMPLETE = NO.**

Next authority: `GAME10_UX.md`.