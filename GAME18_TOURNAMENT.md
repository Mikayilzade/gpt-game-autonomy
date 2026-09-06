# GAME #018 — PHASE 2 CONCEPT TOURNAMENT

Date: 2026-09-06
Status: ROUND B COMPLETE — ROUND C NEXT
Production implementation: NO
Authority: below START_HERE.md, STATUS.md, GAME_INDEX.md, GAME18_RESEARCH.md.

## Round A result retained
Round A attacked 12 concepts under the same 13 dimensions. Six survived into Round B: A1 LOCAL TIME, A2 UNFINISHED SENTENCES, A3 THE ROOM AFTER YOU, A6 TIDE TABLE FOR TWO, A8 ONE MORE CHAIR, A9 AFTERIMAGE DELIVERY. A4/A5/A7/A10/A11/A12 remain killed and are not reopened.

# ROUND B — CONCRETE STRESS PACKETS

Round B is not a score rerun. Each survivor must demonstrate an understandable first 15 minutes, a nontrivial midgame state, a late escalation using the same grammar, bounded production burden, and resistance to its strongest exploit.

## A1 — LOCAL TIME — SURVIVES TO ROUND C

### Exact first 15 minutes
0–3 min: one bakery, one movable clock-zone, two discrete displayed states 07:55 and 08:00. Bread has a public rule: when inside an 08:00 zone at a beat boundary, its RISE step completes. Moving the clock changes only the current local-time label; completed process steps never reverse.
3–7 min: add bridge with public rule OPEN at 08:00 and station whose train DEPARTS at 08:05. Player learns that a zone affects all eligible objects currently inside it, so covering bakery and bridge together can be useful or harmful.
7–11 min: two clock-zones with different current labels and overlapping footprints. Objects do not carry elapsed clock time; they carry irreversible process-state flags such as RAW -> RISEN -> BAKED. Time is therefore a public condition checked at discrete beats, not a rewindable simulation.
11–15 min: first handoff: make bread RISEN under 08:00, slide that zone to bridge, then use 08:05 zone at station without undoing bread. Puzzle asks for three public schedule predicates in four clock moves.

### Representative midgame state
Diorama has bakery B, bridge G, flower stall F, station S. Two radius-2 clock tiles show 08:00 and 08:05. Public rules: dough rises if exposed to 08:00 once; oven bakes RISEN dough if exposed to 08:05; bridge opens while currently under 08:00; flowers close permanently if exposed to 08:05 before delivery; train departs if station is under 08:05 while bridge is open. Player has three zone moves before Resolve beats. Meaningful decision: the obvious move of 08:05 onto bakery finishes bread early but closes flowers; instead use 08:00 to progress bread/open bridge, then reposition zones so station receives 08:05 while flowers remain outside. The puzzle is about arranging simultaneous local predicates plus irreversible process milestones, not changing a global clock.

### Late mastery using same grammar
Three clocks, 6–8 sites, overlapping footprints, multi-step public process chains, and one mobile carrier that transports an already-earned state between zones. No retrocausality, time loops, continuous durations or bespoke exceptions. Mastery comes from ordering zone footprints so current-time predicates and persistent process milestones compose.

### Burden
Low-to-moderate: one diorama kit, clock-zone overlays, roughly 6–10 reusable process props/animations, authored puzzle data. No NPC AI, physics or large narrative content. 30–40 campaign puzzles plus mastery is plausible if process vocabulary stays around 8–10 reusable rule families.

### Strongest exploit
Treat each clock position as a brute-force switch and enumerate placements. Secondary exploit: UI preview could become an oracle if it shows every future consequence.

### Repair / kill threshold
Repair with small move budgets, causal reason traces, partial preview limited to immediate affected predicates, and puzzles where multiple zones interact. KILL if late depth requires adding time travel, rewinding object state, continuous timers, more than ~10 process rule families, or exceptions to “completed process milestones never reverse.”

### Portfolio collision
Clear. Unlike #011 it does not edit cyclic programs; unlike #013 it is not reconstructing history; unlike #017 it does not infer hidden agents. Core identity is spatial placement of public local-time conditions.

## A2 — UNFINISHED SENTENCES — KILL AFTER ROUND B

### Exact first 15 minutes
Player sees physical cards such as MOVE ___ TO BLUE, TURN ___, GIVE ___ TO ___. Objects travel on a small belt; whichever token is physically in a blank socket when a card fires binds to the missing noun. First puzzles route a key/box/ball through one blank, then introduce two blanks and an object that can itself carry another object.

### Representative midgame state
Four cards execute in fixed order: MOVE ___ TO RED; PUT ___ IN ___; TURN ___; MOVE ___ TO EXIT. Two lanes and three objects create aliasing: the box can occupy a noun slot while containing the key. The intended insight is to bind the box as destination on beat 2, then the key as subject later.

### Late mastery
Nested containers, two simultaneous blanks, conditional physical gates and self-reference where a command card can be moved by another command. Same grammar can be deep.

### Burden
Very low assets and high systemic reuse; 40+ puzzles feasible.

### Strongest exploit
Execution-trace brute force and programmer mental models dominate. Once two blanks/nesting arrive, plain-language fiction stops hiding variable binding/aliasing; if UI previews bindings, it solves the puzzle, while without previews novices must mentally execute code.

### Repair / kill threshold
The necessary repair would cap blanks and nesting, but that removes much of hour-5 depth. Keeping depth creates the exact programmer-homework product risk Round A identified.

### Portfolio collision
Clear from prior games, but current market already has a healthy programming/automation-puzzle audience and the concept would compete on that specialist surface rather than escape it.

**KILL REASON:** concretization confirms a structural audience problem: late depth and broad readability pull in opposite directions. The compact grammar is excellent, but its strongest states are visibly program tracing/aliasing.

## A3 — THE ROOM AFTER YOU — KILL AFTER ROUND B

### Exact first 15 minutes
Player arranges chair, lamp, book and tray before leaving. Visitor has three public universal priorities represented by icons: satisfy NEED if reachable; clear BLOCKED path by moving nearest movable blocker to nearest free surface; return carried object to a matching affordance. First visitor moves chair to reach lamp. Second visitor later uses the chair's new position to reach shelf.

### Representative midgame state
Three visitors arrive sequentially. All use the same small verb grammar, but different public needs select targets. Player can move two starting objects. To make visitor C retrieve a parcel, A must move a stool while pursuing light, then B must clear a tray onto that stool, freeing the shelf edge C uses. The chain is readable after resolution.

### Late mastery
4–5 visitors, rooms with 10–14 affordance objects, priorities competing, and one-use states such as OPEN/CLOSED or FULL/EMPTY.

### Burden
High relative to apparent simplicity. Every object needs readable affordances, legal placements, animations and interaction outcomes; visitors require deterministic selection traces. A small universal grammar helps code but visual/content QA scales combinatorially.

### Strongest exploit
Search every starting arrangement and watch the whole chain; reset cheaply. More importantly, the player may experience failures as “NPC chose a weird thing” unless the game previews enough priority logic to become a planning UI.

### Repair / kill threshold
Would need strict sockets, tiny object vocabulary and strong intent previews. At that point the charming room fantasy increasingly reveals an abstract state machine, while asset/animation burden remains above competitors.

### Portfolio collision
Not a direct prior-game collision, though persistent transformations across absent observations faintly echo #007; identity is sufficiently different.

**KILL REASON:** the reusable visitor grammar can be specified, but making every resulting action feel obvious requires disproportionate affordance art, animation and explanation. Production/readability cost rises faster than puzzle depth.

## A6 — TIDE TABLE FOR TWO — KILL AFTER ROUND B

### Exact first 15 minutes
Two cutaway shores share tide states LOW/MID/HIGH. One universal object, a sealed crate, obeys public contact rules: supported on dry ground = weight; floating with water beneath = float; wedged between two supports = bridge; occupying a narrow water cell = flow blocker. Player places crates only between tide beats.

### Representative midgame state
Left shore needs a courier across at MID; right shore needs a marker kept dry at HIGH. Two crates are shared through a transfer dock. Place crate as LOW bridge on left, tide rises and floats it to transfer; on right the same crate must lodge under a ledge before HIGH. Meaningful cross-shore ordering exists.

### Late mastery
Two terrain profiles, 3–4 crates, LOW/MID/HIGH/MID/LOW schedule, current/contact/support determine roles. Terrain geometry creates phase changes without new object classes.

### Burden
Moderate: discrete water rendering is manageable, but each terrain cell/contact configuration must be visually unambiguous. Level authoring burden is significant because useful state transitions depend on geometry.

### Strongest exploit
Once role table is learned, many puzzles become enumerate crate placements at each tide. To deepen, terrain must create increasingly bespoke contact cases, recreating exception pressure.

### Repair / kill threshold
Could restrict to sockets and a tiny state table, but then the hook becomes a conventional phase-gated placement puzzle. If free-ish geometry is restored, QA/readability risk rises sharply.

### Portfolio collision
Some thematic/mechanical adjacency to #016's one object changing future affordance and #001 environmental cascades, though not a direct collision.

**KILL REASON:** Round B exposes a bad trade: universal discrete rules make the system clean but too close to phase-gated placement; richer terrain restores novelty by increasing geometry exceptions and authoring burden.

## A8 — ONE MORE CHAIR — SURVIVES TO ROUND C

### Exact first 15 minutes
0–4 min: four guests around a small table, one empty chair token. Universal etiquette rules are printed as icons on guest cards, not character trivia. Rule 1: a dish passes clockwise to the nearest occupied adjacent seat; an empty chair breaks passing. Player inserts one empty chair between courses to prevent a spicy dish reaching a guest.
4–8 min: Rule 2: a guest with matching preference keeps the first adjacent matching dish instead of passing it. Player learns local interactions can stop propagation.
8–12 min: courses persist: kept dishes occupy a place-setting slot next course, and an empty chair inserted this course becomes a vacant place setting that can redirect the next course's serving start.
12–15 min: two dishes start from different hosts; player may insert one chair and remove one existing empty chair. Goal is not “fix bad adjacency” but produce two end-of-course ownership constraints simultaneously.

### Representative midgame state
Six fixed guests, two empty-chair tokens, two courses. Public rules: dishes pass clockwise unless a matching guest keeps them; a guest holding a dish cannot accept another and therefore passes; empty seats break passing and cause the dish to restart from the host on next course; dessert begins at the seat opposite the last keeper. Goal: guest A must get soup, guest D must not get wine, dessert must start adjacent to C. Inserting a chair to block wine also changes where soup stops and therefore dessert origin. Several placements satisfy one constraint; the decision is choosing a chair placement whose persistent ownership consequence makes course 2 solvable.

### Late mastery
7–8 guests maximum, 3 courses, 2 movable empty chairs, 3–4 universal etiquette rules active. Add no guest-specific verbs; difficulty comes from interaction of occupied hands, pass direction, restart origin and course-to-course state. A late puzzle can ask player to deliberately leave a dish unserved in course 1 to alter course 2 origin.

### Burden
Low. One table scene, reusable guest portraits/animations, dish set, seat sockets and 4–6 universal rule icons. 30–40 authored cases are feasible. Strong controller/Deck fit.

### Strongest exploit
Try every chair slot: with 6–8 seats and one chair, action space is tiny. If every case is one insertion then Resolve, brute force wins instantly. Also risks becoming circular adjacency algebra after comedy fades.

### Repair / kill threshold
Survival requires multi-course persistence and at least two coupled objectives so first legal-looking placement is not enough. Later cases need 2-step policies (insert/remove or choose which empty chair persists) and multiple valid-but-different consequences. KILL if meaningful depth requires tables >8 guests, guest-specific exception rules, or more than ~6 universal etiquette rules.

### Portfolio collision
Clear. Local circular propagation is not topology rewiring (#006), queue diagnosis (#017), cyclic program deletion (#011), or label permutation (#010). Embodied social-comedy presentation is novel in portfolio.

## A9 — AFTERIMAGE DELIVERY — SURVIVES TO ROUND C

### Exact first 15 minutes
0–3 min: courier drives a tiny road loop. Each traversed street stores one arrow showing last travel direction. A public arrow-gate opens only when its approach street currently points toward it.
3–7 min: second delivery starts after first; player intentionally takes a longer first route to write an arrow needed by the second.
7–11 min: overwrite rule: traversing a street opposite direction replaces its arrow. Player learns infrastructure is temporary and routes can destroy prior setup.
11–15 min: two vehicle types with one universal difference: van obeys arrow-gates; bike may cross an unmarked street but erases the arrow it leaves. Player plans two deliveries where first writes and second consumes/overwrites traces.

### Representative midgame state
Compact non-grid neighborhood graph with 9 intersections, 12 street segments, three deliveries in sequence. Trace persists for exactly two subsequent route resolutions, with age shown by 2/1 pips. Gate G needs inbound east arrow; loading dock D rejects a vehicle if its approach arrow points outward; bike erases its departure segment after completion. Player can choose delivery order plus route. Shortest route for package 1 writes the wrong arrow at G; a two-edge detour writes the needed east trace, but if package 2 uses the same segment it overwrites it before package 3. Meaningful decision combines route, order and trace lifespan.

### Late mastery
12–16 intersections, 4 deliveries, trace age 2, 2 vehicle rule families, conflicting required directions and one route that intentionally refreshes an old trace. No traffic simulation, fuel economy, free driving or procedural city. Mastery is writing, preserving, consuming and overwriting temporary street state.

### Burden
Low-to-moderate. One stylized city kit, graph-based road layouts, arrow overlays, 2–3 vehicle skins, gate/dock props. Logic is deterministic and data-driven. 30–45 authored puzzles plausible; graph editor/validator needed later but production code is outside factory.

### Strongest exploit
Generic path search / brute-force route enumeration. If every constraint is just “arrive with arrow X,” solver-like trial can replace insight. Another risk is grid-puzzle perception.

### Repair / kill threshold
Use tiny graphs with visible named landmarks, route previews that show only direct writes not future solved states, coupled delivery order, trace decay/overwrite and different consumers. Human proof should be 2–6 causal deductions rather than route enumeration. KILL if late depth requires >2 vehicle rule families, >16 intersections, arbitrary gate types, or hidden traffic behavior.

### Portfolio collision
Some abstract state-writing resemblance exists to #007 persistent transformed form, but here state is short-lived public infrastructure written by movement and consumed by later routes. It does not edit topology (#006) or permute moving labels (#010). Collision acceptable if temporary trace lifecycle remains central.

# ROUND B RESULT

Advance exactly three concepts:
1. **A1 LOCAL TIME** — best conceptual inversion and strongest clean diorama identity; Round B found a no-retrocausality state model that preserves depth.
2. **A9 AFTERIMAGE DELIVERY** — strongest minute-to-minute agency and causal “route writes next route” loop; needs proof against generic pathfinding.
3. **A8 ONE MORE CHAIR** — strongest scope-to-charm ratio; survives only because multi-course persistent consequences can make tiny action spaces nontrivial.

Killed in Round B:
- **A2 UNFINISHED SENTENCES** — late depth structurally exposes programming/aliasing and narrows audience.
- **A3 THE ROOM AFTER YOU** — readable deterministic NPC behavior demands disproportionate affordance/animation/content QA.
- **A6 TIDE TABLE FOR TWO** — clean universal rules collapse toward phase-gated placement; richer terrain restores novelty through exceptions/authoring burden.

No winner is selected yet.

# ROUND C NEXT — HEAD-TO-HEAD PROOF

For LOCAL TIME, AFTERIMAGE DELIVERY and ONE MORE CHAIR, build equal-format final proofs:
1. exact 25–35 minute six-case demo sequence;
2. representative hour-5 player loop and why it is not the tutorial repeated with larger numbers;
3. target campaign/mastery content count and production estimate;
4. strongest dominant strategy and validator/authoring defense;
5. one-sentence store hook + 10-second trailer/GIF proof;
6. current commercial/saturation distinction and closest analogue risk;
7. portfolio distinction;
8. fatal kill criterion.

Then choose exactly one winner only if it has a coherent product thesis path. If no concept clears the bar, reopen opportunity discovery rather than forcing a winner.
