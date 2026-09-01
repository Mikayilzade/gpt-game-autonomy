# GAME #012 — PHASE 5 CONTENT ARCHITECTURE

Date: 2026-09-01
Status: **PHASE 5 COMPLETE**
Product: **OPENWORK** *(provisional working title)*
Authority: authored campaign/content structure and case-validation contract. `GAME12_MECHANICS.md` remains authoritative for exact rules.

## 1. Content thesis
OPENWORK ships as a compact authored deduction campaign, not as an endless generator. The target is **36 cases**; the launch quality floor is **30 cases**. A weak case is cut rather than justified by quantity.

The campaign must prove a progression of *ways to reason about the same void* rather than introduce new mechanics. The only launch pieces remain 1x1, straight 1x2 and straight 1x3; the only launch objective grammar remains the Phase-4 predicate set.

The core content risk is repetition into “spot the neck.” Therefore content is accepted only when its principal deduction, false candidates and coupled predicates materially differ from neighboring cases.

## 2. Canonical case-data schema
Authored source data is declarative. Derived topology and certificates are never hand-authored as truth.

### Authored fields
- `case_id`: stable unique string, e.g. `ow_a3_c04`.
- `content_version`: integer authoring revision.
- `title_key`: localizable optional display key; not used by rules.
- `act`: 1–6.
- `sequence`: order within act.
- `board.width`, `board.height`: 1–9, both integers.
- `board.fixed_solid_cells`: canonical sorted coordinate list. Every other in-rectangle cell is base OPEN.
- `markers`: 0–6 records `{id, cell, visual_slot}`; IDs unique and cells OPEN.
- `pieces`: 1–4 records `{instance_id, shape, orientation_policy}` using only frozen shapes/policies.
- `predicates`: 1–6 atomic predicates from the frozen grammar. Normal authored range remains 2–5.
- `allow_multiple`: default false. Any true value requires named human review note.
- `family_tags`: one principal F1–F8 tag plus zero or more secondary tags; metadata only.
- `teaches`: short author note describing the intended invariant/aha, never shown as solution text.
- `difficulty_intent`: `INTRO`, `EARLY`, `MID`, `LATE`, `MASTERY`.
- `demo_eligible`: boolean.
- `author_notes`: non-canonical rationale/known false candidates.

### Derived-only fields
Generated from exact case data + exact rules:
- canonical case-data hash;
- legal placement lists per instance/orientation;
- `raw_complete_assignments`;
- `canonical_complete_assignments`;
- satisfying canonical solution count;
- witness solution(s);
- witness derived topology tuple;
- predicate truth vectors for every assignment when generating analysis reports;
- measurable difficulty features;
- similarity fingerprint;
- rules/certifier version and hash.

Derived fields may be cached beside a case but cannot override the evaluator.

### Schema rejection before search
Reject before exhaustive enumeration if:
- any dimensions/piece/marker/predicate count exceed frozen ceilings;
- marker lies on FIXED_SOLID;
- duplicate marker ID/cell exists;
- predicate references unknown marker/boundary;
- impossible or malformed area/boundary multiset length is detectable statically;
- identical atomic predicate is duplicated;
- no complete geometric placement exists for a required piece.

## 3. Campaign structure — 36 target / 30 floor
Six acts of six cases. Acts introduce *reasoning lenses*, not mechanics. Cases within an act are not six variants of one template; every act deliberately cross-pollinates prior families.

### Act I — See the Void (6)
Purpose: teach that remaining OPEN space is the scored object.
- 2 F1 articulation lessons, one truly direct and one marker-constrained.
- 1 F2 first enclosure.
- 1 F3 simple marker partition.
- 1 F7 preserve-the-obvious-neck inversion.
- 1 small coupled recap using component + marker predicates.
Gate: by case 6 the player has seen both “closing a neck is useful” and “closing the obvious neck is wrong.”

### Act II — Inside / Outside (6)
Purpose: holes and exterior contact become intuitive without topology vocabulary.
- 2 F2 ring/seal cases with different piece roles.
- 1 F4 boundary-signature case.
- 1 F7 one-component + one-hole inversion.
- 1 F3 marker partition constrained by exterior escape.
- 1 F6 light hole+partition coupling.
No new UI noun beyond already-visible hole/boundary predicate icons.

### Act III — Who Shares the Space? (6)
Purpose: marker grouping and boundary ownership dominate; articulation is no longer enough.
- 2 F3 partition cases.
- 1 F4 exact boundary signature.
- 1 F5 area-balanced split.
- 1 F8 same topology / wrong sizes.
- 1 F6 coupled partition + hole.
At least 4/6 require >=2 predicate classes to isolate the solution.

### Act IV — False Openings (6)
Purpose: weaponize the player's learned heuristics.
- 2 F7 explicit false-neck/false-ring inversions.
- 1 F4 boundary decoy case.
- 1 F5 area-decoy case.
- 1 F8 same-count, wrong-allocation case.
- 1 F6 three-way coupled case.
Every case has >=2 plausible local candidate zones before global predicates are applied.

### Act V — Coupled Cuts (6)
Purpose: late-game deductions span spatially separated zones.
- 2 F6 coupled hole+partition/boundary cases.
- 1 F5 exact allocation with multiple cuts.
- 1 F8 topology-equivalent decoys.
- 1 F4 boundary signatures with rotatable-bar ambiguity.
- 1 mixed F3/F7 preserve-route case.
At least 5/6 couple >=2 predicate classes and at least 2/6 couple three classes.

### Act VI — Openwork (6)
Purpose: mastery under the same vocabulary, not size inflation.
- 2 F6 mastery cases.
- 1 F8 topology-equivalent decoy mastery.
- 1 F5 quantitative allocation mastery.
- 1 F7 inversion mastery where the visually strongest articulation is a trap.
- 1 finale combining marker partition + boundary signature + hole or area constraint inside <=4 pieces.
No finale may use >9x9, >4 pieces, >6 markers, >6 predicates or a new shape.

## 4. Family allocation / anti-repetition budget
A case may carry several family tags, but one `principal_family` is mandatory for quota accounting.

Target principal-family distribution across 36:
- F1 Articulation cut: **4**
- F2 Seal without severing exterior: **5**
- F3 Marker partition / false necks: **5**
- F4 Boundary signature sculpting: **4**
- F5 Area-balanced split: **4**
- F6 Coupled hole + partition: **6**
- F7 Preserve-the-neck inversion: **4**
- F8 Same topology, wrong sizes: **4**
Total: 36.

This keeps principal single-articulation content at 11.1%, safely below the Phase-4 25% maximum. Even if several secondary cases incidentally contain articulation reasoning, no more than **9/36** may have the principal deduction “occupy a single articulation cell.”

Hard campaign gates:
- Acts III–VI: >=12 of 24 cases must require >=2 predicate classes to reduce the candidate set beyond two assignments; target >=18/24.
- Acts II–VI: every act contains >=1 case where the visually strongest neck is wrong.
- F2–F8 credibility gate: at least four of these families must each yield >=4 accepted cases before a 30-case release is allowed.
- No adjacent pair in campaign order may share the same principal family *and* same piece multiset *and* same primary predicate-class set.

## 5. Authoring -> certification -> curation pipeline
### Stage A — Seed an intended deduction
Designer chooses principal family, board silhouette, piece multiset and 1–3 intended invariant interactions. Start from reasoning, not from a random target tuple.

### Stage B — Generate candidate board/predicate variants
Small scripts may perturb FIXED_SOLID mask, marker cells, orientation policies and legal predicates while staying inside frozen grammar. Generation is an authoring assistant only; generated cases have no standing until exhaustive certification and human review.

### Stage C — Exhaustive certification
Run the exact Phase-4 certifier. Produce all required counts and witnesses. Default acceptance requires exactly **1 canonical solution**.

### Stage D — Diagnostic analysis
For every candidate, compute:
- number of canonical complete assignments;
- number satisfying each individual predicate;
- number satisfying each predicate class alone;
- survivor counts after a proposed human reasoning chain;
- count of visually plausible “critical zones” estimated by topology features (articulation cells, near-ring closures, marker cutsets, boundary exits);
- minimum number of independent predicate classes needed to isolate the witness.

This detects decorative redundant predicates and cases where one obvious local move already solves everything.

### Stage E — Human curation
Human reviewer must answer:
1. Can the intended reason be stated in <=3 short invariant steps?
2. Is there at least one credible false candidate after onboarding?
3. Does each late predicate materially constrain play rather than merely restate the witness?
4. Is failure legible from the resulting void?
5. Is blind retry less attractive than reasoning at the intended band?
6. Does this case feel distinct from its nearest accepted neighbors?

### Stage F — Campaign integration
Only after certification + curation does a case receive final act/sequence. Re-run similarity and pacing checks whenever neighboring cases change.

### Rejection reasons
Stable rejection codes:
- `NO_SOLUTION`
- `MULTI_SOLUTION_UNJUSTIFIED`
- `SEARCH_TRIVIAL`
- `OBVIOUS_SINGLE_NECK`
- `PREDICATE_REDUNDANT`
- `PREDICATE_OVERLOAD`
- `BLIND_RETRY_FRIENDLY`
- `TRACE_NOT_LEGIBLE`
- `NEAR_DUPLICATE`
- `FAMILY_QUOTA_OVERUSE`
- `BOARD_SIZE_CARRYING_DIFFICULTY`
- `PIECE_COUNT_CARRYING_DIFFICULTY`
- `MARKER_CLUTTER`
- `FALSE_DIFFICULTY_FROM_TINY_HITBOX/READABILITY`
- `REQUIRES_NEW_MECHANIC`

## 6. Representative case specifications (12)
These are **content contracts**, not presumed certificates. Every one must be instantiated with exact coordinate masks and pass exhaustive certification before shipping. They deliberately span all eight families and all difficulty bands.

### R01 — One Cut, Two Rooms — INTRO / F1
Board intent: <=5x5 irregular dumbbell with exactly one true cardinal articulation candidate and two marker cells on opposite lobes.
Pieces: `1x1`.
Predicates: `COMPONENT_COUNT==2`, `DIFFERENT(A,B)`, `HOLE_COUNT==0`.
Certification obligation: unique canonical solution; >=10 canonical complete assignments so it teaches recognition rather than a two-choice quiz.
Role: first clean articulation lesson.

### R02 — Don't Cut Here — INTRO / F7
Board intent: <=5x6 with an obvious neck plus an almost-enclosed pocket elsewhere.
Pieces: one `1x1`, one fixed `1x2`.
Predicates: `COMPONENT_COUNT==1`, `HOLE_COUNT==1`, `HOLE_AREAS==[1]`.
Certification obligation: obvious articulation occupancy must be legal but fail; unique solution must seal the pocket while preserving exterior connectivity.
Role: invalidates the belief that necks are always the objective.

### R03 — Keep Them Together — EARLY / F2+F3
Board intent: 6x6 near-ring with markers A/B on exterior-connected sides of the ring.
Pieces: two fixed-orientation `1x2` bars.
Predicates: `HOLE_COUNT==1`, `HOLE_AREAS==[1]`, `SAME(A,B)`.
Certification obligation: >=2 placements satisfy the hole predicates alone; marker relation eliminates all but one canonical assignment.
Role: first explicit predicate coupling.

### R04 — Two Exits — EARLY / F4
Board intent: <=6x7 field with two plausible separating corridors and markers A/B.
Pieces: one rotatable `1x2`, one `1x1`.
Predicates: `COMPONENT_COUNT==2`, `COMPONENT_BOUNDARY_SIGNATURES==[N|W,E|S]`, `DIFFERENT(A,B)`.
Certification obligation: at least two assignments create two components; only one has the exact boundary signature tuple.
Role: teaches that “where a region can escape” matters independently of count.

### R05 — Equal-Looking Split — MID / F5
Board intent: 7x7 irregular field with several two-component cuts.
Pieces: one fixed `1x3`, one `1x1`.
Predicates: `COMPONENT_COUNT==2`, exact `COMPONENT_AREAS` authored from the certified witness, plus one marker relation.
Certification obligation: >=3 assignments must match component count + marker relation while differing in area multiset; exact area isolates the witness.
Role: makes quantity meaningful without arithmetic chains.

### R06 — Four Names, Two Spaces — MID / F3
Board intent: <=7x7 with four markers and at least three plausible cut zones.
Pieces: one rotatable `1x2`, one `1x1`.
Predicates: `SAME(A,B)`, `SAME(C,D)`, `DIFFERENT(A,C)`, `COMPONENT_COUNT==2`.
Certification obligation: unique solution; no single predicate may leave fewer than 3 canonical candidate assignments.
Role: marker partition as a global route constraint.

### R07 — Same Counts, Wrong World — MID / F8
Board intent: <=7x7; multiple placements produce the same number of components and holes.
Pieces: one fixed-H `1x2`, one fixed-V `1x2`, one `1x1`.
Predicates: `COMPONENT_COUNT`, `HOLE_COUNT`, exact `COMPONENT_AREAS` and/or boundary signature from witness.
Certification obligation: >=4 assignments must share `(component_count,hole_count)` with the witness; only one matches the full tuple.
Role: explicit proof that counts alone do not define the void.

### R08 — The False Door — MID/LATE / F7+F4
Board intent: 7x7 with the visually narrowest neck leading to the wrong boundary allocation.
Pieces: two `1x2` bars with different fixed orientations.
Predicates: `COMPONENT_COUNT==2`, exact boundary signatures, marker component A `AVOIDS` one boundary.
Certification obligation: strongest articulation closure must satisfy component count but fail boundary condition; unique alternate solution.
Role: anti-neck mastery.

### R09 — Pocket and Partition — LATE / F6
Board intent: <=8x8 with one near-ring and a separate marker cutset.
Pieces: fixed-H `1x2`, fixed-V `1x2`, `1x1`.
Predicates: one exact hole-area predicate, marker partition, total component count, one boundary predicate.
Certification obligation: each predicate class alone leaves >=2 candidates; at least two classes are necessary before candidate count drops to <=2; unique full solution.
Role: spatially separated coupled deductions.

### R10 — Which Bar Does What? — LATE / F6+F8
Board intent: <=8x8; the two bar roles are visually ambiguous but orientation/area consequences differ.
Pieces: one rotatable `1x2`, one fixed `1x3`, one `1x1`.
Predicates: component areas, one SAME/DIFFERENT relation, boundary signatures.
Certification obligation: >=100 canonical assignments preferred; unique solution; at least two superficially plausible assignments use the same occupied-cell count in different zones.
Role: piece-role ambiguity without adding shapes.

### R11 — Three Consequences — MASTERY / F6
Board intent: <=9x9, three local candidate zones such that one placement simultaneously affects a hole, marker route and exterior signature.
Pieces: 3–4 pieces from frozen vocabulary.
Predicates: 4–5 atoms from >=3 predicate classes.
Certification obligation: 500+ canonical assignments preferred; unique solution; no individual predicate and no obvious articulation choice may reduce search to one.
Role: late layered invariant chain.

### R12 — Openwork — MASTERY / F6+F7+F8
Board intent: finale-sized <=9x9 with multiple believable topologies, not merely maximum cell count.
Pieces: <=4; must include at least two distinct shape/orientation descriptors.
Predicates: marker partition + boundary signature + either hole or exact-area constraint; <=6 atoms total.
Certification obligation: unique canonical solution; >=1000 canonical assignments preferred; at least three distinct false candidates survive the first intended invariant; intended solve explanation must remain <=4 invariant steps.
Role: culmination of the original promise, with no new mechanic.

## 7. Old Round-C witness audit
Round-C examples were explicitly pre-freeze evidence. Phase 4 changed/clarified hole semantics: a hole is a remaining-open component with **zero boundary contact**, and component count includes holes.

A direct independent check of the old Round-C C4 stated witness under the frozen semantics gives:
- `COMPONENT_COUNT = 3`;
- `COMPONENT_AREAS = [1,4,29]`;
- marker partition A/C/D together and B separate;
- boundary signatures `[N, N|W, N|E|S|W]`;
- **HOLE_COUNT = 0**, not 1.

Therefore the old C4 target tuple is **not canonical content** and must not be copied into the campaign. This is exactly why tournament witnesses are evidence only. If its board silhouette is reused, the case must be reauthored around the frozen derived topology or altered to create a genuine boundary-disconnected component, then fully recertified.

Likewise C2's “compact C/ring-shaped mask” lacks exact coordinates and is a design sketch, not an accepted case. C1/C3 also require fresh certificate generation because their historical numbers cannot override Phase-4 semantics.

## 8. Difficulty bands — measurable, not board-size labels
Every accepted case receives a post-certification feature vector. Human curation assigns final band, but the assignment must be consistent with the metrics.

### Metrics
- `A`: canonical complete assignment count.
- `S`: canonical satisfying solution count (normally 1).
- `P`: number of atomic predicates.
- `K`: number of materially necessary predicate classes; a class is material when removing all predicates in it increases satisfying candidates or changes the unique witness set.
- `F`: number of credible false candidate zones/assignments surviving the first obvious local heuristic.
- `I`: intended invariant-chain length, 1–4, human-authored and reviewer-confirmed.
- `R`: redundancy ratio = predicates whose removal does not change candidate solution set / total predicates; accepted target is 0 for most cases.
- `N`: neck dominance flag — whether occupying one visually strongest articulation cell nearly solves the case.

### Band 0 — INTRO
Typical: `A 8–60`, `K 1–2`, `F 0–1`, `I=1`. Deliberately transparent teaching case.

### Band 1 — EARLY
Typical: `A 20–250`, `K 1–2`, `F 1–2`, `I 1–2`. One inversion or coupling is enough.

### Band 2 — MID
Typical: `A 80–1500`, `K>=2`, `F>=2`, `I 2–3`. Obvious local topology is insufficient.

### Band 3 — LATE
Typical: `A 300–10000+`, `K>=2`, usually 3, `F>=2`, `I 2–4`. Two spatially separated constraints or topology-equivalent decoys.

### Band 4 — MASTERY
No minimum board size. Expected `K>=3` or exceptionally strong F7/F8 inversion, `F>=3`, `I 3–4`, and blind enumeration clearly unattractive. Assignment count may be only hundreds if deduction structure is strong; it may be many thousands if readability remains high.

Counts are diagnostics, not automatic difficulty. A 10,000-assignment case with one glowing articulation cell is easier than a 200-assignment case whose candidates survive two coupled invariants.

## 9. Duplicate / perceptual-similarity control
Exact case hashes catch only literal duplicates. OPENWORK also needs structural/perceptual deduplication.

For every accepted case create a normalized fingerprint containing:
- board dimensions normalized under rotations/reflections for comparison only;
- FIXED_SOLID mask canonicalized across D4 board symmetries when dimensions permit;
- marker count and pairwise Manhattan-distance multiset;
- piece multiset by shape/orientation policy;
- predicate-class multiset;
- principal/secondary family tags;
- certified `(A,S,K,F,I)` bucket;
- witness derived topology `(component count, sorted areas, hole areas, boundary signatures)`;
- witness occupied-cell pattern canonicalized under board symmetries;
- intended-invariant tags such as `CUT_TRUE_NECK`, `PRESERVE_NECK`, `CLOSE_RING`, `BOUNDARY_ASSIGN`, `AREA_DISAMBIGUATE`.

Hard reject as `NEAR_DUPLICATE` when two cases share the same normalized board mask, piece multiset and predicate tuple up to symmetry, even if markers are renamed.

Human similarity gate: any pair sharing principal family + piece multiset + predicate-class set + same first intended invariant is reviewed side-by-side. At least one of these must differ materially: false-candidate geometry, invariant chain, resulting topology, or piece-role logic.

Campaign pacing gate: no three consecutive cases may share the same principal family or same first intended invariant.

## 10. Demo slice
Target demo: **6 campaign-equivalent cases**, approximately 20–35 minutes for a new puzzle player. Demo is a curated proof of the law, not Act I copied wholesale.

Suggested slice:
1. D1: direct F1 articulation lesson.
2. D2: F3 marker relation lesson.
3. D3: first F2 hole creation.
4. D4: F7 “do not cut the obvious neck.”
5. D5: light F4 boundary-signature case.
6. D6: mid-strength F6 coupled case as the demo climax.

Content protection rule: each demo case has a campaign sibling teaching the same idea through different geometry; the demo may include at most **one** of the campaign's top-three strongest examples for any family. The mastery cases R09–R12 are never demo content.

If demo progress carries to full game (Phase 7 decision), campaign ordering must handle already-completed sibling concepts without forcing replay.

## 11. Is >=30 quality content credible?
**YES, with an explicit empirical gate rather than blind confidence.**

Reasons the 30-floor remains credible under the frozen ceiling:
1. Eight challenge families already exist without new mechanics, and the target allocation needs only 4–6 principal cases per family.
2. Piece vocabulary has combinatorial role variation without catalogue growth: monomino precision, fixed bars, rotatable bars and mixed lengths create different placement footprints while remaining instantly legible.
3. The objective vocabulary cross-couples five distinct observable structures: component count/area, holes, marker relations and boundary signatures. Content variety comes from conflicts between these, not from six isolated objective types.
4. The certifier can search thousands of candidates cheaply at <=9x9 / <=4 pieces, allowing aggressive rejection rather than hand-protecting weak authored work.
5. Phase-4 anti-neck quotas plus the similarity fingerprint prevent the easiest failure mode from being hidden by reskins.

But the campaign is **not** considered proven merely because 36 slots are planned. Before specification freeze, content proof requires a certified corpus meeting all of:
- >=30 accepted unique-solution cases;
- >=4 accepted cases in at least four of F2–F8;
- <=25% principal single-articulation solutions;
- all Acts II–VI contain a false-neck inversion;
- >=50% of middle/late cases materially couple >=2 predicate classes;
- no near-duplicate hard rejects left in shipping set;
- at least 8 cases at Band 2+, at least 6 at Band 3+, at least 2 at Band 4 in the target 36-set;
- human blind-retry/playtest gate still deferred to Phase 10.

If authoring stalls below 30 under these gates, correct response is **cut/rethink the game**, not add portals, switches, new pieces or oversized boards.

## 12. Content implementation boundaries
Not launch requirements:
- procedural endless mode;
- player level editor;
- daily puzzle feed;
- workshop integration;
- random generated campaign order;
- narrative wrappers between every case;
- collectible modifiers or alternate piece powers.

A post-launch/editor tool may reuse the certifier, but it cannot redefine frozen mechanics.

## 13. Phase-5 acceptance
Phase 5 closes because the content system now has:
- exact authored/derived schema separation;
- a 36-case act plan and 30-case floor;
- explicit F1–F8 allocation and anti-repetition quotas;
- exhaustive authoring/certification/curation pipeline with stable rejection reasons;
- 12 representative case contracts spanning onboarding through mastery;
- a documented invalidation of the old Round-C hole witness under frozen semantics;
- measurable difficulty bands;
- structural/perceptual duplicate detection;
- a protected 6-case demo slice;
- a falsifiable >=30-case credibility gate that does not permit mechanic creep.

No production implementation begins here.

**PHASE 5 = COMPLETE.**

Next: Phase 6 UX / Presentation Architecture must specify controller/mouse interaction, board/piece selection, live topology feedback without becoming an oracle, predicate visualization, first-session onboarding, accessibility, responsive/Deck readability, undo/reset/failure/recovery, menus/settings, audio/visual causal language and demo/full-game continuity presentation.