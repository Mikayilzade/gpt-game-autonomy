# GAME #009 — PHASE 6 UX / PRESENTATION ARCHITECTURE

Status: **PHASE 6 COMPLETE / PHASE 7 READY**
Date: 2026-08-31
Selected game: **Binder's Imposition**
Production implementation: **FORBIDDEN in factory**

Authority: `START_HERE.md` -> `STATUS.md` -> `GAME_INDEX.md` -> Game #009 tournament history -> `GAME9_PRODUCT_THESIS.md` -> `GAME9_MECHANICAL_ARCHITECTURE.md` -> `GAME9_CONTENT_ARCHITECTURE.md` -> this file.

This file defines the complete player-facing interaction and presentation contract. It may externalize or accelerate already-learned mechanics, but it may not change solution validity, invent new fold transforms, add hidden information, or let presentation timing become gameplay authority.

---

# 1. UX thesis

Binder's Imposition must make a mathematically exact permutation puzzle feel tactile without making the player fight a simulation UI.

The player should feel that they are manipulating physical sheets, but mechanically they are editing finite slots and bounded signature roles. Therefore:

- every visually rich action maps to one exact reversible transaction;
- every important property has a redundant icon/text representation and never depends on color alone;
- Fold Preview is fast, repeatable and non-mutating;
- animation explains the transform but never hides state or delays expert iteration;
- the workbench always exposes both **source state** (flat sheets) and **goal/final-state requirements**;
- final-book inspection explains consequences, not solutions;
- controller interaction reaches every action without requiring pointer emulation;
- mouse may be faster but is not mechanically privileged;
- no interaction requires dexterity, timing, dragging precision or holding a button for an exact duration;
- no tutorial modal blocks harmless experimentation after the first required gesture;
- the UI progressively externalizes clerical mappings after comprehension is demonstrated so late-game thought is spent on global constraints.

The UX target is: **think globally, manipulate locally, verify physically, understand exactly.**

---

# 2. Global screen / state flow

Canonical player-facing flow:

`BOOT -> TITLE -> PROFILE/CONTINUE -> CAMPAIGN MAP -> CASE BRIEF -> WORKBENCH -> [FOLD PREVIEW <-> WORKBENCH] -> COMMIT RESULT -> CASE COMPLETE -> CAMPAIGN MAP/NEXT CASE`

A suspended in-progress case may enter via:

`BOOT -> CONTINUE -> RECOVERY CHECK -> WORKBENCH`

## 2.1 Boot

Boot requirements:
- no unskippable logo sequence longer than 2 seconds total;
- any logo/splash can be skipped by any confirm/cancel/pointer input after first frame;
- load settings before showing interactable title UI so text scale, reduced motion and input glyph preference apply immediately;
- if a previous session ended during a case, show `Continue Case` as primary action;
- if no save exists, show `Start` as primary action.

No launcher is required by product design.

## 2.2 Title

Primary actions:
- Continue Case / Continue Campaign;
- Start / Case Select after first completion;
- Settings;
- Accessibility;
- Credits;
- Quit on desktop where platform conventions allow.

The title screen must communicate the hook visually with a looping **flat -> fold -> correct booklet** vignette. This loop is presentation-only and does not autoplay audio at disruptive volume.

## 2.3 Campaign map

The campaign map is deliberately compact, not a world map.

Layout:
- six chapter bands;
- case cards in authored sequence;
- solved, available, locked states;
- optional badge completion shown secondarily;
- current recommended next case receives one obvious focus treatment;
- chapter teaching summary available on demand but not required to enter a case.

Case card shows:
- case number/title;
- 1–3 compact mechanic icons for what it reinforces;
- solved state;
- optional badges only after badges have been introduced;
- best effort stats only if Phase 7 later decides they serve retention without encouraging grind.

No star-rating economy is implied by Phase 6.

## 2.4 Case brief

The brief has three blocks:
1. **Finished book request** — the required final relationships in player language;
2. **Available material** — signatures/templates/locked setup;
3. **New idea** — only when the case introduces a mechanic.

The player may expand a `Rules` drawer containing already-unlocked definitions. The brief must never require remembering industry terms.

`Begin` enters the workbench. Returning to the campaign map from an unsolved case invokes normal save rules rather than discarding silently.

## 2.5 Workbench

The workbench is the main game screen and must support the entire solve loop without modal navigation.

## 2.6 Fold Preview

Preview temporarily changes presentation state, not canonical editable state. Entering/exiting preview never adds history.

## 2.7 Commit result

Commit has three possible player-facing outcomes:
- illegal setup: submission remains disabled and reasons are visible inline before Commit;
- legal but incorrect: result explanation lists all failed required predicates and offers immediate return to the exact layout;
- success: result sequence confirms every required predicate, then offers Next Case / Replay / Campaign Map.

Success presentation may celebrate but cannot delay control for more than a short skippable beat.

---

# 3. Workbench layout

The default 16:9/16:10 arrangement uses four persistent zones.

## 3.1 Zone A — Goal / predicate rail

Left rail on wide screens; top drawer alternative on narrow aspect ratios.

Contains each required predicate as a human-readable card with:
- icon;
- concise localized sentence;
- involved face/signature tokens;
- state during Preview/Commit inspection: `satisfied / failed / not currently evaluable`;
- expandable explanation of the rule definition, not solution advice.

Important rule: while editing flat sheets, required predicates do **not** continuously turn green/red based on hidden full solver evaluation. That would create a monotonic hill-climbing oracle. Predicate truth is revealed only when it is directly observable from the current resolved Preview or after Commit. The source setup may still show legality problems immediately.

## 3.2 Zone B — Flat-sheet canvas

Center and largest region.

Shows all active signatures as cards/sheets. Normally 1–3 signatures are visible without horizontal scrolling at 1280x800.

Each signature header shows:
- visible label/icon (`A`, `B`, `C` plus motif, never color alone);
- material role icon/name;
- chosen fold-template mini-diagram;
- chosen nest role (`Outer`, `Middle`, `Inner` or numbered inward order);
- sheet flip status where available.

Each flat slot shows:
- side A/B identity;
- slot cell marker;
- assigned page-face token or explicit empty state;
- orientation glyph where relevant;
- lock icon if authored fixed;
- trim-zone marking where relevant;
- learned inverse-fill ghost label when that assist has unlocked.

Both duplex sides are never represented as an unexplained hidden back face.

### Side switching
Each signature has explicit `Side A / Side B` tabs. A keyboard/controller action also toggles the focused signature side. Side transitions can use a short flip animation; reduced-motion mode uses an instant crossfade/state change.

The inactive side's assignment summary remains visible as a thin miniature strip so the player remembers that the sheet is duplex.

## 3.3 Zone C — Face tray

Bottom strip by default.

Shows unassigned faces in stable authored order. Sorting may be changed manually among `authored / read order / group`, but the game does not offer a solver-derived “best order.”

Each face tile uses:
- large identifier (`1`, `2`, motif ID etc.);
- orientation arrow if mechanically relevant;
- material/group tags as icon+text abbreviations;
- explicit required blank graphic for `REQUIRED_BLANK`;
- clearly different open-slot symbol for `EMPTY`.

Placed faces disappear from the unassigned tray unless a duplicate display mode is enabled for accessibility; duplicate display mode must mark them as `Placed` and cannot permit duplicate assignment.

## 3.4 Zone D — Action strip

Bottom-right / controller command bar:
- Undo;
- Redo;
- signature/template controls;
- nesting control;
- Fold Preview;
- Commit Bind/Trim;
- restart/menu.

Primary hierarchy:
1. Fold Preview — frequent verification;
2. Commit — deliberate submission;
3. Undo/Redo — always reachable;
4. structural controls.

Commit cannot visually masquerade as Preview.

---

# 4. Mouse and keyboard interaction

## 4.1 Pointer placement

Mouse default:
- click face in tray -> face becomes selected;
- click legal slot -> PLACE;
- click occupied slot while a face is selected -> SWAP if legal;
- click occupied slot with no selected face -> select that face;
- click tray background / Cancel -> clear selection;
- right click or dedicated Remove action -> REMOVE selected/slot face;
- drag-and-drop is supported as a convenience but is never the only method.

Dragging uses generous snap targets. Releasing outside a legal target returns the face to origin and does not create a history transaction.

## 4.2 Keyboard baseline

Required rebindable actions:
- directional focus navigation;
- Confirm / Pick Up / Place;
- Cancel;
- Remove;
- Toggle Sheet Side;
- Previous/Next Signature;
- Template Menu;
- Nesting Menu;
- Flip Sheet / Face where contextually legal;
- Undo;
- Redo;
- Fold Preview;
- Commit;
- Rules/Goal panel;
- Pause.

Defaults may use familiar keys, but no frozen mechanic relies on a specific physical key.

## 4.3 Context menus

Context menus are shallow. A slot context menu may contain at most:
- Remove;
- Rotate Face, if allowed;
- structured operation beginning from this slot, if unlocked.

Common actions must not hide behind context menus.

---

# 5. Controller interaction

Controller is a first-class discrete-focus interface, not a virtual mouse requirement.

## 5.1 Focus model

Every interactable object belongs to one of five navigation groups:
- Goal Rail;
- Signature Header;
- Sheet Slots;
- Face Tray;
- Action Strip.

Directional navigation is spatial and deterministic. Focus never becomes trapped inside a sheet or panel. B/Cancel always backs out one interaction layer without altering layout.

## 5.2 Pick/place model

- Confirm on a face/occupied slot picks it up logically.
- Directional navigation moves focus while the held face remains attached to a cursor token.
- Confirm on legal destination commits PLACE/SWAP.
- Cancel returns the held face to its origin with no transaction.
- Remove has a dedicated context action.

No analog-stick precision is required.

## 5.3 Structural actions

A shoulder-button cycle changes focused signature. Another configurable action toggles A/B side. Template and nesting changes use small radial/list selectors with explicit preview diagrams.

Undo/Redo have direct binds after onboarding; they are not buried in Pause.

## 5.4 Device glyphs

On-screen prompts must reflect the active input family. The design should use an input-action abstraction and, during implementation, prefer Steam Input-compatible device handling so Deck/Steam Controller/third-party controllers can receive suitable glyphs rather than showing keyboard prompts after controller interaction.

This aligns with current Steamworks compatibility guidance.

---

# 6. Deterministic template-capacity transition rule (Phase-4 M30 repair)

Changing a signature's fold template may change its legal slot schema/capacity. UX must define this without silently deleting player work.

**Frozen behavior:** template change is a single reversible transaction with a deterministic carry-over algorithm.

1. Match old and new slots by exact shared `slot_id` first.
2. Preserve assignments in every shared slot that remains legal.
3. Any assignment whose old slot does not exist in the new template, or becomes illegal under the new slot, returns to the face tray.
4. Newly introduced slots start `EMPTY` unless case data supplies a locked authored assignment.
5. Locked assignments are applied as case authority and cannot be displaced by template change.
6. If applying the new template would create a duplicate required face because of locked data, the template option is disabled as schema-invalid rather than repaired at runtime.
7. The confirmation preview states exactly how many placed faces will return to tray (`Changing fold returns 2 placed faces to the tray`).
8. The entire before/after state is one Undo/Redo transaction.
9. The game never auto-fills new slots and never chooses a semantically “closest” replacement location.

This rule preserves player intent where structurally possible, avoids data loss, and does not leak a solution.

---

# 7. Template / nesting controls

## 7.1 Template chooser

The chooser presents only case-legal templates.

Each option shows:
- plain-language name;
- miniature flat-slot diagram for both sides;
- final folded-face count;
- orientation pattern glyphs where relevant;
- trim/cut positions when relevant.

The chooser may animate a generic example sheet but never inserts case faces into a hypothetical solved arrangement.

## 7.2 Sheet flip

When legal, `Flip Sheet` visibly toggles NORMAL/FLIPPED and immediately updates source orientation markers. It is Undo-able.

## 7.3 Nesting control

Default control is a vertical stack labeled `Outer -> Inner`.

Mouse: drag signature cards or use up/down arrows.
Controller/keyboard: select a signature then Move Outward / Move Inward.

Every valid reorder is one transaction.

Nesting stack uses redundant labels and silhouette depth, not color.

---

# 8. Fold Preview

Fold Preview is the game's central explanatory surface.

## 8.1 Entry

Preview can be entered whenever editable setup passes structural transform legality. If required faces remain unassigned, the game may still preview the partial book using explicit empty placeholders **only when the chosen templates themselves resolve legally**. This encourages learning without turning missing assignments into “failed attempts.”

Commit remains disabled until full case legality passes.

## 8.2 Animation sequence

Normal-speed sequence:
1. workbench isolates signature(s);
2. each sheet folds according to its selected template;
3. duplex side/orientation flips are visually explicit;
4. signatures nest outer-to-inner;
5. trim step occurs if relevant;
6. camera settles on final book inspection.

Animation is a rendering of the deterministic Phase-4 transform. Gameplay state is resolved before animation begins; skipping cannot change result.

## 8.3 Speed

Settings:
- Normal;
- Fast;
- Instant.

After a player has seen a specific template animation several times, Fast becomes recommended but never forced. Holding/pressing Skip completes immediately to final resolved view. Repeated Preview from the same source state may default to the player's chosen speed.

Reduced Motion defaults Preview to crossfade/diagrammatic transform with no sweeping camera and no simulated paper bounce.

## 8.4 Final-book inspection

The final book view supports:
- previous/next leaf;
- spread view;
- face orientation markers;
- signature/material ownership indicator for inspected face;
- `source` action that highlights which flat slot produced the inspected face;
- optional ghost path from final face back to source slot after the relevant tutorial.

This source mapping is not solver leakage because the deterministic transform is known and Preview already reveals consequences. It externalizes bookkeeping.

The view may show required predicate truth for the resolved preview because the player can directly inspect that result. It may not show hypothetical truth after uncommitted source edits without running Preview.

## 8.5 Exit

Exit returns to the exact editable layout, selection cleared, with no history entry.

---

# 9. Prediction prompts and onboarding

Prediction prompts exist to build a mental model, not to grade trivia.

## 9.1 Prompt behavior

When a case defines a `PredictionPrompt`, the first Preview may ask one bounded question such as:
- `Which two faces will touch after the fold?`
- `Will MAP_A be upright or inverted?`
- `Which sheet becomes the center of the booklet?`
- `Will the cut mark survive?`

The player can answer or choose `Show me`. There is no progression penalty for a wrong answer or skip.

After the Preview, the game explicitly compares prediction with outcome using one sentence and one visual highlight.

## 9.2 Tutorial overlays

Overlay rules:
- one concept per overlay;
- anchor to the actual object/action;
- no paragraph longer than roughly 2 short sentences on the workbench;
- can be dismissed/reopened from Rules;
- after the first mandatory gesture, exploratory alternative actions remain available unless case mechanics intentionally lock setup;
- no coach marks repeatedly interrupt Undo/Redo experimentation.

## 9.3 Scaffolding decay

The game reduces help by authored chapter progression:
- early T4: source-to-final ghost paths and prompted prediction;
- later T4: ghost mapping available on demand but not automatically animated;
- once the transform is learned, inverse-fill ghosts can remain as an anti-bookkeeping aid;
- new global constraints receive focus, not re-tutorializing the local formula.

Scaffolding never changes case validity.

---

# 10. First-session exact UX

## C01 / D01 — first fold
1. Case brief shows four numbered final pages and one sheet.
2. Workbench opens with large tray and four slots.
3. Overlay: `These are the two sides of one sheet.`
4. Player places first face using click/confirm.
5. After all four faces are placed, Fold Preview pulses once as the suggested action.
6. Preview performs the one-fold reveal.
7. Player sees final sequence and source mapping.
8. Wrong arrangement returns exact visual consequence, not a failure penalty.
9. Prediction prompt on repeat asks for one adjacency.
10. Success transitions to compact summary.

Target: player reaches the first satisfying fold reveal in under ~3 minutes without reading technical terminology.

## C02/D02
Less placement guidance; prediction asks one final adjacency before Preview.

## C04/D03 — duplex orientation
Introduce T4F with one obvious orientation glyph. Tutorial language is `flip the sheet`, not print-shop terminology.

## C05/D04 — fixed two-sheet nesting
Nesting stack first appears already fixed; preview visibly inserts the inner signature.

## C07/D05 — facing spread
Goal rail highlights a facing pair; final-book spread view makes predicate physically obvious.

## C09/D06 — material/signature-role capstone
Player chooses outer/inner role. Two arrangements can satisfy reading order, but only one physical role satisfies material ownership. The result explanation must demonstrate the global reason without naming the source slots that solve it.

Demo completion screen uses the product hook rather than broad content promises: `You learned how a wrong-looking flat sheet becomes the right book.`

---

# 11. Visual information language

Every mechanic gets a fixed visual grammar.

## 11.1 Face identity
- primary: large number/icon/motif;
- secondary: localized short label where needed;
- shape boundary remains high-contrast under grayscale.

## 11.2 Orientation
- large arrow/chevron aligned to intended top edge;
- optional `UP/DOWN` text in expanded accessibility mode;
- never inferred only from illustration direction.

## 11.3 Signature ownership
- unique signature badge (`A/B/C`) + distinct border motif/pattern;
- material role icon/name;
- color may reinforce but never encode alone.

## 11.4 Nest role
- stacked-book silhouette plus `Outer / Middle / Inner` text;
- source signatures show matching role chip.

## 11.5 Facing
Facing-pair predicate uses an open-book spread icon. In Preview the two relevant faces may receive linked brackets.

## 11.6 Same leaf
Uses front/back leaf icon, visually different from facing spread.

## 11.7 Trim
Cut zones use dashed/scissor boundary and explicit `CUT` icon. `Required Blank` uses a page token labeled Blank; `EMPTY` is an absent-slot hatch, never the same artwork.

## 11.8 Template transform
Template diagrams use numbered destination ghosts plus orientation arrows. They are exact diagrams, not realistic folding blueprints.

---

# 12. Camera and presentation

The game has no free-roaming avatar camera.

Workbench camera modes:
- flat editing overview;
- focused signature close-up;
- Fold Preview animation camera;
- bound-book inspection.

Mouse wheel/analog zoom may adjust within safe bounds, but all mechanics remain usable at default zoom. Camera never hides predicate rail or requires rotating a 3D object to discover mechanically relevant information.

A 2.5D presentation is preferred: sheets can have depth, shadows and fold animation while slot authority stays screen-readable.

---

# 13. Animation authority

Animation rules:
- animation starts only after deterministic target state is calculated;
- controls cannot create duplicate input transactions while an atomic edit animation is playing;
- logical input may either queue at most one safe navigation action or remain available after animation depending on implementation, but canonical state must never depend on frame timing;
- all edit animations are short (~100–250 ms target, adjustable/skip-capable);
- Fold Preview sequence should normally remain under ~2.5 seconds at Normal for simple templates and under ~4 seconds for the most complex three-signature reveal;
- Fast target <=1.5 seconds total;
- Instant performs no meaningful motion delay;
- repeated Undo/Redo must remain responsive and may suppress flourish;
- success celebration is skippable immediately.

No mechanically relevant event is communicated only by transient animation. Final state remains inspectable indefinitely.

---

# 14. Audio / haptics / feedback

Audio is supportive, not authoritative.

Sound families:
- pick/place paper tap;
- swap/structured move;
- fold crease;
- nest slide;
- trim cut;
- legality warning;
- preview settle;
- success bind/closure.

Rules:
- failed predicates do not use a harsh repeated buzzer;
- every audio cue has a visible counterpart;
- audio sliders: Master, Music, SFX, UI;
- mute is fully playable;
- controller rumble/haptics are optional and independently disable-able;
- no puzzle asks the player to identify sound.

Incorrect Commit uses a neutral “inspection” finish followed by exact explanation, not punishment framing.

---

# 15. Failure / explanation UX

## 15.1 Illegal setup

Commit button is disabled. Selecting/hovering it shows concise legality reasons.

Examples:
- `Page 6 is still in the tray.`
- `Sheet B needs an Inner/Outer role.`
- `This fold does not permit an empty slot here.`

The game highlights the relevant source object because legality is source-state information, not solution information.

## 15.2 Incorrect Commit

Result panel contains:
- `Book assembled, but 2 requirements fail.`
- every failed predicate grouped by type;
- exact final relationship observed;
- `Return to Layout` as primary action;
- `Restart` secondary;
- no forced animation replay.

Examples:
- `Pages 4 and 5 are not facing; page 4 faces page 3.`
- `MAP_A is upside down in the finished book.`
- `Gold pages are split between Sheets A and C.`

Prohibited explanation:
- `Move page 4 to slot B1.`
- `Make Sheet B the inner sheet.` when that is the actual missing solution.

The UI explains **what is false in the resolved book**, not **which edit would make it true**.

## 15.3 Optional hint boundary

Phase 6 does not freeze a solver-generated hint system. If Phase 7/10 later retains hints, hints must be authored or bounded and cannot silently become a next-move solver. Baseline completion cannot require consuming hints.

---

# 16. Undo / Redo / Restart UX

Undo and Redo are always visible on workbench.

Tooltip/accessible label names the atomic action:
- `Undo: Swap pages 3 and 6`;
- `Undo: Change Sheet B fold to Double Fold`;
- `Undo: Move Sheet C inward`.

Redo mirrors it.

History persists through Fold Preview because Preview is non-mutating. Entering Pause does not clear history.

Restart asks for confirmation only if the layout differs materially from case start. Confirmation text notes that Restart is itself not Undo-able after acceptance unless later technical architecture explicitly preserves a restart snapshot; Phase 6 baseline assumes restart clears case edit history.

---

# 17. Save / load / recovery user contract

Technical serialization is Phase 8, but player-visible behavior is frozen here.

## 17.1 Autosave moments

The game should autosave player-facing progress after:
- every completed atomic edit transaction or a safely coalesced short debounce after it;
- case success;
- settings change;
- leaving workbench;
- chapter/case unlock changes.

The player is never asked to manually manage save slots for baseline campaign.

## 17.2 In-progress case persistence

On reload, an unfinished case restores:
- exact selected case;
- template choices;
- sheet flips;
- nest roles;
- all assignments/orientations;
- current unlocked structured tools;
- case-start authority version;
- Undo/Redo policy as later frozen technically.

Camera transient, hovered object and an active Fold Preview animation do not need restoration.

## 17.3 Recovery

If the application closed while Preview or Commit animation was presenting, reload resolves from the last durable canonical source/progression state, never a half-folded animation pose.

If a successful Commit was durably recorded, reload shows the case as solved even if celebration did not finish.

If the save cannot be loaded, the UX must never silently overwrite it. Technical phase must define backup/recovery; player-facing message should offer `Retry / Use Backup / Return to Title` where applicable.

---

# 18. Pause and settings

Pause contains:
- Resume;
- Restart Case;
- Rules;
- Settings;
- Accessibility;
- Case Select / Title with autosave notice.

Settings baseline:
- display mode/resolution as relevant;
- VSync/frame cap if implementation exposes them;
- master/music/SFX/UI volume;
- controller vibration;
- input remapping;
- text scale;
- UI scale where distinct;
- high-contrast mechanical markings;
- animation speed Normal/Fast/Instant;
- Reduced Motion;
- camera shake (default none/minimal, toggle if used at all);
- hold/toggle preference for any hold interactions;
- glyph family override optional when auto-detection is imperfect.

Settings changes should preview safely and persist globally.

---

# 19. Accessibility baseline

Required baseline, not stretch goals:

## 19.1 Input
- full keyboard remapping;
- full gamepad remapping or action-level mapping compatible with platform input abstraction;
- mouse alternatives for all drag interactions;
- controller parity;
- no rapid taps, timed button presses or simultaneous multi-button dexterity required;
- hold actions must have toggle/press alternative where a hold would otherwise be necessary.

## 19.2 Motion
- Reduced Motion removes sweeping fold-camera moves, bounce and unnecessary parallax;
- animation speed supports Instant;
- state changes remain comprehensible through diagrams/highlights.

## 19.3 Vision/readability
- scalable text;
- mechanically important text and icons meet high contrast targets;
- no color-only encoding;
- pattern/icon labels for signatures/material;
- orientation has arrow plus optional text;
- focus ring remains visible across all backgrounds;
- mechanically important thin lines scale with UI scale rather than becoming subpixel hairlines.

## 19.4 Cognitive load
- Rules glossary reachable in one action;
- case brief can be reopened from workbench;
- predicate cards remain persistent;
- learned fold diagrams can be reopened without penalty;
- source/final mapping available in Preview after introduction;
- no score penalty for reopening tutorials or using accessibility settings.

## 19.5 Hearing
- all audio information duplicated visually;
- no subtitle system is mechanically required unless later narrative/voiceover is added;
- if voiceover is added, subtitles/captions become mandatory.

---

# 20. Steam Deck / handheld target

Fresh Steamworks documentation reviewed 2026-08-31:
- Valve recommends supporting Steam Deck native 1280x800 (preferred) or 1280x720.
- Steam Deck compatibility review requires readable interface text at roughly 30 cm; the smallest on-screen font character must not fall below 9 px at 1280x800, and Valve recommends aiming around 12 px where possible plus configurable text size/contrast.
- controller prompts must correspond to active input; Steam Input is recommended for suitable glyph/device handling.
- text entry, if required, must work through controller/Steam virtual keyboard paths. Binder's Imposition can avoid mandatory text entry entirely.

Sources:
- https://partner.steamgames.com/doc/steamhardware/compat
- https://partner.steamgames.com/doc/steamhardware/steamdeck
- https://partner.steamgames.com/doc/features/steam_controller

### Frozen Game #009 handheld assumptions
- 1280x800 is a first-class layout target, not a late downscale test;
- default smallest important UI text targets **>=12 px character height at 1280x800**, never below Steam's 9 px review floor;
- large face identifiers target substantially larger than body text;
- three signatures at ordinary sizes must fit without precision dragging; if not, focused-signature paging replaces tiny scaling;
- no hover-only information;
- controller flow reaches every action;
- no required external launcher;
- no mandatory keyboard/text entry;
- default UI must remain readable at handheld distance;
- 16:10 layout keeps action strip and tray clear of overlays;
- Steam Deck trackpads may optionally act as pointer convenience, never as the only comfortable control method.

Steam Deck **Verified** is still not a frozen certification claim until implementation/review; it is a product target.

---

# 21. Localization layout contract

Baseline UI must support string expansion without changing puzzle authority.

Rules:
- no mechanics encoded by English initials alone;
- signature IDs A/B/C may remain symbolic identifiers, but role/material labels are localized;
- predicate cards allow approximately 30–50% text expansion before reflow;
- buttons expand or wrap rather than truncate mechanically important verbs;
- no text baked into page artwork for required mechanics;
- motif icons remain language-independent;
- sentence assembly should use localized full templates rather than concatenating fragments where grammar could break;
- right-to-left readiness should be considered at layout/component level even if launch language list is narrower;
- numbers/read-order are logical tokens and must not rely on Latin alphabet shapes;
- controller glyphs are assets/actions, not localized text;
- title `Binder's Imposition` remains working title; storefront localization must not require understanding the technical noun `imposition`.

---

# 22. Demo UX authority — D01 to D06

The Phase-5 six-case demo uses exactly the same workbench and rules as full campaign.

Demo sequence:
1. D01: one T4 sheet, immediate wrong-looking-flat -> correct-fold reveal;
2. D02: T4 prediction reinforcement with less overlay;
3. D03: binary sheet flip/orientation;
4. D04: second signature and fixed nesting;
5. D05: facing-spread constraint;
6. D06: material/signature-role deduction where reading order alone is insufficient.

Demo constraints:
- no separate tutorial game mode;
- no mechanics absent from full campaign;
- total target 20–30 minutes for representative first-time player;
- resume/save works inside demo;
- final screen links the learned mental model to full-game promise, not to grinding a score;
- demo may carry progress into full game only if Phase 7/8 define a robust versioned transfer; UX architecture reserves a clear `Continue in Full Game` surface but does not assume implementation yet.

---

# 23. Presentation boundaries / anti-drift

Forbidden presentation drift:
- realistic print-shop machinery that implies simulation depth not present in mechanics;
- first-person avatar walking between machines;
- tiny skeuomorphic controls replacing readable game UI;
- fake paper physics that can visibly contradict deterministic transform;
- decorative text dense enough that translation becomes a content burden;
- cinematic fold sequences that expert players must repeatedly wait through;
- color-only stock/signature coding;
- hidden backside information requiring camera manipulation;
- always-live green/red objective meters that allow local hill-climbing without Preview;
- hint arrows that identify the next correct source slot;
- controller cursor emulation as the only gamepad scheme.

---

# 24. UX acceptance tests

A future implementation must satisfy these as design acceptance criteria.

## Flow / first session
**UX01** New player can reach D01 workbench from first boot without entering Settings or reading a glossary.
**UX02** First meaningful fold reveal can occur within a target of ~3 minutes for a representative new player.
**UX03** Case brief can be reopened from workbench in one action.
**UX04** Campaign map clearly distinguishes solved, available and locked cases without color alone.
**UX05** Success offers Next Case without forcing return through title/campaign map.

## Source editing
**UX06** Every face can be placed using click-select-click; drag is optional.
**UX07** Every face can be placed/swapped/removed using controller discrete focus with no pointer emulation.
**UX08** Invalid drag release causes no state/history change.
**UX09** Basic PLACE/SWAP/REMOVE each creates exactly one logical transaction.
**UX10** Structured operation is represented as one Undo-able transaction.
**UX11** Locked assignments cannot be accidentally displaced.
**UX12** Side A/B state is always discoverable without rotating a 3D camera.

## Template / capacity
**UX13** Changing to a larger template preserves exact shared legal slots and leaves new slots empty unless locked by case data.
**UX14** Changing to a smaller/incompatible template returns displaced faces to tray and reports count before confirmation.
**UX15** Template change never discards a face silently.
**UX16** Undo after template change restores exact former template, assignments, flips and relevant slot state.
**UX17** Redo reproduces the same deterministic carry-over result.

## Nesting / orientation
**UX18** Outer/Middle/Inner ordering is readable using text+shape without color.
**UX19** Sheet flip status has persistent icon/text state.
**UX20** Orientation-sensitive face has an explicit mechanical arrow/glyph in source and final view.
**UX21** Same-leaf and facing-spread icons cannot be reasonably mistaken for one another in grayscale review.

## Preview
**UX22** Fold Preview never alters source-state history.
**UX23** Preview and Commit render the same deterministic resolved transform for the same legal setup.
**UX24** Preview can be skipped to exact final state without gameplay difference.
**UX25** Instant animation mode exposes final resolved view without waiting for fold motion.
**UX26** Reduced Motion eliminates sweeping camera/fold motion while preserving transform comprehension.
**UX27** Final-book inspection can reveal source slot for any resolved face after the mapping affordance unlocks.
**UX28** Returning from Preview restores exact source layout.

## Solver leakage / explanations
**UX29** Predicate rail does not continuously reveal hidden full-solution truth for unpreviewed source edits.
**UX30** Preview may show truth of predicates directly observable in that resolved book.
**UX31** Incorrect Commit lists every failed required predicate.
**UX32** Failure explanations report actual final state but never name the source edit that would solve it.
**UX33** Illegal setup is explained before Commit and does not count as failed attempt.
**UX34** Prediction prompt can be skipped without progression penalty.

## Undo / recovery
**UX35** Undo/Redo remain available after any number of Previews.
**UX36** Entering/exiting Pause does not clear edit history.
**UX37** Reload after interruption restores canonical editable case state, not a half-animation state.
**UX38** If successful progression commit was durable before crash, reload cannot regress case to unsolved.
**UX39** Corrupt/unreadable save is never silently overwritten by a fresh state.

## Accessibility/input
**UX40** No required gameplay action depends on drag precision.
**UX41** No required gameplay action depends on timed input or rapid tapping.
**UX42** All mechanically relevant color coding has icon/pattern/text redundancy.
**UX43** Keyboard actions are remappable at action level.
**UX44** Controller can access Rules, Preview, Commit, template, nesting, Undo/Redo and every slot/tray face.
**UX45** Active input glyphs update without leaving stale keyboard-only prompts during controller use.
**UX46** All audio cues needed to understand an action have visible counterparts.
**UX47** Reduced Motion, animation speed and text scale are accessible before entering first case.

## Steam Deck / layout
**UX48** Full workbench remains operable at 1280x800.
**UX49** Mechanically important smallest default text targets >=12 px character height at 1280x800 and never falls below 9 px.
**UX50** No hover-only mechanical information exists.
**UX51** Three-signature mature cases do not require tiny precision targets; focused paging/zoom is used instead where needed.
**UX52** No mandatory player text entry exists in baseline campaign.

## Localization
**UX53** Predicate cards can reflow under ~50% string expansion without hiding involved face/signature tokens.
**UX54** Mechanically important buttons wrap/expand rather than ellipsize the only action label.
**UX55** Required mechanics do not depend on interpreting English text baked into page art.

## Demo
**UX56** D01–D06 run on full-game case/workbench UX, not a separate simplified rules engine.
**UX57** D06 demonstrates a global role deduction that cannot be repaired by local face swapping.
**UX58** Demo completion communicates the flat-sheet -> correct-book hook in one visual beat.

## Expert iteration
**UX59** A skilled player can perform Preview -> inspect -> return -> edit without mandatory modal acknowledgement.
**UX60** Repeated Fold Preview at Fast/Instant does not accumulate presentation delay or alter state.

---

# 25. Empirical UX gates retained

These require prototype/playtest evidence and do not block design-phase completion.

1. **Mental-model transfer:** after the fourth tutorial/reinforcement case, >=70% of representative testers should predict at least two requested final adjacencies before Preview.
2. **Hypothesis-driven solving:** mature cases should produce stated plans more often than blind Preview/swap loops.
3. **Manipulation ratio:** in 12–20 face representative mature cases, reasoning time should dominate clerical interaction; if not, structured operations/scaffolding should be improved before increasing puzzle size.
4. **Orientation readability:** orientation mistakes caused by UI interpretation should be a minority of incorrect attempts after orientation chapter introduction.
5. **Deck readability:** representative handheld users can read predicate cards/face IDs at default scale without moving the device unusually close.
6. **Controller parity:** controller completion time should not be dominated by navigation overhead relative to mouse after initial familiarity.
7. **Preview speed:** expert testers should not report fold animation as a primary friction source with Fast/Instant available.
8. **Failure comprehension:** after incorrect Commit, a majority of players can explain what final relationship failed without being told the corrective source move.
9. **Demo identity:** after D06, testers describe the game primarily as arranging flat sheets to predict a folded book, not generic book crafting.

---

# 26. Phase-6 freeze / implementation flexibility

Frozen UX authority:
- global screen/state flow;
- compact four-zone workbench concept;
- source sheet + persistent goal visibility;
- explicit A/B side switching;
- click-select-click baseline plus optional drag;
- discrete controller focus parity;
- deterministic template-capacity carry-over rule;
- visible Outer->Inner nesting control;
- Preview as non-mutating deterministic fold/nest/trim visualization;
- preview speed Normal/Fast/Instant and Reduced Motion path;
- final-book inspection with source mapping;
- prediction prompts as optional learning instruments;
- predicate feedback boundary preventing unpreviewed hill-climbing oracle;
- exact failed-predicate explanations without source-slot solution leakage;
- persistent Undo/Redo workbench affordance;
- autosaved in-progress case expectation;
- accessibility baseline;
- 1280x800 first-class layout target;
- D01–D06 exact UX/demo progression;
- UX acceptance-test set.

Implementation-flexible details:
- exact pixel coordinates and typography family;
- final art style/material shaders;
- exact button/key defaults;
- exact length/easing of animations inside frozen speed ceilings;
- whether wide-screen Goal rail is left or right if information hierarchy is preserved;
- whether signature side change is a tab transition or short 3D flip in non-reduced-motion mode;
- exact visual motif set for signatures/material roles;
- exact title/store branding.

No Phase-6 decision changes mechanical or content validity.

---

# NEXT DESIGN QUESTION — PHASE 7 ECONOMY / RETENTION / COMMERCIAL MODEL

Phase 7 must freeze the commercial package without bolting progression systems onto the puzzle. Required work:
1. refresh current 2026 Steam premium-puzzle pricing/positioning, relevant demos, comparable playtime/value expectations and current storefront practices;
2. choose launch price band and discount philosophy as a design recommendation, not sales certainty;
3. define campaign unlock pacing, replay incentives and whether optional badges/stats/achievements materially help;
4. decide difficulty/accessibility separation and whether optional challenge conditions exist without becoming grind;
5. define Steam achievements and platform-feature boundaries;
6. define demo packaging, D01–D06 save behavior and full-game progress-transfer recommendation;
7. define retention after campaign: replay/selective mastery only if it preserves product thesis; no daily/weekly/FOMO systems;
8. define monetization boundary: premium baseline, no MTX/live service unless product thesis is explicitly reopened;
9. review working title/store positioning against current market language;
10. create commercial/economy acceptance tests and retain empirical gates for later validation.

**DESIGN COMPLETE = NO.**
