# GAME #013 — PHASE 2 CONCEPT TOURNAMENT / ROUND C

Date: 2026-09-02
Status: ROUND C COMPLETE — WINNER SELECTED: **SEAL BREAK**

## Purpose
Round C attacks the three finalists under the same final bar: second hard diagnostic aimed at the surviving weakness, hour-10 campaign diversity, six-case demo deductions, portfolio collision, trailer/readability, controller/Deck burden, asset burden, certifier complexity and implementation risk. A concept wins only if its depth is not merely larger state-space or more predicates.

Fresh market context checked 2026-09-02: compact paper/minimalist puzzle presentation is visibly active on Steam in 2026 (including Cartapli: Fold Quest, Crease Demo, KNICK, Paperlands, Piece by Piece, FILL IT). This strengthens the portfolio/market penalty for another game whose first screenshot is principally flat paper layers. It does not invalidate paper aesthetics, but mechanical identity must read differently before copy is read.

---

# 1. CARBON COPY — FINAL ATTACK / KILL

## C diagnostic A4 — four-sheet coupled transfer with bounded reorder
Attack target: Round B survived only because multi-cell footprints coupled per-cell transfer depth. Round C asks whether deeper play can grow without becoming either a transfer-depth matrix or another flat-layer permutation game.

Kernel extension tested:
- four aligned sheets A/B/C/D, 4x4;
- A is fixed top/writing sheet;
- B/C may swap once before any press; D fixed bottom;
- inventory: H2, V2, L3, T4, each once;
- carbon/non-carbon pattern differs on B and C;
- targets require exact receiving sheets for selected coordinates plus forbidden duplicate marks;
- no rotation of sheets or stamps in this diagnostic.

Naive action surface is `2 * 12 * 12 * 9 * 8 = 20,736` placement/order configurations before overlap legality and target pruning.

### Human deduction test
Useful deductions still exist:
1. coordinates required on D force both middle sheets to be carbon at those rays, constraining the B/C order;
2. mixed receiving depths within one footprint can identify a scarce stamp placement;
3. forbidden duplicate cells can couple two otherwise plausible stamps.

But the new depth source is now explicitly **which flat layer occupies which depth, then which footprint covers a vector of required receiving depths**. The natural expert representation becomes a per-coordinate depth map plus layer-order hypothesis. That is a clean CSP, but it is not a sufficiently different hour-10 reasoning identity from Binder's Imposition (#009), whose mastery is also predicting consequences of source arrangement across layered flat material and deterministic transforms.

### Portfolio attack versus #009
#009 frozen hook: arrange pages on flat sheets so fold/flip/nest/trim transforms yield the correct final book. Carbon Copy does not fold or bind, but its advanced play increasingly asks the player to:
- inspect several aligned flat sheets;
- reason about layer order;
- predict deterministic transformed consequences through depth;
- satisfy final per-layer constraints.

The distinction is physically real but portfolio-level visual/reasoning overlap is too high. Removing sheet reorder would reduce collision but also leaves the Round-B transfer-depth-matrix ceiling exposed.

## Hour-10 campaign audit (hypothetical 30 cases)
Potential families:
1. two-sheet pass/stop — tutorial only;
2. mixed-depth domino fitting — real;
3. scarce footprint identity — real;
4. overlap/no-duplicate interference — real;
5. three-sheet mixed-depth inverse solving — real;
6. bounded layer reorder — real but portfolio-dangerous;
7. extra stamp shapes — mostly content alphabet inflation;
8. larger boards — parameter inflation;
9. more target predicate types — bookkeeping;
10. four sheets — state inflation unless layer order matters.

A 24-case campaign is possible; a 30–36-case campaign without introducing more stamp shapes/predicates/order variants would likely repeat the same 'recover footprint from receiving-depth pattern' deduction.

## Six-case demo beatsheet
1. Press a domino: one cell stops, one passes.
2. Infer a domino from two required receiving depths.
3. Two footprints share a forbidden duplicate cell.
4. Scarce L footprint covers three mixed-depth targets.
5. Three sheets make one receiving-depth pattern impossible under one order.
6. Reorder B/C then solve a compact coupled placement.

The demo is strong, but beat 6 reveals the same feature that creates portfolio collision.

## Presentation / implementation
- Screenshot: attractive exploded translucent stack, but visually adjacent to paper-layer puzzle territory.
- GIF: excellent downward mark propagation.
- Controller/Deck: moderate; layer focus + stamp placement + exploded preview are manageable.
- Asset burden: low-moderate.
- Certifier: easy-to-moderate finite enumeration.
- Implementation risk: low.

**Verdict: KILL.** Not because the mechanic is bad; because surviving depth requires exactly the layer-order/depth abstraction that makes Game #013 too close to #009 while still tending toward matrix reasoning.

---

# 2. BLIND STAPLE — FINAL ATTACK / KILL

## C diagnostic J4 — six layers, three penetration bands
Attack target: factorial permutation surface and flat-layer portfolio collision.

Kernel tested:
- six visible layers A–F;
- three fixed candidate staple families at depths 2, 3 and 4;
- player chooses stack order and exactly two sockets from a bounded set of eight;
- each socket has visible per-layer safe/unsafe puncture status;
- targets specify required adjacent bindings, forbidden bindings and one layer that must remain unpunctured;
- no layer rotation.

Naive stack/socket surface is `6! * C(8,2) = 20,160` before safety pruning.

### Human deduction test
Strong authored cases can still collapse search into penetration bands:
1. a required depth-4 chain can fix the middle members of the top-four band;
2. a depth-2 required pair can orient the top of that chain;
3. an unpunctured layer can be excluded from every selected penetration band;
4. incompatible socket safety sets can eliminate entire socket classes.

This is legitimate deduction, not brute force. However the finite vocabulary is narrow: almost every strong deduction is a statement about adjacency/position inside top-N prefixes. Adding depth 4 expands the band but does not create a new reasoning object.

## Portfolio attack versus #009
Blind Staple is more distinct mechanically than Carbon Copy because staples create adjacency/binding rather than transformed face positions. Still, its screen language and expert mental model remain:
- reorder visible flat layers;
- predict a physical operation through that ordered stack;
- satisfy relational constraints on the resulting layered object.

A player seeing screenshots of Binder's Imposition and Blind Staple would reasonably classify both as tactile paper-stack permutation puzzles before understanding the differing rule. Since #009 already owns the portfolio's flat-sheet/signature lane, #013 should spend its slot elsewhere unless Blind Staple is overwhelmingly stronger. It is not.

## Hour-10 campaign audit (hypothetical 30 cases)
Families:
1. depth-2 pair binding — tutorial;
2. safe/unsafe puncture exclusion — real;
3. depth-3 shared-middle chain — real;
4. two sockets with incompatible safety sets — real;
5. required + forbidden bindings — real;
6. unpunctured-layer exclusion — real;
7. depth-4 band — mostly wider version of same;
8. choose sockets + order together — coupling, but same band logic;
9. extra layers below max depth — invalid/noise;
10. rotations — rejected because they worsen #009 collision/search burden.

A disciplined 24-case campaign is plausible. At 30–36 cases, the design would rely increasingly on denser safety matrices and longer top-prefix chains. That is parameter inflation rather than qualitative mastery expansion.

## Six-case demo beatsheet
1. Depth-2 staple binds only top pair.
2. Unsafe puncture eliminates a candidate top layer.
3. Depth-3 chain: infer the shared middle layer.
4. Choose between sockets by safety compatibility.
5. Two staples intersect top-2/top-3 constraints.
6. Five-layer capstone where lower-order equivalence is intentionally accepted.

Excellent teaching curve, but cases 5–6 already expose most of the durable vocabulary.

## Presentation / implementation
- Screenshot: very legible cross-section, but paper-stack identity is immediate.
- GIF: excellent staple penetration animation.
- Controller/Deck: moderate; reorder + socket selection is clean.
- Asset burden: low.
- Certifier: easy finite permutation/socket solver.
- Implementation risk: low.

**Verdict: KILL.** Good puzzle, insufficient campaign diversity to justify a second flat-layer portfolio entry.

---

# 3. SEAL BREAK — FINAL ATTACK / WINNER

## C diagnostic D4 — witness logic beyond simple first-break ordering
Attack target: prove at least three qualitatively different temporal deductions beyond repeatedly reading `break_time = min(open positions)`.

Diagnostic frame:
- five compartments A–E;
- one compartment may remain unopened;
- player installs a bounded subset of visible seal sockets, then chooses an opening sequence for four compartments;
- a seal crosses a visible finite set of compartment seams and breaks irreversibly on the first qualifying opening;
- evidence can specify a seal's exact break checkpoint, survival through a checkpoint, or final intact state;
- overlapping seals may share some but not all crossed compartments.

Representative raw surface with 12 candidate sockets, choose 6 and order four of five compartments: `C(12,6) * P(5,4) = 924 * 120 = 110,880` configurations. This remains trivial for an offline certifier but large enough that player-facing content must support deductions.

### Deduction class 1 — intersection triangulation
If seal X crosses {A,C} and seal Y crosses {A,D}, and both break at checkpoint 2 while a single-A witness survives checkpoint 1, then A is strongly localized to checkpoint 2 unless two independent compartments happen to occupy that checkpoint, which is impossible. Overlapping witness sets isolate the responsible opening by intersection, not by simply sorting individual deadlines.

### Deduction class 2 — survivorship / unopened-compartment inference
If seal Z crosses {B,E} and remains intact after all four allowed openings, then neither B nor E was opened. Because exactly one compartment may remain unopened, such an evidence combination can prove that a proposed seal placement is impossible, or force the player to choose a different socket whose crossing set is compatible with the single-unopened rule. Survival evidence therefore reasons about the complement of the opening sequence, not only first-break rank.

### Deduction class 3 — negative precedence from delayed break
If seal M crosses {B,C,D} and first breaks at checkpoint 4, then all three candidate compartments are excluded from checkpoints 1–3 except whichever actually occupies checkpoint 4; combined with witnesses that prove B and C were already opened earlier, the target is impossible. Conversely, a delayed multi-crossing witness can force several compartments later than another event. This is a lower-bound/exclusion deduction, not simple identification of the first event.

### Deduction class 4 — placement/order coupling
When the player chooses both which seal socket to install and opening order, an evidence card can be satisfiable under two opening orders for socket S1 but only one order for S2. A witness-placement choice therefore changes the temporal information structure itself. This creates inverse design: choose witnesses that will make the required history provable.

### Deduction class 5 — witness discrimination by shared seam
Two seals may share seam A but diverge on C versus D. If one breaks at checkpoint 1 and the other at checkpoint 3, A cannot be the checkpoint-1 cause for both; the discrepancy proves the earlier tear came through the divergent branch. This is causal discrimination from paired physical traces.

These classes share one rule vocabulary — irreversible tear at first crossed opening — but produce intersection, complement/survival, lower-bound, placement-information and paired-discrimination reasoning. Round C therefore rejects the claim that all advanced play is one repeated ordering formula.

## Hour-10 campaign map (30-case target; 24-case floor)
Six acts of five cases each are plausible without new core rules:

### Act I — Read the tear (cases 1–5)
Single seals, multi-crossing seals, exact first-break checkpoints. Pure onboarding; only first-order reasoning.

### Act II — Compare witnesses (6–10)
Overlapping seals, shared-seam divergence, identity-rich evidence. Introduces intersection triangulation and paired discrimination.

### Act III — Survive the inspection (11–15)
One compartment may remain unopened; intact-through-checkpoint and final-intact evidence create complement reasoning.

### Act IV — Choose the witnesses (16–20)
Opening sequence fixed or partly fixed; player selects limited seal sockets to create a required evidence signature. Inverse placement rather than ordering alone.

### Act V — Reconstruct the opening (21–25)
Seal set fixed; player chooses among bounded opening histories. Delayed-break lower bounds, survivorship and overlap combine.

### Act VI — Build and reconstruct (26–30)
Choose a small seal subset plus a bounded opening sequence. Cases must contain at least three deduction classes and reject brute-force-friendly live oracle feedback.

Optional cases 31–36 are allowed only if playtests discover additional combinations of the same witness vocabulary; they are not required for commercial scope.

### Cosmetic families explicitly rejected
- seal colors with no rule meaning;
- arbitrary durability/HP;
- randomized tearing physics;
- larger cabinets for its own sake;
- narrative evidence text that adds hidden rules;
- dozens of seam types;
- freeform seal drawing.

## Six-case demo beatsheet with expected deductions
1. **One seam, one tear.** Player predicts exactly which opening breaks one seal. Deduction: direct cause.
2. **One seal, two possible causes.** A seal spans A/C; fixed opening order shows first-crossed semantics. Deduction: earliest qualifying event.
3. **Two overlapping witnesses.** {A,C} and {A,D} have different break times. Deduction: divergent branch identifies cause.
4. **The seal that survives.** One compartment may remain unopened; an intact seal crossing two candidates eliminates both from the opened history and forces the omitted compartment logic.
5. **Choose the evidence.** Fixed 3-step opening sequence; choose 3 of 6 seal sockets to match a target evidence card. Deduction: inverse witness placement.
6. **Capstone reconstruction.** Choose 4 seals and one of several bounded 4-step histories; exact break times + one survivor require intersection, delayed-break exclusion and placement/order coupling. No new rule is introduced.

The demo proves escalation with the same physical verb instead of withholding the real game.

## Marketability / presentation
- Screenshot: cabinet/box seams crossed by bright tamper strips and an evidence timeline is visually distinct from the factory portfolio and from 2026 paper-folding puzzle imagery.
- 2–5 second GIF: open compartment -> multiple specific seals tear -> evidence timeline stamps at that checkpoint. Extremely legible causal payoff.
- Trailer: can show prediction, commit, destructive reveal and rewind/reset in a few seconds.
- Controller/Deck: low burden. Navigate compartments/sockets, place/remove seal, order bounded opening cards, commit/replay. No precise cursor is intrinsically required.
- Asset burden: low-moderate 2D/2.5D cabinet fronts, seal strips, tear states, evidence cards; no physics simulation authority.
- Certifier: moderate but bounded. Enumerate legal seal subsets x bounded opening histories, canonicalize evidence signature, require uniqueness/equivalence rules.
- Implementation risk: low-moderate. Tear visuals may animate, but authoritative mechanics are discrete crossing sets and checkpoint state.
- Accessibility: seal identity cannot rely on color; use pattern/icon + label. Timeline/evidence must be readable at handheld scale.

## Portfolio comparison
Seal Break has no substantive collision with #009. It is not a flat-sheet transform puzzle, not topology, not cyclic deletion, not network redistribution, not observation/memory. Its durable reasoning object is **destructive temporal evidence**: choose/read physical witnesses whose irreversible failure reveals or constrains a hidden/target opening history.

---

# 4. Equal final comparison

| Dimension | Carbon Copy | Blind Staple | Seal Break |
|---|---:|---:|---:|
| 10-second hook | 5 | 5 | 5 |
| Same-vocabulary hour-10 diversity | 3 | 3 | 5 |
| Human deductions before enumeration | 4 | 4 | 5 |
| Portfolio distinctness | 2 | 2 | 5 |
| Static screenshot differentiation | 3 | 3 | 5 |
| GIF/trailer causal payoff | 5 | 5 | 5 |
| Controller/Deck fit | 4 | 4 | 5 |
| Asset burden safety | 5 | 5 | 4 |
| Certifier simplicity | 5 | 5 | 4 |
| Implementation risk | 5 | 5 | 4 |
| Demo escalation | 4 | 4 | 5 |
| Anti-repetition confidence | 3 | 3 | 5 |
| **Total / 60** | **48** | **48** | **57** |

Scores are decision aids; decisive evidence is qualitative. Carbon Copy and Blind Staple are both good standalone prototypes, but their strongest advanced forms occupy a layered-paper reasoning lane already represented by #009. Seal Break clears both the diversity and portfolio gates.

# ROUND C VERDICT
**WINNER: SEAL BREAK.**

Concept identity retained for Phase 3:
> A compact deterministic puzzle about placing tamper seals across a compartmented object, then choosing or reconstructing a bounded opening history so the irreversible pattern of torn and surviving seals matches an evidence record.

Non-negotiable winner gates carried forward:
1. final-state-only seal puzzles are tutorial-only;
2. substantive cases use >=2 temporal checkpoints;
3. advanced cases must combine at least two qualitatively different witness deductions, and late cases at least three;
4. all seal crossing sets and all mechanically relevant opening effects are visible before commit;
5. no hidden physics or probabilistic tearing;
6. no freeform sealing/drawing; finite sockets only;
7. evidence must use identity/pattern/icon, not color alone;
8. no live solver oracle that lets players scrub orders until badges turn green;
9. campaign target 30 authored/certified cases, floor 24; 31–36 only if same-vocabulary diversity is empirically justified.

Phase 2 is complete. Proceed to Phase 3 Product Thesis Lock.