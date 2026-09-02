# GAME #014 — PHASE 3 PRODUCT THESIS LOCK

Date: 2026-09-02
Status: COMPLETE — thesis locked; Mechanical Architecture next.
Selected working concept: **Negative Casting**
Authority: `START_HERE.md` -> `STATUS.md` -> `GAME_INDEX.md` -> Game #014 tournament record -> this file.

## 1. Product identity
**Working title:** NEGATIVE CASTING. The title is descriptive/internal and may change later without changing mechanics.

**Genre framing:** compact premium spatial-deduction puzzle game about sculpting with shadows.

**Lead platform:** PC / Steam, with controller and handheld-sized readability treated as baseline rather than post-port extras. Mouse is supported but no mechanic may require pixel precision.

**Target player:** players who enjoy authored deduction puzzles where the state is visible, rules are deterministic, and success comes from eliminating classes of possibilities rather than executing dexterous moves. The player should tolerate compact symbolic information but should not need external notes for ordinary cases.

**One-sentence hook:** Arrange a few strange objects between fixed lights so several walls receive exactly the required pattern of light, single-light shadow, and overlapping shadow.

**Core fantasy:** you are not drawing silhouettes directly; you are staging physical objects whose simultaneous projections create a designed piece of negative space on multiple surfaces.

## 2. Player promise
A good case should create the feeling: “I know this object must turn this way because that bright edge cannot be touched — and now its shadow on the other wall tells me which object owns the dark patch.” The game promises visible cause/effect, short chains of geometric deduction, and a satisfying final reveal when all projection surfaces agree.

The game does **not** promise freeform sculpture, physics simulation, hidden rules, procedural infinite puzzles, or sandbox optimization.

## 3. Product structure
- Finite authored premium campaign.
- Design floor: **24 shipping-quality cases** if every case passes human-route certification.
- Target: **30 cases** only if additional cases remain non-repetitive; quantity never overrides the gate.
- Expected first completion: roughly **3–5 hours**, subject to later whole-game simulation/playtest.
- Typical case target: 4–12 minutes after onboarding; early cases shorter, capstones potentially 15–25 minutes.
- No timer, lives, consumable hint currency, score grind or run reset.
- Cases are replayable individually.
- Campaign unlocks mostly linearly in small groups so a player blocked on one case can have a limited alternate case without turning progression into a map-management game.

## 4. Exact core loop at thesis level
1. **Read target surfaces.** Each target cell communicates one of four semantic states: fully lit, shadowed from light 1 only, shadowed from light 2 only, or shadowed from both. Encoding is redundant and not color-dependent.
2. **Inspect the casting table.** Fixed lights, surfaces, blocker sockets and allowed blocker orientations/positions are visible. Selecting a blocker may show its own physically determined projection paths/masks; this is explanation, not solution scoring.
3. **Deduce.** Protect required-lit cells, identify impossible orientations, use projection endpoints/extents, attribute single-channel shadows, and compare the same blocker's consequences across surfaces.
4. **Adjust one blocker state.** Discrete controller-friendly actions only; no continuous precision placement.
5. **Observe physical result.** Shadows update immediately. The game may show current semantic cell states but must not recommend a move or label a candidate as “correct.”
6. **Commit/check.** Player requests validation when ready. Exact match across every target surface solves the case; mismatch remains inspectable and reversible with no punishment.
7. **Advance/replay.** Completion records the case and opens the next campaign group.

## 5. Frozen source of depth
Depth comes from recombining four consequences of the same projection rule:
- **protected negative space:** required LIT cells eliminate every state whose projection touches them;
- **extent/endpoint geometry:** coherent shadow boundaries constrain blocker orientation/extent;
- **channel attribution:** L1_ONLY/L2_ONLY/BOTH distinguish why darkness exists, not merely whether it exists;
- **cross-surface identity:** the same blocker state projects onto several surfaces, allowing one view to split states indistinguishable on another.

Later phases may refine geometry and content parameters but must not substitute arbitrary masks or bolt-on powers for this grammar.

## 6. Differentiation
The commercial/mechanical distinction is **multi-surface negative-space deduction with channel-specific shadows**. Marketing should show a small physical casting table, two visibly distinct light origins, an object rotating between discrete states, and multiple walls changing together. Avoid presenting the game as a generic grid CSP or a technical lighting editor.

The closest surviving internal tournament concepts were rejected for reasons that define the boundary: no redirecting mirror-path bookkeeping; no theater set-cover game. Those mechanics are not latent features.

## 7. Presentation thesis
Stylized tabletop/studio diorama rather than realistic ray-traced room. Blockers should have memorable sculptural silhouettes and sockets; walls/screens carry large target cells/panels. Actual shadows may be visually soft/stylized, but the logical state is exact and discrete. A target glyph layer ensures semantic readability independent of rendering and color vision.

A short clip must communicate: rotate object -> its shadow changes on wall A **and** wall B -> target symbols flip toward the requested pattern. If that cannot read without explanatory text, presentation has failed.

## 8. Demo thesis
Target demo: roughly 20–30 minutes / 6–8 cases.
- Case 1: direct shadow and protected LIT.
- Case 2: L1-only exclusion.
- Case 3: BOTH decomposition.
- Case 4: endpoint/extent.
- Case 5: first meaningful two-surface identity split.
- Case 6: short synthesis.
Optional 7–8 only if pacing remains strong.

The second-surface reveal is the demo's proof that the game is more than silhouette matching.

## 9. Scope ceiling
At thesis lock:
- two logical light channels are the baseline and campaign-wide semantic vocabulary;
- ordinary cases use a small number of socketed blockers and discrete states;
- multiple projection surfaces are allowed, with three surfaces reserved for later complexity where readable;
- geometry is deterministic/discrete even if rendered attractively;
- no player-authored arbitrary target/mask editor is required for launch;
- no 3D free-camera spatial navigation is required; camera/presentation exists to inspect one compact puzzle table;
- no narrative campaign dependency; light framing/flavor is allowed but bespoke story content cannot become production-critical.

## 10. Explicitly out of scope
- continuous physics placement or precision aiming;
- real-time action/timing challenges;
- free-angle mirror reflection mechanics;
- moving lights during a solve unless a later mechanical phase proves this is already equivalent to the frozen blocker-state grammar (default: out);
- special blocker powers/materials, transparency, colored-light mixing, refraction or penumbra as puzzle rules;
- arbitrary authored bitmask projections disconnected from geometry;
- procedural infinite campaign as a launch requirement;
- roguelike runs, deckbuilding, crafting, upgrades, currencies, energy systems or live-service retention;
- multiplayer/co-op as launch scope;
- mandatory external note-taking;
- color-only information;
- production implementation in the factory.

## 11. Product quality gates carried forward
A case cannot ship merely because a solver proves unique.
- Every MID/LATE case must document >=3 meaningful human class-elimination deductions before residual trial.
- Projection masks must be generated from the same coherent geometry contract used by presentation/certification.
- Multi-surface cases must remain readable at handheld scale.
- Inspection tools may expose physical causality of the selected current state, never counterfactual correctness or solver recommendations.
- If later mechanical specification cannot define a compact deterministic projection model that preserves endpoint/cross-surface deductions, the design returns to REWORK rather than faking geometry with masks.

## 12. Phase-3 lock result
**PASS.** Negative Casting has a bounded product identity, a finite campaign thesis, a demo promise, a frozen source of depth and explicit exclusions. No production implementation has begun.

NEXT ACTION: **Phase 4 Mechanical Architecture.** Define the exact discrete geometry/projection contract; blocker/socket/state model; target semantics; surface topology and limits; legal actions; validation; undo/reset; campaign unlock logic; difficulty knobs; human-route metadata/certifier requirements; symmetry/equivalence handling; and edge cases. Build enough abstract worked examples to prove that geometry actually produces the four frozen deduction families. Do not proceed to content architecture until the projection model is deterministic and non-arbitrary.
