# GAME #010 — PHASE 9 WHOLE-GAME SIMULATION CLOSURE

Date: 2026-08-31
Status: **PHASE 9 COMPLETE — second hostile whole-product pass complete**
Game: Luggage Carousel Zero *(working title)*

Authority: all prior active Game #010 authorities -> `GAME10_PHASE9_SIMULATION.md` -> this file.

This closure performs the exact hostile scenarios required by `STATUS.md`. It does not begin implementation. Findings that belong to adversarial design repair are carried explicitly into Phase 10 rather than silently changing earlier canon here.

---

## 1. Worst-case campaign progression — multiple blockers across acts

Simulated target architecture: A7/B8/C8/D9/E10.

Path:
1. A01–A04 complete; A05 blocks; `Skip for now` opens A06 and consumes A skip.
2. A06/A07 complete; B unlocks with A05 unresolved.
3. B01–B04 complete; B05 blocks; B skip opens B06. B06–B08 complete; C unlocks with A05+B05 unresolved.
4. C repeats the same pattern with C04 unresolved; D unlocks.
5. D repeats with D06 unresolved; E unlocks.
6. E uses its one skip on E08; player completes the remaining reachable E frontier and reaches ending with **five unresolved cases total**, one per act.

Required state at ending:
- `campaign_ending_seen = true`;
- `ALL_CASES_COMPLETE = false`;
- each act whose skip was used keeps `skip_used = true` permanently for progression history;
- each unresolved skipped case remains playable/open;
- no earlier act relocks;
- no second skip becomes available merely because the player entered a later act.

Cleanup path:
1. Player later solves A05 -> A `skipped_open_case_id` clears, A `skip_used` remains true.
2. Repeat B05, C04, D06, E08 in arbitrary order.
3. Clearing the final unresolved case makes the current base-campaign completion predicate true and reconciles `ALL_CASES_COMPLETE` exactly once.
4. `RETURNED_TO_BLOCKER` may be earned on the first qualifying cleanup and is not farmable by replay.

**Verdict:** multiple per-act skips do not create a progression deadlock. Ending access and complete-content status remain correctly separate.

---

## 2. Historical Efficient Route + content/certificate update

### Hostile scenario
Player solved case C05 on content hash `H1` in 6 ticks and earned Efficient Route against certificate minimum 6. A later patch changes the case definition to hash `H2` and recertifies minimum 7 (or 5). The stable `case_id` remains C05 so campaign progression should not be revoked.

The old rule `best_ticks <= current minimum_ticks` is insufficient if `best_ticks` has no provenance. A 6-tick record achieved on H1 is not evidence that the player solved H2 in 6 ticks. If H2 minimum becomes 7, blindly comparing values would incorrectly preserve/grant Efficient Route; if H2 minimum becomes 5, the record could incorrectly appear as a valid but slower attempt on a puzzle never played.

### Required carry into Phase 10
- basic completion may remain monotonic for progression when a stable case ID survives an update;
- **optimization records require content/rules provenance**;
- a best-tick record is eligible for current Efficient Route only when its provenance is compatible with the current case hash + rules semantics according to the certificate compatibility policy;
- incompatible historical optimization records may be retained as history but are not current mastery evidence until the updated case is replayed;
- platform achievements already granted are never revoked because a patch changed a certificate.

This is a specification/persistence repair, not a gameplay mechanic change.

---

## 3. DEAD after every action class

The existing Phase-8 semantics were simulated exactly before adversarial judgment.

### 3.1 First K1 swap -> DEAD
A legal adjacent swap commits, exact feasibility says no winning continuation. State becomes DEAD. Undo restores the pre-swap label vector, K bandwidth, terminal state and last-result state.

State restoration itself is correct.

### 3.2 First K2 swap
After first K2 swap, feasibility search includes the remaining one swap. If no continuation exists even with that remaining bandwidth, old semantics declare DEAD; otherwise the player may make the second swap or Advance. Undo restores K2 turn start correctly.

### 3.3 Second K2 swap -> DEAD
Second swap spends remaining bandwidth. Exact infeasibility raises DEAD; Undo once restores the post-first-swap state with one swap available; Undo twice returns turn start. Restoration is coherent.

### 3.4 ADVANCE miss -> DEAD
ADVANCE rotates, incoming bag misses, tick decrements, K resets if time remains, then exact feasibility says no completion remains. Terminal DEAD coexists with a visible neutral MISS last-result. Undo restores the complete pre-Advance boundary.

### 3.5 ADVANCE pickup -> DEAD
ADVANCE rotates and successfully consumes current bag/passenger, tick decrements, passengers still remain, and the resulting state has no winning completion. Terminal becomes DEAD after the successful pickup. Last result still truthfully records PICKUP. Undo resurrects bag/passenger and restores the prior committed boundary.

### 3.6 Final pickup
If that pickup serves the final passenger, WON wins before budget/dead checks. DEAD can never override a completed queue.

**State-machine verdict:** all action classes have coherent restoration and terminal ordering.

**Product-experience concern carried to Phase 10:** immediate DEAD after a SWAP exposes a perfect binary feasibility oracle before the player advances the carousel. With unlimited Undo and <=8 adjacent edges, a player can probe candidate swaps until the game confirms one still has a winning continuation. This may materially collapse intended reasoning despite state correctness.

---

## 4. Content / certificate / schema mismatch attack

### Case content hash mismatch
Release package containing case hash H2 with certificate for H1 is invalid. Packaging must fail. Development runtime may mark the case uncertified but cannot present heuristic DEAD or Efficient Route as authoritative.

### Rules semantics mismatch
Any rules-semantics bump invalidates affected certificates and exact-feasibility artifacts. Release cannot use old artifacts under new semantics.

### Content manifest mismatch on active case
Profile progression remains. `active_case` is discarded/restarted if its stored case/manifest cannot be proven compatible. One-time notice is sufficient; no mid-puzzle guessed migration.

### Save schema mismatch
Known older schema migrates via chained explicit `vN -> vN+1` functions. Unknown future schema is not rewritten as current; loading fails safe and preserves the source file for recovery/diagnosis.

### Unknown/removed case IDs
Do not reassign. Preserve as orphaned historical progress or ignore for current unlock calculations.

**Verdict:** content/certificate/schema authority remains coherent, with optimization-record provenance repair still required.

---

## 5. Corrupted save / backup paths

### Corrupted active case only
Discard/restart active case; retain profile progression. Never allow active-session corruption to erase campaign progress.

### Corrupted newest profile + valid previous-good backup
Validate newest before promotion. On failure, load previous-good backup, migrate if necessary, and show at most one non-blocking recovery notice.

### Both newest profile and backup invalid
Do not reinterpret arbitrary fields. Start a safe fresh logical profile **only after preserving/quarantining the invalid files where practical**, so a later support/dev recovery remains possible. Content resources are never repaired from player-save data.

### Cloud has older valid profile than local
Merge policy must remain monotonic for supported mergeable fields (completion union, best compatible record by minimum tick value, achievements idempotent) rather than blindly replacing a newer local profile by timestamp alone. Non-mergeable act skip/frontier state is recomputed from canonical source progression fields after merge.

### Cloud contains malformed or future-schema file
Treat it as an invalid candidate, not as authority merely because cloud timestamp is newer.

**Verdict:** recovery can remain loss-minimizing and deterministic.

---

## 6. Achievement reconciliation under updates/recovery

- Platform grants are monotonic; never revoke an achievement because content changed.
- Local achievement reconciliation flags remain idempotent.
- `ALL_CASES_COMPLETE` is evaluated against the frozen base-campaign scope for the shipped product; later bonus/update cases must not retroactively revoke or redefine the already-earned achievement.
- `RETURNED_TO_BLOCKER` needs durable local reconciliation/event history because once a skipped case is completed, current progression state alone no longer proves that it was previously skipped. Existing `achievement_local_flags` can hold this fact; implementation must not attempt to re-derive it only from current `skipped_open_case_id`.

No contradiction with Phase 7 achievement list.

---

## 7. Phase-9 closure verdict

The second whole-game simulation found **no campaign deadlock, terminal-state contradiction or unrecoverable persistence path**. It did uncover two adversarial specification problems that must be repaired in Phase 10:

1. historical `best_ticks` need case/rules provenance before they can qualify for current Efficient Route after content changes;
2. player-facing DEAD after every SWAP acts as a binary solver oracle and may undermine the puzzle's intended reasoning.

These are bounded repairs inside existing systems. They do not require a new mechanic, content family, economy or scope expansion.

**PHASE 9 COMPLETE. DESIGN COMPLETE = NO.**

Next authority: `GAME10_PHASE10_REVIEW.md`.
