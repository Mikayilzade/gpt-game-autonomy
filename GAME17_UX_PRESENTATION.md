# GAME #017 — THE QUEUE KNOWS — PHASE 6 UX / PRESENTATION ARCHITECTURE

Date: 2026-09-05
Status: PHASE 6 COMPLETE
Production implementation: NO
Authority: below `START_HERE.md`, `STATUS.md`, `GAME_INDEX.md`, `GAME17_PRODUCT_THESIS.md`, `GAME17_MECHANICS.md`, and `GAME17_CONTENT.md`.

## 0. UX mandate

The screen must read first as a **small public service hall**, second as an inspectable deduction instrument, and never as a spreadsheet or tycoon dashboard.

The UX must reinforce the product sentence: **change the system -> watch choices -> use those choices as evidence**.

Primary UX risks to defeat:
- player mistakes the game for throughput optimization;
- predicted-choice UI becomes an oracle that reveals hidden type;
- late cases become unreadable at 1280x800;
- controller focus becomes slower than mouse point-and-click;
- reason traces leak actual hidden truth;
- queue animation obscures the exact logical state in which evidence was created.

---

# 1. Current Steam Deck / controller constraints incorporated

Fresh Steamworks review on 2026-09-05 confirms the design should target:
- native 1280x800 support, with 1280x720 also safe;
- full access to all content through the default controller configuration;
- controller glyphs matching the active device rather than showing keyboard/mouse glyphs during controller play;
- readable UI at handheld distance: Steam's compatibility guidance sets 9px character height as an absolute minimum at 1280x800 and recommends aiming around 12px where possible;
- user-configurable text size and preferably contrast;
- no mandatory physical keyboard path; if text input is ever introduced, controller/onscreen-keyboard support is required.

Canonical product response:
- the game requires **no free text entry** for campaign play;
- 1280x800 is a first-class layout target, not a shrink-down of desktop UI;
- minimum shipped logical-text target is **12px apparent character height at 1280x800**, with no required information intentionally designed at the 9px review floor;
- text-scale presets are 100%, 115%, 130%, with layouts allowed to paginate/scroll rather than reduce type;
- input prompts are action-based and dynamically glyph-swapped;
- controller and mouse remain simultaneously usable; changing input does not alter logical focus state.

Research references:
- Steam Deck and Steam Machine Compatibility Review: https://partner.steamgames.com/doc/steamhardware/compat
- Getting your game ready for Steam Deck and Steam Machine: https://partner.steamgames.com/doc/steamhardware/recommendations

---

# 2. Hall composition and camera

## 2.1 Canonical camera
- fixed elevated three-quarter / shallow-isometric service-hall view;
- no free rotation;
- no first-person movement;
- no camera position is mechanically privileged;
- optional small pan/zoom is presentation-only and snaps back to canonical overview;
- controller shoulder focus can auto-frame the selected counter/customer without changing logical state.

## 2.2 Screen zones
At 16:10 1280x800:
1. **Hall field — center ~68–72% width.** Counters occupy upper third, queues extend toward lower center, arriving cohort staging area sits lower/side edge.
2. **Objective rail — upper-left compact card.** One sentence goal, hard constraints, intervention budget, cohort progress.
3. **Context inspector — right-side overlay/drawer.** Closed by default; opens for selected customer/counter/evidence/lever. It never permanently consumes hall width on handheld.
4. **Action strip — bottom.** Current phase, Resolve/Commit/Back glyphs, checkpoint/restart access, intervention budget.
5. **Evidence timeline — lower-left expandable tab.** New evidence creates a small numbered marker; full history opens as an overlay.

Desktop wider layouts may pin the inspector, but the 1280x800 canonical information hierarchy remains valid.

## 2.3 Counter landmarks
Each counter has simultaneously:
- stable letter/name (A/B/C);
- stable silhouette/sign shape;
- public fee marker;
- service-time/capacity marker;
- privacy/category marker when relevant;
- queue-slot rail;
- open/closed state.

Counter identity may use color, but never color alone.

## 2.4 Customer representation
Every relevant customer is a distinct readable token/character with:
- stable ID/name badge on focus;
- current queue slot/location;
- compact candidate-count badge when not focused;
- candidate chips only on focus/inspector, not permanently above every head;
- small evidence-dot count if prior observations exist.

Late 10-customer cases use fixed queue slots and staged cohort trays; characters never overlap into a visually ambiguous crowd.

---

# 3. Information hierarchy

The player should answer these questions without opening more than one secondary panel:
1. What am I trying to prove/do?
2. Which customers are relevant now?
3. What can I change before the next cohort?
4. What are the current public counter properties and queue lengths?
5. What did this customer choose, and what candidates did that choice eliminate?

## 3.1 Objective rail
Always visible:
- objective verb: IDENTIFY / EXCLUDE / SEPARATE / SERVICE / HYBRID;
- named targets;
- world quantifier when relevant, rendered in plain language such as `Must be safe in every remaining possibility`;
- hard wait/service ceiling;
- interventions remaining;
- cohort X/Y.

No score, money, customer-happiness meter, stars-for-speed, or throughput KPI appears in the primary HUD.

## 3.2 Counter quick card
Focus/hover shows:
- fee;
- predicted service-time preset and capacity;
- walk cost when relevant to selected customer;
- privacy/exposure state when relevant;
- waiting/in-service counts;
- exact current predicted completion **for the selected hypothetical customer/type query only when that query is public and type-specific**, never a hidden actual-customer prediction.

## 3.3 Customer inspector
Contains:
- visible initial/current candidate chips;
- public attributes needed by candidates, e.g. familiar counter and Routine threshold;
- current status/location;
- chronological evidence cards;
- player notes/marks;
- proven type only when candidate set is singleton or after allowed terminal reveal.

Actual hidden type has no reserved visual slot, silhouette, ordering, animation, voice, or portrait cue before proof.

---

# 4. Candidate chips and type language

Five canonical chips use icon + word + shape pattern:
- Price — coin/tag icon;
- Urgent — clock/bolt icon;
- Routine — repeat/home-route icon;
- Privacy — shield/curtain icon;
- Convenience — footsteps/shortcut icon.

Color is redundant emphasis only.

Chip states:
- **possible**: normal solid outline;
- **eliminated now**: strike/fade plus contradiction marker;
- **previously eliminated**: muted but inspectable in history;
- **proven**: singleton with `PROVEN` text, not merely green color;
- **player note**: pencil corner mark, visually distinct from mechanically eliminated.

Manual player notes can never remove a candidate from the mechanical candidate set. They are private annotations and may be wrong.

---

# 5. Evidence and reason-trace UX

## 5.1 New choice beat
When a customer chooses:
1. logical choice is already resolved;
2. character moves to chosen fixed slot;
3. a short evidence pulse appears on that customer;
4. any mechanically eliminated candidate chips animate out/strike;
5. concise fact line appears, e.g. `Chose A while B would finish 2 ticks sooner`;
6. player may open the evidence card for exact snapshot.

## 5.2 Evidence card
Stores and displays:
- event/tick/cohort;
- chosen counter;
- miniature frozen pre-choice hall snapshot or exact compact state table for A/B/C;
- public comparisons relevant to eliminated candidates;
- each eliminated type and exact contradiction;
- surviving candidate chips.

Example:
`Urgent eliminated: at this moment B completed in 2 ticks and A in 4; Urgent would choose B, but C3 chose A.`

This is evaluator-derived, not authored prose.

## 5.3 Anti-leak rule
Before proof, reason traces may explain **why a candidate is impossible**, not why the actual hidden type acted.

Forbidden pre-proof:
- `C3 chose A because C3 is Price`;
- highlighting the comparator used by the actual hidden type when multiple candidates survive;
- voice/animation variants by hidden type;
- sorting candidate chips so actual type is consistently first;
- showing a “confidence” score derived from actual truth.

Allowed:
- facts common to all observers;
- counterfactual evaluation of a player-selected candidate type;
- contradiction explanations;
- `Type proven: X` once evidence mechanically leaves singleton X.

---

# 6. Prediction / planning without an oracle

The player may ask public counterfactual questions but may never preview the actual hidden choice.

## 6.1 Type Lens
Selecting a candidate chip enters **Type Lens** for that hypothetical type. The hall overlays how **that rule model** evaluates public counters:
- Price: fee ordering;
- Urgent: predicted completion ordering;
- Routine: familiar counter disadvantage vs threshold;
- Privacy: exposure state;
- Convenience: walk cost ordering.

The header must say `IF THIS CUSTOMER WERE URGENT...`.

The lens can show the deterministic counter that this hypothetical type would choose because that is computable public information.

## 6.2 Multi-candidate comparison
For a selected customer, player can compare candidate outcomes in a small matrix:
`Price -> A | Urgent -> B | Routine -> A`.

This is permitted because it is simply executing every visible candidate model on public state. It does **not** say which row is true.

## 6.3 Forbidden preview
There is no generic `Where will C3 go?` button before Resolve. A customer with candidates {Price,Urgent} can only be previewed as separate explicit counterfactual rows.

No preview may use future congestion from hidden earlier customers in the same unresolved cohort. For sequential arrivals, a Type Lens may evaluate only the **current public state**; it cannot simulate the actual hidden choices of customers who have not yet resolved.

This preserves the central information problem.

---

# 7. Intervention planning UX

Interventions are physical props attached to counters, not abstract settings pages.

Flow:
1. focus a glowing legal lever/sign;
2. Select opens its finite authored values;
3. left/right or stick cycles values; mouse clicks exact value;
4. hall public metrics update as a **draft**;
5. draft changes are marked with striped/outlined `PLANNED` treatment;
6. budget preview shows cost;
7. player can freely revert drafts;
8. `Apply setup` commits the draft intervention set for this window;
9. `Resolve cohort` is a separate deliberate action.

A draft may update public counterfactual Type Lens results, because those are derived from visible proposed state. It may not preview actual hidden choices.

When a lever resets each cohort, its prop carries `RESETS AFTER COHORT` text/icon in both hall and inspector.

---

# 8. Mouse, controller and Steam Deck navigation

## 8.1 Action abstraction
Bindings are semantic actions, not hard-coded keys:
- Navigate Hall
- Next Focus Group
- Previous Focus Group
- Inspect / Select
- Back
- Cycle Value Left / Right
- Type Lens
- Evidence History
- Objective
- Resolve / Advance
- Commit
- Pause
- Fast Forward

All are remappable.

## 8.2 Controller focus groups
Canonical groups:
1. COUNTERS / LEVERS
2. CUSTOMERS
3. OBJECTIVE
4. EVIDENCE
5. PRIMARY ACTION

Shoulder buttons cycle groups. D-pad/stick moves within a group by stable spatial order. Focus never disappears when panels close; it returns to the originating object.

Recommended default:
- left stick/D-pad: spatial navigation;
- A/South: inspect/select;
- B/East: back;
- LB/RB: previous/next focus group;
- X/West: Type Lens / candidate comparison when customer selected;
- Y/North: objective/evidence contextual shortcut;
- triggers: previous/next evidence event when history is open;
- Menu: pause;
- Resolve and Commit use context actions in bottom strip and require explicit press, never a timing hold.

Exact platform glyphs are dynamic.

## 8.3 Mouse
Mouse hover provides focus only; clicking changes active focus. Scroll may zoom the hall or scroll a panel depending on pointer location. Mouse movement alone must not switch the whole UI into keyboard/mouse prompt mode; a meaningful mouse click does. Controller input immediately restores controller glyphs without losing selection.

## 8.4 Touch/trackpad
Optional pointer convenience only. No content requires touch, trackpad precision, drag-and-drop, or hover.

---

# 9. Resolve / Observe presentation contract

Simulation resolves first; presentation replays its event log.

## 9.1 Normal speed
Per arriving customer target presentation beat: ~0.35–0.8 sec depending on distance/animation, with evidence update immediately legible after slot arrival.

A five-customer cohort should not force 10+ seconds of unskippable waiting.

## 9.2 Fast-forward
Holding/toggling Fast Forward accelerates or collapses movement while preserving ordered evidence pulses. At maximum speed, characters snap between fixed slots and evidence markers still appear in event order.

## 9.3 Skip
After player has seen the mechanic once, Resolve can skip directly to final logical positions. A compact `5 choices resolved` stack appears; player can step evidence event-by-event afterward.

## 9.4 Replay
Replay Observation reads immutable event history only. It cannot change state, budget, candidate sets, RNG, checkpoints or save data. Replay may be scrubbed by event, not by continuous simulation time.

## 9.5 Reduced motion
Reduced Motion replaces walking interpolation with short fades/slides between fixed slots, removes camera pans and nonessential pulses, but keeps ordering and state-change indicators.

---

# 10. First-session onboarding: QK01–QK06

## Boot -> title
- no launcher required by product UX;
- Continue appears only after a save exists;
- New Game, Demo/Campaign as appropriate, Settings, Accessibility, Quit;
- controller works immediately without configuration.

## QK01 — teach self-selection, not management
Opening brief: `Goal: identify which rule each customer follows.`
The game explicitly says: `You are not scored for serving faster. Change the hall so different rules produce different choices.`

Sequence:
1. objective rail highlights IDENTIFY;
2. inspect one customer: Price + Routine chips;
3. inspect Price and Routine rule cards;
4. focus B's fee sign;
5. set B FREE;
6. before Resolve, Type Lens explicitly shows `IF PRICE -> B`, `IF ROUTINE -> A` for one customer;
7. Resolve;
8. evidence chips eliminate candidates;
9. Commit when all three are proven.

The first success screen emphasizes `Your sign created the evidence` rather than `Customers served`.

## QK02 — teach active experiment
Baseline Type Lens shows Urgent and Routine both choose A. Objective callout: `Watching this setup cannot distinguish them.`
Player changes A service preset to 3 ticks. Candidate comparison now visibly splits the hypothetical outcomes. Resolve proves the type.

Teaching line: `When candidates act the same, change the test.`

## QK03 — teach congestion confound
Before Resolve, tutorial warns only: `Later customers see the queues created by earlier customers.` It does not reveal outcomes.
After C5 chooses the apparently Price-attractive free counter, evidence review freezes C5's exact pre-choice snapshot and shows why Urgent remains possible.
Teaching line: `Final position is not enough. Evidence belongs to the moment of choice.`

## QK04 — teach sequential policy
After cohort 1, game automatically lands at checkpoint and opens `What changed?` summary: queue state + evidence, no recommended action.
Second intervention window highlights that current state is different from start. Player chooses based on evidence.
Teaching line: `Observe first. Design the next test from what you learned.`

## QK05 — teach partial proof
Objective rail uses explicit wording: `Separate Privacy customers. You do NOT need to identify everyone.`
On success, ambiguous non-target chips remain visibly unresolved and are stamped `Not needed for this proof`.

## QK06 — demo synthesis
Tutorial popups stop. Only established HUD, objective and contextual help remain.
Three counters, two cohorts, hard wait ceiling and two interventions force the player to combine Type Lens, evidence snapshots and contingent planning.
End-of-demo summary asks no quiz; it shows the causal chain:
`Changed hall -> choices diverged -> evidence narrowed possibilities -> second setup used that evidence -> proof complete.`

No management score is shown.

---

# 11. Failure, dead-state and recovery UX

## 11.1 Constraint failure
Freeze at exact logical boundary. Show:
- failed predicate in plain language;
- violating customer/counter;
- exact event/tick;
- `Reload checkpoint` primary;
- `Restart case` secondary;
- `Review evidence` available.

Example: `Wait limit exceeded: C6 began service at tick 6 after arriving at tick 1. Limit: 4.`

## 11.2 Diagnosis failure
After irreversible Commit:
- mark submitted wrong claim;
- reveal actual truth as permitted by mechanics;
- show shortest evaluator/evidence contradiction;
- offer checkpoint/restart.

No vague `Wrong!` screen.

## 11.3 Certified information dead state
Only appears with solver certificate. Wording distinguishes it from ordinary uncertainty:
`No remaining legal setup can distinguish C2's Urgent and Routine possibilities before Commit.`
Actions:
- Reload latest checkpoint;
- Restart case;
- Review the branch that consumed the last separating option.

Never auto-label a state dead because no candidate changed recently.

## 11.4 Restart/checkpoint
- Restart Case always available from pause and failure;
- checkpoint reload states exact cohort/intervention boundary being restored;
- no post-observation undo that preserves knowledge in canonical state;
- loading a checkpoint restores the exact hidden world and evidence branch.

---

# 12. Hint system

Hints teach reasoning premises, not answers. No consumable currency and no score punishment.

Three optional tiers:

**H1 — Goal focus**
Restates what must be proven and which ambiguity matters.
Example: `You only need to distinguish Urgent from Routine for C2.`

**H2 — Comparison prompt**
Points to a public quantity/rule to compare, without naming an action.
Example: `Compare how much slower Routine will tolerate at its familiar counter.`

**H3 — Counterfactual question**
Names a useful test condition or asks the player to construct one, but still does not reveal hidden type or actual future choice.
Example: `Can you make A exactly 2 ticks slower than B? Compare what Urgent and Routine would do there.`

H3 may effectively expose a strong experiment in tutorial content, but never says which hidden candidate is true. Mastery cases may stop at H2 by design, disclosed before launch.

---

# 13. Accessibility

Required baseline:
- full input remapping;
- keyboard/mouse and controller parity;
- dynamic device glyphs;
- text scale 100/115/130%;
- high-contrast UI option;
- all type/counter/evidence states encoded by text/icon/shape as well as color;
- color-vision-safe palette testing, but never color-only logic;
- reduced motion;
- screen shake off by default / none required;
- animation speed Normal/Fast/Instant;
- subtitle/text presentation for every gameplay-relevant audio cue;
- gameplay fully completable with audio muted;
- no timed input requirements;
- no hold requirement for essential actions; hold/toggle choices for fast-forward where relevant;
- separate UI/SFX/music volume;
- pause at any player-controlled phase;
- tutorial replay/reference rulebook;
- focus indicator with high-contrast outline and optional enlarged focus ring.

Localization readiness:
- no logic depends on English wordplay;
- type icons always accompanied by localized labels in inspectors;
- panels allow text expansion/wrapping;
- no fixed-width sentence baked into art.

---

# 14. 1280x800 and 10-customer stress layout

Acceptance target at 1280x800 / 100% text scale:
- three counter landmarks and all occupied queue slots visible in overview;
- objective one-line summary + intervention budget + cohort progress visible;
- no more than one detail drawer open;
- 10 customers represented without overlapping hit/focus regions;
- selected customer remains visually traceable to queue slot while inspector is open;
- candidate chips use 2-column wrapping in inspector rather than shrinking text;
- evidence timeline collapses to numbered markers, not full prose cards;
- action strip uses glyph + short localized action name;
- minimum required text target 12px apparent character height; never intentionally below Steam's 9px compatibility floor;
- at 130% text scale, inspector and evidence history may scroll vertically; hall geometry does not shrink below readable counter/customer silhouettes.

For late 10-customer cases, customers not yet admitted live in cohort trays labeled `NEXT 1/2/3`, preventing all future customers from occupying the hall simultaneously. The 10-visible ceiling remains an absolute stress case, not the default composition.

---

# 15. Pause, settings, save and resume

## Pause
Available during Inspect/Intervene/Observe and after Resolve event playback; if pressed during presentation, animation pauses but logical state is already resolved.

Pause menu:
- Resume;
- Restart from Checkpoint;
- Restart Case;
- Rulebook;
- Settings;
- Return to Case Select;
- Quit to Title.

Destructive restart requires confirmation only when it would discard post-checkpoint progress. Confirmation is a simple Yes/No controller-safe dialog.

## Save
Autosave at:
- case start;
- every canonical checkpoint at start of an Intervene phase;
- case completion;
- settings changes separately.

Save data never needs to serialize animation progress as authoritative gameplay state. Resume restores canonical logical state, then reconstructs presentation.

## Resume
Continue card shows:
- case ID/name;
- chapter;
- checkpoint/cohort;
- objective summary.

If game closed during Resolve animation, resume loads the already-resolved canonical state at the nearest saved checkpoint policy defined in technical spec; it must never reroll or re-resolve hidden behavior.

---

# 16. Detailed UX walkthroughs

## QK01
Player sees three customers staged and two counters. Objective says IDENTIFY, not serve. Focus tutorial opens C1: Price/Routine. Type Lens on current equal-fee hall demonstrates both public models. Fee sign B glows as the only intervention. Setting FREE changes hypothetical rows: Price -> B; Routine -> A. Resolve animates B/A/B. Each evidence pulse strikes one candidate. Commit becomes enabled only when proof predicate is satisfied. Success card: `One sign created three useful observations.`

## QK03
Five arrivals resolve in authored order. Evidence timeline numbers 1–5. Final hall can misleadingly place C5 at free A. Selecting C5 opens event #5 snapshot, not current final queue state. Urgent remains because A/B completion was tied at that exact choice. The UX explicitly labels snapshot `STATE WHEN C5 CHOSE`, preventing current-state contamination.

## QK04
After cohort1, a checkpoint banner briefly says `Observation saved — next setup can depend on this evidence.` The evidence summary groups customers by what was eliminated, then closes automatically. No action is recommended. Player can Type-Lens late customers against the **current** residual queues and choose the second intervention. Returning to checkpoint restores exact evidence and hidden world.

## QK05
Objective panel uses target badge Privacy and `Full identification not required`. When service separation is guaranteed across all remaining worlds, Commit enables even if non-target customers retain multiple chips. Success screen leaves those chips unresolved and explains: `Every remaining possibility satisfies the target separation.`

## QK06
Three-counter overview preserves A/B/C landmarks. Objective rail shows two simultaneous predicates: target proof and Wait <=4. The wait constraint uses a small clock badge on at-risk public states but never predicts hidden future choices. After cohort1, player reviews evidence and current queues, drafts one of the legal second presets, and can inspect hypothetical candidate-rule comparisons only from current public state. Commit/success summarizes both information proof and service constraint.

---

# 17. Anti-oracle acceptance rules

A UI feature is rejected if it does any of the following before legitimate proof/reveal:
1. evaluates the actual hidden type for the player;
2. previews an unresolved customer's actual destination;
3. simulates future actual cohort congestion using hidden choices;
4. exposes hidden type through portrait, animation, voice, sorting, tooltip, focus order or telemetry-derived hint;
5. recommends a mechanically winning intervention from solver knowledge;
6. marks a player note as mechanically true;
7. displays candidate likelihood/probability when the system is exact set elimination;
8. uses current queue state to rewrite the reason for an old evidence event;
9. declares a dead state without exhaustive certificate;
10. makes Commit availability itself leak hidden truth beyond the public proof predicate.

Commit enablement is based only on public evidence/proof requirements, not whether the submitted claim secretly matches actual world.

---

# 18. UX empirical gates for implementation/playtest

These are test obligations, not design gaps:
1. By end QK02, >=80% of observed first-time testers should describe the goal in information/deduction terms rather than queue-speed terms.
2. At 1280x800, testers must correctly identify selected customer, its queue, counter properties and objective without zooming OS-level display.
3. Controller-only QK01–QK06 completion should require no pointer emulation.
4. No tester should infer actual type from reason-trace wording before evidence proves it.
5. In QK03, testers should be able to recover C5's pre-choice state from evidence history after final queues have changed.
6. 10-customer stress case must remain navigable at 130% text scale; scrolling inspector is acceptable, overlapping focus targets are not.
7. Instant/reduced-motion presentation must produce identical logical/evidence result to normal animation.

Failure repair order: simplify information hierarchy -> improve labels/focus -> reduce simultaneous visible density -> adjust content composition. Do not add hidden automation or convert the game into management UI.

---

# 19. Phase-6 acceptance result

Phase 6 now fixes:
- Deck/controller constraints and 1280x800 readability target;
- fixed hall camera and screen zones;
- counter/customer visual identity;
- objective/counter/customer information hierarchy;
- candidate chips and evidence snapshot language;
- exact anti-leak reason traces;
- Type Lens counterfactual planning without oracle behavior;
- intervention drafting/commit flow;
- controller/mouse/Deck navigation;
- Resolve/Fast/Instant/Replay semantics;
- QK01–QK06 onboarding and synthesis UX;
- failure/dead-state/checkpoint recovery;
- three-tier non-answer hint model;
- accessibility/localization requirements;
- 10-customer handheld stress layout;
- pause/save/resume behavior;
- anti-oracle acceptance rules;
- empirical UX gates.

**PHASE 6 UX / PRESENTATION ARCHITECTURE = COMPLETE.**

No production implementation has begun.

# NEXT DESIGN STEP — PHASE 7 COMMERCIAL MODEL

Perform fresh market research and lock:
1. premium MSRP / launch-discount range against current comparable puzzle/deduction indies;
2. target first-completion and completionist length assumptions consistent with 36+12 content;
3. free demo strategy and exact QK01–QK06 boundary;
4. progression/unlock retention without grind, daily chores or live service;
5. achievement philosophy and candidate achievement families;
6. difficulty/accessibility relationship and whether optional challenge modifiers belong in scope;
7. replay incentives, if any, without procedural-content promise;
8. Steam platform features worth supporting (cloud, achievements, controller/Deck, demo save carryover if appropriate);
9. monetization boundaries and DLC/expansion policy;
10. commercial positioning/capsule/trailer proof beats and major market risks;
11. wishlist/demo conversion hypotheses as empirical gates, not fabricated forecasts.

Save canonical `GAME17_COMMERCIAL.md`, update `STATUS.md` and `GAME_INDEX.md`, then advance to Phase 8 if complete.