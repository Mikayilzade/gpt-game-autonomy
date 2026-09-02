# GAME #015 — PHASE 2 CONCEPT TOURNAMENT / ROUND A

Date: 2026-09-02
Status: ROUND A COMPLETE / NO FINAL WINNER
Authority boundary: Game #015 only. Games #001–#014 remain exclusion/portfolio history, not canon.

## 0. Round-A method

This pass applies the exact destructive contract frozen in `GAME15_RESEARCH.md` to all 12 entrants. Every candidate receives:
- a tutorial case, early case and hour-3 case;
- a named human reasoning verb;
- a normalized repetition signature;
- anti-enumeration / anti-pixel-hunt / anti-set-cover attack;
- failure-readability, certification, input/accessibility and production-ratio review;
- exact-mechanic analogue check;
- a PASS / KILL decision under one standard.

The goal is not to find the winner yet. The goal is to remove candidates whose attractive visual transformation does not survive as durable human reasoning.

## 1. Fresh analogue check

Fresh searches on 2026-09-02 found two especially important occupied territories:

- **Superliminal** remains a very strong, highly recognized forced-perspective/scale reference. Its Steam framing is explicitly about forced perspective and perception changing apparent physical scale. That raises the collision bar for `Wrong Scale`: merely making objects visually grow/shrink is not enough. The movable *measurement legend as the causal rule object* must remain the actual puzzle grammar.
  - https://store.steampowered.com/app/1049410/Superliminal/
- **Viewfinder** remains a strong perspective/photo reality-manipulation reference. Its core is placing images into the world to reshape reality. This raises the bar for `Parallax Bureau` and `Contact Sheet`: camera framing alone is not differentiating. The simultaneous fixed multi-view constraint must do the work for Parallax Bureau.
  - https://store.steampowered.com/app/1382070/Viewfinder/

Searches for the remaining exact mechanic phrases did not surface a comparably dominant commercial game built specifically around carbon-copy pressure stacks, wet-stroke transfer windows, spray-painting exposed faces of nested solids, privacy-film layer order, print-registration as the entire puzzle grammar, focus-rack silhouettes, embossing depth stacks, or stencil-clog degradation. Absence from search is not proof of novelty; it is only evidence that no obvious incumbent invalidates them at this stage.

## 2. Candidate attacks

### A. WRONG SCALE — PASS TO ROUND B, HIGH COLLISION RISK

**Concrete tutorial**
A workbench has a key, lock and two removable scale legends: `1:1` and `2:1`. Objects inside a legend's snapped measurement frame use that legend's logical size. The player moves `2:1` from a display bolt to the key; the key doubles and now fits the oversized training lock. No freehand resizing exists.

**Early case**
Three scale domains share interfaces. A crate must pass through a hatch while preserving a fragile item inside. Moving `1:2` onto the crate changes crate and contents together; moving it onto only the hatch changes the opening. The target requires choosing which domain owns containment at the transition.

**Hour-3 case**
Four snapped measurement frames overlap a miniature machine. A shaft must fit a bearing, a carried washer must remain captured, and two mating faces must end at the same world-size despite different printed scales. Legends can be swapped only among fixed sockets. The interesting deduction is not “make X bigger” but tracing which *measurement domain* controls each interface and when containment inherits scale.

**Human reasoning verb**
Trace **domain ownership and interface compatibility** under discrete reassignment of scale legends.

**Anti-bruteforce**
Free placement would be fatal. Round-B survival therefore depends on a discrete architecture: fixed legend sockets, small finite legend set, explicit domain boundaries, exact rational scale values and no continuous transform search. With 4 sockets and 4 legends, naive permutations are only 24, so cases need interacting containment/interface constraints that eliminate whole classes by reasoning rather than merely raising permutation count.

**Failure readability**
Strong if every failed interface identifies the physical mismatch (`shaft too large for bearing`, `contained part crosses domain illegally`) without suggesting which legend to move. Weak if failure is only “scene incoherent.”

**Input/accessibility**
Controller-friendly if all interactions are socket select/swap. Size differences need numeric/shape cues, not visual scale alone.

**Content / certification**
Deterministic if logical sizes are rational and interfaces are authored predicates. Content burden is moderate: cases are small scenes but each needs understandable physical relationships.

**Repetition signature**
Two cases are cognitively identical if both reduce to assigning one unique scale legend to each independent fit constraint with no shared-domain or containment coupling.

**Collision attack**
Superliminal occupies “perception changes size.” `Wrong Scale` survives only because its input is not perspective/camera manipulation: printed measurement legends are movable causal tokens governing discrete physical domains. Any drift toward grabbing/resizing by viewpoint is a kill.

**Round-A verdict: PASS.** Distinct rule object and excellent GIF, but Round B must prove hour-3 reasoning is not 4! legend permutation.

---

### B. CARBON COPY — KILL

**Concrete tutorial**
Stack Form A / carbon / Form B. One pen stroke transfers to both sheets. Add a backing blocker under half the stroke so B receives only one segment.

**Early case**
Three forms require three different subsets of two strokes. Player reorders carbon and blocker layers before pressing.

**Hour-3 case attempt**
Four outputs, several pressure classes, masks and multiple strokes. Desired marks become subset vectors by depth.

**Human reasoning verb**
Choose propagation masks through ordered layers.

**Dominance test**
Once represented cleanly, every pen segment carries a bit-vector of which output layers receive it. Backings/masks select subsets; desired forms specify target subsets. The embodied stack presentation is satisfying, but the reasoning normalizes directly into bitmask composition / set-cover-like selection. Increasing depth mostly increases vector length.

**Failure readability**
Excellent, but that does not rescue the shallow normalized grammar.

**Repetition signature**
Any cases with isomorphic required output-layer subsets are the same puzzle regardless of form art.

**Round-A verdict: KILL — disguised finite subset arithmetic.**

---

### C. BEFORE IT DRIES — PASS TO ROUND B, REQUIRES TURN-BASED WETNESS

**Concrete tutorial**
Two broad paint strips lie on a ceramic tile. Wetness is represented by three discrete action beats, not real-time seconds. Sliding blue across wet yellow transfers a defined edge band; after the next committed action yellow dries and can no longer transfer.

**Early case**
Three movable strokes must create a target with one preserved white gap. One contact transfers pigment in only the moved-stroke direction; moving the donor too early consumes its wet contact opportunity and contaminates the gap.

**Hour-3 case**
Five strokes, each with a deterministic wet-life counter of 1–3 committed moves. Some can be translated once while wet, some act as receivers after they dry. Target constraints care about final pigment regions, protected negative space and transfer provenance. The player reasons about a partial order of contacts while also using geometry.

**Human reasoning verb**
Plan **contact precedence under expiring transformability**, then execute a deterministic short action plan.

**Anti-bruteforce**
Real-time manipulation is forbidden: it would become dexterity/fiddliness. Use discrete sockets/lanes and action beats. Sequence search is a risk, but unlike `Stencil Debt`, each action also changes spatial pigment geometry and future contact relations; Round B must prove deduction can eliminate branches from visible contamination/provenance constraints.

**Failure readability**
Potentially strong: final target can show missing, excess and wrong-source pigment regions; timeline can show which stroke is wet/dry without revealing a solution.

**Input/accessibility**
Controller-safe with snap positions and commit actions. No color-only semantics: pigments also use hatch/texture IDs; reduced motion can replace smear animation with before/after transition.

**Content / certification**
Exact cell/polygon masks plus deterministic transfer rules are certifiable. Art can remain stylized and low-burden. Authoring must avoid one-off fluid simulation.

**Repetition signature**
Two cases are identical if they share the same contact precedence DAG and the same protected-region obligations after normalizing pigment names and geometry symmetries.

**Round-A verdict: PASS.** Strong transformation and a plausible second-order spatial/temporal grammar, conditional on discrete wetness and proof against pure sequence search.

---

### D. ONE-WAY GLASSHOUSE — KILL

**Concrete tutorial**
One pane, two observers, one film. Rotate film to let A see through while B cannot.

**Early case**
Two panes share a rotatable film cassette; three observers have asymmetric visibility requirements.

**Hour-3 case attempt**
Several film types, axes and ordered layers produce observer-dependent transmission states.

**Human reasoning verb**
Compose side/axis-dependent transmission states.

**Dominance test**
To make the behavior reliable and teachable, the game would need a simplified finite transmission table. Once simplified, layers compose as a truth-table/finite-state matching problem. If physically faithful polarization is retained, the rule becomes harder to intuit, hard to represent without formula-like UI, and accessibility/readability degrade. Both branches are inferior.

**Repetition signature**
Cases normalize to assigning film states so each observer/pane boolean target matches.

**Round-A verdict: KILL — either opaque physics or truth-table assignment.**

---

### E. FRESH COAT — PASS TO ROUND B

**Concrete tutorial**
Two rectangular blocks are stacked. A spray pass paints only upward and side faces visible to the nozzle's fixed orthographic direction. Unstack: the covered face remained raw. Goal pattern teaches occlusion-as-mask without text.

**Early case**
Three cuboids can nest or stack in fixed sockets, rotate in 90-degree increments, then receive two paint passes from fixed booth directions. One final object needs a face to stay raw while an adjacent face receives the second coat.

**Hour-3 case**
Four reusable solids with simple cavities. Player may perform a bounded sequence such as `arrange -> spray A -> rearrange once -> spray B -> unpack`. Final constraints combine protected faces, exact coat provenance, and a face that must receive A then B while another geometrically adjacent face receives only B. Occlusion relations created for one pass conflict with later access.

**Human reasoning verb**
Construct **temporary physical masks through occlusion**, anticipating what becomes exposed after unpack/rearrangement.

**Anti-bruteforce**
Continuous packing is forbidden. Shapes use authored discrete sockets, orthogonal rotations and fixed spray directions. The solver can enumerate for certification; the human should reason from visibility/coverage. The core does not reduce to packing because object position matters only insofar as it creates exposure sets, and multi-pass/rearrangement creates coupled exposure history.

**Failure readability**
Excellent: unpacked final objects directly show missing coat, extra coat, wrong coat order and protected-face violation. Inspection can expose current line-of-sight without offering counterfactual best placement.

**Input/accessibility**
Strong controller path. Coat identity uses texture/pattern plus color. No timing or fine aiming.

**Content / certification**
Strong production ratio. A small family of cuboids/L-pieces/cavities plus sockets can generate many exposure relations. Exact face-level occlusion is deterministic and inexpensive to validate compared with arbitrary mesh painting.

**Repetition signature**
Two cases are cognitively identical if each spray pass requires the same normalized exposure-set partition and rearrangement does not change dependency structure.

**Portfolio check**
Not #009 flat-sheet fold/nest/trim: the solved object is not a sheet/signature assignment. Not #014 shadows: visibility is direct booth exposure and persistent paint history, not light classification.

**Round-A verdict: PASS.** One of the cleanest surviving human verbs and failure states.

---

### F. PUNCH LIST — KILL

**Concrete tutorial**
Slide one transparent plan until three inspection circles align with three visible defects.

**Early case**
Flip/rotate two overlays around landmarks so marks refer to correct floor features.

**Hour-3 case attempt**
Multiple floors, partial landmarks, several overlays and “no false condemnation” constraints.

**Human reasoning verb**
Register transformed overlays against sparse landmarks.

**Dominance test**
The mechanic remains visual registration. Added floors and overlays increase transform search, but the reasoning pressure does not qualitatively change: identify anchor, try transform, align marks. Without hidden semantics it is shallow; with hidden semantics it becomes evidence-table deduction.

**Repetition signature**
Same transform group + same anchor ambiguity = same case.

**Round-A verdict: KILL — insufficient hour-3 evolution.**

---

### G. PARALLAX BUREAU — PASS TO ROUND B, TECHNICAL RISK

**Concrete tutorial**
Two chunky sign fragments occupy fixed depth rails. Camera A must see a complete circle; moving the front fragment laterally closes the circle from A while camera B visibly loses its triangle. This teaches shared-scene/multi-view conflict.

**Early case**
Three fragments on discrete X/depth sockets, three fixed inspection cameras, each demanding one simple glyph. One fragment must serve different contours from different views through occlusion.

**Hour-3 case**
Five fragments, 3–4 fixed cameras, discrete rails/rotations. Targets are topology-level glyph features (closed loop, stem-left, notch-top) rather than pixel-perfect images. A fragment hidden behind another in one camera remains structurally necessary in another. The solve requires tracing which visible contour portions are reusable across viewpoints.

**Human reasoning verb**
Allocate **shared physical contour/occlusion resources across simultaneous viewpoints**.

**Anti-bruteforce**
Continuous 3D manipulation is forbidden. Fixed cameras, discrete rail sockets and 90-degree rotations produce finite exact states. Human reasoning must operate on visible silhouette contributions; certification may render deterministic binary/ID buffers from canonical cameras.

**Failure readability**
Strong only if target matching uses coarse semantic contour predicates or snapped vector silhouettes, not pixel distance. Each camera can identify unmet feature classes without naming a move.

**Input/accessibility**
Controller-friendly with socket navigation. Targets need shape/topology labels, not tiny contour differences. Camera switching must be instant and stable.

**Content / certification**
Higher technical burden than Fresh Coat: multi-camera deterministic silhouette classification and authoring useful shared fragments. Still bounded if all pieces are stylized extrusions and transforms discrete.

**Repetition signature**
Cases are identical when the normalized bipartite mapping of piece-visible-contour contributions to camera target features is isomorphic.

**Collision attack**
Viewfinder uses images to reshape reality; Superliminal uses perspective for scale. Parallax Bureau does neither. Its differentiator is one unchanged scene satisfying several *simultaneous fixed viewpoints*. If gameplay allows free camera hunting or turns target matching into arbitrary pictures, kill it.

**Round-A verdict: PASS.** Very marketable, but Round B must prove coarse deterministic target language and acceptable authoring cost.

---

### H. MISALIGNED — PASS TO ROUND B

**Concrete tutorial**
Two tiny vector print plates sit on snapped registration pins. Shift the cyan plate one notch: their overlap produces the target two-part icon, while an explicit forbidden overlap region remains empty.

**Early case**
Three plates, translation plus one 90-degree rotation option, with required single-ink and overlap classes. Player reasons which plate must own each visible region and then infers compatible registration.

**Hour-3 case**
Four plates built from reusable coarse vector cells. Target asks for several provenance classes: C-only, M-only, Y-only, C+M, plus protected paper. Some source regions are hidden in the final composite unless registration is inferred from their effects elsewhere. Optional knockout masks may exist only if they are a universal rule, not level-specific tricks.

**Human reasoning verb**
Infer **layer provenance and registration from required overlap classes**.

**Anti-bruteforce**
Transforms must be discrete and few. Simple cases can be enumerated, so depth must come from coupled provenance: one plate alignment simultaneously explains multiple separated target regions and forbids others. Avoid arbitrary image matching and large grids.

**Failure readability**
Strong with semantic overlap classes and an exploded-plate inspection showing actual plate coverage; no “best alignment” ghost.

**Input/accessibility**
Strong. Every ink uses texture/symbol identity in addition to color; coarse geometry avoids fine vision.

**Content / certification**
Very good technical ratio if vector-cell or polygon plates are used. Exact boolean region operations are deterministic. Content factory can reuse plate motifs while varying registration constraints, but repetition is a real risk.

**Repetition signature**
Two cases are identical when required region-provenance classes induce the same relative transform constraints after plate/color relabeling and symmetry normalization.

**Round-A verdict: PASS.** Clear deductive verb and low production burden; Round B must prove it is richer than finite image-overlay matching.

---

### I. SOFT FOCUS — KILL

**Concrete tutorial**
Two depth layers; focus near shows one readable silhouette, focus far another.

**Early case**
Arrange three layers so two fixed focus distances produce two targets.

**Hour-3 case attempt**
Several blur radii, occlusion relations and focus targets.

**Human reasoning verb**
Allocate projected mass across depth-dependent blur kernels.

**Dominance / accessibility test**
The interesting state is renderer-dependent. Either matching uses image-space thresholds, inviting pixel hunting, graphics-setting sensitivity and accessibility problems, or it is heavily discretized into symbolic blur footprints, at which point the visual fantasy becomes a disguised layer-mask puzzle. Failure cannot be explained cleanly without exposing numeric image-error information.

**Round-A verdict: KILL — renderer-dependent ambiguity / fine-vision burden.**

---

### J. CONTACT SHEET — KILL

**Concrete tutorial**
Place two objects once; two fixed crops must each show a target composition.

**Early case**
Three crops reuse the same objects at different frame boundaries.

**Hour-3 case attempt**
Rotated crops, occlusion and negative-space targets across a larger still life.

**Human reasoning verb**
Place shared scene elements so several frame windows contain required compositions.

**Dominance test**
With continuous placement, this is pixel/placement hunting. With discrete sockets, it normalizes to multi-constraint occupancy assignment. Unlike Parallax Bureau, crops mostly select subsets/regions of the same 2D arrangement; they do not create strong view-dependent occlusion structure. Adding semantic composition rules increases authoring subjectivity.

**Collision attack**
Camera/framing territory is already well populated, and the simultaneous-crop differentiator is weaker in motion than Parallax Bureau's distinct viewpoints.

**Round-A verdict: KILL — placement hunt / subset occupancy.**

---

### K. UNDER PRESSURE — KILL

**Concrete tutorial**
Embossed plate presses through one soft sheet; raised region leaves an imprint.

**Early case**
Stack spacer and two sheets so only the upper sheet receives the shallow relief while a tall relief reaches both.

**Hour-3 case attempt**
Multiple relief heights, blockers and orientations target different imprint sets by depth.

**Human reasoning verb**
Assign relief features to propagation depths.

**Dominance test**
Normalized state is almost exactly Carbon Copy with propagation threshold by height rather than carbon/mask layers: each relief feature maps to a subset of output depths. Additional height classes are parameter inflation, not new reasoning.

**Round-A verdict: KILL — layer bitmask sibling, weaker than Carbon Copy and still killed.**

---

### L. STENCIL DEBT — KILL

**Concrete tutorial**
Stencil prints three apertures; after one pass a visibly flagged aperture clogs and the second print has only two marks.

**Early case**
Two stencils with deterministic per-aperture clog counters must create three edition pages in order.

**Hour-3 case attempt**
Several stencils, limited cleaning and multiple clog thresholds; each future tool state depends on use count/history.

**Human reasoning verb**
Schedule consumable tool states across an output sequence.

**Dominance test**
The premise is visually strong, but once clogging is deterministic the central puzzle is ordering uses/cleaning so future finite states match future targets. Geometry contributes little after the aperture pattern is known. This is sequence permutation with consumable state and comes uncomfortably close to the factory's explicit anti-sequence preference / #011 exclusion boundary. Making clogging spatially complex would increase bookkeeping rather than create a new embodied verb.

**Round-A verdict: KILL — sequence permutation dominates.**

## 3. Round-A survivors

Exactly **5** concepts advance. No ranking here is a winner selection.

1. **Wrong Scale** — domain ownership + interface compatibility; high incumbent/collision risk and permutation risk.
2. **Before It Dries** — spatial pigment transfer + deterministic expiring wet states; sequence-search risk must be attacked.
3. **Fresh Coat** — temporary masking by physical occlusion across persistent multi-pass paint history; strongest current failure readability.
4. **Parallax Bureau** — one discrete 3D scene satisfying simultaneous fixed viewpoints; highest technical/authoring burden of survivors.
5. **Misaligned** — print-layer provenance + discrete registration under required/forbidden overlap classes; repetition/image-overlay risk.

Killed in Round A: **Carbon Copy, One-Way Glasshouse, Punch List, Soft Focus, Contact Sheet, Under Pressure, Stencil Debt**.

No alternate is promoted. `Packing Slip` remains a Phase-1 alternate only and is not active tournament canon unless a later explicit reopen occurs.

## 4. Cross-survivor comparison after destructive pass

| Candidate | Actual human verb | Biggest danger | Failure readability | Certification | Production ratio | GIF hook |
|---|---|---|---|---|---|---|
| Wrong Scale | trace scale-domain ownership/interfaces | permutation + Superliminal adjacency | strong if predicate-based | strong with rationals/sockets | medium | excellent |
| Before It Dries | plan contact precedence under expiring transformability | sequence search / bookkeeping | strong | strong if discrete masks/beats | medium | excellent |
| Fresh Coat | build temporary occlusion masks across paint passes | exposure-set repetition | excellent | excellent at face level | excellent | excellent |
| Parallax Bureau | share contour/occlusion resources across viewpoints | 3D authoring + target ambiguity | medium-strong if semantic | medium-strong | medium-low | outstanding |
| Misaligned | infer plate provenance/registration | overlay matching repetition | excellent | excellent | excellent | strong |

Round A intentionally does **not** canonize `Fresh Coat` despite its favorable profile. Round B must attack all five with equal deeper tests.

## 5. Round-B contract

Round B should reduce five concepts to **2–3 finalists**, not select the final winner unless an entrant suffers a hard kill and only one truly survives.

For every survivor:
1. formalize the smallest exact state model (objects, actions, transforms, predicates, check result);
2. construct **six** cases: tutorial, two early, two mid, one hour-3 stress case;
3. enumerate the bounded state space for at least the hour-3 case on paper or with a throwaway calculation and estimate blind-trial viability;
4. write at least **four qualitatively different reasoning pressures** that arise without new minigames/rule exceptions;
5. define a candidate human-proof route for one mid case: at least three deductions that eliminate state classes before residual trial;
6. define an exact normalized repetition signature and show how a 24-case campaign could avoid duplicates;
7. estimate minimum reusable asset vocabulary and authoring burden;
8. specify a 15–30 minute same-rules demo arc and its final escalation;
9. run fresh exact analogue / current-market checks where the concretized mechanic changes collision risk;
10. attack controller/handheld and non-color accessibility;
11. score all five under one matrix: hook, human reasoning, hour-3 depth, readability, certification, content factory, production ratio, demo strength, collision risk;
12. kill aggressively and retain only 2–3 finalists for Round C.

Special required attacks:
- `Wrong Scale`: prove it is not a legend permutation puzzle and not perceived as Superliminal-lite.
- `Before It Dries`: prove deductions come from visible geometry/provenance, not merely trying action orders.
- `Fresh Coat`: prove multi-pass exposure history yields distinct reasoning families rather than repeated set partitions.
- `Parallax Bureau`: prove exact target matching can remain coarse/readable and authorable without pixel thresholds.
- `Misaligned`: prove plate provenance creates deductions that cannot be replaced by simply nudging overlays until the image looks right.

ROUND A = COMPLETE
PHASE 2 = IN PROGRESS
DESIGN COMPLETE = NO
