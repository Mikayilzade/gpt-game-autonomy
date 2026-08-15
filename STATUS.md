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
- Mechanical architecture complete: **NO — foundational simulation grammar locked**
- Content architecture complete: **NO**
- UX architecture complete: **NO**
- Economy/retention/commercial model complete: **NO**
- Technical specification complete: **NO**
- Whole-game consistency review complete: **NO**
- Adversarial review complete: **NO**
- Specification freeze complete: **NO**
- DESIGN COMPLETE: **NO**
- Implementation started: **NO**

## Current phase
**Phase 4 — Mechanical Architecture**

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
2. `STATUS.md` — current state and next action.
3. `GAME_BIBLE.md` — canonical product thesis and whole-game specification skeleton.
4. `MECHANICS.md` — canonical Phase-4 mechanical architecture appendix.
5. `CROSS_ROUND_FINAL.md` — concept-selection closure.
6. `RESEARCH.md` — market/reference evidence when needed.
7. `TOURNAMENT.md`, `TOURNAMENT_ROUND2.md` — selection history only when needed.

`MECHANICS.md` was introduced because the simulation grammar exceeded a useful single-section size. It is canonical, not scratch notes.

## Completed this cycle

1. Defined the authoritative 2D orthogonal hold topology, occupancy invariants, body footprints, orientation, Manhattan distance, adjacency, range, and limited directed line-of-effect rules.
2. Locked a deterministic integer-tick transit model with exact global phase ordering from route input through environmental propagation, interactions, internal meters, threshold transitions, consequences, and contract evaluation.
3. Reduced the foundation to three spatial environmental channels only: **heat, stress field, contamination**, with explicit mechanical roles and a ban on redundant extra channels without later proof.
4. Defined organism instance structure, foundation meters, behavioral states, condition flags, growth stages, and delivery-condition hooks.
5. Defined stress hysteresis, contamination load, satiety, sleep, criticality, and deterministic state-transition principles.
6. Created a reusable trait grammar and ten foundation trait archetypes covering emissions, sinks, alarm/soothing, contamination, feeding, growth, symbiosis, and reactive state pulses.
7. Locked simultaneous-effect rules, stable tie-breaking, capacity-limited target selection, threshold batching, and restrictions on non-deterministic targeting.
8. Defined discrete growth/footprint-change behavior with predeclared future cells, no automatic pushing, and explicit growth-blocked consequences.
9. Defined deterministic feeding and compatibility allocation without freeform organism movement.
10. Defined six foundation route-hazard families and six candidate support-module families.
11. Defined pre-launch validity, fail-fast philosophy, end-of-transit mandatory predicates, and optional objective structure.
12. Defined the causal event-log schema needed to explain full cascade chains after transit.
13. Attacked universal strategies: isolate-all, sedate-all, maximum empty space, universal buffer organisms, and reusable one-layout templates.
14. Locked determinism invariants, edge-case rules, and invalid-content rejection requirements.
15. Defined challenge-pressure families, a worked multi-tick cascade example, exposed balance variables, and twelve mechanical validation gates.
16. Created `MECHANICS.md` as the canonical implementation-oriented Phase-4 appendix.

## Important current conclusions

- Dynamic transit is now specified as an ordered deterministic simulation rather than an informal concept.
- Three environmental channels are enough for the foundation; additional channels would currently add teaching burden faster than depth.
- Organisms do not move autonomously during transit in the base design. Temporal change comes from meters, emissions, state transitions, feeding, hazards, and footprint growth.
- Growth never pushes neighbors or searches for arbitrary free space; future footprint must be planned.
- Same-tick effects are batched so entity iteration order cannot silently change results.
- Post-run causal explanation is structurally supported by event records rather than handcrafted failure text.
- The mechanics deliberately require beneficial proximity as well as separation pressure, preventing static “space everything apart” play.
- Phase 4 remains incomplete; the project is still **in progress**.

## NEXT ACTION

**Continue Phase 4 — decision architecture, states, resources, and contract language.**

On the next run:
1. define exact pre-launch player action legality, including placement, move, rotate, support assignment, undo/reset, and launch validity;
2. define prediction/preview rules: what the UI may calculate before launch without turning the game into an automatic solver;
3. lock the support-resource model by choosing how space, fixture slots, power, and/or contract allowance constrain supports;
4. define the complete primary behavioral-state precedence and transition table, including CALM/AGITATED/PANICKED/ASLEEP interactions and condition flags;
5. define species/body-plan composition rules and trait-count/compatibility restrictions so procedural content remains readable;
6. define a formal contract predicate grammar for mandatory goals, timeline conditions, forbidden events, and optional objectives;
7. define the mechanical difficulty ladder from tutorial to mastery without relying on organism-count inflation;
8. define scoring/medal principles and eliminate scoring incentives that conflict with welfare/causal play;
9. define the information-uncertainty model for newly introduced traits and what may remain unknown before first successful observation;
10. finalize the foundation support roster or explicitly cut weak supports;
11. specify mechanical acceptance tests for each foundation trait and state family;
12. update `MECHANICS.md` and this file, preserving exposed numeric balance variables rather than inventing false precision.

Do not start production code. Do not declare the project complete.

## Recovery instruction for a new chat
Read in this order:
1. `START_HERE.md`
2. `STATUS.md`
3. `GAME_BIBLE.md`
4. `MECHANICS.md`
5. `CROSS_ROUND_FINAL.md`
6. `RESEARCH.md` only when market/reference evidence is needed
7. `TOURNAMENT.md` and `TOURNAMENT_ROUND2.md` only when concept-selection history is needed

Ignore remembered chat state if it conflicts with the repository. Resume directly from `NEXT ACTION`.
