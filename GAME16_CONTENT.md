# GAME #016 — PHASE 5 CONTENT ARCHITECTURE

Date: 2026-09-03
Status: PHASE 5 COMPLETE
Working title: **ONE-WAY WORKSHOP**
Authority: `GAME16_MECHANICS.md` and prior active Game #016 authorities.

## 0. Content objective
Turn the frozen Phase-4 grammar into an exact 24-case premium puzzle campaign without adding mechanics. Every canonical case must be authorable from existing `SPAN`, `EDGE`, `FACE`, visible `PAIR`, `HOLE`, `MARK`, `SPACING`, `ANGLE`, deterministic two-child cuts, one-jig guided operations, reversible docking, certification and restart.

Canonical campaign = **24 authored cases, six reasoning families × four cases**. Optional variants may remix already-authored job data, but they do not count toward the canonical 24 and cannot introduce new capabilities, operations, assets or progression gates.

---

# 1. Six reasoning families — locked
The Round-C family sketch survives Phase 5, but each family is defined by a distinct proof sentence rather than theme.

## Family I — Immediate Byproduct (OW01–OW04)
**Proof sentence:** “The child that looks like waste after this cut is exactly the jig needed by the next visible operation.”
Purpose: establish the thesis with dependency distance 1 and almost no bookkeeping.

Progression:
1. one forced spacer byproduct;
2. choose between two cut sockets where only one leaves both valid part + next jig;
3. largest-offcut heuristic explicitly loses;
4. one offcut can dock in two visible stations, but only one matches the mandatory next operation.

## Family II — Property Choice (OW05–OW08)
**Proof sentence:** “I must choose which physical property survives the cut, not which child is biggest.”
Purpose: teach capability discrimination across `SPAN`, `EDGE`, `FACE` and first visible `PAIR` use.

Progression:
1. `SPAN` vs `EDGE` conflict;
2. `FACE(NOTCHED)` vs larger flat child;
3. `DIAGONAL_A` vs `DIAGONAL_B` angle-template choice;
4. visible paired siblings: a matched-pair requirement competes with a tempting independent part cut.

## Family III — Delayed Lineage (OW09–OW12)
**Proof sentence:** “A child created now must stay useful for a requirement several commits later.”
Purpose: move from local usefulness to dependency-distance planning while keeping one or two stocks.

Progression:
1. preserve a spacer for two commits;
2. preserve a straight-edge jig across an unrelated guided operation;
3. product-first route destroys a future producer;
4. one delayed child must first be used temporarily as jig, then released and later become a part.

## Family IV — Cross-Blank Ancestry (OW13–OW16)
**Proof sentence:** “The correct cut on stock B is determined by what stock A will need later.”
Purpose: introduce genuine multi-root planning, never secret root identity.

Progression:
1. stock B supplies jig for stock A;
2. two-way crossing: A produces a jig for B, B later produces a jig for A;
3. three roots but only one meaningful crossing pair;
4. two crossings across three roots with one alternative valid solution family.

## Family V — Dual-Use Conflict (OW17–OW20)
**Proof sentence:** “This one child can solve more than one future problem, but it cannot be in both places or survive both uses.”
Purpose: attack hoarding and universal-jig play through occupation/consumption, not inventory punishment.

Progression:
1. one jig fits two stations but must be sequenced;
2. temporary occupancy blocks another required use until released;
3. one operation consumes a dual-compatible child, forcing which requirement gets it;
4. two valid solution families allocate scarce capabilities differently.

## Family VI — Derived Witness Relay (OW21–OW24)
**Proof sentence:** “The tool I need does not exist yet; I must create a child, upgrade it once with a guided witness, then use it elsewhere.”
Purpose: late-game second-order capability chains using existing witnesses, with no universal-tool accumulation.

Progression:
1. create `MARK`ed template then use it once;
2. create `HOLE` or `SPACING` witness on a future jig;
3. combine cross-stock ancestry with one derived-witness relay;
4. capstone: three roots, six commits, two cross-piece witness dependencies, no same-piece witness depth >1.

**Distinctness gate:** these families are retained because their human proof objects differ: immediate consequence / property preservation / time-delayed preservation / cross-root dependency / allocation conflict / capability creation. If playtests collapse two families into the same verbal reasoning, cases are rewritten inside the family before any new mechanic is added.

---

# 2. Capability and witness introduction cadence
No capability exists merely because a later case needs complexity. Introduction is monotonic and front-loaded enough that late cases compose known ideas.

| Case | New player-facing concept introduced |
|---|---|
| OW01 | `SPAN`; exact two-child cut; byproduct docks as spacer; guided operation; certify/restart |
| OW02 | two cut sockets; preview both child outcomes |
| OW03 | size heuristic fails; same `SPAN` bands used in conflicting roles |
| OW04 | one child compatible with multiple visible stations; station-specific need |
| OW05 | `EDGE(STRAIGHT)` as jig property |
| OW06 | `FACE(NOTCHED)` seating requirement |
| OW07 | `EDGE(DIAGONAL_A/B)` and resulting `ANGLE(A/B)` witness |
| OW08 | visible `PAIR(token)` matched siblings; no secret ancestry |
| OW09 | dependency distance >1; preserved loose child |
| OW10 | temporary jig use and later reuse after release |
| OW11 | first explicit “product-first is wrong” case |
| OW12 | one byproduct changes role jig → released → part |
| OW13 | two-root cross-blank dependency |
| OW14 | two-way cross-blank dependency |
| OW15 | three initial stocks, still <=5 intended commits |
| OW16 | first planned alternative solution family in a cross-blank case |
| OW17 | dual station compatibility as allocation problem |
| OW18 | temporary occupancy conflict |
| OW19 | consume-on-operation conflict |
| OW20 | two solution families with different scarce-child allocation |
| OW21 | `MARK(reference)` created on a future jig |
| OW22 | `HOLE(pattern)` or `SPACING(band)` created on a future jig |
| OW23 | derived witness relay crosses stock roots |
| OW24 | full composition: three roots, six commits, witness relay + dual-use pressure |

`HOLE` may appear earlier as a **final-part witness** in OW01/tutorial certification, because the player need only understand “this operation drilled the part.” Its use as a **future jig qualification** is deliberately held until OW22. `SPACING` likewise may appear as an operation result earlier but does not act as a second-order qualification until Family VI. `MARK` is introduced as a qualification at OW21. `ANGLE` first appears in OW07 because diagonal template logic is still direct and visually legible.

---

# 3. Exact 24-case campaign matrix
Expected solve time excludes first-load/tutorial reading but includes normal restart behavior.

| ID | Family / teaching goal | Stocks | Max commits | Key dependency distance | Main conflict | Intended human proof | Dominant-strategy trap | Validation burden | Solve target |
|---|---|---:|---:|---:|---|---|---|---|---|
| OW01 **Keep the Spacer** | I / thesis tutorial | 1 | 2 | 1 | rail span vs spacer span | “The 2+4 cut is the only split that leaves both the 4+ part and the 2 jig.” | biggest child alone | Low | 3–5m |
| OW02 **Two Useful Halves** | I / compare previews | 1 | 2 | 1 | two plausible cuts | “Only one cut gives a valid part and the exact next jig.” | choose visually centered cut | Low | 4–6m |
| OW03 **Small Wins** | I / kill largest-offcut rule | 1 | 3 | 1 | small keyed spacer vs large flat waste | “The smaller child has the needed fit property.” | preserve largest offcut | Low | 5–7m |
| OW04 **Right Tool, Wrong Job** | I / station-specific compatibility | 1 | 3 | 1 | one child seats in two stations | “The next mandatory station fixes which use matters first.” | use first compatible station | Medium | 5–7m |
| OW05 **Reference Edge** | II / `EDGE(STRAIGHT)` | 1 | 3 | 1 | long part vs straight guide | “The shorter child carries the straight edge I need.” | maximize `SPAN` | Medium | 6–8m |
| OW06 **Notched Seat** | II / `FACE(NOTCHED)` | 1 | 3 | 1 | larger flat child vs smaller keyed child | “Only the notch can physically seat in the jig.” | largest / prettiest part | Low–Med | 6–8m |
| OW07 **Angle Choice** | II / diagonal A/B | 2 | 4 | 1–2 | angle template choice vs valid brace stock | “The final brace calls for A, so I must preserve an A edge now.” | any diagonal is equivalent | Medium | 7–10m |
| OW08 **Matched Offcuts** | II / visible `PAIR` | 2 | 4 | 2 | paired siblings vs independent larger pieces | “The plan visibly needs the two matching siblings from one paired cut.” | secret-identity guessing; prevented by visible interface | High | 8–11m |
| OW09 **Save It for Later** | III / dependency 2 | 1 | 4 | 2 | useful byproduct competes with immediate convenience | “This spacer is not for now; the plan shows a later station only it can satisfy.” | consume usefulness immediately | Medium | 7–10m |
| OW10 **Borrowed Straightedge** | III / temporary jig reuse | 2 | 4 | 2–3 | use now vs preserve after release | “I can use this edge now because the station releases it for the later job.” | assume all use consumes | Medium | 8–11m |
| OW11 **Wrong Side First** | III / product-first defeat | 2 | 5 | 3 | direct product cut destroys jig ancestry | “Future angle/spacer needs force the upstream cut before the obvious part.” | make product parts first | High | 10–13m |
| OW12 **Tool Becomes Part** | III / role transition | 2 | 5 | 3 | temporary jig later required as final cap/brace | “Use it without consuming it, then release it into the product.” | permanently categorize child as tool or part | High | 10–14m |
| OW13 **Across the Bench** | IV / first cross-blank | 2 | 4 | 2 | B cut determined by A station | “A cannot be finished unless B leaves this jig.” | solve each stock independently | Medium | 8–11m |
| OW14 **Crossed Favors** | IV / two-way dependency | 2 | 5 | 3 | A→B jig then B→A jig | “Each blank’s correct branch is justified by the other blank’s later station.” | finish one stock completely first | High | 10–14m |
| OW15 **Three Blanks, One Chain** | IV / three roots | 3 | 5 | 3 | one root supplies product, one tool, one intermediary | “The final requirements form one chain across all three roots.” | treat third stock as spare material | High | 11–15m |
| OW16 **Two Ways Across** | IV / alternate families | 3 | 5 | 3 | two different cross-root allocations | “Either A supplies the spacer and B the edge, or vice versa; both preserve the same final needs.” | assume hidden canonical route | Very High | 12–16m |
| OW17 **One Jig, Two Places** | V / dual compatibility | 2 | 4 | 2 | same child fits station X and Y | “Do the releasing use first; the consuming/locking use second.” | first-fit greed | Medium | 9–12m |
| OW18 **Occupied** | V / temporary occupancy | 2 | 5 | 2–3 | current docking makes child unavailable elsewhere | “The order matters because the jig is physically occupied until this operation releases it.” | hoard-by-docking everything | High | 10–14m |
| OW19 **Spend the Tool** | V / consumption conflict | 3 | 5 | 3 | unique child can satisfy two stations, one consumes | “A substitute exists for one station, so save the unique child for the consuming requirement.” | use best universal jig everywhere | High | 12–16m |
| OW20 **Split Decision** | V / multiple valid allocations | 3 | 6 | 3 | two scarce compatible children, two different allocation plans | “Choose one consistent allocation; both can certify.” | search for single intended answer | Very High | 13–18m |
| OW21 **Mark the Template** | VI / first derived qualification | 2 | 5 | 3 | jig must first receive `MARK` | “I am making the future tool now, not modifying the final part.” | target witness operation at product | High | 11–15m |
| OW22 **Drilled Guide** | VI / second derived-witness form | 2 | 5 | 3–4 | child needs `HOLE`/`SPACING` before later station | “This child’s shape is necessary but insufficient until I prepare it.” | choose shape-only compatibility | High | 12–16m |
| OW23 **Relay Across Roots** | VI / witness + cross-blank | 3 | 6 | 4 | root A prepares tool from B that operates on C | “A’s byproduct is needed only to upgrade B, and upgraded B is what C needs.” | solve roots independently / product first | Very High | 14–19m |
| OW24 **Witness Relay** | VI / campaign capstone | 3 | 6 | 4 | notched prep jig → marked straight template → drilled beam; diagonal template → brace | “P2 forces the marked straight template; that forces the notched producer; brace requirement separately forces diagonal A.” | largest, product-first, universal-jig, branch enumeration | Extreme | 16–20m |

OW24 uses the repaired Phase-4 three-root `Witness Relay` structure as its canonical mechanical seed; exact geometry may be tuned during authoring only if all proof relationships and ceilings remain intact.

---

# 4. Demo contract — 20–30 minutes
The demo is **not** simply OW01–OW06 in order, because six full campaign cases would likely exceed the time target and end before the cross-blank thesis becomes visible.

Canonical demo subset:
1. **OW01 Keep the Spacer** — 3–5m;
2. **OW03 Small Wins** — 5–7m;
3. **OW05 Reference Edge** — 6–8m;
4. **Demo Capstone D1 — curated compression of OW13 mechanics** — 8–10m.

D1 is not a 25th canonical campaign case. It reuses OW13 data/assets in a reduced demo configuration: two stocks, one cross-blank jig dependency, max four commits, no mechanic later than OW13. The full game may map demo completion to OW01/03/05 tutorial-clear flags plus a separate `demo_capstone_seen` flag; Phase 7/8 will specify progression import.

Knowledge progression:
- OW01: byproduct is future tool;
- OW03: useful property beats size;
- OW05: property is more than raw span;
- D1: another stock’s cut can be chosen for a future dependency.

Demo completion sentence should be naturally expressible as: **“I cut that blank that way because the leftover became the guide another part needed later.”**

Do not include `PAIR`, dual-use consumption or derived-witness relay in the demo; the demo proves the identity without exhausting late progression.

Target cold-player median: 24–28 minutes. If playtest median exceeds 30 minutes, shorten D1 or OW05 presentation before deleting the cross-blank capstone.

---

# 5. Reusable visual/content kit and bespoke burden
The game must look tactile without requiring 24 bespoke workshop scenes.

## 5.1 Stock geometry kit
Author from a reusable library of approximately **12 root geometry archetypes**:
- straight strip narrow/wide;
- rectangular plank short/long;
- keyed/notched strip;
- wedge blank A/B;
- paired-notch blank;
- plate short/long;
- forked end blank;
- stepped strip;
- simple L-profile/tokenized keyed face.

Each archetype supports authored cut-socket variants; geometry variants may resize/stretch only along declared safe axes. Phase 5 content may create new **instances**, not new mechanical categories.

Target unique child silhouettes across campaign: <=45 reusable geometry tokens. Many cases should reuse silhouettes with different cut socket placement/capability context.

## 5.2 Jig/station kit
Maximum reusable station archetypes: **8**:
1. span spacer cradle;
2. straight-edge fence;
3. diagonal-A template cradle;
4. diagonal-B template cradle;
5. flat/notched seating fixture;
6. guided drill fixture;
7. guided mark fixture;
8. guided spacing/assembly stop.

A station may skin its target silhouette to the current product, but logical affordance must remain visually consistent.

## 5.3 Final-product visual families
Use **6 product silhouette families × 4 cases** rather than 24 unrelated props:
1. small shelf/bracket assemblies;
2. frame/latch assemblies;
3. stands/feet/support shapes;
4. desk organizers/tool holders;
5. compact mechanical toys/fixtures;
6. late composite workshop objects.

These are presentation families only. They cannot introduce physics or one-off functional predicates.

## 5.4 Bespoke burden ceilings
Across 24 cases:
- <=12 root stock archetypes;
- <=45 logical child geometry tokens;
- <=8 station archetypes;
- <=6 final-product visual families;
- <=24 unique product silhouettes, one per canonical case, but each assembled from reusable style modules;
- <=2 new decorative prop modules per family;
- no bespoke animated machine beyond reusable cut, drill, mark, spacing, dock and certify rigs.

If a case needs a unique machine animation to explain its rule, the case is invalid content rather than justification for scope growth.

---

# 6. Exact data-driven authoring schema
Each canonical job is a declarative record. Implementation representation may differ, but these logical fields are mandatory.

```text
JobDefinition
  id
  family_id
  ordinal
  title_key
  teaching_goal
  expected_solve_time_band
  difficulty_vector
  initial_stocks[]
  cut_sockets[]
  part_slots[]
  jig_stations[]
  operations[]
  certification_requirements[]
  presentation_refs
  tutorial_prompts[]
  reference_solution_families[]   # validation only; never runtime truth
  proof_sentences[]               # authoring/QA expected deductions
  intended_wrong_branches[]
  demo_flags
  validation_expectations
```

`initial_stocks[]` fields:
`stock_id, geometry_token, base_capabilities, initial_pose, cuttable, presentation_material`.

`cut_sockets[]` fields:
`socket_id, parent_geometry_token, family, visible_transform, child_a_geometry, child_b_geometry, capability_derivation, optional_prerequisite`.

`jig_stations[]` fields:
`station_id, requirement_predicate, occupancy_mode, operation_ids, physical_fit_ref, tutorial_visibility`.

`operations[]` fields:
`operation_id, effect_family, target_predicate, required_station, prerequisites, deterministic_effect, jig_release_or_consume, commit_cost=1`.

`validation_expectations` must include:
- expected min/max solution commits;
- expected solution-family count range;
- reachable-meaningful-state ceiling;
- max loose children;
- first-choice elimination ratio target;
- max contradiction distance for listed wrong branches;
- empirical gates exercised.

No runtime rule may read `reference_solution_families` or `proof_sentences` to decide success.

---

# 7. Authoring and validation pipeline
Every case moves through the same recoverable pipeline.

## Input
Declarative `JobDefinition` + shared geometry/capability/station library.

## Build-time checks
1. schema/reference integrity;
2. every capability/witness belongs to frozen grammar;
3. every cut has exactly two deterministic children;
4. station predicates are visibly representable;
5. stock/commit/socket/loose-child ceilings;
6. no hidden identity predicate outside visible `PAIR`;
7. same-piece witness upgrade <=1 and cross-piece relay depth <=2.

## Exhaustive mechanical enumeration
A design-time solver enumerates all reachable canonical mechanical states after symmetry/cosmetic-state normalization. It records:
- total reachable meaningful states;
- all certification-success states;
- min/max successful commit counts;
- distinct solution families by semantic commit lineage;
- dead states;
- wrong-branch contradiction distance;
- station/capability usage frequencies.

**Acceptance target:** <=64 reachable meaningful states. If a case exceeds 64, author simplifies sockets/operations. A Phase-8 implementation may refine state-equivalence accounting, but Phase 5 does not grant silent exceptions.

## Runtime dead-state regression
For every enumerated reachable state:
- compare optimistic runtime detector result with exact solver truth;
- **zero false positives required**;
- false negatives allowed but tracked;
- if a false positive occurs, detector logic or case authoring must change before shipping.

## Solution/proof checks
- every reference solution must certify;
- every solver-discovered valid solution must certify, even if not authored;
- no hidden canonical sequence assumption;
- mid/late cases must expose >=1 necessity eliminating >=50% of plausible first destructive choices;
- authored proof sentence must refer only to visible requirements/capabilities;
- intended wrong strategic branches should contradict within 1–3 later commits where practical.

## Content-global checks
- no capability combination satisfies >50% of jig stations unless explicitly tutorial-only;
- each family produces distinct proof-sentence distribution;
- no stock archetype becomes an implicit “always choose me” answer;
- no first-cut socket is correct >60% of times within a four-case family merely by screen position/size convention;
- angle A/B, notched/flat and small/large visual coding are counterbalanced so visual salience alone cannot become a meta-solver.

Outputs: validation report per case + campaign summary + failing-state traces suitable for content revision.

---

# 8. Content reuse rules
1. Reuse geometry aggressively; vary dependency context rather than inventing shapes.
2. Reusing a stock archetype is desirable if a prior obvious heuristic now fails for a new visible reason.
3. No case may depend on remembering an unshown rule from an earlier case; all required station/plan information is visible in the current job.
4. Tutorial prompts may fade, but affordances never become hidden.
5. A new case must add a new deduction relationship or compose known ones; “same puzzle, more sockets” is filler and invalid.
6. Final-product art is flavor; certification logic must remain expressible through PartSlots/witnesses/operations already in the schema.
7. Optional challenge variants may change stock/cut availability, alternate required product skin, or remove nonessential tutorial overlays **only if** the same frozen mechanic grammar is used and exhaustive validation passes.
8. Optional variants do not unlock canonical progression, do not increase the advertised 24-case baseline, and do not justify a new asset family.
9. No procedural/random canonical case generation. Deterministic authored data is baseline.
10. No daily puzzle, Workshop/editor, score medals, par cuts or time trials in Phase 5. Those are not canonical content and may only be reconsidered in Phase 7 without changing the core game.

---

# 9. Tutorialization rules
- Teach by physical consequence before terminology.
- At first appearance of a station family, show one forced compatible piece and one visibly incompatible piece before adding choice complexity.
- First use of a new capability/witness cannot also be the first use of cross-blank planning or consumption conflict.
- Player-facing text names purpose (“fits the narrow spacer cradle”, “matches angle A”) rather than formal tokens (`SPAN`, `EDGE`).
- After OW08, no mandatory modal tutorial text for previously learned capability families.
- Later cases may show a short plan highlight when a requirement is selected, but may not enumerate future solution steps.
- If a player repeatedly certifies with one missing requirement, the certifier may escalate the causal trace; actual hint progression belongs to Phase 6/7.

---

# 10. Production and QA burden estimate
## Authoring burden
Expected per canonical case after toolchain exists:
- early cases: ~0.5–1 design-day each;
- mid cases: ~1–2 design-days each;
- late cases: ~2–4 design-days each due solver/proof tuning;
- final three cases: potentially 3–5 design-days each.

Rough content-design total: **35–55 designer-days** including iteration, excluding engine/tool implementation and art polish. This is a planning estimate, not schedule commitment.

## Validation burden hotspots
Most likely to violate <=64-state / anti-enumeration constraints:
1. **OW16** — alternative cross-blank solution families can multiply semantic states;
2. **OW20** — scarce dual-use allocation with two valid families;
3. **OW23** — witness relay plus cross-root ancestry;
4. **OW24** — six-commit capstone at all ceilings.

Secondary hotspot: OW08 because `PAIR` must remain visible and not become hidden genealogy.

Mitigation order: reduce cut sockets → remove redundant reversible docking variants from meaningful-state accounting → simplify optional operation ordering → reduce alternate solution families. Never add hidden restrictions merely to shrink the solver graph.

## QA matrix minimum
Every canonical case receives automated exhaustive validation plus human checks for:
- cold-read first-cut reasoning;
- physical station legibility;
- child-role readability;
- commit permanence comprehension;
- failure trace usefulness;
- restart flow;
- controller navigation through all relevant pieces/stations.

Late cases additionally require human replay by testers who did not author them; passing solver validation alone does not prove deduction quality.

---

# 11. Phase-5 empirical validation matrix
Legend: P = primary test case, S = supporting test case.

| Empirical gate | Cases |
|---|---|
| 1. Cut tactility | P: OW01, OW03; S: all |
| 2. Lineage readability at high complexity | P: OW23, OW24; S: OW15, OW20 |
| 3. Shape-first station matching | P: OW05, OW06, OW07; S: OW17–OW24 |
| 4. Irreversible commit comprehension | P: OW01, OW02; S: OW11, OW24 |
| 5. Reasoning over enumeration | P: OW11, OW14, OW19, OW23, OW24; S: all mid/late |
| 6. Restart friction | P: OW03, OW11, OW24; S: all |
| 7. Universal-tool non-dominance | P: OW17–OW20; campaign-global solver check |
| 8. Reasoning-family distinctness | P: OW04, OW08, OW12, OW16, OW20, OW24 as family endpoints |
| Product-first heuristic defeated | P: OW11, OW14, OW23 |
| Largest-offcut heuristic defeated | P: OW03, OW05, OW19 |
| Hoarding not a solver | P: OW18–OW20 |
| Cross-stock readability | P: OW13, OW14, D1 demo capstone |
| Derived witness comprehension | P: OW21, OW22; stress: OW23, OW24 |
| Multiple-solution acceptance | P: OW16, OW20; solver-global |
| Zero-false-positive dead-state detector | exhaustive regression on all 24 |

Family endpoints OW04/08/12/16/20/24 form a six-case regression suite after any mechanic or UX change because together they cover the campaign’s distinct reasoning identities.

---

# 12. Canonical campaign pacing summary
- **OW01–OW04:** thesis learned; 1 stock; dependency distance 1.
- **OW05–OW08:** capability grammar becomes expressive; first 2-stock and `PAIR` case.
- **OW09–OW12:** time/delay becomes the puzzle object; product-first intuition is overturned.
- **OW13–OW16:** root-to-root reasoning; player stops solving each blank independently.
- **OW17–OW20:** resource allocation through occupancy/consumption; no new verb.
- **OW21–OW24:** create future capability via one witness upgrade; late composition reaches 3 stocks / 6 commits / distance 4 but does not exceed frozen ceilings.

No “boss puzzle” may exceed limits simply for spectacle. OW24 is difficult because dependencies compose, not because it is bigger than the game’s rules.

---

# 13. Phase-5 lock / handoff to Phase 6
Phase 5 passes the required gate: the entire 24-case campaign can be authored from Phase-4 mechanics without new capabilities, verbs, simultaneous-jig rules, hidden ancestry or continuous geometry. The six families remain meaningfully distinct by proof sentence.

Frozen downstream content contract:
- exactly 24 canonical authored cases;
- six families and four-case progression each as defined here;
- introduction cadence above;
- OW01–OW24 matrix and difficulty ceilings;
- demo subset OW01 + OW03 + OW05 + reduced OW13-derived D1 capstone;
- reusable stock/station/product asset ceilings;
- declarative authoring schema;
- exhaustive solver + dead-state zero-false-positive regression;
- content-global anti-meta checks;
- optional variants are non-canonical and cannot add mechanics;
- Phase-5 empirical gate matrix and risk hotspots.

**No production implementation was started.**

**NEXT:** Phase 6 UX / Presentation Architecture — define exact camera/input/controller paths, workbench layout, plan/requirement inspection, cut preview/commit affordance, child/lineage readability, station matching language, onboarding/tutorial UI, certifier/failure presentation, restart/pause/save interactions, accessibility, audio/visual feedback and first-session/demo experience against OW01–OW24. Do not reopen Phase 5 unless UX proves a content case cannot be expressed legibly under the frozen grammar.