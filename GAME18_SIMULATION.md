# GAME #018 — PHASE 9 WHOLE-GAME SIMULATION

Date: 2026-09-07
Game: **LOCAL TIME**
Status: PHASE 9 COMPLETE — PHASE 10 ADVERSARIAL REVIEW NEXT
Production implementation: NO

Authority: all prior active Game #018 files. This pass simulates the frozen product end-to-end and repairs contradictions; it does not add a ninth gameplay family.

## 1. Simulation verdict
The game remains coherent from first boot through campaign, mastery, persistence and hostile play, provided three clarifications below are canonical: every case has a finite authored `resolve_limit`; a DISPATCH that starts a carrier cannot repeatedly re-enable the same departure; and Undo Resolve restores puzzle state but never decrements the profile/save generation used for persistence conflict handling.

The 30-case quality floor remains credible. Thirty-six campaign cases remain a target, not yet a promise: the late-case proof-shape audit identifies four clusters requiring adversarial differentiation before all 36 can ship.

## 2. First boot -> LT01–LT06
First boot defaults to readable UI scale at 1280x800, asks no account/network question, and reaches case select/tutorial immediately. Settings can be changed before play. Steam absence does not block local play.

LT01 sequence: player inspects RAW dough and Bridge. Place 08:00 on Bakery -> Resolve -> RAW becomes RISEN and trace marks DONE. Relocate 08:00 to Bridge; RISEN remains. Resolve -> Bridge NOW OPEN and objective succeeds. Repeated Resolve at Bakery after RISEN creates NO_CHANGE plus beat use, proving no hidden duration.

LT02: narrow 08:05 Bakery placement bakes safely. Broad Bakery+Flower placement visibly warns permanent consequence; Resolve both bakes and closes unprotected flower from Snapshot0. Undo Resolve restores exact pre-state. Moving an earlier-looking label afterward never reverses BAKED/CLOSED.

LT03: two labels are simultaneously visible. Bridge=08:00 and Station=08:05 are evaluated in one Snapshot0; dispatch occurs only when both are true. Illegal ambiguous same-site coverage cannot commit. This is the first strong proof that the product is spatial local time, not rewind.

LT04: BAKED parcel exists before dispatch. Dispatch/load occurs on one Resolve; carrier executes one step after non-carrier commit; newly arrived parcel is not ACCEPTed until a later Resolve with Destination=08:10. Stage presentation PREPARE -> DISPATCH/HANDOFF -> ARRIVE -> ACCEPT matches logic.

LT05: protection must be earned before tempting broad exposure. Snapshot0 prevents earning protection and consuming it as an undeclared same-Resolve prerequisite. Harmful exposure remains explainable and Undo remains cheap.

LT06: two movable labels + one fixed label compose persistent milestones and simultaneous NOW clauses. Tutorial prompts are absent for the final solve. If validator cannot prove the number of alternate solutions claimed by copy, copy must not promise it.

Onboarding conclusion: every semantic family needed for the campaign has either been directly taught or demonstrated in composition. No hidden timer, rewind, schedule, reaction input or exception is needed.

## 3. Cases 07–36 proof-shape simulation
These are proof obligations/topologies, not permission to invent bespoke runtime rules. Final authored boards may change while preserving each distinct reasoning shape.

### Chapter 2 — Cases 07–12
07 **Which First?** Two persistent one-step processes share one clock. Proof: final gate needs both DONE; either order works, teaching commutativity and clock reuse.
08 **Narrow Before Broad.** Required process shares a harmful broad footprint with fragile site. Proof: use safe narrow exposure before any unsafe broad exposure, or earn protection first.
09 **Three Stages, Two Places.** One ordered chain needs alternating labels. Proof: one transition/entity/Resolve means apparent shortcut cannot skip the middle state.
10 **Keep the Gate for Last.** Persistent work temporarily steals the label from a current final gate. Proof: earn irreversible milestones first, restore NOW condition only at finish.
11 **Spend a Move Once.** Two processes can be served by one strategically reused placement under move budget. Proof: choose the placement whose footprint advances both compatible prerequisites before relocation.
12 **Shared Morning.** Two chains, one protected site, final current condition. Proof: protection precedes broad exposure; persistent chains finish before clock is committed to final NOW state.

### Chapter 3 — Cases 13–18
13 **Already There.** Prepared parcel reaches endpoint then needs later acceptance. Proof: arrival is not acceptance; destination label is valuable only after payload exists there.
14 **Open Road Departure.** Dispatch requires persistent prepared cargo + current bridge gate. Proof: preparation and simultaneous departure condition are separate obligations.
15 **One Tram, Two Parcels.** Shared carrier serves two payloads in authored finite steps. Proof: dispatch order is constrained by carrier occupancy/location, not hidden transit time.
16 **Receiving Window.** STAMPED parcel -> coupled dispatch -> arrival -> later Market=09:10 acceptance. Proof: reserve receiving label until cargo is actually present.
17 **Beat Ledger.** Generous placement options but finite Resolve budget. Proof: no-change Resolve and premature dispatch attempts consume scarce beats; combine compatible state changes without relying on same-beat cascades.
18 **Coupled Departure.** Prepared cargo plus two simultaneous current predicates enable departure. Proof: persistent preparation frees planning attention; final departure needs both NOW clauses in one Snapshot0.

### Chapter 4 — Cases 19–24
19 **Protect Before Broad.** Explicit protection milestone precedes unavoidable broad hazardous exposure. Proof: hazard footprint is mandatory later, so protection is logically first.
20 **Two Fragile Shops.** Two protection milestones have different prerequisite labels. Proof: order protections to avoid one protection action exposing the other fragile site.
21 **Safe Together.** Coupled action is useful only after protection. Proof: simultaneity is not the hard part; making the simultaneous configuration safe is.
22 **Too Late This Beat.** Tempting Resolve would earn protection and trigger hazard simultaneously. Snapshot0 makes protection unavailable to that same Resolve. Proof: protection must pre-exist.
23 **Two Safe Routes.** Board intentionally supports two different protection orders. Proof: both routes satisfy same necessities but diverge in which safe footprint is exploited; validator must preserve both if advertised.
24 **Glass Morning.** Two risks + process chain + final coupling. Proof: establish protections in dependency order, finish persistent chain, then use otherwise-dangerous broad configuration for final NOW coupling.

### Chapter 5 — Cases 25–30
25 **Two Ends.** Two clocks must occupy coupled endpoints simultaneously. Proof: individual useful placements are insufficient; final geometry must satisfy both current clauses.
26 **Use It, Then Move It.** One clock earns a milestone at site A and is then required at final site B. Proof: persistence is what makes relocation possible.
27 **Same Pair, Different Beat.** Coupled condition is needed twice with a persistent transition between uses. Proof: identical-looking configuration has different consequence because public persistent prerequisite changed.
28 **Three Voices.** First three-site COUPLED_CURRENT. Proof: all three clauses are individually visible and must coexist; no sequential accumulation of NOW predicates.
29 **Departure Geometry.** Carrier dispatch under two-clock coordination. Proof: cargo must already be prepared and two spatial current clauses must align before finite one-shot departure.
30 **Move Budget Synthesis.** Multiple individually legal routes exist but only clock reuse preserves move budget. Proof: identify persistent milestone that lets one clock abandon its earlier duty permanently.

### Chapter 6 — Cases 31–36
31 **Two Ovens, One Door.** Two process chains compete with final current gate. Proof: exploit compatible footprint once, finish both persistent chains, then restore gate.
32 **Protected Delivery.** Relay destination is hazardous until protected. Proof: protect endpoint before dispatch because carrier arrival itself is persistent and cannot be safely rerouted by later clock movement.
33 **Local Relay.** Fixed zone + two movable zones + protection + coupled dispatch + later receiving condition. Proof: protect -> prepare -> coupled dispatch -> arrive -> relocate -> accept.
34 **Crossing Couriers.** At most two carriers, each on finite authored endpoints. Proof: carrier occupancy/location constrains dispatch order; there is no routing search or physical collision simulation.
35 **The Bottleneck.** Tight Resolve budget around one configuration that can satisfy two compatible transitions. Proof: identify the only safe multi-benefit Resolve; all other necessities then fit the remaining beats.
36 **Dependency Braid.** >=2 persistent prerequisites, one protection, one dispatch/handoff, final two-site coupled current objective. Intended proof in <=6 necessities: protect fragile endpoint; earn prerequisite A; earn prerequisite B; configure coupled departure; allow finite handoff/arrival; relocate to final coupled NOW state and Resolve.

## 4. Proof-shape diversity audit
Strongly distinct anchors exist for: commutative persistence (07), chain alternation (09), persistent-before-final-current (10), shared-benefit move economy (11), arrival-vs-acceptance (13), carrier occupancy (15), beat economy (17), pre-existing protection/Snapshot0 (22), alternate protection routes (23), pure simultaneous geometry (25/28), persistence-enabled relocation (26), repeated coupling after state change (27), protected relay (32), two-carrier ordering (34), and bottleneck beat packing (35).

Clusters requiring Phase-10 attack:
- 08 vs 19: both narrow/protect-before-broad; one must be cut or 19 must make unavoidable broad exposure the proof while 08 retains optional narrow-route choice.
- 14 vs 18 vs 29: dispatch + current gating. Keep only if topology differs materially: one gate, two-condition coupling, and spatial two-clock geometry respectively.
- 26 vs 27 vs 31: persistence enables clock reuse. Require different dependency topology, not merely new fiction.
- 32 vs 33 vs 36: late relay/protection synthesis. 32 should isolate protected endpoint, 33 isolate fixed-zone relay timing, 36 must be a true dependency braid rather than 'more of 33'.

If these distinctions fail human review, cut toward 30 rather than add rules.

## 5. Campaign completion and mastery
Campaign completion unlocks no new semantic family. It records completion monotonically, shows mastery access, and allows replay. The product is complete at campaign finish; mastery is optional.

Baseline mastery M01–M08 may use tighter fair budgets, larger reachable graphs, three-site coupling, two carriers and existing optional challenge conditions. M09–M12 remain reserve-first cuts. A mastery case that is only a campaign board with a smaller number is rejected.

No globally shortest solution is required for normal completion. Efficiency objectives must be authored explicit optional goals with solver witnesses.

## 6. Undo/restart/quit/load/replay/animation boundaries
Planning move -> Undo Move restores prior planning placement/move count only. Resolve -> canonical post-state is computed and checkpointed independent of animation. Skip animation snaps presentation to that state. Crash after checkpoint but mid-animation reloads post-state.

Undo Resolve restores exact pre-Resolve puzzle state and counters. **Repair P9-A:** persistence metadata is outside puzzle rewind: profile `save_generation` remains monotonic when an undo result is subsequently saved. Otherwise repeated undo could create older-looking generations and confuse cloud/import conflict handling.

Replay uses structured last trace/presentation and never invokes Resolve. Restart returns authored initial state and creates a new valid saved checkpoint generation when persisted. Quit during planning reloads the last safely committed planning/checkpoint state according to application policy; it never serializes half-animation state.

## 7. Demo -> full import simulation
Demo profile: LT01–LT06 completion, settings, tutorial acknowledgements, compatible checkpoint. Full absent -> import validates source, unions monotonic fields, writes atomically, records source fingerprint only after success.

Repeat import -> same completion result; no duplicated achievement intent or regression.

Older demo + newer full -> full completion/checkpoint wins; demo may union only safe missing monotonic flags. Never replace completed full case with demo in-progress state. Demo files remain untouched.

Corrupt demo -> full starts normally and reports import failure/retry; no invented partial progress.

## 8. Offline / Cloud / corruption simulation
Steam offline: local profile/checkpoints work; achievement intents queue idempotently.

Local and Cloud share common generation then diverge: preserve both validated candidates locally; show device/source, generation, modified time, completion count and latest case. Safe profile completion union may be offered through tested merge; in-progress checkpoint is selected whole, never field-merged.

Cloud corrupt + local valid: corrupt candidate cannot overwrite local. Latest local corrupt + known-good backup valid: load backup, preserve profile, report recovery. One case checkpoint corrupt: preserve campaign/profile completion and offer case restart.

## 9. Mouse/controller/Deck simulation
Mouse drag and click-place resolve to same placement command. Controller cycles clocks, enters placement, navigates deterministic socket-neighbor graph, confirms/cancels, inspects sites and Resolve without pointer emulation. Every critical label remains readable at 1280x800 with pattern/text redundancy.

No puzzle requires camera hunting. If a board cannot keep <=8 relevant landmarks legible at target display, content fails before shipping. High contrast/motion reduction/fast animation change presentation only.

## 10. Hostile player behavior
**Resolve spam:** every Resolve consumes finite authored budget and produces NO_CHANGE when appropriate; cannot accumulate duration. **Repair P9-B:** `resolve_limit` is mandatory for every campaign/mastery definition, even when generous, so the reachable graph and solver proof remain finite.

**Socket scanning:** preview exposes footprint/current predicates/risk facts but not future transition oracle. Anti-enumeration human proof remains a shipping gate.

**Broad-warning scanning:** warnings are factual, not 'bad move' labels; intentional hazardous exposure remains possible when objective allows it.

**Undo abuse:** acceptable; puzzle is reasoning, not execution punishment. Undo cannot earn achievements twice because achievement intents use stable idempotent IDs and completion is monotonic.

**Deliberate budget waste:** eventually produces exact budget failure with unmet clauses; never softlocks UI.

**Resolve during animation / double input:** transition lock prevents a second state-changing command; skip only changes presentation.

## 11. Carrier contradiction repair
Existing DISPATCH grammar could be read as re-enabling every Resolve while its current predicates remain true. **Repair P9-C:** every dispatch rule that starts a carrier has a public finite dispatch state/milestone (`READY -> DISPATCHED`, or equivalent). Once committed, that departure edge is consumed unless the authored carrier definition explicitly contains another distinct finite dispatch stage. A single DISPATCH rule cannot repeatedly launch/move the same carrier merely because its predicates remain true.

Carrier movement therefore remains finite and deterministic. At most one authored carrier step occurs per enabled departure/handoff stage per Resolve. Newly arrived cargo remains ineligible for default ACCEPT until a later Snapshot0.

This clarification uses existing persistent milestone/finite-state grammar; it adds no new family.

## 12. Current/persistent/hazard/coupled consistency
Current predicates never persist merely because they were once true. Persistent process/protection/dispatch/accept milestones never reverse because a label moves. Hazards evaluate from Snapshot0 and cannot be defeated by same-Resolve beneficial updates unless explicitly taught `same_resolve_prerequisite=true` (baseline campaign should avoid this flag).

Coupled current predicates are simultaneous Snapshot0 facts, never accumulated across Resolves. Carrier arrival changes persistent location after non-carrier commit; default acceptance sees it only next Resolve. Objectives are evaluated after the carrier step against recomputed current predicates plus committed persistent state.

## 13. Canonical Phase-9 repairs
P9-A — Undo restores puzzle state but persistence `save_generation` is monotonic outside undo.
P9-B — `resolve_limit` is required on every shipped case; 'optional' in early CaseState wording is superseded for authored shipping definitions.
P9-C — carrier-starting DISPATCH consumes a finite public dispatch state/edge; unchanged predicates cannot relaunch it indefinitely.

All later authority must include these repairs.

## 14. Phase acceptance
The paper simulation covers first boot, LT01–LT06, representative proof obligations for Cases 07–36, campaign/mastery boundary, undo/restart/replay/crash, demo import, offline/cloud/corruption, mouse/controller/Deck and hostile behavior. No production code was created.

The game survives Phase 9 with three bounded repairs and a clear repetition-risk list. The 30-case quality floor is credible; 36 remains conditional on Phase-10 proof-shape attack.

**PHASE 9 WHOLE-GAME SIMULATION = COMPLETE.**

# NEXT DESIGN STEP — PHASE 10 ADVERSARIAL REVIEW
Attack fun/repetition, brute-force/socket scanning, the 08/19, 14/18/29, 26/27/31 and 32/33/36 similarity clusters, Resolve-budget design, carrier finite-state exploits, same-Resolve prerequisite ambiguity, undo/save/cloud interactions, controller/readability, content/art scope, demo comprehension, commercial promise and implementation ambiguity. Cut cases/content before adding exceptions. Canonically propagate P9-A/P9-B/P9-C into any final authority. If the design survives, proceed to Phase 11 Specification Freeze; do not start production implementation.