# GAME #011 — PHASE 2 CONCEPT TOURNAMENT — ROUND C / FINAL SELECTION

Date: 2026-09-01
Status: **ROUND C COMPLETE — 3 -> 1 WINNER**
Authority: `START_HERE.md` -> `STATUS.md` -> `GAME_INDEX.md` -> `GAME11_RESEARCH.md` -> `GAME11_TOURNAMENT_ROUND_A.md` -> `GAME11_TOURNAMENT_ROUND_B.md` -> this file.

Winner: **MISSING STEP** (working title; not commercial-title clearance).

Purpose: force each finalist through a 10–15 minute four-case mini-campaign using only its Round-B vocabulary, then compare mastery delta, recovery/preview burden, solver safety, trailer legibility, current market context and portfolio collision. No rescue mechanics were permitted.

---

## 1. Equal Round-C test
Each finalist had to prove four sequential cases:
1. case 1 teaches the causal verb;
2. case 2 breaks the first naive heuristic;
3. case 3 combines already-taught consequences without a new rule family;
4. case 4 is qualitatively deeper, not merely larger.

For every case we record learning delta, likely mistake and required recovery/preview. A finalist fails if case 4 needs a new material/rule family, hidden exception, substantially denser UI, or hand-authored behavior that cannot be certified by the bounded validator.

---

# 2. MISSING STEP — FOUR-CASE MINI-CAMPAIGN — PASS / WINNER

## Frozen Round-C operation semantics
These semantics replace ambiguous Round-B prose and are the authority going forward unless Phase 4 deliberately revises them.

- A case has 1–4 cyclic tracks, each 2–6 visible operation tokens.
- Operations remain exactly `PUSH`, `TURN`, `STAMP`, `CLAMP`.
- A workpiece has `lane in {0,1}`, `orientation in {N,E}`, integer successful-stamp count, and optional visible mark target.
- Before RUN, the player deletes exactly the case-authorized number of eligible tokens: normally one; mastery may authorize one deletion on each of two named tracks. Deleted tokens stay visibly crossed out in preview.
- Deletion permanently shortens that track for the run. Track phase starts at token 0 unless the case data explicitly supplies another visible initial phase.
- Ticks are deterministic. At tick start, the previous tick's clamp latch is known. Tracks execute in fixed A->D order, then all track indices advance modulo their post-deletion lengths.
- `PUSH`: toggle lane 0<->1. If destination is lane 1 while the previous-tick clamp latch is active, the push is blocked and increments `blocked_pushes`; the piece does not move.
- `TURN`: toggle N<->E.
- `STAMP`: if workpiece is in lane 1, increment `successful_stamps`; otherwise no effect.
- `CLAMP`: schedules lane 1 to be clamped on the **next** tick. Any CLAMP during the current tick sets the same next-tick latch; multiple clamps do not stack.
- Targets may inspect only final lane, final orientation, successful-stamp count/range, blocked-push count, and a finite tick horizon. No hidden machine state or random timing.
- Preview may show the deterministic next-cycle alignment and resulting token schedule, but does not automatically solve which token to delete.

This preserves the identity: deleting a step changes a loop's period, which changes future cross-track phase relationships.

## M-C1 — “One Missing Beat” — ~2 minutes
Tracks: A `[PUSH, TURN, STAMP]`; B `[PUSH, CLAMP]`. Short horizon. One deletion on A. Target is chosen so deleting TURN is the certified success while deleting the visually harmful-looking STAMP cannot satisfy mark count.

**Learning delta:** deletion is not cancellation-only; shortening the loop changes when later operations recur.
**Likely mistake:** delete the operation whose immediate effect looks bad.
**Recovery/preview:** instant Reset; timeline shows the post-delete loop length and first six scheduled columns.

## M-C2 — “Bad Step, Useful Timing” — ~3 minutes
A four-token A loop and three-token B loop create a clamp cadence. The direct bad-looking PUSH is a decoy: removing it changes period in the wrong way; removing a TURN produces the needed stamp cadence and safe lane transitions.

**Learning delta:** judge the entire repeated schedule, not the deleted token in isolation.
**Likely mistake:** optimize tick 1–2 rather than the horizon.
**Recovery/preview:** scrub preview by tick; blocked future PUSH is visibly marked, but the UI does not recommend a deletion.

## M-C3 — “Beat Frequency” — ~3 minutes
Two loops have different lengths. One deletion is permitted on A only. Target requires an exact stamp count and final lane. Candidate deletions create different least-common-multiple recurrence patterns despite sharing the same operation vocabulary.

**Learning delta:** repeated alignments, not just first-cycle behavior, determine success.
**Likely mistake:** stop inspecting after the first apparently correct stamp.
**Recovery/preview:** cycle-boundary markers and repeated-alignment ghost columns; no arithmetic notation required.

## M-C4 — “Two Missing Steps” — ~4–5 minutes — exact mastery proof
Initial:
- A = `[PUSH, PUSH, TURN, STAMP]`
- B = `[PUSH, CLAMP, PUSH, TURN]`
- initial lane 0, orientation N, stamps 0, no latch
- horizon = 12 ticks
- delete exactly one token from A and exactly one token from B
- target = final lane 0, final orientation N, exactly 4 successful stamps, **0 blocked PUSHes**.

Exhaustive enumeration of all 4 x 4 = 16 deletion pairs under the frozen semantics finds a **unique** success:
- delete A token 3 = `TURN`;
- delete B token 4 = `TURN`.

Post-edit loops:
- A = `[PUSH, PUSH, STAMP]`
- B = `[PUSH, CLAMP, PUSH]`.

Certified successful trace summary:
- t1 PUSH/PUSH -> lane0, stamps0;
- t2 PUSH/CLAMP -> lane1, next clamp armed;
- t3 STAMP/PUSH -> stamp1, lane0;
- the 3-tick cadence repeats;
- t6 stamp2, t9 stamp3, t12 stamp4;
- final lane0/N, blocked pushes0.

The qualitative step is **coupled editing**: the player now chooses a pair of deletions whose two shortened loops co-determine a repeated safe cadence. No new operation, resource, sensor or exception is introduced. The exact validator can certify uniqueness cheaply by enumerating edit pairs and simulating 12 ticks.

**Learning delta:** reason about two edited periods together.
**Likely mistake:** find one locally promising deletion and treat the other track independently.
**Recovery/preview:** two-row timeline with shared tick columns; Reset is instant; preview highlights clamp-next-tick semantics and resulting scheduled operations.

### Mini-campaign verdict
PASS. Case 4 is deeper through interaction of already-known periodic systems, not through added vocabulary. Exact validation is tiny and deterministic. The main risk remains presentation: it must look like a physical machine losing a step, not a spreadsheet of modular arithmetic.

---

# 3. FOSSIL FORECAST — FOUR-CASE MINI-CAMPAIGN — RUNNER-UP / CUT

## Erosion semantics locked for tournament test
- Orthogonal cell map <=10x8.
- `VOID` is exterior-connected empty space; `BEDROCK` never erodes.
- Named sediment layers begin soft and can be LITHIFY'd; hardened named-layer cells never erode.
- After each LITHIFY, erosion resolves in **waves**. At wave start, every still-soft erodible cell orthogonally adjacent to exterior-connected VOID is marked; all marked cells are removed simultaneously; connectivity is recomputed; repeat until no marked cells remain.
- Fossil cells themselves do not erode. A fossil is LOST only if its case-declared support cell is removed; it is REVEALED when orthogonally adjacent to exterior-connected VOID.
- No gravity, collapse, fluid pressure, diagonal seepage or hardness exceptions.

## F-C1 — “Expose, Don’t Excavate” — ~2 min
One fossil, two layers, one lithify. Player learns simultaneous erosion waves and that a hardened shield can preserve support while side erosion reveals the fossil.
**Mistake:** harden the cell/layer directly above the fossil without considering exposure path.
**Preview:** one-wave preview plus full deterministic time-lapse after commit.

## F-C2 — “Two Fossils, One Mouth” — ~3 min
Two fossils; preserve Q while reveal P and open an exterior-connected extraction mouth. Same layers/materials; budget2.
**Delta:** preservation and access can conflict.
**Mistake:** protect both roofs, accidentally sealing the extraction corridor.
**Recovery:** Undo-before-next-lithify is acceptable because each action is irreversible in simulation but puzzle experimentation should be cheap.

## F-C3 — “Order Is Geology” — ~3 min
Three named layers, budget2. Lithifying X then Y differs from Y then X because erosion resolves fully after each action. A first action can permanently remove the future shielding geometry.
**Delta:** final hardened set is insufficient; order matters.
**Mistake:** assume actions commute.
**Preview:** before commit show only next erosion wave and threatened supports, not the entire optimal sequence.

## F-C4 — “Cross-Section Trade” — ~5 min
Three fossils and three layers; target reveal two, preserve all three supports, open one corridor. The intended depth is choosing an ordered subset under irreversible wave erosion.
**Qualitative depth:** order + multi-target geometry can be deeper without new materials.
**But:** compared with Missing Step, authoring/readability burden is materially higher. A mastery case must communicate exterior connectivity, simultaneous wave marking, support ownership and reveal-vs-lost state on a compact cell map. Exact cell-map certification is easy computationally (<=336 ordered sequences for 8P3), but *human* explanation is less cheap.

### Tournament finding
The explicit wave rule solves the feared physics-exception problem: Fossil Forecast does **not** need collapse physics. It therefore survives on design quality, but loses the final selection because its 10–15 minute teaching burden is higher and its strongest trailer moment (“terrain erodes after lithify”) is less immediately diagnostic of player agency than physically crossing out one machine step and watching loops re-phase.

CUT as runner-up, not as broken concept. Do not silently reuse as Game #011 canon.

---

# 4. QUEUE SCULPTOR — FOUR-CASE MINI-CAMPAIGN — CUT

Frozen rule families remain `AVOID_COLOR`, `SEEK_TAG`, `SIDE(divider)`, `PAIR`; one divider; deterministic front-to-back nearest-later relocation; repeat-state invalid.

## Q-C1 — “Make a Side” — ~2 min
3–4 agents; one SIDE rule and one AVOID rule. Divider makes a stable line.
**Delta:** divider is both boundary and predecessor break.
**Mistake:** place it only to satisfy SIDE.
**Preview:** animated relocation reasons.

## Q-C2 — “The Person Behind” — ~3 min
Mix AVOID + SEEK. Correct divider causes one agent move that changes another agent's predecessor.
**Delta:** local satisfaction cascades.
**Mistake:** evaluate only initial neighbors.
**Recovery:** step-through resolver / reset.

## Q-C3 — “Stable, But Wrong” — ~3 min
Add PAIR from the already-frozen vocabulary. Several placements stabilize, but only one satisfies target relative order.
**Delta:** stability is not equivalent to objective success.
**Mistake:** stop at first no-move line.

## Q-C4 — “Chain Reaction” — ~5 min
6–8 agents, <=4 rule families, one divider. Solver certifies a non-oscillating cascade where an early AVOID relocation enables SEEK, then PAIR, while SIDE constrains the destination segment.
**Qualitative depth:** possible without a fifth rule family.
**However:** mastery readability becomes a list of tiny per-person predicates. The player increasingly predicts a deterministic rules engine rather than manipulating a visually self-explanatory object. The one-divider action space is only N+1 choices, so without obscuring consequences or adding more dividers, late puzzles risk trial-enumeration. Adding more dividers would change the frozen action economy and push the concept toward bookkeeping.

### Tournament finding
CUT. It passes deterministic implementation but fails the strongest hour-8/mastery test among the finalists: bounded one-divider choice count plus four heterogeneous agent rules creates either shallow enumeration or dense rule reading. This confirms Round B's conditional warning; no bespoke exception is added to rescue it.

---

# 5. Fresh market / analogue comparison — 2026-09-01

Fresh research was used only as market context, not as proof of sales.

- `Modulus: Factory Automation` released 2026-04-02 and currently presents a broad creative factory/automation fantasy with cut/paint/stamp/assemble operators, spatial routing and open-ended solutions. It has a materially larger sandbox scope than Missing Step. This means Game #011 must **not** market itself as “another factory automation game”; its trailer and store copy must foreground *delete one repeating step -> change the loop period -> re-phase the machine*. Source: https://store.steampowered.com/app/2779120/Modulus_Factory_Automation/
- `ZAVOD: Conveyor Logic` released 2026-07-24 at $4.99 with 50 minimalist conveyor puzzles and simple controls. This is evidence that small factory-themed puzzle presentation is current and therefore not differentiating by itself. Missing Step needs the crossed-out-step/re-phasing visual in its first seconds. Source: https://store.steampowered.com/app/1437200/ZAVOD_Conveyor_Logic/
- `Robbie the Robot: Space Puzzles` released 2026-04-04 and uses pre-run command planning, disappearing commands, many later tile/mechanic types and a built-in help system. It reinforces both adjacency and separation: pre-run programming puzzles exist, but Missing Step's identity is *removing an existing periodic operation to change recurrence*, while its scope rule explicitly refuses a growing mechanic zoo. Source: https://store.steampowered.com/app/1159740/Robbie_the_Robot_Space_Puzzles/
- `Spring Falls` remains a durable erosion-themed pure puzzler with 60 handcrafted levels and landscape/water presentation. Fossil Forecast is mechanically different, but environmental erosion is not itself a novel marketing word. Source: https://thinkygames.com/games/spring-falls/
- Exact queue searches still mostly surface unrelated queue simulators rather than a strong direct commercial analogue; lack of a direct analogue does not cure Queue Sculptor's internal mastery/readability weakness.

### Trailer legibility
1. **Missing Step:** strongest. Show machine loop, cross out TURN, visible loop contracts, operation columns drift into new alignment, workpiece succeeds. One causal edit reads in seconds if animated well.
2. **Fossil Forecast:** strong visual transformation, but viewer may read erosion as passive spectacle until LITHIFY causality is explained.
3. **Queue Sculptor:** divider -> people move is readable, but why each person moved requires icons/tooltips and risks looking arbitrary in a silent GIF.

### Demo conversion hypothesis
Missing Step offers the cleanest 10–15 minute demo escalation: one-loop deletion -> deceptive deletion -> recurrence -> two-loop coupled deletion. The demo can expose the full product identity without revealing a large mechanic catalog.

### Title/theme expectation
`Missing Step` is a useful internal name but generic/noisy and not commercially cleared. Phase 3 keeps it as working title only. Presentation should avoid promising full factory building; this is a compact machine-sequencing puzzle, not an automation sandbox.

---

# 6. Portfolio collision #001–#010 — final Phase-2 check

**PASS.** Missing Step's irreducible decision is destructive editing of a *periodic instruction sequence*, changing loop length and future phase relationships. It does not transfer properties (#003), conserve/redistribute a scalar network (#005), rewrite adjacency (#006), persistently edit a key vector (#008), fold/trim a sheet (#009), or permute labels around moving luggage (#010). Machine imagery alone does not create a structural collision with earlier games.

---

# 7. Final scoring

| Criterion | Missing Step | Fossil Forecast | Queue Sculptor |
|---|---:|---:|---:|
| 20s causal legibility | 9.2 | 8.3 | 8.2 |
| Same-vocabulary mastery | 9.3 | 8.7 | 7.1 |
| Exact validator safety | 9.7 | 9.0 | 8.8 |
| Human explainability | 9.2 | 7.9 | 7.3 |
| Content efficiency | 9.4 | 8.7 | 7.5 |
| Production scope | 9.4 | 8.3 | 9.0 |
| Demo escalation | 9.5 | 8.5 | 7.8 |
| Market differentiation of verb | 8.8 | 8.8 | 8.1 |
| Portfolio separation | 9.4 | 9.6 | 8.3 |
| **Decision** | **WIN** | CUT / runner-up | CUT |

Scores are comparative design evidence, not revenue forecasts.

# PHASE-2 DECISION
**SELECT MISSING STEP as Game #011.**

The winner is selected because the same tiny vocabulary produces a certified qualitative mastery jump, the validator is exhaustive and cheap, failure is explainable, controller/800p presentation is naturally compact, and the causal hook can be shown without pretending the game is a full automation sandbox.

The two losing concepts remain tournament history only. They are not active Game #011 canon and must not be silently imported later.
