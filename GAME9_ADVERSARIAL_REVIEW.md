# GAME #009 — PHASE 10 ADVERSARIAL REVIEW

Status: **PHASE 10 COMPLETE / PHASE 11 READY**
Date: 2026-08-31
Selected game: **Binder's Imposition** (working title)
Production implementation: **FORBIDDEN in factory**
DESIGN COMPLETE: **NO**

Authority: `START_HERE.md` -> `STATUS.md` -> `GAME_INDEX.md` -> Game #009 tournament history -> `GAME9_PRODUCT_THESIS.md` -> `GAME9_MECHANICAL_ARCHITECTURE.md` -> `GAME9_CONTENT_ARCHITECTURE.md` -> `GAME9_UX_PRESENTATION_ARCHITECTURE.md` -> `GAME9_COMMERCIAL_MODEL.md` -> `GAME9_TECHNICAL_SPECIFICATION.md` -> `GAME9_WHOLE_GAME_SIMULATION.md` -> this file.

This phase is deliberately destructive. It attacks the full product as if a skeptical expert player, speedrunner, accessibility tester, content author, QA engineer and implementation team all try to break it. Repairs below are canonical clarifications or explicitly named narrow reopenings. Phase 3 product thesis remains intact.

---

# 1. Executive verdict

Binder's Imposition survives Phase 10, but not unchanged.

The design has three genuinely material risks:
1. **Preview-as-oracle:** Phase-6 wording that showed every predicate as satisfied/failed during Preview created a free branch-testing oracle in late cases.
2. **late-game clerical drift:** T8 orientation and T6P blank/trim semantics could become bookkeeping rather than deduction.
3. **implementation disproportion:** custom cloud conflict handling, durable history, imports and migrations could consume more engineering than the puzzle core if built too early.

All three are bounded without changing the central game. Additional ambiguities in mixed-size nesting, T4F flipping, T6P cut positions, template carry-over and badge semantics are resolved below.

No new transform family, predicate family, economy, progression currency, procedural mode, multiplayer feature or production implementation is added.

Phase 11 may now freeze the design if it verifies all repairs and empirical gates are represented explicitly.

---

# 2. Attack lane A — fun / repetition after T4 becomes rote

## Concrete attack
Assume an expert has memorized T4 and can inverse-fill any fixed T4 signature almost instantly. Give them ten late cases whose secondary requirements use SAME_SIGNATURE, MATERIAL and SIGNATURE_ROLE with different colors/names.

Observed abstract solve pattern:
1. derive the final page-domain membership of outer/middle/inner;
2. assign each tagged group to the only role that can contain it;
3. inverse-fill each signature using a memorized local map;
4. Preview once as proof.

Even when the face IDs, materials and page counts change, several cases reduce to the same set-partition proof.

## Failure
The game can technically contain 24+ non-isomorphic graphs while still *feeling* like the same reasoning sentence repeated.

Severity: **HIGH content risk, not core-mechanic failure.**

## Repair — reasoning-skeleton diversity is now mandatory
The existing structural fingerprint is extended with a human-level `reasoning_skeleton` label. Every STANDARD/MATURE/CAPSTONE case receives 1–3 ordered reasoning steps chosen from a controlled authoring vocabulary:
- LOCAL_INVERSE;
- NEST_DOMAIN_ELIMINATION;
- FACING_OR_LEAF_GEOMETRY;
- MATERIAL_OWNERSHIP;
- ORIENTATION_PARITY;
- TEMPLATE_ELIMINATION;
- BLANK_CAPACITY;
- TRIM_FATE;
- GROUP_PARTITION;
- LOCKED_EVIDENCE_PROPAGATION;
- MIXED_SIZE_DOMAIN_COMPOSITION;
- SYMMETRY_BREAK.

Release rules:
- no more than **4 shipped strong cases** may share the same ordered reasoning skeleton after cosmetic renaming;
- no two adjacent post-tutorial cases may share the same primary reasoning step unless the second is an explicit reinforcement bridge;
- Chapter VI's six target cases must have six distinct primary+secondary skeleton combinations;
- at least one-third of Chapter IV–VI strong cases must have a primary step other than GROUP_PARTITION or MATERIAL_OWNERSHIP;
- at least four late cases must be primarily about orientation/template/trim/mixed-size geometry rather than assigning colored groups to roles.

This is stricter than graph anti-isomorphism because it rejects experiential repetition even when the exact constraint graph differs.

## Regression tests
- certification report lists structural fingerprint + reasoning skeleton for all release cases;
- automated check rejects exact skeleton-count excess;
- human review compares every new case against its nearest two reasoning summaries;
- playtest debrief asks players to describe the deduction in one sentence; if many answers collapse to the same sentence, the content set is not certified.

Earlier phase reopened? **Phase 5 narrowly clarified.** No mechanical rule changes.

Empirical gate: before content lock, at least 12 representative post-tutorial cases must be playtested; if >50% of tester summaries collapse to the same role-partition description, authoring must be revised before freeze/release.

---

# 3. Attack lane B — Preview / Commit oracle leakage

## Concrete attack
Late two- or three-signature case has only 2 or 6 nest permutations and perhaps two template choices. Player:
1. performs a competent READ_ORDER inverse fill;
2. tests every nest role in turn;
3. runs Preview;
4. watches Goal Rail flip every predicate green/red;
5. chooses the branch with the best visible truth pattern;
6. repeats for template choice.

There is no scalar score, but the vector of predicate truth values is a stronger-than-intended oracle. Six free previews can replace the global deduction.

## Observed failure
Phase 6 allowed required predicate truth to appear for the whole resolved Preview. That contradicts the anti-hill-climb intention.

Severity: **HIGH.**

## Repair — Preview shows consequences, not an aggregate answer key
This explicitly reopens one Phase-6 detail.

### Frozen revised Preview rule
Preview still resolves the *entire exact physical book* and exposes all mechanically observable consequences:
- final face order;
- facing spreads;
- source signature/material ownership when inspected;
- orientation glyphs;
- leaf relationships;
- trim survival/removal;
- source mapping.

However, during ordinary Preview the Goal Rail does **not** automatically paint every authored predicate satisfied/failed.

Instead:
- directly visible requested relationships may be highlighted when the player selects that goal or involved face;
- the UI may say factual statements such as `P06 is on Signature B`, `MAP_A is inverted`, or `P04 faces P05` because these are visible properties of the resolved object;
- it may not automatically summarize `7/9 goals correct`, color the complete predicate list, rank branches, show deltas, or display hypothetical solver distance;
- `Commit` remains the place that evaluates and lists **all failed required predicates** exactly.

This keeps Preview useful as a physical reasoning surface while removing the one-glance branch-scoring vector.

### Commit enumeration attack
A player can still Commit six distinct nest orders for free. The design deliberately does **not** add lives, currency, cooldown or punishment. Exact failure explanation is an accessibility/usability value worth keeping.

Content therefore carries the remaining defense:
- a mature case must contain at least one wrong-global-branch witness;
- branch enumeration should not be faster than making the intended domain deduction once the player understands the rules;
- optional Direct Bind mastery rewards deliberate solving without gating progress.

The product accepts that a determined player can brute-force a tiny bounded structural choice. The design goal is to make reasoning clearer and more satisfying than enumeration, not to cryptographically prevent it.

## Regression tests
- Preview never displays aggregate predicate score/count;
- switching between six nest orders and Previewing cannot produce a sortable numeric/traffic-light vector without manually inspecting final book facts;
- source mapping never suggests an unchosen destination slot or move;
- Commit continues to return all failed predicates and exact final facts;
- same-state Preview and same-state Commit idempotency remain unchanged.

Earlier phase reopened? **YES — Phase 6 Goal Rail/Preview truth-display wording.** Phase 4 Preview transform itself remains unchanged.

Empirical gate: in mature-case playtest, if >40% of successful players primarily solve by systematic Preview/Commit branch enumeration rather than stating a hypothesis, content/onboarding must be repaired; no punitive retry system may be introduced as the first fix.

---

# 4. Attack lane C — D04–D06 tutorial/demo overload

## Concrete attack
A new player reaches:
- D04: second signature and nesting animation;
- D05: first editable nesting role **plus FACING**;
- D06: material ownership / SAME_SIGNATURE as a global tie-break.

Within roughly the final half of a 20–30 minute demo they acquire three global concepts after only three T4/T4F cases.

## Failure mode
The sequence is logically clean but the commercial time target can force rushed comprehension. A player can finish D06 by following highlights while still lacking a durable mental model.

Severity: **MEDIUM-HIGH empirical risk.**

## Repair — pacing gates, not another tutorial system
Canonical lesson order remains D01–D06 from Phase 9. No new mechanic is removed pre-emptively.

Demo certification now requires:
- D04 target competent first-solve time: **<=5 min median** after D01–D03;
- D05: **<=7 min median**;
- D06: **<=8 min median**;
- whole demo target remains **20–30 min median**, but a 75th-percentile completion up to roughly 40 min is acceptable if comprehension is strong;
- D05 uses only one FACING pair and no additional material/orientation novelty;
- D06 introduces material ownership as its only new predicate family; no new transform/template is introduced there;
- if D05 overloads testers, authored fixed evidence/pre-placement may reduce local manipulation before any rule is deleted;
- if D06 overloads testers, the demo may end after a smaller D06 variant while the full campaign keeps the stronger canonical concept. The full game's first six cases must still remain compatible with transferred progress; a demo-specific *subset of starting locks* may be more guided only if completion maps to the same case solution facts and does not create a separate rule system.

## Regression tests
- tester can explain why the wrong nest role cannot be fixed by local swapping after D05;
- tester can identify the physical signature owning a material-tagged face after D06;
- no demo case teaches two new transform families simultaneously;
- demo completion never requires memorizing `imposition` or `signature` terminology.

Earlier phase reopened? **No core rule reopening.** Adds Phase-5/7 empirical pacing acceptance.

Empirical gate remains mandatory before release.

---

# 5. Attack lane D — T8 clerical orientation burden

## Concrete attack
T8 mapping is `[A3,B0,A2,B1,B2,A1,B3,A0]` with alternating orientation bits. Put four orientation-sensitive faces into a mixed T8/T4 case and ask the player to reason about group/material constraints at the same time.

Observed human task becomes:
- remember source slot;
- remember final position;
- remember whether that slot inverts;
- remember selected sheet/role;
- then reason globally.

## Failure
The solver sees a clean XOR. A person sees eight tiny arrows. Difficulty can become bookkeeping unrelated to the satisfying book-fold insight.

Severity: **MEDIUM-HIGH.**

## Repair
T8 is retained but its parity map is treated as persistent visible apparatus information, not something to memorize.

Frozen limits:
- first T8 case has **<=2 mechanically orientation-sensitive faces**;
- ordinary T8 cases target <=3; mature cases may use 4 only when orientation is the primary reasoning family;
- when orientation is not a case's primary reasoning family, orientation-sensitive faces should normally be <=2;
- template mini-diagram and each affected source slot show the same redundant upright/inverted glyph before placement and in Preview;
- learned inverse-fill ghosts may show final-domain labels and orientation parity simultaneously once T8 tutorial is complete;
- no case gets difficulty credit merely from increasing the number of orientation-marked faces.

## Regression tests
- grayscale/high-contrast still exposes T8 parity;
- orientation can be solved without animation;
- test player may use the visible map without losing badge/achievement eligibility;
- content certification records orientation-sensitive face count.

Earlier phase reopened? **Phase 5 authoring limits clarified; Phase 4 transform unchanged.**

Empirical kill gate: if orientation mistakes remain the dominant source of incorrect commits in T8 synthesis after persistent parity aids, simplify T8 orientation requirements or replace weak T8 cases. Do not add more explanation text as the primary fix.

---

# 6. Attack lane E — T6P exception-family / blank bookkeeping

## Concrete attack
Current wording says T6P uses T8 geometry with two sacrificial positions, but did not freeze which positions. It also allowed REQUIRED_BLANK in sacrificial positions while elsewhere REQUIRED_BLANK means a real page that remains in the book.

## Failure
This is an implementation ambiguity and a conceptual trap. `EMPTY`, `REQUIRED_BLANK`, `SACRIFICIAL`, `CUT` and `BLANK_AT` can become an exception table.

Severity: **HIGH specification ambiguity.**

## Repair — exact T6P semantics
This explicitly reopens the incomplete Phase-4 T6P definition.

### T6P exact transform
T6P shares T8 source slots and T8 pre-trim local order:
`[A3, B0, A2, B1, B2, A1, B3, A0]`.

The sacrificial pre-trim local positions are **0 and 7**, corresponding to source slots **A3 and A0**.

After trim, those two positions are removed. The surviving six local faces preserve order:
`[B0, A2, B1, B2, A1, B3]`.

Orientation bits for surviving faces are inherited unchanged from T8.

### Token legality
- sacrificial CUT positions may contain `EMPTY` or an explicit `SACRIFICIAL` face/mark token;
- a `REQUIRED_BLANK` is a real surviving page and therefore is **not legal in a T6P CUT slot**;
- `BLANK_AT(position)` is satisfiable only by a surviving REQUIRED_BLANK face at that final position, never by EMPTY;
- `TRIM_RESULT(..., DISAPPEAR)` may target an explicit sacrificial mark/face in a CUT slot;
- no hidden partial clipping exists.

This turns T6P into one simple statement: **two edge faces are intentionally cut away; a blank page is still a page.**

## Regression tests
- T6P resolver exact fixture for all eight source slots;
- REQUIRED_BLANK in A3/A0 is rejected as illegal setup;
- EMPTY in a surviving slot is rejected unless a future template explicitly permits it (base T6P does not);
- trim explanation identifies source token and disappearance without suggesting a solution;
- T8 -> T6P template switch preserves all shared slot IDs, with A3/A0 assignments retained only if legal under T6P; illegal displaced faces return deterministically to tray under Phase-6 carry-over.

Earlier phase reopened? **YES — Phase 4 T6P exact positions/token legality.** No new transform family.

Empirical gate: if players still describe T6P as arbitrary exception rules after its first two cases, reduce T6P campaign presence rather than adding more trim variants.

---

# 7. Attack lane F — content exhaustion / false distinctness

## Concrete attack
Generate 30 solver-certified cases by varying:
- 2 vs 3 signatures;
- material labels;
- face IDs;
- one FACING pair;
- one SAME_SIGNATURE group;
- locked placements.

Automated graph checks reject exact isomorphs, yet the player experience can remain `determine which role owns this pair, then inverse-fill`.

## Failure
Structural diversity alone does not guarantee experiential depth.

Severity: **HIGH commercial/content risk.**

## Repair
Combine three independent release gates:
1. structural anti-isomorphism from Phase 5;
2. reasoning-skeleton diversity from Section 2;
3. human playtest summaries and manipulation profile.

Additional count rule:
- the game may ship at 24–30 strong cases only if **24 cases survive both structural and reasoning-skeleton review**;
- tutorial/reinforcement cases do not get reclassified as strong merely to reach 24;
- if only 20–23 strong cases survive, Phase 11 must not pretend the value thesis is unchanged: commercial price/content promise must be revisited before release implementation is considered complete;
- no fifth transform is added solely to manufacture case count.

## Regression tests
Certification report includes nearest structural neighbor and nearest reasoning-skeleton neighbor for every strong case.

Earlier phase reopened? **Phase 5 quality floor strengthened.** Phase 7 price band remains planning-only and already allows revalidation.

Empirical gate: a pre-production content spike must prove at least **12 distinct strong cases** across Chapters II–VI before full content production; otherwise the concept returns to design rather than scaling a weak case generator.

---

# 8. Attack lane G — dominant strategies

## Strategy G1: always solve READ_ORDER first
This is often efficient and sometimes correct.

Verdict: **not automatically an exploit.** Learning to inverse-fill is intended mastery. It becomes a problem only if READ_ORDER uniquely determines the rest.

Repair: Phase-5 Q1/Q3 remain authoritative. Mature cases must preserve a global decision that local inverse fill does not settle. Some cases should make role/template elimination the obvious *first* reasoning step, but the game does not force an arbitrary solving order.

## Strategy G2: always test nest roles in fixed order
With at most three signatures, a player can enumerate 2 or 6 orders.

Verdict: accepted bounded brute force, but Preview oracle repair makes it less frictionlessly scored. No artificial retry cost.

Content gate: cases cannot derive their entire challenge from choosing one of six nest permutations.

## Strategy G3: memorize inverse maps
Verdict: **intended mastery.** UX deliberately externalizes learned maps later. Late depth must move upward to role/template/predicate interaction.

## Strategy G4: Preview every edit
Verdict: technically possible. Free Preview is an accessibility-friendly choice.

Repair: same-state Preview reveals nothing new; no aggregate score; mature cases have wrong-global-branch witnesses; content playtest measures hypothesis-driven actions.

## Strategy G5: structured tools accidentally solve
Attack SWAP_PAIR, MOVE_GROUP and INVERSE-FILL GHOSTS.

Repair:
- tools may preserve/accelerate a player-chosen group but never compute which group should move;
- MOVE_GROUP works only on authored visible group tags and requires player destination choice;
- INVERSE-FILL GHOSTS expose deterministic template mapping only, never material/nest/template recommendation;
- if a structured tool reduces a certified mature case to <=3 meaningful choices, that case must be re-certified with the tool unlocked and may fail the strong-case floor.

## Regression
Certification solver/play trace uses the actual tool availability for that chapter, not a primitive-only fantasy interaction model.

Earlier phase reopened? **No.** Clarifies Phase 5 certification.

---

# 9. Attack lane H — late UX at 1280x800/controller/text scale/reduced motion

## Concrete attack
Three signatures, one T8, one T6P, 150% text, Goal Rail with four predicate families, controller-only, Reduced Motion.

Trying to keep all three full sheets, tray, goals and action strip visible makes source slots too small or forces dense scrolling.

Severity: **HIGH UX risk on target handheld if layout is rigid.**

## Repair — focused-signature layout is canonical fallback
At 1280x800 when text scale/layout thresholds cannot keep all active signatures comfortably interactive:
- show one **focused signature** at full workable size in the main canvas;
- retain a compact always-visible `Outer -> Inner` signature stack/overview with material/template/role summaries;
- shoulder buttons / Previous-Next Signature switch focus instantly;
- inactive signature miniature shows occupancy/group summary but is not a tiny precision editing surface;
- face tray and primary Preview/Commit/Undo remain directly reachable;
- Goal Rail may become the existing drawer before source interaction is compressed;
- no requirement says all three full editable signatures must be simultaneously visible.

Reduced Motion uses state diagrams/crossfades and cannot hide nesting order or orientation transitions.

## Regression tests
At 1280x800 test 100/125/150/max supported text scale with:
- three signatures;
- longest pseudo-localized predicate text;
- controller-only navigation;
- focused signature switching;
- no focus trap;
- no mechanically required hover-only content;
- reliable target size unchanged from accessibility floor.

Earlier phase reopened? **YES — Phase 6 layout detail clarified, not interaction semantics.**

---

# 10. Attack lane I — persistence / cloud / import hostile matrix

## Concrete hostile cases
1. crash between `save.tmp` write and primary replace;
2. valid primary + older backup;
3. corrupt primary + valid backup;
4. both corrupt;
5. unknown future schema opened by older build;
6. stale case revision with incompatible slot IDs;
7. repeated demo import after full game has more progress;
8. cloud branches each solve different cases and edit different unsolved cases;
9. cloud conflict copy itself later becomes stale;
10. achievement API offline during imported completion.

Phase 8/9 already handles most correctly.

## Material remaining risk
The specification could tempt implementation to build a miniature distributed database before the vertical slice exists.

Severity: **HIGH schedule risk, LOW game-design risk.**

## Repair — minimum safe implementation boundary
This changes implementation order, not release requirements.

### Mandatory before vertical slice/content production
- versioned local save;
- atomic primary + backup;
- exact in-progress WorkbenchState;
- bounded Undo/Redo persistence;
- known-schema migration fixture path;
- unknown-future-version non-overwrite behavior.

### May be deferred until platform integration phase
- Steam Cloud transport;
- divergent-branch merge UI;
- demo shared-cloud configuration;
- Steam achievement reconciliation calls.

### Release gate if Steam Cloud remains baseline
Before release candidate, cloud/import tests from Phase 8/9 are mandatory. If reliable conflict handling cannot be achieved, **disable Steam Cloud rather than ship state-loss risk**. Offline local progression remains authoritative. Phase 7's Cloud baseline is a target feature, not permission to compromise save integrity.

### Simplification rule
Cloud merge operates only on:
- monotonic campaign facts (union);
- settings mutation records;
- at most one primary in-progress workbench plus retained conflict copies.

Never attempt structural merging of workbench assignments/history.

## Regression tests
Crash-injection + fixture matrix required; no test depends on actual Gmail/email notifications.

Earlier phase reopened? **Phase 8 implementation ordering clarified; release product thesis unchanged.**

---

# 11. Attack lane J — technical scope disproportionate to puzzle size

## Concrete attack
Estimate implementation effort if built naively:
- puzzle resolver/validator/UI core;
- 3D fold animation;
- solver/certifier;
- controller focus;
- localization;
- atomic saves/history;
- custom cloud ancestry/conflicts;
- demo import;
- achievements;
- content anti-isomorphism tooling.

The platform/persistence/tooling tail can exceed the actual game core.

## Failure
A small elegant puzzle becomes a tooling project.

Severity: **HIGH production risk.**

## Repair — scope hierarchy
Implementation authority in dedicated repo must prioritize:
1. pure transform/evaluate core;
2. one T4 vertical slice;
3. authored data path;
4. source/goal UX + Undo/Redo;
5. content certification basics;
6. T4F/T8/T6P and nesting;
7. local persistence/accessibility/controller;
8. full content;
9. platform/demo/cloud polish.

Hard rule: no custom online backend, account system, telemetry service, workshop, leaderboard or runtime solver.

Solver tooling may start simple (exact enumeration/CSP for intended sizes) and only optimize when real authored cases prove it necessary.

Fold presentation may begin 2D/2.5D; polished paper animation is valuable but cannot hold the core hostage.

Earlier phase reopened? **No design reopening.** Phase 8 implementation order strengthened.

---

# 12. Attack lane K — mixed-size nesting ambiguity

## Concrete attack
Nest a T8 outer signature around T4 inner, then three mixed signatures T4/T8/T6P. Phase-4 prose said nesting works over leaves but did not provide one exact general transform.

Severity: **HIGH implementation ambiguity.**

## Repair — exact recursive mixed-size composition
For every resolved signature after its local fold/trim, its surviving local final-face sequence must have an even count `m` in the base catalog.

Define:
- `front_half(S) = local_faces[0 .. m/2-1]`;
- `back_half(S) = local_faces[m/2 .. m-1]`.

For signatures ordered `S0 outer, S1, ... Sn inner`, global face order is:

`front_half(S0) + front_half(S1) + ... + front_half(Sn-1) + local_faces(Sn) + back_half(Sn-1) + ... + back_half(S1) + back_half(S0)`.

Equivalent recursive definition:
`Nest(S_outer, InnerBook) = front_half(S_outer) + InnerBook + back_half(S_outer)`.

Examples:
- T4 outer + T4 inner -> 2 outer front + 4 inner + 2 outer back = 8 faces;
- T8 outer + T4 inner -> 4 + 4 + 4 = 12;
- T4 outer + T8 inner -> 2 + 8 + 2 = 12;
- T6P outer has six surviving local faces after trim -> 3 front + inner + 3 back.

Leaf IDs/facing pairs are then derived from the composed global sequence using each signature's local leaf identity plus nesting boundaries. No raw face-count special cases exist.

## Regression tests
Exhaustive fixtures for all pairwise template mixes and representative three-signature mixes; same input must produce canonical global order independent of renderer.

Earlier phase reopened? **YES — Phase 4 nesting formula clarified.**

---

# 13. Attack lane L — T4F / orientation XOR ambiguity

## Concrete attack
Phase 4 said T4F FLIPPED both `swaps A/B source-side interpretation` and toggles every final orientation. A developer could implement only the XOR bit and forget the source permutation, or vice versa.

Severity: **HIGH implementation ambiguity.**

## Repair — exact T4F mapping
T4F `NORMAL` uses T4 local order:
`[A1, B0, B1, A0]`.

T4F `FLIPPED` uses explicit swapped-source local order:
`[B1, A0, A1, B0]`.

For FLIPPED, the sheet-flip orientation bit is `1` for every resolved face in addition to each source slot/template bit. Thus orientation remains computed through the existing XOR formula.

No other implicit mirror, 90-degree rotation or side reinterpretation occurs.

`sheet_flip_bit=0` NORMAL, `1` FLIPPED for T4F. T4/T8/T6P do not expose FLIPPED unless a future design explicitly reopens their template definition; base campaign does not.

## Regression
Four source faces with unique IDs/orientation markers must resolve through exact NORMAL and FLIPPED fixtures.

Earlier phase reopened? **YES — Phase 4 exact mapping clarification.**

---

# 14. Attack lane M — template carry-over ambiguity

## Concrete attack
Switch T4 -> T8 -> T6P -> Undo/Redo with existing assignments.

Potential ambiguity: shared slot IDs exist across templates, but T6P makes A3/A0 sacrificial; a previously legal REQUIRED_BLANK or content face can become illegal.

## Repair
Phase-6 deterministic carry-over remains authoritative with this precedence:
1. identify shared slot IDs;
2. preserve assignment only if the assignment is legal under the **new template's slot/token rules**;
3. every non-shared or newly-illegal assignment returns to tray;
4. apply authored locked assignments;
5. run uniqueness validation;
6. show exact displaced count before confirmation;
7. record the full delta as one transaction.

For T8 -> T6P, A3/A0 are shared geometrically but their CUT legality is stricter. Ordinary content faces/REQUIRED_BLANK in those slots return to tray unless explicitly typed SACRIFICIAL/allowed.

Earlier phase reopened? **No; Phase 6 algorithm receives exact T6P legality input.**

---

# 15. Attack lane N — source mapping / hint leakage

## Concrete attack
In Preview, choose a failed page and invoke Source. If the UI also shows target final position, the player can infer the needed source slot by cycling candidate faces.

Verdict: deterministic inverse mapping is intentionally learnable and later externalized. Source mapping itself is not solver leakage.

Boundary:
- Source maps **current resolved face -> current source slot only**;
- it never maps desired target position -> recommended source slot for an unplaced/wrong face unless the inverse-fill ghost for that learned template already generically labels source slots by final-domain position;
- inverse-fill ghosts are template-general, not case-solution-specific;
- no button says `move P06 here`.

Earlier phase reopened? **No.**

---

# 16. Attack lane O — badges / stats ambiguity

## Direct Bind ambiguity
Phase 7 says `after the case's first resolved Preview, reach a successful Commit without another incorrect Commit`.

Frozen interpretation:
- Direct Bind eligibility begins only after the case has produced at least one resolved Preview in the current first-solve attempt;
- from that first Preview until first success, zero **distinct failed Commit states** are allowed;
- same-state Commit reopens do not count due to Phase-9 idempotency;
- if player never Previews and Commits successfully, Direct Bind is **not earned**; this badge celebrates prediction-then-bind, not blind direct submission;
- replay may earn the badge only if the case explicitly marks replay mastery as eligible; baseline planning should prefer first-solve-only for Direct Bind to avoid grind.

Predicted remains independent and is not invalidated by accessibility settings or choosing `Show me`; `Show me` simply means that specific prediction was not correctly predicted for badge evidence.

Earlier phase reopened? **Phase 7 clarified.**

---

# 17. Attack lane P — content revision / migration ambiguity

## Concrete attack
A shipped case revision changes locked slots or T6P semantics. Old unsolved WorkbenchState references now-illegal placement/history.

Repair from Phase 9 remains:
- attempt explicit case-revision migration only when authored deterministic mapping exists;
- otherwise preserve old in-progress snapshot/history as a recovery archive and start the revised case clean;
- never reinterpret unknown old slots by visual proximity;
- solved completion facts persist unless the case ID itself is intentionally retired under an explicit migration;
- certification metadata records which case revisions are compatible.

Phase-10 addition: **mechanical template definition revisions require a content-manifest version bump and are not silently hot-swapped under the same template revision.** T4F/T6P exact definitions from this file become the baseline revision used by implementation.

Earlier phase reopened? **No further design change.**

---

# 18. Final cross-phase acceptance matrix

Before Phase 11 may set DESIGN COMPLETE=YES, it must verify the final authority contains all of these:

1. Product identity unchanged: finite premium physical permutation puzzle.
2. Exact transform grammar: T4, exact T4F NORMAL/FLIPPED, T8, exact T6P cut positions/survivors.
3. Exact mixed-size nesting recursion.
4. Exact orientation XOR inputs and no hidden mirror/rotation.
5. REQUIRED_BLANK vs EMPTY vs SACRIFICIAL legality is unambiguous.
6. Preview uses exact transform but does not automatically expose an aggregate predicate truth vector.
7. Commit returns exact failed predicates and is same-state idempotent.
8. Structured tools are re-certified in content difficulty.
9. Reasoning-skeleton diversity supplements graph anti-isomorphism.
10. Demo pacing/comprehension is an empirical gate, not assumed from paper design.
11. T8 orientation counts are bounded and parity aids are permanent visible apparatus.
12. Focused-signature 1280x800 layout is a valid canonical fallback.
13. Local atomic persistence is mandatory before platform cloud complexity.
14. Cloud is disabled rather than shipped unsafely if release QA cannot guarantee integrity.
15. Unknown future saves are never overwritten.
16. No runtime solver, online backend, currency, MTX, live service or production implementation appears in factory.

---

# 19. Remaining empirical gates after Phase 10

These are legitimate implementation/playtest gates, not unresolved game rules:

## E1 — transform comprehension
After tutorial case 4, >=70% of representative testers predict at least two final relationships before Preview or can explain them immediately after one Preview.

## E2 — hypothesis vs enumeration
In representative mature cases, systematic Preview/Commit branch enumeration should not be the primary successful method for >40% of testers.

## E3 — demo cognitive load
Median demo target 20–30 min, with D04/D05/D06 pacing bounds above and demonstrated comprehension.

## E4 — T8 clerical error
Persistent visible parity aids must prevent orientation bookkeeping from becoming the dominant failure cause.

## E5 — T6P conceptual clarity
Players distinguish `Blank page` from `Unused cut-away slot` without relying on color and can explain the two sacrificial edge positions after tutorial.

## E6 — content depth
Pre-production spike proves at least 12 strong post-tutorial cases with distinct reasoning skeletons; full release requires >=24 strong certified cases unless commercial thesis is revisited.

## E7 — manipulation cost
12–20 face mature cases remain reasoning-dominant; structured tools do not trivialize them.

## E8 — handheld UX
1280x800 controller-only with 150% text and Reduced Motion remains fully operable without precision targets or hidden information.

## E9 — persistence
Crash/migration/cloud fixture suite proves no silent loss/corruption; Cloud may be disabled if this fails.

These gates may affect content, presentation, pricing, feature shipping or case selection. They do not authorize invention of new core gameplay without returning to design authority.

---

# 20. Phase-10 verdict

**PASS WITH REPAIRS.**

Binder's Imposition still has a coherent small-rule identity. The adversarial pass found real weaknesses, but none require abandoning or expanding the core concept. The most important change is removing automatic all-predicate truth coloring from Preview; the most important specification repairs are exact T6P semantics, exact T4F FLIPPED mapping and exact mixed-size nesting composition.

The game is ready for **Phase 11 — Specification Freeze**, but DESIGN COMPLETE remains **NO** until that phase produces a final authority document, resolves authority ordering, incorporates the Phase-10 repairs, lists remaining empirical gates and confirms that a fresh implementation session would not need to invent gameplay rules.

## NEXT ACTION
Create `GAME9_FINAL_FREEZE.md` as the single final design authority. Reconcile Phase 3–10 into an implementation-ready specification, explicitly incorporating every Phase-10 repair above. Include authority precedence, exact formulas/tables, content/demo/UX/commercial/technical acceptance gates, implementation-flexible areas, empirical gates, out-of-scope boundaries, migration package checklist and final completion criteria. Only after this reconciliation is internally consistent may Phase 11 set `DESIGN COMPLETE = YES` and attempt migration according to factory continuity rules.