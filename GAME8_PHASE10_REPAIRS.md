# GAME #008 — PHASE 10 ADVERSARIAL REPAIRS

Last updated: 2026-08-30
Phase: **10 — Adversarial Review Repairs**
Selected concept: **G8C02 Locksmith's Margin**
Production implementation started: **NO**

This file is narrow repair authority over conflicting Phase 3–9 wording until Phase 11 normalizes the final specification. It introduces no currency, test cost, timed pressure, real-world locksmith procedure, or production implementation.

## AR1 — Exhaustive free TEST is baseline rational behavior, not a policy the campaign may pretend is strategically wrong
Adversarial proof:
- legal TEST costs no resource, score, time budget, durability, or forward key state;
- a failed TEST adds non-negative information;
- a successful TEST permanently opens a lock on the current forward timeline and can only preserve or increase access;
- therefore, at a fixed forward key state, performing every currently accessible, non-duplicate TEST before the next irreversible FILE is weakly dominant for information.

Repair:
1. Core campaign content may **not** rely on the player irrationally withholding a free currently accessible non-duplicate TEST.
2. `test every accessible lock with the current useful blank before filing` becomes a **baseline adversarial policy**, not a policy that mature content is universally required to defeat.
3. Mature cases must retain a meaningful FILE / partition / preservation decision **after all currently accessible non-duplicate TEST information at that state has been collected**.
4. Diagnostic sequencing remains valid only where the key decision is whether to preserve/alter a blank before information that is not currently accessible can be obtained, usually because access requires an OPEN or because a future vector is different.
5. Access-order content may create strategic choice through which lock is opened / which irreversible key state is committed to expose future locks; it may not claim strategic depth merely from choosing between two equally free currently accessible TESTs.
6. Repeated identical TEST remains informationally useless per Phase-9 R1.
7. No test currency, durability, score penalty, timer, patience meter or other punitive cost may be added to repair this.

Content consequences:
- C10/C12/C23/C25 must be validated specifically against exhaustive-current-state testing.
- C30 survives only if exhaustive testing of every accessible current vector still leaves a destructive compatibility dilemma. If exhaustive-current-state testing resolves the case without a meaningful FILE/partition decision, C30 is rewritten or cut.
- V5 policy suite is revised so exhaustive-current-state testing is an attack harness rather than an automatic required failure.

## AR2 — Unlimited Undo is an explicit assistance/recovery channel whose human-memory leakage is accepted
Adversarial proof:
A player can FILE to a speculative deeper vector, TEST, Undo the TEST and FILE, then retain the result in human memory even though KnowledgeState correctly rewinds. Repeating this can reveal information from counterfactual branches. Software cannot honestly erase human memory.

Repair:
1. This behavior is **allowed** in the base campaign. Undo remains unlimited, exact and non-punitive.
2. The design makes no claim that a player using exhaustive counterfactual Undo preserves the intended information scarcity.
3. Required progression, achievements and ordinary completion may never punish or block this behavior.
4. `Clean Bench` / no-Undo mastery may identify a forward-only replay challenge after first solve, but is optional and never a gate.
5. Hint language, mastery copy and store copy must not claim that hidden information is impossible to inspect via rewind.
6. Required case quality is judged primarily on forward play, but each mature case must also retain at least a non-trivial **omniscient coverage/partition problem** once accepted sets are known. A case whose only depth disappears completely when hidden sets are known is too fragile for the campaign.
7. Empirical gate: if >=25% of fresh target players naturally adopt systematic FILE→TEST→Undo probing before late campaign, or if such behavior materially improves reported fun/clarity over forward play, Phase-11 handoff must flag an implementation playtest decision about whether Undo presentation should be de-emphasized. Rules themselves remain unchanged unless concept authority is deliberately reopened.

## AR3 — D02 / C03 TOO_DEEP tutorial staging is exact and truthful
The previous architecture was ambiguous because a TEST itself is an Undoable history action.

Frozen tutorial blueprint:
1. D02 and C03 begin from a **solvable non-overcut authored state**.
2. The tutorial deliberately asks for one visible practice FILE that creates an overcut for the selected training lock. The state remains recoverable by Undo; no hidden alternate rule is used.
3. Player TESTs and receives TOO_DEEP.
4. Tutorial states: `This test proved the cut is too deep. Rewind the test, then rewind the cut.`
5. First Undo removes the TEST record/its observations from authoritative state; the physical result may remain in player memory, which is acceptable under AR2.
6. Second Undo restores the pre-cut key vector.
7. The case then resumes and remains solvable under ordinary rules.
8. Restart also restores the original solvable state; it is truthful because the authored start is not already overcut.
9. The tutorial never says a single Undo repairs the overcut and never says Restart repairs an authored defect.

D02 is the concise demo version; C03 may add the history-panel explanation but uses identical authority.

## AR4 — Redo tail persists across save/load
Phase 9 left this undecided. It is now frozen.

Persist for the active attempt:
- complete authoritative ActionRecord timeline;
- current timeline cursor/action index;
- enough deterministic state/snapshots to reconstruct the state at the cursor;
- all valid redo-tail ActionRecords after the cursor;
- pending solved-review state when applicable.

Rules:
1. Autosave after Undo/Redo preserves the redo tail.
2. Quit/crash/reload at a mid-history cursor restores both current state and available Redo exactly.
3. A new authoritative FILE/TEST after Undo truncates the redo tail before save, exactly as in-session behavior.
4. Content-version mismatch recovery may discard the whole incompatible attempt including redo tail under Phase-9 R9; committed campaign progress survives.
5. Cloud conflict chooses one validated current-attempt branch as a whole, including its cursor and redo tail; branches are never interleaved.

## AR5 — Solved-review commit transaction has one durable journal boundary
To close final-OPEN race ambiguity:
- active attempt has `attempt_state = ACTIVE | SOLVED_REVIEW_PENDING_COMMIT`;
- campaign has a stable `solve_commit_id = profile_id/case_id/attempt_id` or equivalent idempotency key;
- leave-review writes a local commit journal/transaction that contains solved case fact, unlock consequences, best-stat comparison and local achievement-event IDs;
- recovery replays/finishes the same idempotent commit if journal exists;
- platform achievement grants are downstream reconciliation and never authority for campaign solve;
- Undo is available only while the attempt remains pending review; after durable campaign commit, replay is a new attempt and cannot erase historical completion.

Acceptance requirement: kill/power-loss injection at every write boundary must recover to either exact pending review or exact committed state, never mixed unlocks.

## AR6 — Content quality floor is 28; 32 is aspirational and cannot be defended by parameter variation
Phase 10 does not pre-emptively cut four named cases because tutorial pacing may require simple cases. Instead it freezes stronger distinctness gates:
1. Release floor remains **28 strong cases**; target remains up to 32.
2. Every C07+ case must have a one-sentence `thought delta` that differs causally from its nearest campaign neighbor.
3. Canonical matrix/isomorphism similarity plus identical intended cheap-policy failure set triggers human review.
4. If two cases differ only by labels, column permutation, depth translation, accepted-set widening without new reasoning, or blank/lock renaming, merge/cut the weaker one.
5. Tutorial cases C01–C06 may be mechanically simple because each teaches a distinct truth; mature acts may not use tutorial necessity as filler defense.
6. Before freeze, C08–C12, C15–C16, C22–C26 and C30–C32 receive explicit information-respecting traces demonstrating no clairvoyant cut.
7. C32 must retain >=2 materially distinct valid partitions/traces as already required.

## AR7 — Tactile 3D scope is presentation, not a requirement for bespoke mechanical simulation
Cut scope aggressively:
- one bench environment;
- a small reusable key/lock visual kit;
- discrete generated notch profile from vector;
- cutaway animation driven from semantic TEST result;
- no modeled real pin-tumbler kinematics required;
- no hand/avatar locomotion;
- no physics-derived contact or freehand filing;
- no per-case bespoke lock mechanism;
- no optional `Reveal Mechanism` feature unless it can be built from the same fictional accepted-set visualization at near-zero design/QA risk.

If tactile 3D polish threatens solver/content/accessibility completion, physical fidelity is cut before deterministic domain/ledger/controller quality.

## AR8 — Commercial/store boundary tightened after fresh 2026 analogue check
Fresh evidence on 2026-08-30:
- `Access Key`, released 2026-04-08 on Steam, explicitly advertises locksmith gameplay including **lockpicking, key cutting and re-keying**.
- `Locksmith Simulator` remains listed as coming soon and advertises producing locks/keys plus broader locksmith jobs.

Neither located product owns Locksmith's Margin's multi-lock destructive-overlap grammar, but **key cutting itself is no longer a distinctive storefront verb**.

Repair:
1. Store/trailer/capsule differentiation must lead with **one persistent key opening several different locks / every cut destroys options**, not `be a locksmith` or `cut keys`.
2. Never use lockpick tools in key art/trailer.
3. Store tags/copy should favor Puzzle / Logic / Singleplayer / Relaxing or other accurate final tags over Realistic/Simulation if those tags would imply a trade simulator.
4. Blind capsule/trailer gate: >=70% of target respondents must describe multi-lock key-sharing / preserve-before-cut reasoning before describing burglary, lockpicking or generic job simulation.
5. If a closer direct analogue appears before release, re-run store-positioning review without automatically reopening the mechanical design.

## AR9 — Safety boundary: fictional mechanism must not teach real lock bypass
1. Accepted sets are fictional abstract bands; do not publish real bitting standards, real pin heights, brand keyways, tolerances, impressioning procedure, re-keying procedure, lockpick technique, bypass sequence, or security weaknesses.
2. Cutaway art must be stylized/non-diagnostic and need not correspond to a buildable real cylinder.
3. Tutorial language uses game terms such as `column`, `valid band`, `too shallow`, `too deep`, not real locksmith measurements or procedural advice.
4. `Reveal Mechanism`, if retained, reveals only fictional case matrices already used by the game and never maps them to real hardware.
5. Marketing avoids `learn locksmithing`, `realistic lock`, `authentic key cutting`, or other training claims.

## AR10 — Phase-10 precedence
Until Phase 11:
1. this file supersedes conflicting wording only for AR1–AR9;
2. `GAME8_PHASE9_REPAIRS.md` remains authority for its non-conflicting repairs;
3. owning Phase 3–8 files remain authority elsewhere;
4. Phase 11 must normalize surviving rules into final freeze authority.
