# GAME #018 — PHASE 5 CONTENT ARCHITECTURE

Date: 2026-09-06
Selected concept: **LOCAL TIME**
Status: PHASE 5 COMPLETE — UX / PRESENTATION NEXT
Production implementation: NO

## 1. Final content grammar
The base campaign uses exactly eight reusable semantic families, all instantiated through `GAME18_MECHANICS.md`:
1. CURRENT WINDOW — one public current predicate under one required time label.
2. ONE-SHOT PROCESS — one persistent advance under a visible condition.
3. ORDERED PROCESS — 2–4 persistent stages, max one step per Resolve.
4. EXPOSURE CONSEQUENCE — a visible vulnerable state can become an irreversible bad state.
5. ACCEPT / SERVICE — an eligible object is accepted only while the destination window is true.
6. DISPATCH / CARRIER — a ready source dispatches through one public carrier hop.
7. COUPLED CURRENT EVENT — two, rarely three, CURRENT predicates must hold in one snapshot.
8. PERSISTENT PUBLIC FLAG — once-earned public milestones such as TRAIN_DEPARTED.

Art skins may vary fiction/animation but never semantics. The optional public counter primitive is outside the base 36-case campaign.

## 2. Reusable town kit
Bakery/kitchen/kiln: one-shot or ordered process.
Garden/greenhouse: process + exposure consequence + flag.
Bridge/gate/crossing: current window.
Station/depot/ferry: current window + accept + coupled event.
Market/post office/shop: current window + accept.
Tram/handcart/trolley: dispatch/carrier.
Plaza/courtyard/clock tower: sockets and footprints.
Bell/signal/fountain valve: coupled event/flag.

No skin may contain a private rule.

## 3. Campaign structure — exactly 36 cases
Six chapters of six.

### Chapter 1 — identity, Cases 01–06
LT01–LT06 stay as campaign opening and demo.
Teach: current state; persistence after clock leaves; two local times at once; first handoff; irreversible bad exposure; three-clock synthesis.
Ceiling: <=3 clocks, <=5 sites, <=4 beats.

### Chapter 2 — footprint reasoning, Cases 07–12
07 compatible shared footprint.
08 broad footprint helps one site and threatens another.
09 persistent preparation before repurposing a clock.
10 two clocks with mutually exclusive useful sockets.
11 final objective mixes CURRENT + PERSISTENT truth.
12 first meaningful move budget.
Ceiling: <=2 clocks normally, <=6 sites, <=5 beats.

### Chapter 3 — handoffs, Cases 13–18
13 source -> carrier -> destination.
14 destination time differs from source time.
15 arrival must wait a Resolve before acceptance.
16 two candidate destinations, one causally viable.
17 cargo preparation competes with a visible bad exposure.
18 synthesis with two handoffs + final current gate.
Ceiling: <=2 carrier channels, <=7 sites, <=6 beats.

### Chapter 4 — simultaneity, Cases 19–24
19 two current windows together.
20 persistent preparation enables coupled event.
21 footprint conflict blocks naive simultaneity.
22 three clocks with only two coupled requirements.
23 coupled event plus carrier arrival boundary.
24 synthesis: exposure consequence + coupled trigger + move budget.
Ceiling: <=3 clocks, <=8 sites, <=6 beats.

### Chapter 5 — preserve earned state, Cases 25–30
25 earn a milestone before exposing another site.
26 two safe orderings, one shorter.
27 locally useful placement creates an irreversible bad state.
28 final CURRENT requirement forces leaving a productive site.
29 carrier route competes with safe footprint order.
30 open synthesis with two materially different winning approaches.

### Chapter 6 — town-wide synthesis, Cases 31–36
31 ordered process + final current.
32 two cargo objects share service windows.
33 coupled trigger must occur before a bad exposure.
34 three clocks + two carriers + move budget.
35 multiple solver-proven routes, no narrow trick.
36 finale: <=3 clocks, <=8 sites, all core ideas, no new semantic family.

## 4. Optional mastery — exactly 12 cases
M01–M12 unlock in pairs after Chapters 1–6. Same eight families, greater precision only:
M01 minimal-move LT06 remix;
M02 safe-footprint proof;
M03 ordered process under tight budget;
M04 two carriers sharing one destination window;
M05 coupled event with a misleading legal socket;
M06 final CURRENT + two persistent milestones;
M07 irreversible ordering with multiple safe routes;
M08 symmetric-looking sockets with different causal consequences;
M09 three-clock synthesis;
M10 two-cargo delivery order;
M11 all-family remix;
M12 capstone, <=8 sites, <=5 labels, <=8 Resolves, short human proof.

## 5. Introduction matrix
| Element | First teach | First combination | First pressure |
|---|---:|---:|---:|
| CURRENT WINDOW | 01 | 03 | 19 |
| ONE-SHOT | 02 | 06 | 25 |
| ORDERED PROCESS | 09 | 12 | 31 |
| EXPOSURE CONSEQUENCE | 05 | 12 | 24 |
| ACCEPT | 04 | 13 | 23 |
| CARRIER | 04 | 13 | 29 |
| COUPLED EVENT | 06 | 19 | 24 |
| PUBLIC FLAG | 06 | 18 | 33 |
| final CURRENT goal | 11 | 18 | 31 |
| move budget | 12 | 18 | 34 |
| three clocks | 06 | 22 | 34 |
| two carriers | 18 | 24 | 34 |

A case introducing a new semantic family does not simultaneously introduce another unrelated semantic family.

## 6. Authored case schema
Every case stores: case_id, chapter_id, tier, title, one-line objective, clocks, legal sockets, footprint table, sites, objects, carriers, family instances, objectives, constraints, initial state, budgets, difficulty band, new/reused concept IDs, validator metadata, shortest solver result, human_causal_proof[], anti_enumeration_tags[], art_kit_id, optional efficiency goal, demo flag, mastery unlock dependency.

No case embeds arbitrary runtime code.

## 7. Human proof requirement
After earliest tutorials, every case stores 2–6 short causal claims rather than an intended action list.
Example:
1. Garden must be secured before any 08:05 footprint reaches it.
2. Bakery needs 08:05 only after that milestone.
3. Station departure needs Bridge=08:00 and Station=08:05 in one snapshot.

The proof must use only public rules and materially reduce search before enumeration.

## 8. Reuse targets
Across 36 campaign cases:
CURRENT >=20; ONE-SHOT >=14; ORDERED >=8; EXPOSURE 10–14; ACCEPT >=10; CARRIER 8–12; COUPLED 8–12; FLAG >=10.
No family should dominate every case after Chapter 2.

## 9. Variety gates
Adjacent cases differ in at least three of: family combination, causal ordering, clock count, footprint topology, objective type, exposure role, carrier involvement, final CURRENT requirement, budget pressure, viable solution family.

Within each chapter:
- no more than two cases share the same primary proof shape;
- at least one has >1 materially different winning route;
- at least one emphasizes persistence;
- at least one emphasizes simultaneous current truth.

If testers describe a case as the prior puzzle with renamed buildings, redesign or remove it.

## 10. Tutorial rules
New families use generous budgets. First exposure consequence previews the exact footprint. First handoff separates dispatch, travel and acceptance across Resolve boundaries. First coupled event highlights all required sites together. Do not teach overlap, exposure consequence and carrier simultaneously. Efficiency goals remain optional until chapter completion. Tooltips explain conditions, not recommended actions.

LT01–LT06 remain the planned 25–35 minute demo.

## 11. Representative proofs
**Case 09:** 08:00 + 08:05. Bakery RAW->RISEN->BAKED; Bridge current-open at 08:00. Earn persistent bread stages, then restore final bridge time.

**Case 18:** Bakery ordered process, Dispatch carrier, Station accept, Bridge current window. Finish cargo, allow one arrival boundary, accept at destination window, restore bridge current condition.

**Case 34:** Three clocks, seven sites, two carriers. One cargo needs process->carrier->accept; Garden has exposure consequence; final departure needs Bridge 08:00 + Station 08:05 simultaneously. Human proof: secure Garden, prepare cargo before carrier window, reserve final relocations for the simultaneous state.

All fit Phase-4 ceilings and need no bespoke exception.

## 12. Art/content boundary
One modular miniature-town kit: 6–8 building shells, 4–6 civic/transport props, 3 process-animation families, 2 carrier silhouettes, reusable clock overlays/socket markers, reusable state-change icons/props. No puzzle requires a unique environment.

## 13. Authored vs systemic
Authored: socket graph, footprints, initial state, family parameters, objectives, budgets, art layout, human proof.
Systemic: legality, snapshot derivation, transitions, carrier hops, objective evaluation, reason trace, solver/validator.
No infinite procedural case generator in the base product.

## 14. Expansion boundary
Future content may add cases, art skins and footprint patterns. It may not silently add rewind, continuous clocks, hidden schedules, physics placement or private NPC behavior. Any new semantic family requires new reviewed design authority.

## 15. Scope-reduction gates
Reduce 36+12 before adding mechanics if >20% of cases share the same proof shape; later chapters routinely require >8 sites; more than eight semantic families appear necessary; difficulty comes mostly from socket count; art needs >10 bespoke landmark systems; mastery relies on arbitrary budget harshness; or LT01–LT06 cannot teach the model in 25–35 minutes.

Preferred order: remove repetitive cases, then reduce mastery count. Do not invent mechanics merely to preserve count.

## 16. Phase-4 consistency
No contradiction with `GAME18_MECHANICS.md` found. Base campaign uses eight semantic families; optional public counters remain outside campaign.

**PHASE 5 CONTENT ARCHITECTURE = COMPLETE.**

# NEXT DESIGN STEP — PHASE 6 UX / PRESENTATION
Create `GAME18_UX.md`. Define first boot, progression, mouse/controller/Steam Deck navigation, placement preview, footprint readability, site rule cards, current-vs-persistent language, Resolve animation/reason trace, undo/restart/checkpoint presentation, failure messaging, accessibility, settings/save/load, and moment-by-moment LT01–LT06 onboarding. Evaluate whether one-beat consequence preview improves comprehension without becoming an oracle. Do not begin production implementation.
