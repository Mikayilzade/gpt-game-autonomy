# GAME #015 — PHASE 5 CONTENT ARCHITECTURE

Date: 2026-09-03
Status: PHASE 5 COMPLETE
Working title: **FRESH COAT**
Design complete: NO

## 0. Authority and scope
This file freezes the authored content system for the 24-case main campaign. It adds no new gameplay mechanics beyond `GAME15_MECHANICAL_ARCHITECTURE.md`.

Mechanical ceiling remains absolute for the main campaign:
- maximum two fixed spray passes;
- maximum one rearrangement boundary;
- 2–5 objects, with 4 the normal late-game ceiling and 5 exceptional;
- discrete sockets and orthogonal poses only;
- exact semantic atomic-region exposure/history truth;
- no continuous physics, free aim, timers, resources, third coat or second rearrangement.

Content exists to expose new deductions from the frozen grammar, not to disguise repetition with new meshes, colors or story dressing.

---

## 1. Campaign architecture: eight reasoning families

The campaign contains exactly 24 primary cases, grouped as 8 families of 3. Each family teaches one new reasoning pressure and then combines it with earlier pressures.

### F1 — Occlusion is a mask: FC01–FC03
Purpose: teach direct exposed/occluded complement and the fact that the blocker is a physical workpiece.
- FC01: one blocker protects one required region while leaving another exposed.
- FC02: orientation changes which semantic region is protected; same objects, different exposure relation.
- FC03: first self-obligated masker: the object used as a blocker also has one required painted region.

### F2 — Differential neighboring-face protection: FC04–FC06
Purpose: move from whole-face masking to local spatial discrimination without tiny regions.
- FC04: paint one region while an adjacent region stays raw.
- FC05: two plausible blocker choices differ by one readable leakage relation.
- FC06: the A-stage solution that satisfies the immediate neighbor also preserves access needed by a later B-stage, introducing future-access reasoning without yet requiring ordered A->B history.

### F3 — Masks are constrained resources: FC07–FC09
Purpose: make self-obligation central rather than a tutorial exception.
- FC07: canonical self-obligated masker proof.
- FC08: Y masks X while Y is itself partially masked by Z; dependency chain of depth two.
- FC09: three-object dependency chain solved backward from the terminal object's own paint obligation.

### F4 — Pass-specific exposure: FC10–FC12
Purpose: introduce two passes and the single rearrangement boundary.
- FC10: A-only versus B-only using two objects and an obvious rearrangement.
- FC11: RAW + A-only + B-only coexist on one workpiece; player must reason about both arrangements together.
- FC12: first arrangement must intentionally preserve a region for later B access; immediate A-stage convenience is a trap.

### F5 — Ordered history: FC13–FC15
Purpose: establish that final appearance is not enough; order/provenance matters.
- FC13: A_THEN_B introduced beside A_ONLY with low object count.
- FC14: canonical adjacent A_THEN_B / B_ONLY differential masking case.
- FC15: A_THEN_B and RAW must coexist across both stages, forcing persistent protection plus ordered exposure.

### F6 — Cavity reveal: FC16–FC18
Purpose: use ordinary exact self-occlusion/aperture geometry to change visibility topology.
- FC16: cavity region hidden during A and exposed during B after moving a blocker.
- FC17: exposing cavity for B risks exposing a RAW rim; player must distinguish aperture access from surrounding surface access.
- FC18: canonical late cavity case where target object must not rotate; another object moves to change the cavity exposure relation.

### F7 — Mask-role reversal: FC19–FC21
Purpose: the same constrained objects exchange blocker/recipient roles between passes.
- FC19: X masks Y for A; Y masks X for B.
- FC20: both role-reversing objects carry own-history targets, removing disposable-mask thinking.
- FC21: three-object role-reversal chain; canonical late proof from Mechanical Architecture.

### F8 — Coupled capstones: FC22–FC24
Purpose: combine the learned grammar without adding a mechanic.
- FC22: two apparently independent obligations compete for one critical masking relation/socket.
- FC23: one masker serves two different objects across the two stages and must itself end B_ONLY on a designated region.
- FC24: four-object final capstone with RAW, A_ONLY, B_ONLY and A_THEN_B, one cavity relation, role reversal and a shared masking dependency. No fifth object, no third pass, no new rule.

---

## 2. Reusable solid vocabulary

The main campaign should be buildable from 6–8 highly readable solids. Shape identity exists only where it creates distinct exposure relations.

### S1 — Brick
Rectangular cuboid with large planar faces. Baseline masker/recipient; excellent for tutorials and readable adjacency.

### S2 — Slab
Thin wide cuboid. Creates broad shielding while remaining visually easy to trace. Often used when a large blocker must leave another region exposed.

### S3 — Step
Two-height orthogonal solid. Creates readable partial shielding and an elevated exposed region without arbitrary micro-geometry.

### S4 — L-block
Orthogonal L profile. Supports corner shielding and two-direction relationships while keeping silhouette obvious.

### S5 — U-block / shallow cavity
Chunky U or tray-like solid with large aperture, rim and cavity floor/inner wall regions. Used only from F6 onward except visual foreshadowing.

### S6 — Hood
Three-sided cover with one large open side. Useful for shielding a neighbor while keeping its own outer region exposed.

### S7 — Pillar
Tall narrow cuboid. Creates lane blocking and role reversal without adding shape complexity.

### S8 — Bridge (optional, only if needed after authored review)
Two legs with a broad top span. Permitted only if it produces a non-isomorphic masking relation not achievable with S1–S7. It is not required for the baseline 24 cases.

Guardrails:
- no rounded gameplay surfaces;
- no decorative holes that affect exposure;
- no thin fins/slivers used as difficulty;
- no shape variant may exist solely to create another arbitrary exposure subset;
- semantic region count, not mesh detail, is the content complexity unit.

---

## 3. Socket-frame motifs

Sockets are authored spatial relationships, not arbitrary coordinates. Reuse a small motif vocabulary so players learn to read scenes.

### M1 — Side-by-side lane
Two or more aligned sockets along a booth-orthogonal row. Supports direct shielding and role swaps.

### M2 — Front/back mask lane
Depth-separated sockets along the spray ray. Makes blocker/recipient relation visually obvious.

### M3 — Raised shelf
One high socket and one lower socket. Used for top/side differential exposure and stepped silhouettes.

### M4 — Cradle / cavity insertion
One socket positions a compatible smaller workpiece at or across a larger object's aperture. This is authored nesting, never continuous insertion.

### M5 — Cross lane
Two orthogonal lanes meeting at a shared central masking relation. Useful for coupled obligations and capstones.

### M6 — Parking bay
A clearly shielded or clearly exposed secondary socket used after A. Parking may matter because of actual exposure, never because the game labels it safe.

### M7 — Shared critical socket
A single relation that can satisfy one of two masking jobs at a stage. Used sparingly in F8 to create coupling; it must not become generic resource-allocation UI.

Maximum simultaneous socket count should generally be object count + 1 or +2. Extra empty sockets are forbidden when they only enlarge brute-force search.

---

## 4. Booth-direction vocabulary

Use at most three canonical world directions across the product, chosen for stable readable camera framing:
- `D_FRONT`: horizontal spray from the primary booth side;
- `D_TOP`: vertical downward spray;
- `D_SIDE`: horizontal orthogonal side direction.

A case uses one fixed direction per spray stage. Most two-pass cases should use either the same direction with rearrangement or one simple change between two canonical directions. Direction changes are authored stage data and never player-selected.

No diagonal or perspective-dependent spray direction is needed for the main campaign.

---

## 5. Case data schema

Each shipping case must have explicit authored and derived fields.

### 5.1 Authored identity / progression
- `case_id` (`FC01`…`FC24`)
- `family_id` (`F1`…`F8`)
- `display_order`
- `title_key` (flavor only)
- `prerequisite_case_ids`
- `tutorial_flags`
- `demo_included` boolean
- `expected_reasoning_tags`
- `empirical_gate_tags`

### 5.2 Authored object data
For each instance:
- `object_instance_id`
- `solid_archetype_id`
- `visual_identity_marker`
- `active_region_ids`
- `allowed_socket_ids_by_stage`
- `allowed_orientation_ids_by_socket_stage`
- `symmetry_class`

### 5.3 Authored spatial data
- socket transforms and motif IDs
- compatibility tags
- stage-specific legal occupancy/collision relations
- authored nesting/contact relations
- booth direction per stage
- stage count (1 or 2)
- rearrangement allowed boolean

### 5.4 Authored target data
Per targeted atomic region:
- `target_history`: RAW / A_ONLY / B_ONLY / A_THEN_B / onboarding-only PAINTED_AT_LEAST_ONCE
- target display grouping
- optional tutorial emphasis

### 5.5 Authored proof metadata — developer-only
- `intended_proof_facts[]`
- `intended_dependency_edges[]`
- `intended_elimination_steps[]`
- `known_legitimate_alternate_solution_classes[]`
- `repetition_exception_rationale` if similarity is intentionally accepted

This metadata is never part of normal player-facing truth.

### 5.6 Derived certification data
Generated from geometry and authored legal configurations:
- exact atomic exposure per legal arrangement/stage;
- legal A->B transitions;
- all successful normalized solution classes;
- necessary exposure/occlusion facts;
- region partial-coverage violations;
- normalized repetition signature `R`;
- symmetry quotient statistics;
- blind-trial state counts;
- target-history reachability;
- solution-class count and trivial-solution warnings.

Derived data must never be manually authored to override geometry truth.

---

## 6. Complexity budgets

These are content acceptance budgets, not difficulty scores.

### F1
- objects: 2–3
- targeted atomic regions: 2–5
- legal poses/object: 2–3 typical
- stage count: 1
- solution classes after symmetry: 1–3
- dependency depth: 0–1

### F2
- objects: 2–3
- targeted regions: 3–7
- poses/object: 2–4
- stages: 1, with FC06 allowed 2
- one clearly readable adjacent-region differential relation required

### F3
- objects: 2–3
- targeted regions: 4–8
- self-obligated maskers: 1–2
- dependency depth: 1 for FC07, 2 for FC08–FC09
- avoid more than one cavity-like relation

### F4
- objects: 2–3
- targeted regions: 4–9
- stages: exactly 2
- rearrangement: yes
- target-history classes: up to 3 of RAW/A_ONLY/B_ONLY
- A-stage legal arrangement classes should normally be <=50 after symmetry; large raw Cartesian pose counts must collapse through authored compatibility.

### F5
- objects: 2–4
- targeted regions: 5–10
- target-history classes: 3–4 including A_THEN_B
- at least one self-obligated masker from FC14 onward
- no more than two distinct local differential relations in one case before FC15

### F6
- objects: 3–4
- targeted regions: 6–11
- cavity/aperture motifs: exactly one primary cavity relation per case
- atomic cavity/rim subdivisions must be chunky and visually inspectable
- target object rotation should be constrained only by legal-pose design, never hidden lock rules

### F7
- objects: 2–4
- targeted regions: 6–12
- role-reversal edges: 1 for FC19, 1–2 FC20, up to 2 meaningful edges FC21
- dependency graph depth <=3
- no five-object role chain

### F8
- objects: 4 normal; 5 only if FC23/FC24 cannot pass freshness/readability with 4, and 4 is strongly preferred
- targeted regions: 8–14
- stages: 2; one rearrangement
- one cavity relation maximum
- 2–3 dependency edges, not a dense all-to-all graph
- all four main history classes may coexist
- final successful normalized solution classes target 1–4; more require explicit review for trivial alternatives

Global visual budget:
- no shipping case should require more than ~16 meaningful atomic regions visible/inspectable at once across all active workpieces;
- any single face with more than 3 semantic atomic regions requires special justification;
- tiny sliver regions are automatic rejection candidates.

---

## 7. Full 24-case deep outline

### FC01 — Cover the Top
Objects: Brick T + Slab M. One FRONT/TOP-readable A pass.
Teach: direct masking.
Deduction: RAW target determines blocker placement; exposed side must remain unblocked.
Non-duplicate value: establishes exposure complement with one binary spatial relation.

### FC02 — Turn the Work
Objects: Brick + Slab. One A pass; target brick has two named regions on different faces.
Teach: pose changes semantic face exposure.
Deduction: blocker position alone is insufficient; target pose must align the protected face with the masking lane.
Non-duplicate: first object-pose deduction rather than blocker-position deduction.

### FC03 — The Mask Gets Painted
Objects: two Bricks or Brick + Slab.
Teach: masker has own target.
Deduction: of two blocking poses, only one both protects T and exposes M's required region.
Non-duplicate: creates first dependency edge between recipient and blocker obligations.

### FC04 — Next Door
Objects: Brick T + narrow Pillar/Slab.
Teach: adjacent region differential.
Deduction: blocker must cover T.left while T.right remains exposed.
Non-duplicate: protection is local, not whole-object.

### FC05 — Too Wide
Objects: T plus two candidate maskers of different silhouettes.
Teach: geometry matters, not symbolic blocker identity.
Deduction: wide blocker protects required region but leaks/overcovers adjacent obligation; narrow/stepped relation is correct.
Non-duplicate: compare two physical masking footprints.

### FC06 — Leave a Way In
Objects: 3, two passes, one rearrangement; no A_THEN_B yet.
Teach: preserving future access.
Deduction: two A arrangements satisfy current A targets, but one blocks/eliminates the only legal B-stage exposure relation.
Non-duplicate: first cross-stage dependency; not merely local cover.

### FC07 — Useful Shield
Objects: X + Y.
Teach: canonical self-obligated masker.
Deduction: Y must shield X and simultaneously expose its own required face.
Non-duplicate: reverses mental model from disposable obstacle to constrained workpiece.

### FC08 — Shield the Shield
Objects: X, Y, Z.
Teach: dependency chain.
Deduction: Y shields X, but Z must shield a Y region while leaving Y's target region exposed.
Non-duplicate: two-level backward reasoning.

### FC09 — Work Backward
Objects: 3.
Teach: terminal obligation fixes upstream chain.
Deduction: Z's target fixes its pose; that pose determines how it can shield Y; Y relation then fixes shielding of X.
Non-duplicate: chain solved from terminal object, not target object outward.

### FC10 — Two Coats
Objects: 2, A then rearrange then B.
Teach: A_ONLY vs B_ONLY.
Deduction: one object/face must be exposed only before rearrangement, another only after.
Non-duplicate: first temporal exposure partition.

### FC11 — Save One Raw
Objects: 2–3.
Teach: RAW across both passes together with A_ONLY/B_ONLY.
Deduction: one region needs persistent shielding while neighboring regions change exposure between stages.
Non-duplicate: persistent protection becomes a two-stage invariant.

### FC12 — Don't Paint It Yet
Objects: 3.
Teach: intentional deferral.
Deduction: a tempting A exposure would satisfy a broad-looking visual goal but destroys B_ONLY target; player reserves the region for B.
Non-duplicate: future-history obligation eliminates an otherwise valid current exposure.

### FC13 — Coat Over Coat
Objects: 2–3.
Teach: A_THEN_B.
Deduction: one region must remain exposed in both stages while an adjacent A_ONLY region becomes protected for B.
Non-duplicate: same object carries persistent exposure and newly protected region.

### FC14 — Different Histories Side by Side
Objects: P,Q,R.
Teach: exact ordered-history differential.
Deduction: A_THEN_B next to B_ONLY forces A-stage asymmetric mask; B-stage removes masker while preserving its A_ONLY obligation.
Non-duplicate: canonical ordered-history proof with self-obligation.

### FC15 — Painted Twice, Never Here
Objects: 3–4.
Teach: A_THEN_B plus RAW invariant.
Deduction: one relation must keep RAW region shielded in both stages while a nearby region receives both coats.
Non-duplicate: persistent shield and persistent exposure coexist across same timeline.

### FC16 — Open the Cavity
Objects: U-block + Slab + optional Brick.
Teach: cavity self-occlusion/aperture reachability.
Deduction: remove/move aperture blocker after A so B reaches cavity; no special cavity rule.
Non-duplicate: topology of line-of-sight changes through ordinary geometry.

### FC17 — Mind the Rim
Objects: U-block + two blockers.
Teach: cavity access is not equal to exposing the rim.
Deduction: B must enter aperture while RAW rim remains occluded; one blocker relation shields rim without closing aperture.
Non-duplicate: distinguishes nested exposure channels within one chunky shape.

### FC18 — Move the Mask, Not the Part
Objects: U, S, K.
Teach: cavity reveal through blocker change while target orientation remains fixed by obligations.
Deduction: rotating U invalidates RAW rim; therefore S leaves and K takes shielding lane, opening cavity but protecting rim.
Non-duplicate: target geometry stays fixed while masks reconfigure around it.

### FC19 — Trade Places
Objects: X,Y.
Teach: simple role reversal.
Deduction: X is correctly positioned to shield Y during A; after rearrangement Y must shield X during B.
Non-duplicate: dependency edge reverses direction across stages.

### FC20 — Both Have Jobs
Objects: X,Y,Z optional.
Teach: role reversal with own-history obligations on both participants.
Deduction: each masking pose must also satisfy whether that masker itself receives A/B.
Non-duplicate: role reversal is constrained, not a free swap.

### FC21 — Three-Way Shift
Objects: X,Y,Z.
Teach: late role-reversal chain.
Deduction: use frozen Mechanical Architecture proof: RAW Y.back, A-only X.top, B-only X.side/Z.top, A_THEN_B Y.front force distinct A and B masking relations.
Non-duplicate: multiple dependency edges change direction without adding stage count.

### FC22 — One Socket, Two Needs
Objects: 4.
Teach: coupled obligations through one physical relation.
Deduction: two apparent masking tasks both want the same central socket; another object must solve one indirectly, forcing backward dependency reasoning.
Non-duplicate: first explicit coupling between subproblems that cannot be solved independently.

### FC23 — Double Duty
Objects: 4.
Teach: one workpiece masks two different recipients across stages and has own B_ONLY target.
Deduction: A pose chosen for masking recipient 1 must leave a legal B pose that masks recipient 2 while exposing its own B-only region.
Non-duplicate: one object carries two temporal masking responsibilities.

### FC24 — Final Jig
Objects: 4 preferred. Histories include RAW, A_ONLY, B_ONLY, A_THEN_B; one cavity; one role-reversal relation; one shared masking dependency.
Teach: nothing new.
Deduction structure: (1) RAW invariant removes whole pose families; (2) A_THEN_B/B_ONLY differential fixes first masker; (3) self-obligation fixes its pose; (4) cavity/rim relation constrains B rearrangement; (5) role reversal resolves shared mask relation; (6) harmless symmetry may remain.
Non-duplicate: only case combining all major pressures, but still within four objects/two passes/one rearrangement.

---

## 8. Authoring workflow

Every case must be authored spatial-first, never target-subset-first.

1. **Choose one reasoning family and one spatial motif.** State the intended deduction in one sentence before targets exist.
2. **Choose 2–4 reusable solids** and the minimum sockets/poses that make that physical relation possible.
3. **Enumerate legal configurations** using exact geometry/compatibility; remove redundant poses before target design.
4. **Inspect exposure consequences** and identify an interesting physical dependency: differential shield, self-obligation, future access, cavity relation, role reversal, shared socket, etc.
5. **Derive target histories from that relation.** Do not invent arbitrary target subsets then search for a scene that realizes them.
6. **Run exact certification** across all A/B arrangement classes.
7. **Reject trivial or degenerate solutions** where unrelated parking, symmetry or one obvious all-cover pose solves the target.
8. **Write a human-proof annotation** of at least 2 elimination facts for midgame and 3+ for late cases. These facts must be readable from ordinary target/geometry information.
9. **Compute normalized repetition signature R** and compare against every earlier campaign case.
10. **Human freshness review:** explain in plain language why the case's main deduction is not just a harder copy of an earlier case.
11. **Accessibility/readability review:** all required regions must be visible through normal inspection at handheld scale; no tiny face segmentation.
12. **Empirical queue:** tag cases needed for E1–E5 playtests.

A mathematically valid case is not automatically shippable content.

---

## 9. Human-proof and hint metadata boundary

Proof metadata is stored for authoring, QA and optional hint generation, but normal play never exposes solver state.

### Allowed stored proof facts
- necessary region exposure/occlusion at A or B;
- necessary object participation in a masking relation;
- impossible pose classes caused by a visible target obligation;
- dependency order such as “solve Y's own A_ONLY obligation before deciding how Y can mask X”;
- symmetry/equivalent harmless alternatives.

### Player-facing hint ladder, if Phase 6/7 retains hints
Hints may be derived only as progressively more explicit reasoning prompts:
1. remind a relevant target/history distinction;
2. point to a region whose exposure must differ between stages;
3. name a necessary relationship (“this face must be protected during A”) without naming socket/pose;
4. final optional strong hint may identify one required masker/recipient relationship, but never present the full arrangement.

Hints must never expose:
- complete solution arrangement;
- solver heatmaps;
- ranked candidate poses;
- number of steps from solution;
- hidden future exposure preview;
- certifier solution count as gameplay feedback.

---

## 10. Demo and tutorial subset

Target demo: **FC01–FC07 plus a compact demo finale based on FC10/FC13 grammar**, approximately 20–30 minutes depending on play speed.

For campaign numbering, the shipping demo should normally include canonical campaign cases rather than parallel duplicates. Recommended content:
- FC01 direct mask;
- FC02 orientation;
- FC03 self-obligated masker introduction;
- FC04 neighboring-face differential;
- FC05 compare masker footprints;
- FC07 stronger self-obligation;
- FC10 two-pass/rearrangement;
- a demo finale drawn from FC13 if pacing allows, or a dedicated preview instance only if it is mechanically identical and does not create separate canon.

Preferred final decision for simplicity: **demo = FC01–FC05, FC07, FC10, FC13**, with campaign progress stored against the same case IDs. FC06/FC08/FC09 remain full-game connective content and unlock naturally after purchase.

Prerequisites:
- FC02 requires FC01;
- FC03 requires FC02;
- FC04 requires FC03;
- FC05 requires FC04;
- demo jump to FC07 is allowed only through a curated demo sequence flag, not campaign prerequisite rewriting;
- FC10 demo preview may include a concise “two coats” onboarding card because FC06–09 are skipped in demo order;
- full game campaign preserves FC01→FC24 linear unlock by default, though Phase 6 may allow replay of completed cases freely.

Demo carry-over should store completion for canonical IDs; purchase should not force replay.

---

## 11. Validation and rejection gates

A case is rejected if any of the following is true:
1. its normalized repetition signature is isomorphic to an earlier case and no documented new deduction pressure exists;
2. difficulty comes mainly from extra sockets, poses or objects;
3. a simple rapid pose-cycling strategy is more natural than spatial reasoning;
4. successful play needs solver-like exposure matrices rather than readable geometry;
5. any atomic region is partially covered under a legal arrangement without authored subdivision;
6. subdivision produces tiny/sliver regions that fail handheld readability;
7. the intended solution relies on renderer pixels, camera angle, physical tolerance or hidden compatibility;
8. a self-obligated mask can be replaced by a disposable blocker without changing the proof in F3+ content where dependency is required;
9. an F4+ case splits into independent per-face assignments with no cross-stage/mask dependency;
10. F6 cavity content requires a special “inside paint” rule instead of ordinary reachability;
11. F7/F8 difficulty requires more than one rearrangement or two passes;
12. alternate solution classes trivialize the intended deduction;
13. the human-proof annotation cannot eliminate meaningful configuration classes before trial;
14. four-object inspection routinely requires x-ray/camera hunting rather than normal isolation/semantic-face UI;
15. target histories are mathematically reachable but visually indistinguishable without color-only cues.

---

## 12. Campaign freshness review

Before Phase 11 freeze, build a 24x24 similarity review using normalized signatures plus human labels.

For every case record:
- reasoning family;
- primary deduction verb;
- stage count;
- object count;
- target-history set;
- dependency graph shape;
- cavity motif yes/no;
- role-reversal edge count;
- shared-socket coupling yes/no;
- intended proof length;
- normalized solution class count.

Automatic signature similarity is a warning, not the sole verdict. Human review asks:
- If object names/colors/shapes were abstracted, would the two cases still require the same reasoning sequence?
- Does the later case create a new dependency, or merely a larger instance?
- Can the later case be explained without saying “same as FCxx, but more”?

Family case #3 may intentionally combine previous ideas, but must include a family-specific new pressure or stronger coupling.

---

## 13. Expansion boundaries

A future expansion may add more authored cases, solids or socket motifs while preserving the frozen main grammar. It should prefer:
- new non-isomorphic occlusion motifs;
- new combinations of existing history predicates;
- new cavity silhouettes that remain chunky/readable;
- alternate booth direction combinations from the same small vocabulary;
- harder dependency graphs within four objects.

An expansion must formally reopen mechanical architecture before adding:
- third coat/pass;
- second rearrangement;
- free aim;
- continuous placement/physics;
- new paint chemistry/history states;
- moving booth/nozzle during a pass;
- player-authored cutting/tape/stencils;
- timing/resource economy.

More content cannot justify breaking the two-pass/one-rearrangement identity silently.

---

## 14. Phase-5 acceptance test

Phase 5 passes because a fresh implementation/design session can now build the entire authored campaign structure without inventing:
- what each FC01–FC24 case is for;
- which reusable solids/socket motifs/directions exist;
- exact authored vs derived case data;
- per-family complexity ceilings;
- authoring/certification workflow;
- proof/hint metadata boundary;
- demo subset and carry-over identity;
- repetition/readability rejection rules;
- expansion boundaries.

The remaining open work is presentation/interaction, not content identity.

PHASE 5 = COMPLETE
DESIGN COMPLETE = NO

## NEXT ACTION — PHASE 6 UX / PRESENTATION ARCHITECTURE
Define the complete player-facing experience without changing the frozen mechanics/content: stable camera and inspection model; controller/mouse input map; object/socket/pose manipulation; target-history display; semantic-face selection; current-exposure preview; spray commit confirmation; A->B transition; unpack/result presentation; undo/reset/checkpoint interaction; menus/pause/settings; onboarding for FC01–FC05 and two-pass demo skip; hint UX boundaries; accessibility including non-color coat identity, text size, reduced motion and input remapping; save/load/resume surface; first 10 minutes and first session walkthrough; audio/visual feedback language; Steam Deck/handheld presentation assumptions. If Phase 6 becomes short, continue only into Phase 7 if no mechanical/content reopening is required.