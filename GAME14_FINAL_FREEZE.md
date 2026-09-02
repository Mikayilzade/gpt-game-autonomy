# GAME #014 — FINAL SPECIFICATION FREEZE

Date: 2026-09-02
Working title: **NEGATIVE CASTING**
Status: **DESIGN COMPLETE = YES**
Migration target: `Mikayilzade/negative-casting`
Migration status at freeze: **PENDING — repository not found on 2026-09-02**

This file is the **stand-alone canonical implementation design authority** for Game #014. Earlier Game #014 files remain retained only as design evidence/history until migration integrity is verified. If an earlier Game #014 file conflicts with this freeze, **this file wins**.

No production implementation belongs in the factory repository.

---

# 1. Authority and precedence

For Game #014 implementation, authority order is:
1. `GAME14_FINAL_FREEZE.md` — final gameplay/product/technical authority.
2. Explicit implementation-stage empirical-gate results that do not change frozen grammar.
3. Earlier Game #014 Phase 3–10 files only as explanatory evidence when this freeze is silent.
4. Tournament/research files are historical evidence only and cannot supply new mechanics.

If implementation discovers a contradiction that cannot be resolved by this authority order, mark it **DESIGN REOPEN REQUIRED** rather than inventing a gameplay rule.

Rejected tournament concepts — Missing Reflection, Casting Call and all other rejected candidates — are not latent feature sources.

---

# 2. Product identity

**Genre:** compact premium spatial-deduction puzzle.

**Lead platform:** PC / Steam, controller-first and handheld-readable from the first implementation increment.

**Lead engine direction:** Godot 4.7.x stable, GDScript-first. Canonical puzzle truth is engine-independent and must remain in a deterministic exact-data layer.

**One-sentence hook:** arrange a few socketed opaque sculptures between two fixed lights so several projection surfaces receive exactly the required pattern of fully lit, single-light-shadowed and double-shadowed sample points.

**Core fantasy:** sculpt negative space indirectly. The player does not paint a silhouette; they choose physical blocker poses whose coupled projections across multiple surfaces create the desired light/shadow result.

**Target player:** players who enjoy authored deterministic deduction, visible cause/effect and eliminating classes of possibilities rather than dexterity, hidden rules, external note-taking or random search.

**Product structure:** finite authored premium campaign, 24-case required shipping floor, optional quality-gated NC25–NC30 only if they independently pass the same standards.

**Expected first completion:** approximately 3–5 hours, subject to the empirical duration gate below.

---

# 3. Immutable gameplay grammar

The following are frozen. Changing any item requires explicit design reopen.

## 3.1 Logical world
Each case owns one bounded 2D casting plane with integer-authored geometry and exact rational calculations where required.

Each shipping case contains:
- exactly **2 fixed logical point lights**, `L1` and `L2`;
- **1–3 straight projection surfaces**;
- **2–6 blocker instances** maximum by mechanical ceiling, with the 24-case floor normally using no more than 5;
- one fixed socket per blocker instance;
- normally **2–4 discrete legal poses** per blocker;
- target sample points on each surface;
- exactly four target semantic classes.

Lights do not move during a solve. Blockers do not translate between sockets. The player's meaningful mutation is choosing another allowed discrete pose for a selected blocker.

## 3.2 Blocker geometry
A blocker archetype is a simple positive-area opaque polygon footprint with integer local vertices. Shipping geometry should prefer convex or orthogonally simple shapes; concavity is allowed only when readability remains unambiguous.

Baseline pose transforms are exact 90-degree rotations around the socketed local origin. Explicit mirrored poses are allowed only as separately authored discrete physical poses; reflection is not a continuous player verb.

No special blocker materials, powers, transparency, refraction, partial opacity or hidden state exist.

## 3.3 Surface samples
A projection surface is a straight open segment from authored integer endpoint `A` to `B`, with ordered rational sample parameters `0<t<1`.

Recommended sample count is 3–10; hard frozen ceiling is 12 per surface. Late campaign content must reduce density before increasing UI complexity.

A rendered surface cell may be broad and attractive, but logical truth is evaluated only at its canonical sample point.

## 3.4 Exact occlusion truth
For light `Lj`, sample point `P` and transformed blocker polygon `B`:

`blocked(Lj,P,B) = TRUE` iff the **open line segment** from `Lj` to `P` intersects the **strict interior** of `B`.

Pure tangent/boundary contact does not block. Any positive-length traversal through strict polygon interior blocks.

For a complete blocker configuration `C`:

`s_j(P,C) = OR over all blockers of blocked(Lj,P,B_i[state_i])`.

Target classes are exactly:
- `LIT` = `(s1=0,s2=0)`
- `L1_ONLY` = `(s1=1,s2=0)`
- `L2_ONLY` = `(s1=0,s2=1)`
- `BOTH` = `(s1=1,s2=1)`

The names describe **which light is blocked**, not which remains visible.

## 3.5 Derived truth only
Per-state projection/incidence masks may be cached for speed/tooling but are always derived from canonical geometry. Authoring or hand-editing arbitrary incidence bitmasks as logical truth is forbidden.

Any geometry mutation invalidates incidence, equivalence, solution and route certification caches.

## 3.6 Legal configuration
Default authoring should make the Cartesian set of blocker poses collision-free. Rare explicit illegal joint-state tuples may exist only for physical-collision safety and may not become a primary deduction family.

Blockers may not intersect lights or projection surfaces in any legal pose.

## 3.7 Player actions
Required logical actions:
- previous/next blocker;
- previous/next legal blocker pose;
- previous/next projection surface;
- toggle selected-blocker current-pose contribution inspection;
- explicit Check;
- Undo;
- Redo;
- Reset Case;
- open case menu / pause / leave / replay.

There is no continuous placement, free rotation, moving lights, free camera navigation, timing challenge or physics dexterity.

## 3.8 Current-state observability
Actual current shadows update immediately after a blocker-pose mutation. The player may always see the current semantic state of samples.

Selected-blocker contribution inspection may reveal only what the **currently selected blocker in its current pose** physically occludes. It is explanatory causality, not a solver.

## 3.9 Check / success / failure
Check is explicit; the game does not auto-solve the instant the target matches.

A case is solved iff every sample's exact current semantic class matches its target class.

An incorrect Check has no penalty. It may mark **which samples mismatch**, never which blocker/pose caused the mismatch or how to fix it.

No lives, score, move limit, par, timer or failure economy exists.

## 3.10 Solution semantics
Every physical target-valid blocker-state vector is accepted.

Two blocker poses are observationally equivalent for a case iff they produce identical `(L1,L2)` incidence on all samples and participate identically in explicit legality constraints.

The game may not reject a target-valid solution merely because it differs from the author's preferred pose. Default content preference is one meaningful solution class, not necessarily one unique physical vector.

---

# 4. Frozen sources of depth

All campaign difficulty must arise from consequences of the same projection rule. The canonical human deduction vocabulary is:
- `PROTECTED_LIT_ELIMINATION`
- `ENDPOINT_EXTENT_ELIMINATION`
- `CHANNEL_ATTRIBUTION`
- `BOTH_DECOMPOSITION`
- `UNIQUE_PRODUCER`
- `CROSS_SURFACE_EQUIVALENCE_SPLIT`
- `LEGALITY_CLEANUP` — valid but does not count toward depth gate
- `RESIDUAL_ASSIGNMENT` — valid but does not count toward depth gate

The four protected depth pillars are:
1. **protected negative space:** required LIT samples eliminate every pose that would touch them;
2. **endpoint/extent geometry:** coherent shadow boundaries distinguish poses with similar total coverage;
3. **channel attribution:** L1_ONLY/L2_ONLY/BOTH encode cause of darkness rather than only darkness amount;
4. **cross-surface identity:** a blocker pose ambiguous on one surface can be split by another surface.

A shipping case whose most natural human explanation is only generic exact-cover/set-cover is rejected even if machine-certified.

---

# 5. Human-route certification — final contract

Machine solvability is necessary and insufficient.

Every shipping case must have at least one intended **proof-carrying human route** represented as connected candidate-class reductions.

Each route step records:
- stable `step_id`;
- allowed deduction family;
- exact premises;
- subject candidate class/blocker;
- declared before/after class set or count;
- dependency ids;
- human-readable rationale.

The certifier may not trust author-entered reductions. For every counted step it must independently:
1. reconstruct the candidate class set implied by canonical geometry/target/legality plus only previously certified route facts;
2. verify the declared premises against exact derived truth;
3. apply the family-specific logical elimination predicate;
4. recompute the resulting class set;
5. prove that the claimed reduction is entailed;
6. reject the route if the reduction depends on an unstated assumption, author pose or guessed player knowledge.

## 5.1 Difficulty gates
TEACH/EARLY cases may intentionally have short routes.

Every `MID`, `LATE` and `CAPSTONE` case requires:
- at least **3 meaningful dependency-connected pre-residual class eliminations**;
- at least two counting deduction families;
- at least **2 player-legible geometric/causal grounded steps** before residual assignment;
- at least one grounded step from `PROTECTED_LIT_ELIMINATION`, `ENDPOINT_EXTENT_ELIMINATION`, or `CROSS_SURFACE_EQUIVALENCE_SPLIT`;
- no counted step whose only explanation is “the incidence table says this pose is wrong.”

Late/capstone content should normally use at least 3 meaningful families.

NC24 specifically requires at least **4 connected meaningful eliminations** before residual choice and at least 3 families.

## 5.2 Normalized route signature
Every MID+ case records a normalized cognitive route signature independent of blocker ids/cosmetics, including:
- ordered meaningful deduction families;
- surface count active at each step;
- state-vs-equivalence-class reasoning type;
- geometric-boundary vs channel-causal vs producer-count character;
- number of intended surface-focus switches;
- final pre-residual family.

Acceptance rules:
- adjacent MID+ cases may not share the same normalized signature unless explicitly marked tutorial reinforcement;
- no three-case MID/LATE window may share the same first two normalized operations;
- NC17–NC24 must contain at least 3 materially different normalized route shapes;
- no three consecutive MID/LATE cases may share both the same first decisive and same final decisive family.

---

# 6. Campaign / content freeze

## 6.1 Shipping floor
Canonical floor is **NC01–NC24**, 8 groups of 3 cases.

Group rule: entering an eligible group makes its eligible cases available; normally completing **2 of 3** advances the general group threshold. This is an anti-stuck structure, not permission to bypass foundational vocabulary.

`Campaign Complete` means all 24 `required_for_floor` cases solved.

Optional NC25–NC30, if any, never become retroactively required for `Campaign Complete`.

## 6.2 Foundation prerequisite graph — final repair
The general 2-of-3 unlock system is supplemented by data-driven foundation prerequisites.

Foundation ids:
- `foundation.channel` -> established by completing **NC03**;
- `foundation.both` -> established by completing **NC04**;
- `foundation.multisurface` -> established by completing **NC07**.

Every case declares `required_foundations[]`.

Frozen assignment rule:
- NC01–NC02 require none.
- NC03 establishes channel foundation and requires none.
- NC04 establishes BOTH foundation; it requires `foundation.channel` because BOTH explanation assumes the two channel identities are understood.
- NC05 requires none beyond ordinary earlier campaign availability.
- NC06 requires `foundation.channel` because its intended synthesis includes channel attribution.
- NC07 establishes multi-surface foundation; it does not require BOTH, but requires `foundation.channel` only if its final authored target uses single-channel semantic reasoning materially. Default design should keep NC07 readable if channel knowledge is already available via NC03.
- NC08 requires `foundation.multisurface` and `foundation.channel`.
- NC09–NC24 declare prerequisites from their actual intended route: any route containing CHANNEL_ATTRIBUTION requires `foundation.channel`; any route containing BOTH_DECOMPOSITION requires `foundation.both`; any route containing CROSS_SURFACE_EQUIVALENCE_SPLIT requires `foundation.multisurface`.

Availability is therefore derived from **both** group-threshold state and declared foundation prerequisites.

A skipped non-foundation case never blocks later unrelated content. A skipped foundation remains clearly identified as required for the dependent cases it unlocks. The UI must state the prerequisite plainly without revealing puzzle deductions.

## 6.3 Frozen 24-case progression skeleton
- NC01: protected LIT teaching.
- NC02: protected LIT -> unique producer.
- NC03: channel attribution foundation.
- NC04: BOTH foundation.
- NC05: endpoint/extent.
- NC06: endpoint/extent -> channel synthesis.
- NC07: first second surface / cross-surface foundation.
- NC08: demo synthesis using cross-surface split.
- NC09–NC16: two-surface MID cases interleaving channel/BOTH, protected LIT, endpoint/extent, unique producer and cross-surface splits.
- NC17: first three-surface case with low sample counts.
- NC18–NC22: late synthesis; five blockers only where class-level pruning occurs early.
- NC23–NC24: capstones with full multi-family proof routes.

Three surfaces are a **late representation change**, not permission to add more cells indiscriminately.

## 6.4 Blocker library
Launch target: about 8 logical archetypes, hard ceiling 10 before explicit review.

Preferred families include short/long bars, fins, asymmetric orthogonal shapes, readable convex shapes and stepped shapes. New archetypes are justified by readable geometric relationships, never merely to produce a new bitmask.

Archetypes should be reused across campaign cases so player shape mastery transfers.

## 6.5 Authoring pipeline
Every shipping case must pass:
1. intent/aha sentence;
2. canonical geometry sketch;
3. exact incidence derivation;
4. geometry/collision/grazing sanity;
5. semantic target construction;
6. exhaustive solution/equivalence certification;
7. proof-carrying human-route certification;
8. unintended-solution review;
9. normalized repetition review;
10. hint certification;
11. handheld/readability review;
12. blind difficulty/pacing review;
13. logic-fingerprint/hash freeze.

Any logical mutation re-enters certification. No stale-cache waiver exists.

---

# 7. Demo freeze

Demo is exactly the same rule system and data contract as the full game.

Frozen demo subset: **NC01–NC08**, target approximately 20–30 minutes.

Required beats:
- NC01 select/change pose/check + protected light;
- NC02 contribution inspection + unique producer;
- NC03 channel semantics;
- NC04 BOTH semantics;
- NC05 endpoint/extent aha;
- NC06 synthesis;
- NC07 second-surface reveal;
- NC08 satisfying second-surface synthesis capstone.

Demo must end after a complete solve before purchase/wishlist messaging.

Preferred demo->full transfer is one-way and additive only into a new/empty compatible full campaign. Once valid full progress exists, demo data can never overwrite or roll it back.

---

# 8. UX / presentation freeze

## 8.1 Camera and world presentation
Present each case as a compact stylized casting-table/diorama, not a free-exploration 3D room.

The authored camera must preserve readable relation among both light origins, blocker sockets, the focused surface and target/current sample state.

Rendering may be attractive/soft/3D-looking, but renderer shadow maps, physics queries and visual transforms are never puzzle authority.

## 8.2 Surface layout
One surface: dominant integrated wall/panel.

Two surfaces: one primary + one persistent readable secondary panel; single-action swap.

Three surfaces: one primary + two persistent compact surface cards; never squeeze three equal full panels or present an all-surfaces solver matrix.

Switching surface preserves blocker focus and does not mutate puzzle truth.

## 8.3 Target/current language
Every semantic class has redundant non-color encoding. Hue may reinforce but never carry meaning alone.

Each logical cell communicates separately:
- fixed **target requirement**;
- actual **current physical state**.

Soft rendered shadows never replace crisp semantic glyph truth.

## 8.4 Contribution inspection anti-oracle boundary
Allowed:
- selected blocker only;
- current pose only;
- current physical rays/affected samples;
- no target-evaluation coloring.

Forbidden:
- counterfactual pose previews;
- side-by-side candidates;
- correctness percentage;
- mismatch delta after a move;
- best pose/ranking;
- remaining-solution count;
- heatmaps;
- automatic pose sweep;
- human-route playback.

Manual pose changing and observing the resulting current state is core play and is allowed.

## 8.5 Mismatch feedback
Incorrect Check may show mismatch locations and a neutral mismatch count. It may never identify responsible blockers or recommended changes.

## 8.6 Input model
All actions must exist as logical actions rather than hard-coded buttons. Complete controller and keyboard-only paths are required; mouse support is additive.

One physical accepted input event may yield **at most one logical action**.

If Steam Input and engine events can both represent the same physical press, one layer owns/consumes it so duplicate pose mutation is impossible.

Gameplay inputs do not cross modal boundaries. Opening/closing pause, menus, reset confirmation or completion panels establishes a modal action barrier: stale queued gameplay events are discarded/consumed rather than applied afterward.

Held-repeat is allowed only for explicitly approved navigation actions with controlled repeat cadence; destructive/commit/reset actions do not repeat.

Prompt/device-family changes occur only after deliberate accepted input from another family, not passive mouse/trackpad motion. Glyph changes must not move puzzle focus.

## 8.7 Undo/reset/resume
Every blocker-pose mutation is one atomic undo step. Surface switching/focus/inspection are not undo history.

Reset returns current case poses to authored initial state but never clears prior case completion.

Leaving a case autosaves current blocker poses. The **minimum required resumable truth** is exact blocker-pose vector + compatible case/content logic identity. Undo stack, mismatch highlights and transient focus are optional across restart.

---

# 9. Accessibility freeze

Required design-level invariants:
- all channel/target/current information readable without color;
- no essential audio-only information;
- reduced-motion mode may shorten/cut presentation transitions without altering truth;
- complete control remapping except platform-reserved operations;
- UI scaling cannot invalidate semantic readability;
- controller-only operation of all campaign content;
- no achievement or completion penalty for accessibility settings or hint usage;
- no mandatory external notes for ordinary shipping cases.

Handheld baseline validation remains 1280x800, with 1280x720 and 1920x1080/aspect-ratio checks.

---

# 10. Hint freeze

Hints are free, optional, non-punitive and never paid. Contribution inspection is not a hint.

Each shipping case may have up to three authored tiers:
1. redirect attention to a universal semantic idea;
2. name a case-specific surface/relationship without naming the solution pose;
3. expose one **statically certified logical premise** without stating the final pose.

Hints may never depend on guessed player knowledge/current thought state.

Tier-3 wording such as “remaining” or “now only” is forbidden unless that candidate reduction is itself proven from static certified premises used by the hint chain.

Hints are certified with the case. Geometry/target/route mutation invalidates hint certification.

No full solution reveal exists in the frozen product. Adding one requires design reopen.

---

# 11. Commercial model freeze

Finite premium product. No retention economy.

**Target US base price:** `$11.99`.

Pre-release acceptable decision band without design reopen: `$9.99–$12.99`. `$14.99` requires exceptional production/value evidence and is not the default.

Preferred launch discount: about 10% for 7–14 days if strategically useful, subject to Steam rules current at release.

No ads, currencies, consumables, paid hints, battle pass, subscription, loot boxes, gacha, energy, FOMO, daily rewards, paid skips, grind, cosmetic MTX store or required external account.

Achievements target roughly 10–14, with milestones only. Forbidden achievement purity tests include no-hint, speed, move-count, no-undo/no-reset, specific-device, accessibility-disabled, grind/streak or one-shot missable requirements.

Replay is simple case replay; no leaderboards, scores, daily puzzles, streaks or procedural runs.

Future DLC/content packs may use only the frozen two-light/socketed-opaque-blocker/1–3-surface/four-target-class grammar unless design is explicitly reopened.

---

# 12. Technical implementation contract

## 12.1 Layering
Recommended conceptual layers:
1. Core Logic — exact geometry/incidence/equivalence/evaluation.
2. Content Model — validated schemas, stable ids, revisions, hashes.
3. Game State — session/campaign/progression/hints/save.
4. Presentation/UX — scenes, camera, semantic overlays, animation/audio/input adapters.
5. Platform Services — Steam Input/Cloud/Achievements/store integration.

Layers 4–5 consume truth but cannot create it.

## 12.2 Exact numeric representation
Authored coordinates are integers. Rational values use normalized `(int64 num, int64 den>0)` with exact comparison and checked arithmetic.

Canonical 90-degree transforms use integer matrices; no floating-point trig enters logical pose generation.

## 12.3 Reference segment-polygon predicate
Canonical implementation must use an exact open-segment vs strict-polygon-interior predicate independent of engine physics.

Reference behavior:
- partition the segment by exact boundary-intersection parameters;
- sample exact midpoints of nonzero parameter intervals;
- classify midpoint as OUTSIDE/BOUNDARY/INSIDE using exact predicates;
- return blocked iff any interval within `0<u<1` lies strictly INSIDE.

Tangency/boundary-only overlap therefore remains non-blocking.

Any optimized predicate must be regression-equivalent to the reference implementation on canonical/fuzz fixtures.

## 12.4 Canonical data
Stable ids, never list indices, are required for archetypes, cases, blockers, poses, surfaces, groups, foundations, route steps and hint ids.

Case logical data includes schema/content revision, exact geometry, blocker legal poses, target, campaign metadata, foundations/prerequisites, intended route and hints.

## 12.5 Logic fingerprint
Each case/revision must generate a stable logical compatibility fingerprint covering at minimum:
- core-logic truth version;
- case schema/content revision;
- lights;
- surfaces/sample rationals;
- blocker archetype geometry revisions;
- sockets/legal pose transforms;
- explicit legality constraints;
- target classes;
- accepted-solution policy.

Save/resume migration may not infer compatibility from `case_id` alone.

A changed target/geometry requires an explicit migration declaration before resumable pose state is reused.

## 12.6 Derived caches
Geometry-incidence caches are disposable and keyed by core logic version + normalized geometry hash.

Solution/route/hint certification caches additionally include target hash, certifier version, route revision and hint revision as applicable.

Cache mismatch means regenerate/reject; never reinterpret geometry to match cache.

## 12.7 Certifier
For frozen maxima the reference certifier may exhaustively enumerate legal complete state vectors (ordinary upper bound roughly `4^6 = 4096`) and compute:
- target-valid physical solutions;
- observational equivalence classes;
- legality-sensitive equivalence;
- human-route proof checks;
- hint premise proof checks;
- repetition metadata;
- geometry clearance diagnostics.

Solver uniqueness never substitutes for human-route acceptance.

## 12.8 Runtime session state
Canonical mutable puzzle truth is blocker pose by stable blocker id.

Selection, focused surface, contribution inspection, animation and mismatch highlighting are UI state only.

Logical mutation is atomic; animation may interpolate visually afterward, but intermediate rendered transforms are never sampled as solution truth.

## 12.9 Save / atomicity
Persistence uses recoverability-first primary/temp/backup behavior with validation/checksum/schema metadata and monotonic **save generation**.

A pose mutation completes logically before the persistence transaction begins.

On recovery, select among only validated compatible candidates. Corrupt bytes are never accepted merely because a filename is primary.

## 12.10 Idempotent completion transaction
Case completion is a set fact keyed by compatible stable case identity, not a repeatable event.

Frozen order:
1. exact Check succeeds;
2. local campaign completion set is updated atomically;
3. derived unlock/progression is recomputed;
4. save generation is committed locally;
5. platform achievements/cloud side effects are queued/reconciled afterward.

Repeating Check, replaying a solved case, restarting after crash or re-merging cloud state must not duplicate campaign rewards/events.

Achievements/platform events are derived side effects, never authoritative save truth.

## 12.11 Unlock derivation
Group availability and case availability are derived/verified from:
- compatible solved-case set;
- group thresholds;
- foundation prerequisite ids.

Mutable stored unlock booleans are caches only and cannot override canonical derivation.

## 12.12 Cloud merge boundary
Automatically union-merge only monotonic compatible facts such as:
- solved-case ids;
- opened hint tiers;
- tutorial-seen flags where semantically safe.

Do not field-wise merge two active blocker pose vectors, incompatible content revisions or device-local display state.

When two valid active-session candidates conflict and ordering is ambiguous, preserve a recoverable alternative rather than fabricating a hybrid pose vector.

## 12.13 Demo import
Demo import may seed a new/empty full campaign once. It is idempotent, version/fingerprint aware and cannot overwrite established valid full-game progress.

Campaign availability is recomputed from imported compatible completion facts, never copied as opaque unlock booleans.

## 12.14 Platform failure
Steam Cloud, Steam Input enhancements and achievements may be unavailable/offline without preventing campaign gameplay or local save progression.

Offline single-player remains complete after normal installation/entitlement handling.

---

# 13. Validation / acceptance criteria

A fresh implementation session may consider a build design-conformant only when all applicable conditions hold.

## 13.1 Core logic
- exact reference geometry predicates pass deterministic unit/fuzz tests;
- same canonical case data yields bit-identical target truth independent of renderer/backend;
- arbitrary authored shadow masks cannot override geometry;
- tangent/boundary fixtures follow frozen semantics;
- legality-sensitive observational equivalence is tested;
- every required floor case can be exhaustively certified within practical tooling time.

## 13.2 Content
- 24 required floor cases exist and pass all machine + human-route gates;
- foundation prerequisites are data-driven and cannot be bypassed by 2-of-3 thresholds;
- NC03/NC04/NC07 establish channel/BOTH/multi-surface foundations;
- all dependent cases declare the needed prerequisites;
- no MID+ case passes using merely incidence-table exact-cover logic;
- capstones meet stronger route requirements;
- repetition signature gates pass before shipping.

## 13.3 UX
- controller-only full campaign path works;
- one physical event cannot double-fire a logical action;
- modal barriers prevent queued gameplay mutation;
- target/current/channel semantics remain readable without color;
- contribution inspection never becomes counterfactual/ranking oracle;
- incorrect Check reveals location only, not responsible blocker;
- 1/2/3-surface layouts obey primary-surface hierarchy.

## 13.4 Persistence
- crash during save preserves at least one validated recoverable generation;
- corrupt resume resets only incompatible active case state when safe campaign completion facts remain valid;
- completion transaction is idempotent;
- demo import cannot roll back full progress;
- cloud merge never fabricates hybrid active pose state;
- unlocks are recomputed from completion + prerequisites.

## 13.5 Commercial/product
- demo uses NC01–NC08 same rules and ends on NC08 complete solve;
- all 24 floor cases are required for Campaign Complete;
- hints are free/non-punitive and certified;
- achievements contain no purity/grind/accessibility penalties;
- offline campaign works without server dependency;
- no monetization/retention system alters puzzle truth.

---

# 14. Explicit empirical implementation gates

These questions are intentionally not falsely “solved” on paper. They do not block design freeze because implementation already knows the required response if they fail.

## E1 — late 3-surface readability
Validate representative NC17/NC20/NC24-style layouts at:
- 1280x800 default UI scale;
- 1280x720 default UI scale;
- 1280x800 at launch maximum accessibility UI scale;
- controller-only navigation.

Pass only if players can read target/current/channel on secondary cards, identify mismatch surface/location, switch focus with one action and recover comparison without external notes.

Failure repair order:
1. reduce samples/surface;
2. reduce blocker/UI density;
3. enlarge/switch surface presentation;
4. collapse nonessential HUD chrome.

Forbidden repair: solver matrix, color-only simplification, tiny glyphs or required memorization.

## E2 — perceived repetition
Blind-test NC09–NC24. Record each player's remembered “aha.” If adjacent certified cases are described as the same reasoning rhythm, rework/reorder geometry/content. Machine route-signature diversity is a filter, not proof.

## E3 — completion duration / value
Measure blind first-completion time. If materially below approximately 3 hours, reconsider price/positioning before inflating content. Additional NC25–NC30 cases may be added only if independently quality-certified.

## E4 — visual-clearance threshold
After real renderer/camera exists, freeze a world-space visual clearance diagnostic threshold so shipping rays never depend on visually microscopic tangency. Exact logical incidence never changes with this threshold.

## E5 — Deck-class performance and presentation
Validate 60 fps target at 1280x800 on Deck-class hardware with 30 fps hard floor during cosmetic transitions, plus blocker silhouette/glyph/controller-prompt readability. Logical mutation may not depend on frame-rate/GPU completion.

## E6 — Tier-3 hint sufficiency
Blind-test whether the frozen three-tier hint ladder prevents permanent abandonment without solution reveal. If a full solution reveal becomes necessary, that is **DESIGN REOPEN**, not an implementation convenience.

---

# 15. Unknown audit

At final freeze every previously material unknown is classified:

### Answered
- exact shadow truth;
- number/behavior of logical lights;
- blocker state model;
- target semantics;
- legal actions;
- solution/equivalence acceptance;
- human deduction vocabulary;
- 24-case campaign floor;
- 2-of-3 progression plus semantic foundations;
- demo content;
- multi-surface UX model;
- anti-oracle inspection/check behavior;
- hint policy;
- commercial model;
- deterministic technical architecture;
- save/import/cloud/input ownership contracts;
- authority precedence and implementation acceptance criteria.

### Implementation-flexible without design reopen
- exact art style/materials within readability rules;
- exact physical controller button assignments, provided logical action separation remains;
- precise menu spacing/animation timings;
- cosmetic camera easing;
- localization wording that preserves semantics;
- exact Steam integration wrapper/library choice;
- exact save serialization format, provided frozen atomic/version/fingerprint contracts hold;
- optional macOS support;
- whether NC25–NC30 exist at launch.

### Empirical
- E1 late multi-surface readability;
- E2 perceived repetition;
- E3 first-completion duration/value;
- E4 renderer visual-clearance threshold;
- E5 final Deck performance/readability;
- E6 Tier-3 hint sufficiency.

### Design-reopen blockers
None are currently unresolved. A future need for a third light, moving lights, free placement, transparent/refractive blockers, special powers, new target classes, full solver UI, solution reveal, co-op, procedural mode or other new puzzle rule requires explicit reopen.

---

# 16. Explicit out of scope

Do not add during implementation without design reopen:
- third logical light channel;
- moving lights;
- free blocker translation;
- continuous rotation;
- mirrors/reflection;
- transparent/refractive/colored blockers as puzzle rules;
- penumbra/distance attenuation as logical state;
- arbitrary shadow-mask authoring;
- blocker powers/resources;
- physics/timing challenges;
- free-camera navigation dependency;
- multiplayer/co-op;
- roguelike/deckbuilding/crafting/upgrades/currencies;
- procedural infinite campaign;
- score/timer/par/leaderboard/daily/streak systems;
- paid hints/solutions;
- launch-required level editor/workshop;
- mandatory external notes;
- color-only semantics.

---

# 17. Implementation handoff sequence for dedicated repository

When `Mikayilzade/negative-casting` exists, migration should copy this final freeze and the supporting Game #014 design/history needed for traceability, then create/verify:
- `IMPLEMENTATION_START_HERE.md`
- `IMPLEMENTATION_STATUS.md`
- `CI_NOTIFICATION_POLICY.md` or equivalent explicit CI/email-noise policy

Recommended implementation phases:
- 12A technical bootstrap: pure exact core, schemas, certifier harness, persistence skeleton, input ownership skeleton.
- 12B vertical slice: NC01–NC03 playable end to end with controller/mouse/keyboard and semantic overlay.
- 12C core systems complete: all frozen verbs, two-light geometry, 1–3 surfaces, inspection/check, progression/foundations.
- 12D content population: NC01–NC24 authored and proof-certified.
- 12E UX/accessibility/Deck: surface hierarchy, remapping, glyphs, large UI, demo boundary.
- 12F adversarial QA: saves/cloud/import/idempotency/input races/malformed data/equivalence.
- 12G empirical gates: E1–E6.
- 12H release candidate: demo/full packaging, performance/regression, Steam release checklist.

Implementation is complete only when the dedicated repository sets its own `IMPLEMENTATION COMPLETE = YES`.

---

# 18. Final freeze verdict

**DESIGN COMPLETE = YES.**

A fresh implementation session can now build Negative Casting without inventing important gameplay. Remaining uncertainties are explicit empirical implementation gates with predetermined repair boundaries rather than missing design.

Migration was checked on 2026-09-02. `Mikayilzade/negative-casting` did not exist, so migration is **PENDING**. This full Game #014 package must remain a **frozen NON-ACTIVE safety archive** in the factory until a dedicated repository becomes available and migration integrity is verified.

Per factory continuity rules, pending migration does **not** keep Game #014 active and does **not** block Game #015.
