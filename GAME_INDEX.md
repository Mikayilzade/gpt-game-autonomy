# GAME INDEX

This file tracks games produced by the reusable design factory. Dedicated repositories own implementation. After verified migration, finished game-specific design normally leaves the factory; however, a frozen completed game may remain temporarily as a **non-active safety archive** when its dedicated repository does not yet exist. A pending migration must not block design of the next numbered game.

| # | Game | Design status | Dedicated repository | Implementation status | Notes |
|---|---|---|---|---|---|
| 001 | **Organism Cargo** | DESIGN COMPLETE / specification frozen | `Mikayilzade/organism-cargo` | Dedicated implementation track | Migrated with design canon and autonomous implementation handoff. |
| 002 | **False Map Department** | DESIGN COMPLETE / specification frozen / migrated | `Mikayilzade/false-map-department` | Dedicated implementation track | Migration integrity verified; CI/email-noise guardrail included. |
| 003 | **Borrowed Collision** | **DESIGN COMPLETE / Phase 11 frozen / migrated / integrity verified** | `Mikayilzade/borrowed-collision` | **Phase 12A ready / IMPLEMENTATION COMPLETE = NO** | Frozen design package and autonomous implementation handoff migrated. |
| 004 | **HEARWALL** *(working title)* | DESIGN COMPLETE / Phase 11 frozen / migrated / integrity verified | `Mikayilzade/hearwall` | Phase 12A ready | Dedicated implementation handoff verified. |
| 005 | **Tension Budget** *(internal label; commercial title TBD)* | **DESIGN COMPLETE / Phase 11 frozen / migrated / integrity verified** | `Mikayilzade/tension-budget` | **Phase 12A ready / IMPLEMENTATION COMPLETE = NO** | 26 causal encounter blueprints; dedicated authority/handoff/CI policy present. |
| 006 | **Stitchspace** *(working title)* | **DESIGN COMPLETE / Phase 11 frozen / migration pending / retained non-active safety archive** | `Mikayilzade/stitchspace` *(repository not yet created)* | **NOT STARTED** | Full Game #006 safety copy remains in factory and is not active canon. Migration can happen later without blocking the factory. |
| 007 | **Last Known Shape** *(working title)* | **DESIGN COMPLETE / Phase 11 frozen / migration pending / retained non-active safety archive** | `Mikayilzade/last-known-shape` *(repository not yet created)* | **NOT STARTED** | Full `GAME7_*` safety copy remains non-active because destination repo returned Not Found on 2026-08-30. |
| 008 | **Locksmith's Margin** *(working title)* | **IN DESIGN / Phase 5 content architecture complete / Phase 6 ready** | TBD | **NOT STARTED** | 32-case target / 28-case quality floor; D01–D06 demo; F1–F8 content families; full solver/fairness/anti-isomorphism validator; 90 content acceptance tests. |

## Game #006 frozen identity
- G6C01 Stitchspace; PC/Steam-first premium systemic topology puzzle;
- scarce seam endpoint replacement rewires room adjacency; every new adjacency destroys old;
- C01–C34; deterministic domain; migration pending only.

## Game #007 frozen identity
- selected concept: **G7C02 Last Known Shape**;
- PC/Steam-first premium single-player/offline systemic observation/transformation puzzle;
- authored Observation Frames expose one exact deterministic Candidate; ordinary camera/pixels never control gameplay;
- Confirm writes persistent Remembered form; leaving observation resolves Remembered -> Physical authority;
- depth from preserve/overwrite, affordance conflict, access self-block, relocation, declared dynamic input, destructive re-observation, two-object order and state-dependent reuse;
- main campaign target C01–C34, strong-release target >=28 but filler forbidden; DEMO01–06; R01–R06 maximum/zero minimum;
- main campaign/demo hard ceiling: <=2 reasoning-critical remembered objects, <=1 dynamic input per Frame, <=4 relevant Frames/case, normally 2–3 useful forms/object;
- deterministic Domain Core, exact Undo/Redo, bounded solver/validator and physical state-readable UX;
- working $17.99 USD / $14.99–$19.99 empirical release-review band;
- Godot 4.7.2-stable / GDScript-first initial implementation baseline at freeze;
- `GAME7_FINAL_FREEZE.md` is final authority; **DESIGN COMPLETE = YES**.

## Game #008 selected identity
- selected concept: **G8C02 Locksmith's Margin**;
- PC/Steam-first premium single-player tactile systemic puzzle;
- file discrete irreversible cuts into a few persistent key blanks and use them across several locks;
- normal authority: 4–6 columns, depths 0..D with D<=5, <=3 blanks, <=6 required locks;
- each lock column is only a finite accepted depth set; exact/tolerance/master/wear all reduce to that authority;
- FILE increments one selected column by exactly one authoritative depth step;
- TEST evaluates columns left-to-right and exposes only the first blocker plus deterministic TOO_SHALLOW / TOO_DEEP / BETWEEN_BRANCHES relation; accepted prefix becomes known;
- tests are free and deterministic; repeated identical tests reveal nothing new;
- access restrictions are visible predicates over opened locks, never random/narrative permissions;
- opened locks stay completed even if the opening key is later destructively repurposed;
- unlimited exact Undo/Redo and Restart protect real-world time while forward puzzle state remains irreversible;
- depth progresses through overlap preservation, target partitioning, destructive diagnosis, master branches, wear bridges, access order and mixed finales;
- mature cases must defeat named cheap policies and pass both omniscient solvability and information-respecting fairness validation;
- no lockpicking/burglary, continuous dexterity filing, shop economy, roguelite progression, hidden realism exceptions or numeric-code memorization;
- Phase 3 authority: `GAME8_PRODUCT_THESIS.md`;
- Phase 4 authority: `GAME8_MECHANICAL_ARCHITECTURE.md` with **80 mechanical acceptance tests**;
- Phase 5 authority: `GAME8_CONTENT_ARCHITECTURE.md` with **90 content acceptance tests**, C01–C32 target spine, 28-case quality floor, D01–D06 demo and F1–F8 family/validator system;
- next: Phase 6 UX / Presentation Architecture.

## Game #008 tournament history
- Phase 1: 36 -> 10;
- Run 1: 10 -> 5;
- Run 2: 5 -> 3 finalists;
- final: Locksmith's Margin beat Window Garden and Firebreak Foreman;
- Window Garden rejected after direct plant/pruning-puzzle collision and higher deterministic-preview burden; fresh Aug-27-2026 Topiary metadata materially worsened its boundary;
- Firebreak Foreman rejected for wildfire-puzzle adjacency, larger solver/state surface, VFX/readability risk and tutorial primitive burden;
- rejected concepts are exclusion history only, not active Game #008 canon.

## Numbering rule
Use the next unused sequential number for every new factory design cycle. If a future design is killed before migration, record it here as `KILLED` with a concise reason.

## Migration / continuity rule
1. Dedicated repositories own implementation and future game-specific production work.
2. Never delete a finished game's factory safety copy before destination migration integrity is verified.
3. If the dedicated repository does not yet exist, mark that game `migration pending` and retain its `GAME<N>_*` files as a **frozen non-active safety archive**.
4. A migration-pending archive does **not** block the next sequential design slot.
5. `STATUS.md` must name exactly which numbered slot is active; older retained archives are never active canon for the new game.
6. When the dedicated repository later becomes available, migrate and verify that game's archive independently, then remove only that completed game's retained files.