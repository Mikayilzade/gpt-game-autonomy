# GAME #005 — MECHANICAL ARCHITECTURE

Last updated: 2026-08-23
Factory run: **8**
Phase: **4 — Mechanical Architecture**
Selected concept: **G5C02 — Tension Budget**
Commercial title: **TBD**
Production implementation: **NOT STARTED**

# PHASE 4 STATUS = COMPLETE

This file freezes the authoritative gameplay rules beneath the Phase-3 Product Thesis. It defines deterministic state, ordering, traversal contracts, load behavior, mutation, restart and validation. It intentionally does not specify final content counts beyond already-frozen scope, final UX presentation, commercial details or engine architecture.

---

# 1. Mechanical north star

The game must always feel like this causal sentence:

> **I move one local tension carriage, the rig redistributes a fixed amount of pull, several connected loads visibly change, and I physically traverse the temporary compromise I created.**

A valid mechanic supports that sentence. A mechanic that requires numeric optimization, hidden simulation, precision timing, free rope manipulation, remote graph editing or a second action pillar does not.

The player wins by reasoning about visible state transitions and spatial commitment, not by dexterity, waiting for cycles or calculating engineering values.

---

# 2. Authoritative encounter state model

Each encounter owns exactly one `RigSystem` baseline.

## 2.1 Encounter state tuple

Authoritative gameplay state is conceptually:

`EncounterState = (phase, revision, anchor_band, load_bands[], player_region, objective_state, checkpoint_id)`

Where:
- `phase` = PRE_OBJECTIVE / MUTATING / POST_OBJECTIVE / COMPLETE;
- `revision` = current authored rig revision, normally A before objective and optionally B after one visible mutation;
- `anchor_band` = committed snap-band index on the physical rail;
- `load_bands[]` = derived SLACK / TAUT / HIGH state for each active load;
- `player_region` = current authored walkable connectivity region;
- `objective_state` = NOT_DONE / DONE;
- `checkpoint_id` = current restart authority.

`load_bands[]` is never independently edited by gameplay. It is derived from `(revision, anchor_band)`.

## 2.2 Normal scope

A normal encounter uses:
- one local physical tension carriage;
- one short rail;
- **3–5 snap bands**;
- **2–4 active loads**;
- exactly three canonical cable/load bands: SLACK / TAUT / HIGH;
- baseline load archetypes only: Lift / Counterweighted Gate / Flexible Span;
- zero or one irreversible objective mutation.

Multiple independently controlled tension carriages are not baseline content and remain out of scope.

---

# 3. Internal shared-budget model

The player never sees numbers, but implementation may use a tiny integer model to guarantee deterministic conservation.

## 3.1 Pull quanta

Internally each active load receives an allocation:
- `0 = SLACK`
- `1 = TAUT`
- `2 = HIGH`

For rig revision `R` and committed anchor band `P`, the authored distribution is:

`D[R,P] = [q1, q2, ... qN]`, with every `qi ∈ {0,1,2}`.

The total budget is:

`B = Σ qi`

and **must be identical for every legal anchor band in every revision of the same encounter**.

The integer model exists only to validate conservation. Player-facing presentation must remain fully nonnumeric.

## 3.2 Initial budget convention

For the pre-objective revision, default authoring convention is:

`B = number of active pre-objective loads`.

This makes an all-TAUT distribution physically possible when useful and gives a simple conceptual center of gravity.

This is a default content rule rather than a player-visible law. If a future authored exception is ever needed, Phase 5 must justify it explicitly and preserve all validation rules; Phase 4 does not assume such exceptions.

## 3.3 Mutation preserves budget

If an objective removes a load, the encounter does **not** lose tension budget. The same `B` is redistributed among the remaining loads.

If an objective adds a load, the same `B` is spread across more loads.

That is the mechanical reason an apparently familiar anchor position can mean something different after mutation.

## 3.4 Distribution table is authored, not simulated

The authoritative mapping from anchor band to allocation vector is authored data.

No free rope force solver determines gameplay state.

For every revision:
- every band has one explicit allocation vector;
- the vector sum must equal `B`;
- each load state is deterministic;
- no randomness participates in redistribution;
- save/load/restart reconstruct exactly the same vector.

---

# 4. Anchor rail and snap-band rules

## 4.1 Physical form

The carriage is a local world object on one short axis.

Player flow:
1. enter interaction range;
2. press/hold Interact;
3. carriage enters GRABBED_PREVIEW;
4. player moves it along the short rail;
5. nearby snap bands provide strong tactile/visual attraction;
6. release commits to the nearest legal band;
7. the rig transitions to the derived target distribution.

No remote control is allowed.

## 4.2 Authoritative anchor states

Only snapped bands are authoritative.

Continuous rail position while held is presentation/preview state only.

A normal meaningful grab-to-snap action should later tune toward roughly 2–3 seconds once the player is at the carriage, preserving the Phase-3 empirical gate.

## 4.3 Adjacent-band conservation rule

For normal content, moving from one snap band to an adjacent snap band must transfer exactly **one internal pull quantum** from one load to another:
- exactly one load decreases by 1 band;
- exactly one other load increases by 1 band;
- all other loads remain unchanged.

Therefore adjacent vectors differ by one local give/take exchange, not by an arbitrary whole-rig reshuffle.

This rule is mechanically important because it makes continuous carriage travel readable: one part visibly gives while another takes.

A later content phase may not bypass this merely to create harder lookup tables.

## 4.4 No duplicate snap states

Two snap bands in the same revision may not resolve to identical allocation vectors.

A band that does not change any gameplay-relevant world state is invalid.

## 4.5 Preview contract

While the carriage is held:
- the last committed state remains authoritative for traversal/collision;
- connected cable/load destination poses may preview continuously;
- preview is visually obvious as manipulation-in-progress;
- preview does not create temporary traversal opportunities;
- the player cannot exploit an in-between rail coordinate as a fourth tension band;
- release resolves deterministically to one snap band.

This prevents “hover between states to squeeze through” exploits and keeps gameplay discrete.

## 4.6 Interaction locking

The carriage can be grabbed only when the rig is STABLE.

It cannot be grabbed during:
- committed load transition;
- objective mutation;
- checkpoint reconstruction;
- encounter completion transition.

---

# 5. Commit and transition ordering

Every anchor commit follows this deterministic ordering.

## 5.1 Commit sequence

1. Player releases carriage.
2. Resolve nearest legal snap band.
3. If it equals current band, return to STABLE with no mechanical state change.
4. Validate commit safety.
5. Snapshot old committed band and derived load states.
6. Set new committed anchor band.
7. Resolve target distribution vector from current rig revision.
8. Emit anchor-commit causal feedback.
9. Cable/tension hardware begins the visible state change first.
10. Affected loads move toward their authored destination poses.
11. Traversal permissions update according to per-load transition rules below.
12. When all affected loads settle, RigSystem returns to STABLE.

No gameplay-critical randomness or frame-order dependence is allowed.

## 5.2 Timing is not a puzzle resource

Transition durations are presentation/balance knobs, not a reasoning mechanic.

A valid level may never require:
- slipping through a gate before it finishes moving;
- jumping from a lift at the exact frame;
- entering a span during a transient pose;
- repeatedly cycling the anchor to exploit moving collision.

The player may begin walking toward the next route during a short transition, but the solution must remain correct if transitions are shortened by a reduced-motion accessibility option.

---

# 6. Load archetype rules

The three archetypes are mechanical canon.

Each load owns:
- one stable world pose for SLACK;
- one stable world pose for TAUT;
- one stable world pose for HIGH;
- deterministic kinematic interpolation between poses;
- explicit collision/traversal semantics for every stable pose and transition.

No load uses dynamic rope/rigid-body chaos as authoritative puzzle state.

---

## 6.1 Lift

### Stable response
- **SLACK → LOW dock**
- **TAUT → MID dock**
- **HIGH → HIGH dock**

Exact heights are authored but clearly discrete.

### Traversal
- lift deck is solid in every state;
- the player may stand on and ride the lift during transition;
- player motion is carried kinematically with the deck;
- exits/landings are valid only where the current stable dock aligns with authored walkable geometry;
- no jump is required to board or leave a legal dock.

### Safety
- no crushing state is legal;
- lift swept volume may not intersect solid world geometry in a way that traps/damages the player;
- if a player can legally stand on the lift, every authored transition must transport them safely;
- a valid solution must not depend on stepping off during motion.

### Mechanical role
Lift provides ordered spatial height/position changes and supports:
- route creation;
- traversal commitment;
- player-location-dependent value of the same tension distribution;
- repeated-instance competition in later content.

---

## 6.2 Counterweighted Gate

### Stable response
Gate exposes three authored clearance tiers:
- **SLACK → CLEARANCE 0**
- **TAUT → CLEARANCE 1**
- **HIGH → CLEARANCE 2**

The world shows these as three unmistakable vertical/mechanical positions.

### Traversal
A gate-linked passage declares required clearance:
- ordinary player walkway usually requires tier 1;
- selected machinery/large-path alignment may require tier 2;
- tier 0 blocks passage.

The player does not crouch or perform precision movement to exploit partial gaps.

### Transition rule
- opening clearance becomes traversable only when the required stable clearance is reached;
- closing clearance blocks before a player can enter the swept zone;
- content must place anchor interaction zones so a legal commit cannot crush the player with a gate transition;
- if this cannot be guaranteed, the authored arrangement is invalid.

### Mechanical role
Gate provides monotonic clearance tradeoffs. Its depth comes from sharing the budget with other loads, not from a separate timing mini-game.

---

## 6.3 Flexible Span

### Stable response
- **SLACK → DEEP SAG / NOT TRAVERSABLE**
- **TAUT → USABLE LEVEL SPAN / TRAVERSABLE**
- **HIGH → OVER-LIFTED / TOO STEEP / NOT TRAVERSABLE**

The TAUT state is intentionally the useful middle state.

### Traversal
- only the stable TAUT pose creates a legal walking connection;
- SLACK and HIGH present clear physical barriers/geometry that prevent entering the span as a normal route;
- no balancing, jumping or timing skill is required;
- the player cannot exploit interpolation during a tension transition.

### Transition safety
Because the player must be at the local anchor to change the rig, normal layouts should not allow the player to be standing on a span that is changing.

If a layout could place the player on a span during a legal commit through unusual geometry, that authored state is invalid unless deterministic safe displacement is explicitly specified later. Baseline content should simply avoid it.

### Mechanical role
Span is the canonical proof that “more tension” is not always better. It creates middle-state reasoning without extra resources or rules.

---

# 7. Player movement and interaction contract

Movement exists to let spatial commitment matter; it is not a mastery pillar.

## 7.1 Baseline movement

Required verbs:
- walk in 8-direction/analog top-down space;
- interact/grab;
- release/confirm anchor placement;
- activate simple objective interaction;
- restart/checkpoint command.

Not required:
- jump;
- dash;
- crouch;
- wall-climb;
- combat;
- physics grabbing of generic objects;
- precision ledge traversal.

If implementation later adds purely cosmetic locomotion polish, it may not become completion-critical.

## 7.2 World edges

The suspended setting must not turn ordinary navigation into repeated fall/death friction.

Use authored barriers, clear edge language and non-traversable geometry so walking off valid routes is not a precision hazard.

Falling is not needed as a core fail state.

## 7.3 Interaction priority

When the player is inside an anchor interaction zone, the anchor is the dominant interactable unless an explicit objective interaction has higher local priority.

There must be no ambiguous “grab wrong mechanism” problem.

---

# 8. Rig revisions and objective mutation

## 8.1 Mutation purpose

A mutation exists to change the meaning of the same shared budget after the player has spatially committed.

It is not a random event or surprise rule.

## 8.2 Baseline mutation count

A normal encounter may have:
- zero mutations for teaching/simple content;
- **at most one irreversible completion-relevant mutation** for normal mature content.

Multiple sequential mutations are not baseline Phase-4 mechanics and should not be introduced later merely to extend puzzle length.

## 8.3 Legal mutations

Baseline mutation may:
- visibly remove one active load from the shared rig; or
- visibly add one already-present/in-world load into the shared rig.

The event must be physically legible, e.g. counterweight detaches, latch couples a span, cable clutch engages/disengages.

It may not silently alter a distribution table with no world event.

## 8.4 Mutation ordering

1. Player reaches and activates objective.
2. Objective locks further interaction temporarily.
3. Current anchor band remains physically where it is.
4. Rig enters MUTATING.
5. World visibly adds/removes the load.
6. Revision changes A → B.
7. At the same committed anchor band, the new revision distribution is resolved.
8. The unchanged total budget redistributes across the new active-load set.
9. Affected cables and loads transition using normal causal ordering.
10. Rig stabilizes.
11. Post-objective checkpoint becomes authoritative.
12. Player resumes control for extraction.

This is the canonical source of return inversion.

## 8.5 Revision data constraints

Every rig revision must:
- preserve the same `B`;
- use the same rail and snap-band count;
- preserve anchor-band physical identity/location;
- provide a legal distribution vector for every snap band;
- obey SLACK/TAUT/HIGH bounds;
- obey adjacent-band one-quantum transfer rule;
- remain visually legible.

A revision may not secretly remap snap-band labels or reverse rail controls.

---

# 9. Traversal state graph

Mechanical solvability is modeled as discrete spatial connectivity.

## 9.1 Player regions

Each encounter may be represented by authored walkable regions connected by conditional edges.

Examples of conditional edges:
- Lift at a docking state connects two regions;
- Gate clearance at/above requirement opens a region edge;
- Flexible Span at TAUT opens a region edge.

The player still moves normally in the world; the region graph is an authoring/validation abstraction, not a visible UI.

## 9.2 Meaningful anchor commit

An anchor commit is mechanically meaningful when it changes at least one completion-relevant traversal edge or future rig consequence.

Because budget is conserved, every adjacent meaningful snap move normally changes at least two load bands.

## 9.3 Mature encounter signature

After early teaching content, a mature encounter should normally require at least two meaningful anchor commits separated by one or more of:
- player entering a different traversal region;
- objective mutation;
- change in accessible anchor approach;
- changed value of the same distribution due to player location.

This is a content constraint carried forward from the anti-enumeration thesis.

---

# 10. Safe static socket enumeration — exact rejection rule

The game does not hide preview information and does not punish experimentation. Therefore mature content must prevent one safe anchor station from becoming a complete lookup table.

## 10.1 Failure pattern

A mature encounter is invalid if there exists a solution where:
1. the player can stand in one permanently safe anchor-access region;
2. preview every snap band without any meaningful traversal or mutation;
3. infer the entire completion path from those static previews;
4. make one final selected commit;
5. complete the encounter without a later materially different anchor decision.

## 10.2 Strong mature-content requirement

For mature content, the intended completion path must contain at least one **decision-separating event** after an anchor commit and before another required anchor decision.

Legal decision-separating events:
- traversal to another meaningful region;
- riding a Lift into a spatially committed position;
- crossing a TAUT Span that changes which paths/anchor approaches matter;
- passing a Gate such that the next choice is spatially separated;
- visible rig mutation;
- return inversion after objective.

## 10.3 What is not allowed as anti-enumeration

Do not solve enumeration by:
- hiding future load states;
- randomizing outcomes;
- adding attempt counters;
- charging resources for anchor moves;
- making previews inaccurate;
- slowing transitions to punish experimentation.

The world remains honest; encounter structure provides the depth.

---

# 11. Invalid / ambiguous authoring states

A level/revision is invalid if any of the following is true.

## Budget / distribution
- distribution sum differs from encounter budget;
- allocation outside 0–2;
- two snap bands have identical distributions;
- an adjacent band changes more than one quantum transfer pair;
- a mutation revision cannot preserve the same budget without exceeding load band limits.

## Visual truth
- two mechanically different load bands are visually indistinguishable at normal camera scale;
- a cable says one band while its load response shows another;
- a preview suggests a route that committed collision does not create;
- color/audio is required to distinguish authoritative state.

## Traversal
- solution relies on transitional collision or timing;
- player can be crushed by a legal commit;
- Lift motion can trap player in world geometry;
- Flexible Span interpolation is exploitable as temporary traversal;
- a gate partial gap can be precision-squeezed despite not meeting clearance requirement;
- player can become permanently softlocked without an available restart.

## Puzzle integrity
- mature encounter is solved by one permanent best anchor band;
- all completion-critical reasoning can be exhausted safely from one anchor station before any meaningful state change;
- WAIT is a meaningful route to a different authoritative tension state;
- a nominally different anchor band has no completion-relevant consequence;
- an objective mutation changes rules invisibly.

## Scope
- solution requires a fourth load archetype introduced only for novelty;
- free rope placement or physics chaos determines the answer;
- player needs calculations/numbers to disambiguate legal states;
- additional movement tech is required to make a route work.

---

# 12. Win, fail, reset and checkpoints

## 12.1 Encounter win

Baseline encounter completion condition:
- required objective state satisfied if the encounter has an objective; and
- player reaches the authored exit region in a stable valid rig state.

Teaching encounters may omit an objective mutation and simply require reaching the exit.

## 12.2 Failure philosophy

The puzzle may produce a bad temporary configuration or strand the player spatially. That is a reasoning dead end, not a punitive death system.

Primary recovery is restart/checkpoint.

No lives, resource loss or long replay penalty is allowed.

## 12.3 Checkpoint C0 — encounter entry

At encounter start, save:
- revision A;
- initial anchor band;
- objective NOT_DONE;
- stable derived load states;
- safe player spawn region/transform.

Restart before objective returns exactly to C0.

## 12.4 Checkpoint C1 — post-mutation

If an objective mutation occurs, once the mutation transition is stable:
- revision B;
- unchanged committed anchor band;
- objective DONE;
- newly derived load states;
- safe post-objective player transform

become checkpoint C1.

Restart after objective returns to C1 rather than forcing the player to repeat the solved entry half.

This protects late return-inversion puzzles from replay fatigue.

## 12.5 Restart determinism

Restart must reconstruct state exactly. No residual transform velocity, rope state, animation phase or random seed may change puzzle truth.

---

# 13. Sequencing and state-machine rules

## 13.1 RigSystem states

Conceptual finite state machine:
- `STABLE`
- `GRABBED_PREVIEW`
- `COMMIT_TRANSITION`
- `MUTATING`
- `RESTORING_CHECKPOINT`
- `LOCKED_COMPLETE`

Legal transitions:
- STABLE → GRABBED_PREVIEW
- GRABBED_PREVIEW → STABLE (cancel/same band)
- GRABBED_PREVIEW → COMMIT_TRANSITION
- COMMIT_TRANSITION → STABLE
- STABLE → MUTATING
- MUTATING → STABLE
- any non-complete recoverable state → RESTORING_CHECKPOINT
- RESTORING_CHECKPOINT → STABLE
- STABLE → LOCKED_COMPLETE when exit condition is met.

No nested commit/mutation is allowed.

## 13.2 Objective interaction

Objective interaction is allowed only while RigSystem is STABLE.

If player reaches objective during a short committed transition, interaction waits until stability rather than creating simultaneous state changes.

## 13.3 Exit interaction

Exit completion checks only stable authoritative state. The player cannot trigger completion through a temporary preview or transition pose.

---

# 14. Exact content-data contract needed later

Phase 5/8 may choose exact file formats, but every encounter must be expressible using these conceptual fields.

## Encounter
- encounter_id
- snap_band_count (3–5)
- budget_B
- initial_anchor_band
- load_definitions[]
- revision_A
- optional revision_B
- objective_mode (NONE / REMOVE_LOAD / ADD_LOAD)
- objective_load_id if applicable
- player_regions[]
- traversal_edges[]
- anchor_interaction_region
- entry_checkpoint
- post_mutation_checkpoint if applicable
- exit_region
- difficulty/pacing metadata later

## Load definition
- load_id
- archetype (LIFT / GATE / SPAN)
- SLACK pose
- TAUT pose
- HIGH pose
- transition path
- collision/traversal metadata
- visual-state motif references later

## Rig revision
- active_load_ids[]
- distribution_by_anchor_band[]

The derived world state must be fully reconstructible from authored data plus current encounter state.

---

# 15. Frozen rules vs balance/feel knobs

## 15.1 Frozen mechanics

The following are mechanical canon after Phase 4:
- one local anchor rail baseline;
- 3–5 committed snap bands;
- 2–4 active loads;
- internal 0/1/2 mapping to SLACK/TAUT/HIGH;
- fixed shared budget per encounter across revisions;
- authored deterministic distribution vectors;
- adjacent snap bands transfer exactly one pull quantum between exactly two loads;
- preview is non-authoritative for traversal/collision;
- exactly three baseline load archetypes;
- Lift low/mid/high dock response;
- Gate clearance 0/1/2 response;
- Span only TAUT is normally traversable;
- no solution based on transition timing;
- zero or one baseline objective mutation;
- mutation preserves rail identity, snap count and total budget;
- checkpoint after stable mutation;
- walk/interact/restart movement vocabulary; no movement mastery pillar;
- honest previews and structural anti-enumeration rather than hidden information.

## 15.2 Tunable later

May be tuned empirically without reopening Phase 4:
- player movement speed/acceleration;
- interaction radius;
- rail physical length;
- snap attraction strength;
- exact carriage drag speed;
- transition animation duration within non-timing design bounds;
- camera framing/zoom;
- cable sag amount and tensioner exaggeration;
- haptic/audio strength;
- checkpoint fade duration;
- exact Gate clearance geometry;
- exact Lift heights;
- exact Span curvature;
- teaching highlight duration;
- reduced-motion interpolation duration.

## 15.3 Empirical kill values still unresolved

The one-week prototype must still test:
- whether SLACK/TAUT/HIGH are understandable without numbers;
- whether players predict redistribution at >= roughly 75% after teaching;
- whether physical carriage manipulation feels better than a menu selector;
- whether blind enumeration dominates mature solving;
- whether 2–3 second intended anchor manipulation is comfortable.

These are empirical gates, not reasons to weaken the deterministic model.

---

# 16. Mechanical examples under the frozen rules

These examples are normative sanity checks, not final levels.

## Example A — two-load give/take

Loads:
- Lift L
- Gate G

Budget `B=2`.

Three snap bands:
- P0 = `[2,0]` → Lift HIGH, Gate SLACK
- P1 = `[1,1]` → Lift TAUT, Gate TAUT
- P2 = `[0,2]` → Lift SLACK, Gate HIGH

Adjacent moves exchange one quantum.

Player reads one local tradeoff: raising the Lift reduces Gate clearance and vice versa.

## Example B — three-load middle compromise

Loads:
- Lift L
- Gate G
- Span S

Budget `B=3`.

Four snap bands:
- P0 = `[2,1,0]`
- P1 = `[1,2,0]`
- P2 = `[1,1,1]`
- P3 = `[0,2,1]`

P2 is the only all-TAUT state and may be the only state where Span is walkable while Gate is passable and Lift remains useful.

This proves a middle state without numeric display.

## Example C — visible load removal / return inversion

Pre-mutation active loads L/G/S with `B=3`.

At current anchor P1, revision A may resolve to:
- `[1,2,0]` → Lift TAUT, Gate HIGH, Span SLACK.

Objective visibly removes Gate from the shared rig.

Revision B keeps `B=3` and same P1 physical carriage position, but now active loads are L/S and P1 resolves to:
- `[1,2]` → Lift TAUT, Span HIGH.

The player sees Gate detach, remaining tension redistribute and the Span become over-lifted. The old anchor position is now wrong for the return route.

The new revision table must still obey adjacent one-quantum exchanges across the rail.

---

# 17. Mechanical acceptance tests

Phase 4 is coherent only if all are true.

### State / conservation
- [x] Every authoritative load state derives from revision + anchor band.
- [x] Budget conservation has an exact deterministic internal representation.
- [x] Mutation preserves total budget.
- [x] Snap bands are discrete even though rail manipulation is continuous.
- [x] Adjacent bands create a physically readable one-unit give/take exchange.

### Load rules
- [x] Lift stable/collision behavior is exact.
- [x] Gate stable/collision behavior is exact.
- [x] Span stable/collision behavior is exact.
- [x] Transition timing cannot create solution-only routes.
- [x] No load requires real rope simulation.

### Player / traversal
- [x] Minimal movement vocabulary is sufficient.
- [x] No jump/combat/precision pillar is needed.
- [x] Mature decisions can be separated through player region/state changes.
- [x] Safe static enumeration has an explicit rejection rule.

### Mutation / recovery
- [x] Objective mutation ordering is exact.
- [x] Revision data constraints are exact.
- [x] C0 and post-mutation C1 checkpoint authority are exact.
- [x] Restart is deterministic and low-friction.

### Scope integrity
- [x] No fourth load family was added.
- [x] No numeric/player-facing tension system was added.
- [x] No graph/editor UI was added.
- [x] No timing/dexterity rescue mechanic was added.
- [x] Production implementation remains outside factory.

# PHASE 4 DECISION

**PHASE 4 MECHANICAL ARCHITECTURE = COMPLETE.**

Game #005 now has an implementation-ready rule model: a discrete conserved pull budget, authored snap-band distribution vectors, exact load responses, deterministic mutation/restart ordering, traversal contracts and explicit content-invalidity rules.

The system remains deliberately small. Phase 5 must now prove that these frozen rules can support the target campaign without inventing new mechanics.

## NEXT ACTION — GAME #005 RUN 9 / PHASE 5 CONTENT ARCHITECTURE
1. Re-read the complete authority chain including this file.
2. Create `GAME5_CONTENT_ARCHITECTURE.md`.
3. Convert the 24–28 / target-26 campaign promise into explicit encounter families and progression bands using only Phase-4 mechanics.
4. Define minimum/target counts by reasoning signature, load composition, mutation type and placement count.
5. Specify an authored encounter schema compatible with the Phase-4 data contract.
6. Define validators for budget conservation, adjacent-band transfers, visual distinguishability, safe socket enumeration, one-permanent-best-band, traversal timing dependence, softlocks and repeated systemic signatures.
7. Build a concrete 26-encounter campaign skeleton from teaching through synthesis without adding a fourth load archetype or movement pillar.
8. Define reuse limits so geometry/theme changes do not masquerade as mechanical novelty.
9. Define demo content subset that satisfies every Phase-3 demo promise inside 15–25 minutes.
10. Define optional/remix boundaries and first-cut rules if repetition evidence is weak.
11. Do not begin Phase 6 or production implementation until content architecture is internally coherent.
