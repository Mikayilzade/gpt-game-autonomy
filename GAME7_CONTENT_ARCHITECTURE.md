# GAME #007 — LAST KNOWN SHAPE — CONTENT ARCHITECTURE

Last updated: 2026-08-30
Phase: **5 — Content Architecture**
Selected concept: **G7C02 Last Known Shape**
Production implementation started: **NO**
DESIGN COMPLETE: **NO**

`GAME7_PRODUCT_THESIS.md` remains authority for product identity. `GAME7_MECHANICAL_ARCHITECTURE.md` remains authority for exact mechanics/domain semantics. This file is authority for authored case structure, campaign progression, content data, diversity constraints, validation, demo composition, and optional mastery/remix admission.

---

# 1. Content thesis

Last Known Shape must prove that one observation-write rule supports a full premium puzzle campaign without turning into `find the right frame, transform object, put it in socket` repetition.

Content therefore escalates through **causal composition**, not a late-game pile of magical mechanics. A mature case should force the player to reason about at least two of these at once:
- preserve a useful remembered form;
- deliberately overwrite a useful remembered form later;
- accept a current affordance that harms future access;
- relocate an object between observations;
- change an authored occluder input;
- observe two objects in a required order;
- avoid destructive re-observation;
- reuse the same form for a different purpose after world state changes.

New meshes, new room art, new colors, or a new form name do **not** count as causal variety.

---

# 2. Product-scale counts

## Main campaign
- target: **C01–C34**;
- acceptable release floor after cuts: **28** strong main cases;
- preferred first-clear time: **5–8 hours** if playtest evidence supports it;
- minimum acceptable product first-clear target: **4–7 hours**.

A case may be cut rather than padded. If fewer than 28 causally strong cases survive validation using the frozen vocabulary, the design requires adversarial review rather than unrelated mechanic growth.

## Demo
- **DEMO01–DEMO06**;
- target first clear: **20–30 minutes**;
- demo is representative, not a tutorial-only teaser;
- demo must reach preserve/overwrite and one readable two-object order dependency.

## Optional mastery/remix
- target: **R01–R06 maximum**;
- minimum: zero; optional content ships only if it is causally distinct;
- no remix exists merely to increase Steam-hour count.

---

# 3. Campaign teaching bands

## Band A — Write reality: C01–C05
Purpose: establish the causal sentence with one object, no dynamic occluder dependency.

### C01 — Last Seen
One object, one frame, two forms. Preview -> commit -> leave observation -> physical resolution -> use form to reach goal.

### C02 — Looking Again
Same object, second frame. Player learns that entering/previewing does nothing, but COMMIT overwrites remembered form.

### C03 — Useful Overwrite
First explicit `form A is useful now, form B is useful later` case.

### C04 — Move Without Forgetting
Object is relocated between observation events. Remembered form persists through movement.

### C05 — Bad but Legal
A tempting legal overwrite blocks progress until Undo/alternate planning. Teaches that preview is exact but does not choose for the player.

Band constraints:
- one reasoning-critical object;
- <=2 useful forms per case except C05 may expose a third preview as decoy only if readable;
- <=2 relevant frames;
- no dynamic occluder inputs;
- no case-specific exception text.

## Band B — Affordance conflict: C06–C10
Purpose: make form choice about downstream function, not visual size.

Introduce:
- bridge/step/blocker/fit-narrow/reach-high/contact-family affordances through global tags;
- access self-block;
- fixed authored mask variants.

Required cases:
- at least two where `largest/longest form` is inferior;
- at least two where a form that opens one route closes another;
- at least one where preserving the current remembered form is better than committing the visible new candidate.

C10 must synthesize preserve -> physical exploit -> relocate -> overwrite -> exploit.

## Band C — State-dependent observation: C11–C15
Purpose: the same frame/object relationship can matter differently because declared world inputs change.

Introduce:
- fixed mask family distinctions;
- one named dynamic occluder input where required;
- first explicit authored occluder dependency;
- destructive re-observation risk.

Rules:
- dynamic occlusion remains symbolic/canonical, never camera-ray authority;
- each case has <=1 dynamic occluder input per relevant frame unless an explicit validation exception is approved later;
- UI/presentation must make the dependency inferable from the physical scene before committing.

C15 must require player to change occluder state, observe, then change the occluder back while preserving the target object's memory.

## Band D — Two memories: C16–C22
Purpose: introduce two reasoning-critical objects and observation order.

Required teaching order:
- C16: two transformable objects, but only one is changed at a time and no cross-dependency;
- C17: A's physical form changes access to B's frame;
- C18: A is a declared occluder input for B;
- C19: observe B under A, then overwrite A without changing B;
- C20–C22: increasingly coupled order, relocation, receiver consequences.

Hard ceiling:
- <=2 reasoning-critical transformable objects;
- <=3 useful forms/object;
- <=4 relevant frames/case;
- no recursive candidate dependency.

At least three cases in this band must have a correct solution where the first apparently `progressive` observation must later be undone/overwritten deliberately.

## Band E — Preservation chains: C23–C28
Purpose: deepen planning without adding primitives.

Cases combine 3–4 causal dimensions from:
- access self-block;
- relocation;
- occluder dependency;
- two-object order;
- preserve useful remembered state;
- destructive re-observation;
- receiver/mechanism state;
- state-dependent form reuse.

Every case must require more than blind candidate cycling. At least one later action's value must depend on a state created earlier.

## Band F — Synthesis: C29–C34
Purpose: final mastery using the same vocabulary.

No new magical rule family after C28.

C29–C33 each emphasize a different dominant causal skeleton. C34 is a capstone with two objects, <=4 frames, <=3 useful forms/object, and at least two preserve/overwrite decisions separated by physical exploitation.

C34 must be solvable without a third reasoning-critical object and without precision/timing.

---

# 4. Canonical content families

Each case receives one **dominant family** and zero or more supporting tags.

## F1 — PRESERVE_OVERWRITE
Current remembered form remains useful across an intermediate action; overwrite timing is the core decision.

## F2 — ACCESS_SELF_BLOCK
A physical form changes access to the observation frame/route needed later. Player must sequence transformation and movement around self-created access changes.

## F3 — AFFORDANCE_TRADEOFF
Candidate forms produce conflicting globally defined affordances; no form dominates across the whole case.

## F4 — RELOCATION
The object must move between pose slots while memory persists; correct observation is tied to where the object will be used later.

## F5 — OCCLUDER_DEPENDENCY
A named canonical object/form/pose input changes another object's candidate form at an authored frame.

## F6 — DESTRUCTIVE_REOBSERVATION
A frame that is useful to inspect later becomes dangerous to commit because it would erase a needed memory.

## F7 — TWO_OBJECT_ORDER
A then B differs materially from B then A through access, occlusion, receiver, or movement consequences.

## F8 — STATE_DEPENDENT_REUSE
The same remembered form has different strategic value later because another object/mechanism/player-access state changed.

Supporting tag vocabulary may include:
`FIXED_MASK`, `RECEIVER_CONTACT`, `NARROW_FIT`, `BRIDGE`, `STEP`, `BLOCKER`, `REACH_HIGH`, `FRAME_ACCESS`, `MECHANISM_GATE`, `PRESERVE_ACROSS_MOVE`, `UNDO_TEACHING`, `MULTI_STAGE_RETURN`.

No new dominant family may be invented by a level author without specification review.

---

# 5. Hard diversity quotas

For mature campaign **C11–C34**:
1. no three consecutive cases share the same dominant family;
2. every five-case window contains at least **3** dominant families;
3. C23–C34 contains at least **6** of F1–F8;
4. no dominant family occupies more than **30%** of C11–C34;
5. F5 OCCLUDER_DEPENDENCY occupies no more than **25%** of mature cases so occlusion does not become the whole game;
6. F7 TWO_OBJECT_ORDER appears in at least **5** main cases after C16, but no more than **9**;
7. at least **8** mature cases require physical relocation between two observation commits;
8. at least **8** mature cases require preserving an already useful remembered form rather than immediately accepting a visible candidate;
9. at least **6** mature cases contain a legal attractive overwrite that is strategically wrong for a clear downstream reason;
10. art/layout/theme changes never satisfy a missing family quota.

A validator must compute these quotas from case metadata.

---

# 6. Anti-isomorphism contract

Every C11–C34 case stores a compact causal-skeleton vector:

`[preserve_depth, overwrite_count, access_self_block, relocation_count, dynamic_occluder_count, object_order_depth, receiver_dependency_count, state_dependent_reuse, destructive_reobservation, required_return_path]`

Recommended values are small integers / booleans; exact ranges live in tooling.

Two cases are `near-isomorphic` for content review if:
- dominant family matches;
- useful-form count pattern matches;
- object count matches;
- frame count matches;
- and at least 7/10 causal vector dimensions match.

Hard rule:
- no adjacent mature cases may be near-isomorphic;
- no three near-isomorphic mature cases may ship anywhere in campaign without one being materially redesigned or cut.

Different room geometry alone does not break isomorphism.

---

# 7. Exact case data schema

Each authored case must expose data equivalent to:

```text
case_id
campaign_band
unlock_dependencies[]
dominant_family
supporting_tags[]
causal_skeleton_vector
player_start_region
goal_predicate_id
objects[]
  object_id
  object_definition_id
  start_pose_slot_id
  start_remembered_form_id
  start_physical_form_id
  allowed_pose_slots[]
  useful_form_ids[]
frames[]
  frame_id
  eligible_object_ids[]
  transform_rule_id
  fixed_mask_id|null
  occluder_inputs[]
  access_predicate_id
  teaching_annotation_id|null
pose_slots[]
receivers[]
mechanisms[]
ordinary_navigation_edges[]
expected_shortest_solution_band
solution_family_count_floor
solution_family_count_cap_for_tooling
required_causal_facts[]
forbidden_shortcut_policies[]
hint_fact_ids[]
mastery_eligibility
validator_budget_profile
presentation_theme_id
```

All gameplay dependencies must be declared in this data/global definitions. No case script may silently run custom observation semantics.

---

# 8. Reusable vocabulary ceiling

## Object archetypes
Target reusable physical archetypes: **4–6** visual families, each able to expose multiple authored forms through one shared global form/affordance system.

The campaign may not depend on 34 bespoke hero objects.

## Forms
Ordinary case:
- 2–3 useful forms/object;
- 4th form only as rare proven exception and never required to explain a new rule family.

Product-wide form vocabulary should reuse affordance tags even when meshes differ.

## Observation transform/mask families
Target product vocabulary: **5–7** reusable transform/mask families, such as:
- direct authored alternate form;
- fixed-slot mask selection;
- pose-dependent authored transform;
- named-occluder binary transform;
- named-occluder + pose transform;
- frame-specific finite remap;
- mechanism-state finite remap.

These are implementation families, not magical player-facing rules. Every result is previewed exactly.

## Receivers/mechanisms
Prefer a compact set of global consumers:
- floor/contact receiver;
- bridge/span requirement;
- narrow passage compatibility;
- height/reach receiver;
- simple gate/shutter;
- simple lift/platform state.

No bespoke machine minigame.

---

# 9. Anti-dominant-strategy requirements

Every mature case C11+ declares which cheap policies it rejects.

Required policy set:
- `ALWAYS_COMMIT_VISIBLE_CANDIDATE`;
- `KEEP_LARGEST_FORM`;
- `KEEP_CURRENT_FORM_FOREVER`;
- `OBSERVE_EVERY_FRAME_BEFORE_MOVING`;
- `SOLVE_OBJECT_A_COMPLETELY_THEN_B`;
- `MOVE_OBJECT_DIRECTLY_TO_RECEIVER_THEN_FIND_FORM`;
- `TRY_ALL_CANDIDATES_UNTIL_GOAL`.

Campaign quotas:
- each policy above must be falsified by at least **4** main cases;
- `KEEP_LARGEST_FORM` and `ALWAYS_COMMIT_VISIBLE_CANDIDATE` must each be falsified by at least **8**;
- at least **6** mature cases require interleaving observation and physical movement such that all-observation-first fails.

The validator may use policy bots for structural policies; others require authored reasoning assertions + solver comparison.

---

# 10. Anti-blind-enumeration rules

Free Undo remains baseline. Anti-bruteforce design must come from causal state dependence, not punishment.

From C11 onward:
- a case may not be solved by one blind sequence of visiting every frame and accepting every different candidate once;
- from C16 onward, representative correct solutions must include at least one `preserve` decision where a legal commit is intentionally skipped/cancelled;
- from C23 onward, at least one later useful candidate must become reachable/valuable only after a physical state change;
- candidate count alone is never used as difficulty.

Tooling records simple enumeration-policy success/failure. If an enumeration bot solves too much of a band, cases are redesigned.

---

# 11. Authored mask / occluder readability

A dynamic occluder dependency is valid only when:
1. the occluder object is explicitly named in frame data;
2. qualifying pose/form states are finite and canonical;
3. the player can visually identify the relationship from the frame scene without pixel counting;
4. preview exposes the resulting exact candidate before commit;
5. changing irrelevant objects never changes candidate;
6. renderer/camera resolution cannot alter outcome.

Ordinary frame ceiling:
- 0–1 dynamic occluder input;
- 2 only in rare late case after validator/readability review;
- never >2.

A dynamic occluder may not depend on another object's preview candidate, animation interpolation, or hidden collision callback.

Fixed masks must use readable authored geometry and may not hide a one-pixel alignment puzzle.

---

# 12. Solver / validator pipeline

Every shippable main/demo/remix case passes:

## V1 — Schema validation
All IDs resolve; no undeclared form/frame/receiver dependency; no private callback.

## V2 — Reachability validation
Initial state valid; all required authored regions/frames intended to be usable are reachable in at least one canonical solution path.

## V3 — Deterministic candidate validation
For every reachable frame/object pre-state within budget, `CANDIDATE` returns one deterministic form or stable rejection.

## V4 — Solver termination
Canonical solver terminates under configured authoring budget and reports:
- states visited;
- transitions expanded;
- duplicate states pruned;
- shortest semantic command length;
- number of solutions up to cap;
- termination reason.

## V5 — Shortcut policy validation
Run declared cheap-policy bots and compare against authored forbidden shortcut set.

## V6 — Causal diversity validation
Compute dominant-family windows, causal vectors, near-isomorphism flags, and campaign quotas.

## V7 — Accessibility-validity lint
Reject cases whose required information is encoded only by color/audio or whose required observation action depends on precision pointer/camera movement.

## V8 — Presentation dependency lint
Reject any case whose gameplay result refers to mesh pixels, renderer visibility, animation frame, or camera transform.

### Practical budgets
Initial authoring target per ordinary case:
- <=150k canonical states visited;
- <=1.5M transitions expanded;
- <=5 seconds in optimized headless validation on target CI-class hardware is a design target, not yet a frozen performance guarantee.

Late capstone may use a named larger profile up to 5x ordinary budget only if solver memory/readability remain acceptable. Over-budget cases are simplified/cut; no bespoke semantic pruning.

---

# 13. Demo architecture

## DEMO01 — Remember
One frame, one object. Commit and leave -> form becomes real.

## DEMO02 — Overwrite
Second frame proves memory replacement.

## DEMO03 — Two Uses
Two forms, conflicting affordances; preserve then overwrite.

## DEMO04 — Mask
Fixed authored mask changes candidate deterministically.

## DEMO05 — Keep It
A visible legal candidate must be declined/cancelled to preserve a useful remembered form across relocation.

## DEMO06 — Order
Two objects. A's form changes B's observation candidate/access; B is observed, then A is overwritten while B keeps memory. Ends on a clear two-memory causal payoff.

Conversion thesis:
- player should leave demo understanding this is not merely `perspective magic`;
- demo proves memory persistence, deliberate overwrite, physical exploitation, and two-object order;
- final demo beat should expose richer full-game possibility without introducing an unavailable mechanic.

Demo progress/import policy belongs to Phase 7/8, not this file.

---

# 14. Optional mastery/remix admission

A remix/mastery case may ship only if it changes at least one causal dependency, not merely:
- fewer moves;
- faster completion;
- smaller Undo count;
- same case with recolored forms;
- same solution with a moved goal.

Admission requires one of:
- dominant family changes;
- solution order changes because access/occluder relation changes;
- preserve/overwrite dependency inverts;
- object roles swap under different canonical affordance relation;
- a previously optional state-dependent reuse becomes required.

Remix must pass the same solver, accessibility, anti-isomorphism and deterministic-candidate validators as campaign.

No par-time mastery. No punishment for Undo.

---

# 15. Authoring workflow

1. choose dominant family + supporting tags;
2. write causal skeleton in plain language before layout;
3. define object/form/frame/receiver data;
4. hand-solve expected causal chain;
5. run solver and shortcut bots;
6. inspect solution families / dead-state structure;
7. run causal-vector/isomorphism check against neighboring campaign cases;
8. build presentation layout only after causal structure survives;
9. validate controller/keyboard semantic interaction path in Phase 6 tooling;
10. playtest for prediction/explanation, not merely completion rate.

A visually attractive room is not a case until its causal skeleton passes validation.

---

# 16. Content acceptance tests — 55

CT-01 C01 can be solved with one object and one relevant frame.
CT-02 C01 requires physical exploitation after remembered form resolves.
CT-03 C02 proves preview alone does not overwrite memory.
CT-04 C03 requires at least one deliberate overwrite.
CT-05 C04 proves moving an object does not erase remembered form.
CT-06 C05 contains a legal strategically poor commit recoverable by Undo.
CT-07 C01–C05 contain no dynamic occluder dependency.
CT-08 C06–C10 include at least two cases where largest form is not globally best.
CT-09 C06–C10 include at least two access-self-block cases.
CT-10 C10 requires preserve -> exploit -> relocate -> overwrite -> exploit.
CT-11 C11–C15 use only declared symbolic mask/occluder inputs.
CT-12 C15 requires changing an occluder state and later preserving the target memory while changing occluder back.
CT-13 C16 introduces two objects without requiring cross-dependency.
CT-14 C17 makes A's physical form change B-frame access.
CT-15 C18 uses A as explicit candidate input for B.
CT-16 C19 proves changing A after B commit does not retroactively alter B memory.
CT-17 C16–C22 never require >2 reasoning-critical transformable objects.
CT-18 C23–C28 each combine at least three causal dimensions.
CT-19 C29–C34 introduce no new primitive family.
CT-20 C34 uses <=2 reasoning-critical objects.
CT-21 C34 uses <=4 relevant frames.
CT-22 C34 uses <=3 useful forms/object.
CT-23 No three consecutive mature cases share one dominant family.
CT-24 Every five-case mature window contains >=3 dominant families.
CT-25 C23–C34 collectively contain >=6 of F1–F8.
CT-26 No dominant family exceeds 30% of C11–C34.
CT-27 F5 occupies <=25% of mature cases.
CT-28 F7 appears in at least 5 and no more than 9 main cases after C16.
CT-29 At least 8 mature cases require relocation between observation commits.
CT-30 At least 8 mature cases require preserving a useful remembered form despite a legal visible candidate.
CT-31 At least 6 mature cases contain an attractive-but-wrong legal overwrite.
CT-32 No adjacent mature cases are near-isomorphic under the defined vector test.
CT-33 No three near-isomorphic mature cases ship anywhere in campaign.
CT-34 Every case resolves all schema IDs.
CT-35 Every gameplay dependency is declared in data/global rules.
CT-36 No case script implements a private observation rule.
CT-37 Every reachable legal frame/object state has deterministic candidate result or stable rejection.
CT-38 Every main case solver terminates within its configured budget profile.
CT-39 Solver metrics include visited, expanded, duplicate-pruned, shortest length, capped solution count and termination reason.
CT-40 Every C11+ case declares cheap-policy rejection expectations.
CT-41 KEEP_LARGEST_FORM is falsified by >=8 main cases.
CT-42 ALWAYS_COMMIT_VISIBLE_CANDIDATE is falsified by >=8 main cases.
CT-43 Every listed cheap policy is falsified by >=4 main cases.
CT-44 At least 6 mature cases require interleaved observation and movement so all-observation-first fails.
CT-45 From C16 onward representative correct solutions include a deliberate preserve/skip decision.
CT-46 From C23 onward each case has later candidate value/reachability changed by prior physical state.
CT-47 Candidate count alone is never the only reason a later case is harder.
CT-48 Dynamic occluder inputs are explicit canonical object/form/pose predicates.
CT-49 Irrelevant visual occlusion never changes candidate form.
CT-50 Ordinary frames have <=1 dynamic occluder input; any two-input exception is explicitly tagged/reviewed.
CT-51 No frame has >2 dynamic occluder inputs.
CT-52 DEMO01–06 prove commit, overwrite, conflicting affordances, fixed mask, preserve decision and two-object order respectively.
CT-53 Demo contains no free-camera/pixel-authority puzzle.
CT-54 Remix admission rejects cosmetic/layout-only variants.
CT-55 All remix/mastery content passes the same determinism, solver, accessibility and anti-isomorphism checks as main campaign.

---

# 17. Phase-5 result

**PHASE 5 — CONTENT ARCHITECTURE: COMPLETE ON PAPER.**

The campaign now has a bounded C01–C34 teaching/synthesis structure, DEMO01–DEMO06, eight causal families, hard diversity and anti-isomorphism quotas, a declared data schema, mask/occluder readability limits, anti-dominant-policy requirements, solver/validator pipeline, content budgets, remix admission rules and 55 acceptance tests.

No production implementation has begun.

## NEXT ACTION
Phase 6 — UX / Presentation Architecture. Define physical-world-first observation interaction, exact preview/commit/leave feedback, current-memory inspection, semantic focus for controller/keyboard, object/frame selection, overwrite warnings without solving the puzzle, two-object identity/readability, mask/occluder explanation, camera policy, HUD/menu/onboarding, Undo/Redo, reduced-motion/non-audio/high-contrast paths, Steam Deck 1280x800, persistence-facing UI, and >=50 UX acceptance tests.