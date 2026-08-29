# GAME #006 — STITCHSPACE — PHASE 10 ADVERSARIAL REVIEW

Last updated: 2026-08-29
Phase: **10 — Adversarial Review**
Selected concept: **G6C01 Stitchspace**
Production implementation started: **NO**
DESIGN COMPLETE: **NO**

Purpose: attack the complete Phase-3..9 design as if trying to disqualify it before freeze. This review may narrow rules, add acceptance gates, or preserve empirical uncertainty; it may not rescue weaknesses by feature accretion.

---

# 1. Fun / novelty / hour-3 and hour-6 repetition

## Attack
The central verb is intentionally narrow: move one existing seam endpoint. A weak campaign could become thirty variations of `connect -> cross -> reconnect`. Free Undo and small legal target sets can further turn thoughtful play into enumeration.

## Finding
The design remains viable only if content diversity is measured by *causal skeleton*, not room dressing, number of sockets, or nominal objectives. Phase-9 P9-R9 is therefore promoted from review guidance to a release-content validator requirement.

## Repair P10-R1 — causal-family quota is canonical
Each C15–C34 case must declare a dominant causal-skeleton vector using the Phase-9 dimensions. Two cases are not considered materially distinct merely because rooms, art, socket positions, or goal objects differ.

Required authored-campaign constraints:
- no consecutive 3-case window shares one dominant skeleton family;
- every 5-case window contains >=3 materially distinct families;
- C24–C34 contains >=5 families total;
- no single family occupies >30% of C15–C34;
- if a case cannot be classified without inventing a one-off exception, the case is rejected rather than adding a new rules subsystem.

Empirical gate retained: representative players must still report distinct reasoning rather than cosmetic variation.

---

# 2. Portal misread / persistent relationship identity

## Attack
A two-ended seam that connects distant boundaries can still be perceived as a portal pair, especially if the player mostly acts by selecting an endpoint and a target.

## Finding
The product survives only if the seam reads as one persistent relationship whose endpoint is relocated, with the destroyed adjacency as salient as the new one.

## Repair P10-R2 — relationship continuity protocol
Every endpoint replacement presentation must expose the same semantic sequence:
1. identify seam pair;
2. mark selected endpoint;
3. show `OLD` relationship and its paired remote endpoint;
4. show candidate `NEW` relationship;
5. commit as one atomic replace action;
6. visually retire OLD and establish NEW without a frame in which both are authoritative.

Persistent pair identity from P9-R2 is mandatory when idle, selected, previewing, crossing, paused and reduced-motion mode. The physical seam relation must not be represented as two independent inventory objects.

Empirical kill/reopen gate from Product Thesis remains unchanged: if naive testers persistently explain the mechanic only as portal placement after one bounded presentation/tutorial tuning pass, reopen or kill rather than add powers.

---

# 3. Dominant strategies

Attacked strategies:
- always choose the target nearest the player;
- always connect current room directly to goal room;
- preserve one seam permanently as a lifeline;
- minimize endpoint edits universally;
- cycle every legal target until something works;
- keep one endpoint permanently anchored and only move the other.

## Repair P10-R3 — dominant-strategy rejection fixtures
For C15–C34, content validation must include at least one of the following per case:
- direct-current-room-to-goal move is illegal, strategically losing, or longer than a materially different solution;
- stable-lifeline policy prevents completion or produces a worse causal state;
- both endpoints of a seam matter over the solution, or the case explicitly exists as a one-endpoint literacy exception;
- minimal-edit count is not the sole mastery criterion;
- first locally attractive target leads to an observable but recoverable bad state.

Across representative mature cases, direct current-room-to-goal stitching must not be shortest in >=75% of cases, preserving the inherited prototype gate.

---

# 4. Blind target cycling / brute force

## Attack
Free Undo plus <=6 relevant targets can make exhaustive cycling rational.

## Finding
Undo must remain free; punishing experimentation would damage the product more than brute-force risk. The solution is to ensure each committed legal edit produces legible causal information and that mature cases require multi-step state reasoning rather than one lucky endpoint choice.

## Repair P10-R4 — anti-enumeration structure
A mature case is invalid if a player can solve it reliably by repeated single-step target cycling without tracking entity/topology consequences.

Validator/review requirements:
- at least one intermediate state variable (entity position, useful cut, orientation, loop state, occupancy, seam role, or state-dependent target value) must materially alter which later target is correct;
- no main case may define success as a one-command endpoint guess after C06;
- target density stays within P9-R3 readability bounds; increasing candidate count is not an anti-bruteforce solution.

---

# 5. Alternate solutions / state-space explosion / solver tractability

## Attack
Two seams produce four movable endpoints; 3 seams produce six. Combined with entity states, orientation and Undo history, raw state count can explode and authored alternate solutions may become hard to verify.

## Finding
Undo history is not part of puzzle-state equivalence. Solver state must use canonical domain state only. Three-seam content is unnecessary for the commercial identity and is the largest avoidable explosion source.

## Repair P10-R5 — solver-state boundary
Solver canonical state excludes:
- presentation state;
- camera/focus;
- animation phase;
- save generation metadata;
- Undo/Redo ancestry except where testing history itself;
- purely explanatory seam provenance.

It includes only gameplay-relevant topology/entity/objective state and canonical mover boundary state.

Every shipped main case must satisfy a configured solver budget on reference CI hardware. Exact wall-clock budget is implementation-tunable, but the build must expose deterministic counters: visited canonical states, expanded transitions, duplicate-pruned states, solution count up to a configurable cap, shortest semantic command length, and termination reason.

A case that exceeds budget is simplified/rejected; runtime code may not add bespoke pruning that changes game semantics.

## Repair P10-R6 — three-seam default removal
No main campaign case is *required* to ship with 3 seams. C30 or any other 3-seam candidate remains optional experimental content and must be demoted to a 2-seam alternative unless it passes all later empirical readability gates and solver budget comfortably. C34 remains 2 seams by default.

This turns 3 seams from a planned complexity milestone into an optional proven exception.

---

# 6. Two-seam readability

## Attack
Four endpoints can make players forget which relationship is lost by a selected endpoint move.

## Repair P10-R7 — pair identity + destructive preview gate
With >=2 seams:
- each seam has redundant identity independent of color;
- selecting either endpoint highlights both endpoints of that seam;
- OLD relationship remains visible during target browsing;
- target preview never hides the relationship that will be destroyed;
- focus movement cannot silently switch seams;
- confirm copy/feedback identifies the semantic seam and endpoint, not only screen position.

Empirical gate: representative two-seam cases must be explainable from 1280×800 screenshots/short clips without relying on color alone.

---

# 7. Orientation bookkeeping

## Attack
N/E/S/W mappings can become compass arithmetic and overwhelm adjacency reasoning.

## Finding
Orientation is valid only as a *visible local physical consequence*, never as a numeric rotation puzzle.

## Repair P10-R8 — orientation ceiling
- Player-facing UI never requires numeric angles or compass calculation.
- Every orientation-sensitive consequence must be previewable through destination boundary geometry/arrows/shape.
- Cases whose challenge depends on remembering an unseen previous orientation are rejected.
- No case may combine a novel orientation rule with a novel seam rule; there are no per-case orientation laws.
- If orientation misunderstanding remains >=20% of ordinary failures after tutorial tuning, simplify presentation/content before considering any rules expansion.

---

# 8. Simultaneous crossing / occupancy / mover order dependence

## Attack
A seam edit, automatic mover and crossing could create hidden frame-order dependence or ambiguous occupancy locks.

## Repair P10-R9 — canonical event boundary
Domain mutation occurs only at discrete canonical boundaries. At any command opportunity:
1. all previously accepted canonical transition consequences are fully resolved to the next stable/declared boundary;
2. crossing entities expose an explicit canonical crossing phase;
3. endpoint/socket locks derive from canonical state, never animation interpolation;
4. mover intents for the same canonical step are collected before resolution;
5. conflicts resolve by one global stable order defined in Technical Spec (entity stable ID after rule priority), never scene-tree or frame order;
6. the resulting transition is replayable bit-for-bit from the same pre-state + command.

If multiple movers require a different policy, the policy must be global and data-driven, not a case callback.

Every mover/occupancy case retains P9-R5 Step-compatible fixture.

---

# 9. Undo/Redo / stale commands / persistence / Cloud conflicts

## Attack
Atomic seam replacement plus mover consequences, duplicate commands, stale revisions, crash rotation, demo import and Cloud divergence create many corruption boundaries.

## Finding
The technical design is coherent if transaction scope is explicit.

## Repair P10-R10 — transaction/history invariant
One accepted semantic player command plus all deterministic immediate domain consequences before the next command boundary forms one history transaction. Undo restores the exact transaction parent canonical snapshot/hash; Redo reapplies the exact child snapshot/hash, not a fresh simulation from mutable presentation state.

Duplicate accepted `command_id` returns the previously recorded result without a second mutation. A command ID reused with different payload is a hard reject. Stale expected revision/hash rejects before mutation.

Persistence invariants:
- only committed canonical boundaries are durable;
- temp/primary/backup recovery yields an exact verified generation;
- corrupt generations are never partially merged;
- active-case Cloud branches are never structurally merged;
- monotonic profile facts may merge only through explicit commutative rules.

---

# 10. Input focus / remapping / Deck / pseudolocalization

## Attack
Dense socket layouts and controller target cycling can become unpredictable; remapping can strand the player; localization can crowd OLD→NEW preview.

## Repair P10-R11 — semantic focus invariants
- Authored focus graph is authoritative for controller/keyboard and independent of rendered pixel coordinates.
- Pointer selection resolves to the same semantic target object.
- Focus change never commits a gameplay mutation.
- Leaving/re-entering edit mode returns focus to a deterministic semantic anchor.
- Remap UI prevents a saved configuration from removing all bindings for Confirm, Cancel, Pause/Menu and navigation; recovery defaults remain accessible.
- At 1280×800, no required puzzle fact exists only in hover text or tiny labels.
- Pseudolocalization test uses expanded strings and verifies no topology identity depends on truncated text.

---

# 11. Accessibility abuse / challenge preservation

## Attack
Pause/Step, reduced motion, hints, high contrast or unlimited Undo might trivialize some authored challenge.

## Finding
If accessibility trivializes a case, the case relies on the wrong challenge. Baseline game is reasoning, not reaction or perceptual withholding.

## Repair P10-R12 — accessibility-safe content rule
All main-campaign completion remains valid with:
- Pause/Step where movers exist;
- unlimited Undo/Redo within branch rules;
- reduced motion;
- high-contrast/redundant seam identity;
- remapped controls;
- non-audio play.

Mastery/achievements may not punish use of these baseline accessibility features. Hints may affect only explicit hint-related optional records if any; they may not block campaign completion.

---

# 12. Demo / commercial proof / price/value

## Attack
A clever 20-minute hook may not sustain 5+ hours, and expert puzzle players may clear a 34-case campaign quickly. $17.99 can be weak if late cases feel isomorphic.

## Finding
Price cannot be proven on paper. The design can freeze a decision framework, not a guaranteed price.

## Repair P10-R13 — price remains review variable
Design-time working target remains **$17.99 USD**, bounded release-review band **$14.99–$19.99**. Final list price is not frozen until Phase 12G measures:
- expert first-clear distribution;
- broader-target first-clear distribution;
- demo completion and full-hook comprehension;
- perceived variety/value feedback;
- actual final shipped case/remix count and quality.

Do not inflate level count with weak variants to defend price.

Demo PASS requires all Product Thesis proof conditions by DEMO05, with CTA only after the final causal reveal per P9-R6.

---

# 13. Content-production scope / bespoke-rule creep

## Attack
34 authored cases + remixes + alternate solution validation can become a hidden production burden.

## Repair P10-R14 — content cut ladder
Release scope priority:
1. mechanically distinct C01–C24 core;
2. strongest validated C25–C34 late cases;
3. only then R01–R08 remixes that pass changed-causal-dependency audit.

If production budget slips, cut weak remixes first, then weak late cases, while preserving onboarding and final synthesis. Never compensate by adding one-off socket powers, seam elements, currencies, extra mover species, narrative systems or bespoke case callbacks.

A main case may configure global primitives but cannot define new transition semantics.

---

# 14. Cross-spec implementation ambiguity

Destructive comparison across Product Thesis / Mechanical / Content / UX / Technical specifications found several places where implementation could otherwise improvise.

## Repair P10-R15 — authority reconciliation
The following clarifications are frozen for Phase 11:

1. **Command boundary:** one accepted semantic command + its deterministic immediate consequences is one transaction/history child.
2. **Mover conflict order:** global rule priority then stable entity ID; never runtime object order.
3. **Preview:** presentation-only derived view of a hypothetical legal/illegal command; preview never mutates revision/hash/history.
4. **Socket relevance:** `relevant target` is a content/UX exposure concept, not a second legality system. Domain legality remains canonical.
5. **Case restrictions:** authored allowed-target restrictions may narrow choices but never override global transition semantics.
6. **Three seams:** optional exception, not campaign progression requirement.
7. **Dead-end knowledge:** solver may detect dead states for authoring/tests, but runtime does not expose an oracle by default.
8. **Persistence:** only canonical command boundaries are saved; crossing animation can reconstruct from canonical crossing state but cannot introduce hidden gameplay state.
9. **Cloud:** active puzzle branches never synthesize/merge; profile facts only use explicit monotonic merge rules.
10. **Mastery:** no universal move-count economy; case-specific alternate solution predicates must represent causal distinction.
11. **Presentation geometry:** never authoritative for socket identity/focus/collision outcome.
12. **Content callback ban:** data cannot execute bespoke gameplay code.

---

# 15. Reconciliation of P9-R1..P9-R9

- **P9-R1** retained and strengthened: C07–C10 must document material lost-adjacency purpose.
- **P9-R2** promoted to hard multi-seam identity invariant via P10-R2/R7.
- **P9-R3** retained: normally <=6 currently relevant exposed legal targets; excess requires readability justification.
- **P9-R4** strengthened: C34 defaults to 2 seams; third seam cannot be promoted on paper.
- **P9-R5** retained and expanded by P10-R9 canonical event boundaries.
- **P9-R6** retained: CTA never interrupts DEMO05 causal reveal.
- **P9-R7** retained: bounded invalid-reason codes + localized templates.
- **P9-R8** retained and expanded by P10-R13 separate timing/value cohorts.
- **P9-R9** promoted to hard causal-family quotas via P10-R1.

No Phase-9 repair is dropped.

---

# 16. Retained empirical gates — cannot be closed on paper

Phase 11 may freeze the design while retaining these implementation/playtest gates:

**EG-01 Portal comprehension** — after one bounded tuning pass, >=75% naive testers explain adjacency replacement / old connection loss rather than merely portal placement.

**EG-02 Hook-content validity** — >=5/8 representative grayboxes materially depend on lost adjacency, orientation, occupancy, loop or disconnection.

**EG-03 Solution-family depth** — representative mature cases show >=4 abstract solution skeleton families.

**EG-04 Orientation comprehension** — orientation misunderstanding causes <20% ordinary failures after tutorial.

**EG-05 Anti-direct-goal strategy** — direct current-room-to-goal stitching is not shortest in >=75% representative mature cases.

**EG-06 No dexterity dependence** — baseline solutions require no reaction timing.

**EG-07 Mute-clip legibility** — short mute clip communicates NEW relationship + destroyed OLD relationship.

**EG-08 Two-seam Deck readability** — pair identity and destructive preview remain understandable at 1280×800, grayscale/high-contrast conditions.

**EG-09 Useful disconnection affect** — representative testers describe intentional cut/isolation as understandable and satisfying rather than arbitrary punishment.

**EG-10 Mature repetition** — C15–C34 playtest does not collapse to perceived cosmetic variants of one skeleton.

**EG-11 Controller predictability** — dense mature cases retain predictable semantic target selection.

**EG-12 Three-seam exception** — any proposed shipped 3-seam case must independently pass readability + solver budget; otherwise cut.

**EG-13 Value duration** — measure expert and broader-target first-clear distributions separately before final price decision.

**EG-14 Demo conversion proof** — demo reaches full causal hook before CTA and testers can explain why full game offers more than portal spectacle.

**EG-15 Solver production cost** — full candidate campaign remains within practical deterministic authoring/CI solver budgets without semantic shortcuts.

Failure of EG-01/02/03 after one bounded repair pass is a reopen/kill signal, not permission for feature accretion.

---

# 17. Phase-10 acceptance tests

- **A10-01** Every endpoint move atomically removes OLD adjacency and creates NEW adjacency.
- **A10-02** Preview causes no revision/hash/history mutation.
- **A10-03** Multi-seam idle state retains redundant pair identity without color dependence.
- **A10-04** Selected endpoint always exposes which relation will be destroyed.
- **A10-05** No main case after C06 is solvable as a one-command blind target guess.
- **A10-06** C15–C34 satisfy 3-case/5-case causal-family quotas.
- **A10-07** No single causal family exceeds 30% of C15–C34.
- **A10-08** C24–C34 contain >=5 causal families.
- **A10-09** Mature cases include state-dependent later target value.
- **A10-10** Representative mature direct-goal stitching gate remains >=75% non-shortest target.
- **A10-11** Solver equivalence excludes history/presentation metadata.
- **A10-12** Solver emits deterministic visited/expanded/duplicate/solution/termination metrics.
- **A10-13** Shipped cases exceeding configured solver budget are simplified/rejected.
- **A10-14** No 3-seam case is required for campaign completeness.
- **A10-15** C34 baseline is 2 seams.
- **A10-16** Orientation-sensitive consequence is visible without numeric angle arithmetic.
- **A10-17** Cases never rely on unseen orientation memory.
- **A10-18** Mover intents resolve by global rule priority + stable entity ID.
- **A10-19** Scene-tree/frame/render order cannot change canonical result.
- **A10-20** Every mover case has Step-compatible deterministic fixture.
- **A10-21** One player command + immediate deterministic consequences equals one history transaction.
- **A10-22** Undo restores exact parent canonical hash.
- **A10-23** Redo restores exact child canonical hash until branch truncation.
- **A10-24** Duplicate command ID + same payload is idempotent.
- **A10-25** Duplicate command ID + different payload hard-rejects.
- **A10-26** Stale expected revision/hash rejects without mutation.
- **A10-27** Durable saves occur only at canonical boundaries.
- **A10-28** Fault recovery never merges partial generations.
- **A10-29** Cloud never merges divergent active-case structures.
- **A10-30** Profile Cloud merge uses only explicit monotonic facts.
- **A10-31** Controller/keyboard use authored semantic focus graph.
- **A10-32** Pointer selection resolves to same semantic target model.
- **A10-33** Focus navigation cannot silently switch seam before confirm.
- **A10-34** Remap recovery preserves essential menu/navigation actions.
- **A10-35** 1280×800 exposes every required puzzle fact without hover-only text.
- **A10-36** Pseudolocalization cannot remove topology identity via truncation.
- **A10-37** Pause/Step does not invalidate campaign completion.
- **A10-38** Reduced motion does not alter topology rules.
- **A10-39** Color is never sole seam/orientation signal.
- **A10-40** Audio is never sole puzzle-state signal.
- **A10-41** Undo/accessibility use does not invalidate baseline achievements/mastery.
- **A10-42** DEMO05 causal reveal completes before purchase CTA.
- **A10-43** Price remains release-review variable inside $14.99–$19.99 band.
- **A10-44** Expert and broader-target first-clear times are measured separately.
- **A10-45** Content-cut ladder removes remixes/weak cases before adding new mechanics.
- **A10-46** Case data cannot inject bespoke transition callbacks.
- **A10-47** Authored target restrictions narrow legality only; they cannot redefine global seam semantics.
- **A10-48** Runtime dead-end oracle is absent by default even if tooling knows dead states.
- **A10-49** Mastery predicates represent causal distinction rather than universal edit-count minimization.
- **A10-50** Presentation geometry is non-authoritative for canonical state.
- **A10-51** P9-R1..P9-R9 all remain represented in final acceptance/gates.
- **A10-52** EG-01..EG-15 remain explicitly empirical and are not marked paper-PASS.

---

# 18. Phase-11 freeze prerequisites

Phase 11 may proceed only if:
1. Product Thesis authority remains unchanged.
2. P10-R1..P10-R15 are incorporated into final authority.
3. P9-R1..P9-R9 remain reconciled.
4. canonical command/transaction/event ordering is unambiguous.
5. three-seam content is optional rather than required.
6. causal-family quotas and content cut ladder are explicit.
7. solver-state boundary and instrumentation obligations are explicit.
8. persistence/Cloud branch rules are unambiguous.
9. controller/Deck/accessibility obligations are explicit.
10. price remains an empirical release decision rather than false paper certainty.
11. EG-01..EG-15 are retained for Phase 12G.
12. no new gameplay verb/system is needed to repair any adversarial finding.

All twelve prerequisites are satisfied by the current paper authority.

---

# 19. Phase-10 closure

Fun/repetition attacked: **YES**
Portal misread attacked: **YES**
Dominant strategies attacked: **YES**
Brute-force target cycling attacked: **YES**
Solver/state explosion attacked: **YES**
Two/three-seam readability attacked: **YES**
Orientation bookkeeping attacked: **YES**
Mover/order determinism attacked: **YES**
Undo/persistence/Cloud attacked: **YES**
Input/Deck/localization attacked: **YES**
Accessibility attacked: **YES**
Demo/value/pricing attacked: **YES**
Content scope/bespoke creep attacked: **YES**
Cross-spec ambiguity reconciled: **YES**
P9-R1..P9-R9 reconciled: **YES**
Empirical uncertainty retained honestly: **YES**
New mechanics required: **NO**
Phase 10 complete: **YES**

## NEXT PHASE

**Phase 11 — Specification Freeze.**
