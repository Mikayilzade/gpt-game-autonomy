# GAME #005 — CONTENT ARCHITECTURE

Last updated: 2026-08-23
Factory run: **9 — extended pass**
Phase: **5 — Content Architecture**
Selected concept: **G5C02 — Tension Budget**
Commercial title: **TBD**
Production implementation: **NOT STARTED**

# PHASE 5 STATUS = COMPLETE

This file converts the frozen Product Thesis and Mechanical Architecture into a bounded, validator-driven content plan. It does not add a fourth load archetype, movement pillar, hidden tension rules, free rope simulation, multiple independent carriages, or a second gameplay system.

---

# 1. Content north star

A valid encounter must make the player answer a spatial version of this question:

> **Which temporary distribution do I want now, knowing that reaching the next place or changing the rig will make a different distribution valuable later?**

Geometry, visual theme and fiction may refresh presentation, but they may not masquerade as new mechanical depth.

The 1.0 campaign target remains:
- **24–28 main encounters**;
- working target **26**;
- roughly **4–6 hours** first completion;
- no obligation to pad beyond the proven reasoning ceiling.

---

# 2. Content vocabulary ceiling

## 2.1 Load archetypes
Only:
1. **Lift**
2. **Counterweighted Gate**
3. **Flexible Span**

Repeated instances are legal. Mirroring/orientation/landing arrangement may vary. A fourth load family is forbidden in the planned 1.0 campaign.

## 2.2 Rig scale
Per encounter:
- 1 carriage rail;
- 3–5 snap bands;
- 2–4 active loads;
- 0 or 1 irreversible visible load mutation;
- one fixed conserved budget `B` across every rig revision;
- adjacent snap bands differ by exactly one 1-quantum give/take transfer.

## 2.3 Player vocabulary
Only ordinary traversal, local carriage grab/slide/release, objective interaction and restart/checkpoint. Content may not depend on jump/dash/crouch/combat/precision timing.

---

# 3. Reasoning-signature taxonomy

Every main encounter must declare one **primary signature** and up to two secondary signatures.

### S01 — Direct redistribution
One move clearly improves one load while weakening another. Teaching only.

### S02 — Collateral tradeoff
Two simultaneously useful routes cannot both be maximized; player chooses a temporary priority.

### S03 — Middle compromise
TAUT is required; SLACK and HIGH both fail the intended route.

### S04 — Local equivalence / global consequence
Two bands solve the immediate nearby problem, but only one preserves the later route.

### S05 — Traversal-separated reconfiguration
Player must commit, physically leave the first decision context, then later reconfigure.

### S06 — Spatial commitment
A useful move changes where the player can stand/reach, so the next decision cannot be reduced to the starting safe station.

### S07 — Multi-placement relay
A solution requires 2–4 meaningful carriage commits in a specific causal sequence.

### S08 — Repeated-archetype competition
Two instances of the same load archetype compete for the shared budget.

### S09 — Load removal mutation
An objective visibly removes one load while preserving total budget.

### S10 — Load addition mutation
An already-visible inactive load joins the rig, spreading the same budget more thinly.

### S11 — Return inversion
A configuration useful on entry becomes insufficient/wrong for extraction after player location or rig revision changes.

### S12 — Player-location-dependent value
The same distribution has different usefulness because the player is now in another authored region.

### S13 — Equivalent immediate edge / different future anchor access
Two choices open the same local path, but only one leaves a later carriage approach reachable.

### S14 — Repeated family + mutation
Two same-family loads exist before/after a visible mutation and redistribute asymmetrically.

### S15 — Four-load global compromise
Four active loads require reading more than one local consequence without adding a new rule.

### S16 — Pre/post revision reinterpretation
Same physical snap band remains in place but maps to a meaningfully different derived world state after load mutation.

### S17 — Extraction relay
Post-objective solution is not a simple reversal; it requires at least two meaningful commits.

### S18 — Final synthesis
Three or more established signatures combine without introducing new mechanics.

No encounter may claim novelty solely from a new art theme, camera angle or room shape.

---

# 4. Campaign progression bands

## Band A — Learn the rig (E01–E05)
Goal: teach visible conservation and the fact that HIGH is not universally best.

Required ideas:
- one load response at a time;
- first two-load give/take;
- first TAUT middle-state proof;
- first simple player traversal after a commit.

Target first-solve length: 2–5 min.

## Band B — Temporary compromise (E06–E10)
Goal: turn anchor choice into a sequence rather than a final answer.

Required ideas:
- 2 meaningful commits;
- first local-equivalence/global-consequence state;
- first traversal-separated second decision;
- first three-load rig.

Target first-solve length: 4–7 min.

## Band C — Spatial commitment (E11–E15)
Goal: make player position part of puzzle state.

Required ideas:
- repeated archetype;
- three-placement relay;
- player entering a region where the former best band is no longer useful;
- first safe-static-enumeration-resistant mature layouts.

Target first-solve length: 5–9 min.

## Band D — Rig revision / mutation (E16–E20)
Goal: teach that conserved budget persists when the load set changes.

Required ideas:
- first visible load removal;
- first load addition;
- return inversion;
- pre/post revision reinterpretation;
- mandatory post-mutation checkpoint.

Target first-solve length: 6–10 min.

## Band E — Mastery / synthesis (E21–E26)
Goal: combine established grammar under the exact 1.0 ceiling.

Required ideas:
- 4-load compromise;
- repeated-family + mutation;
- 3–4 commit extraction relay;
- one final encounter that demonstrates the entire product sentence cleanly.

Target first-solve length: 7–12 min, with humane checkpointing.

---

# 5. Concrete 26-encounter skeleton

The names are working encounter labels, not commercial copy.

| # | Working identity | Loads | Bands | Mutation | Primary signature | Placement target |
|---|---|---|---:|---|---|---:|
| E01 | First Pull | 1 Lift | 3 | none | S01 | 1 |
| E02 | Give / Take | Lift + Gate | 3 | none | S02 | 1 |
| E03 | Middle Holds | Lift + Span | 3 | none | S03 | 1 |
| E04 | Gate Then Lift | Lift + Gate | 3 | none | S05 | 2 |
| E05 | Span Commitment | Gate + Span | 3 | none | S06 | 2 |
| E06 | Three-Load Middle | Lift + Gate + Span | 4 | none | S03/S02 | 2 |
| E07 | Same Door, Different Future | Lift + Gate + Span | 4 | none | S04 | 2 |
| E08 | Balcony Relay | Lift + Gate + Span | 4 | none | S07 | 3 |
| E09 | High Is Wrong | Lift + Span + Gate | 4 | none | S03 | 2 |
| E10 | Far-Side Choice | Lift + Gate + Span | 4 | none | S13 | 2 |
| E11 | Twin Lifts | Lift + Lift + Gate | 4 | none | S08 | 2 |
| E12 | Twin Gates | Gate + Gate + Span | 4 | none | S08 | 2 |
| E13 | Twin Spans | Span + Span + Lift | 4 | none | S08/S03 | 2 |
| E14 | Three Placement | Lift + Gate + Span | 5 | none | S07 | 3 |
| E15 | Commit Pocket | Lift + Gate + Span | 4 | none | S12 | 3 |
| E16 | Counterweight Gone | Lift + Gate + Span | 4 | remove Gate | S09/S16 | 2 pre + 1 post |
| E17 | New Span Joined | Lift + Gate; +Span | 4 | add Span | S10/S16 | 2 pre + 1 post |
| E18 | Return Inversion I | Lift + Gate + Span | 4 | remove Lift/Gate instance | S11 | 1 pre + 2 post |
| E19 | Mutation Mid-Route | 3 loads | 5 | add/remove one | S12/S16 | 3 total |
| E20 | Revision Relay | 3→2 or 3→4 loads | 5 | one | S17 | 4 total |
| E21 | Four Loads | 4 loads / 3 families | 5 | none | S15 | 3 |
| E22 | Twin Family Mutation | repeated family + one other | 5 | one | S14 | 3 |
| E23 | Local Decoy | 4 loads | 5 | none | S04/S13 | 3 |
| E24 | Return Inversion II | 4 loads | 5 | one | S11/S17 | 4 |
| E25 | Final Relay | 4 loads | 5 | one | S07/S15/S17 | 4 |
| E26 | Final Budget | 4 loads | 5 | one | S18 | 4 |

### Campaign count checks
- Teaching/light: E01–E05 = 5.
- Mature non-mutation: E06–E15 = 10.
- Mutation/revision: E16–E20 = 5.
- Mastery/synthesis: E21–E26 = 6.
- Total = **26**.

No fourth load family is used.

---

# 6. Encounter authoring schema

Every authored encounter should be representable as data equivalent to:

```text
EncounterDefinition
  id
  progression_band
  primary_signature
  secondary_signatures[]
  intended_first_solve_minutes
  rail
    snap_count: 3..5
    world_transform
    access_regions[]
  fixed_budget_B
  revisions[]
    revision_id
    active_load_ids[]
    distributions_by_snap[][]
  loads[]
    load_id
    archetype: LIFT | GATE | SPAN
    stable_pose_by_band
    traversal_edges_by_band
    transition_safety_volume
  regions[]
  traversal_edges[]
  objective
    type: NONE | ADD_LOAD | REMOVE_LOAD
    target_load_id
    trigger_region
  checkpoints[]
  intended_solution_commits[]
  accepted_alternate_solution_signatures[]
  demo_eligible
  validation_tags[]
```

Authoring tools may expose internal quanta but shipped normal play must not require them.

---

# 7. Mandatory validators

## V01 — Budget conservation
For every revision and snap band, `sum(distribution) == B`.

## V02 — Canonical band bounds
Every load quantum is exactly 0/1/2 only.

## V03 — Adjacent transfer
Every adjacent snap pair changes exactly two load entries: one -1, one +1.

## V04 — No duplicate bands
No two snap bands in one revision have identical distribution vectors.

## V05 — World-state distinction
Every differing gameplay allocation must produce a clearly distinguishable relevant world posture at normal camera scale.

## V06 — Load contract
Every load instance implements exactly its archetype's Phase-4 SLACK/TAUT/HIGH semantics.

## V07 — No transition-timing dependency
Encounter must remain solvable if load transitions are shortened/snap-completed by accessibility settings.

## V08 — No unsafe swept-volume trap
Legal commits may not crush, trap or require precision escape.

## V09 — Reachability / no softlock
Every reachable authoritative state from C0/C1 must either preserve a legal restart path or be recoverable through intended controls.

## V10 — Post-mutation conservation
Mutation preserves `B`, snap count and physical band identity.

## V11 — Mature decision separation
For E06+, intended completion path contains at least two meaningful commits separated by traversal, anchor-access change, mutation or player-region value change unless the encounter is explicitly marked a short bridge/tutorial exception.

## V12 — Safe static enumeration rejection
For mature encounters, reject if all completion-critical reasoning can be solved from one permanently safe carriage-access region by previewing every band before any meaningful traversal/state change.

## V13 — One permanent best band
Reject mature encounter if one band satisfies every completion-critical pre/post state without requiring later reconfiguration.

## V14 — Signature duplication
Compute a systemic signature from: load multiset, snap count, mutation type, primary reasoning family, meaningful commit count, decision-separating events and pre/post revision structure. Flag near-duplicates for human review.

## V15 — Theme-only novelty
Reject campaign adjacency where two encounters share essentially the same systemic signature and differ mainly by art/layout dressing unless one is an intentional tutorial/remix pair.

## V16 — Placement ceiling
Normal main encounters require no more than 4 completion-critical commits under intended solution, excluding harmless no-op exploration.

## V17 — Mutation ceiling
At most one completion-relevant irreversible mutation per main encounter.

## V18 — Archetype ceiling
No unapproved fourth load family in 1.0 main content.

---

# 8. Reuse and repetition rules

1. No more than **2 consecutive main encounters** may share the same primary reasoning signature.
2. Repeated-archetype encounters E11–E13 must be separated by at least one encounter or differentiated strongly by secondary reasoning in final sequencing.
3. Mutation may not appear in every late encounter; at least one mastery problem must be pure redistribution/commitment without revision change.
4. The same load composition + snap count + mutation type + primary signature may appear at most twice in 1.0 main content, and the second must add a materially different decision-separating structure.
5. Geometry may change the traversal graph and therefore mechanical reasoning; mere visual relocation of the same graph does not count as new content.
6. No late encounter may be retained solely because it makes the campaign longer.

---

# 9. Demo architecture — 15–25 minutes

The commercial demo should use a compressed authored subset, not simply E01–E04 in campaign order.

Recommended 4-encounter demo package:

### D01 — First Pull / Give-Take hybrid, 3–4 min
- Lift + Gate;
- one move changes both;
- player sees conservation immediately.

### D02 — Middle Holds, 4–5 min
- Lift + Span;
- TAUT is the useful state;
- proves HIGH is not universally better.

### D03 — Far-Side Choice, 5–7 min
- 3 loads;
- first commit opens route;
- player traverses away and later makes a second materially different carriage decision.

### D04 — Counterweight Gone, 6–8 min
- 3 loads;
- visible objective removes one load;
- same snap band redistributes differently;
- old entry compromise becomes wrong for extraction.

Expected total first-time demo: roughly **18–24 minutes**.

Demo success condition: a player should be able to describe the product as “I pull one carriage, several things trade tension, then I have to move through the consequences and reconfigure” without seeing a number or graph.

---

# 10. Optional/remix policy

Optional content is **not required** for 1.0 value.

If playtests show strong demand, allow at most **4–6 optional mastery remixes** using existing mechanics/data fields only.

Optional content may:
- tighten systemic density;
- use four loads earlier;
- ask for cleaner 3–4 commit solutions;
- remix pre/post mutation structure.

Optional content may not:
- add a fourth archetype;
- add move limits/currency as punishment;
- introduce precision timing;
- add multiple independent carriages;
- require hidden tension values.

### First-cut rule
If repetition testing shows late-main fatigue, cut optional remixes first, then cut the weakest near-duplicate main encounter rather than inventing rescue mechanics.

---

# 11. Content QA questions

Every encounter review asks:
1. What is the primary reasoning sentence?
2. Can the player solve it by standing safely at one rail and cycling bands?
3. Does TAUT/HIGH/SLACK matter physically rather than cosmetically?
4. Is every consequence visible and deterministic?
5. Does player location materially alter the next decision?
6. If mutation exists, is it visibly caused and does it genuinely reinterpret the budget?
7. Is there any timing, dexterity or hidden-information solution dependency?
8. Is the encounter mechanically distinct from its nearest campaign neighbors?
9. Can it be removed without losing an entire reasoning family? If yes, it is a candidate for cut.

---

# 12. Phase 5 acceptance checklist

- [x] 26-encounter skeleton defined within 24–28 frozen range.
- [x] Five progression bands defined.
- [x] 18 reasoning signatures classified.
- [x] Load/snap/mutation/commit expectations bounded.
- [x] Authoring schema defined.
- [x] Budget, adjacency, readability, safety, anti-enumeration and repetition validators defined.
- [x] No fourth load archetype introduced.
- [x] No movement mastery pillar introduced.
- [x] 15–25 minute demo subset satisfies the full Phase-3 promise.
- [x] Optional/remix boundaries and first-cut rules defined.
- [x] Production implementation remains outside factory.

# PHASE 5 DECISION

**PHASE 5 CONTENT ARCHITECTURE = COMPLETE.**

The frozen mechanics support a bounded 26-encounter campaign without feature inflation. Content authority now depends on systemic-signature diversity, traversal-separated decisions, visible mutation and explicit validators rather than raw room count.

## NEXT ACTION — PHASE 6 UX / PRESENTATION ARCHITECTURE
Define controls, camera, HUD, onboarding, world-space tension language, causal feedback, accessibility, pause/settings, restart/checkpoint behavior, first-session flow, failure explanation and presentation rules while preserving zero numeric/graph dependence.