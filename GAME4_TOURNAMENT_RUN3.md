# GAME #004 — CONCEPT TOURNAMENT — RUN 3 FINAL SELECTION

Last updated: 2026-08-21
Factory run: **6**
Phase: **2 — Concept Tournament / FINAL SELECTION**
Concept selected at start: **NO**
Concept selected at end: **YES — G4C19 acoustic-infiltration concept (working title `Soundproof Smuggler`; final title/fantasy wording NOT frozen)**

This pass resumes exactly from the final three in `GAME4_TOURNAMENT_RUN2.md`: **G4C19 Soundproof Smuggler**, **G4C01 Seam Thief**, and **G4C43 Command Wake**. It applies the same final-product tests to all three, attempts to kill each, and selects a winner only if the evidence becomes materially asymmetric.

No production implementation begins here. Product Thesis remains a Phase-3 task.

---

# 1. Fresh nearest-neighbor pressure — 2026-08-21

Fresh targeted searches were used only to update pressure around the final verbs.

## Sound / acoustic stealth
Relevant current/durable references:
- `Stifled` — https://store.steampowered.com/app/514830/Stifled/ — sound-based stealth where sound reveals the world and enemies hear the player.
- Steam Audio — https://partner.steamgames.com/doc/features/steam_audio — documents occlusion, transmission and multi-path propagation around doors/corridors.
- `Soundproof Walls 2.0` for Barotrauma — https://steamcommunity.com/sharedfiles/filedetails/?id=3153737715 — demonstrates sophisticated obstruction/path-based sound as an immersion system.
- Sound Sense PRO — https://www.fab.com/listings/e925988a-4067-4998-94ac-2c518411f47a — demonstrates visualized propagation paths, openings and hearing thresholds as available simulation vocabulary.

These references **increase**, rather than remove, the originality burden. Sound propagation and visualization are not novel on their own. G4C19 survives only because the player physically moves one world-space acoustic blocker to change *who hears what*, and deliberate audibility is as important as silence.

## Spatial topology / portals
Relevant pressure:
- `Portal Together` (2026) — https://store.steampowered.com/app/4204600/Portal_Together/ — current evidence that portal-based traversal remains immediately recognizable.
- `Sophie in the Tangled World` demo — https://daniilstrunov.itch.io/sophie-in-the-tangled-world — uses non-Euclidean/topological space as puzzle subject, but does not expose G4C01's exact player verb of joining authored boundary intervals as shared adjacency.
- `Non-Euclidean Minesweeper` — https://store.steampowered.com/app/3380320/NonEuclidean_Minesweeper/ — reinforces that non-Euclidean geometry itself is not an ownable novelty claim.

No searched result surfaced the exact G4C01 rule. The final risk is therefore not direct imitation but **player perception**: if normal play reads as a portal game, the technical distinction has low commercial value.

## Real-time squad command
Current tactical-command systems continue to lean heavily on explicit command/planning interfaces. For example `DIRECT CONTACT`'s 2026 tactical-command update exposes a command mode, drawn movement paths and waypoint gaze controls rather than embodied wake-crossing. This supports G4C43's input distinctness, but does not solve its readability/choreography risk.

Search conclusion: no direct market kill is triggered for any final-three concept. The final decision therefore turns on product shape, full-game repetition defense, implementation ambiguity and whether the central verb remains frequent and pleasurable after tutorial novelty.

---

# 2. G4C19 — FINAL ATTACK: 12 mature encounter kernels

Frozen tournament grammar remains intentionally small:
- rooms/areas are acoustic nodes embedded in physical space;
- passages are acoustic edges with attenuation class;
- sound strength is a small integer/band set;
- guards/listeners have visible hearing thresholds;
- one movable absorber occupies authored world-space edge slots and adds a fixed attenuation penalty;
- doors/moving physical sources may alter the graph only through visible world state;
- prediction is exact and visually available before the player commits a sound-producing action;
- silence is not always the goal; selective audibility is a first-class solution pattern.

The 12 kernels below are not proposed final levels. They test whether the same grammar can produce mature decisions without relying on hidden systems or long patrol waits.

| # | Kernel | Core decision | Selective audibility? | Active traversal? | Multiple acoustic routes? | Patrol timing required? | Absorber moves |
|---|---|---|---|---|---|---|---:|
| S1 | Static Split | two stationary sentries; make footsteps reach A but not B before crossing | YES | YES | YES | **NO** | 2 |
| S2 | Threshold Fork | weak footsteps may reach one listener; loud glass must be routed differently because thresholds differ | YES | YES | YES | **NO** | 2 |
| S3 | Twin Route Sentry | one listener has two equal-cost acoustic paths; silence-one-door fails, so player preserves the route toward the useful listener | YES | YES | YES | **NO** | 3 |
| S4 | Triggered Investigator | both guards begin stationary; player deliberately makes A hear a thrown object so A self-creates the traversal window while B remains unaware | YES | YES | YES | **NO** | 2 |
| S5 | Door Fork | opening a necessary physical door also creates a second sound route; absorber must move after traversal changes graph | YES | YES | YES | NO cyclic patrol; door-state reasoning only | 3 |
| S6 | Moving Cart Source | cart noise migrates through the building; player repositions blocker so its noise pulls B away without recalling A | YES | YES | YES | minor spatial timing, not patrol waiting | 4 |
| S7 | Footstep Corridor | player's own movement continually changes source node; blocker must be moved while progressing rather than once at entrance | YES | YES | YES | NO | 3 |
| S8 | Strong Leak | loud glass partly survives absorber attenuation while footsteps do not; player exploits threshold asymmetry instead of expecting binary silence | YES | YES | YES | NO | 3 |
| S9 | Two Sound Classes | thrown object and footsteps need different propagation routes in the same spatial state | YES | YES | YES | NO | 4 |
| S10 | Three-Path Lure | two guards + three routes; absorber cannot silence all paths, and the correct solution intentionally leaves one target route open | YES | YES | YES | low | 4 |
| S11 | Return Geometry | objective changes guard locations and a door state; the safe outgoing absorber slot is now the wrong return slot | YES | YES | YES | low | 3 |
| S12 | Final Split | moving source + two guards + changing door + strong final action; player performs four acoustic edits and two deliberate lures during one escape | YES | YES | YES | low; player-created windows dominate | 5 |

## 2.1 Required four no-patrol proofs

The instruction required at least four mature kernels that remain interesting if patrol timing is removed. **S1–S5, S7–S9** all satisfy that condition on paper. Their listeners may react after hearing a sound, but there is no autonomous cycle the player must wait out before making the core decision.

This matters because the game can create stealth tension from **acoustic routing + player-triggered reactions**, rather than borrowing most of its challenge from standard patrol timing.

## 2.2 Absorber interaction frequency

Across the twelve paper kernels:
- total encounter time assumption: **1,460 seconds**;
- total meaningful absorber repositions: **38**;
- mean interval: **~38.4 seconds per meaningful reposition**;
- mean rate: **~1.56 meaningful absorber moves/minute**.

This is frequent enough to remain a central verb, but not so frequent that the player is continuously dragging a panel instead of infiltrating. Dense demo/finale moments can target roughly one meaningful edit every 20–30 seconds; exploratory mature spaces can tolerate 35–45 seconds.

**Product gate:** if a playable prototype falls below roughly one meaningful acoustic edit per 60 seconds for long stretches, the absorber risks becoming occasional setup rather than the game.

## 2.3 Tactility attack

A graph can be intellectually elegant but physically weak. Therefore the absorber interaction should not become `select edge E7 from UI`.

Minimum physical contract for Phase 3 consideration:
- absorber is a large visible world object or shutter moving on rails/tracks;
- player can push/slide/rotate it quickly through snap slots;
- propagation preview updates continuously during the physical move;
- the blocker visibly occludes the doorway/opening it affects;
- player regains traversal control immediately; no modal graph screen;
- at least some mature spaces allow repositioning while the player remains exposed/moving, so acoustic editing and infiltration overlap in time.

If prototype users say they are `editing the map` more often than `moving a soundproof barrier so that only the right guard hears me`, the physical fantasy is failing.

## 2.4 `Smuggler` title/fantasy burden attack

The current working title is now judged a liability rather than an asset.

`Smuggler` implies:
- contraband/cargo as a major object;
- delivery/extraction narrative obligations;
- possibly NPC/economy/content systems unrelated to the acoustic verb;
- unwanted high-level resemblance to earlier factory logistics/cargo identities.

None of those are necessary for the mechanic.

**Tournament decision:** select the **acoustic-infiltration mechanic**, not the `smuggler` wrapper. Phase 3 must test/re-title the product around infiltration, audibility routing or acoustic barriers without inventing a cargo economy. `Soundproof Smuggler` remains only a historical working label until then.

## 2.5 Full-game scaling defense

Credible premium target remains approximately:
- **30–36 main encounters**;
- **8–10 advanced/remix/mastery encounters** if justified;
- 5–8 hour first clear target before optional replay;
- <=12 acoustic nodes in normal mature encounters;
- one absorber baseline;
- <=4 sound-strength bands;
- 2 listeners normal, 3 exceptional;
- no ray-traced acoustics and no hidden hearing math.

The content authoring burden is primarily spatial graphs + physical traversal + listener placement. That is material but data-driven. The 12-kernel test shows at least four distinct reasoning families without new mechanics:
1. **route selection** — which path remains audible;
2. **threshold discrimination** — weak/strong sounds behave differently;
3. **selective lure** — one listener should hear while another should not;
4. **graph mutation during traversal** — doors/moving sources make the useful blocker slot change over time.

This is a stronger hour-10 defense than `silence the nearest door`.

## 2.6 Soundproof kill result

No paper hard-kill triggered.

Remaining empirical kill gates:
- visual-only optimal decisions must be identical to audio-enabled play;
- predicted hearing must match actual hearing 100% in deterministic cases;
- passive waiting must remain <20–25% and preferably <10–15%;
- nearest-door blocking must not dominate mature solutions;
- meaningful absorber edits should not fall below ~1/minute for long mature stretches;
- players must describe deliberate audibility, not only `make everything quiet`.

**FINAL VERDICT: SURVIVES STRONGLY.**

---

# 3. G4C01 — FINAL ATTACK: 12-room paper campaign

The campaign test uses only frozen tournament semantics and no new topology primitives.

## 3.1 Paper progression

| Room | Primary reasoning | Crossing-led? | Contact/support/collateral adjacency materially central? |
|---|---|---:|---:|
| T1 First Stitch | join two static compatible edges and cross | YES | NO |
| T2 Straight / Cross | explain aligned vs reversed endpoint mapping through ghost continuation | YES | secondary |
| T3 Shared Crossing | player + crate use same seam | YES | secondary |
| T4 Sweeper Corner | hazard crosses seam in mapped orientation while player reuses boundary | YES | YES |
| T5 Beam Support | seam creates a contact/support relationship that a simple private doorway would not express | NO | **YES** |
| T6 Bad Neighbor | route is useful but also makes hostile boundary directly adjacent | NO | **YES** |
| T7 Order Swap | reversed tangent mapping changes two bodies' destination ordering | NO | **YES** |
| T8 Occupied Edge | player must clear a body from candidate boundary before seam can be committed | NO | **YES** |
| T9 Contact Relay | one stitch changes two support contacts and one route simultaneously | NO | **YES** |
| T10 Safe Removal | seam must be removed only after dependent contact/crossing occupancy clears | NO | **YES** |
| T11 Collateral Sweep | same adjacency solves access but makes a rolling hazard threaten a previously isolated region | NO | **YES** |
| T12 One Edit / Three Consequences | route + hazard redirection + support condition all change from one seam | NO | **YES** |

Result:
- crossing-led/tutorial-heavy rooms: **4/12**;
- rooms where contact/support/collateral adjacency is materially central: **9/12** counting T4 and T5–T12;
- mature half T7–T12: **6/6** depend on more than `entrance here / exit there`.

The campaign therefore survives the paper portal-equivalence attack.

## 3.2 Final seam lifecycle semantics

The tournament exposed several implementation ambiguities. The smallest safe rule set is:

### Creation
1. seam commands commit only at canonical fixed-step boundaries;
2. only static authored compatible intervals may be endpoints in 1.0;
3. **moving seam endpoints are removed from the 1.0 scope** because moving-frame adjacency adds large collision/readability complexity without being required for the 12-room depth proof;
4. creation is illegal if either endpoint's transfer/contact envelope is occupied in a state that would require body penetration or ambiguous chart ownership;
5. valid creation is atomic; contacts are recomputed before dynamics advance.

### Crossing
- a body crossing an interval maps once per tick;
- tangent coordinate is preserved or reversed according to visible mapping mode;
- local tangent/normal velocity basis maps into the destination interval basis;
- a one-tick crossing token prevents immediate recursive remap;
- no seam-seam recursion because only one active seam pair exists baseline.

### Removal
- removal is accepted only at a fixed-step boundary;
- removal is **blocked** while any body is in the seam transfer envelope or has a multi-boundary dependency that cannot be represented on one physical side after removal;
- ordinary resting contacts that do not span the seam may remain and simply lose the remote adjacency relation;
- if the seam currently supplies cross-boundary support to a body, UI explicitly marks `clear supported object first`; no mid-body splitting/folding semantics are invented for 1.0.

This rule sacrifices dramatic `rip the seam away under a spanning beam` moments, but sharply reduces ambiguity and still preserves the mature support family.

### Reset / death / recovery
- room/case checkpoint stores exact seam endpoint pair + mapping mode + canonical body states;
- restart returns to authored initial state;
- Undo, if later included, restores one exact prior checkpoint rather than inverse topology simulation;
- player death during a crossing can only occur after the atomic crossing result is resolved, never in a half-mapped state;
- reload cannot resume half a seam command.

## 3.3 Reversed mapping without topology jargon

Player-facing language should not say `orientation-preserving/reversing homeomorphism` or `tangent parameter`.

Presentation test:
- every candidate edge has two visible endpoint marks, e.g. **dot** and **notch**;
- `Straight Stitch` preview connects dot→dot and notch→notch;
- `Cross Stitch` preview visibly twists the thread so dot→notch and notch→dot;
- a ghost player/crate continuation appears at the destination before commit;
- arrows on the thread show travel direction after crossing.

A non-technical player only needs to understand `straight` versus `crossed ends`.

## 3.4 Seam Thief product attack

The paper depth case is excellent, but three costs remain higher than G4C19:

1. **Implementation/QA:** even after removing moving endpoints, support/contact relationships across nonlocal stitched intervals require custom deterministic collision/contact logic.
2. **Commercial perception:** the mechanic is meaningfully broader than portals internally, but the first minute still begins with joining two places and crossing between them; empirical `portal` perception remains a hard existential gate.
3. **Explanation burden:** reversed mapping and whole-edge adjacency can be shown visually, but the player must learn a spatial convention before the strongest non-portal value appears.

The content burden remains credible: roughly 32–38 rooms + optional remixes, <=6 dynamic object families, one seam pair baseline.

**FINAL VERDICT: SURVIVES, but loses the risk-adjusted final to G4C19.**

---

# 4. G4C43 — FINAL ATTACK: 10 mature mission kernels

Frozen tactical grammar:
- one directly controlled leader;
- normal mature encounters: **2–3 commandable agents**;
- agents move on deterministic visible route graphs;
- wake crossing issues one short-lived command to the wake owner;
- core command families remain TURN_NEXT, HOLD_ONE_NODE, FOLLOW_WAKE at this tournament stage;
- latest intentional unconsumed crossing overwrites prior pending command for that agent;
- wake lifetime and command expiry use logical simulation time;
- same-tick multi-crossing is deterministic but must not be required for baseline/optimal content.

## 4.1 Mission kernels

| # | Mission kernel | Tactical question | Fixed route becomes memorized after solve? | Leader movement meaningful between commands? |
|---|---|---|---|---|
| C1 | Two-Agent Gate | which ally turns first so both pass a shared gate | YES | moderate |
| C2 | Hold / Pass | hold A for one node so B crosses first | YES | YES, leader must reach B wake next |
| C3 | Hazard Split | redirect one agent around hazard while keeping second on normal route | mostly | YES |
| C4 | Follow Chain | make B follow A's wake for one cycle while leader avoids B's trigger lane | YES | YES |
| C5 | Moving Gap | one altered route creates a temporary leader passage | partly | **YES** |
| C6 | Three-Way Order | sequence A/B/C through constrained junction | **YES strongly** | moderate |
| C7 | Overwrite Recovery | intentionally replace A's pending command after world state changes | partly | YES |
| C8 | Spatially Separated Pair | leader must choose which distant wake to reach before expiry | YES | **YES** |
| C9 | Hazard Escort | commands keep one agent out of hazard while leader traverses parallel danger | partly | **YES** |
| C10 | Final Flow | two temporary commands + one ignored wake create gate order while leader stays in motion | partly | **YES** |

## 4.2 Tactics-versus-route-memorization result

The kernel exercise exposes a structural weakness that earlier traces did not fully resolve:

- because routes, wake meanings and world timing are deliberately deterministic/readable, a successful mission tends to produce a reproducible leader path;
- **at least 5/10 kernels are strongly route-memorizable** once solved;
- another 4/10 can become memorized after the player understands the relevant command sequence;
- only limited moment-to-moment tactical uncertainty remains unless the design adds dynamic variation, stochasticity or more autonomous world response.

Adding such variation would directly worsen the concept's existential readability problem. Therefore the game is better described as a **real-time embodied action-puzzle** than true emergent tactics.

That is not a bad game, but it weakens one of the main reasons G4C43 beat safer puzzle candidates.

## 4.3 Leader-movement dead-air audit

Target healthy rhythm: one meaningful wake choice/avoidance every ~4–9 seconds in mature play.

The ten kernels can meet that target only if:
- routes are compact;
- hazards make travel itself positional rather than empty;
- wake placement is dense enough to keep decisions frequent but below the readability cap.

This creates a narrow tuning corridor: sparse wakes produce running dead air; dense wakes produce visual overload. G4C19 and G4C01 have wider viable density ranges.

## 4.4 Accessibility speed scaling

This part survives strongly.

Define simulation scale `s` over logical time:
- leader speed, agent speed, wake lifetime, fade time, pending-command expiry and hazard motion are multiplied by the same presentation/simulation scale;
- fixed logical event ordering and graph-node transitions are unchanged;
- crossing order is computed in logical step space, not wall-clock milliseconds;
- 0.5× or 0.75× play therefore gives more real-world reading time without changing which command occurs first.

A slower accessibility mode preserves solution logic. Optional mastery could later ignore or include speed only if Phase 7 deliberately chooses; baseline completion must not depend on normal speed.

## 4.5 Capsule / mute-clip attack

A normal clip requires the viewer to understand that crossing a colored/patterned trail changes the *owner's next behavior*, not the leader itself. That relationship can be taught quickly in play, but it is weaker in a silent store-page GIF than:
- Soundproof: barrier moves → sound route visibly changes → guard hears/does not hear;
- Seam: edges zip → spaces visibly join.

This is a meaningful discovery disadvantage under the factory's current demo/clip requirements.

**FINAL VERDICT: SURVIVES as a strong reserve concept, but loses final selection.** The design is promising enough to preserve for future mutation, especially if a later project wants a shorter score-attack/action-puzzle rather than a 5–8 hour systemic premium game.

---

# 5. Uniform final-product test

| Test | G4C19 acoustic infiltration | G4C01 Seam Thief | G4C43 Command Wake |
|---|---|---|---|
| One-sentence pitch without jargon | **Strong** — move one soundproof barrier to decide who hears each action | Strong — sew two room edges so they become one continuous boundary | Medium-strong — issue orders by crossing allies' wakes |
| Mute 10-second clip | Strong with visible wavefronts/listener state | **Very strong** geometry transformation | Medium; owner-command relationship must be learned |
| Minute-1 independent decision | YES | YES | YES |
| Minute-20 demo climax | selective lure + split audibility + changing route | one seam changes route/hazard/support | two-command live chain with leader hazard traversal |
| Hour-3 depth | **Strong** graph/threshold/lure/world-state composition | **Very strong** contact/support/orientation composition | Strong but increasingly choreography-like |
| Hour-10 repetition defense | Strong if selective audibility remains mandatory | Strongest abstract ceiling | Medium-strong; route memorization pressure |
| 5–8 h content burden | **Medium / data-driven** | Medium + high QA | Medium + choreography/readability QA |
| Technical predictability | **High** integer graph | Medium; custom topology/contact | High-medium deterministic graph |
| Accessibility | **Excellent** full visual parity possible | Strong with snapped previews | Strong with global speed scaling, but visual density risk |
| Market / fantasy distance | **Strong**, provided title drops generic smuggling obligations | Strong but portal perception remains | Strong market distance |
| Portfolio distance | **Very strong** stealth/acoustics | Medium-strong systemic puzzle | Very strong action/puzzle |
| One-week kill test quality | **Excellent and quantitative** | Excellent but requires nontrivial topology prototype | Excellent |
| Simplification preserves identity | **YES** — graph model strengthens clarity | Partly; simplification can erase support/contact advantage | Partly; density simplification risks running dead air |
| Biggest unresolved risk | tactile frequency / `silence everything` | portal perception + topology QA | readability + route memorization |

---

# 6. One-week graybox kill plans

## Winner candidate — G4C19
Build:
- 6–8 spatial rooms/nodes;
- 2 guards/listeners;
- footsteps + one louder sound;
- 3–4 absorber slots on a visible rail;
- 2 alternate acoustic routes;
- exact visual preview and no-audio mode;
- one stationary-listener kernel and one active-lure kernel.

Kill if any core condition fails:
1. visual-only player receives less decision information;
2. predicted hearing ever disagrees with deterministic result;
3. players solve primarily by waiting rather than acoustically editing;
4. blocker always goes in nearest doorway;
5. deliberate `make A hear / keep B quiet` is not understood by demo end;
6. blocker is touched so rarely that it feels like setup furniture.

## Seam Thief
Build 12-room geometry test with at least 6 non-crossing/contact/collateral rooms. Kill on >35% portal descriptions, orientation prediction failure or custom collision complexity disproportionate to room count.

## Command Wake
Build 3-agent arena with 3 commands and 10 short sequences. Kill if wake-owner command relation is not understood in mute play, misprediction >15%, pause/dead-air >30%, or solved missions become pure route execution with little ongoing decision value.

---

# 7. Explicit loss cases

## Why Seam Thief loses to G4C19 in this tournament
Seam Thief has the **higher theoretical puzzle ceiling** and arguably the strongest 10-second geometry clip. It loses because:
1. its differentiation from portals depends on contact/support semantics that are also the hardest custom technical/QA area;
2. the strongest mature value arrives after the player understands a nontrivial spatial mapping convention;
3. removing moving seam endpoints and unsafe removal semantics was the correct scope cut, but it shows how quickly technical simplification can consume advertised possibilities;
4. G4C19 achieves a comparably distinctive systemic loop with a simpler deterministic state model and stronger accessibility parity.

This is a risk-adjusted commercial/production loss, not a claim that Seam Thief is the weaker pure puzzle idea.

## Why Command Wake loses to G4C19
Command Wake has the best action/tactics portfolio departure and excellent input economy. It loses because:
1. final mission kernels reveal route memorization as a structural consequence of the very determinism needed for readability;
2. keeping leader movement interesting creates a narrow density window between dead air and wake overload;
3. the normal-play GIF requires one learned owner-command convention before the causal relation is obvious;
4. a 5–8 hour premium game would need careful mission choreography to avoid solved-route repetition.

It remains a valuable reserve for a shorter, more score-driven action-puzzle mutation.

---

# 8. Selection decision

**GAME #004 WINNER: G4C19 — acoustic-infiltration / physical sound-routing concept.**

Historical working label: **Soundproof Smuggler**.

The selection is specifically **not** a lock of that title, cargo/smuggling fiction, campaign size, price, final art style, exact guard fiction or exact progression. Those belong to Phase 3+.

What is selected:
- central fantasy: physically alter the acoustic connectivity of a space so the player controls who can hear an action;
- central repeated verb: move/rotate one world-space sound-absorbing barrier between authored slots and immediately see exact propagation change;
- core tension: silence is not universally optimal; good play selectively routes sound to create openings while suppressing dangerous listeners;
- technical identity: small deterministic spatial acoustic graph, not realistic audio simulation;
- accessibility identity: all mechanically relevant acoustic information must be available visually, so no-audio play preserves the same decisions;
- product shape hypothesis: compact premium single-player infiltration/systemic puzzle with active traversal, not a plan-only graph editor.

Why evidence is decisive enough to stop the tournament:
1. it survives 12 mature kernels using the same small grammar;
2. at least eight kernels remain meaningful without autonomous patrol-cycle timing as the core challenge;
3. paper interaction rate keeps the physical blocker central (~1.56 meaningful moves/minute across mature kernels);
4. deterministic implementation is materially simpler than Seam Thief's topological contact model;
5. final discovery/readability is stronger than Command Wake after one learned visual language;
6. portfolio distance is high without requiring networking, giant art volume or simulation realism;
7. its remaining risks are unusually clean empirical prototype gates rather than missing design primitives.

**PHASE 2 CONCEPT TOURNAMENT = COMPLETE.**

---

# 9. Phase-3 entry constraints

Phase 3 must not quietly rescue the winner with feature growth. Product Thesis should freeze the smallest coherent product around the selected verb.

Mandatory Phase-3 questions:
1. Replace or justify the working title `Soundproof Smuggler`; do not assume cargo/smuggling is core.
2. Freeze target platform/audience/genre framing and one-sentence hook.
3. Freeze whether player physically accompanies the absorber, remotely moves it, or both; preserve in-world tactility and avoid modal graph editing.
4. Define the exact baseline encounter loop from inspect → reposition absorber → preview → create/avoid sound → listener reaction → traverse → revise.
5. Freeze which sound-source families are truly core. Keep the vocabulary tiny.
6. Freeze the role of guard movement: patrols may exist, but the game cannot depend on waiting as its main difficulty source.
7. Freeze a scope ceiling for nodes, listeners, absorber count, sound bands and encounter length.
8. Freeze visual/no-audio parity as a product requirement, not optional accessibility polish.
9. Define first-session/demo promise so selective audibility appears before the demo ends.
10. Keep one-week prototype kill gates explicit and do not claim the mechanic is fun before they are empirically tested.

## NEXT ACTION — PHASE 3 PRODUCT THESIS LOCK

Create `GAME4_PRODUCT_THESIS.md`. Re-read the full Game #004 authority chain, then lock the product identity for the selected G4C19 acoustic-infiltration concept. Use fresh market/title/genre research where useful. Do not begin Phase 4 mechanical expansion until the thesis clearly answers target player, platform, genre framing, hook, fantasy, session structure, core loop, differentiator, scope ceiling, demo promise and explicit non-goals.
