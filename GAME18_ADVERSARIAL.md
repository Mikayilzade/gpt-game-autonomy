# GAME #018 — PHASE 10 ADVERSARIAL REVIEW

Date: 2026-09-07
Game: **LOCAL TIME**
Status: PHASE 10 COMPLETE — PHASE 11 SPECIFICATION FREEZE NEXT
Production implementation: NO

Authority: all prior active Game #018 files, with `GAME18_SIMULATION.md` repairs P9-A/P9-B/P9-C binding. This pass attacks the design and makes only bounded clarifications/cuts; it adds no gameplay family.

## 1. Verdict
LOCAL TIME survives adversarial review. Its strongest risk is not technical feasibility but authored-content repetition and UI-assisted enumeration. The design remains worth freezing if Phase 11 treats 30 campaign cases + 8 mastery as the guaranteed quality floor and 36 + 12 only as a validated ceiling.

No new mechanic is required. The correct defense is stricter case topology, finite budgets, non-oracular presentation and cuts.

## 2. Fun / repetition attack
The core pleasure has three distinct beats: infer a causal necessity; commit spatial local-time coverage; watch persistent consequences free or constrain later placements. Repetition appears when two cases differ only in fiction, socket layout or tighter budgets.

Shipping rule: a later case survives only if its human proof introduces a materially different dependency topology. Changing labels, landmark skins, socket positions or move counts is insufficient.

Canonical count policy:
- 30 campaign = guaranteed design floor if all quality gates pass;
- 31–36 = conditional expansion slots;
- 8 mastery = baseline;
- M09–M12 = reserve only.

Store copy must not promise 36/12 until content validation/playtest proves them.

## 3. Similarity-cluster rulings
### 08 vs 19
Keep both only with this hard distinction:
- 08 = **choice topology**: safe narrow coverage exists, teaching that footprint choice can avoid risk.
- 19 = **necessity topology**: later broad hazardous coverage is unavoidable; a protection milestone must therefore precede it.
If authored 19 contains a safe narrow route that bypasses protection, cut 19.

### 14 vs 18 vs 29
- 14 = one current gate + prepared persistent cargo; isolates separation of preparation from departure.
- 18 = two simultaneous current predicates in one Snapshot0; clock geometry itself is not the main difficulty.
- 29 = two-clock spatial geometry where each clock has competing useful sockets; the proof must eliminate placements before dispatch.
If 29's proof reduces to "do 18 with two clocks," cut 29.

### 26 vs 27 vs 31
- 26 = persistence permits **one-way relocation**: earn A, permanently abandon A, use clock at B.
- 27 = same coupled arrangement is required twice but has different consequences because a persistent prerequisite changes between beats.
- 31 = two independent chains share one compatible exposure before a final current gate; proof is **shared work then restoration**, not simple relocation.
If authored 31 has only one meaningful chain, cut it.

### 32 vs 33 vs 36
- 32 = protection of destination must precede dispatch; isolate protected relay.
- 33 = fixed local-time zone creates a relay constraint that cannot be reproduced by simply moving both clocks.
- 36 = dependency braid: at least two independent persistent prerequisites feed departure, protection constrains one prerequisite/endpoint, handoff consumes a finite dispatch edge, and final coupled NOW state requires reallocating clocks after arrival.
Case 36 ships only if its written proof contains at least four nonredundant necessities and is not equivalent to 33 plus one extra prerequisite.

## 4. Anti-enumeration / preview attack
The legal action space is intentionally small, so brute force can never be eliminated mathematically. The design must make reasoning faster and more satisfying than scanning.

Frozen gate from Chapter 2 onward:
1. human proof states at least two causal necessities before socket choice where complexity permits;
2. at least one tempting action is ruled out by a public fact rather than trial;
3. preview shows coverage, NOW predicates, ambiguity and factual permanent-risk trigger only;
4. preview does not mark beneficial process transitions, future objective completion, future carrier state or recommended sockets;
5. warning language remains neutral: `Permanent consequence on Resolve`, never good/bad grading;
6. case is rejected if testers primarily sweep sockets looking for UI highlights rather than inspect rules.

Optional one-beat consequence preview may be prototyped only as an accessibility/comprehension experiment. It is rejected for default play if it measurably becomes a socket oracle.

## 5. Resolve-budget attack
Mandatory finite `resolve_limit` from P9-B is binding for every shipped case. A generous limit is still finite.

Three authored budget classes:
- **Teaching/generous:** limit prevents infinite state graph but is not intended difficulty.
- **Reasoning:** limit removes obvious waste/no-change spam but leaves >=1 beat of slack over the clean witness when practical.
- **Mastery-tight:** exact/tight budget is itself the puzzle and must be labeled as such.

Campaign difficulty may not rely mainly on counting wasted Resolves. If a normal case becomes interesting only at the globally shortest Resolve count, move that constraint to optional mastery or cut the case.

No-change Resolve remains legal and consumes one Resolve. UI always shows remaining budget before confirmation when failure is possible.

## 6. Carrier finite-state attack
P9-C is binding. Carrier-starting dispatch consumes a public finite departure edge/state.

Additional freeze clarifications:
- each carrier stage has a stable finite ID and can be consumed at most once unless a distinct later stage is authored;
- a carrier cannot be dispatched while already in a non-ready stage;
- payload capacity/occupancy is explicit authored state; dispatch legality rejects over-capacity rather than choosing payload by iteration order;
- simultaneous attempts to claim one exclusive payload/carrier are invalid authored definitions unless rules make the candidates mutually exclusive from Snapshot0;
- default arrival occurs after non-carrier commit and cannot satisfy default ACCEPT until the next Resolve;
- no carrier automatically continues moving merely because its previous dispatch predicates remain true;
- <=2 carriers is mastery/late synthesis territory; routing/pathfinding is out of scope.

Validator must reject ambiguous multi-dispatch ownership and any reachable carrier cycle not bounded by finite authored stages.

## 7. Snapshot0 / same-Resolve attack
Baseline shipped campaign sets `same_resolve_prerequisite=false` and `accept_on_arrival=false`. These flags are technical schema capabilities, not content toys.

Freeze rule: no campaign or mastery case may set either true unless Phase 4 is formally reopened and the behavior receives explicit onboarding. Therefore the base frozen content effectively forbids same-Resolve prerequisite chaining and accept-on-arrival.

Hazard precedence remains: lockout candidates and beneficial candidates are derived from Snapshot0; a protection earned in that Resolve cannot rescue an exposure in the same Resolve.

This removes an implementation ambiguity and prevents clever-looking but unreadable cascades.

## 8. Undo / persistence / cloud attack
P9-A is binding: puzzle undo can restore `beat_index`, placements, milestones, lockouts and carrier state, but cannot rewind persistence generation metadata.

Frozen persistence boundary:
- every persisted mutation creates a new monotonic `save_generation`;
- Undo Resolve followed by autosave is a newer save containing an older puzzle checkpoint state;
- restart followed by save is likewise a newer generation;
- cloud conflict compares validated generations/source markers, never infers puzzle advancement from beat count;
- demo import unions only safe monotonic profile facts and selects whole compatible checkpoints; it never field-merges puzzle state;
- achievement/completion intents use stable idempotency IDs, so undo/reimport cannot duplicate them.

No wall-clock timestamp decides a destructive merge by itself.

## 9. Controller / Deck / readability attack
A puzzle fails shipping if the player must camera-hunt relevant sites or use pointer precision. <=8 relevant sites is a hard readability ceiling, not merely a solver ceiling.

At 1280x800 verify: all active clock labels readable; objective NOW/DONE distinction visible; focused rule text fits at supported UI scale; conflict/risk/persistent states have non-color cues; controller can reach every socket/site/action through deterministic focus; two overlapping footprints remain distinguishable in high-contrast mode.

If art clutter competes with logical carriers/landmarks during Resolve, decoration must quiet or be removed. Charm cannot reduce state legibility.

## 10. Art/content/tooling scope attack
The bounded diorama kit survives commercially only if recombination looks intentional rather than cheap repetition.

Freeze boundaries:
- <=10 landmark shells, <=8 logical object classes, <=3 carrier shells remain targets;
- district skins may alter materials/props/background dressing but not require unique logical animations or rules;
- every logical process state needs a readable reusable presentation set before cosmetic variants;
- no unique hero asset is required to make an individual case understandable;
- authoring/solver tooling is mandatory production infrastructure because 30+ handcrafted finite-state cases cannot be safely maintained by manual intuition alone.

If presentation budget is constrained, prefer fewer polished districts and stronger landmark state animation over 36 visually unique boards.

## 11. Demo comprehension attack
The phrase "time puzzle" is dangerous because players may assume rewind, chronological arithmetic or ticking clocks.

Frozen messaging:
- primary wording: **move pockets/zones of local time**;
- show two neighboring different clock labels in key capsule/trailer imagery where possible;
- never use rewind, reverse time, change the past, timeline or time travel in store/tutorial copy;
- no backward clock-spin VFX or ticking ambience implying continuous simulation;
- LT01 explicitly demonstrates DONE surviving removal of its clock;
- LT02 reinforces that labels are local conditions, not chronology;
- LT06 must be unguided proof of understanding.

Empirical gate remains: if first-time testers primarily describe the mechanic as rewind/time travel after LT02, repair presentation before content production.

## 12. Commercial promise attack
$14.99 remains coherent for a polished 30-case / roughly 5–7 hour floor package; the product must sell density and authored causal quality, not puzzle-count comparison. 36/12 and 6–8h remain target claims only after measured content exists.

Do not inflate playtime through animation, traversal, collectibles, retries or budget variants. Demo must feel like a small complete arc rather than six tutorials. Next Fest remains a one-shot readiness decision at release stage.

## 13. Fresh-implementation ambiguity audit
A new implementation session must not invent these points:
- time labels are semantic equality/membership tokens, not elapsed chronology;
- planning placement changes NOW immediately but persistent mutation occurs only on Resolve;
- every shipped case has finite `resolve_limit`;
- one entity advances <=1 ordered-chain state/Resolve;
- campaign/mastery forbid same-Resolve prerequisite and accept-on-arrival exceptions unless mechanics are formally reopened;
- carrier dispatch consumes finite public stage and cannot repeat from unchanged predicates;
- exclusive payload/occupancy conflicts are invalid authored content, not runtime tie-breaks;
- Undo restores puzzle state, not persistence generation;
- success is predicate-based, not intended-sequence based;
- DEAD requires exact solver certification except explicit fatal/budget failure;
- previews are informational, not solution simulations;
- animation/input/platform services never affect logic;
- 30 campaign + 8 mastery is the floor; additional slots are cut if proof shapes repeat.

## 14. Canonical repairs / rulings from Phase 10
P10-A — Similarity clusters receive hard topology distinctions and cut conditions above.
P10-B — Resolve budgets are classified teaching/reasoning/mastery-tight; normal campaign may not depend on globally shortest play.
P10-C — Base shipped content forbids `same_resolve_prerequisite=true` and `accept_on_arrival=true`; using either requires formal mechanical reopening/onboarding.
P10-D — Carrier capacity/ownership and stage consumption are explicit; ambiguous simultaneous claims are validator errors.
P10-E — Preview cannot automatically expose beneficial transitions/future objective/carrier outcomes; default one-beat oracle remains off.
P10-F — 30 campaign + 8 mastery is the commercial/design floor; 31–36 and M09–M12 are conditional quality slots, not promises.

P9-A/P9-B/P9-C remain fully binding.

## 15. Phase acceptance
Adversarial review attacked repetition, all flagged similarity clusters, enumeration/oracle behavior, Resolve budgets, carrier exploits, Snapshot0 ambiguity, undo/save/cloud interactions, controller/Deck readability, art/tooling scope, demo classification, commercial promises and implementation ambiguity.

No fatal contradiction remains and no ninth semantic family was introduced. Remaining unknowns are empirical prototype/playtest gates already suitable for dedicated implementation.

**PHASE 10 ADVERSARIAL REVIEW = COMPLETE.**

# NEXT DESIGN STEP — PHASE 11 SPECIFICATION FREEZE
Read the entire active authority and produce `GAME18_FINAL_FREEZE.md`. Reconcile authority order and explicitly propagate P9-A/P9-B/P9-C plus P10-A–P10-F. Freeze implementation acceptance criteria, empirical gates, content-count promise boundaries, out-of-scope list and dedicated-repository handoff. Set `DESIGN COMPLETE = YES` only if a fresh implementation session can build the game without inventing important gameplay. Then attempt migration to the dedicated repository if it exists; if unavailable, preserve Game #018 as NON-ACTIVE frozen safety archive, update `GAME_INDEX.md`, and immediately advance `STATUS.md` to Game #019 Phase 1. Do not start production implementation in the factory.