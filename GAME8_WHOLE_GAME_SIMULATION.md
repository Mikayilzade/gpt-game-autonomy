# GAME #008 — WHOLE-GAME SIMULATION ON PAPER

Last updated: 2026-08-30
Phase: **9 — Whole-Game Simulation on Paper**
Selected concept: **G8C02 Locksmith's Margin**
Working title: **Locksmith's Margin**
Production implementation started: **NO**

This phase simulates the complete player/runtime path against Phase 3–8 authority before adversarial review. It is not production code. All corrections discovered here are recorded in `GAME8_PHASE9_REPAIRS.md` and must be normalized at Phase 11.

---

# 1. Simulation method

The simulation uses the strict normal ceilings already frozen:
- 1–3 persistent blanks;
- 1–6 required locks;
- 4–6 columns;
- depths 0..D, D<=5;
- accepted finite depth sets only;
- FILE +1 only;
- deterministic TEST left-to-right, first blocker only;
- visible access predicates;
- exact Undo/Redo/Restart;
- no random/continuous fit authority.

Every trace asks four questions:
1. what is authoritative before the action?
2. what exact transition occurs?
3. what information is the player entitled to after it?
4. what survives save/load/crash/Undo?

---

# 2. First boot / profile / settings / controller detection

## Trace
1. First boot creates no puzzle state until profile namespace exists.
2. Steam/platform service may initialize asynchronously; failure does not block Main Menu.
3. Default accessibility is readable without color/audio dependence.
4. Keyboard+mouse is active; plugging a controller hot-swaps prompt glyphs while menu focus stays on the same semantic control.
5. Player opens Accessibility before C01: enables Reduced Motion, High Contrast, Show Discrete Depth Labels, larger text.
6. Settings save independently from campaign profile.
7. Player starts C01.

## Expected state
- no lock/key authority depends on device;
- no Steam callback can create campaign progress;
- settings corruption can be reset without damaging campaign;
- current input device only changes glyphs/mappings;
- C01 authored initial PuzzleState is identical regardless of accessibility/device.

## Result
PASS after R10 clarification. No product-thesis contradiction.

---

# 3. Demo D01–D06 fresh-player simulation

## D01 — First Mark
Start: one blank `[0,0,0,0]`, one lock.
Player TESTs. Columns 1..j-1 visibly settle; first blocker j reports TOO_SHALLOW. Player highlights j; NEXT CUT preview appears. Preview alone changes nothing. Explicit FILE_COMMIT increments exactly +1. TEST again eventually opens.

Fresh-player failure mode: player attempts to drag/file continuously. Input mapping ignores drag authority; UI teaches one discrete commit.

PASS.

## D02 — Too Far
Pre-cut authored vector creates TOO_DEEP at one column.
Player tries FILE on same column: it may deepen further if not max, but tutorial text correctly states this cannot repair this fit. Player uses Undo if their own cut created the state, or Restart if authored start is intentionally diagnostic. No hidden repair verb appears.

PASS, with content authoring warning: the tutorial must distinguish an authored pre-cut state from a player-created overcut so Undo semantics are not falsely implied. If the case starts already overcut, Restart cannot repair it either; therefore D02 should create the overcut through a safe instructed player action or provide another still-solvable blank. Content validation must reject an authored start that teaches `Restart fixes TOO_DEEP` when restart restores the same overcut.

**Repair disposition:** content-specific implementation gate; no global rule change required.

## D03 — Two Locks
Same persistent key remains selected when player changes lock. Test result on Lock B is based on current key vector, not stored snapshot from A. If A was opened earlier, A stays OPENED even if key later changes.

PASS.

## D04 — Shared Scar
Player can solve using two blanks, but using the same key gives `ONE KEY — TWO OPENS` payoff. No progression depends on discovering optimality.

PASS.

## D05 — Margin
Player reaches a state that already overlaps both locks, previews a tempting deeper cut, then chooses TEST on other lock instead. Preview does not enter history. If player commits the bad cut, Undo is exact and non-punitive.

PASS.

## D06 — Siblings
Three locks/two blanks. One shared pair + specialist. The player may perform wasteful repeated TESTs; no new information appears after exact repeats. History still records actions so Undo behavior matches what player did (R1).

Final TEST opens last required lock → `ATTEMPT_SOLVED`, solved review. Demo CTA appears only after player commits/continues from solved review. Demo completion flag becomes durable once leave-review commit occurs.

PASS after R1/R2.

## Demo transfer
Player buys full game, imports demo. Import recognizes D01–D06/tutorial-understood + compatible settings. Running import twice produces no duplicate state. Full campaign offers C01 or tutorial-recognition path according to Phase 7; no current D06 PuzzleState is transplanted into C-cases.

PASS after R7.

---

# 4. C01–C06 tutorial campaign simulation

## C01
Naive player repeats TEST three times before filing.
- same result every time;
- first TEST adds observations;
- repeats add history records only;
- hint tier/tutorial progression does not advance from repetition;
- Undo once removes only most recent repeated TEST, leaving equivalent visible knowledge from earlier TEST.

PASS after R1.

## C02
Failure at column 4 records accepted-at-current-depth facts for columns 1–3. Ledger distinguishes OBSERVED from UNKNOWN. Player need not retest each prefix column.

PASS.

## C03
TOO_DEEP must be staged so the lesson is recoverable. If authored pre-cut causes TOO_DEEP, the case needs another legal route; if the tutorial expects Undo, the player must first perform the overcut themselves. This is a concrete content authoring requirement for C03/D02.

**Phase-10 attack target:** verify actual C03 blueprint before freeze; content architecture title alone is insufficient to prove recoverability.

## C04
Two trivial locks teach selection and opened persistence. Reopening A with another blank may add accepted observations but cannot duplicate open effects.

PASS.

## C05
Player specializes two blanks unnecessarily. Still solves. No hidden score shame. After solve, mastery is not shown until ordinary completion commit.

PASS.

## C06
Player greedily deepens key and proves state UNSOLVABLE. Runtime checker returns UNSOLVABLE after exact state/version. Banner offers Undo/Restart/Keep experimenting. Player Undoes and tests second lock first, then opens both.

PASS after R6.

---

# 5. C07–C12 partition / diagnostic simulation

## C07 Pair + Specialist
Player uses one blank for current lock, second for next lock, then realizes third lock cannot be covered. Because Undo is unlimited, player backs out to partition earlier. No real-world-time punishment.

PASS.

## C08 Wrong Partition
Cheap policy `finish current lock first` reaches a valid local solution but destroys global completion. Softlock checker may prove UNSOLVABLE only after destructive FILE; if it returns UNKNOWN, no warning appears. Hint must not know hidden accepted sets beyond current observations.

PASS.

## C09 Cross-Pair
Two non-obvious pairings. Solver must validate at least one information-respecting route; omniscient existence alone is insufficient.

PASS subject to Phase-5 V3 validator.

## C10 Probe First
Player specializes probe early. This should remain solvable only if case intended as forgiving; otherwise softlock + Undo protects time. Main educational insight must emerge from observable differences, not unseen target sets.

PASS subject to information-respecting validator.

## C11 Strong Mark Trap
STRONG communicates nearest accepted deeper value is >=2 steps away, not exact target. A player treating STRONG as `cut twice` must be punishable through overlap loss, but presentation cannot imply exact numeric recommendation.

PASS.

## C12 Diagnostic Life
One blank stays non-opening through multiple tests. Repeated tests on unchanged vectors are pruned by solver but retained in human history. After information role is exhausted, conversion is ordinary FILE sequence.

PASS.

---

# 6. C13–C19 master branches / wear simulation

## C13 Two Ways Fit
Accepted set at a column has two disjoint intervals. Player discovers a valid depth through normal TEST/open evidence; no full hidden accepted set is automatically revealed. Presentation may teach concept with visible band metaphor only to the extent logically established.

PASS with one UX caution: cutaway art must not accidentally draw both exact hidden branch intervals before the player has evidence. `Two valid bands exist` can be tutorial knowledge; their undiscovered exact positions cannot leak.

## C14 Between
Current depth lies between branches. TEST returns BETWEEN_BRANCHES. Later columns stay unevaluated. Player sees split-band semantic icon, not exact branch coordinates.

PASS.

## C15 Branch Sharing
Player chooses shallow-compatible branch to preserve B rather than deepen for C. No new mechanic.

PASS.

## C16 Branch Partition
Two branch columns, 4 locks/2 blanks. Max branch ceiling respected. Need validator to ensure no cheap `always shallow` solve.

PASS subject to V5.

## C17 Wide Enough
Broad tolerance is finite accepted set. Player does not need to target a fictional center. Numeric accessibility labels still show key depth only, not tolerance endpoints unless observed/deduced.

PASS.

## C18 Wear Bridge
Broad lock acts as overlap bridge. Repeated testing does not widen it. No dynamic wear.

PASS.

## C19 False Precision
Player repeatedly files toward imagined center and can make state worse. Product promise remains fair because rules never claimed a center.

PASS.

---

# 7. C20–C26 access-order / diagnostic conversion simulation

## C20 Behind A
B is visible from start but marked AFTER A. TEST B is disabled with explicit reason. Opening A changes opened bit and derived accessibility in same successful TEST action. Undo of that TEST restores A closed and B inaccessible (R5).

PASS after R5.

## C21 Any Door
AFTER_ANY(A,B) supports two discovery orders. Access state is derived, not separately mutable. Undo sequence cannot leave a lock accessible without its prerequisite because dependent actions are later in history and unwind first.

PASS.

## C22 Order Debt
Opening obvious lock first remains solvable but costs specialization. This is important: access order should sometimes change efficiency without always becoming a binary softlock, otherwise player experiences gates as arbitrary traps.

PASS.

## C23 Probe Pair
The same blank tests two locks and distinguishes families through first blockers. Later untested columns never appear in ledger.

PASS.

## C24 Delay Completion
Opening current lock immediately via deeper edit removes probe utility. Since OPEN persists once achieved, later filing cannot revoke completion. Puzzle remains about future blanks/locks, not maintaining simultaneous coverage.

PASS.

## C25 Convert the Probe
Probe is converted after information exhausted. Mastery statistics count actual FILE/TEST history, not solver-inferred intent.

PASS.

## C26 Symmetry Break
Two blanks have equal vectors but different observation histories.
- Fit result against any lock is identical for equal vectors.
- Player-facing ledger/history differs by blank identity.
- Omniscient solver may symmetry-collapse for future solvability.
- Information-respecting solver/hints cannot collapse unless knowledge permutation is equivalent.
- Save/load preserves stable blank identity/rack label.

PASS after R11.

---

# 8. C27–C32 late synthesis / maximum normal state

## C27 Branch + Wear
One disjoint accepted set + broad tolerance interact without extra UI grammar. Knowledge panel may become dense but remains bounded at <=3 blanks/<=6 locks/<=6 columns.

PASS.

## C28 Access + Partition
5 locks/3 blanks. Bench overview must show all known locks and access badges without requiring camera walking. Ledger may scroll; physical selected pair remains primary.

PASS.

## C29 Three Policies Fail
Deepest-first, shallowest-only, finish-current all fail. Solver regression must explicitly run P1/P2/P3 against case data.

PASS subject to authored case validation.

## C30 Information Budget Without Currency
Tests are free. If exhaustive testing with every blank against every accessible lock trivially reveals enough information without destructive tradeoff, the case fails its own content premise. Validator/content review must ensure information order matters because access and persistent vector state matter, not because tests cost currency.

PASS as a content gate, not automatic property.

## C31 Workshop Job
5 locks/3 blanks/6 columns. Access + wear + branch + conversion. UI ceiling fits.

PASS.

## C32 Locksmith's Margin
Maximum normal state: 3 blanks, 6 required locks, 6 columns, <=2 branch columns, access depth <=3. Simulated paths:
- intended shared imperfect key + probe + specialist;
- alternate valid partition with different early TEST order;
- greedy deepest-first softlocks;
- high-testing conservative path solves more slowly but without hidden punishment.

UI at 1280×800:
- overview shows 3 stable key slots + 6 lock rail positions;
- labels may abbreviate visually but full localized names/access predicates accessible on focus;
- ledger is scrollable, not microscopic;
- numeric labels optional;
- inspection zoom keeps 6 columns readable.

PASS after R10.

---

# 9. Solved review / replay / mastery / achievements

## Solved review transaction
Last required OPEN enters pending solved review, not permanent campaign commit. Player can:
- inspect final key vectors/history;
- Undo final TEST and return to unsolved attempt;
- Redo it and return to solved review;
- Continue/Return to Case Select to commit solved attempt.

After commit:
- solved case ID/unlock graph update once;
- eligible first-solve achievement event queues once;
- best mastery/stats compare idempotently;
- replay starts a new attempt and cannot erase prior campaign solve.

PASS after R2.

## Alternate partition
A materially different partition counts only if validator defines partition signature. Replaying with same partition but different redundant TEST order does not fake alternate-partition mastery.

PASS.

## Achievement reconciliation
Steam unavailable at commit: local achievement event remains pending. Steam returns later: adapter reconciles and grants once. Repeated reconciliation cannot duplicate counters/unlocks.

PASS.

---

# 10. Persistence / crash / corruption simulation

## Save after FILE
Domain commits FILE +1 and ActionRecord. Autosave candidate represents whole new boundary. Crash during filing animation reloads the fully cut state; animation may be skipped/replayed cosmetically. No half-depth exists.

PASS after R3.

## Save after failed TEST
Knowledge observations + TEST history are one domain transition. Crash during bind animation reloads complete knowledge boundary, never accepted-prefix without blocker or vice versa.

PASS.

## Save after successful TEST/open/access
Opened bit + observations + derived access changes are one nested transition. Crash cannot reopen A without also exposing B if B depends on A.

PASS.

## Crash in solved review
Before leave-review commit: reload solved pending attempt and review. Player can still Undo.
After commit: reload case as committed solved campaign; replay is separate attempt.
During commit: idempotent transaction yields pending or committed, never partial.

PASS after R2.

## Corrupted primary save
Loader validates primary; on failure tries known-good backup. Settings namespace failure does not damage progress. If both profile copies fail, preserve bad files for diagnostics where practical and offer fresh profile rather than crash loop.

PASS.

## Stale case content
Saved attempt signature differs from shipped case. Explicit migration if available; otherwise preserve committed campaign state but restart only incompatible attempt with explanation. Never replay old actions against changed accepted sets.

PASS after R9.

## Long Undo/Redo
Full case history is small enough to retain complete attempt. Undo to start, Redo to end produces identical PuzzleState/Knowledge/opened bits. New action after Undo clears redo tail. Saving/reloading mid-branch preserves current timeline + redo semantics only if format explicitly supports it; otherwise redo tail may be intentionally non-persistent only if UX documents this before freeze. Preferred design requirement: **persist redo tail for exact session continuity** because state size is small.

**New empirical/technical gate:** verify persisted redo-tail format or explicitly downgrade requirement before Phase 11; no silent loss should remain ambiguous.

---

# 11. Platform failure / Cloud / demo import simulation

## Steam unavailable
Launch offline; Achievements/Cloud unavailable badge optional but not blocking. Local saves complete. No puzzle rule changes.

PASS.

## Delayed achievement
Complete C06 offline → commit locally → event pending. Reconnect → reconcile exact event key → grant once. Reconnect again no duplicate.

PASS.

## Cloud conflict
Device A has more committed cases + in-progress C20. Device B has older campaign but different current attempt. Safe monotonic merge may combine solved-case facts if schema and profile match, but current attempt must be chosen as a whole branch. If automatic choice cannot prove safety, show conflict chooser.

PASS after R8.

## Demo import twice
Same outcome after first and second import. Newer full progress never regresses.

PASS after R7.

---

# 12. Input / Deck / accessibility / localization simulation

## Keyboard+mouse
All core actions reachable without drag or hold. Explicit cut commit prevents accidental hover/click mutation.

PASS.

## Controller hot-swap
Player is in ledger on controller, touches mouse, then controller again. Semantic focus remains deterministic; prompt family changes only. No duplicate command from device transition.

PASS.

## Rapid controller repeat
Holding/rapid tapping FILE_COMMIT must not create two cuts from one accepted semantic command. Each +1 requires distinct accepted commit. Animation cannot be authority.

PASS after R4.

## Steam Deck 1280x800
Maximum case uses focus/zoom and scrollable ledger; physical columns never reduced below readable geometry. UI scale increase may reduce simultaneous rows but not hide functionality.

PASS after R10.

## Reduced Motion
Camera cuts/short transitions; TEST can snap directly through accepted prefix to blocker final state. Same observations.

PASS.

## High Contrast
Shapes/outlines duplicate color; later unevaluated columns stay neutral.

PASS.

## Numeric labels
Shows key depths 0..D only. Does not expose lock accepted sets.

PASS.

## Localization expansion
Access badge `AFTER ALL A + B` must support wrapped/expanded text and full tooltip/focus detail. Critical rule text not baked in textures. Long locale cannot force unreadably small font; layout scrolls/reflows.

PASS.

---

# 13. Softlock / hint simulation

## SOLVABLE
Background solver finds completion. No banner. Hint uses information-respecting path only.

## UNSOLVABLE
Proof matches exact current state/version. Warning may appear. No exact mistake is revealed automatically. Undo changes state and invalidates stale warning.

## UNKNOWN
Timeout. No warning. Hint cannot pretend proof exists.

## Stale result
Player FILEs again before solver callback. Callback version mismatch → discard.

PASS after R6.

## Hint request with hidden information
Omniscient solver knows a particular cut is globally optimal; player has insufficient observations. Hint may ask to test a safe accessible lock or recall known overlap, but cannot expose hidden accepted set.

PASS.

---

# 14. Hostile behavior simulation

## Max-depth spam
FILE at D is no-op, no history/progress farming. Neutral MAX DEPTH feedback.

PASS.

## Inaccessible TEST spam
No authoritative TEST history, no knowledge, no hint progression. UI repeats explicit prerequisite.

PASS.

## Identical TEST spam
Creates history entries but zero new puzzle/progression state. History can be fast-forwarded/collapsed visually while Undo remains exact.

PASS after R1.

## Rapid Undo/Redo
Commands serialize against semantic action index. Presentation snaps safely. No stale solver warning survives version change.

PASS after R4/R6.

## New action after Undo
Redo tail clears deterministically. Save reflects new branch.

PASS.

## Repeated solve/replay
First campaign solve/unlock is idempotent. Better mastery may update best stats; achievements do not duplicate. Replay attempt independent.

PASS.

## Quit during FILE/TEST animation
Reload latest committed authoritative boundary, not animation progress.

PASS after R3.

## Quit during solved commit
Pending-or-committed atomic outcome; no half progression.

PASS after R2.

---

# 15. Contradictions found and disposition

### C-01 Repeated identical TEST
Phase 4 wording conflicted with Phase 8 history requirements.
**Repaired by R1.**

### C-02 Solved-state Undo vs permanent campaign progression
Immediate permanent completion would contradict exact Undo from solved review.
**Repaired by R2.**

### C-03 Animation crash boundary under-specified
Domain authority was clear but durability/presentation restart needed an explicit contract.
**Repaired by R3/R4.**

### C-04 Access effects under Undo needed nesting clarity
**Repaired by R5.**

### C-05 Background softlock result staleness
Proof correctness existed, but callback/state version binding was not explicit enough.
**Repaired by R6.**

### C-06 Demo repeated import / divergent Cloud branches
Idempotency existed conceptually; merge boundary needed stronger attempt-vs-campaign semantics.
**Repaired by R7/R8.**

### C-07 Changed case content vs persisted action history
Mismatch detection existed but recovery needed a no-reinterpretation rule.
**Repaired by R9.**

### C-08 Accessibility/numeric labels hidden-information leakage risk
**Repaired by R10.**

### C-09 C26 equal-vector blanks
Solver symmetry and player knowledge needed explicit cross-layer rule.
**Repaired by R11.**

### C-10 D02/C03 TOO_DEEP tutorial recoverability
Potential content contradiction if authored initial overcut is paired with a lesson suggesting Restart repairs it.
**Not a global mechanic repair. Phase 10 must attack concrete D02/C03 authored blueprints and Phase 11 must require a recoverable staging.**

### C-11 Persisted Redo tail
Complete-case history is frozen, but whether redo tail survives app restart is not explicit enough.
**Remaining specification choice/gate for Phase 10:** preferred YES; if NO, must be intentional and clearly communicated before freeze.

---

# 16. Phase-9 regression checklist

WG01 first boot works without Steam.
WG02 settings save independently of campaign.
WG03 controller hot-swap preserves semantic focus.
WG04 C01 failed TEST reveals only prefix + first blocker.
WG05 FILE preview changes no authority/history.
WG06 each FILE commit changes exactly one column +1.
WG07 crash during FILE reloads whole committed cut.
WG08 crash during failed TEST reloads whole knowledge transition.
WG09 identical TEST adds history but no knowledge/progression.
WG10 Undo identical TEST leaves equivalent puzzle knowledge when earlier identical observation remains.
WG11 inaccessible TEST adds no history.
WG12 opened lock remains completed after its key is later filed.
WG13 Undo first successful OPEN restores prior access state.
WG14 later access-dependent actions unwind before their enabling OPEN.
WG15 Redo replays exact stored transition.
WG16 new authoritative action after Undo clears redo.
WG17 max-depth FILE is no-op.
WG18 softlock UNSOLVABLE must match exact state version.
WG19 stale softlock callback is discarded.
WG20 UNKNOWN never warns.
WG21 hints never expose hidden accepted sets.
WG22 equal-vector/different-history blanks fit equally but retain distinct ledger history.
WG23 omniscient solver symmetry cannot leak into player hints.
WG24 BETWEEN_BRANCHES reveals relation only, not full branches.
WG25 wear never changes through repeated TEST.
WG26 access predicates are visible before dependent cuts.
WG27 maximum 3-key/6-lock/6-column state fits bench/inspection UX.
WG28 reduced motion produces identical authority/information.
WG29 numeric labels reveal key depth only.
WG30 high contrast does not expose later unevaluated columns.
WG31 localized long access text remains operable without tiny font.
WG32 final lock OPEN enters pending solved review.
WG33 Undo from pending solved review can restore unsolved attempt.
WG34 Continue/Case Select commits solve exactly once.
WG35 crash before solved commit restores pending review.
WG36 crash during solved commit cannot produce partial progression.
WG37 offline solve queues achievement event locally.
WG38 achievement reconciliation is idempotent.
WG39 repeated replay cannot duplicate first-solve unlocks.
WG40 alternate partition badge requires structural partition signature.
WG41 demo import once and twice produce identical full state.
WG42 demo import never overwrites newer full progress.
WG43 Cloud merge never interleaves two current-attempt histories.
WG44 stale case content never replays old actions against new accepted sets without tested migration.
WG45 corrupt primary save attempts backup recovery.
WG46 corrupt settings cannot corrupt campaign.
WG47 C03/D02 TOO_DEEP staging is recoverable and pedagogically truthful.
WG48 C06 product hook occurs without hint requirement.
WG49 C12 diagnostic blank can remain intentionally non-opening.
WG50 C14 gap feedback is visually distinct from shallow/deep.
WG51 C18 broad tolerance is static.
WG52 C20 access change is nested in successful TEST.
WG53 C26 blank IDs/rack positions survive save/load.
WG54 C29 defeats required cheap policies.
WG55 C30 strategic dilemma does not come from paid/costly tests.
WG56 C32 has at least two strategically distinct valid solution traces.
WG57 rapid FILE_COMMIT cannot duplicate cut without separate accepted commands.
WG58 rapid Undo/Redo cannot display stale domain state as current.
WG59 quit/pause forces or waits for safe local durability boundary where practical.
WG60 platform Cloud is never the sole save authority.
WG61 all demo/campaign cases pass omniscient solvability.
WG62 all required cases pass information-respecting fairness.
WG63 no main case requires new verb after demo.
WG64 no mastery/achievement disables accessibility or hints.
WG65 no hidden real-lock realism exception appears.
WG66 no continuous geometry decides fit.
WG67 full current-attempt action list remains within practical save budget.
WG68 redo-tail persistence choice is explicitly frozen before implementation handoff.
WG69 Phase-9 repairs are merged/normalized at Phase 11.
WG70 final authority chain leaves no contradictory solve/commit semantics.

---

# 17. Remaining empirical gates

Paper simulation cannot prove:
- tactile satisfaction of discrete one-step filing;
- whether first-blocker feedback is understood quickly without over-UI;
- whether 6-column cutaway remains instantly readable on Steam Deck hardware;
- whether mature cases truly resist cheap policies while staying fair to fresh humans;
- C01–C32 actual difficulty/abandonment curve;
- D01–D06 20–30 minute target and >=80% hook comprehension;
- whether the store/trailer looks like lockpicking/burglary despite no pick tools;
- exact softlock solver runtime budgets on target hardware;
- final localization language set and release price.

These are implementation/playtest empirical gates, not unresolved gameplay rules.

---

# 18. Phase-9 verdict

**PHASE 9 COMPLETE WITH REPAIRS.**

The whole game is mechanically coherent after R1–R11. No new gameplay primitive was required. Two explicit specification attacks remain for Phase 10:
1. D02/C03 TOO_DEEP tutorial staging must be proven recoverable and non-misleading;
2. persisted Redo-tail semantics must be either required or deliberately rejected before freeze.

Phase 10 should now attack fun/repetition, solver-cheapness, scope, UX ambiguity, content exhaustion, save corruption, transaction races, platform failure, accessibility and implementation ambiguity using the repaired authority chain.