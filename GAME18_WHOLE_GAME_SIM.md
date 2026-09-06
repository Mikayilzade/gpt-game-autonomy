# GAME #018 — PHASE 9 WHOLE-GAME SIMULATION ON PAPER

Date: 2026-09-06
Selected concept: **LOCAL TIME**
Status: PHASE 9 COMPLETE — ADVERSARIAL REVIEW NEXT
Production implementation: NO

## 0. Purpose and authority rule

This pass simulates the entire product as a hostile player would experience it, using only the frozen Phase-3 through Phase-8 grammar. It is not production code and it does not treat an intended solution script as runtime truth.

Where the simulation exposes a contradiction, this file records an explicit minimal amendment. Earlier files remain historical authority for why the decision existed; the amendments in Section 15 override only the narrow conflicting clauses named there.

Paper layouts below are validation fixtures for the specified campaign case identities. Exact art positions and socket coordinates remain implementation/content-authoring details, but no new mechanic or semantic family is introduced.

## 1. End-to-end player model under test

The product succeeds only if the player repeatedly reasons in this compressed form:

1. identify what must be true **NOW** at the final Resolve;
2. identify what can become **DONE** earlier and remain earned;
3. identify any irreversible **LOCKED OUT** exposure that must happen later or never;
4. identify dispatch/arrival/accept boundaries that require separate Resolves;
5. reserve the final clock layout for simultaneous CURRENT requirements;
6. then choose placements and Resolves.

The product fails its identity if hour-5 play instead becomes:
- hover every socket;
- press Resolve after every legal layout;
- remember which layout caused a green reaction;
- restart and reproduce the discovered sequence.

The whole-game simulation therefore treats causal compression, not raw solvability, as the primary late-game test.

---

# 2. First boot and accessibility path

## 2.1 First launch — keyboard/mouse player
Expected sequence:
1. Logo.
2. Accessibility quick setup appears before prose-heavy onboarding.
3. Player chooses large text and Reduced Motion.
4. New Game begins LT01 after one short premise card.
5. No account, launcher, lore sequence or store upsell blocks first puzzle.

Result: **PASS.** Nothing in the authority chain requires a pre-game system the player cannot understand.

## 2.2 First launch — controller-only / Steam Deck target
At 1280x800:
- D-pad/left stick reaches quick-setup controls;
- A confirms;
- B backs out without trapping focus;
- text size changes do not push Continue/New Game off-screen;
- gameplay opens with the objective strip, selected-detail card and action rail all reachable by semantic focus navigation.

Result: **PASS WITH GATE.** The specification is coherent, but actual 1280x800 layout remains empirical. Phase 10 must attack focus order with maximum text size + pseudolocalization simultaneously.

## 2.3 Accessibility misunderstanding test
Player enables Reduced Motion and animation skip from first boot, then completes the demo. Because puzzle authority is computed before presentation and all state changes are present in icons/text/reason trace, no information is lost.

Result: **PASS.**

---

# 3. LT01–LT06 demo simulation

The target is not merely six solvable puzzles. The sequence must teach the causal language without tutoring the solution.

## LT01 — Breakfast at Eight

### Minute 0–2
The player sees:
- one 08:00 clock-zone;
- Bakery RAW;
- Bridge closed NOW;
- objective: Bread RISEN (DONE) + Bridge OPEN (NOW).

Selecting the clock shows legal sockets and exact footprint. Hover/selection may show that Bakery/Bridge would read 08:00, but does not say “RAW will become RISEN.”

Player places shared footprint and Resolves.

Reason trace:
- `08:00 covers Bakery -> RAW became RISEN (DONE)`
- `Bridge is NOW OPEN at 08:00`

Success.

### Hostile alternate
Player covers Bakery only, Resolves, then moves clock to Bridge and Resolves. RISEN remains. This is accepted and is important: the game does not demand the shortest authored sequence.

Teaching result: **PASS.**
The first case demonstrates that DONE persists after the zone moves if the player explores the alternate route.

## LT02 — Five Minutes Later, Somewhere Else

### Minute 2–6
The player sees fixed 07:55 Garden and movable 08:05. Dough begins RISEN. Garden rule visibly states:
- at safe condition -> COLLECTED;
- UNCOLLECTED under 08:05 -> WILTED (LOCKED OUT).

The first likely safe Resolve collects the flower while Bakery is not yet dangerously covered. Later 08:05 may bake dough.

### Hostile shortcut
Player deliberately places 08:05 over Garden before collection and Resolves.

Expected:
- WILTED is committed;
- hard failure names the exact rule;
- Undo Turn restores the pre-Resolve canonical checkpoint;
- no reverse-time animation occurs.

Teaching result: **PASS**, if the LOCKED OUT explanation is shown after the causal row and not as a generic “wrong move.”

### Critical comprehension checkpoint
After Undo Turn, player should be able to say: “The clock didn’t rewind anything; Undo restored the puzzle checkpoint.” This remains an empirical gate.

## LT03 — Shared Shadow

Two clock labels coexist: Bridge 08:00, Station 08:05. Station departure requires both CURRENT truths in the same pre-transition snapshot.

### Illegal overlap test
Player previews a socket causing 08:00 and 08:05 to cover the same site. Placement cannot commit. No beat or move is charged.

### Valid coupled Resolve
Player reaches Bridge=08:00 and Station=08:05, presses Resolve. TRAIN_DEPARTED is committed from the immutable snapshot.

Player immediately moves a clock after success/replay. Departure remains a persistent flag.

Teaching result: **PASS.**
The core phrase “different local times at once” is now mechanically demonstrated.

## LT04 — Handoff

Bread starts RISEN.

Expected beats:
1. 08:05 at Bakery -> BAKED.
2. Dispatch condition -> carrier moves parcel one hop.
3. Destination 08:10 -> ACCEPT/DELIVERED.

### Hostile expectation
Player expects arrival and acceptance in Beat 2. The animation stops the parcel and explicitly shows `ARRIVED — eligible next Resolve`.

Result: **PASS WITH UX DEPENDENCY.**
Without that boundary label, the rule will feel arbitrary. It is therefore a mandatory state cue, not decorative polish.

## LT05 — Bad Shortcut

No directive prompts. The player must inspect the visible Garden hazard before using the attractive 08:05 footprint that also covers Bakery.

### Failure route
Player takes the tempting broad footprint first:
- Bakery benefits;
- Garden irreversibly WILTS;
- failure explains both the beneficial transition and the fatal one.

This is a key fairness test: the reason trace must not hide a harmful row because success-looking animation occurred first.

Result: **PASS.**

## LT06 — Little Town, Different Times

Three clocks combine:
- ordered Bakery process;
- safe Greenhouse milestone;
- Bridge 08:00 CURRENT;
- Station 08:05 CURRENT;
- departure persistent flag;
- final objective mixes BAKED + TRAIN_DEPARTED + Bridge OPEN + Greenhouse safe.

### Causal solution logic
A competent player does not need an intended action script. The sufficient proof is:
1. secure Greenhouse before dangerous exposure;
2. advance Bakery persistently while temporary layouts are available;
3. create Station 08:05 + Bridge 08:00 simultaneously;
4. finish in a layout that preserves final CURRENT requirements.

### Socket-scanning test
Because the UI previews NOW only, a player can still inspect many sockets, but it does not reveal whether a placement is safe for future milestones. The player must read public rules.

Result: **PASS, but this is the first point where anti-enumeration quality becomes content-dependent rather than mechanically guaranteed.**

## Demo verdict
The six-case sequence is internally coherent and still fits the 25–35 minute target on paper.

No new tutorial case is required.

---

# 4. Demo completion -> full game -> Case 07

Demo completion screen:
- identity line: `Different local times. Persistent consequences.`
- Wishlist / Full Game;
- non-spoiler later-game images;
- no locked-content wall pretending the demo is a live service.

On full-game install, compatible demo progress imports:
- LT01–LT06 completion;
- best records;
- compatible settings/glossary;
- Case 07 unlock prerequisite.

## Clean install
No existing full save. Demo import creates full profile with demo completion and Case 07 available.

**PASS.**

## Existing stronger full progress
Full profile already completed Case 18; demo save only completed LT01–LT06. Import must not reset chapter/mastery unlocks or active progress.

**PASS under Phase-8 monotonic merge.**

## Repeated import
Same demo hash/revision appears again. No duplicate achievements, no new revisions for a semantic no-op, no regression.

**PASS.**

## Newer demo record after full progress exists
A better LT06 move record may merge while campaign progress remains monotonic.

**PASS.**

---

# 5. Representative campaign paper walks

These are not “the one correct route.” They test whether each planned case identity can exist inside the same grammar and still ask a distinct causal question.

## Case 09 — persistent preparation before repurposing a clock

Fixture:
- Clock A = 08:00;
- Clock B = 08:05;
- Bakery ordered RAW -> RISEN at 08:00 -> BAKED at 08:05;
- Bridge final CURRENT OPEN at 08:00;
- objective: BAKED + Bridge OPEN.

Causal proof:
1. bread can earn stages before the final layout;
2. 08:00 is temporarily useful at Bakery but must finish on Bridge;
3. 08:05 cannot substitute for the final CURRENT gate.

Representative route:
- establish 08:00 Bakery, Resolve -> RISEN;
- establish 08:05 Bakery, Resolve -> BAKED;
- restore 08:00 Bridge, Resolve if boundary/objective requires current check.

Hostile no-op:
If the authored ordered process accidentally used 08:00 for both RAW->RISEN and RISEN->BAKED, repeated Resolve with no placement would solve the process by waiting. That is legal kernel behavior but weak content.

**DEFECT FOUND D01: unchanged-layout farming can trivialize ordered processes.**
Minimal repair is a content/validator gate, not a new mechanic: after tutorial cases, no ordered process may gain multiple strategically useful consecutive milestones from repeated Resolve under an unchanged clock layout unless the repeated boundary itself is the explicit teaching point and another interacting system makes the wait meaningful.

## Case 18 — two handoffs + final current gate synthesis

Fixture:
- Bakery prepares cargo;
- trolley carrier transfers one hop to Depot;
- second handoff reaches Station input;
- Station accepts at 08:10;
- Bridge final objective requires NOW OPEN at 08:00.

Causal proof:
1. cargo must be prepared before carrier dispatch;
2. each carrier arrival creates a separate future acceptance boundary;
3. final Bridge CURRENT truth can be restored after persistent cargo milestones are earned.

Representative route:
- prepare cargo;
- dispatch first carrier;
- Resolve arrival;
- dispatch/handoff second channel when enabled;
- Resolve arrival;
- accept at Station under 08:10;
- finish with Bridge under 08:00.

Result: **PASS.**
This case is distinct from Case 09 because the challenge is boundary staging rather than process-state order.

## Case 24 — exposure + coupled trigger + move budget

Fixture:
- Garden UNCOLLECTED becomes COLLECTED under 07:55; exposure to 08:05 while uncollected -> WILTED;
- Bridge is OPEN_NOW at 08:00;
- Station coupled event requires Station 08:05 + Bridge 08:00 same snapshot;
- one cargo arrival must be present before the coupled departure;
- limited moves punish wasteful clock relocation.

Causal proof:
1. secure Garden before any broad 08:05 footprint can cover it;
2. stage cargo arrival before spending final relocations;
3. reserve 08:00 Bridge + 08:05 Station for the coupled Resolve.

Hostile brute force:
A player can enumerate final paired layouts, but doing so before securing Garden loses irreversibly. The public proof eliminates many legal layouts before search.

Result: **PASS if authored footprint topology makes Garden risk meaningful.**

## Case 30 — open synthesis with two materially different winning approaches

Fixture:
- one persistent process can be completed before or after an optional carrier route;
- final current objective requires two sites;
- a safe exposure milestone can be secured using either Clock A early or Clock B later;
- both routes satisfy campaign goal, one is move-efficient and one is beat-efficient.

Route family A:
- secure hazard early;
- finish process;
- stage carrier;
- final simultaneous layout.

Route family B:
- stage carrier first under a safe alternate footprint;
- use persistence to repurpose the clock;
- secure hazard later;
- final simultaneous layout.

Result: **PASS**, provided solver reports two solution families not related only by swapping equivalent clock IDs.

**Phase-10 requirement:** define “materially different route” structurally: different milestone partial order or different carrier/footprint role, not merely symmetric clock labels.

## Case 34 — three clocks + two carriers + move budget

Use the Phase-5 representative proof:
- Garden must be secured;
- cargo must be prepared before carrier window;
- final departure reserves Bridge 08:00 + Station 08:05.

Paper run shows the player can summarize the case in three causal claims before selecting the exact socket sequence.

The challenge remains planning because:
- clocks are only three;
- sites <=7;
- carriers <=2;
- final state consumes two specific clock roles;
- earlier milestones free clocks for repurposing.

Result: **PASS WITH ANTI-ENUMERATION GATE.**
If the socket graph contains many near-equivalent legal placements, the same rules become a scanning puzzle. Late-case difficulty must come from causal interaction, not socket count.

## Case 36 — finale, all core ideas, no new family

Fixture:
- ordered process with distinct stage requirements;
- one exposure consequence;
- one accepted cargo;
- one carrier channel (second optional only if variety requires);
- one coupled CURRENT event;
- final CURRENT objective;
- <=3 clocks, <=8 sites, <=6 normal Resolves target;
- no new time label introduced solely for difficulty.

Causal proof target:
1. irreversible hazard must be neutralized before the dangerous productive footprint;
2. cargo must be prepared and arrive before its service window;
3. persistent milestones free clocks from earlier jobs;
4. finale ends in the coupled CURRENT layout.

Hostile player attempts:
- park a clock and spam Resolve;
- try every final socket pair;
- intentionally create overlap conflict;
- skip all animations;
- undo repeatedly;
- reload between milestones.

None changes authoritative results. The only serious failure mode is authoring a finale whose proof does not compress the legal search.

Result: **MECHANICALLY PASS / CONTENT QUALITY NOT YET PROVEN.**
Phase 10 must attack the final catalog as a proof-shape portfolio, not only individual solvability.

---

# 6. Hour-5 test: causal reasoning vs raw enumeration

Assume the player is in Chapters 5–6.

Expected expert thought process:
- “That Garden must be DONE before I ever put 08:05 on the east footprint.”
- “The parcel can arrive now and wait; acceptance is later.”
- “Bridge and Station consume my 08:00/08:05 clocks in the final Resolve.”
- “Therefore I should earn Bakery’s persistent stage before committing those final roles.”

This is meaningfully different from raw permutation search because public causal claims remove large classes of actions.

## Enumeration pressure points
1. legal socket preview exposes exact coverage;
2. clocks <=3, so raw search may still be computationally easy for a human;
3. Undo is cheap;
4. reason trace makes experiments informative.

These are fairness strengths but can become brute-force encouragement.

## Required authoring defense
The design therefore adopts an explicit Phase-9 amendment:
- from Case 12 onward, every campaign case must have at least one **causal cut**: a public 2–6 claim proof that rules out a meaningful class of otherwise legal first/early placements before experimentation;
- Chapter 4 onward should normally have two independent causal cuts (for example irreversible prerequisite + reserved final current layout);
- a case fails content review if a fresh expert can solve it mainly by cycling all legal sockets without articulating a stable causal claim.

This does not require hidden information or a bigger action space. It requires better authored interactions.

Hour-5 verdict: **IDENTITY SURVIVES ON PAPER, conditional on stronger content gates.**

---

# 7. Resolve/no-op, interruption and recovery

## 7.1 Resolve with no placement
A no-placement Resolve must remain legal because:
- carrier arrival may need another boundary;
- ordered process may intentionally advance on successive boundaries;
- ACCEPT may become eligible after prior arrival.

If nothing authoritative changes and no carrier moves, the Resolve may still consume a beat when the player confirms it.

UX:
`No milestones changed this Resolve.`

Do not disable Resolve merely because no clock moved.

Result: **PASS, now explicit.**

## 7.2 Repeated Resolve spam
Repeated Resolve cannot create more than one persistent advance/entity/Resolve, but can still farm a poorly authored ordered process.

Handled by D01 content gate rather than kernel change.

## 7.3 Undo Placement
Unresolved movement is reverted and move cost refunded. No save/load complexity.

**PASS.**

## 7.4 Undo Turn
Restores exact pre-Resolve checkpoint including planning baseline.

**PASS mechanically.**

## 7.5 Quit after placement before Resolve
Loading should restore last committed canonical state plus safe planning state only if planning persistence is explicitly supported. Baseline may discard unresolved placement and reload committed state; it must not charge the move twice.

**PASS if implementation chooses one deterministic policy and communicates it.**

## 7.6 Quit immediately after Resolve
A contradiction appears between “autosave at pre-Resolve checkpoints” and the need to preserve the just-committed authoritative state.

**DEFECT FOUND D02: save timing could lose a committed Resolve while preserving only its undo checkpoint.**

Minimal amendment:
- each successful Resolve writes the new canonical active case state to profile/autosave;
- the separate pre-Resolve Undo Turn checkpoint is retained alongside it;
- loading resumes the post-Resolve state;
- Undo Turn may still restore the stored checkpoint after load if the case/save version matches;
- autosave failure never changes the already-computed in-memory result and must surface recoverably.

This is a persistence clarification, not a gameplay change.

## 7.7 Replay Last Resolve
Replay consumes trace/snapshots only. Skipping replay, closing it, or loading after it cannot call Resolve again.

**PASS.**

---

# 8. Controller-only and 1280x800 Deck path

Hostile navigation sequence:
1. open objective;
2. shoulder-cycle to Clock C;
3. enter placement mode;
4. navigate only legal sockets;
5. open rule detail on a covered site;
6. cancel;
7. move to action rail;
8. Resolve;
9. open What Changed?;
10. focus causal row and jump back to site;
11. Undo Turn;
12. Restart confirmation;
13. Pause/settings;
14. return to case.

Required invariant: every focus node has a deterministic route back to gameplay/action rail. No modal steals focus permanently.

## Deck readability stress
Worst normal case:
- 3 clocks;
- 8 sites;
- overlapping footprints;
- 3 objective truths;
- long localized selected-detail card;
- maximum text size.

The screen cannot show all full rule prose permanently without crowding. Core state must remain visible; detailed prose may expand in a focused panel.

**DEFECT FOUND D03: Phase-6 “core objective + selected rule + labels + conflict visible without modal” is correct, but late pseudolocalized rule prose cannot be assumed to fit simultaneously.**

Minimal amendment:
- objective strip uses compact semantic labels/icons plus short localized objective text;
- selected-detail card shows one rule at a time with wrapping;
- expanded full rule/reason history may use a non-destructive overlay;
- clock labels, footprint boundaries, NOW/DONE/LOCKED OUT and conflict indicators may never depend on opening that overlay.

No logic change.

---

# 9. Localization / pseudolocalization hostile pass

Stress strings:
- German/Russian expansion +40%;
- CJK fonts with larger glyph boxes;
- controller glyph + long objective;
- reason trace with object/site names;
- `ARRIVED — eligible next Resolve`;
- conflict line with two time labels.

Rules remain based on enums/time IDs, never localized strings, so semantics cannot drift at runtime.

## Reason trace volume
A late Resolve may affect multiple sites, two carriers and objectives. Phase 6 expects a 1–6 row strip, but hiding authoritative causal events would violate explainability.

**DEFECT FOUND D04: fixed six-row visible trace can be insufficient for a valid late Resolve.**

Minimal amendment:
- collapsed `What changed?` view may summarize/group to <=6 visible rows;
- full expanded trace contains every authoritative ReasonEvent for that Resolve;
- grouping cannot merge away a harmful LOCKED OUT event or carrier boundary;
- localized summary is presentation only; structured events remain complete.

Result: **PASS after repair.**

---

# 10. Save, demo import, corruption, offline/cloud, two-device divergence

## 10.1 Clean profile + corrupted current
Current fails checksum/validation; valid backup exists -> load backup and explain recovery.

**PASS.**

## 10.2 Current + backup both corrupt
Preserve evidence, offer new profile. Never overwrite corrupt files silently.

**PASS.**

## 10.3 Interrupted demo import
Original demo stays untouched; pre-import full backup retained; temp write validated before replacement.

**PASS.**

## 10.4 Offline progression
Device A completes Case 20 offline. Save revision increases locally.

When Steam later syncs, game-level logic must not pretend it can control every client conflict. If both candidate profiles become visible to the game:
- campaign completion merges monotonically;
- best records merge by better valid result;
- active checkpoint is not silently merged.

**PASS as a design policy; real Steam build validation remains mandatory.**

## 10.5 Two devices diverge
Device A active in Case 24, Device B active in Case 30. Both have unique valid progression.

Expected:
- union monotonic completion/records where safe;
- preserve divergent active checkpoints as recovery candidates;
- user chooses which active case/checkpoint to continue;
- choosing one does not delete the other immediately if recovery storage permits.

**PASS.**

## 10.6 Save manipulation expectation
A player may edit local files. Product is single-player premium; no anti-cheat is required. Invalid schema/content hashes are rejected safely. Achievements/records need not become an arms race against local tampering.

**PASS.**

---

# 11. Hostile gameplay behavior matrix

| Behavior | Expected result | Verdict |
|---|---|---|
| scan every legal socket | UI shows exact NOW coverage, not future milestone oracle | allowed, but content must resist trivial scanning |
| intentionally overlap different labels | illegal before commit; no move/beat cost | PASS |
| press Resolve repeatedly | deterministic; may consume beat; no hidden timer | PASS with D01 gate |
| Resolve with no changes | explicit no-change trace; legal | PASS |
| animation skip every time | identical state | PASS |
| 2x animation | identical state | PASS |
| Reduced Motion | identical state cues | PASS |
| Undo Turn repeatedly | exact checkpoint restoration | PASS |
| restart after fatal exposure | exact initial state | PASS |
| quit during animation | post-Resolve authority already known; reload canonical save | PASS after D02 |
| replay then quit | replay never mutates authority | PASS |
| brute-force final layouts | possible but should not dominate intended reasoning | Phase-10 target |
| use earlier-looking clock on BAKED item | item remains BAKED; no reverse visuals | PASS |
| exploit carrier arrival ordering | newly arrived cannot ACCEPT same Resolve | PASS |
| rely on frame rate/physics | no effect | PASS |

---

# 12. Content-count re-evaluation: 36 + 12

The paper simulation does **not** justify preserving 48 cases merely because earlier phases named them.

## Campaign 36
The six chapter roles are distinct enough to support 36 in principle:
- identity;
- footprint reasoning;
- handoff boundaries;
- simultaneity;
- earned-state preservation;
- synthesis.

However, Cases 25–36 are at greatest risk of becoming recombinations whose proof is “secure hazard, prepare cargo, reserve final two clocks.”

Decision:
**Keep 36 campaign as the authoring target, but freeze no quota.**
Phase 10 must audit proof-shape duplication across all planned slots. If six or more campaign slots collapse to the same causal partial order, cut to 30 rather than inventing new mechanics.

## Mastery 12
The listed M01–M12 include several themes likely to collapse into tighter budgets, misleading sockets or remixes of late campaign synthesis.

Paper evidence is insufficient to guarantee 12 genuinely new mastery proofs.

**Explicit Phase-9 scope amendment:**
- 8 mastery cases are the baseline content commitment for specification freeze;
- M09–M12 become **reserve slots**, promoted only if each demonstrates a materially distinct causal proof shape not already present in campaign/M01–M08;
- commercial wording remains “8–12 optional mastery cases” until empirical/content proof supports 12;
- no price increase/decrease is driven by mastery count alone.

This follows the existing Phase-5/7 cut policy and reduces filler risk without changing core identity.

---

# 13. Whole-game pacing result

### First 30 minutes
Strong identity formation: NOW vs DONE, local simultaneity, first irreversible consequence, first handoff.

### Hour 1–2
Footprints and move budgets become meaningful. Main risk is repeated process structures; Case 09-style authoring must vary causal order rather than building skin.

### Hour 2–4
Handoffs and coupled CURRENT events add a genuine second dimension: “when can this persistent object be staged?” versus “what must be true now?”

### Hour 4–6+
The system remains viable only if cases use different partial-order proofs. New timestamps, more sockets or harsher budgets are explicitly rejected as substitutes for new reasoning.

### Optional mastery
Should reward tighter understanding or alternate causal structures, not repeated campaign puzzles with smaller move limits.

Overall pacing verdict: **PASS WITH CONTENT-QUALITY CONDITIONS.**

---

# 14. Defect / contradiction ledger

| ID | Severity | Source | Finding | Minimal repair | Status |
|---|---|---|---|---|---|
| D01 | HIGH | Mechanics ordered process + Content | unchanged clock layout can farm consecutive useful process milestones through repeated Resolve | content/validator gate forbids strategically trivial repeated unchanged-layout advancement after tutorials unless explicitly meaningful | AMENDED |
| D02 | HIGH | UX pre-Resolve autosave vs Tech persistence | quit after Resolve could restore only pre-Resolve checkpoint if active post-state is not separately saved | save canonical post-Resolve active state after every successful Resolve; retain pre-Resolve undo checkpoint separately | AMENDED |
| D03 | MEDIUM | UX/Localization | late long localized rule prose cannot be assumed to fit permanently at 1280x800 with max text | compact core strip/card; expanded non-destructive detail overlay allowed; logic cues remain always visible | AMENDED |
| D04 | MEDIUM | UX reason trace | 1–6 visible rows can hide valid late authoritative events | <=6-row collapsed summary allowed; full expanded trace must expose every ReasonEvent | AMENDED |
| D05 | MEDIUM | Content/Commercial | 12 mastery cases not justified by paper uniqueness | baseline 8 mastery + 4 reserve slots promoted only by distinct-proof gate | AMENDED |
| D06 | MEDIUM | Content anti-enumeration | human-proof requirement does not explicitly require it to eliminate a meaningful action class | add causal-cut gate from Case 12, normally two cuts in Chapter 4+ | AMENDED |
| D07 | LOW | UX/Mechanics | no-placement Resolve legality was implied but not explicit in UX | keep Resolve legal without movement; show no-change trace when applicable | CLARIFIED |
| D08 | LOW | Case 30/solver reports | “materially different winning route” undefined | Phase 10 define by different milestone partial order/role structure, not symmetry-only path | OPEN FOR PHASE 10 |

No defect requires rewind, continuous time, hidden state, new semantic families, additional player verbs or production implementation.

---

# 15. Explicit Phase-9 amendments to earlier authority

These are narrow overrides required by the simulation.

## A1 — unchanged-layout repeated Resolve content gate
Overrides only permissive content interpretation of ORDERED PROCESS:
> After introductory teaching, a shipping case must not obtain multiple strategically useful consecutive process advances from repeated Resolve under an unchanged clock configuration unless repeated boundaries are themselves causally meaningful through another public interaction (carrier/accept/coupled requirement). Validator/content review flags such chains.

The kernel still allows no-placement Resolve.

## A2 — save checkpoint separation
Clarifies Phase 6 + Phase 8:
> Every successful Resolve produces a canonical post-Resolve active state that is autosaved/recoverable. The pre-Resolve Undo Turn checkpoint is stored separately. On load, resume post-Resolve authority; Undo Turn may restore the matching checkpoint.

## A3 — compact vs expanded UI
Clarifies Phase 6:
> At 1280x800, clock labels, footprints/conflicts, objective status and NOW/DONE/LOCKED OUT remain visible. Full long rule/reason prose may use a focused non-destructive overlay rather than remaining permanently expanded.

## A4 — complete reason trace
Clarifies Phase 6:
> Collapsed What Changed? may group into <=6 rows, but expanded trace must expose every authoritative ReasonEvent and may not omit harmful transitions or carrier boundaries.

## A5 — mastery count
Overrides “exactly 12” as shipping commitment:
> Baseline is 8 optional mastery cases. Four additional reserve mastery slots may ship only when they pass distinct causal-proof/variety gates. Product target is therefore 36 campaign + 8–12 mastery, with campaign itself still subject to the existing 36->30 quality cut.

## A6 — causal-cut anti-enumeration gate
Strengthens Phase 5:
> From Case 12 onward, each normal campaign case must have at least one public causal claim set that removes a meaningful class of legal early actions before experimentation. Chapter 4+ normally requires two independent cuts. Failing this is a content defect even if the solver proves solvability.

---

# 16. Phase-10 adversarial-review targets

Phase 10 must not merely restate these findings. It should attack them from independent angles.

1. **Fun / repetition attack:** classify every planned Case 07–36 and M01–M08(+reserve) by proof shape; identify duplicates and recommend exact cuts.
2. **Enumeration attack:** define measurable proxies for socket-scanning dominance, including action branching, dominant first-action concentration and proof-based pruning.
3. **No-op exploit attack:** fuzz repeated Resolve sequences and determine where unchanged-layout advancement creates accidental dominant strategies.
4. **Partial-order diversity:** formalize “materially different solution family” for Case 30/35/mastery and reject symmetry-only alternatives.
5. **Late-case complexity:** prove <=3 clocks/<=8 sites still supports depth without tiny visual distinctions or arbitrary move budgets.
6. **UX ambiguity:** hostile review NOW/DONE/LOCKED OUT, carrier arrival boundary, final CURRENT objectives and no-placement Resolve language.
7. **Controller/Deck:** attack focus graph, maximum text size, pseudolocalization and conflict preview at 1280x800.
8. **Accessibility:** verify animation skip/reduced motion/non-color cues preserve all causally relevant information.
9. **Persistence:** adversarial matrix for post-Resolve autosave + pre-Resolve undo checkpoint, corruption, import idempotency, unsupported future schema and divergent devices.
10. **Reason trace:** ensure every mutation is explainable without overflowing or suppressing harmful events.
11. **Commercial scope:** decide whether campaign stays 36 or cuts to 30; mastery freezes at 8 or promotes reserve cases only from proven uniqueness.
12. **Implementation ambiguity:** identify any remaining gameplay decision a fresh implementation agent would have to invent.
13. **Finale attack:** independently construct at least two Case-36 candidate proof structures and kill any that merely repeat Case 24/34.
14. **Authority consistency:** verify Phase-9 amendments A1–A6 are incorporated into the final freeze without silently rewriting historical files.

---

# 17. Phase result

Whole-game simulation finds LOCAL TIME mechanically coherent from first boot through late-game recovery/cloud behavior and hostile interaction.

The core design survives the most important question: **hour-5 play can remain causal reasoning rather than socket enumeration**, but this is not guaranteed by the kernel alone. It requires stronger authored causal-cut and repeated-Resolve gates.

Five substantive repairs were adopted:
- unchanged-layout process farming is now a content defect;
- post-Resolve active state and pre-Resolve undo checkpoint are saved separately;
- Deck UI may expand detailed prose without hiding core state;
- full reason trace cannot be truncated to six events;
- mastery baseline is reduced from 12 to 8, with four reserve slots only if distinct.

No production implementation was started.

**PHASE 9 WHOLE-GAME SIMULATION = COMPLETE.**

# NEXT DESIGN STEP — PHASE 10 ADVERSARIAL REVIEW
Create `GAME18_ADVERSARIAL_REVIEW.md`. Perform destructive review across fun/repetition, socket enumeration, dominant strategies, repeated Resolve/no-op, proof-shape duplication, scope, controller/Deck, accessibility, localization, persistence/import/cloud, reason-trace completeness and implementation ambiguity. Build a planned-case proof-shape matrix for Cases 07–36 and mastery baseline M01–M08 plus reserve M09–M12, identify exact cuts/repairs, and end with a freeze-readiness verdict and exact Phase-11 Specification Freeze requirements. Do not begin production implementation.
