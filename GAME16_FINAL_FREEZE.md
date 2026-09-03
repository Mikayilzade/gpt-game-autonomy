# GAME #016 — FINAL SPECIFICATION FREEZE

Date: 2026-09-03
Status: **DESIGN COMPLETE = YES**
Working title: **ONE-WAY WORKSHOP**

## 0. Authority and purpose
This file is the highest Game #016 design authority. It consolidates binding gameplay/product rules from Phases 3–10 and supersedes older wording wherever an explicit conflict exists. Tournament/research files remain history only.

Authority precedence for Game #016 until migration:
1. `GAME16_FINAL_FREEZE.md`
2. `GAME16_ADVERSARIAL_REVIEW.md`
3. `GAME16_SIMULATION.md`
4. `GAME16_TECH_SPEC.md`
5. `GAME16_COMMERCIAL.md`
6. `GAME16_UX.md`
7. `GAME16_CONTENT.md`
8. `GAME16_MECHANICS.md`
9. `GAME16_PRODUCT_THESIS.md`
10. Round/research files as non-canonical decision history.

A future implementation session may tune presentation/performance inside the flexible boundaries below, but may not invent or reinterpret important gameplay.

---

# 1. Frozen product identity

**Hook:** Every irreversible cut creates both a product piece and a byproduct that may be the only tool/jig capable of making a later operation possible.

**Genre:** single-player deterministic tabletop fabrication puzzle; finite authored work orders; proof-oriented physical logic, not woodworking simulation.

**Core fantasy:** plan a fabrication ancestry in which apparent waste becomes future capability.

**Target:** PC/Steam-first puzzle players; controller and Steam Deck are first-class. No woodworking, engineering, arithmetic or dexterity knowledge is required.

**Core loop:** inspect plan → inspect stock/cut sockets → preview exact two-child result → plan future capability → commit irreversible fabrication → dock/use resulting child as part/jig → perform guided operation → assemble → deliberately certify → restart when lineage is broken or strategy is abandoned.

**Differentiator:** material subtraction creates future capabilities through ancestry. The player repeatedly values the “wrong” side of a cut.

---

# 2. Frozen scope ceiling

Baseline product:
- exactly 24 canonical authored cases, OW01–OW24;
- six reasoning families × four cases;
- one demo capstone D1 derived from OW13 mechanics, not case #25;
- <=3 initial stock roots in a canonical case;
- <=6 irreversible fabrication commits per canonical case;
- <=8 simultaneously loose children;
- <=5 visible cut sockets on one current piece;
- finite authored discrete geometry/tokens only;
- exactly two deterministic children per committed cut;
- no continuous/freehand cut or drill coordinates;
- one bounded tabletop/workbench presentation, no traversable workshop;
- no real-physics correctness dependency;
- target <=45 reusable child silhouettes and <=8 logical station archetypes;
- authored jobs are baseline; procedural campaign generation is out of scope.

If a case cannot be interesting or exhaustively validated inside these ceilings, rewrite/simplify the case. Do not expand the system merely to save one level.

---

# 3. Player verbs and one-way boundary

Puzzle-relevant verbs are fixed:
- inspect plan;
- inspect workpiece/child;
- focus/select one visible authored cut socket;
- preview split;
- commit cut;
- pick/place/dock a child;
- dock/undock reversible jig or part placements;
- perform a guided operation;
- assemble;
- inspect requirement/trace;
- certify;
- restart.

Camera, zoom, overlays, hints and menu actions are support interactions, not puzzle verbs.

A destructive cut and any guided operation that permanently adds a witness or consumes a jig are irreversible inside the attempt. Reversible inspection/docking can be cancelled freely. There is **no gameplay undo across a fabrication commit**. Recovery is near-instant `Restart Job`.

Every irreversible action has an explicit preview and explicit destructive-commit affordance. The UI must distinguish reversible placement from permanent fabrication.

---

# 4. Exact workpiece / cut / lineage model

Each physical workpiece has stable semantic identity, root stock, lineage path, finite geometry token, capabilities, immutable derived witnesses and exactly one availability/role state.

Availability states:
- `LOOSE`;
- `PART_DOCKED`;
- `JIG_OCCUPIED`;
- `CONSUMED`;
- `PARENT_SPENT`.

A committed cut:
1. validates the loose parent and authored socket/prerequisites;
2. atomically records the semantic cut event;
3. makes parent permanently `PARENT_SPENT`;
4. creates exactly two deterministic children with stable lineage-derived IDs;
5. derives physical capabilities from child geometry;
6. resolves any jig prerequisite as authored;
7. recomputes legal state/dead-state evidence;
8. persists only a complete post-transaction state.

No half-cut state exists. Animation and physics never define puzzle truth.

Lineage is always recorded for diagnosis but is not a hidden eligibility key. Secret rules such as “must come from Stock 2” are forbidden. The only ancestry-specific gameplay primitive is visible physical `PAIR` semantics.

---

# 5. Frozen capability and witness grammar

Base physical capability families are fixed:

1. `SPAN(axis, band)` — discrete usable extent band; covers spacer/length roles.
2. `EDGE(kind, band)` where `kind = STRAIGHT | DIAGONAL_A | DIAGONAL_B`.
3. `FACE(kind)` where baseline `kind = FLAT | NOTCHED`.
4. visible `PAIR(token)` — only complementary sibling interface from an authored paired cut.

Derived immutable witness families:
- `HOLE(pattern)`;
- `MARK(reference)`;
- `SPACING(band)`;
- `ANGLE(kind)`.

A station/part requirement can compose visible predicates with AND. No hidden material quality, mass, arbitrary identity, move count or secret property is allowed.

**FACE clarification:** FACE is permitted only when the required seat/contact is physically obvious from silhouette/fixture geometry without relying on text. A FACE predicate that blind players cannot understand from form/contact must be rewritten or removed.

Cuts may derive physical capabilities only from geometry. Guided operations may add witnesses; they do not create material or enlarge a piece.

A derived witness may qualify a piece for at most one further capability-role family per job. Same-piece witness upgrade depth is capped at one. Late depth comes from dependencies across pieces, not leveling one universal tool.

---

# 6. Guided operations

Canonical guided operation families are fixed:
- `GUIDED_DRILL` → adds `HOLE` witness;
- `GUIDED_MARK` → adds `MARK` witness;
- `GUIDED_SPACING` → adds `SPACING` witness or authorizes a frozen operation;
- `GUIDED_DIAGONAL` → adds `ANGLE` witness or authorizes one authored deterministic diagonal operation;
- `ASSEMBLE` → docks/locks a valid part according to the job.

An operation has at most one required jig station at baseline. Each jig use explicitly resolves as `RELEASE` or `CONSUME`. Temporary/released vs consumed use must be visible before the commit.

No arbitrary machining, sanding, gluing system, structural simulation, continuous measurement or emergent tool crafting is part of 1.0.

---

# 7. Certification, failure, dead state and trace

Certification is deliberate and state-based. A case succeeds iff all authored final predicates are true. The runtime never compares against a canonical move string.

Baseline final leaves:
- `PART_PRESENT(slot)`;
- `WITNESS_PRESENT(slot,type,param)`;
- visible paired-sibling relation where explicitly authored;
- `JIG_RELEASED(station)`;
- `OPERATION_DONE(op)`.

Final requirement composition is AND-only. Alternate solution families emerge from multiple valid upstream allocations/ancestries.

Soft certification failure names the first/local unmet requirement and highlights the relevant physical object/station. It does not reveal the winning move sequence.

Runtime dead-state detector is conservative optimistic reachability:
- it may miss deaths caused by competition for one scarce child;
- it may declare `Lineage broken` only when death is proven;
- **zero false-positive dead-state declarations are allowed**.

**Non-assertive silence:** absence of `Lineage broken` means only that the conservative detector has not proved death. It must never be presented as “state is solvable/live.”

Trace View may show past/current semantic ancestry, spent/consumed branches, witness events and currently compatible pieces. Before clear it must not enumerate future producers, rank cuts or reveal an unreachable future branch. After clear it may replay the player’s actual winning causal chain.

---

# 8. Six canonical reasoning families / exact campaign content

Campaign remains exactly:

### I — Immediate Byproduct, OW01–OW04
Proof: the apparent waste from the current cut is the next required jig.

### II — Property Choice, OW05–OW08
Proof: preserve the correct physical property rather than the largest child. Introduces EDGE, obvious FACE, diagonal A/B and visible PAIR.

### III — Delayed Lineage, OW09–OW12
Proof: preserve/use/release a child for a requirement several commits later; includes product-first defeat and tool→part role transition.

### IV — Cross-Blank Ancestry, OW13–OW16
Proof: the correct cut on one root is determined by another root’s future need. OW16 has at least two recognized valid families.

### V — Dual-Use Conflict, OW17–OW20
Proof: one scarce compatible child cannot satisfy all competing roles simultaneously; sequencing/allocation/release/consumption matter. OW20 has at least two recognized valid families.

### VI — Derived Witness Relay, OW21–OW24
Proof: create a child, upgrade it once with an existing guided witness, then use it as a future tool elsewhere. OW24 composes three roots, six commits, cross-piece witness dependencies and dual-use pressure without introducing a new primitive.

Content introduction order from `GAME16_CONTENT.md` is binding unless a case is rewritten inside existing mechanics.

**Proof-distinctness/filler gate:** blind players should describe each family with a materially different causal sentence. OW02 vs OW01 and OW18 vs OW17 are specifically high-risk duplication pairs. If a case is repeatedly solved/explained as merely the same proof with no added planning burden, rewrite that case **inside the frozen grammar**. Keeping the number 24 never justifies filler; adding a seventh mechanic/family is not the repair.

**Preview gate:** inspecting all currently legal cut previews is allowed. A canonical case fails authoring validation if it becomes trivial solely by enumerating <=5 immediate previews; reasoning must depend on future requirement relationships.

---

# 9. Progression, demo and hints

## Campaign unlocks
Fresh profile: OW01 only.

Early:
- OW01 → OW02 + OW03;
- OW02 OR OW03 → OW04;
- OW04 → OW05.

Later exact chain:
`OW05 -> {OW06,OW07} -> OW08 -> OW09 -> {OW10,OW11} -> OW12 -> OW13 -> {OW14,OW15} -> OW16 -> OW17 -> {OW18,OW19} -> OW20 -> OW21 -> {OW22,OW23} -> OW24`.

Unlocks are derived from prerequisite reachability, not stored as authoritative bits.

## Demo
Demo path is exactly OW01 → OW03 → OW05 → D1. D1 is a reduced OW13-derived cross-blank configuration and never becomes OW13 clear.

Demo import is optional, non-destructive and idempotent. Supported clear flags/settings/tutorial flags merge; no in-progress demo attempt imports. Retail prerequisites are recomputed, so imported later clears never bypass teaching gates.

## Hints
Hints are authored H1/H2/H3 reasoning support, with no currency, score penalty or achievement penalty.
- H1: future goal focus;
- H2: conflict/relationship class;
- H3: proof boundary/necessary condition.

No hint may name the correct current cut socket or provide a sequence.

**Binding H3 per-state leakage rule:** for every state in which H3 may appear, combine the hint with already-visible facts. If a genuine multi-action irreversible choice is reduced to exactly one current commit, rewrite H3 toward a contradiction class, comparison task or future invariant. If only one legal irreversible commit existed before the hint, explaining its relevance is allowed, but subsequent sequence remains hidden.

Blind-test gate remains: if >25% of target testers call H3 effectively “the answer,” rewrite the hint/case presentation.

---

# 10. UX / controls / accessibility freeze

All puzzle truth is operable by mouse and by semantic controller navigation. A fake analog cursor is never the only controller path.

Workbench zones remain Plan Rail, Stock Bay, Operation Bay and Assembly Pad in one bounded scene.

Controller focus graph uses logical relationships and stable semantic ordering. **It must not use solver desirability, strategic-safety ranking or “most useful” heuristics.** Root/zone/relation/stable-ID ordering is acceptable.

Compatibility feedback means only current physical fit:
- preferred copy: `Fits this fixture` / `Compatible now`;
- neutral iconography;
- no green “recommended/safe” implication;
- never imply the future remains solvable.

Physical form is primary meaning. Capability/witness information uses redundant form + symbol + optional text; color is reinforcement only.

Dynamic device glyphs, remappable semantic actions, 1280×800 Deck readability, text scaling, reduced motion, persistent guidance, high-information overlay and alternate safe commit-confirmation interactions are requirements.

High-information overlay may show inspectable present facts only; it cannot expose reachability or strategic safety.

Cut sockets must be embodied visible marks on the actual workpiece. Cold-test acceptance requires players to describe where they cut the object rather than merely “choosing option B.”

Post-commit restart target: return to interactive authored initial state in <1.5 s on target hardware in normal conditions; no campaign/menu reload.

---

# 11. Commercial / retention freeze

Product is a complete finite premium puzzle game. No ads, premium currency, lives, paid retries, consumable hints, FOMO/dailies, loot boxes, crafting grind, gameplay MTX or live-service requirement.

Working MSRP: **$12.99**, empirically adjustable pre-release within **$9.99–14.99** without reopening mechanics. Content must never be padded to defend price.

Commercial gate: target median first-clear campaign 5–7 hours; minimum working value gate 4.5 hours. If shorter but high quality, lower price or rewrite weak cases inside frozen mechanics. If longer because of confusion/restart friction, fix UX/hints.

Baseline demo target: 20–30 minutes and must end with the cross-blank causal aha.

Campaign has no stars, par moves, medals, score chase, material-efficiency grade, no-hint grade, dailies, endless mode or leaderboard requirement.

Baseline achievements: exactly 12 as defined in `GAME16_COMMERCIAL.md`, including milestone clears, Tool Becomes Part, Crossed Favors, Prepared Tool, Another Way and Trace the Work. Accessibility/hints never block them.

Final launch-language list is budget-flexible; localization-ready externalized architecture is mandatory.

---

# 12. Persistence / cloud / deliberate reset freeze

Puzzle-domain state transitions are deterministic, atomic and persisted only as complete states.

Persist stable versioned IDs/schema for campaign profile and local active attempt. Save/load may never depend on scene node instance IDs, animation timing or physics.

## `reset_generation`
Profile contains persisted monotonic integer `reset_generation >= 0`.
- fresh profile = 0;
- explicit Reset Campaign Progress increments generation;
- new generation starts with empty campaign-clear/hint/tutorial-progress sets as designed, while profile identity/settings are preserved where applicable;
- cloud merge compares generation **before** any monotonic set union;
- higher generation represents later deliberate reset lineage and lower-generation clears must not silently resurrect;
- equal generation merges monotonic portable progress normally;
- corrupt/irreconcilable generations preserve backups and require recovery instead of guessing.

Reset confirmation must explain that older cloud progress will not automatically restore into the new reset generation.

## 1.0 cloud policy
**Cloud syncs campaign profile/backups and merge-safe portable settings. Active in-progress attempts are local-only.**

Cross-device behavior: cleared progress/settings travel; an unfinished work order does not. Starting that unfinished case on another device begins from authored initial state.

This supersedes any earlier Phase-8 alternative suggesting cloud synchronization of opaque active attempts.

Demo import retains idempotent receipt semantics and never imports an active attempt.

---

# 13. Technical boundaries

Frozen implementation direction: Godot 4.7 stable, GDScript-first, PC/Steam-first unless a future newer stable Godot 4.x upgrade passes deterministic-core compatibility tests and is explicitly documented.

Architecture must separate:
- deterministic domain/puzzle core;
- content data;
- application/session;
- presentation;
- platform adapters;
- offline validation/tooling.

Presentation, meshes, animation, sound and Steam APIs never own puzzle truth.

Canonical content must be data-driven, versioned and validated; case logic must not be hidden in scene scripts.

Semantic commands include CommitCut, Dock/Undock Jig, Dock/Undock Part, CommitOperation, Certify and Restart. Inspection/camera/preview are non-mutating.

Stable semantic trace must reproduce the same canonical domain state hash from the same initial job data.

---

# 14. Offline validator / exhaustive oracle contract

Every shipped canonical job OW01–OW24 and D1 must pass exhaustive finite-state validation under final data.

Required package/content checks:
- all stable references resolve and IDs are unique;
- scope ceilings hold;
- at least one certifying route exists;
- every declared/golden solution family certifies;
- all state transitions preserve identity/occupancy invariants;
- certifier is state-based and accepts valid alternate routes;
- runtime dead-state detector has **zero false positives** against the exhaustive oracle for every enumerated reachable state;
- prerequisite graph matches the frozen campaign;
- hints/requirements/localization references resolve;
- solution-family signatures are valid where used.

If exhaustive search becomes infeasible for one proposed case, **simplify the case**. Do not weaken the zero-false-positive proof gate.

Runtime detector may retain false negatives.

---

# 15. Alternate solution-family signature contract

`Another Way` is supported only on explicitly validator-authored cases such as OW16/OW20.

A family signature:
- uses coarse semantic ancestry/resource-allocation facts (for example, which root supplied which scarce role);
- never uses exact move string, timing or move count;
- is derivable from final semantic trace/state;
- is backed by at least one golden certifying trace;
- is mutually distinguishable from every other recognized signature for that case.

Reordering equivalent actions inside one semantic family does not create a new family.

---

# 16. Explicit out of scope for 1.0

No:
- multiplayer/co-op;
- VR baseline;
- mobile/touch baseline;
- freeform woodworking;
- continuous cut/drill positions;
- physics skill/structural simulation;
- shop/customer economy;
- crafting/resource grind;
- factory automation;
- open world/traversable workshop;
- procedural campaign requirement;
- level editor/Steam Workshop baseline;
- huge narrative/dialogue/cinematic campaign;
- tool durability/meta inventory/currencies;
- undo across committed fabrication;
- score/par/leaderboard optimization loop;
- new seventh late-game mechanic merely to add variety.

---

# 17. Implementation-flexible decisions

The following may be tuned without reopening game design, provided acceptance contracts above remain true:
- exact mesh/art style/material palette inside stylized tabletop identity;
- animation timing, VFX, audio and haptics;
- camera easing and bounded framing details;
- exact controller button mapping/glyph assets under semantic remapping contract;
- layout polish and information grouping;
- exact internal numeric mapping of discrete SPAN bands;
- reusable geometry dimensions that preserve authored predicates/solution families;
- wording/localization copy that preserves meaning;
- save filenames/serialization library/platform adapter implementation;
- renderer/performance optimizations that cannot alter domain truth;
- final MSRP within $9.99–14.99 based on value evidence;
- final launch-language count;
- minor case geometry/hint wording rewrites inside frozen mechanics when validators/playtests demand them.

These are not permission to change puzzle truth, campaign structure, capability families, operation families or one-way commit semantics.

---

# 18. Empirical implementation/playtest gates

These remain intentionally empirical, not design blockers:
1. socketed cuts feel like manipulating/cutting a workpiece rather than selecting a menu option;
2. six-commit / <=8-child ancestry remains readable without genealogy bookkeeping overload;
3. cold players infer jig compatibility primarily from form/contact, with icons/text as reinforcement;
4. irreversible commits feel tense but not punitive because restart is immediate;
5. demo players can explain the byproduct-as-tool causal hook in ordinary language;
6. six reasoning families remain verbally distinct in blind solve debriefs;
7. OW02/OW01 and OW18/OW17 are not redundant filler;
8. H1/H2 usually restore productive reasoning without solving; H3 passes leakage/"answer" gates;
9. consume-vs-release fixtures are unmistakable before commit;
10. OW24 high-information view remains cognitively readable at 1280×800;
11. full campaign meets value/time gate without filler;
12. trailer/store first read communicates deterministic byproduct-as-tool puzzle before generic cozy woodworking.

Failure of these gates triggers presentation/content rewrite inside frozen mechanics, price adjustment, or—if the central tactile hook itself fails—explicit product reconsideration in the dedicated implementation track. It does not authorize silent mechanic invention.

---

# 19. Fresh implementation acceptance checklist

A new implementation team/session can call the major design systems correct only when:
- OW01 can be completed entirely by mouse and entirely by controller with no precision cursor requirement;
- every cut is an authored visible socket producing two deterministic children;
- every domain-changing fabrication command is atomic and replayable from semantic trace;
- no animation/physics state can alter puzzle truth;
- capabilities/witnesses obey the frozen grammar and no hidden predicate exists;
- consume/release/reversible roles are correctly enforced and visible;
- certification accepts any valid state and rejects unmet predicates without move-string comparison;
- `Lineage broken` never fires on an oracle-live state;
- dead-state silence is never labeled solvable;
- Trace View leaks no future solution pre-clear;
- campaign unlock evaluator exactly matches the frozen graph;
- demo import is idempotent and cannot bypass prerequisites;
- active attempts remain local-only while portable profile/settings obey generation-safe cloud merge;
- deliberate reset cannot be undone silently by stale cloud data;
- all 24 canonical jobs + D1 pass exhaustive validation under final data;
- OW16/OW20 alternate-family achievements use validated semantic signatures;
- hints satisfy per-state H3 leakage checks;
- accessibility paths do not alter puzzle truth or block achievements;
- all frozen scope/out-of-scope boundaries are respected.

---

# 20. Contradiction audit / superseded interpretations

Phase-11 audit found no remaining design-blocking contradiction. These interpretations explicitly supersede older ambiguity:

1. Any Phase-8 wording that allowed cloud-syncing an opaque active attempt is superseded: **active attempt is local-only in 1.0**.
2. Any profile schema omitting deliberate-reset lineage is incomplete: **persist `reset_generation` and compare it before merge**.
3. Any UX implication that absence of dead-state warning means “live” is superseded: silence is non-assertive.
4. Any compatibility UI that implies strategic recommendation is superseded: compatibility = current physical fit only.
5. Any controller target ordering based on usefulness/solver ranking is forbidden; ordering must be stable semantic/non-solver.
6. Any H3 rule based only on “do not name the socket” is insufficient; the per-state leakage test is binding.
7. FACE is not an arbitrary keyed-property bucket; its physical contact meaning must be visually obvious.
8. Offline exhaustive validation is required for every shipped canonical case/D1; a large case is simplified rather than exempted.
9. Alternate-family recognition is semantic and validator-backed, never exact move-sequence recognition.
10. Maintaining exactly 24 cases never overrides proof-distinctness/value; weak cases are rewritten within existing mechanics rather than padded or expanded mechanically.

No new gameplay system is left for implementation to invent.

---

# 21. Freeze decision

**DESIGN COMPLETE = YES.**

ONE-WAY WORKSHOP has completed opportunity discovery, concept tournament, product thesis, mechanical architecture, content architecture, UX/presentation, commercial model, technical specification, whole-game simulation, adversarial review and specification freeze.

The design is ready to migrate to `Mikayilzade/one-way-workshop` when that dedicated repository exists. Production implementation must occur there, not inside the factory.