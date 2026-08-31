# GAME #010 — PHASE 5 CONTENT ARCHITECTURE

Date: 2026-08-31
Status: **PHASE 5 ACTIVE — content contract established**
Game: Luggage Carousel Zero *(working title)*

Authority: `START_HERE.md` -> `STATUS.md` -> `GAME_INDEX.md` -> Game #010 tournament history -> `GAME10_THESIS.md` -> `GAME10_MECHANICS.md` -> this file.

Phase 5 may author and classify content using the frozen mechanics. It may not add new verbs, predicate operators, pickups, currencies, bag traits, or passenger systems.

## 1. Product content target
Canonical full campaign target remains **36–48 certified strong cases** plus a **6–8 case demo path** drawn from the same campaign content where practical.

Working target for architecture and production planning: **42 campaign cases**:
- Act A Ownership: 7
- Act B Identity: 8
- Act C Consequence: 8
- Act D Gaps: 9
- Act E Mastery: 10

These are target counts, not a promise that weak filler is retained. Minimum release-quality floor before freeze is 36 strong cases. If only 35 survive validation, content is incomplete rather than padded.

## 2. Canonical case-data schema
Each case definition must contain only data admitted by Phase 3/4:
- stable `case_id` and act/order metadata;
- N and pickup socket;
- label values by socket;
- bag entries: stable data ID, shape, mark;
- initial occupancy bag IDs/GAPs;
- ordered passenger predicates in canonical LABEL -> SHAPE -> MARK display order;
- tick_limit;
- swaps_per_tick;
- optional tutorial-only swappable_socket_mask;
- teaching tags / reasoning tags;
- author note and intended insight (non-runtime);
- solver certification record/hash/version (runtime packaging detail deferred);
- measured metrics: minimum ticks, effective swaps among min-tick solutions, viable opening count, canonical served-trait sequence families, gap sequence tags, intentional-miss test, gap-significance test, staging test, scarcity/substitution test;
- accessibility-safe display tokens for every label/shape/mark value.

No case-specific script is allowed to alter ordering, pickup semantics, predicate grammar, movement, Undo, DEAD, or budgets.

## 3. Content families
Cases are classified by **reasoning relationship**, not by cosmetic theme.

### F1 Alignment
Teach fixed label vs moving bag, next-arrival prediction, and one-step staging.
Primary Acts A/B.

### F2 Trait binding
Passenger requires immutable bag trait + current socket label. Introduces candidate-set reasoning without scarcity dependency.
Primary Acts A/B.

### F3 Substitution
Several bags can serve a passenger, but the choice changes later feasibility/timing.
Primary Acts B/C.

### F4 Scarcity preservation
A unique or near-unique bag trait class must be preserved from an earlier passenger.
Primary Acts B/C/E.

### F5 Intentional miss
Front passenger is serviceable now, but every immediate-service line loses; waiting/non-match is strategically necessary.
Primary Acts C/E.

### F6 Label staging
Useful swap occurs away from pickup and pays off on a later tick; pickup-only policy is insufficient.
Primary Acts B–E.

### F7 Gap phase
Initial or removal-created gap materially changes arrival phase / feasible service sequence.
Primary Acts D/E.

### F8 Duplicate-label flexibility
Repeated label values create several superficially equivalent resources whose socket phase matters.
Primary Acts D/E.

### F9 Bandwidth / K=2
Two swaps per tick create a meaningful 3-cycle/double-transposition planning problem; restricted to Phase-4 Envelope B.
Primary Act E only.

### F10 Synthesis
At least three prior families interact, but no new rule appears. Primary Act E.

A case may carry several tags. F10 is not an excuse for density: it requires distinct causal relationships, not merely more entities.

## 4. Per-act content obligations
### Act A — Ownership (7 target)
Must establish by case 2 that labels are socket-owned and bags move. Use N3–5, K0/1, mostly one-clause predicates. At least one K=0 observation case, but no more than two. End with first non-pickup label staging.

### Act B — Identity (8 target)
N4–6, K1. Introduce shape then mark while keeping max predicate width normally 2. Must contain >=2 genuine substitution cases, >=2 scarcity-preservation cases, >=3 label-staging cases. No intentional-miss requirement yet, though one soft preview is allowed.

### Act C — Consequence (8 target)
N4–7, K1. Queue coupling is central. At least 4 cases must satisfy exact `INTENTIONAL_MISS` metric; at least 3 must combine scarcity/substitution with queue order; at least 4 must defeat pickup-only label policy.

### Act D — Gaps (9 target)
N5–8, K1. At least 6 must satisfy exact `GAP_SIGNIFICANT`; at least 3 specifically require a **removal-created** gap to change a later phase. Duplicate labels enter systematically. No case counts as a gap lesson if removing/compressing the gap counterfactually leaves the same solution class.

### Act E — Mastery (10 target)
N5–8 K1 baseline; K2 only N<=6 and tick<=8. At least 6 synthesis cases with >=3 reasoning-family tags; 2–3 K2 cases maximum; up to three-clause predicates only when the third clause changes candidate competition rather than merely filtering. No case may earn its slot only by larger N, tighter tick limit, or wider predicate.

## 5. Demo path
Target 7 cases, ~15–25 minutes for a first-time thinky player:
1. fixed label vs moving bag;
2. label + shape;
3. first away-from-pickup staging;
4. substitution / preserve future bag;
5. first intentional miss;
6. pickup creates visible gap;
7. compact finale combining intentional miss + gap consequence + staging.

Demo must end before K2 and before dense three-clause cards. Full-game continuation should preserve completion/progress; commercial/technical details deferred to Phases 7/8.

## 6. Strong-case admission pipeline
Every authored/generated candidate passes, in order:
1. schema/invariant validation;
2. exact solvability under its Phase-4 envelope;
3. metric extraction;
4. family-tag proof (tags must match measurable counterfactuals where defined);
5. opening-quality check;
6. forced-wait check;
7. reasoning-trace dedupe against accepted pool;
8. visual/readability review at target presentation density;
9. human author judgment: can the intended insight be explained in one or two sentences without citing solver internals?

Generated candidates are never accepted solely because they are solvable or uniquely solvable.

## 7. Trace deduplication contract
Similarity is evaluated on mechanics, not bag art/name.

For each solution family record:
- passenger service ticks;
- served bag trait-class sequence;
- pickup label sequence at service ticks;
- GAP-at-pickup bit sequence;
- effective pre-Advance label vectors or canonical deltas;
- whether each service was earliest-feasible or intentionally delayed;
- reasoning tags proven by counterfactual tests.

Two cases are likely duplicates if their normalized traces and counterfactual tags are equivalent after renaming label/shape/mark values and trait-identical bags. Cosmetic renaming, ring rotation (normalized with pickup fixed), or larger N with irrelevant filler does not create new content.

## 8. Content quality budgets
- No >2 consecutive zero-effective-swap Advances unless each is justified by a significant gap/intentional miss and the sequence survives human pacing review.
- Passenger cards: max 3 clauses globally; Act A mostly 1, Acts B–D mostly <=2, Act E selective 3.
- Core N<=8; readability may force lower act-specific maxima later in UX phase.
- A case with one solver-viable opening is allowed, but campaigns cannot become a chain of forced first moves; mid/late pool should include both constrained and branching cases.
- Pure execution is impossible: carousel pauses indefinitely; all challenge is reasoning.
- No procedurally infinite/endless mode is promised. Solver-assisted generation is an authoring tool unless Phase 7 later finds a justified replay mode without weakening curation.

## 9. Authored vs generated content
Canonical campaign is **curated authored content**, potentially seeded by enumeration/search tools. Procedural generation is not player-facing canon.

Recommended workflow:
- author a reasoning target/tag combination;
- hand-seed compact state;
- let solver enumerate nearby variants/budgets;
- reject trivial/duplicate traces;
- human-select the clearest representative;
- retain solver certificate and counterfactual evidence.

This keeps content intentional while exploiting the deterministic system for coverage.

## 10. Phase-5 remaining work
Next increment must turn this architecture into a concrete content map, not merely add categories:
1. draft all 42 target case slots with act, N/K/tick envelope, predicate-width target and reasoning-family tags;
2. fully specify and hand-trace the 7 demo cases using exact bag/label/passenger data;
3. define at least 12 late-game case skeletons and prove that they occupy materially different normalized trace/counterfactual families;
4. identify any content-family shortfall or repetition discovered by the map and repair by changing case relationships only—never by adding mechanics;
5. freeze minimum/target per-family coverage and expansion boundaries;
6. close Phase 5 only when another session could populate/validate campaign data without inventing new content rules.

**PHASE 5 ACTIVE. DESIGN COMPLETE = NO.**