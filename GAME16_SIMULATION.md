# GAME #016 — PHASE 9 WHOLE-GAME SIMULATION ON PAPER

Date: 2026-09-03
Status: PHASE 9 COMPLETE — no unresolved structural contradiction after simulation
Working title: **ONE-WAY WORKSHOP**
Authority simulated: all active Game #016 files through `GAME16_TECH_SPEC.md`.

## 0. Purpose and result
This run simulated the frozen game as a player-facing product and as a deterministic state machine without adding mechanics. The simulation covered first boot, demo, all campaign reasoning bands, hints, alternate-solution replay, controller/Deck-only play, accessibility modes, persistence, crash recovery, demo import, cloud merge, deliberate reset and hostile input.

**Result:** the frozen design survives end-to-end. No mechanic, campaign count, capability family, scope ceiling or commercial promise needs reopening. The main Phase-9 job is therefore validation and clarification rather than redesign.

Two implementation-clarity notes were exposed but do not alter puzzle design:
1. the technical spec already requires a reset-generation token for deliberate `Reset Campaign Progress`; implementation must include that token in the persisted profile model rather than treating it as an informal note;
2. the recommended 1.0 cloud policy is interpreted as **profile cloud-sync + active attempt local-only**. This is the only reading used in the simulations below because semantic merging of irreversible attempts is explicitly forbidden.

These are implementation clarifications consistent with Phase 8; Phase 10 should adversarially verify that the final freeze states them unambiguously.

---

# 1. First boot → OW01, mouse path

## 1.1 Boot
Player launches a fresh retail install with no profile and no compatible demo data.

Expected flow:
1. title/logo;
2. `Play` is primary;
3. accessibility quick settings are available but skippable: text scale, reduced motion, commit confirmation mode, controller glyph mode;
4. choosing Play creates profile + OW01 attempt and enters the workbench directly.

No lore wall, account creation, difficulty selection, currency tutorial or case-selection detour appears before the thesis interaction.

## 1.2 OW01 cold-state comprehension
Workbench shows one stock, one final rail slot, one spacing/drill requirement and one spacer cradle. The player receives the four-blocking-prompt budget only as needed.

Mouse path:
- hover stock → identity/capability summary;
- click stock;
- click first cut socket → exact two-child ghost preview;
- cancel;
- inspect second socket;
- observe that one preview leaves both the required rail and the small spacer-capable child;
- hold/single-confirm according to settings to commit;
- domain state changes atomically before split animation;
- byproduct becomes the most relevant post-cut focus target;
- drag/click child to spacer cradle; snap is discrete;
- execute guided spacing/drill operation with irreversible confirmation;
- dock rail into final slot;
- Certify.

Certification succeeds by final state predicates, not by matching the expected move string.

## 1.3 First wrong commit and restart
Simulated cold player intentionally takes the wrong OW01 cut after preview.

After atomic cut:
- no undo is offered across the fabrication commit;
- optimistic reachability proves the mandatory next jig capability unreachable;
- `Lineage broken` appears;
- failed requirement is highlighted;
- `Inspect cause` shows the spent parent/current children but not the correct socket;
- `Restart now` returns to the authored initial state without menu reload.

The tension survives because permanence is real, but experimentation is not punished by loading friction.

**Phase-9 finding:** first-session loop is coherent. Dead-state explanation and restart do not conflict with tutorial simplicity.

---

# 2. First boot → OW01, controller/Steam Deck path

Controller-only simulation begins at 1280×800 with Minimal overlay.

Path:
1. focus Stock Bay;
2. Select stock;
3. move one logical layer to cut sockets;
4. Preview socket A;
5. Cancel;
6. cycle to socket B;
7. Preview;
8. Confirm Commit using hold/double/single-confirm preference;
9. post-cut focus lands on the child with the strongest visible relation to the current station/plan;
10. shoulder action cycles compatible target to spacer cradle;
11. Select docks;
12. focus operation control;
13. Confirm Commit;
14. focus rail child/part slot;
15. dock;
16. Certify.

No analog cursor, tiny freehand drag, mouse fallback or camera precision is required. Dynamic glyph swap was also simulated: moving the mouse during preview changes displayed prompts but preserves semantic focus; returning to controller continues from the same preview state.

**Pass condition:** OW01 is fully completable with semantic actions. No puzzle truth depends on device mode.

---

# 3. Demo simulation — OW01 → OW03 → OW05 → D1

## 3.1 Knowledge state after OW01
Player should know:
- a cut is irreversible;
- both children are useful objects;
- a byproduct can be a jig;
- immediate child outcomes are previewable;
- certification judges the assembled result;
- restart is normal, not failure punishment.

The player is **not** yet expected to understand EDGE, cross-root dependency, consumption, PAIR or derived witnesses.

## 3.2 OW03 Small Wins
No new modal tutorial appears.

Player sees a large visually attractive child and a smaller keyed child after alternative cut previews. Plan/station geometry reveals that the small child is the only useful jig.

Simulated wrong path: preserve largest child. Dead-state can become provable when no keyed producer remains. Cause inspection says the required fit property cannot be produced, not “you should have taken Cut B”.

Knowledge after OW03: **size is not value; future capability matters.**

## 3.3 OW05 Reference Edge
First straight-edge property appears as physical fence silhouette + pattern/icon + optional text.

The player previews two cuts where one preserves more material while the other creates the usable straight guide. Dock preview visibly aligns the guide edge against the fixture.

Knowledge after OW05: byproducts can matter because of a **specific physical property**, not merely because they have the right span.

## 3.4 D1 cross-blank capstone
Two root lanes appear. Non-blocking copy: `A piece from either blank may become a tool for the other.`

Player must inspect future operation needs, then choose a cut on one blank whose child becomes a jig for the other blank. The logic remains within mechanics introduced no later than OW13, with <=4 commits.

The demo ends on successful certification followed by a completed-solution causal recap of the player's own sequence. Because the puzzle is already solved, showing that sequence does not violate anti-spoiler rules.

Expected end-state sentence: **“I cut that blank that way because the leftover became the guide another part needed later.”**

No late mechanics are spoiled.

**Demo result:** the four-case path forms a coherent escalation: immediate byproduct → property beats size → new property family → cross-blank dependency.

---

# 4. Retail first boot and demo-import matrix

## 4.1 No demo
Retail creates fresh profile. `cleared_jobs = {}`. Unlock evaluator returns only OW01. No import UI is shown.

## 4.2 Completed demo + empty retail
Compatible demo contains clears OW01, OW03, OW05 and D1.

Player chooses Import.

Merged retail records:
- OW01 cleared;
- OW03 cleared;
- OW05 clear record retained;
- `demo_capstone_seen=true`;
- tutorial flags OR-merged;
- settings imported only by explicit player choice;
- no D1→OW13 mapping;
- no in-progress demo attempt.

Unlock recomputation uses **retail reachability**, not downstream union from every clear bit.

Immediate retail availability:
- OW02 unlocked because OW01 is clear;
- OW03 already clear;
- OW04 unlocked because OW03 satisfies `OW02 OR OW03`;
- OW05 remains a recorded clear but does not yet make Tray-II B/C reachable because OW04 gate is not yet cleared.

After player clears OW04:
- OW05 becomes reachable and is already clear;
- therefore OW06 and OW07 unlock immediately.

The player never replays OW01/03/05, yet cannot skip OW04.

Achievement reconciliation:
- demo itself granted none;
- retail may grant `First Cut` from valid reachable OW01 clear after import/profile load;
- no later achievement is fabricated from D1.

## 4.3 Completed demo + existing retail
Example retail already has OW01, OW02, OW04, OW05, OW06 clear. Demo adds OW03 + D1 and preferences.

Clear union is monotonic; no existing clear disappears. Existing retail settings remain default choice. Demo import receipt prevents repeated identical mutation. Unlock graph is recomputed and remains valid.

## 4.4 Corrupt/incompatible demo
Retail boot continues normally. Import panel reports failure with Retry / Continue without import. No retail profile is overwritten. Detection remains read-only until Import.

## 4.5 Repeated import spam
Ten repeated imports of unchanged demo yield the same profile after the first successful merge. Receipt identity prevents revision churn or repeated achievement side effects.

**Pass:** demo carryover is deterministic and cannot bypass the campaign concept gates.

---

# 5. Early campaign simulation — OW01–OW08

## OW01–OW04 / Immediate Byproduct
The player graduates from forced offcut usefulness to choosing among plausible cut previews and rejecting “largest is best”. OW04 introduces one child compatible with multiple visible stations; `Fits now` remains neutral rather than strategic endorsement.

Bounded branch behavior:
- OW01 clear opens OW02 + OW03;
- either of those opens OW04;
- the unplayed sibling remains available;
- OW04 opens OW05.

This gives one escape route when stuck without allowing concept skipping.

## OW05–OW08 / Property Choice
OW05 introduces straight EDGE; OW06 keyed FACE; OW07 diagonal A/B and ANGLE witness; OW08 visible PAIR.

A simulated OW07 wrong branch creates the wrong diagonal family. The incompatible future station rejects it visibly with keyed geometry/pattern and optional text. If no alternative producer exists, optimistic dead-state warning is safe.

OW08 tests PAIR without secret identity: the matched sibling relationship is physically visible from the cut scar/notch. Player never needs an arbitrary piece ID.

## Early hint simulation
Example OW05 after 3 minutes post-commit:
- H1: focuses on future need for a straight guide;
- H2: points out that the guide may come from the child not chosen as final part;
- H3: says a usable straight edge must remain after the next fabrication stage.

No hint names a socket or action sequence. If a particular authored configuration leaves only one legal cut, the hint still describes the contradiction/property boundary rather than naming that cut.

**Early result:** the game has a readable learning ladder and no evidence that hints collapse the puzzle into instructions.

---

# 6. Midgame simulation — OW09–OW16

## OW09–OW12 / Delayed Lineage
OW09 preserves a child for two commits. OW10 uses a temporary jig and releases it for later reuse. OW11 explicitly punishes product-first reasoning. OW12 lets one piece move from temporary tool role to final part role.

### Dead-lineage recovery — OW11
Simulated player cuts the obvious product piece first. Three commits later, future angle/spacer producer is gone.

If optimistic closure proves no producer exists:
- `Lineage broken`;
- failed future requirement highlighted;
- backward trace points to the spent branch;
- player chooses Restart.

If competition makes death real but not provable by optimistic detector, **no warning appears**. Later certification can fail locally. This is acceptable and preserves zero-false-positive contract.

## Trace View
By OW09, ancestry is long enough to matter. Player holds Inspect on a future requirement. Current view shows:
- requirement;
- currently satisfying pieces, if any;
- relevant current/historical lineage;
- committed witness events;
- no future producer recipe.

After clear, the same Trace surface is allowed to show the player's full winning sequence.

## OW13–OW16 / Cross-Blank Ancestry
OW13 establishes B→A dependency. OW14 forms A→B then B→A. OW15 uses three roots but only one meaningful crossing chain. OW16 supports at least two validator-recognized solution families.

### Alternate valid family — OW16
Simulate family F1: root A supplies spacer, root B supplies straight edge.
Simulate family F2: root B supplies spacer, root A supplies straight edge.

Both satisfy the same final certification predicates and stay within commit ceilings. Certifier accepts both because it is state-based. Solution-family signature is coarse semantic allocation metadata, not raw move text.

On first clear, signature F1 is persisted. Replay and clear with F2; set now contains `{F1,F2}`. `Another Way` grants exactly once.

**Midgame result:** delayed reuse and cross-root ancestry increase proof depth without a new primitive action.

---

# 7. Late campaign simulation — OW17–OW24

## OW17–OW20 / Dual-Use Conflict
OW17: one child fits two stations; releasing use must precede consuming/locking use.
OW18: temporary occupation makes the child unavailable elsewhere until release.
OW19: one station consumes a unique child; substitute must be found for the other station.
OW20: two scarce children admit two valid allocation families.

The UI always labels temporary vs consume-on-operation before commit. Reversible docking cannot accidentally consume. Compatible-target cycling cannot rank the solver-preferred destination.

### Late hint example — OW19
H1: `One of the remaining operations will permanently consume its jig.`
H2: `The child that fits both stations does not have to serve both.`
H3: `Before the consuming operation, make sure the other station still has some compatible available child.`

Again no exact station order or cut socket is named.

## OW21–OW23 / Derived Witness Relay
The player creates a child whose base shape is insufficient, applies one guided witness, then uses that upgraded child as a future jig. Same-piece witness escalation remains capped; depth comes from relays across pieces.

OW23 simulation: root A byproduct enables an operation that marks/drills B child; upgraded B child then becomes the tool for C. Trace View shows A commit → B witness event → C operation as a bounded causal chain.

## OW24 six-commit capstone
Canonical seed: three roots, six fabrication commits, two cross-piece witness dependencies, no same-piece witness depth >1.

Paper route:
1. inspect final beam/brace requirements;
2. inspect station requiring prepared marked/holed template;
3. choose upstream cut preserving producer for that preparation jig;
4. commit first cut;
5. prepare intermediate child using another root's byproduct;
6. commit witness operation;
7. preserve separate diagonal template lineage for brace;
8. finish remaining cuts/operations within six-commit cap;
9. dock final parts;
10. Certify.

The exact micro-order is content-data authoring, but every required relationship already belongs to the frozen grammar.

### OW24 failure by resource competition
A player may preserve all *types* optimistically but allocate one unique dual-use child incorrectly. Because runtime dead-state analysis ignores competition, it may remain silent. This is correct: zero false positives outrank complete dead-state detection. Certification then identifies the unmet local requirement; Trace View shows where the scarce child was consumed/occupied. Restart remains immediate.

**Late result:** the capstone composes known rules rather than adding a seventh family or hidden mechanic.

---

# 8. Replay, Another Way and Trace the Work

## 8.1 Replay
Cleared case stays clear. Replay loads a fresh attempt but preserves progression. No grade, par, timer or no-hint badge appears.

## 8.2 Another Way
Only OW16/OW20 are baseline achievement candidates because they are explicitly validator-authored for alternate family signatures.

Rules simulated:
- same family repeated ten times does nothing;
- different exact move ordering that maps to the same semantic family does not count twice;
- first validated family + second distinct validated family across clears grants achievement;
- hints/accessibility do not block it.

## 8.3 Trace the Work
After any cleared OW09+ case, player opens completed causal recap and traverses all commit nodes. Boolean persists. Achievement grants idempotently.

Opening Trace before clear does not satisfy the achievement because future solution cannot be shown and the contract specifically asks for a complete cleared-case causal recap.

---

# 9. Persistence simulation — late case at every commit boundary

Use OW24 with six commits. Let stable domain states be `S0..S6`.

For each irreversible commit `Ci`:
1. command validates against `S(i-1)`;
2. domain creates complete `Si` atomically;
3. semantic trace event appended;
4. dead-state evidence recomputed;
5. durable attempt save writes `Si`;
6. presentation animates toward `Si`.

## 9.1 Crash before domain commit
Crash while still in preview/confirmation. No trace event/save mutation exists. Reload returns previous stable state.

## 9.2 Crash after domain commit, before animation completes
Durable state is already `Si`. Reload reconstructs presentation from `Si`; parent is spent, children/witness/consumption exactly match committed truth. No half-cut state can appear.

## 9.3 Crash during temp-save write
Primary remains previous valid file; temp is ignored or validated separately. Backup chain retains known-good copy. At worst the most recent complete transaction may require replay if replacement never completed; no corrupted hybrid is accepted.

## 9.4 Corrupt attempt / valid profile
Discard only attempt and restart current case. Cleared jobs, hints, settings and achievements remain.

## 9.5 Corrupt profile / valid backup
Newest valid backup restores. Invalid primary is preserved for support and not allowed to overwrite backup.

## 9.6 Incompatible content revision
If logical job data changed incompatibly, old attempt is not silently reinterpreted. Preserve profile clears; discard/restart or explicitly migrate only the attempt.

## 9.7 Reversible docking and safe exit
Docking is reversible and need not persist after every movement. If player explicitly exits/pauses through a safe transition, current stable docking may be saved for convenience. Losing an unsaved reversible rehearsal after a crash does not alter any committed fabrication truth.

**Persistence result:** irreversible semantics survive all transaction boundaries.

---

# 10. Cloud/profile merge simulation

Baseline Phase-9 interpretation for 1.0: **profile is cloud-synced; active attempt remains local-only.**

## 10.1 Disjoint clears
Local `{OW01,OW02}`; incoming cloud `{OW01,OW03}`. Merge → `{OW01,OW02,OW03}`. Unlock graph recomputed. No timestamp can discard either clear.

## 10.2 Stale newer-timestamp profile with fewer clears
Local has 12 clears. Incoming has 8 but a later file timestamp. Result keeps union of all 12+ valid unique clears; timestamp is not progress authority.

## 10.3 Portable settings conflict
Progress union happens regardless. If trustworthy last-user-edit metadata exists, deterministic policy may select settings. Otherwise prompt `Use local settings / Use cloud settings`. Machine-local resolution/display settings do not participate.

## 10.4 Corrupt incoming cloud profile
Reject incoming file; retain valid local; do not overwrite the only valid profile.

## 10.5 Active attempt on machine A, profile progress from B
A's OW20 attempt remains local. B clears another case and cloud profile merges to A. Attempt state is not semantically merged or replaced. If newly merged profile marks current case already cleared, attempt may still be resumed or discarded by UX; its branch truth remains local and intact.

## 10.6 Deliberate Reset Campaign Progress
This is the one destructive profile operation and therefore cannot use ordinary set-union semantics blindly.

Simulation contract:
- explicit confirmation creates a new reset generation token/profile generation;
- new generation starts with no campaign clears while preserving only settings that the reset UI promises to keep;
- stale cloud data from the older generation cannot silently resurrect old clears;
- if cloud has a genuinely different/newer generation, preserve both until explicit conflict resolution;
- reset does not need to revoke platform achievements already granted; achievements remain platform history while campaign progression starts fresh.

**Phase-9 clarification:** the generation token must be a real persisted field in implementation, even though the Phase-8 conceptual `CampaignProfile` code block omitted it while later text required it.

---

# 11. Controller/Deck-only hardest-case traversal

OW24 semantic-focus stress simulation:

Starting at Overview, player must be able to reach:
- any of three root lanes;
- each currently relevant child;
- <=5 cut sockets on focused piece;
- each compatible jig/part slot;
- Plan Rail requirement;
- Trace View;
- hint panel;
- Restart;
- Certify;
- Settings.

Navigation uses zone first, then logical siblings/layers, with `Cycle Compatible Targets` as a direct relation shortcut. No local cycle may exceed the frozen limits. A selected child that fits two stations exposes both in stable spatial/plan order.

Simulated full action path includes preview, irreversible cut, temporary dock, operation commit, release, witness inspection, part dock, hint inspection, Trace View, restart, settings change and final certification without touching a mouse.

Device switch mid-preview or mid-bench does not reset focus.

During atomic commit, device input changes may update future glyph presentation but cannot inject a second semantic commit.

**Pass:** hardest-case control surface remains bounded by semantic IDs rather than 3D cursor skill.

---

# 12. Accessibility-mode simulation

## 12.1 Low-information mode
Minimal overlay; player relies on physical form + focused card + station silhouette. No required rule is hidden because every capability has physical/symbol redundancy.

## 12.2 High-information mode
All loose pieces show capability badges and station requirements. This increases external memory support but does not reveal future producers or rank moves. Puzzle truth is unchanged.

## 12.3 Reduced motion
Cut/operation/certification presentation shortens; camera sweeps removed; split state appears from the same domain transaction. Resulting canonical state/hash matches normal motion.

## 12.4 Commit variants
Three equivalent safety paths:
- hold Confirm;
- double press;
- single press after explicit confirmation banner.

They all dispatch exactly one semantic commit. None changes output, timing puzzle or achievement eligibility.

## 12.5 Text scale/color independence
At 150% text, cards must reflow. DIAGONAL A/B, consume/release and pass/fail remain identifiable by keyed geometry/pattern/icon without color.

**Accessibility result:** assists modify information density and interaction burden only.

---

# 13. Hostile-player simulation

## Repeated invalid docking
Player slams every piece into every incompatible station. Result: clean non-commit rejection + missing visible requirement. No penalty, hidden state or hint timer exploit.

## Certification spam
Repeated Certify on incomplete state repeatedly returns stable first local unmet requirement. It cannot mutate the attempt or reveal future solver information.

## Restart spam
Restart after first commit always creates a fresh authored attempt. Profile/tutorial/hint state persists. Repeated restart can unlock hint availability after two restarts as designed; this is an intentional accessibility path, not an exploit affecting certification.

## Input switch mid-commit
Once semantic commit is accepted, input is frozen for transaction/presentation gate. Mouse/controller switching cannot duplicate the command. Glyphs can refresh afterward.

## Quit at transaction boundaries
- before accepted commit: old stable state;
- after accepted domain commit but before animation: new stable state;
- during safe-exit save: atomic file procedure prevents hybrid state.

## Repeated demo import
Receipt makes unchanged import idempotent.

## Replay cleared cases
No clear is removed. Replays may add recognized solution-family signature or Trace achievement state; no progression regression.

## Reversible docking exploit
Player parks a dual-use jig in a temporary station to inspect other consequences. This is allowed rehearsal. If station operation has not committed, undocking remains reversible. No capability is duplicated because a piece can occupy only one place.

## Consumption ordering exploit
A consuming operation validates actual current occupancy and atomically marks the jig consumed. The same piece cannot satisfy a second station afterward. Historical silhouette remains trace-only and cannot be selected as a live tool.

## Preview brute force
Player may inspect every legal cut preview. This is explicitly allowed. Preview exposes immediate exact children but never future solver verdict, so the game remains a planning puzzle. Authoring rules keep socket count <=5 and require human proof routes so enumeration is not the only intended method.

## Save tampering
Unknown IDs/invalid bounds are rejected; unlocks are recomputed. Self-granted valid clear bits are not treated as a security threat because the game has no leaderboard/economy.

**Hostile result:** no mutation path was found that duplicates material, reverses a committed fabrication action, leaks a hidden future solution, or regresses monotonic normal progress.

---

# 14. H1/H2/H3 anti-spoiler audit across early/mid/late

Three representative jobs were simulated.

### Early — OW05
- H1 future requirement focus;
- H2 byproduct-property relationship;
- H3 required EDGE class survival.
No socket named.

### Mid — OW14
- H1 calls attention to a later requirement on the opposite root;
- H2 states that finishing one blank independently can destroy the cross-root dependency;
- H3 says each root must still have a producer for the other root's required capability after the next stage.
No first-root prescription or cut ID.

### Late — OW23
- H1 says a future jig needs a witness it does not yet have;
- H2 says another piece may be required to prepare that jig before it can serve its final role;
- H3 identifies the witness/property boundary that must remain producible before the relay advances.
No exact producer, socket or sequence is named.

**Audit result:** hints can express causal proof structure while preserving player agency.

---

# 15. Contradiction / ambiguity audit

## 15.1 No structural contradiction found
The following remain mutually consistent:
- exactly 24 canonical campaign cases + D1 as demo-only capstone;
- <=3 roots, <=6 committed fabrication operations, <=8 loose children;
- finite visible cut sockets only;
- one-jig guided operations;
- state-based certification;
- zero-false-positive optimistic runtime dead-state warning;
- irreversible commit + near-instant restart;
- bounded branching progression;
- demo imported clear records without prerequisite bypass;
- hints/accessibility do not change puzzle truth;
- active attempt truth remains separate from cloud profile progression;
- achievements are consequences, never progression authority.

## 15.2 Clarification to carry into Phase 10/freeze
Two implementation details should be made explicit in final authority if Phase 10 confirms them:
1. `CampaignProfile` persisted schema includes `reset_generation` (or semantically equivalent token) because Section 23 already requires it for deliberate destructive reset.
2. 1.0 baseline cloud policy is profile/backups + portable settings only; `attempt.json` is local-only. Cross-device attempt continuation is out of baseline unless a later implementation gate deliberately reopens only that platform behavior without semantic merge.

Neither item adds a mechanic or changes player-facing puzzle design.

## 15.3 Empirical gates remain
Paper simulation cannot prove:
- discrete cutting feels tactile rather than menu-like;
- Trace View is understood quickly on Deck;
- D1 cold-player causal comprehension >= target;
- 24 cases achieve 4.5h+ median without filler;
- H3 never feels answer-like in real authored layouts;
- controller navigation meets <=6-input practical expectation under final presentation;
- $12.99 value perception.

These remain implementation/playtest gates, not design unknowns.

---

# 16. Phase-9 acceptance checklist

- first boot + OW01 mouse: **PASS**
- first boot + OW01 controller/Deck: **PASS**
- exact demo path + knowledge progression: **PASS**
- no-demo / demo-empty-retail / demo-existing-retail / corrupt demo: **PASS**
- early campaign + bounded branching + dead-lineage recovery: **PASS**
- midgame Trace View / delayed reuse / cross-root / alternate family: **PASS**
- late occupation/consumption / witness relay / OW24 six-commit composition: **PASS**
- H1/H2/H3 early/mid/late anti-solver rule: **PASS**
- replay / Another Way / Trace the Work: **PASS**
- save/load every late commit + crash boundaries + corruption + revision mismatch: **PASS**
- cloud union / stale regression / settings conflict / corrupt incoming / reset generation: **PASS with clarification noted**
- hardest-case controller-only path: **PASS at design level**
- low/high-information overlays + reduced motion + commit variants: **PASS**
- hostile behavior suite: **PASS**
- unresolved structural contradiction: **NONE**

## Phase-9 conclusion
**PHASE 9 WHOLE-GAME SIMULATION ON PAPER COMPLETE.**

The game survived an end-to-end product/state-machine simulation without requiring new mechanics or scope expansion. The two technical clarifications above should be attacked explicitly in Phase 10, along with fun/repetition, dominant strategies, scope creep, certification ambiguity, dead-state false-positive risk, hint leakage, persistence/reset conflict semantics, content exhaustion, accessibility and implementation ambiguity.

NEXT: **Phase 10 — Adversarial Review.** Run destructive review passes across fun, repetition, dominant strategies, mechanical redundancy, scope/asset burden, content exhaustion, UX ambiguity, accessibility, certifier/dead-state behavior, hints, save/cloud/reset integrity, demo/commercial promise and implementation ambiguity. Patch only demonstrated problems; do not add new mechanics to manufacture novelty.