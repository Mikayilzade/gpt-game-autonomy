# GAME INDEX

This file tracks games produced by the factory. Finished game-specific design should normally leave this repository after verified migration. A completed package may remain temporarily as a safety archive while dedicated-repository migration is being verified; it is not canon for the next design cycle.

| # | Game | Design status | Dedicated repository | Implementation status | Notes |
|---|---|---|---|---|---|
| 001 | **Organism Cargo** | DESIGN COMPLETE / specification frozen | `Mikayilzade/organism-cargo` | Dedicated implementation track | Migrated with full design canon, validation/history and autonomous implementation handoff. |
| 002 | **False Map Department** | DESIGN COMPLETE / specification frozen / migrated | `Mikayilzade/false-map-department` | Dedicated implementation track | Migrated and integrity-verified; autonomous implementation handoff and CI/email-noise guardrail included. |
| 003 | **Borrowed Collision** | DESIGN COMPLETE / Phase 11 frozen | `Mikayilzade/borrowed-collision` | Dedicated migration/handoff track | Factory source package temporarily retained as non-canonical safety archive. |
| 004 | **HEARWALL** *(working commercial title)* | **DESIGN COMPLETE / Phase 11 frozen / migrated / integrity verified** | `Mikayilzade/hearwall` | Phase 12A ready / production implementation not started | Destination final-freeze blob matches factory source SHA `37fbe588f82b65deeeb734597ffe768bb5399dd0`. |
| 005 | **Tension Budget** *(internal label; title TBD)* | **DESIGN COMPLETE / Phase 11 frozen / migration pending** | target `Mikayilzade/tension-budget` — not yet created | Implementation not started | All 26 main causal blueprints, final readiness audit, freeze and migration handoff are complete. Factory cannot migrate until the dedicated repository exists. |

## Game #005 final design state
Phase 1 generated 60 seeds and Phase 2 selected **G5C02 Tension Budget** over final reserve **G5C37 Zero-G Tool Orbit** after equal destructive tournament pressure.

Final tournament result:
- **Tension Budget — 90.1/100; risk-adjusted confidence 0.84 — WINNER**;
- **Zero-G Tool Orbit — 86.8/100; risk-adjusted confidence 0.72 — RESERVE**.

### Final frozen identity
- PC/Steam-first, single-player, offline-capable compact premium puzzle;
- elevated top-down/isometric embodied traversal;
- one local physical tension carriage on 3–5 snap bands;
- 2–4 active loads and one fixed shared tension budget;
- canonical SLACK / TAUT / HIGH only;
- Lift / Counterweighted Gate / Flexible Span only;
- no numeric engineering UI, detached graph editor, free rope construction, timing solutions or rope simulation authority;
- mature play is temporary compromise -> traversal -> reconfiguration -> optional visible mutation/return inversion;
- 26 frozen main encounter blueprints, with 24–28 still the acceptable release range if empirical repetition requires cuts;
- roughly 4–6 hours first completion;
- free representative 15–25 minute demo;
- working $19.99 USD launch target / $17.99–$21.99 release-decision band;
- Godot 4.7.2-stable / GDScript-first / 3D technical baseline at freeze time;
- mandatory early empirical readability/tactility gate before bulk content production.

### Phase 8 — Technical Implementation Specification
`GAME5_TECHNICAL_SPEC.md` freezes deterministic Domain Core/presentation separation, data model, reducers/events, preview/commit/mutation/restart ordering, transition epochs, persistence/recovery, input/accessibility/localization/performance assumptions, validators/solver/test hooks and Phase 12A–12H implementation order.

### Phase 9 — Whole-Game Simulation
`GAME5_WHOLE_GAME_SIMULATION.md` found finite-state contradictions in the earlier skeleton: one-load E01, illegal low-load 3->2 / 2->3 band counts and the original mutation prototype. It established the explicit two-load maximum of three unique states at B=2.

### Phase 10 — Adversarial Review / Authoritative Repairs
`GAME5_PHASE10_AMENDMENTS.md` added V19 Distribution Path Feasibility and V20 Mutation Activation Safety, repaired E01/E16–E20/demo/prototype rules, constrained late mutation families, interleaved repeated-archetype content, froze controller-disconnect behavior and save-corruption recovery, and required exact encounter-level causal lock before final freeze.

### Phase 11 — Specification Freeze
Phase 11 is **COMPLETE**.

`GAME5_ENCOUNTER_BLUEPRINTS.md` now locks every retained main encounter with:
- exact load IDs/archetypes/order;
- snap count and B;
- exact pre/post distribution vector paths;
- mutation load/direction;
- reasoning signatures;
- intended meaningful commit/separation structure;
- canonical region/traversal-edge graph;
- C0/C1/exit requirements;
- alternate-solution boundaries;
- expected V01–V20 contracts.

`GAME5_PHASE11_READINESS_AUDIT.md` result: **PASS FOR DESIGN FREEZE**.

`GAME5_PHASE11_FINAL_FREEZE.md` is the highest Game #005 design authority and declares **DESIGN COMPLETE = YES**.

Migration-ready factory files also exist:
- `GAME5_MIGRATION_MANIFEST.md`;
- `GAME5_IMPLEMENTATION_START_HERE.md`;
- `GAME5_IMPLEMENTATION_STATUS.md`;
- `GAME5_CI_NOTIFICATION_POLICY.md`.

### Migration blocker
The target repository `Mikayilzade/tension-budget` was searched and does not currently exist. The available GitHub connector can write to existing repositories but exposes no repository-creation operation. Therefore Game #005 is design-complete but is **not yet factory-complete**: migration, integrity verification, Game #005 factory cleanup and reset to Game #006 remain pending.

`Tension Budget` remains an internal project/concept label; a later commercial rename is allowed without changing gameplay canon.

## Important Game #005 reserve/removals
- **G5C37 Zero-G Tool Orbit** — strongest tournament reserve; do not hybridize into winner.
- G5C17 Door Memory — eliminated on property-swap market pressure + lower one-bit campaign ceiling.
- G5C21 Broken Rule Workshop — eliminated on structural brute-force dominant strategy.
- G5C05 Shadow Scaffold — hard-killed by direct solid-shadow traversal precedent.
- G5C09 Rain Router — removed by current water-routing precedent + consumer inflation.
- G5C14 Routine Possession — hard-killed by direct embodied record/repeat automation precedent.
- G5C45 Thermal Footprint — hard-killed after movement-trail precedent + execution/consumer inflation.
- G5C41 Crowd Umbrella — cut because hour-5 depth required disproportionate crowd/NPC complexity.
- G5C01 Frame Pin — cut because mature play converged on familiar object-time-freeze phase selection.
- G5C25 Sunpatch Garden — cut because mature variety depended on ecological consumer catalogue and pacing compromise.
- G5C10 Pressure Line — cut because it lost directly to Tension Budget on world readability/ownability.

## Numbering rule
Use the next unused sequential game number for every new factory design cycle, whether the concept later ships or is killed. If a design is abandoned before migration, record it here as `KILLED` with a short reason so the factory does not accidentally rediscover it as if it were new.

## Migration rule
A game receives its own repository once its design is sufficiently stable to justify migration. The dedicated repo owns implementation and future game-specific work. The factory returns to a clean logical design slot only after migration integrity is verified.