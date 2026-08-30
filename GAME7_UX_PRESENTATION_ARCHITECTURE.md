# GAME #007 — LAST KNOWN SHAPE — UX / PRESENTATION ARCHITECTURE

Last updated: 2026-08-30
Phase: **6 — UX / Presentation Architecture**
Run: **2 — COMPLETE**
Selected concept: **G7C02 Last Known Shape**
Production implementation started: **NO**
DESIGN COMPLETE: **NO**

`GAME7_PRODUCT_THESIS.md` governs product identity. `GAME7_MECHANICAL_ARCHITECTURE.md` governs domain semantics. `GAME7_CONTENT_ARCHITECTURE.md` governs campaign/data/diversity. This file governs presentation, interaction, accessibility and player-facing flows only where they do not change those rules.

---

# 1. UX thesis

The player should never ask `what shape did the game think I saw?`.

Five facts must remain continuously recoverable:
1. what an object physically is now;
2. what form reality currently remembers for it;
3. what exact form the selected Observation Frame would write;
4. whether committing replaces another remembered form;
5. when committed memory becomes physical authority.

The world is the primary puzzle surface. Menus/cards support inspection but never become a detached form-management game.

---

# 2. Canonical observation sequence

Every observation write uses the same sequence:
1. approach/activate a clearly authored Observation Frame;
2. acquire one eligible object through semantic focus;
3. enter Preview;
4. show exact candidate form as redundant projected/ghosted physical preview;
5. show current remembered form simultaneously;
6. if different, label the fact neutrally as `OVERWRITE`;
7. Confirm commits remembered form;
8. while direct observation remains active, show memory as committed but physical form unchanged;
9. leave/end observation;
10. show concise causal transition from prior physical form to remembered form;
11. affected mechanisms update only at the canonical resolved boundary.

Cancel during preview never changes gameplay state. Animation may dramatize a transaction but may never imply preview itself mutated the puzzle.

---

# 3. Three-state visual language

## PHYSICAL NOW
Solid object presentation. Current traversal/contact/movement rules use this state.

## REMEMBERED
Persistent shape glyph + compact silhouette token tied to object identity. It remains inspectable without revisiting the source frame.

## CANDIDATE PREVIEW
Projected/ghosted alternate with contour/pattern distinct from both Physical and Remembered. Carries explicit `WILL REMEMBER` language/iconography.

If remembered == candidate: `MEMORY UNCHANGED`.
If different: `REMEMBERED [A] → WILL REMEMBER [B]`.
No numeric form IDs are player-facing. Shape, pattern and text redundancy is mandatory; color is supplemental.

---

# 4. Commit versus physical resolution

On Confirm while observing:
- candidate snaps into the memory token;
- concise `REMEMBERED` confirmation appears;
- physical object remains in current physical form while direct observation is active;
- a persistent `LEAVE FRAME TO RESOLVE` cue appears only until the player has demonstrated comprehension; later it reduces to iconography.

On leaving observation:
- memory token cues resolution;
- object transitions to remembered physical form;
- receiver/gate/path feedback follows deterministic event order;
- reduced-motion uses a short snap/dissolve plus before/after outline rather than morphing.

The player may skip cosmetic animation after the semantic boundary, but not the information that remembered state became physical state.

---

# 5. Observation Frame identity and camera non-authority

Every frame exposes a stable icon/shape, visible activation locus, eligible-object indicators, semantic target order and any authored mask/occluder relation. Fixed masks are literal authored world geometry. Dynamic occluder relationships use world geometry plus redundant inspection cues.

Ordinary camera motion cannot change a candidate. Entering a frame may gently align the camera for readability, but candidate authority is semantic before presentation. No precision camera alignment, head-bob dependence, forced roll or pixel hunting is allowed.

Implementation may choose first- or third-person after prototype, provided all authority/focus/readability invariants survive.

---

# 6. Exact controller-only path

Required controller actions:
- left stick / D-pad: Navigate / semantic menu movement;
- right stick: camera look only;
- South face button: Interact / enter Frame / Confirm in context;
- East face button: Cancel / exit Preview;
- shoulder buttons: Previous / Next eligible semantic target while in Frame;
- one dedicated face/shoulder action: Inspect Memory;
- one dedicated action each for Undo and Redo, or an immediately reachable modifier pair;
- Pause/Menu always reachable without chord timing.

Controller observation flow:
`enter activation locus → Interact → focus first eligible target → shoulders cycle targets → candidate panel updates deterministically → Confirm → memory-written feedback → Exit/Move out → resolve`.

No analog-stick precision is required for target selection. Looking at an object may supplement focus but cannot be the only selection route.

## Semantic focus graph
Each Frame stores an authored ordered eligible-target list. Focus rules:
1. entering Frame selects the first currently legal target or the last valid target for that same Frame during the current visit;
2. Next/Previous walks only legal semantic targets in deterministic authored order;
3. disabled targets may be shown as disabled only when doing so reveals already-knowable legality, never hidden solution information;
4. camera orientation cannot silently reorder focus;
5. two-object cases keep object identity stable while cycling;
6. leaving Frame clears Frame focus but not world object memory;
7. returning never auto-commits.

---

# 7. Keyboard-only and mouse+keyboard paths

## Keyboard-only
Default semantic mapping target:
- WASD/arrows: movement/menu navigation;
- keyboard look alternative is not mandatory for ordinary movement if mouse is absent, therefore a discrete camera-turn binding set must exist for true keyboard-only play;
- E/Enter: Interact/Confirm;
- Esc/Backspace: Cancel/Pause by context with no destructive ambiguity;
- Q/R or equivalent: Previous/Next semantic target;
- dedicated keys: Inspect Memory, Undo, Redo, Restart Case.

All essential Frame interaction is reachable without mouse hover.

## Mouse + keyboard
Mouse controls camera and may point/select an already semantically eligible object. Pointer selection resolves to the same object IDs/focus model as controller. Hover may add convenience text but no puzzle fact exists only on hover. Confirm/cancel may use mouse buttons, but keyboard alternatives remain complete.

Pointer miss, screen-space overlap and resolution never decide candidate form.

---

# 8. Steam Deck / 1280×800 constraints

At 1280×800 on the built-in display:
- current remembered and candidate forms remain simultaneously distinguishable;
- required body text minimum target is 18 px equivalent at default scale; critical labels target 20–24 px equivalent;
- no core comparison requires reading more than two compact object cards simultaneously;
- Frame panel consumes at most ~30% of usable width or ~34% of usable height in its expanded mode;
- panel may collapse contextually after commit but cannot cover the target object and overwrite pair at the same time;
- touch/trackpads are optional conveniences, never mandatory;
- glyphs switch promptly between controller and keyboard/mouse without altering focus state;
- 16:10 layout is first-class, not a cropped 16:9 afterthought.

If two-object causal relation cannot be read at 1280×800 with text scale increased one step above default, the case/presentation fails UX validation.

---

# 9. Remapping and recovery invariants

All semantic gameplay actions may be remapped except platform-reserved system behavior. The remap UI must prevent an unrecoverable state.

Hard invariants:
- Confirm, Cancel/Back, menu navigation and Pause always retain at least one valid reachable binding;
- conflicting bindings produce an explicit conflict resolution screen rather than silent overwrite;
- `Restore defaults` is reachable by controller and keyboard without mouse;
- device disconnect pauses input-sensitive presentation and offers an alternate connected device path;
- remapping never changes semantic focus order or candidate authority;
- hold/toggle options may exist for inspection actions, not for changing puzzle semantics;
- no mandatory multi-button timing chord.

---

# 10. HUD and information-density ceiling

Default world HUD is sparse: current objective/case identity, Undo/Redo availability and contextual interaction prompt. Persistent form tables are forbidden.

Memory inspection has two tiers:
- **Quick Inspect:** world-space badges for up to two reasoning-critical objects, showing identity + Physical + Remembered;
- **Expanded Inspect:** compact contextual cards adding pose/location and already-learned affordance icons.

During Frame Preview, the panel may show only:
- target object identity;
- current remembered form;
- exact candidate;
- neutral overwrite/unchanged fact;
- immediately knowable affordance deltas;
- named dynamic INPUT relation when relevant.

For two-object cases, the panel never displays a future-state table or candidate matrix. `Candidate depends on [A-state token]` is allowed only for a mechanically declared input visible in the current state.

---

# 11. Pause, Settings, Restart, Undo/Redo/history

Pause freezes presentation and input, not by inventing gameplay time semantics. Menu includes Resume, Restart Case, Case Select where unlocked, Settings, Tutorial Facts and Quit/Return.

Undo/Redo are first-class and near-immediate. Presentation shows:
- Undo available/unavailable;
- Redo available/unavailable;
- optional one-line semantic label for the immediately adjacent transaction (`Observed Object A as Bridge`, `Moved Object A to Lift Slot`) using already-known facts.

No full solution-history timeline is required; history must not become a planning oracle. Restart asks for confirmation only after meaningful progress, and the confirmation can be disabled in settings. Undo use never invalidates baseline completion, achievements or accessibility-valid play.

---

# 12. C01–C10 onboarding cadence

Tutorial facts are event-triggered, short and replayable from Pause > Tutorial Facts.

- **C01:** `Preview shows exactly what will be remembered.` → `Confirm remembers it.` → after commit, `Leave the Frame: remembered shape becomes physical.` No other system prose before player acts.
- **C02:** one prompt before first Cancel: `Previewing alone changes nothing.` After successful cancel, suppress repeats.
- **C03:** introduce `OVERWRITE` only when candidate differs: `Confirm replaces the remembered form.`
- **C04:** after first move of a transformed object: `Moving it does not erase its memory.`
- **C05:** no correctness warning; after first strategic bad state/Undo, generic reminder: `Legal observations can still be poor choices. Undo is free.`
- **C06:** first affordance icon glossary opens contextually; max three new icons in one case.
- **C07:** teach a form closing one route through consequence, not predictive solver text.
- **C08:** first fixed-mask frame labels the mask as part of the authored Frame, with no camera-angle language.
- **C09:** first explicit preserve decision may prompt `You do not have to commit every preview.` once.
- **C10:** no new tutorial overlay before the synthesis attempt; tutorial facts remain accessible manually.

After C10, mandatory tutorial popups end unless a genuinely new globally frozen primitive appears. Hints are opt-in.

---

# 13. Invalid-command / rejection messaging

Stable Phase-4 reason codes map to bounded player-facing templates. Messages explain legality, not strategy.

- `FRAME_NOT_ACCESSIBLE` → `You cannot use this Frame from here.`
- `OBJECT_NOT_ELIGIBLE_FOR_FRAME` → `This Frame cannot observe that object.`
- `OBJECT_NOT_AT_REQUIRED_POSE` → `The object is not in a position this Frame can observe.`
- `OBSERVATION_LOCKED` → `Observation is unavailable while this object is locked.`
- `NO_VALID_CANDIDATE` → `This Frame has no valid remembered form in the current state.`
- `PREVIEW_COMMIT_MISMATCH` → internal consistency failure; do not blame player; cancel commit and display `State changed; preview refreshed.` plus telemetry/log assertion.
- `STALE_REVISION` → `State changed; try that action again.`
- `DUPLICATE_COMMAND_ID_PAYLOAD_MISMATCH` → internal/system error path, not normal player text.
- `DESTINATION_OCCUPIED` → `That position is occupied.`
- `FORM_INCOMPATIBLE_WITH_DESTINATION` → `This physical form does not fit there.`
- `MOVE_PATH_BLOCKED` → `The path is blocked.`
- `OBJECT_NOT_MOVABLE_IN_CURRENT_FORM` → `This physical form cannot be moved that way.`
- `INTERACTION_PREDICATE_FALSE` → context-specific global template such as `That mechanism cannot be used in the current state.`

Repeated identical rejection within a short interaction window collapses visually rather than spamming text/audio.

---

# 14. Hint boundary

Hints are optional, per-case authored facts with increasing specificity. They never call a runtime solver to reveal the next move.

Four tiers:
- H0: replay learned global rule/fact;
- H1: point to the causal family (`A remembered form may need to be preserved while you move it.`);
- H2: identify relevant entities/relationship (`Object A can affect what Frame B remembers.`);
- H3: reveal one intermediate subgoal, never the complete command sequence.

No hint states `choose Frame X now` unless the case is an early tutorial whose sole purpose is learning that exact interaction. Hints do not auto-execute, alter state, disable achievements or punish the player.

---

# 15. Save/load/autosave/recovery-facing UX

Technical persistence is deferred to Phase 8, but player contract is frozen now:
- autosave only at committed stable gameplay boundaries, case completion and settings/profile changes;
- a small non-blocking save indicator may appear; player never has to wait before ordinary play;
- Continue resumes the latest verified committed boundary, never a half-morphed presentation state;
- if primary save fails validation and a verified backup is recovered, show plain notice: `Recovered your last verified save.`;
- never silently merge divergent active puzzle branches across devices;
- Case Restart affects only current case branch, not campaign unlocks/settings;
- case completion is recorded before transition to completion screen.

No manual slot management is required for baseline campaign, though implementation may offer one profile backup/export feature later without changing puzzle semantics.

---

# 16. Localization / text expansion

All player-facing strings use localization keys; no gameplay-critical text is baked into textures.

Rules:
- layout supports at least +40% text expansion from English without clipping critical comparison facts;
- candidate/remembered shape icons remain paired with localized labels, reducing dependence on noun length;
- sentence fragments that depend on English word order are avoided;
- tutorial terms have one canonical glossary entry each: Physical, Remembered, Will Remember, Overwrite, Observe, Frame, Input;
- invalid-command templates use named placeholders, never concatenated grammar fragments;
- font fallback must cover shipped language sets and distinguish numerals/glyphs where used;
- no puzzle answer depends on English homophones, letter shapes or text length.

---

# 17. Accessibility paths

Required baseline settings/behavior:
- reduced motion with snap/dissolve transformations and no forced camera swing;
- high-contrast mode strengthening contour/pattern separation;
- shape/pattern/icon redundancy for every color-coded state;
- complete audio-off play; captions/subtitles for any informational voice/audio;
- adjustable text scale with 1280×800 validation;
- screen shake default low/off for transformation events; user-adjustable;
- flash intensity reduction; no comprehension depends on flashes/strobes;
- remappable controls and keyboard/controller complete paths;
- camera sensitivity and inversion options;
- no precision camera requirement or reflex-timed observation;
- unlimited Undo/Redo and Restart;
- tutorial facts replayable;
- optional hold/toggle choice for Inspect/Frame interaction where feasible.

Accessibility use never marks a solution invalid or disables baseline achievements.

---

# 18. First boot / case select / completion / demo end

## First boot
Accessibility-safe defaults first, then language/display/input detection, then title menu. No cinematic is required before the player can reach Settings. New Game reaches C01 quickly; lore cannot delay mechanic comprehension.

## Case select
Campaign is organized by unlocked sequence/bands with compact thumbnails/icons. Shows completion, optional mastery/remix status and replay availability. It does not expose future puzzle solutions or hidden candidate forms.

## Case completion
After win predicate resolves and save commits, show concise completion state, Continue, Replay, Case Select, and optional mastery status if applicable. No star economy or currency celebration.

## Demo end
DEMO06 completion must end after a representative two-object causal chain, not after tutorial-only content. Show succinct full-game proposition: more authored cases, deeper preserve/overwrite/order synthesis, progress-import behavior if supported. No countdown/FOMO/purchase nag loop. Player can replay demo cases and return to menu.

---

# 19. Phase-6 acceptance suite — 64 checks

UX-01 Candidate is visible before every legal commit.
UX-02 Preview cannot mutate canonical state.
UX-03 Remembered form is inspectable without revisiting source Frame.
UX-04 Physical and Remembered are distinguishable without color.
UX-05 Candidate and Remembered are distinguishable without animation.
UX-06 Different candidate shows explicit old→new overwrite pair.
UX-07 Same candidate shows `memory unchanged`.
UX-08 Commit visibly writes memory before physical resolution.
UX-09 Physical transformation does not complete before end-observation semantic boundary.
UX-10 Leaving observation gives readable memory→physical consequence.
UX-11 Reduced-motion conveys identical causal facts.
UX-12 Ordinary camera movement cannot change candidate.
UX-13 Frame activation locus is visually identifiable.
UX-14 Fixed masks are readable authored geometry.
UX-15 Dynamic target/input roles are distinguishable without color.
UX-16 Changing A later never implies B's already-written memory changed.
UX-17 Overwrite warning is neutral, not strategic advice.
UX-18 Baseline preview never identifies a correct solution using solver knowledge.
UX-19 Two critical objects have persistent redundant identities.
UX-20 Core Observe flow needs no precision dragging.
UX-21 Controller target cycle uses deterministic semantic eligible order.
UX-22 Camera direction cannot silently reorder controller focus.
UX-23 Controller can complete Observe/Cancel/Undo/Redo without pointer input.
UX-24 Keyboard-only path can complete all core interactions.
UX-25 Mouse selection resolves to same semantic IDs as controller/keyboard.
UX-26 No required fact is hover-only.
UX-27 At 1280×800 remembered/candidate comparison remains simultaneously legible.
UX-28 At 1280×800 + one text-scale step, two-object causal relation remains readable.
UX-29 Trackpad/touch is never mandatory on Deck.
UX-30 Device-glyph switching does not change focus/candidate state.
UX-31 Confirm/Cancel/Pause cannot all become unbound.
UX-32 Binding conflict is explicit; no silent destructive reassignment.
UX-33 Restore Defaults is reachable without mouse.
UX-34 No mandatory timed button chord exists.
UX-35 Default HUD contains no persistent state spreadsheet.
UX-36 Expanded inspection shows at most currently knowable facts.
UX-37 Two-object Frame panel does not show future-state candidate matrix.
UX-38 Pause is not a gameplay-time exploit because baseline has no wall-clock semantic evolution.
UX-39 Undo restores player to an understandable stable presentation state.
UX-40 Redo availability is visible but history does not expose hidden solution branches.
UX-41 Restart cannot erase campaign unlocks/settings.
UX-42 C01 teaches Preview→Commit→Leave→Resolve with minimal prose.
UX-43 C02 demonstrates Preview/Cancel non-mutation.
UX-44 C03 introduces overwrite only when meaningful.
UX-45 C04 demonstrates memory persistence through relocation.
UX-46 C05 normalizes free Undo without revealing strategy.
UX-47 Mandatory tutorial popups end by C10 absent a genuinely new primitive.
UX-48 Tutorial facts remain replayable.
UX-49 Every Phase-4 normal rejection reason has a bounded player-facing mapping or explicit internal-only classification.
UX-50 Rejection messaging never tells player a legal strategic move is wrong.
UX-51 H0–H3 hints never require runtime solver next-move leakage.
UX-52 Hint use never changes canonical puzzle state.
UX-53 Autosave contract exposes only committed stable boundaries.
UX-54 Recovery notice never claims a hybrid/half-transformed state was saved.
UX-55 Active puzzle branches are not silently Cloud-merged in UX.
UX-56 UI tolerates +40% localized text expansion without hiding candidate/remembered facts.
UX-57 Gameplay-critical text is not baked into textures.
UX-58 Audio-off play preserves all puzzle information.
UX-59 High-contrast path preserves object/form/frame identity.
UX-60 Reduced-motion play remains fully valid for campaign/achievements.
UX-61 First boot allows Settings before any mandatory cinematic.
UX-62 Completion save occurs before leaving the solved case flow.
UX-63 Demo reaches representative preserve/overwrite plus two-object reasoning before purchase proposition.
UX-64 Demo replay remains available without repeated purchase nagging.

---

# 20. Phase-6 result

**PHASE 6 — UX / PRESENTATION ARCHITECTURE: COMPLETE ON PAPER.**

The design now has complete controller-only, keyboard-only, mouse+keyboard and Deck paths; deterministic semantic focus; remapping/recovery invariants; bounded physical-world-first HUD; menus/history/onboarding; rejection taxonomy; non-solver hint boundary; persistence-facing UX; localization rules; accessibility paths; first-boot/case-select/completion/demo-end flows; and 64 acceptance checks.

## NEXT ACTION
Phase 7 — Economy / Retention / Commercial Model. Use fresh market evidence. Freeze working price/release review band, campaign unlock flow, optional mastery/remix admission, achievement philosophy, demo→full continuation/import contract, platform features, replay incentives and monetization boundaries. Do not inflate value through grind or new gameplay primitives.