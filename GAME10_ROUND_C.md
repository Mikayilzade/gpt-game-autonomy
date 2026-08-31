# GAME #010 — CONCEPT TOURNAMENT ROUND C

Date: 2026-08-31
Status: COMPLETE — 3 -> 1
Final concept selected: **LUGGAGE CAROUSEL ZERO**

Authority: `START_HERE.md` -> `STATUS.md` -> `GAME_INDEX.md` -> `GAME10_RESEARCH.md` -> `GAME10_TOURNAMENT.md` -> `GAME10_ROUND_B.md` -> this file.

Round C compares the finalists as sellable, playable products. No rescue mechanics are admitted. Previous games #001–#009 remain exclusion/portfolio history only.

## Fresh market check — 2026-08-31
Current evidence changes the comparative risk profile.

- Inventory-management/backpack games are visibly crowded. `Outpacked` released 2026-04-01 as a pure luggage packing logic puzzle with 61 levels, editor and Workshop; `Backpack Raiders` released 2026-06-03 as a tactical inventory-builder hybrid; `Backpack Dungeon` released 2026-07-14; `Backpack Alchemist` and `Blackbriar Crypt` also market grid inventory as a core mechanic. The lane is viable but no longer visually novel by itself.
  - https://steamdb.info/app/4012320/info/
  - https://steamdb.info/app/1880100/info/
  - https://weloveit.io/game/4478640/
  - https://steamdb.info/app/4534730/info/
  - https://store.steampowered.com/app/4917350/Blackbriar_Crypt/
- `3D Life` released 2026-05-21 around cellular automata and `FUNG` openly markets living-pixel / cellular-automata play. Stencil Orchard is mechanically different, but a cellular-grid presentation needs strong framing to avoid looking like another abstract CA toy.
  - https://store.steampowered.com/app/1089890/3D_Life/
  - https://mellow.games/fung
- Airport/baggage is not empty: `Airport Baggage Simulator` released 2026-05-28 and is about inspection/sorting/automation. However its first-person management structure is materially different from the finite moving-permutation puzzle proposed here. Search also surfaced casual luggage-sorting games, but no close analogue to fixed socket labels + moving bags + public passenger predicates + deliberate non-service.
  - https://store.steampowered.com/app/3887090/Airport_Baggage_Simulator/

Market implication: theme alone is not a moat for any finalist. Inventory Eclipse suffers the highest immediate screenshot-category collision. Luggage Carousel Zero keeps a distinct decision structure if the carousel permutation, socket-owned labels and passenger queue are unmistakable in the first image.

---

# C1 — STENCIL ORCHARD

## Product simulation
### First 20 minutes
Minute 0–3: player sees a 1x3 bed `[0,1,0]`, one bar stencil and target `[1,1,1]`. Drag stencil over middle, preview says HOLD there / ADVANCE elsewhere, Commit. Immediate comprehension is excellent.

Minute 3–8: two-step problem `[1,0,0] -> [1,2,2]`; player learns a correct cell may need protection repeatedly. This is the first genuine planning beat.

Minute 8–13: 3x3 board, L stencil, target regions rather than exact full bitmap. Player rotates the stencil to keep a mature corner cluster while advancing a strip. Strong tactile/visual loop.

Minute 13–20: two target windows share cells; player must schedule protection across two Steps. A failed sequence is explainable by highlighting the first cell that became too old to recover.

Verdict at 20 min: excellent puzzle demo. It communicates faster than the other finalists.

### Hour 2
The player now recognizes recurring reasoning: (a) protect already-correct cells, (b) expose lagging cells, (c) find one stencil placement satisfying several phase groups, (d) schedule the same geometric coverage over several steps. Difficulty rises through mask geometry and target overlap.

The danger becomes visible: many cases reduce to comparing `needed age delta` against `number of future exposures`, then finding a stencil placement matching those exposure counts. The geometry matters, but the mental sentence is often the same.

### Hour 8
Without new species, propagation rules, death rules or stencil consumability, expert problems mostly intensify four existing reasoning families. Larger boards increase bookkeeping faster than conceptual novelty. The concept remains good, but its long-tail content burden is higher than Round-A scoring suggested: authoring must continuously find masks/targets that produce qualitatively different coverage scheduling rather than merely harder exact-cover arithmetic.

## 12 content-case skeletons, clustered
A. **Protect-correct**
1. One mature island held while background catches up.
2. Two disconnected mature islands protected by one perforated stencil.
3. Correct region must be protected across three consecutive Steps.

B. **Catch-up scheduling**
4. Two age bands need different exposure counts.
5. One stencil rotation catches two lagging bands in alternating Steps.
6. A target window has only lower/upper age bounds, requiring minimal exposure rather than exact painting.

C. **Competing windows**
7. Overlapping windows want different cells preserved.
8. One placement helps window A now but makes B impossible next Step.
9. Several legal first moves exist but only one preserves future coverage geometry.

D. **Mask geometry reasoning**
10. Hole alignment protects disconnected cells while exposing center.
11. Rotation parity matters over a rectangular board edge.
12. Two stencil shapes can produce the same immediate state but different future anchor accessibility only if placement legality depends on bounds; this is weaker because state itself does not remember placement.

Repetition finding: clusters A–C are healthy but tightly related. Skeleton 12 exposes a limit: because only resulting COVERED bitsets matter and placement has no persistent state, many geometric stories canonicalize to the same exposure schedule.

## Authored-content burden
Credible premium target: about 45–60 strong puzzles to sustain several hours without rule additions, plus 6–8 demo cases. Solver can generate candidates, but human curation must aggressively deduplicate reasoning skeletons. Content burden: **medium-high** despite low code burden.

## Dominant-strategy attack
Heuristic 1: compute each cell's needed exposures and solve stencil coverage as exact cover. This is not always a trivial solution, but at expert level it becomes a powerful meta-representation that can drain the garden fantasy.

Heuristic 2: always protect maximum number of already-correct cells. Counterexamples exist because lagging/correct groups can conflict, so this does not solve the game.

Heuristic 3: work backward from final exposure counts. This is effectively the intended expert method. That is acceptable, but it confirms the game trends toward discrete scheduling arithmetic.

## Storefront proof
Screenshot: bright age-coded orchard grid, oversized cutout stencil hovering, target flower silhouettes at side. Legible but risks reading as generic grid puzzle before motion is seen.

10-second GIF: place stencil -> covered cells remain -> exposed cells bloom one age -> target window completes. Excellent.

Sentence: **“Shape time with reusable stencils: every uncovered plant grows, every covered plant waits.”** Excellent legibility.

## Controller / 1280x800 / accessibility
Best of field. Cursor snap, rotate, preview, Commit. Color cannot be sole age channel; use bud/leaf/flower silhouettes + numbers/icons. Low motion requirements. Strong handheld product.

## Solver / validator / empirical gates
Simplest exact solver. Key empirical gate: can 30+ strong cases be produced without reasoning duplication? A content prototype must classify solution traces by exposure-count signature and stencil-bitset sequence to quantify sameness.

## Round-C verdict
**SECOND PLACE.** Exceptional compact design and safest implementation. It loses because long-tail reasoning appears narrower than Luggage Carousel Zero under the no-new-mechanics constraint.

---

# C2 — LUGGAGE CAROUSEL ZERO

## Product simulation
### First 20 minutes
Minute 0–3: three fixed sockets on a belt, each with a large colored overhead label. Three bags move one socket when ADVANCE is pressed. One passenger at pickup wants RED. Player swaps RED onto the socket the right bag will occupy after movement. Advance: belt moves, bag arrives, passenger takes it. The distinction between moving bag and fixed socket label is visible in one cycle.

Minute 3–7: passenger wants RED + SQUARE. Bag shape stays with bag; RED stays with socket. Player must line up a bag trait and spatial label at pickup. This establishes the two-layer identity.

Minute 7–12: two passengers. Serving P1 immediately consumes a bag P2 uniquely needs. Player deliberately allows a non-match for one tick. This creates the first memorable anti-greedy story: **not serving someone is a move** even though the only editing verb is label swapping.

Minute 12–16: first gap. After pickup, the empty socket keeps circulating; there is no compression. Player predicts a moving permutation rather than a queue.

Minute 16–20: four-to-five sockets, two label swaps over two ticks, overlapping predicates. Player solves by thinking about where labels must be when specific bags reach pickup, not by matching colors locally. Demo ends with an intentional one-passenger delay that enables two later services.

Verdict at 20 min: slightly slower to explain than Stencil Orchard, but stronger emergent story and clearer “I caused that future” payoff.

### Hour 2
Cases now vary through the SAME vocabulary:
- unique vs substitutable bags;
- overlapping passenger predicates;
- multiple copies of labels;
- circulating gaps;
- finite tick budgets;
- one vs two swaps before a tick;
- intentional misses;
- preserving one bag for a later passenger;
- using a gap as a phase spacer.

The player starts reasoning backward from future pickup phases and forward from current gaps. Crucially, the state is animated and narratively interpretable: “I must let the round red bag pass so the square one takes Blue next loop.”

### Hour 8
Expert cases still use bag permutation + fixed label permutation + public queue. New difficulty can come from interaction density rather than new rules. A bag may satisfy several passengers, so serving it now changes the feasible matching structure later. Gaps alter arrival phase. Duplicate labels create routing flexibility that can be spent too early. One swap can repair one passenger while damaging another future phase.

The game develops three simultaneous planning layers: **which bag should be consumed**, **when it should reach pickup**, and **which socket label it should inherit at that moment**. Those layers recombine naturally and remain explainable.

## 12 content-case skeletons, clustered
A. **Alignment fundamentals**
1. Put required label under one known bag at pickup.
2. Combine bag trait + socket label.
3. Choose between two matching bags, only one preserves a future passenger.

B. **Intentional delay / queue coupling**
4. Front passenger can be served now, but must wait one loop for P2 survival.
5. Front passenger has two valid labels; choose the non-obvious one to preserve the scarce label phase.
6. Two consecutive passengers want overlapping bag traits; consumption order matters.

C. **Gap-phase reasoning**
7. Pickup creates a gap that returns as a timing spacer.
8. Two gaps make identical bag order but different phase relative to duplicated labels.
9. A passenger must intentionally miss because the needed bag arrives at pickup under wrong label; shifting labels early causes a later dead end.

D. **Swap-budget reasoning**
10. One swap/tick forces planning two ticks ahead; immediate repair is impossible.
11. Two swaps are allowed once, but spending both now prevents maintaining two future label phases.
12. Several bags are predicate-equivalent for current passenger but symmetry breaks because only one sits in the correct future phase for P3.

Repetition finding: the clusters correspond to distinct reasoning objects — matching, consumption scheduling, moving-gap phase, and edit-budget planning — despite no new subsystem. This is the strongest diversity of the three finalists.

## Authored-content burden
Credible premium target: **36–48 certified strong cases**, because each case can have richer state than a Stencil puzzle and should take longer. Demo: 6–8 cases. A solver can enumerate and score candidate instances for forced waiting, opening alternatives, consumption dependency, gap significance and solution length. Human authoring remains necessary for visual clarity and avoiding predicate overload. Burden: **medium**.

## Dominant-strategy attack
Heuristic 1: serve front passenger as soon as possible. Explicitly broken by scarce-bag preservation.

Heuristic 2: always place the needed label at pickup. Wrong because labels are socket-owned and future bags inherit them; useful labels may need to be staged away from pickup before movement.

Heuristic 3: assign each passenger a unique best bag greedily, then route. Broken by bag substitutability and future phase; a locally second-best bag can be globally necessary.

Heuristic 4: work backward from final passenger only. Insufficient because earlier removals create gaps that change phase.

No single dominant representation collapses all layers. A full solver is useful, but human expert reasoning still involves qualitative stories rather than only arithmetic.

## Storefront proof
Screenshot: circular/oval belt with 6 bright fixed socket labels, distinct suitcase silhouettes orbiting, one pickup gate, three passenger predicate cards visible as a short queue. Risk: if label ownership is unclear, it looks like ordinary sorting. Mitigation is mandatory art language: labels are large fixed overhead gantries physically bolted to sockets; bags visibly pass beneath them.

10-second GIF: swap two overhead labels -> press ADVANCE -> all bags move -> wrong-looking bag intentionally passes passenger -> next passenger later receives rare bag under preserved label. Excellent motion and causality if edited around one two-step consequence.

Sentence: **“Swap the labels, not the luggage: shape a moving baggage carousel so every passenger gets the right bag — sometimes by making them wait.”** Strong, differentiated and truthful.

## Controller / 1280x800 / accessibility
Strong. <=8 sockets core. D-pad/stick snaps socket focus; select label A, select label B, swap; shoulder or face button previews/advances. Passenger cards must use icons + text, not colors alone. Belt can pause indefinitely; animation speed adjustable/reduced-motion instant-step mode. Preview ghosts next bag positions without solving predicate outcome beyond visible clause highlighting. Cognitive load is higher than Stencil but still one-screen.

## Solver / validator / empirical gates
Finite exact search is straightforward at intended bounds, but stronger than Stencil in content metrics. State = bag permutation including gaps + fixed label permutation + passenger index + ticks + remaining swaps. Symmetry canonicalizes trait-identical bags and duplicate labels where sockets are otherwise equivalent.

Certification metrics should include:
- solvable within budget;
- shortest solution length;
- number of viable first moves;
- whether at least one intentional passenger miss is required for advanced cases;
- whether a removal-created gap changes solution feasibility;
- whether at least one bag has >1 candidate passenger or vice versa;
- maximum predicate clauses shown at once;
- trace dedupe by served-bag sequence + label-phase sequence.

Empirical gates:
1. first-time players understand **labels belong to sockets, bags move** within first two cases;
2. a 6–8 socket expert case remains readable at 1280x800 without tooltips covering the ring;
3. intentional waiting feels clever rather than like arbitrary stalling;
4. carousel animation communicates simultaneous movement and non-compressing gaps perfectly.

## Round-C verdict
**WINNER.** Best combination of product identity, same-vocabulary hour-8 depth, solver-certifiable content, low implementation risk, animated causal readability and market differentiation.

---

# C3 — INVENTORY ECLIPSE

## Product simulation
### First 20 minutes
Minute 0–4: player moves a Shade in a 1x4 pack; its shadow uncovers Crowbar, which phases active; nearby compact-world gate lights up. Strongest single GIF in the field.

Minute 4–8: next gate requires Magnet INACTIVE. Player learns absence is a target state rather than merely lack of access.

Minute 8–14: Rope must remain ACTIVE across two nodes while Magnet stays INACTIVE; repacking only at marked safe point. The world requirement strip begins to matter.

Minute 14–20: orientation-dependent shadow, two simultaneous capabilities. Strong puzzle, but UI now has pack grid, item footprints, shadow overlay, active states and world node requirements competing for attention.

### Hour 2
Good cases require capability schedules across repack boundaries. However authoring repeatedly asks for new world effects or item transformations to make the compact world feel meaningful. If those are held to the strict Round-B vocabulary, the world tends toward a requirement graph whose main function is to ask for active-bit vectors.

### Hour 8
The strongest formal structure is still precompute pack arrangements -> active/inactive bit vectors -> choose arrangements satisfying node sequence. This is deep enough, but the player can increasingly perceive the world as a wrapper around inventory-state SAT. Adding richer physical world interactions would improve fantasy but violates the no-rescue-mechanics test and raises implementation scope.

## 12 content-case skeletons, clustered
A. Single capability toggles
1. Activate one tool.
2. Inactivate harmful tool.
3. Rotate shade to switch which of two tools is active.

B. Simultaneous state vectors
4. Rope+Lamp active / Magnet inactive.
5. Two tools share threatened activation cells.
6. One shade movement toggles three items, requiring exact vector.

C. Commitment across repack points
7. Two nodes, no repack, same vector must satisfy both.
8. First node changes one footprint, second needs resulting vector.
9. Choose between two legal first arrangements; only one remains transform-compatible.

D. Route / acquisition interaction
10. Branch chooses which deterministic item transform is earned first.
11. Optional node requires sacrificing current capability to unlock later geometry.
12. Return to prior requirement after footprint transform, needing a new arrangement.

Repetition finding: D depends heavily on node transforms/unlocks, which are content-specific rule data and can creep toward a subsystem zoo. Without D, most puzzles are active-bit packing plus repack scarcity.

## Authored-content burden
Premium credibility likely needs 30–40 major puzzles/nodesets plus bespoke item silhouettes, world affordance art and carefully curated transforms. Demo 5–7 sequences. Code burden is medium; UX burden medium-high; content burden medium-high.

## Dominant-strategy attack
A solver can precompute all legal pack arrangements and their active vectors. Human players may do a lighter version mentally. This is fine, but once enough items exist, experimentation can become exhaustive packing search.

The design counters “cover unused tools” through harmful-active requirements, but cannot fully escape packing optimization because arrangement is the only real player edit surface.

## Storefront proof
Screenshot: visually attractive pack with sweeping shadows plus compact world strip, but current 2026 market has many grid-inventory games. A still image risks immediate categorization as another Backpack Hero/Outpacked-like inventory puzzler even though shadow activation is novel.

10-second GIF: strongest of all three — move shade, tool phases out, world gate changes. Excellent.

Sentence: **“Repack your tools to cast inventory shadows: what you cover disappears from the world, and sometimes that is exactly what you need.”** Excellent.

## Controller / 1280x800 / accessibility
Grid movement is safe, but split attention is real. Shadows require texture/outline, not translucency/color alone. Multiple overlapping shadows need source tracing. Focus mode may be required on handheld, adding presentation complexity.

## Solver / validator / empirical gates
Solver remains feasible if legal arrangements are precomputed, but deterministic node transforms enlarge state. Empirical gates include whether overlapping shadows remain readable and whether players perceive world transitions as gameplay rather than checklist gates.

## Market penalty
Fresh 2026 evidence makes this penalty material. Outpacked, Backpack Raiders, Backpack Dungeon, Backpack Alchemist and other inventory-first games mean the first screenshot must fight category saturation before the unique eclipse rule can be understood. That does not kill the design, but it removes the differentiation advantage it held in Round B.

## Round-C verdict
**THIRD PLACE.** Strong, marketable design and the best single animation, but higher UX/content scope and current inventory-lane crowding make it weaker than Luggage Carousel Zero for Game #010.

---

# FINAL COMPARISON

| Axis | Stencil Orchard | Luggage Carousel Zero | Inventory Eclipse |
|---|---:|---:|---:|
| 20-minute onboarding | 5 | 5 | 4 |
| Hour-8 same-vocabulary depth | 3.5 | **5** | 4 |
| 12-case reasoning diversity | 3.5 | **5** | 4 |
| Authored-content efficiency | 4 | **5** | 3.5 |
| Hook / GIF | 5 | 5 | **5** |
| Still-image differentiation | 4 | **5** | 3 |
| Controller / 1280x800 | **5** | 4.5 | 3.5 |
| Solver / certification safety | **5** | **5** | 4 |
| Implementation scope safety | **5** | **5** | 3.5 |
| Failure explainability | 5 | **5** | 4.5 |
| Current market collision risk | 4 | **5** | 2.5 |
| Product-story strength | 3.5 | **5** | 4.5 |

## Winner — LUGGAGE CAROUSEL ZERO
Game #010 selects **Luggage Carousel Zero** as its working concept.

Why it wins:
1. the minimal vocabulary creates several distinct expert reasoning types rather than one core calculation repeated at higher density;
2. moving bags + fixed socket labels + passenger consumption + persistent gaps create a mechanically distinctive permutation system;
3. deliberate non-service produces memorable player stories without adding a mechanic;
4. exact solver certification remains practical;
5. production scope is low-to-medium and one-screen;
6. current market evidence shows less direct structural crowding than the inventory finalist;
7. it has a credible demo, screenshot, GIF and one-sentence hook;
8. it does not collide with frozen portfolio identities #001–#009.

## Explicitly frozen Round-C exclusions
- **Stencil Orchard** is eliminated for Game #010, not “saved as a later mechanic.” Do not merge stencils/plant aging into the winner.
- **Inventory Eclipse** is eliminated for Game #010. Do not add pack grids, item shadows or active/inactive inventory states to the winner.
- The winner must remain about **moving permutation + fixed spatial labels + public passenger predicates + removal-created gaps + bounded label swaps**. Do not turn it into an airport-management sim, hidden-deduction game, real-time dexterity game or inventory game.

## Phase-3 handoff questions now answerable
The next authority should lock:
- PC/Steam-first premium single-player puzzle;
- working title and whether “Zero” remains internal;
- exact target audience and session length;
- product-scale content target;
- one-sentence hook and trailer promise;
- core loop and fail/win structure;
- scope ceiling and explicit non-goals;
- empirical gates inherited from Round C.

No production implementation has begun.