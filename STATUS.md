# FACTORY STATUS

Last updated: 2026-08-21
Repository: `Mikayilzade/gpt-game-autonomy`
Branch: `main`

## Factory state
- Reusable factory rules: **YES**
- Game #001 Organism Cargo: **DESIGN COMPLETE / dedicated repository**
- Game #002 False Map Department: **DESIGN COMPLETE / migrated**
- Game #003 Borrowed Collision: **DESIGN COMPLETE / Phase 11 frozen**
- Game #003 dedicated repository: **`Mikayilzade/borrowed-collision` exists**
- Game #003 factory source package: **RETAINED TEMPORARILY AS SAFETY ARCHIVE**
- Game #003 source final-freeze SHA: `d227433d40d4a8e73334702833b099befb25a2b0`
- Current design slot: **Game #004**
- Game #004 autonomous/manual design run count: **12**
- Game #004 concept selected: **YES — G4C19 acoustic-infiltration / physical sound-routing concept**
- Historical working title `Soundproof Smuggler`: **RETIRED from active design**
- Current working product name: **HUSHLINE — provisional / high-risk for final use / final title not frozen**
- Game #004 Phase 1 Opportunity Discovery: **COMPLETE**
- Game #004 Phase 2 Concept Tournament: **COMPLETE**
- Game #004 Phase 3 Product Thesis Lock: **COMPLETE / LOCKED**
- Game #004 Phase 4 Mechanical Architecture: **COMPLETE / LOCKED**
- Game #004 Phase 5 Content Architecture: **COMPLETE / LOCKED**
- Game #004 Phase 6 UX / Presentation Architecture: **COMPLETE / LOCKED**
- Game #004 Phase 7 Economy / Retention / Commercial Model: **COMPLETE / LOCKED**
- Game #004 Phase 8 Technical Implementation Specification: **COMPLETE / LOCKED**
- Game #004 Phase 9 Whole-Game Simulation on Paper: **QUEUED / NOT STARTED**
- Production implementation inside factory: **NO**

## Important transition exception
Game #004 continues while the Game #003 source package remains temporarily retained. All `GAME3_*` files are non-canonical safety archive material and are excluded from Game #004 recovery reading.

## Current phase
**Game #004 — Phase 8 COMPLETE / Phase 9 Whole-Game Simulation queued**

## Active temporary files — mandatory recovery read
1. `GAME4_RESEARCH.md`
2. `GAME4_RESEARCH_RUN2.md`
3. `GAME4_RESEARCH_RUN3.md`
4. `GAME4_TOURNAMENT.md`
5. `GAME4_TOURNAMENT_RUN2.md`
6. `GAME4_TOURNAMENT_RUN3.md`
7. `GAME4_PRODUCT_THESIS.md`
8. `GAME4_MECHANICS.md`
9. `GAME4_CONTENT.md`
10. `GAME4_UX_PRESENTATION.md`
11. `GAME4_ECONOMY_COMMERCIAL.md`
12. `GAME4_TECHNICAL_SPEC.md`

A fresh continuation session must read `START_HERE.md`, this `STATUS.md`, `GAME_INDEX.md`, and all twelve active Game #004 files above. Do not read `GAME3_*` files as Game #004 canon.

## Completed — Game #004 Run 12 / Phase 8 Technical Specification
1. Re-read the full active Game #004 recovery/authority chain and resumed exactly from the Phase-8 handoff.
2. Re-verified current tool/runtime evidence on 2026-08-21 using official sources only for technical decisions.
3. Confirmed **Godot 4.7.1-stable** (2026-07-14) as the initial pinned engine target; 4.7.2 remains RC and 4.8 remains development-only at this checkpoint.
4. Created `GAME4_TECHNICAL_SPEC.md` without changing any locked Phase-3–7 gameplay, content, UX or commercial rule.
5. Defined a four-layer architecture: deterministic Domain Core, Godot runtime/world binding, presentation, and platform adapters.
6. Defined a **60 Hz fixed-step authoritative simulation** with rendering interpolation separated from gameplay truth.
7. Defined stable IDs, integer acoustic math, quantized/fixed-point rule-critical motion and canonical state hashing so engine/render timing cannot become hidden authority.
8. Preserved the exact Phase-4 update order as one explicit domain runner rather than relying on SceneTree callback order.
9. Defined semantic/quantized input packets and a Godot InputMap boundary with separately persisted remaps.
10. Defined deterministic integer acoustic propagation, tied-minimum-route representation and stable route/result traces for <=12-node graphs.
11. Defined authored deterministic listener navigation and preferred custom kinematic player movement so node ownership, direct detection, replays and checkpoints remain reproducible.
12. Defined barrier/door/moving-source/listener implementation contracts preserving +3 snapped attenuation, between-slot inactivity, explicit emission phase and strict-greater retarget logic.
13. Defined prediction as a prospective cloned/copy-on-write domain state that invokes the **same** mutation/propagation/hearing code as committed resolution; 100% parity remains a hard gate.
14. Chose typed Godot custom `Resource` (`.tres`) authoring for content definitions plus explicit WorldBinding data, headless compilation and Phase-5 V01–V16 validation.
15. Added technical content invariants for ID/reference integrity, route-density bounds, checkpoint legality, emission-phase completeness, manifest compatibility and missing world bindings.
16. Defined separate machine-local settings, portable profile/settings and deterministic encounter-checkpoint scopes.
17. Defined versioned explicit save DTOs, atomic temp-write/replace behavior, one-generation backup recovery, content-manifest hashes and tested migration rather than arbitrary live-Node serialization.
18. Defined FULL / DEMO / DEV build flavors where mechanics remain identical and only content/platform gating differs.
19. Grounded demo/full continuity in current Steam documentation: separate demo App ID, optional shared Cloud storage, demo achievements disabled, full-game import only for verified compatible fields/content.
20. Isolated Steam achievements, Cloud, store overlay/full-app checks and rich presence behind a platform adapter; offline campaign progress remains authoritative locally.
21. Defined localization with stable text IDs, pseudolocalization and no localized strings inside gameplay logic.
22. Defined accessibility boundaries: presentation-only settings remain outside domain truth, while deterministic assists such as whole-simulation speed are included in replay/state metadata.
23. Defined structured event logs, deterministic replay fixtures, state hashes, unit/golden/content tests and property/fuzz tests comparing the production path solver against exhaustive small-graph oracles.
24. Defined save/recovery tests covering corruption fallback, schema migration, checkpoint parity and demo/full import safety.
25. Defined performance targets for normal <=12-node / 2-listener content and exceptional 3-listener content, with a 60 FPS / Steam Deck-class 1280×800 target assumption and sub-millisecond acoustic expectations.
26. Defined later dedicated-repository implementation order **12A–12H**, explicitly keeping production code out of the factory.
27. Preserved the anti-notification principle for later CI: local/headless validation first; no unstable every-push Actions until the suite is consistently green and a dedicated CI policy exists.
28. Added twelve empirical technical gates covering engine version, quantized movement feel, cross-platform replay, prediction latency, tied-route density, deterministic collision, handheld performance/readability, three-listener load, save migration, demo/full continuity, Steam-offline behavior and localization stress.
29. No production implementation was started.

## Locked Game #004 technical summary
- Initial engine target: **Godot 4.7.1-stable, GDScript-first**.
- Authoritative rules live in a deterministic Domain Core, not scene callbacks/render/audio/platform code.
- 60 Hz fixed-step domain simulation; rendering interpolates only.
- Integer acoustic truth + stable IDs/order; quantized/fixed-point rule-critical motion preferred.
- No free rigid-body physics authority required.
- Prediction clones prospective state and uses the exact committed solver.
- Listener navigation uses deterministic authored graph/path contracts.
- Typed `.tres` content authoring + world bindings + headless compiler/validators.
- Phase-5 V01–V16 are tooling gates, not documentation-only rules.
- Explicit versioned save DTOs, atomic write + backup recovery, content manifest hashes.
- FULL/DEMO/DEV share identical mechanics; build flavor gates content/platform behavior only.
- Steam integration is adapter-only; offline local progress remains valid.
- Demo achievements disabled; shared Cloud continuity supported where valid.
- Localization uses stable IDs; pseudolocalization required.
- Replays/state hashes/golden tests/property fuzzing are core verification tools.
- Normal target remains <=12 nodes / 2 listeners; 3 listeners exceptional and cuttable.
- Production implementation remains deferred to the dedicated repository after design freeze/migration.

## NEXT ACTION — GAME #004 PHASE 9 WHOLE-GAME SIMULATION ON PAPER
1. Create `GAME4_WHOLE_GAME_SIMULATION.md`.
2. Re-read the complete active authority chain including `GAME4_TECHNICAL_SPEC.md`.
3. Simulate first boot and accessibility setup through immediate player control.
4. Walk D01–D04 as an actual ~20-minute demo, checking first sound, first independent barrier choice, alternate-route comprehension, deliberate investigation and final selective-audibility clarity.
5. Continue into E01–E07 and prove the player understands `heard can be useful` by E07 without tutorial text dependence.
6. Simulate E08–E16 combination pacing, especially exposed barrier manipulation, first door mutation, over-propagation and two-step barrier sequencing.
7. Simulate mature E17–E29, including retarget ordering, moving source introduction, return-path inversion and passive-wait/verb-frequency budgets.
8. Simulate exceptional E28/E33 three-listener states and explicitly decide whether current UX density remains credible on handheld/no-audio paths; do not invent a global graph UI to rescue them.
9. Simulate E30–E34 climax progression, with E34 requiring at least two useful-heard moments while staying <=12 nodes.
10. Walk fail → cause trace → quick restart → checkpoint restore and verify deterministic preview/recovery continuity.
11. Walk save exit/reload, corrupted-save fallback, demo→full import and Steam-offline behavior against Phase-8 contracts.
12. Walk no-audio, reduced-motion, high-contrast, large UI and 70%/55% whole-simulation-speed assist paths without changing acoustic truth.
13. Walk mastery/remix/replay flow and verify no currency/grind/live-service pressure appears.
14. Attack hostile player behavior: permanent barrier parking, silence-everything, equal-lure spam, strongest-sound spam, barrier-midpoint abuse, door-order races, restart brute force and content-signature repetition.
15. Record every contradiction across thesis/mechanics/content/UX/commercial/technical layers and repair only when consistent with existing locks; do not casually add mechanics.
16. If paper simulation exposes unresolved rules rather than empirical gates, repair the upstream specification explicitly and document the amendment before Phase 10.