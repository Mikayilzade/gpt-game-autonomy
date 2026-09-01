# GAME #012 — PHASE 6 UX / PRESENTATION ARCHITECTURE

Date: 2026-09-01
Status: **PHASE 6 COMPLETE**
Product: **OPENWORK** *(provisional working title)*
Authority: interaction, feedback, presentation, onboarding, accessibility, responsive layout and demo/full-game continuity. `GAME12_MECHANICS.md` remains authoritative for rules; `GAME12_CONTENT.md` remains authoritative for campaign/content structure.

## 1. UX thesis
OPENWORK must make the **remaining open space** feel like the active object. The player places solids, but the interface must visually privilege what remains: components, enclosed holes, marker groupings and boundary contacts.

Primary UX goals:
1. every legal placement is easy to preview and execute with controller or mouse;
2. every resulting topological consequence is legible immediately;
3. feedback explains **what changed**, not what move the player should make next;
4. no runtime feature becomes a solver/oracle;
5. undo/retry is near-frictionless because experimentation is part of deduction;
6. all important information remains readable at 1280x800 and handheld scale;
7. the same visual grammar survives from tutorial through mastery without adding interface systems.

## 2. Input model — controller first, mouse equivalent

### Controller baseline
Default bindings:
- Left stick / D-pad: move board cursor among cells.
- LB/RB: previous/next unplaced piece instance.
- LT/RT: rotate selected piece when its orientation policy allows rotation.
- A: place selected piece at current anchor if legal; if current selected placed piece is focused in inspect/reposition mode, confirm new placement.
- B: undo most recent placement action.
- X: pick up/remove the currently focused placed piece for repositioning; B restores prior state if no replacement is confirmed.
- Y: open/close topology inspect overlay.
- View/Select: objective detail panel.
- Menu/Start: pause.
- Hold B: reset confirmation shortcut; reset must never trigger from a brief accidental press.
- D-pad Up/Down while objective panel is focused: move predicate focus.
- Right stick, if present: optional camera/panel focus only; never required for play.

All bindings are remappable in full game. Demo may expose remapping if supported by shared settings architecture; demo must at minimum expose controller layout and sensitivity-independent digital navigation.

### Cursor movement
Cursor movement is cell-to-cell, not pixel-continuous. When a multi-cell piece is selected, the anchor cursor remains on one cell and the full footprint ghost follows it.

Cursor may move over FIXED_SOLID, marker and occupied cells for inspection, but placement ghost visibly shows illegality. Navigation never gets trapped by obstacles.

Wraparound cursor movement is **off** by default because edge contact is mechanically meaningful. Optional UI wraparound may exist only for non-board menus.

### Mouse baseline
- Hover cell: move board focus/anchor preview.
- Left click legal ghost: place.
- Left click placed piece: select for reposition/removal.
- Right click: undo one action.
- Mouse wheel or explicit rotate button: rotate selected rotatable piece.
- Objective icons are clickable/focusable for detail.
- No drag is required. Drag may be implemented as convenience only if click-place parity remains complete.

No information may exist only on hover.

### Keyboard parity
Keyboard must support every controller action, including board cursor, piece cycling, rotate, place, undo, inspect, objective details, pause and reset.

## 3. Piece selection / placement / reposition flow
A case opens with the first unplaced piece selected unless only one piece exists, in which case selection chrome is minimized.

Piece tray behavior:
- shows all required instances simultaneously when space allows;
- unplaced piece = solid silhouette + orientation-policy icon;
- selected = strong outline/focus frame;
- placed = dimmed in tray with a small board-location indicator;
- interchangeable instances may look identical, but tray still shows remaining count clearly.

Placement sequence:
1. select piece;
2. move anchor;
3. ghost footprint appears;
4. legality state is shown continuously;
5. press Place;
6. piece becomes PLACED_SOLID;
7. topology transition feedback runs immediately;
8. next unplaced piece becomes selected automatically unless player explicitly disables auto-advance in settings.

Reposition:
- focusing a placed piece and choosing Pick Up removes it into a temporary held state;
- the old placement remains visually ghosted as a restore reference;
- confirming a new legal footprint commits a single history action equivalent to remove+place;
- cancel restores the previous placement exactly;
- normal Undo after a committed reposition restores the old location/orientation.

## 4. Legal / illegal placement preview
The preview must explain legality without evaluating future objective success.

### Legal ghost
A legal footprint uses:
- semi-transparent solid fill;
- bright perimeter;
- small anchor notch at the canonical anchor cell;
- orientation indicator for bars.

### Illegal ghost
Illegal footprint remains visible but uses:
- cross-hatch/strike pattern independent of color;
- invalid cells each receive a small reason glyph;
- placement button does nothing except a soft reject pulse/audio tick.

Reason glyphs:
- outside board: clipped-edge symbol;
- FIXED_SOLID: blocked-square symbol;
- marker cell: marker-lock symbol;
- overlap with PLACED_SOLID: overlap symbol;
- disallowed orientation: rotation-lock symbol.

Never hide a ghost merely because it is illegal; the player should understand why.

## 5. Live topology feedback — informative, not an oracle
Live feedback may derive **only the topology of the player's current committed partial state**. It may not simulate hypothetical placements beyond the ordinary piece footprint ghost.

Allowed runtime feedback after each committed placement:
- current remaining-open component count;
- current enclosed-hole count;
- current component outlines;
- current marker grouping;
- current boundary contacts;
- current component/hole areas when the related predicate exists or when inspect overlay explicitly requests them;
- current truth state of each target predicate.

Forbidden oracle behavior:
- highlighting cells that belong to any solution;
- showing predicted topology for an uncommitted ghost placement;
- ranking candidate cells;
- saying “this placement is closer”;
- showing number of remaining solutions;
- showing certifier search-space counts during play;
- suggesting articulation cells, near-rings or correct piece roles;
- revealing whether a partial placement can still be extended to a solution.

This distinction is hard: **current-state explanation is UX; future-solution inference is a hint/solver feature and is outside Phase-6 baseline.**

## 6. Visual grammar
Color is supportive, never the sole carrier.

### REMAINING_OPEN
Default open cells are the visual protagonist:
- luminous/light recessed field;
- subtle continuous texture across connected cells;
- component outline appears only after topology inspect or after a topology-changing placement transition;
- the board background should not visually overpower open space.

When multiple components exist, each gets:
1. a distinct outline pattern/dash family;
2. an optional low-saturation tint;
3. a component badge/number in inspect mode, deterministically ordered by rules-core component ID only for stable UI—not as puzzle meaning.

Component IDs are never referenced by objectives.

### Enclosed holes
A hole is not rendered as “filled.” It remains visually open but receives:
- a closed double-outline / halo around its component perimeter;
- an inward-facing enclosure glyph in inspect mode;
- optional soft depth treatment suggesting a sealed pocket.

This prevents confusing “hole” with solid material.

### FIXED_SOLID vs PLACED_SOLID
Both are impermeable mechanically, but provenance must remain unmistakable:
- FIXED_SOLID: board-integrated material, darker/more architectural texture, no selectable outline.
- PLACED_SOLID: brighter/tactile insert, visible seams, selected/focus affordance, removable/repositionable.

Do not rely only on shade. Texture and edge treatment differ.

### Markers
Markers sit **inside remaining-open cells** and must read above region tint/pattern.
Each marker has:
- unique letter/symbol label (A–F baseline);
- unique silhouette ring or secondary shape slot where needed;
- high-contrast center;
- protected-cell placement-lock feedback if ghost overlaps it.

Marker identity cannot depend on color.

### Boundary contact
N/E/S/W board edges have tiny persistent orientation labels in inspect mode and optional subtle edge notches during normal play.
When a component is selected/inspected, every contacted boundary segment receives a pulse/outline and the corresponding N/E/S/W icon lights.

Boundary contact display must not imply pathfinding or shortest paths.

## 7. Predicate-card system
All objective predicates appear as compact cards/chips in a fixed objective rail. Cards use icon + short value; full natural-language explanation appears on focus/inspect.

Each card has four states:
- unmet current state;
- met current state;
- unavailable-to-evaluate only for malformed/internal error states (not normal partial play);
- success-locked during completion animation.

Partial states may show a predicate as currently met, but card chrome explicitly says `CURRENT` through a small dot/state marker rather than implying final success. Overall case completion can occur only after all pieces are placed and all predicates are true.

### Predicate visual contracts

#### COMPONENT_COUNT == n
Compact: region-cluster icon + `= n`.
Detail: “Leave exactly n separate open spaces.”
Inspect: outlines all current components; shows current count.

#### HOLE_COUNT == n
Compact: enclosed-pocket icon + `= n`.
Detail: “Leave exactly n enclosed open pockets.”
Inspect: highlights only current zero-boundary-contact open components.

#### COMPONENT_AREAS == [...]
Compact: region icon + ordered area tokens, e.g. `4 · 9 · 13`.
Detail: “The open spaces must have these sizes.”
Inspect: shows area badge inside each component; list is visibly a multiset, not tied to named regions.

#### ALL_COMPONENT_AREAS_IN [lo,hi]
Compact: region icon + `lo–hi`.
Detail: “Every open space must contain between lo and hi cells.”
Inspect: current area badge on every component with pass/fail outline.

#### HOLE_AREAS == [...]
Compact: hole icon + area tokens.
Detail: “The enclosed pockets must have these sizes.”
Inspect: hole area badges only.

#### ALL_HOLE_AREAS_IN [lo,hi]
Compact: hole icon + `lo–hi`.
Detail: “Every enclosed pocket must contain between lo and hi cells.”

#### SAME(A,B)
Compact: A—B joined-ring icon.
Detail: “A and B must remain in the same open space.”
Inspect: pulse both markers and their current shared component if true; if false, outline each component separately.

#### DIFFERENT(A,B)
Compact: A | B separated-ring icon.
Detail: “A and B must end in different open spaces.”

#### MARKER_COMPONENT_TOUCHES(marker, boundary_set, EXACT)
Compact: marker + mini compass frame with required edges emphasized + `=` glyph.
Detail example: “A's open space must touch exactly North and West.”

#### ... INCLUDES
Compact uses `+`/contains glyph.
Detail: “A's open space must touch at least these edges.”

#### ... AVOIDS
Compact uses crossed required boundary icons.
Detail: “A's open space must not touch these edges.”

#### COMPONENT_BOUNDARY_SIGNATURES == [...]
Compact: stacked mini compass frames, one per required signature, sorted only for display consistency.
Detail: “The final open spaces must have exactly these edge-contact patterns.”
Inspect: each current component shows its compass frame beside its outline.

### Compact handheld rules
At 1280x800:
- objective rail must fit up to 6 cards without requiring scrolling during ordinary play;
- if horizontal width is limited, use two rows of 3 rather than tiny icons;
- focusing a card expands a temporary readable detail panel without covering the selected board cell;
- minimum body text target is equivalent to approximately 18 logical px at 100% UI scale; implementation may tune physical rendering while preserving the readability gate.

## 8. Board / HUD responsive layout
Reference landscape layout:
- board: center-left or centered, largest visual object;
- piece tray: directly below or left of board depending aspect ratio;
- objective rail: right side on desktop/1280x800, bottom collapsible rail only on narrower aspect ratios;
- top bar: case title/progress, undo/reset/pause affordances;
- no permanent minimap or second visualization.

### 1280x800 hard readability target
A 9x9 board plus margins must fit without panning.
Target minimum board-cell visual size at 100% scale: **48 logical px preferred, 40 logical px absolute floor** after objective rail and safe margins. If chosen UI chrome would force smaller cells, chrome must compact/collapse before the board shrinks further.

Marker glyph, piece seams and invalid-placement symbols must remain recognizable at the 40 px floor.

### Focus order
Controller focus order is deterministic:
1. board cursor mode;
2. piece tray;
3. objective rail;
4. top-bar actions;
5. pause/settings when open.

One button always returns focus to board from side panels (default B/cancel if no destructive action is pending).

## 9. Topology inspect overlay
`Y` toggles a non-solver analysis layer over the **current committed state**.

Overlay may display:
- component outline/pattern + area;
- hole halo + hole area;
- marker component membership visually;
- boundary contacts per component;
- current objective truth relation.

Overlay must not:
- show articulation points;
- show hypothetical cuts;
- suggest candidate placements;
- show solution-space information.

Overlay persists through cursor movement but automatically suppresses any visually conflicting placement ghost details except the footprint itself.

## 10. Causal animation / audio
Feedback must be quick enough that repeated reasoning does not feel taxed.

### Placement sequence target
Nominal total causal feedback: **250–450 ms**, skippable/accelerated by subsequent input.
1. piece settles: 70–120 ms;
2. changed component boundaries redraw outward from changed cells: 120–220 ms;
3. newly enclosed hole gets a brief inward ring;
4. affected marker links/boundary icons pulse;
5. predicate cards update in parallel, not sequentially.

Do not animate flood-fill cell-by-cell. That would falsely imply time/order in a static topology evaluation.

### Event sound vocabulary
- legal place: short tactile click;
- illegal attempt: soft dry reject tick;
- split/merge-of-visible-region feedback: low paired tone;
- newly enclosed hole: compact hollow chime;
- predicate met/unmet transition: subtle rise/fall tick;
- all-complete success: one concise resolved chord.

No essential information is audio-only.

### Reduced motion
Reduced-motion mode:
- replaces redraw travel with instant outline change + 80–120 ms opacity crossfade;
- removes board shake, scale bounce and camera movement;
- retains state-change icons and optional sound.

## 11. First boot / first-session onboarding
No topology terminology is required in the first six cases. Tutorial copy uses ordinary language: “open space,” “separate spaces,” “enclosed pocket,” “touches an edge,” “together/apart.” Optional glossary may name formal terms later.

### First boot
1. title screen / Continue if save exists;
2. accessibility quick-start row before gameplay: text scale, reduced motion, high contrast, controller layout;
3. start campaign;
4. first case begins directly—no lore intro or modal rules wall.

### First six-case onboarding contract
Mapped to Act I intent, but exact case IDs come from certified content later.

Case 1 — scored object
- one piece;
- one simple component-count target;
- callout: “Place the piece. The open space is what matters.”
- after placement, component outlines appear automatically once.

Case 2 — markers
- teach SAME/DIFFERENT through marker glow and one short sentence;
- no new modal after first interaction.

Case 3 — enclosed pocket
- first hole predicate;
- on first created enclosure, game briefly labels it “enclosed open pocket.”

Case 4 — boundary touch
- first boundary predicate;
- objective inspect auto-opens only if player pauses on the card or requests detail; no forced long explanation.

Case 5 — inversion
- obvious neck is wrong;
- no tutorial text explains the trick; this is the first trust-the-rules aha.

Case 6 — light coupling
- two predicate classes interact;
- introduces optional topology inspect overlay if player has not used it.

After case 6, contextual tutorial callouts are off by default. New predicate types later may receive one short first-seen tooltip, dismissible and replayable from glossary.

### Tutorial anti-burden rule
No required tutorial panel may exceed **2 short sentences** or block more than one immediate action. If a concept needs more text, the visual grammar has failed and must be redesigned.

## 12. Completion / failure / recovery
There is no destructive failure state.

### Complete-but-unsolved placement
When all pieces are placed and predicates are not all true:
- board remains interactive;
- unmet cards pulse once, then remain steady;
- no “FAILED” modal;
- player may undo, pick up/reposition or reset immediately.

### Success
When all pieces are placed and all predicates become true:
- input remains buffered/ignored only for a very short success lock, target <=450 ms;
- completed topology gets a clean outline settle;
- cards lock as met;
- compact completion panel offers `Next`, `Replay`, `Case Select`;
- `Next` is default focused action.

No forced star score, move count, timer grade or perfection medal in baseline UX.

### Undo / reset
Undo must be available during essentially all ordinary board states.
Reset requires hold or confirmation but then clears instantly.

A case restart never loses campaign progress or settings.

## 13. Pause / settings / case select

### Pause
Pause overlay contains:
- Resume;
- Restart Case;
- Objectives / Glossary;
- Settings;
- Case Select;
- Main Menu.

No quit confirmation is needed unless an unsaved state could be lost; normal board state is autosaved, so quitting should be safe.

### Settings baseline
- master/music/SFX volume;
- text/UI scale;
- high-contrast mode;
- reduced motion;
- component pattern intensity;
- screen shake default off or minimal; if present it must be disableable;
- input remapping;
- controller glyph family auto/manual;
- auto-advance piece selection;
- hold-to-reset duration / confirm-reset alternative.

### Case select
Campaign map/list emphasizes solved/available state, not a decorative world map.
Each case tile may show:
- case number/title;
- solved check;
- principal learned visual icon only if helpful;
- no spoiler of exact solution/topology.

Unlock topology belongs to Phase 7 progression policy, but UX must support branching or sequential availability without redesign.

## 14. Save-facing presentation contract
Persistence details belong to Phase 8, but UX requires visible guarantees:
- autosave after every case completion;
- autosave current case board state after every committed placement/reposition/reset with debounce allowed, provided quit cannot silently lose the latest stable action;
- visible save indicator is subtle and only shown when useful, never a modal;
- `Continue` restores exact case and placements when supported by persistence contract;
- corrupted/incompatible save recovery must never strand the player in a broken board; detailed recovery rules belong to Phase 8.

## 15. Accessibility requirements
Hard Phase-6 requirements:
- full controller/keyboard/mouse parity;
- no hover-only information;
- no color-only marker/component/predicate distinction;
- remappable gameplay controls in full game;
- text/UI scale options, including target **150%** without clipping core menus/objective detail;
- high-contrast mode;
- component patterns/outlines remain distinct under common color-vision deficiencies;
- reduced-motion mode as defined above;
- no timing/reflex requirement;
- no mandatory audio cue;
- focus indicator always visible for controller/keyboard navigation;
- objective detail available in plain language;
- tutorial can be replayed / glossary accessible;
- success/failure meaning is not encoded only by red/green.

Localization readiness:
- no text baked into board art;
- icon-only compact cards always have localized detail text;
- layout must tolerate at least ~35% expansion over English labels without overlapping board controls.

## 16. Demo / full-game continuity
The Phase-5 protected demo is six cases. UX continuity rule: demo and full game must use the same board grammar, menus, controls, settings identifiers and case-completion presentation whenever technically possible.

### Demo completion
After final demo case:
- show concise “Demo complete” panel;
- offer replay/case select and store/exit action as platform permits;
- do not tease locked mechanics that do not exist in full game.

### Progress carry-over presentation
Phase 7/8 will freeze commercial/persistence details, but UX supports carry-over as follows:
- full game detects compatible demo progress;
- one non-blocking prompt: `Use demo progress?` with clear solved-count summary;
- accepting imports solved demo case IDs and shared settings where compatible;
- imported solved siblings are visibly marked as completed;
- campaign must not force replay of imported demo cases solely to unlock post-demo content;
- player can still replay any imported case voluntarily.

Declining import leaves demo data untouched until explicit cleanup policy is defined in technical spec.

## 17. First-session paper simulation
A new player launches with controller:
1. accessibility quick-start is readable and dismissible in seconds;
2. Case 1 immediately shows board, one piece, one objective card;
3. selected piece ghost follows cell cursor;
4. player tries marker/solid/edge overlap and receives specific illegal reason without losing state;
5. legal placement instantly redraws remaining-open outline;
6. objective card changes current truth state;
7. all pieces placed + target true produces compact success panel;
8. Next starts Case 2 with no map/menu detour;
9. by first hole case, visual enclosure halo conveys the concept before formal terminology is needed;
10. by Case 6, player can voluntarily inspect areas, components, holes and edge contacts but has never been shown a correct move.

This satisfies the product promise: reason about stable visible consequences, not UI-debug a hidden simulation.

## 18. UX anti-oracle acceptance gates
Before design freeze / implementation acceptance, representative mid/late cases must verify:
1. a player can understand **why the current state fails** using board + objective inspect without solution hints;
2. placement ghost reveals geometry legality only;
3. live objective badges do not reveal future solvability;
4. topology inspect does not expose articulation/candidate analysis;
5. rapid undo does not accidentally become an optimal brute-force UI because completion feedback is not more informative than current-state truth;
6. component/hole distinction remains readable in grayscale/high-contrast treatment;
7. 9x9 board + six objective cards remains usable at 1280x800;
8. 150% text scale preserves complete access to objective detail and menus, with panels allowed to scroll but gameplay board not requiring pan.

## 19. Explicit presentation exclusions
Phase 6 does not add:
- animated characters;
- narrative dialogue layer;
- 3D camera manipulation;
- procedural material physics;
- solution heatmaps;
- hint arrows;
- move-score grading;
- daily streaks;
- cosmetic progression;
- workshop/level editor;
- touch-first gesture requirements.

These require later explicit product revision, not incidental implementation.

## 20. Phase-6 conclusion
OPENWORK's exact topology rules can be presented with one stable visual language and one controller-first interaction model. The central UX tension is resolved by separating **current-state topology explanation** from **future-solution inference**: players may inspect exactly what their committed placements have done, but never receive certifier-derived advice about what to do next.

The board remains the dominant visual object; open-space components, enclosed holes, marker relations and boundary contacts all have color-independent representations. Tutorial burden stays low, rapid recovery is first-class, and the complete interface is designed to survive 1280x800 / handheld presentation.

**PHASE 6 = COMPLETE.**

Next authority task: Phase 7 Commercial / Retention must use fresh market/pricing research to freeze premium price posture, progression/unlock policy, demo carry-over policy, achievements, replay incentives, hint stance and platform-feature boundaries without adding live-service pressure or undermining the compact authored-puzzle thesis.
