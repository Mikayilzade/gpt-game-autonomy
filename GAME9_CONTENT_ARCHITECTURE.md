# GAME #009 — PHASE 5 CONTENT ARCHITECTURE

Status: **PHASE 5 COMPLETE / PHASE 6 READY**
Date: 2026-08-31
Selected game: **Binder's Imposition**
Production implementation: **FORBIDDEN in factory**

Authority: `START_HERE.md` -> `STATUS.md` -> `GAME_INDEX.md` -> Game #009 tournament history -> `GAME9_PRODUCT_THESIS.md` -> `GAME9_MECHANICAL_ARCHITECTURE.md` -> this file.

This file defines how the frozen mechanical vocabulary becomes a complete campaign without filler, near-isomorphic repetition, vocational-printing drift, or clerical page shuffling. It does **not** add new fold physics or new predicate families.

---

# 1. Content design objective

Binder's Imposition should feel like learning one compact physical language and then being asked increasingly surprising questions in that language.

The campaign is therefore not measured by raw puzzle count. A case earns its place only when it does at least one of the following:
- teaches a new already-frozen primitive cleanly;
- makes an old primitive interact with another in a materially new way;
- creates a false-but-plausible plan that can be disproved by reasoning;
- forces a global signature/template/role deduction before local inverse fill;
- makes the player reuse a learned mapping in a new context rather than repeat it clerically;
- creates a visually strong fold/nest/trim reveal suitable for pacing or demo value.

The content target is **30 strong campaign cases**, but release quality has priority over quota.

### Count policy
- hard minimum for a credible full campaign: **24 certified strong cases**;
- target: **30 certified strong cases**;
- soft stretch ceiling: **34**, only if additional cases survive all quality tests;
- no chapter may be padded to hit a numeric target;
- if only 26–28 cases are genuinely strong, ship the shorter campaign rather than weaken the quality floor.

A short explicit tutorial reinforcement case may be mechanically simpler than the strong-case floor, but it must be brief and must exist because the following case needs it.

---

# 2. Campaign macrostructure

The campaign uses six chapters. Chapter names are presentation-flexible; their mechanical responsibilities are frozen.

## Chapter I — The Wrong-Looking Sheet
**Purpose:** establish inverse-transform intuition before secondary constraints.

Mechanical arc:
1. T4 inverse surprise;
2. predict adjacency before Preview;
3. repeat T4 with less scaffolding;
4. T4F / binary sheet flip and orientation.

Target: **4 cases**.

Completion expectation: player can look at a T4 layout and predict at least one or two final relationships without blindly Previewing every edit.

## Chapter II — One Book, Two Sheets
**Purpose:** make nesting the first genuinely global decision.

Mechanical arc:
1. fixed outer/inner nesting;
2. player-chosen outer/inner role;
3. facing predicate;
4. same-signature grouping;
5. material role breaks an otherwise order-correct tie.

Target: **5 cases**.

Completion expectation: player understands that a wrong signature role cannot always be repaired through local page swaps.

## Chapter III — The Fold Is Not the Puzzle
**Purpose:** turn learned local mappings into primitives while global constraints become the main reasoning object.

Mechanical arc:
1. different-signature constraint;
2. same-leaf reasoning;
3. orientation-sensitive face under T4F;
4. material + facing intersection;
5. first case where several local layouts are correct but one global arrangement survives.

Target: **5 cases**.

Completion expectation: local inverse fill is fast enough that the player spends more time choosing physical roles than recalling the T4 formula.

## Chapter IV — Bigger Folds, Same Language
**Purpose:** introduce T8 and then template choice without making the game feel like memorizing unrelated formulas.

Mechanical arc:
1. guided T8 reveal;
2. T8 orientation pattern;
3. T4 vs T8 comparative reasoning;
4. two legal template choices, one globally viable;
5. mixed T4/T8 signatures with a global group/material constraint.

Target: **5 cases**.

Completion expectation: player treats fold templates as visible transforms with different domains, not trivia to memorize.

## Chapter V — What Gets Cut Away
**Purpose:** introduce required blanks, EMPTY and T6P trim logic while reusing all earlier reasoning.

Mechanical arc:
1. required blank vs EMPTY;
2. sacrificial mark must disappear;
3. trim survival + reading order;
4. partial signature plus material/facing;
5. alternative template where trim makes one branch impossible.

Target: **5 cases**.

Completion expectation: trim is understood as another deterministic final-state predicate, not a hidden destructive surprise.

## Chapter VI — Bindery Tests
**Purpose:** mature synthesis, including the three-signature role deductions promised by Phase 4.

Mechanical arc:
1. three T4 signatures with one material role deduction;
2. three signatures with orientation-capable role deduction;
3. mixed-size signatures and same/different-signature groups;
4. two-template branch + facing + material intersection;
5. blank/trim + three-role interaction;
6. final capstone using 3–4 previously taught secondary predicate families, no new rule.

Target: **6 cases**.

Completion expectation: player can state a hypothesis such as “the gold sheet must be middle because only that domain can contain both required faces,” then perform local inverse fill as proof.

### Target total
4 + 5 + 5 + 5 + 5 + 6 = **30 cases**.

---

# 3. Strong-case quality floor

Except for explicitly tagged tutorial reinforcement, every case after Chapter I must pass all applicable quality gates.

## Q1 — Global decision gate
At least one decision must remain after naïve local inverse filling, or local inverse filling must be preceded by a nontrivial signature/template/nesting deduction.

## Q2 — Constraint relevance gate
At least one secondary required predicate must materially alter the valid solution set. For mature cases, at least two secondary predicate families should interact unless the case is introducing one family for the first time.

## Q3 — No rote fill gate
A case fails if fixed template + fixed nesting + READ_ORDER uniquely determines everything and all remaining work is page placement.

## Q4 — Hypothesis gate
The intended competent solution should admit a short human statement describing why a branch/role/template is chosen or rejected.

Examples:
- “Blue must be inner because only inner owns final positions 3–6.”
- “T8 cannot be used because MAP_A would resolve inverted in every compatible slot.”
- “The sacrificial mark forces the partial template because the normal template has no cut position.”

If the only explanation is “I tried swaps until Preview became green,” the case fails.

## Q5 — Manipulation gate
Predicted competent interaction must stay under the Phase-4 ceiling of ~35 primitive transactions; target mature cases should normally be <=20 primitive-equivalent transactions after structured operations unlock.

## Q6 — Preview resilience gate
Free Preview may verify a hypothesis but must not collapse the case into a monotonic local search. At least one plausible incorrect branch should require understanding a global constraint rather than merely comparing “more green predicates.”

## Q7 — Visual reveal gate
Every chapter should contain at least one case with a strong flat-sheet -> folded-book visual transformation. The campaign cannot become a spreadsheet of predicates even if the solver is good.

## Q8 — Distinctness gate
A case must differ from its nearest campaign neighbor in more than face IDs/material colors. See anti-isomorphism rules below.

---

# 4. Exact case data schema

The content system is data-driven. A future implementation may serialize differently, but every authored case must contain the following conceptual fields.

```text
CaseDefinition
  case_id: string
  chapter_id: string
  sequence_index: int
  title_key: localization key
  case_kind: TUTORIAL | REINFORCEMENT | STANDARD | MATURE | CAPSTONE

  teaching:
    introduced_mechanics: [mechanic_id]
    reinforced_mechanics: [mechanic_id]
    required_prior_case_ids: [case_id]
    prediction_prompt: optional PredictionPrompt
    tutorial_overlays: [overlay_id]

  faces: [PageFaceDefinition]
  signatures: [SignatureDefinition]

  setup:
    allowed_templates_by_signature: map signature_id -> [template_id]
    allowed_sheet_flips_by_signature: map signature_id -> [mode]
    allowed_nest_roles_by_signature: map signature_id -> [role]
    locked_template_choices: optional map
    locked_nest_roles: optional map
    locked_slot_assignments: optional map slot_id -> face_id|EMPTY
    initial_assignments: optional map slot_id -> face_id|EMPTY
    player_face_orientation_allowed: [face_id]
    structured_tools_available: [tool_id]

  required_predicates: [PredicateDefinition]
  optional_badges: [BadgeDefinition]

  presentation:
    motif_set_id: string
    signature_visual_labels: localization keys
    preview_camera_hint: enum/string
    success_reveal_id: optional string
    ambient_variant_id: optional string

  certification:
    intended_solution_tags: [tag]
    intended_reasoning_summary: author-only string
    expected_solution_class_range: {min,max}
    expected_competent_transaction_ceiling: int
    minimum_global_branch_count: optional int
    required_quality_gates: [Q1..Q8]
    symmetry_declarations: [SymmetryDefinition]
    repetition_fingerprint_version: int

  demo_flags:
    included_in_demo: bool
    demo_order: optional int
    demo_completion_boundary: bool

  accessibility/localization:
    mechanically_required_text_tokens: [localization key]
    icon_redundancy_required: bool
    color_only_information_forbidden: true
```

### PredictionPrompt
A prediction prompt never changes puzzle validity. It asks the player to predict one observable relationship before Preview, for example:
- which two faces will become adjacent;
- which signature will become outermost;
- whether a marked face will resolve upright/inverted;
- whether a trim mark survives.

Prediction prompts are onboarding/learning instruments, not scored hidden-information questions.

---

# 5. Content families

These families recombine frozen mechanics. They are authoring lenses, not new rule systems.

## F01 — Inverse Mapping
Core question: which flat slots produce requested final positions?

Use: tutorial and reinforcement only after Chapter I unless combined with another family.

Primary knobs: T4/T4F/T8 mapping; pre-placed faces; prediction prompt.

Failure mode to avoid: rote formula exercise.

## F02 — Nest Role Deduction
Core question: which signature must be outer/middle/inner because of the final position domains?

Typical predicates: SIGNATURE_ROLE, SAME_SIGNATURE, AT_POSITION, READ_ORDER.

Strength: creates a global choice that local swapping cannot repair.

## F03 — Facing / Leaf Geometry
Core question: which faces must land across a visible spread or on opposite sides of one leaf?

Typical predicates: FACING, SAME_LEAF.

Strength: exploits physical book geometry rather than page-number arithmetic.

## F04 — Material Ownership
Core question: which physical signature can carry a named face/group?

Typical predicates: MATERIAL, SAME_SIGNATURE, SIGNATURE_ROLE.

Material remains categorical and symbolic. No cost/thickness/chemistry.

## F05 — Orientation Parity
Core question: which slot/template/flip combination yields required upright/inverted result?

Typical predicates: ORIENTATION plus T4F/T8.

Guardrail: no case may require reading tiny artwork orientation; mechanical glyphs are mandatory.

## F06 — Template Branch
Core question: two fold templates are legal, but global constraints make one viable or materially better suited.

Typical predicates: TEMPLATE plus orientation/facing/material/trim.

Guardrail: template choice must change reasoning, not merely capacity.

## F07 — Blank / Capacity Logic
Core question: where must an explicit blank exist and how is it distinguished from a truly unused sacrificial position?

Typical predicates: BLANK_AT plus required PageFace blank tokens.

Guardrail: never use semantic prose content to decide whether a page “should” be blank.

## F08 — Trim Fate
Core question: which authored mark/face must survive or disappear after T6P trim?

Typical predicate: TRIM_RESULT.

Strength: creates visually satisfying removal while remaining exact.

## F09 — Group Partition
Core question: which groups must share or avoid a physical signature?

Typical predicates: SAME_SIGNATURE, DIFFERENT_SIGNATURE, material/role intersections.

Strength: converts the problem from individual face placement to set partitioning.

## F10 — Symmetry Breaker
Core question: several layouts are equivalent under reading order, but one visible secondary condition breaks symmetry.

Typical predicates: material, orientation, facing, role.

Strength: ideal mature family because it makes the secondary rule genuinely relevant.

## F11 — Locked Evidence
Core question: a few authored pre-placements/locks constrain the remaining inverse problem.

This does not create a new predicate. It varies starting information and can make a familiar transform produce a new deduction.

Guardrail: locks must reduce clerical branching, not turn cases into forced fill.

## F12 — Mixed Signature Synthesis
Core question: different signature sizes/templates coexist, requiring reasoning about leaf-domain composition before inverse fill.

Typical setup: T4 + T8 or T4 + T6P; maximum 3 signatures total.

Guardrail: mixed templates are reserved for later campaign. No case may require learning two new templates simultaneously.

---

# 6. Authored vs generated responsibilities

## Authored authority
Humans/design sessions author:
- teaching intent;
- allowed rule vocabulary;
- face/motif identities;
- case setup and locks;
- required predicates;
- expected reasoning summary;
- intended difficulty band;
- demo placement;
- chapter sequencing;
- optional badges;
- presentation beats.

The campaign is **not** procedurally generated at runtime.

## Solver/automation responsibilities
Tools may:
- verify legality and solvability;
- enumerate/canonicalize solution classes;
- identify redundant predicates;
- calculate branch/domain statistics;
- detect isomorphic or near-isomorphic cases;
- search bounded parameter variants around an authored seed;
- suggest candidates that satisfy a requested structural fingerprint;
- estimate interaction count from a known solution trace;
- test whether local inverse fill alone solves the case;
- test whether removing a teaching predicate changes the solution set.

## Forbidden generator authority
A generator must never silently decide:
- what a chapter teaches;
- which new mechanic to add;
- whether an unintelligible case is fun because it is solver-hard;
- whether a 20-face permutation is acceptable merely because it is solvable;
- whether two numerically different but structurally identical cases count as distinct content.

Generated candidates are raw material; only certified authored cases enter campaign canon.

---

# 7. Solver-backed content certification pipeline

Every candidate case passes the following pipeline before release canon.

### Stage C1 — Schema / legality
Validate IDs, slot capacities, face uniqueness, template availability, nest-role domains, material legality, required assignments and predicate references.

### Stage C2 — Deterministic transform verification
For every small transform/template used, confirm the case resolves under Phase-4 authority with no case-local rule overrides.

### Stage C3 — Solvability
Require >=1 canonical solution class.

### Stage C4 — Constraint relevance
For each required predicate marked `mechanically_required`, temporarily remove it and re-solve.

Classify:
- `ESSENTIAL`: valid solution set expands or changes materially;
- `REINFORCEMENT`: intentionally redundant because the case is teaching visible language;
- `REDUNDANT_ERROR`: no pedagogical reason; reject or rewrite.

After Chapter II, required secondary predicates should almost always be ESSENTIAL.

### Stage C5 — Rote-collapse test
Solve under READ_ORDER plus fixed setup only. If all meaningful decisions are already fixed, reject unless tagged tutorial reinforcement.

### Stage C6 — Structural fingerprint
Compute normalized fingerprint over:
- signature count and template multiset;
- number of template choices;
- nest-role freedom;
- predicate-family multiset;
- face count bucket;
- orientation-sensitive count bucket;
- material-role count;
- blank/trim state;
- locked-information pattern;
- solution-class count bucket;
- dependency graph among faces/signatures/predicates.

### Stage C7 — Isomorphism / repetition comparison
Compare against all prior campaign cases after renaming:
- face IDs;
- signature labels where symmetric;
- material/color names;
- motif names.

Exact graph-isomorphic duplicates are rejected.

Near-isomorphic candidates are rejected when the only change is one of:
- page numbers renamed;
- blue -> gold material rename;
- outer/inner labels mirrored with otherwise identical deduction;
- same predicate graph at a larger face count;
- same solution trace with decorative motif changes.

### Stage C8 — Human reasoning annotation
Author writes 1–4 sentence intended reasoning summary. If this is impossible without narrating dozens of slot-level moves, the case is probably clerical and fails.

### Stage C9 — Interaction budget
Estimate competent primitive-equivalent transactions. Cases above the ceiling are rejected or repaired with structure/locks/tools.

### Stage C10 — Preview-loop attack
For mature cases, construct at least one plausible wrong branch and verify why it fails globally. If every edit can be judged by immediate monotonic improvement after Preview, lower priority or reject.

### Stage C11 — Neighbor distinctness
Every case must be compared with the previous two and next planned two campaign cases. Avoid consecutive cases with the same dominant reasoning family unless one is an explicit short reinforcement pair.

### Stage C12 — Final manual/playtest gate
A solver proves correctness, not fun. Before specification freeze, campaign cases should have paper/prototype simulation evidence that players can form hypotheses and explain failures.

---

# 8. Anti-isomorphism policy

The campaign should not disguise one puzzle as thirty.

## Exact duplicate definition
Two cases are exact structural duplicates if, after canonical renaming, they have the same:
- transform/template choices;
- nesting freedom;
- slot/face-domain structure;
- predicate dependency graph;
- locked information pattern;
- accepted BoundBookState classes.

Only one may remain.

## Near-duplicate warning
Two cases trigger review when >=80% of the structural fingerprint matches and their intended reasoning summaries describe the same deduction.

At least one of the following must then differ materially:
- dominant family;
- global branch decision;
- template choice consequence;
- predicate interaction;
- evidence/lock pattern;
- solution symmetry structure;
- physical reveal.

Adding four more faces is not a material difference.

## Campaign spacing rule
No dominant family should lead more than two consecutive cases. A family may recur throughout the campaign, but its partner interaction should evolve.

---

# 9. Campaign pacing and approximate play length

This is a planning baseline, not a commercial runtime guarantee.

### Chapter I
4 cases, roughly 20–35 minutes total for a new player.

### Chapter II
5 cases, roughly 35–60 minutes.

### Chapter III
5 cases, roughly 45–75 minutes.

### Chapter IV
5 cases, roughly 60–90 minutes.

### Chapter V
5 cases, roughly 60–90 minutes.

### Chapter VI
6 cases, roughly 90–150 minutes.

Baseline first-completion campaign therefore plausibly lands around **5–8 hours** depending on player speed, with optional badges/revisits extending mastery. This is a design pacing estimate, not a storefront promise and must be validated empirically.

No chapter should introduce more than one genuinely new mechanical primitive in a single case. Mature cases introduce no new primitives.

---

# 10. Frozen demo set

Demo target: **6 cases / approximately 20–30 minutes** for a representative first-time player.

The demo is carved from the opening campaign rather than maintained as a separate divergent ruleset.

## D01 — Impossible Order
One T4 sheet, P1–P4. Guided inverse surprise. Player arranges the apparently wrong flat sheet and sees 1–2–3–4 after fold.

Family: F01.

## D02 — Before You Fold
T4 again, less guidance. Player predicts one final adjacency before Preview.

Family: F01 + learning prompt.

## D03 — Turn the Sheet
T4F introduces binary orientation/sheet flip with one orientation-sensitive motif.

Family: F05.

## D04 — Inside Another
Two T4 signatures with fixed initial roles, then one small role choice. Establish outer/inner domains.

Family: F02.

## D05 — Across the Spread
Two signatures; reading order plus one FACING predicate. First secondary predicate changes an otherwise plausible arrangement.

Family: F03.

## D06 — The Blue Insert
Two signatures. Reading order admits multiple role-equivalent local layouts; pages in one tagged group must share BLUE material, forcing the blue signature into the only compatible role. This is the demo capstone.

Families: F02 + F04 + F10.

### Demo boundary
Demo ends immediately after D06's successful fold/nest reveal and a concise teaser montage showing T8, trim and three signatures without exposing solutions.

### Demo success criteria
By D06, representative players should:
- understand that flat order intentionally looks wrong;
- predict at least two final adjacencies at or above the Phase-3 empirical target;
- explain why one wrong signature role cannot be repaired with local swaps;
- perceive the game as deduction through physical transformation, not generic book crafting.

No demo-exclusive mechanic, currency, progression tree or save format is allowed.

---

# 11. Optional challenge / badge content

Baseline completion is always exact satisfaction of required predicates with unlimited free Preview, Undo and failed Commit.

Optional badges may provide mastery goals after the underlying case has been solved once or may be visible from first play if they do not distort baseline understanding.

Allowed badge families:
1. **Predicted** — correctly answer the authored pre-Preview prediction prompt before first Preview.
2. **Clean Plan** — solve under an authored generous Preview-count ceiling.
3. **Few Hands** — solve under an authored transaction ceiling that has been solver/trace certified and is comfortably above theoretical minimum.
4. **No Restart** — solve without Restart; Undo remains allowed.
5. **Alternate Proof** — use a second certified solution class when the case intentionally has multiple meaningful classes.

Forbidden badge families:
- real-time speedrun requirements as primary mastery;
- no-Undo requirements if they punish accessibility/experimentation;
- hidden conditions;
- random daily streaks;
- grind counters such as fold 10,000 pages;
- currency rewards affecting puzzle power;
- badge conditions that make the baseline solution invalid or require a new mechanic.

Badges never gate campaign progression.

---

# 12. Page-face motif and asset grammar

Content should remain readable without bespoke illustration for every case.

## Reusable face channels
A PageFace may communicate through independent channels:
- large sequence number;
- simple central icon/motif;
- group border/symbol;
- orientation arrow/glyph;
- material/signature edge treatment;
- blank/sacrificial symbol;
- trim mark.

Mechanically relevant properties must never rely on one decorative illustration detail.

## Motif sets
A motif set is presentation dressing reusable across 3–6 cases, e.g.:
- botanical stamps;
- geometric astronomy;
- birds/feathers;
- maps/wayfinding symbols;
- theatrical masks;
- abstract ink shapes.

Motif sets must not introduce semantic puzzle rules. A bird icon is just an identity unless a predicate explicitly tags it.

## Visual redundancy rule
Any mechanically relevant use of color also gets a shape/icon/textual label. Material `BLUE` may be visually blue but must also have a material symbol or patterned edge.

## Text burden ceiling
No case should require reading paragraphs of page content. Mechanically relevant text is short labels/numbers/localized case instructions only.

---

# 13. Localization-safe content rules

1. Never encode a solution in English word length, alphabetical order or text direction unless the case is explicitly excluded from localization; baseline campaign does not use such rules.
2. Face identity uses stable IDs/icons independent of localized labels.
3. Required predicates refer to semantic IDs, never rendered string positions.
4. Numbers may be rendered using locale-appropriate glyphs, but sequence authority remains numeric.
5. Orientation glyphs cannot depend on reading English words right-side-up.
6. Tutorial copy must name plain concepts: outer, inner, fold, facing, blank, trim; avoid unexplained professional imposition jargon.
7. Case titles and decorative captions may localize freely without affecting solution state.
8. UI must tolerate text expansion; no mechanically relevant clue may be cropped.
9. Color/material names are redundant with icons/patterns.
10. Demo and full campaign use the same localization keys and case data authority.

---

# 14. Content reuse rules

Allowed reuse:
- fold templates;
- workbench environment;
- fold/nest/trim animations;
- generic page-face motif assets;
- material visual treatments;
- tutorial overlays when same concept is reinforced;
- predicate explanation components;
- audio feedback motifs.

Required variation:
- dominant reasoning structure;
- relevant constraint dependency;
- starting evidence/locks;
- signature/template role where needed;
- case-specific face/group composition;
- success reveal framing often enough to prevent visual monotony.

A case is not “new” because page art changed.

---

# 15. Expansion boundaries

Future DLC/expansion content may:
- create new cases using T4/T4F/T8/T6P;
- add new motif/art packs with no mechanical effect;
- explore more difficult interactions among existing predicates;
- use different pre-placement/lock patterns;
- add one carefully justified fifth transform family only after empirical evidence that existing content is exhausted and the new transform adds a distinct reasoning shape.

Any fifth transform must receive its own mechanical-spec amendment, solver validation and onboarding plan. It is not automatically part of base-game authority.

Expansion content may not silently add:
- continuous paper physics;
- glue/thread/adhesive simulation;
- paper thickness/grain/moisture economics;
- printing press calibration;
- customer/shop management;
- narrative-choice systems that alter puzzle rules;
- crafting inventory;
- random puzzle modifiers;
- deckbuilding/roguelite systems;
- live-service progression;
- 90-degree or arbitrary rotation without reopening orientation architecture;
- hidden fold behavior;
- giant 32/64-page clerical puzzles as “hard mode.”

---

# 16. Proposed 30-case campaign map

Case names are working titles. Mechanical role is authority; prose/title can change in UX phase.

| # | ID | Working title | Dominant families | Core content purpose |
|---:|---|---|---|---|
| 1 | C01 | Wrong on the Table | F01 | Guided T4 inverse surprise, P1–P4. |
| 2 | C02 | Before the Fold | F01 | T4 prediction prompt; less scaffolding. |
| 3 | C03 | One Missing Pair | F01+F11 | Two locked faces; infer remaining pair rather than refill whole sheet. |
| 4 | C04 | Turn It Over | F05 | T4F sheet flip + one orientation-sensitive icon. |
| 5 | C05 | Outside / Inside | F02 | Two T4 signatures, fixed roles first, visible global domains. |
| 6 | C06 | Which One Wraps? | F02 | Player chooses outer/inner; AT_POSITION makes role nontrivial. |
| 7 | C07 | Across the Middle | F03 | First essential FACING predicate. |
| 8 | C08 | Keep Them Together | F02+F09 | SAME_SIGNATURE group forces role reasoning. |
| 9 | C09 | The Blue Insert | F02+F04+F10 | Material group breaks order-correct symmetry; demo capstone. |
| 10 | C10 | Separate Leaves | F03+F09 | DIFFERENT_SIGNATURE + facing interaction. |
| 11 | C11 | Two Sides, One Leaf | F03 | SAME_LEAF introduced with familiar T4 roles. |
| 12 | C12 | Upright Proof | F05+F02 | Orientation requirement selects sheet flip/role. |
| 13 | C13 | Gold Across | F03+F04 | Facing spread and material ownership intersect. |
| 14 | C14 | The False Outer | F02+F09+F10 | Two locally correct fills; group constraint disproves obvious outer choice. |
| 15 | C15 | Fold Twice | F01 | Guided T8 mapping; new transform but low secondary load. |
| 16 | C16 | Half Turn | F05 | T8's fixed orientation pattern becomes essential. |
| 17 | C17 | Four or Eight | F06 | Compare T4/T8 affordances under a simple global condition. |
| 18 | C18 | Choose the Fold | F06+F03 | Two legal templates; only one can create requested facing relation/orientation combination. |
| 19 | C19 | Small Inside Large | F12+F04+F09 | Mixed T4/T8 signatures with material/group role deduction. |
| 20 | C20 | A Real Blank | F07 | REQUIRED_BLANK vs EMPTY, explicitly taught. |
| 21 | C21 | Cut This Mark | F08 | T6P trim disappearance introduced. |
| 22 | C22 | Keep This One | F08+F05 | One mark must survive while orientation still resolves correctly. |
| 23 | C23 | Blank Insert | F07+F04+F03 | Partial signature, material ownership and facing. |
| 24 | C24 | The Fold That Cuts | F06+F08+F10 | Template choice is broken by trim fate. |
| 25 | C25 | Three Layers | F02+F04 | Three T4 signatures; material pages force middle role. |
| 26 | C26 | Inner Turn | F02+F05+F09 | Three roles; inverted-capable face/group forces inner role. |
| 27 | C27 | Unequal Company | F12+F09 | Mixed-size three-signature synthesis with same/different groups. |
| 28 | C28 | Only One Binding | F06+F03+F04+F10 | Template branch + facing + material symmetry break. |
| 29 | C29 | What the Knife Leaves | F07+F08+F02 | Blank/trim requirement interacts with three-role nesting. |
| 30 | C30 | Final Proof | F02+F03+F04+F05 (plus familiar template) | Capstone: 3 signatures, 3–4 secondary predicate families, no new rule; global role deduction before local inverse fill. |

### Map guardrails
- C15 is allowed to be relatively simple because T8 itself is newly introduced; C16 immediately makes its orientation structure meaningful.
- C20–C21 are paired teaching cases but must be short; C22–C24 provide the real trim/blank depth.
- C25–C30 are not “larger page count” difficulty. Their intended page counts should typically be 12–20, with role/constraint structure carrying the challenge.
- C30 should not exceed four secondary predicate families beyond READ_ORDER.

---

# 17. Case-count fallback plan

If solver/playtest review rejects planned cases, cut in this order rather than adding filler:
1. remove a weak reinforcement case whose lesson is already mastered;
2. merge its tutorial overlay into the next strong case;
3. preserve chapter capstones and first-introduction clarity;
4. maintain at least one strong case for every content family that remains in the campaign;
5. maintain at least four mature synthesis cases in Chapter VI.

The product thesis survives with 24–29 excellent cases. It does not survive with 30 cases where several are clerical duplicates.

---

# 18. Content acceptance tests

Future implementation/content tooling should be able to encode these tests.

## Schema / authority
**C-A01** Every campaign CaseDefinition references only frozen Phase-4 templates and predicates.

**C-A02** Every face ID is unique case-locally and every required predicate reference resolves.

**C-A03** No case introduces 90-degree orientation, continuous paper state, real-world press variables or hidden transform behavior.

**C-A04** Every mechanically relevant color property has non-color redundant representation.

## Solvability / relevance
**C-A05** Every campaign case has >=1 canonical solution class.

**C-A06** Every authored initial state is legal.

**C-A07** Every non-tutorial required secondary predicate is ESSENTIAL or has an explicit documented reinforcement exemption.

**C-A08** C09 material predicate changes solution classes; removing it restores at least one additional order-correct signature-role class.

**C-A09** C18's two-template setup contains at least one template branch that cannot satisfy the requested secondary constraints.

**C-A10** C24's trim predicate changes the viable template branch.

**C-A11** C25's material group forces one of three nest roles rather than merely confirming a role fixed by READ_ORDER.

**C-A12** C30 remains solvable with no case-local rules and requires at least one global deduction before local inverse fill.

## Rote / repetition
**C-A13** No STANDARD/MATURE/CAPSTONE case after C09 passes the Phase-4 rote-case definition.

**C-A14** Exact canonical structural duplicate detection reports zero duplicate campaign pairs.

**C-A15** Any >=80% fingerprint-similar pair contains a documented materially different dominant deduction or one is removed.

**C-A16** Renaming page IDs/material colors alone cannot cause a duplicate case to pass distinctness certification.

**C-A17** No dominant family leads more than two consecutive campaign cases.

## Scope / manipulation
**C-A18** Ordinary case face count <=20 unless explicit exception is documented before freeze.

**C-A19** Signature count <=3.

**C-A20** Secondary predicate families beyond READ_ORDER <=4 in ordinary mature cases.

**C-A21** Legal template choices per signature <=2.

**C-A22** Estimated competent solution <=35 primitive transactions; mature target <=20 primitive-equivalent transactions after structured tools where practical.

## Teaching / demo
**C-A23** D01–D06 are identical rules/data to their campaign counterparts, not forked demo mechanics.

**C-A24** D02 includes a non-blocking adjacency prediction prompt.

**C-A25** D06 requires a global material/signature-role deduction that local swaps cannot repair.

**C-A26** Demo contains no T8/trim/three-signature playable case; those may appear only in teaser presentation after D06.

**C-A27** No demo-only currency, unlock, save format or rule exists.

## Localization / accessibility
**C-A28** No baseline solution depends on English word spelling, length or alphabetic order.

**C-A29** Orientation can be solved/read using glyphs independent of text orientation.

**C-A30** Material constraints remain readable in simulated monochrome/color-vision-deficiency conditions through icon/pattern redundancy.

## Optional badges
**C-A31** Removing all badge definitions leaves baseline campaign progression and valid solution set unchanged.

**C-A32** No badge requires random streaks, currency, hidden conditions or accessibility-hostile no-Undo play.

## Campaign health
**C-A33** At least 24 cases survive all required quality/certification gates before design can freeze.

**C-A34** At least four Chapter-VI cases survive as genuine mature synthesis rather than tutorial/reinforcement.

**C-A35** Every chapter has at least one strong visual fold/nest/trim reveal suitable for pacing.

**C-A36** Every mature case has a 1–4 sentence intended reasoning summary that does not devolve into slot-by-slot move narration.

**C-A37** For every mature case, at least one plausible wrong branch has a specific global reason for failure.

**C-A38** No case exceeds two material categories as mechanically relevant unless Phase-4 authority is explicitly reopened and justified.

**C-A39** REQUIRED_BLANK and EMPTY remain mechanically distinct in all T6P content.

**C-A40** All case success states evaluate solely against deterministic `BoundBookState`; decorative art/motif selection never affects validity.

---

# 19. Empirical gates carried forward

Content architecture is complete, but these are deliberately empirical and must survive prototype/whole-game simulation later:

1. **Prediction transfer:** after the first four tutorial cases, >=70% of representative testers should predict at least two final adjacencies before Preview at the defined gate.
2. **Hypothesis behavior:** representative mature play should show a majority of meaningful edits associated with a stated or inferable hypothesis rather than blind Preview/swap enumeration.
3. **Interaction burden:** at 12–20 faces, manipulation time must not dominate reasoning time.
4. **T8 comprehension:** T8 must feel like a readable new transform, not an arbitrary mapping table players memorize externally.
5. **Content distinctness:** paper/prototype tests of the planned 30 must not reveal long stretches that players describe as “same puzzle, more pages.”
6. **Demo identity:** testers should describe the demo primarily as folding/permutation deduction, not as a generic bookbinding or cozy-craft simulator.

Failure of these gates requires case/UX repair; it does not justify adding unrelated mechanics.

---

# 20. Phase-5 closure

Content Architecture is complete enough for UX/presentation design without inventing campaign structure.

Frozen Phase-5 authority:
- 24 hard-minimum / 30 target / 34 soft-ceiling quality-gated case count;
- six-chapter campaign arc mapped to Phase-4 teaching order;
- exact conceptual CaseDefinition schema;
- 12 reusable content families without adding new mechanics;
- authored vs solver/generated responsibility split;
- 12-stage content certification pipeline;
- exact/near-isomorphism rejection policy;
- six-case demo set D01–D06 drawn directly from campaign authority;
- optional non-gating badge boundaries;
- reusable motif/page-face grammar;
- localization-safe content rules;
- expansion boundaries and prohibited drift;
- proposed 30-case campaign map C01–C30;
- 40 content acceptance tests;
- empirical gates carried forward explicitly.

No production implementation has started.

## NEXT ACTION — PHASE 6 UX / PRESENTATION ARCHITECTURE

Build the complete interaction/presentation authority around the frozen product, mechanics and content:
1. define screen/state flow from first boot -> case select -> workbench -> Fold Preview -> result -> progression;
2. define mouse/keyboard and controller interaction for PLACE/SWAP/REMOVE, structured operations, template/flip/nest selection, Undo/Redo and Preview/Commit;
3. choose deterministic behavior for Phase-4 M30 template-capacity changes;
4. define workbench layout, tray, signatures, flat-side switching, nesting controls, final-book preview and predicate panel;
5. define onboarding/tutorial overlay rules and prediction-prompt UX without blocking experimentation;
6. define visual language for face identity, orientation, material, signature ownership, nest role, facing/same-leaf and trim;
7. define animation authority vs skippability/fast-repeat behavior so presentation never slows expert iteration;
8. define audio/feedback language, success/failure explanations and exact non-solver-leaking feedback;
9. define pause/settings, save/load/recovery user flow and case-state recovery expectations for later technical phase;
10. define accessibility baseline: remapping, controller parity, reduced motion, animation speed/skip, text scale, contrast/color redundancy, screen-safe symbols, input hold/toggle choices where relevant;
11. define Steam Deck/readability assumptions and localization layout constraints; use fresh research if current platform expectations materially matter;
12. define first-session UX and D01–D06 demo flow;
13. create UX acceptance tests and leave exact Phase-7 commercial next action;
14. do not start production implementation.
