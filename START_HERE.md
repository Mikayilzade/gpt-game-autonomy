# START HERE — GPT GAME AUTONOMY FACTORY

## Purpose
This repository is a reusable autonomous **game-design factory**. It is not the long-term home of a finished game's implementation.

The factory repeatedly performs this cycle:
1. search the current market and durable game-design references;
2. generate many distinct candidate concepts;
3. eliminate weak, derivative, overscoped, technically disproportionate, or unmarketable ideas;
4. run a concept tournament;
5. select one game;
6. fully specify it from product thesis through mechanics, content, UX, economy, technical architecture, validation and adversarial review;
7. freeze the design only when another implementation session can build it without inventing important gameplay;
8. create/use a dedicated repository for the finished game;
9. migrate the complete game-specific design and add a detailed autonomous implementation handoff;
10. verify migration;
11. remove the finished game's specific design files from this factory;
12. record the game in `GAME_INDEX.md` and begin the next game from a clean slate.

The repository, not chat memory, is authoritative.

---

## Critical continuation rule
A new design chat must read:
1. `START_HERE.md`
2. `STATUS.md`
3. `GAME_INDEX.md`
4. every additional temporary design file named by `STATUS.md`

Then continue exactly from `NEXT ACTION` in `STATUS.md`.

Do not reconstruct project state from memory when GitHub contains a newer state.

---

## User interaction protocol
The user will often send only:

> го

Interpret this as authorization to perform the next meaningful design step autonomously.

During autonomous work, keep chat output minimal:
- `В процессе.` while the factory is still designing the current game;
- `Завершено.` only when the current game's full design is frozen, migrated safely to its dedicated repository, and the factory has been reset for the next game.

An intermediate phase completing does **not** mean the project is complete.

At the end of every substantial run:
1. save all meaningful research/design work to GitHub;
2. update `STATUS.md` with completed work, current phase, run count when relevant, blockers and exact next action;
3. ensure no important decision exists only in chat.

---

# Factory principles

## 1. Design before production code
Do not begin production implementation inside this factory. Throwaway calculations or tiny validation experiments are allowed only when they inform design and do not become an accidental production codebase.

A finished design moves to a dedicated game repository where implementation happens separately.

## 2. Research first, imitate never
Use current web research when market state, saturation, recent games, tools, platforms, pricing or player expectations matter. Study successful and failed games for:
- player desires;
- proven interaction patterns;
- failure modes;
- saturation;
- production burden;
- replayability;
- readability;
- demo potential;
- marketability.

Do not clone a title. Extract lessons and seek original combinations.

## 3. One coherent game, not a feature dump
Every mechanic must serve the core fantasy, core loop, mastery, meaningful progression, tension, expression, discovery or replayability. Remove features that merely sound cool.

## 4. Scope is a design variable
Prefer depth from rules, interactions, procedural recombination and simulation over huge handcrafted worlds, thousands of bespoke assets, massive dialogue trees or networking infrastructure unless the selected concept truly requires them.

## 5. Hook must be legible
The eventual concept should ideally be understandable through:
- one sentence;
- one screenshot;
- a short GIF/clip;
- or a 10–30 second trailer moment.

## 6. Depth over raw volume
Prefer a small vocabulary of rules that recombine into many situations. Avoid relying on hundreds of one-off levels or assets unless justified.

## 7. Design for implementation by another session
Before freeze, specify enough that a fresh implementation session can answer without guessing:
- exact player goal;
- player verbs;
- state transitions;
- core loops;
- rules and ordering;
- resources/economy;
- progression;
- content families;
- generation rules;
- UX and feedback;
- input/accessibility;
- save/load and recovery;
- balance knobs;
- edge cases;
- deterministic behavior where required;
- test/acceptance criteria;
- explicit out-of-scope boundaries.

## 8. Attack the design repeatedly
Dedicated review passes must ask:
- what is boring?
- what becomes repetitive after hours?
- what is redundant?
- what can be exploited?
- what creates a dominant strategy?
- what contradicts another rule?
- what creates runaway production cost?
- what is unclear to a first-time player?
- what cannot be implemented deterministically from the spec?
- what makes a demo weak?
- what prevents players from explaining failure or success?

## 9. Separate frozen rules from empirical gates
Some questions can only be validated by prototypes/playtests. Those may remain as explicit empirical gates after design freeze, but the underlying gameplay rules must still be specified enough to build the prototype.

## 10. Never contaminate the next game with accidental canon
Completed-game-specific files must leave the factory after successful migration. Historical lessons may stay only if generalized and clearly non-canonical.

---

# Reusable design phases

## Phase 0 — Factory / project foundation
Confirm workflow, constraints, scoring approach, handoff method and completion gates. Factory-level Phase 0 persists across games.

## Phase 1 — Opportunity discovery
Research current and durable patterns. Generate a broad field of genuinely distinct concepts. Identify saturated areas, underserved desires and scope traps.

## Phase 2 — Concept tournament
Stress-test finalists with equal destructive criteria. Compare hooks, minute-to-minute play, hour-10 depth, tutorial burden, technical risk, asset burden, demo strength, derivative risk and likely repetition.

## Phase 3 — Product thesis lock
Select one game and freeze the core identity: target player, platform, genre framing, one-sentence hook, core fantasy, session structure, core loop, differentiator and scope ceiling.

## Phase 4 — Mechanical architecture
Fully specify rules, verbs, state changes, resources, simulation systems, progression logic, challenge generation, win/fail states, difficulty and balancing variables.

## Phase 5 — Content architecture
Define content families, minimum/target counts, data fields, dependencies, generation/validation, reuse rules, authored vs procedural content and expansion boundaries.

## Phase 6 — UX / presentation architecture
Define controls, camera, HUD, menus, onboarding, accessibility, feedback, audio/visual language, pause/settings, save/load, failure/recovery and first-session experience.

## Phase 7 — Economy / retention / commercial model
When relevant, define pricing, progression economy, unlock pacing, achievements, difficulty modes, replay incentives, demo strategy, platform features and monetization boundaries.

## Phase 8 — Technical implementation specification
Define engine/runtime direction when needed, state architecture, conceptual data model, deterministic contracts, persistence, generation contracts, performance assumptions, input abstraction, localization readiness, test hooks and implementation order.

## Phase 9 — Whole-game simulation on paper
Walk through first boot, first minutes, first hour, early mastery, midgame, late game, repeat play and hostile/unusual behavior. Repair contradictions.

## Phase 10 — Adversarial review
Dedicated passes for fun, scope, technical risk, balance exploits, economy exploits, UX ambiguity, content exhaustion, repetition, accessibility, persistence/state corruption and implementation ambiguity.

## Phase 11 — Specification freeze
Every important unknown must be answered or intentionally implementation-flexible. Produce acceptance criteria and an authority order. Set `DESIGN COMPLETE = YES` only when a fresh implementation session should not need to invent important game design.

## Migration gate — move finished game out of factory
After `DESIGN COMPLETE = YES`:
1. create/use a dedicated repository named for the game;
2. copy all canonical game files and relevant validation/history;
3. preserve source hashes/content where practical;
4. add `IMPLEMENTATION_START_HERE.md` and live `IMPLEMENTATION_STATUS.md`;
5. define autonomous implementation phases and completion criteria;
6. verify the migrated authority chain;
7. only then remove game-specific files from this factory;
8. update `GAME_INDEX.md`;
9. reset `STATUS.md` for the next game.

---

# Dedicated game-repository implementation template

A migrated game should normally implement in verified increments:

### 12A — Technical bootstrap
Runnable project, deterministic core foundation, data boundaries, input/persistence skeleton, test harness.

### 12B — Vertical slice
One complete playable loop using tiny content.

### 12C — Core systems complete
All frozen mechanics and interactions.

### 12D — Content population
Full frozen content, preferably data-driven.

### 12E — UX / accessibility / controller / target-device support
All required interaction paths and presentation.

### 12F — Adversarial QA
Persistence, duplicates/idempotency, exploits, edge cases, invalid states, recovery and regression.

### 12G — Empirical gates
Prototype/playtest obligations that were intentionally deferred to implementation.

### 12H — Release candidate
Performance, packaging, final regression, demo/release build and release checklist.

A dedicated implementation repository should report completion only when its own `IMPLEMENTATION COMPLETE = YES`.

---

# Working default product constraints
These are defaults, not eternal laws. Current evidence may justify changing them for a future game.

- Prefer PC/Steam-first premium concepts unless another platform clearly fits better.
- Prefer single-player baseline unless multiplayer is central enough to justify networking and QA cost.
- Prefer stylized/readable presentation with low-to-moderate bespoke asset burden.
- Prefer systemic replayability over enormous handcrafted content volume.
- Avoid marketability that depends mainly on expensive art production.
- Avoid direct trend clones when a microgenre is rapidly filling.
- Require a recognizable hook and a second-order source of depth.

---

# Factory completion semantics

The factory itself is never permanently complete while the user wants more games.

For each game:
- `В процессе` = anything before full design freeze + safe migration + factory reset.
- `Завершено` = that game's design package has been fully frozen and migrated safely to its dedicated implementation repository.

Then the factory immediately becomes ready for the next numbered game.

Continue from `STATUS.md`.
