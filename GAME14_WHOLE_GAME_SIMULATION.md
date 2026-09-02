# GAME #014 — PHASE 9 WHOLE-GAME SIMULATION

Date: 2026-09-02
Status: COMPLETE — end-to-end paper simulation passed with clarifications; adversarial review next.
Working title: **NEGATIVE CASTING**
Authority: `START_HERE.md` -> `STATUS.md` -> `GAME_INDEX.md` -> Game #014 tournament record -> `GAME14_PRODUCT_THESIS.md` -> `GAME14_MECHANICAL_ARCHITECTURE.md` -> `GAME14_CONTENT_ARCHITECTURE.md` -> `GAME14_UX_PRESENTATION.md` -> `GAME14_COMMERCIAL_MODEL.md` -> `GAME14_TECHNICAL_SPEC.md` -> this file.

## 1. Phase-9 verdict
**PASS WITH CLARIFICATIONS.** The frozen 24-case campaign, controller-first UX, demo/full boundary, persistence model and late three-surface presentation survive an end-to-end hostile paper simulation without requiring a new gameplay mechanic.

No production implementation begins here. No Phase-4 core rule is changed. The repairs below are clarifications to progression/persistence/UX behavior already implied by frozen authority.

The largest residual risks handed to Phase 10 are empirical rather than structural: late-case visual/cognitive load, whether NC17–NC24 maintain distinct human routes in actual authored geometry, whether hint tier 3 is sufficient for genuinely stuck players, and whether rapid device switching can destabilize focus/glyph presentation without affecting logical input state.

---

# 2. Fresh install / first boot / controller-only path

### Scenario
Fresh full-game install, no prior save, controller connected before launch, 1280x800 display.

### Simulated flow
1. Boot enters local profile creation implicitly; no account or server gate.
2. Main menu exposes `Continue`, `Cases`, `Settings`, `Help`, `Quit`; with no save, `Continue` routes to NC01.
3. Controller focus is visible immediately. No mouse cursor is required.
4. First-run accessibility/settings can be opened before NC01. UI scale, reduced motion, contrast/glyph prominence, subtitles/audio and remapping do not affect puzzle truth.
5. NC01 loads with blocker focus, both lights visible, one dominant surface and target badges readable at 1280x800.
6. Tutorials explain input and canonical state language only; they do not expose an intended solve route.

### Result
PASS. No design contradiction.

### Clarification P9-C1 — first-run input ownership
The active input family used for prompts may change only after a deliberate input event from another device family, not passive mouse motion/trackpad noise. Puzzle focus itself remains stable when glyph family changes. This is a UX implementation clarification, not a mechanics change.

---

# 3. Demo NC01–NC08 first-time-player simulation

## NC01 — protected LIT
Player cycles the initially selected blocker through both poses. Actual surface semantics update immediately. One pose touches a required LIT sample; the player can infer that state is impossible and uses Check.

Hostile action: player rotates randomly several times before reading the target. No penalty, move counter or hidden score exists. Undo returns one blocker pose at a time.

PASS: first case communicates state mutation -> visible consequence -> explicit Check.

## NC02 — unique producer
Contribution inspection is introduced. The player checks one blocker, sees its *current* physical contribution, then switches blocker. The only remaining producer of a required shadow can be inferred without counterfactual preview.

Hostile action: player leaves inspection enabled while changing pose. Inspection updates to the newly chosen current pose; this is legal because it exposes only present causality.

PASS.

## NC03 — channel attribution
L1_ONLY/L2_ONLY are introduced with redundant channel glyphs and physical light origins. Simulated color-blind path uses glyph + line style only and remains solvable.

PASS.

## NC04 — BOTH decomposition
Player first over-blocks a protected sample, checks incorrectly, sees only mismatch locations, undoes one pose, then infers that one BOTH sample requires both channel bits but not any particular blocker identity.

PASS.

## NC05 — endpoint/extent + two incorrect checks
Player attempts two plausible states based on total dark area and checks twice incorrectly. After the second incorrect Check, the generic tip allowed by UX may state that every target sample is exact; it may not point to an endpoint or blocker.

The player then notices the last blocked sample differs between two coherent states.

PASS. Incorrect checks do not become a hint oracle.

## NC06 — synthesis + leave/resume
Mid-case, player changes two blocker poses, switches surface focus/UI state as applicable, then leaves to main menu.

Resume contract:
- blocker configuration must be restored;
- selected blocker / primary surface may be restored when compatible, but they are non-authoritative UI state;
- undo history need not survive restart;
- stale mismatch highlighting is not required to survive;
- tutorial flags remain remembered.

PASS.

### Clarification P9-C2 — resumable-state minimum
A resumable case save is considered successful if it restores the exact canonical blocker pose vector and case/content revision. Restoring undo/redo or mismatch feedback is optional and must never be required for logical recovery.

## NC07 — second-surface reveal
Surface B appears via authored reveal. The player sees two states that are equivalent on A but differ on B. `Switch Surface` is one controller action and preserves blocker selection.

Hostile action: user repeatedly switches A/B while cycling blocker state. Logical state remains blocker-pose only; surface focus cannot alter truth.

PASS.

## NC08 — demo capstone
Player uses A to prune, B to split equivalence, then solves. Demo ends on complete solve before purchase/wishlist call-to-action.

PASS. Demo arc proves the second-order mechanic before commercial messaging.

---

# 4. Demo -> full import and fresh-full alternative

## 4.1 Compatible demo import
Assume demo has NC01–NC08 completions, NC08 solved, tutorial flags, accessibility settings, and a resumable state only if the player had left an earlier case unfinished.

On first full-game boot:
1. full save is checked first; a valid established full save is never overwritten by demo import;
2. if no established full save exists, compatible demo data is offered/imported once;
3. import copies completion for NC01–NC08, compatible resumable case state, tutorial-seen flags and safe settings;
4. campaign unlocks are recomputed from canonical completion state rather than copied as opaque flags;
5. import records its source identity/version so repeating launch is idempotent;
6. demo installation is no longer required.

PASS.

## 4.2 Corrupt/incompatible demo data
If demo data fails checksum/schema/content migration, full game starts normally and preserves the corrupt source for diagnostic/recovery where practical rather than treating it as canonical.

PASS.

## 4.3 No-demo fresh full game
A buyer who never installed the demo starts NC01 normally with no missing tutorial or unlock dependency.

PASS.

### Clarification P9-C3 — import precedence
Demo import is additive only into a new/empty full-game campaign. Once a valid full campaign exists, demo data cannot roll back completion, case state, settings or achievement-supporting state.

---

# 5. Representative hour-1 MID case simulation

Representative structure: NC11-style, four blockers x3 states, two surfaces, six samples each.

### Intended chain
1. Surface A endpoint pattern eliminates one pose class for B2.
2. Two B2 states remain observationally equivalent on A.
3. Surface B splits those states because only one preserves a protected sample.
4. That fixed B2 contribution leaves one L2 producer for a required single-channel sample.
5. The newly forced producer constrains a BOTH cell, leaving a short residual assignment.

### Hostile behavior
- Player rotates every blocker once: actual semantics update, but no correct-state indicator appears.
- Player opens contribution inspection: current contributions are legible but candidate future states remain hidden.
- Player checks early: mismatching samples are highlighted only by location.
- Player undoes twice and branches history: redo clears after new mutation.

### Result
PASS. Human route remains connected across geometry, surface equivalence and channel attribution rather than reducing to blind state enumeration.

---

# 6. Late campaign NC17–NC24 / three-surface simulation

## NC17 — first third surface
One primary surface + two persistent compact cards. Sample counts remain low. A/B can leave two blocker classes tied; C splits them.

PASS if secondary cards can always answer `which region is mismatching?` without requiring memorization. Exact readability remains empirical.

## NC18–NC20 — five blockers and mixed 2/3 surfaces
The intended route always begins with class-level pruning, not object-by-object trial. Three-surface presence is rejected as useful if the third surface merely duplicates information from A/B.

PASS at design level.

## NC21–NC22 — late synthesis
Simulated chain uses endpoint -> channel -> cross-surface -> unique producer, or protected LIT -> endpoint -> BOTH -> cross-surface. Hint tier 1 can redirect attention to a semantic category; tier 2 names a relation/surface; tier 3 exposes one useful premise without naming a final pose.

PASS.

## NC23–NC24 — capstones
Shipping acceptance remains conditional on actual authored case certification:
- >=4 connected meaningful eliminations before residual choice for NC24;
- >=3 meaningful families represented;
- no dependence on microscopic grazing;
- no solver-only uniqueness;
- no requirement to memorize hidden secondary-surface state.

PASS as campaign architecture, with empirical authoring gate retained.

### Cognitive/repetition assessment
The campaign has a plausible escalation because complexity changes representation rather than merely count: early target semantics -> endpoint geometry -> second-surface state equivalence -> attribution interleaving -> late three-surface class splitting. The danger zone is NC17–NC24: if every case begins with protected-LIT pruning and ends with the same cross-surface split, the campaign will feel templated despite different geometry.

### Clarification P9-C4 — late-case sequencing gate
During content population, no three consecutive MID/LATE cases may use the same first decisive family and same final decisive family. Existing Phase-5 repetition signatures already support this; Phase 9 makes the sequence-level check explicit.

---

# 7. Stuck-player / hint ladder simulation

Scenario: player reaches NC20, can identify several mismatches but cannot find a useful first deduction.

1. Tier 1 points attention to a class of observation, e.g. protected light.
2. If still stuck, Tier 2 names a relationship/surface to compare.
3. Tier 3 exposes one useful premise/candidate-class fact but not the final blocker pose.
4. Hints remain free, replayable, non-punitive and achievement-neutral.

Hostile interpretation: repeatedly requesting all hints in every case is allowed; the game does not shame or score purity.

PASS.

Residual risk for Phase 10: if actual playtest shows tier 3 still leaves a meaningful subset of players permanently blocked, a solution-reveal policy would be a product-design reopen rather than a silent implementation convenience.

---

# 8. 2-of-3 group unlocks / skipped-case return / Campaign Complete

### Progression walk
- G1 cases NC01–03 available.
- Complete any 2 -> G2 unlocks.
- This repeats through G8.
- A skipped case remains available forever and can be returned to from Cases.
- Reaching G8 is not `Campaign Complete`.
- All 24 `required_for_floor` cases solved -> Campaign Complete.
- Optional NC25–NC30, if shipped, do not revoke or redefine that state.

Hostile case: player completes 2/3 in seven groups, reaches G8, solves two G8 cases, then returns to eight skipped floor cases. Unlock state remains monotonic; no group relocks.

PASS.

### Clarification P9-C5 — unlock derivation
Group availability should be derivable from completion records + frozen group thresholds, not trusted solely as mutable saved booleans. Stored unlocks may be cached, but loading/recovery recomputes or verifies them. This prevents corrupted unlock flags from becoming campaign authority.

---

# 9. Replay / achievements / offline

Solved cases remain replayable. Resetting/replaying a solved case never clears completion.

Achievements are derived from canonical campaign milestones where possible. If platform achievement unlock fails offline, a pending/reconciliation path retries later; platform achievement state never becomes authoritative campaign state.

Offline launch after entitlement/install works for all campaign gameplay, saves, hints, settings and completion. Platform services may be unavailable without changing puzzle truth.

PASS.

---

# 10. Cloud conflict / recovery simulation

## Conflict A — laptop older, Deck newer
Local Deck save contains more completed required cases. Cloud presents an older campaign save.

Recoverability rule: do not blindly replace the newer valid local campaign with older remote bytes. Compare validated save metadata/progress lineage; preserve both candidates when ordering is ambiguous and select/merge only fields whose semantics are monotonic and safe.

Safe merge candidates:
- solved-case completion is set-union for the same compatible content revision;
- opened hint tiers may be unioned;
- tutorial-seen flags may be unioned;
- accessibility settings require an explicit precedence rule rather than boolean union;
- one active resumable blocker vector cannot be automatically merged from two different devices; choose a validated winner by save generation/timestamp lineage and retain alternate backup where practical.

## Conflict B — corrupt cloud, valid local
Valid local wins; corrupt remote cannot erase it. Preserve/reject corrupt copy according to platform constraints.

## Conflict C — local corrupt, valid backup/cloud
Recovery order uses validated candidates; primary corruption should fall back to valid temp/backup/cloud according to the technical contract.

PASS with clarification.

### Clarification P9-C6 — cloud merge boundary
Only monotonic campaign facts may be automatically union-merged. Active case pose vectors, device-local display settings and incompatible content revisions are never field-wise merged. Ambiguous valid candidates must preserve a recoverable alternative instead of silently fabricating a hybrid session.

---

# 11. Hostile runtime behavior

## Orientation spam
Rapid state-next/state-prev is serialized as atomic legal pose mutations. Presentation animations may coalesce/cancel visually, but canonical state must equal the final accepted input sequence. Impossible in-between visual transforms cannot be sampled as puzzle truth.

PASS.

## Repeated Check spam
Check is idempotent with respect to puzzle state. Incorrect repeated checks do not accumulate penalty, hints or extra solver information beyond the same mismatch locations. Correct solved transaction must not duplicate completion/achievement writes.

PASS.

## Undo/reset abuse
Unlimited use is allowed. Reset changes current case state only. Solved history remains solved. Reset confirmation is UX-only.

PASS.

## Suspend / alt-tab during autosave
Canonical pose mutation completes before persistence transaction begins. A crash/suspend during write must leave either prior valid primary or a recoverable temp/backup candidate; partial bytes cannot become accepted state without validation.

PASS.

## Corrupt resume
If active case pose ids cannot be validated/migrated under current content revision, preserve campaign completions, discard/reset only the incompatible resumable case state, and inform the player concisely if progress in that one case was reset.

PASS.

## Content revision mismatch
Completion of an unchanged conceptual case may remain if migration explicitly certifies compatibility. A changed target/geometry cannot silently reuse an incompatible pose vector. Resume state migrates by stable ids only when exact mappings are declared; otherwise reset that case session while retaining safe campaign facts.

PASS.

## Rapid device switching
Inputs are action-based. Switching controller<->keyboard/mouse changes prompts only after deliberate event. It cannot duplicate a pose action due to one physical press being observed by two bindings in the same frame; implementation must de-bounce event ownership at the action layer.

PASS, residual QA risk.

---

# 12. Whole-campaign pressure and pacing

### First 20–30 minutes
Strong: one surface vocabulary becomes multi-surface before demo end.

### Hour 1
Strong if MID cases alternate first-decisive families; human reasoning representation has expanded beyond target matching.

### Hours 2–3
Risk rises as two-surface cases can converge on the same `prune -> split -> assign` rhythm. Existing repetition signatures plus P9-C4 sequence check are mandatory.

### Final hour
Three surfaces must be used to *split state classes*, not simply add more target cells. Surface count is rejected as difficulty when one surface is informationally redundant or when the player needs external notes.

Expected 3–5 hour product remains plausible on paper. Actual solve-time distribution is an implementation/playtest gate, not design proof.

---

# 13. Repairs / clarifications recorded by Phase 9

No frozen gameplay rule changed. The following clarifications are now authoritative alongside prior files:

1. **P9-C1 input ownership:** prompt-family changes require deliberate device input; focus remains stable.
2. **P9-C2 resumable minimum:** exact blocker pose vector + compatible case revision are the required resume payload; undo/mismatch state is nonessential.
3. **P9-C3 demo import precedence:** demo import can seed a new full campaign but never overwrite established valid full progress.
4. **P9-C4 late sequencing:** no three consecutive MID/LATE cases should share both first and final decisive deduction families.
5. **P9-C5 unlock derivation:** group unlock authority is recomputed/verified from completion records and thresholds.
6. **P9-C6 cloud merge boundary:** auto-merge only monotonic compatible campaign facts; never synthesize active pose vectors across devices.

These do not require reopening Product Thesis or Mechanical Architecture.

---

# 14. Residual attack surface for Phase 10

Phase 10 must attack, at minimum:
1. whether geometry-derived masks still allow authoring shortcuts that accidentally recreate arbitrary exact-cover puzzles;
2. whether contribution inspection plus mismatch locations together leak too much solver information after repeated manual probing;
3. whether NC17–NC24 three-surface UI is actually readable at 1280x800 without memorization;
4. whether the 24-case floor contains enough family-order diversity to avoid repeated solve rhythm;
5. whether blocker archetype reuse creates visual confusion between instance identity and pose identity;
6. whether equivalent physical solutions can produce confusing completion visuals or achievement inconsistencies;
7. whether 2-of-3 progression can let a player reach late cases without necessary tutorial concepts;
8. whether hint tiers can be authored consistently without accidentally naming the answer;
9. save migration, content-revision rollback, cloud conflicts, partial writes and duplicate solve transactions;
10. action-repeat/device-switch races, modal/focus traps and controller glyph churn;
11. accessibility under non-color reading, large UI scale and reduced motion on three-surface cases;
12. content production burden of certifying human routes and repetition signatures for all 24 floor cases;
13. price/value risk if empirical campaign length falls materially below 3 hours;
14. any implementation ambiguity that could cause renderer/physics data to become puzzle authority.

---

# 15. Phase-9 result
**PASS -> proceed to Phase 10 Adversarial Review.** The entire frozen game has been walked from first boot through demo, MID/LATE/capstone progression, replay, hints, completion, offline/cloud/recovery and hostile input/save behavior. No new mechanics were added and no production code was started.

## NEXT ACTION — GAME #014 PHASE 10 / ADVERSARIAL REVIEW
Create `GAME14_ADVERSARIAL_REVIEW.md` and attack the complete frozen design across fun/repetition, geometry integrity, human-route validity, UX/oracle leakage, progression/tutorial bypass, hints, accessibility, content burden, technical determinism, persistence/cloud corruption, device/input races, commercial value and implementation ambiguity. Convert every material finding into one of: `PASS`, `REPAIR NOW`, `EMPIRICAL GATE`, or `DESIGN REOPEN`. Apply safe repairs to the affected authority file(s), then leave Phase 11 a finite freeze checklist and unresolved empirical gates only.