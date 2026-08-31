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
| 008 | **Locksmith's Margin** *(working title)* | DESIGN COMPLETE / migration pending / retained non-active safety archive | `Mikayilzade/locksmiths-margin` *(not yet created)* | NOT STARTED | Final authority `GAME8_FINAL_FREEZE.md`; frozen Game #008 files remain non-active. |
| 009 | **Binder's Imposition** *(working title)* | **IN DESIGN / Phase 8 Technical Specification complete / Phase 9 ready** | TBD | NOT STARTED | Active technical authority is `GAME9_TECHNICAL_SPECIFICATION.md`; working title remains storefront-unfrozen. |

## Game #009 current identity
- selected concept: **G9C02 Binder's Imposition**;
- PC/Steam-first premium single-player/offline systemic permutation/constraint puzzle;
- one-sentence hook: arrange pages on flat sheets so that after they fold, flip, nest and trim, the finished book reads exactly right;
- core reasoning object: deterministic transform from reversible flat sheet/signature assignments and nesting roles to final bound-face positions/orientations;
- frozen mechanical domain: `PageFace`, `FlatSlot`, `Signature`, `FoldTemplate`, resolved `BoundBookState`;
- deterministic resolution order: legality -> local fold -> duplex orientation -> nesting -> leaf/facing -> trim -> constraints -> exact explanation;
- base transform grammar: T4, T4F, T8 and T6P;
- depth comes from intersecting final-book constraints rather than hidden printing rules;
- player editing remains reversible; Fold Preview is non-mutating and mathematically identical to Commit's transform;
- ordinary campaign ceiling: normally <=20 faces, <=3 signatures, <=4 secondary predicate families and <=2 template choices per signature;
- no real print-shop calibration or vocational-training requirement;
- compact workbench scope; no avatar locomotion, shop economy, deckbuilding, roguelite wrapper, multiplayer, MTX or live-service baseline;
- content count policy: **24 certified strong cases minimum / 30 target / 34 soft ceiling**;
- six-chapter content arc and 12 bounded content families are solver-certified/data-driven; authored campaign, no runtime procedural-content promise;
- frozen demo is D01–D06 / 6 real campaign cases / target 20–30 minutes;
- workbench UX is source+goal persistent with mouse click-select-click baseline and discrete-focus controller parity;
- Fold Preview is non-mutating/skippable with Normal/Fast/Instant and Reduced Motion; incorrect Commit explains final failed relationships without giving source moves;
- accessibility includes remapping, controller parity, non-precision alternatives, reduced motion, text scaling, color/audio redundancy;
- 1280x800 is first-class handheld layout; important default text targets >=12 px;
- commercial model is one-time premium complete baseline game: no MTX, ads, paid hints, grind bypass, progression currency or live-service obligation;
- current design-stage USD list-price band **$14.99–$19.99**, preferred planning point **$17.99 pending final empirical validation**;
- progression is authored chapter-gated with small prerequisite-safe local branches; no XP/currency/star gate;
- optional badge vocabulary: Predicted / Direct Bind / Constraint Craft; badges never gate campaign and accessibility is never penalized;
- Steam achievement target 14–18 (planning set 16); Steam Cloud + Achievements baseline;
- D01–D06 demo transfers versioned progress to full game; achievements reconcile idempotently in full build;
- post-campaign retention is finite replay/mastery only;
- `Binder's Imposition` remains internal/working title pending storefront comprehension/collision/legal validation;
- localization-safe content may not depend on English spelling, word length or color-only information;
- Phase-8 technical authority recommends **Godot 4.x stable** by default, while keeping deterministic puzzle authority engine-independent; Unity remains an expertise/integration fallback;
- runtime state is separated into immutable content, editable WorkbenchState, derived BoundBookState, presentation state and persistent profile/campaign state;
- transforms/evaluation/explanations/solver certification have pure deterministic contracts and canonicalization rules;
- Undo/Redo uses semantic atomic transactions and survives normal reload within a bounded/full case-session history policy;
- saves are versioned, atomic, backed up and non-destructively recoverable; unknown future saves are never overwritten;
- demo/cloud merges are monotonic for safe campaign facts; divergent unsolved workbench branches are never structurally merged;
- achievements are recomputable/idempotent consequences of persistent facts;
- semantic input abstraction and animation-independent test mode are mandatory;
- release content passes schema -> transform -> solver -> relevance -> anti-isomorphism -> human review -> package manifest pipeline;
- **DESIGN COMPLETE = NO**; next phase is whole-game simulation on paper.

## Game #009 tournament history
- Phase 1: 36 candidates -> 10 entrants;
- Run 1: 10 -> 5;
- Run 2: 5 -> 3 finalists;
- Run 3 final: **Binder's Imposition** beat `Ink Trap Press` and `Paper Automata`;
- rejected concepts are exclusion/tournament history only, never active Game #009 canon.

## Frozen portfolio identities / exclusion summary
- #001 Organism Cargo: constrained living-cargo/ecology post-commit cascades.
- #002 False Map Department: bureaucracy/reality manipulation.
- #003 Borrowed Collision: property transfer.
- #004 HEARWALL: audio-hidden geometry.
- #005 Tension Budget: conserved-network load/tension redistribution.
- #006 Stitchspace: scarce topology rewiring where new adjacency destroys old.
- #007 Last Known Shape: observation -> exact candidate -> remembered/persistent transformed form.
- #008 Locksmith's Margin: destructive persistent fictional key-vector edits against several finite-set locks.

## Numbering rule
Use the next unused sequential number for every new factory design cycle. If a future design is killed before migration, record it here as `KILLED` with a concise reason.

## Migration / continuity rule
1. Dedicated repositories own implementation and future game-specific production work.
2. Never delete a finished game's factory safety copy before destination migration integrity is verified.
3. If the dedicated repository does not yet exist, mark that game `migration pending` and retain its `GAME<N>_*` files as a **frozen non-active safety archive**.
4. A migration-pending archive does not block the next sequential design slot.
5. `STATUS.md` names exactly which numbered slot is active; older retained archives are never active canon for the new game.
6. When a dedicated repository later becomes available, migrate and verify that game's archive independently, then remove only that completed game's retained files.
