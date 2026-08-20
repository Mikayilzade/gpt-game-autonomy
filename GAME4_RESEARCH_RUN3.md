# GAME #004 — OPPORTUNITY DISCOVERY — RUN 3 FINAL FALSIFICATION

Last updated: 2026-08-20
Factory run: **3**
Phase: **1 — Opportunity Discovery**
Concept selected: **NO**

This run performs the final Phase-1 falsification. It does not select a winner. The purpose is to force each serious concept to survive nearest-neighbor pressure, explicit rules, live-state readability, demo structure, long-session repetition defense and a cheap kill test before Phase 2.

## 1. Fresh nearest-neighbor pressure

Fresh searches on 2026-08-20 reinforced several warnings.

- Negative-space games are not empty territory. `Box or Void` explicitly reverses positive/negative space, while older `SHIFT`, `Gap Monsters`, multiple itch prototypes and the forthcoming `NEGATIVE_SPACE` use void/solid inversion or negative-space navigation. Therefore Negative Space Courier cannot claim the noun `negative space`; its identity must be the live rearrangement of *obstruction panels while the contiguous gap itself is the traversed level*.
- Sound occlusion is increasingly legible as a simulation concept. Existing stealth games and even sophisticated Barotrauma sound-occlusion mods demonstrate obstruction/path-based sound. Soundproof Smuggler therefore survives only if physically editing a small deterministic acoustic graph is the player's central verb rather than an audiovisual effect.
- Umbrella/wind traversal already has recognizable precedent, including Windy Slider's umbrella-as-wind-catcher/jump relationship and broad parasol/glider usage. Umbrella Engine cannot survive as `umbrella + wind`; it must be a bounded multi-affordance actuator with authored response bands.
- Generic remove-a-piece, destruction, elastic construction and one-shot anchors remain crowded mechanic families; each needs a stronger second-order constraint than its object fantasy.

No exact commercial analogue was found in these searches for the full Seam Thief rule proposed below, the physical acoustic-graph blocker of Soundproof Smuggler, or the specific live scenery-track ownership of Stagehand Zero. Absence from search is not proof of novelty; Phase 2 must continue adversarial comparison.

## 2. Finalist falsification

### G4C01 — Seam Thief — SURVIVE

**Why not just play a portal game?** A portal preserves two surfaces and teleports entrants through paired apertures. A seam removes the separation between two authored boundary intervals: contacts/crossings on either interval resolve as if the intervals share an edge. The stitched edge can become floor-to-wall, wall-to-ceiling or reversed adjacency for player, bodies, hazards and continuous geometry simultaneously.

**Frozen Phase-1 seam semantics for tournament testing:**
- only authored compatible boundary intervals may be stitched;
- equal discrete seam lengths only;
- each interval has an outward normal and endpoint order;
- player chooses one of two endpoint mappings: aligned or reversed;
- crossing maps tangent position 1:1; velocity is rotated from source local tangent/normal basis into destination basis;
- one active seam pair initially; no seam-seam crossing or recursive seam endpoints;
- a seam is illegal if either interval is occupied by a static blocking volume, would place an already-overlapping rigid body into invalid geometry, or violates an authored compatibility tag;
- preview shows mapped orientation and ghost continuation before commit.

**Three mature families portals do not reproduce cleanly:**
1. **Shared support:** stitch two floor/wall edges so a long body bridges what becomes one continuous support boundary; removing seam breaks support.
2. **Boundary redirection:** a moving sweeper/hazard crosses a stitched room edge and continues with mapped orientation while the player exploits the same continuous edge from the opposite side.
3. **Topology with collateral adjacency:** joining a safe edge to an exit edge also makes an enemy/hazard region directly adjacent along the whole seam, so the same edit changes multiple local relationships rather than creating a private doorway.

Hook: **Sew two edges of the room together and make distant surfaces become one continuous boundary.**
10-second GIF: select floor edge + vertical edge → zip seam → player runs across what was a corner between distant regions while a crate slides through the same new adjacency.
Minute-1 decision: which two of three compatible edges should become adjacent.
Minute-20 climax: one seam simultaneously reroutes player, rolling hazard and support geometry; reversed endpoint mapping is required.
Hour-3 depth: orientation, multi-object propagation, moving edge eligibility, temporary seam locks, collateral adjacency.
Hour-10 defense: puzzles are authored around relationship graphs and simultaneous consequences, not route length; rule vocabulary stays small while object arrangements vary.
One-week kill: 12 graybox rooms; kill if >35% read as entrance/exit portals or start→goal stitching dominates.
Scope ceiling: 2D deterministic geometry, one seam pair baseline, <=6 dynamic object families, no arbitrary mesh topology.

### G4C19 — Soundproof Smuggler — SURVIVE

**Tiny acoustic graph:** rooms are nodes; open passages are directed/bidirectional edges with attenuation class 0/1/2. A sound event has integer strength 1–4. Propagation uses deterministic shortest attenuation cost; guard hears iff remaining strength at guard node >= guard threshold. The single absorber occupies one authored edge-slot and adds +3 attenuation (normally closing weak sounds, reducing strong ones) rather than simulating wave physics. Multiple equal-cost routes remain visible and can defeat one blocker.

Every prediction is shown visually before commitment: source pulse icon, lit propagation edges, numeric-free 4-step intensity glyphs, guard hearing cone/ring state, and a dashed predicted route for the next player action. Audio mirrors this but carries no exclusive information. A visual-only player receives exactly the same state transitions and optimal decisions.

Why not just play a stealth game? The player is not merely minimizing a noise meter; they physically reroute a small network so the same action is heard by selected rooms and suppressed in others. Mature puzzles can require deliberately sending sound toward one guard while blocking another.

Hook: **Move one soundproof panel to decide which rooms can hear every action.**
10-second GIF: drag absorber across doorway rail → visible pulse route flips from Guard A to Guard B → player breaks glass safely while B investigates elsewhere.
Minute-1 decision: block one of two propagation routes before making a loud traversal action.
Minute-20 climax: intentionally preserve one route as lure while suppressing a second route to cross.
Hour-3 depth: multiple paths, sound strengths, thresholds, moving sources, doors that alter graph.
Hour-10 defense: stealth states arise from graph + patrol interaction; avoid authored one-solution `close door` rooms; optional efficiency/mastery goals reward selective audibility.
One-week kill: kill if visual-only optimal decisions differ, waiting >25% run time, or nearest-door blocking dominates.
Scope ceiling: top-down 2D, <=12 acoustic nodes per encounter, one absorber baseline, <=4 sound strengths, no ray-traced acoustics.

### G4C09 — Negative Space Courier — HARD KILL

Panel contents were removed for the required identity test. With blank rectangles, the mechanic still functions, but mature play collapses toward moving rectangles to open corridors—a sliding-obstacle puzzle whose distinctive noun is already heavily occupied by positive/negative-space games. Making panels semantically rich would restore identity only by contradicting the test and increasing content burden. The concept is memorable visually but does not currently defend enough hour-3 identity. Kill before tournament.

### G4C11 — Stagehand Zero — SURVIVE

Why not a foreground/background puzzle? The player's repeated action is live **collision ownership**: scenery flats occupy one of three discrete stage tracks; only the active performance track is solid, and track changes occur while actors continue deterministic routines. No perspective scaling or hidden depth.

Hook: **Move stage scenery between depth tracks while the show keeps running; whatever reaches the live track becomes real collision.**
10-second GIF: runner approaches gap → player slides painted staircase from backdrop to live track → it snaps solid → runner climbs as a hazard prop is simultaneously pushed backstage.
Minute-1 decision: activate bridge or barrier before actor reaches cue.
Minute-20 climax: one scenery move helps player but changes an NPC/hazard route on the same live track.
Hour-3 depth: shared props, moving scenery rails, track-locked actors, cue windows, multi-use silhouettes.
Hour-10 defense: deterministic actor routines combine with a compact prop grammar; avoid bespoke scripted gimmicks by using shared collision/route rules.
One-week kill: 10 sequences; kill if surprise collisions >10%, pause is needed, or props need bespoke logic.
Scope ceiling: side-view 2D, exactly 3 depth tracks, <=8 reusable prop archetypes, no free perspective.

### G4C04 — One-Bullet Mason — DOWNGRADE / RESERVE

Bounded response table:
- bolt into `HINGE` socket: connects one marked body to socket with one authored rotational axis;
- bolt into `BRACE` socket while body is within snap envelope: locks body to nearest marked support pose;
- bolt into `TETHER` socket: creates fixed-length straight constraint to the one marked compatible body in capture zone;
- firing again atomically removes old relation before applying new one; no free anchors.

This makes implementation deterministic but weakens the original fantasy into `shoot contextual socket to change constraint`. The one-shot flow remains potentially fun, yet its ownable identity is less defensible than the leading concepts. Reserve for tournament substitution only if a survivor fails.

### G4C24 — Debris Sculptor — SURVIVE

Bounded response table replaces free destruction: every breakable object has 2–3 authored fracture IDs; each fracture produces named rigid chunks in exact local poses with fixed affordance tags (`WEDGE`, `STEP`, `ROLLER`, `BLOCKER`). Chunks use deterministic grid/rail settling zones rather than unconstrained pile physics. No inventory; chunks remain in world.

Hook: **Break structures along chosen seams, then build only with the exact pieces you created.**
10-second GIF: choose diagonal fracture → wall becomes wedge + step → wedge redirects rolling body while missing wall opens hazard line.
Minute-1 decision: which of two fracture seams preserves needed structure.
Minute-20 climax: harvest one affordance while source structure must retain another function.
Hour-3 depth: fracture choice, source cost, chunk affordance combinations, irreversible local consequences with quick reset.
Hour-10 defense: combinatorial source/chunk roles, not destruction spectacle; levels demand selective breaking.
One-week kill: kill if break-everything wins >20%, repeated settling retries occur, or inventory desire emerges.
Scope ceiling: 2D deterministic rigid bodies, <=4 chunks per fracture, authored settle zones, <=12 chunk affordance archetypes.

### G4C28 — Tension Window — DOWNGRADE / RESERVE

Bounded table: three tension bands × eight approach-angle buckets × three body mass classes map to one of `CATCH`, `DEFLECT_LOW`, `DEFLECT_HIGH`, `RETURN`, `PASS`; launch speed is a fixed table value. The membrane itself renders a curve but does not determine physics continuously.

This is predictable, but once discretized the concept risks feeling like a contextual bumper selector rather than an expressive membrane; if continuous simulation is restored, QA risk returns. Reserve rather than tournament finalist.

### G4C47 — Umbrella Engine — SURVIVE

Bounded response model: one actuator has four angle bands: CLOSED, NARROW, WIDE, INVERTED. Every environmental interaction is authored through a shared table by wind class and incoming-object class. Examples: WIDE + lateral wind = strong translation / low fall; NARROW = weak translation / medium fall; INVERTED catches downward cargo but creates drag; CLOSED permits narrow passage and sheds cargo. No continuous cloth simulation.

Why not Windy Slider/parasol platforming? The umbrella is not just locomotion: the same four states coherently trade shelter footprint, wind coupling, catch capacity, deflection and passage width for player and cargo.

Hook: **You control one giant umbrella machine; four opening states change how wind, cargo, shelter and passage interact at once.**
10-second GIF: open wide to catch wind and cargo → narrow to clear doorway without dropping it → invert to catch falling object.
Minute-1 decision: open wide for movement or narrow for safe clearance.
Minute-20 climax: carry/catch objective while wind and shelter requirements conflict.
Hour-3 depth: wind directions/classes, cargo classes, overhead hazards, constrained spaces, shelter-sensitive agents.
Hour-10 defense: multi-object state tradeoffs and route execution; not new umbrella powers per level.
One-week kill: deterministic 4-state prototype; kill if one angle dominates >60% active time or players describe states only as speed settings.
Scope ceiling: 2D, four angle bands, <=4 wind classes, <=6 interacting object classes, no cloth/free aerodynamics.

### G4C43 — Command Wake — SURVIVE

60-second trace: 0–10s leader circles Agent A; A follows east patrol. 11s leader crosses A's visible wake from left→right; A switches for exactly one routine cycle to `TURN_RIGHT_AT_NEXT_NODE`. 15–25s leader moves toward B while A reaches node and turns south. 26s leader crosses B wake backwards; B changes from `HOLD` to `FOLLOW_NEXT_WAKE` for one cycle. 30–42s A's altered path opens a moving gap while B begins following A's wake. 43–52s leader crosses A again to restore a useful turn; 53–60s all three pass a gate in required order.

Readability contract: each agent owns one high-contrast wake lane; wake contains arrow glyphs for the command it will apply; crossing flashes command above agent for <=0.6s; predicted next node is ghosted. No hidden AI state and no more than three command meanings in early game.

Hook: **Issue orders by physically crossing your moving squad's wakes while everyone keeps acting.**
10-second GIF: leader cuts through ally wake → arrow flips → ally turns at next junction without game pausing.
Minute-1 decision: which ally wake to cross first.
Minute-20 climax: chain two temporary commands while navigating the leader through hazards.
Hour-3 depth: wake geometry, routine timing, command expiry, interacting agent routes.
Hour-10 defense: live execution + tactical sequencing; maps recombine a tiny command vocabulary rather than add units endlessly.
One-week kill: kill if players pause mentally/physically >30% time, mispredict next action >15%, or wake overlap becomes unreadable with 3 agents.
Scope ceiling: 2D top-down, leader + max 4 agents, <=5 routine verbs, <=4 wake commands.

### G4C45 — Formation Scar — HARD KILL

60-second trace exposed the problem: every dash changes nav topology, forcing several agents to recompute paths. Even with ghost paths, simultaneous path rerouting produces visual churn; with deterministic simple routing it becomes exploitable maze drawing. The repeated verb is strong but readable tactical causality does not survive the no-pause requirement cheaply. Kill before Phase 2.

### G4C46 — Inside-Out Safe — SURVIVE

First independent decision occurs in ~45–75 seconds: after one demonstrated quarter-turn, player chooses clockwise/counter-clockwise and whether to stop at notch 1 or 2 to align one of two visible cam channels. No textual lockpicking explanation required; internals are always visible.

Hook: **Turn one outer ring and watch an entire transparent mechanical safe rearrange inside.**
10-second GIF: rotate ring one notch → cams lift two pins, close one channel, release a rolling latch elsewhere.
Minute-1 decision: choose direction/notch based on visible downstream internals.
Minute-20 climax: achieve two internal conditions in sequence without directly touching internals, using hysteresis/one-way catches.
Hour-3 depth: cams, followers, one-way catches, pressure plates, stateful latches, ring reversal.
Hour-10 defense: target-state puzzles reuse one physical machine grammar; later challenges ask sequences/efficiency rather than introduce arbitrary mechanisms.
One-week kill: transparent graybox safe; kill if >25% decisions are blind timing, players count notches instead of reading mechanism, or puzzles require labels/numbers.
Scope ceiling: one cross-section machine, one ring input, <=7 mechanical primitive families, discrete deterministic notches.

### G4C37 — Contradiction Stamp — DOWNGRADE / RESERVE

First independent decision can occur inside 2 minutes with three claims and one visible evidence node. However the required mute-clip test fails: stamping a clause and watching dependency lines recompute is understandable only after reading semantic claims. Replacing language with symbols removes much of the deduction fantasy and trends toward circuit logic. Strong puzzle seed, weak discovery/GIF fit for this factory target. Reserve.

## 3. Portfolio-distance audit

This audit compares only high-level identity; it does not import prior mechanics as canon.

- **Seam Thief:** spatial adjacency editing. Distinct from organism/cargo logistics, official-map world rewriting, and portable collision consequences. Moderate abstract-system family resemblance to prior puzzle work, but repeated verb and visual noun differ.
- **Soundproof Smuggler:** stealth/acoustic propagation editing. Strong portfolio distance in fantasy, information model and moment-to-moment pressure.
- **Stagehand Zero:** live theatrical scenery ownership. Strong visual/fantasy distance; deterministic spatial puzzle/action still shares broad systemic-design philosophy only.
- **Debris Sculptor:** selective destruction→construction. Strong physical-action distance; must avoid consequence-transfer framing.
- **Umbrella Engine:** one-object action simulation. Strong portfolio distance and broad-audience visual noun.
- **Command Wake:** turnless embodied tactics. Strong genre/interaction distance.
- **Inside-Out Safe:** one-machine mechanical puzzle. Moderate systemic-puzzle family similarity but very different embodiment and production shape.

The seven survivors form a more diverse portfolio than the Run-2 slate.

## 4. Final Phase-1 slate

The instruction targeted 8–10 survivors only if evidence supported them. Evidence does **not** justify padding the slate. Seven concepts pass all mandatory proofs more convincingly than the rest:

1. G4C01 Seam Thief — tournament seed A
2. G4C19 Soundproof Smuggler — seed A
3. G4C11 Stagehand Zero — seed A
4. G4C24 Debris Sculptor — seed A-
5. G4C47 Umbrella Engine — seed A-
6. G4C43 Command Wake — seed A-
7. G4C46 Inside-Out Safe — seed B+

Reserves: G4C04 One-Bullet Mason, G4C28 Tension Window, G4C37 Contradiction Stamp, plus earlier reserves. Hard kills this run: G4C09 Negative Space Courier, G4C45 Formation Scar.

## 5. Phase-1 completion decision

**PHASE 1 OPPORTUNITY DISCOVERY = COMPLETE.**

Why completion is justified:
- field expanded to 48 seeds across spatial, action, stealth, tactics, deduction and one-object simulation;
- direct analogue pressure removed obvious panel/negative-space and generic formulations;
- finalists have explicit repeated verbs, demo moments, long-session hypotheses, scope ceilings and one-week kill tests;
- final slate remains diverse rather than selecting only the highest-scoring spatial puzzle ideas;
- no concept has been selected.

## NEXT ACTION — PHASE 2 CONCEPT TOURNAMENT RUN 1

Do not select a winner at the start. Put all seven survivors through the same destructive tournament rubric. For each: (1) write a 15–25 minute demo beat sheet; (2) define hour-1/hour-3/hour-10 play; (3) quantify content burden and technical risk; (4) identify dominant-strategy/exploit risks; (5) run pairwise `which would I wishlist from a muted 10-second clip?`; (6) test controller/onboarding/accessibility; (7) test whether the one-week graybox can invalidate the core; (8) score hook, feel, depth, demo, scope, market distance and portfolio distance; (9) eliminate at least two if evidence supports elimination; (10) do not lock product thesis until a later tournament pass has attacked the leading 3–4 again.
