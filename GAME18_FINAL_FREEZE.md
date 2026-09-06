# GAME #018 — FINAL SPECIFICATION FREEZE

Date: 2026-09-06
Game: **LOCAL TIME**
Status: **DESIGN COMPLETE = YES**
Production implementation: NO
Migration: PENDING — dedicated repository `Mikayilzade/local-time` not found on 2026-09-06.

## 1. Authority order
For Game #018, this file is the final design authority. Detailed definitions remain in, and are incorporated by reference from: `GAME18_PRODUCT_THESIS.md`, `GAME18_MECHANICS.md`, `GAME18_CONTENT.md`, `GAME18_UX.md`, `GAME18_COMMERCIAL.md`, `GAME18_TECH_SPEC.md`, `GAME18_SIMULATION.md`, `GAME18_ADVERSARIAL.md`. Research/tournament files are provenance, not permission to revive killed concepts. On conflict, this freeze and later-phase explicit repairs override earlier wording.

## 2. Frozen product
LOCAL TIME is a single-player deterministic spatial scheduling/causal puzzle for PC/Steam. The player moves discrete clock-zones around compact diorama towns so different sites can experience different public local-time labels simultaneously. Clock placement changes **NOW** predicates; valid Resolve transitions create **DONE** persistent milestones; permanent harmful transitions are **LOCKED OUT**. Moving a clock never rewinds completed history.

Store hook: **Move pockets of local time around a tiny town, lining up bakeries, bridges, flowers and trains that all need different times at once.**

No global rewind, retrocausality, continuous timers, hidden schedules, reaction-speed play, random puzzle outcomes, arbitrary per-building scripts, economy/tycoon layer, live service, ads or MTX.

## 3. Frozen executable grammar
Canonical logic is a finite deterministic state machine using only eight semantic families: CURRENT, ADVANCE_ONCE, ORDERED_CHAIN, PERMANENT_LOCKOUT, ACCEPT, DISPATCH, CARRIER_HANDOFF, COUPLED_CURRENT.

Clock labels are semantic discrete IDs; familiar values such as 08:00 do not imply elapsed minutes or ordering unless a public rule explicitly declares it. Logical placement is socketed. Relevant sites cannot receive ambiguous time labels except explicit public multi-label coupled semantics.

Resolve is atomic: validate -> derive coverage -> Snapshot0 -> lockout candidates -> beneficial candidates -> accept/dispatch/coupled candidates -> simultaneous non-carrier commit -> enabled carrier edge -> objective/failure evaluation -> beat increment. One ordered entity advances at most once per Resolve. Same-Resolve prerequisites are false by default. Arrival and acceptance are separate Resolves by default.

Every shippable case has a finite public `resolve_limit`. No-change Resolve is legal, consumes one Resolve, and never accumulates hidden duration. Carrier edges are finite, state-qualified and one-shot from their source state; a persistent DISPATCH milestone cannot repeatedly move a carrier.

## 4. Undo / persistence clarification
Undo is a puzzle convenience, not fictional time travel. Undo Resolve restores the exact pre-Resolve **puzzle** state and counters. Persistence metadata such as save generation remains monotonic; persisting an undone puzzle state creates a new atomic save generation rather than decrementing history.

Replay is presentation-only. Animation never determines logic. Save authority is canonical state, never tween/scene state.

## 5. Content freeze
Campaign target: **36**, quality floor **30**. Mastery baseline: **8**, with **M09–M12 reserve only** if each adds a genuinely new proof topology. If fewer than 30 campaign cases survive the quality gate, reopen content architecture rather than pad the game.

Six chapters progress from NOW/DONE distinction through process ordering, carrier relay, protection/lockout deduction, multi-clock coordination and synthesis. Normal ceilings: <=3 movable clocks, <=8 logically relevant sites, bounded reusable landmark/object/carrier kit. New fiction skins do not create new rule families.

From Case 07 onward every case requires a written causal human proof and anti-enumeration reason. Cases whose practical solution is mainly cycling sockets, following warning icons, or brute-force order scanning are reworked or cut. Duplicate-risk clusters `08/19`, `14/18/29`, `26/27/31`, `32/33/36` must preserve distinct dependency topology.

Case 36 is **Dependency Braid**: <=3 clocks, <=8 relevant sites, >=2 persistent prerequisites, one visible protection constraint, one relay, final two-site coupled-current objective, and a human proof of <=6 necessity statements. Do not replace it with a larger two-hazard/two-carrier spectacle merely for finale scale.

## 6. Demo and onboarding freeze
Free demo is LT01–LT06, target 25–35 minutes. It must prove: current condition; persistent milestone; simultaneous different local times; persistent cargo/later condition; irreversible harmful exposure; unguided multi-zone synthesis.

By LT02, target comprehension is that moving a clock changes what is true **now** but does not reverse what is **done**. If players describe the mechanic primarily as rewind/time travel, repair wording/VFX/onboarding rather than adding temporal complexity.

Preview shows exact footprint, resulting current predicates, illegal conflicts and factual currently-triggerable permanent-risk warnings. It does not simulate/rank multi-beat futures. Warnings never claim a move is globally bad or reveal solvability.

## 7. UX/accessibility freeze
Town-first diorama remains primary interface. NOW / DONE / LOCKED OUT are redundantly encoded by text/icon/pattern/shape; color and audio are never sole carriers. Full mouse/keyboard and controller paths are required, with Steam Deck 1280x800 readability as a baseline target. No precision dragging or timed input is required.

Resolve emits structured reason events rendered as concise causal traces. Failure/dead claims must cite public rules; DEAD is shown only for authored monotonic fatal states, exhausted hard budgets, or exact solver certification.

## 8. Commercial freeze
Premium Steam-first single-player product. Base launch MSRP **$14.99 USD**, review band $14.99–$19.99 before store setup; raise only if validated scope/presentation/value materially exceeds the floor. Expected campaign completion 6–8h at target package, roughly 5–7h acceptable at the 30-case quality floor. No filler is added to defend an hour count.

Demo/full progress import is idempotent and monotonic. Steam Cloud, achievements and localization readiness are launch baselines where platform integration permits; offline puzzle play remains valid. Do not spend the game's single Steam Next Fest participation before a polished representative demo/store page and near-release readiness; re-check current Valve rules/dates at implementation marketing time.

## 9. Technical freeze
Implementation direction: latest stable Godot 4.7.x patch available at bootstrap, GDScript, Windows/Steam first, unless a later implementation-stage compatibility fact requires a documented engine patch/line change without altering game design.

Puzzle authority is a pure deterministic domain layer separate from scenes, animation, frame time, physics and Steam APIs. Solver and validator invoke the same production rule core. Canonical state uses stable authored IDs, versioned normalized serialization and stable state hashes. Every canonical mutation emits structured trace data.

Persistence is atomic with known-good fallback. Corrupt/incompatible case checkpoints never cause partial invented state. Demo import cannot overwrite newer full-game progress. Cloud-divergent in-progress checkpoints are selected whole, not field-merged; corrupt cloud state cannot overwrite valid local state.

Required tests include LT01–LT06 golden witnesses, iteration-order determinism, persistence round trips/corruption recovery, undo exact puzzle-state restoration, solver witness replay, ambiguous-overlap rejection, one-transition-per-entity, one-shot carrier edges and trace coverage for every mutation.

## 10. Empirical gates retained for implementation
These are validation obligations, not missing game-design rules:
1. first-time NOW vs DONE comprehension by LT02;
2. no false rewind inference from earlier-looking labels;
3. overlap/clock readability at 1280x800 and non-color mode;
4. controller navigation without pointer emulation;
5. risk warnings inform without becoming an oracle;
6. six-case demo actually lands near 25–35 minutes;
7. 30–36 campaign cases survive proof-shape diversity review;
8. 8 mastery cases survive quality review, reserves only if novel;
9. 6–8h target is validated without filler;
10. clock-zones feel embodied rather than abstract switches;
11. bounded exact solver/validator is practical for authored content.

If an empirical gate fails, first simplify presentation/content or cut weak cases. Do not silently add a ninth semantic family, rewind, continuous time, hidden information or scope-expanding simulation.

## 11. Implementation acceptance handoff
A dedicated implementation session should be able to build without inventing important gameplay. Required order: technical bootstrap -> LT01–LT06 deterministic vertical slice -> solver/validator -> persistence/recovery -> presentation/accessibility/controller -> platform adapters -> quality-gated content population -> adversarial QA/empirical gates -> release candidate.

Do **not** populate all campaign content before the six-case vertical slice proves the mechanic and UX.

Dedicated repository must contain/verify `IMPLEMENTATION_START_HERE.md`, `IMPLEMENTATION_STATUS.md`, and a CI/email-noise policy before migration is considered complete.

## 12. Freeze verdict
Phases 3–10 reconcile without unresolved rule contradiction after the Phase-9 repairs and Phase-10 adversarial decisions above. Remaining unknowns are explicitly empirical implementation gates, not missing core design.

**DESIGN COMPLETE = YES.**

Migration target `Mikayilzade/local-time` was searched on 2026-09-06 and was unavailable. Therefore all `GAME18_*` files remain in the factory as a **FROZEN NON-ACTIVE SAFETY ARCHIVE**. They must not become canon for Game #019. Pending migration does not block the factory.
