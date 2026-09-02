# GAME #014 — PHASE 10 ADVERSARIAL REVIEW

Date: 2026-09-02
Status: COMPLETE — adversarial review passed with finite repairs and empirical gates; Specification Freeze next.
Working title: **NEGATIVE CASTING**
Authority: `START_HERE.md` -> `STATUS.md` -> `GAME_INDEX.md` -> Game #014 tournament record -> `GAME14_PRODUCT_THESIS.md` -> `GAME14_MECHANICAL_ARCHITECTURE.md` -> `GAME14_CONTENT_ARCHITECTURE.md` -> `GAME14_UX_PRESENTATION.md` -> `GAME14_COMMERCIAL_MODEL.md` -> `GAME14_TECHNICAL_SPEC.md` -> `GAME14_WHOLE_GAME_SIMULATION.md` -> this file.

## 1. Phase-10 verdict
**PASS WITH REPAIRS / EMPIRICAL GATES.** No attack found a reason to reopen the core two-light / geometry-derived blocker grammar. The strongest structural weaknesses are not in ray truth but in progression prerequisites, human-route certification rigor, hint truthfulness under arbitrary player state, duplicate/merged persistence transactions, and input-event ownership. These can be repaired without adding a new player verb, resource, blocker power, light channel, surface rule or target class.

No finding is classified `DESIGN REOPEN` in this pass.

This document is an explicit authoritative Phase-10 delta. It does not silently reinterpret earlier files: where it tightens an earlier rule, the repair is named and Phase 11 must fold it into the final frozen authority.

Classification vocabulary:
- `PASS` — existing frozen rule survives the attack.
- `REPAIR NOW` — finite clarification/tightening required before freeze; no gameplay-grammar reopen.
- `EMPIRICAL GATE` — implementation/prototype/playtest must measure it; the design already states what to do if it fails.
- `DESIGN REOPEN` — would require changing frozen gameplay grammar. None required in this review.

---

# 2. Attack matrix summary

| Area | Finding | Class | Phase-10 disposition |
|---|---|---|---|
| Geometry / exact-cover | Geometry can still compile to a CSP, but shipping depth need not be arbitrary exact-cover | REPAIR NOW | Strengthen human-route gate: MID+ routes require visible geometric entailment, not merely incidence-table elimination |
| Contribution inspection + mismatch | Manual pose probing remains possible, but inspection does not reveal counterfactuals and mismatch adds no secret state beyond already-visible actual-vs-target semantics | PASS | Preserve current anti-oracle boundary; no scores/distance/remaining-solutions |
| 2-of-3 progression | Player can skip a concept-teaching case and reach a case that assumes it | REPAIR NOW | Add explicit foundation prerequisites independent of group threshold |
| 3-surface handheld | Paper layout is plausible, not proven | EMPIRICAL GATE | Validate 1280x800 + large UI; reduce samples/surface before adding solver overlays |
| Repetition | Route signatures can converge despite different geometry | REPAIR NOW + EMPIRICAL GATE | Normalize route signatures and reject repeated late rhythms during content population/playtest |
| Hint ladder | Tier-3 authored premise can become false/misleading if it assumes deductions the player has not made | REPAIR NOW | Hints must be logically true from canonical case facts + explicitly established static premises, not inferred player knowledge |
| Accessibility | Non-color design survives; large UI can collide with secondary-surface cards | EMPIRICAL GATE | Test max supported UI scale and switch to focus-first layout rather than shrink glyphs |
| Certifier / human route | Author-entered before/after classes could be trusted without proof | REPAIR NOW | Certifier must independently entail every route reduction from canonical incidence + prior certified facts |
| Equivalence | Existing observational-equivalence semantics are sound if legality context is included | PASS | Add regression/fuzz fixtures for legality-sensitive equivalence |
| Content revisions | Stable ids alone do not prove a resume/completion is compatible after logical edits | REPAIR NOW | Persist logic/content fingerprint and require explicit migration compatibility |
| Atomic saves/cloud | Byte-level atomicity is insufficient if duplicate solves/merges replay side effects | REPAIR NOW | Completion is idempotent set fact; achievements/platform events derive after local transaction |
| Input/device race | Steam Input + engine events can double-fire one physical action; modal focus can accept stale gameplay action | REPAIR NOW | One logical action owner/event, modal action barrier, controlled repeat |
| Commercial value | 24 cases could test below 3 hours | EMPIRICAL GATE | Do not inflate; revisit price/positioning or add only independently passing cases |
| Renderer authority | Existing separation is strong | PASS | Shipping/debug assertion that renderer/physics never supplies solution truth |

---

# 3. Exact-cover / arbitrary-incidence attack

## Attack
Any finite puzzle with <=6 blockers and <=4 poses can be represented as a constraint problem. Geometry-derived masks alone therefore do **not** prove that a player experiences geometry rather than disguised exact-cover. An author could place real polygons so their derived incidence vectors behave like arbitrary set-membership rows, then document three trivial eliminations and technically satisfy the old depth count.

A particularly bad late case would have:
- coherent polygons and exact rays;
- 5 blockers x3 states;
- target-valid unique solution;
- three recorded `UNIQUE_PRODUCER` or channel eliminations;
- no useful visual endpoint, protected-space or cross-surface structure visible to a human before reading contribution tables.

The certifier would pass; the experience would still be a mask CSP.

## Finding
Geometry coherence is necessary but not sufficient. The existing named-family and connected-step requirements are good, but the route verifier needs a stronger distinction between **incidence-table truth** and **human-readable geometric entailment**.

## Classification
**REPAIR NOW — P10-R1: geometric-route grounding.**

### Authoritative repair P10-R1
For every `MID`, `LATE`, and `CAPSTONE` shipping case:
1. the intended route must still contain the existing minimum connected meaningful eliminations;
2. **at least two pre-residual steps must be grounded in a player-legible geometric relation**, meaning their rationale can be demonstrated from target + current canonical geometry without enumerating all complete configurations;
3. at least one of those two must be from `PROTECTED_LIT_ELIMINATION`, `ENDPOINT_EXTENT_ELIMINATION`, or `CROSS_SURFACE_EQUIVALENCE_SPLIT`; channel/BOTH/unique-producer may supply the other if its producer set is visually inspectable;
4. a step whose only rationale is “the derived incidence table says this pose does not work” does not count as geometric grounding;
5. a route where the shortest human explanation is a generic exact-cover/set-cover table is rejected even if machine certification passes;
6. capstones retain the stronger existing >=4 connected eliminations and >=3 families.

This does not prohibit implementation from compiling the puzzle to bitsets/CSP internally. It prohibits shipping content whose **human route** is only that representation.

## Result
Core grammar survives. No new mechanic required.

---

# 4. Contribution inspection + mismatch feedback as a probing oracle

## Attack A — contribution matrix extraction
The player can select each blocker, inspect its current pose, manually cycle the pose, and record which samples it affects. Given enough patience, they can reconstruct the entire incidence table.

## Attack B — mismatch hill-climbing
The player can change one pose, press Check, and compare mismatch locations. Repeating this for every pose may reveal which move reduces errors.

## Analysis
Attack A is not an unintended solver oracle: manually choosing a physical pose and observing its actual causal consequence is the core interaction. Hiding it would contradict the visible-cause/effect product promise. The forbidden boundary remains counterfactual batching, ranking, correctness coloring, remaining-solution counts, or automatic candidate comparison.

Attack B is weaker than it first appears because target badges and current semantic states are already visible simultaneously. Mismatch highlighting after Check mostly emphasizes a comparison the player can already perform. Removing it would not remove manual trial-and-error; it would only worsen readability.

The critical invariant is therefore not “prevent all probing.” It is: **the UI never performs counterfactual search or candidate evaluation on the player's behalf.**

## Classification
**PASS.**

### Guardrails retained for Phase 11
- contribution inspection is one selected blocker / one current pose only;
- changing pose requires a real player action and changes actual puzzle state;
- no side-by-side candidate projections;
- no mismatch count delta such as `-2 errors` after a move;
- no best-pose, correctness percentage, remaining-solution count, heatmap, or ranked recommendation;
- no automated pose sweep;
- mismatch markers never identify a responsible blocker.

No design reopen.

---

# 5. Progression / tutorial bypass attack

## Attack
The global `complete any 2 of 3 to unlock next group` rule can let the player skip a case that introduces vocabulary later content assumes.

Concrete examples:
- skip NC03, then encounter L1_ONLY/L2_ONLY-heavy content without having completed the channel tutorial;
- skip NC04, then later BOTH decomposition can be assumed without its teaching case;
- group containing NC07 can be advanced while missing the first deliberate second-surface lesson, depending on exact group assignment and solved pair.

A glossary is not a substitute for the first authored teaching solve. This is a genuine progression contradiction, not a playstyle preference.

## Classification
**REPAIR NOW — P10-R2: foundation prerequisites.**

### Authoritative repair P10-R2
Keep the 8x3 group structure and the general `2 of 3` anti-stuck rule, but add **foundation prerequisites** that cannot be bypassed by the threshold:

- `NC03` is a **CHANNEL FOUNDATION**. Cases whose intended route assumes L1_ONLY/L2_ONLY reasoning are not progression-eligible until NC03 is complete.
- `NC04` is a **BOTH FOUNDATION**. Cases that assume BOTH decomposition as prior vocabulary are not progression-eligible until NC04 is complete.
- `NC07` is a **MULTI-SURFACE FOUNDATION**. Any case whose intended route requires cross-surface reasoning is not progression-eligible until NC07 is complete.

Implementation should express this as data-driven prerequisite ids, not hard-coded case numbers. Group threshold and prerequisite graph are both checked when deriving availability.

Practical campaign behavior:
- the player still normally has multiple available cases;
- a skipped non-foundation case never blocks forward movement;
- a skipped foundation case remains clearly marked as required to unlock cases that depend on its concept;
- the UI states the prerequisite plainly without revealing a deduction solution;
- `Campaign Complete` remains all 24 floor cases.

This is a progression repair, not a new puzzle mechanic.

---

# 6. Three-surface handheld readability / memory attack

## Attack
At NC17–NC24, one primary surface plus two secondary cards competes with:
- 5 blockers;
- target/current glyph pairs;
- selected-blocker card;
- action prompts;
- large UI scale;
- 1280x800 / 1280x720;
- non-color line/glyph redundancy.

A paper layout can fit yet still force the player to memorize secondary surfaces, defeating the frozen “no external notes for ordinary cases” promise.

## Classification
**EMPIRICAL GATE — P10-E1.**

### P10-E1 acceptance test
Before late content is accepted, test representative NC17/NC20/NC24-style layouts at:
- 1280x800, default UI scale;
- 1280x720, default UI scale;
- 1280x800 at the maximum supported accessibility UI scale intended for launch;
- controller-only navigation.

Pass only if a player can, without external notes:
1. identify target class and actual class for every visible secondary-card sample;
2. identify which surface/card a mismatch belongs to;
3. switch primary surface with one action while preserving blocker focus;
4. recover the compared relationship after switching without re-reading a dense legend;
5. distinguish L1/L2/BOTH without hue.

If the layout fails, repair order is frozen:
1. reduce per-surface sample count;
2. reduce late blocker/UI density;
3. enlarge/switch the surface presentation;
4. move or collapse nonessential HUD chrome.

Do **not** solve failure by shrinking glyphs, introducing an all-surfaces solver matrix, hiding channel redundancy, or demanding memorization.

Current Steamworks compatibility guidance still recommends Deck-native 1280x800/1280x720 and complete default-controller access; this empirical gate is intentionally stricter than the platform minimum.

---

# 7. Repetition / route-signature attack

## Attack
Cases can satisfy the existing repetition signature while still feel identical if geometry changes but the cognitive rhythm stays:
`protect LIT -> compare second surface -> identify channel producer -> residual pose`.

Blocker archetype reuse can magnify this if the same few silhouettes repeatedly occupy similar angular relations.

## Classification
**REPAIR NOW + EMPIRICAL GATE — P10-R3 / P10-E2.**

### Authoritative repair P10-R3 — normalized human-route signature
Each MID+ case adds a normalized route signature that ignores blocker ids and cosmetic geometry and records:
- ordered meaningful deduction families before residual assignment;
- which surface count is active at each step;
- whether the step reasons about one state, a same-surface equivalence class, or cross-surface class;
- whether the step is geometric-boundary, channel-causal, or producer-count based;
- count of times focus must switch surfaces in the intended route;
- final pre-residual family.

Content acceptance rules:
1. adjacent MID+ cases may not have the same normalized signature unless one is an intentional tutorial reinforcement and is labeled as such;
2. no three-case MID/LATE window may share the same first two normalized operations;
3. NC17–NC24 must contain at least three materially different normalized route shapes, not merely different family labels;
4. an archetype/layout pair repeatedly producing the same decisive endpoint or cross-surface relationship is re-socketed/re-lit before inventing a new archetype.

### P10-E2 playtest gate
Blind playtest notes for NC09–NC24 must tag each solve's remembered “aha.” If testers describe several adjacent cases with the same sentence despite different certified routes, rework/reorder those cases. Machine signature diversity is a filter, not proof of perceived variety.

---

# 8. Hint leakage / hint truth attack

## Attack
Hints are authored against an intended route, but the player may request them after arbitrary pose changes and without having made the author's prior deductions. A Tier-3 hint such as “only one remaining sculpture can block Light 2 here” can be false or misleading if “remaining” assumes eliminations the player has not established.

A hint engine that tries to infer the player's internal candidate set would require solver-like tracking and risks becoming an oracle.

## Classification
**REPAIR NOW — P10-R4: state-independent hint truth.**

### Authoritative repair P10-R4
Hints must not depend on guessed player knowledge.

- Tier 1 may reference universal semantic strategy.
- Tier 2 may reference a case-specific surface/relationship that is true from canonical target/geometry.
- Tier 3 may expose **one statically certified logical premise** that is true from canonical case facts and any earlier hint premise, regardless of the player's current blocker pose vector.
- Wording such as `remaining`, `after you eliminate`, or `now only` is forbidden unless the runtime actually proves the stated candidate set from static certified premises rather than from inferred player thought.
- Tier 3 may name a sample/relationship or a candidate class to compare, but still may not state the final correct pose or replay the route.
- Hints are certified alongside the case; changing geometry/target/human-route invalidates hint certification.

The player may be physically in a pose contradicting the hint premise; the hint is about solution constraints, not a claim about the current configuration.

No solution-reveal system is added.

---

# 9. Accessibility adversarial pass

## Non-color
Target and actual semantics have glyph redundancy; light fixtures and contribution lines have channel-specific shape/style. **PASS.**

## Reduced motion
All camera/surface transitions are presentation-only; they can be shortened or replaced by cuts without changing truth. **PASS.**

## Large UI
Potential collision with secondary-surface cards remains. Covered by P10-E1. **EMPIRICAL GATE.**

## Remapping / one-handed feasibility
Core play is discrete and low-frequency, but exact one-handed presets are not required by frozen scope. Full remapping remains required. **PASS.**

## Audio dependency
No essential state is audio-only. **PASS.**

## Cognitive load
Three surfaces may fail no-notes promise; covered by P10-E1. **EMPIRICAL GATE.**

No accessibility setting may alter solution validity, achievements or campaign completion semantics.

---

# 10. Certifier / human-route consistency attack

## Attack
A data schema that stores `before_classes`, `after_classes`, premises and rationale can still become ceremonial if tooling trusts author-entered candidate reductions. Then a case could pass because metadata *claims* a deduction rather than because the deduction follows from exact incidence.

## Classification
**REPAIR NOW — P10-R5: proof-carrying route verification.**

### Authoritative repair P10-R5
The certifier independently verifies every counted human-route step.

For each route step:
1. construct the candidate class set implied by canonical case truth plus only previously certified route facts;
2. validate every declared premise against exact geometry-derived incidence/target/legality;
3. apply the step's family-specific elimination predicate;
4. recompute the resulting class set;
5. compare computed reduction with declared `before/after` metadata;
6. reject the route if the asserted reduction is not entailed, if a prerequisite step is circular, or if the step uses a fact not available to the player under the frozen UX;
7. mark `LEGALITY_CLEANUP` and `RESIDUAL_ASSIGNMENT` non-counting exactly as before.

Family-specific verifier semantics must be explicit in implementation tests. Free-text rationale is explanatory only and never proof.

P10-R1 geometric grounding is a second gate on top of logical entailment.

---

# 11. Observational equivalence / legality attack

## Attack
Two poses may have identical incidence on every sample yet differ because one participates in an illegal joint-state tuple with another blocker. Phase 4 already includes legality-context identity in equivalence, which prevents incorrect quotienting.

## Classification
**PASS**, with mandatory test coverage.

### Freeze test obligations
- equal incidence + different legality context => **not equivalent**;
- equal incidence + identical legality context => equivalent even if rendered pose differs;
- swapping an equivalent pose in every legal context must preserve target truth and legality;
- symmetry is never quotient evidence by itself;
- solution acceptance never compares against author pose.

No repair to grammar.

---

# 12. Content revision / migration attack

## Attack
Stable ids are necessary but insufficient. A case can keep `case.nc20` and pose ids while geometry or target changes. Restoring an old blocker vector into the new logical case could be syntactically valid but semantically unrelated. Similarly, retaining “completed” after a material case rewrite requires an explicit policy.

## Classification
**REPAIR NOW — P10-R6: logic fingerprint compatibility.**

### Authoritative repair P10-R6
Persistence must associate resumable/completion-sensitive data with a canonical logical fingerprint:
- `case_id`;
- `content_revision`;
- `geometry_hash`;
- `target_hash` (or a combined `case_logic_hash`).

Rules:
1. exact matching fingerprint restores pose vector directly;
2. changed fingerprint requires an explicit versioned migration declaration;
3. pose-vector migration must map stable blocker/pose ids and then revalidate legality under the destination case;
4. absent/failed mapping resets only resumable case state, never unrelated campaign completion;
5. whether old completion remains valid after a material case rewrite is an explicit migration decision, not inferred from identical `case_id`;
6. cloud merge never unions incompatible fingerprints as if they were the same active session.

This is a technical persistence repair, not gameplay change.

---

# 13. Atomic save / cloud / duplicate-solve transaction attack

## Attack A — repeated correct Check
Two correct checks or an input duplicate can fire completion twice, duplicate achievement requests, alter recency ordering, or race autosave.

## Attack B — cloud union replay
A merged save may re-trigger “new completion” side effects for cases already completed on one device.

## Attack C — primary/temp/backup ambiguity
Atomic files can all be valid but represent different generations.

## Classification
**REPAIR NOW — P10-R7: idempotent progression transactions.**

### Authoritative repair P10-R7
- Canonical completion is an idempotent fact keyed by stable `case_id` plus compatible content lineage, not an incrementing solve counter.
- Solving an already-complete case may update optional replay metadata but cannot duplicate completion rewards/unlocks.
- A solve transaction first commits local campaign state atomically; platform achievements/events are derived side effects retried from committed state.
- Every save candidate carries a monotonically increasing local `save_generation` plus stable save/profile id and integrity checksum/hash.
- Recovery chooses among validated generations; timestamp alone is insufficient authority.
- Cloud set-union of compatible completion facts does not emit duplicate first-completion events.
- Active pose vectors are not monotonic facts and follow P9-C6/P10-R6 conflict rules.
- If a crash occurs after local completion commit but before platform achievement unlock, later reconciliation unlocks the achievement from campaign state.

No server or online authority is introduced.

---

# 14. Device switching / action repeat / modal focus attack

## Attack A — double source
Steam Input and ordinary engine gamepad input may both represent one physical button, causing two state changes.

## Attack B — held repeat
A held key/button can cycle poses too quickly, landing two states away while animation shows one transition.

## Attack C — modal race
A gameplay `Check` or `State Next` event already queued when Pause/Reset confirmation opens can activate a modal control or mutate the case behind the modal.

## Attack D — glyph churn
Mouse motion or trackpad noise switches prompt family while controller focus remains, producing flicker.

## Classification
**REPAIR NOW — P10-R8: logical action ownership and modal barrier.**

### Authoritative repair P10-R8
1. Each physical event is normalized to at most one logical action; Steam Input and fallback engine input cannot both own the same event path simultaneously.
2. Pose mutation / Check / Undo / Redo default to edge-triggered actions. Held-repeat is disabled unless an explicit accessibility/input option enables a bounded repeat rate; UI navigation may repeat separately.
3. Opening a modal creates an action barrier: gameplay mutations are ignored until the modal closes and fresh post-open input is received.
4. Closing a modal restores previous valid blocker/surface focus but does not replay the button used to close it.
5. Prompt-device family changes only on deliberate accepted action from a new family, preserving P9-C1; passive pointer motion cannot churn glyphs.
6. Automated QA includes same-frame duplicate events and rapid controller<->keyboard/mouse alternation.

Puzzle truth remains unaffected by device family.

---

# 15. Renderer / physics authority attack

## Attack
A production developer may be tempted to use Godot collision, visual shadow maps, screen-space sampling or scene-node transforms as the “easy” answer for runtime truth while keeping the exact certifier only in tools. That creates runtime/editor disagreement.

## Classification
**PASS with freeze assertion.**

Phase 8 already forbids this. Phase 11 must retain a testable invariant:
- runtime semantic target evaluation consumes only core exact/derived logical incidence keyed from canonical geometry;
- debug builds can recompute reference incidence and assert cache equality;
- renderer/physics outputs are presentation-only;
- changing renderer backend, shadow quality, resolution or animation cannot change a semantic cell.

Any implementation that violates this is nonconforming, not an allowed interpretation.

---

# 16. Commercial scope/value attack

## Fresh context — 2026-09-02
A current Steam check still shows `Railbound` at a $12.99 base price with a 240+ puzzle promise, reinforcing that Negative Casting cannot justify $11.99 by raw case count. Current Steam Deck documentation continues to require complete default-controller access and recommends 1280x800/1280x720 support, consistent with the product's handheld emphasis.

## Attack
24 cases may be excellent but solve faster than the 3–5 hour thesis. Inflating weak cases would damage the design more than a lower price or shorter-product framing.

## Classification
**EMPIRICAL GATE — P10-E3.**

### P10-E3 release/value gate
Measure blind first-completion time after implementation and content population.
- If median first completion is plausibly within ~3–5 hours, the frozen $11.99 target remains credible subject to polish/market review.
- If materially below ~3 hours, first reconsider price/positioning and only then consider NC25–NC30 cases that independently pass every quality gate.
- Do not manufacture duration through slower animation, mandatory repeated checks, denser sample grids, hint friction, filler cases or forced replay.
- If added cases repeat normalized route signatures, ship fewer cases and price/position honestly.

This is intentionally an implementation/release decision, not a reason to reopen mechanics today.

---

# 17. Whole-design exploit / ambiguity checks

## State-dependent blocker collisions
Rare explicit illegal joint states remain allowed only for physical safety and do not count toward depth. **PASS.** If authoring begins using them as a major logic family, that is a design reopen.

## Accepted multiple solutions
All target-valid physical solutions are accepted; meaningful class uniqueness is authoring preference, not hidden author-pose enforcement. **PASS.**

## Check spam
No penalty and no incremental secret feedback. **PASS.**

## Undo/reset spam
Unlimited use is compatible with product promise. **PASS.**

## Surface switching spam
UI-only, truth-independent. **PASS**, subject to P10-R8 event handling.

## Hint purity achievements
Forbidden already. **PASS.**

## Optional cases redefining campaign completion
Forbidden already. **PASS.**

## DLC mechanic smuggling
Third lights, transparency, moving lights, mirrors, continuous placement etc. require reopen. **PASS.**

## External notes
Not required by specification; P10-E1 validates late content. **EMPIRICAL GATE.**

---

# 18. Repairs frozen by Phase 10

These are authoritative deltas to be folded into Phase 11 final freeze:

1. **P10-R1 — Geometric-route grounding:** MID+ routes need at least two player-legible geometric/causal pre-residual deductions; incidence-table truth alone does not count.
2. **P10-R2 — Foundation prerequisites:** progression adds data-driven prerequisite cases for semantic foundations, specifically NC03 channel, NC04 BOTH, NC07 multi-surface, while retaining general 2-of-3 anti-stuck groups.
3. **P10-R3 — Normalized route signatures:** content diversity checks compare cognitive route shape, not only family labels and geometry counts.
4. **P10-R4 — State-independent hint truth:** authored hints cannot assume untracked player deductions; every premise is statically certified.
5. **P10-R5 — Proof-carrying human-route verification:** certifier independently entails each counted reduction from canonical facts and prior certified steps.
6. **P10-R6 — Logic fingerprint compatibility:** resume/completion migrations use geometry/target logic fingerprints plus explicit migrations, not stable ids alone.
7. **P10-R7 — Idempotent progression transactions:** completion is a set fact; local atomic commit precedes retriable platform side effects; generations disambiguate saves.
8. **P10-R8 — Logical action ownership/modal barrier:** one physical event -> at most one logical action; no queued gameplay mutation crosses modal boundaries; deliberate-device prompt switching only.

None adds a new puzzle rule.

---

# 19. Explicit empirical gates carried to implementation

Only questions that genuinely require a prototype/build/playtest remain empirical:

- **P10-E1:** NC17–NC24 three-surface readability and cognitive load at 1280x800/1280x720 and launch max UI scale.
- **P10-E2:** perceived repetition across NC09–NC24 despite certified normalized route diversity.
- **P10-E3:** blind first-completion duration/value; if materially under 3 hours, adjust product positioning before inflating content.
- actual world-space visual-clearance threshold for near-ray geometry after renderer/camera exists;
- final 60-fps target / 30-fps floor performance on Deck-class hardware;
- whether Tier-3 hint ladder is sufficient for stuck players. Adding a full solution reveal remains a product-design reopen, not an implementation assumption.
- exact visual legibility of every blocker archetype/silhouette and semantic glyph at target devices.

These gates have defined failure responses; they are not unspecified game design.

---

# 20. Design-reopen triggers after Phase 10

Phase 11/implementation must reopen design rather than improvise if any of these becomes necessary:
- arbitrary authored incidence masks to make content interesting;
- third logical light or new target class;
- transparent/refractive/special blockers;
- moving/free-placement lights or blockers;
- continuous precision rotation/translation;
- solver-like counterfactual overlays required to make late cases readable;
- progression whose teaching dependencies cannot be expressed with finite prerequisites;
- a hint/solution system that auto-solves or changes completion semantics;
- state-dependent collision becoming a primary deduction family;
- procedural/infinite content required to rescue value;
- renderer/physics becoming logical authority.

None is currently required.

---

# 21. Phase-10 acceptance checklist

- [x] Fun/repetition attacked.
- [x] Geometry-derived exact-cover risk attacked.
- [x] Contribution inspection + mismatch probing attacked.
- [x] 2-of-3 progression/tutorial bypass found and repaired.
- [x] NC17–NC24 handheld/memory load converted to explicit empirical gate.
- [x] Blocker/case route repetition tightened with normalized signatures.
- [x] Hint leakage/state-assumption contradiction found and repaired.
- [x] Non-color/large-UI/reduced-motion paths attacked.
- [x] Certifier/human-route proof obligation tightened.
- [x] Equivalence semantics attacked.
- [x] Content-revision migration tightened with logic fingerprints.
- [x] Atomic save/cloud/duplicate-solve semantics tightened.
- [x] Action repeat/modal/device switching tightened.
- [x] Commercial value attacked without content inflation.
- [x] Renderer/logical authority boundary reasserted.
- [x] No production implementation started.
- [x] No Gmail/test-email action performed.

## Phase-10 result
**PASS -> proceed to Phase 11 Specification Freeze.**

`DESIGN COMPLETE` remains **NO** until Phase 11 folds all authoritative deltas into a finite stand-alone freeze, checks contradictions/unknowns, and produces final acceptance/authority order.

## NEXT ACTION — GAME #014 PHASE 11 / SPECIFICATION FREEZE
Create `GAME14_FINAL_FREEZE.md` as the stand-alone implementation design authority. It must:
1. reconcile Phases 3–10 and explicitly incorporate P9-C1..C6 plus P10-R1..R8;
2. resolve the progression prerequisite graph around NC03/NC04/NC07 without losing the general 2-of-3 anti-stuck structure;
3. define final case/content/certifier/hint/persistence/input acceptance criteria;
4. list only truly empirical implementation gates (P10-E1..E3 + renderer clearance/performance/hint sufficiency);
5. define authority precedence so a fresh implementation session never needs to choose between contradictory earlier files;
6. verify every important unknown is either answered or intentionally implementation-flexible;
7. set `DESIGN COMPLETE = YES` only if no gameplay invention remains necessary;
8. if complete, attempt migration to the dedicated `Mikayilzade/negative-casting` repository if it exists; if unavailable, freeze the full Game #014 archive as NON-ACTIVE safety copy, update `GAME_INDEX.md`, advance `STATUS.md` immediately to Game #015 Phase 1, and continue the factory rather than blocking on migration.