# GAME #018 — PHASE 5 CONTENT ARCHITECTURE

Date: 2026-09-06
Game: **LOCAL TIME**
Status: PHASE 5 COMPLETE — PHASE 6 UX / PRESENTATION NEXT
Production implementation: NO

Mechanical authority remains `GAME18_MECHANICS.md`. This file defines authored content only; it does not add runtime grammar.

## 1. Content thesis and count

Target: **36 campaign cases + 12 optional mastery cases**. Count is quality-gated, never a quota.

- Campaign target: 36; acceptable ship range 30–36.
- Mastery target: 12; acceptable ship range 8–12.
- A weak/repetitive case is cut rather than repaired with a bespoke rule.
- If fewer than 30 campaign cases survive quality gates, Phase 5 must be reopened.
- Demo remains LT01–LT06.

## 2. Eight reusable semantic families

All authored content maps to these Phase-4 families:

1. **Current Gate (CURRENT)** — a site is active only while its present local-time predicate is true.
2. **Persistent Step (ADVANCE_ONCE)** — X -> Y once when a public condition is true at Resolve.
3. **Ordered Process (ORDERED_CHAIN)** — finite acyclic chain, normally <=3 transitions, one transition/entity/Resolve.
4. **Permanent Risk (PERMANENT_LOCKOUT)** — a clearly previewed bad exposure permanently invalidates an entity unless an already-earned public protection milestone applies.
5. **Acceptance (ACCEPT)** — an object already at an endpoint is accepted under current public conditions.
6. **Dispatch (DISPATCH)** — current predicates plus persistent prerequisites enable departure.
7. **Carrier Handoff (CARRIER_HANDOFF)** — a visible carrier makes exactly one deterministic authored step after transitions.
8. **Coupled Current (COUPLED_CURRENT)** — normally two, late-game at most three, public current predicates must be true in the same Snapshot0.

A different fiction skin is not a new family. A proposed ninth family requires explicit reopening of mechanical architecture.

## 3. Six-chapter dependency ladder

### Chapter 1 — Here and Now (Cases 01–06)
Canonical LT01–LT06. Teaches current vs persistent state, ordered process, visible permanent risk, simultaneous current predicates, handoff and synthesis.

### Chapter 2 — Finish What You Started (07–12)
Focus: Persistent Step + Ordered Process.
- competing one-step processes;
- a three-stage chain;
- two chains sharing a risky broad footprint;
- restoring a current gate after persistent work;
- move-budget reuse;
- synthesis with two chains + one protected site + final current condition.

### Chapter 3 — Send It Across Town (13–18)
Focus: Acceptance + Dispatch + Carrier.
- prepare -> dispatch -> arrival -> later acceptance;
- departure requiring one current gate plus persistent prerequisite;
- two payloads through one public carrier;
- receiving window competing with next preparation;
- Resolve-budget pressure;
- chapter synthesis with coupled departure.

### Chapter 4 — Protect the Morning (19–24)
Focus: Permanent Risk as deduction.
- protect before broad exposure;
- two protected sites with different prerequisite order;
- coupled action safe only after protection;
- Snapshot0 precedence defeats a tempting shortcut;
- one case with two genuinely different valid protection routes;
- synthesis with two risks + process chain + final coupling.

### Chapter 5 — Two Clocks, One Town (25–30)
Focus: spatial coordination.
- two clocks on two coupled endpoints;
- earn milestone, then reuse that clock in final arrangement;
- repeated coupled needs in different beats;
- first explicit three-site coupled-current case;
- carrier departure under two-clock coordination;
- synthesis under move budget.

### Chapter 6 — The Whole Day at Once (31–36)
All known families, but one dominant insight per case.
- two process chains + current gate;
- relay + protected endpoint;
- two movable clocks + one fixed zone;
- at most two carriers, without routing complexity;
- tight but explainable bottleneck;
- final synthesis: >=2 persistent prerequisites, one protection constraint, one dispatch/handoff sequence, final two-site coupled condition.

Normal ceilings remain <=3 movable clocks and <=8 relevant sites.

## 4. Shippable-case quality gate

A case ships only if:
1. solver confirms at least one solution;
2. required insight fits one sentence;
3. written human proof eliminates meaningful alternatives before enumeration;
4. proof shape is not already overrepresented;
5. no new runtime exception is needed;
6. target-display readability passes;
7. failure is explainable through public reason trace;
8. it is not dominated by a cleaner case with the same insight.

First cuts: cosmetic variants, budget-only difficulty, socket-scanning cases, visually dense boards, bespoke-rule cases.

## 5. Canonical authored-case data

Each case carries:

**Identity:** `case_id`, chapter, title, one-line goal, district skin, introduced/reinforced families.

**Board:** sites, objects, clocks, sockets with exact coverage, carriers with public endpoints, optional fixed local-time sites.

**Rules:** transition/lockout/accept/dispatch/coupled rules using only Phase-4 grammar, objective, fatal conditions, placement-move limit, Resolve limit.

**Validation:** solution witnesses, shortest move/Resolve counts, reachable/dead state counts, ordered `human_proof`, `required_insight`, `anti_enumeration_reason`, dominant-strategy attack, alternate solutions, accessibility notes.

**Review:** nearest similar cases, novelty delta, repetition signature, explicit cut condition, playtest questions.

No free-form gameplay script field is allowed.

## 6. Recombination / anti-repetition matrix

| Chapter | Dominant families | Main proof shape |
|---|---|---|
| 1 | F1–F8 introductions | learn state classes |
| 2 | F2/F3/F4 | persistent order |
| 3 | F5/F6/F7 | relay and beat separation |
| 4 | F4 + prior families | protect before exposure |
| 5 | F1/F6/F8 | simultaneous spatial coordination |
| 6 | all known families | synthesis with one bottleneck |

Each case gets a repetition signature:
`[primary proof][families][clock count][risk count][carrier count][budget pressure][final-objective type]`.

No adjacent campaign cases may share the same primary proof plus same family set. Within a chapter, at most two cases may share a primary proof. A later near-duplicate must add a genuinely different dependency topology or be cut.

## 7. Bounded presentation/content kit

### Landmark shells — target <=10
Bakery; bridge/gatehouse; station/tram stop; greenhouse/flower stall; market; cafe/receiving counter; print shop/workshop; pharmacy/cold store; school/civic hall; square/bell tower.

### Logical object classes — target <=8
Bread/dough parcel; flower/produce; printed parcel; medicine package; ticket/mail; crate; civic token/document; generic delivery parcel.

### Carrier shells — target <=3
Tram; bicycle courier; small delivery cart. They all use the same deterministic Carrier Handoff grammar.

### Clock-zone kit
At most three movable clock body silhouettes in a case. Labels use large text plus shape/pattern cue, never color alone. Fixed local time is visually related but anchored.

Each process should use <=4 clearly distinguishable visual states including a permanent bad terminal state.

## 8. Representative causal proofs

### Early — Case 08
Bread requires 08:05 to finish. A flower is invalidated by 08:05 unless protected. One narrow socket covers only Bakery; a tempting broad socket covers both.
Proof: bread needs 08:05; broad exposure before protection is invalid; therefore use narrow coverage or protect first. Difficulty is causal, not exploratory.

### Mid — Case 16
Parcel must be STAMPED. Dispatch requires Station=08:05 and Bridge OPEN simultaneously. Carrier then moves parcel to Market. Market can accept only on a later Resolve while Market=09:10.
Proof: prepare first; satisfy simultaneous departure; arrival happens after transition evaluation; only then allocate 09:10 to receiving.

### Late — Case 33
One fixed zone, two movable zones, a protection milestone, coupled dispatch and a carrier delivery.
Proof sequence: protect fragile state -> satisfy coupled dispatch -> persistent dispatch frees earlier clock coverage -> carrier arrives -> relocate receiving clock -> satisfy final current condition. No hidden elapsed time is used.

### Case 36 requirement
Final case uses only known families, <=3 clocks, <=8 sites, >=2 persistent prerequisites, one visible protection constraint, one relay and a final coupled-current objective. Intended proof must fit <=6 necessity statements.

## 9. Mastery boundaries

Target 12, floor 8.

Allowed: tighter fair budgets; larger reachable graphs; three-site coupling; two carriers; optimization bonus goals; denser combinations of known families.

Forbidden: new semantic families; >3 clocks/>8 sites without reopening scope; hidden information; reaction-speed demands; mandatory globally shortest solution; surprise same-beat cascades.

M09–M12 are reserve-first cuts if they do not add genuinely new reasoning.

## 10. Anti-enumeration gate

From Chapter 2 onward every case must identify:
- at least one tempting placement ruled out by a causal fact;
- the persistent milestone that changes future freedom;
- any prerequisite before broad risky coverage;
- why simultaneous predicates truly need simultaneity;
- a reasoning route that does not require scanning all sockets.

Reject cases whose written proof is essentially "try A/B/C", whose difficulty collapses into UI scanning, or whose solver depth has no compact human explanation.

## 11. Expansion boundary

New content may recombine the eight frozen families with new fiction skins, geometry, dependencies and budgets.

It may not silently add global rewind/time travel, continuous timers, ticking clocks, hidden schedules, random outcomes, reverse transitions, arbitrary building scripts, same-beat multi-hop cascades, ambiguous overlap priority, physical carrier simulation, or reaction-speed objectives.

## 12. Phase acceptance

Phase 5 now fixes the reusable family vocabulary, six-chapter ladder, 36+12 quality-gated target, authored schema, proof-shape diversity rules, bounded art/content kit, representative causal proofs, mastery limits, anti-enumeration review and expansion boundary.

**PHASE 5 CONTENT ARCHITECTURE = COMPLETE.**

# NEXT DESIGN STEP — PHASE 6 UX / PRESENTATION ARCHITECTURE

Specify exact clock placement/footprint preview, current vs persistent visual language, risk warnings, Resolve reason trace, objectives, carriers, mouse/keyboard and controller/Steam Deck flows, camera/HUD, LT01–LT06 onboarding beats, pause/settings/save/load/restart/undo/replay, non-color accessibility, failure/dead-state communication, animation timing, and immediate-consequence preview boundaries. UI may explain causality but must not become a multi-beat solution scanner.
