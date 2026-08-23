# GAME #005 — DEDICATED REPOSITORY MIGRATION MANIFEST

Target repository slug: `Mikayilzade/tension-budget` unless a different slug is explicitly chosen at migration time.
Commercial title may change later; repository slug may remain stable.

## Canonical files to migrate
1. `GAME5_PHASE11_FINAL_FREEZE.md`
2. `GAME5_ENCOUNTER_BLUEPRINTS.md`
3. `GAME5_PHASE11_READINESS_AUDIT.md`
4. `GAME5_PHASE10_AMENDMENTS.md`
5. `GAME5_TECHNICAL_SPEC.md`
6. `GAME5_UX_PRESENTATION.md`
7. `GAME5_CONTENT_ARCHITECTURE.md`
8. `GAME5_MECHANICS.md`
9. `GAME5_ECONOMY_COMMERCIAL.md`
10. `GAME5_PRODUCT_THESIS.md`
11. `GAME5_ADVERSARIAL_REVIEW.md`
12. `GAME5_WHOLE_GAME_SIMULATION.md`
13. `GAME5_TOURNAMENT_RUN3.md`
14. `GAME5_TOURNAMENT_RUN2.md`
15. `GAME5_TOURNAMENT.md`
16. `GAME5_RESEARCH_RUN3.md`
17. `GAME5_RESEARCH_RUN2.md`
18. `GAME5_RESEARCH.md`

History files 11–18 are rationale/history; authority remains the order in the final freeze.

## Dedicated-repo files to add
- `README.md`
- `IMPLEMENTATION_START_HERE.md`
- `IMPLEMENTATION_STATUS.md`
- `CI_NOTIFICATION_POLICY.md`
- `DESIGN_AUTHORITY.md` or equivalent concise authority map

## Integrity verification
After migration:
1. fetch every destination canonical file;
2. compare content/blob identity where filenames are copied unchanged;
3. verify the destination authority chain points only to destination files;
4. verify `IMPLEMENTATION_START_HERE.md` references the final freeze and exact Phase 12A next action;
5. verify no implementation completion is claimed;
6. verify CI policy prevents unstable push-triggered notification spam;
7. only after successful verification may factory Game #005 source files be removed/reset.

## Cleanup rule
Do not delete Game #005 design files from the factory until destination integrity is verified. After verification:
- update `GAME_INDEX.md` with the dedicated repository and DESIGN COMPLETE/migration state;
- remove Game #005-specific active files from the factory or archive only where factory rules explicitly allow;
- reset `STATUS.md` to clean Game #006 Opportunity Discovery;
- disable the Game #005 recurring design automation.
