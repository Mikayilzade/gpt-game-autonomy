# GAME #009 — FINAL DESIGN FREEZE

Status: **DESIGN COMPLETE = YES / MIGRATION PENDING**
Date: 2026-08-31
Game: **Binder's Imposition** (working title)
Production implementation in factory: **FORBIDDEN**
Preferred dedicated repository: `Mikayilzade/binders-imposition`

## 0. Final authority and supersession

This file is the single final game-design authority for Game #009. Implementation must follow it first. Earlier Game #009 files remain evidence/history and expand details only when they do not conflict with this freeze.

Precedence:
1. `GAME9_FINAL_FREEZE.md`
2. explicit Phase-10 repairs in `GAME9_ADVERSARIAL_REVIEW.md` where this freeze refers to them
3. `GAME9_WHOLE_GAME_SIMULATION.md`
4. `GAME9_TECHNICAL_SPECIFICATION.md`
5. `GAME9_COMMERCIAL_MODEL.md`
6. `GAME9_UX_PRESENTATION_ARCHITECTURE.md`
7. `GAME9_CONTENT_ARCHITECTURE.md`
8. `GAME9_MECHANICAL_ARCHITECTURE.md`
9. `GAME9_PRODUCT_THESIS.md`
10. tournament/research files as historical rationale only.

Rejected tournament concepts are never Game #009 canon. Games #001–#008 are portfolio/exclusion history only.

---

# 1. Product thesis

**Hook:** Arrange pages on flat sheets so that after they fold, flip, nest and trim, the finished book reads exactly right.

PC/Steam-first, single-player, offline-first, premium systemic permutation/constraint puzzle. The fantasy is predicting how a wrong-looking flat duplex layout becomes the correct bound object. The player is not running a shop and is not learning vocational print production.

Core loop:
1. inspect final-book constraints and available signatures/templates;
2. assign/rearrange faces and choose bounded template/flip/nesting roles;
3. use Fold Preview to inspect deterministic physical consequences;
4. revise the reversible source layout;
5. Commit Bind/Trim for exact predicate evaluation;
6. solve and progress.

Ordinary sessions are discrete authored cases, roughly 20–60 minutes depending on difficulty. Compact workbench, normally 4–20 logical faces, <=3 signatures, <=4 secondary predicate families and <=2 template choices per signature.

Non-goals: no walkable shop requirement, customer/economy sim, freeform decoration core, realistic press calibration/paper chemistry/grain science, avatar locomotion, multiplayer, deckbuilding, roguelite wrapper, progression currency, grind, MTX, ads, live service, hidden fold rules, giant page counts for difficulty, or runtime procedural-content promise.

---

# 2. Exact domain/state model

## PageFace
Stable `face_id`; optional `read_index`; `orientation_requirement = ANY|UPRIGHT|INVERTED`; categorical `material_role`; `blank_kind = CONTENT|REQUIRED_BLANK|SACRIFICIAL`; optional trim mark; finite group tags. All mechanically relevant properties are visible.

## FlatSlot
Stable slot ID, side A/B, cell index, binary base-orientation bit, KEEP/CUT trim zone, optional allowed material roles. Exactly one face or legal EMPTY.

## Signature
Stable ID, categorical material, chosen template, legal NORMAL/FLIPPED sheet state, unique nest role `0..N-1` where 0 is outermost, and slot assignment map.

## FoldTemplate
Finite deterministic slot schema + legal flips + source-slot-to-local-final-position permutation + orientation bits + leaf/facing structure + optional trim behavior. No animation/physics authority.

## WorkbenchState
Case ID; chosen templates; sheet flips; nest roles; slot assignments; permitted face orientation edit bits; semantic transaction history/cursor. This is editable mechanical authority.

## BoundBookState
Pure derived ordered final-face records: book position, face/EMPTY, final orientation, signature/material, nest role, leaf, facing partner, trim result. Never hand-edited or serialized as primary authority.

## Persistent state
Versioned profile/campaign facts, completion, badges, settings/accessibility/input preferences, in-progress snapshot/history, import provenance and save lineage. Progression unlocks are recomputable from completion/prerequisites.

---

# 3. Deterministic resolution order

Frozen order:
1. validate editable legality;
2. resolve each signature locally through its template;
3. compute duplex orientation by XOR;
4. compose signatures by nest role;
5. derive global leaves/facing;
6. resolve trim;
7. evaluate predicates when the operation is Commit or an explicit goal inspection requires a directly observable fact;
8. produce semantic explanation tokens.

`resolve(case, workbench)` is pure and deterministic. RNG, wall clock, frame timing, floating-point geometry and animation cannot affect gameplay state.

Orientation formula:
`final_orientation = face_edit_bit XOR flat_slot.base_orientation XOR template.orientation_bit XOR sheet_flip_bit`.

Only 0/180-degree authority exists.

---

# 4. Frozen transform grammar

Exactly four base transform families. A fifth is not part of this design.

## T4
Slots `A0,A1,B0,B1`.
NORMAL local final order:
`[A1,B0,B1,A0]`.
Base template orientation bits are all 0.

## T4F
NORMAL mapping is T4: `[A1,B0,B1,A0]`.
FLIPPED exact source order:
`[B1,A0,A1,B0]`.
FLIPPED additionally XORs the sheet-flip orientation bit into every resolved face. No other flip rule exists.

## T8
Slots `A0..A3,B0..B3`.
Local final order:
`[A3,B0,A2,B1,B2,A1,B3,A0]`.
Upright template parity: `A3,B0,B2,A1`.
Inverted template parity: `A2,B1,B3,A0`.
The parity map is permanently visible apparatus information; memorization is never required.

## T6P
Uses T8 pre-trim order:
`[A3,B0,A2,B1,B2,A1,B3,A0]`.
Pre-trim local positions 0 and 7, source slots `A3` and `A0`, are CUT and removed. Surviving local order is exactly:
`[B0,A2,B1,B2,A1,B3]`.
Survivor orientation bits are inherited from T8.

CUT positions may contain EMPTY or explicit SACRIFICIAL face/mark tokens. REQUIRED_BLANK is illegal in CUT positions. REQUIRED_BLANK is a real surviving page. `BLANK_AT` can be satisfied only by a surviving REQUIRED_BLANK, never EMPTY. Base T6P does not permit EMPTY in surviving slots.

---

# 5. Exact nesting and book geometry

Every signature has a unique outer-to-inner role. For any resolved local signature sequence `S` of even length `m`, define:
- `front(S) = S[0 : m/2]`
- `back(S) = S[m/2 : m]`.

For signatures ordered outermost -> innermost as `S0..Sn`, global composition is recursively:
`Nest(i) = front(Si) + Nest(i+1) + back(Si)`;
innermost base is `Nest(n) = Sn`.

This formula is authoritative for equal and mixed-size signatures. It yields the known equal-T4 domains: two signatures outer `{1,2,7,8}`, inner `{3,4,5,6}`; three signatures outer `{1,2,11,12}`, middle `{3,4,9,10}`, inner `{5,6,7,8}`.

After global composition, adjacent ordered face pairs form physical leaves according to each template's declared local leaf structure carried through composition; facing spreads are derived from the resulting ordered leaf sequence, never authored as case-local exceptions. Template fixtures must exhaustively verify leaf/facing derivation before content production.

---

# 6. Player verbs and edit semantics

Required verbs: PLACE, SWAP, REMOVE, permitted FACE ORIENTATION toggle, CHOOSE TEMPLATE, FLIP SHEET, SET NEST ROLE/reorder, FOLD PREVIEW, COMMIT BIND/TRIM, UNDO, REDO, RESTART CASE.

Anti-bookkeeping tools may unlock after comprehension: SWAP PAIR, authored MOVE GROUP, inverse-fill ghost labels, CLEAR SIGNATURE. They accelerate manipulation but never choose a solution.

All edits are reversible semantic atomic transactions. Structured operations are one transaction. Preview is non-mutating and creates no history entry. Failed Commit does not mutate layout history. New edit after Undo discards the redo tail.

Template change is one transaction: preserve exact shared legal slot assignments; illegal/disappearing assignments return deterministically to tray; new slots start EMPTY unless locked data says otherwise; locked assignments remain authority; no auto-fill; confirmation reports displaced count; Undo restores exact prior state.

Normal reload restores enough history for useful Undo/Redo. Minimum persistence target is last 64 transactions or full case history when <=256; long histories may compact oldest applied entries into an anchor snapshot plus recent tail without changing current WorkbenchState.

---

# 7. Predicate vocabulary and success

Baseline required predicates use AND only:
`READ_ORDER`, `AT_POSITION`, `FACING`, `SAME_SIGNATURE`, `DIFFERENT_SIGNATURE`, `SIGNATURE_ROLE`, `MATERIAL`, `ORIENTATION`, `SAME_LEAF`, `TRIM_RESULT`, `BLANK_AT`, `TEMPLATE`.

No hidden weighted score, fuzzy partial completion or solver-distance meter.

Illegal setup disables Commit with exact structural reason and does not count as an attempt. Legal Commit succeeds iff every required predicate is true.

Incorrect Commit lists all failed required predicates with exact final-book facts, but never prescribes source moves.

Same unchanged failed state is keyed by canonical WorkbenchState hash + case revision: repeated Commit reopens the same result and does not increment incorrect-attempt stats. Any mechanical edit creates a new semantic state.

---

# 8. Preview vs Commit information boundary

This Phase-10 repair is final.

Preview resolves the complete exact physical book and permits inspection of final order, spreads, leaf relationships, orientation, trim fate, signature/material ownership and source mapping. These are physical consequences of the chosen source state.

Ordinary Preview MUST NOT automatically paint the complete authored predicate list green/red, expose a total correctness count, solver distance, branch ranking, warmer/colder signal, or full truth vector.

A player may select a goal/face and inspect directly observable factual relationships such as `P06 is on Signature B`, `MAP_A is inverted`, or `P04 faces P05`. Commit remains the exact all-failed-predicates evaluation surface.

Same-state Preview reveals no additional mechanical information on repetition. Preview may be Normal/Fast/Instant and is fully skippable; Reduced Motion uses diagrammatic/crossfade presentation. Presentation speed never changes resolution.

---

# 9. Content architecture

Six-chapter authored campaign. Target 30 certified cases; hard commercial-quality floor 24 certified strong cases; soft ceiling 34 including optional Mastery Shelf variants. Never pad to quota.

Arc:
- Ch I: T4 intuition, prediction, T4F orientation, fixed-role two-signature bridge — 4 cases.
- Ch II: free nesting, facing, same-signature/material global choices — target 5.
- Ch III: leaf/different-signature/orientation/global intersections — target 5.
- Ch IV: T8, parity, template choice, mixed T4/T8 — target 5.
- Ch V: REQUIRED_BLANK vs EMPTY, T6P trim fate, trim intersections — target 5.
- Ch VI: three-signature/mixed-size synthesis with no new core rule — target 6.

Canonical demo mapping:
D01=G9_C01 T4 surprise;
D02=G9_C02 prediction reinforcement;
D03=G9_C03 T4F duplex/orientation;
D04=G9_C04 second signature with fixed outer/inner roles;
D05=G9_C05 first free nesting + exactly one FACING relationship;
D06=G9_C06 material/signature-role synthesis with no new transform.

Strong cases require a meaningful global decision or interaction, relevant secondary predicates, no rote-collapse, a short human hypothesis, bounded manipulation, Preview resilience, visual reveal and distinctness.

## Anti-repetition
Structural graph/isomorphism checks are necessary but insufficient. Every STANDARD/MATURE/CAPSTONE case receives 1–3 ordered reasoning-skeleton labels from:
`LOCAL_INVERSE`, `NEST_DOMAIN_ELIMINATION`, `FACING_OR_LEAF_GEOMETRY`, `MATERIAL_OWNERSHIP`, `ORIENTATION_PARITY`, `TEMPLATE_ELIMINATION`, `BLANK_CAPACITY`, `TRIM_FATE`, `GROUP_PARTITION`, `LOCKED_EVIDENCE_PROPAGATION`, `MIXED_SIZE_DOMAIN_COMPOSITION`, `SYMMETRY_BREAK`.

No more than four shipped strong cases may share the same ordered skeleton after cosmetic renaming. No adjacent post-tutorial cases share the same primary step unless explicit reinforcement. Chapter VI uses six distinct primary+secondary combinations. At least one-third of Chapter IV–VI strong cases have a primary step other than GROUP_PARTITION/MATERIAL_OWNERSHIP; at least four late cases are primarily orientation/template/trim/mixed-size geometry.

Release pipeline: schema -> transform fixtures -> solver solvability/canonical classes -> predicate relevance -> rote-collapse -> structural fingerprint/isomorphism -> reasoning-skeleton diversity -> interaction budget -> wrong-global-branch/Preview attack -> human reasoning review -> package manifest.

Runtime procedural generation is not promised. Solver is authoring/certification tooling, not required during normal play.

T8 authoring: first case <=2 orientation-sensitive faces; ordinary target <=3; four only when orientation is primary; when orientation is secondary normally <=2.

---

# 10. Progression, badges and hints

Progression is authored prerequisite/chapter gated. Chapter-I tutorial spine is linear; later chapters use small prerequisite-safe clusters. Keystone completion unlocks the next chapter. No XP/currency/star gate; badges never gate campaign.

Badge vocabulary maximum three reusable types:
- Predicted: satisfy authored prediction before first resolved Preview;
- Direct Bind: requires at least one resolved Preview, then zero **distinct failed Commit states** before success; repeated same-state result openings do not count;
- Constraint Craft: visible case-specific alternate challenge using only existing mechanics and solver-certified as meaningful.

Hints are free/non-punitive and move from rule replay -> reasoning question -> optional global deduction. Accessibility never invalidates progression/achievements.

---

# 11. UX/presentation freeze

Workbench always makes source sheets and goal requirements reachable. Wide layout uses goal rail, flat-sheet canvas, face tray and action strip. 1280x800 is first-class.

Mouse baseline is click-select-click; drag is convenience only. Controller is discrete-focus first-class, never virtual-mouse-only. Every action has semantic input abstraction and remapping. Input glyph failure falls back to localized action name.

When text scale/aspect ratio prevents all signatures being comfortably editable, canonical fallback is a **focused-signature full-size view** plus compact persistent Outer->Inner overview; all three signatures need not be simultaneously editable. Goal rail becomes drawer before slot targets are compressed below reliable interaction size.

Required information is never hover-only, color-only, audio-only or dependent on tiny artwork. Orientation has redundant glyphs. REQUIRED_BLANK and EMPTY have distinct non-color-only iconography/text.

Source mapping may highlight the exact flat source slot for an inspected resolved face because it externalizes known transform bookkeeping. It must never recommend an unchosen destination/source move.

Accessibility baseline: full remapping, controller parity, non-precision interaction, text scaling, reduced motion, color/audio redundancy, skippable animations. Settings apply before title interaction.

---

# 12. Commercial freeze

One-time premium complete game. No MTX, ads, paid hints, grind bypass, battle pass, FOMO, energy, progression currency or live-service obligation.

Design-stage USD list-price band: **$14.99–$19.99**, planning point **$17.99** only if final content/presentation/value gates support it. Price is release-validation data, not gameplay authority. Working title `Binder's Imposition` is also not storefront-frozen; naming requires comprehension/collision/legal validation near release.

Demo is D01–D06 and transfers compatible versioned progress into full game. Demo platform achievements remain disabled; full game reconciles eligible achievements from imported persistent facts. Steam achievement planning target 14–18, working set 16. Steam Cloud is a release target, but unsafe Cloud must be disabled rather than risking state loss.

Post-campaign retention is finite replay/mastery only. Optional Mastery Shelf 4–8 variants must fit the 34-case soft ceiling and pass the same quality gates.

---

# 13. Technical architecture freeze

Recommended implementation direction: Godot 4.x stable, but engine choice is implementation-flexible. Deterministic domain authority must remain engine-independent.

Required layers:
L1 immutable content;
L2 editable WorkbenchState;
L3 pure derived BoundBookState;
L4 presentation/UI state;
L5 persistent Profile/CampaignState.

Required pure conceptual interfaces: `validate_editable`, `resolve`, `evaluate`, semantic `explain`, `preview`, idempotent `commit`, authoring `solve/canonicalize/certify`.

Stable opaque IDs and localization keys; gameplay never branches on localized strings. Canonical serialization sorts maps/IDs and uses deterministic integer/enumerated authority.

Implementation order is frozen by risk:
1. pure T4 deterministic core + fixture tests;
2. editable state + semantic transactions + Undo/Redo;
3. atomic local save/reload/recovery;
4. one complete data-driven vertical-slice case with mouse/controller paths;
5. T4F/T8/T6P + exact nesting/leaf/facing fixtures;
6. predicate/evaluation/explanation system;
7. content certification tooling and demo cases;
8. full UX/accessibility/content;
9. demo import/platform achievements;
10. Cloud only after local durability is proven.

Local persistence precedes platform complexity. Save writes are versioned and atomic: candidate -> temp -> flush -> preserve backup -> atomic replace where possible -> reopen/validate. Unknown future save versions are never overwritten.

Successful Commit becomes authoritative only after the completion/profile mutation is durably saved and reopened/verified. Celebration/platform calls occur afterward and are retryable consequences.

Demo import is monotonic/idempotent. Solved flags OR; valid badges union; existing full progress is never removed. Imported provenance prevents repeated older imports from mutating state.

Cloud lineage uses unique `revision_id`, `parent_revision_id`, local logical revision and enough recent ancestry to distinguish descent from divergence. Safe campaign facts may merge monotonically. Divergent unsolved workbench snapshots and transaction histories are never structurally merged; preserve recoverable alternatives. If safe Cloud behavior cannot be proven, ship without Cloud initially.

Stale content revision: deterministically migrate if supported; otherwise preserve old in-progress work as recovery archive and start the revised case cleanly. Never silently destroy old work.

Achievements are recomputable/idempotent consequences of persistent facts.

---

# 14. Empirical gates retained after design freeze

These gates may tune content, onboarding, presentation, case locks/count, price/title/marketing or remove weak cases. They may NOT silently change the core transform grammar, predicate semantics, deterministic resolution order, premium identity or add a new economy. A core-rule failure requires explicit design reopening.

1. **Transform comprehension:** after tutorial case 4, >=70% representative testers predict two final adjacencies before Preview. Allowed change: onboarding/visual aids/locks/pacing.
2. **Hypothesis vs enumeration:** mature play should be reasoning-led; if >40% of successful players primarily systematic-Preview/Commit enumerate branches, repair cases/onboarding before considering mechanics.
3. **Demo pacing/comprehension:** D04 median <=5m, D05 <=7m, D06 <=8m; demo median target 20–30m, ~40m 75th percentile acceptable if comprehension is strong. Allowed: locks/local manipulation/presentation; no separate rule system.
4. **T8 clerical burden:** if orientation mistakes dominate incorrect commits despite visible parity aids, reduce orientation-sensitive counts or replace weak T8 cases.
5. **T6P clarity:** if players still describe T6P as arbitrary exceptions after first two cases, reduce its campaign presence; do not add variants.
6. **Content-depth proof before scale:** prove >=12 distinct strong post-tutorial cases across Chapters II–VI before full content production. If impossible, return to design.
7. **Release content floor:** >=24 cases must survive structural + reasoning-skeleton review. If only 20–23 survive, revisit commercial value/price/content promise rather than relabel tutorial filler.
8. **Reasoning diversity:** playtest at least 12 representative post-tutorial cases; if >50% tester summaries collapse to the same role-partition sentence, revise authoring.
9. **Manipulation cost:** if 12–20-face cases spend more time on clerical movement than reasoning, improve already-authorized structured operations/locks, not automation of deductions.
10. **Handheld UX:** controller-only 1280x800 at 100/125/150% and maximum supported text scale; focused-signature fallback must preserve all required information/actions.
11. **Persistence integrity:** crash injection around edit/Preview/success-save boundaries, repeated import, stale revision and divergent cloud fixtures must preserve progress/recovery.
12. **Engine spike:** Phase 12A must prove one data-driven T4 case resolves headlessly/animation-free, renders, Undo/Redo, save/reload and mouse/controller paths without domain logic entanglement.

---

# 15. Implementation-flexible vs design-authoritative

Implementation-flexible: exact art style within readable tactile premise; camera easing; paper shader/animation technique; sound palette; menu ornament; chapter display names; engine choice if contracts hold; internal class/file names; serialization syntax; storefront title; final price; launch discount; exact achievement names; exact localization wording; optional telemetry implementation.

Design-authoritative: hook/core loop/non-goals; state boundaries; four transform families and exact mappings; orientation XOR; exact T6P legality; recursive nesting; leaf/facing semantics; predicate vocabulary; reversible verbs; Preview/Commit information boundary; idempotency; campaign/demo mapping; strong-content/reasoning-diversity rules; progression/no-currency model; badge semantics; accessibility/controller requirements; premium/no-MTX boundary; local save durability; import/cloud safety semantics; empirical gates and what they may alter.

---

# 16. Cross-phase acceptance checklist

A fresh implementation must be able to answer YES to all before release candidate:
- exact source state always produces exact same BoundBookState;
- T4/T4F NORMAL+FLIPPED/T8/T6P fixtures match this file;
- mixed-size nesting uses one recursive formula, no case exceptions;
- leaf/facing fixtures are exhaustive for every template combination used by shipped cases;
- REQUIRED_BLANK, EMPTY and SACRIFICIAL are mechanically distinct;
- every edit/structured operation is exact Undo/Redo;
- Preview cannot become aggregate answer-key UI;
- Commit reports every failed required predicate without source-move prescription;
- same-state Preview/Commit are idempotent;
- 24+ strong release cases pass solver, structural and reasoning-diversity certification or commercial promise is explicitly revisited;
- D01–D06 IDs/lessons are identical in demo and full content;
- no badge/accessibility setting gates campaign;
- controller can complete the game without virtual mouse;
- 1280x800 focused-signature fallback works at required text scales;
- local save survives crash tests before Cloud integration;
- demo import is monotonic/idempotent;
- divergent unsolved Cloud branches are preserved, not merged destructively;
- platform failure cannot roll back locally durable completion;
- localization cannot alter gameplay semantics;
- normal play never requires runtime solver;
- no production feature violates explicit non-goals.

---

# 17. Dedicated-repository migration package

When `Mikayilzade/binders-imposition` exists, migrate and verify before deleting factory safety files:
1. this `GAME9_FINAL_FREEZE.md` as final design authority;
2. Product Thesis, Mechanical Architecture, Content Architecture, UX/Presentation, Commercial Model, Technical Specification, Whole-game Simulation and Adversarial Review;
3. research/tournament history as non-canonical rationale if useful;
4. `IMPLEMENTATION_START_HERE.md` pointing first to this freeze and defining phases 12A–12H;
5. `IMPLEMENTATION_STATUS.md` with `IMPLEMENTATION COMPLETE = NO`, Phase 12A exact next action and empirical gates;
6. CI/email-noise policy explicitly forbidding test emails/noisy notification workflows and requiring useful CI only;
7. migration manifest listing source filenames and source blob/commit identifiers where practical;
8. verify destination files and authority chain before removing any Game #009 safety copy from factory.

Repository existence check on 2026-08-31 found no accessible `Mikayilzade/binders-imposition`, so migration is **PENDING and non-blocking**. All `GAME9_*` files therefore remain frozen NON-ACTIVE safety archive after STATUS advances to Game #010.

---

# 18. Freeze verdict

All important gameplay rules are specified. Remaining unknowns are empirical gates or implementation-flexible presentation/release choices with bounded authority. A fresh implementation session should not need to invent important gameplay.

**DESIGN COMPLETE = YES.**

Migration: **PENDING / retained frozen NON-ACTIVE safety archive.**

Factory continuity: **advance immediately to Game #010 Phase 1 Opportunity Discovery.**
