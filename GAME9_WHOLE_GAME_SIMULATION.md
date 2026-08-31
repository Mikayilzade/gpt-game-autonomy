# GAME #009 — PHASE 9 WHOLE-GAME SIMULATION ON PAPER

Status: **PHASE 9 COMPLETE / PHASE 10 READY**
Date: 2026-08-31
Selected game: **Binder's Imposition** (working title)
Production implementation: **FORBIDDEN in factory**

Authority: `START_HERE.md` -> `STATUS.md` -> `GAME_INDEX.md` -> Game #009 tournament history -> `GAME9_PRODUCT_THESIS.md` -> `GAME9_MECHANICAL_ARCHITECTURE.md` -> `GAME9_CONTENT_ARCHITECTURE.md` -> `GAME9_UX_PRESENTATION_ARCHITECTURE.md` -> `GAME9_COMMERCIAL_MODEL.md` -> `GAME9_TECHNICAL_SPECIFICATION.md` -> this file.

This phase walks the complete game end to end, including hostile behavior, and repairs contradictions rather than merely recording them. It adds no new core mechanic.

---

# 1. Phase-9 verdict

The game remains coherent from first boot through campaign completion and recovery/cloud/import edge cases. No Phase-3 product-thesis reopening is required.

Material repairs made here:
1. froze one exact D01–D06 mapping so Product/Content/UX/Commercial no longer imply different tutorial sequences;
2. clarified crash ordering around successful Commit so persistence has a single authority point;
3. froze same-state Commit idempotency and post-failure re-enable behavior to prevent meaningless Commit spam without introducing punishment;
4. added explicit save-lineage metadata needed to distinguish clean descent from cloud divergence;
5. froze stale-content-revision recovery behavior so old workbench state is never silently destroyed;
6. clarified bounded-history compaction and replay after very long sessions;
7. clarified demo/full first-launch placement when imported demo progress overlaps later full progress.

These are specification repairs/clarifications, not new gameplay systems.

---

# 2. Canonical demo/campaign mapping repair

Earlier phases agree on the lessons but use slightly different labels. The canonical mapping is now:

| Demo ID | Campaign ID | Chapter | Mechanical responsibility |
|---|---|---|---|
| D01 | G9_C01 | I | T4 inverse-fold surprise; direct arrange -> fold -> 1-2-3-4 reveal. |
| D02 | G9_C02 | I | T4 prediction reinforcement; player predicts one adjacency before Preview. |
| D03 | G9_C03 | I | T4F duplex/orientation; binary orientation glyph and sheet flip. |
| D04 | G9_C04 | I | **Bridge case:** second signature is introduced with authored fixed outer/inner roles; the new lesson is what nesting does, while local transforms remain already-known T4/T4F. No free role choice yet. |
| D05 | G9_C05 | II | First player-chosen two-signature nest role plus one FACING relationship; wrong role cannot be fixed by local swaps. |
| D06 | G9_C06 | II | Demo capstone: reading order has more than one locally valid arrangement; categorical material/SAME_SIGNATURE or role constraint selects the viable global arrangement. |

Consequences:
- the frozen demo is still the **first six authored campaign cases**;
- Chapter I remains four cases;
- Chapter II starts at G9_C05;
- D04 is the intended transition/bridge and does not add a second simultaneous untaught mechanic because nesting role is fixed;
- D05 introduces free nesting choice and facing together only because facing is visually direct in the resolved book and is used to demonstrate why role choice matters; if playtest comprehension fails, FACING may be reduced to a single highlighted pair but the rule itself is not removed;
- D06 introduces no new transform. It is the first synthesis case and teaches categorical material ownership as a tie-breaker.

All future references to D01–D06 use this table.

---

# 3. Trace 1 — fresh install -> D01–D06 demo -> purchase/import -> first new full case

## Start
No profile. Default 1280x800-compatible layout. Settings load before title. Demo build has campaign content only through G9_C06 and no Steam achievements.

## Important transitions
1. Start creates profile UUID and schema version.
2. G9_C01: player places four faces, Previews, sees deterministic T4 fold, Commits successfully.
3. G9_C02: prediction prompt asks one adjacency; answer/skip never gates progress.
4. G9_C03: T4F introduces explicit orientation glyph and sheet flip.
5. G9_C04: second signature appears with locked outer/inner roles; Preview shows one sheet nesting inside the other.
6. G9_C05 unlocks first editable nest order; wrong role produces a resolved book whose requested facing pair fails.
7. G9_C06 reading order can be satisfied in multiple local layouts; material/signature constraint forces the correct physical role.
8. Demo durable save contains solved G9_C01..G9_C06, badge evidence, settings and import provenance fields.
9. Full game first launch discovers demo save, validates and imports idempotently.
10. Full game recomputes prerequisites; first newly available full case is G9_C07, while G9_C01..G9_C06 remain replayable.
11. Achievement reconciliation grants only achievements whose requirements are genuinely satisfied by imported facts.

## Player-visible feedback
Full game: `Demo progress imported — 6 cases completed. Continue with Case 7 or replay earlier cases.` No duplicate reward animation for every imported case; chapter achievement may grant once if eligible.

## Contradiction found
Previous files agreed on D01–D06 lessons but did not align them unambiguously with Chapter-I/II sequence.

## Repair
Section 2 mapping is canonical.

## Regression implications
Content manifest, demo flags, prerequisite graph, commercial copy and onboarding tests must all reference the same G9_C01..G9_C06 IDs.

Earlier phase reopen? **No. Clarification only.**

---

# 4. Trace 2 — new player misunderstands duplex orientation and Previews excessively

## Start
G9_C03. Player understands T4 ordering but assumes Side B uses the same visible orientation as Side A.

## Transitions
1. Player places faces by apparent visual orientation.
2. Preview resolves one orientation-sensitive face inverted.
3. Final-book inspection highlights orientation glyph and offers Source mapping to the exact flat slot.
4. Player exits, flips sheet or face where legal, Previews again.
5. Repeats Preview several times.

## Feedback
- orientation failure says `MAP_A is inverted in the finished book; required upright`;
- source highlight shows where MAP_A came from but does not say which source action solves it;
- T4F mini-diagram permanently exposes flip orientation after tutorial unlock;
- no green/red source-state oracle appears before Preview.

## Ambiguity
Could repeated Preview become the tutorial rather than prediction?

## Repair
No punitive Preview currency. Instead:
- same WorkbenchState hash always resolves to exactly the same cached semantic Preview result;
- replaying it can replay/skip animation but reveals no additional mechanical information;
- after the player has seen the T4F orientation explanation once, the rule drawer and orientation mini-diagram stay available permanently;
- G9_C03 certification requires at least one authored prediction prompt and playtest gate on explaining the orientation outcome.

## Regression
UX test: ten same-state Previews must not mutate history, stats relevant to completion, layout or solver truth.

Reopen? **No.**

---

# 5. Trace 3 — competent Chapter-III player memorizes T4 and hill-climbs

## Start
Mature two-signature case. Player can inverse-fill T4 almost instantly and attempts `one edit -> Preview -> inspect failures -> repeat`.

## Transitions
1. Local read order is made correct quickly.
2. Global SAME_SIGNATURE/MATERIAL/FACING predicate remains impossible under current nest role.
3. Several local swaps change resolved positions but cannot make the wrong role viable.
4. Player eventually changes nest role, after which local inverse fill becomes straightforward.

## Feedback
Preview/failed Commit exposes failed final relationships, never a scalar `% correct`, solver distance, suggested source slot or “warmer/colder” delta.

## Exploit result
Local formula is intentionally learnable; it is not itself an exploit. Hill climbing remains weak because mature certification requires a global branch whose wrong class cannot be repaired by local improvement.

## Repair
Phase-5 quality gate Q6 is strengthened operationally: for every MATURE/CAPSTONE case, certification stores at least one **wrong global branch witness** proving that all assignments inside that branch fail at least one required predicate. This is authoring evidence, not runtime hint data.

## Regression
Phase-10 must attack whether failed-predicate lists are still too informative when many predicates exist.

Reopen? **No; content-certification clarification.**

---

# 6. Trace 4 — first T8 case and first two-template choice

## Start
Chapter IV. Player knows T4/T4F and nesting. First T8 case uses one signature and guided diagram.

## Transitions
1. T8 chooser shows 8 flat slots and frozen alternating orientation glyphs before selection.
2. First Preview folds to exact deterministic T8 order; prediction asks only one bounded relationship.
3. Later case offers T4 vs T8 where both are structurally legal.
4. Capacity/assignment carry-over uses deterministic shared-slot matching; displaced faces return to tray and change confirmation says how many.
5. Secondary orientation/group constraint makes one template globally impossible.

## Feedback
Template chooser communicates final face count, orientation pattern and trim positions; it does not fill pages.

## Ambiguity
Could switching templates destroy work or make Undo non-exact?

## Repair
Existing Phase-6 carry-over rule is sufficient. Phase 9 additionally requires the transaction to record displaced face IDs and their exact prior slots so Undo restores byte-equivalent WorkbenchState.

## Regression
Technical test: choose T8 -> T4 -> Undo must restore the exact pre-change T8 assignments/history cursor.

Reopen? **No.**

---

# 7. Trace 5 — first T6P/trim case, REQUIRED_BLANK vs EMPTY

## Start
Chapter V bridge. T6P has two sacrificial positions. Tray contains explicit `BLANK_A` plus ordinary faces. Unused sacrificial slot can show EMPTY.

## Transitions
1. Player initially leaves a final required blank as EMPTY.
2. Legality permits EMPTY only in template-permitted sacrificial slot; final `BLANK_AT` requires the explicit REQUIRED_BLANK face if a bound position must exist blank.
3. Preview shows EMPTY as absent/cut-away placeholder and REQUIRED_BLANK as a physical blank page.
4. A trim-mark objective requires a sacrificial mark to DISAPPEAR.
5. Commit passes only when explicit blank and trim fate both match.

## Feedback
UI uses distinct symbols and text: `Blank page` versus `Unused cut-away slot`. Failure never says merely `blank wrong`.

## Contradiction risk
Players may treat EMPTY and REQUIRED_BLANK as synonyms because both look white.

## Repair
The first T6P case must use visibly different non-color-only iconography and one direct rule sentence: `Blank page = a real page with nothing printed. Empty = no page remains there.` The distinction is semantic and localized.

## Regression
Accessibility test at grayscale/high-contrast must still distinguish both tokens.

Reopen? **No.**

---

# 8. Trace 6 — late Chapter-VI three-signature case with Undo/Redo, Preview and failed Commit

## Start
Three signatures A/B/C; one material role, one orientation-capable role, 12–20 faces; ≤4 secondary predicate families.

## Transitions
1. Player hypothesizes Gold must be middle.
2. Reorders signatures; one SET_NEST_ROLE transaction.
3. Uses SWAP_PAIR and MOVE_GROUP; each is atomic.
4. Preview confirms most relationships but one orientation fails.
5. Player edits orientation, then Undo, Redo; resolved state returns exactly.
6. Commit is legal but fails one FACING predicate.
7. Failed Commit keeps exact layout/history.
8. Player changes one global role, resolves and succeeds.

## Feedback
Failed Commit groups failures by predicate type and shows final positions; no source-slot prescription.

## Ambiguity
Repeated Commit on unchanged failed state could spam attempts/UI.

## Repair — frozen Commit idempotency
- Commit is keyed by canonical WorkbenchState hash + case revision.
- Re-submitting the identical unchanged failed state returns the same cached evaluation and **does not increment incorrect-Commit stats again**.
- After a failed Commit, the primary Commit control remains available for accessibility but is visually marked `No changes since last bind`; activating it simply reopens the existing result, not a new attempt.
- Any mechanical edit creates a new state hash and re-enables a genuine new Commit.
- No cooldown, currency or punishment is introduced.

## Regression
Direct Bind badge must count semantic distinct failed states, not button presses.

Reopen? **No.**

---

# 9. Trace 7 — quit/crash during edit, Preview and successful Commit

## A. Crash during ordinary edit
Debounced checkpoint may lag by ≤5 seconds. After restart, load last durable WorkbenchState/history. At most the most recent uncheckpointed edits are lost; no solved progress is fabricated.

## B. Crash during Preview
Preview is L4 presentation over immutable source/resolved snapshots. Restart loads editable L2 state from last checkpoint. No Preview history exists, no attempt counted, no transform half-state can persist.

## C. Crash immediately after successful Commit
This needed exact ordering.

### Frozen success transaction order
1. validate -> resolve -> evaluate success in memory;
2. construct CommitPlan;
3. write new campaign/profile state atomically including case completion, badge evidence, progression facts and in-progress-case completion marker;
4. reopen/verify durable save;
5. only then emit authoritative `CASE_SOLVED_DURABLE` to presentation/platform reconciliation;
6. success celebration/result UI may now appear;
7. achievement platform calls may happen after durable local success and may retry later.

If crash occurs before step 4, case is not durably solved and reload restores previous valid checkpoint/layout. If crash occurs after step 4 but before celebration, reload sees the solved case and shows a compact `Case completed` recovery summary or campaign map; it never asks the player to solve again.

## Repair
This ordering is now explicit Phase-9 authority.

## Regression
Crash-injection tests at every boundary 1–7 required in implementation QA.

Reopen? **No.**

---

# 10. Trace 8 — Steam Deck/controller-only, 1280x800, text scaling + Reduced Motion

## Start
Player boots with controller, 150% text scale, Reduced Motion, 1280x800.

## Transitions
1. Settings apply before title interaction.
2. Campaign map reflows without clipping required case state.
3. Workbench keeps ≤3 signatures accessible; if scaled text consumes rail width, Goal rail becomes top drawer while source sheet area stays functional.
4. Discrete focus traverses Goal -> signature header -> slots -> tray -> actions with no virtual mouse.
5. Fold Preview resolves instantly and uses diagrammatic/crossfade presentation; skip cannot change result.
6. All mechanical marks remain icon + text/glyph redundant.

## Feedback
Active input glyphs are controller family; missing glyph falls back to localized action name.

## Ambiguity
`important default text >=12 px` does not itself guarantee 150% scale layout.

## Repair
1280x800 acceptance must test 100%, 125%, 150%, and one maximum-supported text scale. Required rules may wrap/scroll; source slots may not shrink below reliable focus/click target size. If both cannot fit simultaneously, Goal rail becomes drawer before sheet slots are compressed.

## Regression
No required information may exist only in hover tooltip.

Reopen? **No.**

---

# 11. Trace 9 — offline play -> second-device cloud divergence -> merge/recovery

## Start
Device A and B share profile UUID/revision R20. Both go offline.

A: solves G9_C18, edits G9_C19 -> revision branch A22.
B: solves G9_C20, edits G9_C21 -> branch B22.

## Conflict
Simple numeric `save_revision=22` cannot prove ancestry.

## Repair — save lineage metadata
Every durable save revision must include:
- `save_revision` monotonic local integer;
- `revision_id` globally unique opaque UUID/hash;
- `parent_revision_id | NONE`;
- optional bounded ancestor summary/checkpoint hash sufficient to establish direct known ancestry for recent revisions.

Cloud merge:
1. if one revision lineage contains the other, choose descendant;
2. otherwise branch is divergent regardless of equal/higher integer;
3. solved cases union -> both G9_C18 and G9_C20 remain solved;
4. badges/achievement evidence/import provenance union safely;
5. unsolved G9_C19 and G9_C21 workbenches are **not merged**;
6. choose higher local logical revision only for primary resume when clearly ordered; if both are divergent meaningful unsolved snapshots, retain both conflict copies and show one concise choice: `Resume Case 19 from Device A` / `Resume Case 21 from Device B`;
7. never merge transaction histories;
8. merged profile writes a fresh child revision and retains conflict backups until verified checkpoint.

## Feedback
No scary “corrupt” wording for ordinary divergence. Campaign completion is preserved automatically; only competing in-progress work requires a choice.

## Regression
Offline game remains playable without Cloud API. Cloud conflict cannot roll back a solved case.

Earlier phase reopen? **Technical specification clarification only.**

---

# 12. Trace 10 — repeated demo import + achievement reconciliation

## Start
Full profile already imported demo revision D10. User later reopens demo, earns one Predicted badge, producing D11.

## Transitions
1. Reimport D10 -> provenance identifies same/older revision -> no-op.
2. Import D11 -> solved flags OR, badge union; full settings remain authoritative if explicitly changed in full game.
3. Recompute progression.
4. Recompute eligible achievements.
5. Platform unavailable -> local eligibility persists, grant queued/retried on reconnect.
6. Reconnect -> missing eligible achievements requested once/idempotently.

## Feedback
Only newly added progress gets a concise import summary. No repeated six-case completion spam.

## Ambiguity
Demo and full saves could have different UUIDs.

## Repair
Import provenance uses `(source_product = DEMO, source_profile_uuid, source_revision_id/hash)`; source profile need not equal full profile UUID. Eligibility validates known demo case IDs/content revisions before union.

## Regression
Repeated arbitrary import order D11 -> D10 -> D11 must converge to identical full CampaignState.

Reopen? **No.**

---

# 13. Trace 11 — campaign completion -> replay/badges/Mastery Shelf boundary

## Start
Player completes final Chapter-VI capstone.

## Transitions
1. Durable success writes campaign completion.
2. Completion screen celebrates finite ending.
3. Campaign map remains available with solved/replay state.
4. Player may chase visible optional badges.
5. Mastery Shelf appears only if 4–8 variants actually passed the same solver/anti-isomorphism quality floor before release; otherwise it simply does not exist.

## Feedback
No fake infinite mode, daily challenge, currency, “prestige,” reset or mandatory 100% completion.

## Ambiguity
Could Mastery Shelf push total beyond the 34-case soft ceiling?

## Repair
The 34-case soft ceiling includes all shipped Mastery Shelf variants. Baseline 30 campaign + up to 4 shelf cases is the simple target. A shorter 24–28 campaign may allow more shelf variants only if total remains ≤34 and each is distinct; campaign quality still wins.

## Regression
Store copy may not promise Mastery Shelf before final content certification.

Reopen? **No.**

---

# 14. Trace 12 — hostile behavior battery

## 12A Preview spam
100 Previews from same state: no history entries, no persistent mechanical mutation, deterministic same semantic result. Presentation may replay; no new clue channel appears.

## 12B Commit spam
Identical unchanged failed state reopens cached result and increments no additional attempt statistic. Changed state creates one new semantic attempt.

## 12C Restart loops
Restart restores authored initial WorkbenchState as one deliberate action after confirmation when meaningful edits exist. Restart itself is not Undo-able across the whole session unless implementation stores it as a session boundary snapshot; design does not require cross-Restart Undo. Restart never clears solved campaign facts or settings.

## 12D Template thrashing
Every template change is one transaction; displaced assignments return to tray deterministically. Undo restores exact prior template and assignments.

## 12E Huge history
Current state may never depend on retaining unlimited transactions.

Frozen compaction rule:
- keep full history while <=256 compact transactions when practical;
- above implementation budget, create an **anchor snapshot** representing the state immediately before the retained tail and keep at least the newest 64 transactions;
- Undo stops cleanly at the anchor boundary with no corruption;
- current WorkbenchState is serialized independently from history and remains exact;
- Redo tail semantics remain normal after compaction;
- history compaction is not player-visible unless the user reaches the Undo boundary.

## 12F Corrupt save
Primary invalid -> try backup -> validated import source where relevant. Never overwrite corrupt source silently. If no recovery succeeds, preserve corrupt copies and offer new profile/recovery path.

## 12G Stale content revision
Case content may change between builds.

Frozen behavior:
1. solved case IDs remain solved if the new manifest explicitly declares the old completion compatible;
2. unsolved snapshot with same case revision/hash loads normally;
3. known migration maps old slots/faces/template IDs deterministically -> migrated snapshot;
4. if layout migration succeeds but old transaction history is incompatible, keep migrated current layout and clear history with one concise notice;
5. if in-progress layout cannot be migrated safely, retain it as a recovery archive, restart that case from new authored initial state, and say `This case changed in an update; your old work has been preserved for recovery.`;
6. never map removed/renamed IDs heuristically by localized name;
7. unknown future save/content versions are read-only and never overwritten by older builds.

## 12H Stale solver certification
Shipping content manifest includes case revision/hash and certification version. A case whose shipping definition differs from certified hash is a build failure, not runtime content.

---

# 15. Cross-phase contradiction register

| Issue | Severity | Repair | Reopen earlier phase? |
|---|---:|---|---|
| D01–D06 sequence ambiguity | Material | Exact G9_C01..G9_C06 mapping frozen in §2. | No; clarification. |
| Crash immediately after successful Commit | Material | Durable-save-before-solved-UI ordering frozen. | No; technical clarification. |
| Cloud `save_revision` insufficient to prove ancestry | Material | Add `revision_id` + `parent_revision_id` lineage. | No; Phase-8 extension. |
| Identical Commit spam | Moderate | Same-state result idempotent/cached; no repeated attempt increment. | No. |
| Huge transaction history | Moderate | Snapshot anchor + retained tail, current state independent. | No. |
| Stale content revision | Material | Explicit migration/recovery archive policy. | No. |
| REQUIRED_BLANK vs EMPTY visual ambiguity | Moderate | Distinct semantic labels/icons and first-use explanation. | No. |
| Deck text-scale pressure | Moderate | Goal rail collapses to drawer before source slots compress. | No. |
| Preview as hill-climb oracle | Existing risk | No scalar/delta source oracle; mature cases require wrong-global-branch witness. | No; Phase-10 attack required. |

No contradiction requires changing the selected concept, core loop, template grammar, predicate vocabulary, campaign scale, premium model or deterministic architecture.

---

# 16. Phase-10 attack queue

Phase 10 must deliberately try to kill or reopen the design on these remaining risks:
1. **fun/repetition:** after T4 is mastered, do global role deductions stay satisfying across 24–30 cases or feel like repeated set partitioning?
2. **Preview/Commit oracle leakage:** do per-predicate failures allow mechanical hill climbing despite no scalar score?
3. **tutorial compression:** can D04–D06 fit the demo without concept overload while still ending on genuine synthesis?
4. **T8 clerical burden:** does larger face count add reasoning rather than memory/swapping work?
5. **orientation burden:** binary orientation remains the most likely source of unfun bookkeeping;
6. **trim/blank value:** T6P must justify itself as meaningful late vocabulary rather than an exception family;
7. **content exhaustion:** 24 certified strong cases remain a release floor; solver-hard near-isomorphs do not count;
8. **controller/Deck density:** three-signature late cases must remain readable at 1280x800 and scaled text;
9. **save/cloud complexity:** verify these resilience contracts are proportionate and do not contaminate the pure puzzle core;
10. **implementation ambiguity:** attack every transform, nested mixed-size case, source mapping, template carry-over, badge condition and content migration edge for missing ordering rules.

---

# 17. Phase-9 completion gate

PASS if:
- all 12 required scenarios have deterministic expected behavior;
- D01–D06 mapping is singular;
- no important gameplay result depends on presentation timing/platform connectivity;
- crash/cloud/import paths cannot fabricate or silently delete progress;
- hostile Preview/Commit/template/history behavior is bounded without punishment economy;
- every material contradiction has a recorded repair;
- no repair requires a new core mechanic.

**RESULT: PASS. PHASE 9 COMPLETE.**

## NEXT ACTION
Run **Game #009 Phase 10 — Adversarial Review** as a destructive multi-pass review of the full Phase 3–9 authority. Do not merely restate risks. Attempt concrete failure constructions for fun/repetition, dominant strategies, Preview/Commit oracle leakage, tutorial/demo overload, T8/T6P bookkeeping, content exhaustion/isomorphism, controller/Deck readability, persistence/cloud/import ambiguity, technical overscope, and implementation underspecification. Repair canon where possible; explicitly reopen an earlier phase only if a repair changes its frozen design. If the design survives and every material issue has a bounded resolution or empirical gate, advance to Phase 11 Specification Freeze.