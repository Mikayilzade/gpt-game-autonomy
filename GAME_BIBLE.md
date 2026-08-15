# GAME BIBLE

Status: **CONCEPT SELECTED / PRODUCT THESIS LOCKED**
Design complete: **NO**
Last updated: 2026-08-15

This file is the canonical implementation-ready specification for the selected game. `CROSS_ROUND_FINAL.md` contains the selection evidence; this file contains only canonical game decisions and remaining design work.

---

# 1. Product thesis

## Working title
**Organism Cargo** — codename only. Commercial title is intentionally not locked yet.

## One-sentence hook
**Pack living cargo into a tiny transport hold, launch it, then survive the deterministic chain reactions as the organisms grow, eat, sleep, infect, soothe, panic, and change one another during transit.**

## Genre / subgenre
Premium single-player **systemic puzzle / compact strategy simulation** with spatial setup, deterministic short-run simulation, causal diagnosis, and replayable contracts.

It is **not** categorized internally as a packing game. Packing is the setup interface; prediction of a changing living system is the core game.

## Target player
Primary:
- PC players who enjoy compact systems they can understand deeply;
- puzzle/strategy players who enjoy forming hypotheses, testing them, and improving solutions;
- players attracted to satisfying organization but who want consequences beyond static placement;
- players who enjoy short emergent stories produced by simulation rather than long authored narrative.

Secondary:
- optimization/high-score players;
- cozy-task players willing to accept moderate failure and experimentation;
- viewers/streamers who can enjoy visible cascades even without understanding every rule.

Not a primary target:
- players seeking action combat, open-world exploration, large narrative campaigns, competitive multiplayer, or idle progression.

## Primary platform
PC / Steam first.

## Secondary platforms
No secondary platform is promised. Gamepad/Steam Deck viability should be preserved where inexpensive, but PC mouse-first interaction has design priority until UX architecture is complete.

## Core fantasy
**You are the specialist who can safely transport impossible living cargo because you understand how a hold full of strange organisms will evolve after the doors close.**

The fantasy is not animal collection or pet ownership. It is competence: reading traits, planning an initial ecology, committing, watching the consequences unfold, understanding what happened, and making a smarter arrangement.

## Why this game should exist
The game combines several durable satisfactions without inheriting their largest production burdens:
- spatial organization gives immediate physical clarity;
- simulation turns placement into prediction instead of tidying;
- living organisms make state changes intuitive and emotionally readable;
- deterministic outcomes make failures learnable rather than arbitrary;
- short transit runs create visible before/after transformation and shareable cascades;
- modular traits allow many situations from a limited content vocabulary.

The under-served experience is not “another packing puzzle.” It is **designing the starting conditions of a tiny living system, committing to it, and discovering whether your causal model was correct.**

## Core differentiator
**The hold is not solved when the doors close.**

The arrangement is only time-zero. Transit changes organisms and therefore changes adjacency, environmental conditions, needs, hazards, and relationships. A challenge that can normally be solved as a static shape/adjacency checklist violates the product thesis.

## Design pillars

### Pillar 1 — Predictable living cascades
Organisms must behave through learnable deterministic rules. Surprise should come from interaction complexity, not hidden dice.

### Pillar 2 — Setup, commit, observe, explain, improve
The signature rhythm is:
**inspect → hypothesize → arrange/support → commit → simulate → explain → revise.**

The post-run explanation is part of play, not merely a failure screen.

### Pillar 3 — Small vocabulary, deep combinations
A limited set of environmental channels, state transitions, and trait modules should recombine into many meaningful situations. New content should usually add a rule or interaction, not just a cosmetic variant.

### Pillar 4 — Alive at a glance
Every important state change must be readable through organism posture/animation/iconography, hold feedback, and causal overlays. The simulation must look alive even though its rules remain discrete.

### Pillar 5 — Compact competence fantasy
The game should make one small hold feel deep. It must resist pressure to become a ship simulator, colony game, creature collector, logistics empire, or open-world delivery game.

## Explicit anti-pillars
The game must not become:
- a static packing / suitcase / shelf-organization puzzle;
- an inventory autobattler;
- a physics sandbox where outcomes are hard to reproduce;
- a creature-collection treadmill requiring hundreds of bespoke species;
- a pet-care simulator;
- a generic logistics/company-management sim;
- an open-world transport game;
- a roguelite whose depth depends mainly on random upgrades;
- a grind economy with permanent numerical power creep;
- a trial-and-error game where causal explanation is optional;
- a narrative game whose appeal depends on large dialogue volume.

---

# 2. Scope contract

## Production philosophy
- Systemic depth over huge handcrafted content volume.
- Small number of strong player verbs over feature sprawl.
- Recombination over one-off scripted content.
- Readability over visual excess.
- Strong feedback loops over decorative complexity.
- A complete smaller game is preferred to an unfinished ambitious one.

## Locked scope constraints
- Single-player baseline and launch target.
- No mandatory backend/live service.
- Deterministic discrete simulation; no freeform creature physics as a core rule system.
- One primary cargo-hold interaction space per contract.
- Organisms are modular compositions of reusable body/trait/state systems rather than unique code per species.
- Stylized presentation; no photorealism requirement.
- No open world.
- No direct real-time action combat.
- No giant dialogue tree.
- No multiplayer in the base design.
- No monetization model that requires retention manipulation, ads, loot boxes, paid power, or energy timers.

## Scope ceiling
A launch version should be achievable with:
- a small family of cargo-hold layouts;
- a bounded organism body-plan library;
- reusable state animations/effects;
- a data-driven trait grammar;
- contract/route modifiers;
- authored tutorial and milestone contracts plus validated generated/recombined challenges.

If the design begins requiring a large ship interior, explorable stations, crews, combat, hundreds of species, or bespoke animations per organism, scope has escaped and must be cut back.

## Out of scope
Explicitly out of scope unless a later adversarial review proves a tiny version essential:
- multiplayer/co-op;
- PvP;
- first-person walking around the ship;
- piloting/navigation gameplay;
- trading-company simulation;
- breeding/genetics metagame;
- combat between player and creatures;
- procedural open worlds;
- base building;
- romance/NPC relationship systems;
- real-world animal medicine;
- user-generated creature scripting at launch;
- live-service seasons.

---

# 3. Core loop

## Immediate loop — seconds
1. inspect organism/hold/route information;
2. select an organism or support module;
3. place, move, rotate, or inspect it;
4. read direct known effects and space/environment implications;
5. form or revise a prediction.

The immediate reward is increased confidence in a planned living system, not a score popup for every placement.

## Contract loop — roughly 3–8 minutes
1. receive manifest, hold, route, hazards, and objectives;
2. inspect known organism traits/states;
3. arrange organisms and optional support modules;
4. commit to launch;
5. run a short deterministic transit simulation;
6. watch state transitions and cascades;
7. receive success/failure plus a causal timeline;
8. if needed, change the initial setup with a specific hypothesis and rerun;
9. finish when mandatory delivery conditions are met;
10. receive rating based on contract-specific optional goals.

## Session loop — roughly 25–45 minutes
A normal session contains several contracts with a deliberate learning arc:
- one familiar contract to re-enter the rule set;
- one or more contracts combining known traits differently;
- introduction or deeper use of one rule family, route hazard, hold geometry, or support option;
- one higher-complexity contract or optional challenge;
- unlock of knowledge/content rather than raw numerical power.

The player can stop cleanly between contracts.

## Progression loop — hours
Progression expands the possibility space through:
- newly documented organism traits;
- new organism compositions/body plans;
- additional hold geometries;
- route hazards/environmental conditions;
- support modules;
- advanced contract modifiers;
- optional efficiency/welfare/constraint objectives;
- harder combinations of already understood rules.

Permanent progression should primarily unlock **knowledge and new decisions**, not make the player statistically stronger.

## Replay / long-tail loop
Replayability should come from:
- recombined manifests;
- seeded deterministic challenges;
- alternative valid layouts;
- score/medal optimization;
- optional restrictive objectives;
- daily/weekly-style seeds only if they can function without a live backend dependency;
- mastery challenges that use known rules in unfamiliar combinations.

No endless mode is required for design completion. It may be evaluated later if it reuses the same validated systems cheaply.

## Failure philosophy
Failure is evidence, not punishment.

A failed transit should answer:
- what changed first;
- which rule caused it;
- how it propagated;
- which delivery condition failed;
- what remained successful;
- what the player can plausibly change next.

The player should normally be able to retry the same deterministic contract immediately with the same initial conditions and seed.

---

# 4. Player verbs

Current locked high-level verbs:
- inspect;
- select;
- place;
- move;
- rotate where an organism/module supports orientation;
- equip/place a support module;
- review known traits and route conditions;
- commit/launch;
- pause/scrub/review completed transit causality after a run;
- retry/reset contract setup;
- compare result against objectives.

Exact controls, costs, legal targets, edge cases, and interaction rules remain Phase 4 work.

---

# 5. Game state model

TBD in Phase 4/6.

Must eventually identify all major states, including:
- boot;
- main menu;
- new game;
- contract selection;
- pre-transit planning;
- transit simulation;
- post-run causal review;
- contract success;
- recoverable contract failure;
- progression/unlock state;
- paused;
- settings;
- save/load;
- campaign/end state if used.

Transitions must be deterministic and specified.

---

# 6. Challenge and decision architecture

TBD in Phase 4.

Locked direction:
- pressure comes primarily from spatial limits, organism interactions, route hazards, optional efficiency/welfare goals, and commitment before seeing the full cascade;
- luck must not decide transit outcomes for a known initial state;
- later challenges may include incomplete knowledge about newly encountered traits, but uncertainty must be explicit and learnable;
- dominant solutions such as isolate everything, sedate everything, maximize empty space, or use one universal buffer organism must be structurally countered;
- difficulty grows by combining rules and temporal state changes, not merely increasing organism count.

---

# 7. Resources / economy

TBD in Phase 4/7.

Potential resources such as hold power, support slots, contract budget, welfare condition, or consumable support materials must justify themselves through decisions. No generic money/resource layer is mandatory merely because the game has contracts.

---

# 8. Progression

TBD in Phase 4/7.

Locked principles:
- knowledge progression > stat progression;
- unlock new relationships/rules rather than +10% bonuses;
- old organisms/rules should remain relevant in new combinations;
- no grind gate should be required to reach core content.

---

# 9. Content architecture

TBD in Phase 5.

Canonical content families expected:
- organism body plans;
- organism trait modules;
- organism states/state transitions;
- environmental channels;
- hold geometries;
- support modules;
- route hazards/modifiers;
- manifests/contracts;
- mandatory delivery conditions;
- optional scoring objectives;
- tutorial/milestone contracts;
- cosmetic/flavor variants only where inexpensive.

For each family define minimum viable count, launch target count, data fields, generation rules, dependencies, and reuse rules.

---

# 10. Procedural / systemic generation

TBD in Phase 5/8.

Locked generation philosophy:
1. define a deterministic organism/hold/route state;
2. generate or select a candidate manifest and constraints;
3. simulate candidate starting arrangements or construct from a known-valid arrangement;
4. prove at least one valid solution under the allowed content set;
5. reject degenerate cases solved without meaningful transit-state change;
6. reject cases whose causality is too opaque to explain;
7. persist seed/version information for reproducibility.

Procedural generation must create meaningful situations, not random layouts.

---

# 11. Narrative / world / tone

TBD in Phase 5.

Locked boundary: narrative supports the competence fantasy and gives contracts flavor, but the game must remain understandable and enjoyable with flavor text skipped. No large dialogue dependency.

---

# 12. Art direction

TBD in Phase 6.

Locked production boundary:
- stylized readable organisms;
- few reusable body silhouettes/body plans;
- layered patterns/accessories/state effects;
- reusable state animations such as calm, stressed, feeding, sleeping, infected/contaminated, growing, emitting, and recovering;
- visual clarity takes priority over biological realism.

---

# 13. Audio direction

TBD in Phase 6.

Audio must reinforce state changes and causality but every gameplay-critical fact needs a non-audio cue as well.

---

# 14. Camera and controls

TBD in Phase 6.

Mouse-first PC interaction is the current baseline. Free camera movement is not assumed; the whole hold should remain readable with minimal navigation friction.

---

# 15. HUD / menus / UX

TBD in Phase 6.

Key UX obligation already locked: the player must be able to distinguish current direct effects, known conditional effects, actual transit events, and post-run causal explanation without the screen becoming a dependency graph spreadsheet.

---

# 16. Onboarding and learning

TBD in Phase 6.

Locked teaching principle: early organisms have one clear trait each; composite organisms and multi-stage state changes are introduced only after the player can predict the base vocabulary.

---

# 17. Difficulty and accessibility

TBD in Phase 6.

At minimum the final design must provide color-independent information, scalable text/UI, input remapping where practical, reduced flashing/intensity options, and non-audio duplicates for gameplay information.

---

# 18. Save / persistence specification

TBD in Phase 8.

Deterministic contract seeds and content-definition versions must be persisted wherever required to reproduce an in-progress or completed challenge accurately.

---

# 19. Balance model

TBD in Phase 4/7.

Major tuning dimensions will include at least:
- hold size/shape;
- organism count and footprint;
- route tick count;
- state-transition timing;
- environmental production/consumption rates;
- interaction ranges;
- support-module capacity/power/space;
- mandatory delivery thresholds;
- optional scoring constraints;
- retry/knowledge availability.

---

# 20. Commercial / store strategy

Current locked commercial frame:
- premium PC game first;
- no paid power, loot boxes, ad dependency, or manipulative retention systems;
- a downloadable Steam demo is strongly favored because the hook is mechanical and can be proven in a small content slice;
- store/trailer language must emphasize **living cargo changing during transit**, never merely “satisfying packing.”

Demo, pricing, tags, capsule, trailer structure, and release strategy remain Phase 7 work.

---

# 21. Technical architecture

TBD after mechanics stabilize.

Locked direction: discrete deterministic tick-based simulation with data-defined organisms/traits/contracts is preferred. Continuous physics must not become authoritative for gameplay outcomes.

Must eventually specify:
- engine/runtime choice;
- major modules/scenes/states;
- data-driven content model;
- entity/component boundaries if relevant;
- event/message flow;
- input abstraction;
- save serialization;
- procedural seed handling;
- deterministic ordering rules;
- performance budget assumptions;
- target resolution/aspect behavior;
- localization readiness;
- debug/cheat tools required for testing.

---

# 22. QA and acceptance tests

TBD.

The final Bible must include testable statements for each major system, including:
- happy path;
- invalid input;
- boundary values;
- repeated actions;
- interruption;
- save/reload;
- quit/relaunch;
- progression extremes;
- unusual ordering of actions;
- deterministic replay;
- performance stress;
- corrupted/legacy data where relevant.

---

# 23. Vertical slice definition

TBD after mechanical architecture.

The slice must prove dynamic transit, not just attractive packing.

Current primitive validation contract from the final tournament:
- 5x5 grid/hold;
- 8–10 organism tokens;
- 10 modular traits;
- heat, stress, contamination;
- growth and feeding;
- 12 deterministic ticks;
- causal event log;
- 12 known-solvable manifests;
- placeholder icons/colors only.

Primitive pass threshold:
- players can explain failed cascades and propose specific revisions;
- at least half of interesting failures depend on a state change after launch rather than static adjacency.

Primitive kill threshold:
- static inspection solves most cases; or
- transit is only spectacle and is not used as evidence.

This is a later validation specification, not permission to begin production before `DESIGN COMPLETE = YES`.

---

# 24. Release completeness definition

TBD.

Must eventually distinguish:
- prototype complete;
- vertical slice complete;
- alpha;
- beta/content lock;
- release candidate;
- launch-ready.

---

# 25. Open design questions

Concept-selection questions are closed. Current highest-priority unanswered questions are now mechanical:
1. What exact organism trait grammar produces maximum depth with minimum vocabulary?
2. What is the authoritative tick/event ordering model?
3. Which environmental channels are essential and which are redundant?
4. How exactly can organisms grow/change footprint without creating unreadable state?
5. What information is shown pre-launch versus only learned through play?
6. What support modules create genuine trade-offs without becoming universal fixes?
7. What constitutes delivery success, partial success, failure, welfare, and optimization?
8. How are contracts generated/validated without brute-force solver cost exploding?
9. How does the causal timeline remain readable when many events occur on the same tick?
10. How many rules/organisms are needed for hour-10 depth without a content treadmill?

These are the entry questions for Phase 4 Mechanical Architecture.
