# GAME INDEX

This file tracks games produced by the factory. Finished game-specific design should normally leave this repository after verified migration. A completed package may remain temporarily as a safety archive while dedicated-repository migration is being verified; it is not canon for the next design cycle.

| # | Game | Design status | Dedicated repository | Implementation status | Notes |
|---|---|---|---|---|---|
| 001 | **Organism Cargo** | DESIGN COMPLETE / specification frozen | `Mikayilzade/organism-cargo` | Dedicated implementation track | Migrated with full design canon, validation/history and autonomous implementation handoff. |
| 002 | **False Map Department** | DESIGN COMPLETE / specification frozen / migrated | `Mikayilzade/false-map-department` | Dedicated implementation track | Migrated and integrity-verified; autonomous implementation handoff and CI/email-noise guardrail included. |
| 003 | **Borrowed Collision** | DESIGN COMPLETE / Phase 11 frozen | `Mikayilzade/borrowed-collision` | Dedicated migration/handoff in progress; prototype-first implementation gate | Final-freeze SHA in factory: `d227433d40d4a8e73334702833b099befb25a2b0`. Factory source package temporarily retained as safety archive until dedicated migration verification is fully closed. |
| 004 | TBD | **Phase 1 Opportunity Discovery COMPLETE; Phase 2 tournament queued** | TBD after design freeze | Not applicable | 48 seeds explored; seven Phase-1 survivors remain. No concept selected. |

## Completed Game #002 identity
**False Map Department** — ontological cartography puzzle: editing the official map immediately rewrites the tiny world, and success requires solving civic goals without creating worse second-order consequences.

## Completed Game #003 identity
**Borrowed Collision** — systemic causal puzzle in which a real resolved collision creates a portable impact whose direction, magnitude and lineage can be physically routed and spent elsewhere, including to create further real collision consequences.

The dedicated repositories own all implementation and game-specific amendments for Games #001–#003 once migration/handoff is verified. Game #004 must not treat their specific mechanics, content, files or rejected candidate fields as canon.

## Game #004 current Phase-1 survivors
- G4C01 Seam Thief
- G4C19 Soundproof Smuggler
- G4C11 Stagehand Zero
- G4C24 Debris Sculptor
- G4C47 Umbrella Engine
- G4C43 Command Wake
- G4C46 Inside-Out Safe

No Game #004 winner exists yet.

## Numbering rule
Use the next unused sequential game number for every new factory design cycle, whether the concept later ships or is killed. If a design is abandoned before migration, record it here as `KILLED` with a short reason so the factory does not accidentally rediscover it as if it were new.

## Migration rule
A game receives its own repository once its design is sufficiently stable to justify migration, normally at `DESIGN COMPLETE = YES`. The dedicated repo owns implementation and future game-specific work. The factory returns to a clean logical design slot afterward. Temporary safety archives from a prior game may coexist only when explicitly marked non-canonical and excluded from the current recovery chain.
