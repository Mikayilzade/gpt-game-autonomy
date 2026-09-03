# GAME #017 — PHASE 3 PRODUCT THESIS LOCK

Date: 2026-09-04
Selected concept: **THE QUEUE KNOWS**
Status: PRODUCT THESIS LOCKED — MECHANICAL ARCHITECTURE NEXT
Authority: below `START_HERE.md`, `STATUS.md`, `GAME_INDEX.md`, `GAME17_RESEARCH.md`, `GAME17_TOURNAMENT.md`, `GAME17_ROUND_B.md`, `GAME17_ROUND_C.md`.

## 1. Product identity
**Working title:** THE QUEUE KNOWS

**Genre frame:** single-player deterministic deduction / mechanism-design puzzle.

**Platform baseline:** PC / Steam first; full mouse + controller support from the start; Steam Deck readability is a design constraint, not a late porting task.

**Target player:** players who enjoy deduction, compact systemic puzzles, visible cause-and-effect and “design the experiment” thinking, but do not want real-time management stress, deep spreadsheets, free-form detective dialogue or hundreds of bespoke rules.

**One-sentence store hook:**
> Change signs and counter rules in a tiny service hall, watch customers choose their own queues, and use those choices to deduce what each person needs — even when the best experiment makes the line worse on purpose.

## 2. Core fantasy
You are not a queue manager trying to maximize throughput. You are the person designing a tiny public system so that **people reveal useful information through the choices they voluntarily make**.

The fantasy is: **“I changed one visible rule, watched the crowd reorganize, and suddenly understood who these people were.”**

The emotional beat should be a small causal reveal: what looked like crowd chaos becomes interpretable because the player created a discriminating situation.

## 3. Core differentiator
The queue is simultaneously:
- the environment being manipulated;
- the instrument that measures hidden customer needs/types;
- and a stateful system whose congestion can contaminate the measurement.

The player therefore performs **diagnostic mechanism design**, not passive deduction and not conventional queue optimization.

A strong case should create at least one moment where:
1. several hidden candidate types currently behave identically;
2. the player changes a visible hall condition;
3. that intervention causes predicted behavior to diverge;
4. observed choices eliminate candidate types;
5. the intervention may itself alter queue lengths or later behavior, so the player must reason about the measurement they created.

## 4. Session structure
### Campaign session
Typical session: 15–40 minutes, one to four cases.

### Case length targets
- onboarding cases: 2–5 minutes;
- normal cases: 5–12 minutes;
- late synthesis cases: 12–20 minutes;
- mastery/challenge cases may be longer only because of planning depth, never because of waiting or real-time execution.

### Case flow
1. **Brief:** exact operational/deduction goal, constraints, intervention budget.
2. **Inspect:** customers, public candidate-type sets, current counters, visible hall rules.
3. **Predict:** player may inspect what each candidate type would value under known rules, but actual hidden type is not revealed.
4. **Intervene:** change one or more permitted hall levers.
5. **Resolve:** customers choose queues in deterministic tick order; animation follows already-resolved logic.
6. **Observe:** exact behavioral evidence updates customer candidate sets; player can inspect concise reason traces for observed choices without being shown hidden truth.
7. **Repeat** if the case allows another intervention/cohort.
8. **Commit:** identify required customers/types or submit required routing/service claim.
9. **Explain:** success/failure summary shows evidence chain and, after final commitment, exact hidden state as appropriate.

No real-time dexterity, live pausing, staff micromanagement or physics execution.

## 5. Core player verbs
Canonical high-level verbs:
- inspect customer and candidate-type information;
- inspect counter/service properties and current queues;
- place/change an allowed visible intervention (sign/fee flag, opening delay, service-category state, capacity/service-time preset);
- advance/resolve the next deterministic cohort or tick block;
- inspect observed choice evidence and reason trace;
- mark/eliminate candidate types as notes where useful;
- submit the case's required diagnosis/routing claim;
- reset to prior case checkpoint / restart case.

Phase 4 must define exact low-level legality, ordering and state transitions for these verbs.

## 6. Canonical core heuristics — scope ceiling, not final formulas yet
The product targets **five** core customer heuristic families. Phase 4 must specify exact formulas/tie-breaks, but their semantic identities are locked here:

1. **Price** — prioritizes lowest visible fee, then bounded tie-break.
2. **Urgent** — prioritizes shortest predicted completion, ignoring fee.
3. **Routine** — prefers familiar counter unless the delay disadvantage exceeds a visible threshold.
4. **Privacy** — avoids publicly exposing a marked service/category when a feasible more-private route exists.
5. **Convenience** — minimizes walking/transfer burden before completion, then uses a bounded tie-break.

Important boundaries:
- these are deterministic rule models, not personalities or probabilistic AI;
- customers do not secretly change preferences mid-case unless the case explicitly declares a public state transition allowed by the mechanical spec;
- normal campaign content should not casually add a sixth heuristic;
- difficulty comes from populations, intervention timing, congestion, candidate overlap, goals and constraints, not a giant archetype catalogue.

## 7. Hall scope ceiling
Normal campaign baseline:
- 2–3 service counters;
- maximum 10 individually relevant customers visible at once;
- fixed lane/queue slots, not free navigation;
- bounded number of intervention levers per case, normally 1–3;
- no economic management layer;
- no employee roster, hiring, upgrades, construction tree or business simulation;
- no random walk/pathfinding outcome;
- no dialogue-tree interrogation;
- no real-time rush mode required for campaign completion.

Presentation may make the hall charming and lively, but logical state remains compact enough to inspect on Steam Deck.

## 8. Progression thesis
Campaign progression expands **causal relationships**, not raw vocabulary.

### Chapter direction
1. **Visible self-selection:** one intervention cleanly separates types.
2. **Diagnostic contrast:** types that currently pool must be separated deliberately.
3. **Confounded measurement:** congestion caused by the intervention changes later choices.
4. **Sequential cohorts:** early behavior informs later intervention.
5. **Operational separation:** goals sometimes require separating only relevant categories rather than identifying everyone.
6. **Synthesis:** three counters, mixed candidate sets, limited intervention budget and service constraints combine prior ideas.

Phase 5 will define exact content families/counts, but target is approximately **36 campaign cases + 12 optional mastery cases**, with a 6–8 hour first-completion target if empirical testing supports it.

## 9. Demo promise
Target demo: ~25–35 minutes, six cases.

The demo must prove, in order:
1. visible self-selection;
2. deliberate information-gathering intervention;
3. “worse queue on purpose” identity;
4. congestion as a confound;
5. sequential observation/control;
6. first three-counter synthesis.

The demo succeeds only if a new player can explain the game afterward approximately as:
> “You change the queue setup to make different kinds of customers reveal themselves.”

If most players instead describe it as “a queue-management game,” the product thesis has failed and implementation should not compensate by adding management features.

## 10. Fairness / information contract
The deduction must never be statistical guesswork.

Locked principles:
- every customer's actual type belongs to a visible candidate set;
- customers obey deterministic public rule models;
- all state that can affect a choice is inspectable before or after the action at the appropriate time;
- observed behavior can eliminate candidate types only through exact logical inconsistency;
- required diagnosis must be supported by sufficient evidence within the case's allowed action budget;
- multiple successful intervention plans are desirable when logically valid;
- hidden arbitrary exceptions are forbidden;
- explanation uses the same evaluator as gameplay, not handcrafted post-hoc prose.

Phase 4 must specify the exact choice evaluation and tick ordering so that “predicted completion,” queue length and tie-breaks cannot be ambiguous.

## 11. Failure / dead-state thesis
Failure should be understandable and cheap to recover from.

Three categories:
1. **Constraint failure:** a public service constraint is violated (for example wait ceiling). Exact violating state is shown.
2. **Deduction failure:** final committed diagnosis is inconsistent with actual hidden state; explanation shows evidence and truth after commitment according to campaign policy.
3. **Information dead state:** remaining permitted interventions cannot make the required goal uniquely solvable. This may be announced only if an exhaustive mechanical validator can certify it from current state.

No heuristic “you seem stuck” detector may claim impossibility.

Case restart must be instant; later technical specification will define checkpoints/undo policy.

## 12. Presentation thesis
The screen should read as a compact little service hall, not a spreadsheet.

Primary visual language:
- counters as strong landmarks;
- customers as readable tokens/characters with clear queue-slot position;
- interventions as physical/public props: signs, fee marker, opening light, privacy flag, service-time/capacity indicator;
- candidate types as compact icon-backed chips visible on focus, not permanent dense tables;
- reason trace as a short causal chain, e.g. `FREE -> lowest fee -> Counter A`, not algebra.

Crowd motion is feedback only. State resolution must complete independently of animation.

## 13. Controller / Steam Deck thesis
The game must be fully playable without pointer precision.

Baseline navigation:
- focus groups cycle between counters, intervention levers, customers and objective panel;
- selecting a customer opens candidate/reason details;
- intervention values use discrete left/right or radial choices;
- resolution/advance has a dedicated clear action;
- camera remains fixed or only lightly pans/zooms; no free 3D navigation is required.

Deck readability requires the core current state to remain legible without opening more than one secondary detail panel at once.

## 14. Commercial thesis — provisional until Phase 7
Premium single-player, no ads, no microtransactions, no consumable hint currency, no live-service dependency.

Working MSRP assumption for scope planning: **$12.99 USD**, with likely acceptable range $11.99–$14.99 depending on final campaign length/polish. Phase 7 must re-research the market and lock the actual commercial model.

A free Steam demo is part of the product plan because the mechanic benefits from hands-on explanation and the demo can expose the full identity within ~30 minutes.

## 15. Scope exclusions
Explicitly out of scope unless a later phase proves a necessary contradiction repair:
- restaurant/shop tycoon economy;
- staff hiring/scheduling;
- building construction/upgrades;
- procedural endless management mode as core value proposition;
- online multiplayer;
- probabilistic customer AI;
- free-form pathfinding simulation;
- dialogue interrogation;
- narrative branching dependent on hidden social stats;
- deckbuilding/roguelite progression;
- dozens of customer archetypes;
- real-time speed scoring;
- “serve everyone fastest” as the primary objective;
- runner-up mechanics from House Rules or Archive of Almosts.

## 16. Product-thesis acceptance gates
Phase 3 is considered locked because all are answered:
- target player: YES;
- platform baseline: YES;
- genre frame: YES;
- one-sentence hook: YES;
- core fantasy: YES;
- session/case structure: YES;
- high-level verbs: YES;
- differentiator: YES;
- demo promise: YES;
- fairness contract: YES;
- progression direction: YES;
- scope ceiling/exclusions: YES;
- provisional commercial size: YES.

## 17. Empirical gates intentionally deferred
These are implementation/playtest questions, not permission to reinvent the design:
1. Can first-time players understand by case 2 that information, not throughput, is the primary objective?
2. Is a 10-customer cap still readable on Steam Deck at target UI scale?
3. Do five heuristic families create enough distinct cases through hour 6–8 without a sixth archetype?
4. Are exact reason traces explanatory without revealing hidden type prematurely?
5. Does the fixed-slot movement presentation feel alive enough without pathfinding/management spectacle?

If a gate fails later, repair should first simplify/reframe presentation or content. Do not silently convert the game into a management simulator.

---

# PHASE 3 RESULT
**PRODUCT THESIS LOCKED.**

The next authority-building step is **Phase 4 Mechanical Architecture**. It must turn the thesis into exact executable rules: full customer type schema, choice comparator/tie-break order, queue/service timing, fixed-slot movement, intervention legality, cohort/tick resolution order, candidate inference, congestion semantics, service constraints, win/fail/dead states, difficulty knobs, notes/commit/reset semantics, case-state invariants and validator contracts. No production implementation should begin in the factory.
