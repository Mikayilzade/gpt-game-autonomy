# GAME #014 — PHASE 5 CONTENT ARCHITECTURE

Date: 2026-09-02
Status: COMPLETE — 24-case shipping floor and authoring/certification grammar frozen; UX / Presentation Architecture next.
Working title: **NEGATIVE CASTING**
Authority: `START_HERE.md` -> `STATUS.md` -> `GAME_INDEX.md` -> Game #014 tournament record -> `GAME14_PRODUCT_THESIS.md` -> `GAME14_MECHANICAL_ARCHITECTURE.md` -> this file.

## 1. Phase-5 verdict
**PASS.** A 24-case finite premium campaign can be populated with the frozen two-light / geometry-derived projection rule without relying on blocker-count inflation, arbitrary masks, special powers, procedural filler, or bespoke sculptures per puzzle.

The launch content floor is **exactly 24 required-quality authored cases**. A target build may contain up to **30 total cases**, but cases 25–30 are optional expansion-at-launch candidates and ship only if they pass the same human-route, repetition and handheld-readability gates. Quantity is not a completion gate.

The campaign is organized around six reasoning families that are consequences of the same geometry contract:
1. protected light;
2. endpoint / extent;
3. channel attribution;
4. BOTH decomposition / unique producer;
5. cross-surface equivalence splitting;
6. synthesis that interleaves three or more of the above.

No family introduces a new player verb or blocker power.

---

# 2. Content-unit hierarchy

## 2.1 Archetype
A **blocker archetype** owns canonical local polygon geometry and presentation identity. It does not own case-specific projection masks.

Launch blocker library target: **8 archetypes**, hard ceiling **10** before freeze unless a later content audit proves a genuine readability gap.

Recommended launch families:
- `BAR_SHORT` — compact elongated rectangle; easy extent teaching.
- `BAR_LONG` — longer narrow rectangle; stronger endpoint discrimination.
- `TALL_FIN` — narrow orthogonal fin; large angular-span changes under rotation.
- `OFFSET_L` — orthogonally simple L footprint; introduces asymmetric projection without concavity-heavy visual ambiguity.
- `CHEVRON` — convex or near-convex angled silhouette represented by simple polygon; useful for state-equivalence splits.
- `HAMMER` — wide head + narrow stem; readable asymmetric extent.
- `STEP` — stepped orthogonal polygon; two visually distinct endpoint families.
- `KITE` — compact convex non-orthogonal silhouette for late cases where its ray interval remains visually clear.

Archetype restrictions:
- Every archetype must remain identifiable at handheld scale from its silhouette alone.
- No archetype may depend on texture or color to communicate orientation.
- Concave shapes are exceptional and require explicit readability approval.
- An archetype may be reused in many cases; reuse is desirable because mastery should transfer.
- A new archetype is never justified merely to create a new projection mask.

## 2.2 Instance
A blocker **instance** references one archetype, one socket position, 2–4 legal states and optional case-local cosmetic variant. Logical variation comes from light/socket/surface relationships, not bespoke geometry mutation.

## 2.3 Case
A case is one complete authored puzzle with canonical geometry, target, initial state, campaign metadata, derived incidence, solution classes and certified human route.

## 2.4 Group
Cases are arranged into **8 campaign groups of 3 cases** for the 24-case floor. Entering a group unlocks all three. Completing **2 of 3** unlocks the next group. The final campaign completion badge requires all 24 floor cases, but reaching the final group does not require perfect completion of every earlier group.

This creates an alternate route when a player is stuck without turning progression into a map-management system.

---

# 3. Canonical case data contract

Canonical authored fields:

### Identity / version
- `case_id`
- `schema_version`
- `content_revision`
- `display_order`
- `group_id`
- `required_for_floor`
- `demo_included`
- `difficulty_band`: `TEACH / EARLY / MID / LATE / CAPSTONE`

### Casting geometry
- casting bounds
- `L1`, `L2` point coordinates
- surfaces: id, endpoints, ordered rational sample parameters
- blocker archetype definitions by stable id/version reference
- blocker instances: archetype id, socket, ordered legal states
- rare explicit illegal joint-state tuples when collision safety requires them

### Puzzle state
- initial blocker-state vector
- target semantic class at every sample
- accepted-solution policy (normally all physical target-valid solution classes)

### Campaign / presentation metadata
- title/short flavor line if any
- target estimated solve-time band
- focus surface on first load
- tutorial callout flags
- optional intended camera/presentation emphasis ids (non-logical)

### Human-route metadata
- intended route id/version
- deduction steps using Phase-4 vocabulary
- dependency graph between steps
- primary deduction families
- estimated candidate-class reduction after each step
- residual assignment threshold
- author note describing the intended aha in one sentence

### Validation metadata
- certification tool version
- geometry hash
- derived-incidence hash
- target hash
- solution-class count
- observational-equivalence summary
- minimum light/sample clearance diagnostic
- handheld information-load metrics
- repetition-signature vector defined below

## 3.1 Canonical vs derived authority
Canonical truth is: geometry + legal states + target + campaign metadata.

Derived and disposable data:
- per-state light/surface incidence masks;
- state equivalence partitions;
- exhaustive solution lists/classes;
- route verification traces;
- diagnostics and preview thumbnails.

Derived data may be cached for tools/runtime but can never override geometry. A cache mismatch means **cache invalid**, never “geometry should be interpreted to match cache.”

---

# 4. Mutation and invalidation rules

Any change to one of the following invalidates **all** incidence, equivalence, solution and human-route certification caches for the case:
- light coordinate;
- surface endpoint/sample parameter;
- blocker polygon/archetype version;
- socket coordinate;
- legal blocker state transform;
- explicit joint legality relation.

A target-only change invalidates:
- solution classes;
- human-route certification;
- repetition signature fields that depend on target composition;
- tutorial/estimated-time approval.

Cosmetic-only changes do **not** invalidate logic if they preserve the same canonical ids and geometry. However, a cosmetic change still triggers visual readability review if it affects silhouette, target glyph legibility, contrast or camera framing.

A case may never ship with an author manually acknowledging a stale hash. Re-certification is mandatory.

---

# 5. Blocker reuse and visual multiplication ceiling

## 5.1 Logical reuse
The 24-case floor should use the same 8-archetype library repeatedly. Target distribution:
- each core archetype appears in at least 4 cases;
- no archetype appears in more than roughly 14 floor cases unless repetition review explicitly approves it;
- cases should change the *relation* between an archetype, lights and surfaces more often than they change the archetype itself.

## 5.2 Cosmetic variation
Allowed without logical change:
- material family;
- studio-table finish;
- non-semantic decal/engraving;
- socket trim;
- background wall treatment;
- ambient environment dressing;
- subtle surface-frame shape.

Forbidden cosmetic variation when it becomes semantic:
- one material implying a different opacity rule;
- color implying light-channel identity without redundant encoding;
- decorative silhouette protrusions that visually disagree with logical footprint;
- animation deformation that changes apparent occluding extent.

## 5.3 Asset ceiling
Launch presentation target:
- <=10 logical blocker archetype meshes;
- <=4 material/theme sets;
- <=3 surface/frame themes;
- <=3 table/studio environment sets;
- shared light fixtures and socket language.

A case must not require a bespoke environment, sculpture or animation to be understandable or marketable.

---

# 6. Campaign architecture — exact 24-case floor

The table below is a content specification, not finished level coordinates. Counts are targets/ceilings for authored geometry.

| Case | Band | Blockers / states | Surfaces / samples | Primary route | Purpose |
|---|---|---|---|---|---|
| NC01 | TEACH | 2 x2 | 1 / 4 | PROTECTED_LIT | Rotate one blocker; discover that bright target cells are hard exclusions. |
| NC02 | TEACH | 2 x2 | 1 / 5 | PROTECTED_LIT -> UNIQUE_PRODUCER | First required shadow after protected pruning. |
| NC03 | TEACH | 2 x2 | 1 / 5 | CHANNEL_ATTRIBUTION | Introduce L1_ONLY vs L2_ONLY with redundant glyph/origin cue. |
| NC04 | EARLY | 3 x2 | 1 / 6 | BOTH_DECOMPOSITION -> PROTECTED_LIT | First BOTH requirement; one contribution per channel. |
| NC05 | EARLY | 3 x2 | 1 / 6 | ENDPOINT_EXTENT | Same shadow area, different boundary; endpoint matters. |
| NC06 | EARLY | 3 x2–3 | 1 / 7 | ENDPOINT_EXTENT -> CHANNEL_ATTRIBUTION | Combine extent with one exclusive channel. |
| NC07 | EARLY | 3 x2 | 2 / 4+4 | CROSS_SURFACE_EQUIVALENCE_SPLIT | First second surface. Two states identical on A, split on B. |
| NC08 | EARLY | 3 x3 | 2 / 5+4 | PROTECTED_LIT -> CROSS_SURFACE_SPLIT | Demo synthesis; second surface prevents local guessing. |
| NC09 | MID | 3 x3 | 2 / 5+5 | CHANNEL_ATTRIBUTION -> UNIQUE_PRODUCER -> ENDPOINT | First 3-step connected route. |
| NC10 | MID | 4 x2–3 | 2 / 6+5 | PROTECTED_LIT -> BOTH_DECOMPOSITION -> CROSS_SURFACE_SPLIT | Bright islands remove state classes before BOTH resolve. |
| NC11 | MID | 4 x3 | 2 / 6+6 | ENDPOINT -> CROSS_SURFACE_SPLIT -> CHANNEL | Equivalent-on-A blocker pair separated on B. |
| NC12 | MID | 4 x3 | 2 / 7+5 | PROTECTED_LIT -> ENDPOINT -> UNIQUE_PRODUCER | One blocker never directly forced until late chain. |
| NC13 | MID | 4 x3 | 2 / 6+6 | CHANNEL -> BOTH -> CROSS_SURFACE | Darkness amount looks same; channel cause is decisive. |
| NC14 | MID | 4 x3 | 2 / 7+6 | ENDPOINT -> CHANNEL -> UNIQUE_PRODUCER | Alternates geometric and causal deductions. |
| NC15 | MID | 4 x3 | 2 / 6+6 | CROSS_SURFACE -> PROTECTED_LIT -> BOTH | Begin with equivalence classes, not individual states. |
| NC16 | MID | 4 x3 | 2 / 7+7 | PROTECTED_LIT -> CROSS_SURFACE -> CHANNEL | Group capstone; no residual search before 3 connected eliminations. |
| NC17 | LATE | 4 x3–4 | 3 / 5+5+4 | ENDPOINT -> CROSS_SURFACE -> CHANNEL | First third surface; low samples keep information load bounded. |
| NC18 | LATE | 5 x3 | 2 / 7+7 | PROTECTED_LIT -> BOTH -> UNIQUE_PRODUCER -> CROSS_SURFACE | Five blockers only after route proves class-level pruning. |
| NC19 | LATE | 4 x4 | 3 / 5+5+5 | CROSS_SURFACE -> ENDPOINT -> CHANNEL | Four states acceptable because surfaces partition them quickly. |
| NC20 | LATE | 5 x3 | 3 / 5+6+4 | PROTECTED_LIT -> CROSS_SURFACE -> BOTH -> ENDPOINT | Three-surface chain, not more samples. |
| NC21 | LATE | 5 x3 | 2 / 8+7 | ENDPOINT -> CHANNEL -> CROSS_SURFACE -> UNIQUE_PRODUCER | Dense two-surface synthesis with large cells. |
| NC22 | LATE | 5 x3 | 3 / 6+5+5 | PROTECTED_LIT -> ENDPOINT -> BOTH -> CROSS_SURFACE | Intended route touches all main families. |
| NC23 | CAPSTONE | 5 x3–4 | 3 / 6+6+5 | CROSS_SURFACE -> PROTECTED_LIT -> ENDPOINT -> CHANNEL -> BOTH | Penultimate full synthesis; residual assignment <=2 class choices. |
| NC24 | CAPSTONE | 5 x4 max | 3 / 6+6+6 | PROTECTED_LIT -> CROSS_SURFACE -> ENDPOINT -> CHANNEL -> UNIQUE_PRODUCER/BOTH | Final proof case; >=4 connected eliminations before residual choice. |

## 6.1 Why the 24-case floor is viable
The campaign uses the Phase-4 maxima sparingly:
- 6 blockers are never required by the floor skeleton;
- 12 samples/surface are never approached;
- three surfaces appear only at NC17+;
- 4-state blockers are rare and late;
- difficulty growth comes primarily from equivalence classes and interleaved deductions.

Therefore the campaign does not depend on raw Cartesian inflation.

---

# 7. Demo architecture

Frozen demo subset: **NC01–NC08**, target 20–30 minutes for first-time players.

Required beats:
1. NC01 — immediate rotate -> visible projection -> protected-light insight.
2. NC02 — first deduction where target darkness has a unique remaining producer.
3. NC03 — channel identity taught with glyph + line/origin treatment, never hue alone.
4. NC04 — BOTH decomposition.
5. NC05 — boundary/extent aha.
6. NC06 — short synthesis proving the idea is deduction, not silhouette matching.
7. NC07 — **second-surface reveal**, target by roughly minute 15–22 in median play.
8. NC08 — demo capstone requiring the player to use surface B to resolve ambiguity on A.

The demo must end on a complete satisfying solve, not a cliffhanger. It may then show a restrained campaign preview containing later three-surface imagery without adding mechanics in the demo build.

Demo completion data may later carry into full game; persistence details belong to Phase 8.

---

# 8. Optional cases 25–30

Cases NC25–NC30 are **not part of the shipping floor** and must never be used to excuse a weak floor case.

Acceptable purposes:
- alternate late synthesis emphasizing a less-used deduction-family ordering;
- one or two aesthetically striking showcase geometries;
- challenge cases with accepted multiple physical solutions but one meaningful solution class;
- one accessibility-friendly late case with fewer objects but deeper equivalence reasoning.

Forbidden purposes:
- six-blocker brute-force challenges;
- 10–12 sample dense walls for difficulty alone;
- gimmick materials/powers;
- procedural filler;
- “expert” cases whose only challenge is no hint/overlay support.

If fewer than six pass, ship fewer. The product target is `24..30`, not exactly 30.

---

# 9. Authoring workflow

Every case follows this recoverable pipeline:

1. **Intent sentence** — write the desired human aha and primary deduction-family sequence before geometry.
2. **Geometry sketch** — place lights, surfaces, samples, sockets and archetypes using canonical geometry only.
3. **State derivation** — generate exact incidence for every blocker state against every light/sample.
4. **Geometry sanity** — reject grazing, indistinguishable rendering, collision dependence and useless/redundant states.
5. **Target construction** — normally choose a seed physical configuration and derive its semantic target; manual target editing is allowed only at semantic-cell level, never by editing incidence masks.
6. **Exhaustive certification** — enumerate legal state vectors; compute all target-valid physical solutions and observational solution classes.
7. **Human-route certification** — verify the intended class-elimination route against actual derived incidence.
8. **Unintended-solution review** — accept harmless same-class alternatives; rework solutions that bypass the intended central reasoning or create a materially easier route.
9. **Repetition review** — compare case signature to neighboring and global floor cases.
10. **Handheld/readability review** — verify target cells, blocker silhouettes, surface switching and channel encoding at required viewport constraints.
11. **Difficulty/pacing review** — play or simulate without author-only information; update band/position if necessary.
12. **Content acceptance** — freeze case revision + hashes. Any logical mutation returns to step 3.

Authoring is never “draw a desired mask and then fit decorative geometry around it.”

---

# 10. Repetition signature and diversity gates

Each case records a compact repetition signature:
- blocker count bucket;
- blocker-state-count histogram;
- surface count;
- total sample-count bucket;
- target-class proportions;
- primary deduction-family ordered sequence;
- number of meaningful pre-residual eliminations;
- first decisive family;
- cross-surface dependency count;
- number of blocker states equivalent on at least one surface but split globally;
- accepted solution-class count;
- archetype multiset.

Reject/reorder/rework when:
1. two adjacent non-teaching cases have the same first decisive family **and** near-identical family sequence with similar geometry load;
2. three cases in any 5-case window are solved mainly by the same single family;
3. a MID+ case has <3 dependency-connected meaningful eliminations before residual assignment;
4. a LATE/CAPSTONE case uses fewer than 3 meaningful families unless a deliberately unusual deep single-rule proof is documented and adversarially approved later;
5. the strongest route is “try blocker states until mismatch disappears” despite a formal human-route document;
6. a case differs from an earlier one mainly by adding one blocker or more samples;
7. repeated archetype/light/surface layout makes the silhouette composition feel visually duplicated.

Desired global floor distribution of **primary emphasis** (not exclusive use):
- protected LIT: 4–6 cases;
- endpoint/extent: 4–6;
- channel/BOTH attribution: 5–7;
- cross-surface splitting: 5–7;
- synthesis/capstone: 5–7.

Because cases can count toward several families, this is a diversity target rather than a partition.

---

# 11. Human-route acceptance metrics

## TEACH
- may have 1 meaningful deduction;
- intended route <=3 conceptual steps;
- target concept should be inferable without external notes.

## EARLY
- >=2 meaningful eliminations preferred by NC06+;
- no more than 3 blockers x3 states in normal progression;
- second-surface tutorial must make the same-blocker coupling obvious.

## MID
- mandatory >=3 dependency-connected meaningful class eliminations;
- at least 2 distinct counting families;
- residual assignment must not begin while more than roughly 3 meaningful global classes remain.

## LATE
- mandatory >=3, preferred >=4 meaningful eliminations;
- preferred >=3 families;
- at least one deduction must operate on a blocker-state **class** or cross-surface consequence, not isolated target-cell correction.

## CAPSTONE
- >=4 meaningful connected eliminations before residual assignment;
- >=3 families;
- must recombine established rules only;
- no new tutorial concept;
- intended human path should be explainable afterward in <=8 short reasoning statements.

These are authoring gates, not player-facing scoring.

---

# 12. Unintended solutions and alternate routes

Multiple physical solutions are not automatically bad.

Accept when:
- differences are observationally equivalent;
- alternate configurations still require substantially the intended deduction structure;
- symmetry produces equally legible equivalent poses and the game accepts all.

Rework when:
- an alternate solution bypasses two or more core intended eliminations;
- one blocker can be ignored entirely despite the case presenting it as meaningful;
- a target-valid solution depends on a visually ambiguous grazing state;
- a simpler route converts a MID/LATE case into independent local fixes;
- legal-state collision accidentally removes most of the search space.

Certifier output should distinguish `solution_count_physical` from `solution_count_observational_classes`.

---

# 13. Handheld information-load gate

Content Architecture fixes logical load before Phase 6 decides exact screen composition.

For shipping floor:
- recommended simultaneous visible target samples across all surfaces: <=18 early/mid, <=20 late, <=22 capstone only if Phase-6 presentation proves readable;
- no single surface above 8 floor samples in the current skeleton;
- third surfaces use 4–6 samples initially, not dense walls;
- blockers <=5 in the 24-case floor;
- every blocker has a visually distinct selection marker/socket id independent of material color;
- channel semantics require shape/glyph redundancy.

A case that needs a zoomed spreadsheet-like target view to reason is rejected even if technically valid.

---

# 14. Unlock flags and floor semantics

Case fields:
- `required_for_floor = true` for NC01–NC24;
- optional NC25–NC30 use `required_for_floor = false`;
- `capstone = true` for NC23/NC24; optional challenge cases do not substitute for capstones.

Group progression:
- G1: NC01–03
- G2: NC04–06
- G3: NC07–09
- G4: NC10–12
- G5: NC13–15
- G6: NC16–18
- G7: NC19–21
- G8: NC22–24

Unlock next group after any 2 completions in current group. NC24 unlocks only with G8; the final campaign-complete state requires all 24 floor cases, but credits/ending presentation may be shown after NC24 plus a configurable near-complete threshold in Phase 7 if commercial/retention design finds that preferable. Mechanical completion truth remains per-case.

---

# 15. Expansion / DLC boundary

Launch is a finite premium game, not live service.

A later expansion may add:
- new authored cases using the exact frozen projection rule;
- new blocker archetype silhouettes whose states remain ordinary opaque rigid transforms;
- new cosmetic studio/table/surface themes;
- optional challenge groups.

A later product expansion **must reopen design** rather than silently count as content if it adds:
- third logical light channel;
- transparency/material rules;
- movable lights;
- mirrors/refraction;
- dynamic surfaces;
- timed movement;
- blocker powers;
- player-created arbitrary masks.

Those are mechanics, not content.

No procedural infinite generation is assumed. Tool-assisted candidate generation is acceptable internally only if every shipping case passes the same human-route and readability review as hand-authored cases.

---

# 16. Phase-5 acceptance checklist

Phase 5 passes because:
- 24 floor cases have a concrete progression skeleton;
- floor difficulty stays below mechanical maxima rather than leaning on them;
- second surface arrives inside the demo;
- third surface arrives only after established two-surface mastery;
- blocker asset growth is capped and reuse is explicit;
- full case schema separates canonical geometry from disposable derived caches;
- every logical mutation has deterministic invalidation rules;
- authoring pipeline includes exhaustive solution certification **and** human-route certification;
- repetition has measurable rejection gates;
- handheld information load has content-level ceilings;
- optional cases and later expansion cannot dilute the shipping floor or smuggle in new mechanics.

**PHASE 5 VERDICT: PASS.**

`DESIGN COMPLETE = NO`.

## NEXT ACTION — PHASE 6 UX / PRESENTATION ARCHITECTURE
Define the complete player-facing interaction and presentation system without changing mechanics:
1. camera/table/surface layout and how 1/2/3 surfaces remain readable on a handheld-sized viewport;
2. keyboard/mouse + controller input abstraction, focus order and direct blocker-state manipulation without precision aiming;
3. target-cell visual language for LIT/L1_ONLY/L2_ONLY/BOTH with non-color redundant encoding;
4. current-state shadow presentation versus target overlay, selected-blocker contribution inspection and anti-oracle boundary;
5. first-session onboarding NC01–NC08, tutorial prompts, second-surface reveal and skip/revisit behavior;
6. HUD, case browser/group unlock presentation, completion/mismatch feedback, undo/redo/reset/commit and pause/settings flows;
7. accessibility: color vision, text size, contrast, motion, input remap, hold/toggle, audio independence and photosensitivity-safe presentation;
8. audio/visual feedback language, animation timing and rules for decorative shadows vs canonical logical truth;
9. save/load/recovery expectations at UX level, including mid-case resume and reset semantics (technical persistence later);
10. define screenshots/GIF/trailer-readability gates and first 20–30 minute experience acceptance criteria;
11. create `GAME14_UX_PRESENTATION.md`, update `STATUS.md` and `GAME_INDEX.md`, and proceed to Phase 7 only if three-surface late cases remain readable without solver-like overlays.

Do not start production implementation. Do not introduce mirrors, moving actors/flats, special blockers or rejected tournament mechanics.