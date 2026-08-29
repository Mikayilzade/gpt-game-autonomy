# GAME #006 — STITCHSPACE — UX / PRESENTATION ARCHITECTURE

Last updated: 2026-08-29
Factory run: **7**
Phase: **6 — UX / Presentation Architecture**
Selected concept: **G6C01 Stitchspace**
Product thesis: **LOCKED**
Mechanical architecture: **COMPLETE ON PAPER**
Content architecture: **COMPLETE ON PAPER**
UX / presentation architecture: **COMPLETE ON PAPER**
Production implementation started: **NO**
DESIGN COMPLETE: **NO**

This file freezes how Stitchspace communicates remote adjacency replacement without turning the game into a detached graph editor. It implements the Product Thesis, Mechanical Architecture and Content Architecture without adding a new primary verb.

If presentation convenience conflicts with canonical mechanics, mechanics win unless the earlier phase is explicitly reopened. If a visual effect implies simultaneous old/new seam adjacency, arbitrary portal placement, hidden orientation changes, timing-dependent endpoint movement or non-deterministic physical contact, that effect is invalid.

Fresh platform references checked 2026-08-29:
- Steam Deck / Steam Machine compatibility review: https://partner.steamgames.com/doc/steamhardware/compat — preferred Deck resolution 1280×800, absolute minimum UI-character height 9 px at that resolution, with 12 px recommended where practical and configurable text size/contrast recommended.
- Steam hardware recommendations: https://partner.steamgames.com/doc/steamhardware/recommendations — default controller configuration should expose all functionality, offline single-player is strongly recommended, aspect-ratio flexibility is recommended, and device-specific display settings should not be blindly cloud-synced.
- Steam Input: https://partner.steamgames.com/doc/features/steam_controller — semantic/action-oriented input is preferred.
- Steam Input gamepad-emulation best practices: https://partner.steamgames.com/doc/features/steam_controller/steam_input_gamepad_emulation_bestpractices — use appropriate device glyphs/fallbacks rather than assuming one controller family.

These references constrain usability/platform readiness only; they do not create gameplay rules.

---

# 1. UX contract

At every meaningful puzzle state, a player must be able to answer five questions without opening a developer graph:

1. **Which rooms currently touch through each seam?**
2. **If I move this endpoint, which old boundary relationship disappears?**
3. **Which new boundary relationship appears, and how will crossing orient me/an object?**
4. **What entity/world-state consequence happened after my last edit or crossing?**
5. **Why is the current case complete, incomplete, protected, blocked or temporarily waiting for a deterministic mover to settle?**

The intended player rhythm is:

**inspect the physical world -> select one visible seam endpoint -> inspect legal target sockets -> preview old-loss + new-connection + orientation -> commit atomically -> physically use the changed adjacency -> inspect aftermath -> reuse the scarce seam -> Undo/Redo freely when a hypothesis is wrong.**

The player is never required to:
- manipulate an abstract graph as the main game surface;
- remember room IDs or compass arithmetic;
- drag graph nodes around;
- infer seam ownership from color alone;
- free-aim a portal-like surface placement;
- react within a real-time timing window to move an endpoint;
- memorize a remote room’s current socket state after leaving it;
- watch a long animation to discover whether a canonical state has already changed;
- use mouse hover as the only way to learn a rule;
- use audio as the only source of critical information.

---

# 2. Application / screen-state hierarchy

## 2.1 First launch

`Boot -> Accessibility & Input Quick Setup -> Title -> Case Board -> Case Brief -> Case Play -> Completion -> Case Board`.

First-launch quick setup exposes:
- UI/text scale;
- high-contrast topology option;
- reduced motion;
- reduced seam flash/pulse;
- controller glyph auto-detection with manual override;
- hold/toggle preference for Inspect/Topology Overview when relevant.

The player may accept defaults immediately. No mandatory cinematic or lore sequence precedes DEMO01/C01.

## 2.2 Title screen

Primary actions:
- Continue;
- Case Board;
- Settings;
- Accessibility;
- Help / Rules;
- Credits;
- Quit on desktop.

`Continue` loads the latest verified active-case checkpoint when available; otherwise it opens the Case Board.

No launcher outside the game is required for ordinary setup, controller remapping or accessibility.

## 2.3 Case Board

Case selection is a compact physical/diagrammatic board, not a walkable hub.

Each case card shows:
- case ID/title;
- cleared / uncleared;
- optional mastery marker;
- tutorial/new-concept badge when relevant;
- remix marker when unlocked.

The board does not show XP, currencies, lives, energy, daily streaks or grind progression.

## 2.4 Case state machine

`Brief -> Inspect/Traverse/Edit -> Canonical Resolution -> Inspect/Traverse/Edit -> Completion`.

A seam edit is never visually treated as committed until domain acceptance is known. Once accepted, old-loss/new-connection presentation may animate, but the canonical replacement has already happened atomically.

## 2.5 Completion

Completion shows:
- baseline clear;
- optional mastery if authored;
- one compact final topology/causal summary;
- Replay;
- Next Case;
- Case Board.

Completion does not score:
- raw Undo count;
- restart count;
- thinking time;
- Pause/Step use;
- selected UI scale/accessibility mode;
- input device.

---

# 3. World representation

## 3.1 Primary representation: physical room-stage

Stitchspace should present rooms as stable, recognizable local architectural spaces. The exact implementation may be 2D cutaway/isometric/orthographic 3D-like presentation, but the canonical UX target is a **world-stage where rooms are places**, not nodes in a flowchart.

Required characteristics:
- each room has a stable visual identity and local orientation frame;
- each room’s walls/boundaries remain recognizable when remote adjacency changes;
- edge sockets are physically embedded into boundary surfaces;
- ordinary passages look materially different from editable seams;
- seam relationships are traceable without needing the topology overview;
- entities visibly remain located in their current physical room/node state;
- the camera never rotates the world in a way that silently changes the player’s interpretation of socket orientation.

## 3.2 Room recognizability language

Each room should combine at least three redundant identity cues:
- distinct architectural silhouette/layout;
- stable room label or icon in Inspect/Overview;
- unique decorative landmark family/pattern;
- consistent local edge orientation markers.

Color may reinforce identity but cannot be the only cue.

## 3.3 Stable local frames

Rooms do not visually spin, fold or slide around simply because adjacency changed. The world may stage remote rooms near one another for a replacement animation, but their local orientation frame remains canonical and stable.

This prevents seam replacement from being confused with physically moving the rooms themselves.

## 3.4 Camera

Camera goals:
- show current player room and relevant boundary context clearly;
- frame a selected endpoint and candidate target without losing room identity;
- make crossing entry/exit orientation readable;
- support quick focus on remote seam partners;
- avoid cinematic camera motion that obscures immediate old-loss/new-connection feedback.

Camera convenience may include:
- focus selected room;
- jump view to opposite seam endpoint;
- frame source+target preview as split/paired focus;
- Room Overview toggle.

Camera navigation is presentation only and cannot mutate gameplay.

---

# 4. Seam / endpoint / socket visual language

## 4.1 Seam identity

A seam is presented as one persistent relationship with two endpoints, not as two independent portal guns/holes.

Each seam has:
- a seam body/style family shared by both endpoints;
- a persistent seam symbol or number/icon where multiple seams exist;
- a visible relationship trace available on focus/Inspect;
- endpoint A/B distinction only when mechanically necessary; ordinary player language should prefer `this end / other end` unless directionality matters.

With two or three seams, identity must use redundant shape/pattern/icon cues in addition to optional color.

## 4.2 Edge sockets

An edge socket communicates:
- it is a legal authored seam attachment point;
- its owning room;
- local boundary orientation;
- current state: free, occupied by seam endpoint, disabled, crossing-locked;
- if filtered by a selected endpoint, whether it is structurally legal as a target.

Sockets should be visible but not glow like collectible loot. Default treatment is quiet architectural hardware; selection/preview adds emphasis.

## 4.3 Endpoint state

Endpoint states:
- settled/attached;
- selected for move;
- crossing-locked;
- opposite end reference;
- structurally unavailable only where mechanics say so.

Crossing-lock must be visible before the user attempts an edit whenever the lock is canonical and current.

## 4.4 Ordinary passages

Ordinary passages must read as fixed infrastructure. They cannot share the same detachable endpoint hardware, seam-stitch animation or selectable relocation affordance as seams.

---

# 5. Seam replacement animation

## 5.1 Atomic truth vs presentation sequence

Mechanically, old adjacency disappears and new adjacency appears atomically. Presentation may serialize the explanation into a short visual beat, but it must not imply an intermediate playable state.

Recommended visual sequence after accepted command:
1. selected old endpoint and its previous partner flash as the relationship being replaced;
2. old connection visibly unzips/retracts/cuts;
3. selected endpoint traverses a short stylized UI/world path or dissolves/reappears at target hardware;
4. new connection visibly stitches/tensions into place;
5. both destination orientations briefly show crossing direction;
6. control returns immediately when canonical post-state is ready.

The full ordinary sequence should be short enough that repeated edits do not become friction.

## 5.2 Reduced motion

Reduced-motion mode replaces endpoint travel/camera sweep with:
- old pair highlight -> discrete detach state;
- target highlight -> discrete attach state;
- static before/after relation indicators.

No large screen zoom, whip pan, spatial warping or mandatory flashing.

## 5.3 Invalid edit

A structural rejection:
- never plays the full replacement animation;
- keeps endpoint at original socket;
- presents one concise exact reason, e.g. `Socket already holds another seam`, `Endpoint is occupied while crossing`, `That socket cannot form a valid crossing`, `Protected relation cannot be broken`.

A strategically bad but legal edit commits normally; UX must not warn `wrong move` or block it.

---

# 6. Preview contract: old loss + new adjacency

## 6.1 Required preview

Before confirming a target, the UI simultaneously identifies:
- **OLD:** selected endpoint’s current socket and its current opposite seam endpoint;
- **NEW:** proposed target socket and that same opposite endpoint;
- the orientation mapping at both sides;
- any direct structural legality/lock state.

The old relation must remain at least as visually salient as the new target. This is the primary anti-portal UX rule.

## 6.2 Preview visual pattern

Preferred pattern:
- old adjacency uses a `will detach` treatment (broken stitch / receding line / cross-cut bracket);
- new adjacency uses a `will attach` treatment (forming stitch / joined brackets);
- selected endpoint identity remains constant through both;
- the opposite endpoint stays visibly the same relationship anchor.

Do not use only red/green. Shape/icon/text or line style must redundantly distinguish removal/addition.

## 6.3 Allowed direct consequences

Preview may show facts immediately and deterministically implied by the edit:
- which seam pair changes;
- which sockets become directly adjacent;
- crossing exit orientation;
- that a fixed immediate route becomes connected/disconnected;
- structural rejection reason;
- crossing-lock reason;
- direct hard-invariant violation that makes the command illegal.

## 6.4 Forbidden solution-oracle behavior

Preview may not:
- highlight the strategically best socket;
- show the entire future solution route;
- predict several later entity moves through hypothetical future seam states;
- rank edits;
- reveal hidden fixture/solver data;
- label a legal edit `dead end` before the player observes/inspects consequences;
- show `this completes objective after three more moves`.

---

# 7. Crossing-orientation preview without compass bookkeeping

## 7.1 Physical arrow language

Each socket has an authored visible inward/outward edge direction. When previewing a seam, show a small crossing ghost:
- entity arrow enters source wall;
- matching ghost emerges from target wall into the room;
- the destination local lane/facing is shown directly.

The player should not need to think `east to north means 90 degrees`.

## 7.2 Object examples

For a directional object/mover, preview may show a ghost silhouette placed at the destination entry node and facing the canonical exit direction.

For the player, preview may show a small neutral figure/arrow. It should not expose remote future pathfinding.

## 7.3 Orientation labels

Optional high-clarity Inspect may say:
- `Enter here -> emerge facing into this lane`;
- concise compass text may be available but is secondary.

Raw rotation matrices/degrees are forbidden in normal UX.

---

# 8. Physical endpoint-selection/edit flow

The same semantic flow must work for pointer, keyboard-only and controller-only:

`Select/Focus seam endpoint -> enter Move Endpoint mode -> browse structurally relevant legal/illegal socket candidates -> inspect OLD/NEW preview -> Confirm -> domain validation -> accepted replacement or exact rejection -> return to world state.`

## 8.1 Mouse + keyboard

Typical defaults, fully remappable later:
- click endpoint to select;
- click `Move endpoint` or use Interact key;
- candidate sockets receive focus affordances;
- pointer selects target;
- left click/Enter confirms;
- right click/Esc cancels;
- Tab or Q/E cycles candidate sockets without requiring pointer;
- Z / Y or semantic bindings for Undo/Redo;
- Inspect key reveals detailed relation.

No required drag gesture. Dragging an endpoint may be offered as optional convenience only if click/semantic selection remains fully capable and the drag is still constrained to authored sockets.

## 8.2 Keyboard-only

Required:
- deterministic `Focus Next Interactable` action;
- endpoints/sockets reachable without virtual cursor;
- Enter/Space select/confirm;
- Escape cancel;
- candidate sockets cycle in stable authored order;
- room focus next/previous action;
- `Focus Opposite Seam End` shortcut;
- Undo/Redo;
- Inspect;
- Topology Overview.

Keyboard-only must be capable of every baseline and mastery case.

## 8.3 Controller-only

Conceptual mapping, remappable:
- left stick/D-pad: local movement / logical focus depending mode;
- A: interact/select/confirm;
- B: cancel/back;
- X: Move Endpoint when focused on an endpoint, otherwise context action;
- Y: Inspect;
- LB/RB: previous/next seam or endpoint in edit mode;
- LT/RT: previous/next target socket or room group in edit mode;
- Menu: pause;
- View/secondary: topology overview;
- dedicated accessible actions for Undo and Redo through face/shoulder combination or remappable actions, not buried behind a pointer menu.

Context-sensitive button functions must be shown by current glyph/text before activation.

No virtual mouse is required.

---

# 9. Deterministic focus/navigation graph

Every authored case compiles presentation focus metadata for:
- player/interactable entities;
- seam endpoints;
- candidate edge sockets;
- ordinary passages for Inspect;
- relevant objectives/requirements;
- room focus anchors;
- Undo/Redo/Overview utility controls.

Rules:
- geometry may generate a draft neighbor graph;
- authored overrides are permitted and expected;
- focus order cannot depend on animation interpolation, current camera zoom, floating-point nearest comparisons, scene instantiation order or hash iteration;
- when editing one endpoint, target cycle order is stable authored grouping: current room candidates -> adjacent/visible relation group -> remote rooms in stable room order -> stable socket ID fallback;
- disabled/illegal sockets remain inspectable when useful, with reason, but confirmation is unavailable;
- every required target used by a known baseline fixture is reachable by keyboard/controller focus;
- changing display scale/aspect ratio cannot change semantic focus order.

---

# 10. Compact topology overview

## 10.1 Purpose

The overview answers `what touches what now?` and `where are my seams/entities?`. It is an explanatory/navigation aid, not the primary editor.

## 10.2 Layout

Overview shows:
- one stable card/schematic per room;
- ordinary fixed passages;
- current seam connections;
- seam identity;
- approximate socket side/orientation;
- player and materially relevant entity locations;
- occupied/locked endpoint marker;
- unresolved world pickups/items only if future phases ever define such entities (baseline has none).

Room cards preserve physical-room identity via icon/silhouette/landmark cue.

## 10.3 Editing boundary

Default rule: topology overview is **inspect-only** for seam placement. It may allow focus/jump-camera to an endpoint/socket, then return to the physical world edit flow.

A future implementation convenience that permits confirming a seam move directly from Overview is non-canonical by default and requires UX empirical proof that it does not turn mature play into detached graph editing. Phase-6 frozen recommendation is **do not enable direct overview editing in 1.0 baseline**.

## 10.4 Overview accessibility

Connections use line style, seam icon/pattern and labels; color alone is insufficient. Zoom/scroll is optional convenience, not required to read normal <=5-room cases at target layout.

---

# 11. Entity / mover / occupancy presentation

## 11.1 Entity state

Every materially relevant entity can reveal:
- current room/location;
- current local facing when relevant;
- settled / moving / crossing state;
- destination if currently in deterministic committed transition;
- objective relevance in plain language where appropriate.

No raw node IDs required.

## 11.2 Automatic mover

Automatic movers communicate their deterministic next local behavior through authored lane/path markings and an Inspect summary such as:
`Moves one step along this lane when the current action resolves; crosses an active boundary if its lane reaches one.`

Do not show a full multi-edit solution forecast.

## 11.3 Crossing occupancy lock

When an entity is canonically crossing:
- both affected boundary resources show a lock/crossing marker;
- the entity remains visually associated with the crossing;
- selecting the endpoint explains `Cannot move this end until the crossing settles`;
- once the canonical step settles, the lock disappears immediately regardless of lingering cosmetic animation.

## 11.4 No reaction-time trap

If movers matter, Pause/Step and slowed presentation must preserve the same canonical state sequence. A player must never need to `click the endpoint quickly before the mover reaches it`.

---

# 12. Causal explanation after edits and crossings

## 12.1 Causal ribbon

After a committed seam move, crossing or deterministic mover resolution, a compact causal ribbon may show the shortest material chain:

`Seam A end left Loading Bay -> Loading Bay no longer touches Gallery -> Seam A now joins Atrium to Gallery -> Crate crossed into Gallery facing inward -> Isolation objective changed`.

Default budget:
- <=5 material nodes;
- <=2 sibling consequences visible before expansion.

Inert local movement and purely cosmetic animation are collapsed.

## 12.2 Seam history identity

Inspecting a seam may show only the recent relevant endpoint history:
`A: Loading Bay -> Atrium` and `B: Gallery (unchanged)`.

Do not turn ordinary play into a long event log.

## 12.3 Requirement explanation

Selecting an incomplete/broken requirement shows:
- current relevant fact;
- directly affected room/entity/relation;
- last material event that changed it when available;
- camera/focus shortcut.

It does not recommend the next target socket.

---

# 13. Undo / Redo / history presentation

## 13.1 History unit

One accepted semantic domain action is one history card:
- seam endpoint move;
- entity move/crossing command where player-controlled;
- accepted object command;
- deterministic automatic chain nested under its parent accepted action as mechanics require.

Presentation-only camera/Inspect/Overview operations create no history cards.

## 13.2 Undo

Undo visibly restores:
- seam endpoints/adjacency;
- entity room/node/facing;
- objective/invariant state;
- crossing/mover settled state;
- history cursor.

The animation may reverse/fade, but canonical state snaps to the exact checkpoint. Reduced-motion mode uses direct before/after emphasis.

## 13.3 Redo

Redo restores exact intact branch. New accepted action after Undo truncates redo according to mechanics.

## 13.4 History strip

A compact optional strip shows semantic choices, e.g. seam icon + endpoint + room/socket target. It does not show every internal reachability recalculation or animation frame.

No negative `undo count` display exists.

---

# 14. Objectives / invariants / case rail

Case Rail contains concise status rows for:
- required final conditions;
- hard protected invariants when they matter to legality;
- soft/protected conditions where a legal bad edit can break them;
- settlement/pending mover state.

States:
- satisfied;
- unsatisfied;
- protected/broken;
- pending deterministic resolution;
- not currently evaluable.

Expanding a row highlights the physical subject/relation. It never highlights the correct seam target.

The Case Rail should normally occupy a minority of the screen and may collapse on Deck.

---

# 15. Pause / Step semantics

## 15.1 Pause

When automatic movement is active, Pause stops presentation/control at the next canonical movement/crossing-step boundary. It never creates an authoritative mid-edge state.

If pressed during interpolation, the UI may visually settle to the corresponding canonical boundary before showing paused state.

## 15.2 Step

`Step` advances exactly one canonical deterministic movement/resolution step, then pauses again.

The result must match unpaused execution exactly.

## 15.3 Slow presentation

Optional speed presets (for example 1× / 0.5× / 0.25×) affect presentation only. Baseline completion and mastery remain valid at any speed.

## 15.4 Edit availability while paused

Endpoint relocation is available only when mechanics say the canonical state is settled/unlocked. Pause cannot create a special edit window between authoritative substeps.

---

# 16. Accessibility contract

Required for 1.0 baseline:

## 16.1 Color independence
- seam identities: shape/pattern/icon + optional color;
- OLD vs NEW preview: line style/icon/text + optional color;
- socket state: shape/icon/text, not hue only;
- objective states: icon/text;
- room identity: silhouette/label/landmark + optional color.

## 16.2 Motion/flash
- reduced motion removes large endpoint flight, warp-like camera movement and strong spatial distortion;
- reduced flash/pulse setting;
- no essential topology fact communicated only through animation;
- crossing orientation remains visible in static preview.

## 16.3 Audio redundancy
Every critical seam detach/attach, lock, rejection, crossing and objective cue has a visible/text equivalent.

Separate master/music/SFX/UI volume controls are recommended.

## 16.4 Timing
- Pause/Step available where automatic movers matter;
- slower presentation available;
- no baseline task requires reaction timing;
- accessibility timing tools never invalidate mastery/achievement eligibility unless a later achievement explicitly and safely targets a different non-required mode (default: do not).

## 16.5 Input
- full keyboard-only completion;
- full controller-only completion;
- mouse optional, not required;
- no drag-only, hover-only, wheel-only or analog-precision requirement;
- all semantic actions remappable where platform/engine allows;
- Reset Controls always reachable.

## 16.6 Text / UI scale
At 1280×800:
- no critical UI character may fall below Valve’s 9 px absolute Deck compatibility floor;
- ordinary design target should aim at >=12 px character height where practical rather than designing to the minimum;
- at least 100% / 125% / 150% conceptual scale presets or equivalent responsive scaling should be supported;
- high-contrast mode should remain layout-safe;
- mandatory controls/requirements cannot clip at supported scales.

## 16.7 Cognitive clarity mode
Optional high-clarity mode may:
- keep room labels visible;
- keep seam A/B or seam icon labels expanded;
- show `OLD / NEW` words continuously during preview;
- keep orientation ghost arrows visible longer;
- reduce decorative boundary animation.

It cannot reveal solver suggestions or alter mechanics.

---

# 17. Steam Deck 1280×800 target

## 17.1 Default layout

At 1280×800:
- world viewport remains the dominant surface;
- Case Rail collapses into a slide-over or narrow status stack;
- seam identity/status occupies a compact always-readable strip;
- selected endpoint/target preview uses edge overlays rather than a wide modal editor;
- Topology Overview fits the normal <=5-room campaign target without mandatory horizontal scrolling;
- text follows the readability targets above.

## 17.2 Controller coverage

Default controller configuration must expose every required action. Controller-only play must not invoke a desktop virtual mouse.

## 17.3 Glyphs

Input prompts should use current device-specific glyphs where available, with sensible fallback. Switching input devices should update prompts without changing semantic selection/domain state.

## 17.4 Aspect ratios

Presentation should tolerate common 16:9 and 16:10 targets without changing domain layout/focus rules. Wider/taller aspect ratios may reveal more world but cannot become a gameplay advantage required by fixtures.

## 17.5 Offline

All single-player cases, progress and settings needed for normal play must remain usable offline. Steam/platform status is not gameplay authority.

---

# 18. First-session onboarding

Onboarding teaches through physical consequence rather than terminology.

## DEMO/C01 teaching pattern

1. Player crosses an already-existing seam before editing it.
2. Game highlights that both endpoint hardware pieces belong to one seam.
3. First endpoint move preview labels **OLD relation disappears** and **NEW relation appears** simultaneously.
4. Player commits.
5. Camera briefly shows the old wall relation is now ordinary wall/no longer connected.
6. Player physically crosses the new adjacency.
7. Next micro-case requires reusing the same endpoint for a second destination.

The first 10 minutes must prevent the interpretation `I place portals wherever I want`.

Terminology order:
- player-facing `seam`, `end`, `socket`, `room` first;
- `adjacency` and `topology` belong to help/secondary explanatory language, not required tutorial vocabulary.

---

# 19. DEMO01–DEMO05 presentation flow

The demo must communicate the commercial hook in 15–25 minutes.

## DEMO01 — A boundary is real adjacency
- start with an existing seam;
- cross it physically;
- Inspect can show the remote partner endpoint;
- no edit until the relation is understood.

Proof: remote rooms can genuinely become neighbors.

## DEMO02 — Replacement, not portal placement
- move one existing endpoint;
- OLD and NEW preview is mandatory;
- previous route must disappear and matter.

Proof: every new adjacency costs the old one.

## DEMO03 — Reuse for object then player
- object crosses under first seam state;
- endpoint relocates;
- player uses same scarce seam afterward.

Proof: world state persists between topology edits.

## DEMO04 — Orientation / useful cut
- crossing orientation is previewed by a physical ghost;
- after a mover/object crosses, destroying old adjacency produces safety/access.

Proof: seam choice is not simply `connect current room to destination`.

## DEMO05 — State-dependent replacement synthesis
- compact 3–4 room problem;
- entity movement changes which seam target is useful;
- at least one physical traversal/use occurs between meaningful edits;
- final solution requires useful lost adjacency, not just reaching a goal socket.

Proof: mature game loop contains prediction -> replacement -> physical use -> changed-state replacement.

Demo excludes:
- three seams;
- dense simultaneous movers;
- large topology overview reliance;
- high socket counts;
- new late mechanics.

---

# 20. Save / load / recovery messaging boundaries

Phase 8 will define persistence internals. UX freezes these promises:

- autosave indicator appears only after a canonical checkpoint is durably accepted by persistence;
- UI must not display `Saved` while only an animation/intermediate presentation exists;
- reloading restores one exact verified canonical state or a clearly identified earlier safe checkpoint;
- if latest state is invalid/corrupt, recovery explains that an earlier safe checkpoint was restored rather than silently synthesizing a hybrid;
- no save may visually resurrect an old seam connection while entities belong to a newer topology state;
- settings that are device-specific (resolution/display) should remain separate from cloud gameplay progress conceptually.

---

# 21. Help / glossary

Help entries unlock as taught:
- Room;
- Seam;
- Seam End;
- Socket;
- Move End;
- Old/New connection;
- Crossing orientation;
- Ordinary passage;
- Crossing lock;
- Automatic mover;
- Pause/Step;
- Undo/Redo;
- Topology Overview.

Each entry uses a tiny non-solution example. Help does not contain per-case walkthroughs by default.

---

# 22. Visual identity boundaries

The presentation should intentionally avoid Portal-like visual shorthand.

Required differentiation cues:
- seam hardware looks stitched/clamped/resewn into room edges rather than projected oval holes;
- seam endpoints are persistent scarce objects with identity;
- moving an endpoint visibly destroys its prior relationship;
- no blue/orange mandatory pair language;
- no infinite tunnel/recursive portal renderer is needed to understand crossing;
- rooms remain stable local spaces instead of looking like surfaces for a weapon mechanic.

The game may use impossible cutaway staging, paired boundary windows or transition wipes, but the visual message must remain `these boundaries are currently the same adjacency`.

---

# 23. Audio language

Audio reinforces, never replaces:
- seam detach;
- seam attach;
- endpoint selection;
- crossing begin/settle;
- crossing lock;
- structural rejection;
- ordinary passage vs seam distinction;
- objective change;
- Undo/Redo.

Multiple seam identities should not depend on pitch alone.

---

# 24. Empirical UX/readability risk gates

## U6-R1 — Detached graph-editor drift
Risk: players spend mature cases solving primarily in Overview rather than the world.
Gate: in representative C15+ prototype tests, the majority of meaningful seam decisions should be initiated/understood from physical-world context; Overview may clarify state but should not become the dominant editing surface. If testers strongly prefer graph-only editing because the world is unreadable, reopen presentation/content rather than shipping a disguised graph puzzle.

## U6-R2 — Portal mental model
Risk: players describe the mechanic as `placing portals` and ignore old-adjacency loss.
Gate: after DEMO02–DEMO03, representative testers should be able to state unprompted that moving an end removes its previous connection; persistent misunderstanding after one presentation tuning pass is a reopen signal.

## U6-R3 — OLD loss salience
Risk: new target attracts all attention.
Gate: ordinary wrong-solution interviews should show players predicting both gained and lost adjacency before confirmation in mature tutorial transition cases.

## U6-R4 — Orientation bookkeeping
Risk: players mentally calculate compass rotations rather than seeing physical exit direction.
Gate: <=20% of ordinary orientation-related failures after C04/DEMO04 should primarily come from misreading the preview; repeated requests for degree/compass tables are a presentation failure.

## U6-R5 — Room identity confusion
Risk: impossible adjacency makes rooms visually interchangeable.
Gate: testers can identify current player room, opposite seam room and target room without relying only on color in normal 4–5 room mature cases.

## U6-R6 — Controller focus ambiguity
Risk: many sockets create accidental target selection.
Gate: controller-only testers complete demo/early campaign without virtual mouse and with low accidental commit rate after onboarding; every baseline fixture target must be reachable predictably.

## U6-R7 — Mover timing perception
Risk: deterministic occupancy looks like a reflex timing game.
Gate: Pause/Step users can reason about mover/lock states with no loss of rule comprehension, and no ordinary solution requires acting during animation timing.

## U6-R8 — Overview density
Risk: 5-room/10-socket mature state becomes spaghetti.
Gate: normal overview at 1280×800 remains legible with room identity + seams + ordinary passages; if not, content should reduce exposed topology before adding zoom-heavy graph UX.

## U6-R9 — Seam identity in grayscale/no-audio
Risk: 2–3 seams become indistinguishable.
Gate: representative seam states remain correctly traceable in grayscale, muted audio, high-contrast and reduced-motion modes.

## U6-R10 — Repetition friction
Risk: beautiful replacement animations become slow after hundreds of edits.
Gate: experienced testers should not routinely request skipping ordinary detach/attach feedback; animation duration and camera behavior must compress after onboarding while preserving causal clarity.

---

# 25. Phase-6 acceptance tests

## Application / hierarchy
- **U6-01** First launch exposes accessibility/input quick setup without mandatory narrative delay.
- **U6-02** Title -> Case Board -> Brief -> Case Play -> Completion flow requires no walkable hub.
- **U6-03** Continue restores an exact verified active state or Case Board fallback.
- **U6-04** No screen introduces XP/currency/lives/energy UI absent from the Product Thesis.

## World / room identity
- **U6-05** Every room remains visually identifiable through non-color cues.
- **U6-06** Room local orientation frame remains stable across seam edits.
- **U6-07** Camera motion cannot imply canonical room rotation/folding.
- **U6-08** Ordinary passages are visually distinct from editable seams.

## Seam / socket language
- **U6-09** Both endpoints of one seam are traceable as one persistent relationship.
- **U6-10** Multiple seams remain distinguishable without color.
- **U6-11** Free/occupied/disabled/crossing-locked socket states are distinguishable through redundant cues.
- **U6-12** Endpoint crossing lock is inspectable with exact reason.
- **U6-13** Socket affordances do not imply arbitrary free-surface placement.

## Replacement flow
- **U6-14** Before confirmation, OLD adjacency loss and NEW adjacency creation are simultaneously visible.
- **U6-15** OLD loss remains at least equally salient to NEW target in default preview.
- **U6-16** Accepted replacement animation never creates a controllable intermediate one-ended/double-connected seam state.
- **U6-17** Reduced-motion replacement communicates identical old/new facts without travel animation.
- **U6-18** Structural rejection plays no successful attach/detach sequence and gives exact reason.
- **U6-19** Legal but strategically bad edit is not blocked or labeled input error.

## Orientation
- **U6-20** Preview shows direct source-entry -> destination-exit direction physically.
- **U6-21** A directional entity can be previewed at destination facing without numeric degrees.
- **U6-22** Normal play does not require compass arithmetic or rotation matrices.

## Input / focus
- **U6-23** Mouse+keyboard can select/move endpoints without required drag/hover/wheel.
- **U6-24** Keyboard-only can reach every required endpoint/socket/action.
- **U6-25** Controller-only can complete every required case without virtual mouse.
- **U6-26** Focus order is deterministic and independent of camera zoom/animation/hash/scene order.
- **U6-27** Every socket used by a known baseline fixture is reachable through controller/keyboard focus.
- **U6-28** Disabled/illegal sockets can expose reason without becoming confirmable.
- **U6-29** Input-device switch updates prompts without altering domain state/semantic selection.
- **U6-30** Current context-sensitive controller action is visible before activation.

## Overview
- **U6-31** Overview shows current room relationships, seam identity and relevant entity locations.
- **U6-32** Overview is inspect/navigation-first and cannot become required as the only endpoint editor.
- **U6-33** Room cards preserve physical identity through non-color cues.
- **U6-34** Normal <=5-room overview is readable at 1280×800 without mandatory horizontal scrolling.
- **U6-35** Overview presentation does not expose solver rankings/hidden fixture routes.

## Entities / movers
- **U6-36** Material entity location/facing/settled-vs-crossing state is inspectable.
- **U6-37** Automatic mover’s immediate deterministic rule is explainable without full solution forecast.
- **U6-38** Crossing occupancy lock visually associates the relevant entity and boundary resources.
- **U6-39** Cosmetic animation cannot keep an endpoint mechanically locked after canonical settlement.

## Causality / objectives
- **U6-40** Causal explanation can show seam old-loss -> new relation -> crossing -> objective consequence.
- **U6-41** Default causal ribbon displays <=5 material nodes and <=2 siblings before expansion.
- **U6-42** Requirement explanation highlights current fact/cause but not recommended next seam target.
- **U6-43** Case Rail distinguishes hard illegality from legal-bad protected-state failure.

## Undo / Redo
- **U6-44** Undo presentation restores exact seam/entity/objective checkpoint.
- **U6-45** Redo restores exact intact branch and new accepted action truncates redo.
- **U6-46** Camera/Inspect/Overview actions create no domain history cards.
- **U6-47** Raw Undo/restart count is never displayed as a penalty/mastery metric.

## Pause / Step
- **U6-48** Pause stops at canonical movement-step boundary, never authoritative interpolation.
- **U6-49** Step advances exactly one canonical deterministic step.
- **U6-50** Presentation speed cannot change domain result.
- **U6-51** Pause cannot create a special endpoint-move timing window.

## Accessibility
- **U6-52** Seam identity, OLD/NEW, socket state and objectives remain legible without color.
- **U6-53** No essential state is audio-only.
- **U6-54** Reduced motion preserves all required causal facts.
- **U6-55** High-clarity mode changes information persistence/labels only, not solver knowledge or mechanics.
- **U6-56** Reset Controls remains reachable after an unusable remap.
- **U6-57** Supported UI scaling does not clip mandatory preview/objective/control content.

## Deck / platform
- **U6-58** 1280×800 layout keeps world, seam state and critical objective status readable.
- **U6-59** No critical UI text falls below the 9 px Deck compatibility floor; normal targets aim >=12 px where practical.
- **U6-60** Full functionality is exposed by default controller configuration.
- **U6-61** Common 16:9/16:10 aspect-ratio changes do not alter semantic focus/domain behavior.
- **U6-62** Single-player content remains usable offline.
- **U6-63** Device-specific display settings are conceptually separable from cloud gameplay progress.

## Demo / onboarding
- **U6-64** DEMO01 shows physical seam crossing before endpoint editing.
- **U6-65** DEMO02 forces meaningful old-adjacency loss and presents OLD/NEW together.
- **U6-66** DEMO03 reuses one scarce seam after an object/player state change.
- **U6-67** DEMO04 teaches orientation through physical ghost preview, not compass math.
- **U6-68** DEMO04 includes useful disconnection.
- **U6-69** DEMO05 requires physical world use between meaningful topology edits.
- **U6-70** Demo ends only after state-dependent replacement + useful lost adjacency have been experienced.

## Save/recovery
- **U6-71** Autosave indicator appears only after durable canonical checkpoint acceptance.
- **U6-72** Recovery never synthesizes seam topology from one checkpoint with entity state from another.
- **U6-73** Recovery message distinguishes exact latest restore from earlier safe-checkpoint fallback.

## Product identity
- **U6-74** Normal UI never requires raw graph node IDs or solver state hashes.
- **U6-75** Player can perform the primary loop without an abstract graph editor.
- **U6-76** Visual language foregrounds persistent seam replacement rather than fired portal pairs.
- **U6-77** A fresh Phase-7/8 designer can implement application flow, physical edit flow, focus/input, Overview, mover/causal presentation, accessibility, Deck target and demo onboarding without inventing UX rules.

---

# 26. Phase-6 closure decision

- Application/screen hierarchy defined: **YES**
- First-session flow defined: **YES**
- Physical room/camera representation defined: **YES**
- Stable room recognizability defined: **YES**
- Seam/endpoint/socket language defined: **YES**
- Atomic replacement animation boundary defined: **YES**
- OLD-loss + NEW-adjacency preview defined: **YES**
- Orientation preview defined without compass bookkeeping: **YES**
- Mouse+keyboard flow defined: **YES**
- Keyboard-only flow defined: **YES**
- Controller-only flow defined: **YES**
- Deterministic focus/navigation graph defined: **YES**
- Topology Overview boundary defined: **YES — inspect/navigation-first, not primary editor**
- Entity/mover/occupancy presentation defined: **YES**
- Causal explanation defined: **YES**
- Undo/Redo/history presentation defined: **YES**
- Objective/invariant presentation defined: **YES**
- Pause/Step semantics defined: **YES**
- Accessibility/color/no-audio/reduced-motion defined: **YES**
- Steam Deck 1280×800 target defined against current Steamworks guidance: **YES**
- DEMO01–DEMO05 presentation flow defined: **YES**
- Save/recovery messaging boundaries defined: **YES**
- Product visual-identity boundaries defined: **YES**
- UX empirical risk gates: **10**
- Phase-6 acceptance tests: **77**
- Production implementation started: **NO**
- Earlier phase reopened: **NO**
- Phase 6 complete on paper: **YES**
- DESIGN COMPLETE: **NO**

## NEXT PHASE

**Phase 7 — Economy / Retention / Commercial Model.**

The next run should use fresh current market/Steam evidence where pricing/demo/platform expectations matter, then freeze:
- final design-time price band and value thesis;
- campaign unlock structure and completion gating;
- mastery/remix unlock pacing;
- hint/assist philosophy;
- achievement boundaries;
- difficulty/accessibility relationship;
- demo-to-full transition/import policy;
- Steam/Deck feature scope;
- save/cloud/achievement commercial expectations without online dependency;
- retention model without grind/FOMO;
- monetization exclusions;
- optional expansion boundaries;
- commercial/value risks and empirical gates;
- numbered Phase-7 acceptance tests.

Do not add currencies, grind, dailies, lives, seam upgrades, DLC-dependent core mechanics, live-service hooks or feature bloat to manufacture retention.