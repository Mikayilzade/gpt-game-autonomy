# GAME #003 — BORROWED COLLISION — UX / PRESENTATION ARCHITECTURE

Last updated: 2026-08-19
Factory run: **10**
Phase: **6 — UX / Presentation Architecture**
Product thesis: **LOCKED**
Mechanical architecture: **COMPLETE ON PAPER**
Content architecture: **COMPLETE ON PAPER**
DESIGN COMPLETE: **NO**

This file is the canonical Phase-6 interaction and presentation contract for Borrowed Collision. It presents the frozen Phase-3/4/5 rules without adding new impact properties, transform families, receiver mechanics, numerical vector controls, free-angle aiming, reflex capture or inventory systems.

If presentation convenience conflicts with `GAME3_MECHANICAL_ARCHITECTURE.md`, the mechanical architecture wins unless Phase 4 is explicitly reopened. If content convenience conflicts with this file, the UX rule here wins unless Phase 6 is explicitly reopened.

Current Steam/Deck references checked 2026-08-19:
- Steam Deck compatibility recommends 1280×800 support and legible UI text, with 9 px an absolute minimum character-height criterion and 12 px a recommended target where practical: https://partner.steamgames.com/doc/steamhardware/compat
- Steam Input is action-oriented and supports controller remapping/device-specific glyphs; the implementation should expose semantic actions rather than hard-code physical buttons: https://partner.steamgames.com/doc/features/steam_controller
- Steam Input documentation recommends controller-specific glyph handling and user customization rather than assuming one controller layout: https://partner.steamgames.com/doc/features/steam_controller/getting_started_for_devs

These references inform platform/readability targets only. They do not define gameplay.

---

# 1. UX contract

At any meaningful moment, the player must be able to answer five questions without opening debug telemetry:

1. **What physical event created this captured impact?**
2. **What direction and magnitude does the impact currently have?**
3. **What can accept it here, and what transformation will happen before spending?**
4. **What did the last spend/collision actually change?**
5. **Why is the current case complete, incomplete, unsafe or dead-ended?**

The desired rhythm is:

**inspect world -> notice/engineer collision -> impact condenses -> collect -> carry/transform -> preview compatible spend -> commit -> watch bounded consequence -> inspect causal aftermath -> revise**.

The player is never asked to:
- read x/y vectors;
- infer force from color alone;
- free-aim an arbitrary angle;
- catch an impact during a frame-timed animation;
- memorize a donor's origin after carrying it through several rooms;
- watch a long rigid-body simulation finish before understanding failure;
- manage dozens of stored tokens;
- use an engineering dashboard as the main play surface.

---

# 2. Application / screen-state hierarchy

## 2.1 First launch

`Boot -> Accessibility & Input Quick Setup -> Title -> Case Board -> Case Brief -> Case Play -> Completion -> Case Board`.

First-launch quick setup exposes:
- UI/text scale;
- reduced motion;
- impact flash/camera-shake reduction;
- subtitle/text-event presentation;
- controller glyph auto-detection with manual override;
- hold/toggle preference for inspection/slowdown where relevant.

The player may accept defaults immediately. No mandatory cinematic or lore intro precedes the first interactive case.

## 2.2 Title screen

Primary actions:
- Continue;
- Case Board;
- Settings;
- Accessibility;
- Help / Rules;
- Credits;
- Quit on desktop.

`Continue` loads the latest verified safe case state or Case Board if no active case exists.

## 2.3 Case Board

Case selection is a compact physical/diagrammatic board rather than a walkable hub.

Each case card shows:
- case ID/title;
- cleared / uncleared;
- optional mastery marks earned;
- tutorial/new-concept badge only when relevant;
- replay/remix marker when unlocked.

The board does not display currencies, XP bars, energy, lives or grind loops.

## 2.4 Case state machine

`Brief -> Inspect/Edit/Traverse -> Resolution Transaction -> Inspect/Edit/Traverse -> Completion`.

Pause may overlay any non-transition state. Moving-body resolution may be paused/stepped according to the mechanical contract but pause/step never changes canonical collision semantics.

## 2.5 Completion screen

Completion shows:
- baseline clear;
- optional mastery results only when authored;
- one compact final causal summary;
- donor/source preservation state when relevant;
- Replay;
- Next Case;
- Case Board.

Completion does **not** score:
- raw Undo count;
- total failed attempts;
- elapsed thinking time;
- amount of pausing/stepping;
- input device.

---

# 3. Canonical in-case layout

## 3.1 Desktop landscape default

The default layout prioritizes the physical room, not panels.

- **World viewport:** 68–76% of usable area.
- **Case rail:** 18–24% width, collapsible.
- **Impact belt:** compact horizontal/vertical strip integrated near the player/world edge; maximum 3 held slots.
- **Top utility/history strip:** Undo, Redo, Pause/Step state, active room breadcrumb, case menu.
- **Inspection card:** contextual overlay/panel that occupies no more than ~28% of the screen and closes without losing world focus.

The world remains visible while selecting impacts, receivers and transforms. A modal inventory screen is forbidden for ordinary play.

## 3.2 Steam Deck 1280×800 target

Deck default:
- world viewport remains the majority surface;
- case rail becomes a slide-over panel;
- objectives collapse to 2–4 concise status rows/chips, expandable on demand;
- impact belt stays permanently readable because inventory is only 2–3 items;
- inspection opens as a bottom/side card while preserving selected world object context;
- no required panel relies on horizontal text scrolling.

Project UI should target comfortably readable ordinary text above the Steam Deck minimum rather than designing to the absolute floor.

## 3.3 Room breadcrumb

Multi-room cases show a stable breadcrumb such as:
`Freight Annex / Bay 2 of 3`.

It exists for orientation only; rooms are not numbered as a hidden puzzle ordering hint. The player can inspect linked rooms already visited and any explicitly visible destination connection.

---

# 4. Impact visual language

A captured impact must read as **a piece of a real crash**, not abstract ammo.

## 4.1 Direction

Direction uses:
- arrow geometry as primary signal;
- eight snapped compass orientations;
- optional short text on inspect (`East`, `North-East`, etc.);
- matching orientation on belt, world pickup, converter preview and receiver preview.

Direction is never encoded by color.

## 4.2 Magnitude

Magnitude is encoded redundantly:
- WEAK: one chevron / smallest body;
- MEDIUM: two chevrons / medium body;
- STRONG: three chevrons / largest body;
- plain-language label on inspect and in accessibility/high-clarity mode.

Animation emphasis and sound may reinforce magnitude but cannot be the sole signal.

## 4.3 Provenance / lineage

Every impact has a subtle source stamp:
- donor/source icon or short stable source nickname;
- latest collision symbol;
- lineage marker when impact came from a secondary collision.

The default belt shows only compact provenance, e.g. `Crate B -> Gate Bumper` iconography. Full lineage is one Inspect action away.

A player carrying an impact between rooms must not need memory to recall where it came from.

## 4.4 World pickup

When an eligible collision resolves:
1. collision flashes/pulses once;
2. impact condenses into a persistent pickup at the capture location;
3. pickup visibly inherits direction/magnitude/provenance;
4. if inventory has room, pickup may be collected by ordinary interact;
5. if inventory is full, pickup remains in world and is visibly indexed on the room map/breadcrumb.

No timed catch prompt exists.

## 4.5 Inventory slot identity

Held slot displays:
- direction glyph;
- magnitude chevrons;
- provenance stamp;
- transformed-state marker only when it has passed through a fixed device.

No rarity frame, durability meter, element icon, upgrade star or numerical value is allowed.

---

# 5. Donor / source presentation

## 5.1 Capture-enabled source

A source that can emit a harvestable impact uses a consistent `capture source` affordance visible before the collision. It must not imply that every collision in the world is harvestable.

## 5.2 Regeneration classes

Player-facing distinction must be visible without using internal enum names unless glossary is opened.

- **EXHAUSTIBLE:** one-use source marker; after use, visibly spent/broken/empty.
- **RESETTABLE:** source shows its reset mechanism and current reset state; reset path is inspectable.
- **CYCLIC_WEAK:** rhythmic/loop marker plus WEAK output identity; it must not look like an unlimited generic ammo dispenser.
- **CHAIN_GENERATED:** no special pre-source badge is necessary; causal lineage after the secondary collision identifies that the new impact came from the prior spend/chain.

Inspection may expose the formal class names in Help/advanced detail.

## 5.3 Donor preview boundary

Before a collision is triggered, the UI may show:
- that a relation is capture-enabled;
- the movement lane involved;
- the body mass class using words/icons;
- the known output envelope if the collision state is already fully determined.

It may **not** rank whether that donor is strategically best or reveal a full downstream solution chain.

---

# 6. Receiver compatibility language

Every receiver communicates four independent ideas:
1. can this impact structurally enter?
2. which directions are accepted?
3. which magnitude bands are safe/useful/unsafe?
4. what world-state family changes if committed?

## 6.1 Compatibility states

- **Compatible:** receiver can legally accept current impact.
- **Compatible but unsafe/adverse:** legal spend, but visible family rule predicts breakage/overshoot/undesirable band outcome.
- **Structurally incompatible:** cannot commit; exact incompatibility is shown.
- **Disabled/unavailable:** receiver exists but cannot currently receive because its visible enabled condition is false.

Do not label legal-but-bad as input error.

## 6.2 Direction sockets

Accepted direction(s) are shown as physical slot arrows around/on the receiver. When selected, only authored valid snap orientations are focusable.

The player never rotates an impact freely in empty space.

## 6.3 Safe / unsafe magnitude bands

Use a three-band strip with icons and plain-language semantics:
- safe/useful bands;
- accepted-but-dangerous band(s);
- structurally rejected band(s) when relevant.

Examples:
- fragile actuator: WEAK/MEDIUM safe, STRONG `will break`;
- exact window: MEDIUM useful, WEAK `insufficient`, STRONG `overshoots`.

A legal adverse result may be previewed at the **family level** (`will break receiver`, `will move past first stop`) because this is a known direct consequence, not a hidden multi-step solution spoiler.

---

# 7. Pickup / select / carry / transform / spend flow

## 7.1 Collect

World pickup -> focus/select -> `Collect`.

If a slot is free:
- impact moves to first available belt slot;
- provenance remains intact;
- world marker disappears;
- no simulation time advances unless collection itself is explicitly a canonical player movement action already specified mechanically.

If inventory is full:
- collect is disabled with `Impact belt full (2/2)`;
- the pickup remains safely in world;
- player may select a held impact to spend elsewhere first.

No generic discard command is required for baseline 1.0. If an optional discard is later allowed for convenience, it must be explicit, reversible only by Undo/history rules, and cannot duplicate/reset the source.

## 7.2 Select held impact

One button/key cycles 2–3 held slots. Selection is immediate and never opens a separate backpack UI.

Selected impact causes compatible nearby receivers/transforms to receive subtle focus affordances. It does **not** reveal which one is strategically correct.

## 7.3 Transform

Select impact -> select transform device -> preview exact deterministic result -> confirm.

Preview shows:
- before arrow/band;
- device operation icon;
- after arrow/band;
- unchanged provenance/lineage.

Quarter-turn/reverse/mirror/damper are visually physical operations. Transform history remains inspectable but is not shown as a verbose chain unless requested.

A transform is not a spend. After transform, the same impact returns to held/world state according to Phase 4.

## 7.4 Spend

Select impact -> focus compatible receiver -> choose one authored snap orientation if multiple -> inspect direct consequence -> confirm.

Commit feedback:
1. impact leaves belt;
2. short source-line tether traces from impact/provenance to receiver;
3. receiver motion/trigger begins;
4. deterministic transaction resolves;
5. secondary collision outputs condense only after their canonical event resolves;
6. objective/invariant status updates;
7. causal ribbon becomes available.

## 7.5 Cancel

At any pre-commit step, Cancel returns to world focus with no state mutation.

---

# 8. Preview boundaries: informative but not an oracle

## 8.1 Allowed pre-commit information

The UI may show facts deterministically implied by the **immediate selected action**:
- selected direction and magnitude;
- receiver accepted/safe/unsafe bands;
- fixed transform output;
- first authored lane that the receiver will enter;
- direct break/open/latch family consequence;
- receive-window state when the receiver is currently at a valid canonical window.

## 8.2 Forbidden pre-commit oracle behavior

The UI may not:
- trace the full future multi-collision chain before the player has created it;
- identify the best donor;
- highlight the intended receiver;
- rank token choices;
- show `this completes objective 3 after four steps`;
- reveal hidden known-solution fixtures;
- automatically propose converter sequences.

After events happen, causal explanation may be complete and explicit.

---

# 9. Body / donor / receiver inspection

Inspection is one unified command available through pointer, keyboard focus and controller.

## 9.1 Body card

Shows only mechanically relevant information:
- body name/icon;
- mass class in plain language/icon;
- current canonical location/state;
- current movement direction/band if moving;
- relevant receiver/source family tags translated into player language;
- current broken/open/latched/spent state;
- if its current motion came from a portable impact, source lineage shortcut.

No raw IDs or physics coefficients in normal mode.

## 9.2 Donor card

Answers:
- can this collision produce a stored impact?
- what is the donor's current availability state?
- is it one-use, visibly resettable or cyclic weak?
- what source world-state changes when it resolves?
- if already harvested, which impact/lineage came from it?

## 9.3 Receiver card

Answers:
- accepted directions;
- accepted/safe/unsafe magnitude bands;
- current enabled state and why;
- first direct result on receipt;
- whether it is moving and which receive-window states exist.

## 9.4 No engineering telemetry

Normal inspection excludes:
- numeric vectors;
- collision table indices;
- internal state hashes;
- frame/tick counters beyond player-facing step/window labels;
- exhaustive future path search.

A developer/debug build may expose those separately later.

---

# 10. Causal explanation / lineage UX

## 10.1 Causal ribbon

After a spend or collision transaction, default causal ribbon shows the shortest material chain relevant to the selected/broken requirement or selected impact.

Canonical presentation pattern:
`Stored impact from Crate B -> quarter-turn socket -> Cart 2 receives MEDIUM East -> Cart 2 hits Gate Bumper -> new WEAK North impact created -> Door objective changes`.

The ribbon defaults to **<=5 material nodes** and **<=2 sibling branches visible**. Extra consequences collapse under `More affected`.

This is a Phase-6 presentation budget, not a simulation restriction.

## 10.2 Provenance drill-down

Selecting a held/world impact can open:
`Source collision -> transforms -> current impact`.

Selecting a newly generated impact shows its parent spend/collision lineage. This must make CHAIN_GENERATED consequences feel like causal inheritance rather than spawned ammo.

## 10.3 Requirement explanation

Selecting a broken requirement shows:
- current false fact in plain language;
- first material event that made it false where available;
- shortcut to affected body/receiver/source;
- no recommendation for the next move.

## 10.4 Event compression

Repeated movement steps that do not materially alter collision/receiver/objective state are collapsed. The player can expand advanced history, but normal causal view should not become an event log wall.

---

# 11. Pause / Step / moving receive windows

## 11.1 Pause semantics

During moving-body resolution, Pause freezes presentation at the next canonical movement-step boundary. It does not stop midway through an authoritative lane segment.

If Pause is pressed during interpolation, presentation finishes/settles visually to the corresponding canonical boundary and then pauses.

## 11.2 Step

`Step` advances exactly one canonical movement step / collision-boundary resolution unit, then pauses again.

This makes moving-window reasoning accessible without changing outcomes.

## 11.3 Receive-window display

A moving receiver has discrete window states visible in Pause/Inspect:
- `Closed now`;
- `Receives from East now`;
- `Receives WEAK/MEDIUM now`, etc.

A timeline strip may show **the receiver's authored loop states** if those states are already known/deterministic, but it must not simulate arbitrary future branches caused by uncommitted edits.

## 11.4 Slowdown

Presentation speed presets may include 1×, 0.5×, 0.25× or similar. Speed never changes canonical step outcomes.

Baseline completion may be earned at any speed/Pause/Step usage.

---

# 12. Undo / Redo / history presentation

## 12.1 History unit

One accepted semantic player action is one history card:
- collect if Phase-4 implementation treats it as a canonical state action;
- transform;
- spend;
- donor reset/trigger;
- authored player traversal/self-launch command where it mutates state.

Derived collisions are nested inside the parent transaction, never presented as separate user mistakes.

## 12.2 Undo

Undo restores exact prior canonical checkpoint. UI feedback:
- world state snaps/reverses with reduced-motion-safe transition;
- held/world impacts and provenance restore exactly;
- lineage ribbon rewinds to prior transaction;
- no `Undo penalty` indicator exists.

## 12.3 Redo

Redo restores/replays only the intact linear branch. New accepted action after Undo truncates redo branch according to Phase 4.

## 12.4 History strip

Compact icons show the player's accepted choices, not every collision. Expanding one card reveals nested causal consequences.

This lets players understand experimentation without turning the game into a programming debugger.

---

# 13. Multi-room navigation and pickup retrieval

## 13.1 Room transitions

Moving between rooms uses ordinary player traversal/doorways, not a separate map-navigation game.

When a world pickup remains in another visited room:
- room breadcrumb receives a small impact-count badge;
- opening case map/room overview shows pickup icon with direction/magnitude/provenance summary;
- selecting the marker frames the room/route information already discovered.

No automatic teleport/retrieval of portable impacts is allowed by default because physical carrying and room state matter.

## 13.2 Anti-backtracking rule

Content must not create inventory-pressure busywork by forcing repeated long empty walks between known pickups and receivers.

UX/content guardrail:
- once a path is solved and contains no unresolved causal state, traversal back through it may use an optional fast-return/room-snap presentation only if the player's canonical state and carried impact route are unaffected;
- such convenience cannot cross hazards, moving windows, donor resets, unresolved receivers or states where carrying the selected impact changes accessibility;
- otherwise physical traversal remains required.

This is convenience presentation, not a new teleport mechanic.

## 13.3 World pickup indexing

Case overview never hides a stable uncollected impact. It lists visited-room pickups so a two-slot belt does not become a memory test.

---

# 14. Self-launch UX

Self-launch must feel like the same consequence-transfer grammar, not a sudden precision platformer.

## 14.1 Commit flow

Select held impact -> focus R6 Self-Launch receiver -> valid authored launch lane(s) appear -> preview direction/band and destination envelope -> confirm.

No analog aiming/free trajectory arc exists.

## 14.2 Camera

Before commit:
- camera frames origin and immediate destination/first boundary when possible.

During launch:
- camera tracks smoothly but prioritizes destination/collision readability over spectacle;
- reduced-motion mode uses constrained tracking and minimal zoom.

After collision/settle:
- camera holds long enough to show what happened;
- if a secondary impact is generated, its pickup and lineage highlight are visible before camera returns to player control.

## 14.3 Recovery

A legal self-launch may create an undesirable/dead-end state; this is allowed and Undo/Restart remains immediate.

Ordinary baseline cases must not require air control, reflex steering, frame-perfect landing or pixel-perfect launch timing.

---

# 15. Controls / semantic action grammar

The implementation must use semantic actions so mouse/keyboard/gamepad/Steam Input mappings can vary without changing game rules.

## 15.1 Core semantic actions

- Move / navigate world focus
- Interact / collect
- Select impact next / previous
- Open compact impact belt
- Inspect
- Focus next / previous nearby compatible object
- Confirm
- Cancel
- Undo
- Redo
- Pause / Resume transaction
- Step transaction
- Open Case Rail
- Open Room Overview
- Help / Glossary
- Zoom / camera focus where presentation supports it

## 15.2 Mouse + keyboard

- pointer click selects world objects;
- WASD/arrow movement according to traversal mode;
- left click / Enter confirm;
- right click / Esc cancel may be offered, but Cancel must also exist on keyboard independently;
- Q/E or configurable actions cycle impacts/nearby compatible targets;
- Tab cycles major UI regions;
- Z/Y or remappable Undo/Redo defaults;
- Space toggles Pause/Resume during moving resolution; separate Step binding available.

No required drag gesture, mouse wheel or hover-only information.

## 15.3 Keyboard-only

World objects and pickups have a deterministic logical focus graph.

- arrows/WASD move player when free traversal is active;
- Tab/Shift+Tab cycle major regions;
- dedicated `Focus Next Interactable` cycles nearby donor/receiver/transform/pickup candidates in stable authored order;
- Enter/Space confirm;
- Esc cancel;
- Q/E impacts;
- I inspect;
- U/R or remappable Undo/Redo;
- P Pause, `.` or remappable Step.

No virtual mouse requirement.

## 15.4 Controller-only

Default conceptual mapping, remappable:
- left stick/D-pad: move / logical focus;
- A: interact/confirm;
- B: cancel/back;
- X: impact belt / impact cycle context;
- Y: Inspect;
- LB/RB: previous/next held impact or nearby valid receiver depending explicit mode;
- LT/RT: previous/next inspectable causal/history item when Inspect/history mode active;
- Menu: Pause/Case menu;
- View/secondary: Room Overview;
- one remappable action: Step while paused.

Context-sensitive shoulder use must always display current glyph/function. While a spend/transform gesture is active, shoulder buttons cannot silently switch from impact selection to room navigation.

## 15.5 Steam Input / glyph policy

The game should model controls as semantic actions and display controller-specific glyphs where available. Physical glyph assumptions are presentation data, not gameplay logic.

Players may mix controller/mouse/keyboard without corrupting focus or domain state.

---

# 16. Deterministic focus/navigation graph

Every authored room compiles a logical focus order for:
- pickups;
- donor/source inspect points;
- receivers;
- transform devices;
- room exits;
- self-launch receivers;
- case-rail/history controls.

Rules:
- auto-generation from presentation geometry may create a draft;
- authored overrides are allowed and expected in dense rooms;
- all required interactables must be reachable through keyboard/controller focus;
- focus order may not depend on frame layout, zoom level, floating-point nearest comparisons, hash iteration or scene creation order;
- cycling nearby compatible receivers uses stable authored priority then stable ID;
- current selected impact may filter to compatible candidates, but player can still enter Inspect mode on incompatible objects to learn why.

---

# 17. Accessibility contract

Required for 1.0:

## 17.1 Visual redundancy
- direction: arrow geometry + optional compass text;
- magnitude: chevrons/size + text;
- provenance: source icon/label, never color only;
- compatibility: shape/icon/pattern + text;
- safe/unsafe: explicit icon/text distinction;
- donor regeneration state: visible symbol + state text;
- moving receive window: shape/icon and plain-language state.

## 17.2 Motion / flashing
- reduced camera shake;
- reduced screen flash;
- reduced-motion mode removes dramatic token flight/tether sweeps and uses discrete source->pickup->receiver emphasis;
- simulation result remains identical.

## 17.3 Audio redundancy
Every essential impact/capture/break/window cue has visual/text equivalent. Volume controls are separated for master/music/SFX/UI.

## 17.4 Timing
- Pause/Step available wherever moving-body timing matters;
- slowdown available;
- no baseline achievement/mastery invalidation for using these access tools;
- no ordinary reflex capture;
- no frame-perfect self-launch.

## 17.5 Input
- remappable keyboard/gamepad actions;
- keyboard-only complete;
- controller-only complete;
- no analog-only precision;
- hold/toggle options where continuous actions exist;
- Reset Controls always reachable.

## 17.6 UI scale / text
- scalable UI presets;
- Deck-readable default at 1280×800;
- critical panels tolerate localization expansion without clipping;
- compact text uses readable mixed case, not tiny all-caps industrial decoration.

## 17.7 Cognitive clarity
High-clarity mode may:
- always show direction names;
- always show WEAK/MEDIUM/STRONG labels;
- keep source provenance text expanded;
- reduce simultaneous nonessential decorative motion.

It may not rank solutions or alter deterministic mechanics.

---

# 18. Case brief / goals / invariants

The Case Brief contains:
- one short physical problem statement;
- required goals;
- protected invariants separated visually;
- available donor/source types when already known;
- available transforms/receiver families only when relevant;
- optional mastery in subordinate section.

During play, Case Rail shows requirement rows with:
- satisfied;
- broken;
- pending moving-state outcome;
- not currently evaluable.

Expanding a row explains the current physical predicate and highlights subjects/targets. It does not reveal the solution.

Maximum visible complexity follows Phase-5 clause ceilings; machine-level predicates may be grouped into one coherent player requirement.

---

# 19. First-session onboarding

Onboarding is consequence-first and embedded in DEMO/campaign cases.

Teaching method:
1. show a collision;
2. let the impact condense visibly;
3. prompt one collection;
4. show one compatible receiver;
5. player spends impact;
6. world consequence resolves;
7. player is asked to inspect source lineage once;
8. next micro-problem removes step-by-step guidance and requires transfer.

One new interaction concept at a time. Tooltips become recoverable Help entries after first use.

A wrong-but-legal spend should occur early enough that the player learns `bad physical consequence` is not `input error`.

---

# 20. Demo UX — DEMO01..DEMO05

The demo remains 15–25 minutes and obeys Phase-5 content scope.

## DEMO01 — Stored crash
Collision -> pickup -> collect -> ordinary mover.
Goal: understand `crash became portable`.

## DEMO02 — Direction / quarter-turn
Stored impact cannot be freely rotated; use visible socket.
Goal: physical transforms, not vector editor.

## DEMO03 — Magnitude suitability
WEAK/MEDIUM distinction and first fragile/unsafe STRONG consequence.
Goal: stronger is not universally better.

## DEMO04 — Provenance / donor consequence
Use an impact; donor/source state now matters for the remaining problem.
Goal: prevent `arrow inventory` interpretation.

## DEMO05 — Secondary collision synthesis
Spend impact -> moving body -> secondary real collision -> new lineage/pickup -> final receiver/self-launch.
Goal: prove recursive causal reuse and end on the product's strongest `aha`.

Demo excludes:
- 3-slot inventory;
- RESETTABLE/CYCLIC_WEAK complexity unless a tiny visible reset is required only for onboarding polish;
- multiple simultaneous moving receive windows;
- long multi-room retrieval;
- advanced mastery;
- dense chain lengths.

The demo must end after the player intentionally creates and reuses a secondary consequence, not after a trailer-only cliffhanger.

---

# 21. Pause / settings / help / save-load-recovery UX

## 21.1 Pause menu
- Resume;
- Restart Case;
- Settings;
- Accessibility;
- Help / Rule Glossary;
- Case Board;
- Quit.

Leaving/restarting asks confirmation only when active progress would be discarded.

## 21.2 Settings
Categories:
- Gameplay Presentation;
- Controls;
- Accessibility;
- Audio;
- Display;
- Language.

No gameplay setting should silently mutate canonical rules unless Phase 7/8 later explicitly defines an assist variant.

## 21.3 Help / glossary
Entries unlock as concepts are introduced and explain:
- direction;
- magnitude;
- provenance;
- donor states;
- receiver families;
- converters/damper;
- self-launch;
- Pause/Step;
- world pickups;
- causal lineage.

Each entry contains a tiny non-solution example. No dossier walkthroughs by default.

## 21.4 Autosave indication
UX requires a small save indicator only after a state is durably accepted by the persistence layer. Phase 8 defines implementation internals.

## 21.5 Recovery
If a session cannot restore the latest in-progress state exactly, the game must fall back only to a verified safe checkpoint and explain plainly what was restored.

Never display a partially reconstructed collision chain as if exact.

---

# 22. Visual / animation language

The world should intentionally advertise **stylized discrete causal physics**.

## 22.1 Physical look
- chunky machinery;
- authored rails/lanes/bumpers;
- obvious contact boundaries;
- readable silhouettes;
- visible impact sockets;
- no photorealistic free-body chaos promise.

## 22.2 Collision animation
A collision should communicate:
`approach -> contact -> consequence -> impact condenses`.

The animation may embellish, but canonical result is already decided.

## 22.3 Token movement
Portable impacts feel physical but lightweight:
- pickup condenses near source;
- collecting pulls it to belt/player with short path;
- transform visibly rotates/mirrors/damps the token;
- spending visibly hands force to receiver.

Reduced-motion mode replaces travel sweeps with discrete highlight/fade transitions.

## 22.4 Secondary collision highlight
When a spent impact creates a second harvestable collision, presentation briefly marks ancestry (`from your stored impact`) before the new pickup condenses.

This is essential to the product thesis.

---

# 23. Audio language

Audio reinforces causal categories:
- collision family impact;
- harvest/capture cue;
- weak/medium/strong weight character;
- transform device cue;
- receiver accepted/safe/unsafe result;
- breakage;
- secondary lineage creation;
- objective state change.

No unique gameplay information is audio-only.

Avoid realistic physics-audio clutter where many simultaneous contacts obscure the important authored event.

---

# 24. UX empirical risks / gates

## U6-R1 — Arrow bookkeeping perception
Risk: impacts feel like inventory tokens detached from their physical source.
Gate: after the demo, representative testers should describe at least one impact by its source event (`the crate crash`, `the cart hit`) without prompting, not only by `east medium`.

## U6-R2 — Direction/magnitude confusion
Risk: quantization is unreadable without numbers.
Gate: <=20% ordinary failures in the prototype should be primarily caused by misreading direction/magnitude, preserving Product Thesis empirical gate.

## U6-R3 — Receiver icon overload
Risk: safe/unsafe/compatibility/provenance symbols become engineering telemetry.
Gate: new testers can identify `can accept / will break / wrong direction` from the selected receiver presentation without opening Help by the end of early teaching.

## U6-R4 — Multi-room pickup memory/backtracking
Risk: two-slot capacity becomes tedious retrieval.
Gate: testers can locate every previously seen uncollected impact from room overview without verbal memory and do not spend material session time traversing already-solved empty routes solely because the UI hid pickup state.

## U6-R5 — Self-launch turns into platformer
Risk: camera/aim/timing dominates reasoning.
Gate: controller and keyboard testers complete early self-launch cases without unsnapped aiming or reflex steering; failures are explainable as wrong chosen impact/lane rather than dexterity.

## U6-R6 — Causal ribbon becomes debug console
Risk: explanation is too verbose or becomes a solution oracle.
Gate: testers can answer `where did this impact come from?` and `why did this receiver break?` from default/one-level-expanded view without reading raw event logs.

## U6-R7 — Moving windows remain timing barrier
Risk: Pause/Step exists but presentation is still unclear.
Gate: a Pause/Step user can deliberately hit required authored receive windows with no worse rule comprehension than real-time users.

## U6-R8 — Controller focus ambiguity
Risk: dense rooms produce accidental receiver selection.
Gate: controller-only testers can complete demo/early campaign with no persistent need for virtual mouse and with low accidental commit rate after onboarding.

## U6-R9 — Discrete physics looks broken
Risk: lane/band quantization feels like fake physics rather than intentional causal grammar.
Gate: visual language makes snap lanes, impact bands and device rules feel designed; user expectation interviews should not predominantly ask for freeform realistic simulation.

---

# 25. Phase-6 acceptance tests

## Application / hierarchy
- **U6-01** First launch exposes accessibility/input quick setup before mandatory gameplay.
- **U6-02** Case Board, Case Brief, Case Play, Completion and Replay flows require no walkable hub.
- **U6-03** Ordinary bad-but-legal physical outcomes remain in case state; they are not presented as input errors.

## Impact readability
- **U6-04** Every held/world impact exposes direction without color.
- **U6-05** Every held/world impact exposes WEAK/MEDIUM/STRONG using at least two redundant non-audio signals.
- **U6-06** Every impact can reveal source provenance/lineage in one Inspect action.
- **U6-07** A CHAIN_GENERATED impact can reveal the parent spend/collision that created it.
- **U6-08** Inventory never exceeds the Phase-4 2 baseline / 3 absolute ceiling presentation.

## Donors / pickups
- **U6-09** Harvestable collision output becomes a persistent world pickup without frame-timed input.
- **U6-10** Full inventory leaves new pickup visible/indexed rather than silently destroying it by default.
- **U6-11** EXHAUSTIBLE / RESETTABLE / CYCLIC_WEAK source state is visually distinguishable in player language.
- **U6-12** Visited-room pickup overview prevents an uncollected stable impact from becoming a memory-only fact.

## Receivers / transforms
- **U6-13** Selected receiver clearly distinguishes structural incompatibility from legal adverse result.
- **U6-14** Valid input directions are visible and selectable through authored snaps only.
- **U6-15** Safe/useful/unsafe magnitude bands can be understood without numeric force.
- **U6-16** Quarter-turn/reverse/mirror transform preview shows exact before/after direction.
- **U6-17** Damper preview shows exact one-band reduction and never implies an increase.
- **U6-18** Transform flow preserves provenance and does not present transform as a consumed new token.

## Preview / causality
- **U6-19** Pre-commit preview shows direct family consequence but not a multi-step solution forecast.
- **U6-20** Causal ribbon can explain source -> transform -> spend -> receiver -> secondary collision lineage.
- **U6-21** Default causal ribbon shows <=5 material nodes and <=2 sibling branches before expansion.
- **U6-22** Broken requirement can navigate to first relevant material cause without recommending next move.

## Pause / moving state
- **U6-23** Pause settles at a canonical movement-step boundary, never an authoritative mid-lane state.
- **U6-24** Step advances exactly one canonical movement step without altering outcome.
- **U6-25** Presentation speed/slowdown cannot alter canonical case state.
- **U6-26** Moving receiver current receive-window state is inspectable while paused.

## History
- **U6-27** One player transaction is one history card; derived collisions remain nested inside it.
- **U6-28** Undo restores held/world impacts, lineage, body/world state and selected causal state exactly.
- **U6-29** Redo restores exact intact branch; new accepted action after Undo truncates redo branch.
- **U6-30** Raw Undo count is never displayed as a penalty/mastery metric.

## Multi-room / self-launch
- **U6-31** Stable world pickups in visited rooms are locatable through Room Overview.
- **U6-32** Convenience traversal cannot skip unresolved hazards, moving windows, donor resets or carrying-state-dependent routes.
- **U6-33** Self-launch uses authored lanes/snap outcomes and no free-angle aim.
- **U6-34** Self-launch baseline success requires no midair steering or frame-perfect landing.
- **U6-35** Secondary impact created after self-launch remains visible before camera returns full control.

## Input
- **U6-36** Mouse+keyboard can perform every required action without mandatory drag/wheel/hover.
- **U6-37** Keyboard-only can perform every required action through deterministic focus/navigation.
- **U6-38** Controller-only can perform every required action without virtual mouse.
- **U6-39** Required interactables are reachable in authored logical focus graph.
- **U6-40** Focus/cycle order is independent of zoom, frame layout, hash order and scene creation order.
- **U6-41** Context-sensitive controller actions show current function/glyph before activation.
- **U6-42** Input device changes do not alter domain state or lose current semantic selection.

## Accessibility / Deck
- **U6-43** Critical direction/magnitude/compatibility/provenance information has non-color and non-audio redundancy.
- **U6-44** Reduced motion preserves source->pickup->receiver causality without large sweeps/shake.
- **U6-45** No-audio play preserves every gameplay-critical cue.
- **U6-46** Pause/Step/slowdown use never blocks baseline completion or ordinary mastery eligibility.
- **U6-47** 1280×800 default layout keeps world, impact belt and critical case status readable with no mandatory horizontal scrolling.
- **U6-48** UI scaling and localization expansion do not clip mandatory controls/requirements within supported ranges.
- **U6-49** Reset Controls remains reachable after a deliberately unusable remap.

## Onboarding / demo
- **U6-50** DEMO01 communicates `collision -> persistent portable impact -> spend elsewhere` without vector terminology.
- **U6-51** Demo teaches quarter-turn through a physical socket before any complex converter chain.
- **U6-52** Demo demonstrates that STRONG can be worse than MEDIUM/WEAK through a visible receiver consequence.
- **U6-53** Demo includes a source/provenance consequence so impacts do not read as generic arrow ammo.
- **U6-54** DEMO05 ends with an intentionally created secondary collision/new lineage and reuse.
- **U6-55** Demo excludes 3-slot inventory and late dense moving-window/regeneration complexity.

## Recovery / presentation integrity
- **U6-56** Autosave UI never claims a state is durable before persistence confirms it.
- **U6-57** Recovery messaging distinguishes exact restored checkpoint from discarded in-progress presentation.
- **U6-58** Normal player UI never requires raw IDs, state hashes, collision-table indices or vector components.
- **U6-59** Visual/audio presentation never implies realistic free rigid-body behavior absent from canonical mechanics.
- **U6-60** A fresh Phase-7/8 designer can determine screen hierarchy, impact/receiver language, controls, accessibility, causal explanation, demo flow and moving-state presentation without inventing UX rules.

---

# 26. Phase-6 closure decision

- Application/screen hierarchy defined: **YES**
- Desktop/Deck in-case layout defined: **YES**
- Direction/magnitude/provenance language defined: **YES**
- World-pickup/inventory presentation defined: **YES**
- Donor/regeneration presentation defined: **YES**
- Receiver compatibility/safe-unsafe language defined: **YES**
- Pickup/select/carry/transform/spend flow defined: **YES**
- Preview vs solution-oracle boundary defined: **YES**
- Body/donor/receiver inspection defined: **YES**
- Causal lineage/ribbon defined: **YES**
- Pause/Step/moving-window presentation defined: **YES**
- Undo/Redo/history presentation defined: **YES**
- Multi-room pickup/retrieval guardrails defined: **YES**
- Self-launch camera/focus/recovery defined: **YES**
- Mouse+keyboard defined: **YES**
- Keyboard-only defined: **YES**
- Controller-only defined: **YES**
- Deterministic focus navigation defined: **YES**
- Accessibility/no-audio/reduced-motion defined: **YES**
- First-session/demo UX defined: **YES**
- Pause/settings/help/recovery UX defined: **YES**
- Discrete causal-physics visual/audio language defined: **YES**
- UX empirical risks defined: **YES**
- Phase-6 acceptance tests: **60**
- Production implementation started: **NO**
- Earlier phase reopened: **NO**
- Phase 6 complete on paper: **YES**
- DESIGN COMPLETE: **NO**

## NEXT PHASE

**Phase 7 — Economy / Retention / Commercial Model.**

The next run should research current premium puzzle/action-puzzle pricing and Steam demo/platform expectations where useful, then freeze campaign unlock structure, mastery/remix retention, hints/assist philosophy, achievement boundaries, demo-to-full transition, Steam/Deck feature scope, monetization exclusions, optional expansion boundaries, commercial risks and numbered Phase-7 acceptance tests. It must not add currencies, grind, daily systems, live-service hooks, combat rewards, token upgrades/rarities or mechanics merely to manufacture retention.