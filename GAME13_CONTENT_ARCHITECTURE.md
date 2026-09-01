# GAME #013 — PHASE 5 CONTENT ARCHITECTURE

Date: 2026-09-02
Status: PHASE 5 COMPLETE — 24-CASE FLOOR PROVED / 30-CASE TARGET MAPPED
Selected concept: **SEAL BREAK** (working title)
Authority: `GAME13_MECHANICAL_ARCHITECTURE.md` remains authoritative for mechanics; this file freezes authored-content structure, campaign dependencies and anti-repetition requirements.

## 1. Phase-5 verdict up front
The frozen Phase-4 vocabulary supports a **credible 24-case commercial floor and a 30-case target without adding mechanics, predicates, durability, randomness, freeform tearing, larger-count filler or narrative rules**.

The campaign is therefore allowed to proceed to Phase 6.

The 24-case floor is not “30 cases minus six arbitrary levels.” It is a complete four-beat-per-act learning arc across six acts. Cases 25–30 are legitimate capstone/recombination extensions that widen cross-family interaction and mastery, not basic content needed to make the product coherent.

Shipping target remains 30 certified authored cases. If playtesting later proves cases 25–30 repetitive, they may be cut individually down to the 24-case floor without breaking the dependency graph.

---

# 2. Canonical authored case schema

Every shipping case record must contain the following semantic fields, whether represented in JSON, resources or another data format later.

## 2.1 Identity / campaign metadata
- `case_id`: stable global ID, e.g. `SB_01`;
- `title_key`: localization-ready title key, presentation only;
- `act_id`: `A1..A6`;
- `act_position`: integer within act;
- `campaign_position`: 1..30;
- `required_for_floor`: bool; true for cases 1..24;
- `demo_included`: bool;
- `prerequisite_case_ids`: explicit dependency list;
- `teaching_intent`: one concise statement of what the player should learn/prove;
- `difficulty_band`: `INTRO | EARLY | MID | LATE | CAPSTONE`;
- `estimated_first_solve_minutes`: authoring estimate, not a promise.

## 2.2 Mechanical setup metadata
- `compartments`: frozen Phase-4 compartment records;
- `seams`;
- `seal_sockets`;
- `placement_mode`: `FIXED | CHOOSE_EXACT_K | CHOOSE_UP_TO_K | CHOOSE_FROM_GROUPS`;
- `seal_budget_k` where applicable;
- `fixed_installed_sockets` where applicable;
- `history_mode`: one of the four frozen modes;
- `history_bounds`: min/max/exact length;
- `required_open`, `forbidden_open`, fixed position and precedence constraints if any;
- `authored_history_choices` if history mode requires them;
- `evidence_predicates`: frozen Phase-4 vocabulary only;
- `acceptance_projection`: omitted by default; present only for reviewed observable equivalence.

## 2.3 Certification metadata
- `expected_certification_class`: normally `UNIQUE_EXACT` or `UNIQUE_OBSERVABLE`;
- `expected_solution_class_count`: normally 1;
- `legal_submission_space_estimate`;
- `certifier_result_hash/version`: later generated, never hand-authored as authority;
- `zero_solution_guard`: must pass;
- `oracle_free_human_review`: `PENDING | PASS | FAIL`;
- `redundant_evidence_review`: `PASS` or documented tutorial exception.

## 2.4 Reasoning metadata
- `primary_deduction_tags`;
- `secondary_deduction_tags`;
- `required_deduction_count`;
- `setup_class` from Section 3;
- `trigger_motif_ids` from Section 8;
- `similarity_signature`: normalized tuple used for anti-repetition review;
- `anti_repetition_note`: why this case is not merely a denser copy of its neighbors.

A shipping case without these reasoning fields is incomplete content even if mechanically solvable.

---

# 3. Canonical content families / setup classes

Families are combinations of the same frozen rules. They do not authorize new mechanics.

## F1 — Direct witness reading
Fixed seals + fixed history. Player predicts/reads direct break cause and first-crossed semantics.
Purpose: tutorial only.

## F2 — Divergent witness comparison
Fixed seals + fixed or tiny finite history choice. Two or more witnesses overlap on some triggers but diverge on others.
Core deductions: `INTERSECTION_TRIANGULATION`, `PAIRED_DISCRIMINATION`.

## F3 — Survivorship / omitted event
Fixed seals + `ARRANGE_BOUNDED_SUBSET` or authored histories with explicit omission count.
Core deduction: `SURVIVORSHIP_COMPLEMENT`, often paired with `DELAYED_BREAK_BOUND`.

## F4 — Inverse witness placement
Player chooses seals; history is fixed or highly constrained.
Core deduction: `INVERSE_WITNESS_PLACEMENT` — choose which witnesses can generate the required evidence.

## F5 — History reconstruction
Seal set fixed; player arranges or selects history.
Core deductions: `HISTORY_RECONSTRUCTION`, `DELAYED_BREAK_BOUND`, overlap logic.

## F6 — Coupled placement + history
Player chooses both witness subset and bounded history.
Core deduction: `PLACEMENT_HISTORY_COUPLING` plus at least two other tags.
Late-game only.

### What is NOT a content family
The following never justify a campaign slot by themselves:
- +1 compartment;
- +1 seal;
- longer history;
- more evidence cards;
- larger trigger sets;
- changing cabinet art;
- changing labels/colors/patterns;
- replacing exact break predicates with semantically equivalent wording.

---

# 4. Predicate / mode introduction schedule

The player never receives the whole predicate vocabulary at once.

## Cases 1–4
Allowed target language:
- `BREAKS_AT`;
- `FINAL_INTACT`;
- optionally `FINAL_BROKEN` for explanation only.
History: fixed only.
Placement: fixed only until case 4 may expose a tiny authored choice.

## Cases 5–8
Introduce:
- `SAME_BREAK_STEP`;
- `BREAKS_EARLIER`;
- `INTACT_THROUGH`.
History may use `CHOOSE_FROM_AUTHORED_HISTORIES`.
Still no free arrangement.

## Cases 9–12
Introduce omission explicitly:
- `UNOPENED` only as teaching support;
- `ARRANGE_BOUNDED_SUBSET` in controlled form;
- `BREAKS_AFTER` where it creates a lower-bound deduction.

## Cases 13–16
Introduce player witness placement:
- `CHOOSE_EXACT_K`;
- `INSTALLED/NOT_INSTALLED` only when absence itself matters;
- fixed history remains dominant so placement is learned without simultaneous order search.

## Cases 17–20
Introduce history reconstruction:
- `ARRANGE_REQUIRED_SET`;
- `OPENS_AT` only in an onboarding reconstruction case and never as late-game crutch;
- delayed-break and paired comparisons combine.

## Cases 21–24
Introduce genuine coupling:
- seal selection + authored/arranged history;
- at least three deduction classes by case 24.

## Cases 25–30
No new predicate or history mode may appear. Difficulty comes only from recombination, decoys and stronger cross-witness dependency.

---

# 5. Concrete 24-case commercial-floor campaign

Campaign is six acts. Each act has a floor core of four cases. Cases 5,10,15,20,25,30 are target-only fifth beats where applicable; this preserves a coherent 24-case cut as `1–4,6–9,11–14,16–19,21–24,26–29` only if exact numbering were purely positional. To avoid confusing IDs, canonical shipping numbering remains 1–30 and `required_for_floor` marks the exact floor set listed below.

For clarity, the canonical **floor cases are 01–24**. Cases 25–30 are optional target extensions. Thus the first four acts each have five cases and Acts V–VI have two floor cases each before target extensions? That would distort the arc, so instead the canonical act distribution is frozen as **4/4/4/4/4/4 floor + one target extension per act = 5/5/5/5/5/5 at 30**. IDs follow act order: Act I = 01–05, Act II = 06–10, etc. In a 24-case release, each act's fifth case is cut: **05,10,15,20,25,30**. The retained floor is therefore 01–04, 06–09, 11–14, 16–19, 21–24, 26–29. This is the authoritative floor set.

## ACT I — READ THE TEAR
Goal: internalize direct cause, first-crossed semantics and same-checkpoint atomicity.

### SB_01 — One Crossing
- Family: F1
- Setup: 2 compartments, 1 fixed seal, 2 checkpoints, fixed history.
- Tags: `DIRECT_CAUSE`.
- Teaching: a seal tears when the opened compartment traverses one covered seam.
- Anti-repeat: sole pure direct-cause level.
- Floor: YES / Demo: YES.

### SB_02 — First One Wins
- Family: F1
- Setup: 3 compartments, one seal triggered by 2 compartments, fixed 3-step history.
- Tags: `FIRST_CROSSED`.
- Teaching: break time records the first qualifying opening only; later crossings do nothing.
- Anti-repeat: introduces multi-trigger witness, not more witnesses.
- Floor: YES / Demo: YES.

### SB_03 — Same Moment
- Family: F1
- Setup: 3 compartments, 3 fixed seals; one opening crosses seams covered by 2 seals.
- Tags: `DIRECT_CAUSE`, `FIRST_CROSSED`.
- Teaching: several seals can break at one checkpoint and animation order is meaningless.
- Anti-repeat: resolves atomicity misconception rather than adding logical density.
- Floor: YES.

### SB_04 — Which History?
- Family: F1->F2 bridge
- Setup: 3 compartments, 2 fixed overlapping seals, choose 1 of 3 authored histories.
- Tags: `FIRST_CROSSED`, `PAIRED_DISCRIMINATION`.
- Teaching: different histories can produce different tear timing from the same witnesses.
- Anti-repeat: first player history choice; no placement yet.
- Floor: YES.

### SB_05 — Early Audit (target extension)
- Family: F2
- Setup: 4 compartments, 3 fixed witnesses, 4 authored history choices.
- Tags: `FIRST_CROSSED`, `INTERSECTION_TRIANGULATION`, `PAIRED_DISCRIMINATION`.
- Teaching: solve by comparing two overlapping witnesses rather than checking each history in full.
- Anti-repeat: first real inverse elimination across witness intersections.
- Floor: NO.

## ACT II — COMPARE WITNESSES
Goal: prove causes by shared/divergent trigger structure.

### SB_06 — Shared Cause
- Family: F2
- Setup: 4 compartments, witnesses trigger {A,C} and {A,D}; fixed history.
- Tags: `PAIRED_DISCRIMINATION`.
- Teaching: differing break times rule out the shared cause at the earlier checkpoint.
- Anti-repeat: canonical paired-discrimination lesson.
- Floor: YES / Demo: YES.

### SB_07 — Narrow the Intersection
- Family: F2
- Setup: 4 compartments, three overlapping witnesses; choose authored history.
- Tags: `INTERSECTION_TRIANGULATION`, `PAIRED_DISCRIMINATION`.
- Teaching: the common trigger among witnesses can localize one opening.
- Anti-repeat: intersection, not divergence, is primary.
- Floor: YES.

### SB_08 — Equal Does Not Mean Same Cause
- Family: F2
- Setup: 4 compartments, two witnesses share one trigger but each has a distinct alternative; `SAME_BREAK_STEP` target.
- Tags: `INTERSECTION_TRIANGULATION`, `FIRST_CROSSED`.
- Teaching: same break step constrains but does not automatically prove the shared trigger; use a third witness to disambiguate.
- Anti-repeat: attacks false shortcut created by previous cases.
- Floor: YES.

### SB_09 — Before / After
- Family: F2
- Setup: 4 compartments, 4 fixed witnesses, one relative comparison plus `INTACT_THROUGH`.
- Tags: `PAIRED_DISCRIMINATION`, `DELAYED_BREAK_BOUND`.
- Teaching: relative evidence creates order bounds without revealing exact checkpoints.
- Anti-repeat: first non-exact temporal target.
- Floor: YES.

### SB_10 — Witness Net (target extension)
- Family: F2
- Setup: 5 compartments, 5 fixed witnesses with three overlapping motifs; select among 5 histories.
- Tags: `INTERSECTION_TRIANGULATION`, `PAIRED_DISCRIMINATION`, `DELAYED_BREAK_BOUND`.
- Teaching: combine equality, relative order and exact evidence.
- Anti-repeat: dense comparison capstone but no new rule.
- Floor: NO.

## ACT III — SURVIVE THE INSPECTION
Goal: complement reasoning from witnesses that do not tear.

### SB_11 — The One Left Closed
- Family: F3
- Setup: 4 compartments, open exactly 3; fixed seals include one single-trigger witness.
- Tags: `SURVIVORSHIP_COMPLEMENT`.
- Teaching: final intact witness can identify the unique omitted compartment.
- Anti-repeat: only pure omission tutorial.
- Floor: YES / Demo: YES.

### SB_12 — Too Much to Survive
- Family: F3
- Setup: 4 compartments, open exactly 3; one multi-trigger survivor candidate makes one history impossible.
- Tags: `SURVIVORSHIP_COMPLEMENT`, `INTERSECTION_TRIANGULATION`.
- Teaching: a surviving witness can prove impossibility when its trigger set is too large for the omission budget.
- Anti-repeat: contradiction deduction rather than direct omission identity.
- Floor: YES.

### SB_13 — Survive Until Three
- Family: F3
- Setup: 5 compartments, open exactly 4; evidence uses `INTACT_THROUGH(S,3)` then eventual break.
- Tags: `SURVIVORSHIP_COMPLEMENT`, `DELAYED_BREAK_BOUND`.
- Teaching: survival through a checkpoint imposes a lower bound on all relevant triggers, not merely final omission.
- Anti-repeat: converts survival into temporal bound.
- Floor: YES.

### SB_14 — Survivor Pair
- Family: F3/F2
- Setup: 5 compartments, open 4; two overlapping witnesses, one final-intact and one late-breaking.
- Tags: `SURVIVORSHIP_COMPLEMENT`, `PAIRED_DISCRIMINATION`, `DELAYED_BREAK_BOUND`.
- Teaching: combine complement with divergent witness evidence.
- Anti-repeat: first three-class case, but setup remains fixed to isolate reasoning.
- Floor: YES.

### SB_15 — Closed Branch (target extension)
- Family: F3
- Setup: 6 compartments, open exactly 5, 5 fixed witnesses with overlapping survivor candidates.
- Tags: `SURVIVORSHIP_COMPLEMENT`, `INTERSECTION_TRIANGULATION`, `DELAYED_BREAK_BOUND`.
- Teaching: omission is inferred indirectly from a network of survivors rather than a single obvious witness.
- Anti-repeat: target-only complexity extension; invalid if human review devolves into checking six omissions.
- Floor: NO.

## ACT IV — CHOOSE THE WITNESSES
Goal: inverse design — select seals that will create the required evidence under known history.

### SB_16 — Put the Seal Where It Matters
- Family: F4
- Setup: 4 compartments, fixed history, choose exactly 2 of 5 sockets.
- Tags: `INVERSE_WITNESS_PLACEMENT`, `DIRECT_CAUSE`.
- Teaching: choose witnesses by desired break time, not by final broken/intact state.
- Anti-repeat: first placement case; history fully fixed.
- Floor: YES.

### SB_17 — Two Ways to Break, One Way to Prove
- Family: F4
- Setup: 4 compartments, fixed history, choose 3 of 7 sockets; decoy sockets share final state but differ in break time.
- Tags: `INVERSE_WITNESS_PLACEMENT`, `PAIRED_DISCRIMINATION`.
- Teaching: final-state-equivalent sockets are distinguished by temporal signature.
- Anti-repeat: explicit anti-set-cover lesson.
- Floor: YES / Demo: YES.

### SB_18 — Build an Intersection
- Family: F4
- Setup: 5 compartments, fixed history, choose 3 of 8 sockets so target comparisons are satisfied.
- Tags: `INVERSE_WITNESS_PLACEMENT`, `INTERSECTION_TRIANGULATION`.
- Teaching: select witnesses whose overlaps create the required proof structure.
- Anti-repeat: player reasons about information geometry, not just selecting target break times independently.
- Floor: YES.

### SB_19 — One Must Survive
- Family: F4/F3
- Setup: 5 compartments, fixed 4-step history with known omission, choose 4 of 9 sockets.
- Tags: `INVERSE_WITNESS_PLACEMENT`, `SURVIVORSHIP_COMPLEMENT`, `PAIRED_DISCRIMINATION`.
- Teaching: deliberately place one witness outside the opened history while others discriminate the order.
- Anti-repeat: combines inverse placement with survivor design.
- Floor: YES.

### SB_20 — Evidence Designer (target extension)
- Family: F4
- Setup: 5 compartments, fixed history, choose 4 of 10 sockets; target contains exact, relative and survivor predicates.
- Tags: `INVERSE_WITNESS_PLACEMENT`, `INTERSECTION_TRIANGULATION`, `PAIRED_DISCRIMINATION`, `DELAYED_BREAK_BOUND`.
- Teaching: construct a compact evidence suite with no redundant witness.
- Anti-repeat: every selected socket must carry a different logical role; fails content gate if any is decorative.
- Floor: NO.

## ACT V — RECONSTRUCT THE OPENING
Goal: fixed witnesses, player solves the event history itself.

### SB_21 — Put the Openings in Order
- Family: F5
- Setup: 4 compartments, fixed seals, `ARRANGE_REQUIRED_SET`.
- Tags: `HISTORY_RECONSTRUCTION`, `FIRST_CROSSED`.
- Teaching: infer order from exact break checkpoints.
- Anti-repeat: first free permutation, intentionally straightforward.
- Floor: YES.

### SB_22 — Late Witness
- Family: F5
- Setup: 5 compartments, fixed seals, arrange all; evidence includes `BREAKS_AFTER` and exact paired break.
- Tags: `HISTORY_RECONSTRUCTION`, `DELAYED_BREAK_BOUND`, `PAIRED_DISCRIMINATION`.
- Teaching: lower bounds eliminate whole position ranges before exact ordering.
- Anti-repeat: expert representation is position bounds, not checking 120 permutations.
- Floor: YES.

### SB_23 — Reconstruct With One Missing
- Family: F5/F3
- Setup: 5 compartments, open exactly 4; fixed seals.
- Tags: `HISTORY_RECONSTRUCTION`, `SURVIVORSHIP_COMPLEMENT`, `INTERSECTION_TRIANGULATION`.
- Teaching: infer both omission and relative order.
- Anti-repeat: combines subset and ordering; no placement search yet.
- Floor: YES.

### SB_24 — Cross-Examination
- Family: F5
- Setup: 5 compartments, arrange all; 5 fixed overlapping witnesses; exact + relative + same-step predicates.
- Tags: `HISTORY_RECONSTRUCTION`, `INTERSECTION_TRIANGULATION`, `PAIRED_DISCRIMINATION`, `DELAYED_BREAK_BOUND`.
- Teaching: solve a full reconstruction from witness relationships without direct `OPENS_AT` clues.
- Anti-repeat: first full Act-II reasoning reprise under free history arrangement.
- Floor: YES.

### SB_25 — Reconstruction Audit (target extension)
- Family: F5
- Setup: 6 compartments, arrange 5 of 6, 6 fixed witnesses.
- Tags: `HISTORY_RECONSTRUCTION`, `SURVIVORSHIP_COMPLEMENT`, `DELAYED_BREAK_BOUND`, `PAIRED_DISCRIMINATION`.
- Teaching: capstone reconstruction with omission and bounds.
- Anti-repeat: admitted only if intended solution contains at least four deductive eliminations before residual ordering; otherwise cut.
- Floor: NO.

## ACT VI — BUILD AND RECONSTRUCT
Goal: coupled seal selection and history choice. No new vocabulary.

### SB_26 — Witness Changes the History
- Family: F6
- Setup: 4 compartments, choose 2 of 6 sockets + choose 1 of 4 authored histories.
- Tags: `PLACEMENT_HISTORY_COUPLING`, `INVERSE_WITNESS_PLACEMENT`, `PAIRED_DISCRIMINATION`.
- Teaching: a socket choice changes which histories can satisfy the evidence.
- Anti-repeat: starts coupling with finite history choices instead of permutation overload.
- Floor: YES.

### SB_27 — Build, Then Bound
- Family: F6
- Setup: 5 compartments, choose 3 of 8 sockets + arrange required set under one visible precedence lock.
- Tags: `PLACEMENT_HISTORY_COUPLING`, `INVERSE_WITNESS_PLACEMENT`, `DELAYED_BREAK_BOUND`, `HISTORY_RECONSTRUCTION`.
- Teaching: placement establishes which temporal bounds are even possible.
- Anti-repeat: emphasizes lower bounds rather than overlap identity.
- Floor: YES.

### SB_28 — Leave One Closed
- Family: F6/F3
- Setup: 5 compartments, choose 3 of 9 sockets + open 4 of 5.
- Tags: `PLACEMENT_HISTORY_COUPLING`, `SURVIVORSHIP_COMPLEMENT`, `INTERSECTION_TRIANGULATION`, `HISTORY_RECONSTRUCTION`.
- Teaching: omission and witness selection constrain each other.
- Anti-repeat: complement is the primary coupling mechanism.
- Floor: YES.

### SB_29 — Proof by Difference
- Family: F6
- Setup: 5 compartments, choose 4 of 10 sockets + arrange 4-step authored subset; paired divergent witnesses mandatory.
- Tags: `PLACEMENT_HISTORY_COUPLING`, `PAIRED_DISCRIMINATION`, `INTERSECTION_TRIANGULATION`, `DELAYED_BREAK_BOUND`.
- Teaching: choose witnesses that distinguish histories which would otherwise be evidence-equivalent.
- Anti-repeat: information-discrimination capstone rather than mere solve-all-variables density.
- Floor: YES / Demo: YES as demo capstone in reduced content build if difficulty tuning permits; otherwise demo uses a simplified sibling authored specifically from the same setup class.

### SB_30 — Seal Break (target final capstone)
- Family: F6
- Setup ceiling: 6 compartments, <=12 enabled sockets, choose <=5 seals, <=5 checkpoints; no Phase-4 ceiling increase.
- Tags: at least `PLACEMENT_HISTORY_COUPLING`, `INVERSE_WITNESS_PLACEMENT`, `HISTORY_RECONSTRUCTION` plus any two of intersection / discrimination / survivorship / delayed bound.
- Teaching: demonstrate mastery of the complete system with no new rule.
- Anti-repeat: final case must have a human-authored deduction graph with at least five meaningful deductions and at least three different logical roles among selected witnesses. If exhaustive certification produces uniqueness but human review cannot find that path, the case is invalid rather than “hard.”
- Floor: NO.

---

# 6. Demo mapping

The demo must use shipping campaign content, not disposable tutorial-only levels, unless one case requires minor presentation-only shortening.

Canonical six-case demo subset:
1. `SB_01` — direct cause;
2. `SB_02` — first-crossed semantics;
3. `SB_06` — divergent witnesses;
4. `SB_11` — survivor/omission;
5. `SB_17` — inverse witness placement;
6. `SB_29` — coupled capstone **only if playtest median first-solve remains demo-appropriate**.

If `SB_29` proves too difficult for a demo, the fallback is a mechanically identical-family reduced sibling derived from `SB_26`, but the shipping build must still count it as an authored campaign case or an explicit demo variant; no separate mechanic is allowed.

Demo progress carry policy at content level:
- solved shipping case IDs may carry into full game;
- per-case best/solved state may carry;
- campaign unlock state may be recomputed from solved case IDs;
- no commercial entitlement, achievement, cloud or pricing implementation is specified here — later phases own those systems.

---

# 7. Dependency / tutorial graph

Hard prerequisite graph by concepts, not merely numeric order:
- `SB_01 -> SB_02` (direct cause before first-crossed);
- `SB_02 -> SB_03, SB_04`;
- `SB_04 -> SB_06`;
- `SB_06 -> SB_07 -> SB_08 -> SB_09`;
- `SB_02 -> SB_11 -> SB_12 -> SB_13 -> SB_14`;
- `SB_09 -> SB_16` and `SB_11 -> SB_19`;
- `SB_16 -> SB_17 -> SB_18 -> SB_19`;
- `SB_09 -> SB_21`; `SB_21 -> SB_22 -> SB_23 -> SB_24`;
- `SB_17 + SB_21 -> SB_26`;
- `SB_22 + SB_26 -> SB_27`;
- `SB_23 + SB_26 -> SB_28`;
- `SB_24 + SB_27 + SB_28 -> SB_29`;
- target extensions may require their act's four floor cases; `SB_30` requires every floor case in Acts V–VI and at least one target extension from Acts II–V if the progression system later supports optional branches.

Phase 6/7 may choose linear or lightly branching presentation, but they may not violate these knowledge prerequisites.

---

# 8. Trigger-set motif library and reuse rules

To prevent solution memorization, content reuse is tracked at the logical motif level as well as art/layout.

Canonical trigger motifs:
- `M_SINGLE`: one-compartment trigger;
- `M_SHARED_CORE`: two witnesses share one trigger and diverge elsewhere;
- `M_CHAIN`: S1={A,B}, S2={B,C}, S3={C,D}-style overlap;
- `M_NESTED`: one trigger set is strict subset of another;
- `M_CROSS`: overlapping sets with neither subset relation;
- `M_SURVIVOR`: trigger set designed around omission/complement;
- `M_DECOY_FINAL_EQ`: sockets share final broken/intact outcome but differ temporally;
- `M_INFORMATION_PAIR`: two sockets are useful specifically because their divergence distinguishes histories.

Rules:
1. No logical trigger-set graph may be reused verbatim in adjacent cases under only relabeling.
2. A topology may recur after >=5 campaign positions only if placement/history mode or intended deduction graph materially changes.
3. Cabinet/seam art may be reused more freely, but sockets must not occupy identical visual locations with merely renamed compartment labels if that would allow memorized answers.
4. A reused geometry must permute or alter at least two of: active socket subset, trigger graph, placement mode, history mode, target relation, omission rule.
5. Demo cases must not teach a memorized answer that trivially solves a later full-game case using the same logical graph.
6. Purely cosmetic cabinet skins never count as new content.

---

# 9. Quantitative anti-repetition checks

Before Phase-5 content is considered production-ready, the final authored set must pass these checks.

## 9.1 Deduction distribution across 30-case target
Minimum appearances in substantive cases:
- `INTERSECTION_TRIANGULATION`: >=8;
- `PAIRED_DISCRIMINATION`: >=8;
- `SURVIVORSHIP_COMPLEMENT`: >=6;
- `DELAYED_BREAK_BOUND`: >=7;
- `INVERSE_WITNESS_PLACEMENT`: >=8;
- `HISTORY_RECONSTRUCTION`: >=8;
- `PLACEMENT_HISTORY_COUPLING`: all Act-VI cases, >=5 at 30 target / >=4 at 24 floor.

`DIRECT_CAUSE` and `FIRST_CROSSED` are foundations and are not required to be counted as advanced diversity.

## 9.2 Consecutive similarity ceiling
Compute `similarity_signature = (family, placement_mode, history_mode, primary_tags, omission_count, trigger_motif_multiset)`.

Rules:
- no two adjacent substantive cases may match on family + placement mode + history mode + primary tag set;
- no run of 3 may share the same primary deduction tag;
- target extensions are placed after their act and may be more similar to that act, but must still differ in at least two signature dimensions from case immediately before them.

## 9.3 Count ceilings
Campaign medians should remain comfortably below Phase-4 hard ceilings.
- floor median compartments <=5;
- floor median enabled sockets <=9;
- floor median installed/selected seals <=4;
- no more than 4 cases in target may use 6+ compartments;
- no more than 5 cases may expose 10+ enabled sockets;
- no shipping case may require >6 checkpoints.

Count escalation cannot be used to satisfy diversity metrics.

## 9.4 Predicate density
- Intro: <=2 substantive evidence predicates after tutorial explanation.
- Early: usually 2–4.
- Mid: usually 3–5.
- Late: usually 4–6.
- >6 evidence predicates requires a written reason and redundancy check.

A case with many logically redundant predicates fails even if readable.

## 9.5 Trigger-motif repetition
- same normalized trigger graph cannot recur within 5 case positions;
- `M_CHAIN` or `M_SHARED_CORE` may not dominate >35% of cases;
- every Act III–VI case must combine at least two motif roles or explain why a single motif creates the intended deduction.

---

# 10. Authored-case production workflow

Every case must pass this exact pipeline:

1. **Intent draft** — author writes teaching intent and intended deduction graph before geometry.
2. **Logical skeleton** — define compartments and desired trigger-set relations abstractly.
3. **Geometry realization** — map trigger relations to seams + legal sockets under observable-geometry rule.
4. **Schema validation** — IDs, seams, bounds, placement/history legality, dead sockets, impossible fixed constraints.
5. **Submission-space estimate** — reject accidental combinatorial blow-up even if certifier could technically handle it.
6. **Exhaustive certification** — enumerate all legal submissions, authoritative resolve, classify solutions/equivalence.
7. **Zero/ambiguity repair** — zero-solution and accidental multi-valid cases are repaired, never shipped accidentally.
8. **Deduction-tag audit** — reviewer verifies intended tags are actually needed, not labels pasted onto a brute-force puzzle.
9. **Oracle-free human-solvability review** — solve using only legal static preview; reviewer records a meaningful deduction path.
10. **Redundant-evidence review** — remove predicates whose absence does not change solution class or teaching need.
11. **Anti-repetition scan** — compare similarity signature and trigger graph against surrounding campaign.
12. **Campaign placement** — only then assign/finalize campaign slot.
13. **Presentation pass later** — Phase 6 may improve framing/feedback but cannot alter mechanical certification silently.

A certifier PASS without human deduction PASS is insufficient.

---

# 11. Optional cases 31–36 / expansion boundary

Cases 31–36 are **NON-REQUIRED** and are not part of the current commercial promise.

They may be admitted only if all are true:
1. the 30-case target already passes anti-repetition review;
2. the proposed case demonstrates a deduction combination not already represented by a neighboring target case;
3. no new predicate, history mode, seal property or mechanic is required;
4. the case stays within Phase-4 ceilings;
5. exhaustive certification and oracle-free human review both pass;
6. it is not merely a harder version produced by +1 compartment/+2 sockets/more predicates;
7. adding it does not delay core UX, QA or release readiness.

Preferred use if such cases exist:
- optional expert appendix;
- post-campaign challenge page;
- not a seventh act with new rules.

If fewer than six legitimate cases exist, ship fewer. Zero is acceptable.

---

# 12. Floor stress test

The 24-case floor survives because removing target extensions `05,10,15,20,25,30` leaves:
- four introductory/direct cases;
- four witness-comparison cases;
- four omission/survivorship cases;
- four inverse-placement cases;
- four reconstruction cases;
- four coupled late-game cases.

This preserves every essential setup family and deduction class. Nothing essential is introduced only in a target extension.

Floor late-game cases `26–29` already combine >=3 advanced deduction classes; therefore case 30 is a mastery celebration, not a missing final mechanic.

No phase-5 justification depends on procedural generation, random puzzles, new seal types, hidden narrative facts or live solver hints.

---

# 13. Phase-5 freeze decisions

Frozen now:
- complete semantic case schema and reasoning metadata;
- six canonical setup/content families;
- predicate/history/placement introduction order;
- six-act campaign architecture;
- concrete 24-case floor and 30-case target map;
- exact target-extension cut set `{05,10,15,20,25,30}` for a coherent 24-case fallback;
- six-case demo mapping with one difficulty-gated capstone fallback;
- prerequisite graph;
- trigger-motif taxonomy and geometry reuse restrictions;
- quantitative anti-repetition thresholds;
- authored-content production/certification workflow;
- optional 31–36 admission gates;
- proof that 24 cases do not require padding.

Not frozen here:
- final titles/flavor copy for individual cases;
- exact cabinet art/layout;
- case-select UI/progression presentation;
- star/score/achievement systems;
- pricing or commercial entitlement;
- exact implementation data serialization;
- final playtest difficulty numbers.

## Phase 5 verdict
**PASS — CONTENT ARCHITECTURE COMPLETE.**

The content plan demonstrates enough same-vocabulary diversity for a 24-case commercial floor and 30-case target. The next risk is whether the information architecture can make seams, trigger relations, evidence, ordering and commit/replay legible on desktop and handheld without becoming a solver oracle.

## NEXT PHASE
**Phase 6 — UX / Presentation Architecture.** Define controller/keyboard/mouse interaction, cabinet focus/navigation, seal placement affordances, history arrangement, evidence-card language, non-oracular inspect/highlight behavior, commit/replay/scrub/return-to-edit flow, onboarding, first-session sequence, HUD/menu/case-select, accessibility, visual identity, audio/tear feedback, handheld readability, failure/mismatch explanation and pause/settings boundaries. Preserve the Phase-4 oracle prohibition and Phase-5 dependency structure.