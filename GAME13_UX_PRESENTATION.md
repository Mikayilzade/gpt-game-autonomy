# GAME #013 — PHASE 6 UX & PRESENTATION ARCHITECTURE

Date: 2026-09-02
Status: PHASE 6 COMPLETE — CONTROLLER/HANDHELD READABILITY PASS
Selected concept: **SEAL BREAK** (working title)
Authority: Phase-4 mechanics remain authoritative for simulation; Phase-5 remains authoritative for content. This file freezes player-facing interaction, presentation, onboarding, accessibility and the inspection/oracle boundary.

## 1. Phase-6 verdict
Seal Break can remain readable on desktop, controller and handheld without live solver assistance. The interaction model therefore does **not** require a mechanical repair before Phase 7.

The decisive UX choice is to avoid showing cabinet geometry, history construction and evidence as three equally dense permanent panes. The canonical gameplay screen uses one persistent work object plus two switchable structured rails:
- **Workbench**: cabinet/object, seams, sockets and installed witnesses;
- **Plan rail**: opening history construction/selection;
- **Evidence rail**: target facts before commit, observed facts/timeline after commit.

On wide displays the active rail may coexist beside the Workbench. On handheld/narrow layouts the active rail becomes a bottom/side drawer occupying at most roughly 40% of usable area and can be collapsed with one input. No puzzle requires simultaneous pixel-level comparison of all three surfaces.

## 2. Current-platform evidence informing the freeze
Fresh platform/accessibility references checked 2026-09-02:
- Steamworks' current Deck/Machine recommendations require the default controller configuration to expose all game functionality for Verified status and recommend native gamepad/Steam Input support. Seal Break therefore treats controller as a first-class path, not mouse emulation.
- Current Xbox Accessibility Guidelines recommend at least 4.5:1 contrast for standard gameplay-important text/visual elements and 3:1 for large elements; they also explicitly warn against color-only communication.
- Current Xbox text guidance recommends text/icon scaling up to 200% without loss of content/function/meaning. Seal Break adopts reflow rather than shrinking text when scaling.
- Current Microsoft accessibility metadata guidance expects complete keyboard playability and digital/analog UI navigation. Seal Break therefore has keyboard-only and controller-only acceptance paths.

These are design targets, not claims of future certification.

## 3. Canonical gameplay information architecture

### 3.1 Persistent top strip
Always available while solving:
- case title + short case ID;
- one-sentence objective, e.g. `Install exactly 3 seals and arrange all 4 openings.`;
- placement budget `2 / 3 installed` when player placement exists;
- history requirement `4 of 4 openings` or `Open exactly 4 of 5`;
- active mode label: `EDIT`, `REVEAL`, `REPLAY`;
- pause/settings/help access.

Do not show scores, timers, stars or hint currency in Phase 6.

### 3.2 Workbench
The cabinet/object occupies the largest region. Every participating compartment has:
- short stable label visible without hover;
- focus outline independent of color;
- explicit seam drawing;
- sockets drawn as finite anchors rather than freeform placement regions.

Every enabled socket has:
- short identity label/icon;
- a patterned socket marker;
- visible connection to all seams it covers;
- installed/intact/broken state conveyed by shape + pattern + label/state icon, never hue alone.

Focused socket inspection may emphasize its covered seams and dim unrelated seams. Focused compartment inspection may emphasize its traversed seams. This is static authored geometry and is legal preview.

### 3.3 Plan rail
The Plan rail owns opening history and fixed input constraints. It never predicts tear results.

Each history card contains:
- compartment label/icon;
- authored constraint badges such as `required`, `cannot open`, `fixed #3`, or `before D`;
- explicit ordinal slot when ordered.

A compact summary remains visible when rail is collapsed, e.g. `A > C > D > B` or `4/5 chosen`.

### 3.4 Evidence rail
Before commit, this rail displays **target evidence only**. After/during commit it can switch between `TARGET` and `OBSERVED`.

Each evidence card contains:
- witness/compartment identity;
- predicate icon;
- plain-language phrase;
- checkpoint marker where relevant.

Target and observed facts must never be merged into a single ambiguous card. During mismatch inspection, pair them as `TARGET` / `OBSERVED` rows.

### 3.5 Bottom action strip
Contextual actions only:
- Inspect / Select;
- Place or Remove;
- Plan / Evidence rail toggle;
- Undo / Redo while editing;
- Commit when legal;
- Replay / Return to Edit after commit.

Disabled actions state the structural reason on focus, e.g. `Install 1 more seal` or `History needs 4 openings`. These legality messages may identify missing input but may not judge whether the chosen input will solve the case.

## 4. Focus and controller navigation

### 4.1 Focus groups
Three explicit groups:
1. Workbench;
2. Plan rail;
3. Evidence rail.

Shoulder buttons or equivalent `Previous/Next Panel` actions cycle groups. The currently focused group has a strong perimeter/focus heading indicator.

### 4.2 Workbench navigation
D-pad/left stick moves between authored neighboring focus nodes, not screen-space cursor pixels. Neighbor graph is generated from presentation anchors then author-reviewable. If geometry is irregular, author data may override neighbors.

Selection rules:
- A / primary action: inspect/select socket or compartment;
- secondary/context action on an empty legal socket: place seal if placement is editable;
- same action on installed socket: remove seal;
- no drag required.

Mouse:
- hover may preview the same static focus highlight but no information unique to hover;
- click selects;
- click action button or double-click optional convenience may place/remove;
- drag is optional convenience only.

Keyboard:
- arrows/WASD navigate focus graph;
- Enter/Space primary;
- remappable panel/action shortcuts;
- full game playable without mouse.

### 4.3 Focus restoration
Opening/closing a rail, help overlay, pause, replay scrubber or mismatch detail must restore focus to the exact originating semantic object when it still exists. If not, restore to nearest object in same group; only then use group default.

No modal may dump controller focus invisibly to the top-left/default button.

## 5. Seal placement/removal transactions
Placement cases use direct socket occupancy:
1. focus empty socket;
2. primary/context action installs one seal immediately as one edit transaction;
3. focus installed socket;
4. remove action removes it as one transaction.

Optional `Move Seal` convenience may select an installed socket as source then an empty socket as destination, but the completed move is **one** undo transaction. Cancel restores source unchanged.

When exact-K budget is full, empty sockets remain inspectable but placement action is disabled with `Seal limit reached`; the UI never recommends which existing seal to remove.

Fixed seals have a lock badge and cannot be removed.

## 6. History-control UX

### 6.1 FIXED_HISTORY
Cards appear already ordered and locked. Player can focus every card and inspect the corresponding compartment/seams. No reorder handles appear.

### 6.2 CHOOSE_FROM_AUTHORED_HISTORIES
Show a small vertical/list carousel of named neutral options such as `Plan A`, `Plan B`, `Plan C`, each rendering the full compartment order as cards. Selecting one is one edit transaction. Do **not** show predicted tear signatures beside options.

### 6.3 ARRANGE_REQUIRED_SET
All required compartment cards start in the sequence rail. Reorder uses discrete operations:
- focus card;
- enter `MOVE` mode;
- left/right or up/down changes ordinal slot;
- confirm ends move as one undo transaction;
- cancel restores prior position.

Optional mouse drag maps to the same transaction. Ordinal numbers update live because they are player input structure, not simulation output.

### 6.4 ARRANGE_BOUNDED_SUBSET
Use two explicit zones:
- `OPEN` sequence slots, with exact count shown;
- `LEFT CLOSED` pool.

Moving a card between zones is deliberate and discrete. If exact length is 4 of 5, the interface literally states `Open 4 / Leave 1 closed` and reserves four numbered sequence slots. This prevents omission reasoning from becoming a hidden UX rule.

A card in `LEFT CLOSED` is not given any tear/survival forecast.

### 6.5 Fixed positions and precedence constraints
Fixed-position card has a lock + ordinal. Precedence constraints appear as a small neutral rule chip above Plan rail, e.g. `A before D`, with both label and directional icon. Illegal reorder positions are blocked structurally; the UI may say `A must stay before D`. This is authored input legality, not a solver hint.

## 7. Evidence-card grammar
Every predicate has redundant icon + words. Witness identity is pattern/icon/short label.

Canonical phrases:
- `BREAKS_AT(S,3)` -> `S breaks at 3` + broken-strip icon over checkpoint `3`;
- `BREAKS_BEFORE(S,3)` -> `S breaks before 3` + left-arrow/time icon;
- `BREAKS_AFTER(S,3)` -> `S survives 3, breaks later` + intact-then-break icon;
- `INTACT_THROUGH(S,3)` -> `S intact through 3` + intact shield/strip through checkpoint;
- `FINAL_INTACT(S)` -> `S remains intact`;
- `FINAL_BROKEN(S)` -> `S is broken by the end`;
- `SAME_BREAK_STEP(S,T)` -> `S and T break together` + paired equal-step icon;
- `BREAKS_EARLIER(S,T)` -> `S breaks before T`;
- `OPENED(A)` -> `A is opened`;
- `UNOPENED(A)` -> `A stays closed`;
- `OPENS_AT(A,3)` -> `A opens at 3`;
- install predicates -> `S installed` / `S not installed`.

Never encode `before/after/together` only by spatial position or color. Exact checkpoint numbers remain textual.

Evidence density rule: handheld default shows one-line cards and allows a focused card to expand its explanation. If more cards exist than fit, rail scrolls; the Workbench never shrinks below its readability floor merely to expose all evidence simultaneously.

## 8. Allowed inspection vs forbidden oracle

### 8.1 Allowed before commit
The player may always inspect:
- compartment -> traversed seams;
- socket -> covered seams;
- derived trigger compartments for a socket, expressed neutrally as `Opening A, C, or D can tear this seal`;
- fixed/required/forbidden history constraints;
- current tentative installed set;
- current tentative history/order;
- authored target evidence;
- case rules already taught.

Allowed highlighting may isolate these static relations and cross-highlight the same authored relation between Workbench and cards.

### 8.2 Forbidden before commit
The UI must not:
- show predicted break checkpoint for current tentative setup;
- mark a target evidence card green/red based on tentative edits;
- simulate a future tear on hover;
- rank sockets/histories by closeness;
- state that an edit is logically wrong when it is mechanically legal;
- reveal which witness/step should change;
- preview final broken/intact state caused by the current plan;
- expose number of target predicates currently satisfiable;
- auto-complete a deduction.

The line is simple: **input legality and immutable geometry may be explained live; consequences of the player's hypothetical future commit may not.**

## 9. Commit -> reveal -> mismatch/success flow

### 9.1 Commit gate
Commit enabled iff structural legality passes. Pressing Commit:
1. captures immutable submission snapshot;
2. changes mode to REVEAL;
3. locks edit controls;
4. puts focus on reveal controls, preserving last edit focus for later return.

No `Are you sure?` dialog in ordinary play; commit is non-destructive to edit state.

### 9.2 Checkpoint reveal
For each checkpoint:
1. Plan rail highlights current opening card;
2. corresponding compartment opens;
3. traversed seams pulse/emphasize;
4. every seal broken at that checkpoint tears within one presentation beat;
5. checkpoint marker is added to observed timeline;
6. observed evidence state becomes inspectable;
7. continue automatically or under `Next Step`, according to player setting.

When multiple seals break at one checkpoint, their tear animations may stagger for readability but share one clearly persistent checkpoint badge. No ordinal tear numbers appear among them.

### 9.3 Speed and skip
Settings: `Step`, `1x`, `2x`, `Instant` presentation. Hold/press Skip may finish the current committed simulation immediately and materialize authoritative final trace. Skipping cannot alter result.

Reduced-motion mode replaces cabinet motion/tear flourish with short state transitions and checkpoint flashes.

### 9.4 Success
After final evaluation:
- clear `CASE SOLVED` state;
- concise target-vs-observed confirmation;
- `Review Replay`, `Continue`, `Case Select`.

Do not force immediate advance; a player may inspect the successful causal trace.

### 9.5 Mismatch
Mismatch is retrospective, not predictive. After committed evidence exists, the game may state exact causal differences such as:
- `Target: S intact through 3. Observed: S broke at 2 when C opened.`
- `Target: S and T break together. Observed: S broke at 1; T broke at 3.`
- `Target: A stays closed. Observed: A opened at 4.`

It may highlight the already-observed opening and traversed seam that physically caused a tear. It must not add `therefore move S to socket X`, `swap steps 2 and 3`, or any next-action recommendation.

Mismatch summary defaults to the first failed target in authored card order, with `Next mismatch` navigation. It does not calculate a closeness score.

### 9.6 Replay and scrub
After a run, timeline scrubber may inspect checkpoint 0..N of the **committed trace only**. Scrubbing restores historical visual state and observed facts at that checkpoint. It cannot edit history.

`Replay` restarts the same committed snapshot. `Return to Edit` restores the exact tentative submission that produced it and semantic focus returns to the last edited/focused object.

## 10. Onboarding / first-session path
Onboarding uses progressive disclosure and Phase-5 dependencies.

### SB_01 — direct cause
Teach focus, socket inspection, seam relation, Commit, one tear, replay. The game explicitly says a seal tears when an opening traverses a seam it covers.

### SB_02 — first crossing
Teach that a seal spanning multiple qualifying seams records the **first** qualifying opening. Replay/scrub introduced.

### SB_03 — same checkpoint atomicity
Two seals tear from one opening. Explicit microcopy: `They broke at the same checkpoint. Animation order does not matter.` This message appears once and remains in Help.

### SB_04 — authored history choice
Introduce Plan rail and selecting among finite histories. No free reorder yet.

### SB_06 — witness comparison
Introduce paired evidence grammar (`together`, `before`) and cross-highlighting between evidence witness and socket.

### SB_11 — omission
Introduce `OPEN` vs `LEFT CLOSED` bounded-subset layout and final-intact evidence.

### SB_16 — placement
Introduce editable sockets and exact-K budget under fixed history.

### SB_17 — demo placement beat
Reinforce that equal final broken state can hide different break times.

### SB_21 onward
Introduce full arrangement; only late cases expose placement + history simultaneously.

Tutorial principle: never introduce a new input grammar and a new logical predicate in the same first case unless the logical consequence is trivial.

## 11. Handheld / Steam Deck layout targets
Design baseline must be usable at **1280x800** without relying on OS magnification.

Targets:
- no required hover;
- all functionality on default controller mapping;
- core gameplay text at a comfortable handheld size; never solve overflow by shrinking below readability target;
- minimum focused interactive target presentation roughly 44x44 CSS-equivalent logical pixels where layout permits, with larger invisible hit region for pointer/touchpad;
- one evidence card remains fully legible at default scale;
- cabinet labels remain readable at default zoom;
- active rail reflows/collapses instead of reducing cabinet below readable size;
- text scale settings 100/125/150/175/200%; at >=150%, wide layouts may switch to narrow drawer layout automatically;
- icons/button glyphs scale with associated text;
- no critical prompt placed only in screen corners hidden by rail transitions.

A 30-case product should prefer responsive UI over a custom handheld puzzle mode.

## 12. Accessibility specification

### Input
- complete controller-only path;
- complete keyboard-only path;
- mouse path without drag requirement;
- remapping for gameplay actions beyond basic UI navigation/confirm/back;
- digital D-pad and analog navigation both supported;
- configurable hold-vs-toggle for inspect/highlight if any hold actions remain;
- no rapid presses, timed input or precision pointer action required.

### Vision/readability
- seal identity always pattern/icon + short text label; color is secondary;
- standard important text/UI target >=4.5:1 contrast; large important elements >=3:1; high-contrast preset targets stronger separation;
- text scaling through 200% with reflow/no clipped evidence meaning;
- optional stronger seam width and focus outline;
- optional high-contrast workbench that suppresses decorative texture;
- checkpoint numbers always numeric/textual, not color sequence.

### Motion
- reduced motion;
- reveal speed control;
- instant resolution/skip;
- no camera shake required for tear impact;
- no essential information encoded only in animation timing.

### Audio/haptics
- all information available visually/textually;
- separate master/music/SFX controls;
- haptics optional and independently disableable;
- no audio-only seam/witness cue.

### Cognitive/readability
Optional assists may:
- keep rule glossary pinned;
- show static socket->trigger list;
- use persistent labels instead of icons-only;
- pause between reveal checkpoints;
- expand plain-language evidence cards;
- keep target and observed rows visible together after commit.

They may **not** forecast hypothetical results, eliminate legal-but-wrong options or reveal a next move.

## 13. Visual identity
Presentation should read as a clean tactile **inspection bench / sealed object**, not detective corkboard, customs paperwork, bureaucratic office or realistic security product simulator.

Canonical visual hierarchy:
1. neutral compartmented object/cabinet as substrate;
2. seams as mechanically important linework;
3. tamper strips as the strongest object-level accent, differentiated by pattern/icon/label;
4. evidence cards as clean schematic records;
5. restrained background/workbench texture with no gameplay meaning.

Cabinet reuse is allowed aggressively. Cases may vary silhouette, panel arrangement and surface material, but geometry must never obscure trigger relations. Cosmetic screws, hinges and wear must be visibly subordinate to canonical seams.

Do not make realistic logos, legal warnings, police evidence tags, blood/gore, crime photographs or dense paperwork the identity.

## 14. Audio and haptics
Audio is feedback, never authority:
- focus/select: soft neutral tick;
- install/remove seal: adhesive/clip cue;
- opening checkpoint: latch/open cue;
- tear: short tactile rip/snap;
- success/mismatch: distinct but non-punitive stingers.

If several seals tear at one checkpoint, audio may layer/stagger slightly for clarity but a single checkpoint pulse anchors them visually. Audio ordering cannot imply mechanical sub-order.

Haptic rule mirrors audio: one checkpoint pulse plus optional light tear texture; no unique information exists only in vibration.

## 15. Case select, progression-facing hooks, pause/help/recovery
Without pre-empting Phase 7 economy:
- Case Select groups cases by act and shows `locked / available / solved` only;
- solved cases remain replayable;
- act headings can carry one-line concept names (`Read the Tear`, `Compare Witnesses`, etc.);
- no stars/medals/time grades are assumed;
- Help contains learned rules/predicate glossary and control reference;
- pause exposes Resume, Restart Run if committed, Reset Case, Settings, Help, Case Select, Main Menu;
- exiting a case preserves the latest **edit state** and latest committed trace when persistence later permits; no player should lose a carefully arranged legal tentative solution due to ordinary menu exit;
- crash-safe persistence contract belongs to Phase 8, but UX must distinguish `Continue Editing` from `Replay Last Commit` when both exist.

## 16. Mismatch explanation boundary
Allowed causal explanation after commit:
- exact target fact;
- exact observed fact;
- checkpoint where divergence is observable;
- opening that actually occurred there;
- traversed seam/socket relation that caused an observed tear;
- glossary explanation of the rule.

Forbidden:
- comparison against hidden canonical solution;
- 'closest' solution;
- next correct edit;
- auto-marking candidate sockets/histories as impossible based on target;
- percentage solved;
- future consequence preview after returning to edit.

Thus a failed commit teaches **why the submitted run produced what it produced**, not how to solve the puzzle.

## 17. UX acceptance tests
A Phase-8 implementation plan must include at least these tests.

### Controller / focus
1. Finish SB_01-equivalent case with controller only.
2. Finish arrangement case with controller only, no virtual pointer.
3. Finish placement + arrangement case with keyboard only.
4. Open/close Evidence, Plan, Help, Pause and return focus to originating semantic object.
5. Remove focused seal, undo, redo, then switch panel; focus remains deterministic.
6. Rapidly enter/cancel Move mode; no duplicate/missing history cards.

### Transaction stress
7. Place/remove/move seals rapidly, undo to initial state, redo to final state; exact state restored.
8. Reorder history, Commit immediately, press Return to Edit during first reveal animation; committed resolver snapshot is unaffected and edit state restores exactly.
9. Spam Commit input; only one immutable run begins.
10. Skip during a same-checkpoint multi-tear; final break times remain identical and no animation sub-order leaks into evidence.
11. Replay then scrub backward/forward; observed trace is identical and cannot alter edit state.

### Oracle boundary
12. For every legal edit, pre-commit target cards remain visually neutral; no correctness state changes.
13. Static socket highlight lists only immutable trigger relations.
14. Disabled Commit explains only structural illegality.
15. After mismatch, causal trace can identify what happened but contains no next-action recommendation.

### Accessibility/readability
16. Grayscale/color-vision simulation: every seal, focus, state and predicate remains distinguishable.
17. 200% text: no evidence predicate loses words/meaning; rails reflow rather than overlap Workbench.
18. 1280x800 at 150% text: player can inspect cabinet, edit history and read target evidence without pointer precision.
19. Reduced motion + Instant reveal: all checkpoint/break information remains available.
20. Audio muted + haptics off: no information loss.
21. High-contrast mode: gameplay-important standard text/elements meet target contrast.

### Content-layout adversaries
22. Maximum intended cabinet complexity fits handheld layout with all participating labels readable.
23. Maximum intended evidence-card count scrolls inside Evidence rail and never forces Workbench below floor.
24. ARRANGE_BOUNDED_SUBSET with one omitted compartment makes exact open/closed counts obvious.
25. Two or more seals tearing at same checkpoint cannot be mistaken for ordered sub-events.
26. Long localized strings at expansion budget do not overlap glyphs, numbers or predicate identity.

## 18. Hard UX content gates
A case is presentation-invalid even if mechanically certifiable when:
- participating seams cannot be distinguished at target handheld scale;
- socket covered-seam relation requires pixel hunting;
- more than one evidence predicate must be inferred from color alone;
- history constraints cannot fit/reflow without hiding meaning;
- a human needs live hypothetical outcome feedback merely to understand the input state;
- a target requires simultaneous visual comparison that cannot be achieved through focus cross-highlighting or rail switching;
- decorative geometry can be mistaken for a canonical seam.

Such a case must be redrawn or cut; the oracle boundary must not be weakened to rescue it.

## 19. Phase-6 conclusion
**PASS.** Seal Break's cabinet/seam/witness model survives controller-first and handheld UX design without turning inspection into a solver.

Frozen interaction principle:
> The player may inspect every immutable causal relation and every fact produced by an already-committed run, but the game never evaluates the consequences of a tentative future plan before Commit.

Next phase: **Phase 7 — Economy / Retention / Commercial Model.** Freeze premium pricing posture, campaign unlock pacing, demo packaging/carryover, achievements/platform features, replay incentives, hint philosophy if any, save/progression-facing expectations and monetization boundaries without adding gameplay systems.