# GAME #010 — PHASE 6 UX / PRESENTATION ARCHITECTURE

Date: 2026-08-31
Status: **PHASE 6 ACTIVE — CORE UX CONTRACT ESTABLISHED**
Game: Luggage Carousel Zero *(working title)*

Authority: all prior active Game #010 authorities -> `GAME10_PHASE5_CLOSURE.md` -> this file.

This phase defines interaction/presentation only. It may not add mechanics, alter solver semantics, or rescue content with hidden information.

---

## 1. Fresh platform constraints informing UX

Steam/Steam Deck is the primary platform target. Current official Steamworks guidance checked 2026-08-31:

- Steam Deck native 1280x800 is preferred; UI text must remain readable at handheld viewing distance. Source: https://partner.steamgames.com/doc/steamhardware/compat
- Deck/Machine Verified expects all game functionality reachable through the default controller configuration. Source: https://partner.steamgames.com/doc/steamhardware/recommendations
- Steam Input supports action-based input and device-specific action origins/glyphs; UI should not assume one physical controller layout. Source: https://partner.steamgames.com/doc/features/steam_controller/concepts
- Steam recommends device-appropriate/future-proof controller glyph handling where possible. Source: https://partner.steamgames.com/doc/features/steam_controller/steam_input_gamepad_emulation_bestpractices

Design implication: the game is **fully controller-native**, mouse/keyboard equivalent, 1280x800 first, no hover-only information, and no essential text entry during play.

---

## 2. Primary play-screen composition

The game uses one dominant puzzle screen with no camera pan required for canonical N<=8 cases.

### Layout zones at 1280x800
- **Center 65–72% of width:** carousel ring and fixed gantries.
- **Right 24–30%:** passenger queue, front passenger enlarged; next 2 passengers visible in compressed form when space permits.
- **Top strip:** case ID/title, ticks remaining, K swaps/tick and swaps remaining this tick.
- **Bottom strip:** context actions: Select/Swap, Preview, Advance, Undo, Restart, Pause/Menu.

No permanent minimap, inventory panel, objective journal or modal rulebook is required during play.

### Carousel readability
- S0 pickup is always anchored visually at a consistent screen direction, normally bottom-center/right-center depending final art composition.
- Fixed gantries are visibly bolted to the world/ring structure.
- Bags travel beneath/through gantries; labels never ride on bag sprites.
- Socket focus is indicated by shape/outline/scale, never color alone.
- Ring seam S(N-1)<->S0 is drawn as continuous track so seam adjacency is obvious.
- GAP is rendered as a clearly empty moving occupancy marker/spacing ghost, not as invisible absence; players must be able to track that an empty phase is circulating.

---

## 3. Input model

### Controller action abstraction
Use semantic actions rather than hard-coded button names:
- `FocusPrevSocket`
- `FocusNextSocket`
- `SelectSwapOrigin`
- `ConfirmSwapTarget`
- `CancelSelection`
- `Preview`
- `Advance`
- `Undo`
- `Restart`
- `OpenPause`
- `FocusPassengerPanel`
- `TogglePredicateDetails`

Physical glyphs are resolved from active device where supported.

### Canonical controller flow
1. D-pad/left stick moves focus clockwise/counter-clockwise between sockets.
2. Confirm selects current gantry label as swap origin.
3. Only the two adjacent legal targets illuminate.
4. Left/right selects one neighbor; Confirm executes the swap.
5. Cancel returns to neutral focus without spending action.
6. Preview is a dedicated action.
7. Advance is a dedicated action and requires a short confirmation only in accessibility option `Confirm Advance`; default is one press.
8. Undo is always one action away and remains available in DEAD/WON/BUDGET_FAILED states where semantics permit.

No free cursor is required for controller.

### Mouse/keyboard
- Clicking a gantry selects it; only adjacent gantries become valid swap targets.
- Dragging a label directly across the ring is **not** allowed because it visually implies long-distance arbitrary swapping.
- Keyboard arrows/A-D cycle socket focus; Enter/Space confirm; configurable bindings.

---

## 4. Swap-selection feedback

The local-adjacency correction must be taught through interaction, not prose.

On selecting a gantry:
- selected gantry gains a strong focus ring;
- exactly two neighboring gantries pulse/outline as legal targets;
- all other gantries visibly de-emphasize;
- the ring-edge seam neighbor is highlighted identically to the interior neighbor;
- if K=0, gantries remain inspectable but cannot enter swap-select state; the UI says `No swaps this tick` rather than disabling focus entirely.

Equal-value neighbor swaps may be selected but before execution the UI displays `No change` and requires a second confirm only if the player insists. Solver omits them.

---

## 5. One-step Preview

Preview must visualize the frozen Phase-4 contract without becoming a solver oracle.

When Preview is held/toggled:
- every bag and GAP shows one ghost destination one socket clockwise;
- the incoming pickup occupancy receives a stronger ghost highlight;
- front passenger clauses show prospective MATCH/MISS state for that single incoming occupancy under current S0 label;
- a successful immediate pickup may show a translucent `TAKEN` result marker;
- ticks do not decrement and state does not mutate.

Preview never shows:
- future ticks beyond one;
- which swap should be made;
- dead/alive status of hypothetical futures;
- future passenger predicate outcomes after a hypothetical service;
- optimal solution length;
- multi-step arrows.

Reduced-motion mode replaces moving ghosts with static source→destination markers.

---

## 6. Advance animation and causal timing

Default ADVANCE presentation sequence:
1. player input locks for movement resolution;
2. all occupancies move simultaneously one socket clockwise in ~350–500 ms;
3. arriving pickup occupancy settles beneath S0 gantry;
4. predicate clauses resolve left-to-right visually in stable LABEL -> SHAPE -> MARK display order, even though logic is simultaneous/order-independent;
5. if match: bag moves into pickup gate/passenger claim area, then disappears from ring; GAP marker remains at the vacated moving occupancy phase;
6. passenger card exits and next card promotes;
7. tick counter decrements and controls return.

The visual clause sequence is explanatory only and cannot imply order-dependent logic.

Speed settings:
- Normal;
- Fast;
- Instant/Reduced Motion.

All modes resolve exactly the same deterministic state.

---

## 7. Passenger predicate cards

Front passenger is always fully public.

### Clause presentation
Stable order:
1. LABEL
2. SHAPE
3. MARK

Each clause uses:
- icon;
- short localized text/value;
- redundant pattern/symbol when color is used.

Examples should read visually as `RED LABEL` + `SQUARE` rather than Boolean notation. AND is implied by grouping but may be shown as small separators during onboarding.

### Queue visibility
- Front passenger: full predicate.
- Next one/two passengers: full predicates visible whenever layout allows; this is planning information and must never be hidden as difficulty.
- If more passengers remain than panel space, allow scrolling/focus to inspect every remaining passenger without spending a tick.
- No tooltip-only clauses.

---

## 8. Match / miss explanation

After every occupied pickup arrival, player receives explicit clause-level feedback.

Examples:
- LABEL ✓ / SHAPE ✓ -> `PICKUP`
- LABEL ✕ / MARK ✓ -> `MISSED: wrong gantry label`
- SHAPE ✕ -> `MISSED: bag shape`

A miss is neutral, not framed as error, because intentional misses are core strategy. Avoid red alarm language such as `FAIL` for a normal non-match.

The event log stores the last 3–5 pickup outcomes in compact form for review, but does not become a full spreadsheet/history view.

---

## 9. DEAD / budget failure / win UX

### DEAD
Exact solver declares the committed state unsolvable within remaining budget.

Presentation:
- subtle but unmistakable banner: `No completion remains from this state.`
- forward Swap/Advance disabled;
- Undo and Restart emphasized;
- no explanation of which earlier move caused the dead state unless it is simply the immediately impossible passenger/trait availability invariant;
- no suggested move and no automatic rewind.

The purpose is recovery, not oracle-driven exploration.

### Budget failure
When ticks reach zero with passengers remaining:
- state freezes inspectably;
- show `Out of ticks`;
- Undo/Restart available immediately;
- optionally show number of passengers served, but no score economy.

### Win
- short celebratory pickup/queue-clear animation;
- case complete panel with optional mastery stats approved later in Phase 7;
- Continue / Replay / Case Select.

No star rating is assumed in Phase 6.

---

## 10. Undo / Restart presentation

Undo is first-class and consequence-free.

- One input reverses exactly one committed atomic SWAP or ADVANCE.
- Holding/opening Undo history is **not** required; stepwise repeated Undo is enough.
- Undo after Advance reverses movement, pickup, passenger promotion, tick decrement and terminal state atomically.
- Undo after Swap restores exact labels and swap bandwidth.
- Restart asks for confirmation only if the player has made more than one committed action; confirmation can be disabled in settings.

Animations on Undo may play rapidly/reverse, but reduced-motion mode snaps to restored state.

---

## 11. Onboarding plan

Teaching occurs through the demo/campaign cases, not tutorial text walls.

### Case 1
Goal: understand bags move, gantry labels do not.
- K=0.
- Before first Advance, one compact callout points at a bag and gantry: `Bags move. Gantry labels stay here.`
- After Advance, highlight the unchanged gantry position.

### Case 2
Goal: combine label and bag trait.
- first swap tutorial.
- selection affordance itself teaches adjacency.

### Case 3
Goal: away-from-pickup staging.
- no hint names the solution.
- if player repeatedly attempts pickup-only edges and reaches DEAD, one optional contextual hint may say `Labels can be moved before they are needed.` It must not identify the edge.

### Cases 4–5
Goal: candidate preservation and intentional miss.
- first strategic miss is celebrated as valid planning: `A passenger can wait. A matching bag does not have to be taken this tick if the label does not match.`

### Case 6
Goal: persistent gap semantics.
- after first pickup, show one brief callout: `The empty place keeps circling. The belt never compresses.`
- do not claim the gap shifts other bags.

After Case 6, tutorial callouts cease by default; glossary/help remains available.

---

## 12. Hint philosophy

Hints are optional accessibility/assistance, never required.

Three levels may exist later if Phase 7 approves surfacing them:
1. **Rule reminder** — restates a mechanic relevant to the current case.
2. **Reasoning nudge** — names a relationship (`A bag needed later may be worth preserving`).
3. **Structural hint** — identifies a family property (`A winning plan requires moving a label away from pickup first`).

No hint may provide an exact swap sequence unless a future accessibility option explicitly chooses full solution reveal. Full-solution reveal is not base UX canon yet.

---

## 13. Accessibility contract

Mandatory design targets:
- color never sole carrier for LABEL/SHAPE/MARK or match state;
- text scaling with at least 100/125/150% presets while preserving 1280x800 usability;
- adjustable animation speed including instant/reduced-motion mode;
- screen shake off by default or absent;
- no time pressure or dexterity requirement;
- full keyboard remapping and controller remapping compatibility;
- device-appropriate glyphs where possible;
- subtitle-style text unnecessary for gameplay audio because all essential information is visual/textual;
- gameplay does not require audio, but audio cues redundantly support movement, swap, match, miss and dead-state events;
- high-contrast focus mode;
- patterns/symbols for color labels;
- no essential hover states;
- no tiny precision dragging;
- pause at any time outside atomic transition animation; transition can finish then pause.

Screen-reader feasibility for dynamic ring geometry is an empirical/technical gate rather than promised full certification at this stage. Phase 8 must at minimum expose accessible semantic labels in UI architecture where engine/toolkit permits.

---

## 14. Menus and navigation

### Main menu
- Continue
- Case Select
- Settings
- Accessibility
- Credits
- Quit

No account, login, shop, battle pass, daily challenge or online requirement.

### Case select
Acts are visible as compact chapters. Completed cases may show completion and optional mastery marker later approved by Phase 7. Locked progression rules are deferred to Phase 7, but replaying completed cases is always allowed.

### Pause
- Resume
- Undo
- Restart Case
- Settings
- Case Select
- Main Menu

Leaving a case should preserve resumable state if persistence architecture supports it; Phase 8 defines exact save contract.

---

## 15. Audio/visual language

Visual style target remains stylized 2D/2.5D, not realistic airport simulation.

Key visual hierarchy:
1. moving occupancy/bag;
2. fixed gantry label;
3. pickup socket;
4. front passenger predicate;
5. adjacent legal swap relationships;
6. secondary queue/budget information.

Audio is functional:
- soft mechanical click for adjacent label swap;
- carousel movement loop/step cue;
- distinct but non-punitive miss cue;
- satisfying pickup cue;
- subtle dead-state tone;
- no reliance on voiceover.

Busy airport ambience must be low-intensity/optional and may not mask feedback cues.

---

## 16. First-session target

By 20 minutes a new player should be able to answer without tutorial prose:
- labels belong to gantries/sockets;
- bags move clockwise exactly one socket per Advance;
- only adjacent labels can swap;
- passenger wants all shown clauses simultaneously;
- a matching pickup consumes exactly one bag/passenger;
- a miss can be intentional;
- a consumed bag leaves a circulating empty occupancy;
- Undo/Restart are consequence-free;
- Preview shows only the next tick.

Empirical usability gates before final freeze:
1. >=80% of first-time test players can predict Case-2 next pickup after one explanation/case experience;
2. >=80% understand adjacency including seam edge without being told twice;
3. expert N=8 state remains readable at 1280x800 with 125% text scale;
4. players interpret normal misses as neutral state, not accidental failure;
5. reduced-motion mode preserves all predictive information;
6. controller users can complete demo without mouse/touchpad fallback.

Thresholds are prototype/playtest targets, not claims of achieved results.

---

## 17. Open Phase-6 work before closure

The core UX contract is now specified, but Phase 6 is not yet complete. Next pass must:
1. define exact responsive layout behavior for N=3..8 and passenger queues at 1280x800 / 16:9 desktop / ultrawide without moving critical controls unpredictably;
2. define settings/accessibility option defaults and persistence semantics at UX level;
3. specify case-select/progression presentation assumptions handed to Phase 7;
4. run hostile UX walkthroughs: controller-only, color-blind/high-contrast, 150% text, reduced motion, repeated Undo, DEAD after swap, seam swap, K=0 and K=2;
5. resolve whether optional event log and predicate-detail focus remain readable or should be simplified;
6. close Phase 6 only when implementation can construct every required screen/state without inventing interaction rules.

**PHASE 6 ACTIVE. DESIGN COMPLETE = NO.**