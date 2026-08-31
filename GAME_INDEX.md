# GAME INDEX

This file tracks games produced by the reusable design factory. Dedicated repositories own implementation. Frozen completed games may remain temporarily as **non-active safety archives** when dedicated repositories do not yet exist; pending migration never blocks the next design slot.

| # | Game | Design status | Dedicated repository | Implementation status | Notes |
|---|---|---|---|---|---|
| 001 | **Organism Cargo** | DESIGN COMPLETE / migrated | `Mikayilzade/organism-cargo` | Dedicated implementation track | Migrated with autonomous implementation handoff. |
| 002 | **False Map Department** | DESIGN COMPLETE / migrated | `Mikayilzade/false-map-department` | Dedicated implementation track | Migration integrity verified; CI/email-noise guardrail included. |
| 003 | **Borrowed Collision** | DESIGN COMPLETE / migrated / integrity verified | `Mikayilzade/borrowed-collision` | Phase 12A ready | Frozen design package migrated. |
| 004 | **HEARWALL** *(working title)* | DESIGN COMPLETE / migrated / integrity verified | `Mikayilzade/hearwall` | Phase 12A ready | Dedicated handoff verified. |
| 005 | **Tension Budget** *(internal label)* | DESIGN COMPLETE / migrated / integrity verified | `Mikayilzade/tension-budget` | Phase 12A ready | Dedicated authority/handoff/CI policy present. |
| 006 | **Stitchspace** *(working title)* | DESIGN COMPLETE / migration pending / retained non-active safety archive | `Mikayilzade/stitchspace` *(not yet created)* | NOT STARTED | Frozen Game #006 files remain non-active. |
| 007 | **Last Known Shape** *(working title)* | DESIGN COMPLETE / migration pending / retained non-active safety archive | `Mikayilzade/last-known-shape` *(not yet created)* | NOT STARTED | Frozen Game #007 files remain non-active. |
| 008 | **Locksmith's Margin** *(working title)* | DESIGN COMPLETE / migration pending / retained non-active safety archive | `Mikayilzade/locksmiths-margin` *(not yet created)* | NOT STARTED | Final authority `GAME8_FINAL_FREEZE.md`; frozen files non-active. |
| 009 | **Binder's Imposition** *(working title)* | DESIGN COMPLETE / migration pending / retained non-active safety archive | `Mikayilzade/binders-imposition` *(not yet created)* | NOT STARTED | Final authority `GAME9_FINAL_FREEZE.md`; frozen files non-active. |
| 010 | **Luggage Carousel Zero** *(working title)* | **IN DESIGN / Phase 5 active** | TBD | NOT STARTED | 42-slot campaign map and 7-case demo path defined; exact demo finale validated; GAP/blank-tick family undergoing bounded adversarial validation before Phase-5 closure. |

## Game #010 state
- Phase 1: complete; 40 concepts generated, 12 tournament entrants.
- Phase 2: complete; Luggage Carousel Zero selected over Stencil Orchard and Inventory Eclipse in Round C.
- Phase 3: complete; authority `GAME10_THESIS.md`.
- Phase 4: **complete with authoritative correction**; base authority `GAME10_MECHANICS.md`, corrected by `GAME10_MECHANICS_CORRECTION.md`.
- Mechanical correction: labels may be swapped **only across adjacent ring sockets**. The old arbitrary-transposition rule was proven to collapse non-pickup label positions into irrelevant storage, undermining staging, duplicate-label phase and K=2 depth. The correction restores spatial label planning without adding a new verb.
- Phase 5: **active**; base authority `GAME10_CONTENT.md`, concrete map `GAME10_CONTENT_MAP.md`, validation authority `GAME10_CONTENT_VALIDATION.md`.
- Campaign map: 42 target slots = A7/B8/C8/D9/E10; K0 early-only, K2 exactly three bounded mastery slots; 12 late-game relationship skeletons defined.
- Demo: cases 01–06 hand-traced; Demo 04 tick target repaired 4->5; Demo 07 exact N5/K1/T7 finale now validated with required scarce-bag intentional miss and `STAGING_SIGNIFICANT` non-pickup local swap.
- GAP clarification: no compression means a GAP never shifts another bag's socket phase. Its meaningful effect is a persistent **empty pickup phase** plus absence of the consumed bag on later circuits. F7 can only count when the blank tick itself changes adjacent-label scheduling/feasibility.
- F7 floor is provisional pending exact proof of >=3 materially distinct blank-tick scheduling cases; if weak, Act D will be rebalanced rather than rescued with new mechanics.
- Frozen identity: moving bag/gap permutation + fixed socket labels + exactly one pickup + public ordered passengers + bounded **adjacent** label swaps + finite ticks.
- Predicate ceiling: AND of 1–3 positive equality clauses over exactly socket LABEL, BAG_SHAPE and BAG_MARK; one clause/dimension; no hidden logic/OR/NOT/history.
- Budget model: per-case ticks plus case-static swaps-per-tick {0,1,2}; no cumulative swap currency.
- Solver envelope: K=1 standard up to N=8; K=2 mastery restricted to N<=6/ticks<=8; K=0 short teaching only; exact certification mandatory.
- Current content metrics: `STAGING_SIGNIFICANT`, `DUPLICATE_POSITION_SIGNIFICANT`, `K2_SIGNIFICANT`, plus guarded blank-tick/GAP significance under Phase-5 validation.
- Previous games and eliminated Game #010 concepts remain exclusion/history only and may not silently become canon.

## Frozen portfolio identities / exclusion summary
- #001 Organism Cargo: constrained living-cargo/ecology post-commit cascades.
- #002 False Map Department: bureaucracy/reality manipulation.
- #003 Borrowed Collision: property transfer.
- #004 HEARWALL: audio-hidden geometry.
- #005 Tension Budget: conserved-network load/tension redistribution.
- #006 Stitchspace: scarce topology rewiring where new adjacency destroys old.
- #007 Last Known Shape: observation -> exact candidate -> remembered/persistent transformed form.
- #008 Locksmith's Margin: destructive persistent fictional key-vector edits against several finite-set locks.
- #009 Binder's Imposition: reversible flat-sheet/signature assignment through deterministic fold/nest/trim transforms against final-book constraints.

## Numbering rule
Use the next unused sequential number for every new factory design cycle. If a future design is killed before migration, record it here as `KILLED` with a concise reason.

## Migration / continuity rule
1. Dedicated repositories own implementation and future game-specific production work.
2. Never delete a finished game's factory safety copy before destination migration integrity is verified.
3. If the dedicated repository does not yet exist, mark that game `migration pending` and retain its `GAME<N>_*` files as a **frozen non-active safety archive**.
4. A migration-pending archive does not block the next sequential design slot.
5. `STATUS.md` names exactly which numbered slot is active; older retained archives are never active canon for the new game.
6. When a dedicated repository later becomes available, migrate and verify that game's archive independently, then remove only that completed game's retained files.