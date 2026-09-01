# GAME #012 — PHASE 3 PRODUCT THESIS

Date: 2026-09-01
Status: **PHASE 3 COMPLETE — PRODUCT THESIS LOCKED**
Selected mechanical core: Round-C winner formerly labeled `Negative Space Clerk`.
Working product title: **OPENWORK** *(provisional; not a shipping-name commitment)*.
Authority: product identity and scope ceiling. Phase-4 exact mechanics remain to be specified.

## 1. Product identity

### One-sentence hook
**Place a few solid pieces on a tiny board; every objective judges only the topology of the empty space you leave behind.**

### Genre framing
Premium single-player **topological deduction puzzle** / compact thinky puzzle.

It should not be marketed as:
- polyomino packing;
- Sokoban;
- city building;
- automation;
- territory painting;
- abstract mathematics homework.

The approachable fantasy is "shape the emptiness." The formal topology language exists under the hood and in optional advanced explanation, not as prerequisite vocabulary.

### Core fantasy
The player is not constructing the object. They are **sculpting absence**: one tiny solid placement can split a void, seal a pocket, preserve an escape, join a boundary condition or isolate a marked point. Mastery means learning to see critical cells and near-rings before touching the board.

### Target player
Primary:
- players who enjoy compact authored deduction puzzles, spatial invariants and "aha" solutions;
- players comfortable with games such as Linelith-style short-form thinky design, but looking for a distinct causal law rather than another line/box-pushing variant;
- players who value instant retry and low execution burden.

Secondary:
- visually oriented logic-puzzle players who may not know graph/topology terminology but can read connected regions, enclosed pockets and marker grouping from color/outline feedback.

Not targeted:
- players seeking long narrative progression;
- physics-sandbox experimentation;
- speed/action challenge;
- procedural infinite content as the main promise.

## 2. Platform / interaction thesis

### Lead platform
**PC / Steam first.**

### Input posture
**Controller-first parity with mouse.** The puzzle must be fully comfortable on a handheld-sized screen and must never require pixel-precise dragging.

### Steam Deck posture
Design toward Deck-friendly readability from the start:
- compact board;
- large piece silhouettes;
- redundant region outlines/patterns, not color alone;
- no hover-only information;
- all predicates inspectable from controller focus;
- rapid undo/reset.

Deck verification remains an implementation/release gate, not a Phase-3 certification claim.

## 3. Session structure

### Individual puzzle
Expected normal solve time: **2–8 minutes**.
Tutorial cases may take under 2 minutes; mastery cases may take 8–15 minutes without requiring lengthy execution.

### Play session
Natural session: **15–40 minutes**, typically several cases. No run loss, stamina, streak penalty or forced daily cadence.

### Campaign shape
Current product target: **36 authored cases**, with a **30-case quality floor**. Six broad conceptual acts are credible from Round-C evidence; exact act structure belongs to Phase 5.

The game may ship shorter rather than padding weak cases. Case count is subordinate to deduction quality.

## 4. Core loop

1. Read the initial open region, fixed solids, available pieces and visible objective predicates.
2. Inspect likely articulation cells, near-rings, marker routes, component-area constraints and boundary contacts.
3. Select/place the small required set of solid pieces.
4. Receive immediate, fully deterministic evaluation of the **remaining open space**.
5. Compare resulting components/holes/marker relations/boundary relations with the target.
6. Undo/revise until all predicates hold.
7. Advance with the learned invariant, not with a new execution skill.

The game should reward prediction before placement but should not punish experimentation. Undo is a normal reasoning tool.

## 5. Differentiator

The central differentiation is **objective inversion**:
- most placement puzzles score what the player places/builds/connects;
- OPENWORK scores the connected structure of what the player *did not occupy*.

A single placement can have several simultaneous consequences on the void:
- split one component into two;
- close/open a hole;
- alter which markers can reach each other;
- change which boundaries a region touches;
- change component areas.

Depth comes from conflicts between those consequences, not from accumulating a large tool catalogue.

## 6. Presentation thesis

### Theme
Do **not** use literal clerical paperwork/stamps as canon; that risks portfolio contamination with Game #002 and makes the mechanical object feel like a UI metaphor.

Preferred direction: a clean tactile **openwork / material-cutout / architectural-model** abstraction. Solid pieces read as physical inserts or plates; empty regions read as illuminated/recessed space. The game can feel crafted without pretending to simulate real material physics.

### Visual causal moment
The trailer/GIF moment must be readable without narration:
1. player places one small solid plate;
2. the remaining open field instantly re-outlines into two regions and/or a newly enclosed pocket;
3. target icons flip from unmet to met.

The void should visually become the protagonist.

### Tone
Calm, precise, tactile, low-clutter. No need for characters, dialogue-heavy framing or worldbuilding to justify levels.

## 7. Scope ceiling

Phase 4 may refine exact numbers, but it must remain inside this product boundary unless a contradiction forces an explicit Phase-3 revision.

### Board / pieces
- 2D orthogonal finite boards;
- normal authored board ceiling approximately **9x9**;
- typically **1–4 placed pieces** per case;
- tiny reusable shape vocabulary, biased toward 1x1 and short bars;
- no large collectible polyomino catalogue as content padding.

### Objective vocabulary
Stay within stable predicates over remaining open space, principally:
- connected component count;
- enclosed hole count / bounded hole size;
- marker same/different-component relationships;
- component area or area bands;
- boundary contact/avoidance.

Exact predicate syntax/order belongs to Phase 4.

### Explicit exclusions
No:
- moving player avatar;
- Sokoban pushing;
- continuous physics;
- fluids;
- fold/trim simulation;
- movable walls after placement;
- portals/teleporters;
- keys/switches/doors;
- path-drawing;
- timers/reflex mechanics;
- randomized roguelike runs;
- multiplayer;
- level editor required for launch;
- daily/streak retention requirement;
- narrative content burden as a substitute for mechanical depth.

### Content rule
Late-game difficulty should grow primarily through **predicate coupling and deceptive topology**, not through larger boards, more piece types or more placements.

## 8. Commercial posture at thesis stage

Premium one-time purchase is the default direction. Exact price is intentionally deferred to Phase 7 with a fresh launch-window market check.

A demo is highly desirable because the hook can be proven quickly. Demo scope should teach articulation + hole inversion and end on one coupled-predicate case rather than expose a long quantity of content.

No ads, energy, consumable hints, battle pass or live-service dependency.

## 9. Product kill conditions carried forward

Even after selection, the game should be killed or materially redesigned if Phase 4/5 proves any of the following:
1. most cases reduce to "find the one-cell neck" with superficial target variations;
2. strong late cases require >4 pieces or boards much larger than the readability ceiling;
3. hole/component evaluation becomes visually ambiguous on handheld scale;
4. authoring 30 high-quality cases requires adding switches, portals, moving actors or a large polyomino vocabulary;
5. blind placement + instant reset dominates deduction in representative mid/late cases;
6. the exact rules cannot be certified deterministically with cheap offline enumeration.

## 10. Phase-3 freeze statement

Locked identity for subsequent phases:
- **Selected concept:** topology-of-remaining-space placement puzzle.
- **Working title:** OPENWORK (provisional).
- **Lead platform:** PC/Steam, controller-first, Deck-conscious.
- **Core fantasy:** sculpt absence; reason about the void.
- **Core loop:** inspect topology -> place a few solids -> evaluate remaining open space -> undo/refine.
- **Differentiator:** objectives score unoccupied-space topology rather than placed pieces.
- **Product size:** compact premium authored campaign, target 36 / floor 30 cases.
- **Scope ceiling:** orthogonal 2D, small boards, 1–4 pieces, tiny shape vocabulary, no physics/movement/live-service feature creep.

**PHASE 3 = COMPLETE.**

Next authority task: Phase 4 Mechanical Architecture must make the simulation/evaluation order exact, formalize hole semantics and board exterior, define piece placement legality, predicate grammar, win/fail/equivalence/certification contracts, difficulty knobs and demonstrate >=5 mechanically distinct challenge families under the frozen scope ceiling.
