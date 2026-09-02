# GAME #013 — FINAL SPECIFICATION FREEZE

Date: 2026-09-02
Game: **SEAL BREAK** (working title)
Status: **DESIGN COMPLETE = YES**
Migration: pending dedicated repository availability

## 1. Authority and freeze verdict
This file is the highest implementation-facing design authority for Game #013. It consolidates Phase 4–10 and normalizes every Phase-9/10 repair. If older Game #013 wording conflicts with this file, this file wins. Earlier research/tournament files are decision history only.

Authority below this freeze, for detail not contradicted here:
1. `GAME13_FINAL_FREEZE.md`
2. `GAME13_ADVERSARIAL_REVIEW.md`
3. `GAME13_WHOLE_GAME_SIMULATION.md`
4. `GAME13_TECHNICAL_SPEC.md`
5. `GAME13_COMMERCIAL_MODEL.md`
6. `GAME13_UX_PRESENTATION.md`
7. `GAME13_CONTENT_ARCHITECTURE.md`
8. `GAME13_MECHANICAL_ARCHITECTURE.md`
9. `GAME13_PRODUCT_THESIS.md`
10. tournament/research files as historical rationale only.

Final contradiction scan: PASS. Remaining unknowns are empirical/release choices, not missing gameplay design. No production implementation is authorized inside the factory.

## 2. Frozen product identity
PC/Steam-first single-player premium authored deterministic deduction puzzle. The player places or reads tamper-seal witnesses on a compact compartmented object and chooses/reconstructs a bounded opening history so irreversible tear evidence matches a target record.

Core fantasy: physical witnesses prove what happened and in what order.

Core loop: inspect immutable seam/socket relations -> place seals and/or construct a legal bounded history -> commit -> deterministic checkpoint reveal -> inspect tear/survival evidence -> replay/return to edit -> revise -> solve.

The game is not a detective narrative, security simulator, physics sandbox, escape room, paperwork game, roguelite, live service, or freeform destruction game.

## 3. Frozen mechanical contract
A case contains finite compartments, seams, legal seal sockets, placement rules, one bounded opening-history contract, and target evidence predicates.

Canonical geometry:
- each compartment stores the seams traversed when opened;
- each socket stores seams it covers;
- trigger compartments are derived, never independently authoritative;
- installed witness identity is the socket identity.

Opening is atomic. History contains distinct compartments only; omitted compartments remain unopened. One compartment opens per checkpoint.

Authoritative tear rule for installed socket `s` under history `H`:
`break_step(s,H) = min { i | traversed_seams(H[i]) intersects covered_seams(s) }`, else `NEVER`.

At each checkpoint all currently intact qualifying witnesses break atomically and permanently at that same checkpoint. Animation sub-order has no meaning. Broken witnesses never update again.

Canonical placement modes only: `FIXED`, `CHOOSE_EXACT_K`, rare reviewed `CHOOSE_UP_TO_K`, optional finite `CHOOSE_FROM_GROUPS`.

Canonical history modes only: `FIXED_HISTORY`, `CHOOSE_FROM_AUTHORED_HISTORIES`, `ARRANGE_REQUIRED_SET`, `ARRANGE_BOUNDED_SUBSET`. No repeated openings, simultaneous compartment events, hidden branches, random events or conditional AI.

Evidence predicate vocabulary is frozen to: `INSTALLED`, `NOT_INSTALLED`, `BREAKS_AT`, `BREAKS_BEFORE`, `BREAKS_AFTER`, `INTACT_THROUGH`, `FINAL_INTACT`, `FINAL_BROKEN`, `OPENED`, `UNOPENED`, `OPENS_AT`, `SAME_BREAK_STEP`, `BREAKS_EARLIER`.

Success means structural legality plus every authored evidence predicate true. Runtime accepts every satisfying submission. Certification classifies `UNIQUE_EXACT`, `UNIQUE_OBSERVABLE`, intentional `MULTI_VALID_INTENTIONAL`, or invalid ambiguity.

Commit freezes an immutable submission. Resolver completes semantic resolution before presentation. Replay uses the same committed snapshot/trace. Return to Edit restores the exact pre-commit tentative submission. Edit undo/redo never rewinds simulation checkpoints.

## 4. Oracle boundary
Before commit the player may inspect all immutable geometry, socket covered seams/derived trigger compartments, fixed constraints, tentative input structure and target evidence.

Before commit runtime must never reveal hypothetical consequences: no predicted break times/states, live target correctness, future tear hover, suggested edit, closeness, satisfied-predicate count, mismatch relevance ranking or solver-derived next action.

After commit, exact retrospective causality is allowed for the committed trace. Mismatch ordering remains authored target order. On return to edit the active edit surface is neutral; observed history is available only through explicit last-run replay/history inspection.

## 5. Campaign/content freeze
Six reasoning families share the same witness law:
1. direct witness reading;
2. divergent/intersection witness comparison;
3. survivorship/omitted-event reasoning;
4. inverse witness placement;
5. history reconstruction;
6. coupled placement + history.

Shipping commercial floor is exactly 24 cases, identified by `required_for_floor`, not numeric range:
`SB_01–04, SB_06–09, SB_11–14, SB_16–19, SB_21–24, SB_26–29`.

Target configuration is 30 cases by adding `SB_05, SB_10, SB_15, SB_20, SB_25, SB_30` as optional fifth beats. Optional 31–36 are not promised and require strict same-vocabulary novelty gates.

Correct introduction schedule, superseding stale Phase-5 range prose:
- SB_01–14: reading/comparison/survivorship foundations;
- SB_16–19: player witness placement under fixed/highly constrained history;
- SB_21–24: history reconstruction; SB_21 is first free `ARRANGE_REQUIRED_SET`;
- SB_26–29: genuine coupled placement + history; SB_26 is first coupled family;
- fifth beats may recombine already-taught vocabulary but may not introduce a rule required by the floor.

Every MID/LATE/CAPSTONE shipping case requires a written human solve sketch with at least three genuine class eliminations before residual trial. Checking individual submissions does not count. Difficulty may not be justified by merely adding evidence cards, compartments, sockets, trigger-set size, history length or exact checkpoint numbers. Human review must identify first non-trivial deduction, eliminated class, dependent second deduction, and why decoys change reasoning rather than search count.

Certification is exhaustive over bounded legal submissions and uses the same Domain rules as runtime. Default target <=1,000,000 combined legal submissions; warning >250,000; >1,000,000 requires explicit deterministic completeness review.

## 6. UX/accessibility freeze
Canonical gameplay surface: persistent Workbench plus switchable Plan and Evidence rails; on narrow/handheld layouts rails reflow to drawers. Controller/keyboard/mouse are first-class; no gameplay requires pointer precision or drag.

Workbench shows stable compartment labels, explicit seams and finite sockets. Identity uses pattern/icon/text, never color alone. Plan rail exposes only input structure. Evidence rail separates TARGET from OBSERVED.

History arrangement uses discrete focus/move/confirm/cancel operations. Bounded-subset mode explicitly separates OPEN slots from LEFT CLOSED pool. Structural illegality may disable Commit and explain missing input; logical wrongness may not.

Reveal supports Step/1x/2x/Instant/Skip and reduced motion without changing semantic trace. Replay/scrub shows committed checkpoints only.

Release gate: every shipping case must pass controller-only and keyboard-only navigation plus 1280x800 at 200% text with pseudo-long localization. Focused evidence card must preserve witness/compartment identity, predicate and checkpoint as one semantic unit, cross-highlighting must remain available, rail focus must restore exactly, and puzzle difficulty may not depend on remembering inaccessible UI. Important text/visual contrast targets >=4.5:1 standard and >=3:1 large; color-independent semantics are mandatory.

## 7. Commercial/progression/demo freeze
One premium base game + free demo. Planning launch-price anchor is $11.99 within a $9.99–12.99 posture, but final price is a release-time market decision. No ads, MTX, paid hints, lives, premium currency, battle pass, subscription, grind, required daily play or live-service cadence.

Progression is prerequisite/threshold based. Four floor cases per act constitute act core; optional fifth beats never gate the next act. `CAMPAIGN COMPLETE` = all 24 floor cases. `FULL CASEBOOK COMPLETE` = all shipping cases.

Hints are explicitly requested, free, authored and at most three steps: observation, deduction, nudge. They never alter resolver rules or turn edit UI into an oracle. Stable no-hint achievement condition is `max_hint_step_opened == 0`; display wording must truthfully describe that condition.

Demo is six curated beats: SB_01, SB_02, SB_06, SB_11, SB_17, then a true coupled capstone. The sixth beat MUST be mechanically identical to a suitable certified SB_26–SB_29 campaign case or a separately identified/certified demo case derived from that coupled lineage. SB_24 alone cannot satisfy the capstone promise. A mechanically modified demo wrapper never marks a campaign case solved merely by sharing presentation lineage.

Demo->full import is one-way, idempotent and monotonic for compatible facts and never overwrites newer full progress.

Store/trailer must show real physical witness/tear gameplay and a genuine coupled late-loop beat; no implication of procedural infinity, freeform physics/destruction or detective-story gameplay.

## 8. Technical freeze
Recommended future bootstrap: then-current supported stable Godot 4.x; 4.7.2 was the design-time stable baseline, not a permanent lock. GDScript default unless implementation evidence justifies otherwise.

Architecture separates pure Domain, Application, Presentation, Platform adapters and offline authoring/certifier. Domain has no rendering, animation, Steam, filesystem, locale, RNG or wall-clock dependency.

Runtime, replay and certifier share one resolver/predicate contract. Case semantic data is versioned and canonicalized. Required identities include schema/rules/content revision, `mechanics_hash`, submission hash, trace hash and certification hash. Mechanical changes require rules/mechanics compatibility changes and recertification; presentation/localization-only changes do not invalidate solve facts.

Saves use atomic main+backup/recovery, future-version protection and deterministic migration. Cloud/externally changed state arriving during commit/resolve/reveal/replay/result is queued until a safe boundary and may never mutate the active committed snapshot/trace.

Persisted completion distinguishes `historical_completion`, `current_revision_solved`, and `ever_unlocked`. If mechanics/acceptance changes without explicit migration: preserve history, mark current revision revalidation-required, never revoke granted achievements, never relock previously legitimate downstream access, and evaluate future locked prerequisites against current-compatible solve facts plus explicit grandfather migrations. Full Casebook/current completion uses current revision facts.

Draft/replay compatibility is mechanics/rules bound. Incompatible old drafts are not force-applied. Demo/full compatibility likewise requires mechanics/acceptance identity.

## 9. Explicitly out of scope for v1
Multiplayer; networking/social accounts; live service; procedural campaign promise; freeform cabinet construction; physics-authoritative tearing; repeated/reclosable openings; seal durability/strength economy; crafting; NPC simulation; dialogue-heavy mystery; open world; roguelite/deckbuilder wrapper; timers/speed medals/leaderboards as required play; monetized hints; UGC/editor/Workshop as launch requirement; proprietary cross-platform cloud; arbitrary new predicate types; gameplay-affecting DLC withheld from base scope.

## 10. Implementation-flexible items
A future implementation session may choose without reopening design: exact 2D/2.5D shell art, animation easing/timing within accessibility constraints, scene hierarchy, serialization format preserving semantic contracts, Steamworks binding, decorative audio/visual treatment, final commercial title, final localization list, final launch price, achievement display names/icons, and whether certification/playtests justify shipping 24 or 30 cases.

These choices may not change mechanics, oracle boundary, campaign-floor semantics, demo truth, persistence compatibility or accessibility gates.

## 11. Empirical/release gates
Design is complete, but release remains blocked until implementation/playtest proves:
- real first-solve times and onboarding comprehension;
- fatigue/repetition acceptable at hour 3/hour 8;
- all shipping MID/LATE/CAPSTONE cases pass the three-class-elimination human solve gate;
- a demo-readable coupled SB_26–29-lineage capstone exists and certifies;
- mismatch explanation is useful without becoming an oracle;
- 1280x800/200% pseudo-long localization and controller/keyboard paths pass on real UI/art;
- final 24-vs-30 shipping set is certified, non-repetitive and polished;
- all shipping cases exhaustively certify under their declared equivalence policy;
- save corruption/recovery, Cloud conflict/queueing, demo import and mechanics-changing migrations pass fixtures;
- store price/languages/engine stable version are rechecked near release.

Failure of a gate requires content/implementation repair; reopening the frozen mechanic requires explicit design change control.

## 12. Implementation acceptance checklist
A fresh implementation session may claim frozen design implemented only when all are true:
- pure deterministic resolver matches the frozen checkpoint/tear law;
- same-checkpoint tears are atomic and animation-order-independent;
- all four history modes and allowed placement modes obey structural legality;
- exact frozen predicate vocabulary evaluates correctly including NEVER edge cases;
- runtime/certifier/replay parity tests use shared Domain semantics;
- pre-commit UI leaks no hypothetical result/distance information;
- retrospective mismatch references committed causal trace only;
- undo/redo, replay, reset and return-to-edit preserve transaction semantics;
- case schema/hashes/versioning and exhaustive certifier are operational;
- campaign uses explicit prerequisites and `required_for_floor`, never numeric floor inference;
- SB_21/SB_26 onboarding boundaries are respected;
- 24-case floor and optional fifth beats behave correctly in both 24/30 configurations;
- every substantive shipping case has certification + required human solve documentation;
- controller-only, keyboard-only and mouse paths cover all verbs;
- 1280x800/200%/pseudo-long accessibility gate passes every shipping case;
- seal/evidence semantics are never color-only;
- hint steps are explicit, authored, free and isolated from normal edit feedback;
- demo beat 6 is a certified true coupled case from SB_26–29 lineage or separate equivalent-rule demo case;
- demo import is compatible, idempotent and non-destructive;
- save main/backup recovery and future-version protection work;
- external/Cloud changes cannot mutate an active committed trace;
- changed-case progression preserves history/ever-unlocked while requiring compatible current solve unless explicitly migrated;
- achievements are idempotent and no-hint condition uses explicit hint-state semantics;
- no forbidden monetization/retention/physics/procedural feature has crept into core scope;
- empirical gates are recorded and resolved before release candidate.

## 13. Freeze decision
**PASS — DESIGN COMPLETE = YES.**

Seal Break now contains enough mechanical, content, UX, commercial, technical, persistence, accessibility and acceptance authority for a separate implementation session to build without inventing important gameplay. Remaining work belongs to implementation, content authoring/certification and empirical playtesting.

Dedicated migration target must be discovered/verified rather than assumed. If unavailable, this complete `GAME13_*` package remains a frozen NON-ACTIVE safety archive while the factory advances immediately to Game #014.