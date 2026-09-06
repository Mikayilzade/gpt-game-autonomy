# GAME #018 — PHASE 2 CONCEPT TOURNAMENT

Date: 2026-09-06
Status: ROUND C COMPLETE — WINNER SELECTED: LOCAL TIME
Production implementation: NO
Authority: below START_HERE.md, STATUS.md, GAME_INDEX.md, GAME18_RESEARCH.md.

## Prior rounds retained
Round A reduced 12 candidates to six. Round B reduced those six to three: LOCAL TIME, ONE MORE CHAIR, AFTERIMAGE DELIVERY. UNFINISHED SENTENCES, THE ROOM AFTER YOU and TIDE TABLE FOR TWO remain killed. Round C gives the three survivors equal final proof obligations and selects exactly one winner.

# ROUND C — HEAD-TO-HEAD FINAL PROOF

## A1 — LOCAL TIME — WINNER

### Six-case 25–35 minute demo
**LT01 — Breakfast at Eight.** One movable 08:00 clock-zone, bakery and bridge. Dough advances RAW -> RISEN when covered at Resolve; bridge is OPEN only while currently covered. Goal: rise dough and finish with bridge open. Teaches current predicates versus persistent milestones.

**LT02 — Five Minutes Later, Somewhere Else.** Add fixed 07:55 area and movable 08:05 zone. RISEN bread bakes when exposed to 08:05; flowers permanently close if exposed to 08:05 before pickup. Goal: bake bread without closing flowers. Teaches that local time is spatial exposure, not a rewindable global timeline.

**LT03 — Shared Shadow.** Two clock-zones have footprints large enough that a placement can cover two sites. Station departs at 08:05 only while bridge is currently open. Player must arrange 08:00 over bridge and 08:05 over station simultaneously while protecting flowers. First strong screenshot/GIF proof.

**LT04 — Handoff.** Bakery output becomes a parcel token carried automatically along a short public conveyor after baking. The parcel retains BAKED state outside the clock-zone; destination accepts it only under 08:10. Player sequences three clock placements. Teaches persistent process state moving between local conditions.

**LT05 — Bad Shortcut.** Two zones, four sites, three moves. Obvious 08:05 placement progresses bakery but permanently closes a flower needed later. Multiple placements are locally useful; only causal ordering solves all predicates. Introduces failure explanation by exact affected rule.

**LT06 — Little Town, Different Times.** Bakery, bridge, station, greenhouse, two movable zones and one fixed zone. Goal combines two persistent milestones and two simultaneous current predicates. There are multiple valid solutions; demo ends on a town visibly showing different clocks at once while all processes line up.

Demo promise: by 30 minutes a player can explain, “I move patches of local time around the town; things react to the time covering them, and completed steps stay completed.”

### Representative hour-5 loop
Hour 5 is not LT01 with more buildings. A representative puzzle has three movable zones (08:00, 08:05, 08:10), 6–7 sites and two carrier handoffs. Public process graph: seedlings GERMINATE under 08:00; once germinated they may be transported; greenhouse vent is OPEN only under 08:05; kiln can FIRE a prepared mold under 08:10 but heat permanently WILTS uncollected flowers; station dispatch requires current 08:10 while bridge is current 08:05. The player first identifies which states are irreversible milestones and which are simultaneous predicates, then chooses zone footprints/order so one exposure prepares a later handoff without poisoning another site. Late mastery comes from composition of public rule families, overlapping footprints and current-vs-persistent causality, not from hidden schedules or larger arithmetic.

### Content and production target
Target 36 campaign puzzles + 12 mastery. Six chapters of six can introduce: single current predicates; persistent milestones; overlapping footprints; handoffs; multiple clock zones; coupled current/persistent synthesis. Reuse one compact town kit and roughly 8–10 process rule families (rise/bake/open/depart/germinate/close/fire/accept/dispatch etc.), each represented with clear state animation/iconography. Asset burden low-to-moderate; level-authoring burden moderate but bounded by socketed zone positions and discrete Resolve beats.

### Strongest dominant strategy and defense
Dominant threat: enumerate every clock placement/order as switches. Defense is not to hide outcomes. Authoring validator must reject puzzles whose shortest human proof is raw enumeration, require at least one causal dependency chain of 2+ rule interactions after early tutorial, cap legal placements but combine overlapping zones/current predicates/persistent milestones, and record a 2–6 step human proof. Preview may show only immediate coverage and public rules triggered on the next Resolve, never solve future move sequences. Reset remains cheap; difficulty must survive informed experimentation.

### Store hook + 10-second proof
**Store hook:** “Move pockets of local time around a tiny town, lining up bakeries, bridges, flowers and trains that all need different times at once.”

10-second trailer: drag an 08:00 clock-zone over bakery -> dough visibly rises; slide it onto bridge -> bridge opens while bread stays risen; place 08:05 over station -> train leaves across the still-open bridge while nearby flowers remain safely at 07:55.

### Current commercial/saturation distinction
Fresh September 2026 check finds time-puzzle visibility, but prominent examples such as Causal Loop and Timefract center rewind/forward movement, past selves/clones and timeline manipulation. LOCAL TIME explicitly forbids rewind/retrocausality and instead spatializes public time conditions as movable zones. That gives a visually distinct diorama interaction and avoids competing as another time-loop platformer. Current high-profile puzzle releases also raise the quality bar for systemic clarity, so the demo must prove the rule visually rather than rely on “time manipulation” as the pitch.

Closest analogue risk: broad “time manipulation puzzle” labeling can make the product look generic. Marketing and UI must consistently say local-time zones / different times in one town, never imply rewinding history.

### Portfolio distinction
Clear from #001–#017. It does not edit a cyclic program (#011), reconstruct historical evidence (#013), infer hidden agents (#017), or transform remembered objects (#007). Its core state is public spatial exposure to local clock conditions plus irreversible process milestones.

### Fatal kill criterion
Kill/reopen selection if Phase 4 cannot express hour-5 puzzles with <=3 clocks, <=8 sites, <=10 reusable process-rule families and one universal no-retrocausality model; or if useful puzzles require bespoke exceptions/continuous timers/time travel; or if playtesters consistently interpret movement as rewinding objects despite presentation.

**ROUND-C VERDICT: CLEAR PASS.** Strongest hook/depth/scope balance and cleanest product-thesis path.

---

## A8 — ONE MORE CHAIR — RUNNER-UP / KILLED FOR GAME #018

### Six-case demo
OMC01 insert one empty chair to break a clockwise dish pass. OMC02 matching preference causes first adjacent keeper. OMC03 held dish blocks acceptance. OMC04 unserved dish restarts next course. OMC05 dessert starts opposite last keeper. OMC06 two courses, two dishes and insert/remove choice create coupled ownership constraints.

The demo is charming and extremely readable, but its first 30 minutes already consume a large fraction of the clean universal rule vocabulary.

### Hour-5 loop
Seven guests, three courses, two movable empty chairs, three dishes. Course-1 keeper determines course-2 serving origin; occupied hands redirect a second dish; one intentionally unserved dish restarts later. The player chooses insert/remove operations across courses to satisfy three final ownership constraints.

This is deeper than tutorial adjacency, but still fundamentally circular propagation over a tiny slot set. To keep expanding, it pressures guest-specific exceptions, more dish states or more etiquette rules — exactly the complexity ceiling Round B identified.

### Content / burden
30 campaign + 10 mastery plausible with very low assets, but 36+12 high-confidence nonrepetitive cases are less certain than LOCAL TIME. Strong controller/Deck fit and cheapest production of finalists.

### Dominant strategy
Try every chair slot and Resolve. With <=8 guests and 1–2 chair operations, action space is tiny. Multi-course persistence slows brute force but cannot remove it without increasing rule count/action sequence length. A validator can reject one-step triviality, yet late content risks becoming authored permutations rather than fresh conceptual discoveries.

### Store hook + 10-second proof
“Add one empty chair to a dinner table and watch etiquette ripple through every course.” Trailer: chair inserted; wine stops/restarts; soup keeper changes; dessert origin flips across table.

### Commercial distinction
Fresh searches did not expose a close current Steam analogue centered on deterministic dinner-table etiquette, so theme/presentation is distinct. Risk is not saturation but perceived lightweight/mobile-puzzle depth: screenshots can look like a small adjacency toy unless consequences are animated exceptionally well.

### Portfolio distinction
Very clear and charmingly different from prior portfolio.

### Fatal criterion / final verdict
Kill if 36+12 requires >6 universal etiquette rules, >8 guests or guest-specific exceptions. Round C cannot confidently show hour-5 novelty without approaching that boundary.

**VERDICT: STRONG RUNNER-UP, NOT SELECTED.** Best scope/charm ratio but weakest defense against tiny-action brute force and content exhaustion.

---

## A9 — AFTERIMAGE DELIVERY — RUNNER-UP / KILLED FOR GAME #018

### Six-case demo
AD01 first route writes arrows. AD02 take a longer route to prepare a gate for next delivery. AD03 opposite traversal overwrites an arrow. AD04 trace ages 2 -> 1 -> gone. AD05 bike consumes/erases departure trace while van obeys gates. AD06 choose delivery order plus routes so one trace is written, preserved, refreshed and consumed.

### Hour-5 loop
A 13-node neighborhood, 16 edges, four deliveries, trace age 2, van/bike. Gate needs eastbound trace; dock rejects outward approach; one route refreshes an aging trace while another would overwrite it. Player chooses order and route family, reasons about which edge state must survive until delivery 4, then executes.

This genuinely extends tutorial grammar through lifecycle coupling, but route search remains the dominant cognitive surface.

### Content / burden
36 campaign + 12 mastery plausible. Low-to-moderate art, moderate graph authoring, strong need for editor/solver/validator. City layouts must be visually distinct enough to prevent every level reading as another abstract graph.

### Dominant strategy
Generic path enumeration/search. Defense: tiny named-landmark graphs, coupled order + trace lifespan, human-proof gate, no future-state oracle. Even so, a player can reasonably experience the game as “try routes until arrows line up,” and solver-like search scales faster than conceptual vocabulary.

### Store hook + 10-second proof
“Every delivery leaves temporary one-way traces on the streets, so today’s route builds tomorrow’s road rules.” Trailer: van detours and paints arrows; second courier follows/open gate; bike crosses and erases trace; third route suddenly changes.

### Current commercial/saturation distinction
Delivery-route games and path puzzles are common at broad category level; examples include Package Rush-style route management and many casual delivery/pathfinding puzzles. AFTERIMAGE’s state-writing lifecycle is materially different, but store discovery risks first classifying it as another routing game. It needs more explanation than LOCAL TIME before the unique second-order mechanic becomes obvious.

### Portfolio distinction
Acceptable, but temporary state written by movement has mild conceptual adjacency to prior persistent-state designs. Still not a direct collision.

### Fatal criterion / final verdict
Kill if late depth needs >2 vehicle families, >16 intersections, arbitrary gate types or hidden traffic. Round C shows a coherent game, but generic pathfinding remains too central relative to the novel trace layer.

**VERDICT: STRONG RUNNER-UP, NOT SELECTED.** Better raw agency than LOCAL TIME, weaker market legibility/differentiation and higher risk that the novelty becomes route-search bookkeeping.

---

# FINAL HEAD-TO-HEAD

| Gate | LOCAL TIME | ONE MORE CHAIR | AFTERIMAGE DELIVERY |
|---|---|---|---|
| One-sentence hook | Excellent | Excellent | Good |
| 10-second visual proof | Excellent | Excellent | Good after context |
| Hour-5 same-grammar depth | Excellent if process vocabulary stays bounded | Borderline-good | Good |
| 36+12 confidence | High | Medium | High |
| Dominant-strategy resistance | Good with causal-proof authoring | Weakest | Medium |
| Production burden | Low-moderate | Lowest | Low-moderate + graph tooling |
| Market-category distinction | Strong | Strong theme, lightweight perception risk | Weaker broad category |
| Portfolio distinction | Strong | Strongest | Good |
| Product-thesis clarity | Strongest | Good | Good |

# ROUND C RESULT

**SELECTED GAME #018 CONCEPT: LOCAL TIME.**

Why it wins:
1. the core inversion is instantly visual: several local times coexist spatially in one tiny town;
2. Round B produced a clean universal causality model — clock coverage changes current conditions, while completed process milestones never reverse;
3. Round C demonstrates a six-case demo and a materially richer hour-5 loop without time travel, continuous simulation or bespoke exceptions;
4. it supports a bounded 36+12 authored puzzle product with one reusable diorama kit and roughly 8–10 process rule families;
5. its closest current time-puzzle competition is primarily rewind/clone/timeline manipulation, leaving a clearer interaction identity;
6. it has stronger resistance to trivial brute force than ONE MORE CHAIR and less generic route-search gravity than AFTERIMAGE DELIVERY.

ONE MORE CHAIR and AFTERIMAGE DELIVERY are killed for Game #018 and become portfolio history only. They are not backup canon to import silently later.

# NEXT DESIGN STEP
Proceed to **Phase 3 — Product Thesis Lock for LOCAL TIME**. Freeze target player/platform, genre frame, one-sentence hook, core fantasy, exact session/case loop, player verbs, current-condition vs persistent-milestone causality contract, demo promise, scope ceiling, content target, fairness/readability contract, presentation thesis and explicit exclusions. No production implementation.