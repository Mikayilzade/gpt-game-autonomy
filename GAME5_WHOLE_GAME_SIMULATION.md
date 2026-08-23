# GAME #005 — WHOLE-GAME SIMULATION ON PAPER

Last updated: 2026-08-23
Factory run: **10 — extended pass**
Phase: **9 — Whole-Game Simulation on Paper**
Selected concept: **G5C02 — Tension Budget**
Production implementation: **NOT STARTED**

# PHASE 9 STATUS = COMPLETE WITH REPAIR ITEMS FOR PHASE 10

This pass walks the intended product from first boot to late-game replay and hostile runtime behavior. It intentionally looks for contradictions between previously frozen phases rather than assuming the documents are mutually consistent.

---

# 1. First boot / first launch simulation

## 1.1 Boot
Player launches the game for the first time.

Expected path:
1. small title screen;
2. Continue absent / New Game primary;
3. Settings immediately available;
4. controller or keyboard prompts switch through input abstraction;
5. no account/login/network requirement;
6. player enters E01 within a short load.

Result: **coherent**.

No commercial/account system conflicts with the offline thesis.

## 1.2 Accessibility-before-play
Player opens settings before New Game and enables:
- reduced motion;
- larger UI scale;
- optional state labels;
- low/zero vibration;
- subtitles/captions;
- remapped Interact and Restart.

Expected behavior:
- settings persist separately from campaign profile;
- no achievement or progression penalty;
- mechanics remain unchanged;
- state labels show SLACK/TAUT/HIGH only, not internal quanta.

Result: **coherent**.

---

# 2. E01–E03 / first literacy simulation

## 2.1 Intended E01 from Phase 5
Current skeleton says:
- E01 `First Pull`;
- **1 Lift**;
- 3 snap bands;
- no mutation;
- primary S01.

### Mathematical audit
Phase 4 says:
- total budget `B` is conserved across all bands;
- every quantum is 0/1/2;
- adjacent bands transfer exactly one quantum **from one load to another**;
- no duplicate bands;
- normal rig scale uses 2–4 active loads.

With only one active load, a fixed `B` gives exactly one possible vector for that revision. A one-load rig therefore cannot possess three unique conserved bands, and cannot transfer one quantum between two loads because a second load does not exist.

**CONTRADICTION P9-C01 — FATAL UNTIL REPAIRED.**

E01 as currently written is mechanically impossible under Phase-4 canon.

### Correct design direction
Do not weaken conservation/adjacent-transfer for a tutorial exception. Instead E01 must contain at least two loads. The second load may be non-completion-critical in the first teaching beat, but it must visibly participate in the same rig so the player learns the actual product rather than a fake one-load precursor.

## 2.2 E02 Give / Take
Lift + Gate, 3 bands.

A valid conserved example exists with `B=2`:
- [2,0]
- [1,1]
- [0,2]

Adjacent transfer holds, all bands are distinct, visual give/take is clean.

Result: **coherent and likely strong as the true first mechanical grammar.**

## 2.3 E03 Middle Holds
Lift + Span, 3 bands, `B=2` can use the same three-vector pattern.

TAUT/TAUT creates the clear middle compromise.

Result: **coherent**.

---

# 3. First 20–30 minutes / onboarding promise

After repairing E01 to use two loads, the first-session promise can proceed:
- direct cause/effect within 60–90 sec;
- give/take within 5–8 min;
- middle TAUT proof soon after;
- first traversal-separated reconfiguration before interaction feels like a slider.

### Risk
If E01 and E02 both use Lift+Gate with identical 3-band vectors, the campaign could feel like repeating the same tutorial twice.

Repair direction:
- E01: Lift is completion-critical; Gate is visibly responsive but its passage is irrelevant/locked away from the exit. One required pull teaches world response.
- E02: both Lift and Gate are completion-critical, forcing a real choice.

This keeps rules honest while differentiating cognitive demand.

Result after bounded repair: **coherent**.

---

# 4. Demo simulation

Phase 5 demo:
- D01 Lift+Gate give/take;
- D02 Lift+Span middle compromise;
- D03 3-load traversal-separated decision;
- D04 3-load mutation + return inversion.

D01–D03 are structurally viable.

D04 requires deeper state-space audit below because a 3-load removal mutation can produce an impossible post-mutation revision if snap count/budget are not constrained.

Commercial promise remains valid if D04 uses a mathematically legal mutation template.

---

# 5. Finite distribution-state audit

The technical preflight from Phase 8 was applied analytically to the frozen 0/1/2 conserved state model.

## 5.1 One active load
For fixed `B`, exactly **1** legal vector exists.

Therefore:
- any 3–5 band revision with one active load is impossible;
- this confirms P9-C01.

## 5.2 Two active loads
Maximum distinct legal vectors by budget:
- B=0 -> 1
- B=1 -> 2
- **B=2 -> 3**
- B=3 -> 2
- B=4 -> 1

The adjacency graph under the exact one-quantum transfer rule can traverse all three B=2 states:
[2,0] <-> [1,1] <-> [0,2].

Therefore a two-load revision can support **at most 3 snap bands**, and only when `B=2` if all bands must be distinct.

This is a critical design bound not previously stated explicitly.

## 5.3 Three active loads
Legal-vector count by B:
- B=1 -> 3
- B=2 -> 6
- B=3 -> 7
- B=4 -> 6
- B=5 -> 3

The useful central budgets can support 3–5 snap bands.

## 5.4 Four active loads
Central budgets have ample state count for the frozen 3–5 snap bands. Exact authored paths still require V03 adjacency validation.

---

# 6. Mutation audit — 3 loads to 2 loads

Phase 4 default says pre-objective `B = number of active loads`, therefore a normal 3-load pre-revision defaults to `B=3`.

If one load is removed:
- post-revision has 2 loads;
- fixed B remains 3;
- only two legal vectors exist: [2,1], [1,2].

But normal snap count is 3–5 and duplicate bands are forbidden.

Therefore **a default-B 3->2 removal mutation cannot produce a legal 3–5 band post-revision.**

**CONTRADICTION P9-C02 — FATAL UNTIL REPAIRED.**

This affects any content/prototype that assumes a 3-load, 4/5-band rig can simply remove one load while keeping all Phase-4 rules.

## 6.1 Legal narrow 3->2 pattern
A legal 3->2 removal is possible if:
- snap count = **3**;
- fixed B = **2** rather than default 3;
- post-revision uses [2,0], [1,1], [0,2];
- pre-revision uses three legal 3-load vectors summing to B=2 connected by one-unit adjacency.

This is a valid authored exception to the Phase-4 *default budget convention*, not an exception to conservation.

## 6.2 Why this repair is preferable
Do not:
- allow duplicate snap bands;
- change total B on mutation;
- violate 0/1/2 bounds;
- create hidden fourth states;
- disable adjacency transfer.

Those would damage core readability.

---

# 7. Mutation audit — 2 loads to 3 loads

A two-load pre-revision with B=2 supports at most 3 unique bands.

Therefore current E17 wording `Lift + Gate; +Span`, **4 bands**, add Span is also impossible before the mutation.

**CONTRADICTION P9-C03 — FATAL UNTIL REPAIRED.**

A 2->3 add mutation is legal with exactly 3 snap bands / B=2.

For 4–5 band add mutations, start with 3 loads and add the fourth, preserving a central B such as 3.

---

# 8. Audit of mutation-era campaign skeleton

## E16 Counterweight Gone
Current: 3 loads, 4 bands, remove Gate.

Result: **INVALID** by P9-C02.

Repair options:
A. 3 loads ->2, **3 bands / B=2**; or
B. 4 loads ->3, 4 bands / central budget.

For first mutation teaching, A is cleaner.

## E17 New Span Joined
Current: 2 active loads ->3, 4 bands.

Result: **INVALID** by P9-C03.

Repair: **3 bands / B=2** for the first addition lesson.

## E18 Return Inversion I
Current: 3 loads, 4 bands, remove a Lift/Gate instance.

Result: **INVALID** if it becomes 2 loads.

Repair direction: start with **4 loads ->3 loads**, 4 bands. This raises complexity at an appropriate late-Band-D point and avoids another 3-band mutation tutorial.

## E19 Mutation Mid-Route
Current: 3 loads, 5 bands, add/remove one.

Removal 3->2 is invalid; addition 3->4 can be legal.

Repair: **ADD only, 3->4, 5 bands**.

## E20 Revision Relay
Current: 3->2 or 3->4, 5 bands.

3->2 invalid; 3->4 potentially legal.

Repair: **ADD only, 3->4, 5 bands**.

## E22 Twin Family Mutation
Current metadata is underspecified about direction.

Repair rule: if snap count is 5, mutation must remain in a state-space-capable family such as **3->4 add or 4->3 remove**. Do not use 3->2.

## E24–E26
Four-load late encounters with one mutation can legally use **4->3 removal** under an appropriate central B, subject to actual V01–V04 path validation.

---

# 9. Empirical prototype simulation

Phase-3 Product Thesis currently asks the one-week prototype to contain:
- one short **4-position** anchor rail;
- Lift + Gate + Span;
- one load-removal + return-inversion encounter.

If this means one 3-load 4-band rig that removes to 2 loads, it is impossible under the frozen state model.

**CONTRADICTION P9-C04 — prototype brief is internally invalid.**

Repair direction:
Use three small prototype encounters, each testing one existential question:
1. **P-A Give/Take** — 2 loads, 3 bands, B=2.
2. **P-B Mature Traversal** — 3 loads, 4 bands, central conserved budget, no mutation.
3. **P-C Mutation/Return** — 3 loads ->2 loads, **3 bands, B=2**.

This actually tests more of the thesis and keeps every fixture legal.

---

# 10. Band A–C whole-campaign simulation

Assuming E01 repair:
- E01–E03 establish conservation/middle state honestly;
- E04–E10 move from final-choice to sequence/space;
- E11–E15 introduce same-family competition and commitment.

Potential repetition cluster:
- E06/E09 both middle-state 3-load problems;
- E08/E14 are relay-like;
- E11–E13 consecutive repeated-archetype family lessons can feel curriculum-like.

Phase 5 already says repeated-family encounters should be separated or strongly differentiated, but skeleton still lists E11/E12/E13 consecutively.

**P9-R01 — REPETITION RISK, NOT CONTRADICTION.**

Phase 10 should either reorder one of E11–E13 or explicitly require materially distinct secondary signatures/camera/region structure.

---

# 11. Band D simulation after mutation repairs

A strong revised order can teach:
1. 3-band 3->2 removal;
2. 3-band 2->3 addition;
3. 4-load ->3-load return inversion;
4. 3->4 mid-route addition under 5 bands;
5. 3->4 revision relay.

This creates a clean complexity curve:
- first learn revision change under minimal state space;
- then experience higher-snap-count mutation only after the idea is understood.

Result after repair: **stronger than original skeleton**.

---

# 12. Band E / late-game simulation

E21–E26 use four loads and synthesis.

Main risks:
- 5-band 4-load state can look visually dense;
- repeated mutation/return inversion could become the dominant late-game pattern;
- 3–4 required commits are acceptable only if each changes a qualitatively different traversal commitment.

No new mechanic is needed.

Late-game content should preserve at least one pure no-mutation mastery encounter so mutation does not become a mandatory novelty crutch. Phase 5 already requires this.

Result: **coherent with repetition monitoring**.

---

# 13. First hour simulation

Player likely reaches roughly E05–E08 depending on solve speed.

Desired emotional/cognitive progression:
- “I pull the machine.”
- “Pulling here changes something else.”
- “Middle can be right.”
- “I need to cross first, then pull again.”

No resource system or story exposition interrupts mastery.

Potential commercial issue: if carriage travel/animations are too slow, repeated 2–4 commits per encounter can create friction.

Already covered by U03 / empirical <=2–3 sec grab-to-commit target.

Result: **coherent**.

---

# 14. Midgame session / resume simulation

Player exits during E12 after reaching a dead end.

CurrentRunSave stores latest C0 because no mutation.

On resume:
- encounter loads at C0;
- solved partial navigation is not resumed exactly;
- campaign completion remains intact.

This is acceptable for 5–9 minute puzzles and protects deterministic restoration.

After mutation in E18, quit after C1:
- restart/resume returns to C1;
- player does not repeat entry half.

Result: **coherent and humane**.

---

# 15. Pause during transition

Player pauses while Lift is moving after commit.

Required:
- gameplay processing and presentation transition both pause coherently;
- no domain timer continues;
- no stale completion event fires under pause;
- resume continues same transition epoch.

Technical spec supports this. Implementation integration test required.

Result: **coherent if process-mode policy is explicit in implementation**.

---

# 16. Quit during preview

Player holds carriage between bands and Alt-F4/quits.

No preview state is durable.

On return:
- latest C0/C1 reloads;
- committed band from checkpoint is restored;
- no in-between rail coordinate persists.

Result: **coherent**.

---

# 17. Quit during committed transition

Player quits after anchor commit but before loads visually settle.

Baseline current-run durability is checkpoint-level, not arbitrary mid-encounter save.

On resume:
- C0/C1 restore may lose the most recent unsaved local attempt;
- puzzle truth cannot become half-transition.

For short puzzles this is acceptable. A future implementation may save stable commit state after transition, but it is not required for freeze.

Result: **coherent**.

---

# 18. Quit during mutation

Mutation is not durably promoted until stable C1 exists.

If application terminates mid-mutation:
- on next launch use previous durable C0;
- do not reconstruct half-detached loads.

Once C1 write succeeds, it becomes durable.

Result: **coherent**.

---

# 19. Restart spam / stale callbacks

Player commits, instantly requests restart, then rapidly repeats.

Technical spec `transition_epoch` invalidates stale presentation callbacks.

Required invariant:
- no old animation completion can set STABLE or load state after a newer restart epoch;
- derived state always reconstructs from current checkpoint.

Result: **coherent and testable**.

---

# 20. Controller disconnect

Controller disconnects:
- during ordinary movement -> pause or prompt safely;
- during carriage preview -> freeze/cancel behavior must be deterministic; safest baseline is pause and retain preview presentation until input returns or explicit device fallback, without committing;
- during mutation/transition -> world can pause; no input is required.

Implementation choice may auto-pause on last-controller disconnect. It cannot commit a nearest band merely because the controller vanished.

Result: **implementation-flexible but rule clear enough**.

---

# 21. Reduced-motion simulation

Player enables reduced motion mid-campaign.

Stable logic remains identical.

Important test:
- Gate/Span traversal conditions query stable semantic state, not animation percentage;
- Lift still needs deterministic rider transport even if travel is shortened;
- solution graph from validator is unchanged.

Result: **coherent**.

---

# 22. Muted play simulation

Audio at zero:
- snap detents remain visible;
- cable posture + hardware tab + load silhouette communicate state;
- objective mutation has visual physical cause;
- off-screen change uses world/camera/edge cues rather than sound only.

Result: **coherent; U08 remains empirical QA gate**.

---

# 23. Corrupt CurrentRunSave

Current-run file fails schema/checksum/parse validation.

Expected:
- preserve ProfileSave;
- quarantine/ignore invalid CurrentRunSave;
- resume selected encounter from C0 or last safe campaign node;
- communicate recovery without implying campaign loss.

Result: **coherent**.

---

# 24. Corrupt ProfileSave

More serious case.

Technical spec allows previous known-good backup where filesystem permits.

Required priority:
1. validate primary profile;
2. attempt backup;
3. never overwrite corrupted files during failed recovery;
4. if unrecoverable, show explicit recovery error rather than silently starting New Game.

Final implementation details remain technical, not gameplay design.

Result: **coherent**.

---

# 25. Alternate solution simulation

A player finds a valid 3-commit solution where intended is 4.

Policy:
- if all frozen rules, safety and signature goals hold, alternate solution can be accepted;
- do not patch merely because the player was clever;
- validator records alternate signature;
- achievement may optionally recognize selected authored alternates but is not required.

Result: **coherent**.

---

# 26. Hostile enumeration simulation

Experienced player grabs carriage and cycles every band.

Early teaching: acceptable.

Mature content:
- preview is honest;
- player can learn local consequences;
- important later decision is separated by traversal/mutation/anchor access;
- no attempt economy punishes experimentation.

Result: **coherent only if V11–V13 actually reject static lookup-table encounters.**

This remains an authoring/validator existential risk, not a rules contradiction.

---

# 27. Achievement / commercial simulation

Player uses accessibility labels and reduced motion, completes campaign.

Achievements remain active.

No monetization or progression path depends on retries/move counts.

Working price promise relies on 26 high-quality encounters, not optional remixes.

Result: **coherent**.

---

# 28. Demo/full-build technical separation

Demo must use the same Domain Core and load contracts.

Recommended architecture:
- shared source/content schema;
- separate `DemoProgressionDefinition` and demo encounter definitions or explicitly versioned variants;
- no forked simplified simulation code;
- no save leakage that marks retail encounters completed accidentally.

Result: **coherent**.

---

# 29. Commercial-title simulation

`Tension Budget` remains an internal concept label and may sound technical/store-unfriendly.

This does not block mechanical freeze if naming is explicitly implementation/commercial-flexible, but migration needs a stable dedicated repository slug.

Recommended migration fallback if commercial title is still undecided:
- repo slug `tension-budget` as internal project name;
- later commercial rename may change store/title presentation without changing gameplay canon.

This mirrors a safe distinction between project identity and final market title.

Result: **not a design blocker**.

---

# 30. Phase-9 contradiction ledger

## Fatal contradictions requiring Phase-10 amendment

### P9-C01 — one-load E01 impossible
One active load cannot support 3 unique conserved bands or adjacent give/take.

### P9-C02 — default 3->2 removal impossible at 3–5 bands
With pre B=3, post two-load revision has only two legal distinct states.

### P9-C03 — 2->3 addition with 4 bands impossible
Two-load B=2 pre-revision supports only three distinct bands.

### P9-C04 — original 4-band empirical mutation prototype impossible
Three loads -> two with four bands conflicts with conserved bounded vectors/no duplicates.

## Non-fatal repair/risk items

### P9-R01 — E11/E12/E13 repetition cluster
Three repeated-archetype lessons are consecutive in skeleton.

### P9-R02 — mutation direction underspecified in late content
5-band mutation encounters must avoid low-load revisions that cannot support 5 distinct states.

### P9-R03 — controller disconnect while previewing needs deterministic pause/cancel policy
No auto-commit on disconnect.

### P9-R04 — profile corruption recovery deserves explicit implementation acceptance tests
Not a gameplay redesign.

---

# 31. Phase-9 decision

The core selected product survives whole-game simulation. The contradictions are **discrete authoring/math inconsistencies**, not evidence that the Tension Budget thesis fails.

Crucially, the repairs can preserve all valuable rules:
- fixed conserved budget;
- 0/1/2 states;
- one-quantum adjacent transfer;
- no duplicate bands;
- honest nonnumeric presentation;
- no fourth load family;
- no new player mechanic.

Therefore:

**PHASE 9 WHOLE-GAME SIMULATION = COMPLETE, WITH MANDATORY PHASE-10 AMENDMENTS.**

Phase 10 must formalize the finite-state feasibility rule, repair the campaign/prototype metadata, re-attack repetition/scope/accessibility/persistence and decide whether any remaining ambiguity prevents Phase 11.