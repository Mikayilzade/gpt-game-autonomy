# GAME #013 — PHASE 9 WHOLE-GAME SIMULATION ON PAPER

Date: 2026-09-02
Status: PHASE 9 COMPLETE — PASS WITH REPAIRS / PHASE 10 READY
Selected concept: **SEAL BREAK** (working title)

Authority: this file is a Phase-9 integration authority. Phase 4 remains authoritative for mechanics, Phase 5 for content/campaign, Phase 6 for UX, Phase 7 for commercial packaging, and Phase 8 for technical contracts except where this file explicitly records a Phase-9 repair/clarification required to resolve a cross-file contradiction.

## 1. Simulation method
This pass treats the product as if a hostile but reasonable player is using a near-release build. It walks the entire state machine and content dependency graph rather than retelling the intended design. Every transition is checked for: player knowledge, legal inputs, oracle leakage, deterministic ownership, persistence, recoverability, controller focus, progression truth, demo/full identity, and content-version behavior.

The pass covers:
- first boot and first wrong answer;
- first hour across witness comparison and omission;
- Acts III–VI and both the 24-case floor and 30-case target;
- demo -> full import including a mechanically modified demo wrapper;
- repeated wrong submissions, all hint steps, alternate certified solutions, replay/reset/long-absence return;
- controller-only 1280x800 at 200% text and device switching;
- corruption/backup/future-save/Cloud/Dynamic Cloud Sync cases;
- rapid/hostile inputs, pause/skip, repeated import, content change, stale certification and localization failure.

No production implementation is started.

---

# 2. Cross-file defects found and Phase-9 repairs

## Repair P9-01 — content introduction schedule off by one act
A real contradiction exists inside Phase 5: its abstract introduction schedule says Cases 17–20 introduce `ARRANGE_REQUIRED_SET` history reconstruction and Cases 21–24 introduce genuine placement+history coupling, while the concrete canonical campaign and dependency graph place first free reconstruction at **SB_21** and first coupled family at **SB_26**. The concrete case map is more specific and is consistent with Phase 6 onboarding and the dependency graph.

**Phase-9 authority repair:** until Phase 5 is textually normalized, read its introduction schedule as:
- SB_16–SB_19: player witness placement under fixed/highly constrained history;
- SB_21–SB_24: history reconstruction, including first `ARRANGE_REQUIRED_SET` at SB_21;
- SB_26–SB_29: genuine coupled seal selection + history choice/arrangement;
- optional fifth beats SB_20/SB_25/SB_30 remain target extensions and may combine already-taught vocabulary but may not introduce a new mode required by the floor.

The concrete case definitions and dependency graph win over the stale generic range labels. This repair removes the only tutorial-order contradiction discovered in the paper run.

## Repair P9-02 — 24-case floor identity must never be inferred from numeric range
Phase 5 contains an explanatory sentence that momentarily calls “01–24” the floor before immediately correcting to four core cases per act. This is dangerous for implementation because the true floor excludes each act's fifth extension.

**Phase-9 authority repair:** the canonical 24-case floor set is exactly:
`SB_01–SB_04, SB_06–SB_09, SB_11–SB_14, SB_16–SB_19, SB_21–SB_24, SB_26–SB_29`.

Never derive floor membership from `campaign_position <= 24`. The authoritative field is `required_for_floor`; progression/achievements/ending must use that field and explicit prerequisites. Cases `SB_05, SB_10, SB_15, SB_20, SB_25, SB_30` are the six target extensions when the 30-case configuration ships.

## Repair P9-03 — committed reveal ownership during external save reload
Phase 8 already says Dynamic Cloud Sync must not mutate an active committed trace, but the state-machine consequence needs to be explicit.

**Phase-9 authority repair:** if external/Cloud state arrives during `COMMIT_VALIDATE`, `RUN_RESOLVE`, `RUN_REVEAL`, `RUN_REPLAY`, or a result screen retaining a trace, queue it as `pending_external_profile`. Do not merge or reload gameplay/profile-derived case state until the player reaches a safe boundary (`CASE_EDIT` after returning from the committed run, `CASE_SELECT`, or menu). The committed snapshot and trace remain authoritative for that run. If a later merge changes whether the case is already solved, that affects progression display after the safe-boundary merge, not the trace just watched.

## Repair P9-04 — changed case content and saved solve facts
A solved case ID alone is insufficient if mechanics change after release. Demo import already uses mechanics/acceptance compatibility; ordinary saved campaign progress needs the same principle.

**Phase-9 authority repair:** each persisted solved fact must retain the `mechanics_hash` and rules/acceptance compatibility identifier under which it was earned. On load after content update:
- same mechanics/acceptance contract: keep solved status;
- presentation/localization-only revision: keep solved status;
- mechanics/acceptance changed: do not silently assert the new case solved. Preserve the historical completion record, mark current revision `REVALIDATION_REQUIRED`, and recompute unlocks conservatively according to shipped migration policy;
- a release patch that intentionally grandfather-solves a changed case must do so via an explicit tested migration table, not by matching `case_id` alone.

This aligns normal saves with the already-frozen demo-import safety rule.

These four repairs are integration clarifications, not new mechanics.

---

# 3. First boot -> SB_01 minute-by-minute hostile simulation

## 3.1 Boot/profile
Player launches with controller connected and Steam unavailable. `BOOT -> LOAD_PROFILE` succeeds because Steam is optional. No profile exists, so application creates a local profile only after choosing/accepting default settings. Title is fully navigable by controller and keyboard.

First-run accessibility setup may offer text scale, motion and contrast, but must not block entry behind a long wizard. Defaults remain playable; all options stay reachable later.

Player chooses New/Continue -> Case Select. Only SB_01 is available; optional later demo entries are not exposed in full campaign progression.

## 3.2 SB_01 loading and first inspection
`CASE_LOADING` validates case schema/rules/hash and enters `CASE_EDIT`. Workbench shows two labeled compartments and one fixed seal. Plan rail shows fixed history; Evidence rail shows target. Top strip states structural objective.

Expected first 60–90 seconds:
1. focus starts on a meaningful Workbench object, not an empty panel;
2. player focuses the seal -> covered seam(s) highlight;
3. player focuses each compartment -> traversed seam(s) highlight;
4. tutorial text explains only immutable geometry and tear rule;
5. Commit is available because there is nothing structurally incomplete.

No live target card turns green/red while inspecting. This confirms oracle boundary.

## 3.3 First commit and deliberate wrong expectation
SB_01 itself may not allow a mechanically wrong submission if all inputs are fixed; therefore tutorial must frame the task as prediction/reading, not pretend the player made a choice. The first genuine wrong-answer loop occurs at SB_04 or the first editable case unless an earlier case has authored history choice.

Commit freezes snapshot, resolver completes immediately, reveal animates checkpoint 1 and 2. If two visual tear subanimations occur, same-checkpoint atomicity remains clear via shared checkpoint badge. Result screen uses the already-resolved trace.

Replay reproduces identical trace hash. Return to edit restores semantic focus.

**Verdict:** first boot path is coherent. Important expectation: do not market SB_01 as “solve by placement” when it is a reading/tutorial beat.

---

# 4. First wrong submission / replay / return-to-edit cycle

Use SB_04, the first authored-history-choice case.

1. Player inspects two overlapping fixed witnesses and target evidence.
2. Plan rail shows three authored histories with no predicted tear signatures.
3. Player selects Plan B and commits.
4. Resolver returns mismatch.
5. Reveal shows actual tears checkpoint-by-checkpoint.
6. Mismatch summary says, for example, target witness S breaks at 2; observed S broke at 1 when compartment C opened. This is retrospective and legal.
7. Player scrubs checkpoint 0->1->2 and sees only committed trace.
8. Player presses Return to Edit; exact Plan B selection is restored, not default Plan A.
9. Undo returns to the previous authored history selection if one exists; no tear state remains.
10. Player selects Plan C and commits again.

Repeated wrong commits do not consume resource, alter target, auto-open hints, or leak closeness. The player can fail 50 times with identical semantics.

**Pass condition:** mismatch causality must reference observed trace only; “try C first” language is forbidden outside requested authored hints.

---

# 5. First-hour progression simulation

A plausible first-hour route is SB_01 -> 02 -> 03 -> 04, then either optional SB_05 if present or SB_06, with SB_11 reachable later through its dependency path.

## SB_01
Learns direct crossing. No free input burden.

## SB_02
One witness has multiple trigger compartments. Replay/scrub teaches first qualifying opening. No new editing grammar.

## SB_03
Multiple witnesses can break at one checkpoint. One-time help copy explicitly states tear-animation order has no meaning. This prevents the player from learning a false sub-order rule.

## SB_04
First small history choice. New input grammar arrives after tear semantics are stable.

## SB_06
Paired witness discrimination introduces comparison evidence. Player can cross-highlight witness/socket/trigger geometry without running a hypothetical solver.

## SB_07–09
Intersection then relative temporal bounds deepen same vocabulary. `INTACT_THROUGH` is introduced before omission becomes structurally important.

## SB_11
`Open 3 / Leave 1 closed` layout is explicit. The user is not asked to infer the number of omitted compartments from evidence.

**Dependency verdict:** after P9-01 correction, no predicate or input mode is required before its onboarding beat. The first hour can remain comprehension-heavy without presenting placement and free permutation simultaneously.

---

# 6. Act III survivorship simulation

SB_11 establishes one omitted compartment. If a final-intact witness is triggered by one compartment, its survival can identify the omitted compartment.

SB_12 checks impossibility: a multi-trigger witness whose full trigger set cannot all fit into the single omission cannot remain intact. This must be presented as a reasoning contradiction, not as live disabled histories; every structurally legal history remains selectable.

SB_13 uses `INTACT_THROUGH(S,3)` then eventual break. Player must understand “through 3” inclusively means intact after checkpoint 3. Evidence grammar already states this.

SB_14 combines survivor + divergent witness. At least one clue should still be human-invertible; certification uniqueness alone is insufficient.

Optional SB_15 is admissible only if human review proves the player can eliminate omission classes without enumerating all six candidates. If that review fails, cut it; floor remains intact.

No mechanical contradiction found.

---

# 7. Act IV witness-placement simulation

SB_16 is first editable-seal case under fixed history. Exact-K budget means the player cannot commit with too few/many seals. The disabled Commit explanation may say `Install 1 more seal`; it may not say which socket.

SB_17 demonstrates two sockets with same final broken state but different break time. This is important anti-set-cover teaching and one of the demo beats.

SB_18 asks player to build overlapping witnesses. Static trigger highlighting remains legal because it exposes immutable geometry, not current-plan result.

SB_19 combines placement with known omission/survival, still without free history reconstruction. This proves placement mastery before Act V.

Optional SB_20 may be denser but cannot be the first occurrence of a required rule.

**Pass:** fixed history keeps search surface conceptually inverse-witness rather than simultaneous CSP.

---

# 8. Act V reconstruction simulation

SB_21 is the first free `ARRANGE_REQUIRED_SET` reconstruction and is therefore the canonical introduction point after P9-01. Fixed seals ensure the only new manipulation is ordering.

Controller sequence:
- focus history card;
- enter MOVE;
- ordinal positions become explicit;
- move left/right/up/down;
- confirm one transaction; cancel restores previous order.

No tear prediction is shown during reorder.

SB_22–24 add delayed break, overlap and survivor interactions. By SB_24 the player combines at least three reasoning classes but still edits only history, not placement.

Optional SB_25 may capstone Act V but cannot gate Act VI floor unless its explicit prerequisite is intentionally target-only; floor graph must never require a non-floor extension.

No contradiction found in concrete dependency graph.

---

# 9. Act VI coupled simulation

SB_26 introduces coupling safely with choose-2-of-6 sockets plus one of four authored histories, not unrestricted permutation. This is the correct first combined beat.

SB_27–29 may progressively move toward arranged history only after player has independently mastered placement (Act IV) and reconstruction (Act V). Each must retain at least three human deduction eliminations before residual trial.

A hostile player can brute-force by committing many combinations because the game imposes no penalty. The design deliberately does not prevent this with lives/timers/live scoring. Anti-bruteforce responsibility therefore belongs to authored state-space readability and human-review gates, not punitive UX.

**Important acceptance rule:** repeated commits must not progressively reveal a hidden closeness metric through mismatch ordering. Mismatch list remains authored target order, not “closest error first.”

SB_29 is the 24-case floor culmination. If the 30-case target ships, SB_30 is optional mastery extension, not required for Campaign Complete.

---

# 10. 24-case vs 30-case product simulation

## 24-case configuration
Shipping content contains the exact floor set from P9-02. Case Select shows six acts with four cases each; there are no visible empty fifth slots. Commercial copy says 24 cases. Each act core completion unlocks the next act using explicit prerequisites/`required_for_floor` facts.

Completion semantics:
- Campaign Complete = all 24 floor cases;
- Full Casebook Complete = all shipping cases, also 24;
- “Six Acts Mastered” achievement is absent/reworded because no fifth beats ship.

## 30-case configuration
Each act has four floor cases plus one optional fifth extension. Solving the four floor cases unlocks next act. Fifth beat can remain available for mastery. Campaign Complete still occurs after 24 floor cases; Full Casebook requires 30.

A player can finish the story/product spine while leaving fifth beats unsolved, then return.

**Pass:** after P9-02, progression and achievements are truthful in both configurations.

---

# 11. Demo -> full simulation

Canonical demo beats:
1. SB_01;
2. SB_02;
3. SB_06;
4. SB_11;
5. SB_17;
6. a coupled late-loop beat based on certified SB_24/SB_26/SB_29 lineage.

The demo is a curated graph, not full campaign unlocking. Tutorial wrappers may inject explanation, but they may not change Domain mechanics under the same campaign case ID.

## Identical campaign case
Demo solves SB_01 with same mechanics hash/rules/acceptance contract. Full install imports solved fact idempotently. Campaign unlock state is recomputed from imported solved IDs rather than copied blindly. Re-running import creates no duplicate progression event/achievement spam.

## Mechanically modified wrapper
Suppose demo beat 6 is a reduced sibling derived from SB_26. It must have a distinct case ID or a distinct acceptance/mechanics identity. Solving it does **not** mark campaign SB_26 solved. Full import can preserve “demo coupled beat completed” as demo history and copy settings, but not campaign completion.

## Full game already newer
If full profile already solved SB_01, later demo import cannot downgrade hint state, settings generations, completion timestamp semantics, or achievements. Monotonic union wins where compatible.

**Pass:** carryover is truthful and idempotent.

---

# 12. Hints / alternate solutions / reset / long absence

## Three hint steps
Player explicitly opens hint panel.
1. Observation hint points at immutable relation.
2. Deduction hint explains a principle.
3. Nudge eliminates a class or names a constrained witness/compartment.

Hint state persists per case as maximum opened step. It never changes resolver success. A later solve is still a solve. Only a designated positive “without a nudge” achievement may require that hint panel was not opened for that case; no global shame badge.

## Alternate valid solution
For `MULTI_VALID_INTENTIONAL`, any satisfying certified solution succeeds. UI must not say “not the intended solution.” Replay stores the actual successful submission. If optional mastery UI later tracks discovered material solution classes, it uses certifier-declared equivalence, not raw permutation count.

## Reset run
Restarts same committed snapshot from checkpoint 0; no edit loss.

## Reset case
Returns to authored initial edit state after confirmation when progress exists. Solved status is not revoked; reset affects draft/current attempt only.

## Return after months
On case load, saved draft restores only if mechanics/content hash compatible. Otherwise player receives a concise `Case updated; previous draft cannot be restored` notice and starts from authored edit state. Historical solved fact follows P9-04 compatibility rules.

---

# 13. Controller-only handheld 1280x800 @ 200% text

At 200%, application automatically uses narrow drawer layout. Workbench retains minimum readable geometry; active Plan/Evidence rail overlays/reflows rather than shrinking cabinet indefinitely.

Test route performed conceptually:
- Case Select -> SB_11 -> Workbench -> Evidence -> Plan -> OPEN/LEFT CLOSED movement -> Commit -> reveal -> mismatch -> replay scrub -> return to edit -> pause/settings -> change text scale -> return.

Required focus behavior:
- rail open restores last object in that rail;
- closing rail returns to originating Workbench object;
- pause/help returns to prior semantic object;
- mismatch detail returns to selected evidence card;
- after Return to Edit, focus returns to last meaningful edit object;
- if object no longer exists after a legitimate edit/content reload, nearest same-group node then group default.

Device switching:
- controller -> keyboard -> mouse changes glyph family only;
- focus does not reset;
- switching during reveal cannot alter semantic trace;
- no hover-only data;
- drag is convenience only.

Reduced Motion + Instant:
- resolver already completed;
- presentation materializes checkpoint/final states with minimal animation;
- evidence timeline remains fully inspectable.

**Pass condition:** 200% QA must include long localized strings, not English-only layout.

---

# 14. Persistence, corruption and Cloud simulation

## Main save corrupt, backup valid
Load validates main -> fail; backup -> pass; preserve corrupt main as diagnostic/recovery artifact; restore backup and write fresh main with recovery marker. Player is informed non-alarmingly that backup was restored.

## Main + backup corrupt
Preserve both. Offer fresh profile. Do not silently delete files. If export/recovery path exists it is optional support tooling, not gameplay requirement.

## Future save schema
Older binary encountering a save with unsupported newer `save_schema_version` must not overwrite it. Enter a read-blocked/future-save gate: preserve file, explain that this version cannot open newer save, allow exit; starting a new local profile must use a separate file/slot and require explicit confirmation so the future save is retained.

## Union-safe Cloud merge
Compatible profiles merge monotonic solved case facts, achievements-derived facts and per-setting generation semantics. Never choose entire profile merely by newest timestamp.

If local solves A and Cloud solves B, merged profile solves A+B.

## Irreconcilable conflict
If same logical setting/draft has incompatible divergent generations or mechanics identity prevents safe merge, enter `SAVE_CONFLICT_GATE` with human-readable Local/Cloud metadata. Never expose raw hashes as the only explanation. The chosen resolution must be atomic and backed up.

## Dynamic Cloud Sync during CASE_EDIT
External profile is received. If merge does not invalidate current case draft, queue and apply at a safe edit boundary; if the same draft changed externally, offer conflict handling rather than silently replacing active edits.

## Dynamic Cloud Sync during committed reveal
Apply P9-03: queue only. Current immutable snapshot/trace finishes unchanged. Merge after Return to Edit/Case Select/menu.

**Pass:** persistence ownership is deterministic after P9-03/P9-04.

---

# 15. Hostile/unusual input simulation

## Empty/invalid structural submission
Commit disabled when exact-K/history bounds unmet. Focus reason says only structural deficiency. Keyboard shortcut to Commit obeys same gate.

## Rapid Commit spam
First accepted Commit transitions out of CASE_EDIT; further Commit events are ignored/debounced by state ownership. Only one snapshot/run/save event exists.

## Commit then Back in same frame
State transition is atomic. If Back arrives after commit ownership transferred, it follows reveal's allowed behavior (skip/abort to result or Return-to-Edit policy), never edits the frozen snapshot.

## Rapid Back/Skip during reveal
Skip materializes authoritative final trace once. Multiple inputs are idempotent. No duplicate solve event/achievement/write.

## Pause during reveal
Pause freezes presentation cursor only. Resolver trace already exists. Resume continues same presentation checkpoint; no second resolve.

## Quit during reveal
Progress is not awarded merely because resolver internally knows success unless product explicitly commits solve on successful resolution. Canonical safer rule: award/persist solved fact when success result is entered, not mid-animation. If application quits before result transition, case can be replayed; no contradiction or loss of prior profile progress.

## Repeated demo import
Import ledger + monotonic merge makes all repeats no-ops after first compatible import.

## Deleted/changed case content
Missing shipping case on release build is content error; development may enter FATAL_CONTENT_ERROR with case ID. Changed mechanics invalidates drafts/replays and applies P9-04 to solves.

## Achievement idempotency
Achievements are derived/queued from monotonic facts. Calling platform unlock repeatedly is safe; local profile marks requested/confirmed state separately if needed. No toast spam on Cloud merge/import.

## Missing localization key
Development build shows conspicuous key/fallback marker and logs hard QA failure. Release certification rejects missing required key. It must never become empty evidence text that hides a predicate.

## Stale certification hash
Case mechanics hash/rules version not matching shipped certification report is a release-blocking content failure. Runtime may still resolve in development, but shipping pipeline fails. Never silently trust old certifier result.

## Same-checkpoint tear animation order
Rapid/skipped animation cannot imply ordering. All tears from one checkpoint carry identical checkpoint badge/state.

---

# 16. Whole-product repetition attack

The 30-case map remains credible because each act shifts the player-owned unknown:
- Act I: understand destructive witness semantics;
- Act II: infer from relationships among witnesses;
- Act III: reason from what did not happen;
- Act IV: construct the witness set under known history;
- Act V: reconstruct history under known witnesses;
- Act VI: couple both choices.

The largest repetition risk is not mechanical identity but evidence-card density in late cases. Therefore late content must preserve Phase-5 anti-repetition gates:
- three+ deduction classes, not three+ predicate cards;
- at least three human eliminations before residual search;
- target extensions cut if they become enumeration;
- no new predicate alphabet after coupled play begins.

Phase 10 should attack this again from fun/repetition and scope perspectives.

---

# 17. Empirical gates intentionally left for implementation/playtest
These are not unresolved design ambiguity:
1. exact first-solve times and whether SB_29 is demo-appropriate;
2. readability of seam/socket geometry at 1280x800 across real art;
3. late evidence-card density at 200% text in longest planned localization;
4. whether mismatch causal wording feels explanatory without feeling like an unwanted hint;
5. whether optional fifth cases materially add mastery rather than fatigue;
6. whether 30-case target or 24-case floor is the stronger release scope after external playtest.

Rules, ownership and fallback decisions for failures are already defined.

---

# 18. Phase-9 acceptance matrix

| Area | Result | Notes |
|---|---|---|
| First boot / profile | PASS | offline/Steam-absent safe |
| SB_01 onboarding | PASS | reading beat, not fake-choice puzzle |
| Wrong commit loop | PASS | retrospective mismatch only |
| First-hour dependencies | PASS after P9-01 | schedule normalized to concrete campaign |
| Act III survivorship | PASS | omission count explicit |
| Act IV placement | PASS | fixed history isolates new verb |
| Act V reconstruction | PASS after P9-01 | first free arrangement SB_21 |
| Act VI coupling | PASS | first combined beat SB_26 |
| 24/30 progression | PASS after P9-02 | `required_for_floor`, not numeric range |
| Demo/full import | PASS | identity+acceptance compatibility |
| Hints | PASS | explicit authored 3-step max |
| Alternate valid solutions | PASS | certifier equivalence honored |
| Controller/handheld | PASS as design | empirical UI QA retained |
| Local corruption/recovery | PASS | preserve evidence, backup restore |
| Future save | PASS with explicit no-overwrite gate |
| Cloud merge | PASS | monotonic union + conflict gate |
| Dynamic Cloud Sync | PASS after P9-03 | queued during committed run |
| Content update semantics | PASS after P9-04 | solved facts bind mechanics contract |
| Hostile input/idempotency | PASS | state ownership prevents duplicates |
| Certification drift | PASS | release-blocking |

# 19. Phase verdict
**PHASE 9 PASS WITH FOUR INTEGRATION REPAIRS.**

No unresolved design ambiguity blocks adversarial review. The repairs do not change the core mechanic, product thesis, campaign families or commercial model. They normalize stale schedule wording and make persistence/version ownership explicit.

`DESIGN COMPLETE = NO`.

## NEXT ACTION — PHASE 10 ADVERSARIAL REVIEW
Run dedicated destructive passes for:
1. fun/novelty and hour-3/hour-8 repetition;
2. dominant strategies and commit-spam brute force;
3. evidence-card bookkeeping vs genuine deduction;
4. scope/asset/authoring/certification burden;
5. demo weakness and store/trailer truth;
6. controller/200%-text ambiguity;
7. accessibility failures including pattern/icon density;
8. progression/hint/achievement edge cases;
9. persistence/Cloud/demo-import exploit/corruption behavior;
10. implementation ambiguity across Phase 4–9;
11. portfolio collision recheck against Games #001–#012;
12. produce an explicit kill/rework/freeze recommendation and patch any remaining authority contradiction before Phase 11.
