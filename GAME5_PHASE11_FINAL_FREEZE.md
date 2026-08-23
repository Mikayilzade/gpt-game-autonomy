# GAME #005 — PHASE 11 FINAL SPECIFICATION FREEZE

Last updated: 2026-08-24
Factory run: **11 — extended pass**
Selected concept: **G5C02 — Tension Budget**
Commercial title: **TBD**

# DESIGN COMPLETE = YES
# PHASE 11 = COMPLETE

This file is the final design authority for Game #005 before migration to a dedicated implementation repository. It freezes the design, not the production implementation.

## 1. Authority order
For Game #005, resolve conflicts in this order:
1. `GAME5_PHASE11_FINAL_FREEZE.md`
2. `GAME5_ENCOUNTER_BLUEPRINTS.md`
3. `GAME5_PHASE11_READINESS_AUDIT.md`
4. `GAME5_PHASE10_AMENDMENTS.md`
5. `GAME5_TECHNICAL_SPEC.md`
6. `GAME5_UX_PRESENTATION.md`
7. `GAME5_CONTENT_ARCHITECTURE.md`
8. `GAME5_MECHANICS.md`
9. `GAME5_ECONOMY_COMMERCIAL.md`
10. `GAME5_PRODUCT_THESIS.md`
11. tournament/research history for rationale only.

Phase-10 amendments supersede conflicting older content/mechanics wording; the Phase-11 encounter lock supersedes older row-level campaign skeleton details.

## 2. Frozen product
- PC/Steam-first, single-player, offline-capable compact premium puzzle.
- Elevated top-down/isometric 3D presentation.
- Player fantasy: rigger traversing stylized exposed suspended machinery.
- Core hook: move one local physical tension carriage and several connected mechanisms change at once; solve by temporary compromise and traversal.
- Main campaign: 26 locked causal blueprints; acceptable release cut range remains 24–28 if empirical repetition demands cuts.
- First completion target: roughly 4–6 hours.
- Free representative demo: 15–25 minutes.
- Working price target: $19.99 USD; release decision band $17.99–$21.99 without gameplay redesign.

## 3. Frozen mechanics
- exactly one local directly manipulated carriage per normal encounter;
- short rail, 3–5 physical snap bands;
- 2–4 active loads;
- fixed encounter budget B conserved across bands/revisions;
- internal values only 0/1/2 = SLACK/TAUT/HIGH;
- adjacent rail bands exchange exactly one quantum between exactly two loads;
- exact authored vector paths; no free-force solver;
- load archetypes only: Lift, Counterweighted Gate, Flexible Span;
- preview is non-authoritative; commit on released snap only;
- no transition-timing solutions;
- zero/one irreversible visible load mutation per normal encounter;
- mutation preserves B, rail identity and snap count;
- C0 always, C1 only after stable mutation;
- ordinary walking/interact/restart only; no movement mastery pillar.

## 4. Frozen load semantics
- Lift: SLACK/TAUT/HIGH -> LOW/MID/HIGH stable dock.
- Gate: SLACK/TAUT/HIGH -> clearance tier 0/1/2; no partial-gap timing exploit.
- Span: only stable TAUT is traversable; SLACK/HIGH are not normal routes.
- Dynamic rope/physics effects may be cosmetic only and never decide puzzle truth.

## 5. Frozen content law
- Exact campaign causal authority is `GAME5_ENCOUNTER_BLUEPRINTS.md`.
- All retained encounters must pass V01–V20 in serialized implementation data.
- Mature content must preserve decision separation and reject safe static enumeration/permanent-best-band solutions.
- Alternate solutions are welcome only when deterministic/safe and when they do not erase the encounter's declared reasoning family/tutorial purpose.
- A scene that cannot realize its blueprint without new mechanics returns to design review or is cut; implementation may not silently invent another puzzle.

## 6. Frozen UX/accessibility
- controller + keyboard/mouse parity;
- remapping;
- low precision carriage control with strong snap attraction;
- redundant nonnumeric state cues through cable shape, hardware posture and load silhouette;
- no color-only/audio-only truth;
- optional SLACK/TAUT/HIGH labels allowed;
- reduced-motion mode preserves the exact logical solution graph;
- controller disconnect during preview never commits;
- minimal HUD; no numeric tension bars or detached graph UI.

## 7. Frozen persistence/recovery
- semantic deterministic Domain Core is authoritative;
- save C0/C1 semantic state, never transient tween/physics state;
- transition epochs invalidate stale callbacks;
- restart is deterministic/idempotent;
- CurrentRun corruption cannot erase profile progression;
- Profile corruption cannot silently overwrite the corrupt profile with a new one;
- demo and retail use the same gameplay core and separate progression registries.

## 8. Technical baseline
- Godot 4.7.2-stable baseline at freeze time;
- GDScript-first, 3D;
- deterministic Domain Core separated from presentation;
- data-driven encounter Resources/text-diffable definitions;
- headless/static validators, traversal solver, property/integration/golden tests;
- exact Phase 12A–12H implementation sequence remains in `GAME5_TECHNICAL_SPEC.md`.

## 9. Mandatory early empirical gate
Before bulk content production, dedicated implementation must build the three-fixture package from Phase-10 Amendment A10:
- P-A Give/Take: 2 loads / 3 bands / B2;
- P-B Mature Traversal: 3 loads / 4 bands / separated decisions;
- P-C Mutation/Return: 3->2 / 3 bands / B2 / C1.

Pass targets include:
- roughly >=75% median post-teaching consequence prediction;
- most unfamiliar players explain give/take without numbers/graph;
- intentional carriage move roughly <=2–3 seconds once reached;
- blind full enumeration not dominant in P-B;
- no realistic rope simulation required for believable causality.

This gate is empirical-only. The design rules needed to test it are frozen.

## 10. Explicitly out of scope
- second independent carriage as baseline;
- fourth load archetype for 1.0;
- combat/enemies;
- jumping/dashing/crouching as required verbs;
- cutting/tying/free cable construction;
- rope physics as authoritative simulation;
- hidden tension values or numeric engineering calculations;
- graph/circuit editor;
- inventory/crafting/currency/grind;
- move-limit punishment economy;
- multiplayer/network dependency;
- procedural level generation requirement;
- live service.

## 11. Intentionally flexible after freeze
May change without reopening design only if frozen behavior is preserved:
- final commercial title;
- final transforms/metric dimensions/materials;
- transition timings within non-timing bounds;
- camera polish/animation/audio/haptics;
- engine maintenance patch after validation;
- final achievement count within planned range;
- final release price within commercial evidence;
- optional observational hint layer.

## 12. Acceptance statement
The Phase-11 readiness audit passes and every retained main encounter now has an exact causal implementation blueprint. No important gameplay rule, campaign causal structure, recovery behavior or core UX contract is intentionally left for implementation to invent.

**DESIGN COMPLETE = YES.**

Game #005 is not yet factory-complete. Completion requires dedicated-repository creation, migration of this canonical package, autonomous implementation handoff, migration integrity verification, factory Game #005 cleanup, `GAME_INDEX.md` update and reset to Game #006.