# GAME #003 — BORROWED COLLISION — ADVERSARIAL REVIEW

Last updated: 2026-08-20
Factory run: **14**
Phase: **10 — Adversarial Review**
Product thesis through Phase 9: **LOCKED / COMPLETE ON PAPER**
DESIGN COMPLETE: **NO**

This file is the destructive Phase-10 review for Borrowed Collision. It exists to break the design before implementation, not to add features. It attacks identity collapse, dominant strategies, renewable-source exploits, transform busywork, backtracking, self-launch drift, timing illusion, inventory drift, causal-overload, input ambiguity, repetition, mastery/remix padding, persistence/idempotency, simultaneous-collision ambiguity, authoring burden, demo/commercial promise and fresh-session implementation ambiguity.

Where this review narrows an earlier implementation-sensitive rule, the numbered Phase-10 repair is intended to become authoritative in Phase 11. No new portable-impact property, transform family, receiver family, combat verb, free-angle physics mode, progression upgrade, currency or live-service system is introduced.

---

# 1. Executive verdict

**PASS WITH CANONICAL REPAIRS. NO EARLIER PHASE REQUIRES A FUNDAMENTAL REOPEN.**

The game remains internally coherent and implementation-ready in principle. The main danger is not missing mechanics; it is that authored content or presentation can accidentally erase the reason Borrowed Collision exists and reduce play to:

> collect arrow -> rotate arrow -> match arrow to socket.

The design survives only if provenance, donor regeneration, receiver aftermath, physical routing, self/cargo allocation and secondary collisions continue to matter in mature play.

Phase 10 finds:
- **0 fatal product contradictions**;
- **1 previously known documentation conflict** already reconciled by P9-R1 (remix packaging);
- **16 canonical repairs / authoring constraints** needed to prevent known collapse modes;
- **11 empirical gates** that cannot honestly be proven on paper;
- **no justification for a new mechanic**.

The specification may proceed to Phase 11 after these repairs are included in the final authority order.

---

# 2. Attack A — detached-arrow / vector-bookkeeping identity collapse

## Attack

Strip room art, donor animation and lineage stamps away. Represent each held impact only as `direction + magnitude`, each converter as a direction transform and each receiver as an accepted tuple. Many superficially valid cases can then be solved as a small token-matching graph.

That is the existential failure mode identified since the tournament. A technically correct puzzle is not sufficient if collision provenance becomes decorative.

## Failure pattern

A mature case is invalid when:
- any impact of the same direction/band is strategically interchangeable regardless of source;
- harvesting a source does not alter future world options;
- receiver aftermath does not affect future causal possibilities;
- converter use is independent of physical access/topology;
- secondary collisions are optional flavor rather than meaningful alternate sources;
- self-launch can be replaced by a generic teleport without changing reasoning.

## P10-R1 — Mature provenance/world-state dependency rule

For **every campaign case C15–C34 and every remix**, the authored known-solution set must demonstrate at least **two** of the following are materially solution-relevant:
1. donor availability/regeneration class;
2. donor reset consequence;
3. source world-state/provenance distinction;
4. receiver aftermath changing later access/state;
5. secondary collision creating/replacing a needed lineage;
6. self-versus-cargo/environment allocation;
7. physical converter/pickup access topology;
8. protected invariant tied to source/receiver state.

At least **one** of the two must be from items 1–5. Purely spatial walking inconvenience does not count.

A case fails content validation/review if replacing all impacts with anonymous direction/band tokens leaves the same dominant solution reasoning.

## Empirical gate E10-01

In representative C15+, naive/intermediate testers should describe at least one successful decision in source/world-state terms (`I saved that donor`, `I needed the landing collision`, `resetting that changed the route`) rather than only arrow orientation/strength.

---

# 3. Attack B — direction, magnitude and capture-source readability

## Attack

Run the UX mentally at 1280×800, grayscale, no audio, reduced motion, high UI scale and with two or three impacts visible. Direction arrows, magnitude chevrons, provenance stamps, donor class, safe/unsafe receiver bands and capture-enabled sources compete for attention.

The current grammar is complete, but density can still create category confusion.

## P10-R2 — Impact identity hierarchy

Every impact representation must preserve this visual priority:
1. **direction** — strongest shape/orientation signal;
2. **magnitude** — second signal via 1/2/3 chevrons + size/body treatment;
3. **provenance** — compact source stamp;
4. **transform history** — inspect-level detail, not belt clutter.

Transform history must never compete visually with direction/magnitude on the default impact belt.

## P10-R3 — Capture-source affordance budget

Capture-enabled collisions must use one consistent world affordance family. It may vary by theme, but must communicate `this collision can yield a stored consequence` without making every source look like glowing loot.

Rules:
- no more than one primary capture affordance + one state modifier per source in ordinary view;
- regeneration class detail is inspectable and may use a secondary icon;
- non-capture collisions must not accidentally use the same affordance;
- `CHAIN_GENERATED` impacts do not require advance loot markers; their lineage is shown after the real secondary collision.

## Empirical gate E10-02

At Deck size, grayscale/no-audio, after the first-hour teaching packet:
- >=90% sampled impact identifications correctly distinguish direction from magnitude;
- >=85% sampled source inspections correctly identify whether a collision can emit an impact;
- ordinary errors caused primarily by impact-display misunderstanding remain within the inherited <=20% prototype gate.

---

# 4. Attack C — maximum-force dominance and renewable strong-token factories

## Attack

Try to solve every case by acquiring the highest available band. Separately, find every path from RESETTABLE or CYCLIC_WEAK donors through chain bodies/mass relations that can create repeatable MEDIUM/STRONG output.

A renewable WEAK source is dangerous because the collision lookup can legitimately increase resulting transfer band through mass relationships. Therefore `damper never increases` is not enough to prevent escalation.

## P10-R4 — Renewable-lineage escalation invariant

For every RESETTABLE or CYCLIC_WEAK donor, bounded exploit validation must search reachable regeneration cycles and classify the **maximum sustainably repeatable output band**.

A mature case is invalid if an indefinitely repeatable cycle can produce a MEDIUM or STRONG harvest **without** consuming or degrading a bounded world resource, changing a protected state, requiring a non-repeatable lineage, or otherwise creating a meaningful visible cost.

`CYCLIC_WEAK` specifically may have infinite generations only when the indefinitely repeatable net harvest envelope remains WEAK. Any path that turns it into an unbounded stronger factory fails content validation.

A RESETTABLE donor may legitimately recreate stronger impacts only when each generation's reset contract imposes a meaningful world-state tradeoff or route dependency that prevents it from behaving as a free ammo button.

## P10-R5 — Strong-choice distribution gate

From C15 onward, the campaign must not teach a monotonic power heuristic. In each five-case window, at least:
- one case has a meaningful baseline solution where WEAK is strictly preferable to available stronger impact;
- one case has a meaningful baseline solution where MEDIUM is strictly preferable to STRONG;
- no case's known-solution review may rely on STRONG at every meaningful spend unless that case is explicitly tagged as a rare force-routing exception and adjacent cases counterbalance it.

This is a campaign authoring rule, not a hidden per-case penalty.

## Empirical gate E10-03

Representative mature play should remain below the inherited threshold where >=50% of successful solutions use the strongest available impact at every meaningful decision.

---

# 5. Attack D — RESETTABLE donor as ammo button

## Attack

Remove theme fiction and examine reset contracts. If reset is `press switch -> donor reappears` with no route/state consequence, the game has created an ammunition dispenser disguised as machinery.

## P10-R6 — Meaningful reset contract

Every RESETTABLE donor must declare:
- exact reset action;
- exact canonical world-state changes caused by reset;
- at least one access, routing, receiver, body-position, protected-state or future-donor consequence that is material in every case where repeated generation is strategically relevant.

A reset that changes only animation/state label while leaving all meaningful options equivalent is invalid mature content.

The content validator can prove structural fields exist; authored review must prove the consequence is strategically material.

---

# 6. Attack E — transform loops and converter busywork

## Attack

Build a room with quarter-turn, reverse, mirror and damper. A designer can easily manufacture difficulty by forcing a token through a long sequence of devices. That creates clerical arrow manipulation without deeper causal reasoning.

## P10-R7 — Transform meaningfulness and chain ceiling

A required solution chain may contain at most **two transform operations between material world-state events** by default.

A case may exceed two only when:
- transform topology is explicitly the case's dominant reasoning lesson;
- physical access/order changes between transforms;
- the sequence cannot be collapsed into one equivalent fixed transform device without losing the intended causal decision.

No known baseline solution may require more than **four consecutive transforms** without an intervening harvest, spend, body-state change, receiver-state change or traversal-access change.

Repeated transforms that merely compute an orientation are content-smell failures even if technically legal.

## Transform-loop exploit

Because transforms preserve impact identity and do not increase magnitude, loops are not duplication exploits. They can still create infinite busywork/history.

Canonical rule: applying transforms is deterministic and legal, but content must not require cyclic transform traversal whose only result is returning to an equivalent impact state. Validation should detect transform-state cycles and warn/error when a required known solution enters one without a world-state reason.

---

# 7. Attack F — multi-room pickup backtracking

## Attack

Persistent world pickups are mechanically safe but can force repeated walks through already solved rooms. If that walking has no current causal state, it is friction, not gameplay.

On the other hand, teleporting impacts through unresolved rooms would erase physical routing and provenance significance.

## P10-R8 — Solved-route traversal compression boundary

Presentation may compress pickup retrieval/traversal only when **all** of these are true:
1. every traversed player edge has already been visited in the current canonical branch;
2. no traversed room contains unresolved moving bodies, active receive-window state or required player-timed interaction;
3. no traversal command changes donor generation, receiver state, objective/invariant truth, body state or impact state except final pickup collection;
4. the target pickup is already discovered and stable;
5. the player has a legal canonical path to the pickup and back/to the chosen destination under current state;
6. compression emits the same final canonical player node and pickup state as executing the individual traversal commands.

If any condition fails, ordinary traversal is required.

Compression is presentation convenience, **not impact teleportation**. The impact becomes HELD only when the canonical player reaches its pickup node.

## Empirical gate E10-04

Late multi-room cases should not produce repeated complaints that solved-room walking is the dominant time cost. If retrieval friction remains high even with safe compression, content layout should be shortened rather than adding global fast-travel inventory.

---

# 8. Attack G — self-launch drift into platformer/dexterity game

## Attack

Self-launch looks inherently action-heavy. If presentation uses smooth arcs and moving landings, players may reasonably expect analog aim, air control or timing mastery. Adding those would create a second game.

## P10-R9 — Self-launch authored-outcome rule

Every baseline self-launch exposes a finite authored set of legal outcomes before commit. A self-launch receiver defines:
- legal input direction/band combinations;
- corresponding authored launch lane/outcome family;
- canonical landing/collision boundary;
- direct known unsafe family consequence where applicable.

The player may choose among legal snapped outcomes but may not fine-tune launch angle, launch power, midair steering or frame-timed release.

Presentation may interpolate a satisfying arc, but the arc must visually reinforce—not obscure—the authored lane.

Self-launch mastery may reward causal allocation/lineage consequences, never analog execution accuracy or airtime timing.

## Empirical gate E10-05

After first self-launch teaching, players should predict the landing family from UI/world affordances without requesting manual aim. If the dominant desire is `let me aim/jump better`, presentation is signaling the wrong genre and must be simplified/clarified.

---

# 9. Attack H — moving receive-window timing illusion

## Attack

Even canonical step windows can appear reflex-based when animated continuously. Players may mash Spend, abuse Pause, or perceive slowdown as an easier ruleset.

## P10-R10 — Receive-window state legibility

Every moving receiver used in required baseline play must expose:
- discrete canonical state/window label or equivalent shape marker;
- which state(s) accept the selected impact;
- next-state progression when deterministic and already visible under learned rules;
- Pause/Step support at movement-step boundaries.

Spend commits only against a canonical receive-window state, never an interpolation frame.

Pause, Step and slowdown are **fully legitimate** and never reduce completion/mastery/achievement validity. Difficulty may come from scheduling causal chains across states, not reaction speed.

A case is invalid if its core challenge disappears merely because the player uses Step; that means the case was secretly reflex timing rather than causal reasoning.

## Empirical gate E10-06

Controller/Deck testers using Step should still need to solve ordering/source/arrival logic while achieving the same deterministic outcome as real-time presentation.

---

# 10. Attack I — 3-slot inventory / progression-upgrade drift

## Attack

Three slots can look like a permanent capacity upgrade, encourage hoarding, expand UI burden and weaken the game's physical pickup economy.

## P10-R11 — Three-slot justification rule

Inventory capacity remains **2 by default and globally**. A case may define capacity 3 only from the frozen late introduction point onward and only if its content data contains a `three_slot_justification_note` proving all of the following:
1. a known baseline solution genuinely requires or meaningfully uses three simultaneous held lineages;
2. replacing the third held impact with a nearby stable world pickup/cache would materially change the intended ordering insight;
3. the case's dominant reasoning is not generic hoarding;
4. at least one known solution demonstrates why three-way ordering/allocation matters;
5. the case does not imply the player's profile has permanently upgraded capacity.

Phase-10 authoring target: **no more than 4 main campaign cases** should use capacity 3 unless Phase-11 audit proves a stronger reason. C34 may use it; most late cases should remain at 2.

Remixes inherit the source substrate capacity unless changed capacity itself creates a documented changed causal dependency; capacity inflation alone is invalid remix novelty.

---

# 11. Attack J — causal-ribbon ancestry overload

## Attack

A late chain can contain harvest, transform, spend, movement, collision, generated impact, receiver changes and multiple requirements. A literal event DAG is accurate but unusable.

Phase 6 already established <=5 material nodes and <=2 sibling branches. Phase 10 makes the compression semantics implementation-specific enough to prevent arbitrary hiding.

## P10-R12 — Product causal-presentation budget

Default requirement-focused or selected-impact causal ribbon:
- **<=5 visible material nodes**;
- **<=2 visible sibling branches**;
- collapse repeated movement steps with no material state change;
- collapse consecutive transform history into one `transformed through N devices` node unless one transform is itself the selected explanation focus;
- always preserve the first source collision/provenance node and the final selected requirement/receiver consequence node;
- never collapse across a change of lineage identity caused by a real secondary collision;
- never fabricate a single cause when a predicate is genuinely conjunctive.

`More affected` / expanded ancestry may reveal the full material DAG.

## Empirical gate E10-07

Representative late-case testers should be able to answer `where did this impact come from?` and `what first caused this requirement to fail?` without reading raw event IDs or a full transaction log.

---

# 12. Attack K — keyboard/controller focus predictability

## Attack

Mechanical reachability is not enough. Dense late rooms can have many bodies, pickups, transforms and receivers. If focus jumps unpredictably based on screen coordinates or current zoom, controller play becomes frustrating.

## P10-R13 — Authored deterministic focus graph

Every room compiles a deterministic semantic focus graph across:
- player traversal destinations;
- reachable world pickups;
- nearby/accessible receivers;
- transforms;
- donors/source inspection targets;
- relevant room links.

Rules:
- each required interactable is reachable without pointer input;
- directional/focus-next order is stable for a canonical state and independent of camera zoom, animation interpolation, scene-tree order and hash-map iteration;
- author overrides are allowed and required where auto-generated spatial neighbors are ambiguous;
- selected impact may filter/highlight compatible targets, but filtering must never hide structurally incompatible objects needed for inspection/learning;
- contextual controller bindings must display their current function before commit.

This is a content/compiler acceptance requirement, not optional polish.

## Empirical gate E10-08

Controller-only late-case testers should not accumulate repeated accidental target selections after the teaching period. If they do, fix authored focus topology before adding more UI automation.

---

# 13. Attack L — lived reasoning repetition / content exhaustion

## Attack

Formal tags can differ while player cognition repeats. For example:
- case A tagged source selection;
- case B tagged magnitude suitability;
- case C tagged provenance;

Yet all may actually be solved by `save strong donor -> rotate medium arrow -> spend on fragile receiver`.

A tag-diversity rule alone cannot prevent repetition.

## P10-R14 — Reasoning-isomorphism audit

Every C15–C34 case must record one normalized **causal skeleton** for each known baseline solution character. Skeleton nodes use abstract operations, not theme nouns:
- acquire/engineer source;
- preserve/consume donor;
- transform direction;
- damp magnitude;
- spend on self;
- spend on environment/cargo;
- create secondary lineage;
- reset source with consequence;
- align moving state;
- retrieve deferred pickup;
- satisfy/preserve invariant.

Campaign review rules:
- no consecutive **3-case** C15+ window may have all cases sharing the same dominant normalized causal skeleton;
- no consecutive **5-case** window may contain fewer than **3 materially distinct skeleton families**;
- differing room count, theme, direction, magnitude or receiver skin does not count as distinct reasoning;
- if two cases share a skeleton, at least one must change the key dependency/order such that the same heuristic cannot solve both.

The existing reasoning-transformation tags remain useful but are insufficient by themselves; Phase 10 requires skeleton review in addition.

## Empirical gate E10-09

Hour-3/hour-10 testers should be able to describe recent cases using different causal verbs/insights rather than only `get the right arrow to the right place`.

---

# 14. Attack M — mastery threshold shaving

## Attack

Mastery can easily become `same solution but one fewer impact`, which adds checklist pressure without deeper play.

## P10-R15 — Mastery distinction proof

Every mastery contract must contain an internal `mastery_distinction_note` and reference at least one known mastery solution fixture.

Authoring review compares baseline and mastery solution character. Mastery is valid only if it requires at least one of:
- different donor/source choice;
- different lineage generation strategy;
- preservation of a world state not preserved by ordinary baseline solutions;
- meaningful resource allocation difference (self/cargo/environment or renewable/scarce source);
- actual causal compression replacing multiple material events with a different chain;
- stronger Stable Causality condition containing a real moving/reset/chain state transition.

Invalid mastery:
- arbitrary raw command count;
- arbitrary raw harvest/spend threshold with identical causal skeleton;
- Undo/restart/time limit;
- input-device restriction;
- accessibility restriction;
- `leave one token unused` when that happens automatically in baseline.

---

# 15. Attack N — remix parameter padding

## Attack

A remix can appear new by moving bodies, swapping directions or changing a band requirement while leaving the same causal insight intact.

P9-R1 already establishes the authoritative three-pack structure: R01–R03 after C14, R04–R07 after C28, R08–R10 after C34.

## P10-R16 — Remix dependency proof

Every remix must store and review:
- `source_substrate_id`;
- source dominant causal skeleton;
- changed initial facts;
- changed objectives/invariants;
- `changed_causal_dependency`;
- expected new reasoning transformation;
- remix dominant causal skeleton;
- one known baseline solution fixture.

A remix fails if source and remix dominant skeletons remain equivalent after abstracting:
- direction labels;
- magnitude labels;
- start positions;
- art/theme;
- numerical thresholds;
- mastery limits.

Across each remix pack, at least three distinct reasoning/skeleton families must be represented where pack size permits; R-A's three cases must all differ materially.

---

# 16. Attack O — save/lineage duplication and fault recovery

## Attack packet

Attempt:
- double Collect command;
- double Spend command;
- reload after impact consumption but before animation ends;
- crash after collision but before pickup presentation;
- duplicate RESETTABLE donor reset command;
- save/load while world pickup exists with full inventory;
- Undo -> branch -> replay old stale command;
- divergent Cloud active-case branches;
- merge durable profile progress from devices with different active sessions;
- corrupt primary save while backup/temp exist.

## Verdict

Phase 4/8 semantics are coherent if implemented literally:
- domain-changing command IDs are idempotent;
- stale revision/hash rejects before mutation;
- one lineage emits at most one impact;
- a committed resolution transaction persists only at full transaction boundary;
- an incomplete crash restores the exact pre-transaction checkpoint;
- Undo restores canonical lineage state and legitimately permits re-performing the restored branch;
- Cloud progress facts merge monotonically, while divergent active case branches never synthesize a hybrid state.

## Phase-10 tightening

Phase 11 should state explicitly: **donor generation increment and emitted-lineage record must be part of the same canonical transaction/checkpoint as the world-state reset/collision that creates them.** There is no persistence boundary where generation advanced but its reset consequence did not, or where harvest emission exists without the committed collision outcome.

## Empirical/technical gate E10-10

Implementation fault-injection tests must cover every canonical persistence boundary above, including duplicate commands and active-branch divergence.

---

# 17. Attack P — ambiguous simultaneous collisions and chain ceilings

## Attack

Create same-step contact where three bodies converge on one boundary, two independent collisions touch the same body, or a chain hits the hard movement ceiling with bodies still active.

If the content schema merely hopes the collision table handles it, designers will accidentally create undefined states.

## Canonical repair / narrowing

Phase 4 already requires simultaneous grouping and Phase 5 requires `simultaneous_group_key`. Phase 10 makes the ship rule explicit:

- every reachable same-step multi-contact configuration must compile to exactly one registered simultaneous collision-group outcome;
- a body cannot belong to two separately resolved collision groups in the same canonical movement step;
- ambiguous overlap is a **content compile error**, not a stable-ID sequential fallback;
- stable-ID ordering may order independent already-disjoint groups for trace serialization, but cannot choose physical outcome;
- known baseline solutions must terminate below the authored chain ceiling;
- any legal player command that could hit the hard 24-step ceiling must have a defined deterministic `CHAIN_LIMIT_REACHED` safe state and must not leave a half-applied collision group;
- campaign content should treat actually reaching the hard ceiling as a validation failure unless the case intentionally demonstrates a bounded cycle and the resulting state is explicitly authored/visible.

Implementation validation must enumerate/probe reachable simultaneous groups from known fixtures and bounded search where feasible.

---

# 18. Attack Q — content authoring and validator burden

## Attack

The design requires 34 main cases + 10 remixes, known solution fixtures, lineage, regeneration, focus graph, collision grouping, objective predicates, mastery distinction and repetition checks. This is a meaningful authoring/QA burden.

The danger is solving it by adding a generic scripting language or case callbacks. That would destroy deterministic boundedness.

## Verdict

The burden is high but remains acceptable because the grammar is small and data-driven. The correct response is tooling, not more flexibility.

Required implementation-era validator classes are therefore reaffirmed:
- stable IDs/references;
- movement/collision graph structure;
- simultaneous group completeness;
- donor generation/regeneration contracts;
- one-harvest lineage invariant;
- renewable escalation search;
- receiver compatibility/band/window contracts;
- transform graph/cycle report;
- known solution replay;
- objective/invariant/mastery evaluation;
- progression/tutorial graph;
- focus graph reachability;
- three-slot justification;
- reasoning-isomorphism report;
- remix dependency comparison;
- localization/presentation required-token coverage.

No arbitrary per-case gameplay script hook is permitted.

---

# 19. Attack R — demo promise and premium perceived value

## Demo promise attack

A weak demo can prove only `crash makes arrow` and accidentally market the game as a tiny matching puzzler. DEMO01–DEMO05 already contain the right escalation, but Phase 10 freezes the commercial proof condition:

The demo is invalid unless a representative player experiences **all five** before the end:
1. collision -> portable impact;
2. physical transform;
3. magnitude suitability where stronger is not automatically better;
4. provenance/source availability matters;
5. spent consequence creates a deliberate secondary collision/new lineage that is reused.

DEMO05 must require source/world-state reasoning, not merely present it as optional spectacle.

## Price/value attack

The design-time $14.99–$19.99 band / $16.99 center is plausible only if the 34 cases contain lived reasoning variety and the product avoids tutorial-thin padding.

Phase 10 therefore rejects using count alone as value proof.

## Empirical gate E10-11

Before release-price lock:
- measure median first-clear duration and distribution;
- assess perceived repetition by Acts III–V;
- verify demo users can state the full consequence-reuse hook;
- verify players do not primarily describe the game as arrow inventory or simplified physics matching;
- recheck current comparable pricing near release.

If content lands closer to a short 3–4 hour experience or repetition remains high, price should move toward the lower end rather than adding grind/padding.

---

# 20. Fresh-session implementation ambiguity audit

The specification was reread as if implementation were starting with no chat history. The following potential ambiguities were attacked.

## A. Is harvest a reflex catch?
**Resolved already:** no. Eligible collision output becomes a stable world pickup. Collection is ordinary interaction.

## B. Can presentation physics decide collision?
**Resolved already:** no. Authored graph/boundary state is authoritative.

## C. Can impacts be freely rotated?
**Resolved already:** no. Only physical QUARTER_TURN/REVERSE/MIRROR/DAMPER devices.

## D. Does Undo duplicate a lineage?
**Resolved already:** no. Undo restores the prior canonical branch; re-performing restored history is legitimate.

## E. Can a RESETTABLE source increment generation without completing its reset consequence?
**Tightened in Phase 10:** no. Generation increment and reset world-state consequence are atomic.

## F. What if a collision group is ambiguous?
**Tightened in Phase 10:** invalid content. Stable IDs cannot choose physical outcome.

## G. Can solved-route compression teleport an impact?
**Tightened in P10-R8:** no. It only compresses canonical player traversal under strict no-state-change conditions.

## H. Can 3 slots be a profile upgrade?
**Resolved/tightened:** no. Case-authored capacity only, with P10-R11 justification.

## I. Is Step an easier simulation mode?
**Resolved/tightened:** no. It is legitimate presentation of the same canonical states; content relying on reflex timing is invalid.

## J. Can causal UI hide source lineage to reduce clutter?
**Tightened in P10-R12:** source collision and selected final consequence are never collapsed away in default relevant ancestry.

## K. What happens at hard chain ceiling?
**Tightened:** deterministic safe state; shipped known solutions should not rely on hitting it.

## L. Which remix packaging is canon?
**Resolved by P9-R1:** Phase-7 three-pack structure 3/4/3.

No remaining ambiguity requires a new mechanic or a fundamental Phase 3–8 rewrite.

---

# 21. Empirical gate register

These remain intentionally implementation/prototype dependent:

- **E10-01 Product identity:** mature players reason in source/world-state terms, not only arrows.
- **E10-02 Readability:** direction/magnitude/capture-source remain legible at Deck size, grayscale/no-audio/reduced motion.
- **E10-03 Strength distribution:** strongest-impact dominance stays below inherited failure threshold.
- **E10-04 Backtracking:** solved-room pickup retrieval is not the dominant friction.
- **E10-05 Self-launch genre signal:** players understand authored outcomes and do not require analog platformer controls.
- **E10-06 Moving-window legitimacy:** Pause/Step preserves causal challenge and removes reflex interpretation.
- **E10-07 Causal explanation:** late lineage source/failure can be explained from compressed UI.
- **E10-08 Focus usability:** controller/keyboard dense-room navigation is predictable, not merely technically reachable.
- **E10-09 Repetition:** hour-3/hour-10 content produces materially different lived causal reasoning.
- **E10-10 Persistence robustness:** lineage/idempotency/recovery fault injection passes.
- **E10-11 Commercial proof:** demo communicates full hook and final perceived value supports release-time price.

These gates can kill, compress or amend content/UX during implementation. They are not permission to leave domain rules undefined.

---

# 22. Phase-10 acceptance decision

- Detached-arrow identity collapse attacked: **YES — P10-R1**
- Direction/magnitude/source readability attacked: **YES — P10-R2/R3**
- Max-force dominance attacked: **YES — P10-R4/R5**
- RESETTABLE/CYCLIC_WEAK ammo-factory exploit attacked: **YES — P10-R4/R6**
- Transform-loop/busywork attacked: **YES — P10-R7**
- Multi-room backtracking attacked: **YES — P10-R8**
- Self-launch dexterity/platformer drift attacked: **YES — P10-R9**
- Moving-window timing illusion attacked: **YES — P10-R10**
- 3-slot upgrade/inventory drift attacked: **YES — P10-R11**
- Causal ancestry overload attacked: **YES — P10-R12**
- Keyboard/controller dense focus attacked: **YES — P10-R13**
- Reasoning-isomorphism/content exhaustion attacked: **YES — P10-R14**
- Mastery threshold shaving attacked: **YES — P10-R15**
- Remix parameter padding attacked: **YES — P10-R16**
- Save/lineage duplication + Cloud branch attack: **YES**
- Simultaneous collision ambiguity + chain ceiling attack: **YES**
- Authoring/validator burden attacked: **YES**
- Demo/commercial promise attacked: **YES**
- Fresh-session implementation ambiguity audit: **COMPLETE**
- Fatal contradiction found: **NO**
- New gameplay primitive added: **NO**
- Production implementation started: **NO**
- Phase 10: **COMPLETE ON PAPER**
- DESIGN COMPLETE: **NO — Phase 11 freeze still required**

---

# 23. Phase-11 required reconciliation list

Phase 11 must explicitly incorporate/precedence these items:
1. P9-R1 — authoritative 10-remix packaging is Phase-7 three packs (3/4/3), superseding Phase-5 two-pack historical wording.
2. P10-R1 — mature provenance/world-state dependency rule.
3. P10-R2/R3 — impact identity hierarchy and capture-source affordance budget.
4. P10-R4/R5/R6 — renewable escalation, strong-choice distribution and meaningful reset contract.
5. P10-R7 — transform meaningfulness / consecutive-transform ceiling.
6. P10-R8 — exact solved-route traversal-compression boundary.
7. P10-R9 — authored self-launch outcome rule.
8. P10-R10 — moving receive-window state legibility / Pause-Step legitimacy.
9. P10-R11 — three-slot justification and no profile-upgrade interpretation.
10. P10-R12 — causal-presentation compression semantics.
11. P10-R13 — deterministic authored focus graph.
12. P10-R14 — causal-skeleton reasoning-isomorphism audit.
13. P10-R15 — mastery baseline-vs-mastery distinction proof.
14. P10-R16 — remix source-vs-remix dependency/skeleton proof.
15. Persistence atomicity tightening: donor generation + reset/collision consequence + harvest-emission state share canonical transaction boundaries.
16. Simultaneous group completeness: ambiguous reachable multi-contact is invalid content; stable IDs do not choose physics.
17. Hard chain ceiling: deterministic safe termination exists, but shipped known solutions should not depend on reaching the ceiling.
18. Demo proof: DEMO01–DEMO05 must show all five causal layers including deliberate secondary-lineage reuse.
19. Empirical gates E10-01..E10-11 remain implementation obligations, not design ambiguity.

## NEXT PHASE

**Phase 11 — Specification Freeze.**

Perform a fresh implementation-readiness audit across Product Thesis, Mechanics, Content, UX, Commercial, Technical Spec, Whole-Game Simulation and this Adversarial Review. Resolve authority/wording conflicts only at the smallest necessary scope; create `GAME3_PHASE11_FINAL_FREEZE.md`; define final authority order and acceptance checklist; set `DESIGN COMPLETE = YES` only if a fresh implementation session can build Borrowed Collision without inventing important gameplay. Then prepare the dedicated-repository migration/handoff gate. Do not begin production implementation in the factory.