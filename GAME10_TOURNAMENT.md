# GAME #010 — PHASE 2 CONCEPT TOURNAMENT

Date: 2026-08-31
Status: ROUND A COMPLETE — 12 -> 6
Final concept selected: NO

Authority: `START_HERE.md` -> `STATUS.md` -> `GAME_INDEX.md` -> `GAME10_RESEARCH.md` -> this file.

## Round A method
All twelve entrants were attacked on the same axes: 20-second legibility, hour-3 recombination, hour-8 reasoning change, dominant heuristic, deterministic state/validator feasibility, content burden, implementation burden, failure explainability, controller/1280x800 readability, visual motion, and derivative/portfolio risk. Concepts failing a hard gate were killed before expensive microcase work. Serious survivors received two concrete hand-simulated cases and a counterexample to the obvious heuristic.

Fresh analogue/name checks on 2026-08-31 found no obvious game-title/direct-mechanic collision for the leading working concepts. The important risk is structural rather than title collision: garden games are common, so Stencil Orchard/Negative Gardening must market the manipulation rule rather than merely the garden theme; Consensus Machine also evokes real distributed-consensus terminology, so its final title must change if selected.

# T1 — STENCIL ORCHARD — SURVIVES
20 sec: a 5x5 bed pulses. Player drags an L-shaped opaque stencil across it; on STEP only uncovered buds advance, covered buds hold. The resulting flower silhouette visibly differs from the preview.
Hour 3: two reusable masks, cells at ages 0/1/2, harvest requires selected cells reach 2 together while neighbors stay <=1. Mask placement is now temporal sculpting.
Hour 8: several target windows and masks with holes; the same mask can preserve a region while advancing two disconnected fronts. Advanced play is about phase relationships, not bigger grids.

Microcase A: line ages [0,1,0], target [1,1,1], one step, stencil covers exactly one cell. Cover middle; exposed ends advance => [1,1,1]. This teaches that covering is preservation, not deletion.
Microcase B: 2x2 ages [[1,0],[0,1]], target all 1 after one step, domino stencil. A horizontal cover cannot work: one age-1 remains exposed and over-ages. A diagonal-shaped two-hole mask is not available; instead use two steps with vertical domino: cover left first => [[1,0],[1,2]], then cover right while reset/harvest condition would already be violated. Therefore this target is deliberately impossible under the stated inventory; validator can certify impossibility. Change target to [[1,1],[1,2]] and first-step left cover solves immediately. This demonstrates content can include feasibility reasoning, not trial-and-error.
Dominant heuristic: expose maximum number of target cells. Counterexample: ages [1,0,0], target [1,2,2] after two steps. Exposing all initially over-ages cell 1; covering the already-correct cell on both steps is required.
Minimum vocabulary: cell age, deterministic advance, hold mask, target window, reusable mask inventory; later bounded cell rules may add death/harvest but are not needed for core depth.
Burden: low implementation, low asset, medium authoring; exact discrete solver straightforward (state = cell ages + mask inventory + remaining steps).
Failure explainability: excellent if preview highlights ADVANCE/HOLD and post-step marks first violated target window.
Deck/controller: cursor snaps mask anchors; rotate shoulder button; no tiny freehand input.
Risk: can become CA-flavored turn counting. Round B must prove expert depth without adding species/rule soup.

# T2 — LUGGAGE CAROUSEL ZERO — SURVIVES
20 sec: three bags orbit; passenger icon says “RED + ROUND TAG”. Player swaps two overhead labels; belt advances; passenger takes a bag and the gap visibly changes future order.
Hour 3: recognition predicates are public, belt motion is turn-based/plannable, pickups remove bags, labels occupy fixed carousel sockets rather than belonging permanently to bags.
Hour 8: predicates combine visible bag traits and current socket labels; finite swaps before each belt tick; removal changes which bag reaches which socket next. The puzzle is intervention in a moving permutation.

Microcase A: sockets A,B,C carry labels red,blue,green; bags 1,2,3 at A,B,C. P1 takes first red-labelled bag encountered at pickup C after one tick. Swap labels A/B; after tick bag2 reaches C under red path ordering and is removed, preserving bag1 for P2. The key is labels are spatial sockets, not bag properties.
Microcase B: four bags cycle A->B->C->D(pickup). P1 accepts label X; P2 accepts X plus square bag. If bag4(square) currently at C and bag3(round) at D, serving P1 immediately with X at D removes round bag and advances square into D next tick for P2; swapping X to C before tick instead causes square to inherit X at D only after motion depending on socket semantics. Exact discrete ordering creates distinguishable plans.
Dominant heuristic: satisfy earliest passenger ASAP. Counterexample: P1 accepts either X/Y, P2 only X on square. Giving X to P1 removes the only socket timing that can present square+X to P2; give P1 Y instead.
Vocabulary: ring sockets, deterministic tick, fixed pickup point(s), visible bag traits, public predicates, label swap, removal/gap compression rule.
Burden: low implementation, medium UX/content, solver feasible by finite permutation search.
Failure explainability: strong with timeline ghost for next 1–2 ticks and explicit passenger predicate.
Deck/controller: excellent if carousel has <=8–10 sockets on core view and paused planning by default.
Risk: hidden predicates are banned; real-time dexterity is banned. Round B must formalize socket/removal ordering and show generated/authored diversity.

# T3 — NEGATIVE GARDENING — ELIMINATED
20-second inverse-growth hook is excellent, but destructive modeling exposes a semantic problem: “plants grow into space forbidden to them” is catchy yet physically/algorithmically arbitrary. To make local prediction fair, the game needs an explicit boundary-seeking growth algorithm; once shown, play converges toward manipulating a cellular-growth frontier with blockers. Hour-8 depth proposed extra species, delayed pruning and competition—new rule families rather than proof the base inversion scales. Failure explainability also becomes worse whenever several candidate forbidden boundaries tie. KILL: fails its own conditions 1/2/4 risk cluster. Do not silently revive as Game #010 canon.

# T4 — PHOTOCOPIER GARDEN — SURVIVES
20 sec: select a 2x2 patch, stamp a copy beside it; source visibly frosts/freeze-pauses while the new copy advances one generation.
Hour 3: overlapping rectangles create regions with different age offsets; objectives concern synchronization/desynchronization of recognizable motifs.
Hour 8: copy placement changes both spatial multiplicity and temporal phase. Limited copy sizes and source-freeze duration create sequencing without freehand complexity.

Microcase A: source pair ages [0,1], rule advance +1 capped at2. Copy pair to empty slots: source freezes [0,1], copy materializes advanced [1,2]. Goal asks one young+one mature pair; one copy solves visibly.
Microcase B: source 2x2 ages [[0,1],[1,0]], goal requires two adjacent age-2 cells but original center must remain age1. Copy right column first: source right freezes while copy ages; next global tick advances un-frozen left/source and prior copy, creating asymmetric phases unavailable by waiting alone.
Dominant heuristic: copy largest useful region. Counterexample: copying a large rectangle freezes a source cell that must advance this turn; a smaller patch copies the needed motif while leaving that cell live.
Vocabulary: age state, global generation, rectangle source, copy destination, source freeze for N=1 baseline, copied cells receive +1 age, overlap legality.
Burden: low-medium implementation, medium state-visualization, solver feasible on bounded boards.
Failure explainability: good only with clear age/freeze tint and before/after ghost.
Deck/controller: rectangular selection maps cleanly to controller.
Risk: closest survivor to abstract CA editor. Round B must prove goals are meaningful structures rather than arbitrary bitmaps and distinguish it strongly from Stencil Orchard.

# T5 — INVENTORY ECLIPSE — SURVIVES
20 sec: world door needs a crowbar; player opens pack and slides a tall lantern so its projected slot-shadow uncovers the crowbar; crowbar phases visibly into the character’s hand/world.
Hour 3: inventory objects cast fixed grid shadows from their occupied cells; covered tools are inactive/absent, uncovered tools active. World interactions can change item footprints/orientation, feeding back into pack topology.
Hour 8: challenges require capability schedules: keep bridge tool active at checkpoint A, intentionally phase it out so another object can occupy a world socket, then restore it after inventory changes earned in-world.

Microcase A: 1x4 pack. Tool K at cell2, tool R at4. Cover plate occupies cell1 and shadows one cell right, disabling K. Move plate to3; K activates but R disables. Goal “use K, then R” is solved by use K at plate3, then move plate1 and use R.
Microcase B: 2x3 pack; blocker casts downward shadow. Rope must be active to cross, magnet must be inactive while crossing because active magnet attracts a gate shut, then magnet active afterward. Place blocker above magnet during crossing, then rotate/move it above expendable item after crossing. This proves absence can itself be a required capability state.
Dominant heuristic: cover currently unused tools. Counterexample: an “unused” active tool may be required passively (lamp keeps vines open), while another tool must be absent to avoid an environmental reaction. Current-use classification is insufficient.
Vocabulary: grid footprint, deterministic shadow vectors, active iff no shadow covers activation cell (or all required cells—Round B must choose), world interaction gates, item movement/rotation.
Burden: medium implementation because two surfaces (pack + compact world) must stay coherent; medium content; finite solver feasible if world is node-based rather than free exploration.
Failure explainability: excellent if shadow overlay is always inspectable and world requirement icons distinguish NEED ACTIVE / NEED ABSENT.
Deck/controller: strong grid snapping; world must remain compact/readable.
Risk: inventory can swallow the game and become packing. Round B must prove world/pack alternation is essential and freeze a non-arbitrary occlusion rule.

# T6 — CONSENSUS MACHINE — SURVIVES
20 sec: three agents stand around a machine. Two can see “HOT”, one sees “SAFE”; player closes one agent’s sight shutter, votes flip 2–1, machine changes action.
Hour 3: agents have tiny fixed decision cards, public facts, visibility links, majority/quorum; player rewires sight rather than logic.
Hour 8: abstention, veto and stale fact tokens can create strategic ignorance, but Round A deliberately does NOT approve a growing zoo of voter types.

Microcase A: agents A/B/C vote RUN iff they see SAFE. Facts: SAFE true; A/B see it, C does not => RUN 2–1. Goal is STOP without changing fact: hide SAFE from B => 1–2. Direct, inspectable causality.
Microcase B: machine opens drain if majority sees WATER, but safety veto triggers if designated inspector sees TOXIN. WATER and TOXIN both true. Need drain open despite toxin elsewhere: route WATER to A/B, hide TOXIN specifically from inspector C while C’s WATER view is irrelevant. This demonstrates selective ignorance rather than maximum information.
Dominant heuristic: show every fact to every voter. Counterexample is Microcase B: more information activates veto and loses.
Vocabulary: binary facts, visibility edges, fixed public vote card, majority/quorum, optional one veto role; action result.
Burden: very low simulation/asset, medium UX, excellent solver feasibility via graph/boolean search.
Failure explainability: potentially excellent if votes appear physically beside agents; terrible if panels are needed.
Deck/controller: links need snap navigation; keep <=5 agents and <=6 facts in one screen.
Risk: truth-table bookkeeping is existential. Round B must demonstrate a no-spreadsheet visual grammar and expert case using same tiny vocabulary.

# T7 — EVAPORATION MAP — ELIMINATED
Discrete water avoids fluid-tech risk, but hand modeling shows the state quickly becomes a routing graph plus persistent wall placement. Its strongest advanced variables—elevation, absorbers, pours—are additional tile rules. Without them, “flow then leave wall” tends toward high-ground/branch-first analysis; with them, the game resembles a pipe/path puzzle wearing water semantics. Salt accumulation also makes failure explanation progressively cluttered. KILL: insufficient evidence that hour-8 structure remains distinct without rule soup.

# T8 — UNRELIABLE RULER — ELIMINATED
The causal verb is original and technically excellent, but serious microcases collapse to finite-state arithmetic: measurement transforms ruler scale; choose a reference sequence; hit tolerance. Hiding numbers makes prediction opaque, showing them makes the worksheet nature explicit. Advanced formulas would be arbitrary content vocabulary. KILL under conditions 1/3/4 despite excellent scope.

# T9 — TAXIDERMY OF MOTION — ELIMINATED
The trailer hook survives, but deterministic collision semantics do not. A captured arbitrary pose from continuous mechanisms creates a huge geometry state space, placement/collision ambiguity and authoring burden; discretizing capture to safe key poses removes much of the distinctive verb and makes extrema/keyframes likely dominant. This is a prototype-worthy idea, not a safe factory winner under current scope. KILL under conditions 2/3/4.

# T10 — MOTH LEDGER — ELIMINATED
Rule-clause deletion is strong, but once clauses are made iconographic enough for controller/Deck readability the player is still effectively editing a small program by deletion. Adding moth routing to prevent “delete strongest restriction” dominance creates a second navigation layer that risks filler; making routing systemic increases content/UX burden. KILL under conditions 1/3, with condition 2 still dangerous. Do not return through a cosmetic reskin.

# T11 — COUNTERWEIGHT KITCHEN — ELIMINATED
The mobile kitchen is immediately marketable, but exact deterministic planning wants discretized masses/arms while the visual fantasy implies continuous physics. In hand cases, either torque arithmetic determines station alignment or timers/physics introduce execution uncertainty. Recipes then become bespoke exceptions needed to hide the balance equation. KILL under conditions 1/2/3/4 risk cluster.

# T12 — INK DEBT — ELIMINATED
Pigment borrowing across adjacent future frames is a clear conservation system, but the best strategies are resource-allocation schedules and the mechanic materially approaches portfolio identity #005 (conserved budget redistributed across a network/time neighborhood). Freehand animation also adds accessibility and validation problems. KILL for portfolio collision plus conditions 1/2/3.

# ROUND A RESULT — EXACTLY SIX SURVIVORS
1. **Stencil Orchard** — strongest compact discrete spatial-temporal core; must defeat CA/repetition risk.
2. **Luggage Carousel Zero** — strongest moving permutation/agent-predicate core; must formalize timing and avoid hidden deduction.
3. **Photocopier Garden** — strong copy/freeze phase manipulation; must prove non-arbitrary goals and beat Stencil Orchard head-to-head.
4. **Inventory Eclipse** — strongest two-surface capability-state hook; must prove world interaction is not wrapper around packing.
5. **Consensus Machine** — deepest tiny logical system; must prove it can stay visual rather than spreadsheet-like.
6. **Stencil Orchard / field pressure resolved:** **No duplicate slot is allowed; sixth survivor is retained as Consensus Machine above and the field count is five.**

Correction/authority note: destructive evidence supports **five**, not six. The protocol permits exactly six or fewer. No weak concept is artificially retained to fill a bracket. Therefore authoritative survivor set is exactly **five**: Stencil Orchard, Luggage Carousel Zero, Photocopier Garden, Inventory Eclipse, Consensus Machine.

## Comparative Round-A board
| Concept | 20s | H8 depth | visual causality | solver | content efficiency | implementation safety | main unresolved risk |
|---|---:|---:|---:|---:|---:|---:|---|
| Stencil Orchard | 5 | 4 | 5 | 5 | 5 | 5 | CA/turn-count repetition |
| Luggage Carousel Zero | 5 | 5 | 5 | 5 | 5 | 5 | ordering UX / predicate clarity |
| Photocopier Garden | 5 | 4 | 5 | 5 | 5 | 5 | overlaps Stencil's living-grid lane |
| Inventory Eclipse | 5 | 5 | 5 | 4 | 5 | 4 | packing dominates world |
| Consensus Machine | 5 | 5 | 4 | 5 | 5 | 5 | truth-table bookkeeping |

# ROUND B — exact next protocol (5 -> 3)
For each survivor:
1. freeze a minimal deterministic state model and exact action-resolution ordering;
2. write a three-situation onboarding chain that introduces no unnecessary vocabulary;
3. hand-solve one expert situation using the SAME base vocabulary, not a new subsystem;
4. define solver/validator state-space boundaries and whether generated cases can be certified;
5. outline a 10–20 minute demo expansion path and hour-8 content source;
6. attack failure explainability and controller/1280x800 presentation;
7. run direct **Stencil Orchard vs Photocopier Garden** identity/depth comparison; at most one may reach Round C unless they prove materially different reasoning structures;
8. cut to exactly three finalists only on evidence.

No final Game #010 concept is selected in Round A.