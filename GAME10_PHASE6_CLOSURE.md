# GAME #010 — PHASE 6 UX / PRESENTATION CLOSURE

Date: 2026-08-31
Status: **PHASE 6 COMPLETE**
Game: Luggage Carousel Zero *(working title)*

Authority: all prior active Game #010 authorities -> `GAME10_UX.md` -> this file. This file resolves the open Phase-6 items and overrides conflicting optional-UX assumptions.

## 1. Responsive layout contract
The canonical puzzle never requires camera pan for N=3..8.

### 1280x800 / 16:10 baseline
- top status strip: 56 px logical height at 100% text;
- bottom action strip: 64 px;
- right passenger rail: 320 px nominal, 360 px when predicate width requires it;
- remaining center field owns the ring; ring scales down before predicate text is truncated;
- N=3..5 may use larger sockets but socket centers remain on the same conceptual ring; N=6..8 uses the maximum readable ring that preserves >=48 px controller-focus targets.

### Standard 16:9 desktop
Critical zones keep their relative anchors: status top, actions bottom, queue right, carousel center-left. Extra horizontal width enlarges breathing room/ring up to a cap; it does not move controls into new corners.

### Ultrawide
The gameplay composition is width-capped to a centered 16:9/16:10 safe frame. Extra width becomes ambience/background. Passenger queue never migrates to a far screen edge.

### Queue overflow
Front passenger is always full-size and fully visible. Remaining passengers occupy a vertically scrollable rail. At least the next passenger summary is visible at 1280x800/100%; all remaining passengers are reachable by focus/scroll without spending an action. Predicate clauses are never elided. A small `+N remaining` count may summarize offscreen cards but never replaces inspectability.

### 125% / 150% text scaling
At 125%, secondary queue cards collapse to compact full-clause rows and the ring may scale down modestly. At 150%, only the front passenger remains persistently expanded; the queue becomes a focusable compact list whose selected row expands in-place/overlay without covering the pickup socket or tick budget. Bottom action labels may become glyph + short action name. Predicate clauses never truncate; horizontal marquee is forbidden. If a translation exceeds the reserved clause width, cards wrap vertically and the rail scrolls.

## 2. Settings/accessibility defaults
Defaults:
- text scale 100%; presets 100/125/150%;
- animation Normal; Fast and Instant/Reduced Motion available;
- reduced motion OFF;
- high-contrast focus OFF;
- color-redundant symbols/patterns ALWAYS ON and not removable;
- screen shake OFF / no gameplay shake required;
- Confirm Advance OFF;
- Restart confirmation ON after >1 committed action;
- gameplay audio and ambience enabled at moderate independent volumes;
- dynamic controller glyphs ON when available;
- hints available but never automatic after onboarding contextual prompts.

UX-level persistence: settings/accessibility are profile-global and survive case/restart. Input bindings are profile-global. Case-local UI focus is not required to persist across launches. Phase 8 owns exact file/cloud format.

## 3. Case select / progression presentation handed to Phase 7
- Five compact act chapters A–E remain visible from first entry, but locked acts may show title + progress requirement without hiding total campaign scale.
- Case tiles show: ID/title, completion state, optional mastery marker if Phase 7 approves one, and demo/full-product ownership state only where commercially necessary.
- Replaying completed cases is always allowed.
- Case select never shows solver difficulty numbers, optimal solution, solution count or family tags.
- Completing a case returns to a simple Continue/Replay/Case Select panel; no loot/reward animation is assumed.
- Progression gating may unlock small batches rather than force strict linearity; exact rule frozen in Phase 7.

## 4. Hostile UX walkthroughs
### Controller-only
PASS. D-pad/left-stick socket focus, Confirm origin/target, Cancel, dedicated Preview/Advance/Undo/Restart/Pause cover all gameplay. Queue inspection uses panel-focus action then vertical navigation. No mouse fallback.

### Seam adjacency
PASS with requirement: when S0 or S(N-1) is selected, the across-seam legal neighbor receives the same strong edge/outline treatment as interior adjacency. A subtle curved connector appears during selection only. No long-distance line.

### K=0
PASS. Gantries remain focusable/inspectable; selecting does not enter target mode and displays `No swaps this tick`. Advance/Preview remain normal. This avoids teaching that labels disappear when non-editable.

### K=2
PASS with one addition: top strip shows `Swaps this tick: 2` then `1` then `0`; after first swap, focus remains on resulting layout rather than auto-selecting another edge. Undo restores both layout and count visibly.

### 150% text
PASS under compact queue rule above. Critical predicate never hides. Carousel can shrink but pickup/labels remain >= target readability floor. If a locale still overflows, selected passenger details may open a non-modal side overlay; Advance/Swap remain visible and overlay closes with Cancel.

### Reduced motion
PASS. Advance uses instantaneous state replacement plus static origin/destination arrows for one beat; pickup/miss uses icon/text state changes, not motion. Preview uses static destination markers.

### Color-independent labels
PASS. Every label value has text abbreviation + unique symbol/pattern family. Shape and mark use silhouettes/icons plus text in passenger details. Match/miss uses check/cross + words, never hue alone.

### Repeated Undo
PASS. One press = one atomic action. No history modal. Holding Undo may repeat only with a deliberate initial delay to prevent accidental multi-rewind; this is convenience, not a new semantic. Terminal banners disappear/restored exactly with state.

### DEAD immediately after Swap
PASS. Swap animation settles, exact feasibility result then raises `No completion remains from this state.` Forward controls disable; Undo is primary focus. The UI must not flash a future solution or identify the guilty edge.

### Queue overflow
PASS. All predicates remain inspectable through scroll/focus; front passenger cannot scroll off as the active card. Queue scrolling never changes puzzle state.

## 5. Event log and predicate-detail decision
The optional 3–5 row event log is **removed from the permanent play screen**. It competes with queue/predicate space at 1280x800 and 150% text, and repeated Undo already supplies causal inspection.

Replacement: after each occupied pickup, a transient but pausable/reduced-motion-safe result chip remains near pickup (`PICKUP` or `MISSED: wrong gantry label`, etc.). The last result is also available in a small `Last result` line under the front passenger until the next Advance. No multi-event history is canonical.

`TogglePredicateDetails` survives, but is simplified: it focuses/expands the selected passenger card and exposes icon + localized clause text. It does not open Boolean notation, solver data, candidate bags or future evaluation.

## 6. Required screens/states
Implementation can now construct without design invention:
1. main menu;
2. case select with act chapters;
3. primary puzzle screen neutral;
4. swap-origin/target selection;
5. one-step Preview;
6. Advance resolving/default and reduced-motion forms;
7. match/miss result state;
8. DEAD;
9. out-of-ticks;
10. win panel;
11. pause menu;
12. settings/accessibility/input binding;
13. passenger-detail/queue focus at all text scales;
14. onboarding callouts Cases 1–6.

## 7. Phase-6 acceptance
- [x] N=3..8 responsive behavior frozen.
- [x] 1280x800, 16:9 and ultrawide behavior frozen.
- [x] 125/150% text and queue overflow frozen.
- [x] settings/accessibility defaults frozen.
- [x] UX persistence expectations frozen.
- [x] case-select assumptions handed to Phase 7.
- [x] hostile walkthroughs passed without adding mechanics.
- [x] permanent event log removed; last-result feedback retained.
- [x] predicate-detail focus simplified and retained.
- [x] required screens/states enumerable without interaction invention.

**PHASE 6 COMPLETE. DESIGN COMPLETE = NO.**

Next authority: `GAME10_COMMERCIAL.md`.