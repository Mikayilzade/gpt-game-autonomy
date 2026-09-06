# GAME #018 — PHASE 6 UX / PRESENTATION ARCHITECTURE

Date: 2026-09-06
Game: **LOCAL TIME**
Status: PHASE 6 COMPLETE — PHASE 7 COMMERCIAL MODEL NEXT
Production implementation: NO

Authority: `GAME18_PRODUCT_THESIS.md`, `GAME18_MECHANICS.md`, and `GAME18_CONTENT.md`. This file specifies interaction/presentation only and does not add gameplay grammar.

## 1. UX thesis
The player must always distinguish three questions without opening a manual:
1. **NOW** — what local-time conditions are true in the current placement;
2. **DONE** — what persistent milestones have already been earned;
3. **LOCKED OUT** — what irreversible harmful states have occurred.

The town remains the primary interface. Panels explain the diorama; they do not replace it with a timeline editor.

## 2. Screen hierarchy
Baseline 16:9 / Steam Deck 1280x800 layout:
- central 70–80%: fixed/lightly pannable diorama;
- top-left: compact objective card, always visible, with persistent/current clauses separately marked;
- top-center/right: clock-zone selector showing label, footprint glyph, move budget;
- bottom: contextual focused-site/rule strip and Resolve action;
- optional collapsible reason-trace drawer after Resolve.

No permanently open multi-column rule spreadsheet. At 1280x800 the board, clock labels, objective summary and Resolve state must remain simultaneously readable.

## 3. Clock-zone language
Each movable zone has redundant identity cues: large clock label text, unique border pattern/glyph and distinct physical clock-body silhouette when practical. Color may reinforce identity but is never the sole cue.

A zone footprint is a translucent ground patch with a crisp patterned perimeter. Covered relevant sites gain a small matching local-time badge at their base. Overlap of footprints is shown geometrically; an illegal ambiguous site receives a striped conflict badge and placement cannot be committed.

Fixed local time uses the same label grammar but an anchored landmark/ground ring so it cannot be mistaken for movable coverage.

## 4. Placement flow and preview boundary
### Mouse
Select/drag a clock or click its selector -> legal sockets appear. Hovering a socket shows the exact footprint and covered site badges. Click commits; Esc/right-click cancels.

### Controller / Steam Deck
Shoulder buttons cycle clocks. Confirm enters placement mode. D-pad/left stick moves among legal sockets using authored spatial neighbors; selected socket pulses. Confirm commits; cancel restores previous placement. Right stick or triggers may lightly pan/zoom but are never required to solve.

### Preview rule
Before commit the UI shows only:
- exact footprint and sites receiving the clock label;
- resulting **current** predicates (`Bridge: OPEN now`, `Station: 08:05 now`);
- illegal overlap/conflict;
- public risk icon if a covered site's currently visible rule says this label can cause a permanent lockout on Resolve.

It does **not** automatically enumerate state transitions that would occur on Resolve, show future beats, rank sockets, display success probability, or expose a multi-beat path. Players may inspect the site's public rule themselves.

Reason: automatic one-beat outcome scanning across every socket would turn informed reasoning into UI enumeration. This is a frozen baseline; a prototype may reopen only if LT02 comprehension fails badly.

## 5. NOW / DONE / LOCKED OUT presentation
**NOW/current:** animated local badge + live environmental pose, e.g. bridge physically open; disappears/changes immediately when planning placement changes.

**DONE/persistent:** durable transformed object silhouette/state plus small filled milestone pip. Moving the clock never plays reverse animation.

**LOCKED OUT/permanent risk:** durable terminal visual (closed/wilted/etc.), warning-shaped marker, and explicit `Permanent` text in detail panel. Never communicate only with red.

When an earlier-looking label moves over a completed object, the persistent visual remains unchanged. No rewind VFX, reverse particles, backward clock spin or timeline scrub metaphor is permitted.

## 6. Site inspection
Hover/focus a site to show one compact card:
- landmark name;
- current local time (`NONE` allowed);
- current finite state;
- relevant public rule(s) for that state;
- earned persistent milestone(s);
- permanent risk/terminal status;
- carrier endpoint status if relevant.

Rule wording uses condition -> consequence, e.g. `At 08:00 + RAW -> becomes RISEN on Resolve` or `At 08:05 while unprotected -> permanently CLOSES on Resolve`.

## 7. Resolve interaction and animation
Resolve is a dedicated, visually stable action with current beat count when budgeted. Confirming Resolve never hides an unexpected cost.

The canonical state transition is computed first; animation only presents it. Target normal presentation: 0.8–2.5 seconds, with fast-animation option reducing it to ~0.2–0.6 seconds and skip-after-computation permitted.

Presentation order mirrors mechanical reason order: current conditions light -> permanent risks -> beneficial transitions -> accept/dispatch -> carrier handoff -> objective result. Simultaneous logical commits may be visually staggered for readability but the trace labels them as same Resolve.

## 8. Reason trace
After each Resolve, changed entities produce concise ordered entries such as:
- `08:00 covers Bakery -> Dough RAW became RISEN.`
- `08:05 covers Flower while unprotected -> Flower permanently CLOSED.`
- `Station 08:05 + Bridge OPEN -> Tram DISPATCHED.`

No-change Resolve says `No state changed.` and, when relevant, `Resolve 3/4 used.`

Trace can be expanded, replayed or ignored. Selecting an entry focuses the affected site. Trace is explanation, not a hint generator and never contains future advice.

## 9. Objective language
Objective clauses use explicit state class:
- `DONE: Bread is BAKED`
- `NOW: Bridge is OPEN`
- `DONE: Parcel ACCEPTED`
- `AVOID: Flower permanently CLOSED`

Completed persistent clauses stay checked. Current clauses visibly turn on/off as placements change. This prevents a generic checklist from implying all conditions persist.

## 10. Permanent-risk warnings
Warnings are factual, not predictive strategy advice. If the currently previewed coverage matches the visible trigger of an unresolved permanent-risk rule, the affected site receives a warning glyph and its rule card is surfaced. The UI may say `Permanent consequence on Resolve` but not `Bad move` because the exposure may be intentionally valid in another solution.

On the first such event (LT02/LT05 teaching sequence as authored), Resolve may require one acknowledgement the first time in the profile. Thereafter no confirmation spam.

## 11. Carrier presentation
Carriers move only after computed Resolve. Route/endpoints are public and visually marked. A payload icon stays attached to its canonical location. Arrival shows `ARRIVED — acceptance requires a later Resolve` when default semantics apply. The UI never animates multiple logical route steps merely for flourish.

## 12. Undo / restart / replay semantics
`Undo Move`: restores the preceding planning placement and move counter; wording never says rewind.

`Undo Resolve`: restores exact pre-Resolve canonical checkpoint. Confirmation is unnecessary in normal play; the UX calls it `Undo Resolve`, never `rewind time`.

`Replay`: presentation-only; replay button is visually grouped with trace, not Undo.

`Restart Case`: instant reset with confirmation only after meaningful progress; setting may disable confirmation.

Leaving a case saves the canonical post-Resolve checkpoint plus current committed planning placement when safe. Animation progress is never saved as authority.

## 13. Save/load and recovery UX
Autosave after every successful Resolve and case completion, using atomic save semantics to be specified technically in Phase 8. Case select displays completion/mastery status and latest checkpoint.

On incompatible/corrupt checkpoint, never partially reconstruct state. Preserve the profile, offer restart of that case, and surface a plain recovery message. Save failures must not masquerade as puzzle failures.

## 14. Failure and DEAD communication
Hard fatal lockout: affected object/site shows permanent terminal state; if objective is now impossible by authored fatal rule, banner `Case cannot be completed from this state` with `Undo Resolve` and `Restart`.

Budget exhausted: exact unmet clauses are highlighted.

Solver-certified dead state may use the same impossibility language only after exact certification. A heuristic hint may instead say `Review your remaining moves` but never claim deadness.

Failure screen never obscures the board before the player can inspect why.

## 15. LT01–LT06 onboarding
Tutorial uses short contextual prompts, then removes them permanently after demonstrated action. No separate rule encyclopedia is required to begin.

**LT01:** highlight clock -> socket -> footprint. First Resolve teaches `NOW` vs `DONE`; after moving clock away, explicitly point once to RISEN staying DONE while bridge becomes NOW OPEN.

**LT02:** introduces a permanent-risk card and first factual risk warning. After success/failure, one sentence reinforces that clock labels are local conditions, not a global timeline.

**LT03:** introduces second clock and simultaneous NOW clauses. Objective visually groups Bridge OPEN + Station 08:05 with `same Resolve` bracket.

**LT04:** carrier route and stage strip: PREPARE -> DISPATCH/HANDOFF -> ARRIVE -> ACCEPT. Stages are process semantics, not elapsed time. Arrival explicitly teaches later-Resolve acceptance.

**LT05:** removes most tutorial prompts. First case where warning information is sufficient but ordering must be reasoned. Failure trace points to the exact permanent rule.

**LT06:** full normal HUD. No guided placement. Completion screen asks no quiz; the game trusts demonstrated solving.

If playtests show players still describe the system as rewind/time travel after LT02, repair wording/VFX before adding explanation volume.

## 16. Pause, settings and case navigation
Pause menu: Resume, Rules/Controls, Restart Case, Case Select, Settings, Quit.

Settings baseline:
- master/music/SFX volume;
- animation speed + skip Resolve animation;
- camera motion reduction;
- screen shake off by default or minimal;
- text size / UI scale presets;
- high-contrast footprint mode;
- pattern labels always-on option;
- subtitle/text-display controls for any voiced material;
- controller remapping and keyboard remapping;
- hold/toggle behavior where relevant.

Case select shows chapters, completion and optional mastery goals without grading normal solutions by shortest path.

## 17. Accessibility baseline
Core information is redundant across text/icon/pattern/shape, never color-only or audio-only. Full puzzle completion requires no hearing. Resolve audio has matching visual cues.

No timed input, precision dragging or rapid repetition. Controller path reaches every action. Mouse drag always has click-select/click-place equivalent. Focus order is deterministic.

Text avoids tiny labels embedded only in world art; critical time labels and states have UI-scale-aware overlays. High-contrast mode strengthens footprint borders and site badges without changing logic.

Motion-reduction mode replaces large camera/clock movement with short fades/snaps while preserving causal order. Fast animation does not skip reason traces.

## 18. Camera and visual-density rules
Camera is authored per case with modest optional pan/zoom. Default framing must contain every logically relevant site for normal cases when possible. A case that requires constant camera hunting fails the content readability gate.

Decorative townspeople/traffic may exist only if they cannot be confused with logical carriers or state. During placement/Resolve, irrelevant motion should quiet rather than compete with causal feedback.

At <=8 relevant sites, every relevant landmark needs a unique readable silhouette or persistent label at target display size.

## 19. Audio thesis
Soft town ambience supports charm; each semantic event has a short optional earcon, but no rule depends on pitch/rhythm recognition. Clock-zone placement uses distinct but non-semantic tactile sounds; persistent milestone and permanent lockout sounds differ in contour and have simultaneous visual equivalents.

No ticking ambience that suggests continuous elapsed time as a mechanic.

## 20. Empirical UX gates
Implementation prototypes must test:
1. >=80% of first-time testers can explain NOW vs DONE after LT02 without facilitator correction;
2. testers do not infer that moving to an earlier-looking label reverses completed history;
3. LT03 two-zone overlap/current state is readable at 1280x800 and in non-color mode;
4. controller users can select any clock/socket/site without pointer emulation;
5. risk warning informs without being interpreted as a forbidden move;
6. absence of automatic transition preview does not cause rule-memory friction; if it does, test an opt-in one-beat preview, but reject it if players solve mainly by socket scanning;
7. Resolve animation at default speed communicates ordering; fast mode remains understandable via trace;
8. carrier arrival/later acceptance is understood in LT04.

## 21. UX acceptance
Phase 6 fixes the town-first information hierarchy, clock/footprint language, NOW/DONE/LOCKED OUT state grammar, exact preview boundary, Resolve/reason-trace flow, objective/risk/carrier communication, mouse/controller/Deck paths, LT01–LT06 onboarding, recovery semantics, accessibility, camera density and empirical gates.

**PHASE 6 UX / PRESENTATION ARCHITECTURE = COMPLETE.**

# NEXT DESIGN STEP — PHASE 7 COMMERCIAL MODEL
Use fresh September 2026 research. Lock premium price band and launch price, expected campaign/mastery duration, demo content/length and save carryover, Steam/Deck/Cloud/achievements/localization expectations, discount/launch strategy boundaries, and re-evaluate whether 36+12 remains commercially/content-wise justified versus a smaller higher-quality package. No ads, MTX, live-service or production implementation.