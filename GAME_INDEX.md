# GAME INDEX

This file tracks games produced by the factory. Finished game-specific design should normally leave this repository after verified migration. A completed package may remain temporarily as a safety archive while dedicated-repository migration is being verified; it is not canon for the next design cycle.

| # | Game | Design status | Dedicated repository | Implementation status | Notes |
|---|---|---|---|---|---|
| 001 | **Organism Cargo** | DESIGN COMPLETE / specification frozen | `Mikayilzade/organism-cargo` | Dedicated implementation track | Migrated with full design canon, validation/history and autonomous implementation handoff. |
| 002 | **False Map Department** | DESIGN COMPLETE / specification frozen / migrated | `Mikayilzade/false-map-department` | Dedicated implementation track | Migrated and integrity-verified; autonomous implementation handoff and CI/email-noise guardrail included. |
| 003 | **Borrowed Collision** | DESIGN COMPLETE / Phase 11 frozen | `Mikayilzade/borrowed-collision` | Dedicated migration/handoff track | Factory source package temporarily retained as non-canonical safety archive. |
| 004 | **HEARWALL** *(working commercial title)* | **DESIGN COMPLETE / Phase 11 frozen / migrated / integrity verified** | `Mikayilzade/hearwall` | Phase 12A ready / production implementation not started | Top-down real-time acoustic infiltration puzzle. Destination final-freeze blob exactly matches factory source SHA `37fbe588f82b65deeeb734597ffe768bb5399dd0`. |
| 005 | **TBD — tournament queued** | **Phase 1 Opportunity Discovery COMPLETE / Phase 2 queued** | — | Not applicable; design factory only | 60 clean-slate seeds researched. Phase-2 entrants: G5C02 Tension Budget, G5C37 Zero-G Tool Orbit, G5C17 Door Memory, G5C21 Broken Rule Workshop. No winner selected. |

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
Migration to `Mikayilzade/hearwall` was completed and verified on 2026-08-22.

Verification facts:
- dedicated repository exists on `main`;
- all 16 frozen design/history files plus four implementation-handoff files and README were migrated;
- destination `PHASE11_FINAL_FREEZE.md` blob SHA is exactly `37fbe588f82b65deeeb734597ffe768bb5399dd0`, identical to the factory source reference;
- authority chain is self-contained inside the dedicated repository;
- destination `IMPLEMENTATION_STATUS.md` records migration VERIFIED and Phase 12A READY / NOT STARTED;
- destination CI/notification guardrail is present;
- production implementation remains outside the factory.

The Game #004 source/handoff package was removed from the factory only after this verification. `HEARWALL` remains a screened working title, **not legal trademark clearance**. A later legal/store/domain rename is allowed without changing gameplay canon.

## Game #005 current discovery/tournament state
Phase 1 completed after three destructive research runs and a total field of **60 seeds**. Attractive ideas were removed when direct precedent, content inflation, expensive simulation or weak hour-5 depth outweighed their GIF appeal.

### Phase-2 tournament entrants
- **G5C02 Tension Budget** — move one physical anchor; a fixed discrete tension budget redistributes across several visible connected loads, changing multiple mechanisms at once. Main tournament risk: teaching/readability without numeric or graph UI.
- **G5C37 Zero-G Tool Orbit** — place one carried tool onto predictable authored local orbit tracks; the tool persists as a periodic second actor while the player independently moves, catches and transfers it. Main tournament risk: controller/catch feel and late-game `switch hitting` repetition.
- **G5C17 Door Memory** — a memory door and crossing eligible object swap binary HEAVY/LIGHT state, coupling spatial order with object capability. Main tournament risk: full-campaign ceiling without adding property families or box-hauling friction.
- **G5C21 Broken Rule Workshop** — change exactly one physical rule cartridge in a live deterministic machine, run it, observe the causal failure and diagnose/revise. Main tournament risk: bespoke machine authoring and drift into programming/editor homework.

### Important Phase-1 removals
- G5C05 Shadow Scaffold — hard-killed by direct solid-shadow traversal precedent.
- G5C09 Rain Router — removed by current water-routing precedent + consumer inflation.
- G5C14 Routine Possession — hard-killed by direct embodied record/repeat automation precedent.
- G5C45 Thermal Footprint — hard-killed after 2026 `TrailRail` pressure on movement-trail-as-world-material plus execution/consumer inflation.
- G5C41 Crowd Umbrella — cut because hour-5 depth required disproportionate crowd/NPC complexity.
- G5C01 Frame Pin — cut because mature play converged on familiar object-time-freeze phase selection.
- G5C25 Sunpatch Garden — cut because mature variety depended on ecological consumer catalogue and pacing compromise.
- G5C10 Pressure Line — cut because it lost directly to Tension Budget on world readability/ownability and drifted toward pipe-editor abstraction.

No Game #005 winner exists yet. `GAME5_RESEARCH.md`, `GAME5_RESEARCH_RUN2.md` and `GAME5_RESEARCH_RUN3.md` remain the active evidence chain under `STATUS.md`. Phase 2 must compare the four entrants under one equal destructive tournament rubric.

## Final Game #004 tournament reserves
- **G4C01 Seam Thief** — strongest pure abstract puzzle reserve; lost selection on portal perception + topology/contact QA risk.
- **G4C43 Command Wake** — strongest action-puzzle reserve; lost selection on route memorization/choreography + visual readability.
- Other earlier survivors/reserves remain historical research only and are not co-canon with HEARWALL.

## Numbering rule
Use the next unused sequential game number for every new factory design cycle, whether the concept later ships or is killed. If a design is abandoned before migration, record it here as `KILLED` with a short reason so the factory does not accidentally rediscover it as if it were new.

## Migration rule
A game receives its own repository once its design is sufficiently stable to justify migration, normally at `DESIGN COMPLETE = YES`. The dedicated repo owns implementation and future game-specific work. The factory returns to a clean logical design slot afterward. Temporary safety archives from a prior game may coexist only when explicitly marked non-canonical and excluded from the current recovery chain.
