# GAME INDEX

This file tracks games produced by the factory. Finished game-specific design should not remain in this repository after verified migration.

| # | Game | Design status | Dedicated repository | Implementation status | Notes |
|---|---|---|---|---|---|
| 001 | **Organism Cargo** | DESIGN COMPLETE / specification frozen | `Mikayilzade/organism-cargo` | Not started; Phase 12A queued | Migrated 2026-08-18 with full design canon, validation/history and autonomous implementation handoff. |
| 002 | **False Map Department** | DESIGN COMPLETE / specification frozen / migrated | `Mikayilzade/false-map-department` | Not started; Phase 12A queued | Migrated and integrity-verified 2026-08-19; includes autonomous implementation handoff and CI/email-noise guardrail. |
| 003 | TBD | Not started | TBD after design freeze | Not applicable | Next factory design slot. |

## Completed Game #002 identity
**False Map Department** — ontological cartography puzzle: editing the official map immediately rewrites the tiny world, and success requires solving civic goals without creating worse second-order consequences.

Technical direction frozen in its dedicated repository: **Godot 4.7.1-stable, GDScript-first, deterministic 2D domain separated from presentation.**

The dedicated repository now owns all future Game #002 implementation/design-amendment work. The factory must not use its old files as canon for Game #003.

## Numbering rule
Use the next unused sequential game number for every new factory design cycle, whether the concept later ships or is killed. If a design is abandoned before migration, record it here as `KILLED` with a short reason so the factory does not accidentally rediscover it as if it were new.

## Migration rule
A game receives its own repository once its design is sufficiently stable to justify migration, normally at `DESIGN COMPLETE = YES`. The dedicated repo owns implementation and future game-specific work. The factory returns to a clean design slot afterward.
