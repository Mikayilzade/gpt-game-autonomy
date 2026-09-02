# GAME #014 — PHASE 6 UX / PRESENTATION ARCHITECTURE

Date: 2026-09-02
Status: COMPLETE — player-facing interaction, readability and presentation rules frozen; Phase 7 next.
Working title: **NEGATIVE CASTING**
Authority: `START_HERE.md` -> `STATUS.md` -> `GAME_INDEX.md` -> Game #014 tournament record -> `GAME14_PRODUCT_THESIS.md` -> `GAME14_MECHANICAL_ARCHITECTURE.md` -> `GAME14_CONTENT_ARCHITECTURE.md` -> this file.

## 1. Phase-6 verdict
**PASS.** The frozen mechanics remain readable with 1, 2 and late 3-surface cases at handheld-sized viewports without introducing solver-like overlays. The player-facing solution is not to show more derived information; it is to enforce a stable spatial layout, large semantic target cells, discrete focus, fast surface switching, redundant channel encoding and strict separation between **actual current state**, **target requirement** and **selected-blocker contribution inspection**.

The game remains fully controller-operable with no precision aiming, drag requirement, tiny cursor targets or mandatory text entry. Mouse and keyboard are first-class alternatives, but controller navigation defines the baseline interaction model.

No production implementation begins here.

---

# 2. Presentation model: one compact casting table

## 2.1 Camera principle
The player never navigates a free 3D room. Each case is presented as a compact stylized casting-table diorama viewed from one authored oblique camera family. Camera motion is limited to discrete presentation states and small cosmetic easing.

Canonical puzzle truth remains the 2D casting plane from Phase 4. The 3D-looking render is an explanatory shell around it.

The camera must always preserve four simultaneously readable anchors:
1. both light origins;
2. all blocker sockets and blocker silhouettes;
3. the currently focused projection surface;
4. the relationship between target cells and actual shadow cells on that surface.

No camera angle may make a blocker appear to cross or clear a logical ray differently from canonical truth.

## 2.2 1-surface layout
For NC01–NC06 and other one-surface cases:
- casting table occupies roughly the central/lower 55–65% of the gameplay area;
- the projection surface is presented as the dominant back/side panel, never a tiny inset;
- target cells are aligned directly with actual sample cells on the same panel rather than duplicated into a distant HUD diagram;
- both light fixtures remain visible at table edges with stable channel glyphs;
- selected blocker receives a non-semantic outline/focus ring.

The intent is that the first screenshot already reads as “objects between two lights and a patterned wall.”

## 2.3 2-surface layout
For NC07 onward, two surfaces use a **primary + secondary** presentation rather than squeezing both to equal tiny size.

- Primary surface: full readable panel, target and actual cells visible simultaneously.
- Secondary surface: reduced but still semantic thumbnail/panel anchored near the corresponding physical side of the table.
- `Switch Surface` swaps primary/secondary with a short camera/panel transition.
- The table and blocker state do not move relative to puzzle truth during the swap; only viewing emphasis changes.
- A compact two-dot/tab indicator shows which surface is primary.

The secondary panel must still communicate four semantic classes, but it is not required to show verbose labels. If a cell becomes too small to distinguish its redundant glyph at the minimum supported viewport, the layout must enlarge/switch rather than simplify the glyph to color-only.

## 2.4 3-surface layout
Three surfaces appear only from NC17 and have lower sample counts by Content Architecture. The UX uses **one primary surface + two persistent compact surface cards**.

Rules:
- never render three full logical walls at equal size;
- primary surface receives full target/current comparison;
- two secondary cards each show ordered sample cells, target glyph and current-state glyph at compact but validated size;
- shoulder buttons / keyboard surface keys cycle primary focus `A -> B -> C`;
- the physical diorama may visually contain all three walls, but only the selected wall receives strong semantic overlays;
- switching primary surface is one input and preserves selected blocker;
- no multi-surface matrix or solver table is shown.

A late case fails Phase-6 readability if the player must memorize the two secondary surfaces before switching. Each card therefore remains continuously visible enough to answer “which surface is currently mismatching and roughly where?” while detailed deduction occurs on the primary surface.

## 2.5 Handheld baseline
Minimum UX validation viewport: **1280×800 at 100% UI scale**, representing Steam Deck-class 16:10 use. Also validate 1280×720 and 1920×1080. The design must support other common aspect ratios without clipping logical content.

No essential target glyph, focus state, controller prompt or mismatch marker may rely on sub-pixel thin strokes. Gameplay text is sparse; minimum default body text target is approximately 18–20 effective pixels at 1280×800, with user scaling above this in settings.

Steam's current Deck guidance emphasizes complete default-controller access, correct controller glyphs, support for varied aspect ratios, offline single-player access and cloud-friendly save behavior; those expectations are adopted as product gates rather than deferred port polish.

---

# 3. Input abstraction

## 3.1 Logical actions
The implementation must expose input actions, not hard-coded device buttons:
- `FOCUS_PREV_BLOCKER`
- `FOCUS_NEXT_BLOCKER`
- `STATE_PREV`
- `STATE_NEXT`
- `SURFACE_PREV`
- `SURFACE_NEXT`
- `TOGGLE_CONTRIBUTION_INSPECTION`
- `COMMIT_CHECK`
- `UNDO`
- `REDO`
- `RESET_CASE`
- `OPEN_CASE_MENU`
- `OPEN_PAUSE`
- `CONFIRM`
- `BACK`
- directional UI navigation

All gameplay functions must be reachable with the default controller configuration. Device-specific prompts should use the active controller family where available and must not flip rapidly merely because a trackpad/mouse moved without a click.

## 3.2 Controller baseline
Recommended default mapping at design level:
- D-pad left/right: previous/next blocker;
- face left/right or shoulder pair: previous/next state of selected blocker;
- shoulder pair not used for state cycling: previous/next surface;
- primary face button: commit/check when focus is not inside a modal;
- secondary face button: back/close;
- one face/trigger action: toggle selected-blocker contribution inspection;
- dedicated shoulder/face shortcuts: undo / redo;
- menu/start: pause.

Exact physical buttons may change during implementation, but the invariant is that blocker selection, blocker-state cycling and surface cycling are separate one-dimensional discrete actions. No analog cursor is required.

## 3.3 Mouse
Mouse may:
- click a blocker to focus it;
- click left/right state controls near the focused blocker card;
- click a surface card to make it primary;
- click HUD actions.

Dragging a blocker or rotating it with free mouse motion is forbidden because it implies continuous placement. Mouse wheel may cycle states only when a blocker is focused and the setting is enabled.

## 3.4 Keyboard
Keyboard-only play must be complete. Default design mapping uses directional/tab-like focus plus explicit keys for state/surface, undo/redo, commit and pause. All bindings are remappable except platform-reserved operations.

## 3.5 Focus order
Gameplay focus is not arbitrary UI traversal. Primary focus order is:
1. blockers in stable authored order;
2. surface cards in stable A/B/C order when explicitly entering surface UI focus;
3. HUD action row;
4. menus.

Returning from a modal restores the previous blocker/surface focus. A hidden or disabled element is skipped without changing the stable ordering of remaining elements.

Focus must be visible through shape/outline/scale, not color alone.

---

# 4. Semantic language for target and actual shadow

## 4.1 Four canonical states
Canonical ids remain:
- `LIT`
- `L1_ONLY`
- `L2_ONLY`
- `BOTH`

Player-facing labels may use clearer short text, but every cell always has redundant visual encoding.

Recommended semantic glyph family:
- `LIT`: open sun/ring glyph with no blocked-channel notch;
- `L1_ONLY`: ring with the L1-origin side struck/filled plus a small L1 glyph;
- `L2_ONLY`: mirrored equivalent plus L2 glyph;
- `BOTH`: closed/filled double-notch or crossed dual-channel glyph.

Channel identity is repeated on the physical light fixture and, when useful, with a distinct line pattern: e.g. L1 ray/contribution uses one dash family, L2 another. Hue can reinforce but never carry identity alone.

## 4.2 Target versus actual
Target and actual truth must not be conflated.

Default surface cell has two layers:
- **Target badge**: fixed small glyph attached to cell frame/top edge.
- **Actual field**: current physical light/shadow appearance plus an optional compact semantic glyph inside the cell.

This lets the player read what should happen and what is happening without opening a separate comparison screen.

A setting may increase semantic glyph prominence for actual state; it may never hide the target.

## 4.3 No hidden darkness semantics
Stylized soft shadows are allowed visually, but canonical samples must receive a crisp semantic marker. A player must never infer L1_ONLY vs BOTH from apparent grayscale darkness.

---

# 5. Selected-blocker contribution inspection and anti-oracle boundary

## 5.1 Purpose
Contribution inspection explains physical causality for the **currently selected blocker in its current state**. It is an accessibility/legibility tool, not a hint system.

When toggled:
- unrelated blockers visually de-emphasize but remain visible;
- current selected blocker is emphasized;
- rays or projected regions from L1/L2 to samples that this blocker currently occludes may be highlighted using channel line styles;
- affected sample cells may receive a temporary contribution marker.

## 5.2 Strict prohibitions
Inspection may NOT:
- show projections for another state before the player chooses it;
- preview several candidate states side-by-side;
- mark a current contribution as good/bad relative to target;
- say “this blocker causes 2 errors”;
- identify the blocker responsible for a mismatch after commit;
- show remaining-solution counts;
- rank states;
- expose the authored human route;
- automatically cycle through counterfactual poses.

The player may manually change the blocker state and observe the new current contribution. That is normal play, not oracle behavior.

## 5.3 Multi-surface inspection
Inspection respects the primary-surface hierarchy. Full contribution rays/markers appear only on the primary surface. Secondary cards may show a tiny “selected blocker contributes here” non-evaluative mark, but never a target-correctness mark.

This prevents late cases from becoming a matrix of all blocker-to-surface incidence.

---

# 6. Core gameplay HUD

Default gameplay HUD is deliberately small:
- top-left/upper edge: case id/title and group progress;
- top/right or side: primary surface label + surface A/B/C switch indicator;
- lower edge: selected blocker card with blocker name/silhouette, current pose `1/3`, previous/next controls;
- compact action prompts: Inspect, Undo, Redo, Check, Menu;
- no permanent move counter;
- no score, timer, star rating or solution percentage.

The target surfaces themselves are the main information UI.

## 6.1 Blocker card
Selected blocker card contains:
- archetype silhouette;
- stable instance label (e.g. `B`, `C`, or icon token);
- current state index/pose icon;
- legal state count;
- disabled direction cue only when state list does not wrap.

State labels are presentation aids, not logic. Use `Pose 1/3` or orientation icons rather than degrees if the sculpture's logical transform is visually clearer than numeric angle.

## 6.2 Surface cards
Each surface card contains:
- surface identifier/icon;
- compact ordered cells;
- target glyph on every cell;
- actual state glyph when enabled/default readability requires;
- mismatch highlighting only after an explicit check, as defined below.

---

# 7. Commit, mismatch and completion

## 7.1 Check action
`Check` is always explicit. The game does not auto-complete the instant a correct configuration appears, because the player should be able to inspect and decide they are done. Optional subtle ambience may react to a fully matching state only **after** check; never before.

## 7.2 Mismatch response
On incorrect check:
- short non-punitive pulse on mismatching sample frames;
- optional text: `Not a match yet — 3 target cells differ.`
- player remains in the exact configuration;
- mismatching cells can remain marked until the next blocker change or until dismissed, configurable if needed;
- no blocker, pose, ray or deduction is blamed/recommended.

Mismatch highlighting answers **where target and actual differ**, not **how to fix it**. This is allowed by the Phase-4 contract.

## 7.3 Correct response
On correct check:
1. semantic cells confirm match;
2. target badges visually settle into the actual projection presentation;
3. camera may perform a brief authored beauty framing of the final negative cast;
4. completion panel offers Next Case, Group View, Replay/Keep Looking.

Completion celebration must be short and skippable. No essential feedback is audio-only.

---

# 8. Undo, redo and reset

## 8.1 Undo/redo
Every blocker-state change is one atomic history step. Surface switching, focus changes and inspection toggles do not enter history.

Undo restores blocker state only. Redo is available until a new blocker-state mutation branches history.

## 8.2 Reset
Reset returns all blockers to the authored initial state vector. Because it discards current state, it requires a lightweight confirmation only if the player has made at least one state change and has disabled quick-reset confirmation in neither settings nor platform convention.

Reset does **not** remove case completion history, tutorial history or accessibility settings.

## 8.3 Leave case
Leaving a case automatically preserves the current blocker state as resumable progress; the player does not need to choose “save.” A case menu offers `Restart from initial state` separately.

---

# 9. Case browser and campaign navigation

## 9.1 Group view
Campaign browser shows 8 groups of 3 floor cases. Each group card shows:
- three case nodes/cards;
- states: locked / available / complete;
- simple completion count;
- no numeric score or star pressure.

Completing 2/3 unlocks the next group. The UI explicitly says `Complete any 2 to continue` while all 24 remain visible as completion goals.

## 9.2 Case card
Case card may show:
- id/title;
- difficulty band icon only in broad terms, not numeric solver complexity;
- completed marker;
- `In Progress` marker when resumable state differs from initial;
- demo/full availability.

It must not reveal which deduction families solve the case.

## 9.3 Continue
Main menu `Continue` resumes the most recently active incomplete case if one exists; otherwise it opens the latest unlocked group. A secondary `Cases` entry always exposes the browser.

---

# 10. NC01–NC08 onboarding

Tutorial philosophy: teach interface and semantic vocabulary through playable case geometry; do not explain solution chains in text.

## NC01 — select / rotate / light protection
- One brief prompt points to a blocker: `Select a sculpture.`
- Prompt: `Change its pose.`
- Surface cells visibly update.
- Target badge for LIT is introduced with a one-line definition: `Open mark = keep both lights reaching this point.`
- Check is introduced after at least one pose change.
- No contribution inspection yet unless accessibility menu is opened.

## NC02 — current contribution inspection
- Introduce optional `Inspect` after the player focuses a blocker.
- Explain only: `Inspect shows what this sculpture blocks in its current pose.`
- Unique producer insight must still be discovered by player.

## NC03 — channel identity
- L1_ONLY and L2_ONLY glyphs introduced next to physical L1/L2 fixtures.
- Tutorial wording must avoid semantic inversion. Example: `L1 mark = Light 1 must be blocked here; Light 2 must still reach it.`
- A persistent glossary entry becomes available.

## NC04 — BOTH
- BOTH glyph introduced: `Both lights must be blocked.`
- No prompt says which blockers should provide the two channels.

## NC05 — endpoint/extent
- No new mechanic tutorial.
- If the player checks incorrectly twice, a generic interface tip may remind them that every sample is exact; it may not say “look at the endpoint.”

## NC06 — synthesis
- All tutorial callouts default off except controls on first device use.
- This case verifies independence before the second surface.

## NC07 — second-surface reveal
- Surface B enters with a short authored camera reveal.
- Prompt teaches `Switch Surface` and explains that the same blocker pose affects every surface simultaneously.
- No overlay compares future poses between A/B.

## NC08 — demo capstone
- No new tutorial concept.
- All standard tools available.
- Completion leads to demo-end panel in demo build or next group in full build.

## 10.1 Skip / revisit
Tutorial prompts may be skipped globally from the first modal and individually dismissed. Skipping never removes glossary/help access.

`Help > Basics` contains:
- controls;
- four target states;
- current-state inspection explanation;
- undo/reset/check semantics;
- surface switching.

It does **not** list deduction families, strategy advice or case solutions.

A `Replay Tutorial Prompts` setting resets only prompt-seen flags, not campaign progress.

---

# 11. First-session flow

1. Launch -> title/menu, controller immediately usable.
2. `New Game` -> optional accessibility quick setup (UI scale, reduced motion, high contrast) that can be skipped.
3. NC01 begins within two confirmations from title screen.
4. Player changes a blocker in under 30 seconds without needing a camera tutorial.
5. First check/solve ideally occurs within 2–4 minutes.
6. By NC03, all channel semantics are visible.
7. By NC07, second-surface reveal proves the differentiator.
8. Demo/full paths diverge only after NC08 completion.

No launcher, account login, online dependency or mandatory narrative sequence precedes play.

---

# 12. Accessibility architecture

Accessibility options are product requirements, not optional polish.

## 12.1 Vision / color
- color-independent semantic glyphs for all four sample states;
- distinct L1/L2 origin glyph and line patterns;
- high-contrast mode for target/current cell frames and focus;
- UI scale presets plus continuous/stepped larger scaling where layout permits;
- actual-shadow semantic glyph prominence option;
- no puzzle-critical distinction conveyed by material texture alone;
- no tiny grazing-angle deduction in shipping content.

## 12.2 Motion
- `Reduced Motion` disables/reduces camera sweeps, blocker rotation flourish, completion zoom and panel sliding; state changes become near-instant crossfades/snap poses;
- camera shake: none by default;
- no mandatory rapid flashing;
- mismatch/completion feedback must use border/shape plus optional low-frequency brightness change, not repeated flashes.

## 12.3 Input
- full controller support from boot;
- full keyboard-only support;
- mouse-only menus/gameplay also feasible because all mechanical actions are discrete clickable controls;
- remappable gameplay bindings;
- no simultaneous multi-button hold required for puzzle actions;
- hold/toggle option for contribution inspection if implementation uses held inspection by default;
- adjustable repeat delay for held D-pad/menu navigation where practical;
- confirmation behavior for reset can be configured without making ordinary state changes require holds.

## 12.4 Audio independence
No logical information is audio-only. Separate sliders for master/music/effects/ambient/UI are preferred; muting all audio leaves the entire game solvable and navigable.

## 12.5 Text / language readiness
All instructional text uses localization tokens and responsive containers. No text baked into gameplay textures. Glyph + short label combinations must survive longer translations. Avoid directional language such as “red light” as the only identity cue; refer to localized `Light 1 / Light 2` names with icons.

Steam currently exposes store-level accessibility-feature categories including adjustable text sizing and keyboard/mouse/input options; the implementation should later map actual shipped features accurately rather than claiming unsupported capabilities.

---

# 13. Audio / visual feedback language

## 13.1 Blocker state change
- short mechanical/socket sound;
- blocker snaps/rotates through the shortest authored readable path;
- actual rendered shadows update in sync with logical state, not after a long animation;
- semantic sample markers update at the same logical transition point.

## 13.2 Surface switch
- subtle spatial camera/panel emphasis;
- stable blocker focus maintained;
- no long cinematic transition; target under ~300 ms normal mode, near-instant reduced-motion mode.

## 13.3 Contribution inspection
- selected blocker and its two channel relationships receive emphasis;
- other scene lighting must not dim so far that actual state becomes unreadable;
- distinct soft UI sound on enter/exit, non-essential.

## 13.4 Mismatch
- restrained “not yet” sound;
- mismatch cell-frame pulse once;
- no buzzer, red full-screen flash or punishment tone.

## 13.5 Completion
- satisfying but short resonance/lighting settle;
- final cast is visually framed as the reward;
- skip input immediately available.

---

# 14. Decorative render vs canonical truth

This is a hard contract.

Decorative rendering may include:
- soft-edge shadows;
- ambient occlusion;
- stylized volumetric light shafts;
- non-semantic material colors;
- subtle bloom;
- background props;
- extruded 3D blocker meshes that preserve the logical footprint silhouette from relevant casting directions.

It may **not**:
- visually show a sample as shadowed by a channel when canonical `blocked()` is false;
- visually leave a sample apparently lit when canonical `blocked()` is true;
- create decorative protrusions that imply extra occlusion;
- use penumbra as a semantic half-state;
- hide a light origin needed to understand channel direction;
- animate a blocker through a resting pose that appears to have a different logical answer after input has settled.

Acceptance test: for every sample, an implementation debug comparison between canonical bits and semantic presentation markers must be exact. If beauty lighting conflicts with truth, beauty lighting changes.

---

# 15. Save / load / recovery expectations at UX level

Technical storage belongs to Phase 8, but player behavior is frozen now.

Persist automatically:
- completed cases;
- group unlocks derived from completion;
- current in-progress blocker state for each entered unsolved case;
- last active case/surface/blocker focus where safe;
- tutorial-seen flags;
- settings/accessibility/remaps.

## 15.1 Mid-case resume
Re-entering an unsolved case defaults to `Resume` at last persisted blocker configuration. Case menu also offers `Restart from initial state`.

A crash/relaunch must not intentionally discard the last meaningful blocker mutation. Autosave may debounce writes technically, but user-visible recovery should lose at most a very small number of recent non-critical UI actions; exact durability contract is Phase 8.

## 15.2 Changed content revision
If implementation/content revision later makes stored blocker-state ids incompatible, the player must never load a malformed configuration. UX fallback is:
- preserve completion if still valid by migration policy;
- reset the incompatible in-progress case to its current authored initial state;
- show a restrained one-time notice: `This puzzle was updated, so its in-progress arrangement was reset.`

Do not silently map unknown poses by index.

## 15.3 Settings scope
Display/device-specific settings should remain local rather than being blindly cloud-synced across devices; campaign progress is suitable for cloud sync. This aligns with current Steam Deck recommendations.

---

# 16. Demo/full transition UX

Demo content is NC01–NC08 and must behave like the same product, not a separate tutorial app.

At demo completion:
- show completion summary and a still/short preview of later 3-surface cases;
- offer Steam store/full-game action where platform permits;
- clearly state whether demo progress can import/carry over once that technical contract is finalized in Phase 8;
- never imply that unplayed demo cases are required if the user already completed NC01–NC08.

If progress import is implemented, it must be idempotent and must not overwrite newer full-game progress; exact merge rules belong to Phase 8.

---

# 17. Pause and settings

Pause menu:
- Resume
- Restart Case
- Case Browser
- Help / Basics
- Settings
- Main Menu

Settings categories:
- Controls / Remap
- Interface / UI scale / actual-state glyph prominence
- Accessibility / high contrast / reduced motion / inspection hold-toggle
- Audio
- Graphics / display
- Language

Changing UI scale or contrast previews immediately and cannot make the current modal impossible to navigate. Restore Defaults is per category where practical.

---

# 18. Screenshot, GIF and trailer readability

## 18.1 Screenshot gate
A representative store screenshot must communicate without caption:
- two distinct light origins;
- several recognizable socketed blockers;
- at least one projection surface with ordered target cells;
- visible cast shadows;
- compact readable semantic target language.

If the UI requires a giant legend in the screenshot, it fails.

## 18.2 5–8 second GIF gate
Required marketing beat:
1. selected blocker visibly changes pose;
2. its physical shadow changes immediately;
3. at least two surfaces visibly change together;
4. target/current cell relationship becomes closer/readable;
5. no explanatory text wall.

The clip should make viewers ask “how can one object satisfy both walls?” rather than “what do these colored squares mean?”

## 18.3 Trailer early beat
Within first ~10–15 seconds of a trailer, show:
- one simple one-surface cause/effect;
- channel-specific target glyph contrast;
- second-surface reveal.

Do not open with menus, narrative framing or late three-wall complexity.

---

# 19. First-session and readability acceptance gates

Phase 6 passes into commercial/economy design only if later implementation/prototype can satisfy these tests. They are frozen validation targets:

### Input
1. From boot, all required game functions are available on a standard controller with no mouse/keyboard fallback.
2. A first-time player can select a blocker, change pose, switch surface, inspect, undo and check without precision cursor use.
3. Keyboard-only path reaches all gameplay/menu functions.

### Semantic readability
4. In grayscale or with hue removed, testers can distinguish LIT/L1_ONLY/L2_ONLY/BOTH from glyph/shape/origin cues.
5. At 1280×800 default UI scale, every target cell in NC24-size load remains individually identifiable.
6. Secondary surface cards in 3-surface cases identify target/actual class without requiring memorization before switching.

### Anti-oracle
7. Contribution inspection never exposes any unselected counterfactual blocker state or target-correctness score.
8. Incorrect check identifies mismatching target cells only, never the responsible blocker or recommended pose.

### Onboarding
9. NC01 reaches first meaningful pose change in <30 seconds for a player using only default prompts.
10. By NC04 the player has seen all four semantic target classes without reading a long help screen.
11. NC07 introduces second-surface switching in one prompt and the player can complete NC08 without a new mechanic tutorial.

### Presentation truth
12. Canonical sample bits and semantic displayed actual-state glyphs agree 100% under automated/debug comparison.
13. Decorative shadows never create a shipping screenshot where a sample appears semantically opposite to canonical truth.

### Accessibility
14. Entire campaign remains mechanically playable with audio muted.
15. Reduced Motion removes nonessential sweeps/zooms without hiding state transitions.
16. High-contrast/color-independent mode retains all channel semantics.
17. Remapping cannot leave required gameplay actions unreachable without a warning/recovery path.

### 3-surface gate
18. A representative NC23/NC24-style case can be reasoned through with one primary + two compact cards; no matrix of all blocker contributions or counterfactual overlays is required.
19. If testers repeatedly require external notes solely to remember surface states, the late-case content is reworked/reduced rather than adding a solver notebook.
20. If target/sample glyphs need to shrink below validated legibility to fit a late case, reduce sample count/content density rather than shrinking UI.

---

# 20. Fresh platform evidence adopted this phase

Research date: 2026-09-02.

Current Steamworks guidance for Steam Deck / Steam Machine reinforces several frozen choices:
- default controller configuration should expose all functionality;
- controller prompts should correspond to the active device and Steam Input can provide future-proof glyphs;
- games should support varied aspect ratios;
- single-player content should function offline;
- save progress should be cloud-friendly across PC/Deck while per-device graphics settings should not be indiscriminately synced.

Steamworks accessibility-feature documentation also recognizes adjustable text size and alternate input modalities as explicit player-facing accessibility features. Negative Casting therefore treats large scalable UI, full controller operation, keyboard-only operation, remapping and non-color semantic coding as launch-quality requirements, while actual store feature declarations must later match what implementation truly ships.

No market finding requires reopening the frozen mechanic.

---

# 21. Phase-6 result and authority boundary

**PASS.** The 3-surface late-game design remains viable without solver-like overlays under the following non-negotiable UI rules:
- one primary surface at a time;
- persistent but compact secondary surface cards;
- large ordered semantic cells;
- redundant non-color channel encoding;
- selected-current-state contribution inspection only;
- discrete controller-native blocker/surface navigation;
- explicit check with mismatch-location feedback but no solution attribution;
- content density must yield to readability, never the reverse.

No new mechanic has been introduced. Missing Reflection/Casting Call systems remain rejected history.

## NEXT ACTION — PHASE 7 ECONOMY / RETENTION / COMMERCIAL MODEL
Define the finite-premium commercial package without adding grind or retention systems: launch price target/range with fresh market comparables, demo/full conversion contract, campaign progression/unlock presentation, achievements, optional hints/assist policy, replay/challenge incentives, Steam/Deck/cloud/platform feature assumptions, discount/DLC boundaries, completion/100% semantics, and monetization exclusions. Preserve 24-case floor / 30-case ceiling and 3–5 hour thesis unless fresh evidence justifies reopening them. Then create `GAME14_COMMERCIAL_MODEL.md` and proceed to Phase 8 only if the product remains commercially coherent without padding.