# GAME #011 — PHASE 2 CONCEPT TOURNAMENT — ROUND B

Date: 2026-09-01
Status: ROUND B COMPLETE — 5 -> 3
Authority: `START_HERE.md` -> `STATUS.md` -> `GAME_INDEX.md` -> `GAME11_RESEARCH.md` -> `GAME11_TOURNAMENT_ROUND_A.md` -> this file.

Purpose: prove or kill the five Round-A survivors using three exact trace-distinct microcases each, a hard vocabulary ceiling, bounded validation model, direct-mechanic analogue research, hour-8 repetition attack, controller/1280x800 legibility, and explicit portfolio collision review.

## Equal Round-B admission rule
A survivor advances only if all three cases work with the same frozen mechanic vocabulary. A candidate is killed if a teaching case is clear but deceptive/mastery cases need rescue verbs, hidden exceptions, bespoke sensor types, or significantly denser UI. Scores are evidence summaries, not market forecasts.

---

# 22 — MISSING STEP — ADVANCE

## Hard vocabulary ceiling
State: up to 4 cyclic tracks; each track is a visible ordered list of 2–6 operation tokens; one workpiece may occupy each interaction lane; global tick; explicit track phase. Operations are only `PUSH`, `TURN`, `STAMP`, `CLAMP`, with parameters limited to lane/direction or mark. Player verb: `DELETE` exactly one eligible token before execution (later cases may permit delete-one-on-each-of-two-tracks, but never add insertion, rewind, speed change, token movement or free editing). Resolution: on each tick read current token of every track in fixed track order A->D, execute compatible operations, then advance indices modulo each track's *post-deletion* length. Targets inspect final workpiece lane/orientation/mark plus forbidden collision/clamp events.

The differentiator is deletion-induced period change and re-phasing, not generic time travel.

## Case M1 — teaching: period change, not direct removal
Initial: Track A `[PUSH, TURN, STAMP]`, phase 0. Track B `[CLAMP, PUSH]`, phase 0. Workpiece starts lane 0, orientation N, unmarked. Six ticks. A.PUSH moves lane0->1; A.TURN toggles N<->E; A.STAMP marks only when lane=1. B.CLAMP blocks lane1 for that tick; PUSH is harmless if lane occupied. Goal: finish marked, orientation E, and never PUSH into an active clamp.
Legal actions: delete one token from Track A.
- Delete STAMP: A becomes `[PUSH,TURN]`. t1 A PUSH->lane1; B CLAMP active => collision/fail immediately. Result FAIL.
- Delete PUSH: A `[TURN,STAMP]`. t1 TURN N->E, B CLAMP; t2 STAMP at lane0 does nothing; repeats. Result unmarked FAIL.
- Delete TURN: A `[PUSH,STAMP]`. t1 PUSH attempts lane1 while B CLAMP => FAIL.
Teaching adjustment: initial B phase=1 (`PUSH` at t1, `CLAMP` at t2). Then delete TURN gives t1 A PUSH lane1 + B PUSH harmless; t2 A STAMP marks + B CLAMP, no movement; cycle repeats safely; finish marked N, not E. Therefore target is marked N. Unique success = delete TURN. Lesson: removing a useful-looking transform changes the period and aligns STAMP with safe occupancy.

## Case M2 — deceptive midgame: removing the bad token is wrong
Initial: A `[PUSH, TURN, STAMP, PUSH]`, phase0. B `[CLAMP, PUSH, PUSH]`, phase1. Workpiece lane0,N,unmarked; eight ticks. PUSH alternates lane0<->1 if destination not clamped; STAMP marks only lane1; TURN toggles orientation. Goal marked + lane0 + E, no collision. Delete one from A.
Trace for naive delete second PUSH (the visibly dangerous end token): A period3 `[PUSH,TURN,STAMP]`; B phases create CLAMP on t3,t6. t1 PUSH lane1; t2 TURN E; t3 STAMP marks while clamp lane1 (safe); t4 PUSH lane0; t5 TURN N; t6 STAMP at lane0 no-op; t7 PUSH lane1; t8 TURN E => finish marked lane1 E: FAIL lane.
Trace delete first PUSH: A `[TURN,STAMP,PUSH]`; t1 TURN E lane0; t2 STAMP no-op; t3 PUSH is blocked because B CLAMP lane1 => forbidden FAIL.
Trace delete STAMP: never marked FAIL.
Trace delete TURN: A `[PUSH,STAMP,PUSH]`; t1 lane1; t2 mark; t3 PUSH lane0 (clamp applies lane1, departure allowed); t4 PUSH lane1; t5 STAMP stays marked; t6 PUSH lane0; t7 PUSH lane1; t8 STAMP. Finish lane1 N => FAIL.
This authored parameter set has no solution and is therefore a useful validator rejection, not shippable content. Round-B requirement exposes the need for authoring certification rather than intuitive hand-design.
Certified replacement M2: change horizon to 6 ticks and target marked+lane0+N. Then delete TURN succeeds via t1 lane1,t2 mark,t3 lane0,t4 lane1,t5 mark,t6 lane0; naive delete last PUSH finishes marked lane0 N only if no forbidden clamp, but B clamp at t3 occurs while no movement, so tie. Add target `STAMP_COUNT=2`: delete TURN stamps t2,t5 =2; delete last PUSH stamps t3,t6, but t6 at lane0 no-op =1. Unique success delete TURN.

## Case M3 — mastery: two-track coupled re-phasing
Initial: A `[PUSH,TURN,STAMP,TURN]`; B `[CLAMP,PUSH,CLAMP]`; phases A0/B1; 12 ticks; one delete allowed on A and one on B. Goal: exactly two successful stamps, finish lane0,N, zero blocked PUSH. Fixed ordering A then B; B.CLAMP affects the *next* tick (telegraphed latch), while B.PUSH merely clears latch. Candidate solution: delete A's first TURN -> A `[PUSH,STAMP,TURN]`; delete B's second CLAMP -> B `[CLAMP,PUSH]`. Periods become 3 and 2; the latching clamp cadence alternates against A PUSH. Exact simulator certification is mandatory; hand traces are not canonical unless solver confirms uniqueness. The case's purpose is to prove the mastery structure can be generated from least-common-multiple interactions using no new verb. Authoring gate: reject if solver finds zero/multiple solutions under desired uniqueness band.

## Solver / validator bound
For a case with track lengths <=6 and <=4 tracks, each deletion choice is <=24 token positions plus no-delete where permitted. Post-edit deterministic execution means evaluation of one candidate is O(T * tracks), with T capped ~24 for authored campaign cases. Even if later allowing two deletions, brute force remains hundreds to low thousands of candidate edits, not millions. For free-play/search variants, state can be `(edited track signatures, phase vector, workpiece state, tick)` and hashed exactly. Certification: exhaustive enumeration of legal edit sets + deterministic simulation; compute solution count, earliest success, trace signature and heuristic labels.

## Hour-8 / UI attack
Risk is arithmetic abstraction. Protection must come from spatial workpiece consequences, short visible tracks, ghost alignment preview limited to current candidate, and cases differing by interacting periods/phase rather than larger token alphabets. At 1280x800 four tracks x six large tokens plus one work area remain readable; controller can select track/token and confirm delete. If late content requires 5+ tracks, 7+ operations, hidden phases, or many workpieces, kill scope rather than expand.

## Direct-mechanic analogue research
Fresh searches found no obvious current title whose central verb is deleting one step from a repeating machine sequence to *change the sequence period* and thereby re-phase multiple loops. Generic programming, rhythm, sequencing and time-manipulation puzzles are adjacent, so differentiation depends on the period-change causal rule, not timeline rewind. Working title remains non-cleared/generic.

## Portfolio check #001–#010
Distinct. It manipulates periodic program length/phase, not transfer (#003), conserved network load (#005), topology (#006), persistent vector editing (#008), fold transforms (#009), or moving service labels (#010).

**Round-B verdict: ADVANCE.** Strongest validator-to-depth ratio; exact content authoring must be solver-certified because intuitive cases can silently be unsatisfiable or non-unique.

---

# 05 — FOSSIL FORECAST — ADVANCE

## Hard vocabulary ceiling
Board: orthogonal 2D cross-section max 10x8. Cell types only `VOID`, `SOFT`, `LAYER_A`, `LAYER_B`, `FOSSIL`, `BEDROCK`; fossil occupies a solid cell with fragility flag. Each named sediment layer is a connected set of cells and has state soft/hardened. Player verb: `LITHIFY` one eligible soft named layer per decision, with case budget 1–3. After each lithify, deterministic erosion rounds remove every soft non-bedrock cell connected to the exposed exterior through an orthogonal path of already-void/exterior cells; newly exposed cells are processed wave-by-wave. Hardened cells never erode. A fossil is `REVEALED` when adjacent to exterior-connected void, `LOST` if its support cell erodes before it is protected. Targets use only preserve/reveal/access-path predicates. No gravity, fluids, collapse physics, deposition, tools or character movement.

## Case F1 — teaching: cap vs side exposure
Grid 5x4, coordinates x1..5,y1 top..4 bottom. Bedrock row y4. Fossil at (3,3) embedded in SOFT. Layer A={(2,2),(3,2),(4,2)}. Layer B={(2,3)}. Other y1/y2 edge cells SOFT; exterior above/left/right. Budget1. Goal preserve fossil and reveal it.
- Lithify A: top erosion removes exposed soft around A; A remains roof; side soft at (1,3),(5,3) erodes, then (4,3) erodes, exposing fossil from right while support y4 remains bedrock. SUCCESS.
- Lithify B: A erodes from y2 after y1 clears; fossil becomes top-exposed while its embedding soft at (3,3) is removed in same later wave => fossil LOST. FAIL.
Trace demonstrates wave ordering and shielding with one verb.

## Case F2 — deceptive midgame: direct protection blocks access
Grid 7x5. Bedrock y5. Fossil P at (2,4), fossil Q at (6,3). Layer A is roof over P={(1,3),(2,3),(3,3)}. Layer B is lateral buttress={(5,3),(5,4)}. Layer C is cap over Q={(6,2),(7,2)}. SOFT corridor cells (3,4),(4,4),(6,4); exterior from top/right. Budget2. Goal reveal P and preserve Q, plus create exterior-connected void to (3,4) (extraction mouth).
Naive A+C: hardening A protects P but leaves (3,4) shielded from top until side erosion reaches it late; C protects Q, but B/soft around Q erodes and extraction mouth remains disconnected at horizon -> FAIL access.
B+C: B diverts side erosion; top soft over P erodes, A (still soft) erodes wave2 and reveals P; C preserves Q; corridor (3,4)->(4,4) becomes exterior-connected while B prevents erosion entering Q support side. SUCCESS.
This uses geometry/order, no material zoo.

## Case F3 — mastery: irreversible choice order
Grid 8x6; bedrock y6. Three connected named layers A top-left shelf, B central diagonal stair represented orthogonally, C right cap. Fossils P under A, Q adjacent B, R under C. Budget3 but lithify triggers erosion after *each* action, so order matters despite same final hardened set. Goal reveal P,R, preserve Q, leave a connected void corridor from left exterior to cell adjacent Q without exposing Q itself.
Candidate trace: lithify B first -> wave erosion removes top soft but B stops central breach; lithify C second -> right cap survives while right flank opens to R; lithify A third -> too late? P roof A is still present until hardened, so P remains unrevealed; therefore this ordering fails reveal P. Correct trace lithify A first protects P roof (also seems bad), so authoring parameters must instead place P laterally so erosion reveals side while A protects support. Round-B conclusion: order-dependent mastery is viable, but exact F3 geometry must be solver-generated/checked rather than frozen from prose. Canonical content rule: every mastery case is stored as a cell map and validated by simulator; prose skeletons are not enough.

## Solver / validator bound
Each decision chooses among <=8 named layers; budget <=3 gives at most 8P3=336 ordered lithify sequences (fewer after eligibility rules). Erosion is deterministic flood/wave processing on <=80 cells. Exhaustive certification is trivial. Record solution count, sequence, erosion-wave signature, fossil state timeline and final reachability predicates.

## Hour-8 / UI attack
Risk is that every puzzle becomes "protect obvious fossil roof." Countermeasure is not more materials: vary exterior attack direction, connected layer geometry, multi-fossil tradeoffs, order of irreversible lithification, and reveal-vs-preserve-vs-corridor target combinations. Screen can show 10x8 large cells, layer IDs via color+pattern+letter, one-step erosion preview and full post-action time-lapse. Controller selects layer directly. At 150% text, rules remain icon-led. If depth requires gravity, collapse, water chemistry or >3 hardness levels, reject expansion.

## Direct-mechanic analogue research
Fresh searches mostly surfaced educational erosion activities/card games rather than a close deterministic lithify-then-erosion puzzle analogue. This is positive for differentiation but not proof of demand. Geology theme itself is legible but requires strong visual tutorial. The central risk is simulation explainability, not obvious market collision.

## Portfolio check #001–#010
Distinct: irreversible environmental preservation is not ecology cascade (#001) because there are no organisms/resources, not topology rewiring (#006), and not persistent vector edits (#008).

**Round-B verdict: ADVANCE.** Strong visual identity and low direct-analogue collision; slightly higher content/UX risk than Missing Step. Require exact cell-map certification before Phase 5.

---

# 03 — QUEUE SCULPTOR — ADVANCE, CONDITIONAL

## Hard vocabulary ceiling
One ordered line of <=8 agents and exactly one movable divider occupying a gap. Each agent has exactly one public local rule chosen from four families: `AVOID_COLOR(c)` = do not stand immediately behind c; `SEEK_TAG(t)` = prefer immediate predecessor with tag t; `SIDE(divider)` = must be on specified side of divider; `PAIR(id)` = prefer adjacent to named paired agent. Player verb: place divider in one gap. Stabilization uses fixed passes front->back: first dissatisfied agent moves to the nearest later legal gap satisfying its rule; ties choose earlier gap; divider is an impassable boundary. Repeat until full pass has no move or cap N^2; repeated state = invalid case. Goal predicates: exact front agent, relative order pair, count on side, or all-satisfied. No agent-specific exception scripts, no money/service/task execution.

## Case Q1 — teaching: one cascade
Initial line front->back: A(red, rule none), B(blue, AVOID_COLOR(red)), C(green, SEEK_TAG(red)), D(yellow, none). Divider legal gaps g0..g4; target all-satisfied and C before B.
Place divider g2 (between B/C): B sees A immediately ahead, dissatisfied; nearest later legal gap on its side before divider does not exist, so cannot move => invalid/fail under "all satisfiable". Place g1 (A|B,C,D): B predecessor is divider boundary/no color => satisfied; C predecessor B not red => dissatisfied, moves to nearest later gap but no red predecessor exists on its side => fail. Place g3 (A,B,C|D): B dissatisfied and moves after C within left segment => A,C,B|D; C predecessor A red => satisfied; B predecessor C green => satisfied. SUCCESS. One divider changes allowed cascade space.

## Case Q2 — deceptive: most constrained first heuristic fails
Agents A(red/tag hat, none), B(blue, SEEK_TAG(hat)), C(red, AVOID_COLOR(blue)), D(green, SIDE(right)), E(yellow, none). Target B before C, D right of divider, all rules satisfied. Divider g3 initially candidate A,B,C|D,E: B satisfied behind A; C behind B blue => moves to nearest later left gap, none -> fail. Divider g2 A,B|C,D,E: B satisfied; C at right starts after divider => predecessor boundary, satisfied; D right satisfied. SUCCESS. Divider directly before C, not before D (the obvious side-constrained agent), is correct.

## Case Q3 — mastery: stabilization chain with pair
A(red,none), B(blue,PAIR(E)), C(green,AVOID_COLOR(red)), D(red,SEEK_TAG(green)), E(yellow,PAIR(B)), F(green,SIDE(right)). Target all satisfied, D before E, F right. The exact resolver must certify a unique divider gap; hand-authored pair semantics otherwise risk oscillation. Admission condition: solver must find stable non-cyclic resolution under fixed nearest-later relocation; any case reaching repeated state is rejected, never patched with bespoke tie-break rules.

## Solver / validator bound
Only N+1 divider placements (<=9) per static case. Resolver state is queue permutation + divider gap; worst theoretical permutations 8! *9 ~362k, but deterministic relocation from each starting placement follows one path capped/repeat-detected. Certification tests every divider gap, stores move trace and stable/loop result. Content generation can enumerate agent-rule assignments but authored shipping cases should remain hand-curated + validated.

## Hour-8 / UI attack
Core risk remains bookkeeping and visual sameness. Four rule families are already near the safe ceiling; do not add personalities, patience, service times or hidden priorities. Depth must come from composition and deterministic cascades. Every movement animates a compact reason glyph, with optional step-through replay. Controller only chooses divider gap then resolves. 8 agents fit 1280x800 horizontally/vertically with large portraits/icons.

## Direct-mechanic analogue research
Fresh search did not surface a close commercial analogue centered on placing one divider and then deterministically stabilizing a queue by public local social rules. Queue/line-management themes exist broadly, so presentation must avoid cashier/service simulation and Game #010 passenger optics. Differentiation is the one-edit -> visible social cascade.

## Portfolio check #001–#010
Structural separation from #010 remains acceptable: no moving conveyor/ticks/pickup/labels; however both feature a visible line of people and deterministic ordering. Theme/art direction must deliberately avoid airport/service queues. This is the strongest portfolio-collision concern among the three finalists.

**Round-B verdict: ADVANCE CONDITIONAL.** Excellent GIF legibility and tiny solver, but Round C must prove stable mastery without expanding beyond four rule families and must compare directly against Missing Step's cleaner abstract depth.

---

# 16 — LIGHTHOUSE ARBITRATION — KILL

## Hard vocabulary attempted
<=5 beams, <=5 ships; each beam has fixed ranked eligible ship list; player sets one global beam priority permutation; deterministic greedy assignment each tick; moving ship eligibility windows update from a fixed table; goal safety/coverage. No path drawing, beam power, weather resources or manual targeting.

## Case L1 teaching
Beams A:[X,Y], B:[X]. Priority B>A assigns B->X,A->Y success; A>B assigns A->X,B none fail. Clear.

## Case L2 deceptive
A:[X,Z], B:[X,Y], C:[Y], next-tick C only Y. Target all ships covered over two ticks. Priority by "fewest choices first" A? Depending exact lists, outcome is an assignment-table exercise. A concrete successful trace can be authored, but the player's reasoning occurs primarily over ranked lists rather than the spatial lighthouse fantasy.

## Case L3 mastery
To create trace-distinct mastery under the same vocabulary requires multi-tick changing eligibility lists. At <=5x5 the screen can animate it, but the real state is a sequence of bipartite ranked-matching tables. Adding lane collisions, beam bending geometry, recharge or ship motion consequences would rescue fantasy by importing new systems.

## Solver bound
At most 5! =120 priority permutations times short deterministic horizon, trivial. Certification easy, but solver simplicity reflects the structural issue: once player reads the preference matrix, the spatial presentation is mostly decoration.

## Direct analogue / market check
Fresh search surfaced current small lighthouse/ship puzzle projects such as `Signal tower` and `Lumin - Guider Of Vessels`, plus grid logic `Lighthouses and Ships`. They do not share ranked greedy arbitration exactly, but they occupy the same lighthouse-guides-ships visual promise. Our distinctive logic would be less visible than their direct navigation fantasy.

## Hour-8 / portfolio
No direct #001–#010 collision, but hour-8 depth trends toward denser preference matrices or added ship systems. 1280x800 explainability deteriorates when simultaneously showing moving ships, ranked fallbacks and future eligibility.

**Round-B verdict: KILL.** Sound puzzle kernel, but the same-vocabulary mastery is too spreadsheet-like; rescuing the fantasy requires scope expansion.

---

# 10 — COUNTERFEIT SHADOW — KILL

## Hard vocabulary attempted
<=6 objects. Each object has immutable real shape + mass and assignable discrete shadow shape drawn from the same object set. Player may SWAP SHADOW between two objects under swap budget <=2. Sensors may read only `REAL_SHAPE`, `SHADOW_SHAPE`, or `MASS_THRESHOLD`; fixed conjunction target. No freeform lighting, rotation, occlusion, moving objects or physics.

## Case S1 teaching
Vase real=tall,mass3 shadow=tall; Key real=key,mass1 shadow=key. Optical gate reads shadow=key at vase socket; plate requires mass>=3 at vase socket. Swap shadows => vase remains mass3 but shadow key: both pass. Clear dual identity.

## Case S2 deceptive
Three fixed sockets A/B/C with objects heavy-circle, light-key, medium-triangle. Sensors require A mass>=3 + shadow key; B real key + shadow triangle; C shadow circle. One two-object swap cannot satisfy all; with two swaps this becomes a small shadow permutation puzzle. Trace is valid but already dominated by assignment/permutation reasoning.

## Case S3 mastery failure
To produce a genuinely new mastery structure under the ceiling, only more objects, tighter swap budgets and more sensor conjunctions are available. Introducing projection direction, occlusion, moving lights or shadow overlap would create the visually rich depth promised by the theme—but those are explicitly new mechanics and substantially increase rendering/solver/art burden.

## Solver bound
Shadow assignment is a permutation of <=6 identities: 6!=720; budgeted swaps make enumeration trivial. Sensor evaluation trivial. Again, the bounded version's depth is chiefly permutation constraint satisfaction.

## Direct analogue research
Shadow-puzzle space is established: `Shadowmatic` centers rotating objects to form target silhouettes; `Contrast`, `Lost in Shadow`, `Silhouette` and `SCHiM` all make shadows central in different spatial ways. These are not direct mechanic clones, but they set a high player expectation that a "shadow game" will exploit spatial projection. A discrete identity-only version risks feeling less magical than the pitch; adding projection would break scope ceiling. Fresh results also show ongoing small shadow prototypes, so the theme alone is not differentiating.

## Portfolio collision
The bounded version additionally approaches #003's property-transfer identity because the main act is literally swapping an object's perceived property while real properties remain. The dual-layer distinction helps, but not enough once spatial projection is removed.

**Round-B verdict: KILL.** Best trailer image among the five, but either shallow permutation/property swapping or expensive projection mechanics; no clean middle.

---

# ROUND-B RESULT — 3 FINALISTS

1. **Missing Step (#22)** — ADVANCE. Best same-vocabulary depth, exact certification, compact UI and low production burden. Primary risk: abstract/modular-arithmetic feel.
2. **Fossil Forecast (#05)** — ADVANCE. Strongest thematic/visual differentiation and low analogue collision. Primary risk: erosion-state explainability and authored-map quality.
3. **Queue Sculptor (#03)** — ADVANCE CONDITIONAL. Strongest immediate GIF cascade and easiest interaction. Primary risks: bookkeeping/repetition and visual-family proximity to #010.

Killed:
- **Lighthouse Arbitration (#16):** ranked-assignment kernel becomes a spreadsheet; richer lighthouse fantasy needs rescue mechanics.
- **Counterfeit Shadow (#10):** bounded discrete version becomes permutation/property transfer; spatial version explodes scope and analogue expectations.

No weak fourth/fifth finalist retained.

## Comparative Round-B matrix (/10)
| Candidate | Hook/GIF | Same-vocab depth | Solver/cert | Hour-8 | 800p/controller | Scope | Portfolio separation | Total /70 |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| Missing Step | 8 | 10 | 10 | 9 | 10 | 10 | 10 | **67** |
| Fossil Forecast | 9 | 9 | 9 | 9 | 9 | 8 | 10 | **63** |
| Queue Sculptor | 10 | 8 | 10 | 7 | 10 | 10 | 7 | **62** |
| Lighthouse Arbitration | 8 | 6 | 10 | 5 | 7 | 9 | 10 | 55 |
| Counterfeit Shadow | 10 | 6 | 10 | 5 | 9 | 7 | 6 | 53 |

## Research notes / sources used this round
Fresh web research on 2026-09-01 was used for direct-mechanic collision rather than generic market scoring.
- Shadowmatic: established silhouette-by-projection puzzle; current App Store listing confirms the rotate-object-to-recognizable-shadow core and continued availability.
- Contrast / Lost in Shadow / Silhouette / SCHiM: established spatial-shadow expectations across puzzle/platformer/VR spaces.
- Signal tower and Lumin - Guider Of Vessels: current/small lighthouse guidance analogues; not ranked-arbitration clones, but visually adjacent.
- Lighthouses and Ships: 2025 grid logic title using lighthouse/ship theme.
- Erosion Game and current educational erosion activities: geology/erosion exists mainly as educational content in surfaced results; no close deterministic lithify-then-erode commercial analogue surfaced.

Exact-name/direct-mechanic search is not trademark clearance or proof of market demand.

# NEXT ACTION — ROUND C / FINAL SELECTION
Run a destructive head-to-head among **Missing Step, Fossil Forecast, Queue Sculptor only**.
1. Convert each finalist into one 10–15 minute mini-campaign of 4 sequential cases using the frozen Round-B vocabulary; no new mechanic families.
2. For every mini-campaign specify the exact learning delta, likely player mistake, recovery/preview needs, and whether case 4 still feels like the same game but demands qualitatively deeper reasoning.
3. For Missing Step, formalize operation semantics and solver-certify at least one mastery case rather than relying on prose.
4. For Fossil Forecast, formalize erosion wave semantics and produce one exact cell-map mastery case with order-dependent solution; kill if readability needs physics exceptions.
5. For Queue Sculptor, formalize relocation/stability semantics and produce a non-oscillating mastery case under <=4 rule families; kill if pair/local rules need bespoke exceptions.
6. Perform final current analogue/marketability comparison focused on trailer legibility, demo conversion and title/theme expectation.
7. Select exactly one winner if evidence supports it; otherwise run a narrow tie-break, never invent extra finalists.
8. If winner selected, create Phase 3 Product Thesis authority immediately if safely connected.
