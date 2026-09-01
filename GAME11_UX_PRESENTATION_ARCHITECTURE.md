# GAME #011 — MISSING STEP — PHASE 6 UX / PRESENTATION ARCHITECTURE

Date: 2026-09-01
Status: **PHASE 6 UX / PRESENTATION ARCHITECTURE COMPLETE**
Authority: `START_HERE.md` -> `STATUS.md` -> `GAME_INDEX.md` -> `GAME11_PRODUCT_THESIS.md` -> `GAME11_MECHANICAL_ARCHITECTURE.md` -> `GAME11_CONTENT_ARCHITECTURE.md` -> this file for player-facing interaction/presentation.

Fresh platform constraint check (2026-09-01): current Steamworks Deck compatibility guidance prefers 1280×800 support, requires readable interface text at Deck distance, and recommends configurable text size/contrast; controller glyphs must match active input. Missing Step therefore treats 1280×800/controller as primary constraints rather than later polish.

---

## 1. Screen model
The game uses one primary puzzle screen rather than separate code/editor and machine views.

At 1280×800 baseline:
- top band: case title/progress + target card + horizon;
- center-left/center: machine diorama and workpiece lane/orientation/mark state;
- lower/center-right: shared tick timeline with tracks A–D as rows and global ticks as columns;
- bottom action band: DELETE selection state, PREVIEW/RUN, RESET/BACK, help/settings hints.

The exact proportions are implementation-flexible, but all mechanically relevant information must fit without scrolling during a standard <=4-track case. At 150% text, secondary explanatory prose may collapse behind focus/help, but target clauses, selected token, active tick, track IDs and primary actions must remain visible.

No dense source-code view exists.

---

## 2. Planning interaction
### Controller
Primary baseline:
- D-pad / left stick: move focus among timeline tokens, target clauses and major controls;
- A / south: select eligible token for deletion / confirm focused primary action;
- B / east: cancel current deletion selection or back out of modal;
- X / west: toggle Preview schedule expansion / compact view;
- Y / north: open contextual rule explanation for focused token/target;
- LB/RB: jump between tracks;
- LT/RT: scrub preview tick when preview is open;
- Menu/Start: pause/settings.

Exact glyph mapping may adapt through Steam Input, but every required puzzle action must be reachable without pointer emulation or text entry.

### Mouse/keyboard
- pointer selects tokens/controls directly;
- arrow keys/WASD can mirror controller focus navigation;
- Enter/Space confirm, Esc back/pause;
- keyboard-only path must never require hover.

### Input-mode switching
Glyphs switch only after a meaningful input from the new device. Mouse motion alone should not constantly flip controller prompts. Mixed controller + mouse use remains functional.

---

## 3. Token identity and deletion
Each token shows redundantly:
- opcode icon silhouette;
- short localized text label on focus/help, not necessarily always printed inside every compact token;
- stable positional notch/slot marker along the loop;
- eligibility state via shape/border + interaction, not color alone.

When selected for deletion:
1. token receives a high-contrast cross/remove treatment;
2. preview immediately shows the surviving loop closing the gap;
3. original position remains ghosted enough to communicate what was removed;
4. start-anchor pointer visibly resolves to the next surviving clockwise token if the anchor was deleted.

Duplicate PUSH/PUSH or STAMP/STAMP tokens must remain positionally distinguishable even in monochrome. Do not label them with arbitrary “PUSH 1 / PUSH 2” unless necessary for accessibility help; spatial slot and focus narration should carry identity.

For two-track mastery, deletion slots are independent and visibly labeled “Remove 1 from A” / “Remove 1 from B”; RUN is unavailable until both required edits are selected.

---

## 4. Preview contract in UX
Preview displays only information allowed by Phase 4:
- post-edit loop rows;
- exact opcode alignment through public horizon;
- cycle-boundary markers;
- active start anchors;
- CLAMP-active-at-start tick markers derived from schedule.

Preview never simulates future workpiece lane/orientation, stamp count, blocked pushes or target pass/fail before RUN.

To prevent accidental oracle presentation:
- target clauses do not turn green/red during planning;
- no token receives “better/worse” highlighting;
- no automatic comparison against unselected edits exists;
- “CLAMP active” is shown as machine schedule information, not “this PUSH will fail.”

The player may scrub the timeline and inspect which opcodes execute on a tick. A small “A → B → C → D” execution-order ribbon remains visible wherever same-tick operations are displayed.

---

## 5. CLAMP visualization
CLAMP is the rule most likely to be misread because it acts next tick.

Canonical presentation:
- executing a CLAMP token emits a visible mechanical latch/arming cue toward lane 1;
- timeline shows a thin one-column arrow from the CLAMP occurrence to the next tick header;
- the next tick header shows a clamp/shutter icon indicating lane 1 starts that tick blocked;
- multiple CLAMPs on one tick converge to one next-tick marker;
- consecutive scheduled clamps show separate arrows/markers, never a numeric stack.

Reduced-motion mode replaces travel animation with immediate state change + arrow/icon pulse. Audio cannot be the sole telegraph.

---

## 6. RUN presentation
RUN is deterministic playback, not a timing challenge.

At each tick:
1. global tick column highlights;
2. prior CLAMP latch state is visibly established;
3. A, then B, then C, then D token fires with short causal pulse;
4. machine diorama mirrors immediate PUSH/TURN/STAMP effects;
5. CLAMP schedules its next-tick marker;
6. counts/target-observable values update;
7. cursor advances.

Default playback should make causality readable but retries fast. Player can:
- pause deterministic playback;
- step one token/tick while paused after at least one full normal run of the case, or via accessibility setting;
- accelerate playback (e.g. 1×/2×/4× implementation choice) without changing simulation;
- skip to result only after the case has been watched at least once or through an accessibility setting.

There is no input affecting puzzle state during RUN.

---

## 7. Success/failure explanation
At horizon:
- target card compares expected vs actual for every active clause;
- wrong lane/orientation use icon + text/state shape;
- stamp/blocked counts show exact actual value;
- if a monotone upper/equality bound was exceeded and playback stopped early, the exact tick and exceeded clause are highlighted.

Failure copy must describe outcome, never solution:
- acceptable: “Blocked pushes: 2 / target 0”;
- unacceptable: “Delete A3 instead.”

Primary failure actions:
- `REVISE` returns to planning with the last selected deletion(s) retained;
- `WATCH AGAIN` replays same deterministic run;
- `RESET CASE` clears edits.

Success primary action is `NEXT CASE`; replay remains available.

No life loss, score shame screen or resource penalty.

---

## 8. Onboarding / first eight demo cases
Tutorial language is layered and dismissible.

Case 1:
- visually point to loop, start anchor, DELETE, RUN;
- one short statement: removing a step closes the loop.

Case 2:
- introduce horizon columns and recurrence; no arithmetic formula.

Case 3:
- second track appears; A→B order ribbon introduced.

Case 4:
- CLAMP arrow explicitly teaches “arms lane 1 for the next tick.”

Case 5:
- tutorial deliberately stops telling which consequence to inspect; introduces comparison after failure.

Case 6:
- duplicate-position lesson: two identical opcode icons, different slots.

Case 7:
- same-tick order lesson with visible A then B execution.

Case 8:
- two-track mastery teaser; deletion requirements shown as two separate slots.

After onboarding, no mechanic tooltip appears automatically unless a genuinely new already-frozen concept is first encountered. Help remains available contextually.

---

## 9. Accessibility and readability
Required launch accessibility contract:
- text-size setting with baseline and enlarged mode; 150% must keep primary puzzle truth usable at 1280×800;
- high-contrast option;
- no information encoded solely by color;
- color-blind-safe palette choices plus icon/shape redundancy;
- reduced motion: removes loop-collapse travel, camera shake, parallax and repeated sliding while preserving state-change cues;
- screen flash intensity limiter / no required flashing;
- separate music, effects and UI volume controls;
- subtitles/captions for any spoken or mechanically relevant audio; launch can simply avoid required speech;
- controller remapping via platform/input layer where supported, plus logical action abstraction internally;
- keyboard-only and controller-only complete paths;
- focus indicator always visible in non-pointer navigation;
- optional persistent opcode legend;
- optional step-through RUN from first attempt for players who need slower causal inspection;
- adjustable playback speed independent of difficulty;
- confirmation for abandoning an unsaved in-progress case selection only when actual progress would be lost; otherwise avoid nuisance confirmations.

Smallest essential text should target comfortably above Valve's 9px Deck approval floor; implementation should aim for approximately 12px-or-better readable character height at 1280×800 before user scaling, subject to font metrics.

---

## 10. Audio/visual language
Presentation fantasy: compact mechanical repair bench, not industrial factory management.

Visual hierarchy:
- tracks = physical instruction rings/strips with large pictographic tokens;
- global timeline = diagnostic overlay that unfolds from those physical loops;
- workpiece = one expressive object whose lane/orientation and accumulated stamps are obvious;
- machine events use consistent spatial verbs: push actuator, turntable, stamp head, clamp shutter.

Each opcode has a distinct silhouette and sound family:
- PUSH: short linear actuator hit;
- TURN: rotational ratchet;
- STAMP: percussive press with visible mark count change on success and softer/no-mark cue on lane0 no-op;
- CLAMP: arming click now, shutter closure cue at next tick.

Sound is reinforcement only. Success should sound like a machine settling into a clean cadence, but there is no rhythm-timing mechanic.

Avoid screen-filling particle effects, decorative belts/resources, worker characters or background machinery whose motion could be mistaken for puzzle state.

---

## 11. Pause, settings, save/load surface
Puzzle state is planning-only persistent state plus campaign progression; RUN can always be deterministically reconstructed.

Pause menu:
- Resume;
- Restart case;
- Case Select (with loss-of-current-selection warning only if needed);
- Help / Rules;
- Settings;
- Main Menu.

Settings accessible from title screen and pause before gameplay.

Auto-save expectations for Phase 8 specification:
- save after case completion;
- save current case ID and selected deletion(s) while planning;
- saving mid-RUN is unnecessary because RUN is deterministic and short; resume may restore planning state and selected edits;
- never require manual save slots for normal campaign.

Case select shows completed/uncompleted and act progression without exposing solver difficulty numbers or solution counts.

---

## 12. Hostile UX walkthroughs
### Controller-only at 1280×800
PASS by contract: every action has focus navigation; no hover/text-entry dependency; target and all active tracks remain on one puzzle screen.

### 150% text
PASS with responsive collapse rule: explanatory prose/tooltips may become focus-driven overlays, but target clauses, actions and token rows cannot be hidden behind scrolling during planning.

### Duplicate identical tokens
PASS: stable slots, focus highlight, ghosted deletion position and spatial identity prevent color/name-only ambiguity.

### Deleted start token
PASS: phase anchor visibly walks clockwise to next survivor during loop-close animation; Preview shows first executed token.

### Same-tick A/B interaction
PASS: persistent A→D ribbon + sequential firing inside highlighted shared tick.

### CLAMP on final tick
PASS: arrow may point to an out-of-horizon faded boundary but no active next-tick marker appears inside play; result explanation never calls it a failure by itself.

### Failure after long deceptive prefix
PASS: result shows clause delta; replay can scrub/step/accelerate; no solver solution leak.

### Reduced motion
PASS: all travel animations have discrete state-equivalent replacement cues.

### Rapid retries
PASS: REVISE returns instantly with edit retained; playback speed/skip rules prevent animation from becoming punishment.

---

## 13. Phase-6 acceptance gates
- Controller-only path: PASS.
- Mouse/keyboard and keyboard-only path: PASS.
- 1280×800 first-class layout: PASS.
- 150% text contract: PASS.
- Correct active-input glyph behavior: PASS.
- Token positional identity: PASS.
- Deleted-start-anchor communication: PASS.
- Preview non-oracle boundary preserved: PASS.
- A→D same-tick order communicated: PASS.
- CLAMP next-tick semantics communicated redundantly: PASS.
- RUN causality / acceleration / step inspection: PASS.
- Failure explanation without solution leak: PASS.
- First-eight-case onboarding path: PASS.
- Reduced motion/color redundancy/contrast/text sizing: PASS.
- Pause/settings/save surface: PASS.
- Hostile UX walkthroughs: PASS.

**PHASE 6 COMPLETE.**

## Phase 7 handoff
Research and freeze the commercial/retention model without turning the game into grind: current comparable premium puzzle pricing/value expectations, demo strategy and carry-over, campaign unlock pacing, case-skip policy, achievements, replay/mastery incentives, optional hints/help boundaries, Steam platform features and monetization exclusions. Preserve instant experimentation: retries, preview and accessibility may never be monetized or progression-gated.