# GAME #011 — MISSING STEP — PHASE 5 CONTENT ARCHITECTURE

Date: 2026-09-01
Status: **PHASE 5 CONTENT ARCHITECTURE COMPLETE**
Authority: `START_HERE.md` -> `STATUS.md` -> `GAME_INDEX.md` -> Phase-2 history -> `GAME11_PRODUCT_THESIS.md` -> `GAME11_MECHANICAL_ARCHITECTURE.md` -> this file for launch content structure.

This phase does not change Phase-4 mechanics. It answers how a full campaign is authored, certified, paced, deduplicated and kept varied with exactly one workpiece and the frozen four-opcode vocabulary.

---

## 1. Canonical authored case schema

Every shipping case is data, not bespoke code. Minimum conceptual schema:

```text
case_id: stable string
case_data_version: integer
case_rules_version: integer
act_id / ordinal: campaign placement
working_title: localization key
teaching_tags: ordered list
challenge_family_tags: subset F1..F6
tracks:
  - track_id: A..D
    start_token_id: stable token ID
    tokens: [{token_id, opcode}]
initial:
  lane: 0|1
  orientation: N|E
  clamp_active: bool (normally false)
horizon_ticks: 4..24
edit_contract:
  type: SINGLE | TWO_NAMED_TRACKS
  editable_tracks: [...]
  eligible_token_ids_by_track: {...}
target:
  conjunction of Phase-4 predicate grammar only
presentation:
  focus_hint: optional non-solver tutorial callout
  camera/layout preset: semantic preset only
certificate_ref: exact artifact ID/hash
```

Authoring invariants:
- every token ID is stable and unique inside a case even when opcode duplicates;
- every editable track retains >=2 tokens after every legal deletion;
- authored start anchor uses token ID, never numeric position alone;
- eligibility is explicit and mechanically visible;
- no content row can override A->D execution order or opcode semantics;
- no case-local script, hidden trigger, special material, fifth opcode, second workpiece or secret predicate exists;
- launch default initial counters are zero and initial clamp false; any exception requires a visible tutorial reason and is disfavored.

### Certified artifact schema
A certificate is generated from canonical serialized case data + `case_rules_version` and stores:
- case hash and certificate format version;
- legal edit-set count;
- for every legal edit set: selected token IDs, post-edit track signatures, full trace hash, compact trace signature, final lane/orientation/stamp/blocked values, success, first monotone fail if any;
- raw successful edit-set count;
- behaviorally distinct successful-trace count;
- equivalence groups;
- uniqueness band;
- difficulty feature vector;
- duplicate/near-duplicate fingerprints;
- validator build/rules hash.

A case cannot enter campaign manifests unless its certificate matches its exact case hash and rules version.

---

## 2. Launch campaign shape — 6 acts

Target campaign: **42 certified cases**. Launch floor: **36 strong certified cases** if curation kills weak candidates late. The product must not pad back to 42 with near-duplicates.

### Act I — THE GAP — 6 cases
Learning delta: DELETE is destructive but loop closure is the real effect.
- one editable track first;
- horizon 4–7;
- normally 3-token track;
- introduce PUSH, TURN and STAMP physical consequences;
- second track appears by the end only as a simple visible cadence;
- family emphasis: F1 period contraction, basic F3 parity.

Gate: player can explain why deleting TURN changes *when PUSH/STAMP recur*, not merely that TURN disappeared.

### Act II — WINDOWS — 7 cases
Learning delta: a new period is good or bad relative to another track.
- introduce/foreground CLAMP next-tick latch;
- horizons 6–10;
- two tracks normally;
- family emphasis: F2 clamp-window avoidance + F1 recurrence;
- first deceptive-prefix cases where ticks 1–3 look correct but later recurrence fails.

Gate: player reads the shared timeline rather than judging only first cycle.

### Act III — WHICH ONE? — 7 cases
Learning delta: identical opcode names are not identical edits.
- duplicate opcode positions become deliberate;
- non-zero visible start anchors may appear;
- 2–3 tracks;
- family emphasis: F4 positional duplicate deletion + F3 orientation parity;
- targets reach 3 clauses regularly.

Gate: player reasons about cyclic position and surviving order, not “delete a PUSH.”

### Act IV — SAME TICK — 7 cases
Learning delta: recurrence controls which operations meet, and A->D determines their physical order.
- same-tick STAMP/PUSH/TURN interactions become central;
- 2–4 tracks but keep <=10 legal single deletions for most cases;
- family emphasis: F5 same-tick choreography plus F2/F3;
- first cases in which two candidate deletions produce similar schedules early but different workpiece traces.

Gate: player can explain an outcome using both column alignment and A->D order.

### Act V — FALSE FRIENDS — 7 cases
Learning delta: locally sensible deletion can create a globally wrong beat.
- horizons 10–18;
- 3–4 target clauses;
- stronger deceptive-prefix similarity;
- combine F1–F5 without adding rules;
- duplicate positions, clamp windows and parity deliberately cross.

Gate: player tests a hypothesis across the whole horizon and can diagnose a late divergence.

### Act VI — TWO ABSENCES — 8 cases
Learning delta: two edited periods co-determine one rhythm.
- introduce `TWO_NAMED_TRACKS` with exactly one deletion on each;
- first mastery case has 3×3=9 pairs; later cases may reach 6×6=36;
- family emphasis: F6 coupled two-delete beat frequency, then combinations with F2/F4/F5;
- no third deletion and no expansion of operation vocabulary.

Final gate: solve coupled rhythms by understanding interaction, not exhaustive trial. Campaign climax should visually echo the core hook: two tiny removals make a seemingly impossible machine settle into a clean repeating cadence.

### Count map
6 + 7 + 7 + 7 + 7 + 8 = **42 target cases**.

A 36-case floor may contract the middle acts, but must preserve:
- >=5 Act-I teaching cases;
- >=5 Act-II clamp/recurrence cases;
- >=5 Act-III positional/parity cases;
- >=5 Act-IV same-tick cases;
- >=6 Act-V synthesis cases;
- >=7 Act-VI two-delete mastery cases.

---

## 3. Demo subset

Target demo: **8 cases / roughly 20–35 minutes for a first-time puzzle player**, subject to Phase-7 commercial validation.

Demo curriculum:
1. one-track deletion/closure;
2. recurrence count;
3. second-track cadence;
4. CLAMP next-tick window;
5. deceptive bad-looking-step case;
6. duplicate-position distinction;
7. same-tick choreography;
8. compact 3×3 two-delete teaser.

The demo must expose the complete product identity. It must not end before recurrence becomes cross-track reasoning. Demo content should be a subset of full-game canonical cases rather than separate mechanics or “demo-only” rules.

---

## 4. Generator / search / validator pipeline

The content pipeline is **candidate generation -> exact certification -> structural filtering -> similarity filtering -> human curation -> campaign placement -> recertification**.

### 4.1 Candidate generation
Generator/search may vary only frozen knobs:
- track count and lengths;
- opcode sequences from PUSH/TURN/STAMP/CLAMP;
- start anchors;
- editable tracks and eligible token IDs;
- horizon;
- initial lane/orientation;
- target conjunction chosen from observed candidate outcomes.

It may use constructive generation: choose a legal edit, simulate its trace, derive a target from a subset of its final values, then enumerate all edits and retain only desired uniqueness/difficulty bands.

### 4.2 Hard rejection before human review
Reject automatically if any applies:
- UNSAT;
- EQUIVALENT_MULTI for normal campaign;
- TRACE_MULTI unless explicitly admitted to late open-solution content (launch campaign default: reject);
- legal edit count <3 outside first tutorials;
- legal edit count >12 for ordinary single-delete campaign content without explicit late-act justification;
- mastery pair count <9 or >36;
- solution can be identified solely because only one eligible token has a required opcode and deletion trivially removes it, unless it is an Act-I teaching case;
- solution trace reaches target without a meaningful recurrence/re-phasing difference from failed candidates;
- horizon >24;
- any track >6 original tokens;
- post-delete track <2;
- certificate/version mismatch;
- monotone target can be decided before re-phasing matters in a non-tutorial case;
- target has >4 clauses or uses grammar outside Phase 4.

### 4.3 Duplicate and near-duplicate detection
Exact duplicate fingerprint:
- normalize track labels only where relabeling does not alter A->D semantics;
- retain opcode cyclic order, start anchors, edit contract, horizon, initial state and target;
- compare certificate trace sets.

Near-duplicate score uses:
- same solution opcode/position pattern;
- same post-edit period vector;
- same horizon and target shape;
- same successful trace signature after harmless token-ID renaming;
- same first-divergence tick distribution among closest failed edits;
- same family/tag vector.

Automatic curation rule: if two candidates have identical successful trace signatures and >=0.85 normalized structural similarity, keep at most one unless their teaching purpose is explicitly different. Campaign neighbors must not share both the same solution-period vector and the same dominant trap.

### 4.4 Human-curation obligations
The solver proves correctness, not fun. A human pass must verify:
- the intended insight is perceptible without brute-force enumeration;
- failure is visually explainable;
- the solution feels caused by period re-phasing;
- no misleading decorative motion implies nonexistent rules;
- two visually identical tokens are positionally distinguishable;
- target wording and timeline fit 1280×800/150% text constraints;
- the case adds a learning or synthesis delta relative to adjacent campaign cases;
- RUN animation duration does not make retries tedious.

A mathematically unique but ugly or clerical case is rejected.

---

## 5. Difficulty bands

Difficulty is certificate-derived and then human-calibrated. No single scalar is treated as truth.

### Feature vector
`D = {legal_edits, pair_space, track_count, editable_track_count, post_edit_period_vector, recurrence_count_within_horizon, LCM_visibility, horizon, target_clause_count, exact_count_clause_count, duplicate_opcode_positions, clamp_active_tick_count, same_tick_interaction_count, first_decisive_divergence_tick, deceptive_prefix_length, solution_vs_nearest_failure_trace_distance}`.

### Band 0 — EXPLAIN
- 3–4 legal edits;
- horizon <=6;
- 1–2 tracks;
- 1–2 target clauses;
- no duplicate-position ambiguity;
- decisive difference appears early.

### Band 1 — READ THE LOOP
- 3–6 edits;
- horizon <=9;
- 2 tracks typical;
- recurrence/CLAMP matters;
- target 2–3 clauses;
- deceptive prefix <=2 ticks.

### Band 2 — COMPARE RHYTHMS
- 5–9 edits;
- 2–3 tracks;
- horizon 7–14;
- duplicate opcode or parity/same-tick interaction;
- target 2–4 clauses;
- closest wrong candidate may match useful behavior for 3–5 ticks.

### Band 3 — SYNTHESIZE
- 6–12 single-delete choices;
- 3–4 tracks or dense two-track interaction;
- horizon 10–18;
- >=2 challenge families materially contribute;
- deceptive prefix may reach 6 ticks;
- target normally 3–4 clauses.

### Band 4 — COUPLED MASTERY
- exactly two named editable tracks;
- 9–36 edit pairs;
- horizon 9–18 typical, <=24 hard ceiling;
- coupled recurrence is necessary;
- >=2 meaningful interaction families beyond raw pair search;
- certificate uniqueness plus human evidence that preview permits reasoning rather than brute-force clicking.

Difficulty is never raised by hiding state, slowing RUN, disabling reset, tiny UI or adding operation families.

---

## 6. Representative certified case skeletons

These 12 cases are **content-architecture witnesses**, not automatically final campaign levels. Token IDs are positional (`A1...`, `B1...`). Unless stated otherwise, all tokens on A are eligible, B is fixed, start anchors are token 1, initial lane0/N, clamp false, and target is the exact four-value tuple `(final lane, orientation, stamps, blocked)` shown. Exhaustive enumeration under the Phase-4 simulator was used to verify that the stated edit or edit pair is the only edit set producing that full target tuple. Final authored levels still require persisted validator certificates before shipping.

### C01 — First Closure — Band 0 / F1
- A `[PUSH, TURN, STAMP]`; horizon 4.
- delete **A2 TURN**.
- target `(lane0, N, stamps1, blocked0)`.
- unique among 3 legal deletions.
- lesson: a 3-step loop becomes 2; remaining actions recur sooner.

### C02 — Longer Echo — Band 0–1 / F1
- A `[PUSH, TURN, STAMP]`; horizon 6.
- delete **A2 TURN**.
- target `(lane1, N, stamps2, blocked0)`.
- unique among 3 edits.
- lesson: the same removal changes repeated count across a longer horizon.

### C03 — Which STAMP? — Band 2 / F4
- A `[TURN, STAMP, PUSH, STAMP, STAMP]`;
- B `[STAMP, CLAMP]`; horizon 9.
- delete **A2 STAMP**.
- target `(lane0, E, stamps4, blocked0)`.
- unique among 5 A deletions.
- lesson: deleting one of several identical opcodes is a positional choice.

### C04 — Clamp Roof — Band 2 / F2
- A `[CLAMP, STAMP, PUSH, STAMP]`;
- B `[STAMP, CLAMP, STAMP, STAMP]`; horizon 7.
- delete **A1 CLAMP**.
- target `(lane0, N, stamps4, blocked0)`.
- unique among 4 A deletions.
- lesson: contraction shifts future PUSH against next-tick clamp windows.

### C05 — Safe Window — Band 2 / F2
- A `[CLAMP, TURN, PUSH]`;
- B `[PUSH, STAMP, CLAMP, TURN]`; horizon 9.
- delete **A3 PUSH**.
- target `(lane1, N, stamps1, blocked0)`.
- unique among 3 A deletions.
- lesson: removing an action also changes the cadence of remaining CLAMP/TURN events.

### C06 — Parity Horizon — Band 2 / F3
- A `[PUSH, STAMP, PUSH, TURN, CLAMP, STAMP]`;
- B `[CLAMP, TURN]`; horizon 6.
- delete **A3 PUSH**.
- target `(lane0, N, stamps2, blocked0)`.
- unique among 6 A deletions.
- lesson: final orientation is a repeated parity consequence, not just “did TURN survive?”.

### C07 — Ordered Column — Band 2–3 / F5
- A `[PUSH, CLAMP, STAMP, STAMP, CLAMP, STAMP]`;
- B `[PUSH, TURN]`; horizon 7.
- delete **A2 CLAMP**.
- target `(lane0, E, stamps2, blocked0)`.
- unique among 6 A deletions.
- lesson: same-column PUSH/STAMP effects must be read in A->B order.

### C08 — Same Shape, Different Failure — Band 3 / F4+F2
- A `[CLAMP, PUSH, PUSH, STAMP, CLAMP]`;
- B `[CLAMP, PUSH, TURN, PUSH, STAMP]`; horizon 13.
- delete **A1 CLAMP**.
- target `(lane0, E, stamps3, blocked4)`.
- unique among 5 A deletions.
- lesson: duplicate PUSH rhythm and clamp cadence can make a late exact-count target distinguish superficially similar schedules.

### C09 — Two Absences I — Band 4 / F6
- A `[PUSH, PUSH, TURN, STAMP]`;
- B `[PUSH, CLAMP, PUSH, TURN]`; horizon 12.
- edit contract: one deletion on A and one on B; 16 pairs.
- delete **A3 TURN + B4 TURN**.
- target `(lane0, N, stamps4, blocked0)`.
- unique among 16 pairs. This is the Round-C canonical mastery witness.

### C10 — Two Absences II — Band 4 / F6+F3
- A `[TURN, PUSH, PUSH]`;
- B `[STAMP, PUSH, CLAMP, TURN, STAMP]`; horizon 12.
- 15 legal pairs.
- delete **A1 TURN + B3 CLAMP**.
- target `(lane1, E, stamps4, blocked0)`.
- unique among 15 pairs.
- lesson: one deletion fixes orientation cadence while the other changes hazard timing.

### C11 — Two Absences III — Band 4 / F6+F2
- A `[TURN, PUSH, STAMP]`;
- B `[STAMP, CLAMP, PUSH, PUSH, STAMP]`; horizon 8.
- 15 legal pairs.
- delete **A1 TURN + B2 CLAMP**.
- target `(lane0, N, stamps4, blocked0)`.
- unique among 15 pairs.
- lesson: coupled edits can remove a transform and a hazard yet depth comes from the resulting periods, not simple subtraction.

### C12 — Two Absences IV — Band 4 / F6+F5
- A `[STAMP, STAMP, TURN, CLAMP]`;
- B `[TURN, PUSH, CLAMP, CLAMP, TURN]`; horizon 9.
- 20 legal pairs.
- delete **A4 CLAMP + B1 TURN**.
- target `(lane1, E, stamps3, blocked0)`.
- unique among 20 pairs.
- lesson: coupled periods create same-tick physical ordering consequences while duplicate opcodes remain positional.

Witness-set result: tutorial, deceptive recurrence, duplicate-position, clamp-window, parity, same-tick-order and four two-delete mastery structures all exist without adding any mechanic.

---

## 7. Repetition / content-exhaustion attack

### Attack A — “Every answer is delete TURN”
Real risk: TURN is visually tempting to remove and appears in several early witnesses.
Mitigation is curation, not a new opcode. Across any rolling 8 campaign cases:
- no opcode family may be the successful deleted opcode in >4 cases;
- no exact token position pattern may solve >2 neighboring cases;
- mastery pair solutions must vary opcode-pair category and positional relationship.

This is a content-distribution rule, not a mechanical balancing rule.

### Attack B — brute-force every token
Single-delete search spaces are intentionally small, so brute force is always physically possible. The game cannot and should not prevent experimentation. Content quality instead requires:
- RUN/Reset fast enough that trying is painless;
- explanation strong enough that players learn from trials;
- later cases whose nearest failures share long deceptive prefixes, making blind enumeration less cognitively satisfying than understanding;
- achievements/commercial progression must never punish use of retries.

The game is a logic puzzle, not an anti-brute-force security system.

### Attack C — “It is modular arithmetic in a skin”
The content floor requires all six challenge families across the campaign, with F2/F4/F5 producing physical consequences not reducible to counting one period. At least 40% of Act III onward must combine two or more families, and at least half of Act IV onward must contain a same-tick, clamp-window, duplicate-position or coupled-edit consequence in addition to recurrence count.

### Attack D — horizons become tedious
Target authored horizon distribution:
- Acts I–II median <=8;
- Acts III–IV median <=12;
- Acts V–VI median <=16;
- only rare cases may reach 19–24 and must justify every extra tick through recurrence visibility.

RUN presentation may accelerate after a repeated prefix is understood, but simulation truth and certificate horizon never change.

### Attack E — target conjunction becomes arbitrary
Targets must arise from visible machine outcomes. Human curation rejects cases where a fourth clause exists only to force uniqueness. If uniqueness needs an unnatural target clause, regenerate the machine instead of adding arbitrary constraints.

### Attack F — generator produces mathematical sludge
Expected. Automated generation is a search assistant, not the designer. A low acceptance rate is acceptable. The release target is dozens of excellent cases, not millions of generated candidates.

---

## 8. Trace-variety sufficiency proof

A full campaign does not need a fifth opcode because its combinatorial content dimensions multiply before art/rule expansion:
- 1–4 tracks;
- 3–6 token positions on editable tracks;
- four opcode identities with positional duplicates;
- multiple visible start anchors;
- one-edit eligible sets spanning tracks;
- post-delete periods 2–5 from a six-token ceiling;
- relative recurrence/LCM relationships;
- horizons 4–18 normally;
- lane and orientation state;
- exact/ranged stamp/blocked outcomes;
- CLAMP next-tick windows;
- A->D same-tick choreography;
- single-delete vs bounded two-track coupled deletion.

More importantly, Phase 4 already proved six **reasoning families**, and this phase produced 12 exact witness skeletons covering all of them. The campaign architecture deliberately changes the question being asked—cadence, hazard window, parity, positional identity, intra-tick order, coupled beat—rather than only making tracks longer.

**Content sufficiency verdict: PASS.** No evidence justifies a fifth opcode, second workpiece, longer tracks, third deletion, hidden state or case-local rule.

---

## 9. Phase-5 acceptance gates
- Canonical authored case schema: PASS.
- Certificate/version contract: PASS.
- 5–7 act campaign: PASS — 6 acts.
- Minimum/target release count: PASS — floor 36 / target 42.
- Demo subset: PASS — 8-case curriculum.
- Generator/search/validator pipeline: PASS.
- Automatic rejection thresholds: PASS.
- Duplicate/near-duplicate detection: PASS.
- Human-curation obligations: PASS.
- Measurable difficulty bands: PASS — Bands 0–4.
- >=10 representative certified skeletons: PASS — 12 witness skeletons.
- Tutorial/deceptive/duplicate/clamp/parity/same-tick/two-delete coverage: PASS.
- Repetition/content-exhaustion attack: PASS with explicit curation rules.
- Four-opcode/single-piece vocabulary sufficiency: PASS.
- New mechanic required: **NO**.

**PHASE 5 COMPLETE.**

## Phase 6 handoff
Design UX/presentation around the frozen mechanical and content contracts. Must specify controller + mouse/keyboard flows, 1280×800/150% text layout, planning timeline, deletion/preview/RUN interaction, A->D ordering communication, CLAMP next-tick visualization, target comparison, failure/reset, onboarding across the first eight demo cases, pause/settings/save/load surface, accessibility, reduced motion, animation acceleration and audio/visual language. The UX must preserve the Preview non-oracle boundary and make positional duplicate tokens distinguishable without relying on color alone.