# GAME #018 — PHASE 6 UX / PRESENTATION ARCHITECTURE

Date: 2026-09-06
Selected concept: **LOCAL TIME**
Status: PHASE 6 COMPLETE — COMMERCIAL MODEL NEXT
Production implementation: NO

## 1. UX objective
The player must understand LOCAL TIME as a physical planning puzzle about simultaneous local clock conditions and persistent process milestones, never as rewind/time travel. At any decision point the screen must answer: what is true now, what has already been earned permanently, what will this placement cover, what is legal, and why did the last Resolve change state.

## 2. First boot / profile / progression
First boot: logo -> accessibility quick setup -> New Game / Continue if save exists. No mandatory account. Quick setup exposes text size, reduced motion, high-contrast/non-color cues, master volume/subtitles, controller glyph preference.

New Game enters LT01 directly after a <=20 second visual premise card: `Different parts of this town can have different LOCAL TIMES.` No lore prologue.

Case Select is a compact town-board: chapter rows, six case cards each, mastery pair below each chapter. Cards show completion, optional efficiency mark, best moves/beats, and introduced/reused concept icons. Normal progression unlocks next case on completion; completing a chapter unlocks the next chapter and its mastery pair. Replay is always allowed. No star grind gates.

Autosave occurs after case completion, settings changes, and at pre-Resolve checkpoints. One local profile is sufficient baseline; Phase 8 defines slots/cloud conflict details.

## 3. Screen hierarchy
Primary play screen has four stable layers:
1. town diorama — sites, objects, carriers, clock zones and sockets;
2. objective strip — 1–3 concise required truths with CURRENT or MILESTONE badges;
3. selected-detail card — site/object/clock rules and current state;
4. action rail — Undo Placement, Resolve, Undo Turn, Replay Last Resolve, Restart/Pause.

Do not use a timeline. Beat count may appear as `Resolve 2/5`, never as elapsed minutes.

## 4. Current versus persistent visual language
Canonical terms in player-facing UI:
- **NOW** badge = CURRENT predicate; icon is an outlined clock face plus condition text such as `NOW: OPEN at 08:00`.
- **DONE** badge = PERSISTENT milestone; icon is a solid stamped check/medallion plus state such as `DONE: RISEN`.
- **LOCKED OUT** = persistent bad milestone; broken-seal icon plus exact cause.

These categories must differ by icon shape, border treatment, text label and motion pattern, never color alone. Tooltips explicitly say `NOW changes when local time changes` versus `DONE remains even when the clock moves` during onboarding.

Earlier-looking clock labels never produce reverse animation. Moving 08:00 over a BAKED loaf leaves it visibly baked.

## 5. Mouse / keyboard placement
Mouse: click clock zone -> legal sockets highlight; hover socket -> ghost zone and exact covered-site outlines; click socket -> unresolved placement; right-click/Escape cancels current placement. Dragging may be supported as presentation sugar only if it snaps to identical legal sockets and never creates intermediate logical coverage.

Keyboard baseline: Tab/Shift+Tab cycles clocks/sites/objective/action rail; arrows/WASD move among spatially nearest legal sockets while in placement mode; Enter/Space confirm; Escape cancel; R Resolve only when focus is not in a destructive confirmation; Z Undo Placement; Shift+Z Undo Turn. All bindings remappable.

## 6. Controller / Steam Deck
D-pad/left stick moves focus between landmarks. Shoulder buttons cycle clocks. A selects/places, B cancels, X opens rule details, Y toggles footprint/rule overview, right trigger Resolve, left trigger Undo Placement; Undo Turn remains action-rail accessible and remappable to avoid accidental destructive recovery.

On clock selection, only legal sockets enter the navigation graph. Focus never requires pixel precision. Current target socket receives a thick animated perimeter plus clock label. Covered sites receive numbered/shape-linked footprint marks.

Steam Deck baseline is 1280x800. Core objective, selected rule, clock labels and footprint conflict must be legible without opening a modal. Default text target is equivalent to >=18 px at 1280x800 for essential labels, with larger accessibility setting.

## 7. Footprints, overlap and illegal conflicts
Selecting a clock displays a translucent footprint plus a hard perimeter and small repeated clock-label stamps inside the footprint. Every covered logical site receives a matching perimeter notch/shape marker.

When same-time footprints overlap, hatch directions combine but remain legal and the shared site shows one effective label.

When a candidate placement would create different labels over one site, the socket is visibly illegal before confirmation: crossed-clock icon on the contested site, two explicit labels (`08:00 / 08:05 CONFLICT`), and the destination cannot be committed. Red may reinforce but cannot be the only signal.

Preview is exact logical coverage; decorative geometry never implies partial coverage.

## 8. Site/object rule cards
Selecting a site opens one compact card:
- landmark name and icon;
- effective local time or `NO LOCAL CLOCK`;
- persistent state of resident object/site;
- relevant rule family in plain language;
- NOW predicates with outlined clock badge;
- DONE/LOCKED OUT milestones with persistent badge;
- if a carrier is involved, public next hop and acceptance boundary.

Example: `BAKERY | Local 08:05 | Dough: RISEN (DONE) | Rule: RISEN -> BAKED when NOW is 08:05.`

Cards show rules, not recommended moves.

## 9. Placement preview and anti-oracle decision
**Locked baseline: NO automatic one-beat consequence preview.** Placement preview shows exact footprint, resulting effective local times and resulting NOW predicates only. It does not label `will advance`, `safe`, `fatal`, winning moves, or future persistent writes.

Reason: persistent transitions are the puzzle's causal reasoning surface. Showing every immediate persistent consequence on hover would encourage socket scanning and convert hazards into an oracle.

Comprehension aid: while a socket is previewed, rule cards whose NOW condition would become true receive a neutral `condition matched` outline, but the UI does not state the resulting transition. In LT01–LT02 only, an optional tutorial pulse may visually connect matched condition text to the relevant rule after the player deliberately selects the site.

Empirical gate: test a variant with explicit one-beat consequence icons. Keep it only if first-time comprehension improves materially and blind socket-scanning does not. Shipping authority remains the no-consequence-preview baseline unless that gate is passed and documented.

## 10. Resolve presentation
Resolve input first locks planning state, then deterministic logic computes instantly. Presentation follows canonical mechanical order but may overlap harmless visual effects after computation:
1. clock zones pulse once and effective local labels appear at affected sites;
2. NOW predicates activate/deactivate;
3. persistent transitions animate one entity at a time in deterministic reason-trace order;
4. dispatch/carrier hop animates after persistent transitions;
5. newly arrived cargo visibly stops with `ARRIVED — eligible next Resolve` when relevant;
6. objectives update;
7. success/failure boundary appears.

Player can speed animation to 2x or skip after computation. Skip never changes state. Reduced Motion replaces travel/pulses with fades/state swaps.

## 11. Reason trace
After every Resolve, a collapsible `What changed?` strip contains 1–6 causal rows, ordered exactly like authoritative writes.

Examples:
- `08:00 covers Bakery -> RAW dough became RISEN (DONE)`
- `Bridge is NOW OPEN because local time is 08:00`
- `Parcel moved Bakery -> Depot; acceptance waits until next Resolve`
- `Garden was UNCOLLECTED under 08:05 -> WILTED (LOCKED OUT)`

Rows can be selected to focus the responsible site, clock footprint and rule card. If nothing persistent changed, state `No milestones changed this Resolve` and list relevant NOW changes.

Replay Last Resolve replays only these already-recorded visuals/reason rows and is labeled `Replay animation`; it cannot alter state.

## 12. Undo / restart / checkpoint language
Undo Placement: reverses most recent unresolved clock relocation and refunds move cost.
Undo Turn: `Restore before last Resolve`; immediately restores canonical pre-Resolve checkpoint. It is UI recovery, never called rewind/time travel.
Restart Case: confirmation only if progress exceeds first Resolve; restores authored initial state.

After Undo Turn, a subtle `Restored planning checkpoint` toast appears. No reverse-motion animation is used.

## 13. Failure and certified dead-state UX
Explicit irreversible hard failure pauses after reason trace and names cause + violated objective: `Garden WILTED after 08:05 exposure. Objective requires FLOWERS COLLECTED.` Buttons: Undo Turn / Restart / Review Rule.

Budget failure: `No Resolves remain; objectives are incomplete.`

Solver-certified dead state may show `No winning continuation from this state` only when exhaustive proof is available. It must offer Undo Turn / Restart and `Why?`, where Why gives a short proof-derived public blocker if available. If proof is unavailable, never claim dead; allow play/restart normally.

Wrong but nonterminal choices are not scolded and do not trigger hints.

## 14. Camera and readability
Default is a fixed three-quarter diorama camera with authored framing per case. Player may pan slightly and zoom within authored limits; `Focus All` restores framing. No rotation required for logic. Every logically relevant site must be selectable from default framing; occluding decoration fades when focused.

At 1280x800: objective strip max two compact rows before expansion; clock labels remain readable at default zoom; footprint outlines >=2 logical pixels plus pattern; essential state icons have text on focus; no critical rule depends on tiny world animation.

## 15. Accessibility/settings
Required baseline:
- full remapping for keyboard/controller;
- mouse-only and controller-only completion paths;
- three text sizes;
- UI scale;
- high-contrast footprint mode;
- non-color-only state encoding always on;
- reduced motion and animation speed/skip;
- screen shake off by default (none required);
- independent master/music/SFX levels;
- subtitles/captions for all informational audio; informational audio duplicated visually;
- focus highlight strength;
- hold/toggle choice where applicable;
- confirm/cancel glyph localization;
- pause at any planning point;
- no reaction-time requirement.

Color-vision presets may tune reinforcement colors but cannot be required for comprehension.

## 16. Pause / settings / save-load / interruption
Pause freezes presentation only; simulation already has no real-time progression. Menu: Resume, Rules Glossary, Restart Case, Case Select, Settings, Quit.

Autosave canonical checkpoint before every Resolve and after completion. Quitting during planning restores the latest saved canonical checkpoint plus unresolved placement state only if Phase 8 persistence can guarantee exactness; safer baseline is restore the last pre-Resolve checkpoint and show `Planning changes since last Resolve were not committed.`

If interrupted during Resolve animation, load authoritative post-Resolve state plus recorded reason trace and offer Replay Last Resolve. Never re-run logic from animation progress.

## 17. Rules glossary / help
Glossary is unlocked contextually and contains only already-introduced families. Core permanent entries: LOCAL TIME, NOW, DONE, Resolve, footprint, carrier arrival boundary, LOCKED OUT. Each uses one static example and one sentence. No solution walkthroughs in baseline campaign.

## 18. LT01–LT06 onboarding moment by moment
**LT01:** camera frames Bakery + Bridge + 08:00 clock. Prompt selects clock, previews one socket, confirms, then Resolve. After first persistent change, overlay contrasts `Dough is RISEN — DONE stays` with `Bridge OPEN — NOW depends on clock`. Player then moves clock away and sees bread stay risen before second Resolve. Free input after <=3 prompts.

**LT02:** introduce fixed 07:55 and movable 08:05. First selection of Garden shows explicit public hazard rule. Footprint preview makes Garden coverage unmistakable. No `this will wilt` oracle. On safe collection, DONE badge anchors persistence; dangerous exposure later, if chosen, demonstrates LOCKED OUT with exact reason.

**LT03:** teach two simultaneous local times. Selecting Station highlights its coupled rule and Bridge requirement together. Overlap/conflict presentation is introduced with one harmless illegal preview that cannot be committed. No new recovery concept.

**LT04:** carrier handoff. Before first dispatch, a three-icon rule diagram states `Prepare -> dispatch/hop -> accept on a later Resolve`. Arrival animation stops visibly and card says `Eligible next Resolve`; this prevents apparent bug/confusion.

**LT05:** remove directive tutorial prompts. Objective + public rules only. First true test of reading an irreversible exposure before acting. On fatal shortcut, failure reason links directly to the previously visible Garden rule; Undo Turn is highlighted once.

**LT06:** no new grammar. At start, one optional overview highlights three clocks and objective categories. Player must independently compose persistence + simultaneity + hazard knowledge. Demo completion screen asks no quiz but shows concise identity line: `Different local times. Persistent consequences.`

## 19. UX acceptance / empirical gates
Phase-6 prototype/playtest gates:
1. >=80% of first-time testers can explain NOW vs DONE after LT02 without facilitator correction.
2. <=10% describe Undo Turn or earlier-looking clock movement as in-fiction rewind after LT03.
3. At 1280x800, testers identify all sites covered by a selected footprint and any conflict without zoom in >=95% of trials.
4. Controller-only LT01–LT06 completion requires no pointer-like precision and no focus traps.
5. Reason trace lets testers correctly explain a failure cause in LT05 without external help.
6. Compare no-consequence-preview baseline against explicit one-beat preview; reject explicit preview if it materially increases hover-scanning or lowers causal explanation quality.
7. Reduced Motion + animation skip preserve every authoritative state cue.

## 20. Explicit UX exclusions
No timeline scrubber; no rewind iconography; no predicted multi-beat path; no winning-socket highlight; no auto-solver hint in base UI; no continuous clock animation implying ticking; no hidden hover-only rule; no color-only footprints; no mandatory drag precision; no modal stack required to compare two sites; no decorative occlusion of logic.

## 21. Phase result
Phase 6 locks first boot/progression, play-screen hierarchy, mouse/keyboard/controller paths, exact footprint/conflict language, NOW-vs-DONE presentation, rule cards, anti-oracle preview baseline, Resolve/reason-trace sequence, recovery/failure language, camera/Deck readability, accessibility/settings/interruption behavior and LT01–LT06 onboarding.

No contradiction with Phase 4 or Phase 5 was introduced.

**PHASE 6 UX / PRESENTATION ARCHITECTURE = COMPLETE.**

# NEXT DESIGN STEP — PHASE 7 COMMERCIAL MODEL
Use fresh current web research. Create `GAME18_COMMERCIAL.md`. Lock target premium price/range, realistic campaign/mastery playtime, demo packaging and save carryover, launch platform/features, achievement philosophy, replay/efficiency incentives, difficulty/accessibility relationship, discount/bundle assumptions, localization scope, wishlisting/Next Fest/demo positioning, and explicit monetization boundaries. Re-test whether 36+12 remains commercially justified versus a smaller stronger package. Do not begin production implementation.