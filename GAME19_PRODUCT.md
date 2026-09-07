# GAME #019 — PRODUCT THESIS LOCK

Date: 2026-09-07
Status: ACTIVE CANON — Phase 3
Design complete: NO
Working title: **TIDE TABLE**

## 1. Product thesis decision
**LOCK TIDE TABLE.** The concept survives Phase 3 only as a compact deterministic puzzle game about changing one shared water level and exploiting cargo-induced draft changes. It is not a harbor-management game, boat-navigation game, fluid simulation, logistics economy, or narrative campaign.

## 2. Target player
Primary: players who enjoy compact systemic deduction puzzles where a tiny public ruleset produces multi-step consequences and where success can be reasoned about before acting.

Secondary: Steam/handheld puzzle players attracted by a strong physical metaphor, short self-contained levels, quick restart, and visible cause/effect rather than story or dexterity.

Not targeted: players seeking free sailing, real-time management, transport tycoon economy, realistic maritime simulation, survival, or large narrative progression.

## 3. Platform and product shape
- PC / Steam first.
- Single-player premium game.
- Mouse and full controller parity from the start; Steam Deck readability is a design constraint.
- Discrete deterministic simulation; no timing/reflex requirement.
- Level-based structure rather than campaign-world traversal.
- Target play session: one or several 3–12 minute puzzles; harder mastery cases may run longer.
- Demo target: 20–40 minutes and must reach the true draft-coupling idea, not merely basic tide alignment.

## 4. Genre framing
A **deterministic systemic harbor puzzle game**.

Store-facing shorthand: **“Set the tide, move the cargo, change what can line up next.”**

The harbor is a legible machine. Water level is the shared control variable; cargo is both objective and state-changing mass.

## 5. One-sentence hook
**Choose one tide for the whole harbor, then transfer cargo when interfaces align — but every load changes a boat’s draft and therefore changes which alignments will exist at the next tide.**

Short trailer/GIF hook: move tide one notch -> every hull rises/falls together -> transfer a heavy crate -> that hull visibly settles one draft unit -> a previously impossible later rendezvous becomes possible.

## 6. Core fantasy
The player feels like a clever harbor planner solving a miniature mechanical system by understanding waterline, load and clearance. The pleasure is not piloting boats; it is seeing a whole harbor reconfigure coherently from one global choice and deliberately using cargo weight to reshape future opportunities.

## 7. Exact player verbs
Canonical base verbs:
1. **Inspect** — read public tide levels, current hull draft/interface heights, cargo mass units, destinations, capacities, tether bands and clearances.
2. **Set Tide** — choose the next legal discrete global water level. Every floating object's authoritative vertical state updates from the same tide.
3. **Transfer Cargo** — move a cargo unit across a currently legal interface: dock↔boat or boat↔boat. Transfer immediately updates source/destination load and therefore their draft/interface heights.
4. **Undo / Reset** — deterministic puzzle recovery; exact UX/persistence contract belongs to Phase 6/8.

No direct steering, throttle, rope manipulation, crane dexterity, free object dragging through space, waiting for a real-time tide, or continuous ballast sliders.

## 8. Central discrete draft rule — Phase-4 authority
All gameplay heights use small integer **height units (HU)**. No continuous buoyancy value is authoritative.

For each boat `b`:
- `tide` = current global integer tide level.
- `base_offset_b` = boat-specific unloaded interface offset, an integer shown/derivable from the boat's public height strip.
- Cargo has public integer **draft weight**; base campaign cargo should normally use weight 1, with heavier values allowed only if Phase 4 proves readability.
- `load_b` = sum of draft weights currently aboard.
- `draft_step_b` = normally 1 HU per load unit. Any exception must be explicit level data and visually public; Phase 4 should prefer no exceptions.
- Canonical interface height: `interface_height_b = tide + base_offset_b - load_b * draft_step_b`.

Thus loading one ordinary heavy cargo unit makes the boat's transfer interface sit exactly **1 HU lower relative to the world** at every later tide until that cargo leaves; unloading reverses that contribution. Tide affects all floating boats globally; load affects only the boats whose cargo changes.

A fixed dock interface has a world-space integer height. A boat/dock transfer is height-eligible when their active transfer interfaces are equal. A boat/boat transfer is height-eligible when their active interfaces are equal. Phase 4 may add capacity, tether and clearance predicates, but equality of public integer interface height remains the core alignment test.

### Important sequencing consequence
A transfer can change the receiving and sending boat heights immediately at the current tide. Therefore Phase 4 must define transfer atomicity and whether multiple transfers at one tide can chain after each recomputation. Default thesis: **yes, state recomputes after every transfer and another transfer may occur at the same tide if it is legal in the new state**. This creates reasoning depth without inventing a second time system.

## 9. Core loop
1. Read delivery goals and the compact public harbor state.
2. Predict which interfaces will align at candidate tide levels.
3. Set one global tide.
4. Observe deterministic global vertical motion and legal-interface feedback.
5. Choose a legal cargo transfer, if useful.
6. Boat load changes; affected draft/interface heights recompute immediately.
7. Re-evaluate the same tide or choose another tide.
8. Finish when all required cargo/delivery predicates are satisfied; optional mastery may reward fewer tide changes or another explicit public budget.

The game must reward prediction. Free experimentation is acceptable because undo/reset is humane, but UI must not become an oracle that automatically enumerates future tide sequences.

## 10. Level/session structure
- Self-contained authored deterministic puzzle cases selected from a compact level map/list.
- Each level begins in a fully specified harbor state and ends on explicit delivery predicates.
- Early levels isolate one causal idea; later levels recombine the same vocabulary.
- No overworld traversal is required.
- Progression unlocks harder compositions, not player stats or economic upgrades.
- Optional mastery challenges can revisit solved levels with a tide-change budget or stricter target, but base completion must remain reasoning-first rather than optimization-only.

Provisional content shape for later validation: compact premium scale, not a 1,000-level arms race. Phase 5 must derive minimum/target counts from genuinely distinct proof families rather than promise volume now.

## 11. First-session promise
Within roughly the first 5 minutes, the player understands that one tide moves every boat and can make a dock transfer possible.

Within roughly 10–15 minutes, the player must personally cause or observe **load-changes-draft**: transfer cargo, see the receiving boat settle exactly one public unit, and use that changed geometry in a later decision.

Within the demo, the player must solve at least one **boat-to-boat relay** where changing one boat's load alters a later rendezvous tide. If the demo cannot communicate this without dense explanation, the product thesis has failed and should be revisited rather than padded with simpler levels.

## 12. Differentiator
The differentiator is the conjunction, not any single familiar element:
- one global discrete environmental control;
- several floating objects respond coherently;
- the objective objects themselves alter local response through draft;
- transfers therefore edit the future alignment graph;
- all authority remains tiny, public, integer and deterministic.

The mental model is: **cargo is not just something to route; it changes the geometry of routing.**

## 13. Anti-scheduling invariants
These are mandatory. If Phase 4 violates them, TIDE TABLE should be repaired or killed rather than becoming a timetable puzzle.

1. **Draft coupling appears early and is mandatory.** A meaningful share of core levels cannot be solved by treating boat heights as fixed tables.
2. **Transfers change future opportunity structure.** Later puzzles must require choosing not merely when to transfer, but which boat should carry which load because that changes later alignment.
3. **At least two boats matter in developed play.** Dock-only pickup/drop scheduling is tutorial material, not the long-tail game.
4. **Same-tide recomputation matters.** Some puzzles should exploit a transfer changing another legal relation without spending another tide change.
5. **Small tide alphabet, rich state.** Do not create depth by adding dozens of tide values or long blind sequences. Prefer roughly 3–7 meaningful tide levels per puzzle, subject to Phase-4 validation.
6. **No hidden mass arithmetic.** Cargo draft weight, capacity and resulting boat height must be inspectable before commitment.
7. **No wait mechanic.** Tide changes are player-selected discrete state transitions, not elapsed time.
8. **No sequence-programming UI.** Player chooses the next tide in the current state; they do not write a script and press Run.
9. **No oracle preview.** UI may show current consequences of a selected/current state, but must not auto-solve or expose complete future reachable-state trees.
10. **Constraints share the height model.** Tethers and bridge/overhead clearance constrain current height/range; they do not introduce unrelated minigame resources.

## 14. Scope ceiling
Allowed systemic vocabulary for the full game, pending Phase-4 proof:
- global discrete tide;
- boats with public unloaded offset/draft response and capacity;
- cargo with destination and small integer draft weight;
- fixed dock interfaces;
- boat↔dock and boat↔boat transfers;
- finite tether operating bands;
- simple fixed overhead/bridge clearance predicates;
- limited tide-change budget as challenge/mastery pressure;
- fixed blockers/one-way transfer interfaces only if they can be expressed cleanly inside the same state model and survive adversarial review.

Prefer depth from recombination of these systems. Adding a new subsystem requires proving that existing rules cannot create the needed decision family.

## 15. Explicit non-goals
Do NOT add:
- harbor ownership/management;
- money, trading, contracts, fuel or economy;
- free boat navigation/pathfinding;
- real-time tides, clocks, weather or day/night;
- realistic fluid, rope or rigid-body physics as gameplay authority;
- waves, currents, wind, hull damage or docking dexterity;
- crew simulation;
- crane-control minigames;
- narrative campaign, dialogue trees or large writing burden;
- procedural world generation;
- multiplayer/co-op;
- roguelite/deckbuilding/metaprogression wrapper;
- movable semantic time/region zones, milestones or Local-Time-style logic;
- giant cargo taxonomy whose purpose is content inflation.

## 16. Presentation identity boundary
Presentation should make the integer model feel physical without pretending to be a simulator: compact side/oblique harbor diorama, strong horizontal height bands, visible waterline movement, boats settling/rising after load changes, clear dock lips/transfer points, and readable tether/clearance states.

Animations interpolate between authoritative discrete states. They never decide outcomes.

## 17. Product failure conditions to carry forward
Kill or substantially redesign if later architecture shows any of these:
- interesting levels reduce to looking up a fixed tide schedule;
- cargo mass is mostly cosmetic or only an occasional gimmick;
- boat-to-boat relay cannot stay readable with 3+ relevant hulls;
- optimal play requires arithmetic tables rather than spatial reasoning;
- tether/clearance rules dominate the draft interaction;
- difficulty requires very long tide sequences or large state counts;
- solver-generated levels are technically valid but human reasoning paths are opaque;
- small-screen/controller presentation cannot show current height/load/goal state without inspection overload.

## 18. Phase-3 lock
Product identity is now frozen enough for mechanical architecture:
- PC/Steam-first compact premium deterministic puzzle;
- one global discrete tide;
- tide choice + legal cargo transfer are the only strategic base verbs;
- cargo load changes boat interface height through public integer draft units;
- transfer recomputes state immediately and may enable another same-tide transfer;
- depth must come from state-dependent future alignment, not scheduling length;
- no production implementation begins in the factory.

## NEXT PHASE
**Phase 4 — Mechanical Architecture.** Specify authoritative state, transition ordering, legal-transfer predicates, cargo/capacity model, tether/clearance semantics, tide-change legality/budgets, goals, fail/deadlock handling, undo/reset behavior at design level, difficulty variables, representative puzzle proofs, solver/validator state representation and anti-dominant-strategy gates. Do not expand the product scope while doing so.
