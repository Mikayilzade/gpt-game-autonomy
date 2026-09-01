# GAME #012 — FINAL SPECIFICATION FREEZE

Date: 2026-09-01
Product: **OPENWORK** *(provisional working title; implementation repository target `Mikayilzade/openwork`)*
Status: **PHASE 11 COMPLETE — DESIGN COMPLETE = YES**

This file is the stand-alone implementation-facing authority for Game #012. It consolidates and supersedes conflicting wording in earlier Game #012 research/tournament/product/mechanics/content/UX/commercial/technical/simulation/adversarial files. Earlier files remain evidence/history; when they conflict with this file, **this file controls**.

No production implementation belongs in the factory repository.

---

## 1. Product contract

OPENWORK is a premium single-player topological deduction puzzle for PC/Steam, controller-first and Steam-Deck-conscious.

**Hook:** Place a few solid pieces on a tiny orthogonal board; every objective judges only the topology of the empty space left behind.

**Fantasy:** sculpt absence / reason about the void.

**Core loop:** inspect initial open space and visible predicates -> place/reposition 1–4 solids -> evaluate current remaining-open topology -> inspect consequences -> undo/refine -> solve when every required piece is placed and every predicate is true.

The game is finite and authored. Target campaign = 36 cases; quality floor = 30. Difficulty comes from coupling constraints and deceptive topology, not board inflation or a growing mechanic catalogue.

Lead interaction targets: controller, keyboard, mouse. No pixel-precision drag is required. Offline play remains complete without Steam.

---

## 2. Exact board and topology rules

A case is a finite rectangular grid, coordinates `(x,y)` with origin upper-left. Every in-rectangle cell is immutable base `OPEN` or `FIXED_SOLID`. Outside the rectangle is `EXTERIOR`, used only for boundary/enclosure classification.

After player placements, an OPEN base cell is `REMAINING_OPEN` or `PLACED_SOLID`. Only REMAINING_OPEN cells participate in topology predicates. Connectivity is cardinal/4-neighbour only; diagonals never connect and never seal a diagonal leak.

Markers are immutable metadata on OPEN cells. Marker cells are protected from placement and therefore always remain in exactly one remaining-open component.

A remaining-open component is a maximal cardinally connected set of REMAINING_OPEN cells. Component area is cell count. Boundary set is the subset of `{N,E,S,W}` touched by its cells.

**Hole definition:** an enclosed hole is exactly a remaining-open component with **zero board-boundary contact**. Equivalently, flood EXTERIOR into edge-connected remaining-open cells; any remaining-open component not reached is a hole. Therefore holes are included in component count. Hole area = component area. This definition is absolute launch canon.

Deterministic component IDs exist only for stable implementation/presentation: sort each component by its minimum `(y,x)` cell and number from zero. Objectives never refer to component IDs.

Evaluation order for every committed legal state:
1. construct REMAINING_OPEN set;
2. derive 4-connected components;
3. deterministically ID components;
4. derive area, markers and boundary mask per component;
5. classify holes as zero-boundary components;
6. derive hole areas/IDs;
7. evaluate every predicate independently;
8. state is solved iff every required piece is placed and every target predicate is true.

Placement order has **no game semantics**.

---

## 3. Piece vocabulary and legality

Each case contains exactly 1–4 required piece instances. Frozen shapes:
- `1x1` monomino;
- straight `1x2` domino;
- straight `1x3` triomino.

Bar orientation policy per authored instance is `FIXED_H`, `FIXED_V`, or `ROTATABLE` (H/V only).

A placement `(instance_id, anchor, orientation)` is legal iff every footprint cell:
- lies inside the board;
- is base OPEN;
- is not a marker cell;
- does not overlap another placed piece;
- uses an allowed orientation.

Pieces may touch solids/pieces cardinally or diagonally. No gravity, support, adjacency bonus, physics or order effect exists.

Hard launch ceilings:
- board <=9x9;
- pieces 1–4;
- only the three frozen straight shapes;
- markers <=6;
- predicates <=6 (4–5 preferred late-game);
- no case-specific simulation rules.

A content idea that requires exceeding these limits is cut or re-authored; it does not silently expand the core.

---

## 4. Frozen predicate grammar

A case target is an unordered set of 1–6 atomic predicates combined by logical AND only. Allowed families:

- `COMPONENT_COUNT == n`
- `HOLE_COUNT == n`
- `COMPONENT_AREAS == sorted_multiset`
- `ALL_COMPONENT_AREAS_IN [lo,hi]`
- `HOLE_AREAS == sorted_multiset`
- `ALL_HOLE_AREAS_IN [lo,hi]`
- `SAME(markerA,markerB)`
- `DIFFERENT(markerA,markerB)`
- `MARKER_COMPONENT_TOUCHES(marker,boundary_set,EXACT|INCLUDES|AVOIDS)`
- `COMPONENT_BOUNDARY_SIGNATURES == sorted_multiset_of_boundary_masks`

Boundary bitmask canonicalization: N=1, E=2, S=4, W=8.

No path length, perimeter, shape-match, diagonal connectivity, symmetry objective, nested boolean language, hidden predicate, arithmetic expression, named-component identity, keys, switches, portals or moving actors are launch canon.

When component-count and hole-count objectives coexist, UI copy must explicitly communicate in ordinary language that enclosed pockets are themselves open spaces and therefore count in the total.

---

## 5. Solution identity and certification

A solution is a complete placement assignment satisfying all predicates.

Interchangeable piece instances are those with identical shape + orientation policy and no instance-specific rule. Their ID permutations do not create distinct solutions.

Canonical solution representation:
1. each placed instance -> `(shape,resolved_orientation,sorted_footprint_cells)`;
2. sort tuples lexicographically;
3. serialize sorted tuple list.

The offline certifier is exhaustive and must use the **same evaluator contract** as runtime. It validates schema/ceilings, enumerates every legal non-overlapping complete assignment with interchangeable-instance quotienting, evaluates every assignment, and emits deterministic certificate/report data.

Campaign default is exactly **one canonical solution**. `allow_multiple=true` is exceptional and requires an explicit human review record; absent such approval, >1 solution rejects the case.

Certificate minimum: case/rules/schema/content identity and canonical content hash, dimensions, solids/markers/pieces/predicates, raw and canonical assignment counts, canonical solution count, at least one witness, witness derived topology, certifier version/hash.

Any gameplay case/rules change invalidating semantics requires re-certification.

---

## 6. Campaign structure and progression

Shipping manifest: **30–36 active cases**, always **six acts**, each with **5 or 6 active cases**. A reduced manifest is re-curated; cases are not simply deleted without progression/content validation.

Reasoning arc:
- Act I — See the Void
- Act II — Inside / Outside
- Act III — Who Shares the Space?
- Act IV — False Openings
- Act V — Coupled Cuts
- Act VI — Openwork

### Mandatory foundation
Act I C1–C4 are mandatory sequential foundation cases and teach, in order:
1. remaining open space is scored;
2. marker same/different grouping;
3. enclosed pockets/holes;
4. boundary contact.

C5/C6 may be optional campaign cases; they remain preferred inversion/coupling material and protected demo material.

### Unlock rules for every valid 30–36 manifest
- Act II unlocks after Act-I C1–C4 are solved.
- For Acts II–V, the next act unlocks after **4 solved cases in the current act**, regardless of whether that act has 5 or 6 active cases.
- Act VI additionally requires **>=24 total active campaign cases solved**.
- Finale requires **4 other active Act-VI cases solved**.
- Campaign completion = finale solved.
- Current 100% = every current active shipping case solved.

Unlock state is derived, never stored as independent authority.

Manifest lint fails if a later case depends on a predicate meaning whose only prior introduction is skippable and not self-describing through already-established card grammar.

---

## 7. Content families and anti-repetition gates

Canonical content-family vocabulary remains F1–F8:
- F1 articulation cut;
- F2 seal/enclosure without severing exterior;
- F3 marker partition / false necks;
- F4 boundary signature sculpting;
- F5 area-balanced split;
- F6 coupled hole + partition / multi-zone coupling;
- F7 preserve-route / false-neck inversion;
- F8 same counts/topology class, wrong allocation.

A 36-case target distribution may use the prior 4/5/5/4/4/6/4/4 principal-family plan, but quotas never override experiential curation.

Every accepted case stores authoring-only `reasoning_skeleton` of 1–4 ordered abstract steps from:
`CUTSET/ARTICULATION`, `ENCLOSURE/RING`, `MARKER PARTITION`, `BOUNDARY ALLOCATION`, `AREA ALLOCATION`, `PIECE ROLE/ORIENTATION`, `INVERSION/PRESERVE ROUTE`.

Hard gates:
- <=25% of shipping cases may be `ARTICULATION_DOMINANT`;
- Acts III–VI: >=60% of cases must have first decisive step other than initial articulation spotting;
- no 3 consecutive campaign cases share the same first 2 reasoning-skeleton steps;
- every act after Act I has >=1 case where the strongest obvious initial neck is legal but non-solving;
- at least 4 of F2–F8 must each yield >=4 accepted cases before a 30-case release is valid;
- neighboring cases may not be near-duplicates in principal family + piece multiset + predicate-class set + reasoning skeleton.

If a quality 30-case manifest cannot satisfy these gates without new mechanics, the correct result is redesign/kill, not padding.

---

## 8. Anti-brute and predicate-necessity gates

Assignment-count guidance:
- INTRO/EARLY may be small for teaching;
- MID normally >=40 canonical complete assignments, >=100 preferred with multiple pieces;
- LATE normally >=100;
- MASTERY normally >=500;
- finale >=1000 preferred.

Counts are necessary evidence, never sufficient evidence. Representative Acts III–VI cases require a human solve trace showing how intended invariants eliminate **classes** of placements before complete-state testing. Reject/rework any case where competent systematic complete-state enumeration is easier/faster than using the intended 2–4 invariant chain.

For every LATE/MASTERY case, offline analysis performs leave-one-out predicate ablation. Removing any atomic predicate must admit at least one additional canonical solution candidate; otherwise that atom is logically redundant and must be removed/redesigned. Six-predicate cases require every atom individually necessary and >=3 materially necessary predicate classes.

Class-level ablation is also required: removing a displayed predicate class must expand candidates or materially change the intended proof.

No artificial retry delay, limited undo, fail modal or hidden feedback may be used to patch brute-force risk.

---

## 9. UX and presentation authority

The remaining open space is visually primary. FIXED_SOLID and PLACED_SOLID are mechanically impermeable but visually distinct by texture/edge treatment, not color alone. Markers use labels/symbols and cannot rely on color.

Component rendering may use outline pattern + optional tint. Hole rendering uses the **same component outline** plus enclosure halo/double outline; never render a hole as filled solid.

Boundary contacts use N/E/S/W edge language. Predicate cards use icon + value + focusable natural-language explanation.

### Controller baseline
- D-pad/left stick: cell cursor;
- LB/RB: cycle unplaced pieces;
- LT/RT: rotate selected rotatable piece;
- A: place / commit legal reposition;
- B: undo normally; **while held-reposition is active B cancels held state only**;
- X: pick up focused placed piece for reposition;
- Y: toggle current-state topology inspect;
- View/Select: objective details;
- Start: pause;
- hold B outside held mode: reset confirmation.

Keyboard has complete parity. Mouse supports hover focus, click-place/select, right-click undo and rotate control; drag is optional convenience, never required. No information is hover-only.

### Held reposition exact matrix
While `REPOSITION_HELD`:
- cursor/rotation modify provisional ghost only;
- A attempts one legal atomic reposition commit;
- B cancels and restores old committed placement; it does **not** additionally undo;
- LB/RB cycling disabled;
- reset-hold accumulation disabled;
- pause allowed and preserves temporary held UI state in memory;
- quit/reload restores last committed placement, never provisional ghost;
- inspect/objective details show **committed topology only**, with ghost visibly provisional.

Outside held mode, legal commands commit/evaluate immediately. Stale animations cancel/retarget. Undo acts on latest committed transaction, never animation state. On solve, progress commits atomically before success navigation; destructive board commands during the short success lock are ignored and never replayed later.

### Current-state feedback vs oracle
Allowed: topology of current committed state, component/hole counts/outlines/areas, marker grouping, boundary contacts, current predicate truth.

Forbidden: hypothetical topology for ghost placement, correct-cell highlights, articulation highlights, candidate ranking, remaining-solution counts, satisfying assignments, “closer” scoring, partial-state extendability or any solution-derived hint.

### Layout/accessibility
1280x800 must support a full 9x9 board without pan. Preferred cell size >=48 logical px; absolute floor **40 logical px**. UI chrome must compact before cells shrink below 40. Up to six compact objective cards must be identifiable without ordinary scrolling; focused details may expand without covering the selected board cell.

Support remapping, text scaling, high contrast, reduced motion and redundant non-color cues. No achievement may require speed, no-undo, no-hint, default controls or default visual settings.

---

## 10. Assistance and runtime oracle firewall

OPENWORK has no solution-directed hint ladder. Unlimited undo/reposition/reset, predicate explanations, glossary/tutorial replay and current-state inspect are baseline.

Optional reasoning primers may state only reusable general concepts already taught. Primer eligibility may use non-solution engagement metadata or explicit request. Primer selection is authored/general-family metadata only and may **not** query solution sets, candidate ranking or extendability.

Ordinary shipping runtime may consume only:
- case data;
- current committed placements;
- deterministic current evaluation snapshot;
- explicitly whitelisted non-solution metadata for UI/progression.

Ordinary shipping runtime must not consume/package into normal content paths:
- canonical witness solutions;
- satisfying-assignment sets;
- assignment counts used for authoring;
- ablation survivor tables;
- candidate rankings;
- authoring articulation/critical-zone analysis;
- partial-state extendability;
- pre-solve reasoning skeleton.

Certificate integrity metadata may ship only when it cannot expose solver data. Test/dev builds may contain authoring diagnostics behind non-shipping boundaries.

---

## 11. Persistence, Cloud and demo import

Persistence stores authoritative monotonic facts, not cached progression truth.

Logical save separation:
- progress/profile: historical solved IDs, tutorial/glossary seen, last navigation convenience, achievement reconstruction metadata;
- settings: accessibility/audio/input/UI;
- resume: optional committed placements for one in-progress case.

Resume is lower authority and is discarded on incompatible case revision; solved history is not.

### Atomic local write
Serialize new payload to temp -> flush/close -> verify parse/integrity -> rotate existing primary to bounded backup -> atomic rename temp to primary where supported -> retain at least one known-good backup. Never edit primary in place.

### Authoritative recovery order
1. valid supported primary -> use;
2. invalid primary + valid supported backup -> restore backup atomically;
3. both invalid -> preserve/quarantine both and enter `UNCOMMITTED_RECOVERY`; **do not write/upload blank progress**;
4. initialize platform defensively and attempt compatible Cloud recovery;
5. valid compatible Cloud -> atomically restore locally, then ordinary semantic sync;
6. unavailable/invalid Cloud -> explicit player action may create a new profile; only that deliberate commit authorizes later Cloud upload;
7. any future-version profile locally or in Cloud is preserved and blocks destructive older-version merge/upload for that profile.

### Cloud semantics
Cloud is transport, not puzzle authority. Valid compatible progress merges by set union of compatible solved facts and tutorial/glossary facts. Progression/completion/achievements are recomputed. Resume is chosen/discarded as convenience; it is never unioned. Device-local settings win by default unless a separately tested explicit settings policy exists. Wall clocks may choose convenience metadata only, never which solved facts survive.

Semantic merge -> atomic local commit -> Cloud upload. Platform failure never rolls back a local solve.

### Demo -> full import
Demo and full have separate product identities. Import is explicit, crash-safe and idempotent. Compatible demo solved IDs union into existing full solved facts; they never replace a larger full set. Current full settings remain unless the player explicitly imports whitelisted compatible demo settings. Achievements/unlocks are reconstructed after merge, never copied blindly.

Repeated import after crash is safe because set union is idempotent; provenance records close the transaction but are not required to prevent duplicate/erasing effects.

Future/incompatible demo schemas are refused/deferred without damaging full progress.

---

## 12. Content lifecycle and monotonic achievements

Solved facts are append-only historical profile facts unless the player explicitly resets the save.

- Same stable case ID revised after release: prior solve remains grandfathered for progression/completion/achievements; resume is invalidated; UI may say `Solved (updated)` until replay.
- Removed case: historical solve remains but case is excluded from current active denominator and current progression gates.
- Materially new replacement: new case ID, initially unsolved; old removed ID remains historical.
- Current 100% denominator = current active shipping campaign IDs.
- Once a platform achievement is unlocked, never revoke it.
- Any not-yet-unlocked achievement must remain attainable from the current active manifest; if its sole trigger case is removed, remap the achievement before shipping that update.

---

## 13. Commercial and platform commitments vs variables

### Frozen design commitments
- finite premium game;
- no ads, premium currencies, consumable hints, battle pass, FOMO/streak economy or live-service dependency;
- six-case demo intended to include inversion/coupling aha, not six trivial tutorials;
- 12 accessibility-neutral achievement targets;
- Steam Cloud/full-controller/offline-capable architecture;
- no editor/Workshop/procedural-infinite promise required for launch;
- no score/par/no-undo progression economy.

### Business variables — may change without reopening game design
- provisional list price **$8.99**, acceptable current band $7.99–$9.99;
- launch discount timing/percentage;
- exact final shipping case count within 30–36 after quality gates;
- exact localization list/count;
- release date/store wording;
- final Steam binding/plugin version;
- whether Deck reaches Valve `Verified` status.

Do not advertise exact case count, exact playtime, Deck Verified or language count before verified release facts exist.

Price-value empirical gate: if final accepted campaign is only 30 cases and median blind first-play completion is <3 hours, reassess toward $7.99 rather than pad content.

---

## 14. Technical authority and implementation-flexible choices

Use Godot 4.x supported stable branch at implementation bootstrap, newest compatible stable patch after green deterministic/save fixtures. The domain rules core remains scene-independent, integer/boolean/set-based and independent of wall clock, RNG, locale, frame timing, Steam account and floating-point geometry.

Authority flow:
`IMMUTABLE CASE DATA -> RULES CORE -> DERIVED TOPOLOGY -> PREDICATE RESULTS -> SESSION STATE -> PRESENTATION`.

Runtime and certifier share evaluator semantics; runtime enumeration is forbidden.

Version concepts remain distinct: `rules_version`, `case_schema_version`, per-case `content_version`, `save_schema_version`, plus build version for diagnostics.

Implementation-flexible provided all acceptance tests pass:
- exact class/node/file names;
- whether services are autoloads/resources/plain objects;
- internal bitset vs arrays for masks;
- exact atomic-file helper/platform abstraction;
- exact layout animation easing/audio sample/art treatment within frozen readability language;
- exact UI placement of board/rail/tray at each responsive breakpoint;
- whether reset itself is undoable, provided reset is safe/quick and never conflicts with held-state matrix;
- exact Godot Steamworks binding version/adapter internals;
- telemetry may be omitted entirely; if included it is opt-in/minimal/privacy-safe and never required for gameplay;
- final localizable wording that preserves predicate meaning;
- optional cosmetic presentation polish with zero rules effect.

These are not permission to change mechanics, progression gates, persistence semantics, oracle boundary or scope ceilings.

---

## 15. Empirical release gates carried beyond design freeze

The design is complete even though these questions require implementation/playtest evidence:

**E1 — 1280x800 worst case:** 9x9 board + six cards + max supported UI/text scale + high contrast + controller glyphs. Pass with board >=40 logical px/cell, no board pan, no required card scrolling, readable focused details not hiding selected cell.

**E2 — anti-brute playtest:** representative Acts III–VI first-time competent puzzle players should solve primarily through intended invariants, not systematic complete-state enumeration. Re-author failing cases; do not add retry friction.

**E3 — handheld fatigue:** representative 9x9/4-piece/6-card case supports ~10 minutes repeated inspect/reposition/undo without focus loss, mistaken piece identity or unreadable topology. Re-author failing content before adding UI complexity.

**E4 — six-case demo comprehension:** fresh players understand that empty space is scored, can distinguish open component vs enclosed pocket, understand marker/boundary semantics, and encounter at least one inversion/coupling aha without solution-directed hints.

**E5 — price/value:** validate final campaign length and blind first-play completion before locking store price/playtime claims.

These gates may cut/re-author content or tune presentation/business variables. They do not authorize silent new mechanics.

---

## 16. Concrete implementation acceptance tests

### Rules fixtures
Golden fixtures cover: single component, multiple components, zero-boundary hole, diagonal leak non-connectivity, marker membership, each boundary bit, component/hole area multisets, each predicate mode, marker-protected placement, overlapping/outside/fixed-solid illegality, rotatable/fixed orientation and interchangeable-instance canonicalization.

### Certificate tests
For every shipping case: canonical content hash matches; certificate rules version matches; exhaustive current certifier returns required canonical solution count; runtime evaluator returns witness topology/predicate truth exactly; mutated case data invalidates certificate.

### Progression tests
Across every active 30–36 manifest: C1–C4 mandatory; Acts II–V unlock at four current-act solves; Act VI impossible before >=24 active solves; finale impossible before four other active Act-VI solves; removed historical IDs cannot satisfy current gates; 100% denominator equals active manifest.

### Persistence/Cloud/import tests
Crash/fault injection before/after every atomic-write stage; corrupt primary/backup combinations; valid Cloud recovery after both-local-corrupt; Cloud unavailable in uncommitted recovery; future-version local/Cloud refusal; disjoint solved-set union; offline solve then platform return; repeated demo import; demo smaller/larger/incompatible; case-revision grandfathering; removed/replaced IDs; achievement reconstruction. No tested path may shrink historical solved facts without explicit profile reset.

### Controller race tests
Held reposition + B/LB/RB/reset/pause/inspect; rotate/place spam during topology animation; undo during stale animation; solve then destructive input during success lock; keyboard/mouse parity. Domain snapshot must always correspond to latest committed transaction, never a provisional ghost or animation frame.

### Localization/layout tests
Every supported locale at 1280x800 and larger text scale, six longest predicate cards, controller glyph variants, no meaning relying on color, no marker/invalid-state glyph collision, focused details not hiding selected cell.

### Oracle leakage tests
Release package/static scan and runtime tests confirm no ordinary play path can access witness solutions, satisfying assignments/counts, ablation/critical-zone diagnostics, extendability or pre-solve reasoning skeleton. Ghost preview derives footprint legality only; inspect derives committed state only.

### Save/version tests
Every supported migration chain has golden input/output, idempotent destination behavior and downgrade/future-version refusal.

---

## 17. Out-of-scope and change control

Launch canon excludes: Sokoban pushing, moving avatar, physics, fluids, fold/trim, portals, keys/switches/doors, path drawing, timers/reflex challenge, randomized roguelike runs, multiplayer, daily/streak systems, required editor/Workshop, server dependency, new polyomino catalogue, hidden objectives and solution-directed runtime hints.

**Design-change rule:** any proposed change to board semantics, connectivity/hole definition, piece vocabulary, predicate grammar, progression gates, oracle firewall, save monotonicity/recovery, 9x9/4-piece ceilings or finite-premium product identity is a post-freeze design change. It must be documented explicitly, re-run affected certification/fixtures/adversarial review, and may require rules-version change. An implementer must never “fill a gap” by inventing such behavior.

Content re-authoring inside frozen grammar is normal implementation/content work provided it passes all certification/curation gates.

---

## 18. Title and repository target

`OPENWORK` may remain the provisional product title during implementation. It is not a promise that trademark/store collision review has been completed. A later shipping-name change is allowed as a business/branding variable if mechanics/content identity remain unchanged.

Deterministic dedicated-repository target for this frozen design: **`Mikayilzade/openwork`**.

---

## 19. Authority and freeze verdict

A fresh implementation session can build the complete intended game without inventing important gameplay behavior. Earlier historical contradictions have been resolved here, especially:
- holes are zero-boundary remaining-open components and count as components;
- Act-I C1–C4 are mandatory;
- reduced 30–35 manifests retain six acts of 5–6 cases and four-solve gates;
- Act VI requires >=24 active solves and finale requires four other Act-VI solves;
- anti-repetition uses reasoning-skeleton gates, not family quotas alone;
- late/mastery predicate redundancy is objectively ablated;
- held reposition has a deterministic command matrix;
- current-state explanation never becomes hypothetical solver preview;
- both-local-corrupt state remains uncommitted until Cloud recovery or explicit new profile;
- future-version profiles block destructive older writes;
- solved facts and unlocked achievements are monotonic across ordinary revisions/removals;
- runtime is firewalled from certifier oracle data.

Remaining unknowns are explicit empirical release gates or implementation-flexible engineering/business variables, not missing core design.

**PHASE 11 = COMPLETE.**

**DESIGN COMPLETE = YES.**
