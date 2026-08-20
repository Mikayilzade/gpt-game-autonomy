# GAME #004 — CONTENT ARCHITECTURE

Last updated: 2026-08-21
Factory run: **9**
Phase: **5 — Content Architecture**
Working name: **HUSHLINE** (provisional)
Phase status: **COMPLETE / LOCKED FOR DOWNSTREAM DESIGN**
Production implementation: **NOT STARTED**

This file proves that the locked Phase-3/4 vocabulary can sustain the target campaign without adding a second gameplay pillar. Content is authored from reusable graph, listener, source, barrier, door and objective data. New mechanics are not introduced here.

---

## 1. Content thesis

A HUSHLINE encounter is a compact physical infiltration problem in which the player:
- reads visible acoustic routes;
- physically reaches and moves one barrier along authored slots;
- decides which listener should or should not hear specific actions;
- uses deterministic investigation to create traversal openings;
- resolves the objective and extracts with little or no passive waiting.

The campaign must scale by **recombining route structure, listener thresholds, source strengths, barrier slot topology, door mutations and traversal exposure**, not by inventing one-off gadgets.

A mature encounter is invalid if its meaningful solution is merely `put barrier on the nearest guard-facing doorway and stay quiet`.

---

## 2. Reusable encounter reasoning families

These are reasoning families, not separate mechanics. Most main encounters should combine two or more by the mature campaign.

### F1 — Single-route screening
Teach the barrier physically and causally.
- one relevant source;
- one listener;
- one obvious route;
- one useful barrier slot.

Use only in the opening teaching band. It cannot dominate later content.

### F2 — Alternate-route denial
A listener has two or more acoustic routes. Blocking the visually nearest route is insufficient.
- teaches tied/minimum-route behavior;
- requires reading the whole physical space;
- often paired with different attenuation values.

### F3 — Selective audibility
One event should reach Listener A but not Listener B.
- core mature identity;
- mandatory in main campaign;
- should recur in substantially different physical layouts.

### F4 — Deliberate investigation opening
The player intentionally creates a sound to move a listener away from a traversal/objective region.
- route is player-created, not patrol-waited;
- strength must be physically tied to the chosen source/action;
- return/search timing is short and deterministic.

### F5 — Over-propagation tradeoff
A stronger source is useful for reaching one listener but risks reaching another.
- makes strength-4 actions non-dominant;
- source strength is not menu-selected;
- relies on physical source choice or required objective action.

### F6 — Barrier travel exposure
The correct acoustic edit requires physically reaching a manipulation zone that is not permanently safe.
- world remains live during manipulation;
- exposure comes from layout and listener state, not artificial cooldowns;
- use sparingly enough that direct manipulation remains satisfying rather than tedious.

### F7 — Door-state reroute
A visible door mutation changes both traversal and acoustic graph.
- event ordering uses locked BEFORE_MUTATION / AFTER_MUTATION semantics;
- door state is always visually legible;
- no hidden leaking unless a reusable distinct door archetype is explicitly present.

### F8 — Moving-source pressure
A visible moving environmental source changes where sound originates over time.
- exceptional mature family;
- deterministic authored route;
- used to make routing state evolve without requiring patrol waiting.

### F9 — Threshold split
Two listeners with visibly different hearing thresholds react differently to the same event.
- teaches that selective audibility can come from both routes and thresholds;
- thresholds remain persistent and visible.

### F10 — Sequence preservation
A barrier position that solves the current action makes the next action worse, forcing a planned sequence of local edits.
- protects against one-slot camping;
- should emerge from route/source/objective sequence rather than arbitrary locks.

### F11 — Return-path inversion
The barrier arrangement used to enter or complete the objective is not the correct arrangement for extraction.
- uses the same graph in a changed world state;
- may combine with opened doors, moved listeners or consumed objective sources;
- avoids simple mirrored backtracking by changing one visible state.

### F12 — Multi-event ordering
Two near-term sounds must be triggered in a meaningful order because listener retarget rules and graph state differ.
- never relies on same-tick ambiguity;
- intended order must be readable from preview and listener state.

No additional family should be added during production unless the existing twelve demonstrably fail the campaign-scaling tests and the new proposal survives a design amendment review.

---

## 3. Canonical content data schema

### 3.1 Encounter
Required fields:
- `encounter_id`
- `campaign_band`: TEACH / COMBINE / MATURE / CLIMAX
- `estimated_first_clear_minutes`
- `start_node`
- `exit_node`
- `objective_ids[]`
- `checkpoint_ids[]`
- `reasoning_families[]`
- `required_selective_audibility`: bool
- `target_listener_count`
- `acoustic_node_count`
- `mastery_predicate_ids[]`
- `validator_overrides[]`: normally empty; any use requires explicit documented design amendment

### 3.2 Acoustic node
- `node_id`
- `world_region_id`
- `is_start_region`
- `is_exit_region`
- `is_objective_region`
- `visual_readability_tag`

### 3.3 Acoustic edge
- `edge_id`
- `node_a`
- `node_b`
- `direction`
- `base_attenuation`: 0–2
- `door_id`: optional
- `barrier_slot_id`: optional
- `physical_passage_id`
- `preview_visible`: must be true for every enabled route

### 3.4 Listener
- `listener_id`
- `start_node`
- `hearing_threshold`: 1–3
- `route_id`: optional short deterministic patrol/return route
- `posted_anchor_id`
- `search_duration_band`
- `direct_detection_profile_id`
- `presentation_pattern_id`

Normal mature count: **2**. Three listeners require an exceptional-density justification and validator pass.

### 3.5 Source
- `source_id`
- `source_family`: LOCOMOTION / DISTRACTION / OBJECTIVE / MOVING_ENV
- `strength_band`: 1–4
- `start_node`
- `trigger_type`
- `reusable_or_single_cycle`
- `movement_route_id`: only for MOVING_ENV
- `emission_phase`: BEFORE_MUTATION / AFTER_MUTATION when applicable
- `visual_strength_pattern_id`

### 3.6 Door
- `door_id`
- `edge_id`
- `start_state`: OPEN / CLOSED
- `mutation_trigger_ids[]`
- `visible_state_profile_id`
- `emission_phase_contract` where action-generated sound is involved

Baseline CLOSED means graph/traversal disconnected. A leaking-door archetype is **not introduced in Phase 5**.

### 3.7 Barrier rail / slot
Rail:
- `rail_id`
- `reachable_handle_zone_id`
- `ordered_slot_ids[]`
- `rotation_station_ids[]`: optional
- `safe_manipulation_rating`: SAFE / EXPOSED / TRANSITIONAL

Slot:
- `slot_id`
- `rail_id`
- `edge_id`
- `world_pose`
- `reach_requirement_id`
- `presentation_marker_id`

One barrier instance baseline. All useful slots must map to visible acoustic edges.

### 3.8 Objective
- `objective_id`
- `objective_type`: REACH / INTERACT / RETRIEVE_LIGHT / SABOTAGE_LIGHT / ACTIVATE / EXTRACT
- `node_id`
- `required_order_group`: optional
- `sound_event_id`: optional
- `irreversible_failure_rule`: optional and must be immediately legible

Objective types are light wrappers only. They do not imply inventory, economy or dialogue systems.

### 3.9 Checkpoint
- `checkpoint_id`
- `activation_region/state`
- `safe_state_required`: true
- `snapshot_scope`: canonical full deterministic snapshot

### 3.10 Mastery predicate
Allowed reusable types only:
- `NO_RESTART`
- `TIME_TARGET`
- `MAX_BARRIER_EDITS`
- `SELECTIVE_HEARING(listener_A, listener_B, event_id)`
- `MAX_PASSIVE_WAIT_PERCENT`
- `FAST_MOVE_USAGE_TARGET`

No mastery predicate may modify acoustic rules or unlock a parallel power tree.

---

## 4. Reusable content archetype families

### 4.1 Listener families
Content variation uses the locked listener machine rather than new AI types.

**L-A Posted Watcher**
- stationary anchor;
- threshold 1–3;
- clean teaching/puzzle role.

**L-B Short-Route Watcher**
- deterministic 2–4 node patrol;
- used only when movement adds route interaction;
- patrol cycle should be short enough that waiting is never the intended main solution.

**L-C Investigation-Critical Watcher**
- placement specifically supports deliberate lure displacement;
- often starts posted near an objective choke.

These are encounter roles, not different underlying mechanics.

### 4.2 Source families
**S-A Footstep carrier** — WALK/FAST_MOVE locomotion.
**S-B Fixed lure** — visible environmental distraction, usually strength 2–3.
**S-C Required loud objective** — strength 3–4; campaign uses it to force selective hearing.
**S-D Route-changing source** — deterministic moving source, exceptional mature content only.

Reuse rule: no encounter should require players to memorize bespoke source behavior. Strength and trigger semantics must be visible before use.

### 4.3 Door families
Only one baseline family is currently allowed:
**D-A Binary physical door** — OPEN connected / CLOSED disconnected.

Variation comes from when and why it mutates, not hidden attenuation rules.

### 4.4 Barrier-slot families
**B-A Safe teaching slot** — reachable outside direct exposure; early campaign only.
**B-B Exposed slot** — manipulation occurs while listener movement matters.
**B-C Choice rail** — 3–4 meaningful slots serving different edges.
**B-D Sequential rail** — correct useful slot changes after objective/door/listener state changes.

A rail with many meaningless slots is invalid. Mature rails target **3–5 meaningful snap choices**, not slot spam.

---

## 5. Campaign budget: 34 main encounters

Target selected: **34 main encounters**, inside the locked 30–36 range. This gives enough combinatorial runway without forcing filler.

### Band A — Teaching / identity formation: E01–E07 (7)
Goal: establish exact causal model quickly.

- E01: F1 single-route screening; one posted listener; first barrier choice.
- E02: locomotion band difference; barrier local manipulation during movement.
- E03: F2 alternate-route lesson; one listener, two visible routes.
- E04: first deliberate distraction; F4 investigation opening.
- E05: threshold contrast preview with two listeners but simple geometry.
- E06: first required loud objective; player must pre-route sound.
- E07: first true F3 selective-audibility encounter: one listener should hear, one should not.

By E07 the player must understand that being heard can be correct. If not, campaign onboarding has failed.

### Band B — Combination / confidence: E08–E16 (9)
Goal: combine two reasoning families per encounter without density spikes.

- E08: F2 + F4 alternate route + lure.
- E09: F3 + F9 selective audibility + threshold split.
- E10: F6 exposed barrier manipulation + posted listener.
- E11: F7 first door-state reroute with explicit event ordering.
- E12: F5 over-propagation tradeoff using two fixed source strengths.
- E13: F10 sequence preservation: barrier must move twice for different actions.
- E14: F4 + F6 player-created investigation window while crossing to exposed rail.
- E15: F7 + F3 door mutation changes which listener should hear.
- E16: mini-climax combining F2 + F3 + F10 with two listeners and 7–8 nodes.

### Band C — Mature systemic play: E17–E29 (13)
Goal: 2–3 families per encounter; 8–12 nodes; two listeners normal.

- E17: F11 return-path inversion.
- E18: F12 two-event ordering under retarget rules.
- E19: F9 threshold split + F5 over-propagation.
- E20: F6 exposed rail + F3 selective audibility.
- E21: F7 door mutation + F10 sequence preservation.
- E22: F4 lure + F11 return-path inversion.
- E23: first F8 moving environmental source with otherwise simple graph.
- E24: F8 + F2 moving source plus alternate route.
- E25: F12 event ordering + two listeners; no patrol timing required.
- E26: F3 + F5 + F10 selective hearing across three required actions.
- E27: F6 + F7 + F11 barrier exposure, door reroute and changed extraction state.
- E28: exceptional 3-listener encounter, capped at <=10 nodes; selective audibility across two listener groups.
- E29: mature synthesis with moving source but only two listeners; no new rules.

### Band D — Campaign climaxes: E30–E34 (5)
Goal: prove full vocabulary scales without adding mechanics.

- E30: 10–12 nodes, two listeners, multiple tied minimum routes, F3/F10.
- E31: objective sequence with F7/F12 and required loud action.
- E32: F8 moving source + F11 extraction inversion; barrier must be relocated at least three meaningful times.
- E33: exceptional 3-listener selective-audibility puzzle; no cyclic patrol timing required.
- E34: final synthesis: alternate routes, threshold split, door mutation, deliberate lure, required loud objective, exposed barrier travel and extraction inversion. The intended solution must include at least two moments where a listener **should hear** a sound.

E34 must remain readable at <=12 nodes and must not depend on hidden state, random hearing or long waits.

---

## 6. Optional advanced/remix budget

Target: **8 optional encounters**, expandable to 10 only if production evidence shows low authoring cost.

Optional content may:
- reuse main encounter geometry with changed start state/listener threshold/source availability;
- remix two mature reasoning families at higher density;
- require stricter mastery predicates;
- remove a checkpoint;
- tighten time or barrier-edit budgets.

Optional content may **not**:
- add new barrier powers;
- add new listener AI families;
- add combat;
- add progression currency;
- unlock permanent acoustic upgrades;
- introduce hidden routes/thresholds;
- require audio-only performance.

Suggested R01–R08 mix:
- 2 selective-audibility remixes;
- 2 low-edit optimization remixes;
- 2 no-restart/time-flow remixes;
- 1 moving-source remix;
- 1 three-listener expert remix.

---

## 7. Difficulty/progression ramp

Difficulty increases through **combinatorial responsibility**, not obscurity.

### Early
- 3–6 nodes;
- one listener, then two;
- 2–3 meaningful barrier slots;
- one reasoning family at a time;
- stationary listeners dominate.

### Mid
- 6–9 nodes;
- two listeners normal;
- 3–4 meaningful slots;
- two reasoning families combined;
- short deterministic listener routes permitted;
- first door mutation and threshold splits.

### Mature
- 8–12 nodes;
- two listeners normal;
- 3–5 meaningful slots;
- 2–3 reasoning families combined;
- deliberate lure and selective hearing common;
- moving source occasional;
- extraction may invert earlier route logic.

### Exceptional/climax
- <=12 nodes;
- up to three listeners only with validator approval;
- no more than 3–4 simultaneous decision-relevant acoustic routes on screen;
- complexity comes from sequence and conflicting listener outcomes, not bigger graphs.

Forbidden ramp methods:
- longer patrol cycles;
- faster hidden hearing;
- surprise thresholds;
- arbitrary extra barrier slots;
- more listeners as routine difficulty;
- fake prediction uncertainty.

---

## 8. Content validators

Every encounter must pass deterministic static checks plus authored-solution telemetry checks.

### V01 — Hidden-edge rejection
Every enabled acoustic edge must map to a visible physical passage and be preview-visible.

### V02 — Threshold signaling
Every listener threshold must have the canonical visible pattern. No encounter-local hidden modifier.

### V03 — Node/listener density
- mature nodes <=12;
- listeners <=2 normally;
- 3 requires `exceptional_listener_density=true` and explicit readability review;
- >3 hard reject.

### V04 — Meaningful slot density
Reject rails where >40% of slots are never strategically useful across intended solution variants, or where slot count exceeds five in normal mature content without explicit reason.

### V05 — Permanent nearest-door dominance
For mature content, test each barrier slot as a persistent parking state. Reject if one slot allows completion while keeping every dangerous listener below threshold for all completion-critical sounds without a deliberate hearing requirement.

### V06 — Selective-audibility coverage
Campaign validator:
- E07 or earlier must include selective audibility;
- at least **14 of E17–E34** must require or strongly reward one listener hearing while another does not;
- E34 must require it at least twice.

### V07 — Deliberate-hearing coverage
At least 18/34 main encounters must include a mechanically useful heard event initiated or knowingly caused by the player.

### V08 — Passive-wait ceiling
Using authored reference solutions and later playtest telemetry:
- mature target <15% passive waiting;
- warning at >=15%;
- reject/redesign at >25% representative successful time.

Waiting excludes active barrier manipulation, movement, preview reading during movement, objective interaction and deliberate search-state observation immediately following a player-created lure.

### V09 — Barrier-frequency floor
Warning if meaningful barrier edits average worse than 1 per 60 seconds across a representative first-clear reference path; reject long stretches where the barrier becomes incidental.

### V10 — Physical-reach relevance
At least one meaningful mature barrier edit must require traversal to a local handle zone; reject content functionally solvable as remote graph editing from a safe starting pocket.

### V11 — Bespoke-rule rejection
No encounter-local acoustic modifier, one-off hearing exception, secret material, special frequency or custom listener logic may exist outside canonical schemas.

### V12 — Equal-route preview consistency
If multiple routes tie for minimum attenuation, all must be mechanically represented and previewed; authored content cannot rely on hidden tie-breaking.

### V13 — Door-ordering explicitness
Every door-causing sound event must declare BEFORE_MUTATION or AFTER_MUTATION and pass preview/resolution parity.

### V14 — Brute-force susceptibility
Flag encounters where trying every barrier slot once yields a solution faster than reading the causal state in the authored reference. This is a content-design warning, never grounds for adding restart friction.

### V15 — Silence-everything collapse
Reject mature encounters whose optimal/reference solution contains no strategically useful heard event when that encounter is assigned F3/F4/F5/F9/F12.

### V16 — Repetition fingerprint
For every main encounter compute a content signature:
`reasoning_families + listener_count + node_count_band + source_family_set + door_mutation_count + barrier_slot_count + required_heard_listener_pattern`.

No run of three main encounters may share the same dominant signature, and no exact mature signature should appear more than twice unless one is an intentional tutorial/remix pair.

---

## 9. Authored vs data-driven boundary

### Data-driven/reusable
- node/edge graph;
- attenuation values;
- listener thresholds and deterministic routes;
- source strengths/families;
- barrier rails/slots;
- door state transitions;
- objective predicates;
- mastery predicates;
- checkpoint snapshots;
- validator metadata;
- preview/resolution telemetry hooks.

### Authored
- physical room geometry/readability;
- placement of passages, rails, objectives and listeners;
- intended encounter reasoning composition;
- reference solution(s) and expected alternative-solution space;
- visual staging so the acoustic graph reads as a place rather than a diagram.

### Explicitly not bespoke per encounter
- acoustic formulas;
- listener hearing rules;
- retarget rules;
- barrier attenuation;
- door semantics;
- prediction model;
- fail/restart semantics.

This separation is mandatory for production scalability and test coverage.

---

## 10. Minimum credible asset/content budget

The product should be visually stylized and reuse modular pieces.

Design-level minimum:
- 4–6 modular facility environment kits/visual themes, each capable of producing several encounters without changing mechanics;
- 1 player character set;
- 1 listener base rig/animation set with presentation variants rather than separate AI species;
- 1 barrier family with a small number of physical cosmetic variants;
- 1 binary door family;
- 6–10 reusable distraction/objective prop visual archetypes mapped to canonical source strengths;
- 1 moving-source base family with 2–3 visual wrappers if Phase-5 mature content proves it useful;
- canonical acoustic route/strength/threshold VFX language shared across the whole game.

Avoid unique hero assets for every encounter. A new environment theme must justify readability and pacing, not a new rule.

---

## 11. Demo subset — 20 minute nominal sequence

The demo should use either four compact encounters or a tightly linked four-zone sequence; content architecture assumes **4 encounters** because it best demonstrates quick reset and systemic escalation.

### D01 — 3–4 minutes
- visible footsteps;
- one posted listener;
- one barrier rail with two slots;
- first independent choice within ~2 minutes of boot including minimal intro.

### D02 — 4–5 minutes
- alternate acoustic route;
- one deliberate distraction;
- listener investigation opens traversal.

### D03 — 5 minutes
- two listeners with visible threshold/route difference;
- first required loud objective;
- one door mutation or changed route.

### D04 — 6–7 minutes climax
- 6–8 nodes;
- two listeners;
- one absorber rail with 3–4 meaningful slots;
- player must preserve audibility to Listener A while suppressing Listener B;
- deliberate heard event creates the opening;
- player must physically traverse to reposition barrier before extraction.

Demo failure condition: if D04 can be solved by simply making all completion-critical sounds inaudible, the demo does not represent the product and must be redesigned.

---

## 12. Representative paper-test slots

These paper tests validate campaign scaling using only locked systems.

### P1 — Two-route posted puzzle
6 nodes, 1 listener threshold 2, objective source strength 3, two routes cost 0+1 and 1+0. Barrier can add +3 to either one route, but blocking only one tied path still leaves hearing. Player must first close/open a visible door to remove one route, then place barrier for the objective action.

Uses: F2 + F7. No new mechanics.

### P2 — Useful-hearing threshold split
7 nodes, Listener A threshold 1, Listener B threshold 3. Distraction strength 3. One barrier placement makes A receive intensity 1 and B 0; objective later reverses desired relationship through another path. The same source cannot simply be maximized or silenced.

Uses: F3 + F9 + F10.

### P3 — Active lure instead of wait
8 nodes, two listeners, both posted. Player must trigger a strength-2 source routed only to A, causing A to investigate away from the rail handle. While A moves, player crosses to the handle, repositions barrier and performs strength-4 objective action screened from B but audible to displaced A through a longer route.

Uses: F4 + F6 + F3. Passive waiting is unnecessary.

### P4 — Door-ordering sequence
8 nodes, two listeners. Player interaction opens a door and emits a strength-3 event AFTER_MUTATION, intentionally reaching A through the newly opened edge. A later door-closing interaction emits BEFORE_MUTATION, so the sound uses the still-open route. Both are previewed exactly.

Uses: F7 + F12. Tests canonical ordering without adding rules.

### P5 — Moving-source mature state
9 nodes, one moving source on a deterministic three-node route, two posted listeners. The moving source periodically threatens to reach B through an alternate path. Player's barrier sequence is driven by source position while deliberate lure to A creates the traversal window. No patrol cycle is needed.

Uses: F8 + F2 + F4 + F10.

### P6 — Return-path inversion
9 nodes, two listeners. Entry is solved with barrier on edge X and one deliberate lure. Objective opens a door, changing graph. Returning with barrier still on X causes footsteps to reach B; player must physically reach the rail and move to Y while A is in investigation.

Uses: F11 + F7 + F6.

### P7 — Exceptional three-listener test
10 nodes, three listeners with thresholds 1/2/3. Required loud source strength 4 must reach A, can reach C harmlessly, but must not reach B. Barrier plus base attenuation creates this split. No patrol timing. If visual listener prediction is crowded, this content class is removed rather than increasing UI abstraction.

Uses: F3 + F9. Validates the exceptional ceiling.

### P8 — Final-style synthesis
12 nodes, two listeners, one short deterministic route on A, B posted, one door mutation, one fixed lure, one required loud objective and three meaningful barrier positions. Intended sequence: route lure to A only → traverse to rail → reposition to screen B while objective must still reach A → objective opens door → graph changes → reposition for extraction because footsteps now have a new alternate route.

Uses F2/F3/F4/F6/F7/F10/F11. No new mechanics. This proves the campaign can reach climax density through recombination alone.

Paper-test conclusion: the locked vocabulary supports teaching, combination, mature and climax content without adding a second mechanic family. The main risk is encounter-signature repetition, addressed by V16 plus the campaign allocation.

---

## 13. Content acceptance gates

Phase 5 is considered complete because:
- campaign target is fixed at **34 main encounters** within the 30–36 thesis range;
- 8 optional remix/mastery encounters are defined without a progression economy;
- campaign has explicit teaching, combination, mature and climax bands;
- twelve reusable reasoning families use only Phase-3/4 mechanics;
- reusable schemas cover encounter, graph, listeners, sources, doors, barrier, objectives, checkpoints and mastery;
- normal mature density remains 2 listeners and <=12 nodes; 3 listeners exceptional;
- validators explicitly reject hidden routes, unsignaled thresholds, nearest-door dominance, silence-everything collapse, excessive waiting, barrier scarcity, excessive density and bespoke rules;
- selective audibility and deliberate useful hearing have campaign-level coverage requirements;
- demo subset ends in selective audibility, not generic silence;
- eight representative paper tests demonstrate scaling without new mechanics;
- authored-vs-data-driven boundary is explicit;
- minimum credible asset/content budget remains compact and modular.

**PHASE 5 CONTENT ARCHITECTURE = COMPLETE.**

## NEXT DESIGN HANDOFF
Proceed to **Phase 6 — UX / Presentation Architecture**. Create `GAME4_UX_PRESENTATION.md`. Define camera/readability, world-embedded acoustic prediction, barrier interaction feedback, listener state/threshold language, source-strength language, HUD/minimal overlay boundaries, controls for keyboard/mouse/controller, onboarding from boot through the demo, pause/settings, accessibility and complete no-audio parity, failure/restart/checkpoint presentation, reduced-motion/contrast/simulation-speed behavior, and the visual/audio identity needed to keep the game feeling like physical infiltration rather than graph software. Do not change acoustic mechanics or content schemas for presentation convenience; any contradiction must be documented and resolved explicitly.