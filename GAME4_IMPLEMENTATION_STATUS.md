# HEARWALL — IMPLEMENTATION STATUS

Prepared: 2026-08-21
Source factory: `Mikayilzade/gpt-game-autonomy`
Intended dedicated repository: `Mikayilzade/hearwall`
Design status: **DESIGN COMPLETE = YES**
Implementation complete: **NO**
Production implementation started: **NO**

This factory-side file must be copied/renamed to `IMPLEMENTATION_STATUS.md` in the dedicated repository after migration.

## Current phase
**MIGRATION GATE — dedicated repository verification required before Phase 12A.**

## Current authoritative design
Highest authority: `PHASE11_FINAL_FREEZE.md` after migration (factory source: `GAME4_PHASE11_FINAL_FREEZE.md`).

Working commercial title: **HEARWALL**. This is a screened working title, not legal trademark clearance.

## Implementation phase state
- 12A Technical bootstrap: **NOT STARTED**.
- 12B Vertical slice / empirical kill build: **NOT STARTED**.
- 12C Core systems complete: **NOT STARTED**.
- 12D Content population: **NOT STARTED**.
- 12E UX/accessibility/controller: **NOT STARTED**.
- 12F Adversarial QA: **NOT STARTED**.
- 12G Empirical gates: **NOT STARTED**.
- 12H Release candidate: **NOT STARTED**.

## Frozen implementation-critical constraints
- Godot 4.7.1-stable, GDScript-first initial target.
- Deterministic Domain Core separated from presentation/platform adapters.
- One local/direct barrier baseline and 1.0 ceiling.
- Strength 1–4 / attenuation 0–2 / threshold 1–3 / barrier +3.
- Tied minimum routes are real and equally represented.
- BEFORE_MUTATION events own immutable pre-commit graph revisions; AFTER_MUTATION events own post-commit revisions.
- Exact preview and committed hearing share the same solver; parity target 100%.
- Maximum two listeners in all 1.0 content; three-listener gameplay is cut.
- No-audio completion/decision parity is mandatory.
- Direct detection is bounded secondary pressure, no combat branch.
- 34 main encounters; 8 optional remixes are first-cut if repetition evidence is poor.
- V17 safe-preview-enumeration and V18 content-signature-dedup validators are mandatory.

## Migration blocker/checkpoint
At preparation time the intended destination repository `Mikayilzade/hearwall` was not found through the connected GitHub search. Current connected actions do not expose repository creation.

Therefore production implementation must **not** start in the factory and no Game #004 source file may be deleted yet.

## NEXT ACTION
1. Verify whether `Mikayilzade/hearwall` now exists.
2. If it exists, copy the complete migration package exactly as defined by `MIGRATION_MANIFEST.md`.
3. Rename factory handoff files to destination names (`IMPLEMENTATION_START_HERE.md`, `IMPLEMENTATION_STATUS.md`, `CI_NOTIFICATION_POLICY.md`, `MIGRATION_MANIFEST.md`) and add destination README.
4. Verify `PHASE11_FINAL_FREEZE.md` content identity against factory source blob SHA recorded in the manifest.
5. Verify every authority-chain file is present and all links/references can resolve inside the dedicated repository without chat/factory dependency.
6. Only after migration verification, set Phase 12A as active and begin deterministic technical bootstrap.

Do not mark `IMPLEMENTATION COMPLETE = YES` until Phase 12A–12H and empirical/release gates are actually complete.
