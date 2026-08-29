# GAME #006 — STITCHSPACE — PHASE 11 SPECIFICATION FREEZE

Last updated: 2026-08-29
Phase: **11 — Specification Freeze**
Selected concept: **G6C01 Stitchspace**
Production implementation started: **NO**
DESIGN COMPLETE: **YES**
Migration complete: **NO**

This file freezes the canonical design package for Stitchspace. A fresh implementation session should be able to build the game without inventing important gameplay. Unknowns that require real prototype/playtest evidence are retained as explicit empirical gates rather than guessed closed.

---

# 1. Frozen product identity

**Working title:** Stitchspace

**Platform/product:** PC / Steam first, premium, single-player, offline-capable, controller + keyboard/mouse, Steam Deck-friendly.

**Genre:** systemic spatial / topology puzzle.

**Hook:** Rewire which rooms physically touch by relocating an endpoint of a scarce persistent seam; every new adjacency destroys the old adjacency.

**Core fantasy:** a spatial seam technician changes physical neighboring relationships between stable rooms, using the same scarce relationship repeatedly to route the player/objects and exploit useful disconnection.

**Primary repeated verb:** `MOVE_SEAM_ENDPOINT`.

The game is not a portal-placement game, folding game, construction sandbox, momentum game, physics sandbox, graph editor, combat game, progression economy or live service.

---

# 2. Frozen gameplay vocabulary

Canonical primitive families:
1. stable rooms with authored local traversal;
2. visible authored edge sockets;
3. fixed ordinary passages;
4. scarce persistent seams with exactly two endpoints;
5. atomic endpoint replacement;
6. finite visible crossing orientation mapping;
7. deterministic discrete entities;
8. bounded seam/socket occupancy locks;
9. deterministic automatic mover boundaries where authored;
10. objectives/mastery expressed through global rules and data, never bespoke transition callbacks.

Normal campaign uses 1–2 seams. Three seams are optional exceptions only after solver/readability proof; no shipped campaign arc depends on a third seam. C34 defaults to two seams.

---

# 3. Frozen command semantics

Canonical semantic command:

`MOVE_SEAM_ENDPOINT(seam_id, endpoint_selector, target_socket_id, expected_revision/hash, command_id)`

Validation occurs against one immutable pre-command canonical state. Structural illegality rejects before mutation. Legal but strategically poor edits commit.

Accepted commit is atomic:
- remove OLD seam adjacency;
- detach selected endpoint;
- attach it to target socket;
- create NEW adjacency to the persistent opposite endpoint;
- recompute derived orientation/mapping;
- resolve deterministic immediate consequences to the next canonical command boundary;
- increment revision and produce one canonical history child.

There is never an authoritative intermediate state where OLD and NEW adjacency coexist.

Preview is presentation-only and may never mutate revision, hash, history or canonical state.

---

# 4. Frozen deterministic ordering

Gameplay authority is discrete. Renderer, scene-tree order, animation interpolation, frame delta and physics callback order never decide results.

At canonical event boundaries:
1. previously accepted transition consequences resolve fully to the next declared stable boundary;
2. mover intents for the same step are collected;
3. global rule priority resolves intent class;
4. ties resolve by stable entity ID;
5. crossing/socket locks derive from canonical state;
6. identical pre-state + identical semantic input yields identical canonical post-state/hash.

Every mover/occupancy case must provide a Step-compatible baseline fixture and may not depend on wall-clock timing.

---

# 5. Frozen orientation contract

Orientation is finite, visible and geometric. Crossing maps local facing from source boundary to destination boundary using authored socket frames/lane mapping.

Player-facing rules:
- no numeric angles or compass arithmetic are required;
- orientation-sensitive consequences must be previewable from physical boundary geometry/arrows/shape;
- no case may introduce a private orientation law;
- no challenge may depend on remembering hidden orientation state.

---

# 6. Frozen Undo / Redo / idempotency

One accepted semantic player command plus all deterministic immediate domain consequences before the next command opportunity forms one history transaction.

Undo restores the exact parent canonical snapshot/hash. Redo restores the exact child while the branch remains intact. A new accepted command after Undo truncates Redo descendants.

Duplicate handling:
- same `command_id` + identical payload returns the already-recorded result with no second mutation;
- same `command_id` + different payload hard-rejects;
- stale expected revision/hash rejects before mutation.

Unlimited ordinary Undo/Redo is part of baseline design and may not be punished by campaign completion or baseline achievements.

---

# 7. Frozen content architecture

Main campaign target: **C01–C34**.

Demo: **DEMO01–DEMO05**.

Optional remixes/mastery: target **R01–R08**, only if they pass changed-causal-dependency review. Weak remixes are cut before adding systems.

Campaign progression teaches replacement first, then useful disconnection, orientation, object/entity ordering, occupancy, two-seam reasoning, loop creation/breaking and state-dependent seam reuse.

From C15–C34 every case stores a compact dominant causal-skeleton vector including relevant dimensions such as:
- useful cut/isolation;
- orientation dependency;
- seam preservation/inversion;
- entity ordering;
- loop creation/destruction;
- state-dependent target value;
- occupancy/mover sequencing;
- multi-seam role swap.

Hard content-diversity constraints:
- no consecutive three-case mature window shares one dominant skeleton family;
- every five-case mature window contains >=3 materially distinct families;
- C24–C34 contains >=5 families total;
- no one family occupies >30% of C15–C34.

Art/layout changes alone do not count as causal variety.

Every main case after C06 must require more than a one-command blind target guess. Mature cases must include state-dependent later target value.

C07–C10 explicitly document why lost adjacency materially matters.

---

# 8. Frozen dominant-strategy defenses

Representative mature content must prevent one policy from solving the game:
- direct current-room-to-goal stitching is not shortest in >=75% of representative mature cases;
- permanent lifeline preservation must fail or become strategically inferior in relevant cases;
- both endpoints must matter across the mature campaign, except explicit literacy exceptions;
- universal move-count minimization is not the mastery economy;
- locally attractive legal edits may create informative bad states rather than hidden punishment.

Free Undo is preserved. Anti-bruteforce design comes from causal state dependence, not punishment or target-count inflation.

---

# 9. Frozen solver / validation contract

Solver uses only gameplay-relevant canonical domain state. It excludes presentation, camera/focus, animation interpolation, save-generation metadata, explanatory provenance and ordinary Undo ancestry.

Tooling must expose deterministic metrics:
- canonical states visited;
- transitions expanded;
- duplicate states pruned;
- shortest semantic command length;
- solution count up to configured cap;
- termination reason.

Every shipped main case must terminate within a configurable practical authoring/CI budget. Over-budget cases are simplified or cut; bespoke semantic pruning is forbidden.

Solver may detect dead states for tooling/tests, but runtime exposes no default dead-end oracle.

Case data may narrow legal destinations but may not redefine global transition semantics or execute bespoke gameplay callbacks.

---

# 10. Frozen UX / presentation contract

The physical world is the primary play surface. A compact topology overview may assist inspection but may not become the authoritative detached graph puzzle.

Required edit sequence:
1. choose seam;
2. choose endpoint;
3. inspect persistent pair identity;
4. browse deterministic semantic target focus;
5. preview OLD relationship to be destroyed and NEW relationship to be created;
6. preview orientation consequence;
7. confirm/cancel;
8. observe atomic replacement and resulting physical consequence.

With >=2 seams, pair identity is persistent and redundantly encoded by shape/pattern/icon; color may supplement but never carry meaning alone.

Selecting one endpoint highlights both endpoints of that seam. Browsing targets never hides the relationship that will be destroyed. Focus movement cannot silently switch seams.

Reduced motion may simplify animation but cannot hide OLD→NEW causality.

Invalid edits use bounded reason codes + localized templates.

---

# 11. Frozen input / accessibility contract

Required complete paths:
- controller only;
- keyboard only;
- mouse + keyboard;
- Steam Deck built-in controls.

Core endpoint editing never requires precision dragging or reflex timing.

Controller/keyboard use an authored semantic focus graph independent of pixel geometry. Pointer selection resolves to the same semantic object model.

Remapping must preserve recoverable access to Confirm, Cancel, navigation and Pause/Menu.

At 1280×800 every required puzzle fact is visible without hover-only text or tiny mandatory labels.

Accessibility-valid campaign play includes:
- Pause/Step for mover cases;
- unlimited Undo/Redo;
- reduced motion;
- high-contrast/redundant seam identity;
- remapped controls;
- muted/non-audio play.

Color and audio are never sole carriers of puzzle state. Accessibility use does not invalidate baseline completion or achievements/mastery.

---

# 12. Frozen persistence / Cloud / demo-import contract

Only committed canonical command boundaries are durable.

Persistence uses verified temp/primary/backup generations with integrity checking and fault-injection tests. Recovery yields an exact prior or exact later committed generation, never a hybrid topology/history state.

Active puzzle branches from different devices are never structurally merged. Explicit monotonic profile facts may merge only through documented commutative rules.

Demo→full import is explicit, versioned and idempotent. Compatible profile/settings/progress facts may import monotonically; active demo puzzle state is never guessed equivalent to campaign branch state.

---

# 13. Frozen commercial frame

Premium purchase; no ads, MTX, consumables, currencies, XP, dailies, FOMO or mandatory online account.

Working list-price target: **$17.99 USD**.
Release-review band: **$14.99–$19.99 USD**.

Final price is deliberately not paper-frozen. Phase 12G must consider:
- expert first-clear time distribution;
- broader-target first-clear time distribution;
- final validated case/remix count;
- perceived causal variety/value;
- demo comprehension and interest.

Do not inflate case count with weak variants to defend price.

Demo must prove before CTA:
1. persistent seam relationship;
2. endpoint replacement destroys old adjacency;
3. orientation matters;
4. useful disconnection matters;
5. seam reuse after physical/entity state change;
6. final synthesis is not honestly describable as ordinary portal placement.

Purchase CTA appears only after DEMO05 causal reveal.

---

# 14. Frozen scope / cut ladder

1.0 explicitly excludes:
- multiplayer/co-op;
- procedural campaign;
- user level editor/Workshop;
- open world;
- combat;
- inventory/crafting;
- narrative branching;
- physics sandbox;
- free portal placement;
- momentum/flinging;
- recursive portal rendering requirement;
- folding/scaling/gravity manipulation systems;
- time clones/property transfer;
- seam upgrade/rarity/element systems;
- currencies/XP/skill trees;
- live service/dailies/FOMO;
- large bespoke dialogue/voice campaign;
- mobile-first design;
- bespoke per-case transition code.

If schedule/budget contracts:
1. cut weak remixes first;
2. cut weak late cases second while preserving a strong finale;
3. simplify/remove optional 3-seam experiments;
4. preserve core C01–C24 teaching/depth arc and demo proof;
5. never rescue scope by feature accretion.

---

# 15. Frozen technical direction

Initial implementation pin: **Godot 4.7.2-stable**, with GDScript-first unless a measured implementation need justifies a bounded alternative.

Architecture authority:
- deterministic Domain Core;
- Presentation layer that derives visuals/input affordances from canonical state;
- Platform Adapter for persistence/Steam/platform integration;
- shared Domain Core for runtime, content compiler, validator, solver and replay verification.

Canonical serialization uses stable ordering and SHA-256-compatible content/state hashing. Runtime IDs are stable semantic IDs, not scene-instance identity.

Production implementation order follows Phase 12A–12H from factory rules.

---

# 16. Empirical gates retained for Phase 12G

These are explicitly **NOT paper-PASS**.

- **EG-01 Portal comprehension:** >=75% naive testers explain adjacency replacement/old-connection loss after one bounded tuning pass.
- **EG-02 Hook-content validity:** >=5/8 representative grayboxes materially depend on lost adjacency, orientation, occupancy, loop or disconnection.
- **EG-03 Solution-family depth:** mature representative cases show >=4 abstract skeleton families.
- **EG-04 Orientation comprehension:** orientation misunderstanding <20% of ordinary failures after tutorial tuning.
- **EG-05 Anti-direct-goal strategy:** direct current-room-to-goal is not shortest in >=75% representative mature cases.
- **EG-06 No dexterity dependence:** baseline solutions require no reaction timing.
- **EG-07 Mute-clip legibility:** NEW + destroyed OLD relationship is understandable in a short mute clip.
- **EG-08 Two-seam Deck readability:** identity/preview understandable at 1280×800 and without color reliance.
- **EG-09 Useful-disconnection affect:** intentional cut/isolation feels understandable and satisfying, not arbitrary punishment.
- **EG-10 Mature repetition:** C15–C34 does not play as cosmetic variants of one skeleton.
- **EG-11 Controller predictability:** dense mature cases retain predictable semantic target selection.
- **EG-12 Three-seam exception:** any shipped 3-seam case passes readability + solver budget independently; otherwise cut.
- **EG-13 Value duration:** expert and broader-target first-clear distributions measured separately before final price decision.
- **EG-14 Demo proof:** demo communicates full causal hook and creates credible interest beyond portal spectacle.
- **EG-15 Solver production cost:** candidate campaign remains practical to validate/iterate without semantic shortcuts.

Failure of EG-01/02/03 after one bounded repair pass requires reopen/kill consideration, not feature accretion.

---

# 17. Canonical authority order after migration

The dedicated implementation repository must preserve this authority order:
1. `IMPLEMENTATION_START_HERE.md` — implementation workflow/handoff only;
2. `IMPLEMENTATION_STATUS.md` — live implementation state/NEXT ACTION only;
3. `GAME6_FINAL_FREEZE.md` — final design authority and conflict resolver;
4. `GAME6_PRODUCT_THESIS.md`;
5. `GAME6_MECHANICAL_ARCHITECTURE.md`;
6. `GAME6_CONTENT_ARCHITECTURE.md`;
7. `GAME6_UX_PRESENTATION_ARCHITECTURE.md`;
8. `GAME6_ECONOMY_COMMERCIAL.md`;
9. `GAME6_TECHNICAL_SPEC.md`;
10. `GAME6_WHOLE_GAME_SIMULATION.md`;
11. `GAME6_ADVERSARIAL_REVIEW.md`;
12. research/tournament files as rationale/history only.

Conflict rule: the final freeze wins over earlier files where it explicitly narrows or clarifies them. Product identity cannot be silently reopened by implementation convenience.

---

# 18. Frozen acceptance summary

Implementation must preserve at minimum:
- atomic OLD→NEW seam replacement;
- deterministic canonical command/event ordering;
- exact Undo/Redo transaction hashes;
- idempotent duplicate/stale-command handling;
- finite visible orientation mapping;
- persistent multi-seam pair identity;
- semantic focus parity across controller/keyboard/pointer;
- no timing-dependent baseline puzzle solutions;
- safe canonical-boundary persistence/recovery;
- no active-branch Cloud synthesis;
- versioned idempotent demo import;
- causal-family campaign diversity;
- no mandatory 3-seam content;
- solver/validator using the same domain semantics;
- no bespoke per-case gameplay callbacks;
- accessibility without invalidating completion;
- demo proving useful destroyed adjacency, not just impossible-space spectacle;
- retained EG-01..EG-15 empirical gates.

Phase-4 acceptance tests, Phase-5 tests, Phase-6 tests, Phase-7 tests, Phase-8 tests, Phase-9 checks and Phase-10 A10-01..A10-52 remain part of the implementation acceptance corpus unless this final freeze explicitly supersedes an older expectation.

---

# 19. Freeze decision

Important gameplay unknowns requiring invention: **NONE**
Implementation-flexible presentation details: **YES, bounded by frozen UX/authority**
Empirical prototype/playtest unknowns retained explicitly: **YES — EG-01..EG-15**
Scope ceiling explicit: **YES**
Core transition ordering explicit: **YES**
Content diversity/cut rules explicit: **YES**
Persistence/Cloud/import contracts explicit: **YES**
Input/accessibility/Deck contracts explicit: **YES**
Commercial uncertainty honestly bounded: **YES**
Production implementation started in factory: **NO**

**DESIGN COMPLETE = YES**

## NEXT ACTION

Migrate the complete canonical Stitchspace package to a dedicated repository (preferred name `Mikayilzade/stitchspace`), add `IMPLEMENTATION_START_HERE.md`, `IMPLEMENTATION_STATUS.md`, and CI/email-noise policy, verify source/destination integrity, then update `GAME_INDEX.md`, remove Game #006 active files from the factory, and reset `STATUS.md` to Game #007.

Do not delete the factory safety copy until migration integrity is verified.
