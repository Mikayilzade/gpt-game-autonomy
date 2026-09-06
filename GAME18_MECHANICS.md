# GAME #018 — PHASE 4 MECHANICAL ARCHITECTURE

Date: 2026-09-06
Selected concept: **LOCAL TIME**
Status: PHASE 4 COMPLETE — CONTENT ARCHITECTURE NEXT
Production implementation: NO

## 1. Mechanical identity
LOCAL TIME is a deterministic authored causal puzzle. The player moves public local-time zones among discrete authored sockets, then commits one discrete Resolve beat.

Canonical distinction:
- **CURRENT predicates** are recomputed from the clock configuration every Resolve and may freely become true/false.
- **PERSISTENT milestones** are earned state transitions and never reverse merely because a clock moves away.
- Permanent hazards/lockouts are persistent bad milestones.

There is no simulation between Resolves, no rewind, no continuous elapsed time and no hidden schedule.

## 2. Canonical state
`CaseState`: case_id, beat_index, move_count, optional move_budget/beat_budget, clock_zones, sites, objects, carriers, objectives, constraints, checkpoint_snapshot, public case_flags, terminal_status.

`SiteState`: site_id, logical coverage links, base_tags, derived current_time, derived current_predicates, persistent_state, resident objects, exactly one reusable rule_family_id plus bounded public params, hazard_flags.

`ObjectState`: object_id, object_family, persistent_state enum, logical location, public_tags, hazard_flags. No hidden timestamps or age.

`ClockZone`: clock_id, semantic time_label, current socket_id, footprint_id, movable flag, move_cost (default 1), allowed_socket_ids. Labels never tick.

`CarrierState`: carrier_id, public finite path, transfer rule, optional payload, public enabling predicate. Carriers are not hidden-schedule NPCs.

Decorative animation/camera/audio state is never puzzle authority.

## 3. Placement and footprint legality
- Clocks occupy only authored legal sockets.
- Every socket+footprint resolves to an explicit finite set of covered site IDs.
- No partial logical coverage.
- Preview shows destination sockets and exact sites that would be covered.
- Footprints may overlap empty ground.
- Two clocks may cover the same logical site only if their time_label is identical.
- Different labels covering one site is an illegal configuration; there is no priority/winner rule.
- Fixed local-time areas are simply non-movable clock zones.
- Moving to a different legal socket charges move_cost. Inspect/cancel/no-op costs 0.
- Several clock placements may occur before one Resolve if budgets allow.

## 4. Time-label semantics
07:55, 08:00, 08:05, etc. are semantic public labels, not points on a continuously running clock. 08:05 is not five simulated minutes after 08:00. Rules test labels; ordered chains are state-machine order, not elapsed-time simulation. Earlier-looking labels never rewind persistent state.

## 5. Reusable transition grammar
All shipping process families must compile into these primitives:

**G1 CURRENT** — derive public predicates from the pre-Resolve snapshot, e.g. Bridge OPEN_NOW iff local time = 08:00.

**G2 ADVANCE** — if persistent state A and public condition C(snapshot), advance A->B. Default max one persistent advance per entity per Resolve, preventing RAW->RISEN->BAKED in one beat.

**G3 LOCKOUT/HAZARD** — if source state and hazard condition hold in the same snapshot, advance to a persistent bad state such as WILTED. Positive and bad intents for one entity must be mutually exclusive; validator rejects ambiguity.

**G4 ACCEPT** — if eligible cargo is already present at destination input in the initial snapshot and destination current predicate holds, advance acceptance/delivery state.

**G5 DISPATCH** — if source milestone and current predicate hold, create a deterministic transfer intent.

**G6 CARRIER/HANDOFF** — after persistent transitions commit, each enabled carrier moves at most one public hop. A newly arrived object cannot also be accepted in that same Resolve; it becomes eligible next Resolve.

**G7 COUPLED CURRENT TRIGGER** — require multiple CURRENT predicates in the same immutable pre-transition snapshot, e.g. Station at 08:05 AND Bridge OPEN_NOW.

**G8 PERSISTENT FLAG** — public irreversible milestones such as TRAIN_DEPARTED or FLOWERS_COLLECTED.

No bespoke hidden scripts are allowed.

## 6. Canonical Resolve order
1. **Legality gate:** reject illegal clock/socket/conflict configuration without consuming a beat.
2. **Snapshot S0:** freeze persistent states, object locations, clock placements, budgets and coverage.
3. **Derive C0:** compute effective local times and all CURRENT predicates from S0.
4. **Evaluate intents:** all ADVANCE, LOCKOUT, ACCEPT, DISPATCH and coupled triggers read S0+C0 only.
5. **Compatibility check:** contradictory intents are an authoring error, never runtime tie-breaking.
6. **Commit persistent writes** atomically.
7. **Carrier stage:** commit dispatch/handoffs; each carrier moves max one hop; arrival stops there.
8. **Recompute presentation/current truth** under unchanged clock layout.
9. **Check hard-fail, success, budget/dead-state** at the boundary.
10. **Increment beat and record exact public reason trace.**

Animations visualize already-computed logic and cannot affect outcome.

## 7. Moves, beats and limits
A move is a confirmed clock relocation. A beat is one successful Resolve.

Defaults:
- onboarding: 1 clock, 1–3 beats;
- normal: 1–3 clocks, 1–5 beats;
- late synthesis: <=3 clocks, normally <=6 beats;
- mastery ceiling: <=3 clocks, <=12 moves, <=8 beats without explicit re-review.

Hard content ceilings:
- <=3 player-controlled clocks;
- <=8 logically relevant sites;
- <=10 reusable process families;
- <=2 active carrier channels in normal campaign;
- <=4 semantic time labels in normal cases, mastery max 5;
- no difficulty via long execution chains.

## 8. Objectives, win/fail and dead state
Objective language is built from public predicates:
MILESTONE(entity,state), CURRENT(site,predicate), OBJECT_AT(object,site), FLAG(flag,value), ALL, ANY, NOT, AT_MOST_MOVES, AT_MOST_BEATS.

Success is checked only at a Resolve boundary after committed transitions and handoffs.

Hard fail is allowed only when an explicit public irreversible state proves a required objective impossible, and must name the violated rule/objective.

Budget exhaustion checks success first, then fails if unmet.

A non-obvious state may be labeled DEAD only when an exhaustive deterministic solver over the exact remaining finite action graph proves there is no winning continuation. Otherwise the game may offer Restart but cannot claim impossibility.

## 9. Recovery semantics
- Restart restores the exact initial canonical state.
- Before every Resolve, store the exact pre-Resolve planning snapshot.
- Undo Placement reverses an unresolved clock move and refunds its cost.
- Undo Turn restores the pre-Resolve checkpoint. UX calls this recovery/undo, never in-fiction rewind.
- Replay Last Resolve is non-authoritative animation only.

Because rules/state are public, Undo creates no hidden-information exploit.

## 10. State invariants
1. Every movable clock occupies exactly one legal socket.
2. No site has two different local-time labels simultaneously.
3. Coverage derives only from clock socket+footprint data.
4. Current predicates are derived, never authoritative stored state.
5. Persistent transitions follow declared reusable family edges only.
6. Clock movement alone never reverses a persistent milestone.
7. No rule depends on real elapsed time or animation.
8. Carrier movement is max one hop per Resolve.
9. Newly arrived cargo cannot be accepted until a later Resolve.
10. Every mutation has a public causal reason trace.
11. Identical canonical state + actions gives identical result.
12. Runtime never tie-breaks ambiguous transition conflicts.
13. DEAD requires exhaustive solver proof.
14. Decorative entities cannot affect logic.
15. Cross-site dependencies must be explicit public predicates.
16. Multiple valid solutions are accepted.
17. Earlier-looking time labels have no rewind semantics.

## 11. Validator obligations
Structural:
- unique IDs and valid references/enums;
- explicit footprint sets;
- legal clock sockets and conflicts;
- valid budgets and hard ceilings.

Determinism:
- reject contradictory reachable intents;
- reject runtime randomness;
- reject carrier-order dependence;
- verify one-hop arrival boundary;
- verify serialization round-trip equivalence.

Solvability:
- every shipping case has >=1 exhaustive solver-proven winning path;
- store shortest cost as (moves, beats);
- ensure objectives are not accidentally initially satisfied;
- include all hazards and constraints in solver state.

Human-proof:
- after earliest tutorials, every case stores a 2–6 claim causal proof rather than an intended action script;
- at least one claim connects two reusable rule interactions, e.g. “Collect flowers before any 08:05 footprint can touch Garden”;
- proof must reduce meaningful search before enumeration.

Enumeration resistance:
- reject cases solved only by scanning near-identical sockets;
- reject one repeated obvious placement as a dominant strategy;
- reject difficulty based mainly on giant permutation counts;
- reject previews that rank winning moves.

Reasoning must compress search while all information remains public.

## 12. Exact demo simulations

### LT01 — Breakfast at Eight
Clock 08:00; Bakery RAW->RISEN at 08:00; Bridge OPEN_NOW at 08:00. A shared socket can cover both. Goal RISEN + Bridge OPEN_NOW. One shared Resolve succeeds; a two-beat “rise then move clock to bridge” solution is also valid if budget allows, proving persistence.

### LT02 — Five Minutes Later, Somewhere Else
Fixed 07:55 covers Garden; movable 08:05. Dough starts RISEN and bakes at 08:05. Flower UNCOLLECTED becomes COLLECTED at safe 07:55, but UNCOLLECTED + 08:05 -> WILTED permanently. Required causal fact: collect flower before dangerous 08:05 exposure.

Repair from Round C: “pickup” is now a public one-shot milestone, not a new manual player verb.

### LT03 — Shared Shadow
Clock 08:00 covers Bridge; 08:05 covers Station. Station sets TRAIN_DEPARTED only if Station current 08:05 and Bridge OPEN_NOW in the same C0 snapshot. The train animation does not later re-check the bridge.

### LT04 — Handoff
Bread begins RISEN.
Beat 1: Bakery under 08:05 -> BAKED.
Beat 2: dispatch/carrier moves baked parcel one hop to destination input.
Beat 3: destination under 08:10 ACCEPT -> DELIVERED.

No bake+move+accept cascade in one beat. This repairs Round-C ambiguity.

### LT05 — Bad Shortcut
Two zones, Bakery, Garden, Bridge. Bread needs 08:05; flower must be COLLECTED at 08:00 before any 08:05 footprint touches Garden; Bridge current-open requires 08:00. One tempting 08:05 socket covers Bakery+Garden and is fatal if used too early. Human proof: Garden collection must precede dangerous bakery placement.

### LT06 — Little Town, Different Times
Fixed 07:55 + movable 08:00 and 08:05. Bakery RAW->RISEN->BAKED across separate Resolves; Greenhouse collection is safe under 07:55; Bridge open at 08:00; Station departure requires simultaneous Station 08:05 + Bridge 08:00. Final objectives mix BAKED + TRAIN_DEPARTED with final current Bridge OPEN and Greenhouse safe.

The case uses no new grammar primitive and accepts multiple valid orderings.

## 13. Anti-enumeration authoring gate
After Chapter 1, normal cases should contain at least two of:
- irreversible prerequisite before hazardous exposure;
- simultaneous current predicates requiring distinct clock layouts;
- persistent milestone enabling later acceptance;
- footprint helping one process while threatening another;
- handoff forcing an additional beat boundary;
- final objective mixing current and persistent truth;
- move budget that matters only after causal ordering is understood.

At least one must be expressible as a short causal sentence before solving.

Never use hidden outcomes, random hazards, secret interactions, giant socket counts, tiny visual differences or arbitrary exception buildings.

## 14. Acceptance result
Phase 4 fixes exact state boundaries, placement/overlap semantics, discrete time semantics, transition grammar, Resolve ordering, move/beat accounting, objectives and dead-state rules, recovery, limits, invariants, validator/solver obligations, LT01-LT06 simulations and anti-enumeration gates.

**PHASE 4 MECHANICAL ARCHITECTURE = COMPLETE.**

# NEXT DESIGN STEP — PHASE 5 CONTENT ARCHITECTURE
Create canonical `GAME18_CONTENT.md`. Define <=10 reusable process families that instantiate this grammar; 36 campaign + 12 mastery structure; site/object/carrier data fields; chapter progression and dependency matrix; authored-case templates; validator metadata; asset-semantic families; tutorial-to-synthesis sequencing; anti-repetition gates; and expansion boundaries. Simulate representative early/mid/late cases to prove the catalog needs no bespoke exceptions. Do not alter Phase-4 causality without explicitly documenting a contradiction and repair.
