# GAME #004 — OPPORTUNITY DISCOVERY — RUN 2

Last updated: 2026-08-20
Factory run: **2**
Phase: **1 — Opportunity Discovery**
Concept selected: **NO**

This run attacks the 12 Run-1 Tier-A candidates with direct analogue pressure, defines fast graybox falsification, expands underrepresented design territories, and reduces the field without opening Phase 2.

---

# 1. Current analogue pressure checked

Fresh searches were run 2026-08-20 across topology/panel manipulation, construction-shot/physics, destruction, acoustic stealth and chain-reaction spaces.

Important precedents:
- **FRAMED** — rearranges animated comic panels to alter story outcome; later puzzles can manipulate panels while action plays.
- **Gorogoa** — moves/stacks/explores image panels and uses visual alignment/masking as puzzle grammar.
- **The Pedestrian** — rearranges and reconnects signs, including spatial alignment of doors/ladders, then traverses them.
- **Viewfinder** — camera/images reshape traversable 3D reality; strong warning against broad camera/perspective claims.
- **Bionic Bay** — action-platforming built around swapping positions with objects plus physics; evidence that a single direct manipulation verb can support action/speedrun depth, but raises bar for physical-tool feel.
- **Gunpoint** — readable 2D building stealth plus rewiring of environmental controls; warning that stealth/system routing needs an ownable physical verb.
- **Mark of the Ninja** — visually represents sound propagation, proving visual redundancy can be core rather than accessibility afterthought.
- **Stifled / A.V.** — sound-centric stealth/puzzle identities already exist; Soundproof Smuggler must be about reshaping propagation topology, not merely seeing/hearing sound.
- **ABRISS** — building-to-destroy physics puzzle with limited parts and spectacular destruction; strong pressure on generic construction/destruction concepts.
- **Armadillo Run** — materials, anchors, tension and simulation-based construction already form a deep puzzle space; Tension Window cannot merely be a one-material bridge builder.

Search conclusion: panel/layout manipulation is a mature design territory, while **edge adjacency editing**, **negative-space traversal**, and **physically blocking/re-routing sound** still have defensible whitespace if their repeated verbs remain narrower than their precedents.

---

# 2. Tier-A candidate attacks and graybox gates

## G4C01 — Seam Thief — KEEP / HIGH
**10-second verb:** snap cursor to two authored compatible boundary segments; hold Stitch; the segments zip together; anything crossing either edge immediately exits the other with orientation determined by seam arrows.

**Analogue pressure:** portals own paired traversal surfaces, but the proposed distinction is that stitching changes *world adjacency* for all eligible contact/crossing relationships along the seam, not an isolated teleport trigger. This distinction must survive graybox.

**One-week graybox:** 12 flat rooms, 3 seam lengths, player + crate + moving hazard; no art. Require solutions involving (a) player crossing, (b) non-player propagation, (c) seam orientation, (d) one seam helping and harming simultaneously.

**Kill if:** >35% of test rooms reduce to `put entrance here, exit there`; seam orientation is hard to predict; or 8/12 rooms can be solved by stitching nearest-start to nearest-goal boundaries.

## G4C02 — Missing Piece — KEEP / MEDIUM
**10-second verb:** target one marked shape cell embedded in an object, extract it, then snap the exact piece into one of a few matching sockets; the source becomes a real hole while destination gains material.

**Analogue pressure:** less direct than panel games, but risks becoming ordinary key/block placement with a removal animation.

**One-week graybox:** 5 shape families, 10 rooms, no freeform geometry. Source holes must alter traversal/visibility/support while the inserted piece performs a second role elsewhere.

**Kill if:** players describe pieces primarily as keys; source-hole consequence is irrelevant in >30% of useful moves; or shape recognition needs labels/rotation fiddling.

## G4C03 — Frame Job — HARD KILL
FRAMED already rearranges comic panels, including during playback; Gorogoa makes panel position/alignment itself causal. Moving borders rather than whole panels is not enough competitive distance unless a stronger second-order rule appears. Current muted clip would be read as `another comic-panel puzzle`.

## G4C04 — One-Bullet Mason — KEEP / MEDIUM-HIGH
**10-second verb:** aim with heavy snap at authored anchorable surfaces, fire the single live bolt, and instantly replace the previous bolt; the bolt creates one structural relation selected by impact context: hinge, brace, or tether endpoint.

**Analogue pressure:** grapples, construction games and physics platformers are crowded. Identity depends on **exactly one live shot** and contextual structural conversion, not inventory construction.

**One-week graybox:** side-view action room set with one bolt, three context outcomes, moving player and deterministic bodies. Test continuous shoot→move→reshoot flow.

**Kill if:** average player stops moving for >3 s before most shots; one context outcome handles >65% of successful interactions; or aim assist makes placement trivial while free aim feels mandatory.

## G4C05 — Cutaway House — DOWNGRADE / RESERVE
The source-cost idea is understandable, but carrying/reinstalling wall/floor panels trends toward block transport and backtracking. Keep as reserve only if later mutation removes manual carrying and makes structural exposure immediate.

## G4C09 — Negative Space Courier — KEEP / HIGH-RISK HIGH-IDENTITY
**10-second verb:** grab one bounded world-panel and slide it on a snap grid; the player continues moving through the contiguous *gap* around panels, so every layout move immediately reshapes traversable negative space.

**Analogue pressure:** The Pedestrian rearranges signs and their connections; Gorogoa rearranges image panels. Here the panel content is obstruction/context and **the gaps themselves are the level**. That inversion is defensible but fragile.

**One-week graybox:** fixed 16:9 logical playfield independent of physical screen; 8 panel layouts; player movement never pauses while panel movement is allowed. Test same puzzle at 16:9, 16:10, 4:3 via letterboxed logical canvas.

**Kill if:** players focus on panel contents rather than gaps; solutions feel like sliding-block puzzles; controller panel selection exceeds 1.5 s median; or aspect-ratio normalization changes route semantics.

## G4C11 — Stagehand Zero — KEEP / MEDIUM-HIGH
**10-second verb:** while actor/player motion continues, tap a lane and slide one scenery flat between three discrete depth tracks; when it clicks into the active track its silhouette becomes collision geometry immediately.

**Analogue pressure:** foreground/background and page/world transitions exist broadly, but discrete live scenery ownership plus theatrical staging remains ownable if depth is binary-clear.

**One-week graybox:** 3 depth tracks, 6 prop archetypes, one runner, 10 short sequences. No perspective scaling; track tint + shadow/contact cue must predict collision before activation.

**Kill if:** >10% of playtest collisions surprise players; pausing is needed to understand track ownership; or each prop needs bespoke behavior rather than shared geometry rules.

## G4C14 — Threadbare Heist — DOWNGRADE / RESERVE
Finite thread and authored snaps solve freehand input, but the concept overlaps grappling/rope-route construction and risks optimal straight-line shortcuts. Reserve pending a mutation where thread has a second live consequence beyond path length.

## G4C19 — Soundproof Smuggler — KEEP / HIGH
**10-second verb:** grab/rotate one absorber panel on authored floor/wall rails; visible sound fronts immediately bend around blocked portals and guards' predicted hearing regions update before the player moves.

**Analogue pressure:** stealth games already model/visualize sound; Mark of the Ninja makes sound circles readable and advanced games propagate through rooms/openings. The ownable action is therefore **editing the propagation graph physically with one blocker**, not generating or visualizing noise.

**One-week graybox:** top-down 8-room graph rendered as rooms/doorways; one absorber; three sound classes; moving guards. Every audible rule has simultaneous visible wavefront/route feedback.

**Kill if:** optimal play is waiting for patrol cycles >25% of run time; players cannot predict whether a guard hears a planned action before committing; visual-only play changes optimal decisions; or absorber placement becomes simple `close nearest door`.

## G4C24 — Debris Sculptor — KEEP / MEDIUM-HIGH
**10-second verb:** strike one highlighted fracture seam; object splits into 2–4 deterministic authored chunks that remain exactly where the break logic predicts; immediately push/stand/wedge using those chunks.

**Analogue pressure:** ABRISS strongly occupies build-to-destroy spectacle and complex debris. Differentiation requires the reverse loop: **destroy authored structure to obtain the only construction vocabulary**, with deterministic qualitative chunks rather than free debris spectacle.

**One-week graybox:** 6 source objects, each with 2 fracture choices; 12 chunk archetypes; no inventory and no arbitrary rotation. Rooms require preserving some structure while harvesting specific chunk affordances.

**Kill if:** `break everything` succeeds in >20% of rooms; chunk resting positions require repeated physics retries; or players want/need an inventory to manage fragments.

## G4C28 — Tension Window — KEEP / MEDIUM
**10-second verb:** choose two nearby snap anchors and pull one membrane to one of three tension bands; release; the single live membrane catches, redirects or launches bodies according to approach angle and tension band.

**Analogue pressure:** Armadillo Run and broad physics construction already own ropes/elastic/tension as materials. The only defensible identity is a **single live membrane used during action**, not prebuilt structures.

**One-week graybox:** deterministic segmented curve, not free soft-body simulation; 3 tension bands; 8 approach-angle buckets; one membrane maximum; 10 action rooms.

**Kill if:** outcome variance exceeds one player-body width on repeated identical inputs; setup dominates play time; or catching/launching cannot share one learnable response model.

## G4C34 — Single Cause — DOWNGRADE / RESERVE
**10-second verb:** choose one attachment point and one trigger type, press run, then scrub/restart rapidly.

The production scope is attractive, but one-trigger contraption/chain-reaction space inherits The Incredible Machine/contraption lineage and plan→watch agency risk. Keep only as reserve for a future mutation where the player remains embodied during the cascade.

**Kill as current finalist if:** observation exceeds interaction by >2:1 in the first graybox; median restart-to-new-decision >4 s; or players solve by exhaustive trigger placement rather than causal reasoning.

---

# 3. Underrepresented-territory expansion — 12 new seeds

## Non-spatial deduction

### G4C37 — Contradiction Stamp
A stream of 6–10 compact claims describes one machine/person/event. Player may stamp exactly one clause `FALSE`; all downstream clauses instantly recompute under explicit logical dependencies. Goal is to make the final observed evidence consistent.
- repeated verb: mark one claim false, inspect causal rewrite, revoke/re-stamp;
- strength: deduction is visible as a live dependency transformation;
- risk: becomes spreadsheet logic.

### G4C38 — Alibi Relay
Four witnesses each answer only about the previous witness's last statement. Player chooses who speaks next; statements mutate the reachable truth-state rather than merely reveal clues.
- repeated verb: select next speaker to force a useful constrained statement;
- risk: dialogue/content burden.

### G4C39 — Exception Clerk
A rule engine processes objects automatically. Player may author exactly one exception token (`IF visible property A AND B -> ignore rule R`) and must make a batch pass without breaking protected cases.
- repeated verb: compose one tiny exception from physical property chips, run batch;
- strength: non-spatial systemic deduction;
- risk: office/software presentation may look like work.

## Direct score attack

### G4C40 — Ricochet Ledger
One arena, one puck, one impulse per rally. Score multiplies for distinct surface categories touched before goal, but every extra category increases hazard speed.
- repeated verb: aim/launch, then immediately reposition the next scoring surface while puck stays live;
- risk: physics unpredictability / pinball comparison.

### G4C41 — Close Call
Player draws no route: steer a continuously moving courier through hazards; score only accumulates while inside visible danger envelopes, with combo broken by touching safety zones.
- repeated verb: deliberately skim threat boundaries;
- strength: clip-readable mastery without content-heavy systems;
- risk: generic arcade movement unless envelope behavior is ownable.

### G4C42 — One More Cut
A deterministic moving shape crosses a field. Each run permits one straight cut that divides both obstacle geometry and scoring regions; score comes from how many newly created boundaries the shape crosses without dying.
- repeated verb: place one cut during live motion;
- risk: Slice-it lineage / geometry abstraction.

## Turnless tactics

### G4C43 — Command Wake
Three agents move continuously on simple visible routines. Player directly controls only the leader; crossing another agent's wake changes that agent's routine for exactly one cycle.
- repeated verb: weave leader through moving wake lanes to issue embodied commands;
- strength: tactics without pause/menu orders;
- risk: route-following chaos.

### G4C44 — Threat Magnet
Enemies always target the currently loudest unit. Player can make one allied unit louder by physically dashing through it; aggro transfers instantly while everyone keeps moving.
- repeated verb: dash through ally to hand off threat;
- risk: aggro juggling may become repetitive.

### G4C45 — Formation Scar
Every dash leaves one short-lived impassable scar. Units, allies and enemies route around all scars continuously; player fights by carving temporary tactical topology while moving.
- repeated verb: dash to both reposition and author temporary terrain;
- risk: pathfinding readability.

## One-object simulation

### G4C46 — Inside-Out Safe
The entire game is one mechanical safe cross-section. Rotate one external ring; internal cams, pins and channels move continuously. Objectives ask for multiple internal states without ever directly touching internals.
- repeated verb: rotate/reverse one ring while reading internal consequences;
- strength: one-object production scope, physical causal readability;
- risk: lockpicking/schedule arithmetic.

### G4C47 — Umbrella Engine
Control only the opening angle of one giant umbrella-like machine while wind, falling objects and rolling cargo continue. Angle changes simultaneously alter shelter, lift, deflection and catch area.
- repeated verb: open/close to discrete angle bands during live simulation;
- strength: one object, multiple coherent affordances;
- risk: wind physics unpredictability.

### G4C48 — Bellows City
One bellows is the only input to a tiny mechanical settlement. Compression amount and release speed route pressure through visible valves, moving lifts, shutters and inhabitants.
- repeated verb: compress/release one actuator with timing and magnitude;
- strength: embodied one-input causal machine;
- risk: resembles pressure/circuit routing and timing puzzle.

---

# 4. Uniform scoring

Weighted score uses Run-1 model. Values below are /100 after weighting 1–5 ratings. Hard-killed concepts are excluded regardless of numeric appeal.

| ID | Concept | Score | State | Main falsification risk |
|---|---|---:|---|---|
| G4C01 | Seam Thief | **85.0** | Finalist | portal equivalence |
| G4C19 | Soundproof Smuggler | **82.5** | Finalist | waiting / prediction |
| G4C09 | Negative Space Courier | **81.5** | Finalist | sliding-block equivalence |
| G4C11 | Stagehand Zero | **80.0** | Finalist | depth ambiguity |
| G4C04 | One-Bullet Mason | **79.5** | Finalist | aim/setup friction |
| G4C24 | Debris Sculptor | **78.5** | Finalist | deterministic chunk feel |
| G4C43 | Command Wake | **78.0** | Finalist | live-state readability |
| G4C47 | Umbrella Engine | **77.5** | Finalist | simulation variance |
| G4C02 | Missing Piece | **77.0** | Finalist | key/block collapse |
| G4C28 | Tension Window | **76.5** | Finalist | elastic predictability |
| G4C45 | Formation Scar | **76.0** | Finalist | pathfinding readability |
| G4C46 | Inside-Out Safe | **75.5** | Finalist | arithmetic/timing feel |
| G4C37 | Contradiction Stamp | **74.5** | Finalist | dry logic UI |
| G4C41 | Close Call | 73.5 | Reserve | generic arcade identity |
| G4C44 | Threat Magnet | 72.5 | Reserve | repetitive aggro juggling |
| G4C40 | Ricochet Ledger | 71.5 | Reserve | pinball/free physics |
| G4C48 | Bellows City | 71.0 | Reserve | signal-routing familiarity |
| G4C39 | Exception Clerk | 70.0 | Reserve | work/software surface |
| G4C42 | One More Cut | 69.5 | Reserve | geometry abstraction |
| G4C38 | Alibi Relay | 67.5 | Reserve | writing/content burden |
| G4C05 | Cutaway House | 70.5 | Reserve | carrying/backtracking |
| G4C14 | Threadbare Heist | 70.0 | Reserve | rope-route familiarity |
| G4C34 | Single Cause | 68.5 | Reserve | plan/watch agency |
| G4C03 | Frame Job | — | **HARD KILL** | FRAMED/Gorogoa comparison |

Scores are triage, not winner selection. Competitive whitespace has intentionally low weight; a mechanically excellent concept is not killed merely because a neighboring genre exists, but noun+verb+fantasy equivalence triggers the hard kill.

---

# 5. Serious Phase-1 finalist slate — 13

1. **G4C01 Seam Thief** — strongest topology candidate; must prove adjacency rather than portal routing.
2. **G4C19 Soundproof Smuggler** — strongest stealth/system candidate; physical propagation editing is distinct.
3. **G4C09 Negative Space Courier** — strongest pure visual identity; high analogue pressure but clear inversion.
4. **G4C11 Stagehand Zero** — strong theatrical clip language with discrete deterministic depth.
5. **G4C04 One-Bullet Mason** — strongest direct-action construction candidate.
6. **G4C24 Debris Sculptor** — destruction with source-constrained construction vocabulary.
7. **G4C43 Command Wake** — promising turnless embodied tactics.
8. **G4C47 Umbrella Engine** — promising one-object action simulation.
9. **G4C02 Missing Piece** — conservation-of-shape remains visually strong but needs anti-key proof.
10. **G4C28 Tension Window** — expressive one-tool action if deterministic simplification works.
11. **G4C45 Formation Scar** — movement authors tactical topology without command menus.
12. **G4C46 Inside-Out Safe** — compact one-object causal machine with strong scope discipline.
13. **G4C37 Contradiction Stamp** — best non-spatial deduction seed; intentionally retained to prevent spatial-puzzle monoculture.

No concept is selected. Phase 2 is not open yet.

---

# 6. Cross-field lessons

1. **Panel manipulation has a high originality tax.** FRAMED, Gorogoa and The Pedestrian collectively cover ordering, stacking/alignment and reconnecting/rearranging panels/signs. A future panel concept needs a consequence those games do not already visually claim.
2. **Sound is viable only as topology, not meter.** Existing stealth already visualizes and propagates sound. Soundproof Smuggler survives because the player changes the propagation graph with an embodied blocker and sees the prediction before acting.
3. **Physics spectacle is not whitespace.** ABRISS and broad construction games mean Debris Sculptor/Tension Window must use bounded deterministic response models; realism is a liability, not a selling point.
4. **Direct action should preserve thought without creating setup pauses.** One-Bullet Mason, Tension Window and Umbrella Engine all need median decision-to-action loops measured in seconds.
5. **The best new underrepresented territory is turnless tactics.** Command Wake and Formation Scar create tactical state through movement rather than pause menus, potentially combining clip clarity with systemic depth.
6. **One-object simulation is scope-efficient but vulnerable to timing arithmetic.** Inside-Out Safe/Umbrella Engine need multiple coherent affordances from one input, not increasingly complicated schedules.
7. **Keep one non-spatial finalist deliberately.** Contradiction Stamp is not currently top-ranked, but its survival prevents the tournament from becoming a topology/physics echo chamber.

---

# 7. NEXT ACTION — Run 3 / final Phase-1 falsification

Do not open Phase 2 yet.

1. Attack all 13 finalists with **pairwise nearest-neighbor searches** and explicit `why not just play X?` answers.
2. For Seam Thief, specify seam legality, orientation, object-crossing semantics and three mature puzzle families that portals cannot reproduce.
3. For Soundproof Smuggler, specify a tiny deterministic acoustic graph and prove a no-audio player receives identical decision information.
4. For Negative Space Courier, test whether panel contents can be removed entirely; if the concept dies without decorative panel identity, kill it.
5. For One-Bullet Mason, Tension Window, Debris Sculptor and Umbrella Engine, define bounded deterministic response tables instead of free physics.
6. For Command Wake and Formation Scar, write 60-second live-state traces and identify whether tactics remain readable without pause.
7. For Inside-Out Safe and Contradiction Stamp, prove the first independent decision occurs inside 3 minutes and the muted clip is legible.
8. Run a **portfolio-distance audit** against Games #001–#003 without importing their mechanics as canon.
9. Require every survivor to state: one-sentence hook, 10-second GIF, minute-1 decision, minute-20 demo climax, hour-3 depth source, hour-10 repetition defense, one-week kill test, and scope ceiling.
10. Reduce to **8–10 Phase-1 survivors** only after those proofs. Then and only then open Phase 2 Concept Tournament in the following run.
