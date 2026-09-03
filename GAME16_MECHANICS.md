# GAME #016 — PHASE 4 MECHANICAL ARCHITECTURE

Date: 2026-09-03
Status: PHASE 4 COMPLETE
Working title: **ONE-WAY WORKSHOP**
Authority: `GAME16_PRODUCT_THESIS.md` plus prior Game #016 tournament history.

## 0. Mechanical objective
The game is a finite deterministic fabrication puzzle in which irreversible cuts create children whose physical properties determine future capabilities. The solved object is not merely the final assembly: it is a valid **fabrication ancestry** that preserves the right pieces long enough to perform every required operation.

No production implementation is started here. This file freezes the rules that Phase 5 may author content against.

---

# 1. Exact puzzle state
A job state is:

`JobState = {job_id, plan, stocks, loose_children, stations, operations, part_slots, assembly_state, requirement_state, commit_index, trace}`

All player-visible puzzle-relevant state is finite and deterministic.

## 1.1 Job
A `Job` contains:
- a finite set of initial `Stock` objects;
- a finite ordered/unordered set of `Operation` definitions;
- `PartSlot` definitions for the final product;
- `JigStation` definitions referenced by operations;
- final `CertificationRequirement`s;
- authored dependency metadata used only by validators/certifier explanation, never to force one solution path;
- presentation metadata irrelevant to logical correctness.

A job may have more than one valid solution family. The runtime certifier judges state, not a hidden canonical move list.

## 1.2 Workpiece identity: Stock and Child
Every cuttable/usable physical piece is a `Workpiece` with:
- immutable `piece_id` unique within an attempt;
- immutable `root_stock_id`;
- immutable `lineage_path` (e.g. `S1/L/R`);
- current geometry token from an authored finite geometry family;
- current capability set;
- availability state;
- optional assigned `PartSlot`;
- optional occupied `JigStation`;
- optional derived witnesses added by guided operations.

Initial stock is a root workpiece with `lineage_path = root_stock_id`.

A committed cut destroys the parent as an available object and atomically creates exactly two child workpieces `A` and `B`. Children inherit root identity and receive deterministic lineage suffixes. A destroyed parent can never reappear inside the attempt.

Lineage is semantic ancestry, not a score. Two geometrically identical children remain distinct if born from different parents because downstream authored constraints may require only geometry/capability, never an arbitrary secret identity unless the plan visibly names ancestry class (see §3.5).

## 1.3 Availability state
A workpiece is exactly one of:
- `LOOSE`: may be inspected, cut if cuttable, docked or assigned;
- `PART_DOCKED`: occupying one final part slot;
- `JIG_OCCUPIED`: currently occupying a reversible jig station;
- `CONSUMED`: permanently unavailable after a consuming operation;
- `PARENT_SPENT`: historical node after cutting; not physical/current.

No piece can occupy multiple places simultaneously.

## 1.4 CutSocket
A `CutSocket` is an authored destructive transform attached to one geometry token. It contains:
- socket id and visible physical location/orientation;
- cut family: `STRAIGHT` or `DIAGONAL`;
- two deterministic child geometry outputs;
- child capability derivation rules;
- optional prerequisite jig/operation witness for later cases;
- optional visual preview data.

There are no continuous coordinates. If a cut is not represented by a visible legal socket, it cannot be performed.

## 1.5 JigStation
A `JigStation` is a physical socket associated with one guided operation. It contains:
- station id;
- `CapabilityRequirement` predicate;
- occupancy mode `TEMPORARY` or `CONSUME_ON_OPERATION`;
- optional orientation/face requirement drawn from the normalized grammar;
- a visible target silhouette/fit affordance;
- operation ids it enables.

Docking is legal only when the piece satisfies the station predicate. Incompatible pieces visibly fail to seat; there is no hidden penalty.

## 1.6 Operation
An `Operation` is an authored guided transform. It contains:
- operation id;
- target workpiece/part-slot predicate;
- zero or one required JigStation (baseline; no multi-jig simultaneous operation);
- prerequisite witnesses, if any;
- deterministic effect;
- whether the jig is released or consumed after execution;
- whether the target remains loose or becomes fixed into a part slot.

Canonical operation effects are only:
1. `GUIDED_DRILL`: add one hole-pattern witness to target;
2. `GUIDED_MARK`: add one reference-mark witness to target;
3. `GUIDED_SPACING`: add one spacing witness to target;
4. `GUIDED_DIAGONAL`: add one diagonal/angle witness to target;
5. `ASSEMBLE`: dock/lock a valid part into its final slot.

A guided operation never changes arbitrary dimensions, duplicates material, spawns new stock, or unlocks freeform crafting.

## 1.7 PartSlot
A `PartSlot` contains:
- slot id;
- geometry/capability predicate for the workpiece accepted;
- required derived witnesses, if any;
- whether docking remains reversible before certification.

Baseline rule: part docking is reversible before certification unless the job explicitly marks an `ASSEMBLY_LOCK` operation as one of the <=6 committed fabrication operations. Ordinary placement into a part outline is not itself an irreversible fabrication commit.

## 1.8 CertificationRequirement
A final requirement is one of:
- `PART_PRESENT(slot)`;
- `WITNESS_PRESENT(slot, witness_type, parameter)`;
- `ANCESTRY_RELATION(a,b, relation)` only when visibly declared in the plan and physically meaningful (e.g. “matched pair cut from the same parent”);
- `JIG_RELEASED(station)` if final product cannot be certified with a temporary jig still occupying an assembly region;
- `OPERATION_DONE(op)`.

Certification predicates may compose with AND only at baseline. No opaque OR chains in final requirements; alternative solution families emerge upstream from multiple ways to create capabilities.

---

# 2. Normalized capability grammar
The thesis listed several overlapping properties. Phase 4 reduces them to four base capability families plus witnesses.

## 2.1 Base physical capabilities
Every physical capability must be inferable from shape/fit and optionally reinforced by an icon.

### A. `SPAN`
Represents a usable one-dimensional extent band.
`SPAN(axis, band)` where axis is one of the workpiece's authored local axes and band is a named discrete band, not a player-entered number.

Named bands within a job are ordered, e.g. `S < M < L`, and may map to exact internal units. UI primarily shows matching silhouettes/notches; numeric dimensions are optional accessibility/inspection detail.

Uses:
- spacer width;
- rail/part length requirement;
- reference-edge minimum usable extent.

This replaces separate “length band” and “spacer width” primitive families.

### B. `EDGE`
`EDGE(kind, band)` where `kind ∈ {STRAIGHT, DIAGONAL_A, DIAGONAL_B}` and band is minimum usable extent.

Uses:
- straight guide/reference edge;
- diagonal template.

There are no arbitrary angle values in baseline. `DIAGONAL_A/B` are job-legible authored angle families with distinct physical station fits.

### C. `FACE`
`FACE(kind)` where baseline `kind ∈ {FLAT, NOTCHED}`.

This exists only to let a station require a stable seating face or a visibly keyed shape. Do not proliferate decorative face predicates.

### D. `PAIR`
`PAIR(token)` is allowed only for two children born from one explicitly authored paired cut where the physical relationship is visible (mirror/notch mate). It is not an arbitrary identity key. It supports rare “matched cut siblings” content without secret genealogy checks.

## 2.2 Derived witnesses
Witnesses are added only by guided operations and are immutable once added:
- `HOLE(pattern)`;
- `MARK(reference)`;
- `SPACING(band)`;
- `ANGLE(kind)`.

A witness proves that a guided operation occurred on this exact child. It can qualify the child as a later part or jig, creating second-order capability chains.

Witnesses do not grant generic new cutting options unless a pre-existing visible cut socket explicitly requires that witness. Thus the game remains finite and authored.

## 2.3 Matching semantics
A requirement matches iff all of its clauses are satisfied exactly by the current piece.

Examples:
- spacer station: `SPAN(X, S)`;
- straight-reference station: `EDGE(STRAIGHT, M+) AND FACE(FLAT)`;
- angle station: `EDGE(DIAGONAL_A, S+)`;
- drilled template station: `HOLE(P2) AND EDGE(STRAIGHT, S+)`.

`M+` is internal author shorthand for band M or larger; player UI shows the required physical extent, not inequality notation.

No station may test hidden mass, hidden quality, historical move count, arbitrary piece id, or a property not visually represented.

## 2.4 Capability conservation
Cuts derive capabilities from resulting child geometry. They do not copy a single unique physical feature onto both children unless geometry legitimately gives both children that feature.

Guided operations add witnesses to one target. They cannot add `SPAN`, create new material, or enlarge an edge.

This is essential to prevent universal-tool snowballing.

---

# 3. Cut legality and irreversible ordering

## 3.1 Preview
Before commit, the player may freely:
- inspect every currently legal cut socket;
- preview both exact child silhouettes;
- preview each child's base capability icons/physical station matches;
- inspect which currently known stations each child could satisfy;
- rotate/view stock and children;
- dock/undock loose compatible pieces in non-consuming stations as planning rehearsal if the target operation has not been executed.

Preview never simulates the entire future dependency chain or says “this is the correct cut.”

## 3.2 Commit sequence
A cut commit is atomic:
1. validate parent is `LOOSE` and socket exists on current geometry;
2. validate any cut prerequisite jig/witness;
3. freeze input for the short commit animation;
4. append `CUT_COMMIT(parent, socket)` to trace;
5. mark parent `PARENT_SPENT`;
6. create exactly two children with deterministic ids/lineage/capabilities;
7. release/consume any cut jig as specified;
8. recompute legal operations and dead-state evidence;
9. return control.

No intermediate state may be saved or interactable.

## 3.3 Undo boundary
- Camera movement, inspection, preview, picking up, rotating, and reversible docking can be undone/cancelled freely.
- Once the player confirms a destructive cut or a guided operation whose effect adds a witness/consumes a jig, that fabrication commit cannot be undone inside the attempt.
- The only rollback across a fabrication commit is **Restart Job**.

This preserves the one-way fantasy while avoiding accidental UI punishment through explicit hold/confirm or equivalent commit affordance.

## 3.4 Guided-operation commit order
1. validate target and jig are present;
2. preview exact operation result/witness;
3. confirm commit;
4. append trace event;
5. add witness/effect;
6. consume/release jig according to operation definition;
7. recompute dead-state evidence.

## 3.5 Ancestry semantics
Lineage is always recorded for diagnosis. Gameplay predicates normally care about geometry/capability, not ancestry identity.

The sole baseline ancestry exception is a visibly physical `PAIR(token)` relation created by one authored paired cut. If used, the plan/station visibly shows the matched interface. No requirement may secretly say “must originate from Stock 2” merely to force the intended path.

---

# 4. Guided operations without crafting-system creep

## 4.1 Drill
Target piece has one or more authored drill sockets. Required jig physically aligns one socket. Committing adds `HOLE(pattern)` to that target. The drill does not remove a reusable child and does not create arbitrary hole coordinates.

## 4.2 Mark
A station places a jig edge/template against a target's authored mark zone. Committing adds `MARK(reference)` used by a later visible operation. A mark alone has no generic numeric coordinate.

## 4.3 Spacing
A spacer piece is docked between a stop and target. Committing adds `SPACING(band)` or authorizes one pre-existing target operation. This is the primary tutorial bridge from “offcut” to “future capability.”

## 4.4 Diagonal
A child with `EDGE(DIAGONAL_A/B)` docks as a template against a target's authored diagonal operation socket. Committing adds `ANGLE(kind)` or unlocks one deterministic diagonal child split already present in the job definition.

## 4.5 Chaining rule
A derived witness may qualify a child for **at most one additional capability role family per job**. Authors may not create recursive chains where witness A enables B enables C enables D on one universal piece. Late complexity should come from dependency graph across pieces, not leveling up one tool.

---

# 5. Win, fail, dead state, restart, proof trace

## 5.1 Win
A job wins only when the player invokes `CERTIFY` and every `CertificationRequirement` evaluates true.

Certification is never automatic. It is a deliberate final physical test/reveal.

## 5.2 Soft failure
If certification fails but some legal fabrication route may still satisfy all requirements, the certifier reports the first/most local unmet requirement and returns control.

Example: “Brace is missing ANGLE A witness” with the relevant brace and angle station highlighted.

## 5.3 Detectable dead state
A state is *provably dead* when, under the finite remaining transform graph, at least one unmet mandatory requirement has no reachable producer from any current loose/docked piece.

The runtime may detect dead state using an optimistic reachability analysis:
- ignore competition between future resource uses;
- allow every remaining legal transform independently;
- compute closure of capabilities/witnesses each current piece could still reach;
- if even this optimistic closure cannot satisfy a mandatory requirement, death is certain.

This detector is intentionally incomplete: it may fail to flag a state that is dead because two requirements compete for the same unique child. It must never falsely declare a live state dead.

When certain death is detected, the game says **Lineage broken** and identifies the impossible requirement plus relevant spent/current branch, but does not name the cut that should have been chosen.

## 5.4 Restart
Restart is available at all times after first fabrication commit. It:
- resets the job to authored initial state;
- preserves tutorial/hint accessibility settings;
- may preserve a non-scoring personal note/bookmark UI if Phase 6 adopts one;
- takes the player back to interactive initial state without campaign/menu reload.

Target recovery friction: effectively immediate.

## 5.5 Proof trace
Every commit writes a compact semantic event:
- cut parent + socket → child ids/capabilities;
- operation target + jig → witness added / jig consumed;
- assembly dock/lock;
- certification result.

The certifier can walk backward from an unmet requirement through producer relationships and show **why the current ancestry cannot produce it**. It never displays the hidden future winning sequence.

Diagnostic ladder:
1. requirement name + physical highlight;
2. current missing capability/witness;
3. on request, ancestry trace showing which branch was spent/consumed or lacks a producer;
4. optional hint system later may point to a contradiction class, but is Phase 6/7 design, not automatic certifier output.

---

# 6. Difficulty and progression variables
Difficulty may increase only through the following bounded variables:

1. `stock_count`: 1 → max 3;
2. `committed_operation_count`: 1–2 tutorial → max 6;
3. `active_loose_children`: target <=6, hard max 8;
4. `future_dependency_distance`: immediate next operation → up to 4 commit steps later;
5. `capability_choice_degree`: one obvious useful child → one child compatible with 2–3 stations;
6. `cross_stock_dependency_count`: 0 → max 2 meaningful crossings;
7. `derived_witness_depth`: 0 → max 2 chained guided operations across different pieces; max 1 witness-upgrade step on the same piece;
8. `alternative_solution_families`: 1 early → preferably 2–4 later;
9. `temporary_occupancy_conflict`: none early → at most 2 simultaneously meaningful station conflicts;
10. `cut_socket_count_per_piece`: tutorial 1–2; hard max 5 visible sockets on a current piece.

Forbidden difficulty inflation:
- tiny visual differences;
- hidden station predicates;
- continuous measurement;
- timing/dexterity;
- more than three base angle families (baseline uses two);
- >8 loose pieces;
- >6 fabrication commits;
- arbitrary recipe knowledge;
- giant cut trees whose difficulty is enumeration.

---

# 7. Dominant-strategy attacks

## 7.1 “Preserve the largest offcut”
Countermeasure: capability matching is shape/type specific. A small S-span offcut may be the only spacer; a large rectangular piece may lack the diagonal edge needed later. Jobs must include at least one case where largest-preservation provably loses before Family 3 ends.

## 7.2 “Make product parts first”
Countermeasure: at least one future operation on a product part requires a jig born upstream. If the player takes the visually direct product cut first, the parent containing that future jig geometry is destroyed. This remains the central signature.

## 7.3 “Hoard everything”
Hoarding loose pieces has no material penalty by itself; punishing inventory would add an unrelated economy. Instead conflicts arise because:
- some guided operations consume jigs;
- some useful pieces must be committed as product parts or altered with witnesses;
- a child may satisfy multiple stations but only one at a time;
- operation ordering can make its current form unavailable.

Therefore “keep all pieces” is allowed but not a solver.

## 7.4 “Restart-enumerate every branch”
The game cannot technically stop a player from brute-force restarting. Content must make deduction cheaper than enumeration.

Authoring anti-enumeration rules:
- <=5 cut sockets per current piece, but no job may be solvable by a flat one-step guess across all sockets after tutorial;
- plan reveals every mandatory station before first commit;
- every wrong major branch should contradict a visible future requirement within 1–3 commits, not after six silent moves;
- at least one human-readable necessity should eliminate >=50% of plausible first cuts in mid/late jobs;
- late jobs should have dependency reasoning across branches, not merely more sockets.

## 7.5 “Build one universal jig”
Prevented structurally by normalized grammar, no capability enlargement, guided-witness chain ceiling, and consumption/occupation. A workpiece may satisfy multiple station predicates if physically justified, but authored jobs must not allow one child to accumulate arbitrary EDGE/SPAN families.

## 7.6 Branch explosion
Each cut creates two children, but only authored sockets on currently cuttable children continue the tree. Validator hard gates:
- total reachable unique physical workpiece states in a canonical job <=64 under exhaustive design-time enumeration;
- total legal fabrication commits from any runtime state <=8, preferably <=5;
- no canonical job may require >6 commits;
- if exhaustive state graph exceeds these limits, simplify sockets/operations before adding content.

The 64-state ceiling is a design-time mechanical-state target, not a player-facing number; Phase 8 may refine implementation measurement while preserving boundedness.

---

# 8. Three worked deterministic cases

## Case T — “Keep the Spacer” (tutorial)
Purpose: teach byproduct = future capability with no ambiguity.

### Initial state
Stock `S1`: strip geometry length 6 internal units; cut sockets:
- `C2`: children span 2 + 4;
- `C3`: children span 3 + 3.

Plan:
- final rail slot accepts `SPAN(X,4+)`;
- drill operation on rail requires spacer station `SPAN(X,2)`;
- certification requires rail present + `HOLE(P1)`.

### Reasoning
If player cuts C2:
- child A span2 fits spacer station;
- child B span4 fits rail;
- dock A as spacer, B as drill target;
- guided drill adds `HOLE(P1)` to B;
- release A;
- dock B as rail; certify.

If player cuts C3:
- both children span3;
- no span4 rail can ever exist; optimistic dead-state detector immediately flags final rail impossible.

No hidden rule/new verb. One destructive cut + one guided operation.

Human proof: “I need four for the part and two for the tool, so 2+4 is forced.”

## Case M — “Wrong Side First” (midgame)
Purpose: defeat product-first and largest-offcut heuristics; introduce cross-blank ancestry.

### Initial state
Stock A: rectangular strip 10, sockets A4 (4+6), A3 (3+7).
Stock B: wedge blank, sockets BdiagA and BdiagB; each produces one 5-span rectangular child plus one triangular child with EDGE(DIAGONAL_A) or EDGE(DIAGONAL_B).

Plan:
- rail part requires `SPAN(X,7+)` + `ANGLE(DIAGONAL_A)` witness;
- foot part requires rectangular `SPAN(X,5+)`;
- rail guided diagonal operation requires jig `EDGE(DIAGONAL_A, S+)`;
- rail hole operation requires spacer `SPAN(X,3)`;
- certify rail + foot.

### Valid route
1. Cut B at `BdiagA` → triangular A-template + rectangular 5 foot candidate.
2. Cut A at A3 → spacer3 + rail7.
3. Dock A-template to rail diagonal station; guided diagonal adds `ANGLE(DIAGONAL_A)` to rail; release template.
4. Dock spacer3 for guided drill if plan includes its required hole witness; operation adds `HOLE(P1)` (optional variant; count remains <=4/5 commits).
5. Dock rail7 + foot5; certify.

### Losing plausible routes
- A4 gives 4+6: largest child6 looks attractive but rail7 becomes impossible.
- BdiagB creates wrong diagonal template even though its rectangular child still fits foot; certifier later reports missing producer for ANGLE_A.
- Product-first attempt to immediately assign an unmodified rail is reversible placement, but certification exposes missing angle; player must preserve/use the template first.

Human proof: future angle station forces BdiagA; rail size forces A3; spacer is therefore free consequence of the same forced cut.

No arbitrary ancestry predicate is required.

## Case L — “Witness Relay” (late)
Purpose: derived witness chain, dual-use conflict, three stocks, multiple valid families while remaining deductive.

### Initial state
Stock A: bar 12, cut sockets A3 (3+9), A4 (4+8), A5 (5+7).
Stock B: keyed plank 8, sockets Bstraight (2+6; 6 child has EDGE(STRAIGHT,M)), BdiagA (3+5; 3 triangular child EDGE(DIAGONAL_A)).
Stock C: small plate, two sockets Cleft/Cright creating either a flat S-span child or notched S-span child; only notched child can seat in mark station due `FACE(NOTCHED)`.

Plan final parts:
- Main beam: `SPAN(X,8+)`, requires `HOLE(P2)` and `MARK(R1)`;
- Brace: `SPAN(X,5+)` + `ANGLE(DIAGONAL_A)`;
- Cap: any `SPAN(X,S+)` remaining compatible child.

Operations:
1. Mark main beam: station requires `FACE(NOTCHED)` jig; adds `MARK(R1)`.
2. Drill P2: station requires a template with `MARK(R1)` **and** `EDGE(STRAIGHT,S+)`.
3. Diagonal brace operation: station requires `EDGE(DIAGONAL_A,S+)`; adds `ANGLE(DIAGONAL_A)`.

Key rule: a witness belongs to the target piece, not the jig unless operation says so. Therefore the authored mark operation in this case targets the straight-edge B child specifically, turning it into the future P2 drill template. This is visibly shown in the plan: “prepare drill template” subassembly, not an arbitrary hidden upgrade.

### Valid family 1
1. Cut Cleft → notched jig + cap candidate.
2. Cut Bstraight → straight-edge 6 template blank + 2 spare.
3. Dock notched jig to mark station targeting B6; guided mark adds MARK(R1) to B6.
4. Cut B's separate diagonal-capable sibling is impossible from same spent B root, so this family must obtain diagonal from a second visible diagonal socket on a preserved B child only if authored. To avoid hidden branch creep, freeze valid authored variant instead: Stock B consists of two root stocks B1 straight plank and B2 wedge within the three-stock ceiling, while A is main bar and C is notched plate. Thus late canonical case uses exactly A, B1, B2 and encodes notched jig as a child of A's spare branch.

The initial sketch above exposes a four-root pressure and is therefore rejected by the scope validator. It is repaired below rather than silently expanding scope.

### Repaired late case (canonical worked version)
Stock A bar12 sockets:
- A3 => child A3 span3 with FACE(NOTCHED), child A9 span9;
- A4 => child A4 span4 flat, child A8 span8.
Stock B straight plank8: B2 => B2 span2 + B6 span6 with EDGE(STRAIGHT,M).
Stock C wedge10:
- CdiagA => Ctri span3 EDGE(DIAGONAL_A) + C7 span7;
- CdiagB => CtriB span4 EDGE(DIAGONAL_B) + C6 span6.

Final parts:
- beam requires span8+ and HOLE(P2);
- brace requires span7+ and ANGLE(DIAGONAL_A);
- cap requires span2+.

Operations:
1. `PREP_TEMPLATE`: B6 target + jig FACE(NOTCHED) => add MARK(R1) to B6.
2. `DRILL_BEAM`: beam target + jig `EDGE(STRAIGHT,M) AND MARK(R1)` => add HOLE(P2) to beam; jig B6 consumed.
3. `ANGLE_BRACE`: brace target + jig EDGE(DIAGONAL_A) => add ANGLE(DIAGONAL_A) to brace; template released.

Valid route:
1. Cut A3 → notched A3 jig + A9 beam candidate.
2. Cut B2 → B2 cap candidate + B6 straight template.
3. PREP_TEMPLATE using A3 on B6 → B6 gains MARK(R1); A3 released.
4. Cut CdiagA → Ctri angle jig + C7 brace.
5. DRILL_BEAM using B6 on A9 → A9 gains HOLE(P2); B6 consumed.
6. ANGLE_BRACE using Ctri on C7 → C7 gains ANGLE_A.
7. Dock A9 beam, C7 brace, B2 cap; certify.

Fabrication-commit count is 6 if all three cuts and three guided operations count, exactly at ceiling. Loose-child peak is <=6.

Losing routes:
- A4 makes A8 beam but no notched jig exists, so PREP_TEMPLATE has no producer despite adequate beam size.
- CdiagB leaves plausible brace6 + wrong diagonal; brace size and ANGLE_A both fail.
- consuming B6 in DRILL is impossible before PREP_TEMPLATE because it lacks MARK(R1); the station rejects it, so operation order is legible rather than hidden.

Human proof route:
1. P2 drill station visibly requires a straight marked template → only B6 can become it.
2. B6 needs notched prep jig → forces A3, which still leaves A9 valid beam.
3. brace requires both 7+ and diagonal A → forces CdiagA.
Thus three root cut choices are deductively forced; execution then validates the planned ancestry.

No new primitive verb or secret property was required.

---

# 9. Authoring validation invariants
Every Phase-5 canonical case must pass all of these before inclusion.

## Logical correctness
1. At least one valid solution exists under exhaustive design-time solver/certifier.
2. Every requirement and station predicate uses only normalized capabilities/witnesses.
3. No hidden workpiece identity is used except visible `PAIR` semantics.
4. Every destructive transform creates exactly two deterministic children.
5. Every guided operation has one deterministic effect.
6. Runtime dead-state detector has zero false positives against exhaustive solver.
7. Certification accepts all valid solution families, not just authored reference route.

## Complexity
8. <=3 initial stocks.
9. <=6 fabrication commits in any intended canonical solution.
10. <=8 loose children at runtime; target <=6.
11. <=5 visible cut sockets on one piece.
12. exhaustive mechanical state graph target <=64 reachable meaningful states; hard exceptions require explicit Phase-4 amendment, not silent content inflation.
13. no operation requires more than one simultaneous jig.
14. same-piece witness upgrade depth <=1; cross-piece derived chain depth <=2.

## Deduction / anti-bruteforce
15. Mid/late case has at least one visible necessity that removes >=50% of plausible first destructive choices.
16. A wrong strategic branch becomes explainably contradictory within 1–3 further commits where practical.
17. At least one authored proof route can be written in ordinary language without enumerating every state.
18. “largest offcut,” “product first,” and “keep everything” must not solve all cases in a family.
19. A late case should have 2+ valid solution families when possible, but alternate families are not mandatory if the single route is richly deduced rather than guessed.

## Presentation legibility
20. Station compatibility is primarily visible by physical fit/silhouette.
21. Capability icons never introduce a rule not represented in geometry/plan.
22. A cold observer can distinguish product part vs loose byproduct vs docked jig.
23. Commit preview shows exact immediate children/effect.
24. Failure names a requirement and causal lineage, not generic “wrong move.”

---

# 10. Empirical gates handed to Phase 5+
These are not unresolved rules; they are validation obligations.

1. **Cut tactility gate:** discrete sockets must feel like direct manipulation, not a list/menu.
2. **Lineage readability gate:** six-commit case with <=8 children must remain understandable without opening a genealogy screen.
3. **Shape-first grammar gate:** at least 80% of cold-test station matches should be inferred from geometry/fit before reading text; exact threshold may be tuned in implementation playtest but failure requires presentation/content simplification, not adding more labels.
4. **Irreversibility gate:** players should understand a commit is permanent before confirming; accidental-cut reports must be rare in usability testing.
5. **Reasoning-over-enumeration gate:** cold players on midgame samples should verbalize at least one future requirement before choosing first cut; if most simply enumerate sockets, Phase 5 cases must be redesigned.
6. **Restart friction gate:** restart must return to interactive initial job state fast enough that failure tension is strategic rather than punitive.
7. **Universal-tool gate:** exhaustive content validation must show no single capability combination dominates >50% of jig stations across the campaign unless intentionally tutorial-only.
8. **Content variety gate:** six proposed reasoning families must produce meaningfully different proof sentences with the same verbs; if two families reduce to identical cut-choice logic, merge/replace before freeze.

---

# 11. Phase-4 lock
Mechanical architecture is stable enough for authored content without inventing mechanics.

Frozen for downstream phases:
- finite deterministic workpiece/lineage model;
- exactly-two-child destructive cuts;
- discrete cut sockets only;
- four-family base capability grammar (`SPAN`, `EDGE`, `FACE`, visible `PAIR`) plus four guided witnesses;
- one-jig guided operations;
- irreversible fabrication commits with free pre-commit inspection and instant restart;
- optimistic zero-false-positive dead-state detector;
- state-based certification plus causal proof trace;
- bounded difficulty variables and hard scope ceilings;
- authoring validator/anti-bruteforce invariants;
- three worked cases verified against the same rules.

No Phase-5 content should add a capability, operation family, hidden identity predicate, second simultaneous jig, continuous geometry or new puzzle verb without explicitly reopening Phase 4.

**NEXT:** Phase 5 Content Architecture — turn the six Round-C reasoning families into an exact 24-case campaign data plan, map capability/witness introduction cadence, define reusable visual/stock/jig kits, authoring schema, case validation matrix, demo subset, difficulty curve, reuse rules and content-production estimates while staying within this mechanical contract.
