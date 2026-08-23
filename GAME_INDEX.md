# GAME INDEX

This file tracks games produced by the factory. Finished game-specific design should normally leave this repository after verified migration. A completed package may remain temporarily as a safety archive while dedicated-repository migration is being verified; it is not canon for the next design cycle.

| # | Game | Design status | Dedicated repository | Implementation status | Notes |
|---|---|---|---|---|---|
| 001 | **Organism Cargo** | DESIGN COMPLETE / specification frozen | `Mikayilzade/organism-cargo` | Dedicated implementation track | Migrated with full design canon, validation/history and autonomous implementation handoff. |
| 002 | **False Map Department** | DESIGN COMPLETE / specification frozen / migrated | `Mikayilzade/false-map-department` | Dedicated implementation track | Migrated and integrity-verified; autonomous implementation handoff and CI/email-noise guardrail included. |
| 003 | **Borrowed Collision** | DESIGN COMPLETE / Phase 11 frozen | `Mikayilzade/borrowed-collision` | Dedicated migration/handoff track | Factory source package temporarily retained as non-canonical safety archive. |
| 004 | **HEARWALL** *(working commercial title)* | **DESIGN COMPLETE / Phase 11 frozen / migrated / integrity verified** | `Mikayilzade/hearwall` | Phase 12A ready / production implementation not started | Top-down real-time acoustic infiltration puzzle. Destination final-freeze blob exactly matches factory source SHA `37fbe588f82b65deeeb734597ffe768bb5399dd0`. |
| 005 | **Tension Budget** *(concept label; title TBD)* | **Phases 1–10 COMPLETE / Phase 11 queued / DESIGN COMPLETE = NO** | — | Not applicable; design factory only | G5C02 selected; technical spec, whole-game simulation and adversarial repairs complete. Phase 11 must lock exact causal blueprints for all retained encounters before freeze. |

## Completed Game #002 identity
**False Map Department** — ontological cartography puzzle: editing the official map immediately rewrites the tiny world, and success requires solving civic goals without creating worse second-order consequences.

## Completed Game #003 identity
**Borrowed Collision** — systemic causal puzzle in which a real resolved collision creates a portable impact whose direction, magnitude and lineage can be physically routed and spent elsewhere, including to create further real collision consequences.

## Completed Game #004 identity
**HEARWALL** — working commercial title for a top-down real-time acoustic infiltration puzzle where the player physically repositions one soundproof barrier so the right listener hears an action while the wrong listener does not, then exploits the deterministic reaction to infiltrate.

### Game #004 migration state
Migration to `Mikayilzade/hearwall` was completed and verified on 2026-08-22. The destination final freeze matches factory source blob SHA `37fbe588f82b65deeeb734597ffe768bb5399dd0`; the dedicated authority chain and implementation handoff are self-contained. Production implementation remains outside the factory.

## Game #005 current design state
Phase 1 generated 60 seeds. Phase 2 selected **G5C02 Tension Budget** over final reserve **G5C37 Zero-G Tool Orbit** after equal destructive tournament pressure.

Final tournament result:
- **Tension Budget — 90.1/100; risk-adjusted confidence 0.84 — WINNER**;
- **Zero-G Tool Orbit — 86.8/100; risk-adjusted confidence 0.72 — RESERVE**.

### Frozen identity through Phase 7
- PC/Steam-first, single-player, offline-capable compact premium puzzle;
- elevated top-down/isometric embodied traversal;
- one local physical tension carriage on 3–5 snap bands;
- one fixed shared tension budget;
- SLACK / TAUT / HIGH;
- Lift / Counterweighted Gate / Flexible Span only;
- no numeric engineering UI, graph editor, free rope construction, timing solutions or rope simulation authority;
- mature play is temporary compromise -> traversal -> reconfiguration -> optional visible mutation/return inversion;
- working 26 main encounters inside a 24–28 acceptable release range, roughly 4–6 hours;
- free representative 15–25 minute demo;
- working $19.99 USD launch target / $17.99–$21.99 business decision band.

### Phase 8 — Technical Implementation Specification
`GAME5_TECHNICAL_SPEC.md` freezes:
- **Godot 4.7.2-stable / GDScript-first / 3D** baseline as of 2026-08-23;
- deterministic Domain Core separated from presentation;
- Encounter/Load/Revision/traversal/runtime/checkpoint data model;
- command -> reducer -> event ordering;
- preview/commit/mutation/restart authority and transition-epoch stale-callback protection;
- deterministic load adapters;
- versioned atomic save/recovery architecture;
- input/controller/accessibility/localization/performance assumptions;
- V01–V18 executable contracts, finite traversal solver and test architecture;
- early empirical gate after vertical slice and before bulk content.

### Phase 9 — Whole-Game Simulation
`GAME5_WHOLE_GAME_SIMULATION.md` found real finite-state contradictions in the earlier skeleton/prototype:
- one-load E01 cannot support 3 conserved distinct bands;
- default 3-load B=3 ->2-load removal cannot support 3–5 unique post-revision states;
- 2-load B=2 pre-revision cannot support a 4-band 2->3 addition;
- original 4-band 3->2 empirical prototype is impossible.

It also established the explicit low-load bound: a two-load revision supports at most **3** unique snap states, with full three-state coverage at B=2.

### Phase 10 — Adversarial Review / Authoritative Repairs
`GAME5_ADVERSARIAL_REVIEW.md` and `GAME5_PHASE10_AMENDMENTS.md` preserve the selected thesis and repair the contradictions without adding mechanics.

Key authoritative repairs:
- **V19 Distribution Path Feasibility** checks that each revision has enough distinct conserved vectors forming a valid adjacent one-quantum path for its snap count;
- **V20 Mutation Activation Safety** checks every objectively reachable mutation band for safe stable C1 reconstruction;
- E01 becomes Lift + Gate / 3 bands / B=2, with Gate visible but non-completion-critical in the first teaching beat;
- 3->2 REMOVE and 2->3 ADD teaching mutations use exactly 3 bands / B=2;
- 4/5-band mutations use feasible 3->4 ADD or 4->3 REMOVE families;
- Band C repeated-archetype lessons are interleaved rather than consecutive;
- E16–E20 mutation direction/snap/B metadata are now explicit and feasible;
- demo D04 uses the legal 3-band removal template;
- empirical prototype becomes three fixtures: give/take, 4-band mature traversal, 3-band mutation/return inversion;
- controller disconnect during preview never commits;
- corrupt-save recovery may not silently erase campaign progress or overwrite a bad profile;
- 26 remains working count, but weak repetition may be cut down to 24–25 without adding rescue mechanics.

### Phase-11 requirement
`DESIGN COMPLETE = YES` is not yet allowed.

Phase 11 must create an implementation-ready encounter lock for every retained main encounter, including:
- exact load IDs/archetypes;
- snap count and B;
- exact pre/post distribution paths;
- mutation direction/load;
- reasoning signatures;
- intended meaningful commit/separation structure;
- canonical region/traversal graph;
- C0/C1/exit requirements;
- alternate-solution boundaries;
- V01–V20 expectations.

Final art transforms may remain flexible, but implementation may not be left to invent causal puzzle design.

`Tension Budget` remains an internal project/concept label; a later commercial rename is allowed without changing gameplay canon.

## Important Game #005 removals/reserve
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

## Final Game #004 tournament reserves
- **G4C01 Seam Thief** — strongest pure abstract puzzle reserve; lost selection on portal perception + topology/contact QA risk.
- **G4C43 Command Wake** — strongest action-puzzle reserve; lost selection on route memorization/choreography + visual readability.

## Numbering rule
Use the next unused sequential game number for every new factory design cycle, whether the concept later ships or is killed. If a design is abandoned before migration, record it here as `KILLED` with a short reason so the factory does not accidentally rediscover it as if it were new.

## Migration rule
A game receives its own repository once its design is sufficiently stable to justify migration, normally at `DESIGN COMPLETE = YES`. The dedicated repo owns implementation and future game-specific work. The factory returns to a clean logical design slot afterward. Temporary safety archives from a prior game may coexist only when explicitly marked non-canonical and excluded from the current recovery chain.