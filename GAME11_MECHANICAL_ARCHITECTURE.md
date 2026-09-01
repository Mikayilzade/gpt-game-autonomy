# GAME #011 — MISSING STEP — PHASE 4 MECHANICAL ARCHITECTURE

Date: 2026-09-01
Status: **PHASE 4 MECHANICAL ARCHITECTURE COMPLETE**
Authority: `START_HERE.md` -> `STATUS.md` -> `GAME_INDEX.md` -> Phase-2 history -> `GAME11_PRODUCT_THESIS.md` -> this file for exact mechanics.

## 1. Canonical simulation state
A case contains exactly one workpiece and 1–4 cyclic tracks A–D.

Workpiece state:
- `lane ∈ {0,1}`;
- `orientation ∈ {N,E}`;
- `successful_stamps >= 0` integer;
- `blocked_pushes >= 0` integer.

Global state:
- `tick` beginning at 1 when RUN starts;
- finite `horizon_ticks`;
- `clamp_active_this_tick` boolean;
- `clamp_scheduled_next_tick` boolean;
- for each track: ordered surviving token IDs and one current token cursor.

There is no hidden state, randomness, physics truth, velocity, resource economy, damage, score multiplier, timing window or second workpiece.

### Single-workpiece decision
**FROZEN: exactly one workpiece for the full launch campaign.**
The one piece already exposes lane timing, orientation parity, successful/no-op STAMP timing, blocked PUSH timing, same-tick order, different periods, initial phase and coupled two-delete mastery. A second piece would multiply readability/state without creating a new kind of subtractive-period reasoning. Phase 4 therefore rejects it.

## 2. Token and phase identity
Every authored token has a stable unique `token_id` even when two tokens have the same opcode.

A track stores a visible `start_token_id`, shown by the phase pointer before editing. Deletion does not renumber token identity. After edits:
1. if `start_token_id` survives, it executes first;
2. if it was deleted, the first surviving token clockwise after it in the original cycle executes first;
3. thereafter the cursor advances clockwise among surviving tokens modulo post-delete length.

This prevents ambiguous “did deleting a token before phase zero rotate the loop?” behavior. Deletion changes period and removes an event; it never secretly rotates the authored start anchor.

Minimum original track length is 2. A legal deletion may not reduce a track below length 2. Standard campaign content should normally start at length 3–6 on editable tracks.

## 3. Exact RUN tick ordering
At RUN start:
- workpiece uses authored initial lane/orientation;
- counts are zero unless a teaching case explicitly authors otherwise (launch campaign default: zero only);
- `clamp_active_this_tick = false` unless the case explicitly shows an initial active latch;
- `clamp_scheduled_next_tick = false`;
- each track resolves its post-edit cursor from its visible start anchor.

For each global tick `t = 1..horizon_ticks`:
1. promote the prior scheduled latch: `clamp_active_this_tick = clamp_scheduled_next_tick`;
2. clear `clamp_scheduled_next_tick = false`;
3. execute exactly one current token from each track, in fixed visible order **A -> B -> C -> D**;
4. opcode effects are immediate except CLAMP, which only schedules next tick;
5. after all tracks execute, advance every track cursor by one surviving token;
6. record the complete trace row;
7. if a monotone hard-fail bound has already been exceeded, RUN may stop early; otherwise continue to the exact horizon;
8. after the final tick evaluate all target predicates simultaneously.

Tracks are therefore not simultaneous in the mathematical sense. The fixed A->D order is intentional, public and visually encoded. It matters when PUSH/STAMP/TURN on different tracks touch the same workpiece during one tick. CLAMP is exempt from same-tick ambiguity because it only affects the next tick.

## 4. Four opcodes — frozen semantics
### PUSH
- Compute destination `1 - lane`.
- If destination is lane 1 and `clamp_active_this_tick == true`, PUSH is blocked: lane does not change and `blocked_pushes += 1`.
- Otherwise lane toggles.
- A PUSH from lane 1 to lane 0 is never blocked by the lane-1 clamp.

### TURN
Toggle orientation `N <-> E` immediately.

### STAMP
- If lane == 1 at the instant this track executes, `successful_stamps += 1`.
- Otherwise STAMP is a visible no-op.
- There is no binary “marked” state separate from the count; UI may visually show accumulated marks, but mechanical truth is the integer count.

### CLAMP
Set `clamp_scheduled_next_tick = true`.
- It never blocks on its own current tick.
- Multiple CLAMP operations in one tick coalesce to the same boolean next-tick latch.
- The latch lasts for exactly one tick unless one or more CLAMPs during that tick schedule the following tick again.
- Non-CLAMP operations do not “clear” a currently active latch early.

## 5. Planning/edit contract
All edits happen before RUN. RUN itself has no player input.

### Standard deletion budget
A standard case authorizes **exactly one deletion total** from a public eligible set. The eligible set may span 1–4 tracks, but strong campaign cases should usually expose <=12 legal positions and never more than 24.

### Mastery deletion budget
A mastery case may authorize **exactly one deletion on each of two named editable tracks**. Each named track has its own public eligible set. Maximum search space under launch ceilings is 6×6 = 36 edit pairs.

No launch case permits:
- two deletions from the same track;
- “up to” N deletions where skipping one is strategically valid;
- insertion;
- moving/reordering tokens;
- changing opcode parameters;
- disabling an entire track;
- editing during RUN.

### Eligibility
Eligibility is explicit case data and visible before selection. Default authored rule is “every token whose removal leaves >=2 survivors is eligible.” Tutorials may lock tokens to focus a lesson, but locked tokens must be visibly mechanically fixed rather than mysteriously unclickable. Mastery content should avoid tiny artificial eligible sets; target >=3 eligible positions per editable mastery track.

### Duplicate opcodes
Two visually identical opcode tokens at different positions remain different legal edits because `token_id` and cyclic position differ. Solver solutions are edit sets of token IDs, not opcode names. If deleting duplicate tokens produces the same complete trace and target outcome, those edits are **behaviorally equivalent solutions** and count against uniqueness unless the case intentionally allows a multi-solution band.

## 6. Target predicate grammar
A case target is a conjunction of a subset of these public predicates, evaluated at the horizon unless stated monotone:
- `FINAL_LANE == 0|1`;
- `FINAL_ORIENTATION == N|E`;
- `STAMP_COUNT == n`;
- `STAMP_COUNT in [min,max]`;
- `BLOCKED_PUSH_COUNT == n`;
- `BLOCKED_PUSH_COUNT in [min,max]`.

Launch authoring limits:
- count bounds are non-negative integers and small enough to read directly;
- no OR, NOT, hidden predicate, intermediate-tick positional target, arbitrary history query, token-specific trigger, score formula or secret bonus condition;
- horizon is public case data, not a target predicate;
- typical target uses 2–4 clauses.

`STAMP_COUNT` and `BLOCKED_PUSH_COUNT` are monotone. If a candidate exceeds an authored maximum/equality value during RUN, success has become impossible and the run may visibly stop with the exact exceeded clause. Lane/orientation cannot be declared impossible early merely from current state. The validator may know more, but the player UI does not expose solver-derived dead-state predictions.

## 7. Win, fail and early-impossibility semantics
A RUN wins iff every target clause is true after the exact final tick.

Failure categories are explanatory, not separate game rules:
- wrong final lane;
- wrong final orientation;
- too few/many stamps;
- too few/many blocked PUSHes;
- monotone bound exceeded early.

There is no life loss, resource loss, grade penalty or permanent consequence for failure. Reset returns immediately to planning with the previous deletion selection retained so the player can compare/revise.

The UI must identify the first monotone hard failure if one happened and otherwise show final target deltas. It must not say “wrong deletion” or reveal an unchosen solution.

## 8. Preview boundary — information without oracle behavior
Preview exists to remove clerical modular-arithmetic transcription, not to solve the target.

After the player chooses a candidate edit set, Preview may show:
- shortened loops with crossed-out token IDs;
- resolved first token after the phase anchor;
- exact opcode alignment across all tracks for every tick up to the public horizon;
- cycle-boundary/period markers;
- which ticks begin with the CLAMP latch active, because that follows directly from the visible opcode schedule;
- hover/scrub explanation of opcode semantics.

Preview must **not** show before RUN:
- simulated future lane/orientation;
- predicted stamp count;
- predicted blocked PUSH outcomes;
- target pass/fail lights;
- “dead” status;
- solution count;
- recommendation/ranking/highlight of better deletions;
- alternate edits not selected by the player.

Thus Preview makes re-phasing visible but leaves the player to reason through physical consequences. RUN remains the experiment that resolves the workpiece trace.

## 9. Solver / certificate authority
Every shipping case is exhaustively certified from authored legal edit sets. No prose-intuited case ships without certification.

### Canonical certificate inputs
- `case_rules_version`;
- exact case data hash;
- ordered tracks with token IDs/opcodes/start anchors;
- eligible token IDs and deletion budget contract;
- initial workpiece/latch state;
- horizon;
- target clauses.

### Enumeration
Standard: enumerate each legal single token ID.
Mastery: Cartesian product of eligible IDs on the two named tracks.
For each candidate: apply edit, simulate exactly, evaluate target.

### Per-candidate certificate data
- sorted/ordered edit token IDs;
- post-edit track signatures;
- final target values;
- `success` boolean;
- canonical full trace hash;
- human-readable compact trace signature: per-tick executed opcodes + lane/orientation/stamp/blocked/latch outcomes;
- first monotone hard-fail tick/reason if any.

### Case certificate data
- legal edit-set count;
- raw successful edit-set count;
- number of **behaviorally distinct successful traces**;
- solution edit sets;
- equivalence groups where different edit IDs produce identical traces;
- intended heuristic trap labels;
- difficulty feature vector.

### Uniqueness bands
- `UNIQUE`: exactly one successful edit set and one successful trace. Preferred for teaching/core campaign.
- `EQUIVALENT_MULTI`: >1 edit sets but one identical successful trace. Reject from normal campaign; duplicates make the authored choice misleading.
- `TRACE_MULTI`: >1 behaviorally different successful traces. Allowed only in explicitly labeled open-solution late content; default campaign rejects it.
- `UNSAT`: zero successes; reject.

The normal campaign target is UNIQUE. A case generator/authoring tool may create candidates, but only certified case data is authority.

## 10. Difficulty feature vector
Difficulty is tuned with these knobs only:
1. number of tracks 1–4;
2. original lengths 3–6 on editable tracks;
3. post-delete period relationships / LCM within horizon;
4. visible non-zero start anchors;
5. legal edit count;
6. one editable track vs several eligible tracks;
7. single-delete vs named two-track mastery;
8. horizon length (campaign target 4–18; hard ceiling 24 unless Phase 5 proves a specific exception unnecessary);
9. target conjunction size;
10. exact vs range count target;
11. number/placement of CLAMPs;
12. number of duplicate opcode occurrences;
13. same-tick interactions caused by fixed A->D order;
14. deceptive early success that diverges later in the horizon.

Difficulty must not be increased by shrinking icons, hiding phase, adding operations, increasing workpieces, adding arbitrary token parameters or extending horizons until manual arithmetic becomes the challenge.

## 11. Six trace-distinct challenge families — Phase-4 proof
The campaign has at least six mechanically different families without expanding the four opcodes. These are families of reasoning, not new rule types.

### F1 — Period contraction / recurrence
A deletion changes a 4-step track to period 3; a desired STAMP recurrence moves from every fourth to every third global tick. Target count distinguishes edits. Core question: “what cadence did I create?”

### F2 — Clamp-window avoidance
A shortened PUSH cadence lands inside or outside next-tick CLAMP windows. Target commonly requires `BLOCKED_PUSH_COUNT == 0` plus a final state. Core question: “does my new period repeatedly enter the dangerous window?”

### F3 — Orientation parity against horizon
Deleting a TURN or changing the recurrence of remaining TURNs changes how many toggles occur by the exact horizon. The correct edit may preserve a seemingly harmful TURN because its new cadence fixes final orientation. Core question: “how does contraction change parity over repeated cycles?”

### F4 — Positional duplicate-token deletion
Witness validated under canonical simulator:
- A `[PUSH, TURN, PUSH, STAMP]`, B `[STAMP, CLAMP, TURN]`, horizon 8, edit A only.
- delete A token1 PUSH -> final `(lane1,E,stamps2,blocked0)`;
- delete A token3 PUSH -> final `(lane1,E,stamps3,blocked0)`.
The opcode removed is identical but the cyclic sequence that closes the gap is different. Target `lane1/E/stamps2/blocked0` distinguishes the first position. Core question: “which occurrence is missing?”

### F5 — Same-tick track-order choreography
Because A->D effects are immediate, a STAMP before a same-tick PUSH can differ from a STAMP after it. Deletion changes which operations coincide, while the public order remains fixed. A minimal checked witness shows reversing track order would change stamp outcome, proving this is not reducible to independent per-track arithmetic. Core question: “when rows align, which physical event happens first?”

### F6 — Coupled two-delete beat frequency
Round-C mastery remains canonical witness:
- A `[PUSH,PUSH,TURN,STAMP]`;
- B `[PUSH,CLAMP,PUSH,TURN]`;
- horizon12, initial lane0/N;
- delete exactly one from each;
- target lane0/N, stamps4, blocked0.
Exhaustive 4×4 enumeration yields exactly one success: delete TURN from A and TURN from B, producing periods 3 and 3 and four safe stamps. Core question: “which pair of contractions creates a joint rhythm?”

These families are trace-distinct: cadence count, hazard-window interaction, parity, positional duplicate identity, intra-tick causal order and coupled edit interaction require different explanations while using the same state vocabulary.

## 12. Adversarial edge-case rulings
### Degenerate loops
- Post-delete length <2: illegal at authoring/certification time.
- A legal loop may contain only one opcode family (e.g. PUSH/PUSH), but Phase 5 should reject cases whose solution is obvious by opcode count and lacks re-phasing value.

### Multiple CLAMPs
Coalesce into one next-tick boolean. Consecutive ticks may stay clamped only if each prior tick executes at least one CLAMP. No stack count exists.

### Multiple PUSHes in one tick
Resolve A->D sequentially. A successful PUSH can change lane before a later PUSH. Each blocked attempt increments blocked count independently.

### STAMP no-op
A lane0 STAMP is legal, visible and count-neutral. It does not create a “failed stamp” counter.

### Horizon edge
Actions on the final tick execute fully in A->D order before target evaluation. A CLAMP scheduled on the final tick has no effect beyond horizon and is not itself a failure.

### Initial latch
Allowed by schema only if visibly authored. Campaign default is false; use sparingly because an initial active latch adds explanation without showcasing deletion-induced cadence.

### Deleting the authored start token
Legal if eligible. Cursor begins at the next surviving clockwise token according to the stable anchor rule.

### Identical-token misleading solutions
Different token IDs with identical opcode are separate edits. If they generate identical full traces and both succeed, certificate marks EQUIVALENT_MULTI and normal campaign rejects the case.

### Track-order dependence
Always A->D; never authored per case. UI labels and vertical ordering must match execution authority so there is no hidden priority.

### Solver-known impossibility
Never surfaced in planning/preview. Solver is certification authority, not a player oracle.

## 13. Mechanical acceptance gates
- Exact state variables: PASS.
- Initial phase/deleted-anchor semantics: PASS.
- Tick ordering and same-tick effects: PASS.
- CLAMP lifetime: PASS.
- Deletion budgets/eligibility: PASS.
- Two-delete search-space bound: PASS (<=36 under mastery ceiling).
- Target grammar: PASS.
- Win/fail/early-impossibility semantics: PASS.
- Preview non-oracle boundary: PASS.
- Solver/certificate schema: PASS.
- Duplicate-solution semantics: PASS.
- >=5 trace-distinct challenge families: PASS (6 frozen families).
- Degenerate/adversarial rules: PASS.
- Single workpiece campaign sufficiency: PASS; second piece rejected.
- New operation/mechanic required: NO.

**PHASE 4 COMPLETE.**

## Phase 5 handoff
Build content architecture without changing this mechanical authority. Required next work:
1. define canonical case data schema and authored/certified artifact split;
2. map 5–7 campaign acts to the six challenge families and learning deltas;
3. set minimum/target case counts and demo subset;
4. define generator/search pipeline, rejection thresholds and human curation rules;
5. establish difficulty bands from measurable certificate features rather than prose labels alone;
6. build at least 10 representative certified case skeletons, including tutorials, deceptive cases, positional duplicate, same-tick ordering and two-delete mastery;
7. prove campaign variety without a fifth opcode, second workpiece or hidden target grammar.
