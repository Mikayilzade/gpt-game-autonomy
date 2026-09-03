# GAME #017 — PHASE 2 CONCEPT TOURNAMENT / ROUND B

Date: 2026-09-03
Status: ROUND B COMPLETE — THREE FINALISTS, NO WINNER SELECTED
Authority: below `START_HERE.md`, `STATUS.md`, `GAME_INDEX.md`, `GAME17_RESEARCH.md`, `GAME17_TOURNAMENT.md`.

## Method
Round B re-tested the seven Round-A survivors at product scale. No Round-A score carried forward. Every candidate received: a concrete 20–30 minute demo arc; at least three structurally distinct later reasoning families; hour-5 novelty test; UI/state and production/QA ceiling; controller/Deck test; current-market and portfolio collision probe; minimum falsification prototype; strongest likely player complaint; and the same 10×0–5 destructive rubric.

Scores are ordered: hook / learnability / systemic depth / sustained novelty / fair causality / production proportionality / controller readability / demo conversion / distinctness / commercial legibility.

Fresh-market evidence is used only where current positioning matters. Sources sampled on 2026-09-03 include:
- Steam `Switchboard`, released 2026-04-16: https://store.steampowered.com/app/3931650/Switchboard/
- `Hello Operator`, a 2026 narrative switchboard game: https://www.maingamers.com/games/hello-operator
- Steam `Auction King`, planned Q4 2026: https://store.steampowered.com/app/4894520/Auction_King/
- Steam `Auction Simulator`: https://store.steampowered.com/app/5095790/Auction_Simulator/
- `BidKing`, released 2026-04-16, and `Double Dealers`, released 2026: https://steambase.io/games/bidking/info and https://steambase.io/games/double-dealers/info
- Steam `Dupery: A Game of Solo Deduction`, current solo-deduction competitor emphasizing 200+ handcrafted roles and procedural cases: https://store.steampowered.com/app/3845070/Dupery_A_Game_of_Solo_Deduction/

---

# C01 — NIGHT SHIFT SWITCHBOARD
## 20–30 minute demo arc
**0–4 min — physical promise.** A four-operator board, three calls, and one visible rule per operator. Player plugs Caller A directly to Payroll and gets a clean refusal reason: identity not confirmed. A second call to Security visibly creates a verification token. The board changes rather than merely displaying a score.

**4–9 min — first mastery.** Player realizes one call can prepare state for another. The first satisfying chain is `badge call -> Security -> verification shared -> payroll caller -> Reception -> Payroll`. A short replay overlay shows exactly which conversation created which authorization.

**9–15 min — first failure.** A player burns the only internal consultation on an easy delivery call, then discovers a later alias-equivalence route now cannot be completed. Failure is not instant; the board reaches a certified no-route state and explains the consumed bridge.

**15–22 min — richer case.** Two callers share a project alias, one operator can learn equivalence, another can authorize transfer only after hearing it from an internal source. Player intentionally routes a call through a seemingly unnecessary operator to seed that knowledge.

**22–28 min — trailer beat.** Four lines light in succession as an early caller triggers a fact exchange that unlocks three later transfers; the player sees a dense-looking switchboard collapse into a clean prepared route.

Tutorial burden is moderate and mostly diegetic, but the concept requires the player to read operator state cards carefully.

## Mid/late reasoning families
1. **Provenance routing.** Facts are not binary flags: some permissions require a fact learned from a caller, others from an operator, others from a named department. Novelty comes from source-sensitive bridges.
2. **Consumable communication windows.** Operators have one consultation / one escalation / one transfer favor. The player decides which caller should spend the bridge and which later route depends on it.
3. **State contamination / incompatibility.** Discussing one topic temporarily blocks or supersedes another authorization. A productive route may deliberately avoid teaching an operator too much too early.
4. **Multi-call synchronization.** A call can be held while another call creates prerequisite state; order and hold capacity interact without becoming real-time dexterity.

These are genuine interaction families rather than extra operator types. Hour-5 depth is plausible.

## UI / production / controller ceiling
Truthful screen needs 4–7 operators, 3–6 active calls, operator knowledge/permission chips, transfer affordances, call hold state, and provenance explanations. This is dense but controller-feasible via focus lanes and radial transfer selection. Production can remain 2D/stylized, but selling the switchboard fantasy strongly invites voice, character art, ringing/line animation, and period dressing.

QA burden is medium-high because every case needs reachable-state validation, dead-route certification, explanation correctness and no accidental hidden state.

## Collision probe
Mechanically it does not collide with Games #001–#016. Commercially, however, the surface is now badly occupied: `Switchboard` released on Steam on 2026-04-16 with a tactile historical telephone-exchange fantasy, and `Hello Operator` also occupies a narrative switchboard-routing mystery surface in 2026. Our state-preparation puzzle is deeper, but screenshots/trailer thumbnails must first overcome near-literal job/furniture overlap. This is not a theoretical future risk; it is current 2026 positioning.

## Minimum falsification prototype
One flat 2D board, four operators, five calls, exactly two knowledge mutations, one consumable consultation and one dead-state detector. No voice, no story. If five fresh players cannot explain why call #5 became routable after call #2 without opening a symbolic ledger, kill.

## Strongest likely complaint
> “This looks like another switchboard game, except I spend more time reading little permission tags.”

## Round-B score
4 / 4 / 5 / 5 / 5 / 3 / 4 / 4 / 2 / 2 = **38/50**

**Decision: KILL.** The mechanic survives, but 2026 market collision destroys the clean product identity and raises presentation cost. Do not rescue by reskinning: the routing metaphor is carrying too much of the readability.

---

# C04 — THE QUIET AUCTION
## 20–30 minute demo arc
**0–5 min — obvious auction.** Three lots, two deterministic rivals, public budget. The player only needs Lot C. First round teaches that rivals have bounded policy cards, not human-like hidden AI.

**5–10 min — deliberate loss.** The player sees Iris overvalue botanical sets and Pavel become aggressive after losing. A cheap bid on a decoy changes who owns the prerequisite item and therefore suppresses a later rival bid.

**10–16 min — first failure.** Player wins too many attractive lots, arrives at the target underfunded, and sees an exact post-auction counterfactual showing which earlier victory increased the final clearing price or depleted cash.

**16–23 min — bundle twist.** Two lots are substitutes for one rival but complements for another. The player uses a small bundle bid not to win both but to alter which rival contests the target.

**23–28 min — trailer beat.** Player intentionally bids up a worthless-looking object, lets a rival overpay, then takes the desired final lot for one unit above reserve. The causality can be shown in a six-second before/after budget strip.

## Mid/late reasoning families
1. **Budget exhaustion manipulation.** Player shapes rivals' future feasible actions by making them spend now.
2. **Complement/substitute topology.** Ownership of one lot changes deterministic valuation of another; the player can break or create sets.
3. **Tie-break / clearing-price engineering.** Player may want to be second-highest, not first, to set a rival's cost or preserve initiative.
4. **Information-value lots.** Some cheap lots reveal which bounded rival policy is active; bidding is simultaneously experiment and economic action.

Hour-5 novelty is structurally plausible, but arithmetic density rises quickly.

## UI / production / controller ceiling
Low asset burden: lots can be iconographic cards/objects, 2–4 rivals, budget strips, bid dial, history. Controller is excellent. Core simulation is deterministic and compact. QA burden is medium because bid interactions, bundles and tie-breaks require exhaustive testable resolution.

## Collision probe
No portfolio collision. Current commercial collision is meaningful: 2026 has `Auction King`, `Auction Simulator`, `BidKing`, and `Double Dealers`, all selling some combination of incomplete information, rival reading, valuation, bluffing or manipulation. Our deterministic bounded-policy puzzle is cleaner and single-player, but screenshots still read as “auction strategy.” A differentiator would have to be communicated in text or tutorial rather than instantly in the prop itself.

## Minimum falsification prototype
Twelve lots across three short auctions, three rival-policy families, exact revealed bids after resolution. Test whether players voluntarily describe their success as “I manipulated the bidders” rather than “I solved the numbers.” If the latter dominates, kill.

## Strongest likely complaint
> “It is clever, but it feels like doing auction math against bots.”

## Round-B score
4 / 4 / 5 / 5 / 5 / 5 / 5 / 4 / 3 / 3 = **43/50**

**Decision: KILL, narrowly.** Strong system, excellent scope, but the current auction surface is crowded enough that the product hook is weaker than the three finalists. Keep only as rejected history, not canon.

---

# C05 — ARCHIVE OF ALMOSTS
## 20–30 minute demo arc
**0–4 min — concrete objects first.** Four tabletop prototype heaters have visible switches, lids and indicators. Three anonymous failure reports sit beside them. The player is told only that each report came from one prototype.

**4–8 min — first diagnostic test.** Player chooses one prototype and a bounded test setup (`lid open`, `already hot`, `short run`). The machine produces a tiny deterministic trace. Candidate cards visibly split: two fault models die immediately.

**8–13 min — mastery beat.** The player discovers that a good test is not “try the most likely answer” but “choose conditions whose possible outcomes divide the remaining hypotheses.” The UI previews no answer, only which measurable dimensions will be observed.

**13–17 min — first failure.** Spending both allowed retests on redundant conditions leaves two prototypes observationally equivalent. The game can prove that the test budget was wasted and permit instant case reset.

**17–23 min — masking case.** Two faults coexist but one normally triggers first. Player deliberately suppresses overheating so a power-cycle fault becomes observable. This creates a strong physical reveal: nothing happens under the obvious test, but the diagnostic setup exposes the hidden second failure.

**23–28 min — trailer beat.** One deliberately weird setup sends four predicted behavior traces in four different directions; the actual prototype follows exactly one. Candidate stack collapses from six to one in a single satisfying test.

## Mid/late reasoning families
1. **Partition design.** Pick an experiment that maximizes discriminating power across remaining models; the puzzle is active information acquisition, not passive clue matching.
2. **Fault masking / intervention.** Disable or avoid one mechanism so another latent mechanism can manifest. This changes causal structure rather than adding candidates.
3. **Temporal-order faults.** Two models produce the same final state but different intermediate trace; player must choose when to observe, not merely what condition to set.
4. **Shared-resource coupling.** Two prototypes interact through one bounded test rig (power rail, coolant line, trigger bus). Testing one can perturb evidence in another, creating experimental controls and confounds.
5. **Negative-control design.** Some reports can only be matched by proving a condition has no effect under one model.

Hour-5 novelty can come from intervention grammar, observation timing and coupling while keeping a small device vocabulary.

## UI / production / controller ceiling
Truthful screen can be tactile and sparse: one test bench, 3–6 prototype objects, condition toggles, 2–4 measurable channels, candidate hypothesis cards, and a time trace. No large world or character simulation. Controller/Deck works through snapped test sockets and toggle focus. Asset reuse is excellent if prototypes are modular shells plus indicators.

Implementation ceiling is low-medium: deterministic finite-state devices, trace recorder, candidate simulator, case validator and optional automated proof that each authored case is solvable within test budget. QA is substantial but computationally bounded and directly automatable.

## Collision probe
No Games #001–#016 identity collision. It is deduction, but unlike `Dupery` and familiar detective/social-deduction products, the player designs interventions on physical systems rather than interrogating roles or consuming authored clues. The commercial risk is dryness, not direct mechanic saturation.

## Minimum falsification prototype
Six fault models over one four-control device; five cases; two tests per case; automatic solver computes optimal partitions. Use flat shapes and graphs only. Kill if players spend most time enumerating candidate rows manually or if the optimal test is repeatedly obvious from one highlighted difference.

## Strongest likely complaint
> “I understand the logic, but I feel like I am doing a lab worksheet.”

## Round-B score
4 / 5 / 5 / 5 / 5 / 5 / 4 / 4 / 5 / 4 = **46/50**

**Decision: PASS TO ROUND C.** Strongest production-to-depth ratio in the field. Round C must prove that physical presentation can create emotional/tactile satisfaction without bloating bespoke device content.

---

# C07 — COMMON KNOWLEDGE
## 20–30 minute demo arc
**0–5 min — first-order knowledge.** Two characters, one deadline, private notes. Player tells both separately; both know the fact, but neither commits. A visual “who saw this” ribbon explains why.

**5–10 min — public observability.** Player posts one public notice. Both see it, but the puzzle introduces a participant who cannot see whether the other has seen it. The first apparent contradiction exposes the difference between shared information and common knowledge.

**10–16 min — first failure.** The player uses private acknowledgements and reaches a state where every person knows the deadline but a commitment predicate still fails. A capped second-order ledger explains the missing reciprocal observation.

**16–23 min — mastery.** A public acknowledgement, not another fact, closes the loop. The player starts thinking about observable receipt rather than message content.

**23–28 min — trailer beat.** One character silently raises a visible placard; three commitment icons flip simultaneously because everyone can see everyone else see the acknowledgement.

## Mid/late reasoning families
1. **Channel observability.** Different media reveal message content, receipt, or both.
2. **Witnessing acknowledgements.** The action that proves someone knows can itself be public/private and create higher-order consequences.
3. **Asymmetric senses / partitions.** Some agents can see but not hear, or hear through walls but cannot identify the speaker; common knowledge is constructed via shared observable events.
4. **Commitment thresholds.** Different actions require first-order mutual knowledge versus capped common-knowledge predicates.

The families are genuinely distinct, but all depend on teaching one abstract epistemic distinction extremely well.

## UI / production / controller ceiling
The spatial scene can be small and controller-friendly. The real cost is explanatory UI: every failure must say who knows what and who knows that another knows it, without symbolic notation. Capping at second order helps, but the game remains conceptually dense. Localization burden is manageable because facts can be icons, yet tutorial and wording must be exact.

## Collision probe
No portfolio collision and no obvious direct Steam clone found in this run. Distinctness is excellent. The risk is category legibility: “epistemic logic puzzle” is not a market category and screenshots do not reveal the hook without explanation.

## Minimum falsification prototype
Three agents, three channels, six microcases, no algebraic notation anywhere. If a new player cannot predict the final commitment after case #3 and explain the failed state in ordinary language, kill immediately.

## Strongest likely complaint
> “The game keeps telling me everybody knows it, then says that still is not enough.”

## Round-B score
3 / 2 / 5 / 5 / 4 / 4 / 4 / 3 / 5 / 2 = **37/50**

**Decision: KILL.** Brilliant formal material but severe teachability and trailer-legibility risk. The interface would be forced to explain the concept more than the player manipulates it.

---

# C10 — THE QUEUE KNOWS
## 20–30 minute demo arc
**0–4 min — readable crowd.** Six customers enter a tiny service hall. Three candidate customer types are public. Player can mark Counter A “Free” or open Counter B one minute late. Customers choose deterministically.

**4–8 min — inference from behavior.** Three customers self-sort. Clicking any customer shows a short trace: “A is Free -> price-sensitive chooses A.” The player tags two likely types.

**8–13 min — first experiment.** Two customer types currently behave identically. Player changes signage, creating a condition under which only one type switches. The queue is not merely an obstacle; it becomes the measurement instrument.

**13–17 min — first failure.** The experiment is too aggressive: everyone piles into A, congestion makes an urgent customer switch too, destroying the clean signal. Exact choice traces show that the intervention changed the state being measured.

**17–23 min — mastery.** Player uses a two-stage intervention: first a neutral capacity change, then a sign after the early cohort commits. This separates latent types while preserving service target.

**23–28 min — trailer beat.** One sign flips; a seemingly chaotic six-person queue reorganizes into three visibly meaningful groups, and the UI reveals the hidden type candidates collapsing in real time.

## Mid/late reasoning families
1. **Diagnostic mechanism design.** Configure visible incentives so latent types choose different actions.
2. **Endogenous congestion / confounding.** The measurement intervention changes queue lengths, which changes later choices; player must design experiments robust to self-created state.
3. **Sequential cohorts.** Early customers reveal information that changes the optimal intervention for later arrivals; observation and control alternate.
4. **Pooling vs separating equilibria.** Sometimes the goal is not identify everyone individually but create a configuration where only the operationally relevant type separates.
5. **Counterfactual service constraints.** The best diagnostic setup may delay service; player must satisfy a bounded service target while preserving information value.

These produce hour-5 novelty from interactions among the same public heuristics, not from dozens of new customer types.

## UI / production / controller ceiling
One room, 2–4 counters, 5–10 customers, simple signs, visible queues and per-customer reason traces. Characters can be abstract/stylized tokens with strong silhouettes; no dialogue needed. Controller focus can snap between counters/signs/customers. Deck readability is viable if crowds cap at ~10 and reason traces use one-line icon chains.

Implementation is medium: deterministic choice evaluator, queue timing, intervention actions, exact trace generation, candidate-type inference helper and authored/procedural validator. Avoid pathfinding simulation; customers move on fixed lanes/slots so the puzzle remains state-based, not agent-navigation QA.

## Collision probe
No portfolio collision if service optimization remains secondary and there is no luggage-label/permutation identity. Generic shop/queue management is common, but current queue products mostly treat lines as throughput problems. The hook here is **use the queue as a diagnostic instrument**, which survives without management economy, upgrades, timers or real-time stress.

## Minimum falsification prototype
Two counters, three type heuristics, eight customers, five cases, fixed queue slots. No animations beyond token movement. Kill if players optimize throughput without noticing the inference layer, or if the UI must reveal customer types too strongly to make failures fair.

## Strongest likely complaint
> “Why am I making the queue worse on purpose? I thought I was supposed to serve people faster.”

## Round-B score
5 / 5 / 5 / 5 / 5 / 4 / 5 / 5 / 5 / 4 = **48/50**

**Decision: PASS TO ROUND C.** Best immediate visible cause/effect and strongest demo transformation. Round C must prove it does not drift into queue-management optimization and that hidden types remain fair rather than guessy.

---

# C11 — HOUSE RULES
## 20–30 minute demo arc
**0–5 min — one tiny base game.** Four guests play a fictional 12-card matching game. Canon rules fit on one screen. Each guest has exactly one misconception chosen from a visible hypothesis set. Player acts as host and chooses legal demonstration moves.

**5–9 min — social evidence.** A same-number/different-suit play triggers objections from two guests but not the others. The player marks candidate misconceptions. Reactions are deterministic speech bubbles/icons, not natural-language AI.

**9–14 min — first diagnostic turn.** Player deliberately chooses a suboptimal but legal move because it separates two remaining hypotheses. This is the core pleasure: play the board game as an experiment on the people playing it.

**14–18 min — first failure.** Player corrects one guest too early, erasing evidence before distinguishing which misconception they held. The final diagnosis becomes underdetermined; the game proves the ambiguity.

**18–24 min — learning dynamics.** One public ruling updates flexible guests but not a stubborn guest. The player must test before teaching, then use the corrected guest's later reaction as evidence about another player.

**24–28 min — trailer beat.** Host makes one odd-looking card play; three guests react differently at once, their hypothesis chips collapse, and the player identifies all four misconceptions before the final hand.

## Mid/late reasoning families
1. **Diagnostic move design.** Choose legal plays whose accept/object pattern partitions guest-rule models.
2. **Evidence destruction by teaching.** Correcting a misconception changes the system, so information gathering must precede intervention.
3. **Public-ruling propagation.** Guests have bounded update traits; one ruling can alter multiple future observers and create second-order experiments.
4. **Rule interaction cases.** Two canon rules become relevant in one move, letting different misconceptions predict the same immediate objection for different reasons; later test disambiguates cause.
5. **Selective demonstration.** Player can expose only one board feature at a time to isolate whether a guest misremembers legality, turn ending, draw timing or scoring.

Hour-5 novelty is plausible with one immutable base game plus ~8–12 misconception modules and a small set of learning traits. Do not add multiple invented games.

## UI / production / controller ceiling
A tabletop with 12–20 cards, four guest portraits, compact reaction icons and per-guest hypothesis chips. Excellent controller fit via snapped card selection. Art burden is modest and character reactions add warmth without systemic animation. Localization is moderate but bounded; misconception text must be precise and all reactions can be icon-backed.

Implementation is medium-low: base-game rules engine, guest belief-model rules engine, diagnostic reaction comparison, learning updates, case validator and underdetermination proof. It can be exhaustively tested because state/action space is tiny.

## Collision probe
No direct Games #001–#016 collision. It sits near solo deduction, but unlike current role-heavy products such as `Dupery`, the unknown is each player's **incorrect model of a public rule system**, and the player's evidence comes from deliberately chosen valid game actions rather than interrogation clues. The one-table social presentation is commercially legible if trailer copy says “figure out which rule each friend remembers wrong.”

## Minimum falsification prototype
One 12-card game, four misconception hypotheses, three NPC guests, six cases, no character art. Kill if players spend more cognitive effort relearning the fictional base game than diagnosing the guests, or if optimal tests are always the same move pattern.

## Strongest likely complaint
> “I have to learn a fake card game before I can solve the actual puzzle.”

## Round-B score
5 / 4 / 5 / 5 / 5 / 5 / 5 / 5 / 5 / 5 = **49/50**

**Decision: PASS TO ROUND C.** Strongest human-readable fantasy in the final field. Round C must attack tutorial tax and prove one base game supports enough distinct diagnostic families without content bloat.

---

# C13 — MINUTE HAND
## 20–30 minute demo arc
**0–5 min — visual fault.** Three clocks start together. Public candidate faults: fixed offset, periodic stall, periodic double-step. Player advances a reference interval and watches hand traces.

**5–10 min — experiment choice.** A +3 minute observation leaves two models equivalent; a subsequent +1 separates them. Player learns that interval choice matters.

**10–15 min — first failure.** Player spends the limited observation windows on periods where candidate traces coincide. End state is underdetermined and the solver demonstrates an unused discriminating interval.

**15–22 min — coupling.** Two clocks share a circuit; one chime resets another's stall counter. Player must decide whether apparent drift is independent or event-coupled.

**22–27 min — trailer beat.** Four clocks advance; one chime occurs, another unexpectedly snaps into phase, and three hypothesis cards vanish at once.

## Mid/late reasoning families
1. **Interval selection / aliasing.** Different observation lengths hide or reveal periodic faults.
2. **Event-triggered coupling.** Fault state resets or advances when another mechanism emits a visible event.
3. **Observation scheduling.** The player has limited windows and chooses not just duration but when to inspect intermediate state.
4. **Reference uncertainty.** A trusted reference is itself drawn from a bounded candidate set, requiring relational rather than absolute reconstruction.

These are real families, but all remain variations on finite model discrimination over periodic processes.

## UI / production / controller ceiling
Excellent: 3–6 large clocks, timeline, interval buttons and hypothesis chips. Very low assets, trivial controller support, strong deterministic testing. However, explaining periodic state without turning the game into tables/timelines becomes harder later.

## Collision probe
No portfolio collision and little direct current-market collision found. The bigger problem is internal: the core can be solved as arithmetic/hypothesis partitioning, and adding richer physical clockwork risks scope rather than deepening the same elegant loop.

## Minimum falsification prototype
Six fault families, ten generated cases, optimal-test solver. Kill if optimal strategy converges to “always choose the interval with maximum candidate split” without meaningful causal interpretation.

## Strongest likely complaint
> “Once I learned the fault patterns, I was just doing modular arithmetic.”

## Round-B score
4 / 5 / 4 / 3 / 5 / 5 / 5 / 4 / 5 / 3 = **43/50**

**Decision: KILL.** Beautiful scope and fairness, but weaker sustained novelty than the finalists; later complexity trends toward algebra rather than new interaction.

---

# ROUND-B SCOREBOARD

| Candidate | Score | Round-B decision | Primary reason |
|---|---:|---|---|
| **House Rules** | **49** | **ROUND C** | human-readable diagnostic play; excellent scope and distinctness |
| **The Queue Knows** | **48** | **ROUND C** | strongest visible intervention→behavior→inference loop and demo beat |
| **Archive of Almosts** | **46** | **ROUND C** | best production/depth ratio; active experimental deduction |
| The Quiet Auction | 43 | KILL | strong system, but crowded 2026 auction positioning and arithmetic surface |
| Minute Hand | 43 | KILL | elegant but long-run novelty trends toward periodic arithmetic |
| Night Shift Switchboard | 38 | KILL | 2026 near-literal market collision despite good mechanics |
| Common Knowledge | 37 | KILL | teachability/explanation burden overwhelms manipulation |

## Exact Round-C finalists
1. **C11 HOUSE RULES**
2. **C10 THE QUEUE KNOWS**
3. **C05 ARCHIVE OF ALMOSTS**

No winner is selected in Round B.

---

# ROUND C — REQUIRED FINAL TOURNAMENT
Round C should be a winner-selection pass, not another broad ideation pass. Use only the three finalists above; killed concepts remain exclusion history.

For each finalist:
1. write the exact one-sentence store hook and 15-second trailer sequence;
2. define a six-case vertical slice, with each case proving a distinct piece of the long-run depth claim;
3. perform a **tutorial tax test**: what must be understood before the first satisfying decision, and can it fit in <5 minutes without text walls;
4. perform a **content exhaustion test** at hours 1 / 3 / 5 / 8, explicitly naming what changes and what must NOT be added;
5. derive a rough full-product content target and the minimum demo subset;
6. perform deterministic solvability / explanation / dead-state requirements;
7. run an implementation pre-mortem: top five likely causes of production slippage and the scope cut that answers each;
8. run a player-comprehension pre-mortem using the strongest complaint from Round B;
9. compare screenshot/GIF legibility, Steam capsule/title positioning, controller/Deck experience, localization burden and likely MSRP/value perception;
10. score all three from zero again and **select exactly one winner**, unless a mandatory kill destroys all three.

After selecting the winner, Phase 3 must immediately lock the product thesis if the decision is stable: target player, platform, genre frame, one-sentence hook, core fantasy, session structure, core loop, differentiator, demo promise and scope ceiling. Do not carry runner-up mechanics into the winner unless independently justified by the winner's own design.
