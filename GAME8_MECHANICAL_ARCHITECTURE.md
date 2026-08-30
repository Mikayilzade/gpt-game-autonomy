# GAME #008 — MECHANICAL ARCHITECTURE

Last updated: 2026-08-30
Phase: **4 — Mechanical Architecture**
Selected concept: **G8C02 Locksmith's Margin**
Working title: **Locksmith's Margin**
Production implementation started: **NO**

This file is the complete Phase-4 mechanical authority for Game #008. It refines `GAME8_PRODUCT_THESIS.md` without changing the locked product identity. The lock/key system is intentionally fictionalized, discrete and puzzle-first. It is **not** a simulation or instruction set for real-world lock bypass.

---

# 1. Mechanical design goals

The system must make these thoughts recur at increasing depth:
1. `What exactly blocked this key?`
2. `Do I need to cut now, or should I preserve this state?`
3. `Which other lock can this partially compatible key still cover?`
4. `Is this blank more valuable as information than as an immediate opener?`
5. `How should several persistent keys partition several overlapping lock acceptance sets?`

The mechanical architecture therefore prioritizes:
- deterministic causality;
- irreversible committed edits;
- exact but initially incomplete information;
- overlap preservation;
- persistent artifacts reused across targets;
- small complete state;
- bounded authored complexity;
- no hidden exception trivia;
- no dexterity authority;
- no random failure;
- no real-world locksmith procedure.

---

# 2. Canonical notation

A **case** contains:
- `C`: column count;
- `D`: deepest legal depth index;
- a finite blank set `B`;
- a finite required lock set `L`;
- optional test-access gates;
- optional per-lock master branches and wear widening encoded only through accepted sets;
- optional case-level cut cap only for explicit challenge variants, never core campaign gating.

## 2.1 Columns
Columns are indexed left-to-right `c = 1..C` in the game's fictional mechanism.

Normal campaign ceiling:
- minimum `C = 4`;
- normal maximum `C = 6`;
- no main-campaign case may exceed 6 reasoning-critical columns.

## 2.2 Depths
Each column has integer depth:

`k[c] ∈ {0,1,...,D}`

where:
- `0` = untouched/shallowest state;
- larger values = one or more committed filing steps;
- filing can only increase depth by exactly `+1` per committed action.

Normal campaign:
- `D ∈ {3,4,5}`;
- therefore 4–6 discrete depth states including zero;
- no fractional authoritative depths.

## 2.3 Key state
For blank `b`, the authoritative key vector is:

`K_b = [k_b[1], ..., k_b[C]]`

Every blank begins from an authored start vector, normally all zero but not required. A pre-cut blank is legal only if the case explicitly shows its current physical profile at start.

The key vector is the only authority for fit. Mesh shape, animation, shader wear, scratches and audio never affect fit.

## 2.4 Lock state
For each lock `l` and column `c`, define a non-empty finite accepted depth set:

`A[l,c] ⊆ {0,...,D}`

A key opens a lock iff:

`∀c, K_b[c] ∈ A[l,c]`

Accepted sets are the single canonical representation. Terms such as `exact`, `master`, and `worn` describe authored shapes of these sets; they never add alternate fit logic.

---

# 3. Legal filing transition

## 3.1 FILE action
`FILE(b,c)` is legal iff:
- blank `b` is available on the bench;
- `K_b[c] < D`;
- no case state currently disables filing that blank through an explicit visible case rule.

Commit transition:

`K_b[c] := K_b[c] + 1`

Exactly one authoritative depth step changes.

## 3.2 Preview and commit
Selecting a file target may display a **candidate ghost notch** for the next depth, but does not change authority.

A committed filing action occurs only after the explicit commit input. Animation duration does not define the state change. If animation is skipped, interrupted or sped up, the resulting vector is identical.

## 3.3 Irreversibility
Inside forward puzzle state, filing is irreversible:
- no `add metal` verb;
- no shallowing;
- no replacement insert;
- no repair item;
- no random recovery.

Recovery is provided by the bounded Undo/Restart system defined later, not by fictional exceptions.

## 3.4 Maximum-depth behavior
Attempting to file a column already at `D`:
- performs no transition;
- gives immediate neutral feedback `MAX DEPTH` through icon/shape/audio accessibility-equivalent feedback;
- consumes no move, information or resource;
- cannot be used as an exploit to advance scripted state.

---

# 4. Lock acceptance semantics

Accepted sets are authored directly and evaluated directly.

## 4.1 Exact column
An exact column accepts one depth:

`A[l,c] = {x}`

## 4.2 Tolerance interval
A tolerance interval accepts contiguous depths:

`A[l,c] = {a, a+1, ..., b}` where `a ≤ b`

This is the normal representation of an imperfect/worn fictional lock.

## 4.3 Master branch
A master branch is a union of at most two contiguous intervals:

`A[l,c] = I1 ∪ I2`

with `I1` and `I2` disjoint.

Normal content constraint:
- at most two disjoint intervals in one column;
- at most two master-branch columns per normal case;
- no third branch.

The player experiences this as one column having two visibly valid alignment bands after sufficient inspection/feedback. It is not a real-world master-pin simulation.

## 4.4 Wear widening
Wear never changes rules dynamically during a case. A `worn` lock simply begins with a wider contiguous accepted set than a precise lock.

Forbidden:
- widening after repeated tests;
- stochastic wear;
- deterioration during play;
- hidden condition percentages.

Thus testing cannot alter a lock's acceptance set.

## 4.5 Empty acceptance
No required lock may contain `A[l,c] = ∅`. Validator rejects such content.

---

# 5. Fit evaluation order

Testing is deterministic and ordered.

For `TEST(b,l)`:
1. verify test access is currently legal;
2. evaluate columns in fixed visible order `1 → C`;
3. if every column is accepted, result is `OPEN`;
4. otherwise let `j` be the smallest column index where `K_b[j] ∉ A[l,j]`;
5. result is `BLOCKED_AT(j, feedback_class)`;
6. only information permitted by that failed test is revealed/updated;
7. neither key nor lock mechanical state changes because of the test, except opened-state/access consequences on success.

The physical animation must visually bind at the same `j` returned by authority.

No later incompatible column is revealed during that same failed test.

---

# 6. Deterministic impression / failed-test information

The player must learn something exact enough to reason, but a failed test must not dump the whole hidden vector.

## 6.1 Directional relation
At first blocking column `j`, compare current depth `x = K_b[j]` to accepted set `A = A[l,j]`.

Define:
- `minA = min(A)`;
- `maxA = max(A)`.

Three canonical failure relations exist:

### TOO_SHALLOW
If `x < minA`, feedback says this column needs to be **deeper than current**.

### TOO_DEEP
If `x > maxA`, feedback says this column is **already deeper than every accepted value**.

### BETWEEN_BRANCHES
If `minA < x < maxA` but `x ∉ A`, then the column lies in a gap between two accepted master branches. Feedback says **current depth lies between valid bands**.

No other failure class exists.

## 6.2 Impression strength
For presentation/tutorial readability, TOO_SHALLOW may additionally expose a bounded qualitative distance:
- `LIGHT` if the nearest accepted deeper value is exactly `x+1`;
- `STRONG` if nearest accepted deeper value is `≥ x+2`.

This strength is deterministic and optional for solving. It never gives exact hidden depth unless the set can logically be deduced from accumulated evidence.

TOO_DEEP has no misleading `file more` mark. It uses a visibly different overcut scar/indicator.

BETWEEN_BRANCHES uses a split-band symbol, never a conventional impression mark.

## 6.3 Knowledge ledger
For each `(blank, lock, column)`, player-visible knowledge stores monotonic logical observations, not guessed hidden values:
- untested/unknown;
- this column was accepted during a test that reached beyond it;
- too shallow at tested depth `x`, with LIGHT/STRONG if shown;
- too deep at tested depth `x`;
- between branches at tested depth `x`;
- lock opened with tested depth `x`.

The UI may summarize deductions, but must distinguish:
- **observed fact**;
- **logical deduction**;
- **still unknown**.

## 6.4 Accepted-prefix information
If a failure occurs at column `j`, then columns `1..j-1` are known to accept their currently tested depths. This is legitimate information and is recorded automatically.

Columns `j+1..C` remain completely unevaluated to the player for that test.

## 6.5 Repeated identical tests
Repeating `TEST` with identical key vector, lock and access state:
- returns exactly the same result;
- adds no new information;
- does not alter any state except presentation counters that are non-authoritative;
- cannot advance hints or unlock gates merely through repetition.

---

# 7. Successful test semantics

When every column is accepted:
- the lock enters `OPENED` state;
- the tested key is unchanged;
- all current tested depths are recorded as accepted observations for that lock;
- any explicit access consequences of opening that lock resolve immediately in the deterministic ordering defined below.

A required lock remains satisfied even if the player later files the key that opened it into an incompatible shape. The fantasy is that the job requires each lock to have been successfully opened at least once, not that all final keys must simultaneously still open every completed lock.

However, content may define a visible **Final Coverage** objective requiring simultaneous end-state coverage; such an objective is reserved for optional mastery cases unless explicitly introduced into core progression in Phase 5. Main-campaign default is `opened once = completed`.

This distinction prevents solved work from being silently invalidated and keeps state legible.

---

# 8. Test access and order rules

The system may create information-order puzzles, but restrictions must be systemic and visible rather than arbitrary fiction.

## 8.1 Access model
Each lock has an access predicate over already-opened locks and explicit case switches.

Normal allowed forms:
- `ALWAYS`;
- `AFTER_OPEN(lock_x)`;
- `AFTER_ANY(set)`;
- `AFTER_ALL(set)`.

No hidden clock, random customer arrival or narrative permission can decide test legality.

## 8.2 Access graph constraints
Validator requires:
- access graph acyclic for mandatory locks unless an alternate initially accessible route exists;
- at least one legal test action at initial state;
- every required lock eventually reachable in at least one valid solution;
- access restrictions visible before the player commits irreversible cuts that depend on them.

## 8.3 Lock opening may reveal another lock
Opening a lock can expose a later cylinder/fixture on the same authored bench/case. This is presentation of `AFTER_OPEN`, not a new mechanic.

## 8.4 Test cost
Core campaign tests cost no consumable resource and no score. Their cost is information order and the risk that the player chooses to file based on partial information.

No stamina, money, durability or time tax may be attached to testing in core campaign.

---

# 9. Multi-key / multi-lock lifecycle

## 9.1 Persistent blanks
Every blank remains in the case from start to finish unless the player explicitly restarts to a prior state.

A blank can be:
- untouched;
- partially filed;
- diagnostic-only so far;
- already used to open one or more locks;
- later further filed and repurposed.

There is no `assign key to lock` action. Coverage emerges only from actual successful tests.

## 9.2 Blank identity
Blank identity matters because knowledge is tied to the tested physical artifact state at the time of observation. Two blanks with identical current vectors are mechanically interchangeable for fit, but their history/knowledge ledger can differ.

For future solvability ignoring player knowledge, identical vectors can be symmetry-collapsed by solver. For information-respecting hints, they remain distinct when their observation histories differ.

## 9.3 Opened lock persistence
Once opened, a required lock remains marked complete. Opening it again:
- is legal if accessible;
- yields no new completion progress;
- can still yield accepted observations for a different blank/vector;
- cannot duplicate rewards or access effects.

## 9.4 Key disposal
There is no discard/destroy verb in core campaign. A hopelessly overcut key remains visible as a consequence and may still carry diagnostic history.

---

# 10. Commitment, Undo, Restart and recovery

The product thesis requires irreversible reasoning without punishment through lost real-world time.

## 10.1 Action timeline
Authoritative actions are discrete:
- `FILE`;
- `TEST`;
- `OPEN` consequences are part of TEST resolution;
- explicit case switch actions if Phase 5 introduces any, but no such switch is required by Phase 4 core.

Camera/UI actions never enter puzzle history.

## 10.2 Undo policy
Core campaign supports unlimited stepwise Undo back to case start, with these rules:
- Undo reverses the last authoritative action exactly;
- Undo may reverse FILE, TEST knowledge updates and OPEN/access consequences;
- Undo is immediate and deterministic;
- using Undo does not reduce completion rating in the base campaign;
- optional mastery badges may track `No Undo`, but content cannot require them for progression.

Why this does not violate irreversible cuts: irreversibility is the forward-state decision grammar. Undo is a puzzle recovery/time-respect affordance, equivalent to rewinding the authored state machine.

## 10.3 Redo
Redo is available until the player takes a different authoritative action after Undo. Redo replays exact stored transitions, never recomputes against mutated hidden state.

## 10.4 Restart
`Restart Case` restores exact authored initial state and clears case knowledge/history. Confirmation is required only if at least one authoritative action has occurred.

## 10.5 Softlock detection
After every FILE and successful access change, a bounded background validator may determine whether any solution remains from authoritative state.

If proven unsolvable:
- game does **not** auto-rewind;
- player receives a neutral `NO VALID COMPLETION REMAINS FROM THIS STATE` option after a short grace interval or when requesting hint;
- primary choices: Undo / Restart / Continue Experimenting;
- the game must not identify the exact mistake unless the hint system has progressed to that tier.

If solver cannot prove unsolvability within budget, no false warning is shown.

## 10.6 Auto-checkpoints
Every authoritative action is an in-memory checkpoint. Persistent save stores the current state plus enough history for a bounded Undo window covering at minimum the entire current case; preferred implementation stores the complete case action list because state ceilings are small.

---

# 11. Win, fail and no-dead-time rules

## 11.1 Case win
Default required-case win:

`all required locks have OPENED = true`

Then the case enters solved review. Player may inspect/replay solution before continuing.

## 11.2 Fail
Core campaign has no punitive immediate fail for a wrong cut. A case is effectively failed only when:
- no valid completion remains from current state; and
- player chooses Restart/Undo rather than continuing exploration.

No lives, currency loss or campaign setback.

## 11.3 No-dead-time contract
- filing animation target ≤0.8 s at normal speed and skippable/accelerable;
- test animation target ≤1.5 s to first meaningful result, then may continue flourish in background;
- repeated test can be fast-forwarded after first presentation;
- restart target near-instant after transition;
- no mandatory walk between bench objects;
- no hold-to-file grind;
- no repeated multi-stroke input for one depth step.

These are mechanical pacing requirements, not final animation timings.

---

# 12. Progression and difficulty grammar

No new fundamental verb is introduced after the demo. Difficulty grows through composition of the same primitives.

## Tier 0 — Causal literacy
Purpose: learn one-step cut, test, first-blocking order, overcut permanence.

Structure:
- 1 lock;
- 1 blank;
- 4 columns;
- mostly singleton accepted sets;
- no access gates/master/wear.

Thought: `test → identify first blocker → file exactly as needed`.

## Tier 1 — Preserve overlap
Add 2–3 locks with obvious shared accepted values and enough blanks to recover.

Thought: `opening current lock is not the only objective`.

## Tier 2 — Partition targets
Fewer blanks than locks; at least one key must open multiple locks.

Thought: `which locks should share an artifact?`

## Tier 3 — Destructive diagnosis
Multiple testable locks; current blank can reveal useful prefix/directional facts before it is committed.

Thought: `information can be worth more than immediate completion`.

## Tier 4 — Master branches
Introduce accepted-set unions. Branches create shallow/deep alternatives without new action vocabulary.

Thought: `which valid branch preserves cross-lock compatibility?`

## Tier 5 — Wear bridges
Introduce wider intervals that can bridge otherwise incompatible targets.

Thought: `do not optimize toward the apparent center of a tolerant target`.

## Tier 6 — Access order
Some locks become testable only after others open. The access graph is visible.

Thought: `what must I learn before a destructive commitment, given future information order?`

## Tier 7 — Mixed finales
Combine:
- 5–6 columns;
- 4–6 locks;
- 2–3 blanks;
- ≤2 master columns total per lock and ≤2 disjoint intervals per column;
- ≤2 worn/wide columns per lock;
- shallow access graph;
- at least two plausible but losing greedy policies.

Thought: `partition + preserve + diagnose + branch + order`.

---

# 13. Anti-greedy / dominant-policy requirements

A mature case is invalid if any of the following cheap policies solve it without a materially distinct decision:

`G1` — File the first blocking column until the current lock opens, then move on.

`G2` — Always use a fresh blank for a newly encountered lock while blanks remain.

`G3` — Always keep every column as shallow as possible.

`G4` — Always cut toward the deepest hinted need.

`G5` — Always test locks in listed/left-to-right order when multiple are accessible.

`G6` — Once a key opens one lock, never modify it again.

`G7` — Once a key fails a lock, abandon that key for that lock.

`G8` — Reserve one blank untouched until the final lock regardless of evidence.

## Mature-case validation requirement
For cases labeled Tier 3+, content validator must evaluate at least G1–G6. At least two of those policies must either:
- provably fail; or
- produce strictly dominated final state under an authored mastery metric without being required for campaign win.

Tier 6–7 should defeat at least three cheap policies.

No case should defeat a policy only through a one-off exception rule.

---

# 14. Solver and validator contracts

## 14.1 Omniscient solvability solver
Static input:
- all `A[l,c]`;
- starting key vectors;
- lock access graph;
- required-open set.

State sufficient for future physical solvability:
- key vectors for all blanks;
- opened-lock bitset;
- access state if not derivable purely from opened locks.

Knowledge ledger is excluded from omniscient solvability because hidden knowledge does not change fit or legal FILE transitions.

## 14.2 Information-respecting solver
For hint/fairness validation, state additionally includes player-observable knowledge ledger.

Its policy may only choose actions justified by:
- visible starting state;
- prior deterministic observations;
- rules already taught by that campaign point.

It may not read unrevealed accepted sets to choose an action.

A case is **information-fair** if at least one winning policy exists under these constraints without trial branches that require knowing hidden state in advance.

## 14.3 Search action pruning
Solver may prune:
- repeat identical TEST with no new state;
- FILE at max depth;
- TEST of inaccessible lock;
- symmetric blanks only in omniscient mode when vector and access consequences are identical;
- actions after win.

## 14.4 Content rejection gates
Reject case if:
- no solution exists;
- information-respecting solver finds no fair policy within exhaustive bounded state;
- required content depends on more than defined ceilings;
- opening a lock depends on presentation state;
- a hidden rule changes accepted sets;
- mature case is solved by too many cheap policies;
- every winning solution requires arbitrary blind guessing between observationally equivalent actions with different hidden outcomes;
- solution length is dominated by repetitive filing rather than decisions.

---

# 15. Balance knobs and hard ceilings

## 15.1 Primary knobs
- columns `C`: 4–6;
- depth max `D`: 3–5;
- locks: 1–6 normal, 7 absolute authored exception ceiling for optional challenge only;
- blanks: 1–3 normal, 4 absolute ceiling;
- accepted interval width;
- number of disjoint branch intervals;
- overlap density between locks;
- number/depth of access dependencies;
- number of plausible partitions;
- information gained per test through first-blocking position;
- initial pre-cut depth if used;
- count of mandatory destructive conversions after diagnostic use.

## 15.2 Hard complexity ceilings
Main campaign:
- `C ≤ 6`;
- `D ≤ 5`;
- `|L| ≤ 6`;
- `|B| ≤ 3`;
- ≤2 disjoint accepted intervals per `(lock,column)`;
- ≤2 master-branch columns per lock;
- ≤2 widened/wear-signaled columns per lock;
- access dependency depth ≤3;
- no more than 3 simultaneously inaccessible future required locks;
- no timed reasoning;
- no consumable test resource.

## 15.3 Busywork ceiling
A validated intended solution should normally require:
- ≤18 committed FILE actions;
- ≤12 information-producing failed TEST actions;
- ≤30 total authoritative actions excluding optional exploratory/repeated tests.

Tier 0 tutorial may be smaller. Optional challenge may exceed by ~25% only if action diversity remains high.

---

# 16. Edge-case ordering

For one authoritative action, use this exact order.

## FILE ordering
1. validate case not already in solved-locked transition;
2. validate blank/column legal;
3. create pre-action undo record;
4. increment depth exactly one;
5. update rendered candidate/current profile;
6. invalidate derived fit previews/hints;
7. run bounded softlock check asynchronously or deterministic deferred step;
8. autosave action record.

## TEST ordering
1. validate lock access;
2. snapshot key vector;
3. evaluate columns `1..C` against immutable accepted sets;
4. derive OPEN or first blocker + relation;
5. create pre-action undo record;
6. merge observations into knowledge ledger;
7. if OPEN and not already opened, set opened bit;
8. resolve all access predicates from new opened bitset;
9. check case win;
10. update presentation;
11. autosave action record.

## Simultaneous access unlocks
If one OPEN causes several locks to become accessible, all are enabled in ascending authored lock ID in data but presented simultaneously. There is no intermediate decision between them.

## Testing an already-open lock
Allowed. It follows normal TEST semantics. `opened` remains true and access side effects are idempotent.

## Undo of a first-time OPEN
Undo returns:
- opened bit to prior value;
- access state to exact prior derivation;
- knowledge ledger to prior state;
- no residual presentation can remain authoritative.

---

# 17. Deterministic replay contract

Given:
- case content version/hash;
- authored initial state;
- ordered authoritative action list;

the game must reconstruct identical:
- key vectors;
- opened-lock bitset;
- access state;
- knowledge ledger;
- win/unsolvable status.

Replay may differ only in non-authoritative interpolation, particles, camera and audio variation.

Random seeds are unnecessary for the core domain and must not affect it.

A save loaded mid-case must be equivalent to replaying its stored authoritative action list from the same content version, or to loading a snapshot verified against that replay.

---

# 18. Hint mechanical authority

Detailed UX belongs to Phase 6, but Phase 4 defines what hints are allowed to know.

Hint tiers may use information-respecting solver only.

Allowed progression:
1. **State hint:** point out an already observed fact or conflict the player may have missed.
2. **Question hint:** identify the strategic question (`Do these two locks still share a possible depth here?`).
3. **Action-class hint:** recommend testing a particular accessible lock or preserving a particular blank, without revealing hidden values.
4. **Direct next action:** only after explicit player request; may say `test B on lock 3` or `file column 2 one step` if that action is justified by current visible knowledge.

Forbidden:
- revealing unrevealed accepted depth values;
- selecting an action using omniscient hidden state when the player could not infer it;
- silently correcting a case after bad cuts.

---

# 19. Mechanical acceptance tests

The following are mandatory acceptance tests for implementation and later content validation. IDs are stable Phase-4 references.

## A. Key/file authority
**M01** A blank at `[0,0,0,0]`, FILE(c2), becomes `[0,1,0,0]` and nothing else changes.

**M02** Two FILE(c2) actions produce depth `2`, never one continuous/fractional state.

**M03** FILE on a column at `D` performs no authoritative transition.

**M04** Canceling a preview before commit leaves key vector unchanged.

**M05** Skipping filing animation yields the same key vector as watching it fully.

**M06** A visual notch that disagrees with vector state is a presentation bug; fit follows vector state.

**M07** No legal forward action can reduce a key depth.

**M08** Undo after FILE restores exact previous vector.

**M09** Redo after M08 restores exact filed vector.

**M10** Taking a new authoritative action after Undo invalidates incompatible Redo history.

## B. Fit / accepted sets
**M11** Key opens when every depth is a member of its column accepted set.

**M12** One incompatible column prevents OPEN even if all others match.

**M13** Contiguous interval `{1,2,3}` accepts all three and rejects 0/4.

**M14** Two-branch set `{1,2} ∪ {4}` accepts 1,2,4 and rejects 3.

**M15** Wear/wide interval does not change after repeated tests.

**M16** Required content with an empty accepted set is rejected by validator.

**M17** Accepted-set membership is integer/discrete; floating render position cannot change result.

**M18** Same key vector against same lock always yields same fit result.

## C. First-blocking / information
**M19** With incompatibilities at c2 and c4, a failed test reports c2 only.

**M20** After M19, current tested depths at c1 are recorded accepted; c3–c4 remain unobserved.

**M21** TOO_SHALLOW occurs only when current depth is below every accepted value.

**M22** TOO_DEEP occurs only when current depth is above every accepted value.

**M23** BETWEEN_BRANCHES occurs only when current depth lies inside the span but outside a disjoint accepted union.

**M24** LIGHT too-shallow mark occurs when nearest deeper accepted value is exactly +1.

**M25** STRONG too-shallow mark occurs when nearest deeper accepted value is +2 or more.

**M26** Repeating an identical failed TEST adds no new knowledge.

**M27** Filing an earlier blocker so it becomes accepted allows the next incompatible column to become the reported blocker on retest.

**M28** Successful OPEN records all current column depths as accepted observations for that lock.

**M29** Knowledge ledger never labels an untested later column as accepted merely because an earlier column failed.

**M30** A hint never exposes an unrevealed exact accepted depth unless logically forced by observations.

## D. Access/order
**M31** Inaccessible lock rejects TEST with no puzzle-state mutation.

**M32** Opening prerequisite lock makes AFTER_OPEN target accessible in the same resolved action.

**M33** AFTER_ALL requires every named prerequisite opened.

**M34** AFTER_ANY resolves after the first named prerequisite opens.

**M35** Opening the same prerequisite again does not duplicate access effects.

**M36** Validator rejects mandatory cyclic access with no initially accessible break/alternate route.

**M37** Initial state always has at least one legal TEST in validated campaign content.

**M38** Access restrictions are encoded in case data, not narrative/random timing.

## E. Persistent key lifecycle
**M39** Key that opened lock A can later be filed deeper and still leaves A marked completed.

**M40** That deeper key may lose physical ability to reopen A without undoing A's completion bit.

**M41** Same key may open A and B if its vector belongs to both complete acceptance products.

**M42** Two different blanks with identical vectors produce identical fit results on the same lock.

**M43** Those two blanks may retain different knowledge histories without changing physical fit.

**M44** There is no campaign action to discard a blank and receive a replacement.

**M45** Already-open lock may be tested with another key and can add knowledge without duplicate completion.

## F. Undo/restart/replay
**M46** Undo of failed TEST restores knowledge ledger exactly to pre-test state.

**M47** Undo of first OPEN restores lock to unopened and reverses newly unlocked access.

**M48** Restart restores authored initial vectors, lock bits, access and empty case knowledge.

**M49** Replaying stored action list reconstructs same final authoritative state.

**M50** Save/load of the same state yields same next TEST result.

**M51** Repeated TEST presentation counters, particles or camera changes do not enter solver state.

**M52** If a solver proves current state unsolvable, game offers recovery but does not auto-undo.

**M53** If bounded solver cannot prove unsolvability, game never falsely labels state dead.

## G. Win/fail
**M54** Case wins exactly when all required lock opened bits become true under default objective.

**M55** Optional locks do not block default case win.

**M56** A bad cut alone does not trigger a punitive fail screen.

**M57** Player may continue testing/experimenting in a proven dead state until choosing recovery.

**M58** No base-campaign score/reward is lost for Undo.

## H. Anti-greedy adversarial cases
**M59** At least one Tier-2+ validation case defeats `fresh blank for every new lock` because blanks < locks and overlap permits success.

**M60** At least one Tier-3+ case defeats `file current first blocker until current lock opens` while an information-respecting winning policy exists.

**M61** At least one master-branch case defeats `always choose deepest valid branch`.

**M62** At least one case defeats `always stay shallow` because a non-overlapping deep target must be committed.

**M63** At least one access-order case defeats left-to-right testing without adding hidden/random rules.

**M64** At least one mature case requires modifying a key after it has already opened a lock.

**M65** At least one mature case rewards preserving a failing diagnostic key through ≥2 informative tests before converting it.

**M66** A mature case is rejected if G1–G6 all solve it with no meaningful divergence.

## I. Information fairness
**M67** A validated authored case has at least one information-respecting winning policy.

**M68** Two actions indistinguishable under all current observations cannot be made secretly outcome-critical unless later safe testing can disambiguate before irreversible commitment.

**M69** No required solution assumes knowledge of a later column that has never been reached by a test or logically deduced.

**M70** The omniscient solver may find shorter solutions than information-respecting solver; content scoring never treats the omniscient path as the expected player path.

**M71** Hint solver chooses only actions justified by currently visible knowledge.

**M72** Repeating a no-information test cannot unlock a stronger hint tier merely by repetition.

## J. Complexity/pacing ceilings
**M73** Main campaign validator rejects C>6.

**M74** Main campaign validator rejects D>5.

**M75** Main campaign validator rejects >3 blanks.

**M76** Main campaign validator rejects >6 required locks.

**M77** Normal content rejects >2 disjoint accepted intervals in one column.

**M78** Normal content rejects access dependency depth >3.

**M79** Intended normal solution >18 FILE actions triggers content-review warning.

**M80** Intended normal solution >30 authoritative actions triggers content-review warning.

---

# 20. Phase-4 closure criteria

Phase 4 is complete because the design now fixes:
- discrete cut coordinates and transitions;
- exact accepted-set semantics;
- master/wear representation without realism exceptions;
- deterministic fit and blocker ordering;
- exact failure-information classes and accepted-prefix knowledge;
- test access/order grammar;
- persistent multi-key/multi-lock lifecycle;
- commit/Undo/Redo/Restart/softlock recovery;
- case win/fail semantics;
- progression from exact correction through mixed partition/information finales;
- anti-greedy requirements;
- omniscient and information-respecting solver contracts;
- balance knobs and hard ceilings;
- action ordering and deterministic replay;
- hint information authority;
- **80 mechanical acceptance tests**.

No unresolved Phase-4 blocker requires a new verb or realism exception.

## NEXT PHASE
**Phase 5 — Content Architecture.**

Phase 5 must define:
- campaign structure and target case count;
- demo sequence;
- exact case/content data schema;
- structural puzzle families and minimum/target counts;
- tutorial dependency graph;
- authored vs generated responsibilities;
- case generator/solver/validator pipeline;
- anti-isomorphism metrics and duplicate detection;
- difficulty/readability/content-review gates;
- mastery/optional case boundaries;
- minimum shippable content vs target content;
- content expansion boundaries without new mechanics;
- >=50 content acceptance tests.
