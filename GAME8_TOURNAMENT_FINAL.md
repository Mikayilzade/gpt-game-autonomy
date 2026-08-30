# GAME #008 — CONCEPT TOURNAMENT FINAL

Last updated: 2026-08-30
Phase: **2 — FINAL**
Input: Locksmith's Margin / Window Garden / Firebreak Foreman
Output: **WINNER — G8C02 Locksmith's Margin**

This run follows the equal final gate in `STATUS.md`. No prior score grants protection.

## Fresh mechanic-level analogue check
Fresh searches were run for all three surfaces. No current result located a Steam game whose central grammar is destructively filing one persistent key to satisfy overlapping tolerance sets across several locks. That is not proof of uniqueness, but it preserves Locksmith's Margin's current differentiation hypothesis.

Window Garden's collision worsened materially: **Topiary: A Pruning Puzzle** appeared in current Steam metadata on 27 Aug 2026 and explicitly pitches pruning branches, awakened buds/forking, season growth and shaping a continuously growing plant. Alongside Prune/Cloud Gardens/Botany Manor, this makes pruning-driven plant geometry a crowded explanatory surface even though Window Garden's shutter/light scheduling differs.

Firebreak Foreman retains the previously identified Wildfire Swap collision and also suffers a naming/search-noise problem from FBC: Firebreak. The latter is mechanically unrelated, but it makes `Firebreak` a poor commercial title word and increases store/search ambiguity.

---

# 1. G8C02 LOCKSMITH'S MARGIN

## Eight exact blueprints
All use only: discrete key columns/depths, file-one-step, lock acceptance intervals, optional master interval, wear widening, visible first-blocking impression, test, finite blanks.

**L01 Training Cut** — 4 columns, one lock, one blank. Start [0,0,0,0], target singleton [1,0,2,1]. Tests reveal first blocking column. Teaches irreversible one-step filing and exact physical causality.

**L02 Stop Cutting** — 4 columns, two locks, two blanks. A accepts [1,1,2,1], B [1,1,1–2,1]. Player learns that opening A at depth 2 can still preserve B; success is compatibility, not visual perfection.

**L03 Siblings** — 5 columns, locks A/B/C, two blanks. A and B overlap on all columns only at one deliberately non-central vector; C requires one incompatible deeper column. Correct partition is shared A/B key + C key. No new primitive after this blueprint.

**L04 Greedy Scar** — 5 columns, 3 locks, 2 blanks. Strongest current impression on A suggests a deeper cut that opens A but destroys A/B overlap. Player must stop after a lighter mark and test B before committing.

**L05 Master Fork** — 5 columns. A has two valid depths at c3, B overlaps shallow branch, C overlaps deep branch elsewhere. Test order reveals which blank should remain shallow. Master interval is a parameter of the already visible accepted-set model, not a new verb.

**L06 Wear Bridge** — 6 columns. Service lock has one widened interval; cabinet lock is precise. The broad service tolerance permits a shared key if player refuses to `match` the worn lock's apparent center. Third lock consumes the other blank.

**L07 Diagnostic Life** — 6 columns, four locks, three blanks. One blank is intentionally kept non-opening through two tests because its first-blocking marks distinguish which family two later locks belong to; only after information is exhausted is it converted into an opening key.

**L08 Margin Finale** — 6 columns, five locks, three blanks. Two master intervals, one worn interval, fixed test access order. Required solution contains one exact specialist, one deliberately imperfect shared key and one diagnostic-then-converted key. Greedy deepest, shallowest-only, current-lock-first and one-key-per-lock all fail.

## Formal state / smallest solver state
Case static data: lock set `L`; for each lock/column accepted finite depth set `A[l,c]`; blank count; column count/depth max; allowed test-access relation/order.

Dynamic authoritative state: each blank vector `K[b,c]`; each blank's accumulated visible impression knowledge `I[b,l,c]` (none/light/strong or equivalently the authored feedback class required to reproduce player-visible information); which locks are opened; current test-access state; committed cut/test history only where needed for undo/replay, not solution equivalence.

Transition `FILE(b,c)`: legal iff `K[b,c] < Dmax`; increments exactly one. Never reversible inside puzzle authority except explicit restart/undo boundary defined later.

`TEST(b,l)`: evaluate columns in declared physical order; open iff every `K[b,c] ∈ A[l,c]`; otherwise expose the first incompatible column's deterministic feedback class and update I. No randomness/floating tolerance.

For solver search, smallest complete future-state key is `(K vectors, opened-lock bitset, access state, knowledge state if future legal decisions/access depend on revealed knowledge)`. Presentation/history are excluded. If access never depends on knowledge, I is not needed to determine solvability but remains needed to model information-respecting hint validation.

## Naked grammar
Remove locksmith fiction: **irreversibly edit a small set of vectors so each target acceptance-set is covered, while tests reveal partial constraint information and edited vectors persist across targets.** This remains a distinctive decision grammar.

Case 5 thought: `What does this failed fit tell me, and should I cut?`
Case 15: `Which targets can share a still-useful artifact, and when does information outweigh completion?`
Case 30: `How do I partition targets across artifacts while sequencing destructive information and preserving overlap branches?`

## 30-second trailer
0–4s: blank clamped; file removes one crisp notch step.
4–8: key enters cutaway lock; pins rise; one binds; bright impression appears on corresponding notch.
8–12: player starts to file, stops; pulls key away.
12–17: same scarred key enters second lock and turns — first `aha`.
17–22: bench reveals three locks/two blanks; rapid tests create two different marks.
22–27: one deliberate shallow cut; first and second lock both open with same key.
27–30: hero close-up of visibly imperfect key beside several opened cylinders; title.
No explanatory text is required beyond optional `ONE KEY. SEVERAL LOCKS. EVERY CUT COSTS OPTIONS.`

## Capsule test
Single readable image: large brass key in vice with visibly stepped cuts; behind it, three cutaway cylinders whose pin lines align differently against the same key. Risk: can be mistaken for lockpicking sim. Mitigation: never show pick tools; key/file/three cylinders must dominate.

## Production burden
Vertical slice: 3 locks, 2 blanks, 5 columns, one transparent cylinder, file/test/reset, deterministic solver/validator. Low-medium technical burden; tactile animation/presentation is the main craft risk.
Demo: 5–6 cases, ~20–30 min, 2 cylinder visual families max; medium polish burden.
~30 cases: data-driven accepted sets + solver validation; low asset scaling. Hand-authoring difficulty curves and preventing isomorphic cases is the primary content burden.

## Accessibility/readability failure analysis
- color cannot be sole feedback; pin/mark shape + motion + optional labels;
- fine motor filing is never authoritative: one input = one discrete depth step;
- cutaway lock and enlarged bench zoom required for low vision;
- haptics/audio supplement but never encode unique state;
- hold/toggle alternatives for inspection;
- no timed decisions in core campaign;
- high-contrast key edge/impression mode;
- textual depth numbers optional accessibility aid, not required optimal surface.

## Final verdict
**WINNER.** It retains its grammar after theme removal, has the smallest complete state, lowest content/exception burden, strongest tactile causal loop and cleanest 30-second `mistake -> restraint -> same key opens another lock` reveal.

---

# 2. G8C04 WINDOW GARDEN

## Eight-blueprint stress
W01 shutter redirects one sun lane; W02 trellis fork; W03 prune updates exact next-day ghost; W04 temporary shade; W05 support reservation; W06 bridge-then-remove for pollinator passage; W07 two-plant mutual interference; W08 three-day shade/support/vent finale. No primitive after W03.

## Formal state
Facade occupancy grid, plant graph/tip states, shutter orientations, support cells, day/epoch, deterministic sun lane, objective flags. Advance is a pure growth function; prune deletes a branch/subgraph; preview calls identical function without commit.

## Naked grammar
**Edit current environment/branches to control a deterministic future occupancy graph under delayed occlusion/support constraints.** Deep, but less commercially distinct because pruning/growth geometry is already an explicit puzzle surface.

Case 5 thought: `Where will this branch grow tomorrow?`; case 15: `Which temporary obstruction/support should exist for one cycle?`; case 30: `How do several delayed occupancy graphs reserve cells/light for each other?` Good evolution.

## Trailer/capsule
Trailer is excellent: shutter -> ghost branch -> prune -> day advance -> exact growth -> shade saves second plant. Capsule is weaker: a beautiful facade with plants/shutters still reads `cozy plant game` before the deterministic grammar is understood.

## Burden
Vertical slice medium-high because preview must equal resolution and readable growth geometry is art+tech coupled. Demo requires polished plants/sun/shadows. Thirty cases require authored facade/growth graphs and anti-isomorphism validation; still feasible but materially above Locksmith.

## Accessibility/readability
Occlusion, thin branches, sunlight/shadow and multi-day ghost layers create visual-density risk. Needs outlines, reduced-motion advance, non-color light bands and preview stepping. Exact preview is mandatory; any ambiguity feels like simulation betrayal.

## Fresh collision / final verdict
Current **Topiary: A Pruning Puzzle** (Steam metadata updated 27 Aug 2026) explicitly sells `cut branch -> buds fork -> grow season -> cut again -> shape plant`. That does not duplicate shutters/light/support, but it materially weakens the one-verb visual novelty exactly at final selection time.

**RUNNER-UP / KILL FOR GAME #008.** Preserve lesson only, not canon.

---

# 3. G8C07 FIREBREAK FOREMAN

## Eight-blueprint stress
F01 clear one spread edge; F02 burn-duration/spent fuel; F03 declared wind epoch; F04 soak exact one-step delay; F05 remote break before wind; F06 worker-access-first; F07 controlled sacrificial burn; F08 mixed two-objective/two-wind finale. No primitive after F03 would violate the stated final gate, so this exposes a problem: soak/access/sacrifice cannot all be introduced honestly after blueprint 3 unless tutorial 1–3 become overloaded. Compressing them into the first three harms onboarding.

## Formal state
Cell material/state, deterministic ignition/burn timers, allowed spread edges, wind epoch, worker location/access, intervention inventory/availability, objective states. Event-step transition is deterministic. Solver state is substantially larger than rivals because fire timers + worker reachability + wind time all matter.

## Naked grammar
**Modify a spreading deterministic cellular process before declared direction changes, using delay and intentional fuel consumption while preserving agent access.** Strong and dramatic.

Case 5 thought: `Where will wind make today's fire relevant?`; case 15: `What should I let burn now so it cannot burn later?`; case 30: `Which sacrifice/delay preserves future intervention access across epochs?` Excellent mature thought evolution.

## Trailer/capsule
Best spectacle. Thirty seconds easily communicates bulldozed break, wind turn, sacrificial shed, protected asset. Capsule reads wildfire/firefighting immediately but not the deterministic puzzle distinction; commercial word `Firebreak` also collides noisily with FBC: Firebreak despite unrelated gameplay.

## Burden
Highest. Even discrete authority needs convincing fire/smoke/VFX that never lie, site art, worker path readability, event preview and accessibility layers. Thirty cases require careful maps and simulation validation.

## Accessibility/readability
Smoke and fire are inherently occluding/high-motion. Reduced VFX, edge outlines, pause/step mode, wind timeline and non-color material states are mandatory. Exact causality can still be misread as stochastic because players bring real-fire expectations.

## Final verdict
**KILL FOR GAME #008.** Mechanically strong, but highest implementation/readability burden, existing wildfire-puzzle adjacency, and tutorial primitive compression all lose to Locksmith's Margin.

---

# Pairwise final decision

| Criterion | Locksmith | Window Garden | Firebreak |
|---|---:|---:|---:|
| Naked grammar distinctness | 5 | 4 | 4 |
| 30s demo causality | 5 | 5 | 5 |
| Capsule category clarity | 4 | 3 | 4 |
| Mature depth with fixed vocabulary | 5 | 4 | 4 |
| Solver/state compactness | 5 | 4 | 3 |
| Readability reliability | 5 | 3 | 2 |
| ~30-case content efficiency | 5 | 4 | 3 |
| Current analogue distance | 5 | 2 | 2 |
| Portfolio distance | 5 | 4 | 5 |
| Overall production risk | low-medium | medium-high | high |

**Selection: G8C02 Locksmith's Margin.**

Selection is based on core grammar + demo + feasible mature depth, not aggregate arithmetic. Window Garden and Firebreak Foreman are rejected Game #008 concepts and are portfolio/exclusion history only.
