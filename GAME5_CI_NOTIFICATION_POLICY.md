# GAME #005 — CI / NOTIFICATION POLICY

Migration-ready policy for the dedicated repository; copy/rename to `CI_NOTIFICATION_POLICY.md`.

## Goal
Get useful automated validation without repeated push-triggered notification spam.

## Baseline
- Do not enable a noisy broad workflow on every documentation/status push.
- Prefer local/headless Godot validation during early unstable implementation.
- CI may run on pull requests and explicit `workflow_dispatch` while the project is unstable.
- If push CI is later enabled, path-filter it to implementation/content/test paths; Markdown-only status/handoff updates should not trigger expensive suites.
- Batch coherent fixes; avoid repeated speculative push/fail/push loops.

## Required validation layers
1. static/content validators V01–V20;
2. domain/headless unit/property tests;
3. traversal/state solver tests;
4. integration tests for commit/mutation/restart/transition epochs;
5. persistence corruption/recovery tests;
6. controller/accessibility logical-parity tests;
7. representative scene/runtime smoke tests;
8. packaging/demo-retail separation checks near release.

## Failure handling
- Inspect the first actual failure before changing thresholds.
- Fix the defect rather than weakening validators merely to make CI green.
- Do not suppress failures by removing coverage without a documented design reason.
- One coherent run should normally produce one implementation checkpoint rather than many tiny notification-generating commits.

## Email rule
No test emails and no Gmail-based project notifications. GitHub/CI notifications should be minimized through trigger design rather than routed to mail tests.

## Completion
Release-candidate CI policy may become stricter once stable, but must preserve quiet documentation-only updates and the exact frozen deterministic/validator contracts.