# GAME #007 — LAST KNOWN SHAPE — PHASE 10 ADVERSARIAL REVIEW

Last updated: 2026-08-30
Phase: **10 — Adversarial Review**
Selected concept: **G7C02 Last Known Shape**
Production implementation started: **NO**
DESIGN COMPLETE: **NO**

Authority entering this pass: Product Thesis -> Mechanical Architecture -> Content Architecture -> UX/Presentation -> Economy/Commercial -> Technical Specification -> Whole-Game Simulation repairs P9-R1..P9-R27. Tournament/research are rationale only.

This pass assumes every written rule is hostile until it survives an explicit collapse test. It does not paper-PASS empirical fun/readability/value gates.

---

# 1. One-gimmick / hour-4 repetition

## Attack
The first transformation is visually novel, but a 34-case campaign can degenerate into `walk to frame -> inspect candidate -> commit -> carry/use object -> repeat`. Eight metadata families do not guarantee eight felt puzzle families.

## Surviving risk
High. This is the largest product risk and cannot be eliminated purely by specification.

## P10-R1 — felt-family gate
C11+ content is invalid unless the shortest/representative solution requires at least two distinct causal decisions among preservation, overwrite timing, access self-block, relocation, declared input manipulation, two-object ordering, destructive re-observation, receiver-state dependency, or state-dependent reuse. Merely visiting two frames is not two causal decisions.

## P10-R2 — mature-session diversity gate
A representative 30–45 minute mature slice must contain >=3 player-perceived planning families, not merely validator labels. If blinded testers describe all sampled cases as the same `pick the right shape` puzzle, the content set is redesigned/cut; adding new forms is forbidden as the repair.

Kill condition: if a representative mature slice cannot sustain >=3 felt families without private mechanics, **kill or radically shrink the product rather than pad to 28 cases**.

---

# 2. Free-camera / perspective-game misread

## Attack
Marketing and visuals can still make players assume ordinary camera angle changes object shape, creating frustration when it does not.

## P10-R3 — frame-authority proof
Every store/demo/onboarding proof must show an authored Frame before or during the first transformation. At least one early interaction must visibly demonstrate that moving the ordinary camera while remaining outside a Frame does nothing to Candidate/Remembered state.

No store copy may lead with `change perspective to reshape reality`. Required language foregrounds `Observation Frames`, `remembered form`, or equivalent plain physical phrasing.

Empirical gate EG7-03 remains unpassed: mute clip comprehension must distinguish persistent authored observation from free-camera perspective tricks.

---

# 3. Detached menu / form-selection collapse

## Attack
Because Candidate is exact and safe to preview, the optimal interface can become a list of object cards and forms. The world risks becoming decorative traversal between menu terminals.

## P10-R4 — embodied observation contract
No baseline screen may enumerate all Frames, all possible forms, or a full candidate matrix for a case. Candidate exists only for the currently reached/activated Frame and selected eligible object. Quick/Expanded Inspect may show current Physical/Remembered facts and learned affordances, never future candidates globally.

## P10-R5 — world-use ratio review
For C11+ content, authored review must reject cases where all strategically meaningful decisions occur while standing in one Frame UI with no intervening physical exploitation/access/relocation/world-state change. Mature solutions must alternate observation choice and world consequence.

---

# 4. Dominant strategies / blind candidate cycling

## Attack
Unlimited Undo + exact preview makes exhaustive trial cheap. A player might visit every accessible Frame, commit each candidate, Undo on failure, and solve without causal planning.

## P10-R6 — anti-enumeration strengthened
Phase-5 shortcut policy `TRY_ALL_CANDIDATES_UNTIL_GOAL` is expanded into two bots/review modes:
1. **greedy-visible**: commit every newly seen candidate immediately;
2. **local-enumeration**: at each reachable Frame, try every candidate branch before performing non-required relocation/world manipulation.

From C16 onward, >=75% of mature validated cases must defeat both within a configurable shallow search horizon because success requires preservation or state change before candidate value is known. This is a campaign/content gate, not runtime punishment.

## P10-R7 — preview remains informative, not predictive oracle
Preview may show immediately knowable current affordance deltas, but never downstream receiver chains that are not already visible/learned facts. It cannot label `best`, `required`, `progress`, `dead end`, or shortest-path implications.

---

# 5. Form/object identity ambiguity and two-object bookkeeping

## Attack
Two objects can share forms and both possess Physical/Remembered/Candidate states, producing six visually competing facts.

## P10-R8 — two-object information ceiling
At ordinary play, only the currently targeted object's Candidate is expanded. The other reasoning-critical object retains compact persistent identity + Physical/Remembered status. Both objects use stable non-color identity tokens across meshes/forms.

## P10-R9 — no third critical memory in main campaign
Three simultaneously reasoning-critical transformable objects are removed from main-campaign allowance, not merely discouraged. C01–C34 and DEMO01–06 use at most two reasoning-critical remembered objects. A third may exist only as non-critical scenery/receiver or future expansion after a separate spec.

This narrows earlier `possible after proof` language.

---

# 6. Dynamic input / occluder arbitrariness

## Attack
A declared symbolic occluder is deterministic but can still feel arbitrary if a table maps visually similar states to unrelated forms.

## P10-R10 — transform-family consistency
Every reusable transform/mask family must have one player-learnable invariant. Case data may select among a finite result table, but may not map equivalent visible relations to unrelated form outcomes merely to create difficulty.

## P10-R11 — input dependency disclosure
A dynamic input can affect Candidate only when the world-space causal bridge is currently visible/inspectable from the Frame interaction context. The UI may name the input but cannot be the sole evidence.

Ordinary frames retain 0–1 dynamic input. Two dynamic inputs are removed from baseline main campaign; any such experiment belongs outside C01–C34 until separately proven.

Kill condition: if authors repeatedly require exception prose to explain why an input changes a Candidate, that transform family is cut.

---

# 7. Content authoring / asset / QA burden

## Attack
34 3D authored puzzles with multiple forms, observation framing, bespoke collision/presentation, solver validation, localization and Deck readability can exceed small-team scope even without new mechanics.

## P10-R12 — release cut ladder
Release target remains C01–C34, but production order/cut logic is explicit:
1. build/validate teaching spine C01–C19;
2. build mature pool beyond the spine;
3. retain only causally distinct mature cases;
4. release floor remains 28 **only if** 28 pass readability/diversity/solver/production-cost gates;
5. if 24–27 exceptional cases produce the measured value target, Phase 12G may request a commercial scope review rather than adding weak filler;
6. if value cannot be supported after cuts, delay/resize/kill instead of inventing mechanics.

The paper `28` floor is therefore a target gate, not permission to ship filler.

## P10-R13 — reusable asset ceiling
Main campaign targets 4–6 reusable object visual families and 5–7 transform/mask families. A case requiring a one-off transformation pipeline, one-off interaction system, or hero asset solely to make its logic work fails scope review unless it replaces rather than adds to the vocabulary.

---

# 8. Solver/state explosion and validator false confidence

## Attack
Two objects × forms × poses × frame access × player regions can still explode. A solver proving solvability does not prove player readability or fun.

## P10-R14 — solver budget hierarchy
Ordinary case budget remains <=150k semantic states / <=1.5m transitions target. Named late profile may rise only after memory/frontier instrumentation. Over-budget response order: remove irrelevant pose states -> reduce frame/object branching -> simplify receiver dependencies -> cut case. Bespoke pruning that changes completeness is forbidden.

## P10-R15 — validator claims ceiling
V1–V8 may prove schema, determinism, bounded solvability, shortcut properties and metadata diversity. They may **not** mark `fun`, `readable`, `fair`, `good value`, or `felt variety` PASS. Those remain empirical gates with recorded tester evidence.

---

# 9. Traversal tax / pacing

## Attack
Embodied world-use can become walking tax, especially when the correct plan requires returning to earlier Frames.

## P10-R16 — decision-density gate
P9-R11 is hardened: in representative first clears of C20+, if >~33% of active puzzle time is repeated traversal through already-understood safe space with no new observation, movement, receiver or preservation decision, the case must shorten routes, open a rule-consistent solved-state shortcut, or be redesigned/cut.

No global fast travel is added to puzzle semantics.

---

# 10. Undo/history memory and branch persistence

## Attack
`Unlimited` Undo can create pathological memory/save growth, while compaction risks violating exact restoration.

## P10-R17 — exactness before optimization
Visible active-case Undo remains effectively unlimited. Implementation may checkpoint/delta/compact only after property tests prove exact semantic hash restoration over long random command traces, branch-after-Undo, save/reload, and redo invalidation. No silent history-depth cap may be introduced as an optimization.

History ancestry remains excluded from solver equivalence but active branch metadata required for Cloud divergence must remain durable.

---

# 11. Save/content migrations and corruption recovery

## Attack
Stable IDs and checksums are insufficient if a patch changes semantic rules behind the same ID.

## P10-R18 — semantic content compatibility
Durable saves record both content version and global rule-schema version. A migration may map IDs only when semantic compatibility is explicit. Reusing an old `form_id`, `transform_rule_id`, or case ID for materially different semantics is forbidden.

Every public/demo compatibility change requires fixture saves from at least the previous supported version. Unsupported incompatible active puzzle branches degrade to a transparent safe restart of that case only after preserving profile progress where valid; never heuristic state surgery.

---

# 12. Cloud divergent branches / offline-first

## Attack
Cloud conflict UI can itself become a support burden and accidentally overwrite a preferred branch.

## P10-R19 — Cloud release kill switch
Cloud remains strictly optional. It ships only if divergence fixtures prove: ancestor detection, profile monotonic merge, preservation of both divergent active branches, non-spoiler choice metadata, offline round-trip and recovery after interruption. Failure of any required branch-integrity fixture disables Cloud for release rather than weakening local correctness.

Wall-clock `newest wins` is never sufficient for divergent ancestry.

---

# 13. Demo -> full import/versioning

## Attack
Demo saves may outlive renamed semantic input actions/settings and become an accidental migration surface.

## P10-R20 — demo import minimum surface
Full game imports only whitelisted settings/accessibility/language, recognized semantic remaps, tutorial acknowledgements and monotonic demo facts. No active demo puzzle state, remembered forms, case branch or guessed campaign completion crosses product boundary.

Unknown/remapped actions receive safe defaults and binding-recovery validation. Re-import is idempotent.

---

# 14. Controller / keyboard / Deck / remapping

## Attack
3D traversal + Frame targeting + Inspect + Undo/Redo can overload standard gamepads; large text can obscure causal geometry.

## P10-R21 — device proof suite
Before bulk content, DEMO01–06 equivalent vertical slice must be completed end-to-end using:
- controller only;
- keyboard only;
- mouse+keyboard;
- Steam Deck built-in controls at 1280×800.

Each path includes remapping Confirm/Cancel/Inspect/Undo/Redo and recovering defaults without another device. Failure blocks content population, not merely polish.

Panel layout validation uses causal-subject visibility, not percentage size alone.

---

# 15. Reduced motion / non-audio / localization / accessibility

## Attack
The transformation spectacle may carry the very information the accessibility mode removes.

## P10-R22 — semantic redundancy invariant
Commit and resolution must remain distinguishable with animation disabled, audio muted and color ignored. Required minimum is two discrete visual/state markers: `memory written` then `physical resolved`, paired with persistent tokens/outline change.

Every required puzzle fact must survive +40% text expansion and one-step-above-default text size on Deck target. If not, content/layout fails rather than shrinking critical text.

Accessibility settings never change candidate semantics or invalidate achievements.

---

# 16. Onboarding/hints as correctness oracle

## Attack
Because the core rule is unusual, tutorials/hints can accidentally tell the player which form is correct.

## P10-R23 — causal-fact hint boundary
Hints may identify learned rule, relevant entities/relationship, or one intermediate subgoal. After tutorial cases they may not say `commit Frame X`, `keep Form Y`, reveal a dead state, or expose solver-derived next action. Hints are authored facts, never runtime solver oracle.

C05/P9-R3 consequence-first pedagogy remains mandatory.

---

# 17. Pricing / value / demo conversion / store claims

## Attack
$17.99 and 5–8 hours can become circular paper justification. Current competitor price points do not prove willingness to pay for this product.

## P10-R24 — evidence-only commercial claims
Working $17.99 and $14.99–$19.99 band remain planning hypotheses. Final price/store duration/value claims require measured non-expert first-clear distribution, surviving case count, perceived causal variety, presentation quality and demo intent. Optional remixes contribute zero promised value before they exist and pass causal-distinction tests.

No store page may promise exact hour count derived only from author estimates.

---

# 18. Engine/runtime/platform assumptions

Fresh check 2026-08-30: official Godot archive lists 4.7.2-stable (2026-08-18) and 4.8-dev4 (2026-08-26). Therefore Phase-8 initial 4.7.2-stable pin remains coherent; 4.8 development snapshots are not baseline.

## P10-R25 — version pin is provisional implementation baseline
The frozen design requires deterministic/domain behavior, not Godot 4.7.2 specifically forever. Dedicated implementation starts on 4.7.2-stable unless a newer stable exists at bootstrap and passes an explicit upgrade evaluation. Any upgrade requires domain/save/input/Deck regression and rollback point.

No design requirement may depend on a dev-only engine feature.

---

# 19. Cross-spec contradiction reconciliation

Reviewed Product Thesis, Mechanical Architecture, Content Architecture, UX/Presentation, Economy/Commercial, Technical Specification and P9-R1..P9-R27 against this pass.

Resolved conflicts/narrowing:
- Earlier allowance for a third reasoning-critical object is superseded by **P10-R9: main campaign/demo max two**.
- Earlier allowance for rare two-dynamic-input Frames is superseded by **P10-R11: main campaign max one dynamic input per Frame**.
- 28-case release floor is not permission for filler; P10-R12 establishes an evidence-driven scope-review/cut path.
- Candidate/inspect information is explicitly bounded by P10-R4/P10-R7; no global candidate atlas or correctness oracle.
- Solver/validator cannot paper-certify player experience (P10-R15).
- Cloud is optional and must be cut on branch-integrity failure (P10-R19).
- Godot version is implementation baseline, not gameplay canon (P10-R25).

No contradiction requires adding a new mechanic.

---

# 20. Empirical gates carried to implementation

The following remain explicitly **UNPASSED** until prototype/playtest:
- EG7-01 exact candidate/form prediction after tutorial;
- EG7-02 zero unpreviewed camera/pixel authority;
- EG7-03 mute-clip hook comprehension and non-perspective misread;
- EG7-04 / P10-R2 felt mature-family variety;
- EG7-05 two-object readability without detached table;
- EG7-06 reduced-motion/non-audio causal comprehension;
- EV7-01 mute store-hook comprehension;
- EV7-02 measured non-expert first-clear duration;
- EV7-03 final strong-case count/diversity survival;
- EV7-04 perceived causal variety;
- EV7-05 demo finale/readability/full-game interest;
- EV7-06 final price/value perception;
- EV7-07 optional remix admission/value proof;
- EV7-08/P10-R19 Cloud integrity;
- P9-R19 keyboard-only comfort;
- P10-R21 full device-path proof;
- solver production-cost/frontier profiling;
- transformation/art-production cost versus reusable-asset ceiling.

Any empirical gate may trigger content reduction, presentation change within frozen semantics, Cloud removal, price change, or product kill. It may not silently create unrelated gameplay systems.

---

# 21. Phase-10 acceptance checklist

1. Hour-4 repetition attacked with felt-family and kill gates — PASS ON PAPER.
2. Free-camera misread boundary explicit — PASS ON PAPER.
3. Detached-menu collapse blocked — PASS ON PAPER.
4. Blind enumeration/dominant strategies attacked — PASS ON PAPER, empirical verification pending.
5. Two-object identity/readability bounded — PASS ON PAPER.
6. Dynamic input arbitrariness bounded — PASS ON PAPER.
7. Content/asset/QA burden has cut ladder — PASS ON PAPER.
8. Solver explosion/fake-confidence bounded — PASS ON PAPER.
9. Traversal tax has measurable rejection gate — PASS ON PAPER.
10. Undo/history exactness preserved — PASS ON PAPER.
11. Save/content migration semantics explicit — PASS ON PAPER.
12. Cloud branch safety has release kill switch — PASS ON PAPER.
13. Demo import bounded/versioned — PASS ON PAPER.
14. Controller/keyboard/Deck proof required before bulk content — PASS ON PAPER.
15. Accessibility paths retain semantics — PASS ON PAPER.
16. Hints cannot become correctness oracle — PASS ON PAPER.
17. Price/value claims remain empirical — PASS ON PAPER.
18. Runtime pin rechecked and bounded — PASS ON PAPER.
19. Cross-spec authority reconciled — PASS ON PAPER.
20. Fatal paper contradiction remaining — **NO**.

# Phase-10 result

**PHASE 10 — ADVERSARIAL REVIEW: COMPLETE.**

No unresolved fatal paper-level flaw remains. The design still has serious empirical risks — especially mature felt variety, authored-Frame comprehension, two-object readability, production cost and demo/value proof — but each has an explicit gate/kill response rather than an undefined mechanic.

## NEXT ACTION
Proceed directly to Phase 11 Specification Freeze. Produce `GAME7_FINAL_FREEZE.md` with canonical authority order, all narrowed gameplay/content/UX/commercial/technical contracts, P9/P10 repairs, empirical gates, scope/cut ladder and implementation acceptance boundaries. Set `DESIGN COMPLETE = YES` only if a fresh implementation session would not need to invent important gameplay.