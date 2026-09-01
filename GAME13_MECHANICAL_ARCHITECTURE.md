# GAME #013 — PHASE 4 MECHANICAL ARCHITECTURE

Date: 2026-09-02
Status: PHASE 4 COMPLETE — CANONICAL RULE SYSTEM FROZEN
Selected concept: **SEAL BREAK** (working title)
Authority: this file refines the Phase-3 thesis. If a lower-level mechanical statement here conflicts with earlier tournament examples, this file wins for Game #013 mechanics.

## 1. Mechanical design goal
Seal Break is a finite deterministic witness puzzle. The player is never simulating material strength or freeform tearing. A seal is a binary intact/broken witness installed at a legal socket. Opening a compartment traverses a known finite set of seams. An intact installed seal breaks at the first checkpoint whose opening traverses at least one seam covered by that socket.

The game derives depth from several witnesses observing overlapping subsets of the same opening history.

Core equation for installed socket `s` under history `H`:

`break_step(s,H) = min { i | traversed_seams(H[i]) intersects covered_seams(s) }`

If that set is empty, `break_step = NEVER` and the seal remains intact.

This equation is authoritative, but the player-facing game should teach the physical cause rather than show formulas.

---

# 2. Canonical data/state objects

## 2.1 Compartment
A `Compartment` is one independently openable unit.

Required fields:
- `compartment_id`: stable unique case-local ID;
- `display_label`: short accessibility-safe label;
- `traversed_seams`: non-empty set of `seam_id` values crossed when this compartment is opened;
- `openable`: normally true; false only for decorative/non-participating geometry, which should usually be omitted from puzzle data.

A compartment opening is atomic mechanically. Animation may show several hinges/latches moving, but the rules see one opening event.

## 2.2 Seam
A `Seam` is a named discrete boundary/path segment that an opening action can traverse.

Required fields:
- `seam_id`;
- presentation anchors needed later to draw the seam/socket relation.

A seam has no durability, direction, ownership or hidden state. It is only a stable geometric relation used to derive which openings tear which sockets.

## 2.3 Seal socket
A `SealSocket` is one authored legal place where one witness may be installed.

Required fields:
- `socket_id`: stable unique ID and canonical witness identity;
- `covered_seams`: non-empty set of `seam_id` values;
- `enabled`: true for playable sockets;
- presentation anchor/shape data to make every covered seam visually inspectable.

Derived field:
- `trigger_compartments = { c | c.traversed_seams intersects socket.covered_seams }`.

**Canonical representation choice:** case data stores seams and socket `covered_seams`; trigger-compartment sets are derived and validated. Tournament examples that directly listed `{A,C}` crossing sets are shorthand for this derived relation, not a second authority model.

Why this model is frozen:
- seams preserve the physical fantasy and allow two sockets to share one seam but diverge on another;
- derived trigger sets make certifier logic simple;
- there is no duplicate hand-authored trigger table that can disagree with geometry.

## 2.4 Installed seal
An `InstalledSeal` is binary witness state attached to one socket.

Fields:
- `socket_id`;
- `state`: `INTACT | BROKEN`;
- `break_checkpoint`: `NONE` while intact, otherwise exact 1-based checkpoint index.

There are no mechanically distinct seal items in v1. Seal identity is the socket/witness identity. The player spends a case-local seal budget by occupying sockets; there is no token-to-socket permutation, inventory rarity, color power or durability.

## 2.5 Opening step / history
An `OpeningStep` contains exactly one `compartment_id`.

An `OpeningHistory` is an ordered list of distinct openable compartments. A compartment may appear at most once. Re-closing/re-opening is not part of authoritative puzzle history.

A history therefore defines both:
- which compartments were opened;
- the order in which they were first opened.

Any compartment omitted from the list remains unopened for that run.

## 2.6 Checkpoint
Checkpoint `i` is the resolved state immediately after opening history step `i` and applying every tear caused by that opening.

There is one checkpoint per opening step. No checkpoint exists between individual seal tears caused by the same opening.

Checkpoint 0 is the pre-opening state and may be shown in UI, but target evidence uses checkpoints 1..N unless a tutorial explicitly checks initial installation.

## 2.7 Evidence target
An `EvidenceTarget` is a conjunction of allowed predicates from the frozen vocabulary in Section 7. It can inspect installed witness identity, exact break time, survival through time, final witness state, and explicitly authored opened/unopened compartment facts.

Evidence never invokes hidden narrative facts or free-text interpretation.

## 2.8 Player-edit state
Before commit, the mutable submission state consists only of:
- tentative installed socket set;
- tentative opening-history choice/order where the case exposes history editing;
- UI focus/selection state, which has no mechanical meaning.

Committed simulation state is separate and immutable except by replay/reset/undo-to-edit.

---

# 3. Socket legality and seal placement

## 3.1 General legality
A socket is mechanically legal iff:
1. its `covered_seams` set is non-empty;
2. every seam ID exists;
3. its derived `trigger_compartments` set is non-empty;
4. it is enabled for the case;
5. the socket geometry can visibly communicate every covered seam under the presentation rules later.

A socket that would never be crossed by any openable compartment is invalid content, not an intentionally surviving witness.

## 3.2 Placement legality
At most one seal occupies one socket. A player may install seals only in enabled sockets.

Case placement modes:
- `FIXED`: authored installed socket set; player cannot change it;
- `CHOOSE_EXACT_K`: player must install exactly K sockets;
- `CHOOSE_UP_TO_K`: permitted only for an authored reason and should be rare; certifier must prove solutions cannot win by trivial under-placement;
- `CHOOSE_FROM_GROUPS`: optional later content tool where finite authored groups specify e.g. exactly one of group X, but it is not required for campaign floor and must pass anti-bookkeeping review.

Default for player-placement cases is `CHOOSE_EXACT_K`.

## 3.3 No crossing multiplicity
If one opening traverses two or more seams covered by the same socket, that seal still breaks once at that checkpoint. Multiplicity has no extra effect.

If several installed seals are triggered by one opening, all of them receive the same `break_checkpoint`.

---

# 4. Canonical opening-history model

## 4.1 Core constraints
Every committed history must satisfy:
- length within authored `[min_steps, max_steps]`;
- each referenced compartment exists and is openable;
- no compartment repeats;
- any `required_open` compartment appears;
- any `forbidden_open` compartment does not appear;
- any authored fixed position/precedence constraints are satisfied.

The history is always finite and fully knowable before commit. There is no randomness or AI event selection.

## 4.2 History control modes
Only four modes are canonical:

### `FIXED_HISTORY`
The full history is authored and visible. Player solves seal placement/evidence reading only.

### `CHOOSE_FROM_AUTHORED_HISTORIES`
Player selects one history from a small visible finite list. Useful for tutorials or readability-sensitive mixed cases.

### `ARRANGE_REQUIRED_SET`
A fixed visible set of compartments must all be opened exactly once; player chooses their permutation.

### `ARRANGE_BOUNDED_SUBSET`
Player chooses a subset and order subject to explicit bounds, e.g. open exactly 4 of 5 compartments. This is the canonical way to create an unopened-compartment deduction.

Do not add arbitrary hidden branching, conditional events, repeated openings or simultaneous multi-compartment steps in v1.

## 4.3 Optional unopened compartments
A compartment is unopened iff absent from the committed history. The number of omitted compartments is determined by history bounds.

For complement reasoning to remain legible, authored cases using omitted compartments must expose the exact history length (for example, “open exactly four of five”). The player must never have to infer an unstated number of omissions.

## 4.4 Fixed/partial constraints
A case may visibly pre-lock a position or precedence relation, e.g. `A before D` or `B is checkpoint 3`. These are input constraints, not evidence predicates. They narrow legal histories before solving.

Use sparingly: more than two independent pre-lock rules in one case requires an anti-bookkeeping review.

---

# 5. Authoritative commit and checkpoint resolution

Given legal installed set `S` and legal history `H`:

## 5.1 Initial state
At commit:
1. copy tentative submission into an immutable run snapshot;
2. every installed witness becomes `INTACT`, `break_checkpoint=NONE`;
3. every compartment becomes `CLOSED/UNOPENED`;
4. clear prior run evidence;
5. set checkpoint counter to 0.

## 5.2 For each opening step i = 1..N
Resolve in this exact order:
1. increment checkpoint to `i`;
2. identify the single compartment `c = H[i]`;
3. mark `c` opened for historical state;
4. compute `T = c.traversed_seams`;
5. collect **all currently intact** installed seals whose `covered_seams intersects T`;
6. atomically set every collected seal to `BROKEN` with `break_checkpoint=i`;
7. seals broken earlier remain broken and never change break time;
8. materialize the complete checkpoint snapshot;
9. evaluate/display any evidence predicates whose observation point is checkpoint `i`;
10. only after the snapshot is authoritative may presentation continue to the next opening step.

The visual order in which multiple strips animate tearing within one checkpoint has zero mechanical meaning.

## 5.3 Simultaneous crossing rule
There are no simultaneous compartment openings. “Simultaneous” in this design means several seams and/or several seals are crossed by the one atomic compartment opening at the same checkpoint. They all resolve as one unordered tear set.

This avoids accidental sub-order deductions from animation.

## 5.4 Already-broken seals
A broken seal is inert for future checkpoint mechanics. Later qualifying openings do not update, re-break, score or annotate it.

## 5.5 End state
After final checkpoint:
- every opened compartment remains historically opened;
- every omitted compartment is `UNOPENED`;
- every unbroken installed witness is `INTACT` with break time `NEVER`;
- target predicates are evaluated against the full run trace.

---

# 6. Replay, reset, retry and undo transaction semantics

## 6.1 Commit is a transaction boundary
Pre-commit editing and committed resolution never interleave.

Once COMMIT begins:
- placement/history editing is locked;
- the run resolves from the immutable snapshot;
- animation skip/fast-forward may alter only presentation timing.

## 6.2 Replay
`REPLAY` replays the same committed snapshot and therefore must produce the exact same checkpoints and evidence. It never re-randomizes anything.

## 6.3 Return to edit / undo
After or during a committed presentation, `RETURN TO EDIT` aborts presentation if needed and restores the exact tentative placement/history that produced that commit. No torn state leaks back into edit state.

The player may then make edits. Ordinary undo/redo acts on edit transactions only:
- place/remove/move one seal = one transaction;
- reorder one history card operation = one transaction;
- selecting a different authored history = one transaction.

Undo never steps backward through simulated tear checkpoints. Replay/scrub handles evidence inspection; edit undo handles solution construction.

## 6.4 Reset
Two reset scopes are canonical:
- `RESET RUN`: replay committed setup from checkpoint 0; no edit loss;
- `RESET CASE`: restore authored initial edit state after confirmation if meaningful progress exists.

## 6.5 Failure semantics
There is no irreversible gameplay fail state. An incorrect submission produces a deterministic mismatch report after commit and the player can inspect/replay then return to edit.

No lives, timer penalty, score loss or lockout.

---

# 7. Frozen evidence predicate vocabulary

V1 authored targets may use only the following mechanical predicates.

## 7.1 Seal installation predicates
1. `INSTALLED(socket)` — witness exists at socket.
2. `NOT_INSTALLED(socket)` — witness absent.

Use mainly when installation itself is part of the evidence target; do not redundantly restate an exact-K placement rule.

## 7.2 Exact break predicates
3. `BREAKS_AT(socket, i)` — installed witness first breaks at checkpoint i.
4. `BREAKS_BEFORE(socket, i)` — break checkpoint < i.
5. `BREAKS_AFTER(socket, i)` — witness is still intact through checkpoint i and breaks later within the history.

`BREAKS_BEFORE/AFTER` are allowed only when they create interval/lower-bound deductions. Do not use them merely to make evidence cards look varied.

## 7.3 Survival/state predicates
6. `INTACT_THROUGH(socket, i)` — installed witness is intact after checkpoint i.
7. `FINAL_INTACT(socket)` — installed witness never breaks in the committed history.
8. `FINAL_BROKEN(socket)` — installed witness breaks at some checkpoint.

## 7.4 Compartment-history predicates
9. `OPENED(compartment)` — compartment appears somewhere in history.
10. `UNOPENED(compartment)` — compartment is omitted.
11. `OPENS_AT(compartment, i)` — compartment is the opening at checkpoint i.

These are allowed as explicit target facts only in limited tutorial/reconstruction cases. They must not become a second puzzle system that simply gives away the history.

## 7.5 Equality/comparison predicates between witnesses
12. `SAME_BREAK_STEP(socket_a, socket_b)` — both break and their exact first-break checkpoint is equal.
13. `BREAKS_EARLIER(socket_a, socket_b)` — both break and A's break checkpoint < B's.

These comparison predicates are retained because they support paired-witness discrimination without requiring numeric checkpoint labels on every card.

## 7.6 Explicitly rejected predicate inflation
Not canonical for v1:
- counts such as “exactly 3 broken” as a primary target;
- sums/scores/weights;
- parity;
- arbitrary colors/types with rule meaning;
- damage percentage;
- “almost broken” states;
- probabilistic tear claims;
- narrative truth/lie predicates;
- adjacency of break animations;
- exact animation order among same-checkpoint seals;
- hidden predicates revealed only after commit.

A future predicate may enter only if playtest demonstrates a qualitatively new deduction class and the design freeze is deliberately reopened.

---

# 8. Solve acceptance, equivalence and uniqueness

## 8.1 Primary acceptance rule
A submission solves a case iff:
1. placement and history are legal;
2. deterministic resolution completes;
3. every authored evidence predicate evaluates true.

The game does **not** require matching a secretly stored canonical solution unless the case explicitly contains a uniqueness gate for design certification.

## 8.2 Mechanical equivalence
Two submissions are mechanically equivalent for certification if all differences are irrelevant to every future rule and target observation.

For v1, canonical equivalence is determined by a normalized solution signature:
- installed socket set;
- opening history after removing no steps — history order is normally mechanically meaningful;
- full per-socket break-time vector including `NEVER`;
- opened/unopened set.

Two histories that differ in order but produce the same complete break-time vector are **not automatically equivalent**, because the opening order itself may be an exposed solution object and future compartment predicates can distinguish them.

A case author may declare a narrower `acceptance_projection` that intentionally ignores specified history positions or witnesses when those variables are truly mechanically unobserved. Example: if two unopened decorative candidates are outside all witness trigger sets and no target references them, their relative non-event has no order because they are absent anyway.

## 8.3 Uniqueness policy
Player-facing success accepts every satisfying submission.

Certification classifies cases as:
- `UNIQUE_EXACT`: exactly one normalized satisfying submission;
- `UNIQUE_OBSERVABLE`: multiple satisfying submissions exist but all map to one declared observable equivalence class;
- `MULTI_VALID_INTENTIONAL`: several materially different solutions are deliberately allowed and documented;
- `INVALID_AMBIGUOUS`: multiple materially different solutions exist unintentionally.

Default for authored campaign cases is `UNIQUE_EXACT` or `UNIQUE_OBSERVABLE`. `MULTI_VALID_INTENTIONAL` is permitted only when the learning goal benefits from freedom and the UI does not imply a unique reconstruction.

## 8.4 Certifier requirement
The offline/content certifier must enumerate or otherwise exhaustively prove all legal placement/history submissions within authored bounds, evaluate the same authoritative resolver, group satisfying submissions by declared equivalence, and emit the classification above plus trace signatures.

Runtime and certifier may be implemented separately later, but Phase 8 must require one shared rules contract and cross-tests so their results cannot drift.

---

# 9. Preview / oracle boundary

The player may inspect before commit:
- all compartment labels and traversed seams;
- all enabled sockets and each socket's covered seams;
- derived “this socket can be crossed by A/C/etc.” explanation on focus;
- placement budget and all legal history bounds;
- fixed/required/forbidden opening constraints;
- target evidence predicates;
- consequences of **already committed** history during replay/scrub.

The pre-commit UI may also reject structurally illegal actions immediately (duplicate compartment in history, over-budget seal, disabled socket).

The pre-commit UI must **not**:
- simulate tear results for the tentative full history;
- display predicted break checkpoint for a tentative witness;
- mark a tentative order as closer/farther from target;
- count unsatisfied future evidence predicates live;
- highlight “good” sockets, forced openings or contradictions discovered by solver reasoning;
- expose number of remaining solutions;
- auto-complete forced deductions.

A focused socket may visually highlight its authored covered seams/trigger compartments because that is static geometry, not an oracle.

After commit, replay may explain exactly why a seal broke: “checkpoint 2: compartment C crossed seam m3 covered by S4.” Explanation is retrospective and safe.

---

# 10. Difficulty knobs

Valid difficulty knobs manipulate coupling, not just quantity:
1. number of overlapping trigger sets among active sockets;
2. degree of trigger-set intersection/divergence;
3. fixed history vs authored-history choice vs permutation vs bounded subset;
4. seal-placement fixed vs chosen;
5. number of temporal checkpoints actually referenced by evidence;
6. exact break predicates vs interval/survival/comparison predicates;
7. presence of one known omission (`ARRANGE_BOUNDED_SUBSET`);
8. number of deduction classes required in the shortest human solution;
9. decoy sockets that are geometrically plausible but eliminated by cross-witness reasoning;
10. placement/history coupling: whether choosing a witness changes which histories can satisfy evidence.

Weak knobs that do not count as new depth:
- larger cabinet alone;
- more labels alone;
- more seals with independent trigger sets;
- more evidence cards that repeat the same fact;
- denser graphics;
- longer histories without new overlap structure.

Recommended campaign bounds to carry into Phase 5:
- compartments: usually 3–6, hard provisional ceiling 7;
- enabled sockets: usually 3–12, hard provisional ceiling 14;
- installed seals: usually 1–6, hard provisional ceiling 7;
- checkpoints: usually 1–5, hard provisional ceiling 6;
- omitted compartments: normally 0 or 1; more than 1 requires explicit adversarial review.

These are content/scope ceilings, not balance promises; Phase 5 may lower them but should not raise them without reopening Phase 4 risk review.

---

# 11. Hard authored-content validity gates

Every substantive non-tutorial case must pass all applicable gates:

1. **Temporal gate:** at least two checkpoints matter to the target/solution.
2. **Witness interaction gate:** at least two installed/candidate witnesses have overlapping or otherwise coupled trigger sets; fully independent witnesses are tutorial material.
3. **Reasoning gate:** shortest intended human solution uses at least two Round-C deduction classes in midgame and at least three in late game.
4. **No final-state collapse:** a solver using only final broken/intact sets must leave multiple candidate submissions for any case whose intended deduction is temporal.
5. **No live-bruteforce gate:** case must remain reasonably solvable without hypothetical live scoring.
6. **No decorative predicate gate:** removing a target predicate must either change the legal solution class or its intended deduction path; redundant evidence is allowed only for explicit teaching emphasis.
7. **Observable geometry gate:** every trigger relationship used in reasoning must be inspectable without hidden rules.
8. **Certifiability gate:** legal submission space must be finite and exhaustively tractable offline under Phase-8 implementation assumptions.
9. **Ambiguity gate:** case must certify as `UNIQUE_EXACT`, `UNIQUE_OBSERVABLE`, or documented `MULTI_VALID_INTENTIONAL`; accidental ambiguity fails.
10. **Anti-parameter gate:** increasing counts alone cannot justify the case's campaign slot.

Round-C deduction classes used for tagging:
- `DIRECT_CAUSE`;
- `FIRST_CROSSED`;
- `INTERSECTION_TRIANGULATION`;
- `PAIRED_DISCRIMINATION`;
- `SURVIVORSHIP_COMPLEMENT`;
- `DELAYED_BREAK_BOUND`;
- `INVERSE_WITNESS_PLACEMENT`;
- `HISTORY_RECONSTRUCTION`;
- `PLACEMENT_HISTORY_COUPLING`.

Every case record in Phase 5 must declare its required/intended deduction tags.

---

# 12. Canonical mechanical examples

These examples are rule proofs, not guaranteed shipping levels.

## Example M1 — shared seam, same-checkpoint atomic tear
Seams: `mA`, `mB`.
- compartment A traverses `{mA}`;
- compartment B traverses `{mB}`.
Sockets:
- S1 covers `{mA}`;
- S2 covers `{mA,mB}`.
Installed: S1,S2. History: A,B.

Resolution:
- checkpoint 1 opens A -> both S1 and S2 break at 1 atomically;
- checkpoint 2 opens B -> S2 is already broken; no state change.

No animation ordering between S1/S2 can create evidence.

## Example M2 — divergent witnesses identify cause
Seams map so:
- Sx trigger compartments = `{A,C}`;
- Sy = `{A,D}`.
History length 3. Evidence:
- `BREAKS_AT(Sx,1)`;
- `BREAKS_AT(Sy,3)`.

A cannot be checkpoint 1, because that would also break Sy at 1. Therefore C is checkpoint 1. If Sy breaks at 3 and A is the only remaining trigger opened by then, A is localized later. This proves paired discrimination from one shared cause plus divergent causes.

## Example M3 — omitted compartment / survivor
Compartments A,B,C,D; open exactly 3 of 4.
Sockets:
- S1 triggers `{B}`;
- S2 triggers `{B,D}`.
Evidence:
- `FINAL_INTACT(S2)`.

Because exactly one compartment is omitted, both B and D cannot simultaneously be omitted. Therefore this placement/evidence combination is impossible for any legal 3-of-4 history. The certifier rejects it as zero-solution content. This demonstrates that survival can prove impossibility, not just identify a late event.

A valid variant uses S2 trigger `{D}`; `FINAL_INTACT(S2)` then forces D to be the unique omission.

## Example M4 — delayed multi-trigger lower bound
History opens all A,B,C,D. Socket S triggers `{B,C}` and target is `BREAKS_AT(S,4)`.

This immediately forces whichever of B/C occurs first to be checkpoint 4, but since both must appear somewhere and there is only one checkpoint 4, the case is impossible. Thus exact late break on a multi-trigger witness can certify contradiction unless some trigger compartments are omittable.

If history instead opens exactly 3 of 4, the same predicate can be feasible only if one of B/C is omitted and the other is checkpoint 4 (where history length is 4 only if five compartments exist). Authors must reason from exact bounds, not assume “late” is always possible.

## Example M5 — placement/history coupling
Compartments A,B,C; history is any permutation of all three.
Candidate sockets:
- S1 triggers `{A,B}`;
- S2 triggers `{A,C}`;
- S3 triggers `{B}`;
Choose exactly 2. Target:
- one installed witness breaks at checkpoint 1;
- the other breaks at checkpoint 2;
- their identities are specified as `BREAKS_AT(S2,1)` and `BREAKS_AT(S3,2)`.

Choosing S2+S3 admits histories beginning C then B (A later): S2 breaks on C at 1, S3 on B at 2. Choosing S1+S3 can never satisfy the specified identity target because S2 is absent. Placement therefore changes the viable history family; this is not merely solving order after witnesses are fixed.

---

# 13. Adversarial edge cases and rulings

## E1 — socket covers seam no opening traverses
Invalid case data. Certifier/schema validation fails before puzzle certification.

## E2 — compartment traverses same seam twice visually
Mechanically seam membership is a set. Duplicate visual crossings cannot create multiple tears.

## E3 — seal covers two seams both crossed by one opening
Break once at that opening's checkpoint.

## E4 — two compartments share a seam
Allowed if geometry communicates it. Opening either may tear a socket covering that seam. This is useful for shared-cause witnesses.

## E5 — already-broken seal crossed again
No change; original break checkpoint remains authoritative.

## E6 — zero installed seals
Allowed only in a dedicated tutorial explaining placement UI; never substantive content. A CHOOSE_EXACT_K case should normally have K>=1.

## E7 — history length zero
Not shipping puzzle content. Schema may permit it for unit tests only; campaign cases require at least one checkpoint.

## E8 — target references non-installed witness
Predicates requiring state (`BREAKS_AT`, `FINAL_INTACT`, etc.) evaluate false when that socket is not installed. Authors must use `NOT_INSTALLED` when absence itself is the desired fact.

## E9 — `SAME_BREAK_STEP` when both never break
False. “Same break step” requires both to break. Final co-survival is represented with `FINAL_INTACT` predicates.

## E10 — `BREAKS_EARLIER` when one never breaks
False. The predicate compares two actual finite break checkpoints; it does not treat NEVER as infinity. Use survival predicates for that reasoning.

## E11 — commit with illegal setup
Commit is disabled with a structural explanation. Illegal edits are not simulated and do not count as failed attempts.

## E12 — skip animation immediately after commit
Rules resolve to the exact same trace and target result. Animation is never authority.

## E13 — player exits mid-animation
Persistence requirements later must save either pre-commit edit snapshot plus committed submission, or a completed deterministic run trace. Reload may safely recompute the run from committed submission; it must never persist a half-torn authoritative state.

## E14 — multiple valid solutions
All satisfy success. UI must not say “the unique history” unless certification class guarantees it.

## E15 — evidence card is logically redundant
Permitted only for an explicit teaching case and tagged as teaching redundancy. Mid/late content fails the no-decorative-predicate gate.

---

# 14. Mechanical acceptance tests for later implementation

Phase 8 must turn these into automated tests:
1. resolver determinism for identical case + submission;
2. break time equals first triggering checkpoint or NEVER;
3. multiple trigger seams in one opening still produce one break;
4. multiple seals at one checkpoint share index with no sub-order;
5. broken witness never changes break time;
6. omitted compartments never trigger witnesses;
7. replay produces byte/logically identical trace;
8. return-to-edit restores pre-commit submission exactly;
9. all evidence predicates match truth tables including absent-witness behavior;
10. certifier and runtime resolver agree on every enumerated submission for fixture cases;
11. equivalence grouping matches declared acceptance projection;
12. illegal histories/placements cannot commit;
13. animation skip cannot affect outcome;
14. structural data validator rejects dead sockets, unknown seams, duplicate IDs and impossible fixed constraints.

---

# 15. Phase-4 freeze decisions

Frozen now:
- seam-backed geometry with derived trigger-compartment sets;
- one atomic compartment opening per checkpoint;
- irreversible first-trigger tear rule;
- no tear multiplicity/durability/randomness;
- socket is the canonical witness identity;
- four bounded history-control modes;
- explicit omitted compartments via bounded history length;
- atomic checkpoint resolution and same-checkpoint tear set;
- edit/commit/replay separation;
- complete v1 evidence predicate vocabulary;
- non-oracular preview boundary;
- success by predicate satisfaction, not hidden canonical answer;
- explicit exact/observable/multi-valid certification classes;
- Round-C deduction tags and hard content validity gates;
- provisional mechanical ceilings for Phase 5.

Not frozen here because they belong to later phases:
- exact shipping case list/count distribution beyond floor/target;
- visual layout, controls, evidence-card composition and animation timing;
- progression/unlock sequence;
- pricing/demo commercial details;
- engine/runtime architecture;
- exact save schema.

## Phase 4 verdict
**PASS — MECHANICAL ARCHITECTURE COMPLETE.**

The system is deterministic, finite, non-physics-authoritative and internally coherent. The central risk is no longer rule ambiguity; it is content repetition. Phase 5 must therefore prove that 24–30 authored cases can be distributed across the frozen deduction classes without padding, predicate inflation or count-only escalation.

Next phase: **Phase 5 Content Architecture** — define campaign acts/families, case schema, floor/target counts, demo subset, authored-content production pipeline, certifier metadata, tutorial/reuse rules, difficulty progression and expansion boundaries; construct a concrete 24-case minimum campaign map and a 30-case target map before allowing Phase 6.