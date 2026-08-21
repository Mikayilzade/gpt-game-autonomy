# HEARWALL — CI / NOTIFICATION POLICY

Prepared: 2026-08-21
Applies to implementation in intended dedicated repository `Mikayilzade/hearwall`.

This factory-side file must be copied/renamed to `CI_NOTIFICATION_POLICY.md` in the dedicated repository.

## Purpose
Preserve strong automated verification without creating GitHub Actions/email notification storms while the project is unstable or being iterated autonomously.

## Default policy
1. Prefer **local/headless deterministic tests** during normal development.
2. Prefer GitHub Actions triggers that are deliberate and bounded:
   - `workflow_dispatch` for manual checks;
   - `pull_request` once the relevant suite is stable enough to be useful.
3. Do **not** enable broad `push` CI on every checkpoint merely for convenience.
4. Documentation-only `.md` changes should not trigger expensive/runtime CI.
5. Batch a coherent autonomous run into as few pushes/commits as practical; normally target one coherent checkpoint commit rather than a burst of speculative fixes.
6. Never add a matrix or repeated retry workflow until its notification/failure surface is understood.
7. If a CI run fails, inspect the failure and make one focused repair batch; do not repeatedly push tiny guesses that each trigger another run.

## Required verification quality
Anti-spam policy does not mean weak testing. Before implementation/release gates are marked complete, the project must have repeatable coverage for:
- deterministic fixed-step/domain state;
- acoustic minimum-cost and tied-route results;
- prediction vs committed hearing parity;
- BEFORE_MUTATION / AFTER_MUTATION graph revision ownership;
- listener retarget ordering;
- barrier snap/between-slot semantics;
- content validators including V17/V18;
- save/schema/hash/backup/recovery;
- replay/state hash consistency;
- demo import idempotency;
- platform-adapter offline/failure behavior;
- representative no-audio/accessibility flows where automation can validate state truth.

## Workflow changes
Any workflow addition/change should document:
- why CI is needed rather than local/headless execution;
- trigger type;
- expected runtime/cost;
- whether failures can email/notify repeatedly;
- path filters if appropriate;
- how to run the same validation locally.

## Escalation
A stable fast suite may later move to pull-request or carefully scoped push CI after it has proven consistently green. This is a deliberate implementation decision, not the bootstrap default.

## Release candidate
Phase 12H may use broader release/package workflows when needed, but these should be manual/tag/release-oriented and separately validated before relying on them for shipping.
