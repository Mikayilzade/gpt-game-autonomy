# GAME BIBLE

Status: **PRE-CONCEPT / NOT LOCKED**
Design complete: **NO**
Last updated: 2026-08-15

This file will become the canonical implementation-ready specification for the selected game. At this stage it intentionally contains structure, decision criteria, and known project constraints rather than pretending a concept has already been chosen.

---

# 1. Product thesis

## Working title
TBD after concept tournament.

## One-sentence hook
TBD.

## Genre / subgenre
TBD.

## Target player
TBD.

## Primary platform
Working assumption: PC / Steam first.

## Secondary platforms
TBD only after control and UI requirements are understood.

## Core fantasy
TBD.

## Why this game should exist
TBD. Must eventually answer:
- what experience is under-served;
- what familiar player desire it satisfies;
- what distinct twist makes it memorable;
- why the twist changes play rather than merely changing theme.

## Design pillars
TBD. Final set should be small, usually 3–5 pillars.

## Explicit anti-pillars
TBD. Define what the game must not become.

---

# 2. Scope contract

## Production philosophy
- Systemic depth over huge handcrafted content volume.
- Small number of strong player verbs over feature sprawl.
- Recombination over one-off scripted content.
- Readability over visual excess.
- Strong feedback loops over decorative complexity.
- A complete smaller game is preferred to an unfinished ambitious one.

## Working scope constraints
- Single-player baseline.
- No mandatory backend/live service.
- No design that requires hundreds of bespoke 3D character animations to function.
- No open world merely for marketing language.
- No massive dialogue tree unless the selected concept proves narrative is the core mechanic.
- No multiplayer unless its benefit clearly outweighs networking, synchronization, matchmaking, moderation, and QA cost.
- No monetization model that requires manipulative retention mechanics.

## Out-of-scope list
To be locked with final concept.

---

# 3. Core loop

TBD after concept lock.

Must eventually specify:
1. immediate action loop (seconds);
2. encounter/task loop (minutes);
3. session loop (tens of minutes);
4. progression loop (hours);
5. replay/endgame loop if applicable.

Each loop must document:
- input;
- player decision;
- system response;
- feedback;
- reward/cost;
- state change;
- reason to continue.

---

# 4. Player verbs

TBD.

For every verb eventually define:
- trigger/control;
- valid targets;
- invalid targets;
- cost;
- timing;
- feedback;
- interruptibility;
- edge cases;
- upgrades/modifiers;
- interaction with every other major system.

---

# 5. Game state model

TBD.

Must eventually identify all major states, including:
- boot;
- main menu;
- new game;
- active gameplay;
- paused;
- modal interaction;
- success;
- failure;
- transition;
- save/load;
- run/session end;
- meta progression;
- credits/end state if relevant.

Transitions must be deterministic and specified.

---

# 6. Challenge and decision architecture

TBD.

Must answer:
- what creates pressure;
- what information is known vs hidden;
- what trade-offs exist;
- what causes meaningful mistakes;
- what can be mastered;
- how luck affects outcomes;
- how the game prevents obvious dominant strategies;
- how recovery from mistakes works;
- how difficulty scales without only inflating numbers.

---

# 7. Resources / economy

TBD if concept uses resources.

Every resource must eventually have:
- sources;
- sinks;
- storage rules;
- caps;
- exchange relationships;
- scarcity intent;
- UI representation;
- exploit checks;
- progression effects.

No resource should exist only because games in the genre usually have one.

---

# 8. Progression

TBD.

Potential dimensions to decide explicitly:
- run-local progression;
- permanent progression;
- unlock progression;
- skill mastery;
- difficulty progression;
- collection/completion;
- narrative progression;
- cosmetic progression.

Progression must increase possibility space or mastery where possible, not merely inflate stats.

---

# 9. Content architecture

TBD.

Will eventually define all relevant content families, such as:
- levels/rooms/zones;
- objects;
- tools;
- machines;
- enemies/hazards;
- NPCs/customers;
- jobs/contracts;
- modifiers;
- events;
- objectives;
- upgrades;
- collectibles;
- achievements.

For each family define minimum viable count, launch target count, data fields, generation rules, dependencies, and reuse rules.

---

# 10. Procedural / systemic generation

TBD.

If used, specify:
- generation seed behavior;
- allowed building blocks;
- constraints;
- validation;
- solvability rules;
- difficulty parameters;
- repetition protection;
- persistence behavior;
- failure fallback.

Procedural generation must create meaningful situations, not just random layouts.

---

# 11. Narrative / world / tone

TBD only to the extent required by the selected game.

Must define:
- premise;
- tone;
- setting rules;
- narrative delivery method;
- amount of authored text;
- relationship between story and mechanics;
- whether lore is optional or required for comprehension.

The game must remain understandable before lore is read.

---

# 12. Art direction

TBD.

Must eventually specify:
- visual perspective;
- dimensionality (2D/2.5D/3D);
- readability hierarchy;
- palette logic if relevant;
- silhouette rules;
- animation requirements;
- VFX language;
- environmental density;
- UI/world visual separation;
- production shortcuts that preserve identity.

A distinctive art rule-set is preferable to expensive realism.

---

# 13. Audio direction

TBD.

Must define:
- feedback sounds for important actions;
- warning hierarchy;
- ambience;
- music state transitions;
- repetition tolerance;
- mute/volume categories;
- accessibility implications.

---

# 14. Camera and controls

TBD.

Must eventually specify keyboard/mouse baseline and whether gamepad support is required at launch.

For every control:
- default binding;
- rebinding policy;
- hold/toggle behavior;
- conflicts;
- contextual behavior;
- accessibility alternative where important.

---

# 15. HUD / menus / UX

TBD.

Must eventually define screen-by-screen behavior for:
- main menu;
- new/continue game;
- gameplay HUD;
- inventory if any;
- task/goal view;
- upgrade/progression view;
- pause;
- settings;
- save/load;
- success/failure/results;
- tutorial/onboarding;
- confirmation dialogs.

Every visible number/icon must have a reason to exist.

---

# 16. Onboarding and learning

TBD.

Must specify the first:
- 30 seconds;
- 5 minutes;
- 15 minutes;
- first full session.

Prefer teaching by constrained play and feedback rather than long text walls.

---

# 17. Difficulty and accessibility

TBD.

Consider as relevant:
- difficulty modes;
- assist options;
- timing leniency;
- color-independent information;
- text scale;
- motion/camera options;
- flashing reduction;
- remapping;
- subtitles;
- audio-independent cues;
- pause expectations;
- failure penalties.

Accessibility options should avoid breaking core rules where possible, but player access takes priority over purity.

---

# 18. Save / persistence specification

TBD.

Must eventually define:
- what data persists;
- autosave triggers;
- manual save availability;
- number of slots;
- atomicity / corruption recovery expectations;
- save versioning assumptions;
- seed persistence;
- settings storage;
- achievements/stat tracking behavior;
- behavior after crash/forced quit.

---

# 19. Balance model

TBD.

Every major mechanic should expose intentional tuning variables rather than hard-coded magic numbers.

Must eventually include:
- target session length;
- pacing targets;
- expected success/failure bands;
- resource flow targets;
- progression rates;
- difficulty curves;
- anti-snowball / anti-stall rules if relevant;
- dominant-strategy tests.

---

# 20. Commercial / store strategy

TBD after concept selection.

Working assumptions:
- premium PC game is the default commercial model considered first;
- demo may be valuable if the core hook is immediately playable;
- no paid power;
- no loot boxes;
- no design dependency on ads;
- DLC only if future content naturally expands a complete base game.

Must eventually define target price logic, demo boundaries, store tags, capsule/trailer communication, and what the first 10 seconds of a trailer prove.

---

# 21. Technical architecture

TBD after mechanics stabilize.

Must eventually specify at conceptual implementation level:
- engine/runtime choice;
- major modules/scenes/states;
- data-driven content model;
- entity/component boundaries if relevant;
- event/message flow;
- input abstraction;
- save serialization;
- procedural seed handling;
- deterministic vs non-deterministic systems;
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
- performance stress;
- corrupted/legacy data where relevant.

---

# 23. Vertical slice definition

TBD after product thesis lock.

The vertical slice must prove the real core fun and technical risks, not just produce a pretty room.

It should eventually define:
- exact slice content;
- systems included;
- systems intentionally mocked/omitted;
- success criteria;
- failure criteria;
- test questions.

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

Current highest-level unanswered questions:
1. Which core concept wins the tournament?
2. What is the strongest player verb/hook?
3. What is the source of long-term systemic depth?
4. What produces variation without excessive asset/content burden?
5. What is the right balance between cozy satisfaction and pressure/challenge, if that design family survives?
6. Can the hook be communicated instantly in motion and screenshots?
7. Is the game premium single-player, or is there a compelling reason to alter that baseline?

These questions are intentionally unresolved until Phase 1–3 research is complete.
