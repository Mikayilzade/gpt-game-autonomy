# GAME INDEX

This file tracks games produced by the factory. Finished game-specific design should normally leave this repository after verified migration. A completed package may remain temporarily as a safety archive while dedicated-repository migration is being verified; it is not canon for the next design cycle.

| # | Game | Design status | Dedicated repository | Implementation status | Notes |
|---|---|---|---|---|---|
| 001 | **Organism Cargo** | DESIGN COMPLETE / specification frozen | `Mikayilzade/organism-cargo` | Dedicated implementation track | Migrated with full design canon, validation/history and autonomous implementation handoff. |
| 002 | **False Map Department** | DESIGN COMPLETE / specification frozen / migrated | `Mikayilzade/false-map-department` | Dedicated implementation track | Migrated and integrity-verified; autonomous implementation handoff and CI/email-noise guardrail included. |
| 003 | **Borrowed Collision** | DESIGN COMPLETE / Phase 11 frozen | `Mikayilzade/borrowed-collision` | Dedicated migration/handoff track | Factory source package temporarily retained as non-canonical safety archive. |
| 004 | **HEARWALL** *(working commercial title)* | **DESIGN COMPLETE / Phase 11 frozen / migration blocked** | Intended: `Mikayilzade/hearwall` | Not started; Phase 12A only after verified migration | Top-down real-time acoustic infiltration puzzle. Final-freeze blob SHA `37fbe588f82b65deeeb734597ffe768bb5399dd0`. Destination repository not found as of 2026-08-21. |

## Completed Game #002 identity
**False Map Department** — ontological cartography puzzle: editing the official map immediately rewrites the tiny world, and success requires solving civic goals without creating worse second-order consequences.

## Completed Game #003 identity
**Borrowed Collision** — systemic causal puzzle in which a real resolved collision creates a portable impact whose direction, magnitude and lineage can be physically routed and spent elsewhere, including to create further real collision consequences.

## Completed Game #004 identity
**HEARWALL** — working commercial title for a top-down real-time acoustic infiltration puzzle where the player physically repositions one soundproof barrier so the right listener hears an action while the wrong listener does not, then exploits the deterministic reaction to infiltrate.

### Game #004 frozen product rules
- PC/Steam-first; single-player/offline baseline.
- One local/direct physical barrier on authored rails/snap slots.
- Exact deterministic graph acoustics shown in the physical world.
- Strength 1–4; base attenuation 0–2; listener thresholds 1–3; barrier +3.
- Tied minimum routes are mechanically real and equally presented.
- Prediction and committed hearing use the same solver; parity must be 100%.
- Useful hearing/selective audibility is mandatory campaign language.
- Maximum **two listeners across all 1.0 content**; three-listener gameplay is cut.
- Direct detection is bounded deterministic secondary pressure, not a twitch-stealth/combat pillar.
- Complete visual/no-audio decision parity.
- Main campaign target **34 encounters**; **8 optional remixes** are first-cut if repetition evidence is poor.
- Premium one-time purchase; no progression currency/power grind/live service.
- Current empirical price range $14.99–$19.99; final price not frozen.
- Godot 4.7.1-stable / GDScript-first / deterministic Domain Core implementation direction.
- Mandatory mature-content validators include V17 safe-preview enumeration and V18 systemic-signature deduplication.
- BEFORE_MUTATION events own immutable pre-commit graph revisions; AFTER_MUTATION uses post-commit revisions.

### Game #004 migration state
`GAME4_PHASE11_FINAL_FREEZE.md` is the highest factory authority and sets `DESIGN COMPLETE = YES` after a 48/48 implementation-readiness pass.

Factory-side migration/handoff files are prepared:
- `GAME4_IMPLEMENTATION_START_HERE.md`
- `GAME4_IMPLEMENTATION_STATUS.md`
- `GAME4_CI_NOTIFICATION_POLICY.md`
- `GAME4_MIGRATION_MANIFEST.md`

The intended dedicated repository `Mikayilzade/hearwall` was not found through the connected GitHub view on 2026-08-21, and repository creation is not exposed by the available connector actions. Therefore the factory retains all Game #004 files and must not start production implementation or reset to Game #005 until migration integrity is verified.

`HEARWALL` is a screened working title, **not legal trademark clearance**. A later legal/store/domain rename is allowed without changing gameplay canon.

## Final Game #004 tournament reserves
- **G4C01 Seam Thief** — strongest pure abstract puzzle reserve; lost selection on portal perception + topology/contact QA risk.
- **G4C43 Command Wake** — strongest action-puzzle reserve; lost selection on route memorization/choreography + visual readability.
- Other earlier survivors/reserves remain historical research only and are not co-canon with HEARWALL.

## Numbering rule
Use the next unused sequential game number for every new factory design cycle, whether the concept later ships or is killed. If a design is abandoned before migration, record it here as `KILLED` with a short reason so the factory does not accidentally rediscover it as if it were new.

## Migration rule
A game receives its own repository once its design is sufficiently stable to justify migration, normally at `DESIGN COMPLETE = YES`. The dedicated repo owns implementation and future game-specific work. The factory returns to a clean logical design slot afterward. Temporary safety archives from a prior game may coexist only when explicitly marked non-canonical and excluded from the current recovery chain.
