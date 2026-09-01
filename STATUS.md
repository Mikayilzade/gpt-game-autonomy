# FACTORY STATUS

Last updated: 2026-09-01
Repository: `Mikayilzade/gpt-game-autonomy`
Branch: `main`

## Factory state
- Reusable factory rules: **YES**
- Games #001–#005: **DESIGN COMPLETE / migrated**
- Games #006–#011: **DESIGN COMPLETE / migration pending / retained non-active safety archives**
- Current design slot: **Game #012**
- Selected concept: **OPENWORK** *(working title; topology-of-remaining-space puzzle)*
- Production implementation inside factory: **NO**

## Continuity / active canon
Game #012 remains cleanly separated from Games #001–#011. Older games are exclusion/portfolio history only. Ink Bleed is rejected history, not parallel canon.

## Current phase
**Game #012 — PHASE 8 TECHNICAL IMPLEMENTATION SPECIFICATION COMPLETE / PHASE 9 NEXT.**

## Active authority for Game #012
1. `START_HERE.md`
2. `STATUS.md`
3. `GAME_INDEX.md`
4. `GAME12_RESEARCH.md`
5. `GAME12_TOURNAMENT.md`
6. `GAME12_ROUND_C.md`
7. `GAME12_PRODUCT_THESIS.md`
8. `GAME12_MECHANICS.md` — exact Phase-4 rules; controls over loose tournament examples
9. `GAME12_CONTENT.md` — Phase-5 campaign/content/certification architecture
10. `GAME12_UX.md` — Phase-6 interaction/presentation/accessibility/onboarding authority
11. `GAME12_COMMERCIAL.md` — Phase-7 commercial/progression/demo/platform authority
12. `GAME12_TECHNICAL.md` — Phase-8 technical/runtime/persistence/platform/test authority

## This run completed
### Game #012 Phase 8 — Technical Implementation Specification
- Resumed exactly from prior `NEXT ACTION`; no production implementation started.
- Performed fresh engine/platform verification. Godot release policy currently lists 4.7 as supported; Godot 4.7.2 was released 2026-08-18. Frozen implementation policy is current supported stable Godot 4.x latest patch at bootstrap, presently 4.7.2 rather than a 4.8 development build.
- Added `GAME12_TECHNICAL.md` as canonical Phase-8 authority.
- Defined one-way authority layering: immutable case data -> deterministic rules core -> derived topology/predicates -> session state -> presentation. Offline certifier wraps the same evaluator contract; runtime never enumerates candidate solutions.
- Defined conceptual data structures for boards, markers, pieces, placements, predicates, topology snapshots, evaluation snapshots and certificates.
- Separated `rules_version`, `case_schema_version`, per-case `content_version` and `save_schema_version`; froze deterministic canonicalization/hashing requirements.
- Defined application/services/screen architecture with gameplay truth outside UI nodes and Steam as an optional adapter rather than a dependency.
- Defined atomic placement/reposition/history semantics. Temporary held/reposition state is never persisted as committed truth.
- Defined persistence with temp-write/validation/backup/atomic replacement, migration fixtures, corruption recovery and hard future-version refusal so an older build cannot overwrite a newer save.
- Repaired progression authority: solved case IDs are monotonic truth; unlocks are derived, never independently saved as authoritative flags.
- Defined semantic Steam Cloud merge: compatible solved sets union; clocks never choose solved progress; resume/settings use separate conflict rules; local solve commits before platform sync.
- Defined crash-safe, idempotent demo->full import using source provenance, compatible case/content identity, solved-ID union, explicit settings whitelist and achievement reconstruction.
- Defined Steam/null platform abstraction for achievements, Cloud and controller glyphs; offline/local play remains fully functional when Steam is absent.
- Defined logical input actions and localization-key boundaries; physical button names/rendered text never enter puzzle truth.
- Set runtime performance policy for <=9x9: full topology recomputation is acceptable; runtime solution enumeration is forbidden. Added offline certifier workflow budgets.
- Defined golden topology/predicate/placement/certificate tests, save/import/Cloud/progression fixtures, controller/focus/accessibility regression and anti-oracle regression.
- Froze no-required-custom-telemetry privacy posture.
- Hostile-passed Phase-7 progression/import/achievement rules and repaired stale unlock flags, timestamp overwrite ambiguity, demo achievement trust, incompatible revised cases, accessibility setting conflicts, resume-vs-solved conflicts, Steam outage handling and demo/full Cloud path collision.
- Defined future dedicated-repository implementation order T1–T11 and explicit non-goals.

## Fresh evidence recorded
- Godot official release policy: 4.7 supported; 4.8 development/Q4 estimate.
- Godot 4.7.2 stable maintenance release dated 2026-08-18.
- Current Steamworks Steam Input guidance continues to support logical action/native-mode abstraction and action-origin glyph lookup.
- Current Steam Cloud documentation remains the platform target for cross-device persistence while semantic save merge remains game-owned.

## Frozen migration state
Game #006 Stitchspace: pending, non-blocking.
Game #007 Last Known Shape: pending, non-blocking.
Game #008 Locksmith's Margin: pending, non-blocking.
Game #009 Binder's Imposition: pending, non-blocking.
Game #010 Luggage Carousel Zero: pending, non-blocking.
Game #011 Missing Step: pending, non-blocking; final authority `GAME11_FINAL_FREEZE.md`.

## NEXT ACTION — GAME #012 PHASE 9 WHOLE-GAME SIMULATION
Perform one substantial paper-simulation/adversarial journey increment. Use the frozen mechanics/content/UX/commercial/technical authorities and repair contradictions immediately rather than merely listing them.

Minimum scenario matrix:
1. fresh keyboard/mouse first boot through first 6 onboarding cases;
2. controller/Deck first boot at 1280x800 with text scaling, high contrast and reduced motion;
3. player repeatedly skips the two hardest cases allowed by every 4/6 gate and tries to reach Act VI/finale;
4. strong player brute-tests placements instead of reasoning in early, mid and mastery cases;
5. struggling player uses unlimited undo, inspect and permitted reasoning primers without case-specific hints;
6. demo partial/full progression -> full install -> import -> achievements/unlocks;
7. existing full progress plus older/newer/incompatible demo import attempts;
8. two-device Cloud conflict with disjoint solved sets plus conflicting resume/settings;
9. offline solves -> Steam returns -> achievement/Cloud reconciliation;
10. corrupt primary + valid backup, both corrupt, and future-version save opened by older build;
11. content update changes a previously solved/demo case;
12. late 9x9 / 4-piece / 5–6-predicate case on handheld for readability and interaction fatigue;
13. 30-case floor vs 36-target campaign value/session shape;
14. 100% completion/replay/postgame without grind;
15. rapid input during animations, reposition, undo, reset-hold and success transition.

Required outcome:
- write `GAME12_SIMULATION.md` with journey traces, contradictions, fixes, empirical gates and any resulting amendments to earlier authorities;
- verify progression skip paths do not bypass necessary predicate teaching;
- verify no save/import/Cloud path can silently shrink solved progress;
- verify the anti-oracle boundary still makes experimentation usable;
- if Phase 9 closes cleanly, set exact Phase-10 adversarial-review attack list as NEXT ACTION.

## Blockers
**NONE for factory continuation.** Pending migrations #006–#011 are explicitly non-blocking.

DESIGN COMPLETE = NO (current active Game #012).
