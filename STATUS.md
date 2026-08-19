# FACTORY STATUS

Last updated: 2026-08-20
Repository: `Mikayilzade/gpt-game-autonomy`
Branch: `main`

## Factory state
- Reusable factory rules: **YES**
- Game #1 migrated: **YES — Organism Cargo -> `Mikayilzade/organism-cargo`**
- Game #2 migrated: **YES — False Map Department -> `Mikayilzade/false-map-department`**
- Factory cleanup after Game #2: **COMPLETE**
- Current design slot: **Game #3**
- Game #3 autonomous design run count: **12**
- Game #3 concept selected: **YES — Borrowed Collision**
- Phase 1 Opportunity Discovery: **COMPLETE**
- Phase 2 Concept Tournament: **COMPLETE**
- Phase 3 Product Thesis Lock: **COMPLETE**
- Phase 4 Mechanical Architecture: **COMPLETE ON PAPER**
- Phase 5 Content Architecture: **COMPLETE ON PAPER**
- Phase 6 UX / Presentation Architecture: **COMPLETE ON PAPER**
- Phase 7 Economy / Retention / Commercial Model: **COMPLETE ON PAPER**
- Phase 8 Technical Implementation Specification: **COMPLETE ON PAPER**
- Phase 9 Whole-Game Simulation on Paper: **NEXT**
- Production implementation started: **NO**

## Current phase
**Game #3 — Phase 9 Whole-Game Simulation on Paper / Phase 8 complete on paper**

## Active temporary files — mandatory recovery read
1. `GAME3_RESEARCH.md`
2. `GAME3_RESEARCH_RUN2.md`
3. `GAME3_RESEARCH_RUN3.md`
4. `GAME3_TOURNAMENT.md`
5. `GAME3_TOURNAMENT_RUN2.md`
6. `GAME3_TOURNAMENT_RUN3.md`
7. `GAME3_PRODUCT_THESIS.md`
8. `GAME3_MECHANICAL_ARCHITECTURE.md`
9. `GAME3_CONTENT_ARCHITECTURE.md`
10. `GAME3_UX_PRESENTATION_ARCHITECTURE.md`
11. `GAME3_ECONOMY_COMMERCIAL.md`
12. `GAME3_TECHNICAL_SPEC.md`

## Completed — autonomous run 12
1. Re-read `START_HERE.md`, prior `STATUS.md`, `GAME_INDEX.md`, and every active Game #3 recovery file named by status before acting.
2. Resumed exactly from Phase 8 and created canonical `GAME3_TECHNICAL_SPEC.md` without starting production implementation or reopening gameplay mechanics.
3. Rechecked current official engine/platform evidence on 2026-08-20. Godot 4.7.1 remains the latest stable 4.7 release; 4.7.2 is still release-candidate and 4.8 development-only. Froze **Godot 4.7.1-stable, standard build, GDScript-first, deterministic 2D Control/Canvas architecture**, with an explicit pin/no-ambient-upgrade rule.
4. Froze strict **Domain Core / Application Services / Presentation / Platform Adapter** authority boundaries. Engine physics contacts, scenes, animation timing, render coordinates, locale and Steam identity cannot become gameplay truth.
5. Froze canonical `CaseDefinition`, `CaseState`, player, body, movement-lane, collision-relation, portable-impact, lineage, donor-generation, receiver/transform and objective/invariant/mastery state models.
6. Froze semantic command families for traversal, impact collection, impact transformation, impact spending and RESETTABLE donor reset, plus exact stale/double-command idempotency rules. Self-launch remains an ordinary R6 spend.
7. Froze deterministic movement/collision transaction architecture with same-step snapshot intents, simultaneous collision grouping, data-driven collision outcomes, one-impact-per-lineage emission and bounded chain resolution.
8. Froze canonical serialization independent of Godot object serialization and **SHA-256 `canonical_hash_version=1`** golden replay identity; locale, device, presentation speed and insertion order are forbidden from changing hashes.
9. Froze exact full-checkpoint Undo/Redo architecture for the compact case scale, including player node, bodies, inventory/world pickups, lineage emission, donor generations, receiver states, objectives and causal graph.
10. Froze the content compiler/validator for R1–R8, four donor regeneration classes, four transform families, collision coverage, simultaneous-contact validity, C01–C34 prerequisite graph, tutorial tags, reasoning-transformation windows, mastery distinction notes, remix changed-causal-dependency requirements and known solution fixtures.
11. Added bounded exploit tooling requirements for lineage duplication, donor factories, CYCLIC_WEAK escalation, strong-force dominance and provenance counterfactual failures.
12. Froze persistence domains and save envelopes, validated temp/backup/primary recovery, schema migration, active-case incompatibility handling and the rule that partial collision chains are never persisted as canonical state.
13. Froze Steam Cloud semantics: monotonic profile merge, per-setting logical revisions, strict active-case command-history/hash ancestry for automatic descendant selection, and no synthetic merge of divergent active-case branches. Offline/local correctness remains independent of Steam.
14. Froze demo->full import identity as explicit versioned mapping with monotonic/idempotent receipts; similarity alone cannot auto-clear campaign cases and incompatible active demo state cannot be synthesized.
15. Froze semantic input abstraction plus deterministic authored focus graph for mouse+keyboard, keyboard-only, controller and Deck. Focus cannot depend on zoom, UI scale, scene/hash order or runtime nearest-float ambiguity.
16. Froze localization-ready stable-token architecture and explicitly prohibited translated strings from serving as gameplay identity. Direction enums remain physical-world semantics independent of UI text direction.
17. Froze one documented Godot `--headless` deterministic test entrypoint and 22 required test families covering collision/lineage/donor/receiver/self-launch/moving windows, Undo/Redo, content, persistence, Cloud, demo import, focus, localization and golden replays.
18. Added metamorphic tests and save fault-injection tests covering duplicate commands, lineage emission, transform identity, locale/device/presentation invariance and every durable-write interruption stage.
19. Defined compact performance/memory/load/save targets and a 12A–12H implementation ladder that proves consequence-transfer determinism/readability before large content production.
20. Added notification-safe future implementation expectations: local/headless tests and manual remote CI during unstable bootstrap; automatic push/PR CI only after baseline is consistently green.
21. Added **72 numbered Phase-8 acceptance tests (`T8-01..T8-72`)** spanning architecture, determinism, commands, lineage/donors, history, content compiler, persistence, Cloud/demo, input/localization/Deck, headless replay, fault injection and CI safety.
22. Phase-8 closure: **COMPLETE ON PAPER**. No true Phase-3..7 contradiction was found. One narrow implementation clarification was added: ordinary authored player traversal is canonical node-to-node state for exact save/Undo/accessibility, without adding free-space physics or advancing autonomous collision chains.
23. Production implementation remains **NOT STARTED**.

## Locked Game #3 thesis
**Borrowed Collision** — Steal the force from one crash and spend it somewhere else: harvest collisions as portable impacts, route them through physical sockets, and reuse those consequences on carts, doors, cargo — or yourself.

### Non-negotiable differentiation rule
**A resolved physical consequence becomes a portable resource, and the world-state that created and receives that consequence must continue to matter.**

## NEXT ACTION
Execute **Phase 9 — Whole-Game Simulation on Paper**:
1. walk the product from first boot/accessibility setup to Case Board and DEMO01..DEMO05, recording exact comprehension/interaction risks;
2. simulate the first 20 minutes and first 60 minutes including first fragile/strong-is-bad lesson, first secondary lineage, first donor scarcity and first self-launch;
3. walk Acts I–V through representative cases, especially first two-token ordering, RESETTABLE/CYCLIC_WEAK donor economy, moving receive-window case, multi-room pickup routing, first 3-slot case and C34 synthesis;
4. test whether the product remains `reuse consequences` rather than degrading into detached arrow inventory/vector bookkeeping;
5. attack provenance loss, strong-force dominance, converter busywork, multi-room backtracking/pickup friction, self-launch dexterity drift, moving-window ambiguity, causal-ribbon overload and hour-10 reasoning exhaustion;
6. simulate baseline completion, mastery replay and all three remix packs for genuinely changed causal insights rather than threshold padding;
7. simulate demo->full import, incompatible active demo state, interrupted transaction/save recovery, corrupted primary save, Cloud progress merge and divergent active-case branches;
8. simulate mouse+keyboard, keyboard-only, controller-only and Steam Deck paths, including focus graph, broken remap recovery, no-audio/reduced-motion/slowdown/Pause-Step use;
9. simulate hostile/unusual behavior: duplicate command spam, repeated donor reset attempts, inventory-full harvests, identical-looking impacts with distinct lineage, transform loops, intentionally broken receivers, dead ends, repeated Undo/Redo branching and room hopping;
10. perform hour-10 content-exhaustion audit across the frozen reasoning-transformation vocabulary and identify any repeated three/five-case windows that still feel cognitively identical despite formal tags;
11. record every contradiction/risk and repair only the smallest canonical phase when a genuine contradiction is proven;
12. create `GAME3_WHOLE_GAME_SIMULATION.md` with Phase-9 acceptance checklist and next adversarial targets.

## Completion rule
Game #3 remains **IN PROCESS** until full design freeze, dedicated-repository migration, autonomous implementation handoff + CI/email-noise guardrail, migration verification, `GAME_INDEX.md` update and factory cleanup/reset for Game #4 are all complete.

## Recovery rule
Read `START_HERE.md`, this file, `GAME_INDEX.md`, then every file listed under Active temporary files, and execute `NEXT ACTION` exactly.
