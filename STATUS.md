# STATUS

Last updated: 2026-08-15
Repository: `Mikayilzade/gpt-game-autonomy`
Branch: `main`

## Critical chat-status rule

The user has clarified the terse protocol:
- Do **not** say `Завершено.` merely because one work cycle finished.
- Until at least one game is fully specified and the canonical design reaches `DESIGN COMPLETE = YES`, every cycle remains **`В процессе.`** in chat.
- Intermediate milestones are recorded here in GitHub, not announced as project completion.

## Autonomous cadence

- Hourly continuation requested by user: **ACTIVE**
- Each run resumes from this file, performs one substantial bounded stage, saves progress before ending, and updates the exact next action.
- Goal condition: at least one game is fully specified, internally reviewed, implementation-ready, specification-frozen, and `DESIGN COMPLETE = YES`.
- If the goal condition becomes true, future design work stops rather than inventing unnecessary scope.

## Master state

- Project initialized: **YES**
- External opportunity research complete enough for selection: **YES**
- Broad opportunity discovery complete: **YES**
- Candidate field generated: **YES — 30 distinct seeds**
- All 8 original finalists stress-tested: **YES**
- Cross-round final comparison complete: **YES**
- Concept tournament complete: **YES**
- Final concept selected: **YES — C13 Organism Cargo**
- Product thesis locked: **YES**
- Mechanical architecture complete: **YES — Phase 4 closure passed**
- Content architecture complete: **YES — Phase 5 closure passed**
- UX / presentation architecture complete: **NO**
- Economy / retention / commercial model complete: **NO**
- Technical specification complete: **NO**
- Whole-game consistency review complete: **NO**
- Adversarial review complete: **NO**
- Specification freeze complete: **NO**
- DESIGN COMPLETE: **NO**
- Implementation started: **NO**

## Current phase
**Phase 6 — UX / Presentation Architecture**

## Selected game

### Codename
**Organism Cargo**

### Locked thesis
A compact deterministic strategy/puzzle game where the player packs living cargo into a constrained transport hold, commits to launch, then watches organisms change state and interact through a short transit simulation. Success comes from predicting the future ecology, explaining cascades, and improving the initial arrangement — not from satisfying static packing rules.

### Non-negotiable differentiation rule
**The hold is not solved when the doors close.**

Transit must create meaningful, deterministic, learnable state changes that alter relationships after commitment.

## Canonical files for current work

1. `START_HERE.md` — operating rules and handoff.
2. `STATUS.md` — exact current state and next action.
3. `GAME_BIBLE.md` — canonical product thesis and whole-game specification skeleton.
4. `MECHANICS.md` — canonical simulation foundation.
5. `DECISION_ARCHITECTURE.md` — canonical player-decision, contract, support, state, scoring, uncertainty, and acceptance-test layer.
6. `PHASE4_CLOSURE.md` — representative-contract, paper-simulation, exploit-review, and mechanical-freeze evidence.
7. `CONTENT_ARCHITECTURE.md` — canonical launch roster, content counts, campaign, generation, demo, framing, and data schemas.
8. `CROSS_ROUND_FINAL.md` — concept-selection closure.
9. `RESEARCH.md` — market/reference evidence when needed.
10. `TOURNAMENT.md`, `TOURNAMENT_ROUND2.md` — selection history only when needed.

## Completed this cycle

1. Closed Phase 5 in new canonical `CONTENT_ARCHITECTURE.md` without reopening the Phase-4 tick architecture.
2. Locked exact content targets for MVP, public demo, and launch.
3. Locked launch scope at **22 mechanically distinct species**, **4 body plans**, **10 trait families**, **6 supports**, **5 hold families / 12 authored layouts**, **7 route-hazard families**, **48 authored campaign contracts**, and **24 generated/recombined challenge templates**.
4. Defined systematic parameter bands for stress thresholds, contamination profiles, satiety, source/sink magnitude, social effects, ranges, and lifecycle timing.
5. Authored the full 22-species launch roster with body/stage, thresholds/profile, trait composition, role, useful/dangerous partners, lifecycle behavior, readability hook, tier range, and generator exclusions.
6. Preserved the nine mechanically validated Phase-4 species and added 13 compositions using only the frozen grammar.
7. Defined five hold families and prohibited arbitrary procedural topology at launch; generation uses authored layouts plus safe transforms/assignments.
8. Defined seven route-hazard families entirely through existing heat/stress/contamination/wake/power inputs and set tier-based sequencing limits.
9. Structured the campaign as six chapters of eight authored contracts with exact teaching order from orientation through mastery recombination.
10. Defined eight discovery placements and bounded-information rules so campaign progression never depends on blind guessing.
11. Locked the final campaign test `Living Manifest` to use only learned rules and require multiple valid Bronze strategy families.
12. Defined authored-vs-generated content boundaries and a nine-stage deterministic generation pipeline.
13. Added structural solvability proof, medal validation, causal-opacity rejection, transit-significance rejection, anti-template diversity metrics, difficulty calibration, and seed/version freeze records.
14. Defined low-dialogue narrative framing, species memory aids, and tone boundaries.
15. Defined conceptual data schemas for species, trait instances, holds, routes, contracts, flavor variants, and documentation state.
16. Locked a 10-contract, roughly 60–90 minute public demo with explicit included/excluded species, supports, hazards, and holds.
17. Passed the Phase-5 acceptance checklist.

## Important current conclusions

- The project now has a finite launch content target rather than an open-ended creature/content ambition.
- Content variety comes from composition and timing, not new one-off simulation systems.
- Four body plans and ten trait families are currently sufficient for launch; additional ones carry a high burden of proof.
- Generated challenges are an extension of validated authored content, not a random-content engine.
- The campaign teaches every fundamental relationship before asking for mastery recombination.
- Discovery content reveals bounded unknowns and cannot require blind guessing.
- The final campaign test introduces no new rule.
- The overall project remains **in progress** because UX, commercial/economy, technical implementation, whole-game simulation, adversarial review, and specification freeze are still incomplete.

## NEXT ACTION

**Build Phase 6 — UX / Presentation Architecture and first-session experience.**

On the next run:
1. define the complete player-facing state flow from boot/main menu through contract select, planning, launch, transit, causal review, success/retry, unlock, settings, save/load, and campaign completion;
2. define exact mouse-first controls plus keyboard shortcuts, drag/drop, rotation, inspection, overlays, undo/redo, reset, launch confirmation, playback pause/speed/scrub, and post-run navigation;
3. define the authoritative planning-screen layout and information hierarchy: hold, manifest tray, selected-entity inspector, route timeline, objectives, support allowance/power, overlays, warnings, launch status;
4. define transit presentation, animation timing relative to authoritative ticks, event emphasis, speed modes, pause behavior, and rules for never letting visuals change simulation outcomes;
5. define causal-review UX that can explain a failure chain without becoming a spreadsheet: event grouping, timeline, jump-to-cause, organism/cell focus, direct vs propagated effects, and retry-from-last-launch flow;
6. define complete onboarding for the first 10 demo/campaign contracts, including exactly what is taught, when tooltips unlock, what the player must demonstrate before scaffolding is removed, and how discovery cues differ from tutorials;
7. define visual language for body plans, primary states, condition flags, heat/stress/contamination, growth previews, feeding/symbiosis edges, supports, route zones/hazards, unknown information, and medal predicates;
8. define art-direction production grammar for 22 species using reusable silhouettes, state animation sets, palettes/pattern variants, effects, and strict asset-count ceilings;
9. define audio language and non-audio equivalents for every gameplay-critical cue;
10. define accessibility: scalable UI/text, color-independent channels, reduced motion/flashing, playback speed, pause, input remapping, screen-safe event communication, dyslexia-friendly font option if practical, and information-density controls;
11. define gamepad/Steam Deck compatibility boundary without compromising mouse-first PC design;
12. define settings, resolution/aspect behavior, windowed/fullscreen, audio sliders, control rebinding, content-warning boundaries, and localization-safe layout rules;
13. define UX failure/edge cases: illegal drop, impossible support link, overlapping modal, launch with warnings, quit during planning/transit/review, reconnect not applicable, controller disconnect, missing localization, corrupted layout reference fallback;
14. define Phase-6 acceptance tests and a paper walkthrough of first launch -> first contract -> first failure -> causal review -> successful retry;
15. save the result in a canonical UX architecture file and update this status.

Do not start production code. Do not declare the project complete.

## Recovery instruction for a new chat
Read in this order:
1. `START_HERE.md`
2. `STATUS.md`
3. `GAME_BIBLE.md`
4. `MECHANICS.md`
5. `DECISION_ARCHITECTURE.md`
6. `PHASE4_CLOSURE.md`
7. `CONTENT_ARCHITECTURE.md`
8. `CROSS_ROUND_FINAL.md`
9. `RESEARCH.md` only when market/reference evidence is needed
10. `TOURNAMENT.md` and `TOURNAMENT_ROUND2.md` only when concept-selection history is needed

Ignore remembered chat state if it conflicts with the repository. Resume directly from `NEXT ACTION`.