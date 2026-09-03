# GAME #015 — PHASE 9 WHOLE-GAME SIMULATION

Date: 2026-09-03
Status: PHASE 9 COMPLETE
Working title: **FRESH COAT**
Design complete: NO

## 0. Purpose
This is a destructive paper simulation of the shipped experience using only the authority frozen in Phases 3–8. The goal is to find contradictions, friction, exploit incentives, prerequisite mistakes and recovery ambiguity before adversarial review.

No production implementation is started here.

## 1. Simulation method
Every walkthrough records:
- player-visible state;
- semantic state;
- likely confusion/friction;
- whether existing authority resolves it;
- repair if needed.

The simulation assumes the certified case data exists and that UI presentation is a projection of semantic truth, never a second authority.

---

## 2. First boot — desktop / Steam Deck

### Visible state
First boot opens directly into a controller-complete main menu. Active-device glyphs appear from the latest meaningful input. `Continue` is unavailable on a clean profile; `Case Select`, `Settings`, `Accessibility`, `Credits`, and platform-appropriate Quit are available. No launcher precedes the game.

The first-run accessibility affordance is visible without forcing a wizard: text scale, coat-pattern redundancy, reduced motion, high-contrast selection outline, camera sensitivity/invert, and control remapping are reachable before FC01.

Selecting Start/FC01 shows the canonical stable booth view with two workpieces, target rail, stage rail `Arrange A -> Spray A -> Reveal`, action strip, and exposure preview ON.

### Semantic state
`profile.schema_version` valid; no completed cases; `latest_case = FC01`; puzzle state enters `EDIT_A`; certified FC01 package loaded; arrangement references only stable IDs.

### Friction attack
- Deck player must not need touch/mouse for Settings or first puzzle.
- coat A cannot appear as color-only before accessibility settings are discovered.
- device switching during menu navigation cannot lose focus.

### Resolution
Existing UX/technical authority resolves all three. **No repair.**

---

## 3. FC01 — first arrangement, first Spray, first failure, Undo/reset

### Visible state
Player selects the slab. Valid sockets highlight. Cycling legal poses never shows illegal intermediate geometry. Exposure preview labels target regions only as factual `EXPOSED NOW` / `PROTECTED NOW`; it does not judge them against targets.

A first-ever Spray micro-confirmation explains that every currently exposed region receives A. Player intentionally or accidentally chooses the wrong masker socket and commits.

Spray animation finishes; `Reveal` separates the workpieces. Result says factual discrepancies, e.g. `top needed RAW; received A` and `side needed A; remained RAW`.

Failure actions expose `Undo Last Spray`, `Reset`, Targets and replay of actual attempt. Undo returns to the exact editable pre-A arrangement.

### Semantic state
Before Spray: `EDIT_A`, legal `arrangement_id=A17`, histories all `[]`.
Spray transaction creates `(attempt_id, tx_seq=1, stage=A)` and exact histories from certified exposure set. Result is target validation only.
Undo replaces state with saved pre-A checkpoint; no inverse paint calculation is performed.

### Friction attack
A binary `wrong` result would turn Spray into a Check oracle. Existing design instead gives rich region consequences. The player can experiment, but each experiment requires interpreting a physical exposure result.

### Resolution
Existing authority resolves it. **No repair.**

---

## 4. FC02–FC05 onboarding and family unlock behavior

### Visible state
FC02 adds pose cycling. FC03 exposes a target card for the masker itself. FC04 introduces adjacent semantic regions. FC05 removes most tutorial prompting and asks the player to compare blocker footprints.

Family F1 contains FC01–FC03. Completing any two would normally satisfy the 2-of-3 family rule, but FC03 is a mandatory self-obligated-mask knowledge gate for content that assumes that rule.

### Semantic state
Progress stores completed case IDs independently from family availability. `family_unlock(F2)` cannot be represented as only `count(F1_completed)>=2`; it must also evaluate mandatory gates required by the destination content.

### Contradiction found
Commercial authority says both:
1. completing 2/3 in a family unlocks the next family;
2. FC03, FC10, FC13, FC16 are mandatory concept-introduction gates before entering content that assumes those concepts.

Without a precise graph, a player completing FC01+FC02 could appear to have unlocked F2 while FC03 remains mandatory for F3 self-obligation-heavy content. Likewise demo imports can mark FC10/FC13 complete before intervening families are reached.

### Repair
Freeze unlock semantics as **availability predicates**, not one global sequential boolean:
- family N+1 normally becomes visible/playable after 2 completed cases in family N;
- a case additionally checks only the concept prerequisites it actually assumes;
- FC03 is required before FC07+ and any earlier case explicitly tagged `requires_self_obligated_mask`;
- FC10 is required before any non-FC10 two-pass case whose proof assumes two-pass manipulation;
- FC13 is required before any case with A_THEN_B targets;
- FC16 is required before any case whose proof depends on cavity-region semantics;
- completion imported from the demo satisfies the same gate by stable case ID even if intervening cases/families remain incomplete;
- no imported completion auto-completes skipped cases or family 3/3 marks.

This repair is patched into Commercial Model after this simulation.

---

## 5. Exact seven-case demo -> full-game import

### Demo sequence
Canonical demo sequence:
`FC01 -> FC02 -> FC03 -> FC05 -> FC10 -> FC13 -> FC14 (or certified mechanically identical smaller FC14-family finale if C2 pacing gate requires it)`.

### Visible state
The demo openly labels these as real campaign cases. Skipped IDs are not displayed as completed. On demo finish, player may replay demo cases and receives storefront CTA.

On first full launch, imported progress is reflected in Case Select: FC01,02,03,05,10,13,14 are complete. FC04,06–09,11–12 remain incomplete. Campaign entry defaults to the earliest unlocked incomplete case rather than jumping to FC15 merely because later demo cases are complete.

### Semantic state
Import unions completed shared case IDs and tutorial acknowledgements by stable IDs. Import fingerprint prevents duplicate application. Achievement reconciliation runs once in full build.

### Friction attack
Potentially confusing state: later cases are already complete while middle campaign cases are not. A naive `highest_completed_case + 1` Continue algorithm would jump too far; a naive sequential lock algorithm would hide imported later completions.

### Repair
`Continue` selection must be progression-aware:
1. resume a valid in-progress attempt if present;
2. else choose the lowest-display-order unlocked incomplete primary case;
3. else, if all currently unlocked cases are complete but next content is blocked by a mandatory gate, choose that gate case;
4. else choose campaign completion/replay surface.

Case Select always shows imported later completions even if surrounding families are not yet naturally reached. Completing an imported gate never fabricates completion for skipped predecessors.

This is also patched into Commercial/Technical authority.

---

## 6. FC10 — two-pass teaching and interruption between A/B

### Visible state
Before play, stage rail explicitly shows `Arrange A -> Spray A -> Rearrange -> Spray B -> Reveal`. A and B have distinct pattern/symbol identity. After Spray A, history badges update factually and B-stage legal sockets/poses become available. No automatic movement occurs.

Player rearranges, then suspends/exits before Spray B.

### Semantic state
Durable state is post-A checkpoint plus current editable B arrangement, with A histories preserved. Resume reconstructs `EDIT_B`; no paint animation needs to be resumed and no B coat exists yet.

### Friction attack
If only the A checkpoint were saved, the player's B edits would be lost. UX Phase 6 says leaving a puzzle may restore latest committed checkpoint plus current editable arrangement; Phase 8 allows editable resume snapshot. This is sufficient but should be treated as required for leaving/suspend, not optional convenience.

### Repair
For explicit exit, app suspension and Dynamic Cloud Sync hand-off, persist the current **valid editable arrangement snapshot** in addition to the latest durable spray checkpoint. It remains non-transactional puzzle state and may be discarded on corruption while preserving the spray checkpoint.

Technical authority patched accordingly.

---

## 7. FC13 — A_THEN_B introduction

### Visible state
Target rail shows `A -> B`, never only a combined final surface. One explicit one-time explanation says the region must receive A on the first pass and B on the second. Exposure preview remains current-stage factual only.

A common failure paints B only. Reveal says `needed A -> B; received B`, and may show actual exposure stages.

### Semantic state
Target predicate is exact ordered history `[A,B]`. Appearance shader may visually combine coats but cannot decide success.

### Friction attack
Player may assume final visible B equals success if combined appearance hides history. Existing badge/history strip resolves this if kept persistent.

### Resolution
**No repair.** Maintain ordered-history badge in target/reveal and optional actual-history strip during play.

---

## 8. FC16 — cavity inspection without camera hunting

### Visible state
Cavity floor and rim appear as separate semantic target entries. Selecting cavity floor in region browser focuses it; Inspect Object makes other pieces translucent while preserving their positions. A one-time cavity explanation states that inside faces are ordinary regions reached only through the aperture.

Player never needs to rotate camera into the cavity to discover whether it is currently exposed; semantic browser can state current factual exposure status.

### Semantic state
Certified exposure is ordinary ray reachability/self-occlusion. Camera position has no semantic effect.

### Friction attack
Object isolation could become an oracle if it removes blockers semantically or displays counterfactual spray reach. Existing authority explicitly forbids this.

### Resolution
**No repair.** QA gate: translucent blockers must remain spatially legible enough that isolation does not falsely suggest open rays.

---

## 9. FC21 role reversal and FC24 capstone readability

### FC21 visible experience
Three objects, two passes. Player traces own-target cards plus changing masking roles. Stage B starts from exact A arrangement and requires deliberate reassignment. The successful reveal demonstrates X/Y/Z histories; player can inspect their own successful A/B arrangements afterwards.

### FC24 visible experience
Four objects, 8–14 targeted regions, RAW/A_ONLY/B_ONLY/A_THEN_B, one cavity, role reversal and shared critical masking relation. Canonical camera plus object selection/isolation keeps one piece cognitively foregrounded at a time. Target rail groups requirements per object, not as a single 14-row undifferentiated list.

### Semantic state
No new mechanics exist. Certifier confirms <=4 normal solution classes and repetition signature is non-isomorphic to earlier cases.

### Friction attack
The danger is bookkeeping overload rather than mechanical ambiguity. A four-object scene can become a visual spreadsheet if target requirements cannot be chunked.

### Repair
Late-case target rail must default to **object-grouped collapsed cards** with concise per-object history summary and one-click expansion. Selecting an object automatically scopes/highlights its target card; selecting a target row focuses its region. This is UX-only and does not expose solution information.

Patch UX authority.

---

## 10. Campaign completion, achievements, replay, alternate solutions

### Visible state
Completing FC24 does not automatically claim 24/24 if earlier skipped cases remain incomplete. The campaign-complete achievement requires all 24 stable IDs complete. The player who used 2-of-3 progression can therefore beat the final capstone before 24/24, then clean up skipped cases.

Family 3/3 achievements unlock only when all three in that family are complete. Hints/undo never block achievements.

Case replay preserves prior completion and can record another legitimate normalized solution class only if implementation can map it safely; undiscovered classes are never shown as empty silhouettes or completion pressure.

### Contradiction found
Commercial language calls `Completing all 24` canonical campaign completion, but 2-of-3 progression permits reaching later families while skipping cases. A final capstone clear therefore needs a separate state from 24/24 completion.

### Repair
Define:
- `FINAL_CASE_CLEARED` = FC24 complete;
- `CAMPAIGN_COMPLETE` = all FC01–FC24 complete;
- credits/end celebration may trigger on first FC24 clear, but campaign completion achievement/100% family marks require 24/24;
- post-FC24 Case Select clearly shows remaining incomplete cases without shaming/score penalty.

Patch Commercial Model.

---

## 11. Steam Deck suspend -> cloud -> PC resume

### Sequence
1. On Deck in FC10/FC21 `EDIT_B`, player moves pieces but has not sprayed B.
2. Suspension hook persists valid editable snapshot plus latest committed checkpoint and flushes stable save revision.
3. Dynamic Cloud Sync transports semantic files.
4. PC loads same profile/content version, validates save and reconstructs exact `EDIT_B` arrangement.
5. Presentation starts from stable pose; no half-animation is synchronized.

### Semantic state
Profile monotonic sets merge normally. Puzzle branch retains same attempt lineage and greater checkpoint/snapshot revision.

### Friction attack
No contradiction if editable snapshot is required as repaired above.

### Resolution
**Resolved by technical patch from Walkthrough 6.**

---

## 12. Irreducible divergent-attempt cloud conflict

### Sequence
Deck and PC were both offline after common ancestor. Deck advances FC21 attempt A to post-A `EDIT_B`; PC resets FC21 and creates attempt B with a different A spray. Both later sync.

### Semantic state
Branches have distinct `attempt_id`; completion sets can union, but in-progress puzzle states cannot be spliced.

### Visible state
Conflict prompt appears only because material unsynchronized branches are irreducible. It shows semantic summaries, not timestamps alone:
- `This device: FC21 — between A and B`
- `Other device: FC21 — after Spray A`
with choice of branch. Completed-case union is preserved whichever attempt is selected.

### Friction attack
If the two branches are at apparently equal stage, player needs enough context to choose.

### Repair
Conflict summary may include stable factual metadata: case, stage, last committed coat, object arrangement thumbnail generated from that branch, and device label if platform exposes one. It must not compare which attempt is closer to solution.

Technical/UX authority can carry this to Phase 10; no rule change required.

---

## 13. Corrupt latest puzzle state / valid profile recovery

### Visible state
On launch, profile completion remains intact. Latest puzzle state fails checksum/semantic validation. Backup checkpoint is valid, so game reports: `Latest puzzle state could not be loaded. Resumed from the previous safe checkpoint.` Continue enters the recovered stage.

If editable snapshot alone is corrupt, discard it and recover the last spray checkpoint. If puzzle file is unrecoverable, discard only that in-progress attempt; never erase completion/settings with it.

### Semantic state
Profile and puzzle-state validity are separable. Unknown arrangement IDs are never approximated.

### Resolution
Existing Phase 8 policy resolves it. **No repair.**

---

## 14. Hostile behavior simulation

### Rapid pose cycling
Only certified legal poses are cycled. Rendering animations may coalesce/skip, but committed arrangement is always the most recently accepted semantic pose. No intermediate transform can be sprayed.

### Repeated Spray/Undo
Spray becomes unavailable immediately on transaction start. Transaction ID makes callbacks/idempotent recovery safe. Undo restores checkpoint; a rapid button repeat cannot append a coat twice.

### Modal double input
Opening Targets/Pause/confirmation consumes the triggering semantic action and blocks propagation into the newly opened modal. Closing a modal cannot also commit Spray or move a piece.

### Skipping one case per family
Allowed where destination cases do not depend on an uncompleted mandatory concept gate. Final case can be reached with incomplete earlier cases. 24/24 completion remains distinct from final-case clear.

### Hint use
Hints can name a proof fact but never a socket/pose. Achievement eligibility remains unchanged.

### Attempted brute force
Player can cycle legal arrangements and use factual exposure preview, but has no binary arrangement Check. Spray creates semantic consequences and branch cost only in attention/time, not resources. If observed testers systematically enumerate rather than reason, empirical gate E3 fails and affected case/content must be revised.

### Reset during transaction / animation
Reset is disabled during semantic Spray transaction. After transaction is durable, presentation can be skipped; Reset then creates a fresh attempt state atomically. No visual animation callback may mutate old attempt state.

### Input device switching mid-modal
Glyph update is presentation-only. Modal focus/selected semantic action remains stable.

---

## 15. Unlock graph — frozen Phase-9 interpretation

To eliminate prerequisite ambiguity, progression is modeled as predicates over stable completed-case IDs and concept tags.

### Family visibility/playability
- F1: available initially.
- F2: available after any 2/3 of F1.
- F3: available after any 2/3 of F2; individual F3 cases require FC03 complete because F3 assumes self-obligated masks.
- F4: available after any 2/3 of F3. FC10 itself is the two-pass teaching gate; cases in F4 that precede/lead to FC10 may remain accessible according to their authored tags, but no case requiring established two-pass reasoning may require the player to infer an untaught rule.
- F5: available after any 2/3 of F4 and FC10 complete. FC13 is the A_THEN_B teaching gate; FC14–FC15 require FC13.
- F6: available after any 2/3 of F5. FC16 teaches cavity semantics; FC17–FC18 require FC16.
- F7: available after any 2/3 of F6 and concept requirements inherited by their authored target tags.
- F8: available after any 2/3 of F7 and all concept gates required by each capstone (normally FC03, FC10, FC13, FC16).

### Authoring invariant
Each case package must explicitly list `prerequisite_case_ids` / concept requirement tags. UI family visibility is convenience; **case-level predicates are authority**. Therefore demo-imported later cases can remain complete without corrupting the graph.

### Continue invariant
Continue never uses `highest_case_id + 1`. It resumes in-progress state or chooses the lowest-display-order unlocked incomplete primary case, preferring a blocking mandatory gate when that gate is the only path forward.

---

## 16. Repairs required by this phase

Phase 9 found no contradiction in core mechanics, exposure truth, coat history, one-rearrangement ceiling, undo semantics, demo import identity, or cloud branch non-splicing. It found four specification gaps that must be patched upstream:

1. **Progression graph precision:** 2-of-3 is a family-flow convenience; case-level concept prerequisites are authoritative.
2. **Continue after demo import:** choose earliest unlocked incomplete/gate, never `highest completed + 1`.
3. **Editable-state persistence:** explicit exit/suspend/cloud hand-off must save the current valid editable arrangement snapshot in addition to the last spray checkpoint.
4. **Completion semantics:** FC24 clear and 24/24 campaign completion are distinct states.
5. **Late target readability:** FC21–FC24 target rail groups/collapses by object and selection synchronizes 3D region <-> target card.

These repairs do not reopen the game's product identity or mechanics.

---

## 17. Phase-9 conclusion

The complete shipped loop survives paper simulation from first boot through demo carry-over, two-stage interruption, ordered histories, cavities, role reversal, capstone, replay, suspend/cloud conflict, save corruption and hostile input behavior.

The largest discovered risk was not mechanical truth but progression ambiguity created by combining non-linear 2-of-3 advancement with mandatory concept gates and imported later demo completions. The repaired predicate model removes that contradiction without forcing a purely linear campaign.

No new gameplay mechanic is required.

PHASE 9 = COMPLETE
DESIGN COMPLETE = NO

## NEXT ACTION — PHASE 10 ADVERSARIAL REVIEW
Run dedicated destructive passes across the entire frozen Game #015 package. At minimum attack: fun/repetition after the novelty reveal; brute-force and exposure-preview over-assistance; four-object cognitive load; misleading renderer/semantic divergence; content freshness across all 24 cases; progression/gate/demo edge cases; hint leakage; accessibility parity; controller/modal races; save/undo transaction corruption; cloud branch conflicts; demo import duplication; achievement/progression idempotency; implementation ambiguity; scope creep; price/value risk; and empirical gates E1–E5/C1–C6. Produce explicit KEEP / PATCH / KILL findings. Patch upstream authority for any contradiction. If the game survives without unresolved design questions, advance to Phase 11 Specification Freeze.