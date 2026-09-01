# GAME #012 — PHASE 2 ROUND C HEAD-TO-HEAD

Date: 2026-09-01
Status: **ROUND C COMPLETE — WINNER SELECTED**
Authority: final tournament decision for Game #012. Phase-4 rules are NOT frozen here.

## Decision
**Winner: Negative Space Clerk (mechanical label; title/theme are not final).**

Ink Bleed remains a valid toy and a possible future exclusion-history reference, but it is rejected for Game #012. Its best cases depend on mentally simulating several sequential wavefronts; the topology candidate instead lets players make deductions from stable, directly visible structures (articulation points, rings, marker partitions and boundary contacts) before committing placements. This is a stronger fit for the factory's controller-first, low-asset, systemic-puzzle goals.

---

## Fresh collision / market check — 2026-09-01

### Negative-space lane
Searches for a current Steam game centered on *placing blockers so predicates are evaluated over the connected topology of the remaining empty cells* did not surface a close commercial analogue. However, `Negative Space` is already the name of a 2025 Steam roguelike deckbuilder, and `NEGATIVE_SPACE` is also an unreleased puzzle-platformer. Therefore **Negative Space Clerk must not be treated as a shipping title**.

Relevant checks:
- https://store.steampowered.com/app/3624300/Negative_Space/ — `Negative Space`, released 2025-11-21, unrelated deckbuilder.
- https://store.steampowered.com/app/1017990/NEGATIVE_SPACE/ — coming-soon inversion puzzle-platformer.
- https://thinkygames.com/games/sudoku-topology/ — 3D Sudoku-on-topology, mechanically unrelated but evidence that topology language is understandable to dedicated puzzle audiences.
- `Hex` / Shannon switching are durable connection-game references, but they are adversarial path-connection games rather than authored void-topology placement puzzles.

### Ink lane
The current surface is noisier. `Spill The Ink` is already listed for February 2027 and uses drawn ink + physics as its visible hook; `Floating Ink VR` (2026-07-16) explicitly advertises wet-ink bleed simulation; `Cellchemist` (2026-02-13) markets pixel-level substance simulation. None shares Ink Bleed's exact historical-barrier rule, but screenshots/trailers would initially compete in a familiar "ink/liquid spreads" semantic lane and invite physics expectations the design intentionally does not satisfy.

Relevant checks:
- https://steamdb.info/app/4743960/ — `Spill The Ink`, currently listed for 2027.
- https://store.steampowered.com/app/4884570/Floating_Ink_VR/ — wet-ink bleed simulation.
- https://store.steampowered.com/app/4254360/Cellchemist/ — physics/pixel material puzzle sandbox.

Market conclusion: **neither candidate is killed by collision, but the topology candidate owns a cleaner mechanical sentence and avoids liquid-physics expectation debt.**

---

# FINALIST A — NEGATIVE SPACE CLERK

## Four-case 10–15 minute mini-campaign
All cases use only the Round-B vocabulary: finite orthogonal open region, fixed blocked cells, tiny opaque pieces, and final predicates over remaining open space. Coordinates below are 0-based `(x,y)`, origin upper-left. These are certifier witnesses, not final authored levels.

### C1 — Articulation lesson (2–3 min)
Board: 5x5. Preblocked cells `{(1,3),(1,4),(2,2),(2,3),(2,4)}`. Place exactly one 1x1 blocker. Markers `A=(1,1)`, `B=(0,4)`.

Target predicates:
- exactly 2 remaining-open components;
- A and B in different components;
- component areas 18 and 1;
- no enclosed hole.

Intervention space: **20 geometrically legal blocker cells; 18 remain legal after marker exclusion.**
Certified witness: blocker `(0,3)`.
Certificate result: **unique under the stated predicate tuple**.

Deduction learned: do not "fill space"; identify the articulation cell whose removal changes the topology of what remains.

### C2 — Hole inversion (2–3 min)
Board: compact 6x6 C/ring-shaped authored mask. Place two fixed-orientation 1x2 blockers. Goal keeps all remaining open cells connected while creating exactly one enclosed dry/void hole of area 1; both named markers must remain connected.

Authoring contract for final level: certifier enumerates every non-overlapping pair. With at most 30 legal placements per bar on the intended irregular mask, the exact pre-overlap assignment space is **30 x 30 = 900 ordered assignments**; because the two bars are visually/type-identical, shipping certification canonicalizes them as an unordered pair and records the exact legal-pair count in the level certificate.

The inversion is qualitative, not board inflation: the same opaque placement verb that previously *split* open space is now used to *close a loop without splitting the exterior*.

### C3 — Coupled predicates (3–4 min)
Board: 6x6. Preblocked `{(0,0),(0,1),(1,0),(1,1),(1,2),(2,0),(2,1),(3,1)}`. Place one horizontal 1x2 blocker plus one 1x1 blocker. Markers `A=(3,4)`, `B=(5,3)`, `C=(3,3)`.

Target predicates:
- exactly 2 open components;
- component areas 24 and 1;
- exactly one enclosed hole, area 2;
- A/B/C remain in the same component;
- the singleton component touches west only; large component touches all four boundaries.

Intervention space: **546 geometrically legal ordered piece assignments; 368 marker-safe assignments.**
Certified witness: horizontal bar `{(1,4),(2,4)}`, blocker `(0,3)`.
Certificate result: **unique under the full predicate tuple**.

New deduction pattern: the player must simultaneously recognize a near-ring and a sacrificial pocket. Solving either the hole or component objective alone points toward several false placements.

### C4 — Mastery: two cuts, one hole, one escape (4–5 min)
Board: 7x7. Preblocked boundary-connected wall `{(0,1),(0,2),(0,3),(0,4),(0,5),(1,1),(1,2),(1,3),(1,4),(2,3)}`. Place exactly one horizontal 1x2, one vertical 1x2, and one 1x1 blocker. Markers `A=(5,2)`, `B=(2,2)`, `C=(3,5)`, `D=(4,3)`.

Target predicate tuple:
- exactly 3 remaining-open components;
- component areas `(1,4,29)`;
- exactly one enclosed hole of area 1;
- marker partition: A/C/D together, B separate;
- boundary-contact multiset: one component touches north only, one touches north+west, one touches all four boundaries.

Intervention space: **29,085 geometrically legal ordered assignments; 15,221 marker-safe assignments.**
Certified witness:
- horizontal bar `{(1,0),(2,0)}`;
- vertical bar `{(4,0),(4,1)}`;
- 1x1 blocker `(3,2)`.

Exhaustive enumeration result: **exactly one assignment satisfies the full tuple**.

Mastery novelty proof: this is not merely a larger articulation puzzle. The first two pieces alter which apparent bottlenecks are real after the third placement, while the hole and marker partition constrain different portions of the board. The useful human method is a layered invariant proof: (1) preserve A/C/D route, (2) force B's separation through a permissible cut, (3) satisfy boundary signatures, then (4) close the single-cell hole. This prunes thousands of placements without trial animation.

## 30–45 case campaign estimate
A compact full campaign is credible at **36 target cases / 30 quality floor**, organized around six same-vocabulary families:
1. articulation cuts;
2. ring/hole completion;
3. marker partitions;
4. boundary-contact signatures;
5. area-band components;
6. coupled topology / false bottlenecks.

Suggested six acts of 6 cases each, with predicates recombined rather than one new mechanic per act. The late game should increase *constraint coupling* more than board size. Recommended board ceiling for normal play: roughly 9x9; piece count normally 1–4.

Tutorial burden: low. "Place blockers; only the shape of what remains open is scored" plus graphical icons for components, holes and marker relationships.

Authoring burden: moderate-low. Designers need irregular masks and target tuples, but the offline certifier can enumerate small piece vocabularies and reject non-unique/degenerate cases.

Certifier complexity: low. Grid flood-fill, component areas, exterior flood-fill for holes, marker-component IDs and boundary flags; finite enumeration of piece placements.

Controller / Steam Deck: strong. D-pad/stick cursor, shoulder buttons cycle piece types/instances, A place, B undo, Y predicate overlay. No pixel precision, drag requirement or long text.

Screenshot/trailer legibility: strong if the remaining open regions are visually emphasized after placement. A 5-second clip can show one blocker dropping, a formerly connected void splitting into two tinted regions, and objective icons resolving.

Replay/repetition risk: medium but controllable. The danger is "find the neck" repetition. Countermeasure is not new mechanics: ensure at least half of mid/late cases require two or more predicate classes whose locally obvious moves conflict.

**Round-C verdict: PASS / WINNER.**

---

# FINALIST B — INK BLEED

## Four-case 10–15 minute mini-campaign
All cases retain the repaired Round-B law: public fixed pulse depth P; ordered drops; a drop spreads through currently dry orthogonal cells up to P pulses; previously wet cells permanently block later colors.

### C1 — First barrier (2 min)
5x5 corridor substrate, P=2, red then blue, 4 legal pads. Goal: blue owns one target beyond a fork.
Intervention space with distinct sources: **P(4,2)=12 ordered source assignments**.
The useful move is placing red so its frontier closes one branch and leaves the other dry.

### C2 — Protected dry cell (2–3 min)
6x5 irregular substrate, P=2, red/blue/green, 5 legal pads. One marked cell must remain dry and green must own two targets.
Intervention space: **P(5,3)=60 assignments** before dynamic source-invalidity pruning.
Inversion: territory acquisition is sometimes bad; early colors are barrier material.

### C3 — Aperture chain (3–4 min)
7x6 irregular substrate, P=2, four fixed-order colors, 6 legal pads. Goal combines one protected dry cell, one exact-color target and a late-color area band.
Intervention space: **P(6,4)=360 assignments** before source-invalidity pruning.
The new reasoning pattern is a two-stage aperture: color 1 shapes color 2, and color 2 must stop short so color 4 retains a route.

### C4 — Certified mastery (4–5 min)
7x6 board, blocked cells `{(0,0),(0,2),(1,0),(3,1),(4,4),(5,3),(6,1)}`, P=2. Legal source pads:
`[(4,5),(2,0),(4,3),(3,0),(3,5),(6,4),(0,3)]`.
Fixed color order `R,G,B,Y`.

Target predicates:
- cell `(2,4)` is Green;
- cell `(4,0)` remains dry;
- Yellow final area is exactly 6.

Raw assignment space: **P(7,4)=840** distinct ordered pad assignments.
After rejecting assignments in which a later source was already wetted before its turn, **384 dynamically valid assignments remain**.
Certified witness sources: `R=(4,3), G=(3,5), B=(6,4), Y=(0,3)`.
Exhaustive result: **exactly one dynamically valid assignment satisfies all three target predicates**.

Mastery novelty proof: the target requires a historical barrier chain, not simply a larger flood. Nevertheless, the reasoning object is a four-step simulated trace; the player cannot inspect the final topology directly until earlier wavefronts are mentally or interactively propagated.

## 30–45 case campaign estimate
A 36-case campaign is technically possible across choke denial, dry apertures, protected cells, area bands, component goals, barrier chains and fixed-order/source variants.

Tutorial burden: medium. Pulse radius, blocking by prior wet cells, invalid future sources and ordered history all need explicit visualization.

Authoring burden: moderate. Certifier is easy, but good cases require avoiding accidental source invalidation and visually inscrutable overlapping wavefronts.

Certifier complexity: low-medium. BFS/wavefront simulation per candidate, dynamic validity checks, then target evaluation.

Controller / Steam Deck: strong mechanically, but source-pad selection is less of an issue than trace comprehension on a small screen. Preview overlays risk becoming either noisy or an oracle.

Screenshot/trailer legibility: high spectacle, medium rule legibility. Ink spreading looks good; communicating *why earlier wet cells block later spread* needs a sequence, not a still screenshot.

Replay/repetition risk: medium-high. Barrier chains are real depth, but repeated four-drop forecasting can become execution/trace labor. Increasing P or board size worsens this faster than it improves deduction.

**Round-C verdict: REJECT FOR GAME #012.** Good mechanical seed, weaker full-game fit than the winner.

---

# Head-to-head score after actual mini-campaigns

| Criterion | Negative Space Clerk | Ink Bleed |
|---|---:|---:|
| 10-second causal hook | 5 | 5 |
| Still-image legibility | 5 | 3 |
| Human deduction advantage | 5 | 3 |
| Same-vocabulary depth | 5 | 4 |
| 30–45 case confidence | 4 | 4 |
| Tutorial burden | 5 | 3 |
| Authoring/certification | 5 | 4 |
| Controller/Deck clarity | 5 | 4 |
| Trailer spectacle | 4 | 5 |
| Repetition resilience | 4 | 3 |
| Market/surface distinctness | 5 | 3 |
| Production scope safety | 5 | 4 |
| **Total / 60** | **57** | **45** |

## Final selection rationale
The winner is not selected because its pitch is cleaner. It wins because a real mastery witness leaves **15,221 legal candidate assignments** yet supports direct topological pruning and a unique certificate, while the Ink mastery witness leaves only **384 dynamically valid assignments** and asks the player to forecast a four-stage simulation to obtain equivalent certainty.

**GAME #012 SELECTED CONCEPT = Negative Space Clerk mechanical core.**

Title/theme remain intentionally open. Phase 3 must retheme away from literal office paperwork and must not ship under `Negative Space` because of existing title collisions.
