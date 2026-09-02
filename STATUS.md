# FACTORY STATUS

Last updated: 2026-09-02
Repository: `Mikayilzade/gpt-game-autonomy`
Branch: `main`

## Factory state
- Reusable factory rules: **YES**
- Games #001–#005: **DESIGN COMPLETE / migrated**
- Games #006–#013: **DESIGN COMPLETE / migration pending / retained NON-ACTIVE safety archives**
- Current design slot: **Game #014**
- Selected concept: **NEGATIVE CASTING — Phase 8 Technical Implementation Specification complete**
- Production implementation inside factory: **NO**

## Continuity / active canon
Game #014 is the only active design slot. Games #001–#013 are exclusion/portfolio history only. Frozen archives #006–#013 are explicitly NON-ACTIVE and must not leak canon into #014. Rejected Game #014 tournament concepts are evidence/history, not mechanics available for silent reuse.

## Current phase
**Game #014 — PHASE 8 TECHNICAL IMPLEMENTATION SPECIFICATION COMPLETE / PHASE 9 WHOLE-GAME SIMULATION NEXT.**

## Active authority for Game #014
1. `START_HERE.md`
2. `STATUS.md`
3. `GAME_INDEX.md`
4. `GAME14_RESEARCH.md`
5. `GAME14_TOURNAMENT.md`
6. `GAME14_ROUND_B.md`
7. `GAME14_ROUND_C.md`
8. `GAME14_PRODUCT_THESIS.md`
9. `GAME14_MECHANICAL_ARCHITECTURE.md`
10. `GAME14_CONTENT_ARCHITECTURE.md`
11. `GAME14_UX_PRESENTATION.md`
12. `GAME14_COMMERCIAL_MODEL.md`
13. `GAME14_TECHNICAL_SPEC.md`

## This run completed — Game #014 Phase 8
- Re-read the complete active authority chain and resumed exactly from Phase-8 `NEXT ACTION`.
- Performed fresh 2026-09-02 engine/platform research before freezing implementation-sensitive assumptions.
- Selected **Godot 4.7.x stable, GDScript-first** as the lead implementation direction; puzzle truth is explicitly engine-renderer/physics independent.
- Froze a five-layer architecture separating exact Core Logic, Content Model, Game State, Presentation/UX and optional Platform Services.
- Defined canonical integer/rational geometry with normalized `int64` rationals, exact 90-degree transforms and checked-overflow policy.
- Defined the reference `open light->sample segment intersects strict polygon interior` algorithm using exact boundary-intersection parameters, interval midpoints and exact point-in-polygon classification. Pure tangency/boundary travel does not block; positive-width interior traversal does.
- Defined canonical blocker/case/surface/human-route schemas with stable ids, revisions and localization-key boundaries.
- Defined structural + geometry validation, geometry/target/certification SHA-256-style hashes, derived-cache invalidation and a hard ban on authored incidence-mask authority.
- Defined runtime case state machine, atomic pose mutation, undo/redo/check/reset boundaries and the invariant that only blocker pose state affects puzzle truth.
- Defined deterministic exhaustive certifier for the frozen <=4^6 ordinary state space, observational equivalence, meaningful solution classes and acceptance of every physically valid target-matching vector.
- Defined a machine-verifiable human-route contract for the Phase-4 deduction families; solver uniqueness remains insufficient for shipping.
- Froze renderer/logical-truth separation: GPU shadows are cosmetic; semantic target/current/contribution overlays consume canonical incidence only.
- Defined recoverability-first persistence with primary/temp/backup atomic writes, checksum validation, per-case content revision handling and stable-id migrations.
- Defined one-way idempotent demo->full import for NC01–NC08 completion/resume/tutorial/hints/safe settings and safe fallback when demo data is absent/corrupt/incompatible.
- Defined Steam Cloud as transport, never authority; offline play remains complete, achievement state reconciles from campaign state, and graphics/device-sensitive settings remain local.
- Defined localization/accessibility persistence boundaries and explicit non-effect on puzzle truth/achievement eligibility.
- Defined Deck-class performance/readability targets: 1280x800 baseline, 60 fps play target, 30 fps hard floor during heavy visuals; exact logic is expected to be negligible compared with rendering.
- Added automated geometry/incidence/equivalence/human-route/state/save/input tests, malformed-content hard rejection matrix and developer-only debug hooks.
- Defined dedicated-repo implementation order: exact headless kernel -> schema/certifier -> headless runtime/persistence -> NC01–NC03 vertical slice -> NC01–NC08 demo architecture proof -> full production phases.
- Preserved all Phase 3–7 exclusions; no production implementation started. No email/Gmail notification sent.

## Fresh external facts used this run
- Godot current release policy lists 4.7 (June 2026) as a supported stable branch; 4.8 remains a Q4 2026 development target.
- Godot 4.7 desktop exports support modern Vulkan/Direct3D/Metal paths and Compatibility/OpenGL fallback depending on platform/render method.
- Current Steam Deck compatibility guidance still requires full default-controller access, correct active-device glyphs, native 1280x800/1280x720 support and a playable default 30 fps-at-800p floor; this design targets 60 fps.
- Current Steam Cloud docs retain OS root-override support for cross-platform Auto-Cloud paths; exact Auto-Cloud vs explicit API choice remains an implementation-stage platform decision after app ids/save roots exist.

## NEXT ACTION — GAME #014 PHASE 9 / WHOLE-GAME SIMULATION
Create `GAME14_WHOLE_GAME_SIMULATION.md` and simulate the frozen game end-to-end rather than adding systems.

Required work:
1. simulate fresh install / first boot / controller-only path / settings and accessibility;
2. walk NC01–NC08 as a first-time player including wrong actions, two incorrect checks, hint use, leave/resume and NC07 second-surface reveal;
3. simulate demo->full import plus a no-demo fresh full-game path;
4. simulate a representative hour-1 MID case with connected human deductions;
5. simulate NC17–NC24 late/three-surface progression, stuck-player behavior and hint ladder use;
6. simulate 2-of-3 group unlocks, skipped-case return and all-24 Campaign Complete semantics;
7. simulate replay, achievements, offline use, cloud conflict/recovery;
8. attack orientation spam, repeated Check, undo/reset abuse, suspend/alt-tab during save, corrupt resume, content revision mismatch and rapid device switching;
9. assess campaign-wide cognitive/repetition pressure and repair contradictions only within frozen mechanics;
10. record every repair and hand Phase 10 a concrete residual attack-surface list.

If a Phase-9 contradiction requires changing a frozen rule rather than clarifying implementation, record it explicitly as a design repair and update the affected authority file rather than silently overriding it.

## Blockers
**NONE for factory continuation.** Pending migrations #006–#013 remain non-blocking.

DESIGN COMPLETE = NO (current active Game #014; Phase 8 complete, Phase 9 next).
