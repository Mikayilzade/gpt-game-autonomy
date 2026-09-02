# GAME #014 — PHASE 4 MECHANICAL ARCHITECTURE

Date: 2026-09-02
Status: COMPLETE — deterministic geometry and puzzle rules frozen; Content Architecture next.
Working title: **NEGATIVE CASTING**
Authority: `START_HERE.md` -> `STATUS.md` -> `GAME_INDEX.md` -> Game #014 tournament record -> `GAME14_PRODUCT_THESIS.md` -> this file.

## 1. Phase-4 result
**PASS.** The product thesis survives a concrete geometry contract. Every logical shadow bit is derived from exact ray/opaque-footprint intersection in one compact 2D casting plane; no authored projection bitmask is canonical data. The model naturally produces protected-LIT, endpoint/extent, channel-attribution and cross-surface identity deductions.

The logical model is intentionally simpler than the attractive render. Rendering may extrude footprints into tabletop sculptures and walls into vertical screens, but it may not change logical incidence.

---

# 2. Canonical casting-plane geometry

## 2.1 Coordinate domain
Each case owns a bounded 2D Cartesian casting plane with **integer authored coordinates**. Logical calculations use exact rational arithmetic where line intersections require it. Recommended authored bounds are `0..32` on each axis; larger bounds are rejected unless a later implementation proves equal readability.

The casting plane contains:
- exactly **2 logical point lights**, `L1` and `L2`;
- **1–3 projection surfaces**;
- **2–6 blocker instances** in ordinary shipping content;
- one fixed socket per blocker instance;
- each blocker has **2–4 legal discrete states** in ordinary content.

The maxima are content/readability ceilings, not difficulty targets. Early cases should be far below them.

## 2.2 Logical lights
A light is an authored point `L=(x,y)` with stable channel id `L1` or `L2`. Lights never move during a solve. They must not lie on a projection surface, inside a blocker footprint, or at a sample point.

Light color is presentation only. Channel identity must also have a distinct glyph/shape and origin-line style.

## 2.3 Projection surfaces
A surface is an authored **open line segment** from integer endpoint `A` to integer endpoint `B`, plus ordered sample parameters. Shipping surfaces are straight; curved walls are presentation-only unless a future design revision explicitly reopens this phase.

A logical target cell is represented by one sample point on that segment:
`P_k = A + t_k(B-A)`, where each `t_k` is an authored rational strictly between 0 and 1 and sample order is increasing.

Recommended surface cell count: **3–10**, hard Phase-4 ceiling **12**. Cells may render as broad panels, but their logical state is evaluated at the canonical sample point only.

This center/sample contract prevents renderer resolution, antialiasing or penumbra from changing puzzle truth.

## 2.4 Blockers and sockets
A blocker archetype is a simple opaque polygon footprint with integer local vertices around local origin `(0,0)`. Shipping canonical footprints must be:
- simple/non-self-intersecting;
- positive area;
- no holes;
- preferably convex or orthogonally simple for visual readability; concavity is allowed only if human-route review proves it legible.

A blocker instance references one archetype and one fixed socket translation `S=(x,y)`. A legal state is a discrete rigid transform around the local origin. Baseline transforms are rotations by multiples of 90 degrees. Reflection is **not** a player action unless an archetype explicitly has mirrored states that are physically represented as distinct socketed poses; default content should avoid this.

The transformed polygon is `S + R_state(footprint)`.

Blockers never translate between sockets during a solve. A state change is therefore “rotate/change pose of this sculpture,” not free placement.

## 2.5 Physical validity of blocker states
A legal authored state must:
1. remain inside the case casting bounds;
2. not contain either light;
3. not intersect a projection surface;
4. not overlap another blocker's footprint in **any simultaneously legal combination** used by the case, unless the case explicitly removes the conflicting state combination from its legal state space.

Default authoring rule: use sockets/footprints that make all Cartesian combinations collision-free. State-dependent blocker collision is allowed only as an explicit legal-state constraint and should be rare; it is **not** a source of campaign depth and does not count as a human class-elimination deduction.

---

# 3. Exact projection / occlusion contract

For light `Lj`, surface sample `P`, and blocker state polygon `B`:

`blocked(Lj,P,B) = TRUE` iff the **open ray segment** from `Lj` to `P` intersects the **strict interior** of polygon `B`.

Endpoint contact and pure tangency do not count as blocking. A ray that crosses any positive-length interior portion does count. Because logical geometry is exact, this result is deterministic and renderer-independent.

For a complete player configuration `C`, channel shadow is union occlusion:

`s_j(P,C) = OR over blockers i of blocked(Lj,P,B_i[state_i])`.

No blocker priority, opacity amount, additive darkness, distance attenuation or penumbra exists logically. One or several blockers on the same ray produce the same channel bit.

The semantic target class at `P` is exactly:
- `LIT` = `(s1=0, s2=0)`
- `L1_ONLY` = `(s1=1, s2=0)`
- `L2_ONLY` = `(s1=0, s2=1)`
- `BOTH` = `(s1=1, s2=1)`

Names describe **which light is blocked**, not which light remains visible. UI copy must teach this explicitly; presentation may later choose clearer player-facing labels while preserving these canonical ids.

## 3.1 Boundary robustness / authoring clearance
Although exact tangency is defined, shipping cases must not rely on visually ambiguous grazing. For every authored legal blocker state and every light-to-sample segment, compute a clearance diagnostic to polygon vertices/edges. If a ray is tangent or falls within the implementation's frozen visual-clearance threshold of a state-changing boundary, the state/case is rejected or geometry is moved.

Thus the mathematical tie rule exists for determinism, while shipping content avoids asking players to perceive microscopic ties.

## 3.2 Derived masks only
A blocker state's per-light/per-surface incidence vector may be cached by tools/runtime, but it is **derived data**. Authoring files may never define or override it manually. Any cache must be reproducible from canonical geometry and invalidated when geometry changes.

---

# 4. Canonical case state model

A case contains:
- `case_id`, rules/schema version;
- casting bounds;
- two lights;
- ordered surfaces and samples;
- blocker archetype geometry;
- blocker instances, sockets and ordered legal states;
- optional explicit illegal joint-state combinations (rare collision safety only);
- target class for every surface sample;
- initial blocker state vector;
- accepted-solution policy;
- campaign/unlock metadata;
- human-route/certification metadata defined below.

Runtime mutable puzzle state is only:
- current state id for each blocker;
- undo history;
- whether current configuration has been committed/checked;
- completion record outside the case simulation.

There are no hidden resources, random variables, action counters or irreversible moves.

---

# 5. Player actions and observation

Legal mechanical actions:
1. select next/previous blocker;
2. cycle that blocker's legal state forward/backward, or choose a visible state directly;
3. select/inspect a surface;
4. inspect one selected blocker's **current-state** physical projection contribution from L1/L2 across surfaces;
5. undo one state change;
6. redo where supported by UX;
7. reset to case initial state;
8. commit/check;
9. leave/restart/replay case.

Changing a blocker updates actual current shadows immediately. The player may always see current semantic sample states. Inspection may isolate/highlight what the **currently selected physical state** blocks. It may not preview unselected counterfactual states side-by-side, mark a state as target-correct, compute “remaining errors solved by this pose,” or recommend a move.

## 5.1 Commit/check
On commit, evaluate every sample against its target. If all match, the case solves. Otherwise no punishment occurs: configuration remains, mismatch feedback may identify which target cells currently disagree, but must not identify which blocker should change.

Undo/reset remain available after mismatch.

---

# 6. Solution, equivalence and symmetry semantics

## 6.1 Physical solution
A physical solution is any complete legal blocker-state vector whose derived target classes exactly match all samples.

## 6.2 Multiple valid physical solutions
The campaign does **not** require a unique physical state vector. If two configurations are target-equivalent and both satisfy the target, both must be accepted. The game never secretly demands the author's pose.

Default shipping preference is a single **meaningful solution class**, not necessarily one vector.

## 6.3 State equivalence
Two states of the same blocker are **observationally equivalent for a case** if their derived `(L1,L2)` incidence is identical on every sample of every surface and they participate identically in explicit legality constraints. Such states are one equivalence class for uniqueness and human-route certification.

A case must not pretend choosing between globally equivalent states is a deduction. Equivalent states may remain for visual flavor only if the UI communicates that either is acceptable; default authoring should remove redundant states.

Two complete solutions are equivalent when every differing blocker state is within its case-level observational equivalence class.

## 6.4 Symmetry
Geometric mirror/rotation symmetry is not automatically equivalent. It counts as equivalent only when it yields identical observed incidence and legality under the actual lights/surfaces/targets. Certifiers quotient only proven observational equivalence, never aesthetic resemblance.

---

# 7. Win/fail/retry and campaign mechanics

There is no mechanical fail state beyond “commit does not match.” No lives, move limit or timer.

Campaign completion is per case. Recommended mechanical unlock rule, frozen for later content tuning:
- cases are arranged in small ordered groups of **2–4**;
- entering a group unlocks all cases in that group;
- completing a configured threshold (normally all but at most one) unlocks the next group;
- the final campaign completion gate requires all designated floor/capstone cases; optional target-count cases may be non-required.

Exact group composition belongs to Content Architecture, but progression must always leave at least one alternate case during the main campaign where feasible.

Replay never removes completion. Reset affects only current case state.

---

# 8. Difficulty knobs — structural, not raw-state inflation

Allowed knobs, in preferred order:
1. **protected-LIT pressure** — placement of bright samples that eliminate whole state classes;
2. **endpoint discrimination** — states with similar shadow area but different first/last affected sample;
3. **single-channel attribution density** — L1_ONLY/L2_ONLY constraints distinguish cause of darkness;
4. **cross-surface equivalence splitting** — states identical on one surface but distinguishable on another;
5. **producer multiplicity** — number of blockers that could cause one required shadow bit;
6. **deduction interleaving** — one surface forces extent, another channel, a third identity;
7. **solution-class symmetry** — carefully controlled ambiguity that is later split or intentionally accepted;
8. blocker count / states per blocker / sample count, only after structural knobs.

Forbidden fake difficulty:
- merely increasing grid/sample resolution;
- near-tangent geometry;
- tiny visual differences;
- many globally redundant blocker states;
- huge Cartesian state count without a shorter human route;
- relying on blocker collision constraints as the main puzzle;
- hiding channel identity through color confusion.

---

# 9. Human-route metadata and certifier gates

Every shipping case must be exhaustively machine-certified for validity and accepted-solution classes. In addition, authored metadata records at least one intended human route as **class eliminations**, not exact click instructions.

## 9.1 Deduction step schema
Each documented step contains:
- `step_id`;
- `family` from the frozen vocabulary below;
- `premises`: target samples / already established blocker-state classes;
- `subject`: blocker or blocker-state equivalence class being reduced;
- `before_classes` and `after_classes` or an equivalent finite candidate count;
- short human-readable rationale;
- whether the deduction depends on another documented step.

Frozen Phase-4 families:
- `PROTECTED_LIT_ELIMINATION`
- `ENDPOINT_EXTENT_ELIMINATION`
- `CHANNEL_ATTRIBUTION`
- `BOTH_DECOMPOSITION`
- `UNIQUE_PRODUCER`
- `CROSS_SURFACE_EQUIVALENCE_SPLIT`
- `LEGALITY_CLEANUP` (does not count toward depth gate)
- `RESIDUAL_ASSIGNMENT` (does not count toward depth gate)

Content Architecture may add a label only if it describes a consequence of the same frozen projection rule, not a new mechanic.

## 9.2 Required certification
A case is rejected if:
- no physical solution exists;
- target truth depends on arbitrary mask data;
- an accepted solution violates physical validity;
- an unintended solution class destroys the authored reasoning premise;
- intended deductions rely on visual grazing;
- a target sample is semantically color-only;
- its claimed human route cannot be verified against the actual derived incidence table.

EARLY cases may intentionally have one obvious deduction. **MID/LATE/CAPSTONE cases require at least 3 meaningful, dependency-connected class-elimination steps before residual assignment.** At least two of those steps must come from different counting families; three repeated protected-LIT eliminations do not satisfy the spirit or gate.

For LATE/CAPSTONE content, preferred gate is three families among protected-LIT, endpoint/extent, channel/BOTH attribution, and cross-surface splitting.

The exhaustive solver may enumerate the full Cartesian state space, but solver uniqueness never substitutes for the human-route gate.

---

# 10. Authoring rejection conditions

Reject or rework a case when any of these hold:
1. arbitrary projection masks are required to make it interesting;
2. difficulty comes mainly from trying orientations;
3. all target constraints reduce to “cover these dark cells” without channel/geometry/cross-surface structure after onboarding;
4. multiple surfaces are independent rather than coupled by the same blocker states;
5. more than 6 blockers, 4 ordinary states/blocker, 3 surfaces or 12 samples/surface are needed to create the intended depth;
6. a human needs pixel-level ray judgment or external notes for the intended route;
7. the case's only uniqueness comes from state-dependent blocker collisions;
8. globally equivalent states are treated as wrong answers;
9. an unintended solution is harmless but rejected by author-pose comparison;
10. target cells or actual current cells cannot be read without color.

---

# 11. Exact worked abstract cases

The examples use small coordinates to prove the geometry can generate the frozen deductions. They are validation examples, not guaranteed campaign levels.

## 11.1 Worked A — protected LIT emerges from geometry
Light `L1=(0,0)`. Surface W is vertical `x=8` with samples `P1=(8,2), P2=(8,4), P3=(8,6)`.

Blocker B is a thin rectangular prism footprint centered at socket `(4,2)` with two 90-degree states:
- state H: rectangle spanning approximately `x=3..5, y=1.5..2.5`;
- state V: rectangle spanning approximately `x=3.5..4.5, y=0..4`.

Ray `L1->P1` passes through the H footprint; ray `L1->P3` is steeper and can remain clear. V reaches a larger angular interval and can additionally intercept a higher sample. If target `P3` is LIT and V blocks it while H does not, V is eliminated immediately. The logical mask is not authored: it follows from ray/interior intersection.

Shipping geometry would use integer polygon vertices at a scaled coordinate factor (for example x2) to avoid decimal authoring.

## 11.2 Worked B — endpoint / extent deduction
Let `L1=(0,4)`, surface `W: x=12`, samples at `(12,1),(12,3),(12,5),(12,7),(12,9)`. Socket B lies near `(5,4)` and has a long horizontal versus tall vertical rectangular footprint.

Because rays fan from one point light, the tall state subtends a larger angular interval on W and its blocked sample run extends farther toward W's upper/lower ordered endpoints than the horizontal state. If the target changes from `L1_ONLY` to LIT exactly between samples 4 and 5, and only one B state has its derived last blocked sample at 4, that **boundary**, not total dark area, fixes B's state.

This proves endpoint/extent is a genuine consequence of point projection plus discrete samples.

## 11.3 Worked C — channel attribution
Use two lights `L1=(0,2)`, `L2=(0,8)` and a surface `W: x=12`. A blocker near the lower half of the table can intersect `L1->P` while missing `L2->P`; another upper blocker can do the converse. For a sample target `L1_ONLY`, every state intersecting `L2->P` is forbidden even if the cell would look equally dark in a single-channel silhouette.

For target `BOTH`, after protected cells eliminate several poses, if only blocker A can intersect the L1 ray and only blocker C can intersect the L2 ray, the two contributions are independently forced. Union occlusion means an extra blocker may redundantly cover a channel, so the certifier checks complete configurations; the human route reasons about remaining producer classes.

## 11.4 Worked D — cross-surface identity split
Let a blocker socket lie between two perpendicular surfaces: east wall `WE: x=12` and north wall `WN: y=12`. Two elongated blocker states can be chosen so their angular silhouette from `L1` toward sampled `WE` is identical (same sampled incidence) while their extent toward `WN` differs because the footprint rotates around the socket.

On WE the two states therefore form one observational class **with respect to that surface**. A protected LIT or exclusive-channel endpoint on WN intersects only one rotated footprint's ray, splitting the class. No arbitrary second mask is supplied: both incidence vectors come from the same transformed polygon and the same light.

This is the canonical later-game reason for multiple surfaces.

## 11.5 Worked E — chained synthesis
Two lights, two surfaces, three blockers A/B/C with 2–3 states each:
1. a LIT sample on W1 eliminates A-long and C-tall;
2. W1's last L1_ONLY sample has an endpoint reachable only by B-wide, fixing B's extent;
3. B-wide has two poses observationally equal on W1 but different on W2;
4. W2 LIT eliminates one of those poses, a cross-surface split;
5. a W2 BOTH sample now has only C as remaining L2 producer, fixing C's surviving class.

This is a dependency-connected five-step human route using one projection law. It demonstrates the intended MID/LATE grammar without special blocker powers.

---

# 12. Determinism and implementation-facing invariants

These are mechanical contracts to preserve later:
- canonical truth comes from exact authored geometry, not rendered pixels;
- derived incidence for `(case geometry, blocker state, light, sample)` is deterministic and cacheable;
- changing one blocker state cannot alter another blocker's geometry or legal state except a rare explicit collision constraint;
- shadow combination is Boolean OR independently per light channel;
- target comparison is exact over the two channel bits at every sample;
- validation accepts every physical solution, not only an authored vector;
- case serialization order must not affect truth;
- no RNG participates in solving;
- inspection is observational, never a counterfactual solver oracle.

---

# 13. Phase-4 freeze / remaining implementation-flexible details

Frozen here:
- exact logical geometry type;
- ray-interior occlusion rule;
- two-channel truth table;
- surface sample model;
- socketed discrete blocker-state grammar;
- player verbs and validation semantics;
- solution/equivalence behavior;
- campaign mechanical progression shape;
- structural difficulty knobs;
- human-route certification gates and rejection conditions.

Intentionally deferred without changing mechanics:
- exact visual-clearance numeric threshold (Technical Spec must freeze it consistently with rendering scale);
- final archetype library and case coordinates (Content Architecture);
- final player-facing names/glyphs for four states (UX);
- exact campaign groups/count above the 24-case floor (Content Architecture/Commercial Model);
- engine/rendering implementation (Technical Spec).

## Phase-4 verdict
**PASS -> proceed to Phase 5 Content Architecture.** The chosen discrete geometry produces all four promised depth sources without arbitrary masks. No production implementation has begun.

NEXT ACTION: define the authored content system and campaign grammar: blocker archetype families and reuse limits; case schema/content fields; 24-case floor and 30-case target by teaching/deduction family; sample/surface/blocker progression; case-authoring workflow; geometry-to-derived-incidence validation; human-route metadata workflow; asset reuse; demo subset; optional/floor flags; content acceptance/rejection gates; and expansion boundaries. Build a concrete campaign skeleton showing that the mechanical maxima are not used as routine difficulty inflation.
