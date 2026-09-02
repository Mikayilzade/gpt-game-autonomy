# GAME #015 — PHASE 6 UX / PRESENTATION ARCHITECTURE

Date: 2026-09-03
Status: PHASE 6 COMPLETE
Working title: **FRESH COAT**
Design complete: NO

## 0. Authority and boundary
This file freezes the player-facing experience implied by Product Thesis, Mechanical Architecture and Content Architecture. It does not reopen puzzle truth, add mechanics, or begin production implementation.

Gameplay truth remains exact semantic exposure/history over discrete poses. Camera, rendering, animation, audio and input only expose or manipulate that truth; none may create hidden gameplay state.

Fresh Steam/Steam Deck guidance checked 2026-09-03. Relevant constraints carried into this specification: complete controller access, device-appropriate glyphs, no controller-hostile launcher/text-entry dependency, readable handheld UI, and a playable default Deck configuration. Steamworks currently cites 30 fps at 800p as the Deck compatibility performance floor and requires Deck-readable text; this game's own target is stricter where practical because the scene is visually simple.

## 1. Player-facing screen model
The core puzzle screen has four persistent semantic surfaces:
1. **Work area** — stable 3D booth/table view containing the active objects and authored sockets.
2. **Target rail** — compact per-object final history requirements.
3. **Stage rail** — current stage (`Arrange A`, `Spray A`, `Rearrange`, `Spray B`, `Reveal`) and immutable coat order.
4. **Action strip** — current valid actions with device-correct glyphs.

No solver matrix, exposure list, solution heatmap, minimap, inventory grid or abstract CSP view is shown in normal play.

The target rail and stage rail must remain visible without covering the object silhouettes at 1280x800. On smaller/handheld layouts they may collapse to icon-first compact mode, but all target truth must remain reachable within one button press.

## 2. Stable camera and inspection

### 2.1 Canonical camera
Every case ships with one authored canonical perspective chosen to make the active socket motif and booth direction readable.
- camera truth never affects exposure;
- no puzzle requires discovering a hidden face by free camera hunting;
- initial view must show all active object silhouettes and primary sockets;
- the booth direction is represented in world space by a large fixed nozzle/arrow frame, not inferred from lighting.

### 2.2 Comfort orbit
A bounded optional orbit is allowed for comfort and spatial understanding only.
- yaw: approximately +/-35 degrees from authored center;
- pitch: approximately -10 to +25 degrees from authored center;
- no free roll;
- no zoom below the minimum semantic-face legibility threshold;
- camera automatically recenters on request.

If any solution becomes materially easier only from a noncanonical camera angle, content review must verify that the same factual relation is accessible through semantic inspection; camera angle cannot become a hidden clue.

### 2.3 Object isolation
Selecting an object allows **Inspect Object**:
- selected object remains fully opaque;
- other objects become neutral translucent silhouettes while preserving their current spatial positions;
- authored semantic regions on the selected object receive subtle boundary lines and stable labels/icons;
- actual accumulated coat-history badges remain visible;
- current blockers may be outlined, but blocker identity is not named as correct/incorrect.

Isolation is factual, not counterfactual. It does not move anything, show alternate poses, expose future stage state, or reveal which socket should be chosen.

### 2.4 Semantic-face browser
Every targeted region is reachable from a semantic region list associated with its owning object. Selecting a region focuses/highlights it in the 3D view and displays:
- region identity;
- required final history;
- actual history already accumulated;
- current exposure status for the active pre-spray arrangement, if exposure preview is enabled.

This browser guarantees accessibility to hidden/cavity targets without x-ray camera hunting.

## 3. Visual language

### 3.1 Object identity
Object identity matters whenever targets differ. Use a redundant trio:
- distinct silhouette/archetype;
- simple object marker glyph (e.g. square/triangle/stripe family);
- short stable display label only when needed (`Piece A`, `Piece B`) and localizable.

Never rely on hue alone to distinguish objects.

### 3.2 Coat identity
Main campaign coat identities are **A** and **B**, each represented by:
- high-contrast color;
- distinct surface pattern/texture;
- stable letter/symbol badge.

Recommended semantic pattern families: A = diagonal hatch; B = dotted/grid pattern. Exact art may vary, but they must remain distinguishable in grayscale and common color-vision deficiencies.

`A_THEN_B` must not be shown merely as the final B appearance. Its badge/history strip shows `A -> B`, and the surface treatment may carry a subtle combined edge motif. Ordered truth is always available textually/iconically.

### 3.3 Exposure preview
Before SPRAY, optional factual preview marks semantic regions as:
- **EXPOSED NOW**: animated/static nozzle-facing hatch rim;
- **PROTECTED NOW**: neutral shield/occluded rim.

It must not color exposure as good/bad relative to the target. Example: a target RAW region that is currently exposed is still labeled only `EXPOSED NOW`, never red/wrong.

Preview is ON by default for FC01–FC05. From FC06 onward the player may keep it on permanently; it is an accessibility/readability tool, not a difficulty option.

### 3.4 Target cards
Each object has a compact target card showing only targeted regions. Every row contains:
`region pictogram/name | required history badge`.

Cards can expand to a face diagram for players who prefer diagrammatic inspection. Diagram regions must correspond exactly to semantic region IDs and never imply pixel-level paint coverage.

## 4. Controller-first input model
All game content must be completable with a conventional controller and default Steam Deck controls. Mouse/keyboard is an equal path, never a superset.

### 4.1 Gameplay action vocabulary
Abstract actions, not physical buttons, are authoritative:
- `NavigateObject`
- `NavigateSocket`
- `CyclePose`
- `PlaceOrSwap`
- `InspectObject`
- `ToggleExposurePreview`
- `OpenTargets`
- `CommitSpray`
- `Undo`
- `ResetCase`
- `RecenterCamera`
- `OrbitCamera`
- `Pause`
- `Confirm`
- `Cancel`

Controller glyphs must reflect the active device where platform APIs allow. Steam Input support should use in-game actions and official controller configuration rather than hard-coding Xbox-only prompts.

### 4.2 Recommended controller behavior
- Left stick/D-pad: move selection among objects/sockets/menu items using authored spatial navigation graph.
- Right stick: bounded comfort orbit.
- Confirm: pick/place or confirm highlighted legal socket.
- Shoulder buttons: cycle legal poses/orientations for selected object.
- Face action: inspect/isolate selected object.
- Face action: target rail/details.
- Trigger or explicit face action: `SPRAY` commit only when stage permits.
- Undo: dedicated easily reached action.
- Reset: pause/menu action, never adjacent to Spray without confirmation.

Exact physical binding remains implementation-flexible and remappable; the semantic separation is frozen.

### 4.3 Selection flow
Controller manipulation uses a two-step state:
1. select workpiece;
2. valid destination sockets become visually emphasized;
3. move focus among only legal destination sockets;
4. cycle only legal poses for that object/socket;
5. confirm placement atomically.

Illegal placements are not accepted and do not generate error spam. If a socket is incompatible, it may remain visible but subdued with a concise reason on focus (`Piece does not fit this fixture`) only when useful.

The player may freely continue editing the current arrangement before Spray. There is no move counter.

### 4.4 Mouse/keyboard
Mouse may directly click object/socket and drag only as a presentation shortcut. Drag release must snap to the same authored legal pose set as controller navigation; continuous world coordinates never become state.

Keyboard navigation must expose the same abstract actions and allow complete play without mouse.

### 4.5 Mixed-input behavior
Switching between mouse/keyboard and controller must be seamless. Prompts update to the most recently active device without modal interruption. Mixed-device input must not reset selection or camera.

## 5. Spray commit and transition UX

### 5.1 Pre-commit
`SPRAY A/B` is visually dominant but cannot be triggered accidentally while a placement transaction is in progress. The action strip states the immutable coat identity and current stage.

For FC01 only, first-ever spray may show a one-time micro-confirmation: `Paint every region exposed to the booth now?` with a 2-frame visual preview. After that, no routine confirmation dialog is used; replay/undo is the safety net.

### 5.2 Commit
On Spray:
1. controls that alter arrangement lock atomically;
2. camera recenters if materially off-axis, unless reduced-motion mode skips movement;
3. booth pulse/nozzle sweep communicates the fixed direction;
4. exposed semantic regions receive coat treatment simultaneously or in a short deterministic wipe;
5. newly accumulated history badges update;
6. branch checkpoint is created conceptually by the mechanical system;
7. stage rail advances.

Animation length target: roughly 0.8–1.8 seconds normal mode, always skippable after first viewing. No animation timing affects truth.

### 5.3 A -> B rearrangement transition
After Spray A in two-stage cases:
- stage rail visibly locks `A` as completed;
- target cards may show actual A histories, not judgment;
- booth label changes to B and authored B direction if different;
- scene remains in exact A arrangement until player moves objects;
- available sockets/poses update to legal stage-B domains;
- no automatic rearrangement occurs.

If a case has no meaningful B edit, content is suspect; Phase-5 authoring gate should reject it unless explicitly tutorialized.

## 6. Unpack / result reveal
The final reveal is the emotional payoff and proof surface.

### 6.1 Reveal sequence
After final spray:
1. `UNPACK / REVEAL` becomes the only forward action;
2. objects separate into a clean authored display row/grid without changing their semantic orientation labels;
3. each targeted region displays required and actual history;
4. correct regions resolve quietly;
5. failed regions remain highlighted with factual discrepancy badges;
6. overall result appears only after per-region truth is visible.

Success language: concise, e.g. `All pieces match.`
Failure language: `3 regions differ.` rather than `Wrong arrangement.`

### 6.2 Failure explanation
Selecting a failed region shows only:
- required history;
- received history;
- actual stage(s) when it was exposed/painted;
- optional replay of the player's committed spray result.

Forbidden: intended blocker, correct socket, correct pose, comparison to nearest solution, percentage closeness, or move recommendation.

### 6.3 Post-result actions
Failure: `Undo Last Spray`, `Return to A Arrangement` where mechanically valid through undo chain, `Reset`, `Targets`, `Replay Attempt`.
Success: `Next Case`, `Replay`, `Case Select`, and optional `View Solution History` showing only the player's successful A/B arrangements.

## 7. Undo/reset/checkpoint UX
- Undo is always visible in the action strip when available.
- Arrangement edits before spray undo one placement transaction at a time.
- Undo across Spray restores the exact prior editable checkpoint defined mechanically.
- Holding Undo may open a tiny factual branch breadcrumb (`Before Spray B`, `Before Spray A`) but never solution alternatives.
- Reset requires confirmation only after at least one spray commit; before any commit it may reset instantly.
- Leaving a puzzle uses the persistence rules defined later; resume must label whether the player is `Before Spray A`, `Between A and B`, or `After Spray B / Reveal`.

No score, star rating or achievement is reduced by undo/reset.

## 8. Menus and navigation

### 8.1 Main menu
Minimal:
- Continue
- Case Select
- Settings
- Accessibility
- Credits
- Quit (desktop platforms)

No launcher required for gameplay settings.

### 8.2 Case select
24 cases arranged by F1–F8 groups. Show:
- case ID/title;
- completion state;
- family icon;
- demo/full entitlement state if relevant.

Do not show numeric difficulty ratings that imply a false linear scale. Later cases naturally unlock via progression.

### 8.3 Pause
Pause freezes presentation immediately and offers Resume, Targets, Controls, Settings, Restart Case, Case Select, Main Menu. Since gameplay has no timers, pause never changes puzzle state.

## 9. Save/load/resume surface
Autosave points:
- case completion;
- spray checkpoints;
- leaving a puzzle;
- settings/accessibility changes.

The UI must distinguish progress persistence from puzzle-state persistence. Continue resumes the most recent in-progress case unless that state is invalid/corrupt, in which case recovery falls back to the most recent valid committed checkpoint and reports this plainly.

No player-facing manual save-slot management is needed for the baseline product. A single campaign profile plus platform cloud sync is sufficient unless Phase 8 identifies a technical reason otherwise.

## 10. Onboarding FC01–FC05

### FC01 — direct mask
Teach by affordance, not paragraph:
- target card pulses RAW and A target examples;
- selectable object -> valid socket -> pose;
- exposure preview automatically on;
- first Spray micro-confirmation;
- reveal explicitly pairs `needed RAW / received RAW` and `needed A / received A`.

### FC02 — pose
Introduce pose cycling only when selecting the target object. One short prompt: `Turn the piece to change which face sits behind the mask.`

### FC03 — masker has own target
Target rail now includes both objects before any new prompt. If player ignores masker's target and fails, reveal naturally demonstrates the rule. Optional hint can point to the masker's target card, not the correct pose.

### FC04 — neighboring regions
Introduce semantic subregion boundary styling and region focus. No new input.

### FC05 — compare blocker footprint
No tutorial prompt by default. This is the first case expected to be solved using inspection plus physical prediction with minimal guidance.

By the end of FC05, normal gameplay UI is fully taught except two-pass stage flow, ordered history and cavity-specific inspection, each introduced when mechanically relevant.

## 11. Later concept introductions

### FC06/FC10 — two-stage flow
FC06 may foreshadow future-access reasoning. FC10 is the clean canonical two-coat tutorial: stage rail visibly shows `A -> rearrange -> B` before play. The player cannot change order.

### FC13 — ordered history
First A_THEN_B requirement receives one explicit history animation/badge explanation. Never describe it as final mixed color; teach `this region must be exposed on both passes, in this order`.

### FC16 — cavity
Region browser demonstrates that cavity floor/rim are ordinary semantic regions. A one-time isolation hint may show the aperture relation, but no x-ray solver view.

## 12. Demo structure and skip handling
Recommended canonical demo remains a curated subset of full campaign cases, not parallel content. Exact subset may be refined commercially, but must include representative milestones through two-pass/A_THEN_B play.

If demo-to-full carry-over skips full-game cases such as FC07, FC10 or FC13 depending on final subset/order, the full game performs **knowledge checks**, not duplicate tutorial rules:
- entering a case whose prerequisite tutorial was not completed triggers the same concise mechanic card used originally;
- the player may open `How This Works` cards from pause/targets at any time;
- there are no demo-exclusive mechanics or flags that alter case truth.

Progress import records completed case IDs and tutorial-card acknowledgements separately.

## 13. Hint system
Hints are optional, non-consumable, and never monetized. They are derived from designer-reviewed proof metadata but must be authored as escalating conceptual nudges rather than exposing certifier state.

Three maximum tiers per eligible case:
1. **Goal-focus hint** — names the relevant obligation class (`One face must avoid A entirely.`).
2. **Relationship hint** — names the kind of spatial dependency (`The piece that protects X also has to receive A itself.`).
3. **Proof-step hint** — states one necessary factual elimination (`Any A arrangement that exposes X.side cannot work.`).

Forbidden even at tier 3:
- correct socket ID;
- exact pose/orientation;
- full A/B arrangement;
- intended blocker name when that identity is itself the deduction;
- solver-generated nearest solution.

Hints may mark a target region referenced by the text, because that is already known target truth.

## 14. Accessibility freeze
Required baseline options/features:
- coat identity never color-only;
- object identity never color-only;
- scalable UI/text with at least 100/125/150% presets or continuous equivalent;
- handheld layout tested at 1280x800;
- smallest essential UI text must remain comfortably above platform minimum legibility; target approximately 18–24 px effective at 1280x800 for normal labels, with larger headings/action prompts;
- reduced motion: disable camera swoops, shorten spray/unpack transforms, replace with fades/snap transitions;
- optional screen shake OFF by default or absent;
- full control remapping target;
- independent camera sensitivity and invert options;
- no hold/repeated rapid-input requirement for puzzle completion;
- no timed decisions;
- audio never carries unique puzzle truth;
- captions/subtitles for any voiced/flavor audio if added later;
- high-contrast selection-outline option;
- exposure-preview intensity option without changing truth;
- target card diagram + textual history badges available together;
- all menus and puzzle actions controller reachable.

Accessibility cannot reveal counterfactual solution truth. It may improve readability of already factual state without being treated as cheating.

## 15. Audio and haptics language
Audio supports state, never rule discovery.
- selection: quiet tactile click;
- legal snap/place: mechanical fixture clack;
- illegal/incompatible focus: subtle neutral tick, not failure buzzer;
- Spray: short compressed-air burst tied to fixed booth action;
- coat application: material swish;
- reveal: layered unpack clicks;
- success: restrained confirmation chord;
- failure: neutral discrepancy tone, not punitive alarm.

Haptics, when available:
- light pulse on snap;
- medium short pulse on Spray commit;
- subtle reveal ticks per object.

All haptics independently disableable. No haptic-only information.

## 16. First 10 minutes / first session walkthrough

### Minute 0–2
Boot -> controller/mouse immediately works -> Continue/New Game. FC01 opens directly with two objects, one target card, one booth direction. Player selects, snaps blocker, sees factual exposure preview, sprays, unpacks.

### Minute 2–5
FC02 introduces rotate/cycle pose. FC03 reveals that the masking object itself has a target. Target cards and isolation become familiar through use rather than a modal tutorial sequence.

### Minute 5–10
FC04/FC05 introduce neighboring semantic regions and comparing blocker footprints. By now the expected mental language is: `What is exposed? What must stay protected? What does the mask itself need?`

Target first-session end around FC06–FC08 for a new player, depending on pace. The session should end after a meaningful self-obligated/dependency solve, not after a rules dump.

## 17. Steam Deck / handheld validation contract
Fresh Steamworks guidance checked 2026-09-03 and translated into product requirements:
- every game/menu action accessible using default controller configuration;
- on-screen glyphs match active controller/device where supported;
- no mouse/keyboard-only launcher or mandatory text entry;
- UI readable at 1280x800 and at handheld viewing distance;
- default graphics configuration must be playable on Deck-class hardware; Valve's compatibility floor is 30 fps at 800p, while Fresh Coat should target stable 60 fps on Deck-class hardware in normal scenes because render complexity is low, with 30 fps remaining an acceptable fallback mode if implementation evidence requires it;
- mixed controller/mouse input supported cleanly;
- gamepad disconnect pauses or leaves the puzzle in a safe non-changing state;
- no puzzle truth depends on hover, tiny cursor precision or right-click context menus.

Phase 8 must translate these UX obligations into exact runtime/input/performance acceptance tests.

## 18. UX anti-drift / rejection gates
Reject or reopen any implementation/content proposal that causes:
1. camera hunting to discover required target truth;
2. continuous placement or precision dragging becoming strategically necessary;
3. exposure preview judging good/bad rather than factual exposed/protected;
4. target UI leaking solver facts;
5. color being the only coat/history cue;
6. four-object scenes requiring permanent x-ray/exploded view to reason;
7. hidden compatibility states not communicated by socket affordance;
8. a binary Check-spam loop during arrangement;
9. a second input system for mouse that has capabilities controller lacks;
10. result reveal delaying or obscuring exact per-region discrepancies;
11. tutorial variants creating rules absent from the main campaign;
12. accessibility options changing puzzle truth rather than readability.

## 19. Phase-6 acceptance test
Phase 6 passes because another session can now build the entire player-facing interaction without inventing:
- canonical camera/inspection behavior;
- controller and mouse interaction semantics;
- factual exposure and target-history presentation;
- Spray/rearrangement/reveal flow;
- failure/undo/reset behavior;
- menu/progression/resume surfaces;
- tutorial sequencing;
- hint boundaries;
- accessibility requirements;
- audio/haptic feedback roles;
- handheld/controller validation obligations.

No contradiction requiring Product/Mechanical/Content reopening was found.

PHASE 6 = COMPLETE
DESIGN COMPLETE = NO

## NEXT ACTION — PHASE 7 COMMERCIAL MODEL / RETENTION / PLATFORM PACKAGE
Re-read all active Game #015 authority and define the finite premium commercial package without retention-system drift. Required: current market/pricing analogue research; price hypothesis/range; campaign value proposition; demo exact packaging and carry-over policy; Steam achievements and platform-feature boundaries; progression/unlock pacing; optional replay/completion incentives; difficulty/hint positioning; localization/store-page implications; launch/content-expansion boundaries; and explicit monetization exclusions. Then determine whether Phase 8 Technical Specification can begin in the same or next run. Do not begin production implementation.