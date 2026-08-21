# HEARWALL — MIGRATION MANIFEST

Prepared: 2026-08-21
Source repository: `Mikayilzade/gpt-game-autonomy`
Intended destination: `Mikayilzade/hearwall`
Design status: **DESIGN COMPLETE = YES**
Migration status: **BLOCKED — DESTINATION REPOSITORY NOT FOUND**

## Safety rule
Do not delete any Game #004 source file from the factory until the dedicated destination exists, every required file below has been copied, final-freeze content identity is verified, the authority chain is self-contained, implementation handoff/status/CI policy exist in destination names, `GAME_INDEX.md` records the verified migration, and factory `STATUS.md` is safely reset for Game #005.

## Frozen design/history package to migrate
Copy these factory files into the dedicated repository. Destination may drop the `GAME4_` prefix as shown where useful, but content must remain unchanged unless a documented normalization is required.

1. `GAME4_RESEARCH.md` -> `RESEARCH.md`
2. `GAME4_RESEARCH_RUN2.md` -> `RESEARCH_RUN2.md`
3. `GAME4_RESEARCH_RUN3.md` -> `RESEARCH_RUN3.md`
4. `GAME4_TOURNAMENT.md` -> `TOURNAMENT.md`
5. `GAME4_TOURNAMENT_RUN2.md` -> `TOURNAMENT_RUN2.md`
6. `GAME4_TOURNAMENT_RUN3.md` -> `TOURNAMENT_RUN3.md`
7. `GAME4_PRODUCT_THESIS.md` -> `PRODUCT_THESIS.md`
8. `GAME4_MECHANICS.md` -> `MECHANICS.md`
9. `GAME4_CONTENT.md` -> `CONTENT.md`
10. `GAME4_UX_PRESENTATION.md` -> `UX_PRESENTATION.md`
11. `GAME4_ECONOMY_COMMERCIAL.md` -> `ECONOMY_COMMERCIAL.md`
12. `GAME4_TECHNICAL_SPEC.md` -> `TECHNICAL_SPEC.md`
13. `GAME4_WHOLE_GAME_SIMULATION.md` -> `WHOLE_GAME_SIMULATION.md`
14. `GAME4_ADVERSARIAL_REVIEW.md` -> `ADVERSARIAL_REVIEW.md`
15. `GAME4_PHASE10_AMENDMENTS.md` -> `PHASE10_AMENDMENTS.md`
16. `GAME4_PHASE11_FINAL_FREEZE.md` -> `PHASE11_FINAL_FREEZE.md`

Historical files may contain retired names (`Soundproof Smuggler`, `HUSHLINE`). They are retained as historical evidence only. `PHASE11_FINAL_FREEZE.md` controls and names the current working title HEARWALL.

## Destination handoff files
Copy/rename:
- `GAME4_IMPLEMENTATION_START_HERE.md` -> `IMPLEMENTATION_START_HERE.md`
- `GAME4_IMPLEMENTATION_STATUS.md` -> `IMPLEMENTATION_STATUS.md`
- `GAME4_CI_NOTIFICATION_POLICY.md` -> `CI_NOTIFICATION_POLICY.md`
- `GAME4_MIGRATION_MANIFEST.md` -> `MIGRATION_MANIFEST.md`

Add destination `README.md` stating at minimum:
- project: **HEARWALL** (working commercial title; not legal clearance);
- design status: `DESIGN COMPLETE = YES`;
- implementation status: not started;
- first read: `IMPLEMENTATION_START_HERE.md`;
- highest design authority: `PHASE11_FINAL_FREEZE.md`;
- CI guardrail: `CI_NOTIFICATION_POLICY.md`;
- initial implementation phase: 12A after migration verification.

## Integrity reference
Factory final-freeze blob SHA at migration-manifest preparation:

`37fbe588f82b65deeeb734597ffe768bb5399dd0`

Destination `PHASE11_FINAL_FREEZE.md` content should match this source exactly. Direct blob equality is preferred when Git path/line normalization permits it. If a documented normalization changes the blob, verify decoded text identity intentionally and record the reason.

## Final authority chain expected in destination
1. `PHASE11_FINAL_FREEZE.md`
2. `PHASE10_AMENDMENTS.md` — historical rationale, already integrated
3. `TECHNICAL_SPEC.md`
4. `MECHANICS.md`
5. `CONTENT.md`
6. `UX_PRESENTATION.md`
7. `ECONOMY_COMMERCIAL.md`
8. `PRODUCT_THESIS.md`
9. `WHOLE_GAME_SIMULATION.md`, `ADVERSARIAL_REVIEW.md`
10. tournament/research files — history/evidence only

`IMPLEMENTATION_START_HERE.md` must point implementation sessions to this chain and to live `IMPLEMENTATION_STATUS.md`.

## Destination verification checklist
- [ ] Dedicated repo `Mikayilzade/hearwall` exists with `main`.
- [ ] All 16 frozen design/history files exist.
- [ ] `PHASE11_FINAL_FREEZE.md` matches source blob/content reference.
- [ ] `IMPLEMENTATION_START_HERE.md` exists and defines Phase 12A–12H.
- [ ] `IMPLEMENTATION_STATUS.md` exists and remains NOT STARTED until migration verification passes.
- [ ] `CI_NOTIFICATION_POLICY.md` exists and prevents unstable notification-heavy push CI.
- [ ] `MIGRATION_MANIFEST.md` exists.
- [ ] `README.md` states authority/first-read/implementation state.
- [ ] No implementation rule depends on chat memory or factory-only paths.
- [ ] Authority chain resolves entirely inside destination.
- [ ] Phase-11 supersessions are understood: HEARWALL working title; all 1.0 three-listener content cut; E28/E33 two-listener definitions; V17/V18 mandatory; bounded direct detection; immutable BEFORE_MUTATION snapshot ownership.
- [ ] `GAME_INDEX.md` updated to verified dedicated repo only after the above checks.
- [ ] Only after every item above: remove Game #004 source/handoff files from factory and reset `STATUS.md` for Game #005.

## Current blocker
Targeted connected-GitHub repository search on 2026-08-21 did not find `Mikayilzade/hearwall`.

The currently exposed GitHub actions allow reading/writing existing repositories, blobs, trees, commits and branches but do not expose creation of a new repository.

Therefore the safe current state is:
- retain the entire Game #004 package in the factory;
- mark design frozen but migration blocked;
- do not start production implementation in the factory;
- on a later run, first re-check whether the destination exists, then migrate if available.
