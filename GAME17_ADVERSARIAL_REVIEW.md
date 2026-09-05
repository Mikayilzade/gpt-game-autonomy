# GAME #017 — THE QUEUE KNOWS — PHASE 10 ADVERSARIAL REVIEW

Date: 2026-09-06
Status: PHASE 10 COMPLETE
Production implementation: NO
Authority: active Game #017 authority through GAME17_WHOLE_GAME_SIMULATION.md.

This review attacks the design as if trying to disprove that it should proceed to specification freeze. It records failure modes, severity, repairs, rejection rules, and empirical gates. It does not add production code.

## 1. Executive verdict

**The design survives Phase 10, but only with tighter anti-trivialization and content-certification rules.**

The central danger is not mechanical unsoundness. The dangerous collapse is: open Type Lens -> cycle candidate rows / draft presets -> pick a state where rows differ -> Resolve.

If that loop becomes dominant, the game remains correct but becomes shallow and spreadsheet-like. The fix is not to hide deterministic information. The fix is to require content where the meaningful decision concerns causal consequence, contingent future value, operational cost, or which ambiguity matters.

No unresolved design blocker remains after the repairs below. QK04/QK06 exact certified data remain implementation-data gates and must survive into Phase 11 handoff.

## 2. Fun / Type Lens trivialization attack

### Failure hypothesis
Because every candidate rule is public and Type Lens can evaluate each candidate against a draft state, the player could brute-scan allowed presets until a visible matrix differs. This is especially dangerous in two-counter/two-type cases, one-intervention cases with only a few values, singleton IDENTIFY objectives, and cases without congestion or future consequence.

### Why hiding Type Lens is rejected
Removing or obscuring candidate comparisons would increase bookkeeping, memorization burden, and unfairness. Fairness stays. Content must carry the depth.

### Canonical repair — Diagnostic Depth Gate
For every non-tutorial campaign case QK07+ at least one must be true:
1. More than one draft state creates immediate candidate divergence, but only some preserve the final objective.
2. The best immediate split creates a later congestion/service problem, so information value and consequence conflict.
3. The useful intervention depends on which ambiguity/objective matters; maximum row divergence is not sufficient.
4. A contingent second-stage policy matters: first-stage value depends on future observation branches.
5. The objective allows pooling/EXCLUDE/service proof, so making every row unique is unnecessary or wasteful.
6. A public cardinality constraint changes which distinctions matter.

If none applies, the case is tutorial-grade and cannot occupy late campaign space.

### Canonical repair — Scan Resistance Metric
Validator/content tooling must report:
- count of legal draft states;
- count producing any candidate divergence;
- count satisfying eventual objective under at least one policy;
- whether choosing the draft with maximum immediate partition count is always sufficient.

Reject QK07+ if maximum immediate partition is a universally winning greedy rule, or if one draft is uniquely informative and uniquely successful with no meaningful tradeoff, unless the case is explicitly a short chapter refresher.

Manual review question for every case: Why is choosing the most visibly separating current draft not enough? If there is no good answer after Chapter 1, cut/rework the case.

## 3. Cross-case dominant strategies

Attacked policies: always make one counter FREE; always slow the familiar counter by Routine threshold; always minimize predicted completion first; always spend all interventions before first Resolve; always isolate Privacy at the highest-privacy counter; always maximize candidate-row divergence; always identify everybody before Commit.

Portfolio-level repairs:
1. No lever family may be the decisive action in >35% of campaign cases.
2. No exact intervention-template sequence may be the decisive route in more than 2 adjacent cases.
3. At least 12 of 36 campaign cases must punish greedy immediate-information choice through later consequence, budget loss, or irrelevant information.
4. At least 8 campaign cases must succeed with some customers intentionally unresolved.
5. At least 6 campaign cases must have materially distinct certified policy classes.
6. At least 6 campaign cases must require different second-stage actions in different observation branches.
7. At least 4 campaign cases must make the highest-throughput setup fail the information objective.

A policy is materially distinct when it differs in intervention family, timing, or branch logic, not merely equivalent counter labels.

## 4. 36+12 content exhaustion attack

Five heuristics, three counters and four lever families may not sustain 48 strong authored cases. The target remains plausible only if chapter novelty is defined by causal structure, not vocabulary.

Before release-candidate content lock, score every campaign case on primary reasoning family, decisive heuristic pair, objective family, lever family, cohort structure, and proof motif; cluster near-duplicates; cut/rewrite cases that differ only numerically; prefer 30–36 excellent campaign cases over 36 padded ones; preserve all six chapter identities and all mandatory foundation cases.

Repetition kill conditions: external players describe 3+ consecutive cases as same thing with more people; player solves mainly by scanning Type Lens rather than predicting consequences; Chapter 3 onward still feels one-step; Chapter 5/6 difficulty is mainly more customers/candidates; mastery feels like tighter arithmetic instead of new proof structure.

The commercial MSRP can move inside the already-approved band if quality cuts reduce measured length. Do not pad to protect price.

## 5. QK04 / QK06 contingent-policy feasibility attack

QK04 must have at least two allowed cohort-1 observation branches, different residual public states, different second interventions required or materially preferable for guaranteed success, and no blind fixed second action that succeeds across all worlds.

QK06 must preserve 8 customers, 3 counters, 2 cohorts, budget 2, information goal plus wait <=4, at least two observation partitions requiring different safe second actions, and no blind two-step script succeeding across all worlds unless data simplification is required while preserving the same learning beat.

These are mandatory certification gates before vertical-slice/demo acceptance. If bounded solver search cannot produce satisfying data, first change candidate sets, arrival order, thresholds, public world constraints or preset values; then simplify customer/world complexity while preserving the learning beat; only after repeated bounded failure may design reopen. Do not silently weaken contingent policy into two-stage but same answer.

## 6. Scope / asset / authoring burden attack

Risks: 48 certified cases may be designer-time heavy; hints/explanations may duplicate solver work; animation polish may grow; visual themes may expand art scope; localization of exact logic can be costly.

Repairs: one primary hall environment family is sufficient; chapter variation uses lighting/signage/props rather than new simulation spaces; customer cosmetics stay independent from logic; no bespoke per-case animation; reason traces are generated from evaluator facts; hints are premise-level, not branching dialogue; launch does not require voice acting.

If average certified-case authoring becomes unsustainable, cut toward the 30-case floor before adding tooling complexity or one-off mechanics.

## 7. Solver/world-space/performance attack

Heavy certification is an authoring/build-time concern, not a per-frame runtime obligation.

Canonical constraints:
- runtime evaluator stays O(customers * counters) scale;
- Type Lens evaluates only selected visible candidate models from current/draft public state;
- runtime dead-state detection may be omitted unless a cheap precomputed certificate/state lookup exists;
- authored-case certification may use offline exhaustive/search tooling;
- if a dead state cannot be proven cheaply at runtime, UI stays silent rather than guessing.

Certification tooling may memoize canonical public states, merge equivalent candidate-world partitions, precompute evaluator outcomes, and use exact symbolic partition compression. It may not approximate correctness or prune by designer intuition. If one case needs disproportionate solver infrastructure, simplify the case.

## 8. Hidden-truth leakage / oracle attack

Strengthened anti-leak rules:
1. Commit enablement depends only on public proof requirements and submission completeness, never secret correctness.
2. Candidate chips reorder only by stable public order, never actual type.
3. Customer visual/audio variants may not correlate with hidden heuristic.
4. Evidence animation intensity may not differ based on actual type except through public consequence.
5. Achievement triggers cannot reveal hidden truth before terminal proof.
6. Debug/QA truth overlays exist only behind explicit developer flags unavailable in release UI.
7. Save files may contain hidden world internally but normal UI/log/export must not expose it.
8. Hint selection must be authored from public state/objective or pre-authored tier, not dynamically selected from actual hidden type.

Existing Phase-6 anti-oracle rules remain authoritative and are strengthened by these points.

## 9. Controller / 1280x800 late-case ambiguity attack

The 10-customer ceiling remains a stress maximum, not target density.

Late-case acceptance: future cohorts stay in trays until admitted; hall overview never requires all candidate chips visible simultaneously; selected customer links visibly to queue slot and evidence history; evidence timeline is indexed; at 130% text scale drawers may scroll; no logical text is shrunk; controller focus transition from hall object to relevant detail panel stays within two actions.

Kill condition: if a late case cannot be understood on 1280x800 without repeatedly opening 5+ individual customers to reconstruct one basic comparison, simplify population composition.

## 10. Accessibility contradictions attack

No core logical distinction may depend on color, animation speed, audio, precise pointing, timed reaction, small text, or holding a button. Reduced Motion / Instant animation must produce identical evidence and event ordering. Challenge/mastery may not require accessibility features disabled. No achievement may require default text scale, animation, audio, or a specific input method.

No unresolved accessibility contradiction remains.

## 11. Checkpoint / save / cloud / demo-import corruption attack

Canonical locks:
- checkpoint reload restores full authoritative branch including candidate/evidence state;
- user memory after rewind is acceptable in a single-player puzzle;
- no automatic merge of current-session states;
- completed-case union only under compatible schema/version;
- demo import is idempotent and imports completion/settings, not arbitrary in-progress state;
- save migration writes new structure only after validation;
- previous-good backup is retained until migrated save validates;
- replay is read-only event presentation;
- changed case data invalidates an in-progress attempt rather than semantically remapping old evidence.

## 12. Objective / world-quantifier ambiguity attack

Every objective record must explicitly contain objective predicate, evaluation boundary, world quantifier, commit requirement, and whether singleton diagnosis is required.

Allowed quantifiers:
- ACTUAL_WORLD: only for post-commit truth checks where luck cannot bypass required public proof;
- ALL_REMAINING_WORLDS: default for operational guarantees;
- ALL_ALLOWED_WORLDS_FROM_START: used for certification of a strategy/policy, not necessarily runtime success predicate.

Runtime UI translates these as Guaranteed in every remaining possibility, Identify, Prove not X, or Separate target group rather than solver jargon.

If an objective conceptually requires proof, actual-world correctness alone is insufficient; the public evidence/proof predicate must also pass.

## 13. Cross-file implementation ambiguity attack

Phase-11 precedence must consolidate these rules:
1. later phase files override earlier descriptive/tournament wording for the same mechanic;
2. GAME17_MECHANICS.md owns formulas/order;
3. GAME17_CONTENT.md owns case architecture/content boundaries;
4. GAME17_UX_PRESENTATION.md owns reveal/navigation/presentation;
5. GAME17_COMMERCIAL.md owns price/demo/platform commercial choices;
6. GAME17_TECHNICAL_SPEC.md owns implementation architecture/persistence/testing;
7. GAME17_WHOLE_GAME_SIMULATION.md owns repaired cross-file interpretations recorded there;
8. this adversarial review owns new rejection/empirical gates;
9. Phase 11 must produce the final consolidated authority.

Known repaired ambiguity remains locked: older actual-type reason-trace wording is non-canonical before proof; QK01–QK06 all required before Chapter 2; Chapters 2–5 may use 4-of-6 advancement subject to prerequisites; all 36 are required for campaign completion unless final implementation cuts content and the acceptance package is updated accordingly.

## 14. Commercial / demo failure attack

Demo risks and repairs:
- demo reveals whole trick: later chapters must visibly escalate consequence, partial proof, contingency and three-counter synthesis;
- demo too hard: QK04/QK06 must not require manual world enumeration; simplify data while preserving beats;
- reads as queue management: no throughput score, profit, staff, satisfaction stars or management progression;
- $12.99 value mismatch: measure completion length/repetition and adjust inside approved band rather than padding;
- visual blandness: at least one store/trailer shot must show a public-rule change, visible queue split, and candidate elimination.

## 15. Empirical gates that MUST survive into implementation

Core fun/comprehension:
1. By QK02, most first-time testers describe the goal as learning/deduction rather than speed/management.
2. QK07+ play does not reduce primarily to scanning Type Lens drafts for first row divergence.
3. External players do not report material repetition before Chapter 5.
4. At least one late case produces a remembered intentionally-made-the-system-worse-to-learn moment.

Content/data:
5. QK04 certified instance proves branch-dependent second intervention.
6. QK06 certified instance proves branch-dependent second intervention plus wait <=4.
7. Every shipped case passes solver certification and human-solvability proof.
8. 36-case target may be cut toward floor if repetition gates fail.

UX/accessibility:
9. Controller-only demo completes without pointer emulation.
10. 1280x800 + 130% text late stress case remains navigable.
11. QK03 evidence snapshot is correctly interpreted by external testers.
12. No hidden type is inferred from reason trace/presentation before proof.
13. Normal/Fast/Instant/Reduced Motion produce identical logical results.

Technical/persistence:
14. Determinism golden traces match across supported platforms/builds.
15. Save/resume during/after Resolve preserves exact authoritative state.
16. Cloud conflict never silently merges incompatible current attempts.
17. Demo import is idempotent and non-destructive.

Commercial:
18. 10–20 sec hook clip is understood as change setup to learn from choices.
19. Demo completion/drop-off is measured before release decisions.
20. Price is rechecked against current market and measured content length near launch.

## 16. Severity ledger

Critical — repaired by gate: Type Lens scan-row trivialization; hidden-truth leakage through UI/Commit/reason traces; QK04/QK06 being treated as close-enough illustrative data.

High — managed: content repetition before 36 cases; greedy immediate-information dominant strategy; handheld information density; demo mistaken for queue management; solver blow-up from overlarge case data.

Medium — bounded: art/case authoring scope; save/cloud/demo-import edge cases; localization precision; $12.99 value perception.

No unresolved critical/high design blocker remains.

## 17. Phase-10 acceptance

The design advances because deterministic fairness is preserved; anti-oracle rules remain strong; scan-row trivialization is now an explicit validator/content rejection target; dominant strategies have portfolio-level caps; repetition can reduce case count rather than force filler; QK04/QK06 contingent-policy obligations are preserved; solver/runtime responsibilities are separated; handheld/accessibility limits are bounded; persistence/import paths have safe behavior; objective quantifiers are clarified; and all required empirical gates are enumerated.

**PHASE 10 ADVERSARIAL REVIEW = COMPLETE.**

No production implementation has begun.

# NEXT DESIGN STEP — PHASE 11 SPECIFICATION FREEZE

Phase 11 must:
1. produce one final authority/precedence order;
2. consolidate all repaired rules from Phase 9 and Phase 10;
3. list implementation-flexible presentation/art choices separately from frozen mechanics;
4. list every empirical/data gate intentionally deferred;
5. produce implementation acceptance criteria for 12A–12H;
6. confirm QK04/QK06 obligations without weakening them;
7. confirm 36+12 target with quality cut allowed to documented floor if repetition requires it;
8. create final freeze file;
9. set DESIGN COMPLETE = YES only if a fresh implementation session can build without inventing gameplay;
10. then attempt migration to a dedicated repository; if unavailable, preserve Game #017 as NON-ACTIVE frozen safety archive, update GAME_INDEX, and immediately advance STATUS to Game #018.