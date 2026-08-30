# GAME #008 — UX / PRESENTATION ARCHITECTURE

Last updated: 2026-08-30
Phase: **6 — UX / Presentation Architecture**
Selected concept: **G8C02 Locksmith's Margin**
Working title: **Locksmith's Margin**
Production implementation started: **NO**

This file is the complete Phase-6 interaction and presentation authority. It may expose, clarify and recover the mechanics frozen in `GAME8_PRODUCT_THESIS.md`, `GAME8_MECHANICAL_ARCHITECTURE.md` and `GAME8_CONTENT_ARCHITECTURE.md`; it may not create alternate fit logic, extra information, timing pressure, lock-specific exceptions or new puzzle verbs.

Current platform evidence used for this phase is implementation guidance, not game canon: Steam Deck verification expects the default controller configuration to reach all in-game functionality, and current Godot input guidance favors semantic input actions rather than device-specific gameplay code. Locksmith's Margin therefore treats keyboard+mouse, controller and Steam Deck as first-class paths from the start.

---

# 1. Presentation thesis

The player should feel seated at one compact locksmith bench, not walking through a room or operating a spreadsheet.

Three rules govern presentation:
1. **the physical artifact is primary** — the key profile, lock mouth/cutaway, vice, file target and opened fixture carry the causal story;
2. **the ledger explains memory, never replaces observation** — UI records what was observed/deduced but does not reveal hidden accepted sets;
3. **every authoritative fact has at least two readable channels** when practical: geometry/shape + text/icon, motion + static end-state, audio/haptic + visual rather than audio/haptic alone.

The visual fantasy may be tactile, warm and mechanical; the rules remain discrete and fictionalized.

---

# 2. Bench and camera composition

## 2.1 Single-station bench
A case is presented as one fixed workbench with five semantic zones:
- **Key Rack** — all 1–3 persistent blanks, always reachable without walking;
- **Vice / Filing Stage** — selected blank enlarged and aligned to discrete columns;
- **Lock Rail** — all currently known locks as physical cylinders/fixtures; inaccessible locks remain visible but physically recessed/latched with their access predicate shown;
- **Inspection Stage** — enlarged cutaway view of selected lock and inserted key during TEST;
- **Ledger Drawer** — optional UI panel for accumulated observations, deductions and history.

No WASD traversal is required. Camera movement is selection-driven and bounded.

## 2.2 Camera states
Four authored camera states only:
- `BENCH_OVERVIEW` — all blanks and known locks readable;
- `KEY_FOCUS` — selected key in vice, all columns visible;
- `LOCK_FOCUS` — selected lock, access state and current selected key visible;
- `TEST_CUTAWAY` — key inserted, columns read left-to-right, first blocker emphasized.

Transitions may animate but input authority switches immediately according to destination focus state. Reduced-motion mode cuts or strongly shortens transitions.

## 2.3 No walking friction
Changing selected blank, lock or ledger view is one navigation action. There is no avatar locomotion, collision, reach distance, body animation, drawer-opening requirement or hidden hotspot.

## 2.4 Readability ceilings
At normal campaign maxima (3 blanks / 6 locks / 6 columns):
- all blanks remain individually identifiable in overview;
- all known locks have distinct stable positions and labels/icons;
- selected artifact is never obscured by the HUD;
- critical notch/pin geometry remains readable at 1280×800 Steam Deck resolution at default UI scale;
- inspection zoom is available independently of gameplay camera transitions.

---

# 3. Input abstraction and mappings

All gameplay uses semantic actions. Device bindings are defaults and fully remappable where the platform permits.

Canonical actions:
`NAV_LEFT`, `NAV_RIGHT`, `NAV_UP`, `NAV_DOWN`, `CONFIRM`, `BACK`, `SELECT_NEXT_KEY`, `SELECT_PREV_KEY`, `SELECT_NEXT_LOCK`, `SELECT_PREV_LOCK`, `ENTER_FILE_MODE`, `FILE_PREVIEW`, `FILE_COMMIT`, `TEST`, `INSPECT`, `LEDGER`, `HISTORY`, `UNDO`, `REDO`, `RESTART`, `HINT`, `PAUSE`, `ZOOM_IN`, `ZOOM_OUT`.

Gameplay code may not depend on physical keycodes/buttons.

## 3.1 Keyboard + mouse default
- mouse left: select focused bench object / activate focused ordinary UI control;
- mouse wheel: inspection zoom when over artifact; otherwise scroll panel;
- `A/D` or arrows: move columns or horizontal bench focus;
- `W/S` or arrows: move vertical UI focus;
- `Q/E`: previous/next key;
- `R/F`: previous/next lock;
- `Space`: TEST when a key+accessible lock pair is selected;
- `Enter`: contextual CONFIRM; in filing mode advances from preview to explicit commit prompt, never silently commits from mere selection;
- `X`: explicit FILE_COMMIT default inside filing mode;
- `Tab`: Ledger;
- `H`: Hint;
- `Ctrl+Z`: Undo;
- `Ctrl+Y` and `Ctrl+Shift+Z`: Redo;
- `Esc`: Back/Pause.

Mouse drag is never required for filing. Clicking a notch target selects it; commit is discrete.

## 3.2 Controller / Steam Deck default
- left stick / D-pad: spatial UI and column navigation;
- `A / South`: CONFIRM / select;
- `B / East`: BACK;
- `X / West`: explicit FILE_COMMIT while filing target is armed;
- `Y / North`: TEST with selected key+lock;
- LB/RB: previous/next key;
- LT/RT: previous/next lock;
- View/Select: Ledger;
- Menu/Start: Pause;
- left-stick click or dedicated remappable action: Inspect/Zoom mode;
- D-pad up/down in inspection: zoom steps;
- shoulder chord is **not** required for any essential action.

Exact glyph family follows detected controller, with generic fallback. Controller hot-swap updates prompts without losing focus.

## 3.3 Focus safety
Every interactive UI state has exactly one initial focus target. Returning from modal/pause restores the prior semantic focus when still legal; otherwise nearest deterministic valid target.

No mouse hover may steal focus from controller navigation. Controller input from an unfocused application must be ignored at implementation level.

## 3.4 No mandatory hold
No core action requires holding a button. Optional hold-to-inspect may exist only alongside toggle mode. Filing one authoritative depth is always one deliberate commit action.

---

# 4. Filing interaction

## 4.1 Entry
Selecting a key and choosing FILE moves it into `KEY_FOCUS`. The key profile is aligned on a visible 1..C column jig. Each column has discrete depth teeth/guide marks corresponding to authoritative states without requiring numbers.

## 4.2 Candidate notch preview
Highlighting a legal column shows exactly one candidate next-depth ghost:
- current metal/profile remains solid;
- material that would be removed is hatched/outlined;
- candidate resulting edge is a dashed/ghost contour;
- label: `NEXT CUT` plus optional `depth x→x+1` when numeric accessibility labels are enabled.

Preview never changes key authority or action history.

At max depth the column displays a capped end-state and `MAX DEPTH`; no commit affordance is armed.

## 4.3 Explicit FILE commit
Commit requires a separate `FILE_COMMIT` action after the candidate is visible. On commit:
1. authoritative key vector changes immediately by +1 at that column;
2. animation removes the corresponding discrete notch;
3. history gets one FILE entry;
4. solver/softlock check may run downstream;
5. focus remains on the edited column unless the player leaves filing mode.

There is no timing meter, freehand cursor accuracy or multi-stroke grind.

## 4.4 Accidental-cut protection
The game does not require a confirmation dialog for every ordinary cut; that would create friction. Protection instead comes from the two-stage `select/preview → explicit FILE_COMMIT` grammar plus unlimited Undo.

Settings may enable `Confirm every cut` as an accessibility/preference option.

---

# 5. TEST interaction and physical/UI authority

## 5.1 Selecting a test
A key and currently accessible lock must be selected. TEST is disabled with an explicit reason if the lock is inaccessible; the access predicate remains visible.

## 5.2 Evaluation presentation
The same authoritative left-to-right evaluation order is visualized:
- key inserts;
- columns already accepted settle into an aligned state one by one or as a rapidly readable sequence;
- first incompatible column physically binds and becomes the only failure focus;
- later columns remain visually unresolved/neutral, never accidentally implying evaluation.

Meaningful result must appear within the Phase-4 pacing target; flourish can finish after the result exists.

## 5.3 TOO_SHALLOW
Redundant encoding:
- blocking pin/slider sits visibly above its alignment band;
- notch column gets an outward/downward `DEEPER NEEDED` arrow or notch-shape icon;
- text label `TOO SHALLOW` available in inspection/ledger;
- LIGHT vs STRONG uses one-notch vs multi-notch chevron count/shape, not color alone.

## 5.4 TOO_DEEP
Redundant encoding:
- alignment has passed beyond all valid band positions;
- broken/overcut-style static symbol distinct from shallow mark;
- text `TOO DEEP — FILING MORE CANNOT FIX THIS FIT` in tutorial/expanded inspection.

No ordinary impression animation suggests more filing.

## 5.5 BETWEEN_BRANCHES
Redundant encoding:
- split valid-band symbol with current position visibly in the gap;
- paired/bracket icon;
- text `BETWEEN VALID BANDS` after the concept is introduced.

It must never reuse the shallow/deep icon family.

## 5.6 Accepted prefix
Columns before the blocker receive a subtle stable `accepted at this tested depth` marker. This is an observation, not revelation of the whole accepted set.

## 5.7 OPEN
Successful lock turn is clear and tactile, then lock receives persistent OPENED state:
- physical latch/indicator moves;
- stable `OPENED` shape/icon remains in overview;
- access changes resolve visibly;
- later filing of that key cannot make the completed marker disappear.

---

# 6. Knowledge ledger

The ledger exists to externalize memory and reduce note-taking burden while preserving deduction.

## 6.1 Structure
Rows: locks. Columns: key blanks. Expanding a key/lock pair shows column observations 1..C.

Every item is classified visibly as:
- **OBSERVED** — directly produced by an authoritative TEST/OPEN;
- **DEDUCED** — logically implied by already observed facts under universal rules;
- **UNKNOWN** — not established.

These states use different border shapes/icons and text labels; never color alone.

## 6.2 What ledger may show
Allowed:
- tested key vector snapshot at time of observation;
- accepted-prefix facts;
- failure column and relation at tested depth;
- LIGHT/STRONG if observed;
- OPEN with tested depths;
- visible access predicates;
- logically certain deductions computed only from public rules + player observations.

Forbidden:
- hidden accepted values not logically deduced;
- later-column data from a first-blocking failure;
- solver-only solution partitions;
- probability/confidence pretending hidden data is known.

## 6.3 Deductions
A deduction engine may summarize exact consequences such as `depth 2 was accepted here` or `current depth 4 is already too deep for this lock`, but every deduced statement must provide a `Why?` expansion listing the observations used. If an implication is not certain, it stays UNKNOWN.

## 6.4 Physical-first shortcut
From any ledger entry, `Inspect` returns to the corresponding physical key/lock pair with no state change.

---

# 7. HUD and overlays

Normal bench HUD is intentionally small:
- case title/progress `opened n/N`;
- currently selected key identity;
- currently selected lock identity + access state;
- compact Undo/Redo availability;
- Hint availability;
- optional mastery goals.

No permanent numeric matrix, hidden-state meter or solver estimate is shown.

## 7.1 Access predicates
Inaccessible known locks remain visible. Their badge states one of:
- `AVAILABLE`;
- `AFTER A`;
- `AFTER ANY: A / B`;
- `AFTER ALL: A + B`.

Selecting it highlights prerequisite physical locks on the bench.

## 7.2 Optional numeric aid
Accessibility setting `Show discrete depth labels` overlays 0..D/current integer on key columns. It may improve legibility but cannot reveal lock acceptance values not known through observation/deduction.

---

# 8. Action history, Undo, Redo, Restart and softlock UX

## 8.1 History
History is a chronological reversible action list:
- FILE: key, column, old→new depth;
- TEST: key, lock, result summary;
- OPEN/access effects nested under the successful TEST.

Camera/menu/ledger interactions are excluded.

Selecting an entry previews what Undo would remove but does not jump arbitrarily in time in core UI.

## 8.2 Undo / Redo
Undo is always one authoritative action. Feedback must state exactly what changed (`Undo: Key B column 3 returned 2→1`; `Undo: removed Test B→Lock C and its learned facts`).

Redo mirrors stored transition exactly. Taking a new authoritative action after Undo clears future redo and communicates this without modal interruption.

## 8.3 Restart
Restart is in pause and history. If no authoritative action occurred, restart is immediate; otherwise one confirmation states that current case actions/knowledge will reset. Campaign progress outside the current unsolved case is unaffected.

## 8.4 Proven softlock warning
Only a proven unsolvable state may show warning. Initial passive form is a compact neutral banner:
`No valid completion remains from the current cuts.`
Actions: `Undo`, `Restart`, `Keep experimenting`, `Why am I seeing this?`.

The warning must not reveal which cut was the mistake. It is suppressible for the current state and can be disabled globally; requesting Hint may surface it again if relevant.

Solver timeout/unknown never produces a false warning.

---

# 9. Onboarding C01–C06

No tutorial text wall. Each concept follows `show physical state → one short prompt → required action → visible consequence → prompt disappears`.

## C01 First Mark
- spotlight one blank and training lock;
- prompt `TEST THE KEY`;
- after first blocker, camera lingers on exact bound column;
- prompt points to that same column: `SELECT THE MARKED COLUMN`;
- candidate notch appears; prompt `FILE ONE STEP`;
- after commit/retest/open, control is fully released.

## C02 Prefix
No new modal instruction. After a failure at later column, accepted earlier columns settle with stable ticks. A one-line callout: `Everything before the blocker accepted this tested depth.` Ledger tab briefly pulses once.

## C03 Too Far
Pre-cut state creates TOO_DEEP. Short callout: `This cut is already past every valid band here. More filing cannot repair this fit.` Undo button receives one-time focus suggestion; player may also Restart.

## C04 Two Locks
Bench overview teaches lock selection and opened-state persistence. No compatibility lesson forced yet.

## C05 Shared Scar
After first key opens Lock A, overview deliberately leaves that key selected when Lock B is chosen. If player uses spare key, case remains solvable; if same key opens B, a small `ONE KEY — TWO OPENS` payoff appears.

## C06 Stop Cutting
After a shallow-compatible state is reached, no prompt tells player not to cut. The level must produce the insight. If player hovers the tempting deeper cut, preview clearly shows removed metal but no spoiler warning. Hint ladder may later direct them to test the other lock before changing the key.

Tutorial rules:
- no rule exists only in narration, animation, sound or color;
- all instructional callouts can be reopened from Help;
- prompts pause no simulation because puzzles are untimed;
- controller glyphs update live;
- skip tutorial explanations is available, but never skips authoritative case actions.

---

# 10. Hint UX

Hints are optional, deterministic and non-punitive. They never gate progression or cost currency.

Three tiers:
1. **Recall** — points to relevant observed facts / access state without suggesting an action;
2. **Reasoning nudge** — names the question to consider (`Would this key still be useful elsewhere before you cut?`);
3. **Action-local** — suggests a safe next TEST or identifies a cut that should not yet be committed, based only on information available to the player.

A fourth explicit `Show solution step` may exist only after repeated requests / solved-review context and must be clearly labeled as a spoiler. Hint state is not advanced by repeating identical tests.

Hint panel can cite ledger facts with `Why?` links. Solver clairvoyance may never leak hidden accepted sets.

---

# 11. Menus and campaign flow

## Main menu
`Continue`, `Case Select`, `Demo/Full Import` when applicable, `Settings`, `Accessibility`, `Credits`, `Quit`.

## Case Select
Cases are shown in campaign order with:
- title;
- solved/unsolved;
- optional mastery badges;
- best visible stats only after solve;
- locked future cases with simple progression requirement.

No star economy. Base progression unlocks the next required case through completion; optional mastery never gates campaign.

## Solved review
After win, show:
- physical final keys in hero layout;
- locks opened by each key over the action trace;
- total FILE / TEST / Undo counts;
- optional mastery achieved;
- `Review Timeline`, `Replay Case`, `Next Case`.

The review may reconstruct observed history but cannot claim that final key vectors still open locks that were completed before later repurposing unless actually true.

## Pause
Pause includes Resume, Undo/Redo shortcuts, Restart Case, Help, Settings, Accessibility, Return to Case Select, Quit to Menu. Puzzle state does not advance while paused because no time system exists.

---

# 12. Demo UX and full-game import

Demo and full game share the same input, accessibility, ledger and save semantics for D01–D06.

At demo completion:
- hero image: shared key + specialist key + opened cylinders;
- concise product promise;
- `Replay`, `Wishlist / Store` where platform integration permits, `Quit`;
- no fake locked-feature carousel or urgency/FOMO.

Full game may detect a valid demo completion record. Import behavior:
- import settings/accessibility preferences where compatible;
- mark equivalent tutorial concepts T0–T7 as `seen`, not automatically mark main campaign C01–C08 solved;
- offer `Start normally` or `Condensed onboarding`; player can always replay tutorials;
- never import an in-progress demo puzzle into a non-identical campaign case;
- invalid/older demo schema falls back safely to normal onboarding without deleting either save.

Exact persistence schema belongs to Phase 8.

---

# 13. Accessibility baseline

Required baseline:
- full keyboard-only path;
- full mouse+keyboard path;
- full controller-only path;
- Steam Deck default controller reaches every in-game function;
- complete remapping for gameplay semantic actions, with protected fallback for menu navigation;
- toggle alternatives for any optional hold behavior;
- UI scale presets 100/125/150/175/200% subject to layout validation;
- text-size presets independent where feasible;
- inspection zoom;
- high-contrast artifact edge mode;
- non-color encodings for OPENED, access, shallow/deep/branch, observed/deduced/unknown;
- reduced motion;
- animation speed 0.5× / 1× / 1.5× / instant-result-friendly setting while authority remains identical;
- skippable repeated TEST flourish;
- screen shake off by default unless later proven valuable; never authoritative;
- audio sliders: master/music/SFX/UI separately;
- subtitles/captions for any voiced/non-verbal narrative audio if introduced; core puzzle never depends on hearing;
- haptics intensity/off; haptics never unique information;
- controller vibration absent hardware must lose nothing;
- dyslexia-friendly/font substitution may be offered if it preserves layout; no puzzle depends on letter shape;
- optional discrete-depth numeric labels;
- help glossary for all universal feedback symbols.

Colorblind-specific palettes may supplement but cannot be the sole accessibility solution because shape/text redundancy is canonical.

---

# 14. Save, load, crash recovery and conflict messaging

UX contract, with exact serialization deferred to Phase 8:
- current case state autosaves after every settled authoritative action;
- no save occurs halfway through a FILE/TEST presentation transition; authority commits first, then presentation can resume/skip after reload;
- loading restores the last settled authoritative state and full supported Undo history;
- campaign completion/settings save separately enough that one corrupt current-case record need not destroy all progress;
- a backup/recovery slot is retained before destructive save migration where implementation permits;
- corruption never silently starts a fresh campaign.

## Crash recovery
On next boot after interrupted session:
`Recovered your last completed puzzle action. The unfinished animation was not part of puzzle state.`
Then resume bench with stable state.

## Cloud/local conflict
Never choose silently when both saves contain divergent meaningful progress. Present:
- timestamp;
- solved-case count;
- current case/action count;
- device label if available;
- `Use this save`, `Use other save`, `Back up both then choose`.

If one save is structurally invalid and the other valid, explain recovery and preserve invalid copy for diagnostics when possible.

---

# 15. Visual language

Working direction: compact late-night repair bench, stylized rather than photorealistic, with clean exaggerated mechanical shapes.

Authority layers:
- brass/metal silhouette = key physical state;
- engraved column jig = discrete authoritative locations;
- cylinder cutaway = fit causality during TEST;
- fixed bench positions = blank/lock identity and access relationships;
- paper tags/etched labels = textual redundancy.

Avoid:
- realistic pin-tumbler instruction detail;
- tiny physically accurate components that harm readability;
- dark cinematic lighting that hides cuts;
- holographic spreadsheet overlays as primary play;
- red/green-only status language;
- particle marks that disappear before player can inspect them.

Unknown internals may be visually abstracted; the game does not owe realistic lock construction because it is puzzle fiction.

---

# 16. Audio and haptic roles

Audio goals:
- FILE commit: short material scrape + decisive end click;
- TEST: insertion, sequential light mechanical settling, distinct bind, successful turn;
- Undo/Redo: quiet reversible UI cue distinct from physical forward action;
- access unlock: spatial latch sound paired with visible bench change.

Audio may reinforce LIGHT/STRONG impression intensity but cannot be the only difference.

Haptics:
- light pulse on FILE commit;
- small sequential ticks during accepted columns if hardware supports it;
- distinct bind pulse on blocker;
- broader turn pulse on OPEN.

All haptics optional/off and informationally redundant.

---

# 17. VFX non-authority boundaries

VFX may interpolate or emphasize an already-resolved state. VFX may never:
- decide fit;
- reveal a later untested column;
- imply an accepted depth not established;
- show a key cut before FILE authority commits;
- change access state before successful TEST resolution;
- hide critical geometry through smoke/sparks/depth-of-field;
- encode knowledge only through transient animation.

If presentation and domain state disagree, domain state wins and the mismatch is a release-blocking bug.

---

# 18. First-session target

Within roughly the first 10 minutes, a fresh target player should be able to say:
- `I test a key and the first bad column tells me why it failed.`
- `Filing always makes one column deeper and I can undo mistakes.`
- `A key can be useful for more than one lock.`

By C06 / demo D05–D06, they should additionally articulate:
- `The best move can be not cutting yet.`
- `I should test other locks before destroying overlap.`

If players instead describe the game as `copy the marks until the key works`, onboarding/content has failed even if controls are understood.

---

# 19. UX / presentation acceptance tests

The following are release/spec acceptance tests; identifiers are stable for implementation tracking.

## Bench / camera
**UX01** At 3 blanks/6 locks, every known object is selectable from BENCH_OVERVIEW without avatar locomotion.
**UX02** Switching selected key requires at most one repeated semantic action per adjacent rack item.
**UX03** Switching selected lock requires at most one repeated semantic action per adjacent rail item.
**UX04** Camera animation never changes puzzle authority.
**UX05** Reduced-motion mode can replace every gameplay camera transition with a cut/short transition.
**UX06** At 1280×800 default scale, selected key columns 1..6 remain distinguishable.
**UX07** Inspection zoom does not alter candidate selection or authoritative state.

## Input
**UX08** Every core gameplay function is reachable with controller only.
**UX09** Every core gameplay function is reachable with keyboard only.
**UX10** Mouse drag is not required for filing or testing.
**UX11** Hot-swapping controller↔keyboard changes prompts without losing semantic focus.
**UX12** Remapping gameplay actions does not remap away all menu recovery navigation.
**UX13** No essential action requires a multi-button chord.
**UX14** No essential core action requires holding a button.
**UX15** Unfocused application ignores controller gameplay input.
**UX16** Back from Ledger returns to the prior physical semantic focus if still valid.

## Filing
**UX17** Selecting a column shows candidate next-depth geometry without mutating key state.
**UX18** FILE requires a distinct explicit commit after preview.
**UX19** One FILE commit changes exactly one column by +1.
**UX20** Max-depth column cannot arm FILE commit.
**UX21** Skipping filing animation yields identical settled state.
**UX22** `Confirm every cut` setting adds confirmation without changing action semantics.
**UX23** Undo immediately after FILE restores exact prior key profile and ledger/history state.

## TEST / feedback
**UX24** TEST animation's physical first blocker equals mechanical authority result.
**UX25** No column after first blocker is visually marked accepted/rejected by that failure.
**UX26** TOO_SHALLOW remains distinguishable without color and without audio.
**UX27** TOO_DEEP remains distinguishable from TOO_SHALLOW without color and without audio.
**UX28** BETWEEN_BRANCHES remains distinguishable from both other failures without color/audio.
**UX29** LIGHT vs STRONG, when shown, has non-color visual distinction.
**UX30** Accepted-prefix markers correspond only to columns actually evaluated before blocker.
**UX31** Successful OPEN leaves a persistent physical + icon/text completion state.
**UX32** Later filing of the opening key does not visually revoke OPENED completion.
**UX33** Repeated identical TEST can fast-forward presentation and adds no apparent new knowledge.

## Knowledge ledger
**UX34** Every ledger fact is labeled observed, deduced or unknown.
**UX35** Ledger never shows later-column information from a first-blocking failure.
**UX36** Deduced facts offer a `Why?` explanation from legitimate observations.
**UX37** Uncertain inference is never presented as DEDUCED.
**UX38** Ledger can be fully operated by controller.
**UX39** Ledger can return directly to corresponding key/lock physical inspection without changing state.
**UX40** Optional numeric depth labels reveal only key's public current depths, never hidden lock sets.

## Access / HUD
**UX41** Inaccessible lock states why it is inaccessible before any attempted TEST.
**UX42** Selecting an access predicate highlights referenced prerequisite locks.
**UX43** HUD does not require a permanent numeric matrix for optimal ordinary play.
**UX44** OPEN progress n/N is visible from normal bench state.

## History / recovery
**UX45** History contains every authoritative FILE/TEST in exact order and excludes camera/UI actions.
**UX46** Undo of TEST removes exactly the observations/access effects created by that action.
**UX47** Redo restores stored transition exactly.
**UX48** New authoritative action after Undo clears redo branch with non-modal feedback.
**UX49** Restart after actions requires one explicit confirmation; before actions it does not.
**UX50** Softlock warning is shown only after solver proof, never timeout/unknown.
**UX51** Softlock warning offers Undo, Restart and Continue Experimenting.
**UX52** Softlock warning does not identify the exact mistaken cut by default.

## Onboarding / hints
**UX53** C01 teaches TEST→blocker→FILE through physical focus plus <=1 short line at a time.
**UX54** C02 communicates accepted prefix in a persistent inspectable form, not animation alone.
**UX55** C03 teaches TOO_DEEP and recovery without requiring a punitive restart.
**UX56** C04 teaches lock switching/opened persistence without introducing new mechanics.
**UX57** C06 never explicitly tells the player `do not cut` before the intended discovery.
**UX58** Every tutorial callout can be reopened from Help.
**UX59** Hint tier 1 reveals no solver-only hidden accepted-set value.
**UX60** Hint tier 3 chooses only actions justified by current legitimate player knowledge.
**UX61** Repeating an identical TEST does not advance hint tier automatically.

## Menus / campaign / demo
**UX62** Case Select can be fully navigated by keyboard and controller.
**UX63** Optional mastery badges never block selecting the next base campaign case once ordinary completion requirement is met.
**UX64** Solved review distinguishes historical lock openings from final-state simultaneous key coverage.
**UX65** Demo D01–D06 use identical universal feedback/input semantics as full game.
**UX66** Full-game demo import never marks non-identical campaign cases solved.
**UX67** Invalid demo import falls back to normal onboarding without deleting source save.

## Accessibility / Deck
**UX68** Default Steam Deck controller configuration reaches every in-game function without external keyboard/mouse.
**UX69** 200% UI scale remains navigable without hiding mandatory controls; scrolling is allowed where needed.
**UX70** Core puzzle is completable with all audio muted and haptics off.
**UX71** Core puzzle is completable with color removed/desaturated.
**UX72** Core puzzle is completable with reduced motion and repeated animations skipped.
**UX73** Inspection zoom preserves stable readable labels and focus at Deck resolution.
**UX74** Controller glyphs have generic fallback when device family is unknown.

## Save/crash/conflict
**UX75** Autosave after FILE occurs only after authoritative transition is settled.
**UX76** Crash during filing animation restores either pre-commit or committed settled state, never fractional depth.
**UX77** Crash during TEST animation restores a settled state with knowledge exactly matching whether TEST committed.
**UX78** Corrupt current-case save does not silently erase campaign completion/settings.
**UX79** Divergent cloud/local saves present meaningful comparison rather than silently overwriting one.
**UX80** Recovery messaging states what was recovered without claiming an unfinished animation was authoritative.

## Presentation integrity
**UX81** No VFX exposes later-column fit information during a failed TEST.
**UX82** No audio-only event carries unique puzzle information.
**UX83** No haptic-only event carries unique puzzle information.
**UX84** Every transient critical failure mark has a persistent inspectable equivalent.
**UX85** Physical key mesh/profile after settle matches authoritative discrete key vector.
**UX86** Cylinder presentation after settle matches OPENED/access authority.
**UX87** A presentation/domain disagreement is treated as a blocking defect, never accepted as cosmetic.

---

# 20. Phase-6 closure

**PHASE 6 COMPLETE.**

The interaction/presentation layer now specifies:
- bench and camera authority;
- keyboard/mouse/controller/Steam Deck input abstraction;
- candidate-notch preview + explicit FILE commit;
- physical first-blocking TEST language;
- observed/deduced/unknown knowledge UX;
- HUD/access state;
- history, Undo/Redo/Restart and proven-softlock recovery;
- C01–C06 onboarding;
- hint ladder;
- menus/campaign/solved review;
- demo/full import behavior;
- accessibility baseline;
- save/crash/cloud-conflict UX contract;
- visual/audio/haptic/VFX boundaries;
- **87 UX/presentation acceptance tests**.

No frozen Phase-3/4/5 mechanic was changed and no production implementation was started.

## Phase 7 handoff
Next design phase is **Economy / retention / commercial model**. It should define premium pricing hypothesis, release/demo positioning, achievements/mastery/replay incentives, progression/unlock policy, platform features and hard monetization boundaries. It must not add grind, consumable hints, paid puzzle power, FOMO or a shop-management economy merely to create retention.
