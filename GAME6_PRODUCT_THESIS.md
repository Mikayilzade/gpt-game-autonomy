# GAME #006 — STITCHSPACE — PRODUCT THESIS LOCK

Last updated: 2026-08-29
Factory run: **4**
Phase: **3 — Product Thesis Lock**
Selected concept: **G6C01 Stitchspace**
Product thesis: **LOCKED**
Production implementation started: **NO**
DESIGN COMPLETE: **NO**

This file freezes the product identity of Game #006 after the Phase-2 final selection. Later phases may refine exact mechanics, content, UX, commercial details and technical architecture, but may not silently turn Stitchspace into a portal-placement game, folding game, construction sandbox or feature-heavy non-Euclidean adventure.

---

# 1. Working title

**Stitchspace** is the working title and internal canonical label.

Naming constraints for later commercial review:
- must evoke joining/cutting/reseaming space rather than teleportation;
- avoid `Portal`, `Fold`, `Warp`, `Wormhole` as primary title language;
- title should remain easy to say/search and not imply sewing/crafting economy as the core game.

No commercial-title change is required before mechanics are proven.

---

# 2. Target player

Primary target:
- players who enjoy authored systemic puzzle games with a small ruleset and escalating recombination;
- players attracted to spatial `aha` moments, impossible architecture and graph/topology reasoning without requiring formal math;
- controller/Steam Deck and desktop players who prefer thoughtful play over dexterity;
- players comfortable experimenting with immediate Undo/Redo and learning through physical consequence.

Secondary target:
- fans of compact first-/third-/diagrammatic spatial puzzlers who value a strong visual mechanic and 4–8 hour premium experience;
- puzzle players who enjoy alternate solutions/mastery when they are causal rather than score-grindy.

Non-target:
- players seeking Portal-style momentum/flinging/platforming mastery;
- freeform level-building/construction sandbox players;
- players seeking open-world exploration, narrative-heavy adventure, combat, crafting or simulation realism;
- players who want a huge quantity of one-off mechanics rather than depth from one rule.

---

# 3. Platform / commercial frame

Baseline:
- **PC / Steam first**;
- single-player;
- offline-capable;
- premium purchase;
- controller + keyboard/mouse baseline;
- Steam Deck-friendly layout/input target;
- representative free demo strongly preferred if the empirical hook gate passes.

Working design-time price hypothesis remains **$14.99–$19.99**, with final pricing deferred to Phase 7 and later market evidence.

No live-service, ads, microtransactions, consumable economy or mandatory online account.

---

# 4. Genre framing

Primary framing:
**systemic spatial puzzle / topology puzzle**.

Player-facing store language should prefer plain physical language over mathematical jargon:
- `change which rooms physically touch`;
- `move a seam and lose the old connection`;
- `route yourself and objects through impossible neighboring rooms`.

Do not market primarily as:
- portal puzzle;
- non-Euclidean walking simulator;
- folding puzzle;
- graph theory game;
- programming game;
- physics sandbox.

`Topology` may appear in secondary descriptive copy, not as required comprehension.

---

# 5. Frozen one-sentence hook

> **Rewire which rooms physically touch: move the ends of a few persistent seams, cross the impossible boundaries you create, and exploit the route you destroy every time you make a new one.**

Short internal hook:
**Every new adjacency destroys an old one.**

---

# 6. Core fantasy

The player is not firing teleport gates. The fantasy is being a **spatial seam technician** who treats room boundaries as a small reconfigurable topology.

A room edge can be physically resewn to a distant room edge. That boundary then acts as actual adjacency for everyone and everything allowed to cross it. Moving one end of the same seam unsews its previous destination and stitches the new one.

The satisfying moment is not `I found where to put the exit`. It is:

> `I made these two rooms neighbors just long enough for the crate to cross, then cut that relationship and reused the same seam to change the rest of the world.`

---

# 7. Product-level primitive vocabulary ceiling

Phase 4 will specify exact mechanics, but Product Thesis freezes the conceptual ceiling.

Required primitive families:
1. **Rooms** — stable local spaces.
2. **Edge sockets** — authored legal boundary attachment points.
3. **Seams** — scarce persistent adjacency links with two endpoints.
4. **Endpoint replacement** — moving one endpoint atomically removes its old adjacency and creates the new one.
5. **Crossing orientation** — crossing maps local direction/orientation according to visible socket/seam rules.
6. **Seam occupancy** — a crossing can temporarily make an endpoint unavailable to move if a canonical entity is mid-crossing.
7. **Ordinary passages** — fixed authored adjacency that provides topology for loops/alternatives.
8. **Discrete entities** — player and a small set of deterministic movers/objects that make seam state consequential.

Allowed depth sources:
- connection;
- disconnection/isolation;
- orientation;
- loops;
- scarce seam reuse;
- occupancy/order;
- swapping adjacency;
- state-dependent rewiring after entities have moved.

Forbidden as baseline feature growth:
- portal colors/pairs as inventory;
- momentum/flinging physics;
- arbitrary free-surface placement;
- recursive portal rendering as a gameplay requirement;
- folding/overlapping rooms;
- scaling rooms/objects;
- gravity-flip system unless later empirical contradiction proves absolutely necessary (default: excluded);
- time clones;
- property transfer;
- seam upgrades/rarities/elements;
- freeform graph editor detached from the world;
- dozens of seam types.

The game must survive on the frozen depth sources above.

---

# 8. Exact player-facing core loop

1. **Inspect** current room adjacencies, seam endpoints, ordinary passages, entities and goals.
2. **Predict** what useful connection and what useful disconnection the next endpoint move will create.
3. **Select** one existing seam endpoint and one legal target edge socket.
4. **Preview** the direct old-adjacency loss, new adjacency and crossing orientation.
5. **Commit** the endpoint replacement atomically.
6. **Traverse / move entity / allow deterministic local consequence** using the new topology.
7. **Observe** which route/entity state is now available, isolated, stranded or oriented differently.
8. **Reuse** the same scarce seam for the next topology state.
9. Undo/Redo freely when testing a hypothesis.

A mature solution should alternate topology edits and physical use of the changed topology. Long stretches of detached graph editing are not the intended experience.

---

# 9. Repeated verb

Primary repeated verb:
**MOVE ONE EXISTING SEAM ENDPOINT TO A DIFFERENT AUTHORED EDGE SOCKET.**

The action must visibly communicate both halves of its atomic consequence:
- old boundary relationship disappears;
- new boundary relationship appears.

The game may include ordinary traversal/interact actions, but they support this verb rather than compete with it.

---

# 10. Session structure

Target ordinary session:
- 10–30 minutes;
- complete 1–4 authored cases depending difficulty;
- each case is a compact self-contained topology problem;
- immediate restart/Undo encourages experimentation;
- optional mastery/remix can extend a solved concept without grinding.

Campaign target from Phase 2:
- ~30–36 main cases;
- ~4–7 hour minimum first-clear target, 5–8 hours preferred if content quality supports it;
- 6–10 optional remix/mastery cases only if later content review proves genuine causal distinction.

Campaign should teach the primitive vocabulary early and spend the majority of playtime recombining it rather than introducing mechanics late.

---

# 11. Progression thesis

Progression is **cognitive, not statistical**.

The player gains:
- understanding of adjacency replacement;
- comfort with orientation;
- ability to reason about useful disconnection;
- loop/cut intuition;
- ability to sequence object/player crossings;
- ability to reason with two scarce seams;
- ability to compress several obvious rewires into one topology plan.

The player does not gain:
- stronger seams;
- more seam capacity as an RPG upgrade;
- currency;
- XP;
- skill tree;
- permanent movement powers;
- randomized loot.

If a rare case uses a third seam, it is authored case state, not permanent progression.

---

# 12. Failure / experimentation philosophy

Wrong topology edits are expected puzzle probes, not punishment.

Rules:
- Undo is immediate and effectively unlimited for ordinary play;
- Redo is supported while branch remains intact;
- restart is immediate;
- no lives/energy/time penalty;
- no mastery based on raw Undo count, restart count or thinking time;
- baseline content cannot depend on hidden irreversible stranding before the relevant concept is taught;
- legal but strategically bad edits commit so the player can observe causal consequence;
- structurally illegal edits reject before mutation with a clear reason.

Optional mastery may reward causal elegance only when it represents a different solution character, not reluctance to experiment.

---

# 13. Presentation thesis

The world must make topology change readable without requiring a separate abstract graph.

Presentation priorities:
1. **rooms remain spatially recognizable as stable local places**;
2. exposed edge sockets are visible but not glowing-loot clutter;
3. seam endpoints and the relationship between them are always traceable;
4. when an endpoint moves, the old relationship visibly unzips/cuts before/while the new one stitches;
5. crossing shows local orientation clearly;
6. remote rooms becoming adjacent should be understandable in a short mute clip;
7. the player can inspect a compact topology overview, but the physical world remains the primary play surface.

Visual identity should intentionally separate Stitchspace from Portal:
- seams are persistent physical boundary relationships, not fired surface holes;
- the old seam is visibly consumed/repositioned;
- room-boundary sockets and seam scarcity are foregrounded;
- no blue/orange paired-portal language.

No expensive photorealism is required. Stylized architectural modules, strong edge language and clean transitions are preferred.

---

# 14. Camera / spatial representation thesis

Exact camera mode is implementation-flexible until Phase 6/8 research, but it must satisfy:
- player can understand multiple room identities and seam relationships;
- no nausea-inducing camera discontinuity is required for ordinary crossing;
- remote adjacency change is readable;
- controller focus on edge sockets is deterministic;
- 1280×800 remains usable;
- no gameplay-critical free-look precision.

Candidate presentation modes for later evaluation:
- 2.5D cutaway/isometric rooms;
- diagrammatic multi-room stage with local movement;
- carefully bounded 3D rooms with topology overview.

Product Thesis does **not** lock first-person 3D. The cheapest presentation that preserves the spatial fantasy and trailer clarity should win later.

---

# 15. Input / accessibility thesis

Required baseline paths:
- controller-only;
- keyboard-only;
- mouse + keyboard;
- Steam Deck built-in controls.

Core endpoint editing cannot require precision dragging.

Semantic interaction target:
- focus/select seam;
- choose endpoint;
- cycle/select legal edge socket;
- preview;
- confirm/cancel;
- move/traverse;
- Inspect;
- Undo/Redo;
- restart.

Accessibility principles:
- no reflex timing requirement for baseline;
- deterministic occupancy/state rather than frame-dependent crossing windows;
- color is never the sole seam/socket/orientation signal;
- crossing orientation has shape/arrow/text redundancy where useful;
- reduced motion can replace dramatic zip/camera motion without changing topology;
- no audio-only information;
- scalable UI and deterministic focus order;
- Undo/Redo/accessibility aids do not invalidate baseline completion.

---

# 16. Differentiation rule

A shipped Stitchspace case is valid only if its interesting reasoning depends materially on **adjacency replacement or an emergent consequence of that replacement**.

From midgame onward, each main case must materially use at least one of:
- the old adjacency disappearing;
- useful disconnection/isolation;
- orientation mapping;
- seam occupancy/order;
- loop creation/breaking;
- scarce seam reuse between different entities/routes;
- state-dependent rewiring after a crossing.

A case whose dominant solution can be paraphrased as `put entrance near A and exit near B` with no material lost-adjacency consequence is **invalid content**, even if visually attractive.

---

# 17. Scope ceiling / 1.0 exclusions

1.0 target:
- 30–36 main cases;
- 1–2 seams typical; rare 3-seam case only if justified;
- 2–5 rooms typical;
- small deterministic entity vocabulary;
- PC/Steam first;
- premium single-player;
- complete controller/Deck path;
- representative demo if empirical gate passes.

Explicit exclusions unless a later documented canonical amendment proves necessity:
- multiplayer/co-op;
- procedural campaign;
- user level editor/Workshop;
- open world;
- combat;
- inventory/crafting;
- narrative branching system;
- physics sandbox;
- free portal placement;
- momentum/flinging;
- recursive spatial rendering requirement;
- folding/scaling/gravity manipulation as extra core verbs;
- currencies/XP/upgrades;
- live service/dailies/FOMO;
- large bespoke dialogue/voice campaign;
- mobile-first touch design.

---

# 18. Commercial/demo proof condition

A 15–25 minute demo must prove all of these before ending:
1. seam crosses a remote room boundary;
2. moving one endpoint destroys the prior adjacency;
3. orientation matters once;
4. one seam is reused for different routes/entities;
5. the player deliberately uses **disconnection/isolation** as a benefit;
6. the final demo synthesis cannot be described honestly as ordinary portal placement.

If the demo ends before useful disconnection/replacement is understood, it does not prove the commercial hook.

---

# 19. Inherited empirical prototype gate

The Phase-2 winner decision carries one mandatory kill/reopen gate into implementation.

After a primitive vertical slice, PASS only if all are true after one tuning pass:
- >=75% naive testers explain the core as changing room adjacency / moving a connection that removes the old connection rather than merely placing portals;
- >=5/8 representative grayboxes materially depend on lost adjacency, orientation, occupancy, loop or disconnection;
- mature representative cases exhibit >=4 abstract solution skeleton families;
- orientation misunderstanding causes <20% ordinary failures after tutorial;
- direct current-room-to-goal stitching is not the shortest solution in >=75% of representative mature cases;
- no baseline solution requires dexterity/timing;
- a mute clip communicates that moving the seam creates one relationship while destroying another.

Failure response:
- first apply only presentation/tutorial/content repairs that preserve the Product Thesis;
- if comprehension/depth still fails, **reopen or kill**;
- do not rescue with portal powers, momentum, new currencies or feature accretion.

---

# 20. Product risks frozen for later attack

P3-R1 — **Portal interpretation:** players see entrance/exit placement, not adjacency replacement.

P3-R2 — **Orientation bookkeeping:** seam mappings become compass homework rather than spatial intuition.

P3-R3 — **Graph abstraction takeover:** optimal play migrates to a detached topology UI instead of the physical world.

P3-R4 — **Content isomorphism:** many cases reduce to connect-cross-move endpoint-cross.

P3-R5 — **Stranding annoyance:** scarce seams create busywork/restart rather than insight.

P3-R6 — **Remote readability:** players cannot track which rooms currently touch without constant map checking.

P3-R7 — **Two-seam state explosion:** solver/content QA cost grows faster than puzzle value.

P3-R8 — **Spatial presentation cost:** making impossible adjacency look good accidentally requires expensive recursive/non-Euclidean rendering.

Later phases must attack these directly instead of hiding them with more mechanics.

---

# 21. Phase-3 acceptance

- Selected concept fixed: **YES — Stitchspace**
- Working title fixed: **YES**
- Target/non-target audience: **YES**
- PC/Steam premium frame: **YES**
- Genre language: **YES**
- Exact hook: **YES**
- Core fantasy: **YES**
- Repeated verb: **YES**
- Core loop: **YES**
- Primitive vocabulary ceiling: **YES**
- Differentiation rule: **YES**
- Progression thesis: **YES**
- Failure/Undo philosophy: **YES**
- Presentation thesis: **YES**
- Input/accessibility thesis: **YES**
- Scope ceiling: **YES**
- Explicit exclusions: **YES**
- Demo proof conditions: **YES**
- Empirical kill/reopen gate: **YES**
- Product risks retained: **YES**
- Product Thesis Lock: **COMPLETE**
- Production implementation started: **NO**
- DESIGN COMPLETE: **NO**

## NEXT PHASE
**Phase 4 — Mechanical Architecture.**

Define exact room/socket/seam data model, endpoint replacement semantics, orientation transforms, crossing and occupancy timing, entity movement, legal/illegal edit validation, ordinary passage interactions, two-seam ordering, objectives/invariants, soft-lock policy, Undo/Redo transaction boundaries, deterministic resolution order, solver-state representation, difficulty knobs, anti-portal authoring constraints and numbered mechanical acceptance tests. Do not add new primary verbs merely to create content.