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
| 009 | **Binder's Imposition** *(working title)* | **IN DESIGN / Phase 10 Adversarial Review complete / Phase 11 ready** | TBD | NOT STARTED | Current repair authority `GAME9_ADVERSARIAL_REVIEW.md`; DESIGN COMPLETE remains NO. |

## Game #009 current identity
- selected concept: **G9C02 Binder's Imposition**;
- PC/Steam-first premium single-player/offline systemic permutation/constraint puzzle;
- one-sentence hook: arrange pages on flat sheets so that after they fold, flip, nest and trim, the finished book reads exactly right;
- core reasoning object: deterministic transform from reversible flat sheet/signature assignments and nesting roles to final bound-face positions/orientations;
- frozen mechanical domain: `PageFace`, `FlatSlot`, `Signature`, `FoldTemplate`, resolved `BoundBookState`;
- deterministic resolution order: legality -> local fold -> duplex orientation -> nesting -> leaf/facing -> trim -> constraints -> exact explanation;
- base transform grammar remains T4, T4F, T8 and T6P only;
- **T4F NORMAL** local order `[A1,B0,B1,A0]`; **T4F FLIPPED** exact source order `[B1,A0,A1,B0]` plus orientation flip bit XOR;
- **T8** local order `[A3,B0,A2,B1,B2,A1,B3,A0]` with its visible frozen orientation pattern;
- **T6P** uses T8 pre-trim order, cuts local positions `0` and `7` = source slots `A3` and `A0`, leaving `[B0,A2,B1,B2,A1,B3]`; REQUIRED_BLANK is not legal in cut slots;
- mixed-size nesting is exact recursive composition: each outer signature contributes its front half, then the entire inner book, then its back half;
- depth comes from intersecting final-book constraints rather than hidden printing rules;
- player editing remains reversible; Fold Preview is non-mutating and mathematically identical to Commit's transform;
- **Phase-10 Preview repair:** ordinary Preview exposes the complete resolved physical book and inspectable facts but does not automatically paint the full authored predicate list true/false, expose a correctness count, solver distance or warmer/colder branch vector;
- Commit remains exact all-failed-predicates feedback and same-state failed Commit remains idempotent;
- ordinary campaign ceiling remains normally <=20 faces, <=3 signatures, <=4 secondary predicate families and <=2 template choices per signature;
- no real print-shop calibration or vocational-training requirement;
- compact workbench scope; no avatar locomotion, shop economy, deckbuilding, roguelite wrapper, multiplayer, MTX or live-service baseline;
- content count policy remains **24 certified strong cases minimum / 30 target / 34 soft ceiling including shipped Mastery Shelf variants**;
- structural anti-isomorphism is now supplemented by **reasoning-skeleton diversity**: no more than four shipped strong cases may share one ordered reasoning skeleton after cosmetic renaming, and late chapters require primary-family diversity;
- six-chapter content arc and 12 bounded content families remain solver-certified/data-driven; authored campaign, no runtime procedural-content promise;
- canonical demo mapping remains **D01..D06 = G9_C01..G9_C06**; D04 fixed-role two-signature bridge, D05 first free nesting + one facing relation, D06 material/signature-role synthesis;
- frozen demo remains six real campaign cases with 20–30 minute median target, now backed by D04–D06 pacing/comprehension empirical gates;
- workbench UX remains source+goal persistent with mouse click-select-click baseline and discrete-focus controller parity;
- 1280x800 remains first-class; when text/layout pressure prevents all signatures being comfortably editable, a **focused-signature** full-size view plus compact Outer->Inner overview is the canonical fallback;
- Fold Preview is non-mutating/skippable with Normal/Fast/Instant and Reduced Motion; same-state previews reveal no additional mechanical information;
- incorrect Commit explains final failed relationships without giving source moves; identical unchanged failed Commit does not increment attempt stats again;
- accessibility includes remapping, controller parity, non-precision alternatives, reduced motion, text scaling, color/audio redundancy;
- commercial model remains one-time premium complete baseline game: no MTX, ads, paid hints, grind bypass, progression currency or live-service obligation;
- current design-stage USD list-price band **$14.99–$19.99**, preferred planning point **$17.99 pending final empirical validation**; price is not gameplay authority;
- progression remains authored chapter-gated with small prerequisite-safe local branches; no XP/currency/star gate;
- optional badge vocabulary remains Predicted / Direct Bind / Constraint Craft; badges never gate campaign and accessibility is never penalized;
- Direct Bind now has exact semantics: requires at least one resolved Preview and then zero distinct failed Commit states before success; same-state reopens do not count;
- Steam achievement target 14–18 (planning set 16); Steam Cloud remains a release target, but unsafe Cloud must be disabled rather than risk save loss;
- D01–D06 demo transfers versioned progress to full game; repeated import is monotonic/idempotent and achievements reconcile from persistent facts;
- post-campaign retention is finite replay/mastery only;
- `Binder's Imposition` remains internal/working title pending storefront comprehension/collision/legal validation;
- localization-safe content may not depend on English spelling, word length or color-only information;
- Phase-8 technical authority recommends Godot 4.x stable by default while keeping deterministic puzzle authority engine-independent;
- runtime state remains separated into immutable content, editable WorkbenchState, derived BoundBookState, presentation state and persistent profile/campaign state;
- transforms/evaluation/explanations/solver certification have pure deterministic contracts and canonicalization rules;
- Undo/Redo uses semantic atomic transactions and survives normal reload; very long history may compact to an anchor snapshot plus retained recent tail without altering current WorkbenchState;
- saves are versioned, atomic, backed up and non-destructively recoverable; unknown future saves are never overwritten;
- successful Commit becomes authoritative only after durable local save verification; platform achievement calls are later/retryable consequences;
- cloud lineage requires unique revision IDs + parent revision IDs so clean descent can be distinguished from divergent offline branches;
- safe campaign facts merge monotonically across cloud branches; divergent unsolved workbench branches are never structurally merged;
- local durable save/recovery is required before cloud/platform work; custom distributed-state complexity may not block the vertical slice;
- stale content revisions use explicit deterministic migration when possible; otherwise old in-progress work is preserved as recovery archive before clean case restart;
- achievements are recomputable/idempotent consequences of persistent facts;
- semantic input abstraction and animation-independent test mode are mandatory;
- release content passes schema -> transform -> solver -> relevance -> anti-isomorphism -> reasoning-skeleton -> human review -> package manifest pipeline;
- whole-game simulation passed all 12 normal/hostile scenarios; Phase 10 then passed destructive review with bounded repairs;
- remaining empirical gates cover transform comprehension, hypothesis-vs-enumeration, demo load, T8 clerical errors, T6P clarity, content-depth proof, manipulation cost, handheld UX and persistence integrity;
- **DESIGN COMPLETE = NO**; next phase is Specification Freeze.

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