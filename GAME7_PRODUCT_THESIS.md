# GAME #007 — LAST KNOWN SHAPE — PRODUCT THESIS LOCK

Last updated: 2026-08-30
Phase: **3 — Product Thesis Lock**
Selected concept: **G7C02 Last Known Shape**
Product thesis: **LOCKED**
Production implementation started: **NO**
DESIGN COMPLETE: **NO**

## 1. Product identity
Working title: **Last Known Shape**. Internal canonical label only; commercial naming review remains later.

PC/Steam-first premium single-player systemic puzzle. Offline-capable. Controller + keyboard/mouse baseline. Steam Deck-friendly target. No reflex platforming, combat, live service, procedural grind, free-camera perspective hunting or arbitrary computer-vision interpretation.

Genre framing: **systemic observation / transformation puzzle**. Player-facing copy should explain the physical rule rather than use quantum jargon.

## 2. Frozen hook
**Observe an object in one exact form, walk away, and that last remembered shape becomes physically real — until you deliberately observe it differently.**

Internal causal sentence: **Last committed observation becomes authoritative form when direct observation ends.**

## 3. Core fantasy
The player operates a strange but rule-bound facility where observation is a physical write operation. Marked Observation Frames do not merely show objects from another angle: they expose an exact deterministic candidate remembered form. Committing an observation stores that form. When the object is no longer directly observed under the declared rule, its remembered form becomes its physical/functional authority.

The fantasy is not `trick the camera`. It is **choose what reality is allowed to remember, preserve that memory while exploiting it, then overwrite it at the right moment**.

## 4. Frozen repeated verb
Primary repeated verb: **OBSERVE / COMMIT an object's candidate form from an authored Observation Frame.**

Supporting verbs: ordinary traversal, push/place/interact where mechanically necessary, and free Undo/Redo. Supporting interaction must not outgrow OBSERVE as the design center.

Every observation commit must communicate before confirmation:
- which object will be written;
- exact candidate remembered form;
- which prior remembered form will be overwritten;
- immediately knowable affordance changes.

No hidden pixel classification, free-camera threshold, precision alignment or ambiguous silhouette is allowed to determine authoritative state.

## 5. Core loop
1. Inspect current remembered forms, physical affordances, frames, receivers and access.
2. Predict which form must be preserved or overwritten next.
3. Enter/select an authored Observation Frame.
4. Preview exact candidate form.
5. Commit OBSERVE.
6. Leave/end direct observation so the committed form becomes authoritative under global rules.
7. Traverse/place/use the resulting object affordance.
8. Manipulate access/occluder/object state to make a different observation possible.
9. Preserve or overwrite memories in deliberate order.
10. Undo/Redo freely when testing a hypothesis.

Mature play alternates observation decisions and physical exploitation; it must not become a detached form-selection menu.

## 6. Target player and session
Primary: players who enjoy authored systemic puzzles, strong visual `aha` moments, small rule sets with deep recombination, and experimentation without dexterity punishment.

Target session: 10–30 minutes, roughly 1–4 cases depending difficulty.
Target first-clear product: approximately 4–7 hours minimum; 5–8 hours preferred if causal variety validates.
Target campaign at thesis stage: ~30–36 main cases plus a compact demo and only genuinely distinct optional mastery/remix cases.

## 7. Frozen depth sources
Allowed primary depth sources:
- preserve versus overwrite;
- different forms having conflicting affordances;
- frame-specific deterministic transforms/masks;
- access changed by current remembered form;
- one object acting as an authored occluder/state input for another observation;
- observation order across 2 objects;
- physical relocation between observations;
- destructive re-observation;
- state-dependent value of the same form later.

Possible only after proof: 3 simultaneously reasoning-critical remembered objects.

Forbidden baseline growth:
- arbitrary free-camera perspective scaling;
- pixel/image recognition;
- continuous silhouette authority;
- dozens of bespoke magical observation rules;
- combat;
- precision platforming;
- stealth timing;
- recursive portals/non-Euclidean adjacency;
- player-created geometry;
- physics-sandbox authority;
- time clones/replay;
- RPG upgrades/currencies;
- procedural level generation as content substitute.

## 8. Differentiation boundary
The game is not sold as `perspective changes reality`. Authored Observation Frames make observation a discrete persistent write to remembered physical form. The puzzle is primarily **which memory to preserve, when to overwrite it, and how one remembered state changes access to the next observation**.

This boundary separates the product from free-camera perspective/scale puzzlers and from temporal replay games. Existing factory games are exclusion history only; no adjacency rewiring, conserved tension, transferable collision property, audio-led inference, map-authority bureaucracy or cargo identity may enter as hidden canon.

## 9. Presentation thesis
Physical world first. Observation Frames are unmistakable authored locations/devices. Candidate form is shown before commit using redundant shape/outline/material cues. Current remembered form remains inspectable without requiring memory of prior steps.

A silent short clip must be able to show: preview form -> commit -> leave observation -> physical transformation -> exploit -> second preview threatening overwrite.

Reduced motion must preserve causal legibility. Color and audio are never sole state carriers.

## 10. Progression thesis
Progression is cognitive, not statistical.

Early: observation commits persistent form; overwrite is deliberate.
Middle: form tradeoffs, masks, access self-block, preservation.
Mature: two-object order, authored occlusion dependencies, staged relocation, destructive re-observation and state-dependent reuse.
Late: synthesize these without introducing a new magical subsystem.

No XP, upgrades, currencies, randomized loot, daily systems or permanent power tree.

## 11. Commercial frame
Premium PC/Steam first. Working price range remains intentionally unfrozen until Phase 7/current market review; likely compact-premium territory if 5–8 hours and causal variety validate. Free representative demo is strongly preferred if empirical hook comprehension passes.

No ads, MTX, mandatory account or online dependency.

## 12. Scope floor / ceiling
Floor for a viable full product: 28 strong main cases, small reusable object/form vocabulary, 5–7 observation transform/mask families, one- and two-object reasoning, complete controller/keyboard path.

Ceiling: 36 main cases + <=6 proven mastery/remix cases; normally <=2 reasoning-critical objects, <=4 relevant frames/case; no narrative-heavy exploration layer or bespoke mechanic pileup.

If content variety cannot sustain this floor with the frozen vocabulary, cut/kill rather than inflate with unrelated systems.

## 13. Empirical gates retained
EG7-01 form prediction: after tutorial, players predict committed form before OBSERVE.
EG7-02 preview authority: no unpreviewed camera/pixel detail changes authoritative form.
EG7-03 hook comprehension: mute clip communicates persistent last-observed-form rule.
EG7-04 mature variety: representative slice proves >=3 causal families.
EG7-05 two-object readability: observation order understandable without detached table.
EG7-06 accessibility/presentation: reduced motion and non-audio play preserve causal understanding.

These are prototype/playtest gates, not excuses to leave rules undefined.

## 14. Product thesis lock
**G7C02 Last Known Shape is selected and Phase 3 is COMPLETE.**

Phase 4 may define exact form authority, observation lifecycle, occlusion transforms, object/receiver states, movement/interactions, Undo/Redo, failure, deterministic ordering, solver representation and acceptance tests. It may not silently turn the game into free-camera perspective manipulation or add unrelated feature families to manufacture depth.

## NEXT ACTION
Phase 4 — Mechanical Architecture. Specify the exact deterministic domain contract, including: observation eligibility/preview/commit/end-of-observation transition; remembered-form overwrite; authored frame transform and occluder rules; physical affordance mapping; object movement/placement; multi-object ordering; legality and rejection reasons; stable event ordering; Undo/Redo/idempotency; win/fail/dead-state policy; solver/canonical state; difficulty knobs; anti-dominant-strategy fixtures; and >=40 acceptance tests. Resolve every paper-level ambiguity before Phase 5.
