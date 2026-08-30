# GAME #008 — CONTENT ARCHITECTURE

Last updated: 2026-08-30
Phase: **5 — Content Architecture**
Selected concept: **G8C02 Locksmith's Margin**
Working title: **Locksmith's Margin**
Production implementation started: **NO**

This file is the complete Phase-5 content authority. It uses only the mechanics frozen in `GAME8_PRODUCT_THESIS.md` and `GAME8_MECHANICAL_ARCHITECTURE.md`. It may compose accepted sets, blank counts, access predicates, initial cuts and authored visibility, but may not introduce new puzzle verbs or realism exceptions.

---

# 1. Content goals

The campaign must teach and deepen five recurring decisions without relying on locksmith trivia:
1. what did this failed test actually prove?
2. should I cut now or preserve compatibility?
3. which locks belong on the same persistent key?
4. when is a blank more valuable as a probe than as an opener?
5. how does access order change the information value of a test?

Content quality is measured by causal distinctness, not case count. A parameter swap, lock renaming or mirrored column order is not new content.

---

# 2. Campaign size and release floor

## 2.1 Target
- **Target main campaign: 32 authored cases** numbered C01–C32.
- **Strong release band: 28–34 validated cases.**
- **Minimum shippable campaign: 28 cases** only if all mandatory families and finales below are represented and no filler is needed.
- Cases above 32 are optional only if they introduce a genuinely distinct causal structure under the frozen mechanics.

## 2.2 Session length bands
- C01–C06: 2–6 minutes expected first-solve.
- C07–C16: 5–10 minutes.
- C17–C26: 8–15 minutes.
- C27–C32: 12–22 minutes.
- No required case should exceed 25 minutes median first-solve in target-player testing.

## 2.3 No volume quota override
If only 29 strong cases survive validation, ship 29 rather than inflate to 32 with isomorphs. The campaign number is a planning target, not authority over quality.

---

# 3. Tutorial dependency graph

Tutorial concepts form a DAG; later cases may assume all ancestors but may not require an unintroduced concept.

`T0 discrete key state`
→ `T1 TEST first blocker`
→ `T2 FILE +1 and forward irreversibility`
→ `T3 accepted-prefix knowledge`
→ `T4 overcut / TOO_DEEP`
→ `T5 multi-lock overlap`
→ `T6 deliberate non-cut / preserve margin`
→ `T7 multiple blanks / partition`
→ `T8 diagnostic value before opening`
→ `T9 master branch / BETWEEN_BRANCHES`
→ `T10 wear bridge / broad accepted set`
→ `T11 visible access predicates`
→ `T12 diagnostic-then-convert`
→ `T13 mixed multi-family planning`

Rules:
- T0–T6 must be learned by C06.
- T7 by C08.
- T8 by C12.
- T9 by C16.
- T10 by C19.
- T11 by C22.
- T12 by C25.
- T13 is the late-game synthesis, not a new mechanic.
- No tutorial may depend on optional mastery completion.

---

# 4. Campaign spine C01–C32

## Act I — Causal literacy / first compatibility aha (C01–C06)
**C01 First Mark** — 1 lock / 1 blank / 4 columns. Singleton sets. Demonstrates TEST → first blocker → FILE one step.

**C02 Prefix** — 1 lock / 1 blank. Requires noticing that every column before the blocker was accepted; fewer tests solve if player trusts accepted-prefix evidence.

**C03 Too Far** — starts with one pre-cut column. Player encounters deterministic TOO_DEEP and learns that further filing cannot repair it; Undo/Restart is surfaced without punishment.

**C04 Two Locks** — 2 locks / 2 blanks. Both are individually trivial; purpose is bench navigation, actual successful test coverage and persistent opened-state semantics.

**C05 Shared Scar** — 2 locks / 2 blanks. One key vector can open both; specialization remains possible, so overlap is discovered safely.

**C06 Stop Cutting** — 2 locks / 1 blank. Opening both requires deliberately refusing an unnecessary deeper cut. This is the first mandatory product-hook case and demo finale candidate.

## Act II — Partition and information value (C07–C12)
**C07 Pair + Specialist** — 3 locks / 2 blanks. One shared key plus one specialist.

**C08 Wrong Partition** — 3 locks / 2 blanks. Early tempting A/B pairing is feasible locally but blocks C; intended lesson is evaluate coverage topology before finishing a current lock.

**C09 Cross-Pair** — 4 locks / 2 blanks. Two non-obvious pairings; column overlap differs by lock so one-key-per-lock is impossible.

**C10 Probe First** — 3 locks / 2 blanks. One blank should remain non-opening after first test because its state is informative against another lock.

**C11 Strong Mark Trap** — strongest current TOO_SHALLOW information suggests a deep correction that destroys cross-lock overlap; accepted-prefix facts point to a safer test first.

**C12 Diagnostic Life** — 4 locks / 3 blanks. First explicit case where a diagnostic-only key is valuable for multiple tests before later conversion.

## Act III — branching accepted sets (C13–C16)
**C13 Two Ways Fit** — introduces one visible master-branch column in an otherwise easy case.

**C14 Between** — intentionally lands in a branch gap and teaches BETWEEN_BRANCHES as exact information, not noise.

**C15 Branch Sharing** — shallow branch overlaps B, deep branch overlaps C; choice is about future grouping.

**C16 Branch Partition** — 4 locks / 2 blanks, two branch columns; must choose compatible branch combination across targets. No access gates yet.

## Act IV — tolerance / wear as overlap shape (C17–C19)
**C17 Wide Enough** — first worn column. Broad accepted interval is a benefit; exact-centering behavior is explicitly unnecessary.

**C18 Wear Bridge** — a broad service lock bridges compatibility between a precise lock and an otherwise awkward key state.

**C19 False Precision** — multiple broad columns punish copying an imagined center; intended solve minimizes destructive edits while satisfying all sets.

## Act V — access-order information (C20–C22)
**C20 Behind A** — first `AFTER_OPEN(A)` gate. Opening A exposes B; solution remains easy and focuses on legibility.

**C21 Any Door** — `AFTER_ANY({A,B})` creates two valid discovery orders with different information efficiency.

**C22 Order Debt** — 4 locks / 2 blanks; opening the most obvious initial lock first remains solvable but forces extra destructive specialization, while another first test preserves a shared branch. Access rules are all visible at start.

## Act VI — mature diagnostic conversion (C23–C26)
**C23 Probe Pair** — one blank distinguishes two hidden compatibility families through first blockers.

**C24 Delay Completion** — current lock can be opened immediately, but doing so via a deeper edit removes the best probe state for a gated lock.

**C25 Convert the Probe** — diagnostic blank is deliberately kept non-opening through two locks and then converted only after its information role is exhausted.

**C26 Symmetry Break** — two blanks begin with identical vectors but different observation histories; fit symmetry is preserved while information history makes the next rational test differ.

## Act VII — mixed mastery (C27–C30)
**C27 Branch + Wear** — branch choice on one column and broad tolerance on another create a shared key that looks less exact than either lock alone would suggest.

**C28 Access + Partition** — 5 locks / 3 blanks; access DAG and coverage partition jointly matter.

**C29 Three Policies Fail** — constructed to defeat deepest-first, shallowest-always and finish-current-lock policies using only already learned rules.

**C30 Information Budget Without Currency** — tests remain free; challenge comes solely from irreversible state and access sequence. Case is rejected if adding tests monotonically eliminates the strategic dilemma.

## Act VIII — finales (C31–C32)
**C31 Workshop Job** — 5 required locks / 3 blanks / 6 columns. One exact specialist, one shared branch key, one diagnostic-then-converted key. At least one wear bridge and one access predicate.

**C32 Locksmith's Margin** — 6 required locks / 3 blanks / 6 columns. Maximum normal campaign complexity: <=2 branch columns total, <=3 access depth, no new rules. Intended solution includes: an early imperfect shared key, a probe held past an available opening, one deliberate irreversible commitment that becomes correct only because of previously gathered prefix evidence, and a final repurposed key. Must admit at least two strategically distinct valid solution traces, not one brittle sequence.

---

# 5. Demo architecture

Target: **6 cases / 20–30 minutes**. Demo content may use dedicated IDs `D01–D06`; it should not require a save from the full campaign, though full release may recognize completion and skip equivalent tutorials.

**D01 First Mark** — one lock, one blank; first blocker + one-step file.

**D02 Too Far** — safe overcut demonstration with immediate Undo.

**D03 Two Locks** — same key tested across two cylinders; player sees persistent artifact value.

**D04 Shared Scar** — first actual same-key multi-lock opening, but spare blank keeps pressure low.

**D05 Margin** — two locks / one blank; obvious unnecessary cut would destroy overlap. First strong `do not cut` realization.

**D06 Siblings** — 3 locks / 2 blanks; must partition one shared pair plus specialist. End image is one visibly scarred/imperfect key opening two locks beside the specialist key.

Demo hard rules:
- no master branch, wear or access gates;
- no more than 5 columns and D<=4;
- D06 must be solvable in <=12 authoritative FILE actions in the intended solution;
- median fresh-player demo completion target 20–30 min;
- product hook must be encountered by D05 even if player brute-forces earlier cases;
- demo ends immediately after the multi-lock compatibility payoff, not with a feature teaser dump.

---

# 6. Structural puzzle families

Families classify the main causal reason a case is interesting. A case may have secondary tags, but only one primary family counts toward family quotas.

## F1 — Causal Literacy
First blocker, prefix, TOO_SHALLOW/TOO_DEEP, discrete irreversibility.
- minimum 3 / target 4.

## F2 — Overlap Preservation
One current key can satisfy multiple locks if player avoids unnecessary edits.
- minimum 4 / target 5.

## F3 — Coverage Partition
Several locks must be grouped across a smaller set of blanks.
- minimum 4 / target 5.

## F4 — Diagnostic Sequencing
A key/test is valuable because of information before completion.
- minimum 4 / target 5.

## F5 — Master Branch
Disjoint accepted bands create branch-choice compatibility.
- minimum 3 / target 4.

## F6 — Wear Bridge
Broad accepted intervals create deliberate compatibility bridges; never `damaged lock randomness`.
- minimum 2 / target 3.

## F7 — Access Order
Visible test-access predicates alter which information/coverage is available first.
- minimum 3 / target 3.

## F8 — Mixed Finale
At least three already-learned families interact and no one family dominates the solve.
- minimum 3 / target 3.

At 32 cases target distribution may exceed these minima. If a case appears to fit no family, it probably relies on an unauthorized gimmick and is rejected.

---

# 7. Exact case-data schema

Each authored case is a declarative data record.

## 7.1 Metadata
- `case_id`: stable unique string (`C01`, `D01`, etc.).
- `schema_version`.
- `title_loc_key`.
- `campaign_order` or demo order.
- `primary_family`: F1..F8.
- `secondary_tags`: bounded list.
- `tutorial_concepts_introduced`.
- `tutorial_concepts_required`.
- `expected_first_solve_minutes_min/max`.
- `author_notes` excluded from runtime authority.

## 7.2 Domain dimensions
- `column_count C` in 4..6 for main campaign.
- `depth_max D` in 3..5.
- `blank_count` in 1..3 main campaign.
- `required_lock_ids` count 1..6.

## 7.3 Blank records
For each blank:
- `blank_id` stable within case.
- `start_vector[C]`, each 0..D.
- `visual_variant_id` presentation-only.
- optional `tutorial_focus` presentation hint only.

No blank-specific hidden fit rule exists.

## 7.4 Lock records
For each lock:
- `lock_id` stable within case.
- `required: bool` (main campaign normally true; non-required locks allowed only as clearly labeled practice/information objects and must be bounded).
- `accepted_sets[C]`, each non-empty finite set of integers 0..D.
- `access_predicate`: `ALWAYS | AFTER_OPEN | AFTER_ANY | AFTER_ALL` with referenced IDs.
- `visual_family_id` presentation-only.
- `knowledge_display_policy` must use global mechanics; no lock-specific secrecy exceptions.

## 7.5 Objective
Default: `OPEN_ALL_REQUIRED_ONCE`.
Optional mastery-only objective flags may include:
- `NO_UNDO`;
- `FILE_ACTIONS_AT_OR_BELOW(n)`;
- `TEST_ACTIONS_AT_OR_BELOW(n)` only as a mastery statistic, never to charge tests;
- `FINAL_COVERAGE` only for optional mastery cases explicitly labeled as such.

No optional objective may gate main campaign progression.

## 7.6 Validation expectations
- `intended_solution_examples`: 1–3 traces for author diagnostics, never runtime authority.
- `required_policy_failures`: list of named cheap policies that must fail when family maturity requires it.
- `max_reasonable_file_actions`.
- `max_reasonable_tests`.
- `expected_solution_partitions` optional structural target.
- `canonical_signature_version` for duplicate detection.

---

# 8. Authored vs generated responsibility

## 8.1 Authored authority
Humans/design agents author:
- campaign placement and tutorial purpose;
- lock count, blank count, access graph;
- accepted-set topology targets;
- desired overlap/partition/diagnostic insight;
- case title/presentation wrapper;
- whether a cheap policy must fail;
- pacing and difficulty intent.

## 8.2 Bounded candidate generation
Tools may generate candidate accepted-set matrices within a requested structural template, for example:
- `3 locks / 2 blanks / require exactly one 2-lock shared key + one specialist`;
- `one master branch; shallow branch overlaps lock B, deep branch conflicts`;
- `one worn interval creates unique bridge`;
- `access depth 2; at least two valid initial test choices`.

Generator must not create mechanics, narrative exceptions, random acceptance or hidden rules.

## 8.3 Generated content is never auto-published
Every generated candidate must pass the full validator and an authored causal review. A solver finding a solution proves feasibility, not fun, explainability or distinctness.

---

# 9. Validation pipeline

Every main/demo case must pass all stages.

## Stage V0 — schema/static legality
Reject malformed IDs, out-of-range depths, empty accepted sets, unknown access references, >2 disjoint intervals/column, forbidden dimensions or unauthorized objective flags.

## Stage V1 — access reachability
From authored initial state, prove at least one legal TEST exists. Prove every required lock becomes reachable in at least one solution. Reject mandatory access cycles with no reachable break.

## Stage V2 — omniscient solvability
Use complete hidden lock data. Prove at least one completion from initial state within state/action budget. Store solution length/partition summary, not merely boolean.

## Stage V3 — information-respecting fairness
Search policies that may choose only from observations/deductions legitimately available at each state. Require at least one policy path to completion without clairvoyant accepted-set knowledge.

This validator may branch over player choices. If no information-respecting path exists while omniscient path does, case is unfair and rejected.

## Stage V4 — forward-state softlock correctness
Enumerate/bound reachable FILE states. Every state labeled unsolvable by runtime softlock checker must truly have no completion. False positives are release blockers. Unknown due to budget is permitted and yields no warning.

## Stage V5 — cheap-policy attacks
Named baseline policies:
- P1 `FILE toward first TOO_SHALLOW until current lock opens`;
- P2 `finish current lock before testing another`;
- P3 `always keep every key as shallow as possible`;
- P4 `use one blank per currently targeted lock`;
- P5 `test every accessible lock with same blank before switching`;
- P6 `choose largest current known compatibility count`;
- P7 `never repurpose a key after opening a lock`;
- P8 `always pick the shortest apparent path to next OPEN`.

Tutorial cases may be solvable by simple policies. Mature cases tagged for a policy failure must produce a concrete counterexample trace where that policy either softlocks or uses materially more cuts/blanks than a valid intended-quality solution.

## Stage V6 — solution quality metrics
Compute:
- minimum FILE actions;
- minimum TEST actions conditional on information-respecting play where tractable;
- number of strategically distinct completion partitions;
- forced-action prefix length;
- branching factor over meaningful decisions;
- number of irreversible decisions before first informative alternate test opportunity;
- count of keys repurposed after first opening;
- count of diagnostic tests made before that blank's first opening;
- overlap density between lock acceptance regions at relevant depths.

No metric alone defines fun; they detect degenerate cases.

## Stage V7 — readability/pacing bounds
Reject or flag if:
- intended solution exceeds authored FILE-action ceiling;
- >3 consecutive FILE actions on same column are required in normal campaign after C06;
- case requires >4 repeated identical-result tests;
- solution contains >8 authoritative actions with no new observation, opening, access change or meaningful commitment;
- first meaningful information after case start requires >3 blind cuts;
- access depth >3;
- >2 simultaneously relevant branch columns;
- a required logical deduction depends on distinguishing presentation-only visual variants.

## Stage V8 — duplicate/isomorphism test
Canonicalize structure as defined below and reject near-duplicates unless tutorial purpose is explicitly different and the second case is intentionally simpler/earlier.

## Stage V9 — authored causal review
Reviewer must be able to write one sentence: `The interesting decision is ___ because ___; the obvious policy fails when ___.`
If that sentence is just `the numbers are harder`, reject.

---

# 10. Anti-isomorphism and duplicate detection

Parameter-swapped cases do not count as new content.

## 10.1 Exact structural canonicalization
Create a canonical signature invariant under:
- blank renaming;
- lock renaming that preserves required/access roles;
- uniform column permutation **only when** first-blocking evaluation order is permuted with the full case and thus remains behaviorally equivalent;
- cosmetic lock/key visual variants;
- title/narrative label changes.

The signature includes:
- C, D, blank start vectors;
- accepted-set matrices;
- required-lock flags;
- access predicate graph;
- tutorial/objective flags that alter legal play;
- evaluation order.

Enumerate bounded renamings/permutations at C<=6 and small lock/blank counts; choose lexicographically minimal serialized representation/hash.

## 10.2 Behavioral fingerprint
Because exact matrices can differ yet play identically, also record:
- set of minimal lock-to-blank coverage partitions under omniscient solve;
- minimum FILE length;
- reachable first-blocker observation tree up to bounded depth;
- named cheap policies defeated;
- access unlock sequence classes;
- presence/count of diagnostic-then-convert behavior.

Cases with identical/near-identical behavioral fingerprints enter manual duplicate review.

## 10.3 Diversity floor
Within any consecutive 4 main-campaign cases after C08:
- at least 3 different primary/secondary family signatures;
- no same canonical coverage topology twice unless information/access structure is materially different;
- no three cases with identical `(locks, blanks, C, D)` tuple;
- no back-to-back cases whose intended insight is `pair two locks, specialist third` without a new information/access cause.

---

# 11. Difficulty and readability gates

## 11.1 Complexity ceiling
Main campaign retains Phase-4 hard ceilings:
- C<=6;
- D<=5;
- <=6 required locks;
- <=3 blanks;
- <=2 disjoint accepted intervals per lock/column;
- <=2 master-branch columns per normal case;
- access depth<=3.

## 11.2 Cognitive staging
A case may introduce at most one new tutorial concept. It may combine previously learned concepts freely only after at least one reinforcement case for the newest concept.

## 11.3 Action economy
Target intended-solution FILE actions:
- tutorials <=8;
- early <=12;
- mid <=18;
- late <=24;
- finale <=30.

More than 30 FILE actions in a required case is a rejection signal; difficulty should come from choosing cuts, not performing them.

Target intended TEST actions:
- no hard scoring cap in core;
- tutorials <=10 typical;
- mature cases <=24 typical;
- >30 expected tests requires causal review for information grind.

## 11.4 Branching
At each mature decision point there should usually be 2–5 plausible meaningful actions, not dozens of equivalent TEST permutations. Benign redundant tests may exist, but content should not require exhaustive combinatorial probing.

---

# 12. Optional mastery and challenge content

Optional mastery is additive and cannot change core campaign rules.

Allowed:
- No Undo badge.
- Efficient Filing badge if completed within an authored non-tight FILE threshold.
- Insight badge for a designated structural behavior such as opening two locks with one key or converting a diagnostic blank.
- Final Coverage optional cases where all required locks must be simultaneously coverable by final key states, clearly labeled before play.
- Post-campaign `Workshop Challenges` using the same C<=6/D<=5 baseline and at most the same 3 blanks/6 locks.

Forbidden:
- timed dexterity challenges;
- limited tests as currency;
- random lock generation as required progression;
- larger-than-readable 8–10 column `expert` locks;
- realism modifiers;
- new tools or lock failure modes;
- achievements that require hundreds of repetitive cases.

Target optional challenge count at release: **0 minimum / 4–8 maximum**. Main campaign must stand alone.

---

# 13. Expansion boundary

Future expansion may add:
- more authored accepted-set topologies;
- new combinations of existing access predicates;
- new visual bench/cylinder/key themes;
- more optional mastery objectives from the allowed list;
- more campaign/challenge cases passing the same validators.

Expansion may not silently add:
- continuous filing;
- random jams/wear progression;
- pick tools;
- key copying/crafting economy;
- customer/shop management;
- currency;
- timed lock work;
- hidden mechanical exceptions;
- acceptance sets that change during a case.

Any such proposal reopens product/mechanical design rather than counting as ordinary content.

---

# 14. Content acceptance tests

A release candidate content set must satisfy all applicable tests.

### Schema / legality
CT01 Every case has stable case_id and schema_version.
CT02 Main case C is 4..6.
CT03 Main case D is 3..5.
CT04 Every blank start depth is within 0..D.
CT05 Every accepted set is non-empty and within 0..D.
CT06 No column has >2 disjoint accepted intervals.
CT07 No main case has >3 blanks.
CT08 No main case has >6 required locks.
CT09 Every access reference points to an existing lock.
CT10 Every objective flag is from the allowed global set.

### Tutorial graph
CT11 C01 requires no concept beyond T0.
CT12 A case never requires a tutorial concept whose dependency ancestor is absent.
CT13 No case introduces >1 new tutorial concept.
CT14 T0–T6 are all introduced by C06.
CT15 T7 is introduced by C08 or earlier.
CT16 T8 is introduced by C12 or earlier.
CT17 Master branch is not required before T9 introduction.
CT18 Wear is not required before T10 introduction.
CT19 Access order is not required before T11 introduction.
CT20 Diagnostic conversion is not required before T12 introduction.

### Reachability / solving
CT21 Initial state has at least one legal TEST.
CT22 Every required lock is reachable in at least one valid solution.
CT23 Omniscient solver proves at least one solution.
CT24 Information-respecting solver proves at least one fair solution.
CT25 No required case depends on hidden accepted-set knowledge unavailable from legal observation.
CT26 Every runtime-proven softlock state is actually unsolvable.
CT27 Solver timeout/unknown never emits a false softlock warning.
CT28 Opening a lock cannot duplicate access effects on repeated openings.
CT29 A completed lock remains completed after the opening key is repurposed.
CT30 Identical TEST state returns identical result and no new knowledge.

### Demo
CT31 Demo contains 5–6 cases; target is 6.
CT32 Demo uses no master branch.
CT33 Demo uses no wear mechanic.
CT34 Demo uses no access gate.
CT35 Demo never exceeds 5 columns or D=4.
CT36 Product-hook `do not cut / preserve overlap` is unavoidable by D05.
CT37 D06 requires multi-lock partition across <=2 blanks.
CT38 D06 intended solution uses <=12 FILE actions.
CT39 Demo has no content teaser requiring unexplained future mechanics.
CT40 Full-game save/import can map demo completion without making demo save authoritative over campaign balance.

### Family / diversity
CT41 Campaign contains at least 3 F1 cases.
CT42 Campaign contains at least 4 F2 cases.
CT43 Campaign contains at least 4 F3 cases.
CT44 Campaign contains at least 4 F4 cases.
CT45 Campaign contains at least 3 F5 cases.
CT46 Campaign contains at least 2 F6 cases.
CT47 Campaign contains at least 3 F7 cases.
CT48 Campaign contains at least 3 F8 cases.
CT49 Every case has exactly one primary family.
CT50 Every mature case can state its interesting decision and obvious-policy failure in one sentence.

### Anti-isomorphism
CT51 Exact canonical signatures are unique except explicitly approved tutorial reinforcement pairs.
CT52 Cosmetic renaming alone cannot create a unique signature.
CT53 Lock renaming alone cannot create a unique signature.
CT54 Blank renaming alone cannot create a unique signature.
CT55 Behaviorally near-identical fingerprints trigger manual review.
CT56 No consecutive four post-C08 cases violate the diversity floor.
CT57 No three consecutive cases share the same locks/blanks/C/D tuple.
CT58 Back-to-back `pair two + specialist` structures require materially different information/access causality.
CT59 Mirror/permutation variants do not inflate content count.
CT60 Generated candidates are never accepted solely because their exact hash differs.

### Pacing / readability
CT61 No required tutorial intended solution exceeds 8 FILE actions without explicit review.
CT62 No required finale intended solution exceeds 30 FILE actions without rejection review.
CT63 No normal solution requires >3 consecutive FILE actions on one column after C06.
CT64 No intended solution contains >8 authoritative actions without observation/open/access/meaningful commitment.
CT65 A required case never demands >3 blind cuts before first meaningful information.
CT66 No access dependency depth exceeds 3.
CT67 No normal case has >2 simultaneously relevant branch columns.
CT68 Presentation-only visual identity never changes logical solution.
CT69 No puzzle requires color-only distinction.
CT70 No puzzle requires audio/haptic-only distinction.

### Cheap-policy / mature depth
CT71 Every case tagged `defeat P1` actually makes P1 fail or materially underperform a valid path.
CT72 Same for P2.
CT73 Same for P3.
CT74 Same for P4.
CT75 Same for P5–P8 when explicitly tagged.
CT76 At least one C27–C32 case defeats three named cheap policies simultaneously.
CT77 C31 contains at least three previously taught families.
CT78 C32 contains no new mechanic or exception.
CT79 C32 has at least two strategically distinct valid completion traces.
CT80 C32 remains within 6 locks / 3 blanks / 6 columns / D<=5.

### Product integrity
CT81 No case uses random fit or changing accepted sets.
CT82 No case uses continuous/freehand filing authority.
CT83 No case charges currency/time/stamina for TEST.
CT84 No case introduces lockpicking or bypass tools.
CT85 No case introduces shop/customer economy.
CT86 No case requires real-world locksmith knowledge.
CT87 Optional mastery never gates main progression.
CT88 Optional Final Coverage is labeled before the first irreversible action.
CT89 Optional challenge content obeys the same discrete mechanical authority.
CT90 If a case cannot be explained without a bespoke exception, it is rejected rather than patched.

---

# 15. Phase-5 closure

**PHASE 5 CONTENT ARCHITECTURE = COMPLETE.**

The content system now defines:
- 32-case target campaign and 28-case quality floor;
- exact tutorial dependency DAG;
- six-case 20–30 minute demo;
- eight structural puzzle families and quotas;
- exact declarative case schema;
- authored vs generated boundary;
- omniscient + information-respecting validation pipeline;
- cheap-policy attacks and solution-quality metrics;
- exact structural canonicalization + behavioral duplicate fingerprinting;
- pacing/readability ceilings;
- optional mastery and expansion limits;
- **90 content acceptance tests**.

No new mechanic was added. Phase 6 may define presentation, controls, HUD, onboarding delivery, inspection/knowledge visualization, accessibility, menus and save/recovery UX without changing this content grammar.