# GAME #006 — CONCEPT TOURNAMENT — RUN 3 FINAL SELECTION DUEL

Last updated: 2026-08-29
Factory run: **4**
Phase: **2 — Concept Tournament / FINAL SELECTION**
Final concept selected: **YES — G6C01 Stitchspace**
Production implementation started: **NO**

This run executes the exact final-selection duel required by `STATUS.md` across the remaining three contenders: **Stitchspace**, **Signal in Flight**, and **The Short Circuit**. The decision is made under one common small-team assumption and emphasizes a market-legible repeated verb, hour-scale depth without feature accretion, deterministic implementation, controller viability, content throughput, demo conversion, and portfolio distance from Games #001–#005.

---

# 1. Fresh exact-mechanic market check — 2026-08-29

The final check used the refined mechanic wording, not broad genre labels.

## 1.1 Stitchspace
The unavoidable comparison set is still spatial-puzzle games rather than a direct mechanical match. `Portal`/Portal-derived games establish the audience expectation for two-endpoint traversal links, while `Manifold Garden` and `Viewfinder` prove that a premium game can successfully sell a single strong spatial rule when the rule is visually unmistakable and produces escalating transformations. `Folding Dungeon` remains the closest 2026 warning because it explicitly folds/connects space.

Relevant references:
- Portal 2 / Portal lineage: https://store.steampowered.com/app/620/
- Bridge Constructor Portal: https://store.steampowered.com/app/684410/
- Manifold Garden: https://store.steampowered.com/app/473950/
- Viewfinder: https://store.steampowered.com/app/1382070/
- Folding Dungeon: https://store.steampowered.com/app/4576650/Folding_Dungeon/

No current checked product was found whose primary repeated action is exactly **moving one endpoint of a scarce persistent seam so that one room-boundary adjacency is destroyed at the same instant another adjacency is created**, with orientation, occupancy and disconnection as core puzzle state.

Market conclusion: **meaningful whitespace survives, but only if the game presents seams as adjacency replacement, not portal placement**.

## 1.2 Signal in Flight
`The Signal State` is an established modular-signal puzzle with Very Positive reception, and signal-routing/logic games remain common. The finalist is mechanically distinct because it edits the machine **after commands have already entered execution**, but the market screenshot vocabulary still risks reading as wires/nodes/signals until motion is seen.

Relevant references:
- The Signal State: https://store.steampowered.com/app/1577620/
- Sokosignal: https://store.steampowered.com/app/2154700/Sokosignal/

Market conclusion: distinction is real, but the hook is less screenshot-legible and more dependent on moving UI/state explanation than Stitchspace.

## 1.3 The Short Circuit
Searches still found electronics construction, fault-as-failure and broad satirical wiring/fault products, but no checked game centered cleanly on **deliberately invoking deterministic protection/fallback states as the repeated puzzle verb**. This is good whitespace.

The problem is not novelty; it is content breadth. Four fallback families are enough for a strong demo, but there is a material risk that hour-5 player language collapses to `trip the right breaker after preparing the room`.

Market conclusion: strongest surprise fantasy of the three, but weaker evidence for sustained transformation without bespoke device/fallback content.

---

# 2. Finalist A — STITCHSPACE

## 2.1 Exact Steam pitch
**Rewire which rooms physically touch: move the ends of a few persistent seams, cross the impossible boundaries you create, and exploit the route you destroy every time you make a new one.**

This wording deliberately avoids `portal`, `teleport`, `fold` and `connect any two places`.

## 2.2 Ten-second muted trailer beat
0–2s: three separated rooms sit in one readable diagrammatic world; a seam visibly joins Room A north edge to Room B west edge.
2–4s: a rolling crate crosses and exits sideways in B.
4–6s: player drags only endpoint B from B-west to C-south; the old A↔B seam visibly unzips while A↔C zips into existence.
6–8s: the crate is now stranded in B while the player crosses into C.
8–10s: moving the other endpoint creates a loop and a previously isolated hazard loses access to the player.

Required silent takeaway: **a seam is scarce persistent adjacency; moving it replaces the old connection and changes the topology for everyone.**

## 2.3 Exact first 20 minutes
0–4: one seam already exists. Player crosses it, then moves one endpoint once. The destroyed old adjacency is shown as strongly as the new one.
4–7: a rolling object establishes orientation mapping. The player chooses edge pair for exit direction rather than distance.
7–10: one seam must first route a crate and then the player. The key lesson is reuse, not two-portal placement.
10–13: the player deliberately moves an endpoint after a hazard/object crosses, turning **disconnection** into a positive action.
13–16: first loop using two ordinary passages plus one seam. Crossing order changes which local side an object can approach from.
16–20: compact three-room synthesis with two valid solutions: one orientation-first and one temporary-isolation-first. A direct current-room-to-goal seam is intentionally insufficient.

By minute 20 the product must already have shown connection, replacement, orientation, scarce reuse, and useful disconnection.

## 2.4 First two hours
0:20–0:45: adjacency replacement becomes the default assumption; first cases where a useful previous route must be sacrificed, plus simple loops and object/player ordering.
0:45–1:15: second seam, deterministic occupancy lock, temporary bridging, swapped adjacency between four rooms.
1:15–2:00: mature small graph states with 3–4 rooms, 1–2 seams, one moving/rolling entity and one material disconnect consequence. At least three solution skeleton families appear before hour 2.

No new primary verb is required after the second seam appears. Later depth should come from graph cuts, loops, orientation, occupancy and state-dependent rewiring.

## 2.5 Minimum shippable commercial scope
- PC/Steam first, single-player premium;
- 30–36 main authored cases;
- 6–10 optional remix/mastery cases only if they change causal topology rather than socket labels;
- 1 seam early, 2 seams common later, 3 seams absolute rare ceiling unless empirical evidence proves need;
- 2–5 rooms per normal case, with 6 only for exceptional late synthesis if readable;
- authored boundary sockets only; no free wall drawing;
- deterministic room-local movement and crossing state;
- immediate Undo/Redo and restart;
- 4–7 hour first-clear target, 5–8 hours preferred after prototype/content-throughput proof;
- 15–25 minute representative demo that includes useful disconnection and at least one non-portal-like replacement consequence;
- no combat campaign, procedural infinite mode, recursive portals, freeform non-Euclidean renderer, momentum flinging, physics sandbox, open world or level editor required for 1.0.

## 2.6 Content-production / validation tooling plan
Each case data file declares:
- stable room IDs;
- room-local nodes/lanes;
- exposed edge sockets and orientation mapping;
- ordinary passages;
- seam count and initial endpoints;
- legal endpoint destinations;
- seam occupancy/crossing rules;
- entities and deterministic local movement;
- objectives/invariants;
- known baseline fixture(s);
- transformation tags: CONNECT, DISCONNECT, ORIENTATION, LOOP, OCCUPANCY, SCARCE_REUSE, SWAP, ISOLATE;
- abstract solution skeleton for anti-repetition auditing.

Required tools:
1. structural validator for IDs/sockets/orientation;
2. small graph-state solver/BFS over seam endpoints + discrete entities;
3. known-solution replay;
4. soft-lock/reachability audit;
5. direct-to-goal shortcut search;
6. reasoning-isomorphism report over consecutive cases;
7. portal-like-content detector: flag cases where the lost old adjacency never materially affects the shortest/known solution.

Tooling burden: **medium-high but bounded**. State is discrete and far smaller than general spatial physics.

## 2.7 Content throughput hypothesis
After tooling stabilizes, one designer should be able to graybox several candidate cases/day and promote roughly 1–2 robust cases/day after solver/novelty review. The main production bottleneck is **puzzle quality**, not art or bespoke subsystem coding.

The game is therefore commercially plausible only if the vertical slice proves that replacement/disconnection creates enough distinct skeletons to support ~30 excellent cases without introducing extra verbs.

## 2.8 Strongest likely negative Steam review
> “It’s basically Portal without momentum: put the two ends on the right walls, walk through, repeat.”

This review is treated as an existential content failure, not a marketing complaint.

Canonical defense for later phases:
- mature cases must require a material consequence from the adjacency that disappears;
- disconnection/loop/orientation/occupancy must increasingly matter;
- no level should be included merely because it offers a new geometric place to put entrance/exit.

## 2.9 Perceived value
Spatial transformation has a higher visual/value ceiling than abstract node UI if presentation clearly shows distant rooms becoming neighbors. Premium references such as Manifold Garden ($19.99 checked 2026-08-29) and Viewfinder ($24.99 checked 2026-08-29) demonstrate that a strongly presented single-rule spatial puzzle can sustain premium positioning, but Stitchspace should not assume their art/production level.

Working design-time hypothesis: **$14.99–$19.99**, with $14.99–$17.99 the safer center unless duration, audiovisual identity and review/demo evidence justify $19.99.

## 2.10 Implementation schedule risk
Domain/topology core: Low–Medium.
Crossing/orientation semantics: Medium.
Presentation of remote adjacency: Medium–High.
Content solver/tooling: Medium–High.
Authored content: High design burden, low asset burden.
Controller/input: Low–Medium.
Persistence: Low.
Physics/animation dependency: Low.
Catastrophic unknown: **whether players perceive adjacency replacement rather than portal placement** — cheap to test in primitive graybox.

## 2.11 One-week prototype binary gate
Day 1: room/socket graph + seam endpoint replacement + canonical hash.
Day 2: player crossing + orientation preview + Undo/Redo.
Day 3: deterministic rolling object + old-adjacency destruction visualization.
Day 4: occupancy lock + loop/isolation state.
Day 5: SS01–SS04.
Day 6: SS05–SS08 + bounded solver/shortcut audit.
Day 7: naive user tests + muted 10-second clip test.

PASS only if all are true after one tuning pass:
- >=75% naive testers explain the verb as **changing which rooms are adjacent / moving a connection that removes the old connection**, not simply `placing portals`;
- >=5/8 grayboxes materially depend on the adjacency that is lost, orientation, occupancy, loop or disconnection;
- mature SS04–SS08 produce >=4 abstract solution skeleton families;
- orientation misunderstanding causes <20% ordinary failures after tutorial;
- direct-current-room-to-goal seam is not a shortest valid solution in >=6/8 cases;
- no baseline requires dexterity or timing;
- mute clip communicates that a remote old route disappeared when the new one appeared.

If this fails, do not rescue the game with portal modifiers, momentum or extra seam powers. Reopen or kill.

---

# 3. Finalist B — SIGNAL IN FLIGHT

## 3.1 Exact Steam pitch
**Send commands into a tiny live machine, then change the route while they are already travelling — redirect, separate and synchronize visible pulses whose history decides what your edits can still affect.**

## 3.2 Ten-second muted trailer
Two pulses launch. Junction changes after pulse A crosses. A reaches door; B takes new branch. Player pauses, advances one canonical step, flips another junction and forces simultaneous arrival at two actuators.

The hook is mechanically excellent but requires temporal reading; a still image communicates it poorly.

## 3.3 First 20 minutes / two hours
The existing Run-2 pacing remains sound: one pulse -> mid-flight reroute -> two-pulse order -> Pause/Step -> synchronization. Hour 1 adds queue/history and one pulse changing a route for another; hour 2 reaches 3–4 pulse networks where one static pre-run configuration is insufficient.

## 3.4 Minimum scope
30–36 main cases, 2–5 pulses normal, 6 rare ceiling, finite tracks and authored junctions, canonical Pause/Step, 4–7 hour first clear. No free wiring, programming language or analog timing.

## 3.5 Content/tool burden
State = topology × pulse positions × queue state × actuator state. A bounded solver remains possible but grows faster than Stitchspace. Content tooling needs timeline/state visualization in addition to structural validation, and authoring/debugging alternate solutions is materially heavier.

## 3.6 Negative review
> “A circuit puzzle where I wait for dots to move, pause, flip a switch, and repeat.”

To defeat this, almost every mature case must depend on execution history and create a reason that static configuration cannot express. That is achievable, but readability/UI becomes the dominant production problem.

## 3.7 Perceived value
Strong systemic depth, but screenshots resemble an already familiar signal/logic space. Premium value therefore depends on unusually polished movement/causal visualization and a large enough set of visibly different machines.

Working hypothesis: **$12.99–$17.99** absent exceptional presentation.

## 3.8 Implementation risk
Domain core Medium.
Temporal ordering Medium–High.
UI/readability **Very High**.
Content solver High.
Content QA Very High.
Asset burden Low.
Controller Medium.

The existential question is less cheap than Stitchspace because primitive functionality may work before multi-pulse readability failure appears.

## 3.9 One-week binary gate
PASS only if >=75% testers correctly predict next destinations in mature grayboxes, >=6/8 cases cannot be solved by static pre-run configuration, replay-spam is not the dominant strategy, Pause/Step remains reasoning rather than bookkeeping, and 3–5 simultaneous pulses stay readable on target layout.

**FINAL VERDICT: SECOND PLACE.** Strongest formal depth and excellent portfolio independence, but higher UI/solver/QA risk and weaker still-image/store-page legibility than Stitchspace.

---

# 4. Finalist C — THE SHORT CIRCUIT

## 4.1 Exact Steam pitch
**Fix machines by breaking them on purpose: bridge exposed fault contacts, trip the right protection zone, and use deterministic fail-safe motions before resetting power changes the room again.**

## 4.2 Ten-second muted trailer
Player bridges two service contacts; fuse pops; powered latch drops open; motor spring-returns and shoves a crate; a backup path lights; reset closes the first door while preserving the moved crate.

Best single surprise clip of the field.

## 4.3 First 20 minutes / two hours
Run-2 pacing remains credible: useful trip -> collateral loss -> domain choice -> spring return -> reset consequence -> two-fault synthesis. Primitive vocabulary is complete around 90 minutes.

## 4.4 Minimum scope
28–34 main cases, 3–7 devices/case, 1–3 protection domains early and <=4 normal late, four fallback families, deterministic reset/fault semantics, 4–6 hour first clear. No ordinary circuit construction or electrical arithmetic.

## 4.5 Content/tool burden
State space is discrete and smaller than Signal in Flight. Tooling is feasible: domain validator, fallback/reset transition table, bounded solver, brute-force `trip all domains` audit and solution-skeleton clustering.

The larger burden is authored physical variety. If DROP/SPRING_RETURN/COAST/FAILOVER all use visually similar doors/motors, the commercial fantasy shrinks; if every machine needs bespoke art/animation, production cost rises.

## 4.6 Negative review
> “Funny premise, but every puzzle is set things up, trip a breaker, watch the machine fall back, reset, repeat.”

This is harder to repair canonically than Stitchspace's portal comparison because the repetition may be inherent in the verb rather than merely bad content selection.

## 4.7 Perceived value
Excellent demo/trailer conversion potential, but weaker confidence in 5–8 hour depth. Working hypothesis **$12.99–$17.99** unless testing proves unusually broad non-isomorphic fallback play.

## 4.8 Implementation risk
Domain state Low–Medium.
Visual causal clarity Medium.
Solver Medium.
Content breadth **High existential**.
Asset/animation Medium–High if machines must feel distinct.
Controller Low.

## 4.9 One-week gate
PASS only if >=4/8 cases require pre-fault preparation, >=3 fallback families produce genuinely different solution skeletons, brute-force trip/reset is not shortest in >=6/8, players predict fallback without electronics knowledge, and testers still describe distinct reasoning rather than `breaker puzzle` after the mature packet.

**FINAL VERDICT: THIRD PLACE.** Best surprise fantasy, but its hour-scale breadth is the least proven and the likely repair path increases bespoke content burden.

---

# 5. Final comparison

Scale 1–10, higher is better. `Schedule predictability` means lower development risk.

| Criterion | Stitchspace | Signal in Flight | The Short Circuit |
|---|---:|---:|---:|
| One-sentence hook | **9** | 8 | **9** |
| 10-second mute clarity | **10** | 8 | **10** |
| Still-image/store-page legibility | **9** | 6 | 8 |
| Exact-mechanic whitespace | **9** | 8 | **9** |
| Hour-5/10 depth without new verbs | **9** | **10** | 7 |
| Scope efficiency | **10** | 8 | 8 |
| Deterministic implementation | **10** | 8 | 9 |
| Content solver tractability | **9** | 7 | 9 |
| Content breadth confidence | **9** | 9 | 7 |
| UX/readability risk | **8** | 5 | 8 |
| Controller viability | **10** | 8 | 10 |
| Asset burden | **10** | 10 | 7 |
| Demo strength | **10** | 8 | 10 |
| Cheap existential falsification | **10** | 7 | 9 |
| Portfolio independence | **10** | **10** | 10 |
| Premium-value ceiling | **9** | 8 | 8 |
| Schedule predictability | **9** | 6 | 8 |
| **Total /170** | **160** | **136** | **148** |

The numeric score is not the sole reason for selection. The decisive asymmetry is:

- **Stitchspace** has one major existential risk — `does adjacency replacement read as its own verb rather than portals?` — and that risk can be falsified cheaply with six rectangles and a seam. If it passes, the implementation, solver and asset paths are unusually bounded for the amount of spatial spectacle and systemic depth available.
- **Signal in Flight** may ultimately support the deepest formal puzzle design, but its difficult problem is not the state machine; it is making multiple execution histories continuously legible on controller/Deck-sized UI while keeping authoring/solver complexity manageable.
- **The Short Circuit** has a fantastic premise and demo, but its existential risk appears later: whether the same bounded fault verb genuinely supports a premium-length campaign without bespoke fallback/device proliferation.

---

# 6. Why this game, why now, why not the other two

## Why Stitchspace
1. It creates a strong **visible transformation of space** from a small deterministic graph rule.
2. The repeated command is concise and controller-friendly.
3. Connection and **disconnection are the same atomic action**, giving second-order consequences without an extra resource system.
4. Orientation, loops, occupancy and scarce reuse emerge from the rule rather than from feature accumulation.
5. It can be grayboxed and solver-audited cheaply.
6. It has strong portfolio distance from all previous five games.
7. The spatial hook supports a premium presentation/value ceiling without requiring premium asset volume.
8. The biggest risk can be tested before expensive content production.

## Why now
2026 remains crowded with conventional logic, conveyor, signal and folding/portal-adjacent products. That makes generic `connect spaces` insufficient, but it also sharpens the opportunity: **a game explicitly about replacing physical adjacency rather than placing teleport endpoints or folding geometry** has a clean sentence and visual rule if executed carefully. A crowded Steam environment rewards a mechanic that can be shown in one silent transformation.

## Why not Signal in Flight
Not because it is weaker intellectually. It loses because the core value is harder to communicate before the viewer watches history unfold, and multi-pulse readability/solver QA creates a larger delayed risk. Keep it as the strongest preserved rejected finalist for a future factory cycle only if materially recontextualized.

## Why not The Short Circuit
Not because the premise lacks novelty. It loses because evidence for hour-5/10 transformation is weaker, and the natural repair path is more fallback types / more bespoke machines — exactly the type of feature/content accretion this factory tries to avoid.

---

# 7. Final selection

## WINNER — G6C01 STITCHSPACE

Phase-2 final concept selected: **YES**.

Selection is conditional only on the explicit empirical prototype gate; that gate does **not** prevent Product Thesis from freezing the design direction. If a future prototype fails the adjacency-vs-portal comprehension threshold, the implementation track must reopen/kill rather than silently adding portal-like powers.

Rejected finalists are preserved as selection history and must not be merged into Stitchspace.

---

# 8. Phase-2 closure

- Final market check: **YES**
- Exact pitch/trailer for all finalists: **YES**
- Product pacing comparison: **YES**
- Minimum shippable scope: **YES**
- Content/tooling comparison: **YES**
- Perceived-value review: **YES**
- Schedule-risk comparison: **YES**
- One-week binary gate: **YES**
- Why-now/why-not comparison: **YES**
- Final Game #006 concept: **G6C01 Stitchspace**
- Phase 2 complete: **YES**
- DESIGN COMPLETE: **NO**

## NEXT PHASE
**Phase 3 — Product Thesis Lock for Stitchspace.**

Freeze target player/non-target audience, platform/commercial frame, genre language, exact hook and fantasy, repeated verb, session/core loop, topology vocabulary ceiling, progression thesis, failure/Undo philosophy, presentation thesis, accessibility/input thesis, scope ceiling, explicit 1.0 exclusions, and inherited empirical gate before Phase 4 mechanics.