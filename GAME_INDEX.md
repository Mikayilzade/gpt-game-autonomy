# GAME INDEX

This file tracks games produced by the factory. Finished game-specific design should normally leave this repository after verified migration. A completed package may remain temporarily as a safety archive while dedicated-repository migration is being verified; it is not canon for the next design cycle.

| # | Game | Design status | Dedicated repository | Implementation status | Notes |
|---|---|---|---|---|---|
| 001 | **Organism Cargo** | DESIGN COMPLETE / specification frozen | `Mikayilzade/organism-cargo` | Dedicated implementation track | Migrated with full design canon, validation/history and autonomous implementation handoff. |
| 002 | **False Map Department** | DESIGN COMPLETE / specification frozen / migrated | `Mikayilzade/false-map-department` | Dedicated implementation track | Migrated and integrity-verified; autonomous implementation handoff and CI/email-noise guardrail included. |
| 003 | **Borrowed Collision** | DESIGN COMPLETE / Phase 11 frozen | `Mikayilzade/borrowed-collision` | Dedicated migration/handoff in progress; prototype-first implementation gate | Final-freeze SHA in factory: `d227433d40d4a8e73334702833b099befb25a2b0`. Factory source package temporarily retained as safety archive until dedicated migration verification is fully closed. |
| 004 | **HUSHLINE** *(provisional; high-risk for final use / title not cleared)* | **Phase 1–7 COMPLETE; Product Thesis, Mechanics, Content, UX/Presentation and Commercial Model LOCKED; Phase 8 queued** | TBD after design freeze | Not applicable | Top-down real-time acoustic infiltration puzzle. 34 main encounters + 8 optional remixes; premium one-time purchase; current price test range $14.99–$19.99; world-first acoustic prediction and complete no-audio parity locked. |

## Completed Game #002 identity
**False Map Department** — ontological cartography puzzle: editing the official map immediately rewrites the tiny world, and success requires solving civic goals without creating worse second-order consequences.

## Completed Game #003 identity
**Borrowed Collision** — systemic causal puzzle in which a real resolved collision creates a portable impact whose direction, magnitude and lineage can be physically routed and spent elsewhere, including to create further real collision consequences.

The dedicated repositories own all implementation and game-specific amendments for Games #001–#003 once migration/handoff is verified. Game #004 must not treat their specific mechanics, content, files or rejected candidate fields as canon.

## Game #004 locked Product Thesis summary
`HUSHLINE` is a provisional continuity name only and now carries material naming-conflict risk; final commercial title remains unresolved.

Locked identity:
- **top-down real-time acoustic infiltration puzzle**;
- PC/Steam-first, single-player/offline baseline;
- physically and **locally/directly** reposition one visible soundproof barrier between authored slots;
- exact deterministic acoustic propagation is shown in the physical world;
- decide **who should hear each action**, not merely how to remain silent;
- deliberate lures/selective audibility are mandatory mature play;
- player-created acoustic openings take priority over passive patrol waiting;
- complete visual/no-audio decision parity;
- graph acoustics rather than realistic/ray-traced wave simulation;
- compact premium scope, approximately 5–8 hours first clear and 34 main encounters.

## Game #004 locked mechanical summary
- Acoustic graph uses visible physical nodes/edges, attenuation 0–2, sound strength 1–4 and visible listener thresholds 1–3.
- Hearing uses minimum route attenuation; all tied minimum routes count and are previewed.
- One local/direct rail-bound barrier adds +3 attenuation only while snapped to one authored edge slot.
- Hearing drives deterministic investigation rather than automatic failure; equal-strength lure spam cannot endlessly retarget an investigating listener.
- Fixed-step ordering and one shared prediction/resolution model require 100% deterministic hearing parity.
- Fast deterministic restart/checkpoint recovery is part of the core mechanical contract.

## Game #004 locked content summary
- **34 main encounters**: 7 teaching, 9 combination, 13 mature, 5 climax.
- **8 optional remix/mastery encounters**, with no parallel currency/power progression.
- 12 reusable reasoning families use only locked mechanics.
- Normal mature density remains 2 listeners and <=12 acoustic nodes; 3 listeners exceptional.
- Content validators reject hidden edges, unsignaled thresholds, permanent nearest-door dominance, silence-everything collapse, excessive waiting, barrier scarcity, excessive density, bespoke rule exceptions and repetitive encounter signatures.
- Selective audibility must appear by E07; mature campaign repeatedly requires useful heard events and listener-specific outcomes.
- Four-encounter ~20-minute demo culminates in selective audibility and physical barrier repositioning.

## Game #004 locked UX / presentation summary
- World-first top-down physical infiltration presentation; acoustics stay embedded in doors/corridors rather than a detached graph view.
- Source strength, passage attenuation, barrier effect and listener thresholds use redundant numeric-free shape/count/pattern language; optional explicit numbers are nonessential.
- Every tied minimum acoustic route is shown with equal mechanical emphasis.
- Prediction and committed propagation use the same visual grammar with explicit HEARS / DOES_NOT_HEAR outcomes.
- Barrier interaction is local, tactile, rail-constrained and live; between slots it is visibly acoustically inactive until snap.
- Listener hearing/investigation and direct detection/failure are distinct visual systems.
- Minimal HUD; no baseline minimap graph, suspicion bar, sound meter, inventory or barrier resource system.
- Keyboard/mouse and controller are equal first-class targets, fully remappable and free of pixel-precision requirements.
- Complete no-audio decision parity, color-independent motifs, high contrast, reduced motion, text/icon scaling and deterministic whole-simulation speed assists are designed in.
- Failure/cause traces explain why a listener heard or detected the player without hidden information.
- Store/trailer identity must communicate physical selective audibility — one listener hears, another is screened — rather than generic sound stealth.
- Three-listener exceptional content remains an empirical readability gate and may be cut rather than rescued with abstract UI.

## Game #004 locked commercial summary
- Premium one-time purchase; no currency, power grind or live-service retention.
- Current USD price test range: **$14.99–$19.99**; provisional planning anchor **$17.99**.
- 1.0 value remains **34 main + 8 optional remixes / 5–8h first clear**.
- Commercial demo: four curated encounters / about 20 minutes, ending on selective audibility.
- Demo achievements disabled; settings/completion metadata continuity preferred when practical.
- Retention comes from learning, mastery and remixes rather than grind.
- Steam achievement target: **18–24**.
- Steam Cloud, controller support and handheld readability are high platform priorities.
- Preferred launch discount: **10%**, with 10–15% acceptable for 7–14 days.
- Early Access is not baseline.
- Paid power, consumables, gambling, energy, battle passes, ads, FOMO and artificial wait friction are explicitly excluded.
- `HUSHLINE` is provisional and now a likely replacement candidate after fresh web search found active conflicting uses; real title clearance remains mandatory before final lock.

The historical label `Soundproof Smuggler` is retired from active design. Cargo, contraband, delivery economy and logistics are not part of the locked thesis.

## Final Game #004 tournament reserves
- **G4C01 Seam Thief** — strongest pure abstract puzzle reserve; lost selection on portal perception + topology/contact QA risk.
- **G4C43 Command Wake** — strongest action-puzzle reserve; lost selection on route memorization/choreography + visual readability.
- Other earlier survivors/reserves remain historical research only and are not co-canon with the selected concept.

## Numbering rule
Use the next unused sequential game number for every new factory design cycle, whether the concept later ships or is killed. If a design is abandoned before migration, record it here as `KILLED` with a short reason so the factory does not accidentally rediscover it as if it were new.

## Migration rule
A game receives its own repository once its design is sufficiently stable to justify migration, normally at `DESIGN COMPLETE = YES`. The dedicated repo owns implementation and future game-specific work. The factory returns to a clean logical design slot afterward. Temporary safety archives from a prior game may coexist only when explicitly marked non-canonical and excluded from the current recovery chain.
