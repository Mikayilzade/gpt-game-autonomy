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
- Mechanical architecture complete: **NO — foundation + decision architecture locked; vertical-slice/adversarial closure pending**
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
4. `MECHANICS.md` — canonical Phase-4 simulation foundation.
5. `DECISION_ARCHITECTURE.md` — canonical Phase-4 player-decision, contract, support, state, scoring, uncertainty, and acceptance-test layer.
6. `CROSS_ROUND_FINAL.md` — concept-selection closure.
7. `RESEARCH.md` — market/reference evidence when needed.
8. `TOURNAMENT.md`, `TOURNAMENT_ROUND2.md` — selection history only when needed.

The second Phase-4 appendix was introduced because the decision layer is large enough to remain readable separately from the tick-resolution/simulation foundation. Both mechanical appendices are canonical.

## Completed this cycle

1. Defined exact pre-launch action legality for inspect/place/move/rotate/remove/support-link/undo/redo/reset/launch.
2. Locked planning as free and reversible: no move counter, no real-time planning pressure, no penalty for rearranging before launch.
3. Distinguished structural launch validity from predicted success: known bad setups remain launchable so the player can run deliberate experiments.
4. Defined future-growth warnings without turning growth prediction into an automatic launch blocker.
5. Locked three preview layers: known facts, immediate direct influence preview, and committed transit evidence.
6. Explicitly prohibited full-future auto-simulation, safe/unsafe verdicts, placement recommendations, and solver-like previews before launch.
7. Allowed exact current-state arithmetic assistance where it reduces clerical work without predicting future transitions.
8. Locked the support-resource model to three meaningful constraints only: physical space/fixture topology, utility power capacity, and contract support allowance. No generic per-contract money budget.
9. Defined deterministic brownout power priority chosen before launch.
10. Finalized all six foundation supports: Cooler, Filter, Baffle, Nest Pad, Feed Cartridge, and a redefined Monitor Beacon that trades mitigation for bounded information rather than solving the future.
11. Locked exact behavioral-state precedence and hysteresis for CALM / AGITATED / PANICKED / ASLEEP, including waking, sleep-vs-wake conflicts, stress accumulation during sleep, and orthogonal condition flags.
12. Defined species construction as body plan + thresholds + 1–3 significant reusable traits + optional lifecycle, with composition validator restrictions against self-canceling and self-sustaining loops.
13. Locked a small launch-oriented body-plan grammar (Dot, Domino, Corner, Bar), footprint ceilings, and growth-stage ceilings.
14. Defined a formal contract predicate grammar for final-state goals, timeline conditions, forbidden events, aggregate selectors, mandatory delivery requirements, and optional mastery requirements.
15. Defined a six-tier mechanical difficulty ladder after onboarding, increasing temporal/relationship complexity rather than merely adding organisms.
16. Locked campaign medals to transparent Bronze/Silver/Gold predicate completion with no hidden weighted score, retry punishment, planning-time score, or welfare-hostile efficiency incentives.
17. Defined the information-uncertainty model: DOCUMENTED vs UNDOCUMENTED rules, bounded clues, safe first exposure, permanent documentation after valid observation, and rare bounded route uncertainty.
18. Defined explicit acceptance tests for all four primary behavioral states, all ten foundation trait families, all six support/resource families, preview/contract logic, medals, retry determinism, and discovery transparency.
19. Added hard-reject and design-warning rules for content combinations that are technically valid but mechanically degenerate or unreadable.
20. Created `DECISION_ARCHITECTURE.md` as a canonical Phase-4 appendix.

## Important current conclusions

- The player is now allowed to experiment freely before launch, while meaningful commitment begins exactly at transit launch.
- Preview is deliberately informative but incomplete: it removes clerical arithmetic without solving future ecology.
- Support design is now constrained enough to avoid “equip every mitigation tool” play: space, fixtures, power, allowance, brownouts, and finite capacities create opportunity cost.
- Sleep is not a universal fifth mood layered on top of panic; it is an exclusive primary behavioral override with stress continuing underneath and deterministic wake precedence.
- Species complexity is capped by grammar rather than by hope; most organisms will expose only 1–3 significant traits.
- Contract success and medals are formal Boolean predicates, not opaque scoring formulas.
- Campaign failure/retry remains educational rather than punitive.
- Unknown rules must announce that an unknown exists and be introduced through bounded, non-blind discovery contracts.
- Phase 4 now needs validation/closure rather than more foundational systems.
- The overall project is still **in progress**.

## NEXT ACTION

**Close Phase 4 through representative contracts, paper simulation, and adversarial mechanical review.**

On the next run:
1. define the exact Phase-4 vertical-slice content set: hold geometry, route, support allowance, 8–10 organism instances/species compositions, all numeric placeholder ranges needed for paper simulation, and the subset of traits actually exercised;
2. author at least **six fully specified representative contracts** spanning Orientation / Single Causal Link / Competing Proximity / Temporal Planning / Cascades & Scarce Mitigation / Mastery Recombination;
3. for each representative contract, specify manifest, starting state, route timeline, hold/fixtures, supports, mandatory predicates, Silver/Gold predicates, intended pressure families, at least one known valid layout strategy, and at least one plausible failure cascade;
4. paper-simulate at least two advanced contracts through enough authoritative ticks to validate the exact Phase-A→I ordering and causal log structure;
5. attack self-sustaining food/filter loops, stress-soothing cancellation loops, contamination farming, power-priority exploits, growth-block abuse, infinite/recursive state pulses, isolate-all, universal buffer species, and template reuse;
6. test that every foundation support has at least one contract where it is useful and one where choosing it is inferior to another option;
7. test that Bronze/Silver/Gold incentives never reward worse organism welfare or random brute-force behavior;
8. reconcile any contradiction discovered among `GAME_BIBLE.md`, `MECHANICS.md`, and `DECISION_ARCHITECTURE.md`;
9. if the representative contracts and adversarial pass succeed, mark **Mechanical architecture complete = YES** and move NEXT ACTION to Phase 5 Content Architecture; otherwise repair mechanics first;
10. save all findings in a canonical Phase-4 closure file rather than expanding chat output.

Do not start production code. Do not declare the project complete.

## Recovery instruction for a new chat
Read in this order:
1. `START_HERE.md`
2. `STATUS.md`
3. `GAME_BIBLE.md`
4. `MECHANICS.md`
5. `DECISION_ARCHITECTURE.md`
6. `CROSS_ROUND_FINAL.md`
7. `RESEARCH.md` only when market/reference evidence is needed
8. `TOURNAMENT.md` and `TOURNAMENT_ROUND2.md` only when concept-selection history is needed

Ignore remembered chat state if it conflicts with the repository. Resume directly from `NEXT ACTION`.