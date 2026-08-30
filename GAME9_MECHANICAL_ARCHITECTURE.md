# GAME #009 — PHASE 4 MECHANICAL ARCHITECTURE

Status: **PHASE 4 COMPLETE / PHASE 5 READY**
Date: 2026-08-31
Selected game: **Binder's Imposition**
Production implementation: **FORBIDDEN in factory**

Authority: `START_HERE.md` -> `STATUS.md` -> `GAME_INDEX.md` -> Game #009 tournament history -> `GAME9_PRODUCT_THESIS.md` -> this file.

This file turns the Phase-3 product thesis into deterministic gameplay authority. Real print-shop practice may inspire presentation, but it is not gameplay authority unless explicitly represented below.

---

## 1. Mechanical design goal

The player solves a finite inverse-transform puzzle:

> choose which page face occupies each editable flat-sheet slot, choose the bounded physical roles of the available signatures, then predict the deterministic fold/nest/trim transform so the final bound object satisfies every case constraint.

Difficulty must come from reasoning over a small visible transform system. It must **not** come from memorizing industry jargon, counting large page ranges, dragging twenty individual cards repeatedly, hidden fold rules, animation timing, dexterity, random outcomes, or undocumented exceptions.

---

# 2. Canonical domain model

A case is fully described by the following data.

## 2.1 PageFace

A `PageFace` is one logical face to be placed into the book.

Fields:
- `face_id`: stable case-local identifier; examples `P01`, `P02`, `MAP_A`, `BLANK_1`.
- `read_index`: optional integer used when the case has a sequential reading order. `null` for non-numbered inserts or decorative faces.
- `orientation_requirement`: `ANY | UPRIGHT | INVERTED` relative to final-book upright.
- `material_role`: one finite symbolic role such as `STANDARD`, `BLUE`, `GOLD`, `TRANSLUCENT`; names are fictional labels, not simulation parameters.
- `blank_kind`: `CONTENT | REQUIRED_BLANK | SACRIFICIAL`.
- `trim_mark`: optional symbolic mark that may be required to `SURVIVE` or `DISAPPEAR` after trim.
- `group_tags`: finite case-local tags used by same/different-signature and facing constraints.

There is no hidden content inside a page face. All mechanically relevant properties are visible before editing.

## 2.2 FlatSlot

A `FlatSlot` is one editable position on one physical signature before folding.

Fields:
- `slot_id` stable within its signature.
- `side`: `A | B`.
- `cell`: symbolic coordinate inside the selected template, usually `0..3` or `0..5`; coordinates are presentation labels, not world-space physics.
- `base_orientation`: `0 | 180` degrees. Phase 4 uses only binary upright/inverted authority.
- `trim_zone`: `KEEP | CUT` for the face area that matters to a trim-survival rule.
- `allowed_material_roles`: optional finite set. Normally unrestricted unless the case explicitly uses stock/material constraints.

One slot holds exactly one `PageFace` or the explicit token `EMPTY` when the template permits an unused face.

## 2.3 Signature

A `Signature` is one physical sheet/signature object.

Fields:
- `signature_id`.
- `material_role`.
- `chosen_template_id`.
- `sheet_flip`: `NORMAL | FLIPPED` when the chosen template exposes a legal flip choice.
- `nest_role`: an integer rank `0..N-1`, where `0 = OUTERMOST` and larger values move inward.
- `assignment[slot_id] = face_id | EMPTY`.

Signatures are physically distinguishable in presentation even when their rules are symmetric. For solution counting, truly interchangeable signatures are canonicalized as described in the solver section.

## 2.4 FoldTemplate

A `FoldTemplate` is a finite deterministic transform definition, not simulated paper physics.

It contains:
- fixed flat-slot schema;
- legal `sheet_flip` modes;
- a bijection from each occupied flat slot to one **local final face position** within that folded signature;
- an orientation transform bit for that local final face;
- a leaf-pair structure identifying which local final faces are opposite sides of one leaf;
- a local facing map after the fold;
- optional trim behavior for designated sacrificial zones.

A template never changes behavior based on animation, frame order, or floating-point geometry.

## 2.5 BoundBookState

The deterministic resolved output is an ordered sequence of final faces.

Each final-face record contains:
- `book_position` from first visible face to last;
- `face_id | EMPTY`;
- `final_orientation` = XOR of page requirement-independent slot/template/flip orientation bits;
- `signature_id`;
- `nest_role`;
- `leaf_id`;
- `facing_partner_position | NONE`;
- `trim_result`: `SURVIVES | REMOVED | NOT_APPLICABLE`;
- `material_role` inherited from the physical signature unless a case explicitly defines an insert token as material-bearing.

This resolved state is the only authority checked by final constraints.

---

# 3. Deterministic resolution order

The canonical order is frozen:

1. **Validate editable setup.** Confirm every placed face is legal for its slot/signature and that required faces are assigned exactly once.
2. **Resolve each signature locally.** Apply its selected `FoldTemplate` to flat slots.
3. **Apply duplex orientation.** Combine slot base orientation, template orientation output and legal `sheet_flip` bit by XOR. No other orientation rule exists.
4. **Resolve nesting.** Sort signatures by `nest_role`; map each signature's local folded faces into its global bound-book position domain.
5. **Resolve leaf/facing relationships.** Build final leaf pairs and facing-spread adjacency from the global nested order.
6. **Resolve trim.** Any designated sacrificial region is deterministically `REMOVED`; all other mechanically tracked regions survive.
7. **Evaluate constraints.** Every case objective is evaluated against the resulting `BoundBookState`.
8. **Generate explanation.** Failed constraints return exact machine-readable failure reasons which presentation converts to player language.

`Fold Preview` executes steps 1–6 without committing progression. `Bind / Trim` executes the same transform and then evaluates step 7 as the official attempt.

Preview and Commit are therefore mathematically identical transforms; Commit does not introduce surprise rules.

---

# 4. Frozen template grammar

The game uses a small fictionalized catalog. Names shown to the player should be plain-language visual names; internal IDs can remain technical.

## 4.1 T4 — Single Fold / 4 faces

Slots: `A0,A1,B0,B1`.

For `NORMAL`, local final read order is:
`[A1, B0, B1, A0]`.

Canonical final orientation bits:
- `A1: 0`
- `B0: 0`
- `B1: 0`
- `A0: 0`

This is the tutorial primitive. Presentation may animate one physical fold, but the permutation above is authority.

## 4.2 T4F — Single Fold with legal sheet flip

Same local position map as T4 before flip. `FLIPPED` swaps A/B source-side interpretation and toggles the orientation bit of every resulting face.

Purpose: teach that duplex orientation is a visible transform choice, not hidden printer jargon.

## 4.3 T8 — Double Fold / 8 faces

Slots: `A0..A3,B0..B3`.

Local final read order:
`[A3, B0, A2, B1, B2, A1, B3, A0]`.

Canonical orientation bits by source slot:
- upright: `A3, B0, B2, A1`
- inverted: `A2, B1, B3, A0`

The alternating orientation pattern is intentionally visible in the template preview. The player never needs to infer an undisclosed rotation.

## 4.4 T6P — Partial Fold / 6 usable faces + 2 sacrificial faces

Uses T8 geometry, but exactly two named local positions are `SACRIFICIAL` and removed at trim. Those positions may host `EMPTY`, `REQUIRED_BLANK`, or an explicit disposable trim mark according to the case.

Purpose: introduce blank/trim reasoning without adding new fold mathematics.

## 4.5 Catalog ceiling

Phase-4 catalog ceiling for the base campaign is **four transform families**: `T4`, `T4F`, `T8`, `T6P`. Phase 5 may define content variants that restrict which templates are available, but it may not invent additional fold transforms casually. Any fifth transform requires an explicit depth justification and must replace, not merely stack on top of, an existing weak family if cognitive load becomes excessive.

---

# 5. Nesting semantics

Nesting is discrete and fully visible.

For `N` signatures, every signature receives one unique `nest_role` from `0..N-1`.

For a folded signature with `m` local final positions:
- the outermost signature contributes a prefix and matching suffix to the global book;
- the next signature contributes the next inner prefix/suffix;
- and so on until the innermost signature occupies the central block.

For equal 4-face signatures this produces the already validated domains:
- two signatures: outer `{1,2,7,8}`, inner `{3,4,5,6}`;
- three signatures: outer `{1,2,11,12}`, middle `{3,4,9,10}`, inner `{5,6,7,8}`.

Mixed-size templates use the same rule over leaves, not raw face counts: each signature contributes its outer leaf pair(s) around all more-inner signatures while preserving its local within-signature order.

The UI must show these destination domains during Fold Preview and may show them as ghost bands before preview after the relevant tutorial unlock.

---

# 6. Player verbs

All editing before Commit is reversible.

## 6.1 Basic verbs

1. **PLACE** — move an unassigned face to an empty legal flat slot.
2. **SWAP** — swap two occupied legal slots.
3. **REMOVE** — return a placed face to the unassigned tray.
4. **ROTATE / FLIP FACE** — only available when the case permits player-controlled face orientation; toggles one binary orientation bit.
5. **CHOOSE TEMPLATE** — select one allowed template for a signature.
6. **FLIP SHEET** — toggle a template-supported `NORMAL/FLIPPED` mode.
7. **SET NEST ROLE** — reorder physical signatures outer -> inner.
8. **FOLD PREVIEW** — resolve the deterministic book without progression commit.
9. **COMMIT BIND/TRIM** — submit current setup for official constraint evaluation.
10. **UNDO / REDO** — history operations over reversible edits.
11. **RESTART CASE** — restore authored initial state.

## 6.2 Structured anti-bookkeeping verbs

These unlock only after the player understands the primitive they accelerate.

### SWAP PAIR
Swap two selected leaf-pair source groups while preserving their internal face orientation. This reduces four individual moves to one transaction but does not identify which pair should move.

### MOVE GROUP
Move a case-defined tagged face group together when all target slots are legal. Group membership is visible and authored; the tool never computes a helpful grouping from the solution.

### INVERSE-FILL GHOSTS
After the player has solved several cases of one fold template, the UI may show faint final-position labels on its flat slots (`final 1st`, `final 4th`, etc.). This externalizes learned clerical mapping but does not assign pages, choose nesting, or satisfy secondary constraints.

### CLEAR SIGNATURE
Return every editable face on one signature to the tray as one Undo-able transaction.

These operations exist to protect reasoning time. They are not difficulty settings and do not alter solution validity.

---

# 7. Undo / Redo / Preview / Commit authority

## 7.1 History

Every reversible edit creates one atomic history transaction. Structured operations create one transaction, not one entry per moved face.

Undo/Redo includes:
- face placement/swaps/removal;
- face orientation toggles;
- template choice;
- sheet flip;
- nesting order;
- structured operations.

Fold Preview does **not** create history because it does not change canonical editable state.

## 7.2 Commit

A failed Commit does not destroy the layout. It records an attempt result and returns to the same editable setup.

A successful Commit marks the case solved only after the success result is generated. Later persistence architecture must make this idempotent.

There is no consumable cost for preview or failed commit. Trial-and-error is discouraged by case structure and explanation quality, not by punishment currency.

---

# 8. Constraint language

All case objectives are built from the following finite predicate set.

1. `READ_ORDER(face_ids...)` — listed sequential faces occupy listed global book positions/order.
2. `AT_POSITION(face, position)`.
3. `FACING(face_a, face_b)` — occupy one visible facing spread in either left/right order unless the authored constraint specifies order.
4. `SAME_SIGNATURE(group)`.
5. `DIFFERENT_SIGNATURE(face_a, face_b)` or groups.
6. `SIGNATURE_ROLE(face_or_group, OUTER|MIDDLE|INNER|role_index)`.
7. `MATERIAL(face_or_group, role)` — resolved physical signature material matches.
8. `ORIENTATION(face, UPRIGHT|INVERTED)`.
9. `SAME_LEAF(face_a, face_b)` — opposite sides of one physical leaf.
10. `TRIM_RESULT(mark_or_face, SURVIVE|DISAPPEAR)`.
11. `BLANK_AT(position)`.
12. `TEMPLATE(signature, allowed_set)` — normally encoded by legal setup rather than scoring, but permitted when a case explicitly asks the player to choose among templates.

Compound objectives use AND only in baseline campaign scoring. There is no hidden weighted score and no fuzzy partial success.

Optional challenge badges in later phases may introduce explicit secondary conditions such as move/preview limits, but baseline case completion remains exact satisfaction of required predicates.

---

# 9. Orientation semantics

Orientation is deliberately binary.

Represent upright as bit `0`, inverted as bit `1`.

For each resolved face:
`final_orientation = face_edit_bit XOR flat_slot.base_orientation XOR template.orientation_bit XOR sheet_flip_bit`.

A face with `orientation_requirement=ANY` ignores the result for scoring. `UPRIGHT` requires 0. `INVERTED` requires 1.

No 90-degree orientation, mirrored text, grain direction, front/back ink registration, or press feeding direction exists in base authority.

The presentation must always show an orientation glyph on orientation-sensitive faces. A player should never need to judge tiny artwork visually to know the mechanical orientation.

---

# 10. Blank, insert and material rules

## 10.1 Required blank

A `REQUIRED_BLANK` is an explicit face token that must occupy a valid final position. It behaves like any other page face for placement and nesting but displays as blank.

## 10.2 EMPTY

`EMPTY` means no page face is present in a template-permitted sacrificial slot. It is not interchangeable with a required blank unless the predicate explicitly accepts `EMPTY`.

## 10.3 Sacrificial trim

A sacrificial page/mark located in a `CUT` zone receives `trim_result=REMOVED`. This can satisfy a `DISAPPEAR` objective. A mark in a `KEEP` zone survives. There is no partial clipping percentage.

## 10.4 Material role

Material is a categorical property of the physical signature. Putting a face on a signature means that face resolves on that signature's material unless the face is an explicit special insert with its own authored override.

Material categories do not have thickness, cost, durability, opacity simulation or chemistry in Phase 4.

---

# 11. Legality vs failure

The game distinguishes **illegal edit state** from a **legal but incorrect submitted solution**.

## 11.1 Illegal state

Commit is disabled and the exact reason is shown when any of these holds:
- a required face is unassigned or assigned more than once;
- a slot contains a face/material combination forbidden by case data;
- two signatures share the same nest role;
- an unavailable template or sheet-flip mode is selected;
- a required slot is empty when the selected template forbids it;
- a structured move would violate slot capacity or a locked authored assignment.

Illegal state is not counted as a failed attempt.

## 11.2 Legal but incorrect Commit

Commit resolves successfully but one or more predicates fail. The result panel must report every failed required predicate, grouped by type.

Examples:
- `Reading order fails at positions 3–4: P04 and P03 are reversed.`
- `P06 and P07 do not face each other.`
- `Gold pages P04/P09 are split across signatures B and C.`
- `MAP_A resolves inverted.`
- `CUT_MARK survives trim but must disappear.`

The explanation may point to resolved final positions but may not reveal a missing source-slot assignment that would solve the puzzle.

## 11.3 Success

Success occurs iff setup is legal and every required predicate evaluates true.

There is no partial-progress meter that leaks solver information beyond per-predicate truth already observable in the resolved preview/book.

---

# 12. Fold Preview contract

Preview is a learning and verification tool, not a hidden-information oracle.

It must show:
- physical fold/nest animation or equivalent deterministic visualization;
- final page sequence;
- page orientation glyphs;
- signature/material identity;
- facing spreads;
- trim disappearance when relevant.

It may optionally show current predicate status after those predicate families have been taught.

It must not:
- recommend a page placement;
- rank candidate swaps;
- show future consequences of edits not yet made;
- say which template/nesting choice is closest to the solution;
- automatically enumerate alternatives.

Preview can be repeated without cost. Mature cases therefore must remain interesting even when every proposed state can be inspected.

---

# 13. Difficulty architecture

Difficulty is controlled by a finite set of knobs. Raw face count is the last knob, not the first.

Knobs:
1. number of signatures: 1 -> 2 -> 3, baseline ceiling 3;
2. template vocabulary available in a case: 1 -> choice of 2;
3. fold family complexity: T4 -> T4F -> T8/T6P;
4. nesting choice count;
5. number of secondary predicate families simultaneously active;
6. orientation-sensitive face count;
7. same/different-signature group coupling;
8. material-role restrictions;
9. required facing/same-leaf relations;
10. blanks/trim survival;
11. symmetry: multiple locally equivalent assignments before a global constraint breaks the tie;
12. amount of pre-placed/locked information;
13. face count, normally 4–20.

A mature case should usually increase **constraint interaction**, not all knobs at once.

---

# 14. Rule-introduction order

Frozen campaign teaching order:

1. **T4 inverse surprise** — four numbered faces, one sheet, no orientation constraints.
2. **Preview prediction** — ask player to predict one adjacency before preview.
3. **Duplex flip/orientation** — introduce binary orientation glyph; still one signature.
4. **Second signature / nesting** — outer vs inner changes global domains.
5. **Facing spread** — first secondary final-book predicate.
6. **Same-signature group** — page order alone no longer chooses a unique physical role.
7. **Material role** — one categorical stock constraint chooses among order-correct layouts.
8. **T8 or mixed fold family** — local fold mapping changes while mental model remains inverse transform.
9. **Alternative template choice** — two legal transforms, only one satisfies global constraints.
10. **Required blank / partial signature / trim**.
11. **Three-signature role deduction**.
12. **Mature intersections** — 2–4 already-taught secondary predicate families; no new rule introduced inside the hardest cases.

The demo target ends around steps 6–7.

---

# 15. Solver / validator contract

The design requires an exact non-production validator eventually, but Phase 4 defines its behavior rather than implementation technology.

## 15.1 Inputs

Validator receives:
- case page-face set;
- available signatures and their categorical materials;
- allowed templates per signature;
- legal sheet flips;
- editable/locked slots;
- legal nest roles;
- required predicates;
- optional authored symmetry declarations;
- optional intended solution-depth metadata.

## 15.2 Search variables

Primary variables:
- template choice per signature;
- sheet flip per signature;
- nest-role permutation;
- page-face assignment to flat slots;
- editable face orientation bit where allowed.

## 15.3 Propagation strategy expected by spec

A validator should exploit deterministic transforms rather than naïvely enumerate `n!` flat assignments:
1. enumerate small template/flip/nest choices;
2. derive global final-position domains for every signature/slot;
3. apply hard page-position/read-order predicates;
4. propagate material/signature-role/group/facing/orientation domains;
5. only then assign unresolved page faces to compatible flat slots;
6. verify trim and remaining predicates.

This makes intended 4–20-face cases tractable even though raw permutations are huge.

## 15.4 Solution equivalence

Two solutions are equivalent when they produce the same mechanically relevant `BoundBookState` after canonicalizing signatures declared interchangeable by the case.

Differences that do **not** matter for solution counting:
- swapping labels of two signatures with identical material, allowed templates, locked state and nest-role capability when the final resolved book is otherwise identical;
- moving `EMPTY` among mechanically indistinguishable sacrificial slots when no predicate observes them;
- presentation-only animation choices.

Differences that **do** define separate solution classes:
- different template choice;
- different nest-role assignment among mechanically distinguishable signatures;
- different final orientation of ANY-orientation art only if another predicate observes the affected leaf/signature arrangement; otherwise it may be canonicalized;
- different final signature membership of a face when signature membership/material is mechanically observable.

## 15.5 Case certification

Every campaign case must pass:
- `SOLVABLE`: >=1 solution class;
- `LEGALITY_CLEAN`: every authored initial state is legal;
- `RULE_COVERAGE`: intended introduced predicate actually constrains at least one solution dimension;
- `NO_REDUNDANT_REQUIRED_CONSTRAINT`: removing each marked teaching constraint should increase solution classes or otherwise change the solution set, unless explicitly marked explanatory/reinforcement-only;
- `NONTRIVIAL`: intended case is not solved by the initial state and not reducible to one forced clerical assignment after reading order alone, except explicit tutorials;
- `NO_SINGLE_FORMULA_COLLAPSE`: mature cases cannot all be solved by applying local template inverse then filling signatures sequentially without reasoning about at least one global constraint;
- `INTERACTION_BUDGET`: predicted manipulation transactions stay within authored ceiling.

## 15.6 Rote-case rejection

For cases after the early tutorial arc, reject a case as rote if all of the following are true:
1. template and nesting are fixed;
2. `READ_ORDER` uniquely determines every face position;
3. no secondary predicate changes any decision;
4. the remaining task is only applying a learned inverse mapping.

Such a case may exist only as a short reinforcement tutorial, never as mature campaign content.

---

# 16. Anti-bookkeeping limits

Hard design ceilings for baseline campaign:
- maximum logical page faces in ordinary cases: **20**;
- maximum signatures: **3**;
- maximum simultaneously editable flat slots: **20**;
- maximum active required predicate families in one ordinary mature case: **4** beyond reading order;
- maximum legal template choices per signature in one case: **2**;
- no 90-degree rotation state;
- no more than two material categories introduced as relevant to one case unless a later empirical test proves clarity;
- no case should require more than **~35 primitive drag/swap transactions** in an intended competent solution; structured operations should lower mature cases below this when possible.

Phase 5 must treat these as content-authoring guardrails. A case that is hard only because it violates them is not acceptable content.

---

# 17. Mechanical acceptance tests

These are design-level tests a future implementation must be able to encode.

## A. Deterministic transforms

**M01 T4 mapping** — assign `A1=P1,B0=P2,B1=P3,A0=P4`; preview resolves `[P1,P2,P3,P4]` exactly.

**M02 T4 inverse failure** — swap A1/A0 from M01; preview resolves `P4,...,P1`; Commit reports reading-order positions rather than generic failure.

**M03 identical preview/commit** — same legal setup must produce byte-equivalent mechanically relevant BoundBookState in Preview and Commit.

**M04 T8 orientation** — an orientation-sensitive face placed in an inverted-output source slot resolves inverted unless player-edit/sheet-flip XOR corrects it.

**M05 no physics authority** — changing fold animation speed/frame rate cannot change resolved output.

## B. Nesting

**M06 two T4 domains** — outer signature owns final positions `{1,2,7,8}` and inner `{3,4,5,6}`.

**M07 three T4 domains** — outer/middle/inner map to `{1,2,11,12}`, `{3,4,9,10}`, `{5,6,7,8}`.

**M08 wrong role globally impossible** — in the tournament red/gold-style case, putting the constrained material signature in the wrong nest role cannot be repaired by local swaps.

**M09 nest reorder undo** — one Undo after nest reorder restores exact prior order and assignments.

## C. Constraints

**M10 facing true** — center pair in an 8-face two-signature book evaluates FACING true.

**M11 facing false but order true** — construct order-correct pages whose authored requested pair is not a facing spread; reading predicate passes while facing predicate fails.

**M12 same signature** — two faces on same physical signature pass regardless of flat-side A/B.

**M13 different signature** — same final adjacency cannot override different-signature failure.

**M14 material inheritance** — face resolves with the categorical material of its signature.

**M15 orientation ANY** — ANY ignores final orientation bit.

**M16 orientation required** — UPRIGHT fails when resolved bit is 1 and explanation names the face.

**M17 trim disappear** — mark in CUT zone reports REMOVED and satisfies DISAPPEAR.

**M18 trim survive fail** — same mark in KEEP zone fails DISAPPEAR with exact explanation.

**M19 required blank vs EMPTY** — EMPTY cannot satisfy a required-blank predicate unless explicitly authored as acceptable.

## D. Editing / history

**M20 swap atomicity** — SWAP creates exactly one Undo transaction.

**M21 pair-swap atomicity** — SWAP PAIR moves all constituent faces but creates exactly one history entry.

**M22 preview non-mutating** — repeated Preview leaves edit-state and history cursor unchanged.

**M23 failed commit non-destructive** — failure leaves layout intact and editable.

**M24 restart** — restores authored starting template/flip/nest/assignment and clears redo history.

**M25 new edit after undo** — clears redo tail.

## E. Legality

**M26 missing face** — Commit disabled when required face remains in tray.

**M27 duplicate face impossible** — one face ID cannot occupy two slots through any edit path or load.

**M28 duplicate nest role impossible** — editor rejects or atomically swaps nest roles; never permits ambiguous resolved state.

**M29 illegal material slot** — placement is blocked before commit with visible reason.

**M30 template capacity change** — when changing template would strand assigned faces, game must either return displaced faces to tray in one explicit atomic transaction or block the change; it may not silently delete them. UX phase may choose one behavior, but implementation must be deterministic.

## F. Solver/content quality

**M31 tutorial uniqueness not required** — early tutorial may have multiple equivalent layouts if every accepted layout teaches same intended transform.

**M32 mature secondary relevance** — removing mature case's material-role predicate must enlarge solution set or otherwise change valid solution classes.

**M33 symmetry canonicalization** — swapping two declared-identical signatures does not double solution count.

**M34 nontrivial mature case** — validator flags a case where read order alone fixes all decisions and all secondary predicates are redundant.

**M35 bounded scale** — campaign content above 20 faces fails authoring validation unless explicitly exempted with documented reason.

## G. Concrete tutorial/mid/mature cases

**M36 Tutorial B-T1** — one T4 sheet, target P1..P4; exact accepted assignment `A1=P1,B0=P2,B1=P3,A0=P4` modulo no symmetry.

**M37 Mid B-M1** — two T4 signatures; outer `{1,2,7,8}`, inner `{3,4,5,6}`; constrained material pages `{3,6}` force the material signature inner; page8 outer; pages4/5 facing. Validator must find valid class and reject material-signature outer.

**M38 Mature B3-H** — three T4 signatures with gold pages `{4,9}`, foldout pair `{6,7}` on innermost and one orientation-reversed, page12 outer, group exclusions `{1,2}` and `{11,12}` from gold. Gold must resolve middle; reversed-capable signature must resolve inner; remaining signature outer.

**M39 local-formula insufficiency** — for M38, correctly inverse-filling all three signatures under the wrong role assignment still fails global predicates.

**M40 preview-loop resilience gate** — design acceptance, not automated proof: mature playtest sample must show players making hypothesized edits rather than majority blind swap->preview enumeration; if it fails, content/UX must be repaired before freeze.

---

# 18. Known implementation-flexible choices deferred intentionally

These are not unresolved game design; later phases may choose presentation/engineering details without changing mechanics:
- exact visual geometry of fold animation;
- whether template-capacity change in M30 blocks or atomically ejects displaced faces, as long as no data is lost and history is deterministic;
- mouse gesture vs click-select interaction;
- exact iconography and colors for orientation/material/nest role;
- solver algorithm/library;
- internal serialization format;
- whether final positions are numbered continuously on screen or represented spatially once the player understands them.

---

# 19. Phase-4 closure

Mechanical architecture is now sufficient to author content without inventing core gameplay.

Frozen Phase-4 authority:
- canonical PageFace / FlatSlot / Signature / FoldTemplate / BoundBookState model;
- exact transform ordering;
- T4/T4F/T8/T6P catalog grammar and base catalog ceiling;
- binary orientation XOR semantics;
- deterministic nesting domains;
- finite predicate language;
- reversible edit/history contract;
- preview/commit equivalence;
- legality/failure/success semantics;
- difficulty knobs and teaching order;
- solver/equivalence/certification contract;
- anti-bookkeeping ceilings;
- 40 mechanical acceptance tests.

No production implementation has started.

## NEXT ACTION — PHASE 5 CONTENT ARCHITECTURE

Define the complete content system around these mechanics:
1. campaign chapter/family structure mapped to the frozen teaching order;
2. minimum/target case counts and quality floor rather than filler quota;
3. exact case data schema and authoring fields;
4. at least 8–10 content families that recombine existing rules rather than add uncontrolled mechanics;
5. authored vs generated responsibilities;
6. solver-backed generation/validation pipeline and anti-isomorphism/repetition checks;
7. demo case set and campaign pacing;
8. optional challenge/badge content if it does not contaminate baseline completion;
9. content reuse, motifs, page-face asset grammar and localization-safe content rules;
10. expansion boundaries and explicit prohibited content drift;
11. concrete content acceptance tests and a proposed ~30-strong-case campaign map.
