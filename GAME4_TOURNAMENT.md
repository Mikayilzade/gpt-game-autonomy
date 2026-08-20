# GAME #004 — CONCEPT TOURNAMENT — RUN 1

Last updated: 2026-08-20
Factory run: **4**
Phase: **2 — Concept Tournament**
Concept selected: **NO**

This pass applies one destructive rubric to all seven Phase-1 survivors. It does not select Game #004. Current analogue checks were refreshed before scoring. Search also surfaced the older mobile game **Stagehand: A Reverse Platformer**, whose identity is controlling/moving stage platforms while an auto-runner moves; this materially increases naming and nearest-neighbor pressure on G4C11 even though G4C11's three depth-track collision-ownership rule remains mechanically different. The tournament therefore judges the mechanic, not the working title.

---

## 1. Uniform destructive rubric

Each concept is judged on the same ten dimensions, 0–10 each:
1. **Hook** — understandable in one sentence and visually ownable.
2. **Repeated feel** — the core 5–15 second action looks satisfying after novelty fades.
3. **Demo strength** — supports a 15–25 minute demo with escalation and a memorable climax.
4. **Hour-10 depth** — can deepen without rule sprawl or huge authored volume.
5. **Systemic leverage** — small rule/content vocabulary produces many situations.
6. **Scope safety** — feasible for a small implementation track; lower bespoke burden scores higher.
7. **Technical predictability** — deterministic, testable and low-fragility.
8. **Readability/accessibility** — controller, mute play, visual prediction, low surprise.
9. **Market distance** — survives nearest-neighbor comparison.
10. **Portfolio distance** — meaningfully different from Games #001–#003.

Hard failures override totals: dominant trivial strategy; core depends on trial-spam; demo needs long explanation; accessibility changes optimal logic; one-week graybox cannot invalidate the thesis; or the identity collapses when simulation is bounded enough to ship.

---

# 2. G4C01 — Seam Thief

## Demo beat sheet (20 minutes)
- **0:00–2:00:** movement and one authored seam pair demonstrated without text; stitch two equal floor edges and cross the resulting continuous boundary.
- **2:00–5:00:** first independent choice among three compatible edges; wrong seam is visibly legal but creates a longer route, teaching that seam is adjacency rather than a key.
- **5:00–8:00:** orientation preview; aligned vs reversed endpoint mapping changes exit direction.
- **8:00–12:00:** crate and rolling hazard cross the same seam, proving it is not player-only teleportation.
- **12:00–16:00:** shared-support puzzle: one long body relies on the stitched boundary while player must also traverse it.
- **16:00–20:00:** climax: one seam simultaneously gives the player access, redirects a hazard and changes support; reversed mapping is required. End on a clean multi-object chain visible in one screen.

## Long-session play
**Hour 1:** stitch/unstitch while moving through compact deterministic rooms; inspect ghost continuation, commit, exploit one adjacency, revise. **Hour 3:** moving eligible edges, collateral adjacency, seam locks and multi-object timing create relationship-graph puzzles. **Hour 10:** mastery is recognizing which single adjacency edit changes several relationships at once; optional low-edit solutions and remix rooms can vary object arrangements without new seam verbs.

## Burden / risk
Bespoke burden: **medium** — authored compatible edges and rooms. Systemic leverage: **high** — orientation × object families × support × hazards. Technical risk: **medium** because edge mapping/collision continuity must be exact. QA surface: **medium-high** around bodies occupying seam boundaries and orientation transitions.

Dominant strategy risk: stitch nearest useful edge to goal. Countermeasure must come from authored compatibility plus collateral consequences, not arbitrary seam cost. Brute force risk: moderate if rooms expose too many compatible pairs; cap early choice sets and make preview causal. Waiting risk: low. Readability risk: medium around transformed orientation.

Controller/onboarding/accessibility: snap only to compatible intervals; two-button endpoint mapping; preview tangent arrows, ghost body continuation and illegal reason. No color-only semantics. First independent decision by minute 3.

One-week graybox remains existential: 12 rooms can kill the concept if >35% are perceived as portals or if multi-object adjacency does not produce richer reasoning.

**Score:** Hook 9.2 / Feel 8.0 / Demo 9.1 / H10 8.8 / Leverage 9.0 / Scope 8.0 / Tech 7.5 / Readability 7.7 / Market 8.4 / Portfolio 8.0 = **83.7/100**.

**Verdict: ADVANCE.** Highest puzzle-system ceiling, but Phase-2 Run 2 must attack portal equivalence and collision-edge QA harder.

---

# 3. G4C19 — Soundproof Smuggler

## Demo beat sheet (20 minutes)
- **0:00–2:00:** player walks; footsteps emit visible propagation pulse; guard hearing state changes with no audio dependency.
- **2:00–5:00:** slide absorber into one doorway and preview the next footstep route before moving.
- **5:00–8:00:** two paths around rooms show why blocking one edge may be insufficient.
- **8:00–12:00:** two sound strengths: footsteps vs glass; player must choose which route can safely carry each.
- **12:00–16:00:** deliberate lure: preserve audibility toward Guard A while suppressing Guard B, then cross during investigation.
- **16:00–20:00:** climax combines moving source, two guards and a door changing graph topology; solution requires selective hearing rather than silence.

## Long-session play
**Hour 1:** move blocker, preview propagation, execute traversal/lure. **Hour 3:** multiple routes, thresholds, doors, moving sources and patrol interaction. **Hour 10:** challenge comes from choosing *who should hear what* while traversing, with mastery goals for time/no resets/selective alerts rather than simply perfect stealth.

## Burden / risk
Bespoke burden: **medium** — encounter graphs and patrols. Systemic leverage: **high** if sound classes and patrols recombine. Technical risk: **low-medium** because integer graph propagation is deterministic. QA surface: **medium**; every predicted route must match actual hearing exactly.

Dominant strategy risk: nearest-door blocking or waiting. Waiting is existential: levels need moving objectives/short patrol cycles without turning into twitch stealth. Brute force: moderate but preview reduces random testing. Readability: potentially excellent if graph is rendered spatially without becoming an abstract overlay.

Controller/accessibility: blocker rails and snap slots; every acoustic state has simultaneous visual route/intensity glyphs; no audio-only cue. First decision before minute 3.

One-week graybox is strongly falsifiable: visual-only parity, waiting share, blocker dominance and prediction accuracy are measurable.

**Score:** Hook 8.7 / Feel 7.7 / Demo 8.9 / H10 8.6 / Leverage 8.8 / Scope 8.5 / Tech 8.7 / Readability 8.5 / Market 8.4 / Portfolio 9.2 = **86.0/100**.

**Verdict: ADVANCE.** Best current balance of novelty, determinism, accessibility proof and portfolio distance. Main danger is stealth pacing becoming wait-heavy.

---

# 4. G4C11 — Stagehand Zero (working title invalid)

Fresh search found **Stagehand: A Reverse Platformer** (2017), explicitly built around controlling/repositioning stage platforms while an automatically moving character traverses hazards. That does not duplicate three-track collision ownership, but it invalidates the working name and narrows the claimable fantasy space.

## Demo beat sheet (18 minutes)
- **0:00–2:00:** actor walks continuously; player slides a painted stair from backdrop to live track and it becomes solid.
- **2:00–5:00:** first choice: activate bridge or barrier before cue.
- **5:00–8:00:** move live prop backstage to remove collision, proving both activation and subtraction.
- **8:00–12:00:** actor and hazard share live track; one scenery move helps one and harms the other.
- **12:00–15:00:** two props on rails with timing overlap.
- **15:00–18:00:** climax requires a three-step scenery sequence while show continues, ending with visible stage transformation.

## Long-session play
**Hour 1:** timed track swaps and route shaping. **Hour 3:** track-locked actors, shared props, cue windows. **Hour 10:** concern rises sharply: if all mature content remains `make silhouette solid/not solid at right time`, authored sequence burden may grow faster than systemic depth.

Bespoke burden: **medium-high** because good sequences need choreography. Leverage: medium. Tech: high predictability with discrete tracks. QA: medium. Dominant strategy: parking universally useful props on live track; needs spatial conflicts. Waiting: low-medium. Readability: strong if tracks are unmistakable, but auto-runner pressure can become execution rather than reasoning.

Controller path is simple lane select + track shift. Accessibility requires generous cue timing, speed options that preserve logic, clear collision preview and no depth communicated by color alone.

One-week graybox can kill on surprise-collision rate and prop exception count.

**Score:** Hook 8.3 / Feel 8.1 / Demo 8.5 / H10 7.1 / Leverage 7.2 / Scope 8.1 / Tech 8.7 / Readability 8.2 / Market 6.8 / Portfolio 8.8 = **79.8/100**.

**Verdict: ELIMINATE from leading tournament.** Mechanically viable, but nearest-neighbor fantasy pressure plus choreography burden and weaker hour-10 systemic leverage place it below four stronger concepts. Preserve as reserve only; working title must never ship.

---

# 5. G4C24 — Debris Sculptor

## Demo beat sheet (22 minutes)
- **0:00–3:00:** choose one of two fracture seams; resulting step/wedge appears in deterministic pose.
- **3:00–6:00:** source wall now has a real opening, teaching destruction cost.
- **6:00–10:00:** wedge redirects a roller while remaining wall blocks hazard.
- **10:00–14:00:** two source structures; breaking both is demonstrably worse than selective harvest.
- **14:00–18:00:** same chunk affordance solves traversal or machinery depending on placement zone.
- **18:00–22:00:** climax requires preserving one support, harvesting a blocker and using source hole as route.

## Long-session play
**Hour 1:** inspect fracture previews, break, exploit source consequence and chunk affordance. **Hour 3:** source functions and chunk roles cross-combine. **Hour 10:** risk is authored-fracture fatigue: deterministic chunks solve QA but reduce expressive destruction, potentially turning each object into a disguised multi-choice dispenser.

Bespoke burden: **high-medium** — every source needs meaningful authored fractures and settle zones. Systemic leverage: medium-high. Technical risk: medium-low after deterministic bounding. QA: medium-high because chunk/source combinations multiply.

Dominant strategy: break everything; hard kill if >20%. Brute force: choose each fracture and reset. Need preview to make reasoning causal, but too-complete preview can make puzzles mechanical. Waiting: low. Readability: good.

Controller: target fracture, preview pieces, confirm; no pixel placement. Accessibility straightforward with shape/affordance icons and quick reset.

One-week graybox is existential and cheap enough.

**Score:** Hook 8.6 / Feel 8.5 / Demo 8.7 / H10 7.7 / Leverage 7.9 / Scope 7.4 / Tech 8.0 / Readability 8.3 / Market 7.6 / Portfolio 8.8 = **81.5/100**.

**Verdict: ADVANCE, but fourth seed.** Strong physical trailer language; must prove deterministic destruction still feels like destruction and not a menu of fracture recipes.

---

# 6. G4C47 — Umbrella Engine

## Demo beat sheet (20 minutes)
- **0:00–3:00:** four angle states introduced through one windy corridor; wide catches wind, closed passes narrow gap.
- **3:00–6:00:** first cargo falls; choose wide to deflect or inverted to catch.
- **6:00–10:00:** shelter-sensitive passenger makes wide state valuable while lateral wind makes it dangerous.
- **10:00–14:00:** carry caught cargo through doorway by narrowing without losing it under explicit state rule.
- **14:00–17:00:** overhead hazard + crosswind creates state timing conflict.
- **17:00–20:00:** climax chains catch → travel → shelter → narrow passage using the same four states.

## Long-session play
**Hour 1:** open/close state switching while moving through environmental tradeoffs. **Hour 3:** cargo classes, wind classes, shelter agents and tight passages. **Hour 10:** danger: authored environments may simply ask players to recognize which of four states matches the current obstacle; mastery can become state lookup rather than emergent control.

Bespoke burden: medium. Leverage: medium-high if several systems react simultaneously. Technical risk: low after response-table bounding. QA: medium. Dominant state risk is directly measurable (>60% active time). Brute force low because only four states, which is also a depth warning. Readability and controller fit are excellent.

Accessibility: four visually distinct silhouettes plus icons/haptics/audio redundancy; remappable state cycling/direct buttons; generous timing mode.

One-week graybox can falsify state dominance and whether players describe states as meaningful tradeoffs versus speed modes.

**Score:** Hook 9.0 / Feel 8.6 / Demo 9.0 / H10 7.3 / Leverage 7.8 / Scope 8.8 / Tech 8.9 / Readability 9.1 / Market 7.8 / Portfolio 9.3 = **85.6/100**.

**Verdict: ADVANCE.** Exceptional immediate legibility and production shape; Phase-2 Run 2 must attack hour-10 depth and four-state brute-force ceiling.

---

# 7. G4C43 — Command Wake

## Demo beat sheet (20 minutes)
- **0:00–3:00:** leader movement and one ally routine visible; cross wake once to flip next-node command.
- **3:00–6:00:** first independent choice between two ally wakes.
- **6:00–10:00:** temporary command expiry forces route planning while leader stays embodied.
- **10:00–14:00:** two agents' paths interact; one altered route creates a moving opening.
- **14:00–17:00:** overlapping wakes introduced with strict priority/visual separation.
- **17:00–20:00:** climax chains two commands while leader avoids hazard and squad reaches gate in order.

## Long-session play
**Hour 1:** weave through wakes to alter near-future routines. **Hour 3:** route geometry, expiry, command sequencing and hazards. **Hour 10:** can support score/mastery through fewer crossings/continuous flow, but readability deteriorates rapidly as agent count and command vocabulary rise; the scope ceiling of four agents/four commands is necessary.

Bespoke burden: medium. Leverage: high if maps and routine combinations suffice. Technical risk: medium-low deterministic graph movement. QA: medium-high around simultaneous crossings and wake priority.

Dominant strategy: repeatedly cross same wake to force desired command; needs cooldown/one-cycle semantics that do not feel arbitrary. Brute force possible if reset is fast. Waiting low. Readability is existential with three+ moving agents.

Controller: direct leader movement only; command is embodied collision with wake, excellent input economy. Accessibility requires high-contrast patterns/arrows, reduced-motion wake option, command preview and speed scaling without changing ordering.

One-week graybox has strong quantitative kill gates: misprediction >15%, mental/physical pause >30%, unreadable overlap.

**Score:** Hook 8.4 / Feel 8.7 / Demo 8.4 / H10 8.3 / Leverage 8.6 / Scope 8.2 / Tech 8.5 / Readability 6.9 / Market 8.3 / Portfolio 9.4 = **83.7/100**.

**Verdict: ADVANCE.** Strongest action/tactics departure, but readability risk is higher than its raw score suggests.

---

# 8. G4C46 — Inside-Out Safe

## Demo beat sheet (20 minutes)
- **0:00–3:00:** one outer-ring quarter-turn demonstrated; cams and pins visibly respond.
- **3:00–6:00:** first choice: direction and stopping notch to open one of two channels.
- **6:00–10:00:** introduce one-way catch; reversal no longer simply undoes state.
- **10:00–14:00:** rolling latch couples two distant internal regions.
- **14:00–17:00:** target asks for two simultaneous visible conditions.
- **17:00–20:00:** climax requires short sequence using hysteresis, with no labels/numbers and no blind timing.

## Long-session play
**Hour 1:** read visible mechanism, turn/reverse ring, form causal model. **Hour 3:** cams, followers, catches, plates and latches combine. **Hour 10:** major content problem: one physical machine can become visually dense, while multiple safe layouts weaken the `one object` identity. Puzzles may devolve into counting notches/state-search once mechanism is learned.

Bespoke burden: medium-high because mechanisms must be authored and visually debugged. Leverage: medium. Tech: high predictability. QA: medium. Dominant strategy: systematic notch enumeration. Brute force: high because one input and finite states make exhaustive traversal tempting. Waiting low. Readability initially strong but density ceiling arrives early.

Controller/accessibility excellent: left/right/stop, zoom/focus, motion speed controls, persistent state highlights. No audio dependency.

One-week graybox can directly measure blind timing and notch-counting.

**Score:** Hook 8.9 / Feel 7.8 / Demo 8.5 / H10 7.0 / Leverage 7.1 / Scope 8.2 / Tech 9.1 / Readability 8.0 / Market 8.0 / Portfolio 8.3 = **80.9/100**.

**Verdict: ELIMINATE from leading tournament.** Elegant and feasible, but finite-state brute force, visual-density ceiling and authored mechanism burden weaken long-session defense. Preserve as reserve.

---

# 9. Pairwise muted-clip wishlist tournament

Question: with no explanatory text/audio, which normal-play 10-second clip more likely makes the mechanic legible and worth opening the store page?

| Pair | Winner | Reason |
|---|---|---|
| Seam Thief vs Soundproof Smuggler | Seam Thief | geometry visibly zips into new adjacency; sound routing needs wave overlay literacy |
| Seam Thief vs Umbrella Engine | Umbrella Engine | broad physical noun and immediate multi-object reaction are faster to parse |
| Seam Thief vs Command Wake | Seam Thief | wake-command meaning needs one learned convention |
| Seam Thief vs Debris Sculptor | Debris Sculptor | break→use pieces is instantly physical, though less novel |
| Soundproof Smuggler vs Umbrella Engine | Umbrella Engine | absorber route flip is readable, umbrella state tradeoff is more universal |
| Soundproof Smuggler vs Command Wake | Soundproof Smuggler | visible propagation route has simpler causal before/after |
| Soundproof Smuggler vs Debris Sculptor | Debris Sculptor | destruction/construction is immediately understood |
| Umbrella Engine vs Command Wake | Umbrella Engine | one object, one silhouette change, several reactions |
| Umbrella Engine vs Debris Sculptor | Umbrella Engine | more ownable silhouette and less generic destruction association |
| Command Wake vs Debris Sculptor | Debris Sculptor | wake command needs glyph comprehension |

Muted-clip wins among leaders: Umbrella Engine 4, Debris Sculptor 3, Seam Thief 2, Soundproof Smuggler 1, Command Wake 0. This is a discovery test, not the overall winner; Command Wake can still win on sustained feel/depth.

---

# 10. Tournament Run-1 ranking

1. **G4C19 Soundproof Smuggler — 86.0** — strongest all-round system/portfolio case.
2. **G4C47 Umbrella Engine — 85.6** — strongest instant hook/feel/scope; depth unproven.
3. **G4C01 Seam Thief — 83.7** — strongest pure puzzle-system ceiling; technical/portal pressure.
4. **G4C43 Command Wake — 83.7** — strongest turnless tactics identity; readability pressure.
5. **G4C24 Debris Sculptor — 81.5** — strong physical demo, higher authored/QA burden.
6. G4C46 Inside-Out Safe — 80.9 — reserve, eliminated from lead set.
7. G4C11 Stagehand Zero — 79.8 — reserve, eliminated from lead set; working title invalid.

## Advancement decision
Five remain alive because Run 1 produced a genuine split between discovery strength and long-session strength. **No final concept is selected.** Run 2 should be harsher and reduce to 3–4.

### Mandatory Run-2 attacks
- **Soundproof Smuggler:** prove active stealth can keep waiting below 20–25%; test whether graph overlay feels like playing the map rather than inhabiting a space.
- **Umbrella Engine:** generate at least 12 mature encounter states using only four actuator states and existing object/wind classes; kill if obstacle→correct-state lookup dominates.
- **Seam Thief:** produce six non-portal-equivalent mature puzzle proofs and explicit seam collision/occupancy ordering; kill if authored compatibility feels arbitrary.
- **Command Wake:** simulate three-agent wake overlap and command priority for 3 minutes; kill if state cannot be predicted at normal speed.
- **Debris Sculptor:** prove 10 fracture decisions where source consequence and harvested affordance are both material; kill if fracture choice behaves like selecting a recipe.

Run 2 must also compare production burden for a 5–8 hour premium game, identify the smallest credible full-content target, and conduct a final nearest-neighbor search around the top concepts. Do not lock Phase 3 until a later pass has falsified the leading 3–4.