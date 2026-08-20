# BORROWED COLLISION — MIGRATION MANIFEST

Prepared: 2026-08-20
Source repository: `Mikayilzade/gpt-game-autonomy`
Intended destination: `Mikayilzade/borrowed-collision`
Migration status: **BLOCKED — DESTINATION REPOSITORY NOT FOUND**

## Safety rule
Do not delete any Game #003 file from the factory until the dedicated destination exists, every required file below has been copied, `GAME3_PHASE11_FINAL_FREEZE.md` has been verified content-identical, the authority chain is self-contained, implementation handoff/status/CI policy exist, and `GAME_INDEX.md` has been updated.

## Frozen package to migrate exactly
- `GAME3_RESEARCH.md`
- `GAME3_RESEARCH_RUN2.md`
- `GAME3_RESEARCH_RUN3.md`
- `GAME3_TOURNAMENT.md`
- `GAME3_TOURNAMENT_RUN2.md`
- `GAME3_TOURNAMENT_RUN3.md`
- `GAME3_PRODUCT_THESIS.md`
- `GAME3_MECHANICAL_ARCHITECTURE.md`
- `GAME3_CONTENT_ARCHITECTURE.md`
- `GAME3_UX_PRESENTATION_ARCHITECTURE.md`
- `GAME3_ECONOMY_COMMERCIAL.md`
- `GAME3_TECHNICAL_SPEC.md`
- `GAME3_WHOLE_GAME_SIMULATION.md`
- `GAME3_ADVERSARIAL_REVIEW.md`
- `GAME3_PHASE11_FINAL_FREEZE.md`

## Destination handoff files
Copy/rename:
- `GAME3_IMPLEMENTATION_START_HERE.md` -> `IMPLEMENTATION_START_HERE.md`
- `GAME3_IMPLEMENTATION_STATUS.md` -> `IMPLEMENTATION_STATUS.md`
- `GAME3_CI_NOTIFICATION_POLICY.md` -> `CI_NOTIFICATION_POLICY.md`
- this manifest -> `MIGRATION_MANIFEST.md`

Add destination `README.md` that states:
- project: Borrowed Collision;
- design status: `DESIGN COMPLETE = YES`;
- implementation status: not started;
- first read: `IMPLEMENTATION_START_HERE.md`;
- CI guardrail: `CI_NOTIFICATION_POLICY.md`;
- highest implementation-sensitive authority: `GAME3_PHASE11_FINAL_FREEZE.md`.

## Integrity reference
Factory final-freeze blob SHA at manifest creation:
`d227433d40d4a8e73334702833b099befb25a2b0`

Destination final-freeze content must match exactly unless Git content identity changes only because of an intentional documented file-normalization step; direct blob equality is preferred.

## Destination verification checklist
- [ ] Dedicated repo exists with `main`.
- [ ] All 15 Game #003 research/design/validation files exist.
- [ ] `IMPLEMENTATION_START_HERE.md` exists and defines 12A–12H.
- [ ] `IMPLEMENTATION_STATUS.md` exists and points to 12A only after migration verification.
- [ ] `CI_NOTIFICATION_POLICY.md` exists and forbids unstable push-triggered CI.
- [ ] Final-freeze blob/content matches factory reference.
- [ ] Authority chain resolves entirely inside destination.
- [ ] No implementation depends on chat memory or factory-only files.
- [ ] `GAME_INDEX.md` updated to Borrowed Collision + dedicated repo.
- [ ] Only after all above: remove every `GAME3_*` file from factory and reset `STATUS.md` for Game #004 Phase 1.

## Current blocker
Targeted GitHub repository search did not find `Mikayilzade/borrowed-collision`. Current connected GitHub capabilities in this run support read/write on existing repositories but do not expose repository creation.

Therefore the safe state is to keep the entire frozen Game #003 package in the factory and continue migration only when the destination exists or repository-creation capability becomes available.