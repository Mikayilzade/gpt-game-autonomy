# GAME #007 — LAST KNOWN SHAPE — UX / PRESENTATION ARCHITECTURE

Last updated: 2026-08-30
Phase: **6 — UX / Presentation Architecture**
Run: **1 — FOUNDATIONS**
Selected concept: **G7C02 Last Known Shape**
Production implementation started: **NO**
DESIGN COMPLETE: **NO**

`GAME7_PRODUCT_THESIS.md` governs product identity. `GAME7_MECHANICAL_ARCHITECTURE.md` governs domain semantics. `GAME7_CONTENT_ARCHITECTURE.md` governs campaign/data/diversity. This file governs how the player perceives and operates those rules.

Phase 6 is **IN PROGRESS**. This run establishes the non-negotiable interaction and causal-presentation foundation; the next run must complete controls/focus, menus/onboarding/accessibility/persistence-facing UX and the full acceptance suite.

---

# 1. UX thesis

The player should never ask `what shape did the game think I saw?`.

The UX must make five facts continuously recoverable:
1. **what the object physically is now**;
2. **what form reality currently remembers for it**;
3. **what exact form this Observation Frame would write**;
4. **whether committing would overwrite a different remembered form**;
5. **when the committed memory actually becomes physical authority**.

The physical world remains the primary puzzle surface. There is no detached form-management screen and no free-camera silhouette hunting.

---

# 2. Canonical player-facing observation sequence

Every ordinary observation write uses the same causal sequence:

1. approach/activate a clearly authored Observation Frame;
2. select or acquire one eligible object through semantic focus;
3. enter **Preview**;
4. show exact candidate form as a redundant projected/ghosted physical preview;
5. show current remembered form simultaneously;
6. if candidate differs, mark the action as **OVERWRITE** without declaring it good/bad;
7. Confirm = commit remembered form;
8. while direct observation remains active, present memory as committed but not yet physically resolved;
9. leave/end observation;
10. show a short causal transition from prior physical form to remembered form;
11. update affordance/world feedback only at the canonical resolved boundary.

Cancel during preview never changes gameplay state.

The presentation may dramatize a commit/resolution, but it may never imply that preview itself changed the object.

---

# 3. Three-state visual language

The game must distinguish these without relying on color alone:

## PHYSICAL NOW
Solid rendered object with ordinary material/outline. This is what current traversal/contact/movement rules use.

## REMEMBERED
Persistent small shape glyph + compact silhouette token associated with the object. It remains inspectable whenever the object is relevant. It may be shown on the object, on nearby frame UI, or in a minimal object-card, but must not require remembering a prior animation.

## CANDIDATE PREVIEW
Projected/ghosted silhouette or alternate model with animated contour/pattern distinct from both solid physical state and remembered token. Preview carries explicit `WILL REMEMBER` language/iconography.

If remembered == candidate, UI states `MEMORY UNCHANGED` rather than pretending an overwrite has occurred.

If remembered != candidate, UI shows a direct old -> new pair using shape glyphs/patterns:
`REMEMBERED [A]  →  WILL REMEMBER [B]`.

No numeric shape IDs are player-facing.

---

# 4. Commit versus physical resolution

The product hook depends on the delay between memory write and reality resolution being understandable rather than confusing.

On Confirm while observing:
- candidate preview snaps into the object's **memory token**;
- a concise `REMEMBERED` confirmation appears;
- physical object stays visually/semantically in its current physical form while direct observation remains active;
- presentation must not morph the world yet.

On leaving observation:
- memory token visually cues `reality resolving`;
- object transitions to remembered physical form;
- affected receiver/gate/path feedback follows the deterministic event order;
- camera does not cut away from the changed object unless needed for accessibility or player control;
- reduced-motion mode replaces morphing with a short dissolve/snap plus before/after outline, preserving causality.

The player may skip/reduce animation after the semantic state change, but cannot skip the information that old physical state became remembered state.

---

# 5. Observation Frame identity

Observation Frames are unmistakable authored world objects/locations, not arbitrary camera angles.

Every frame exposes:
- stable frame icon/shape;
- activation locus visible on floor/device geometry;
- currently eligible object indicators;
- semantic target focus order;
- mask/occluder relationship when relevant;
- exact candidate only after/selecting eligible object, unless a later tutorial intentionally reveals it earlier.

A player turning the ordinary camera while standing near a frame never changes the candidate unless a canonical semantic frame-selection action changes state. Free camera is presentation only.

Frames with fixed masks physically include that mask in their authored structure. Dynamic occluder frames visibly align the named occluder relation using world geometry plus redundant outline/connection cues when inspected.

---

# 6. Overwrite communication without puzzle-solving

The UX warns about **fact loss**, not strategy.

Allowed:
- `This will replace the remembered form`;
- old -> candidate shape preview;
- affordance deltas that are immediately and globally knowable from the forms, such as `fits narrow slot` or `bridge span no longer present` when already learned;
- showing which current remembered token will be destroyed.

Forbidden default assistance:
- `Do not overwrite this yet`;
- `You still need the bridge later`;
- highlighting the correct frame among several based on solution state;
- dead-state oracle;
- showing future candidate chains not currently inspectable under normal rules.

A later hint system may state increasingly specific authored facts, but baseline preview never becomes a solver.

---

# 7. Current-memory inspection

At any ordinary command boundary the player can inspect each reasoning-critical transformable object's:
- identity;
- current physical form;
- remembered form;
- pose/location;
- currently active global affordance tags expressed as icons/plain language;
- observation status if currently committed-observed.

This information must be recoverable without returning to the frame that created it.

For two-object cases, object identity uses redundant cues:
- persistent shape badge/icon;
- world-space marker when inspection is active;
- name/ordinal only as supplemental text;
- color may supplement but never be sole identity.

No detached spreadsheet/table is required to solve ordinary cases.

---

# 8. Two-object readability foundation

When object A can affect B's candidate as a declared occluder/input:
- selecting B's frame highlights B as target;
- the relevant A object receives a secondary `INPUT` outline/relationship cue;
- the preview panel shows `Candidate depends on: [A-state token]` using learned iconography rather than raw rule expressions;
- changing A later does not visually imply B's already remembered form changed;
- B's memory token remains visually stable until B itself is explicitly committed again.

The UX must therefore reinforce the mechanical rule: **observation writes a snapshot result, not a live binding**.

---

# 9. Camera foundation

Baseline camera policy:
- conventional authored third-person or first-person spatial camera may be used, but it is never gameplay authority;
- entering an Observation Frame may gently align the camera to an authored readable composition, but candidate calculation is already determined semantically;
- player may retain look control where this does not obscure required preview information;
- no precision camera alignment is required;
- no head-bob/forced roll during core observation interaction;
- camera transitions must have reduced-motion alternatives;
- an object required for old/current/candidate comparison may not be hidden by a cinematic cut at commit.

Final first-person vs third-person implementation choice may remain flexible until prototype if both satisfy these invariants; the puzzle rules cannot depend on that choice.

---

# 10. Initial input model

Semantic actions required regardless of device:
- Navigate / Move;
- Look / camera presentation control;
- Interact;
- Enter/Exit Observation interaction;
- Cycle semantic eligible target Previous/Next;
- Confirm Commit;
- Cancel Preview;
- Inspect Memory;
- Undo;
- Redo;
- Restart Case;
- Pause/Menu.

No core observation action requires pointer dragging, tracing silhouettes, holding a precise camera angle, or timed release.

Controller/keyboard target selection must use an authored semantic focus graph / eligible-object order, not screen-pixel proximity alone.

The next Phase-6 pass must freeze complete controller, keyboard-only, mouse+keyboard and Steam Deck paths plus remapping invariants.

---

# 11. Onboarding presentation principles

Tutorial text follows `show rule -> require prediction -> confirm consequence`.

C01 should not frontload prose. Required first-session comprehension sequence:
1. see object and frame;
2. enter frame;
3. exact alternate candidate appears;
4. simple prompt states that Confirm will **remember** this form;
5. commit;
6. object remains physically unchanged while still observed;
7. leave frame;
8. visible resolution occurs;
9. immediately use the resulting affordance.

C02 explicitly demonstrates that merely previewing/canceling does not overwrite.

C03 names the concept of overwrite only after the player has experienced one harmless overwrite path.

Terms should remain plain: `Physical`, `Remembered`, `Will Remember`, `Overwrite`, `Observe`. Avoid required `quantum`, `topology`, `state machine`, or computer-vision jargon.

---

# 12. Early accessibility invariants

Already frozen for final Phase 6 completion:
- color is never sole carrier of object/form/frame identity;
- audio is never sole carrier of commit/resolution/receiver consequence;
- reduced motion preserves old -> remembered -> physical causality;
- core play supports non-audio completion;
- no precision camera placement;
- Undo/Redo remain unlimited and first-class;
- readable UI target at Steam Deck 1280x800;
- text scaling/localization must not obscure candidate/remembered comparison;
- flashes/strobes are unnecessary for understanding the transformation;
- essential tutorial prompts remain replayable/inspectable.

---

# 13. UX risks carried into next pass

UX-R1: committed memory but unchanged physical form while direct observation remains active could be misread as input failure. Mitigation must be tested with explicit memory-token lock and leave-to-resolve cue.

UX-R2: two-object occluder dependency could feel like unexplained magic. Need a consistent relationship cue and first dedicated teaching case.

UX-R3: too much persistent HUD could turn a physical puzzle into state-management UI. Memory inspection should be compact/contextual, not a permanent table.

UX-R4: morph animation could imply continuous/intermediate physics. Presentation must clearly remain cosmetic around a discrete semantic boundary.

UX-R5: a generic `overwrite warning` could train players to fear every overwrite. It must communicate fact replacement neutrally, never red-alert good/bad judgment.

---

# 14. Phase-6 Run-1 acceptance checks — 24

UXF-01 Candidate form is visible before Confirm for every legal observation commit.
UXF-02 Preview does not visually imply canonical physical mutation.
UXF-03 Remembered form remains inspectable without revisiting its source frame.
UXF-04 Physical form and remembered form can be distinguished without color.
UXF-05 Candidate preview and remembered form can be distinguished without animation alone.
UXF-06 Different remembered candidate shows explicit old -> new overwrite pair.
UXF-07 Same remembered candidate shows memory-unchanged feedback.
UXF-08 Commit confirmation visibly writes memory before end-observation resolution.
UXF-09 Object does not visually complete physical transformation before the semantic end-observation boundary.
UXF-10 Leaving observation produces a readable memory -> physical consequence.
UXF-11 Reduced-motion path preserves the same causal information.
UXF-12 Ordinary camera movement cannot silently change candidate.
UXF-13 Observation Frame activation locus is visually identifiable.
UXF-14 Fixed mask relationship is visible as authored world geometry.
UXF-15 Dynamic occluder target/input roles can be distinguished without color.
UXF-16 Changing A after B has been remembered never visually implies B memory changed.
UXF-17 Preview warns about replacement but never labels a legal overwrite strategically wrong.
UXF-18 No baseline preview identifies the correct solution frame using hidden solver knowledge.
UXF-19 Two reasoning-critical objects have persistent redundant identities.
UXF-20 Core Observe flow is operable without precision pointer dragging.
UXF-21 Keyboard/controller target cycle follows semantic eligible targets rather than arbitrary pixel order.
UXF-22 C01 can teach the rule through action with minimal prose.
UXF-23 C02 can visibly demonstrate preview/cancel non-mutation.
UXF-24 Audio-off play preserves all required observation/overwrite/resolution information.

---

# 15. Run-1 result

**PHASE 6 — UX / PRESENTATION ARCHITECTURE: IN PROGRESS.**

This run freezes the causal presentation contract: physical/current vs remembered vs candidate states, exact preview/commit/leave sequence, neutral overwrite communication, current-memory inspection, authored frame identity, two-object snapshot readability, camera non-authority, initial semantic actions, onboarding language, accessibility foundations and 24 foundation checks.

## NEXT ACTION — PHASE 6 RUN 2
Complete the UX specification with:
1. exact controller-only path and focus graph rules;
2. exact keyboard-only and mouse+keyboard paths;
3. Steam Deck 1280x800 layout constraints;
4. remapping/recovery invariants;
5. HUD/context panels and two-object information density limits;
6. pause, settings, restart, Undo/Redo/history presentation;
7. onboarding C01–C10 prompt cadence and tutorial replay;
8. invalid-command/rejection messaging taxonomy mapped from Phase 4 reason codes;
9. hint architecture boundary without solution leakage;
10. save/load/autosave/recovery-facing UX assumptions for later technical freeze;
11. localization/text expansion rules;
12. accessibility settings and non-audio/reduced-motion/high-contrast paths;
13. first-boot / case-select / completion / demo-end flows;
14. complete Phase-6 acceptance suite to >=55 total checks.

If Phase 6 closes cleanly, advance to Phase 7 commercial/economy review with fresh current-market pricing/context research.