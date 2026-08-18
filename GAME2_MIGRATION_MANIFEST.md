# GAME #002 — FALSE MAP DEPARTMENT — MIGRATION MANIFEST

Prepared: 2026-08-19
Source repository: `Mikayilzade/gpt-game-autonomy`
Intended destination: `Mikayilzade/false-map-department`
Migration status: **BLOCKED — DESTINATION REPOSITORY DOES NOT YET EXIST**

## Safety rule
Do not delete any Game #002 file from the factory until the dedicated destination exists, all files below have been copied, `GAME2_PHASE11_FINAL_FREEZE.md` has been verified identical by blob/content hash, the destination authority chain is self-contained, `IMPLEMENTATION_START_HERE.md` and `IMPLEMENTATION_STATUS.md` exist there, and `GAME_INDEX.md` has been updated.

## Frozen source package to migrate
Copy these files with exact content:
- `GAME2_PHASE11_FINAL_FREEZE.md` — final authority; source blob SHA at manifest creation: `fc988f8eaa031507f5ae84d6e60316356bc6cb2a`
- `GAME2_ADVERSARIAL_REVIEW.md`
- `GAME2_MECHANICAL_ARCHITECTURE.md`
- `GAME2_CONTENT_ARCHITECTURE.md`
- `GAME2_UX_PRESENTATION_ARCHITECTURE.md`
- `GAME2_ECONOMY_COMMERCIAL.md`
- `GAME2_TECHNICAL_SPEC.md`
- `GAME2_PRODUCT_THESIS.md`
- `GAME2_WHOLE_GAME_SIMULATION.md`
- `GAME2_TOURNAMENT_RUN5.md`
- `GAME2_TOURNAMENT_RUN4.md`
- `GAME2_TOURNAMENT.md`
- `GAME2_RESEARCH.md`
- `GAME2_IMPLEMENTATION_START_HERE.md` -> copy/rename in destination to `IMPLEMENTATION_START_HERE.md`
- `GAME2_IMPLEMENTATION_STATUS.md` -> copy/rename in destination to `IMPLEMENTATION_STATUS.md`

## Destination files to add
`README.md` should state:
- project: False Map Department;
- design status: `DESIGN COMPLETE = YES`;
- implementation status: not started;
- first read: `IMPLEMENTATION_START_HERE.md`;
- highest implementation-sensitive authority: `GAME2_PHASE11_FINAL_FREEZE.md`.

A frozen `DESIGN_STATUS.md` or equivalent pointer may be added, but it must not create a conflicting authority order.

## Destination verification checklist
- [ ] Destination repo exists and is clearly dedicated to False Map Department.
- [ ] All 13 Game #002 design/research/history files exist.
- [ ] `IMPLEMENTATION_START_HERE.md` exists and defines 12A–12H.
- [ ] `IMPLEMENTATION_STATUS.md` exists and points to 12A Technical Bootstrap.
- [ ] Final-freeze destination blob/content matches source `fc988f8eaa031507f5ae84d6e60316356bc6cb2a` when exact file content/name encoding permits direct blob comparison.
- [ ] Authority chain resolves entirely inside destination.
- [ ] No implementation depends on reading factory chat/history.
- [ ] `GAME_INDEX.md` updated to migrated dedicated repo.
- [ ] Only after all checks pass: remove every `GAME2_*` file from factory and reset `STATUS.md` to Game #003 / Phase 1.

## Current blocker
The connected GitHub capability can read/write existing repositories but exposes no repository-creation action. `Mikayilzade/false-map-department` was searched and does not exist. The local runtime also has no authenticated GitHub CLI/token path available for repository creation.

Therefore the only safe state is to preserve all Game #002 source files in the factory, stop automatic migration retries, and resume once the destination repository exists or a repository-creation capability becomes available.
