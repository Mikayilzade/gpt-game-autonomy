# GAME #015 — PHASE 2 CONCEPT TOURNAMENT / ROUND B

Date: 2026-09-02
Status: ROUND B COMPLETE / 3 ROUND-C FINALISTS / NO WINNER
Authority boundary: Game #015 only.

## Method
All five Round-A survivors were forced into the same bounded architecture: discrete transforms, deterministic state, six concrete cases, explicit stress-state estimate, human-proof route, normalized repetition signature, ~24-case content path, demo arc, controller/non-color check, and common score matrix. Certification enumeration is allowed for tooling; a candidate fails when enumeration is also the dominant human play.

Fresh exact-name/mechanic search was repeated before decisions. No search result invalidated the retained mechanics, but two naming/commercial notes matter: `Misaligned` is already used by a 2023 Steam shooter and a March-2026 30-level puzzle, so it is not a viable shipping title; `Spray Paint Simulator` (2025, with 2026 DLC) occupies satisfying freeform spray/restoration, making Fresh Coat's differentiator specifically *objects as reusable physical masks plus persistent multi-pass exposure history*, not spraying itself.

---

## A. WRONG SCALE — KILL IN ROUND B

### Exact state
A case has objects O, fixed measurement domains D, legend tokens L with exact rational scale factors, discrete legend sockets, containment edges, and interface predicates. A state is `(legend->socket permutation, inherited-domain assignment induced by containment)`. No free resizing or perspective rule exists.

### Six-case ladder
1. Tutorial: swap 1:1 / 2:1 legends so a key fits one lock.
2. Early A: one legend controls both crate and contained part; only scaling the hatch preserves containment.
3. Early B: two mating faces need equal world-size although nominal sizes differ.
4. Mid A: nested object crosses a domain boundary; containment inheritance rules eliminate two apparent swaps.
5. Mid B: shared shaft must fit two bearings in different domains, forcing a ratio chain.
6. Stress: 5 legends/sockets, two nested assemblies, three shared interfaces and one transport clearance.

### Stress space / blind trial
5! = 120 top-level legend permutations; induced containment is deterministic. Even 6! = 720 is tiny. Increasing sockets mainly raises permutation count, not reasoning quality. A human can spam swaps/checks unless Check is artificially rationed. Rationing Check would hide the weakness rather than solve it.

### Four pressures attempted
Ratio-chain compatibility; containment inheritance; shared-domain coupling; clearance-before/after transfer. These are genuinely distinct presentations, but all ultimately constrain the same legend permutation.

### Human-proof mid route
For Mid B: (1) shaft/bearing A equality eliminates every legend pair except ratios {1:2,2:4}; (2) bearing B equality fixes which member of that pair owns the shaft domain; (3) containment clearance removes one remaining socket swap. This is readable deduction, but it is still permutation constraint propagation.

### Repetition signature / 24-case path
Normalized signature = factor-domain bipartite graph + containment edges + equality/inequality interface predicates. A 24-case campaign would require increasingly ornate physical stories around a narrow assignment grammar. New qualitative families quickly require adding new scale laws, which is parameter inflation.

### Assets / demo
Reusable: 8–12 miniature workshop props, domain frames, legends, interface glyphs. Demo could teach key -> containment -> ratio chain in six cases. Very strong GIF and controller path; numeric ratios plus shape cues are accessible.

### Special attack conclusion
It is clearly *not* Superliminal-lite when legends remain causal tokens and perspective never resizes anything. But the stricter version exposes the deeper problem: it is a compact legend-permutation CSP. **KILL.** Market hook cannot compensate for hour-3 grammar collapse.

---

## B. BEFORE IT DRIES — PASS TO ROUND C

### Exact state
Board uses coarse cells/sockets. Stroke i has immutable pigment identity, footprint mask, current socket/orientation, wet-life integer `w_i`, and accumulated pigment/provenance mask. One committed action is `move one currently movable wet stroke to a legal socket/orientation`; all positive wet-life counters then decrement. Contact transfer is directional: moved donor transfers its defined contact band into overlapped receiver cells if both rule preconditions hold. Dry strokes lock spatially and no longer donate; they may remain receivers only where the universal material rule permits. State stores exact per-cell pigment layers/provenance, not fluid simulation.

### Six-case ladder
1. Tutorial: one wet donor, one receiver; move before donor dries.
2. Early A: preserve a white gap; obvious contact contaminates it.
3. Early B: donor has two candidate receivers but only one can receive before its own lock state.
4. Mid A: transfer creates a secondary donor region; provenance target forces which contact occurred first.
5. Mid B: three strokes form a precedence fork: either branch seems legal, but protected negative space eliminates one entire order class.
6. Stress: 5 strokes, wet lives {1,2,2,3,3}, 3 sockets each average, one move maximum per beat, 2 protected regions, target requires three provenance classes and one deliberately unused contact.

### Stress space
Loose upper bound ignoring early locks: about `5! * 3^5 = 29,160` move/socket assignments; legal wetness and collision constraints reduce it sharply. Unlike Wrong Scale, a move changes geometry, pigment state and future legality, so states are not mere permutations.

### Four distinct pressures
1. deadline/precedence from wet-life;
2. geometric contact opportunity;
3. contamination avoidance / protected negative space;
4. provenance chains where a transferred region later acts differently from original pigment.
A fifth optional pressure is deliberate drying as a way to make a formerly dangerous donor inert; it uses the same rule rather than a new subsystem.

### Human-proof Mid B route
Target region R must contain pigment from B but protected gap G must remain raw. (1) Any class where A contacts B before A leaves socket S creates A-provenance in G, eliminating all A->B-first histories. (2) C needs B-derived pigment, so B must receive before B's final movable beat; this eliminates histories that spend beat 1 moving C. (3) With those classes removed, B must receive from A at socket T on beat 1, then contact C on beat 2; remaining choice is only which harmless final parking socket A occupies. Three state classes die from visible target/provenance facts before residual execution.

### Repetition signature / 24-case path
Signature = normalized contact-opportunity graph + wet-life partial order + protected-region obligations + provenance dependency DAG. Credible 24-case families: single deadline; protected gap; competing receivers; provenance relay; deliberate dry/inert barrier; precedence fork; geometry changes contact graph; two independent chains that couple through one socket. Each family can have 3 cases without renaming pigments as fake novelty. Hard gate: no shipping pair may be isomorphic under pigment relabel + board symmetry + precedence-DAG equivalence.

### Assets / authoring
Very low bespoke art: 5–7 broad stroke silhouettes, 3 substrate materials, socket/lane motifs, pigment textures. Authoring burden moderate because each case needs exact contact masks and proof-carrying route; certifier can exhaust discrete action histories.

### Demo arc (20–25 min)
6 cases: transfer -> drying lock -> protected gap -> competing receiver -> first provenance relay -> small precedence fork. Same rules as full game; no demo-only mechanic.

### Input/accessibility
Socket navigation, rotate if allowed, commit, undo/reset, inspect. Pigments always carry hatch/symbol IDs; wetness has icon + outline state + integer pips; reduced motion replaces smears with deterministic before/after wipes.

### Round-B verdict
**PASS.** Geometry/provenance facts can eliminate whole action-order classes; sequence matters but is not the sole reasoning object. Main Round-C risk: the wet-life counter can still feel like a scheduling puzzle unless provenance relay and contact geometry remain dominant.

---

## C. FRESH COAT — PASS TO ROUND C / CURRENT STRONGEST PRODUCTION RATIO

### Exact state
A case contains 2–5 rigid orthogonal solids represented by authored face IDs, fixed arrangement sockets, legal 90-degree poses, and fixed booth spray directions. A spray action computes exact exposed face-regions by deterministic orthographic ray/face occlusion; exposed regions append coat ID to persistent ordered paint history. Between passes, only authored rearrangement operations are legal. Final target predicates operate on face-region coat histories: raw, A-only, B-only, A-then-B, protected, etc. No freeform spray aiming.

### Six-case ladder
1. Tutorial: stack two blocks; one covered face stays raw after A.
2. Early A: rotate one block to protect adjacent face while exposing top.
3. Early B: three objects; one object is a mask for another and must itself meet a paint target.
4. Mid A: spray A, one rearrangement, spray B; target includes A-only, B-only and raw.
5. Mid B: nested cavity creates exposure that appears only after the first rearrangement; one face requires A->B while neighbor requires B-only.
6. Stress: 4 solids, 5 arrangement sockets, 4 poses each where legal, exactly 2 sprays and one rearrangement; 18 semantic face-regions, 6 target-history classes, one object must mask two different objects in different passes.

### Stress space
A deliberately loose arrangement upper bound is `(5*4)^4 = 160,000` poses per arrangement; two arrangements would be huge if unconstrained, so authoring must use compatibility/socket graphs and indistinguishable-state collapsing. Typical certified case target: <=20k legal first arrangements and <=150 legal rearrangements from any first arrangement, with pruning by target exposure obligations. Human play sees physical occlusion, not this state count.

### Four distinct pressures
1. protect a region from every pass;
2. expose a region on exactly one pass;
3. ordered history A->B versus B-only/A-only;
4. use an object that itself has final paint obligations as a temporary mask;
5. rearrangement creates/deletes cavities and therefore future exposure.
These arise from one exposure-history grammar.

### Human-proof Mid B route
Face X needs A->B, face Y (adjacent on same object) needs B-only, cavity face Z must stay raw. (1) Any first arrangement exposing Y is impossible, eliminating all poses with Y facing A booth. (2) X therefore must face A while Y is occluded; only the large mask object can cover Y without covering X, eliminating all arrangements using the small mask. (3) Z raw forbids the apparent post-A rotation that opens the cavity toward B, leaving the rearrangement class where the painted object stays posed and the large mask moves away. Only harmless placement symmetry remains. This is spatial deduction before trial.

### Repetition signature / 24-case path
Signature = per-pass exposure-obligation hypergraph + mask-object dependency graph + rearrangement transition class + ordered coat-history predicates. Credible eight 3-case families: single-mask basics; self-obligated mask; protected neighbor; pass-specific exposure; ordered double coat; cavity reveal; mask-role reversal across passes; coupled two-object mask chain. Repetition gate compares normalized exposure/dependency graphs, not meshes/colors.

### Assets / authoring
6–8 chunky reusable solids (cuboid, L, U/cavity, slab, stepped block), modular booth/sockets, 3 coat materials. Visual payoff is high while art burden is low. Exact semantic face regions avoid texture-pixel truth. Authoring needs socket compatibility and exposure precompute; far cheaper than arbitrary 3D packing.

### Demo arc (20–25 min)
7 cases: basic masking, rotate, protected neighbor, object-as-mask-with-own-target, second coat, one rearrangement, finale requiring A->B plus protected face. Demo can end on satisfying unpack reveal.

### Input/accessibility
Controller excellent: object -> socket -> pose; spray is explicit commit. Coat classes use color + texture/pattern + layer-order badges. Current-exposure preview may show only what the nozzle can physically see now; it must not preview counterfactual placements or solve future passes.

### Market/collision note
Current `Spray Paint Simulator` markets precision spraying, masking and restoration. Fresh Coat therefore must never sell itself as a spray simulator. Its hook is: **stack ordinary objects as masks, paint the pile, rearrange once, then unpack the hidden paint history.** That remains materially different.

### Round-B verdict
**PASS.** Best combination of visual hook, explainable failure, deterministic certification, bounded art, and multiple same-rule reasoning families. Round C must attack whether exposure histories secretly normalize to set partitions and whether face-level readability survives 4-object scenes.

---

## D. PARALLAX BUREAU — KILL IN ROUND B

### Exact state
2–5 extruded contour fragments occupy fixed depth/X rails with discrete sockets/rotations. 2–4 canonical cameras render exact ID/silhouette buffers. Targets use semantic contour predicates (component count, closed loop, stem/notch side, required contributor IDs), never fuzzy pixel similarity.

### Six-case ladder
Tutorial circle from two fragments / two cameras; early shared fragment; early occlusion conflict; mid three cameras; mid contributor-hidden-in-one-view; stress five fragments/four cameras with 4 sockets x 4 poses average.

### Stress space
Loose bound `(4*4)^5 = 1,048,576` scene assignments before collision pruning. Enumeration is feasible offline, but authoring useful target sets requires searching a large scene space and then checking whether each camera image is human-readable.

### Four pressures
shared contour reuse; viewpoint-specific occlusion; contributor visibility; negative-space topology. On paper these differ.

### Human-proof route attempt
Camera A closed-loop target forces fragments P/Q to overlap in one depth relation; Camera B notch-right excludes Q's rear socket; Camera C required contributor R fixes its rotation. This gives three eliminations, but the player must judge projected contour consequences across cameras. To make those consequences exact, UI needs contributor/highlight inspection; too much inspection approaches an oracle, too little makes reasoning mental-3D trial.

### Repetition / content burden
Signature = camera-feature-to-piece contribution hypergraph + occlusion order. 24 non-isomorphic cases are theoretically possible, but every case also needs silhouettes that remain recognizable, attractive and readable from all cameras. That couples puzzle generation to visual design far more tightly than the other finalists.

### Demo / input/accessibility
Camera switching and socket moves are controller-safe; non-color is fine. A demo can look spectacular. The problem is not controls but target semantics: coarse predicates make the target feel like a checklist rather than “make this image”; rich images reintroduce pixel/contour ambiguity.

### Special attack conclusion
Exact/readable target matching and bounded authoring cost pull in opposite directions. The design can be made deterministic, but doing so strips part of the intuitive visual promise and leaves a high authoring/QA burden. **KILL.** Strong trailer idea, weaker small-team production ratio.

---

## E. MISALIGNED — PASS TO ROUND C, SHIPPING TITLE MUST CHANGE

### Exact state
A case has 2–4 coarse vector/cell print plates, each with immutable plate ID/ink texture, finite transform set (small translations, optional 90-degree rotation), and fixed registration pins. Composite truth is exact region provenance: which subset of plates covers each semantic region. Optional knockout is excluded for now; it is not needed to prove depth. Final target predicates require/forbid provenance classes and protected paper.

### Six-case ladder
1. Tutorial: two plates, one shift; create C-only / M-only / C+M regions.
2. Early A: protected paper eliminates the visually obvious alignment.
3. Early B: one plate alignment must explain two separated overlap regions.
4. Mid A: three plates; a region hidden inside triple overlap is inferred from same plate's exposed witness elsewhere.
5. Mid B: plate has a distinctive disconnected source island; target provenance couples distant regions and fixes transform without nudging.
6. Stress: 4 plates, each 9 legal transforms, 16 semantic regions, required singles/pairs/triple plus 3 protected regions.

### Stress space
`9^4 = 6,561` transform tuples before symmetry/collision normalization: small for certification and dangerously small for blind checking. Shipping UX therefore cannot reward rapid Check spam; more importantly, cases must expose deductions that fix plate transforms from multiple separated provenance witnesses. Increasing transform count is forbidden as fake depth.

### Four distinct pressures
1. single-plate provenance anchors;
2. forbidden-overlap/protected paper;
3. distant-region coupling by one rigid plate transform;
4. hidden provenance inferred from exposed witness regions;
5. pair/triple overlap compatibility.

### Human-proof Mid B route
Target region A is K-only and region D is K+M; the only K source island capable of A fixes K's translation class. (1) This eliminates 7/9 K transforms at once. Protected region P rules out one of the two remaining K rotations. (2) K is fixed. D then requires M coverage while target E must remain M-free; among M transforms, all but two violate E. (3) A second K+M witness F removes one of those two. Y plate then has only residual symmetry. The solve is provenance deduction, not visual nudging.

### Repetition signature / 24-case path
Signature = rigid-source-region incidence graph + required provenance hyperedges + forbidden-region constraints + transform-group symmetry. Credible families: anchor singles; protected paper; distant rigid coupling; pair overlap; triple overlap; hidden-region inference; competing anchors; decoy symmetry. Three cases each is plausible, but a strict graph-isomorphism repetition gate is mandatory.

### Assets / authoring
Excellent ratio: vector plates, paper, registration pins, 4 ink textures. Content can be generated/filtered then art-directed. Exact polygon/cell boolean truth is easy to test.

### Demo arc (15–20 min)
7 compact prints: shift -> protected paper -> distant witness -> third plate -> pair overlap -> hidden inference -> small three-plate finale. Very low tutorial burden.

### Input/accessibility
Controller/pointer both strong; transform snapping only. Every ink is texture + symbol + color; exploded plate view shows actual source geometry but no suggested transform. Coarse semantic regions prevent pixel hunting.

### Market/naming note
`Misaligned` is already a Steam game title and also the name of a 2026 pure puzzle. Keep only as internal candidate label; a winner requires a new title search.

### Round-B verdict
**PASS.** The provenance route is stronger than “nudge until it looks right.” Main Round-C risk: 6,561-ish spaces make Check-spam viable and the grammar may still feel like repeated overlay CSP unless hidden-provenance and rigid distant coupling sustain novelty.

---

## Common score matrix (10 = best; collision risk score means LOW collision is high score)

| Candidate | Hook | Human reasoning | Hour-3 depth | Readability | Certification | Content factory | Production ratio | Demo | Low collision risk | Total /90 | Decision |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---|
| Wrong Scale | 10 | 6 | 4 | 9 | 10 | 5 | 8 | 9 | 5 | 66 | KILL |
| Before It Dries | 9 | 8 | 8 | 8 | 8 | 8 | 8 | 9 | 9 | 75 | ROUND C |
| Fresh Coat | 10 | 9 | 9 | 10 | 9 | 9 | 10 | 10 | 8 | 84 | ROUND C |
| Parallax Bureau | 10 | 7 | 7 | 6 | 7 | 5 | 5 | 10 | 7 | 64 | KILL |
| Misaligned | 8 | 9 | 8 | 9 | 10 | 8 | 10 | 9 | 7 | 78 | ROUND C |

Scores are comparative decision aids, not evidence by themselves.

## Round-B survivors
Exactly three advance:
1. **Fresh Coat** — strongest current production ratio and physical reasoning readability.
2. **Misaligned** *(internal label only)* — strongest low-cost exact provenance deduction.
3. **Before It Dries** — strongest temporal/spatial transformation, with scheduling-collapse risk still open.

Killed: `Wrong Scale`, `Parallax Bureau`.

## Round-C contract
Do not select by score alone. Run one final destructive comparison using a shared 24-case campaign skeleton and explicit anti-bruteforce policy.

For each finalist:
1. define the minimum rulebook with no optional mechanics;
2. map 24 candidate cases into 8 x 3 progression groups and show which new reasoning family each group earns;
3. construct at least two late/capstone proof routes with >=3 class eliminations before residual trial;
4. normalize the underlying CSP and ask whether the physical presentation adds reasoning or merely hides it;
5. define Check/undo/inspection so blind enumeration is not encouraged without artificial punishment;
6. estimate authoring + certifier complexity and identify the first vertical-slice empirical gate;
7. attack screenshot/GIF legibility and 20-minute demo ending;
8. run final portfolio/collision/title check;
9. select exactly one winner only if it survives. If no candidate clears the bar, kill all three and return to fresh discovery rather than force a winner.

Special final attacks:
- `Fresh Coat`: prove ordered exposure history is not merely repeated set partition; prove 4-object scenes remain readable.
- `Misaligned`: prove 24 cases do not collapse to transform enumeration; rename if selected.
- `Before It Dries`: prove wet-life is not disguised job scheduling and that provenance/contact geometry remains the player's main mental model.

PHASE 2 ROUND B = COMPLETE
DESIGN COMPLETE = NO
