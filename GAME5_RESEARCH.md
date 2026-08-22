# GAME #005 — OPPORTUNITY DISCOVERY — RUN 1

Last updated: 2026-08-22
Factory run: **1**
Phase: **1 — Opportunity Discovery**
Concept selected: **NO**
Production implementation: **NOT STARTED**

This is the first clean-slate discovery pass for Game #005. Previous games are historical portfolio constraints only; none of their mechanics are privileged starting points.

---

## 1. Current market/discovery pressure

### 1.1 Steam is extremely crowded
Third-party release analysis counted more than 21,000 Steam launches in 2025, roughly dozens of new releases per day. A good small game therefore cannot rely on genre label or competent execution alone; the first store image and first seconds of play need a specific, ownable interaction.

Reference:
- Indie Launch Lab, 2026 Steam-release analysis: https://indielaunchlab.com/blog/20k-games-launched-on-steam-in-2025-what-the-data-reveals-about-your-competition

### 1.2 Next Fest is useful but not a rescue mechanism
Valve describes Next Fest as a demo-first audience/feedback event and explicitly positions demos as useful when players need to touch a game to understand it. Current Steam documentation also confirms demos are separate App IDs and that a title normally chooses one Next Fest appearance.

Third-party 2026 festival analyses consistently show a very top-heavy result distribution: thousands of demos compete at once and a small top slice captures most wishlist gains. One June-2026 dataset tracked 4,244 demos and estimated that roughly the top 4% captured about 70% of wishlist gains. Exact third-party numbers are not treated as Steam truth, but the directional lesson is strong: **a merely decent demo is not enough; the mechanic itself must create immediate desire.**

References:
- Steamworks demos: https://partner.steamgames.com/doc/store/application/demos
- Steamworks Next Fest: https://partner.steamgames.com/doc/marketing/upcoming_events/nextfest
- Steamworks upcoming events: https://partner.steamgames.com/doc/marketing/upcoming_events
- SakujoData June 2026 analysis: https://www.sakujodata.com/reports/steam-next-fest-june-2026
- Steam Page Analyzer 2026 synthesis: https://www.steampageanalyzer.com/blog/how-to-get-steam-wishlists

### 1.3 Genre demand does not erase saturation
Current public analyses show continued demand for cozy games, simulation and some strategy subgenres, but also heavy competition. June-2026 Next Fest analysis suggested Simulation/RPG over-indexed while broad Strategy/Adventure were crowded, and Tower Defense under-indexed. Roguelite/deckbuilder/survivors-style spaces remain highly supplied. Cozy language has expanded sharply on Steam over recent years.

The factory should therefore use these as **audience signals**, not as permission to clone a trend. A small project entering cozy, horror, automation or roguelite territory still needs a mechanical signature visible before the player reads a paragraph.

References:
- PC Gamer / GameDiscoverCo cozy trend summary: https://www.pcgamer.com/games/life-sim/the-cozy-game-boom-is-the-clearest-trend-on-steam-over-five-years-of-data/
- Steam Trend Hunter current public radar: https://steamtrendhunter.com/
- SakujoData June 2026 analysis: https://www.sakujodata.com/reports/steam-next-fest-june-2026

### 1.4 Indie opportunity remains real, but novelty must be producible
Recent industry coverage continues to describe a gap between risk-averse large publishers and smaller studios able to make distinctive games. This is favorable to the factory only if novelty comes from **small rules with strong consequences**, not expensive content or technical spectacle.

Reference:
- The Guardian, 2026-08-19, indie-development landscape: https://www.theguardian.com/games/2026/aug/19/will-the-future-of-gaming-be-powered-by-upstart-indie-developers

---

## 2. Run-1 opportunity rules

A seed advances only if it plausibly offers all of the following:
1. a 5–15 second repeated action, not only a high-level premise;
2. visible immediate consequence suitable for a muted GIF/clip;
3. second-order depth from interaction of a small rule set;
4. a 15–25 minute demo that reaches the true differentiator;
5. low-to-moderate bespoke art/content burden;
6. controller viability without pixel-precision UI;
7. cheap one-week graybox falsification;
8. a credible 4–8 hour premium shape without feature inflation;
9. enough market distance that the pitch is more specific than a saturated tag;
10. enough portfolio distance from Games #001–#004.

### Portfolio exclusion pressure
Do not rediscover prior factory identities as Game #005:
- no cargo/logistics game whose central fantasy is moving resources through a system;
- no official-map/label edit that rewrites world ontology;
- no portable collision consequence / impact banking;
- no sound-routing barrier / selective-hearing stealth;
- avoid simply reviving Game #004 tournament reserves (`Seam Thief`, `Command Wake`, etc.) under new nouns.

---

# 3. Broad opportunity field — 40 distinct seeds

The working names below are disposable labels. None is selected.

## Territory A — motion / physical-state manipulation

### G5C01 — Frame Pin
**Verb:** touch one moving mechanism/object to pin it at its exact current animation pose; pinning another releases the first.

Visible payoff: a crusher freezes halfway down and becomes a bridge; later a rotating arm freezes as cover while the old bridge resumes moving.

Depth source: one-active-pin constraint + pose choice + moving machinery + player traversal. Cheap graybox. Main risk: familiar time-freeze perception unless the `one pose becomes physical infrastructure` identity is strong.

### G5C02 — Tension Budget
**Verb:** drag one anchor along a visible cable network; tension redistributes deterministically through connected lifts, gates and platforms.

Visible payoff: pull one line tighter and a distant platform rises while another sags.

Depth source: conserved tension across several loads. Risk: cable physics can become opaque or technically fussy; should use discrete deterministic states rather than soft-body simulation.

### G5C03 — Friction Exchange
**Verb:** slide a single friction token between marked surfaces; making one grippy makes another slick because total friction budget is conserved.

Visible payoff: crate stops on one ramp while another begins sliding.

Depth source: surface state × moving bodies × traversal. Risk: abstract resource explanation and low fantasy appeal if not embodied physically.

### G5C04 — Anchor Swap
**Verb:** designate exactly one movable object as world-anchored; environmental motion then moves everything except the anchor.

Visible payoff: room shifts/tilts while one selected crate remains fixed, becoming a relative-motion tool.

Depth source: reference-frame reasoning. Risk: camera/physics readability and potential similarity to gravity/perspective puzzles.

---

## Territory B — light / shadow / visibility

### G5C05 — Shadow Scaffold
**Verb:** reposition one portable lamp so selected cast shadows become solid walkable/occluding geometry.

Visible payoff: a statue's shadow becomes a bridge; turning the lamp changes both route and enemy cover.

Depth source: object silhouette × light angle × traversal × hazards. Strong GIF. Risk: robust shadow collision and expectation management.

### G5C06 — Searchlight Mason
**Verb:** deliberately step into/redirect hostile searchlights because illuminated construction surfaces become solid only while watched by the beam.

Visible payoff: bait a sweeping light across a gap to temporarily build your own platform.

Depth source: exposure as both danger and construction resource. Risk: could collapse into timing platformer rather than systemic planning.

### G5C07 — Reflection Predator
**Verb:** rotate one mirror panel; your reflection becomes an autonomous hostile/usable physical copy moving symmetrically.

Visible payoff: rotate mirror so the reflection presses a distant switch while avoiding collision with you.

Depth source: mirror geometry + symmetric movement + hazards. Risk: clone/mirror puzzles are established and may be too execution-heavy.

### G5C08 — Aperture World
**Verb:** rotate a physical aperture/lens that exposes only one angular slice of a layered room; objects in the exposed slice become interactive/solid.

Visible payoff: turning the aperture swaps which machinery layer physically exists.

Depth source: spatial selection + motion. Risk: perception can resemble dimension-switching games; must stay visually immediate.

---

## Territory C — fluid / weather / environmental routing

### G5C09 — Rain Router
**Verb:** slide/rotate one gutter/awning module to redirect visible rainfall between channels, machines, plants and electrical hazards.

Visible payoff: move an awning; one turbine stops, a plant bridge grows elsewhere, a short-circuit threat moves with the water.

Depth source: one water stream feeding mutually exclusive consequences. Strong cozy/industrial visual range. Risk: growth pacing and water-flow readability.

### G5C10 — Pressure Line
**Verb:** move one seal/valve between authored pipe junctions; pressure reroutes through a small visible network and physically drives doors, pistons and launchers.

Visible payoff: seal one branch and three gauges/pistons change immediately.

Depth source: pressure path + mechanical state + traversal. Risk: could feel like generic pipe puzzle unless the player manipulates the same live machinery while moving through it.

### G5C11 — Tide Ledger
**Verb:** open one basin gate at a time in a fixed-volume water system; every rise somewhere visibly lowers another region.

Visible payoff: flood a channel to float a raft while exposing a lower tunnel elsewhere.

Depth source: conserved water volume + buoyancy/traversal. Risk: slow state changes and content becoming basin arithmetic.

### G5C12 — Fog Valve
**Verb:** route one bank of dense fog through ducts; fog blocks sight, reveals airflow and changes which surfaces condense/slip.

Visible payoff: move fog from enemy corridor to turbine intake, trading stealth cover for machine behavior.

Depth source: one environmental state serving several affordances. Risk: visual obscurity and accidental stealth overlap with Game #004.

---

## Territory D — time / process / routine

### G5C13 — Deferred Step
**Verb:** mark one action so it repeats automatically exactly a few seconds later while the player continues moving.

Visible payoff: press a switch now; its echo press happens later while you are elsewhere.

Depth source: delayed causality + positioning. Risk: time-loop/echo mechanics are crowded and can become timeline bookkeeping.

### G5C14 — Routine Possession
**Verb:** directly control one worker/robot for a short route, then release it to repeat that learned routine while you possess another.

Visible payoff: teach bot A a 6-second loop, leave it running, then embody bot B to exploit the synchronized routine.

Depth source: authored short routines composing into live automation. Risk: route memorization and automation scope; should remain tiny-room action-puzzle, not factory logistics.

### G5C15 — Conveyor Deadline
**Verb:** physically tag one moving job/object as `NEXT`; autonomous workers immediately reorganize around that priority while the floor keeps running.

Visible payoff: one priority touch reshuffles several worker routes and machine waits.

Depth source: queue priority + spatial consequences. Risk: logistics/production identity too close to earlier portfolio and UI abstraction.

### G5C16 — Machine Pause
**Verb:** stop exactly one machine process while all others continue; releasing it resumes from its exact phase rather than resetting.

Visible payoff: freeze a piston cycle to create a temporary route while another system overtakes it.

Depth source: phase relationships among a few deterministic machines. Risk: overlaps G5C01; weaker physical noun and more timing-oriented.

---

## Territory E — object-property inheritance / conservation

### G5C17 — Door Memory
**Verb:** every special doorway remembers one visible property of the last object that passed through and applies that property to the next eligible object.

Visible payoff: push a heavy crate through; the doorway becomes `heavy`, then the next light cart emerges heavy enough to trigger a plate.

Depth source: local property sequencing + traversal. Risk: rule explanation and semantic similarity to world-property puzzle games; must stay physical and finite.

### G5C18 — Shape Budget
**Verb:** stretch one linked object and another shrinks because the pair shares fixed total volume/length.

Visible payoff: lengthen a bridge while a blocking pillar visibly contracts.

Depth source: conserved geometry + simultaneous utility/cost. Risk: deformation tech and `size puzzle` familiarity.

### G5C19 — Shared Mass
**Verb:** pump mass between exactly two marked objects while conserving total mass.

Visible payoff: make one crate heavy enough to anchor a lift while the other becomes light enough to float/blow away.

Depth source: mass affects pressure, acceleration, buoyancy. Risk: could become a property-transfer cousin of previous causal-transfer design; physics QA can expand quickly.

### G5C20 — Polarity Inheritance
**Verb:** the last object crossing a gate sets its magnetic polarity; the next object inherits it, changing attraction/repulsion relationships.

Visible payoff: one crossing flips a whole small chain of object motion.

Depth source: ordered transfer + magnetic geometry. Risk: magnets are familiar and polarity chains can be hard to predict visually.

---

## Territory F — repair / deduction / controlled failure

### G5C21 — Broken Rule Workshop
**Verb:** inspect a tiny live machine, swap exactly one connection/rule chip, then run it and watch the causal failure/success immediately.

Visible payoff: reroute one link and a whole absurd machine behaves differently in seconds.

Depth source: diagnosis from behavior, not static logic grids; small reusable components. Risk: may become an engineering puzzle UI instead of embodied play.

### G5C22 — Fault Cartographer
**Verb:** deliberately induce one controlled overload/test pulse to reveal hidden structural faults through visible failure propagation, then choose the next test location.

Visible payoff: one stress pulse cracks/reveals a network of weak joints without destroying the whole facility.

Depth source: deduction from partial observations + risk budget. Risk: content authoring and explanation burden; hidden-information fairness must be excellent.

### G5C23 — Machine Autopsy
**Verb:** remove one moving module from a broken machine and place it on a test bench; the machine's remaining behavior reveals what the module was actually doing.

Visible payoff: removing a gear makes one subsystem fail but unexpectedly fixes another.

Depth source: causal isolation. Risk: content-heavy bespoke machines and low replay/systemic leverage.

### G5C24 — Live Blueprint
**Verb:** trace one physical linkage in the world and temporarily highlight every downstream dependent mechanism; choose one intervention point.

Visible payoff: one traced lever reveals a whole live dependency chain.

Depth source: systems comprehension. Risk: too close to analysis tool rather than a satisfying repeated action; also drifts toward map/graph abstraction.

---

## Territory G — ecology / cozy systemic play

### G5C25 — Sunpatch Garden
**Verb:** move one large mirror/reflector to relocate a bright sun patch; plants and small creatures react on compressed time and reshape traversal/resources.

Visible payoff: move sunlight from vine A to flower B; one bridge retracts while pollinators reroute and another path opens.

Depth source: one energy source with competing ecological consumers. Strong cozy readability. Risk: waiting/growth pacing and asset animation burden.

### G5C26 — Bee Traffic
**Verb:** relocate one physical scent marker; nearby bees reroute their deterministic pollination circuit toward it.

Visible payoff: swarm route bends, flowers bloom in a new order, opening environmental consequences.

Depth source: routing + plant state + player movement. Risk: can become graph-routing cousin of previous games and may read as cute automation rather than action.

### G5C27 — Pond Pump
**Verb:** rotate one reversible pump between pond channels; water level/flow changes fish, lilies, debris and access.

Visible payoff: reverse pump and a whole tiny pond ecosystem reconfigures visibly.

Depth source: flow + buoyancy + ecology. Risk: similar to Tide Ledger but less distinctive.

### G5C28 — Root Pressure
**Verb:** clamp one root junction in a visible underground network, forcing growth pressure/nutrients into another branch that physically pushes through terrain.

Visible payoff: clamp left root; right root swells, lifts a stone and opens a route.

Depth source: biological network + physical growth. Risk: close to pipe-routing logic and potentially expensive organic animation.

---

## Territory H — management / automation without spreadsheet play

### G5C29 — Load Shedding
**Verb:** physically plug one portable power coupler into a machine; because total power is capped, another machine immediately slows/stops.

Visible payoff: power the lift, lights dim and a conveyor halts; replug mid-route to reshape the facility.

Depth source: conserved power + live traversal/production. Risk: familiar power-routing puzzle and potential setup play.

### G5C30 — Queue Warden
**Verb:** move one physical priority gate in a crowd/service queue; people reroute according to visible needs and deadlines.

Visible payoff: shift gate one lane and the whole crowd composition changes, helping one case while delaying another.

Depth source: queue dynamics + conflicting service goals. Risk: NPC AI/content burden and abstract management rules.

### G5C31 — Junction Foreman
**Verb:** carry one route-sign module and snap it onto an intersection, changing deterministic cart/worker routing while you stay on the floor.

Visible payoff: one sign move redirects several moving agents.

Depth source: live routing. Risk: **high portfolio contamination** with cargo/logistics and close conceptual ancestry to factory-routing games.

### G5C32 — Night Shift Relay
**Verb:** possess one autonomous worker at a time to perform a short task, then leave behind that repeated routine; later workers interact with those loops.

Visible payoff: a tiny workplace gradually runs itself from routines the player physically taught.

Depth source: embodied automation + interference between routines. Risk: overlaps Routine Possession and can balloon into management/content scope.

---

## Territory I — architecture / structure

### G5C33 — Hinge Room
**Verb:** grab one structural wall/floor segment and rotate it around a fixed hinge while attached objects and routes remain physically coherent.

Visible payoff: a wall becomes floor, redirects rolling hazard and exposes a doorway in one move.

Depth source: one rigid transform with multiple collateral effects. Risk: spatial puzzle familiarity and collision QA.

### G5C34 — Load Path
**Verb:** remove/reinsert exactly one support beam; the small structure flexes into one of several deterministic load states rather than freely collapsing.

Visible payoff: pull beam A; upper walkway sags into a ramp while another gap opens.

Depth source: structural dependency + traversal. Risk: must look physical without requiring expensive structural simulation.

### G5C35 — Tape Floor
**Verb:** peel one marked strip of floor/wall and re-stick it onto another compatible surface, carrying its friction/conveyor/hazard property.

Visible payoff: peel a moving walkway strip and stick it on a wall to make a vertical conveyor route.

Depth source: relocating surface affordance. Risk: topology/portal-adjacent perception and technical edge cases; too close to prior Seam-style reserve territory.

### G5C36 — Window Counterweight
**Verb:** slide one giant window/opening along a wall; because it is counterweighted, another opening moves oppositely elsewhere in the structure.

Visible payoff: opening a route for yourself simultaneously exposes/closes another route.

Depth source: coupled architecture. Risk: low systemic ceiling unless combined carefully; may feel like linked doors.

---

## Territory J — action / expressive systemic oddities

### G5C37 — Zero-G Tool Orbit
**Verb:** release/throw a tool in a compact zero-g room; instead of drifting away forever it enters a predictable orbit around a local anchor until caught/reused.

Visible payoff: throw wrench into orbit, let it repeatedly hit switches/obstacles while you move elsewhere, then intercept it.

Depth source: persistent trajectories + small set of tool interactions. Strong action clip. Risk: orbital readability and input feel; must avoid full orbital-physics simulation complexity.

### G5C38 — Harvest Shockwave
**Verb:** harvest/cut one plant; the action emits a visible mechanical shock through connected stems, causing neighboring plants/objects to bend, seed or release.

Visible payoff: one harvest triggers a controllable chain that changes the garden and movement route.

Depth source: chain topology + timing + cultivation. Risk: can resemble chain-reaction mobile puzzle if traversal/action is weak.

### G5C39 — Mirror Chase
**Verb:** rotate/slide one mirror plane while an enemy/creature on the reflected side mirrors your movement; geometry changes which reflected motion is dangerous or useful.

Visible payoff: alter the mirror so your pursuer's symmetric path hits a switch instead of you.

Depth source: live movement + reflection geometry. Risk: mirror-clone precedent and cognitive load.

### G5C40 — Heatmark Runner
**Verb:** every fast movement leaves a short-lived hot trail that powers/warps only objects it touches; the player deliberately draws routes while staying in motion.

Visible payoff: sprint a curve around machinery, the glowing trail sequentially opens/overheats devices behind you.

Depth source: movement expression + trail geometry + time decay. Risk: drawing-path games and execution precision; controller smoothing needed.

---

# 4. Destructive triage — Run 1

This triage is intentionally coarse. It removes obvious scope/identity problems but does **not** select a concept.

## Early CUT — poor factory fit unless radically mutated
- **G5C12 Fog Valve** — mechanical state is interesting, but stealth/visibility routing sits too close to HEARWALL's portfolio territory and fog hurts readability.
- **G5C13 Deferred Step** — delayed-action echo is understandable but crowded and easily becomes timeline bookkeeping.
- **G5C15 Conveyor Deadline** — routing/priority language drifts toward logistics/automation already represented elsewhere.
- **G5C16 Machine Pause** — dominated by the more physical and marketable G5C01 Frame Pin.
- **G5C23 Machine Autopsy** — high bespoke content burden per puzzle; weak systemic reuse evidence.
- **G5C24 Live Blueprint** — repeated action is mainly analysis/highlighting rather than a satisfying world manipulation.
- **G5C27 Pond Pump** — dominated by Rain Router/Tide Ledger; weaker visual identity.
- **G5C31 Junction Foreman** — strong live-routing verb but too close to logistics/factory portfolio territory.
- **G5C32 Night Shift Relay** — currently dominated by the smaller/cleaner G5C14 Routine Possession.
- **G5C35 Tape Floor** — too close to topology/seam reserve territory and exposes disproportionate collision/placement QA.
- **G5C36 Window Counterweight** — clean but likely too shallow as a whole premium game without adding systems.

## HOLD / needs an attack before survival
- G5C03 Friction Exchange — strong systemic math, weak fantasy/marketing noun.
- G5C04 Anchor Swap — interesting reference-frame reasoning, technical/readability risk.
- G5C06 Searchlight Mason — great clip, danger of becoming timing platformer.
- G5C07 Reflection Predator — readable but familiar mirror/clone ancestry.
- G5C08 Aperture World — strong image, dimension-switch familiarity.
- G5C11 Tide Ledger — elegant conservation, potentially slow/arithmetical.
- G5C18 Shape Budget — good collateral consequence, deformation/size-puzzle familiarity.
- G5C19 Shared Mass — deep property interactions, but physics QA and transfer-theme overlap risk.
- G5C20 Polarity Inheritance — good chains, magnets highly familiar.
- G5C22 Fault Cartographer — strong deduction, hidden-information fairness/content cost unresolved.
- G5C26 Bee Traffic — charming but routing ancestry and swarm readability risk.
- G5C28 Root Pressure — unusual physical fantasy, organic animation and network-puzzle risk.
- G5C29 Load Shedding — clear, but conventional power-budget puzzle territory.
- G5C30 Queue Warden — potentially distinctive management, NPC/content burden high.
- G5C33 Hinge Room — clean physical verb, genre familiarity and collision burden.
- G5C34 Load Path — strong structural fantasy if deterministic, but simulation illusion must be cheap.
- G5C38 Harvest Shockwave — strong chain visual, risk of shallow chain-reaction puzzle.
- G5C39 Mirror Chase — action potential, mirror precedent/readability risk.
- G5C40 Heatmark Runner — expressive movement, may become precision path drawing.

## ADVANCE to deeper Phase-1 pressure
These are **not finalists**; they are the strongest Run-1 evidence targets.

### A1 — G5C01 Frame Pin
Why alive: immediate physical clip, one-button noun/verb, cheap deterministic graybox, strong sequencing potential, good controller fit.

Run-2 kill question: after 12 mature states, is it more than `freeze moving thing at useful moment`?

### A2 — G5C02 Tension Budget
Why alive: one visible local action causes several collateral physical changes; conservation creates second-order tradeoffs.

Run-2 kill question: can the player predict tension without numbers/soft-body simulation, and can 10-second clips show cause clearly?

### A3 — G5C05 Shadow Scaffold
Why alive: exceptionally visual, traversal + cover/hazard consequences from one light move, strong screenshot/GIF identity.

Run-2 kill question: does solid-shadow behavior remain intuitive across varied shapes, or does it become fragile geometry tech and trial-and-error?

### A4 — G5C09 Rain Router
Why alive: physical environmental noun, potentially cozy or industrial, multiple mutually exclusive consequences from one water route.

Run-2 kill question: can it stay active and tactile instead of becoming slow setup/growth waiting?

### A5 — G5C10 Pressure Line
Why alive: small deterministic network can generate visible multi-machine reactions, easy to prototype with discrete pressure states.

Run-2 kill question: can normal play look like inhabiting machinery rather than solving pipes on a graph?

### A6 — G5C14 Routine Possession
Why alive: embodied automation has action/management crossover and a strong `teach one bot, leave it running` clip.

Run-2 kill question: can it avoid route memorization, dead waiting and factory/logistics scope while supporting hour-5 depth?

### A7 — G5C17 Door Memory
Why alive: unusual local causal rule, sequencing depth from a tiny vocabulary, easy deterministic prototype.

Run-2 kill question: can a non-technical player predict property inheritance from world presentation alone, and is the fiction more than arbitrary magic doors?

### A8 — G5C21 Broken Rule Workshop
Why alive: controlled experiment loop, low art requirement, highly streamable `change one thing → machine behaves unexpectedly` moments.

Run-2 kill question: does the repeated action feel like play rather than circuit-editor homework, and can content scale systemically?

### A9 — G5C25 Sunpatch Garden
Why alive: strong cozy audience compatibility without cloning farming loops; one sunlight source creates competing ecological consequences.

Run-2 kill question: can growth/reaction happen fast enough to support a 5–15 second loop and demo without feeling fake or idle?

### A10 — G5C37 Zero-G Tool Orbit
Why alive: tactile action identity, persistent consequences, high GIF value, portfolio distance, tiny-room scope.

Run-2 kill question: can orbits be predictable/controller-friendly without exposing heavy orbital mechanics or devolving into throw-at-switch puzzles?

---

# 5. Preliminary rough score — evidence priority only

Scores are intentionally low-confidence. They decide what to attack next, not what to build.

Dimensions: Hook / Repeated feel / Demo / Systemic depth / Scope safety / Technical predictability / Readability-controller / Market distance / Portfolio distance / Cheap falsification. Each 0–10, equal-weight for this first pass.

| Seed | Score /100 | Run-1 note |
|---|---:|---|
| G5C01 Frame Pin | **86** | cleanest physical verb + cheap graybox; originality ceiling unproven |
| G5C05 Shadow Scaffold | **84** | strongest visual hook; geometry/readability risk |
| G5C02 Tension Budget | **82** | excellent collateral-system promise; predictability risk |
| G5C37 Zero-G Tool Orbit | **81** | action/portfolio strength; trajectory feel risk |
| G5C09 Rain Router | **80** | broad visual/systemic potential; pacing risk |
| G5C10 Pressure Line | **79** | deterministic and scalable; pipe-puzzle abstraction risk |
| G5C17 Door Memory | **78** | unusual rule and sequencing; explanation/fantasy risk |
| G5C25 Sunpatch Garden | **78** | cozy-compatible distinctive control; growth/wait risk |
| G5C14 Routine Possession | **77** | embodied automation; choreography/scope risk |
| G5C21 Broken Rule Workshop | **76** | strong deduction loop; UI/editor feel risk |

No score is decisive enough for Phase 2.

---

# 6. Cross-concept discoveries

Run 1 suggests several promising opportunity shapes that are more useful than any single seed yet:

1. **Conserved physical quantity** is promising when visually embodied (tension, water, mass, power), because every helpful change automatically creates a cost elsewhere. The danger is arithmetic/UI abstraction.
2. **One active world-state override** is especially scope-safe (one pinned pose, one light, one barrier-like physical controller) because it creates sequencing without inventory. Game #005 should avoid repeating HEARWALL's barrier identity, but the general production lesson remains valid.
3. **Embodied automation** can bridge action and management if the player teaches/manipulates routines directly in space instead of operating a spreadsheet. Scope must stay tiny.
4. **Compressed ecology** may offer a cozy-facing systemic product without farming-sim content burden if reactions are immediate enough to feel like gameplay rather than waiting.
5. **Controlled failure/diagnosis** is an underused fantasy with low asset needs, but it needs a tactile world verb; pure circuit UI is not sufficient.
6. In this market, **mute-clip legibility and demo interaction are not marketing extras**. The candidate mechanic itself should be the marketing material.

---

# 7. Run-2 falsification plan

Phase 1 is **not complete**. The next pass must broaden and attack before the tournament.

### Mandatory next work
1. Expand the field from 40 to at least **50–60 seeds**, specifically adding territories underrepresented in Run 1: direct action/combat-without-combat, social/crowd systems, spatial audio-excluded sensory mechanics, micro-simulation/management, and non-room-based formats.
2. Run targeted nearest-neighbor searches for the ten current ADVANCE seeds before emotionally attaching to them.
3. For each current ADVANCE seed, write at least **6 mature encounter/state kernels** using only its smallest rule vocabulary.
4. Kill candidates whose depth requires adding a second pillar, large bespoke content, freeform physics, long waiting, or a modal graph/editor UI.
5. Perform a muted 10-second clip test and a 20-minute demo beat test on at least the top 12 after expansion.
6. Explicitly compare production burden and one-week graybox cost.
7. Reduce Phase-1 survivors to roughly **6–10** only after those attacks.
8. Do **not** select Game #005 until Phase 2 Concept Tournament.

## NEXT ACTION
Create `GAME5_RESEARCH_RUN2.md` with field expansion, nearest-neighbor pressure and mature-state falsification. Phase 2 remains locked until Phase 1 has a defensible survivor set.
