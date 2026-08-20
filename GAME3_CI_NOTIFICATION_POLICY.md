# BORROWED COLLISION — CI / EMAIL NOISE POLICY

This policy is part of the autonomous implementation handoff and must be copied to the dedicated repository as `CI_NOTIFICATION_POLICY.md`.

## Hard rule
Do **not** enable push-triggered GitHub Actions for an unstable or expected-to-fail suite.

During Phase 12A and early 12B:
- run Godot headless/domain/unit/content tests locally inside the implementation session whenever possible;
- batch coherent work rather than pushing every micro-fix;
- if remote CI is needed before baseline stability, use manual `workflow_dispatch` where practical;
- enable automatic push/PR CI only after the baseline suite is consistently green;
- if a workflow begins producing repeated failing runs, return it to manual-only or disable the noisy trigger until fixed;
- do not intentionally create repeated failed workflow runs merely to probe runner/environment behavior;
- documentation-only commits should not run expensive game tests unless there is a specific reason;
- prefer one coherent checkpoint commit/push per autonomous increment when practical.

GitHub email delivery itself is controlled by account/repository notification settings. This policy addresses the avoidable source of notification storms: repeated failing Actions runs.

## Required testing principle
Reducing email noise must never mean reducing verification quality. Prefer:
1. local/headless deterministic test execution;
2. content compiler/fixture validation;
3. manual remote CI while bootstrap is unstable;
4. automatic CI after the baseline is green and useful.

Do not turn off a useful stable test suite merely to hide real failures.