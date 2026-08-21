# HEARWALL — IMPLEMENTATION START HERE

Prepared: 2026-08-21
Source factory: `Mikayilzade/gpt-game-autonomy`
Intended dedicated repository: `Mikayilzade/hearwall`
Design status: **DESIGN COMPLETE = YES**
Production implementation status: **NOT STARTED**

This file is the autonomous implementation entry point prepared in the factory. In the dedicated repository it must be copied/renamed to `IMPLEMENTATION_START_HERE.md`.

## 1. Source of truth
Do not reconstruct design from chat memory. In the dedicated repository, read in this order:
1. `PHASE11_FINAL_FREEZE.md` — highest gameplay/design authority.
2. `TECHNICAL_SPEC.md` — detailed architecture where not superseded by the freeze.
3. `MECHANICS.md` — detailed mechanics where not superseded.
4. `CONTENT.md` — detailed content schema/campaign where not superseded.
5. `UX_PRESENTATION.md` — UX/accessibility/presentation where not superseded.
6. `ECONOMY_COMMERCIAL.md` — commercial/demo/platform package where not superseded.
7. `PRODUCT_THESIS.md` — product rationale where not superseded.
8. `WHOLE_GAME_SIMULATION.md`, `ADVERSARIAL_REVIEW.md`, `PHASE10_AMENDMENTS.md` — validation and repair rationale.
9. Tournament/research files — historical evidence only.

If two files disagree, `PHASE11_FINAL_FREEZE.md` wins.

## 2. Frozen identity that implementation must preserve
- Top-down real-time acoustic infiltration puzzle.
- One local/direct physical soundproof barrier on authored rails/snap slots.
- Core question: **who should hear each action**, not how to make everything silent.
- Deterministic graph acoustics: strength 1–4, attenuation 0–2, listener thresholds 1–3, barrier +3.
- All tied minimum routes are mechanically real and presentation-visible.
- Exact preview and committed hearing use the same solver and must match 100%.
- Main campaign has at most two listeners per encounter; three-listener gameplay is cut from 1.0.
- No-audio decision parity is mandatory.
- Direct detection is bounded secondary pressure, not a twitch-stealth/combat pillar.
- 34 main encounters; 8 optional remixes are first-cut if repetition evidence is poor.
- Premium buy-once product; no currency/grind/live-service systems.

## 3. Technical baseline
Initial target: **Godot 4.7.1-stable, GDScript-first**.

Required architecture:
- deterministic Domain Core;
- Godot runtime/world-binding orchestrator;
- non-authoritative presentation layer;
- platform adapters with offline `NullPlatformAdapter` path.

Gameplay truth must not depend on SceneTree callback order, render interpolation, audio timing, Steam callbacks or free rigid-body outcomes.

Target authoritative simulation: 60 domain ticks/s with stable IDs and deterministic ordering. Quantized/fixed-point authoritative motion is preferred unless an implementation substitute proves identical replay/hash behavior across target platforms.

## 4. Autonomous implementation phases

### 12A — Technical bootstrap
Goal: runnable project + deterministic domain/test foundation, not a polished game.

Required deliverables:
- Godot 4.7.1 project pinned/documented;
- Layer A/B/C/D folder/module boundaries;
- canonical stable-ID content definitions;
- semantic input packet model;
- 60-tick deterministic loop;
- graph revisions/snapshots supporting BEFORE_MUTATION and AFTER_MUTATION;
- acoustic solver with tied-minimum-route traces;
- listener threshold/hearing/retarget state logic;
- one barrier state machine skeleton;
- deterministic state serialization/hash;
- headless test runner/fixtures;
- CI remains manual or pull-request gated until stable.

Gate to 12B: core acoustic/parity fixtures pass headlessly and a minimal scene can bind to the Domain Core without making gameplay decisions in presentation.

### 12B — Vertical slice / empirical kill build
Goal: prove the product thesis cheaply with a tiny playable slice before full content production.

Implement only enough content to exercise:
- local barrier reach/grab/move/snap;
- one/two listener states;
- locomotion + distraction + loud objective sounds;
- alternate/tied routes;
- one door mutation with BEFORE/AFTER semantics;
- deliberate useful hearing;
- exact world-space preview;
- direct detection at bounded/simple pressure;
- quick restart/checkpoint;
- keyboard/mouse + controller basics;
- muted/no-audio completion.

Measure the Phase-11 empirical gates, especially barrier tactility, >=~1 meaningful edit/minute over representative stretches, <=~2–3s grab-to-meaningful-snap once in reach, 100% prediction/hearing parity, no-audio optimal-decision parity, waiting thresholds and `heard can be useful` comprehension.

If the frozen core fails an empirical gate, repair within existing scope or create a documented design amendment. Do not hide failure by adding unrelated mechanics.

### 12C — Core systems complete
Implement all frozen mechanics and infrastructure:
- WALK/FAST_MOVE cadence;
- barrier full state machine and rail/orientation rules;
- doors/object mutation semantics;
- all four source families;
- listener POSTED/INVESTIGATE/ARRIVED_SEARCH/RETURN/ALERT_FAIL;
- deterministic navigation/retargeting;
- direct detection bounded profiles;
- objectives/win/fail/checkpoints;
- prediction cache without second solver;
- telemetry needed by validators/mastery;
- simulation-speed assists preserving domain ordering.

### 12D — Content population
Build the 34-main campaign data-first using the 12 reasoning families and validators.

Mandatory tooling/validation includes:
- hidden-edge rejection;
- threshold signaling/density checks;
- meaningful slot checks;
- permanent parking/silence dominance checks;
- selective-audibility coverage;
- waiting/verb-frequency telemetry;
- tied-route density limits;
- `V17_SAFE_PREVIEW_ENUMERATION`;
- `V18_CONTENT_SIGNATURE_DEDUP`.

Freeze-specific late campaign identities:
- E28: two-listener tied-route + threshold split + selective audibility.
- E33: two-listener tied routes + threshold split + sequence preservation, >=3 completion-critical barrier placements.
- E34: two-listener final synthesis, >=2 useful-heard moments.

No three-listener content.

### 12E — UX / accessibility / controller / target-device support
Implement the complete world-first presentation and settings:
- acoustic route/source/attenuation/threshold motifs;
- tied-route equal emphasis;
- barrier physical feedback;
- listener state and detection distinction;
- automatic local + hold + optional persistent preview;
- keyboard/mouse + controller remapping;
- high contrast, UI/text scale, reduced motion, optional explicit numbers;
- whole-simulation speed 100/85/70/55%;
- handheld readability passes;
- full no-audio decision parity.

### 12F — Adversarial QA
Attack determinism, exploits and recovery:
- prediction mismatch;
- nearest-door parking;
- silence-everything routes;
- safe preview enumeration;
- equal-strength lure spam;
- passive waiting;
- direct-detection microtiming dominance;
- duplicate content signatures;
- tied-route overload;
- save/checkpoint corruption;
- replay/hash divergence;
- demo import duplication;
- platform adapter failure/offline behavior.

### 12G — Empirical gates
Run the complete Phase-11 empirical-gate matrix on representative teaching/mature/climax content, including E16/E28/E33/E34-class states.

Do not mark a failed empirical gate green by weakening observability. Record evidence and repair the bounded cause.

### 12H — Release candidate
- performance and deterministic regression on target builds;
- package demo + full app separately;
- Steam Cloud/offline/import paths on real App IDs;
- achievements 18–24 target, demo achievements disabled;
- save migration/backup/fallback final pass;
- controller/input metadata;
- store/demo CTA flows;
- title/legal/store/domain check (rename if HEARWALL fails; gameplay unchanged);
- pricing from real store/demo evidence in $14.99–$19.99 test range;
- final release checklist.

## 5. Completion semantics
Implementation is complete only when the dedicated repository explicitly states:

`IMPLEMENTATION COMPLETE = YES`

Do not report `Завершено` because one subsystem, prototype, campaign pass or CI run is complete.

## 6. Progress persistence
At the end of every substantial autonomous run:
- commit coherent code/content/test/doc changes;
- update `IMPLEMENTATION_STATUS.md` with phase/subphase, evidence, blockers, exact next action and empirical-gate state;
- never leave important implementation decisions only in chat;
- prefer one coherent checkpoint commit over bursts of small pushes.

## 7. CI / notification guardrail
Read `CI_NOTIFICATION_POLICY.md` before changing workflows. Do not create unstable push-triggered GitHub Actions that can generate notification/email storms. Prefer local/headless tests plus manual `workflow_dispatch` or pull-request CI until consistently stable.

## 8. First implementation action
After migration integrity is verified, start **Phase 12A only**. Do not begin full encounter authoring or release packaging before deterministic bootstrap/parity fixtures exist.
