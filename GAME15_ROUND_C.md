# GAME #015 — PHASE 2 CONCEPT TOURNAMENT / ROUND C

Date: 2026-09-03
Status: ROUND C COMPLETE / WINNER SELECTED
Authority boundary: Game #015 only. Games #001–#014 remain exclusion/portfolio history, never canon.

## 0. Decision standard
Round C re-read the full active Game #015 authority and attacked the three finalists under the exact STATUS contract. Each candidate was reduced to a minimum rulebook, mapped to 24 cases (8 groups x 3), normalized as a CSP, given two late/capstone proof routes, tested against Check/undo brute-force incentives, content/certifier burden, first vertical-slice empirical gate, 10-second communication, 20-minute demo strength, portfolio collision, and its candidate-specific failure mode.

A finalist only wins if embodiment adds a durable human reasoning layer rather than decorating finite assignment/search.

Fresh market/collision refresh performed 2026-09-03. Relevant references are market evidence only:
- Spray Paint Simulator (2025) occupies freeform spray/restoration and includes masking of surfaces/objects; this strengthens the requirement that the selected concept is *not* a spraying simulator and that spray input is a discrete commit over an already-arranged mask state.
- Masking Print (KAYAC, 2020) uses masks plus paint order to reproduce shirt designs, demonstrating that flat mask/order puzzles are occupied territory; Game #015 must remain about 3D reusable objects as masks, persistent face exposure histories, self-obligated mask objects, and rearrangement between passes.
- Tag: The Power of Paint and other paint games use paint as traversal/property mechanics and do not collide with the retained grammar.
- Exact-name searches did not surface a dominant game titled `Fresh Coat`; nevertheless the title remains working/provisional until later commercial/title verification.

## 1. FINALIST A — FRESH COAT

### Minimum rulebook — frozen for tournament comparison
1. A case contains 2–5 chunky rigid orthogonal solids with authored semantic face-regions.
2. Objects may occupy only authored discrete sockets and legal 90-degree poses.
3. A booth has a small fixed set of orthographic spray directions; there is no free aim.
4. `SPRAY coat_id` paints exactly the face-regions currently exposed to that booth direction. Occluded regions receive nothing.
5. Paint history is persistent and ordered per semantic face-region: raw, A, B, A->B, etc.
6. Between authored spray passes, a case may allow a bounded rearrangement action. There is never unconstrained continuous packing.
7. Every physical object can simultaneously be a mask and have its own final paint obligations.
8. Final truth is expressed only through exact face-region history predicates and object final-placement predicates if explicitly authored.
9. Undo/reset are unlimited. No real-time pressure, lives, consumable Check, or hidden physics.
10. Current-state inspection may reveal what is exposed *now* and actual accumulated paint history, never counterfactual best placements or future-solution heatmaps.

Optional mechanics are excluded at this stage: freehand spraying, fluid paint, partial coverage percentages, arbitrary mesh sculpture, physics stacking, paint consumption economy, cleaning, solvents, stickers/tape, NPC jobs, workshop upgrades.

### 24-case campaign — 8 groups x 3
Each group must earn a new reasoning family; case 2/3 deepen interaction rather than only add objects.

**F1 — Occlusion is a mask**
- FC01: one block protects one face of another.
- FC02: rotate the protected object; same masker now protects a different semantic region.
- FC03: masker itself has one face that must be painted, introducing self-obligation.
Reasoning family: direct exposure complement.

**F2 — Protected neighbor**
- FC04: one face must paint while adjacent face remains raw.
- FC05: two candidate maskers differ in which neighbor leaks exposure.
- FC06: one orientation satisfies the protected neighbor but creates a later accessibility debt.
Reasoning family: local differential masking, not whole-object cover.

**F3 — One object, two jobs**
- FC07: masker must meet its own A-only target.
- FC08: same masker protects object X while being protected by object Y.
- FC09: mask dependency chain of length two; solve from terminal paint obligations backward.
Reasoning family: masks are constrained resources, not disposable blockers.

**F4 — Pass-specific exposure**
- FC10: A-only vs B-only introduced with one rearrangement.
- FC11: raw + A-only + B-only on one object.
- FC12: first arrangement must intentionally leave a region for later access.
Reasoning family: exposure schedule across passes.

**F5 — Ordered history**
- FC13: A->B introduced alongside A-only.
- FC14: A->B and B-only are adjacent, forcing asymmetric masking across passes.
- FC15: one region requires A->B while another must stay raw through both passes.
Reasoning family: same final color is insufficient; provenance/order matters.

**F6 — Cavity reveal**
- FC16: cavity face is initially unreachable and becomes exposed after rearrangement.
- FC17: opening cavity for B would also expose a protected rim.
- FC18: object orientation must remain while a different object moves to alter cavity exposure.
Reasoning family: rearrangement changes visibility topology without adding a new rule.

**F7 — Mask-role reversal**
- FC19: X masks Y on A; Y masks X on B.
- FC20: both objects also carry own-history targets.
- FC21: three-object cycle where only one role ordering avoids contaminating a protected face.
Reasoning family: temporal allocation of masking roles.

**F8 — Coupled mask chain / capstones**
- FC22: two independent-looking paint obligations share one critical mask socket.
- FC23: four objects; one masker serves two objects in different passes and has its own B-only face.
- FC24: four objects, two sprays, one rearrangement; protected raw, A-only, B-only and A->B regions coexist, with a cavity and role reversal. No new mechanic.
Reasoning family: combine the learned exposure-history graph into one compact spatial proof.

### Normalized CSP and embodiment test
Certification model can normalize a state as:
`(object -> socket/pose assignments at each authored arrangement stage, per-region ordered coat history)`.
A spray is a deterministic exposure-set transform. Therefore an abstract solver can view the game as satisfying exposure-history predicates over assignment stages.

The critical question is whether the player also experiences it merely as set partitioning. Round C verdict: **NO, if four constraints are enforced**:
1. exposure sets are not displayed as abstract lists;
2. pieces are simple enough that occlusion can be predicted spatially;
3. the same object has obligations as both target and mask, coupling partitions through physical pose;
4. rearrangement changes which surfaces exist in line-of-sight, so the player reasons about temporary physical configurations, not choosing prewritten subsets.

Embodiment therefore supplies a legitimate reasoning operation: mentally tracing exposed/covered faces and using constrained objects as temporary masks. The solver representation is finite, but the human representation is not arbitrary finite assignment.

### Capstone proof route A — FC21 mask-role reversal
Target: X.top = A-only; X.side = B-only; Y.front = A->B; Y.back = raw; Z.top = B-only.
1. Because Y.back must remain raw, every A-stage pose exposing Y.back is eliminated. This removes the apparent orientation where Y directly shields X.side.
2. X.top needs A, but X.side must avoid A; among remaining A-stage relations only Z can cover X.side while leaving X.top exposed. This fixes Z as X's first-pass masker and eliminates all Y-as-mask A-stage classes.
3. Y.front needs A and later B, so Y must itself be exposed to A while its back is hidden; the only compatible socket puts X behind Y. Thus X masks Y.back while Z masks X.side.
4. After A, X.side needs B and Z.top needs B, so Z must vacate the shielding socket. Y.front must also receive B, while Y.back stays hidden. This forces role reversal: Y moves to shield X's already-correct A-only top while exposing X.side, and X's body continues to shield Y.back.
Residual choice is a harmless symmetry between two equivalent parking sockets. Three major configuration classes are eliminated before any trial.

### Capstone proof route B — FC24 cavity / double-history
Target includes: P.cavity = B-only; P.rim = raw; P.outer = A->B; Q.top = A-only; R.side = B-only; S.front = raw.
1. P.rim raw means no legal stage may aim an unblocked booth ray at the rim. This immediately eliminates every A-stage arrangement where P's cavity faces the booth and every B-stage plan that rotates P to open it.
2. P.outer needs A->B while cavity is B-only. Therefore A must see P.outer but not cavity; only Q's wide slab pose can cover the cavity mouth without covering outer. This fixes Q as A-stage masker and rules out R/S substitutes.
3. Q.top is A-only, so Q must be exposed during A but hidden during B. The B-stage cannot simply remove Q into a free exposed socket.
4. Since P may not rotate for B, cavity access must be created by moving Q away. R.side needs B, so R takes Q's old masking lane, where its geometry blocks P.rim but leaves the cavity aperture visible. This simultaneously hides Q.top behind S.
5. S.front raw removes the remaining mirror arrangement because that mirror exposes S to B. One B-stage class remains modulo equivalent object ordering.
Again the solve is driven by visible spatial obligations before residual execution.

### Brute-force / Check design
- No separate Check button during arrangement. The game continuously shows only factual current state: current exposure preview and already-applied coat histories.
- `SPRAY` is the meaningful commit. Before spraying, the player can inspect current exposure; after spraying, result is permanent within the branch but unlimited Undo is available.
- Final validation occurs after the authored last spray/unpack action.
- Undo returns immediately to prior arrangement/state and is never penalized.
This makes experimentation pleasant without enabling a rapid `try assignment -> Check oracle -> repeat` loop. A spray gives rich consequence, not a binary clue.

### Content / certifier burden
Target object vocabulary: 6–8 reusable chunky solids; 5–7 socket-frame motifs; 2–3 booth directions; 2 base coats for campaign, optional third only if later proof requires it (not assumed now). Semantic face subdivision should stay coarse.

Certifier burden is favorable: precompute exact region exposure per `(scene arrangement, booth direction)`, enumerate only authored compatibility graphs, normalize equivalent arrangements under object/socket symmetry, verify at least one solution, verify intended difficulty proxies, and reject campaign pairs with isomorphic normalized exposure/dependency signatures.

### First vertical-slice empirical gate
Build only as a future implementation gate, not factory production: FC01, FC05, FC10, FC14, FC18, FC21 using 4 reusable solids. Test with fresh players whether, before committing spray, they can correctly predict >=80% of exposed semantic regions after onboarding and can explain failures in terms of physical masking/history rather than random placement. Four-object scenes fail the gate if players routinely need hidden exposure-list UI or rotate camera hunting to understand what is covered.

### 10-second communication
Silent clip:
1. show three plain blocks with tiny final-pattern cards;
2. stack them;
3. hit one giant `SPRAY A` commit and visibly coat only exposed surfaces;
4. rearrange one block, `SPRAY B`;
5. explode/unpack the stack to reveal different hidden face histories matching targets.
Input -> surprising consequence -> goal is visible without rules text.

### 20-minute demo finale
7-case demo can end around FC10/FC13 hybrid: two passes, one rearrangement, one self-obligated mask, raw + A-only + B-only + A->B. It uses no demo-only mechanic and provides the satisfying unpack reveal.

### Special attack: set-partition collapse
If content is authored by directly choosing arbitrary required exposure subsets and selecting whichever object/socket realizes them, the game will become disguised set partition. Required countermeasures are now tournament gates:
- every late case needs at least one self-obligated masker;
- every group after F3 needs a mask-dependency edge or rearrangement dependency, not independent face classes;
- the certifier records normalized exposure/dependency graph and rejects isomorphic duplicates;
- no case may be solved purely from a printed exposure matrix because no such matrix is player-facing;
- content authoring begins from spatial object relations/occlusion motifs, then derives targets, rather than inventing target subsets first.

### Special attack: 4-object readability
Four objects are allowed only with fixed sockets, chunky silhouettes, stable camera, selectable ghost outline, object isolation inspection, and semantic face badges. The normal simultaneous visible set should be <=4; five is an exceptional authoring ceiling, not a target. If implementation testing needs constant x-ray or exploded oracle view, the affected case is rejected.

### Round-C verdict
**PASS — strongest finalist and selected winner.**

---

## 2. FINALIST B — MISALIGNED (INTERNAL LABEL) — KILL

### Minimum rulebook
2–4 rigid coarse print plates; 5–9 discrete transforms each; composite truth = exact per-region set of contributing plate IDs; required/forbidden provenance targets; no knockout, paint physics or continuous nudging; unlimited undo; factual exploded-layer inspection only.

### 24-case attempt — 8 groups x 3
M1 anchor singles; M2 protected paper; M3 distant rigid coupling; M4 pair overlaps; M5 triple overlaps; M6 hidden-region inference; M7 competing anchors; M8 decoy symmetry/capstones.

The ladder is feasible, but groups M3–M8 repeatedly reuse the same operation: infer one plate transform from source/target incidence, then propagate overlap constraints to the next plate. Triple overlap and hidden witness feel harder, but they do not create enough new human reasoning families.

### Normalized CSP
For each plate p choose transform `t_p` from a finite domain. Every semantic target region constrains the subset `{p | transformed_plate(p,t_p) covers region}`. This is a textbook finite-domain constraint problem over rigid transforms.

The embodied printshop presentation improves legibility but does not add a second-order reasoning action: once plate-source islands are visible, the human effectively performs transform-domain elimination. That is exactly the same normalized object the certifier enumerates.

### Capstone proof route A
K-only anchor removes 7/9 K transforms; protected region removes one remaining transform; K+M distant witness removes all but two M transforms; second witness fixes M; triple region constrains Y. This is good deduction, but it is still transform-domain pruning.

### Capstone proof route B
Two disconnected C islands must land in C-only and C+M regions, fixing C; paper-protected strip fixes M orientation; a triple-overlap island fixes Y. Again three class eliminations occur, but every step is `source feature -> allowable transform`.

### Brute-force / Check
Removing a binary Check helps, but 3 plates x 9 transforms is only 729 tuples and four plates is 6,561. A player can manually cycle transforms while watching factual composite changes, especially on controller. Preventing this would require hiding useful feedback or artificially increasing transform counts, both bad.

### Content/certifier burden
Extremely low implementation burden and easy generation, but that is also the warning sign: producing many mathematically distinct transform graphs is easier than producing cognitively distinct puzzles. A graph-isomorphism gate can remove duplicates yet is unlikely to create 24 qualitatively fresh cases.

### Vertical-slice empirical gate
Six cases would test whether players infer transforms or simply cycle them. The hypothesis is unfavorable enough that the factory should not spend the slot on this experiment while Fresh Coat already survives more strongly.

### Communication/demo
Excellent GIF and compact demo. However flat mask/order territory also has a direct adjacent reference in Masking Print, increasing derivative risk unless deeper mechanics are added; adding them would be rule inflation.

### Special attack: transform enumeration/repetition
**FAILED.** Enumeration remains both a certification method and an attractive human strategy; the 24-case ladder mostly changes constraint density, not reasoning family.

### Title
`Misaligned` is already occupied and could not ship under that label, but naming is irrelevant after mechanical kill.

### Round-C verdict
**KILL — elegant finite transform CSP with insufficient second-order embodiment.**

---

## 3. FINALIST C — BEFORE IT DRIES — KILL

### Minimum rulebook
Coarse stroke masks on discrete sockets; each stroke has pigment/provenance, wet-life integer, position/orientation; one committed move per beat; moved wet donor transfers deterministic contact band under universal rules; wet counters decrement after each action; dry strokes lock; exact protected/provenance targets; no real-time timing/fluid simulation.

### 24-case attempt — 8 groups x 3
B1 contact before dry; B2 protected negative space; B3 competing receivers; B4 provenance relay; B5 deliberate drying/inert donor; B6 precedence fork; B7 movement changes contact graph; B8 two coupled provenance chains.

This ladder has more variety than Misaligned, but groups B1/B3/B5/B6 repeatedly resolve to action deadlines and partial-order scheduling, while B4/B7/B8 add the geometry/provenance layer that makes the game interesting. The temporal counter remains structurally central.

### Normalized CSP
A state is `(stroke poses, wet-life counters, accumulated provenance masks)`. Each action advances global discrete time, changes one pose, applies contact-transfer effects, and reduces future action domains. Abstractly this is finite-horizon planning with deadlines and stateful spatial side effects.

Embodiment does add useful contact geometry, so this is not merely permutation. But Round C asks which mental model dominates late play. When wet-life values differ, the first question becomes `what must happen by beat k?`; geometry then decides which scheduled contact is feasible. That is disguised scheduling more often than desired.

### Capstone proof route A
Protected gap kills A-before-B at socket S; C needs B-derived pigment before B locks, forcing B move on beat 1; contact geometry fixes B target socket; beat 2 must relay B->C. This is readable, but the decisive chain is deadline propagation.

### Capstone proof route B
D can only receive transferred A-provenance from C; C must first receive from B; B dries after beat 2; protected region forbids B's direct route to C from its initial socket; therefore beat 1 repositions B, beat 2 transfers B->C, beat 3 transfers C->D. Three history classes disappear, but they disappear chiefly because of temporal deadlines.

### Brute-force / Check
No Check spam is necessary because every move itself advances the timeline and produces visible consequences. Undo is required. This is robust.

### Content/certifier burden
Moderate: deterministic masks and exhaustive histories are manageable, but authoring proof-carrying cases with non-isomorphic contact DAGs is harder than Fresh Coat and more vulnerable to accidental softlocks/unintended provenance paths.

### Communication/demo
The wet-stroke transfer is visually attractive, but a 10-second silent clip needs wetness counters/icons to explain why a move is legal now and illegal later. Fresh Coat communicates its core consequence more immediately. A 20-minute demo can work but would likely emphasize countdown-style planning.

### Special attack: disguised scheduling
**FAILED at product-identity level.** Contact/provenance is meaningful, but the universal wet-life countdown makes scheduling the reliable dominant framing in harder cases. Removing differing wet lives weakens the concept; hiding them makes it opaque; adding more spatial transfer rules is rule inflation.

### Round-C verdict
**KILL — good puzzle system, but late-game identity drifts toward deadline scheduling rather than contact/provenance.**

---

## 4. Final comparison

| Criterion | Fresh Coat | Misaligned | Before It Dries |
|---|---|---|---|
| Human reasoning beyond certifier CSP | **Strong** spatial occlusion + constrained masker obligations | Weak/moderate transform-domain elimination | Moderate contact geometry, but deadline planning dominates |
| 24-case qualitative ladder | **Credible 8-family ladder** | Repetition by transform pruning | Credible but several families are scheduling variants |
| Brute-force attraction | Low/moderate; spray is rich commit | **High** due tiny transform domains | Low/moderate due timeline consequence |
| Failure readability | **Excellent** after unpack/history | Excellent | Good, more timeline/provenance UI needed |
| 10-second hook | **Excellent** stack -> spray -> unpack | Excellent | Good |
| 20-minute same-rules demo | **Excellent** | Excellent | Good |
| Authoring/certifier ratio | **Strong** | Excellent but shallow risk | Moderate |
| Controller/handheld | **Excellent** | Excellent | Excellent |
| Candidate-specific attack | **Survives with explicit gates** | Fails enumeration/repetition | Fails scheduling dominance |
| Portfolio collision | Clear | Clear | Clear |

## 5. WINNER

**Selected Game #015 concept: FRESH COAT (working title).**

Canonical reason: it best combines an immediately legible physical transformation with a human reasoning representation that is meaningfully different from the certifier's finite CSP. The player reasons about temporary 3D occlusion, constrained physical objects serving as masks, and persistent exposure history. The 24-case ladder can earn new reasoning families without adding minigames, timers, freehand precision or production-heavy simulation.

This selection does **not** freeze all details from the tournament. Only the minimum rule identity and constraints needed to select the concept become inputs to Phase 3. Phase 3 owns the formal product thesis.

PHASE 2 = COMPLETE
DESIGN COMPLETE = NO

## NEXT ACTION
Proceed to Game #015 Phase 3 Product Thesis Lock. Freeze target player, platform, genre framing, one-sentence hook, fantasy, session structure, core loop, differentiator, scope ceiling, explicit non-goals, demo promise and empirical gates. Do not begin production implementation.