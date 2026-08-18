# FACTORY STATUS

Last updated: 2026-08-18
Repository: `Mikayilzade/gpt-game-autonomy`
Branch: `main`

## Factory state
- Reusable factory rules: **YES**
- Completed Game #1 migrated out: **YES — Organism Cargo**
- Dedicated Game #1 repository: **Mikayilzade/organism-cargo**
- Factory cleanup after Game #1: **COMPLETE**
- Current design slot: **Game #2**
- Game #2 autonomous design run count: **10**
- Game #2 concept selected: **YES — False Map Department**
- Product Thesis locked: **YES**
- Phase 4 Mechanical Architecture: **COMPLETE ON PAPER**
- Phase 5 Content Architecture: **COMPLETE ON PAPER**
- Phase 6 UX / Presentation Architecture: **COMPLETE ON PAPER**
- Phase 7 Economy / Retention / Commercial Model: **COMPLETE ON PAPER**
- Phase 8 Technical Implementation Specification: **COMPLETE ON PAPER**
- Game #2 DESIGN COMPLETE: **NO**
- Dedicated Game #2 repository: **NOT YET — create only after design freeze/migration gate**

## Current phase
**Game #2 — Phase 9 Whole-Game Simulation on Paper NEXT**

## Active temporary files — mandatory recovery read
1. `GAME2_RESEARCH.md`
2. `GAME2_TOURNAMENT.md`
3. `GAME2_TOURNAMENT_RUN4.md`
4. `GAME2_TOURNAMENT_RUN5.md`
5. `GAME2_PRODUCT_THESIS.md`
6. `GAME2_MECHANICAL_ARCHITECTURE.md`
7. `GAME2_CONTENT_ARCHITECTURE.md`
8. `GAME2_UX_PRESENTATION_ARCHITECTURE.md`
9. `GAME2_ECONOMY_COMMERCIAL.md`
10. `GAME2_TECHNICAL_SPEC.md`

## Completed — autonomous run 10
1. Re-read `START_HERE.md`, `STATUS.md`, `GAME_INDEX.md` and every active Game #2 recovery file before acting.
2. Executed Phase 8 as one substantial technical-specification pass without starting production code or changing the six map primitives.
3. Performed fresh official technical checks against current Godot and Steamworks documentation.
4. Froze **Godot 4.7.1-stable / GDScript-first / 2D** as the implementation direction, with exact stable engine pinning rather than ambient latest-version upgrades.
5. Separated the architecture into Domain Core, Application Services, Presentation and replaceable Platform Adapters; presentation scenes are explicitly non-authoritative for gameplay.
6. Froze the conceptual data model for authoritative map state, derived world, agents, objectives/invariants, linked authority and causal events.
7. Froze deterministic-domain rules: integer/enums where possible, explicit stable sorting, no frame time/physics/hash iteration/locale/platform identity in gameplay, canonical serialization/hash and replay fixtures.
8. Froze semantic `EditCommand` + idempotent transaction commit with pre-state hash protection and exact Phase-4 A–I resolution ordering.
9. Froze simultaneous reaction beats using one immutable start snapshot and two-buffer intent/apply semantics.
10. Froze linked-map authority as a validated DAG with cycle/double-owner rejection and the four-layer content ceiling enforced by tooling.
11. Froze Undo/Redo as exact canonical checkpoints per accepted edit; derived consequences remain part of the parent transaction, and Stability gets explicit recovery semantics.
12. Froze separate settings/profile-progress/active-session save domains with versioned envelopes, checksums, generations, primary/temp/backup recovery and no assumption that filesystem rename is universally crash-atomic.
13. Froze schema migration versus content-version compatibility: incompatible active cases restart safely while compatible long-lived progress remains preserved.
14. Froze Steam Cloud semantic progress merge when multiple candidates are available: baseline clears/tutorial tags/mastery facts merge monotonically; divergent active dossier branches are never synthesized. Documented the adapter limitation when Steam exposes only one conflict-selected candidate.
15. Froze demo->full import as versioned, monotonic and idempotent through explicit mapping + receipt IDs.
16. Froze InputMap-style semantic action abstraction, logical keyboard/controller focus graph, remapping/recovery and Deck 1280×800 technical constraints.
17. Froze tokenized localization, gettext/Godot-compatible translation pipeline, pseudolocalization and the rule that translated text can never be a gameplay ID.
18. Froze data-driven dossier compilation/validation covering references, authority DAG, campaign prerequisites, content ceilings and exact-version known-solution fixtures.
19. Froze a headless deterministic test harness with primitive, archetype, simultaneous movement, causal ancestry, history, Stability, linked authority, persistence, migration, demo and golden-replay fixtures.
20. Defined performance/memory/load targets suitable for the deliberately small 2D domain and Steam Deck-class hardware.
21. Defined failure handling for illegal edits, partial transactions, corrupted saves, incompatible content versions and platform outages.
22. Defined implementation slices from domain test skeleton -> road-only executable map -> D08-like local vertical slice -> full local semantics -> linked authority -> campaign/profile/demo/platform -> content population.
23. Recorded ten major technical risks and explicit gates.
24. Added Phase-8 acceptance tests **T8-01 through T8-47**.
25. Closure review found no genuine technical contradiction requiring Phase 3–7 reopening. Phase 8 is **COMPLETE ON PAPER**.

## Locked Game #2 thesis
**False Map Department** — Redraw the official map and the tiny world must obey: move roads, borders, rivers and landmarks to solve civic problems without creating worse consequences elsewhere.

### Non-negotiable differentiation rule
**The map is not a representation of the world. The map is an executable authority over the world.**

## NEXT ACTION
Execute **Phase 9 — Whole-Game Simulation on Paper** as one substantial pass.

Before acting, read `START_HERE.md`, this file, `GAME_INDEX.md`, and every file under Active temporary files.

Walk the canonical product end-to-end and pressure-test at minimum:
1. first boot/accessibility setup -> Department Desk -> D01;
2. exact first 5 minutes and first 15–25 minute demo experience;
3. first 30–60 minutes through early primitive teaching;
4. Act-I completion D08 and first remix-pack unlock;
5. Act II semantic/permission escalation;
6. Act III second-order chains and first Procession/complex Stability use;
7. first linked-map dossiers around D23–D25 and layer-authority comprehension;
8. Act IV/V late-game density, including Deck readability and causal ancestry under 2–4 layers;
9. D40 synthesis and baseline completion with zero mastery;
10. post-campaign mastery/remix loop and whether it feels meaningful rather than checkbox cleanup;
11. demo -> full-game import on same and incompatible content versions;
12. mid-edit/mid-Stability quit/recovery and Cloud conflict examples;
13. mouse+keyboard, keyboard-only and controller-only complete interaction paths;
14. unusual/hostile behavior: brute-force Undo, edit thrashing, layer hopping, duplicate semantic names, intentionally trapped agents, repeated restart, corrupted save, stale command/double input;
15. hour-10 repetition/content-exhaustion risk;
16. whether any sequence dilutes the executable-map fantasy.

Record exact contradictions, boredom/opacity risks and repair proposals. Reopen only the smallest affected earlier phase if a true inconsistency is found; otherwise leave frozen rules intact. Create a canonical Phase-9 whole-game simulation file and acceptance/repair checklist. Do not declare design complete yet.

## Completion rule
Remain **В процессе** until Game #2 has:
- full specification through Phase 11;
- `DESIGN COMPLETE = YES`;
- safe migration to its own dedicated repository;
- autonomous implementation handoff created and verified;
- `GAME_INDEX.md` updated;
- factory cleaned/reset for Game #3.

## Recovery rule
Read `START_HERE.md`, this file, `GAME_INDEX.md`, then every file listed under Active temporary files, and execute `NEXT ACTION` exactly.