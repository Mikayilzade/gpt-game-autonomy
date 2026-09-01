# GAME #012 — CONCEPT TOURNAMENT

Date: 2026-09-01
Status: **PHASE 2 ROUND B COMPLETE — 2 finalists**
Authority: tournament evidence only; no final winner or frozen mechanics.

## Round A retained history
Round A forced the 12 Phase-1 survivors through two concrete micro-cases each and killed six concepts whose pitch quality did not survive actual player decisions.

### Round A kills
- **Margin of Error** — arithmetic worksheet / enumeration collapse.
- **Misprint Foundry** — inferior structural sibling of Wrong-Side Assembly.
- **Debt of Distance** — conserved-resource portfolio collision with Game #005.
- **Witness Protection** — exact-cover/incidence-matrix structure without sufficient second-order depth.
- **Public Secret** — state-communication burden overwhelms trailer/UI clarity.
- **Courtesy Gap** — pairwise permutation adjacency to Game #010.

### Round A survivors entering Round B
1. Negative Space Clerk
2. Wrong-Side Assembly
3. The Quiet Majority
4. One Bad Ruler *(fragile)*
5. Ink Bleed
6. Spare Chair

Round B follows the destructive depth-proof contract from `STATUS.md`: tutorial -> inversion/aha -> mastery, minimum grammar, actual search space, human deduction vs blind retries, five content families, collision/saturation check, and candidate-specific kill gates.

---

# ROUND B

## Fresh collision / saturation check — 2026-09-01
The current market makes two collisions especially important.

- **Is This Seat Taken?** (Steam, released 2025-08-07) is already a highly visible seating-preference logic puzzle whose entire surface language is people, seats, adjacency and personal preferences. Steam currently shows thousands of overwhelmingly positive English reviews. Even though Spare Chair uses chair removal + greedy arrival rather than direct placement, a screenshot/trailer would initially communicate the same commercial fantasy and invite direct comparison.
- Ordinary **flood-fill/color-spread** puzzles remain abundant, including current browser/mobile variants and older Steam titles. Ink Bleed can survive only if the player is visibly reasoning about *earlier wet cells becoming future barriers*, not merely maximizing territory or recoloring a connected region.
- A search for negative-space/topology puzzle competition did not reveal a close current Steam analogue whose core verb is placing occluders to satisfy predicates over the *remaining* connected void. The Steam title `Negative Space` (2025) is instead a roguelike deckbuilder, so the phrase itself is occupied as a title but not as this mechanical lane.
- Cellular-automata/majority systems are a known design family. The Quiet Majority therefore needs unusually strong player-readable causal intervention to justify itself rather than relying on simulation spectacle.

Sources checked this round:
- https://store.steampowered.com/app/3035120/Is_This_Seat_Taken/
- https://www.gamingonlinux.com/2025/08/is-this-seat-taken-is-a-wonderful-cosy-logic-puzzle-game-where-you-move-people-around/
- https://store.steampowered.com/app/3624300/Negative_Space/
- https://store.steampowered.com/app/385710/INK/
- https://store.steampowered.com/app/2474880/Paint_by_Cubes/
- https://store.steampowered.com/app/1400920/Flood_Fill/
- https://3dlifegame.com/

---

# 1. Negative Space Clerk — **FINALIST**

## Minimum complete grammar
Theme is explicitly non-canonical; if selected, retheme away from paperwork/stamps. Mechanical grammar needs only:
1. a finite orthogonal board containing initially open and blocked cells;
2. 1–3 placeable opaque pieces from a tiny public shape set (primarily 1x1, 1x2, 1x3; no free polyomino catalogue);
3. pieces occupy open cells and cannot overlap;
4. after placement, the game evaluates predicates over the **remaining open space**: connected-component count, enclosed-hole count/size, boundary contact, component area, and whether named markers share a component.

No movement, rotation system, physics, fold, trim, or document semantics are needed.

## Three-case mini-arc
### B1 — tutorial: cut the bridge
A 5x5 open region has a one-cell neck connecting two lobes. Place one 1x1 occluder. Goal: exactly two open components; both must contain a marked node.

Human deduction: identify the articulation cell. Search space is only ~20 legal cells, but the causal lesson is immediate and visual.

### B2 — inversion/aha: make a hole without disconnecting the world
A 6x6 region contains a C-shaped pre-blocked wall. Place two 1x2 bars. Goal: open space remains one connected component **and** gains exactly one enclosed hole of area 1.

The player must stop thinking "block a bridge" and instead complete a ring while leaving global connectivity intact.

### B3 — mastery: two local cuts, one global escape
An 8x8 irregular region contains three chambers, two narrow necks, an almost-ring, and four named markers. Place exactly three pieces: two 1x2 bars and one 1x1 blocker. Final predicates:
- exactly two open components;
- markers A+B connected;
- marker C isolated from A/B but connected to D;
- exactly one enclosed hole of area 1;
- neither component may touch both north and south boundaries.

The winning reasoning requires identifying two articulation zones **and** noticing that completing the near-ring too early can create the hole while also severing the required A-B escape route.

## Search-space reality
On an 8x8 irregular board, a 1x2 bar has at most 112 axis-aligned placements and a 1x1 blocker at most 64. A naive ordered ceiling for two non-overlapping bars plus one blocker is under ~800k combinations; a realistic authored irregular board with legal masks reduces this substantially (typically tens to low hundreds of thousands) and is trivial for an offline certifier.

For the player, blind enumeration is unattractive because each attempt contains three placements and multiple simultaneous topological predicates. Human topology shortcuts prune aggressively:
- articulation points / one-cell necks predict component changes;
- near-rings predict hole creation;
- marker connectivity narrows which bottlenecks may be closed;
- boundary predicates eliminate entire regions without testing individual cells.

This is a genuine deduction advantage rather than a retry-speed advantage.

## Five+ content families without a new core verb
1. **Bridge severance** — create N components by closing articulation zones.
2. **Ring completion** — create exact hole count/size while preserving exterior connectivity.
3. **Marker partition** — force named markers into specified same/different components.
4. **Boundary topology** — components must touch/avoid specific board edges.
5. **Area-band components** — each remaining region must fall inside public size bands.
6. **False bottleneck** — several apparent necks exist, but only one satisfies another predicate simultaneously.
7. **Coupled topology** — one placement both closes a bridge and completes/prevents a ring.

These are predicate recombinations over the same placement verb and same open-space analysis; they do not require switches, keys, movable actors or a growing polyomino library.

## Kill-gate result
**PASS.** Differentiation survives removal of the document/stamp theme. Content does not need to become generic polyomino placement if the placeable vocabulary stays tiny and challenge comes from predicates over remaining space.

## Portfolio separation
Distinct from #002 because no bureaucracy/reality semantics are mechanically relevant; distinct from #006 because adjacency is not rewired/traded; distinct from #009 because there is no folding/nesting/trim transformation. The active object is the topology of what remains empty.

**Round-B verdict: FINALIST.**

---

# 2. Wrong-Side Assembly — **KILL**

## Minimum grammar tested
Rooted tree; each edge can be normal/back-made; a back edge toggles front/back orientation of its entire descendant subtree; final node faces are public targets; optionally exactly K edges must be back-made.

## Three-case mini-arc
### B1 — tutorial
One branch must flip: choose the edge above it.

### B2 — inversion
Nested back-joints cancel, restoring a deeper branch while the ancestor remains reversed.

### B3 — mastery
A 12-node asymmetric tree contains three target subtrees, two forbidden joints and exactly four permitted flips. Final orientation pattern alternates across nested branches.

## Search-space reality
With 11 edges, unconstrained binary intervention is only `2^11 = 2048`; exactly four flips is `C(11,4) = 330`. Offline validation is excellent.

The destructive problem is human reasoning: every node orientation is simply the XOR/parity of flipped ancestor edges. Once a player understands that, the apparent assembly geometry contributes little. A target node whose parent target differs directly tells the player whether the connecting edge must be flipped. On a tree, the solution can be reconstructed top-down in linear time. Forbidden joints or exact-K constraints add bookkeeping, not a richer spatial law.

## Content-family attempt
Single subtree, nested cancellation, shared ancestor, forbidden joint, exact-K, partial targets, symmetric decoys. These look different visually but remain the same parity equation. To create deeper assembly reading would require adding connector compatibility, physical overlap, branch ordering or face-specific attachment rules — multiple new nouns and a new problem class.

## Kill-gate result
**FAIL.** Mastery reduces to obvious parity/XOR once learned; spatial/assembly presentation does not remain meaningfully causal.

**Round-B verdict: KILL.** Strong toy, insufficient full-game depth under current factory standards.

---

# 3. The Quiet Majority — **KILL**

## Minimum grammar tested
Fixed graph; each node has ON/OFF state; active nodes contribute their current state as a vote to a public neighborhood; silenced nodes contribute no vote but remain nodes and continue to update; all nodes update synchronously; ties preserve state; player silences exactly N nodes; horizon is 1–3 rounds.

## Three-case mini-arc
### B1 — tutorial
Six-node line, silence one hub-equivalent voter so a central tie preserves ON.

### B2 — inversion
Eight-node ring, silence two nodes; the desired round-2 state depends on deliberately preserving a round-1 tie rather than immediately creating a majority.

### B3 — mastery
Twelve-node asymmetric graph, choose exactly three silenced nodes, public target pattern at round 3 plus two protected nodes that must never change during the trace.

## Search-space reality
Mastery intervention count is `C(12,3) = 220`; even 14 choose 4 is only 1001. That is ideal for certification but dangerous for play.

The human must forecast synchronous local majorities over two or three rounds. A single changed vote can alter several round-1 states, which then alter several round-2 votes. The useful causal cone expands quickly. By round 3, showing enough trace information to make reasoning comfortable starts to resemble a simulation debugger.

Meanwhile blind retries are cheap: choose 3 of 12, run a sub-second animation, compare target, repeat. The design can slow retries or hide feedback, but those are punitive patches rather than depth. Raising graph size worsens readability before it meaningfully fixes enumeration.

## Content-family attempt
Immediate majority, tie preservation, delayed cascade, hub suppression, protected state, exact ON count, target pattern, asymmetric neighborhoods. Variety exists, but the mastery burden shifts toward multi-round state tracing rather than a compact visual deduction shortcut.

## Kill-gate result
**FAIL.** At the mastery scale, the design violates the specific gate: causal reasoning is not reliably cheaper than subset brute force, and three rounds are already near the readability ceiling. More than three rounds would be worse.

**Round-B verdict: KILL.**

---

# 4. One Bad Ruler — **KILL**

## Minimum grammar tested
Sequential measurement operations; each measurement starts from the previous cut; a bad ruler has one missing tick and snaps a requested distance to the next available tick; exactly one operation uses the bad ruler; final cut/landmark silhouette is the target.

## Three-case mini-arc
### B1 — tutorial
Three requested lengths; choose the one operation whose +1 snap produces the final marks.

### B2 — inversion
Four cuts and two landmarks; using the bad ruler early shifts a later notch into alignment while a later bad use cannot.

### B3 — mastery attempt
Seven requested lengths with three judged landmarks and a final length band. To make the choice nontrivial, the case must either use more than one missing-tick behavior, allow alternative measurement origins, or combine different ruler defects.

## Search-space reality
With exactly one bad use among seven operations, there are only 7 interventions. Even 12 operations gives only 12. Blind testing is essentially the solution method unless each evaluation is made artificially slow.

Keeping one ruler and one known missing tick means every intervention simply adds the same offset from one point onward. The human shortcut is "find where the cumulative offset should begin" — good for a handful of levels, not a campaign.

## Content-family attempt
Early vs late shift, align a landmark, avoid a landmark, exact final length, several judged cuts. These are target variations on the same cumulative-offset equation. Real depth immediately asks for multiple rulers, multiple missing ticks, alternate origins, unit scales or tolerance bands — exactly the arithmetic/mechanic creep prohibited by the gate.

## Kill-gate result
**FAIL.** Depth requires multiple ruler behaviors and extra numeric annotation; otherwise search is tiny and repetitive.

**Round-B verdict: KILL.**

---

# 5. Ink Bleed — **FINALIST, RULE REPAIR REQUIRED**

Round A exposed an important underspecification: if a drop instantly flood-fills its entire ordinary connected dry component, the first drop often consumes everything and later drops have no interesting job. The candidate only survives if the history-dependent barrier law is made mechanically exact without feature creep.

## Minimum repaired grammar
1. finite orthogonal absorbent grid with blocked cells;
2. 2–4 colored drops placed sequentially on public legal source cells;
3. each drop spreads through dry cardinal neighbors for a **public finite absorption depth P** (normally 2–4 wavefront pulses, fixed per case); no color-specific terrain rules;
4. cells wetted by an earlier drop are permanently impermeable to later drops;
5. a new drop may start only on a dry legal source cell;
6. objectives inspect final ownership, protected dry cells, component connectivity of a color, and exact/area-band counts.

The only substantive repair versus Round A is finite absorption depth. This is one shared rule noun, not a collection of color powers.

## Three-case mini-arc
### B1 — tutorial: first wet wall
A 5x5 corridor map, P=2, red then blue from two selectable source pads. Goal: blue reaches a marked pocket. Red must be placed so its two-pulse diamond wets a choke cell, forcing blue around the other branch rather than occupying the direct corridor.

### B2 — inversion/aha: spend territory to create a future corridor
A 6x6 fork, P=3, three drops. Goal: green must occupy two target cells while red owns fewer than six cells. A seemingly weak early red placement is correct because its wet frontier blocks blue from sealing the only dry route green can later use.

### B3 — mastery: barrier chain
An 8x7 irregular substrate, P=3, four ordered drops with 5–7 legal source pads each. Goals simultaneously require:
- two exact-color target cells;
- one protected cell must remain dry;
- yellow final area 7–9;
- green final cells form exactly two components.

The solution requires reading successive dry-space cuts: drop 1 creates a wall for drop 2; drop 2 leaves a deliberate dry aperture; drop 3 closes a different choke; drop 4 exploits the surviving pocket. Solving by "largest territory" heuristics fails.

## Search-space reality
If four ordered colors each choose from 7 distinct legal source pads, naive source assignment is at most `7*6*5*4 = 840` before legality pruning. If order is also selectable for four colors, ceiling is 20,160, but authored cases should normally fix either order or sources rather than maximize both dimensions simultaneously.

Offline certification is trivial: each candidate solution runs at most a few pulses over <100 cells.

Human deduction can beat blind retries when objectives expose choke structure:
- Manhattan/P-step reach shows which cells a drop can possibly wet;
- earlier wet frontiers permanently remove cells from later reachability;
- protected-dry cells eliminate entire source regions;
- component goals force deliberate apertures/barriers rather than territory maximization.

Blind testing 840–20k animated four-drop sequences is substantially less attractive than tracing two or three critical choke cells.

## Five+ content families without a new core verb
1. **Choke denial** — wet one critical cell so a later color cannot cross.
2. **Dry aperture preservation** — deliberately stop an early frontier short of a future route.
3. **Protected dry island** — sequence barriers so a marked cell is never wetted.
4. **Exact-area / area-band ownership** — shape a frontier through prior barriers.
5. **Color component count** — force a later drop into separated reachable pockets.
6. **Barrier chain** — drop A shapes B, which shapes C.
7. **Source-choice vs order-choice** — use the same simulation with one dimension fixed and the other open.

No pumps, portals, color powers, moving actors or procedural fluids are required.

## Kill-gate result
**PASS, conditional on the repaired finite-depth law.** The mastery examples fundamentally exploit wet-history barriers. Ordinary Flood-It reasoning (grow/recolor the largest connected territory) is insufficient.

## Market separation
Color-spread games are common, so presentation must make the *sequence of impermeable historical frontiers* the hook. `INK` uses paint to reveal invisible platform geometry; `Paint by Cubes` is movement-to-paint with special fields; ordinary flood-fill games recolor/expand a current region. None of those retrieved analogues uses earlier color ownership primarily as immutable walls for later finite wavefronts.

## Portfolio separation
Distinct from #001 post-commit ecology, #003 property transfer, #005 conserved networks, #006 topology trade and #011 program deletion. The causal state is irreversible substrate wet-history.

**Round-B verdict: FINALIST.**

---

# 6. Spare Chair — **KILL**

## Minimum grammar tested
Fixed seat layout; people arrive in public order; each person has a visible ranked list of up to three preferred available chairs; they take the highest available option, otherwise remain standing; player removes exactly N chairs before seating; goals concern final adjacency/separation/standing relations.

## Three-case mini-arc
### B1 — tutorial
Four chairs, three people, remove one chair. The removal redirects P1, consuming P2's first choice and cascading P2/P3.

### B2 — inversion
Six chairs, five people. Goal requires deliberately making an early person take their second choice so a later person retains the only seat satisfying a friend-adjacency goal.

### B3 — mastery
Nine chairs, seven people, remove two. Preference lists are capped at three visible chairs/person. Simultaneous goals: two friends adjacent, one rival pair separated, one named person seated, another not in an aisle seat.

## Search-space reality
Mastery remove-two space is only `C(9,2)=36`; even 14 chairs remove 3 is 364. The human can reason through the greedy chain, but blind testing is cheap.

More importantly, the 2025 hit **Is This Seat Taken?** already owns the immediately legible commercial surface of quirky people + seats + preferences + adjacency. Our greedy arrival/removal law is mechanically different, but store capsule, screenshots and first trailer seconds would need to work hard to communicate that distinction. Retheming away from seats would remove the strongest physical metaphor.

## Content-family attempt
Cascade displacement, reserve a seat, force standing, friend adjacency, rival separation, seat-type constraint, empty-gap target. These remain viable under three-choice lists, so the preference-list kill gate itself is not the failure.

## Kill-gate result
Preference-list gate: **PASS** — three choices/person is enough for the tested mastery. Commercial differentiation gate: **FAIL**. Combined with only 36–364 interventions and fast deterministic resolution, the candidate is weaker than the two finalists.

**Round-B verdict: KILL.**

---

# Round-B decision

## Finalists retained for Round C
1. **Negative Space Clerk** *(candidate label only)* — strongest pure deduction/topology concept; extremely compact implementation; human structural shortcuts scale better than blind retry; requires retheme and likely a new title.
2. **Ink Bleed** *(candidate label only)* — strongest animated causal hook; repaired finite-depth wavefront produces genuine history-dependent barrier reasoning; higher simulation/UX burden than Negative Space Clerk but stronger trailer motion.

## Round-B kills
- **Wrong-Side Assembly** — mastery collapses to tree parity/XOR; assembly geometry is mostly presentation.
- **The Quiet Majority** — 2–3 round causal tracing becomes harder than cheap subset brute force; readability ceiling reached too early.
- **One Bad Ruler** — one-defect search space is tiny; depth demands prohibited arithmetic/ruler proliferation.
- **Spare Chair** — mechanically workable but commercially collides with the already-successful seating-preference lane and remains easy to enumerate.

## Why only two finalists
Keeping a third candidate for symmetry would weaken the tournament. Negative Space Clerk and Ink Bleed are the only survivors whose mastery proof simultaneously preserves:
- one compact causal law;
- at least five content families;
- deterministic exact certification;
- a human deduction shortcut materially better than blind retries;
- portfolio separation;
- plausible 30+ case content without mechanic proliferation.

# NEXT ROUND — ROUND C
Run a head-to-head final between **Negative Space Clerk** and **Ink Bleed**.

For each finalist:
1. build a 10–15 minute four-case mini-campaign using only its Round-B grammar;
2. include onboarding, first inversion, midgame composition and mastery;
3. specify exact candidate solution spaces and construct at least one case with a unique certified solution or a deliberately bounded small equivalence class;
4. test whether case 4 still creates a new deduction pattern rather than merely a larger board;
5. estimate 30–45 case campaign architecture, tutorial burden, content-authoring burden, solver/certifier complexity, controller/Deck interaction and screenshot/trailer clarity;
6. perform a final fresh market/name collision check;
7. select **one winner** only if it clearly survives the full mini-campaign.

If a winner survives, continue safely in the same run into **Phase 3 Product Thesis**: lock target player/platform, genre framing, one-sentence hook, core fantasy, session structure, core loop, differentiator and scope ceiling. Do not freeze Phase-4 mechanics during Phase 3.
