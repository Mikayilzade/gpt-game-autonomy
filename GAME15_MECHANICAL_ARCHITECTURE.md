# GAME #015 — PHASE 4 MECHANICAL ARCHITECTURE

Date: 2026-09-03
Status: PHASE 4 COMPLETE
Working title: **FRESH COAT**
Design complete: NO

## 0. Authority and intent
This file freezes the mechanical truth implied by the selected concept and Product Thesis. It does not start production implementation. Rendering may illustrate these rules but may never decide puzzle truth.

## 1. Canonical case model
A case is a finite deterministic tuple:

`Case = (Objects, Regions, Sockets, PoseDomains, Compatibility, BoothStages, RearrangementContract, Targets, SymmetryMetadata)`.

### 1.1 Object
Each rigid workpiece has:
- stable `object_id`;
- authored solid geometry used only to derive exact semantic occlusion data;
- semantic face-regions with stable IDs;
- finite legal poses, always orthogonal rotations from an authored subset;
- socket compatibility tags;
- optional cavity/aperture descriptors;
- symmetry metadata for certification/equivalence.

Objects never deform, scale, free-rotate, balance physically or occupy continuous coordinates.

### 1.2 Semantic face-region
A region is the smallest gameplay-relevant paint unit. It has:
- `region_id` unique within object;
- owner object;
- exact planar support and boundary in canonical object coordinates;
- outward normal;
- authored subdivision polygon(s), with rational/integer-grid coordinates;
- current ordered coat history;
- optional target predicate.

A visible rendered face may contain several semantic regions when masking can split it meaningfully. Region subdivision is authored before play; gameplay never creates arbitrary new truth pixels.

### 1.3 Socket
A socket is a discrete transform anchor with:
- stable ID;
- exact world transform;
- occupancy capacity (normally one root object);
- compatibility tags;
- optional parent/cavity relationship;
- legal object/pose pairs;
- collision/containment relationships prevalidated by content tooling.

Sockets can represent tabletop positions, nested cavity positions, or authored mask lanes. They are not generic inventory slots: their spatial relationship determines exposure.

### 1.4 Pose
A pose is `(socket_id, orientation_id)`. Orientation IDs map to exact 90-degree orthogonal transforms. A case explicitly lists legal poses per object/socket. If a pose is not authored legal, it cannot be reached.

## 2. Arrangement legality
An arrangement maps every active object to exactly one legal pose.

It is legal iff:
1. every object occupies one compatible socket/pose;
2. exclusive sockets are not multiply occupied;
3. authored collision constraints are satisfied;
4. containment/nesting requirements are satisfied;
5. no two solids have positive-volume overlap;
6. authored accessibility constraints for the current rearrangement stage are satisfied.

Face touching is allowed only when the case data explicitly validates that contact. The player never resolves near-contact tolerance.

No continuous physics is consulted at runtime. Production may animate movement between legal poses, but the committed state snaps atomically to the exact pose.

## 3. Booth and spray stages
A case contains one or two primary spray stages in the main campaign.

Each stage has:
- fixed `coat_id`;
- fixed booth direction chosen from the product vocabulary;
- one pre-spray arrangement state;
- one explicit `SPRAY` commit.

### Campaign ceiling resolution
**Two coats and one rearrangement are the universal main-campaign ceiling.** This is now frozen, not merely a default.
- Cases may use one spray only.
- Cases may use two sprays with zero or one rearrangement boundary.
- No main-campaign case uses a third coat, third spray, or second rearrangement.
- A future expansion could formally reopen this ceiling, but Phase 4 will not rely on it for depth.

This preserves a compact mental timeline and prevents late difficulty from becoming sequence planning.

Canonical two-stage timeline:
`arrange A -> SPRAY A -> rearrange (if allowed) -> SPRAY B -> unpack/validate`.

The player cannot reorder coat identities or spray stages.

## 4. Exact exposure truth
Exposure is directional orthographic reachability, not lighting and not renderer visibility.

For stage direction `d`, a point on a semantic region is exposed iff the open ray from that point opposite the incoming spray direction reaches the booth exterior without intersecting any solid first.

### 4.1 Region exposure must be exact
A semantic region may be subdivided into authored atomic subregions when one blocker can cover only part of a face. Each atomic subregion has exact polygonal geometry. Gameplay truth is computed from exact projected polygon coverage / authored precomputed exposure, never samples, pixels, depth-buffer thresholds, antialiasing or percentage coverage.

For every legal arrangement and booth direction, certification tooling produces an exact exposure class for every atomic region:
- `EXPOSED` — the whole atomic region is reachable;
- `OCCLUDED` — none is reachable.

A region that would be partially exposed must have been subdivided at the relevant blocker boundary into atomic regions before shipping. A shipping atomic region may never resolve to a fractional percentage.

### 4.2 Multiple blockers
Occlusion is union coverage: any blocker may shield a subregion. Blocker identity may be recorded for authoring/debugging but is not part of paint truth unless a future formally reopened mechanic needs it.

### 4.3 Self-occlusion
An object's own geometry may occlude its cavity regions. Self-occlusion is treated exactly like another solid for reachability, except the target surface itself is excluded from the ray-origin intersection.

## 5. Coat-history state machine
Each atomic semantic region stores an ordered list of coat IDs actually received.

Main-campaign reachable histories are bounded by the fixed pass schedule:
- `RAW = []`
- `A_ONLY = [A]`
- `B_ONLY = [B]`
- `A_THEN_B = [A,B]`

If a one-pass case uses only A, only `RAW` and `A_ONLY` exist.

A spray appends its coat ID exactly once to every exposed atomic region and changes nothing else. There is no thickness, drying, blending, overwrite, paint quantity or color-mixing truth. Visual material may depict a final combined look, but ordered history remains authoritative.

Repeated spraying of the same stage is impossible: `SPRAY` advances the case atomically to the next stage. Undo can restore the prior branch state.

## 6. Rearrangement contract
When enabled, rearrangement occurs only after A and before B.

- Paint history remains attached to semantic regions through movement.
- Objects may move only to legal stage-B poses.
- A case may constrain which objects are movable after A only when this is physically communicated by authored socket accessibility; arbitrary per-level 'you cannot move this piece now' rules are forbidden.
- Default is that all objects can be reassigned among legal B-stage poses.
- Stage-B legality may differ because an authored nesting relationship makes a socket inaccessible/available after an object is removed, but this must be represented in case data and visible interaction affordance.
- There is no action-count cost inside the rearrangement stage. The player can freely revise the B arrangement until committing spray B.

Thus the puzzle concerns the two committed exposure states, not optimal movement choreography.

## 7. Final targets and validation
Targets are predicates over exact region histories, plus optional final-placement predicates only where mechanically justified.

Allowed region predicates:
- exact `RAW`;
- exact `A_ONLY`;
- exact `B_ONLY`;
- exact `A_THEN_B`;
- `PAINTED_AT_LEAST_ONCE` only for onboarding cases where order is not yet taught.

Late campaign uses exact histories; broad predicates must not weaken capstones.

Optional final-placement predicates are allowed only for explicit unpack/display teaching and cannot become a parallel packing objective. Default final placement is irrelevant after unpack.

A case succeeds iff all required region predicates and any explicit final predicates pass. Extra paint on a targeted RAW region is a failure; missing/incorrect/order-wrong paint is a failure.

## 8. Failure explanation without oracle leakage
Final reveal may state factual discrepancies per region:
- `needed RAW; received A`;
- `needed B only; received A -> B`;
- `needed A -> B; received B`;
- `needed A; remained raw`.

It may visually isolate the failed region and replay actual committed exposure history. It must never say which object/socket/pose should have been used, which blocker was 'intended', or show a counterfactual correct arrangement.

## 9. Current-state inspection
Before a spray, the player may inspect factual current exposure:
- exposed atomic regions receive a booth-facing highlight/hatch;
- occluded regions receive a distinct neutral protected state;
- already accumulated coat-history badges remain visible;
- selected object may be isolated visually while all blockers remain represented as silhouettes/ghosts.

Inspection answers only: **what would this already-committed current arrangement expose if I spray now?** It does not compare against targets, mark 'good/bad exposure', recommend a pose, rank moves, show future B exposure, or reveal solution-equivalent configurations.

Camera orbit, if present for comfort, cannot change truth and cannot be required to discover a region; semantic face list/isolation provides complete factual access.

## 10. Undo, reset and branch recovery
- Arrangement edits before spray are freely reversible and do not enter permanent history.
- `SPRAY` creates a branch checkpoint containing exact arrangement, stage, and all region histories.
- Undo after A restores the editable pre-A arrangement.
- Undo after B restores the editable post-A/pre-B arrangement while preserving the exact A checkpoint.
- Reset returns to authored initial state.
- Leaving/reloading a puzzle restores the latest committed checkpoint plus current editable arrangement if persistence later chooses to save it; it may never recompute paint from rendered appearance.
- No undo cost, limit, score penalty or achievement penalty.

## 11. Difficulty knobs that preserve reasoning
Allowed difficulty growth:
1. number of simultaneously constrained semantic regions;
2. differential masking of adjacent regions;
3. masker has own paint obligation;
4. dependency-chain depth among mask objects;
5. introduction of second fixed pass;
6. need to reserve access for B while satisfying A;
7. ordered-history distinction;
8. cavity/self-occlusion topology;
9. role reversal between A and B;
10. coupling two obligations through one spatial relation/socket.

Guardrails:
- adding sockets/poses solely to enlarge search is forbidden;
- object count alone is not difficulty;
- five objects exceptional, never required for freshness;
- no hidden compatibility;
- no tiny atomic regions used merely to make visual prediction harder;
- no new coat/pass/rearrangement after the fixed ceiling.

## 12. Equivalence and repetition signature
A complete solution is represented by the normalized pair `(A arrangement class, B arrangement class if present)` plus induced per-stage exposure sets and final histories.

Two physical arrangements are solution-equivalent if, after permitted symmetry relabeling, they produce identical:
- per-object/per-region exposure at each spray stage;
- final coat histories;
- mask-dependency relations relevant to the case;
- target satisfaction.

Case repetition signature:
`R = (stage count, normalized target-history multiset, exposure-obligation hypergraph, self-obligated-mask dependency graph, rearrangement transition class, cavity/self-occlusion motifs, role-reversal edges)`.

Mesh identity, color, object names, mirrored socket labels and harmless parking symmetries are normalized away. Content certification must reject campaign cases isomorphic on `R` unless the later case introduces a genuinely new deduction pressure documented by authoring review.

## 13. Certifier responsibilities
The offline authoring/QA certifier must:
1. enumerate all legal discrete arrangements per stage;
2. compute exact atomic-region exposure for every legal arrangement/direction;
3. apply spray/history transforms exactly;
4. enumerate legal A->B transitions when rearrangement exists;
5. find all successful solution classes;
6. collapse object/socket symmetries and harmless parking differences;
7. verify at least one solution;
8. flag excessive solution-class counts;
9. produce candidate human-proof facts (necessary exposure/occlusion obligations) for designer review, not player UI;
10. calculate repetition signatures across the campaign;
11. flag any atomic region that becomes partially covered under a legal arrangement, requiring author subdivision or pose removal;
12. detect unreachable target histories and illegal/ambiguous contact geometry.

Uniqueness is not universally required. Multiple arrangements are acceptable when they embody the same intended reasoning or legitimate alternate spatial proofs. The certifier records solution classes so content review can judge whether alternatives trivialize the case.

## 14. Canonical geometric edge cases

### Touching / coplanar surfaces
Exact touching is legal only when authored. A face in flush contact with another solid is occluded from the contacting direction. There is no epsilon gap. Coplanar overlapping surfaces cannot both occupy the same positive-area plane unless explicitly modeled as nested contact; the outward-facing topmost surface receives spray, the contacted interior does not.

### Edge-only / point-only contact
Zero-area edge or point contact does not occlude positive-area region truth. Atomic polygons are not split for zero-area contact.

### Cavities
A cavity is ordinary solid geometry plus an aperture. A cavity region is exposed only if an orthographic ray through the aperture reaches it unobstructed. No magical 'inside' flag paints or protects it.

### Hidden regions
Every targeted region must be inspectable through object isolation/semantic face UI even if physically hidden in the current arrangement. Hidden rendering never means hidden rule state.

### Identical objects
Mechanically identical objects still have stable IDs when their targets differ. If targets and geometry are identical, the certifier may quotient their permutation as symmetry. Player-facing markings distinguish objects whenever identity matters.

### Symmetry
Symmetric poses with identical exposure consequences are one equivalence class. UI may still allow both if natural, but content cannot count them as distinct solutions/difficulty.

### Object as masker with own target
No exception exists: a masker's exposed regions are painted normally. It must satisfy its own history targets, which is the central coupling rule.

### Role reversal
Objects may exchange masker/target roles across A/B because all are always both potential blockers and paint recipients. No special role token exists.

## 15. Worked puzzles

### Worked 1 — FC01 direct mask
Objects: target block T and slab M. One A spray from +Z. T.top requires RAW; T.side requires A. M has no target.

Legal arrangements offer M either above T.top or beside T.side.
Reasoning: T.side must see A, so M cannot occupy side-mask socket. T.top must remain raw, so M occupies top-mask socket. Spray A. Exact exposure appends A to T.side while T.top is occluded. Unpack: target passes.

Human proof is one differential exposure fact, suitable onboarding.

### Worked 2 — FC07 self-obligated masker
Objects X and Y. A spray from +X. X.front requires RAW, X.top requires A; Y.front requires A. Y can mask X.front only in a pose that leaves Y.front itself facing booth; alternate rotated pose masks X.front but also self-occludes Y.front.

Reasoning: X.front RAW requires a blocker. Only Y can block it. Y.front A eliminates Y's rotated blocking pose, fixing the pose where Y blocks X.front while remaining exposed. X.top remains exposed in both, receives A. This teaches that a mask is not disposable.

### Worked 3 — FC14 ordered history
Objects P, Q, R. A then B with one rearrangement. P.outer requires A->B; P.neighbor requires B_ONLY; Q.top requires A_ONLY; R has a RAW face.

A-stage proof: P.neighbor must avoid A while P.outer receives A. Q's wide pose is the only relation that covers neighbor but not outer. Q.top simultaneously faces A, satisfying its first requirement.

B-stage proof: P.outer and neighbor both need B, so Q must move. But Q.top must avoid B; Q therefore moves behind R rather than to the exposed parking socket. R's RAW face must remain away/covered, removing the mirrored arrangement. Spray B yields P.outer [A,B], P.neighbor [B], Q.top [A].

### Worked 4 — FC18 cavity reveal without rotating target
Object U has cavity floor = B_ONLY, rim = RAW, outer = A->B. Slab S has top = A_ONLY. Block K has side = B_ONLY.

A-stage: outer needs A while cavity must avoid A. S covers the aperture while leaving outer exposed; S.top itself is exposed and gets A. Rim is shielded by S's authored lip relation.

B-stage: rotating U to expose cavity would expose RAW rim and is eliminated. Therefore U remains fixed. S must leave aperture but must avoid B itself. K moves into the side lane: its geometry shields rim while leaving aperture line open and K.side exposed. S parks behind U. Spray B reaches cavity floor, U.outer and K.side; rim remains raw; S.top remains A-only.

This establishes cavity depth without a special cavity rule.

### Worked 5 — FC21 late role reversal
Targets: X.top=A_ONLY; X.side=B_ONLY; Y.front=A_THEN_B; Y.back=RAW; Z.top=B_ONLY.

A stage:
1. Y.back RAW eliminates all poses exposing its back.
2. X.top needs A while X.side must avoid A. Only Z can cover X.side without covering top, fixing Z as X's A-stage masker.
3. Y.front needs A while back remains hidden; remaining relation places X behind Y, where X's body shields Y.back.
Spray A: X.top and Y.front receive A; X.side/Y.back/Z.top do not.

B stage:
4. X.side and Z.top need B, so Z vacates the X-side shield and becomes exposed.
5. X.top must avoid B. Y takes the shielding relation over X.top while keeping Y.front exposed to B.
6. X continues to shield Y.back. Spray B.
Result: X.top [A], X.side [B], Y.front [A,B], Y.back [], Z.top [B]. Masking roles reverse using the same universal geometry rules.

## 16. Mechanical empirical gates carried forward
- E1 spatial predictability: players should correctly predict most current atomic-region exposure after onboarding without solver overlays.
- E2 four-object readability: selection/isolation must suffice; no x-ray oracle dependency.
- E3 reasoning vs permutation: playtests must show class elimination from physical obligations, not systematic socket cycling.
- E4 24-case freshness: repetition signatures plus human review must reject cognitively duplicate cases.
- E5 reveal satisfaction: unpack remains proof, not opaque delayed grading.

Additional Phase-4 gate E6: authored atomic subdivision must remain visually coarse. If exact exposure routinely requires tiny slivers or many subregions, reject the geometry/case rather than increase semantic resolution.

## 17. Phase-4 acceptance
Mechanical architecture now answers without invention:
- exact discrete state and legality;
- exact semantic exposure independent of renderer thresholds;
- paint-history transition order;
- fixed two-pass/one-rearrangement ceiling;
- rearrangement semantics;
- success/failure and factual inspection;
- undo/reset branch semantics;
- difficulty knobs and anti-inflation guardrails;
- equivalence/repetition model;
- certifier obligations;
- canonical geometric edge cases;
- concrete early/mid/late proof routes.

PHASE 4 = COMPLETE
DESIGN COMPLETE = NO

## NEXT ACTION — PHASE 5 CONTENT ARCHITECTURE
Specify the complete 24-case content system: finalize F1–F8 progression and case IDs; define reusable solid/socket/booth vocabulary; exact case-data fields and dependency graph; authored-vs-derived content; target counts and complexity budgets; authoring workflow from spatial motif -> targets -> certification -> human-proof annotation; repetition/freshness gates; tutorial/demo subset; hint/proof metadata boundaries; content validation and expansion rules. Fully outline all 24 cases deeply enough that Phase 6 UX can reason against actual campaign content. Do not add mechanics beyond this Phase-4 authority merely to make cases different.