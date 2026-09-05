# GAME #017 — THE QUEUE KNOWS — FINAL SPECIFICATION FREEZE

Date: 2026-09-06
Status: **DESIGN COMPLETE = YES**
Production implementation in factory: NO

This file is the final consolidated authority for Game #017. A fresh implementation session should be able to build the game without inventing important gameplay. Where earlier files conflict, use the precedence below.

## 1. Final authority / precedence

Highest to lowest for game-specific questions:
1. `GAME17_FINAL_FREEZE.md` — final consolidation, repaired interpretations, acceptance gates.
2. `GAME17_ADVERSARIAL_REVIEW.md` — anti-trivialization, rejection and empirical gates.
3. `GAME17_WHOLE_GAME_SIMULATION.md` — repaired lifecycle/progression/evidence interpretations.
4. `GAME17_TECHNICAL_SPEC.md` — architecture, data, persistence, validation and test contracts.
5. `GAME17_COMMERCIAL.md` — price/demo/platform/commercial boundaries.
6. `GAME17_UX_PRESENTATION.md` — player-facing reveal, navigation, evidence and accessibility.
7. `GAME17_CONTENT.md` — campaign structure, case families, authoring and validation boundaries.
8. `GAME17_MECHANICS.md` — exact evaluator formulas, tick order, state transitions and objective grammar.
9. `GAME17_PRODUCT_THESIS.md` — product identity and scope ceiling.
10. Round C/B/tournament/research — historical rationale only; later files override descriptive wording.

Factory-level `START_HERE.md`, live `STATUS.md`, and `GAME_INDEX.md` govern factory continuity, not shipped gameplay.

## 2. Frozen product identity

Working title: **THE QUEUE KNOWS**.
Genre: single-player deterministic deduction / mechanism-design puzzle.
Platform: PC / Steam first, mouse + controller, Steam Deck/1280x800 first-class.
Store hook: change signs and counter rules in a tiny service hall, watch customers choose queues, and use those choices to deduce what they need — even when the best experiment makes the line worse on purpose.

The player is not a queue manager. The core fantasy is designing a public system so voluntary deterministic choices become evidence.

Canonical loop: **inspect -> predict counterfactually -> intervene -> resolve -> observe evidence -> infer -> repeat -> commit**.

No production implementation may add a throughput-management metagame, economy, staff roster, randomized customer AI, real-time reaction, free pathfinding, dialogue interrogation, roguelite/deckbuilding layer, or sixth heuristic without an explicit design reopen.

## 3. Frozen mechanical language

Exactly five base heuristic families:
- PRICE: lowest visible fee, then exact Phase-4 tie-breaks.
- URGENT: shortest predicted completion, fee ignored as preference.
- ROUTINE: familiar counter unless completion disadvantage exceeds visible threshold; equality stays familiar.
- PRIVACY: avoid public exposure when feasible.
- CONVENIENCE: lowest walk cost, then completion/fee/stable tie-breaks.

Exact comparator ordering, predicted-completion formula, capacity-2 scheduling, cohort arrival ordering, service tick ordering, fixed-slot movement, intervention legality, evidence elimination, checkpoint semantics, and objective predicates are frozen by `GAME17_MECHANICS.md` unless explicitly repaired later in this file.

Customers do not spontaneously re-queue. Animation never determines logic. Same authoritative state + hidden world + legal action must produce the same result.

## 4. Frozen information / fairness contract

Every actual type belongs to a visible candidate set. All decision-relevant state is public at the appropriate time. Deduction is exact, never probabilistic.

Before proof, UI may show public facts, candidate sets, candidate-specific counterfactual evaluation, and contradiction-based eliminations. It may not reveal actual hidden type, probability/confidence, actual-world future choice, actual-type-specific reason wording, or truth-correlated art/audio/order.

Type Lens remains available because hiding public deterministic reasoning would create bookkeeping rather than depth. It is strictly counterfactual: `IF THIS CUSTOMER WERE X...`.

Evidence belongs to immutable pre-choice state. Final queue position is not evidence by itself. Reason traces explain contradictions/public facts; they do not explain the hidden actual type before proof.

Commit enablement cannot depend on secret correctness.

## 5. Frozen scope ceilings

Base campaign:
- 2–3 counters, hard max 3;
- max 10 individually relevant visible customers;
- 1–3 cohorts normal, hard max 4;
- 1–3 interventions normal, hard max 4;
- exactly five heuristics;
- candidate sets normally 2–4, all five only rare mastery;
- max 2 public global cardinality constraints;
- integer fee/service/walk/privacy/threshold scales only;
- fixed slots, no physics/pathfinding truth.

These ceilings are not targets. Late content should use fewer elements when readability or human-solvability improves.

## 6. Frozen content architecture

Target: **36 campaign cases + 12 optional mastery cases**.
Quality floor after empirical cuts: **30 campaign-equivalent cases + at least 8 mastery cases**, while preserving six chapter identities, QK01–QK06, required reasoning families, and campaign coherence. Quality cuts are preferred to filler.

Chapters:
1. READ THE LINE — self-selection and evidence basics.
2. TEST, DON'T GUESS — active diagnostic state selection.
3. THE CROWD IS PART OF THE TEST — congestion-mediated evidence.
4. ENOUGH TO ACT — partial proof, pooling, all-remaining-world guarantees.
5. DESIGN THE HALL — three-counter/tight-budget/contingent mechanism design.
6. THE QUEUE KNOWS — synthesis without new rules.

Progression repair is final:
- QK01–QK06 are all mandatory before Chapter 2.
- Chapters 2–5 may use 4-of-6 next-chapter flexibility only when named foundation prerequisites are satisfied.
- all retained campaign cases are required for final campaign completion.
- mastery never gates campaign.

No shipped case may be a numerical reskin or rely on an authored correct-action script as runtime truth.

## 7. Diagnostic Depth / anti-trivialization freeze

For every non-tutorial QK07+ case, at least one must hold:
1. multiple immediate-divergence drafts exist but only some preserve final success;
2. strongest immediate split creates later congestion/service cost;
3. relevant ambiguity matters more than maximum total split;
4. contingent future action changes first-stage value;
5. pooling/EXCLUDE/service proof makes full separation wasteful;
6. a public cardinality constraint changes which distinctions matter.

Validator must report legal draft count, divergent draft count, eventual-success draft count, and whether maximum immediate partition is a universally winning greedy rule.

Reject QK07+ when `scan Type Lens -> choose maximum current divergence` is universally sufficient, except an explicitly short refresher.

Portfolio-level content requirements:
- no lever family decisive in >35% of campaign;
- at least 12/36 cases punish greedy immediate-information choice through consequence/budget/irrelevance, scaled proportionally if campaign is cut;
- at least 8/36 succeed with intentional unresolved customers;
- at least 6/36 have materially distinct certified policy classes;
- at least 6/36 require branch-dependent second-stage actions;
- at least 4/36 make highest-throughput setup fail information objective.

If final campaign is below 36, preserve these ratios approximately and never reduce branch-dependent cases below 5 or intentional-pooling cases below 6.

## 8. QK04 / QK06 non-negotiable data gates

QK04 exact authored data must prove:
- at least two allowed cohort-1 observation branches;
- different residual public states;
- different second interventions required or materially preferable for guaranteed success;
- no blind fixed second action succeeds across all allowed worlds.

QK06 exact authored data must prove:
- 8 customers, 3 counters, 2 cohorts, budget 2 unless simplification is necessary for human readability;
- information goal + wait <=4 ticks;
- at least two cohort-1 observation partitions requiring different safe second actions;
- no blind two-step script succeeds across all worlds.

If solver search cannot produce valid data, first change candidate sets, arrival order, thresholds, public world constraints or preset values. Then simplify data while preserving the same contingent-learning beat. Do not silently weaken contingency.

## 9. Objectives / world quantifiers

Every objective specifies predicate, evaluation boundary, world quantifier, commit requirement, and whether singleton diagnosis is required.

Allowed quantifiers:
- ACTUAL_WORLD only for post-commit truth checks where luck cannot bypass required public proof;
- ALL_REMAINING_WORLDS as default operational guarantee;
- ALL_ALLOWED_WORLDS_FROM_START for strategy/certification obligations.

Player UI uses plain language (`Guaranteed in every remaining possibility`, `Identify`, `Prove not X`, `Separate target group`) rather than solver jargon.

Actual-world correctness alone cannot satisfy a proof objective if public evidence requirement is not met.

## 10. UX / presentation freeze

Canonical view: fixed elevated three-quarter/shallow-isometric hall, no free rotation, fixed queue slots, strong A/B/C counter landmarks.

1280x800 is first-class. Required logical text targets ~12px apparent character height minimum at base scale, with 100/115/130% text presets. Layout scrolls/paginates instead of shrinking required text.

Core information hierarchy: objective/constraints/budget/cohort always visible; hall state readable; inspector shows one focused customer/counter/evidence; evidence history is indexed and immutable.

Controller is fully sufficient. No drag, hover, physical keyboard, touch, pointer precision, audio cue, color-only cue, timed reaction, or held input is required.

Normal/Fast/Instant/Reduced Motion change presentation only and must yield identical logical event traces.

At 10-customer late density, if a basic comparison requires repeatedly opening 5+ individual customers, content must be simplified rather than UI made denser.

## 11. Commercial freeze

Planning MSRP: **$12.99 USD**.
Pre-release empirical adjustment band: $11.99–$14.99.
Launch discount baseline: 10% for 7–14 days, with 15% only as evidence-driven alternative.

Premium single purchase. No ads, microtransactions, paid hints, consumable currency, battle pass, daily chores, live-service dependency or day-one carved puzzle pack.

Free Steam demo: QK01–QK06, target 25–35 minutes. Desired full-game carryover is completion/settings only through safe idempotent import; carryover is never required to play.

Target campaign time 6–8h and completionist 9–13h are empirical planning targets, not filler mandates or store promises before measurement.

## 12. Technical freeze

Recommended engine: Godot 4.7.x stable, GDScript baseline; C# acceptable while preserving contracts. Engine change is implementation-flexible only if all deterministic/test/persistence contracts survive.

SimulationCore is authoritative and headless-testable. Presentation, animation, camera and platform services cannot mutate game truth directly.

CaseDefinition, CaseState, evidence, save, checkpoint and validation data are versioned. Evidence stores structured reason codes/arguments, not localized final prose.

Hidden actual world remains private to simulation/session. Player-facing APIs never receive raw actual type before allowed reveal.

Offline validator partitions hidden worlds by deterministic public observation and proves contingent policies. Release packaging must include only certified campaign/mastery case data.

Runtime dead-state messaging requires exact certificate/proof; otherwise remain silent.

Saves use atomic write/validate/replace and previous-good backup. Current attempts never silently merge across Cloud conflicts. Demo import is idempotent and non-destructive. Changed incompatible case data restarts current attempt rather than remapping old evidence semantically.

## 13. Implementation-flexible choices

Implementation may choose without design reopen:
- exact 2D vs light 2.5D art technique;
- character/counter cosmetic style, animation style and non-logical props;
- soundtrack, ambience and non-semantic audio;
- exact tween duration inside UX bounds;
- desktop-wide panel pinning while handheld hierarchy remains valid;
- exact localization technology;
- Godot GDScript vs C#;
- exact internal container/data structures and solver optimization techniques that preserve exact results;
- exact Steam integration library;
- exact save file encoding/compression;
- exact menu transitions and cosmetic chapter themes;
- final achievement names/text inside frozen achievement philosophy;
- final price within $11.99–$14.99 after empirical review.

Implementation may not reinterpret these flexible choices to change mechanic truth, information availability, difficulty by hiddenness, or scope boundaries.

## 14. Empirical/data gates intentionally deferred

These are implementation/playtest obligations, not missing design:
1. By QK02, representative first-time players understand deduction/information over throughput.
2. QK07+ does not collapse primarily into Type Lens row scanning.
3. External players do not report material repetition before Chapter 5.
4. At least one late case creates a memorable deliberate-worse-system-for-information moment.
5. QK04 exact data passes branch-dependent certification.
6. QK06 exact data passes branch-dependent + wait<=4 certification.
7. Every shipped case passes solver certification and plain-language human proof.
8. Final case count may be cut toward floor if repetition fails.
9. Controller-only demo is completable without pointer emulation.
10. 1280x800 + 130% text late stress case is navigable.
11. External testers correctly understand QK03 historical evidence snapshot.
12. No tester can infer hidden type from reason-trace/presentation leakage before proof.
13. Normal/Fast/Instant/Reduced Motion have identical logical traces.
14. Determinism golden traces match supported OS/build targets.
15. Save/resume around Resolve preserves exact authoritative state.
16. Cloud conflicts never silently merge incompatible attempts.
17. Demo import is idempotent/non-destructive.
18. 10–20 second hook clip is understood as changing setup to learn from choices.
19. Demo completion/drop-off is measured before release decisions.
20. Price is rechecked near launch against current market and measured content length.
21. Fixed-slot movement feels sufficiently alive without pathfinding.
22. Five heuristics sustain final content without sixth heuristic.

A failed empirical gate triggers the smallest compatible repair first: content data -> UX framing -> presentation -> case count/price within allowed bounds. Adding a new mechanic/heuristic or management layer requires design reopen.

## 15. Implementation acceptance criteria — 12A to 12H

### 12A — Technical bootstrap
Complete when:
- runnable Godot project on target desktop;
- SimulationCore exists independently of scenes;
- versioned CaseDefinition/CaseState/evidence/save skeleton parses and validates;
- five evaluator unit contracts and canonical tie-breaks have tests;
- deterministic cohort/service event ordering has golden trace;
- hidden-world player-facing API boundary test exists;
- atomic save + previous-good backup skeleton works;
- CI runs headless tests without notification spam.

### 12B — Vertical slice
Complete when:
- QK01–QK03 playable end-to-end with real authoritative evidence;
- one intervention -> Resolve -> evidence -> Commit loop is complete;
- Type Lens is counterfactual and passes no-oracle tests;
- mouse + controller paths work;
- checkpoint/restart/replay/fast-forward operate without state divergence;
- no management score/economy appears.

Do not call demo complete at 12B.

### 12C — Core systems complete
Complete when:
- all five heuristics and all four intervention families work;
- 3 counters, capacity2, up to 4 cohorts/interventions supported;
- IDENTIFY/EXCLUDE/SEPARATE/POOL_ALLOWED/SERVICE/HYBRID + quantifiers implemented;
- exact evidence/history/inference/dead-state-certificate interfaces work;
- all persistence/checkpoint/cloud conflict core logic exists;
- solver/validator can certify contingent policies.

### 12D — Content population
Complete when:
- QK01–QK36 target plus MQK01–MQK12 target authored or documented quality-cut set at/above floor;
- every retained case has certification artifact tied to content hash;
- QK04/QK06 mandatory gates pass;
- Diagnostic Depth / Scan Resistance metrics pass QK07+;
- repetition/dominant-strategy quotas pass portfolio audit;
- each QK13+/mastery case has concise human proof route;
- no numerical-reskin filler remains.

### 12E — UX / accessibility / controller / target-device
Complete when:
- first-session QK01–QK06 flow matches frozen onboarding;
- full controller path and dynamic glyphs work;
- 1280x800 at 100/115/130% text passes readability stress;
- non-color coding, reduced motion, audio independence, remapping, hold/toggle choices work;
- evidence snapshots/reason traces pass anti-leak tests;
- 10-customer stress case meets navigation gate;
- pause/settings/save/resume are complete.

### 12F — Adversarial QA
Complete when:
- deterministic golden/property tests pass;
- no hidden truth leaks through UI, achievements, hints, logs or release debug surfaces;
- save corruption/migration/backup recovery tested;
- Cloud divergence preserves both incompatible attempts and never silent-merges them;
- demo import repeated/corrupt/incompatible cases are safe;
- restart/checkpoint/replay/fast-forward are idempotent regarding game truth;
- objective/world-quantifier edge cases pass;
- invalid/uncertified content cannot enter release package.

### 12G — Empirical gates
Complete only after representative external playtests address all gates in section 14, with recorded evidence and repairs. Critical product gates are QK02 identity comprehension, QK07+ scan resistance, QK04/QK06 data certification, no repetition before Chapter 5, Deck/controller usability, evidence comprehension and no hidden-truth leakage.

A failed gate is not waived by internal familiarity with the design.

### 12H — Release candidate
Complete when:
- retained campaign/mastery content is fully certified;
- demo QK01–QK06 is release-quality and carryover behavior safe;
- Windows + Linux/Deck target builds pass deterministic regression;
- Steam achievements/Cloud/controller integration is idempotent and tested;
- current market/price check completed and final price set within approved band or design reopened;
- performance, packaging, localization and accessibility regression pass;
- store/trailer creative communicates deduction rather than queue management;
- release checklist has no unresolved critical/high issue;
- dedicated repository sets its own `IMPLEMENTATION COMPLETE = YES` only then.

## 16. Final contradiction check

No important gameplay decision remains undefined. Known earlier ambiguities are resolved:
- actual-type reason wording before proof is forbidden;
- QK01–QK06 are all mandatory before Chapter 2;
- later 4-of-6 progression is conditional on foundations;
- all retained campaign cases required for final completion;
- QK04/QK06 are strict data-certification obligations;
- Type Lens remains fair public computation but content must resist greedy scanning;
- runtime dead-state announcement is optional unless exactly proven;
- quality cuts are allowed before filler, within the documented floor;
- sixth heuristic is a design reopen.

The remaining unknowns are empirical or implementation-flexible, not missing gameplay design.

# FINAL RESULT

**GAME #017 DESIGN COMPLETE = YES.**

Migration is now required. If a dedicated repository is unavailable, retain all Game #017 files in this factory as a frozen **NON-ACTIVE safety archive**, mark migration pending, and immediately advance the factory to Game #018 clean-slate Phase 1.
