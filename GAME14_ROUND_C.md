# GAME #014 — PHASE 2 CONCEPT TOURNAMENT — ROUND C

Date: 2026-09-02
Status: COMPLETE — Negative Casting selected; Phase 3 next.
Authority: `START_HERE.md` -> `STATUS.md` -> `GAME_INDEX.md` -> `GAME14_RESEARCH.md` -> `GAME14_TOURNAMENT.md` -> `GAME14_ROUND_B.md` -> this file.

## Method
Round C attacks the three finalists as products rather than toy CSPs. No rescue mechanics are permitted. Each receives a 24-case family skeleton, first-20-minute/hour-1/hour-3 simulation, explicit failure-hypothesis attack, and equal scoring. Counts below are campaign architecture targets, not promises that every case ships unchanged.

## Fresh commercial check — 2026-09-02
Current puzzle market continues to reward clear, compact premises but gives little protection to merely competent abstract logic games. `Is This Seat Taken?` (released 2025-08-07) remains a useful low-scope benchmark: $9.99, a demo, Steam Deck-tested requirements, and 97% positive English reviews in the current Steam result. Its appeal is immediately readable and scenario-driven rather than dependent on large systemic complexity. `The Séance of Blake Manor` (PC 2025-10-27) has 94% positive English Steam reviews and announced PS5/Xbox Series/Switch 2 ports for 2026-10-27, showing continued appetite for strongly framed puzzle/mystery experiences, but its content/narrative burden is far above this factory's desired scope. `Blue Prince` remains a high-attention puzzle benchmark and reached Switch 2 in March 2026, but its eight-year solo-development history is a warning against matching ambition through content volume.

Commercial implication: Game #014 should win on a GIF-readable physical rule, a satisfying short demo, and recombinable authored logic rather than narrative scale or hundreds of puzzles. Color/channel information must never be color-only.

---

# FINALIST A — NEGATIVE CASTING

## 24-case campaign skeleton
Frozen tournament rule remains: socketed opaque blockers, fixed discrete lights/projection surfaces, geometrically derived projection masks, target cells classified LIT / L1_ONLY / L2_ONLY / BOTH. No arbitrary masks or new powers.

### Act A1 — Protect the light (NC01–04)
One wall, two lights, 2–3 blockers. Teach LIT as hard exclusion, then one exclusive channel and BOTH decomposition. NC04 combines all four target classes.

### Act A2 — Read the edge (NC05–08)
One wall, longer coherent projections. Target transition/endpoints force blocker extent/orientation before blocker identity. Cases distinguish equal area but different interval endpoints.

### Act A3 — Same object, second wall (NC09–12)
Add second projection surface. Two orientations deliberately equivalent on wall A but different on wall B. Cases alternate cross-wall identity, unique producer and protected-cell deductions.

### Act A4 — Attribution (NC13–16)
3–4 blockers. Several target cells have identical total darkness but different channel class. Player must attribute which light is blocked where; a blocker can solve one channel requirement while violating another surface.

### Act A5 — Projection equivalence classes (NC17–20)
4–5 blockers, 2–3 surfaces. Begin by grouping blocker states that are indistinguishable on one surface; another surface splits the class. Endpoint and channel attribution then cross-couple. This is not object-count inflation: the intended move is reasoning over equivalence classes rather than individual states.

### Act A6 — Negative casts (NC21–24)
Capstones recombine protected lit islands, structured endpoints, cross-surface identity and channel attribution. NC23/24 require at least three class-eliminating human deductions before residual choice; certifier uniqueness alone is insufficient.

## First 20 minutes
NC01 visually demonstrates that placing a blocker changes symbols on the target strip. NC02 teaches that a required LIT cell can eliminate a blocker state without trial. NC03 introduces L1_ONLY/L2_ONLY with redundant glyph + light-origin line, not color alone. NC04 introduces BOTH and yields a short chain: protect -> attribute -> decompose. By minute ~15, NC05 adds an endpoint deduction. The demo can end at NC06/07 with a second surface reveal: the same sculpture casts two useful answers at once. This produces a trailer beat without explaining a large vocabulary.

## Representative hour-1 case
Four blockers x3 states, two walls. Wall A has two LIT islands eliminating orientations; an L1_ONLY transition fixes the extent of B2. B2's two remaining states are identical on A but project differently on wall B; B's protected endpoint fixes the state. A BOTH cell then has one remaining L2 producer, forcing B4. Human chain alternates geometry, channel and surface; it is not simply cover all dark cells.

## Representative hour-3 case / failure-hypothesis attack
Five blockers x4 states, three surfaces. If represented as arbitrary masks this is exact cover, so the authored case is rejected unless every mask is generated from blocker geometry and the intended route contains: (1) protected LIT pruning; (2) interval-boundary class elimination; (3) equivalence-class split on a second surface; (4) channel attribution on a third; (5) only then residual assignment. A test case meeting this route demonstrates that later depth can come from *why* a shadow exists, not merely whether a cell is covered. Shipping gate: MID/LATE cases need >=3 named human class eliminations before residual search; otherwise reject them even if unique.

## Round-C judgment
PASS. The exact-cover risk is real but controllable as an authoring/certification gate without changing the rule. Four genuinely recombinable families exist: protected negative space, geometric extent/endpoints, channel attribution, cross-surface equivalence splitting. Visual complexity rises slower than mirror ray length. The physical sculpture/light/wall presentation also hides the CSP representation better than Casting Call's explicit blocker obligations.

---

# FINALIST B — THE MISSING REFLECTION

## 24-case campaign skeleton
### B1 Direct absence (MR01–04)
One mirror interaction; forbidden object pruning and unique-source visibility.
### B2 Shared mirror (MR05–08)
Two ports constrain the same mirror state.
### B3 First divergence (MR09–12)
Two candidate paths share prefix then split; force earliest relevant orientation.
### B4 Backward feasibility (MR13–16)
Required endpoint has only one feasible predecessor chain under negative constraints.
### B5 Occlusion order (MR17–20)
Nearer hits invalidate otherwise plausible reflected paths; shared mirror coupling remains.
### B6 Two-bounce synthesis (MR21–24)
Ordinary cap remains <=2 mirror interactions; capstones combine shared mirror, first divergence, forbidden endpoints and backward feasibility.

## First 20 minutes
The first reflection is delightful and understandable. A forbidden object immediately gives a strong 'turn the mirror away' deduction. Shared-mirror cases teach coupling well. By the time two-bounce paths arrive, however, the player already benefits heavily from selecting a port and stepping through path segments.

## Representative hour-1 case
Four mirrors x2, three ports. Port P's two candidates diverge at M1; one branch eventually hits forbidden D, forcing M1. That changes the nearer-hit ordering for Q and makes one M3 state impossible; R then has one source for C. Strong human chain, still readable.

## Representative hour-3 case / failure-hypothesis attack
Six mirrors, 2–3 states, four ports, maximum two mirror interactions. The logical route is sound: forbidden endpoint removes a path class; backward feasibility fixes a predecessor; shared mirror resolves another port. But the player must repeatedly maintain which segment belongs to which port, which mirror has already been traversed, and where nearer hits terminate paths. Increasing logical coupling also increases diagram-tracing burden. If UI overlays every candidate path/class, it approaches solver assistance; if it only shows current rays, comparison becomes repeated visual tracing.

## Round-C judgment
KILL at final selection, not because the mechanic is weak but because the hour-3 cost is intrinsic. The two-bounce cap prevents runaway complexity yet also caps expansion space. Its best deductions require more visual bookkeeping than Negative Casting for comparable state depth, and handheld readability is materially worse. Adding ray notebooks, path pinning or special mirrors would be rescue complexity.

---

# FINALIST C — CASTING CALL

## 24-case campaign skeleton
### C1 Preserve the star (CC01–04)
Required-visible rays eliminate flat positions; one forbidden actor forces a blocker.
### C2 One flat, two jobs (CC05–08)
Blocker-sharing across seats/actors.
### C3 Near and far (CC09–12)
Depth dominance: nearer flat positions subsume far opportunities but may violate protected rays.
### C4 Track competition (CC13–16)
Two useful positions cannot coexist because flats share track occupancy.
### C5 Complement audiences (CC17–20)
Exact visible subsets across seats create cross-seat obligations and symmetry breaking.
### C6 Full house (CC21–24)
Combine protected rays, shared blockers, depth dominance and track competition.

## First 20 minutes
Best onboarding in the field. Seat overlay makes 'A must remain visible' and 'B must disappear' immediate. Moving one flat to satisfy two seats is a strong early aha. A six-case demo is straightforward and controller-native.

## Representative hour-1 case
Four flats, three seats. Protecting three required rays removes roughly half the positions. One remaining position blocks two forbidden actors, but occupying it prevents another flat from using the track segment needed for seat 3. Depth dominance makes a farther blocker the only compatible solution. Clean and satisfying.

## Representative hour-3 case / failure-hypothesis attack
Six flats x4 positions, five seats. Regardless of theatrical dressing, every flat state contributes a fixed blocked-ray set. Required rays delete states; forbidden rays become coverage clauses; track collisions add incompatibility clauses. Depth dominance improves human pruning but does not alter this monotone structure. After the player learns preserve-required -> cover-forbidden -> resolve track conflicts, the intended routes differ mainly in which coverage clause is tight. The campaign families are presentation variants of the same set-cover/CSP grammar.

## Round-C judgment
KILL at final selection. It has the strongest UX and demo but confirms the Round-B repetition hypothesis. Later variety would require lights, moving actors, timed cues or special flats, all prohibited rescue mechanics. Negative Casting keeps similarly readable visibility constraints while channel attribution and multi-surface projection provide a stronger second-order grammar.

---

# Equal scorecard
Scores 1–5; repetition/content/technical are scored with 5 = lower risk/burden.

| Criterion | Negative Casting | Missing Reflection | Casting Call |
|---|---:|---:|---:|
| Hook / GIF | 5 | 5 | 5 |
| Human insight | 5 | 5 | 4 |
| Low repetition risk | 4 | 3 | 2 |
| Tutorial burden | 4 | 3 | 5 |
| Handheld/controller UX | 4 | 3 | 5 |
| Low content burden | 4 | 3 | 5 |
| Low technical burden | 4 | 3 | 5 |
| Portfolio distance | 5 | 5 | 5 |
| Demo strength | 5 | 5 | 5 |
| Commercial framing | 5 | 4 | 4 |
| **Total / 50** | **45** | **39** | **45** |

The tie in raw score is deliberately not broken arithmetically. Casting Call's 2/5 repetition score is fatal because campaign depth is a core gate. Negative Casting's risks are specification/authoring constraints rather than a demonstrated collapse of its rule grammar.

# FINAL SELECTION

## WINNER — NEGATIVE CASTING
Game #014 proceeds with **Negative Casting** as the selected working concept.

Why it wins:
- a blocker state has coupled consequences across light channels and projection surfaces, preserving several qualitatively different deductions under one physical rule;
- hour-3 depth can be gated by geometric coherence + human-route certification rather than rescued with new mechanics;
- the premise is GIF-readable: arrange objects so several walls contain the *right kinds of shadow and light*;
- content can be data-driven and visually themed as small sculptural casting tables rather than arbitrary bitmasks;
- a short premium demo can reach the second-surface reveal quickly;
- it remains materially distant from Games #001–#013.

## Non-negotiable carry-forward gates
1. Projection masks are derived from coherent discrete geometry; arbitrary authored cell masks are forbidden as shipping canon.
2. Channel identity uses redundant glyph/shape/line encoding; never color alone.
3. Static inspection may explain a selected object's physical projection, but UI must not become a combined-solution oracle.
4. MID/LATE authored cases require >=3 named human class-elimination deductions before residual search.
5. Campaign depth must use the same light/blocker/projection rule; no special blocker powers are assumed by selection.
6. The product must remain readable on a handheld-sized viewport; multi-surface presentation needs a dedicated UX solution later.

## Phase-2 result
**PASS -> Negative Casting selected.** Missing Reflection and Casting Call become rejected tournament history only and must not silently supply mechanics later.

NEXT: Phase 3 Product Thesis Lock. Freeze target player/platform, product framing/title direction, one-sentence hook, core fantasy, session structure, exact core loop, differentiation, scope ceiling, campaign duration, and explicit out-of-scope boundaries before Mechanical Architecture.
