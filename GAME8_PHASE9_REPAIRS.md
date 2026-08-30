# GAME #008 — PHASE 9 CROSS-AUTHORITY REPAIRS

Last updated: 2026-08-30
Phase: **9 — Whole-Game Simulation Repairs**
Selected concept: **G8C02 Locksmith's Margin**
Production implementation started: **NO**

This file records narrow corrections discovered by end-to-end simulation. It is **repair authority** over conflicting Phase 3–8 wording until Phase 11 consolidates the final specification. It does not add a new gameplay verb, content family, economy, or platform promise.

## R1 — Repeated identical TEST is an authoritative history action, but not new puzzle information
Conflict found:
- Phase 4 §6.5 says an identical repeated TEST "does not alter any state except presentation counters";
- Phase 8 §4.2 correctly needs every legal TEST to produce an ActionRecord so Undo/Redo/history match what the player actually did.

Repair:
- a repeated identical legal TEST **does append one authoritative TEST history record/checkpoint**;
- its tested vector/result are identical;
- it adds **zero new KnowledgeState observations/deductions**;
- it changes no key vector, opened bit, access state, case progress, hint tier, tutorial trigger, reward, mastery counter, or achievement counter merely because it was repeated;
- Undo removes that repeated TEST record/checkpoint and returns to an otherwise equivalent puzzle state;
- solver/search may safely prune such a TEST when history itself is irrelevant to future solvability.

Therefore "no new state" in Phase 4 is read as **no new puzzle/knowledge/progression state**, not "no history record".

## R2 — Solved attempt and committed campaign progression are separate transaction boundaries
Problem found:
If opening the final required lock immediately writes permanent CampaignProgress/achievement unlocks, then exact Undo from solved review can restore an unsolved PuzzleState while the campaign remains permanently solved. That violates the player's visible causal model and makes crash recovery ambiguous.

Repair:
1. The TEST that opens the final required lock produces `ATTEMPT_SOLVED` and enters `SOLVED_REVIEW_PENDING_COMMIT`.
2. The complete attempt timeline, including the successful final TEST, remains Undo/Redo-capable while the player stays in solved review.
3. No new permanent campaign unlock, first-solve achievement, best-stat replacement, or case-completion commit occurs merely from the animation/result frame.
4. `Continue`, `Return to Case Select`, or an explicit equivalent leave-review action performs one idempotent `COMMIT_SOLVED_ATTEMPT` transaction.
5. After that transaction the case is permanently solved in CampaignProgress. Re-entering/replaying the case creates a new attempt; ordinary in-attempt Undo does not erase previously committed campaign history.
6. Quitting/crashing in solved review **before** commit reloads the solved pending-review attempt and permits Continue or Undo.
7. Quitting/crashing **during** commit resolves idempotently to either the prior pending-review record or fully committed campaign progress; never half-unlocked progress.
8. Achievement/platform reconciliation consumes committed campaign events, not raw animation callbacks.

This repair supersedes any Phase-8 wording suggesting campaign solve may be permanently recorded immediately on `CASE_SOLVED`.

## R3 — Authoritative action durability precedes presentation completion
For FILE and legal TEST:
- Domain Core commits the complete semantic transition first;
- the new attempt state + history checkpoint becomes the next save candidate before or concurrently with downstream animation;
- animation is a replayable projection of already-committed domain events;
- a crash during filing/test animation may skip the remaining animation after reload, but **must never leave a half-cut key, partially learned TEST, half-open lock, or duplicated action**.

Minimum durability policy:
- autosave request after every authoritative FILE/TEST/Undo/Redo/Restart and after solved-attempt transition;
- writes may be coalesced for performance only if crash semantics still restore the latest fully committed authoritative boundary;
- pause/quit waits for or forces a safe local write when practical;
- platform Cloud sync is never the durability boundary.

## R4 — Presentation input lock cannot create a second authority timeline
Rapid input during FILE/TEST animation is handled as follows:
- semantic command acceptance is determined by Application/Domain state, not animation frame;
- while a command's result presentation is in a non-skippable critical beat, new authoritative FILE/TEST commands are queued at most one deep or rejected with neutral busy feedback; implementation chooses one policy globally and tests it;
- Undo may be accepted as a semantic request after the prior authoritative transition exists; presentation must snap/fast-forward safely before rendering the undone state;
- no double-click/button repeat may produce two FILE commits without two separately accepted `FILE_COMMIT` commands.

## R5 — Solved/opened access semantics during Undo
A successful TEST nests `newly_opened_lock` and derived access effects in the same ActionRecord.
- Undo of that TEST removes its new observations and, if it was the first opening of that lock on this timeline, restores the prior opened bitset and therefore prior derived access visibility.
- Any later TESTs that became possible through that opening would necessarily be later history entries and are undone first by stepwise Undo, so no dangling inaccessible-history state exists.
- Reopening an already-open lock creates a TEST record and observations but no duplicated open/access event.

## R6 — Runtime softlock result is advisory metadata tied to exact state identity
Background solver result must carry the exact canonical state/version it analyzed.
- `UNSOLVABLE`, `SOLVABLE`, or `UNKNOWN` is discarded if PuzzleState/action index has changed before delivery.
- `UNKNOWN` never surfaces as failure.
- Undo/Redo/new FILE immediately invalidates stale warnings.
- hint logic may use only a result matching current state and may never transform omniscient proof data into hidden accepted-set revelation.

## R7 — Demo → full import is idempotent recognition, never current-attempt transplantation
Repeated import twice must produce the same full-game state as import once.
Allowed imported domains:
- compatible settings/accessibility/input mappings;
- D01–D06 completion flags;
- tutorial-understood recognition;
- demo-earned eligible event facts that are explicitly mapped to full-game achievements after full-game commit/reconciliation.

Forbidden:
- arbitrary demo PuzzleState into C01–C32;
- duplicate achievements/unlocks;
- overwriting newer full-game progress with older demo flags;
- importing corrupt payload by partial field salvage unless each salvaged namespace independently validates.

## R8 — Cloud conflict policy remains local-first and attempt-aware
When Steam/platform service is unavailable, local play/save is complete.
When Cloud later presents divergent valid saves:
- never silently replace a newer in-progress local attempt solely because cloud timestamp is newer;
- compare schema/profile identity and committed campaign facts separately from current-attempt payload;
- present a human-readable conflict choice when automatic monotonic merge cannot prove safety;
- settings may use independent last-write selection because settings cannot erase puzzle completion;
- committed solved-case set/one-time event flags may merge monotonically where schemas match;
- current attempt history is chosen as one whole validated branch, never interleaved action-by-action.

## R9 — Content-version mismatch recovery
A saved current attempt records content identity/signature.
On mismatch after development/update:
- if an explicit tested migration exists, migrate then revalidate/replay history;
- otherwise preserve committed campaign completion/mastery, discard only the incompatible in-progress attempt, and restart that case from current authored initial state with an explanatory recovery notice;
- never reinterpret old action records against materially changed accepted sets;
- release updates should avoid modifying shipped case authority unless a bug requires it.

## R10 — Accessibility cannot change information authority
Reduced motion, high contrast, numeric depth labels, text-size/UI-scale, controller glyphs, localization and audio settings may alter presentation only.
- numeric depth labels expose current key depths already visible in key geometry, not hidden lock accepted depths;
- high contrast may emphasize the same first blocker/prefix, not later unevaluated columns;
- reduced motion may jump directly to the same final TEST/FILE presentation state;
- localization text expansion may reflow ledger/access text but never hide prerequisite IDs or semantic labels;
- all six-lock/three-key/six-column cases remain operable at 1280×800 with inspection zoom and scrolling rather than shrinking decision-critical text below the supported minimum.

## R11 — Identical-vector blanks remain distinct in player-facing knowledge/history
C26 and later cases depend on this.
- fit uses only vector + lock accepted sets, so equal vectors have equal fit outcomes;
- KnowledgeState/history is keyed by blank identity and may differ;
- omniscient solver may symmetry-collapse proven-equivalent blanks;
- information-respecting solver/UI/hints may collapse only under a knowledge-preserving permutation;
- key labels/physical rack positions remain stable through the attempt and save/load.

## R12 — Phase-9 authority precedence
Until Phase 11 freeze, if wording conflicts:
1. later explicit Phase-9 repairs in this file govern only the repaired clause;
2. otherwise the owning Phase 3–8 authority remains unchanged;
3. Phase 10 may attack these repairs;
4. Phase 11 must merge/normalize all surviving repairs into final authority and remove ambiguity.

No other Phase 3–8 rules are reopened by this file.