# GAME #004 — UX / PRESENTATION ARCHITECTURE

Last updated: 2026-08-21
Factory run: **10**
Phase: **6 — UX / Presentation Architecture**
Working name: **HUSHLINE** (provisional)
Phase status: **COMPLETE / LOCKED FOR DOWNSTREAM DESIGN**
Production implementation: **NOT STARTED**

This phase translates the locked Product Thesis, Mechanical Architecture and Content Architecture into a readable, physical, controller-safe presentation. It does **not** alter acoustic rules, listener state rules, content schemas, campaign counts or deterministic ordering. The presentation must make the exact simulation legible without turning the game into graph software.

---

## 1. Presentation thesis

HUSHLINE should read first as **a compact physical infiltration space**, second as **an acoustic-routing puzzle**, and never as a detached network editor.

The player should be able to answer, at a glance:
1. Where am I and where can I physically move?
2. What action will make sound next?
3. Which visible passages will that sound use?
4. Which listeners will hear it?
5. What does the movable barrier currently block, and where can I move it next?
6. What changed after I acted?
7. If I failed, exactly which listener detected me and why?

The presentation therefore follows six rules:
- **world first** — routes are drawn through physical doors/corridors, not a separate node diagram;
- **prediction before commitment** — near-term sound consequences are readable without arithmetic;
- **resolution mirrors prediction** — actual propagation uses the same visual grammar as preview;
- **direct manipulation stays tactile** — barrier feedback is local, heavy and physical;
- **no-audio parity is structural** — every required acoustic fact exists visually at equal fidelity;
- **density is bounded** — exceptional three-listener content may be cut if it cannot remain readable without abstract UI.

---

## 2. Camera and world framing

### 2.1 Baseline camera
Canonical baseline: **top-down 2D/2.5D fixed-angle camera** with compact authored encounter framing.

Preferred behavior:
- camera tracks the player smoothly inside authored bounds;
- no free rotation is required;
- zoom is authored per encounter and may ease within a narrow range to keep current player, relevant listener(s), active barrier rail and near-term route readable;
- camera never reveals hidden acoustic topology: if a passage is mechanically active, it must be physically visible or intentionally revealed before it becomes decision-relevant;
- no cinematic camera move may delay input or hide current acoustic state during active play.

### 2.2 Framing targets
At normal desktop presentation, the active decision should ideally fit within one screen or one short camera follow. A player should not need to memorize a remote listener state from several rooms away while acting locally.

Handheld target:
- the player sprite, barrier handle, active passage outlines and listener state symbols remain legible at Steam Deck-class viewing distance;
- essential symbols target a minimum apparent size equivalent to roughly 18–24 px at 1280×800 baseline, with UI scale options above this;
- thin acoustic lines may visually expand on handheld instead of increasing information density.

### 2.3 Occlusion and walls
Walls use clean cutaway/top-down treatment so openings remain obvious.
- full walls: visually solid and acoustically non-edges;
- active passages: physically open and outlined subtly even when no preview is active;
- closed doors: physically shut with a distinct silhouette, not merely a color change;
- barrier-capable passages: rail/slot hardware visibly integrated into architecture.

No route should depend on interpreting decorative wall texture.

---

## 3. Spatial acoustic language

The acoustic graph must be understandable without exposing node IDs, weights or arithmetic.

### 3.1 Three layers of acoustic information

**Layer A — persistent world structure**
Always or nearly always visible:
- physical openings/passages;
- barrier rail and legal snap slots;
- listener threshold motif on each listener;
- source-strength motif on targetable sound-producing objects;
- door state.

**Layer B — contextual prediction**
Visible when the player is near a meaningful action, manipulating the barrier, holding preview, or has enabled persistent preview:
- predicted source pulse;
- minimum route(s) through physical passages;
- attenuation/intensity decay along the route;
- listener outcome: HEARS / DOES NOT HEAR;
- barrier-current and barrier-candidate route effects.

**Layer C — committed resolution**
Short-lived after the action:
- the actual pulse travels through the exact same route language;
- reached listeners react with an immediate state transition marker;
- non-hearing can be shown briefly only where useful; do not spam every uninvolved listener.

### 3.2 Source strength — four bands without required numbers
Strength 1–4 is shown by a canonical shape/pulse vocabulary:
- Band 1: one compact ring / one-chevron source glyph;
- Band 2: two nested rings / two-chevron glyph;
- Band 3: three nested rings / three-chevron glyph;
- Band 4: four-ring burst / four-chevron glyph.

The exact motif must survive monochrome and color-blind modes. Size, count and pulse rhythm are redundant channels. Optional settings may display the numeric band for players who prefer explicit data, but numbers are never required.

### 3.3 Edge attenuation — classes 0–2
Base attenuation should be communicated through the physical passage treatment rather than labels:
- attenuation 0: open/clear passage motif;
- attenuation 1: one visible acoustic-break motif integrated into doorway trim;
- attenuation 2: two-break/heavier damping motif.

During prediction, the route pulse visibly loses one strength step per attenuation cost using the same ring/chevron count language. The player sees **remaining strength**, not a hidden formula.

### 3.4 Barrier effect
A snapped barrier is visually massive enough that its effect is intuitive.
- the blocked passage receives a bold physical seal/shutter presence;
- during prediction, the route reaching that passage visibly loses three steps at once;
- strength-4 leakage is therefore shown as a weak one-step residual pulse rather than implying perfect silence;
- when the barrier is between slots, the previously blocked edge visibly reopens before the new slot activates, matching the locked mechanic.

No partial/gradient attenuation is shown while sliding between slots.

### 3.5 Minimum routes and tied routes
The UI never claims there is only one route when mechanics say otherwise.

If one minimum route exists:
- preview emphasizes that physical path.

If two or more minimum routes tie:
- all tied minimum routes illuminate simultaneously with equal emphasis;
- a small split-pulse at the branching passage makes the equivalence obvious;
- there is no sequential animation implying the first route is mechanically preferred;
- stable ordering may govern animation start only, never emphasis or outcome.

If the player blocks one tied route and another remains, the still-audible route stays visible immediately. This is a key anti-nearest-door lesson.

### 3.6 Listener threshold — three bands
Listener threshold 1–3 uses a persistent, compact motif attached to the listener silhouette:
- threshold 1: one notch/arc;
- threshold 2: two;
- threshold 3: three.

When prediction reaches the listener, the incoming remaining-strength motif is compared visually against the listener threshold motif. Outcome then resolves to a large simple state badge:
- **HEARS**: ear/attention shape opens + directional reaction arrow toward source;
- **DOES NOT HEAR**: muted/closed-ear shape with low-emphasis outline.

Color is supporting only. Shape, animation and pattern carry the result.

### 3.7 Numeric-free comparison
A player should not need to compute `strength - attenuation >= threshold`. The presentation should make it perceptual:
- source begins with N visible pulse units;
- passage cost visibly removes units;
- listener threshold visibly requires M units;
- HEARS/DOES_NOT_HEAR is stated directly.

Optional advanced setting may expose small numbers, but the game is designed to be fully solvable without them.

---

## 4. Prediction interaction model

### 4.1 Automatic local preview
Prediction appears automatically for the **most immediate targetable action** when that action would emit sound and at least one relevant listener exists.

Examples:
- standing near glass shows the glass-event propagation;
- highlighting a distraction shows its route;
- approaching a node boundary may preview the next locomotion pulse;
- manipulating the barrier updates the currently highlighted action preview continuously.

This avoids forcing the player into a separate tactical mode for every step.

### 4.2 Hold-to-preview command
A dedicated preview command is available on both keyboard/mouse and controller. Holding it:
- does not pause simulation;
- emphasizes acoustically relevant world structure;
- displays next locomotion pulse from the player;
- displays source-strength motifs on nearby usable sources;
- displays HEARS/DOES_NOT_HEAR for relevant listeners for the selected/targeted source.

The player may move while preview is held unless another interaction state already constrains movement.

### 4.3 Persistent-preview accessibility option
Optional `Persistent Acoustic Preview` keeps route information visible at reduced emphasis outside active interaction.
- mechanical state is unchanged;
- no extra future information is granted;
- only already-available current-state prediction is kept on screen.

### 4.4 Future consequence boundary
Prediction is exact only for the current event/committed mutation snapshot. It must never imply guaranteed future listener positions when the player has not yet caused those reactions.

Presentation distinguishes:
- **current event result** — solid route + definite HEARS/DOES_NOT_HEAR;
- **post-hearing investigation target** — dashed movement arrow to the event source location;
- later route consequences — not predicted as certainty unless fixed by the currently committed state.

This protects the mechanical preview-equivalence contract.

---

## 5. Barrier manipulation UX

Barrier movement must feel like handling a physical object, not selecting graph edges.

### 5.1 Discoverability
Barrier rail is visually distinctive but environmental:
- floor/wall track;
- visible handle;
- snap sockets aligned with real openings;
- candidate slots use physical brackets, not floating map icons.

When the player enters reach volume:
- handle gains a clear interaction highlight;
- one-line contextual prompt may appear in early onboarding;
- rail endpoints and legal slots brighten subtly.

### 5.2 Grab
On grab:
- camera eases slightly to include the rail and nearest relevant listeners, within authored bounds;
- player animation visibly takes hold;
- controller/keyboard movement is constrained along the rail state space as defined mechanically;
- current active slot receives a strong physical lock indicator;
- acoustic preview appears automatically if the barrier affects a relevant route.

### 5.3 Moving between slots
While moving:
- old active slot unlocks visibly and its route immediately returns to normal once the panel leaves the snap envelope;
- candidate slot displays a ghosted barrier silhouette and predicted route consequence;
- a tactile snap-zone animation/haptic cue grows as the barrier nears a legal slot;
- invalid/blocked movement stops physically at the obstruction boundary; it never accepts input then silently refuses later.

### 5.4 Snap
On canonical snap:
- short mechanical clamp animation;
- concise haptic pulse on controller;
- acoustic route redraw resolves in the same frame/tick presentation;
- affected passage receives the barrier-seal visual;
- no long celebratory animation interrupts the live world.

### 5.5 Invalid states
Reasons are local and specific:
- `BLOCKED PATH`: world obstruction marker on the rail;
- `OUT OF REACH`: handle-zone icon rather than global error text;
- `INVALID SLOT`: crossed physical bracket if a slot is temporarily unusable.

Do not display simulation jargon such as `edge disabled` or `node mismatch` in normal play.

### 5.6 Release between slots
If released between slots:
- a clear return-arrow points to the deterministic destination slot;
- the barrier visibly rolls/slides back;
- preview shows no attenuation until it re-snaps;
- the player can immediately re-grab if still in range after return.

### 5.7 Rotation stations
If a rail contains an authored rotation station:
- rotation is presented as a physical hinge/turntable event;
- only legal orientations are shown;
- rotation never suggests a different attenuation magnitude unless a future formally approved content amendment creates a visibly distinct canonical archetype.

---

## 6. Listener presentation

Listener states must be understandable without a suspicion meter.

### 6.1 Persistent identity
Each listener receives:
- stable silhouette/accent pattern;
- threshold motif 1–3;
- optional label A/B/C only in accessibility/debug-like clarity mode, not required baseline;
- direct-detection boundary presentation appropriate to encounter geometry.

For two-listener selective-audibility content, the two listeners must be distinguishable by more than color alone: silhouette accessory, stripe pattern, icon shape or stance.

### 6.2 State language

**POSTED**
- neutral stance/patrol motion;
- small anchor/route indicator only when relevant;
- threshold motif persistent.

**INVESTIGATE**
- immediate `heard` flash using the same incoming pulse motif;
- investigation target marker appears at the physical source-at-emission position;
- listener path arrow is short/local, not a full abstract nav mesh;
- state symbol points toward target.

**ARRIVED / SEARCH**
- compact search arc around the event source location;
- fixed-duration progress shown by shrinking/filling motif if timing matters;
- no random wandering visual language.

**RETURN**
- return-anchor icon + subdued path cue;
- no misleading `still alerted` red state if the listener is mechanically returning normally.

**ALERT_FAIL**
- direct detection connection from listener to player is shown clearly;
- failure presentation distinguishes **heard event** from **direct detection** so players do not learn the false rule `hearing = fail`.

### 6.3 Current investigation ownership
When a listener is investigating an event, the causing event's strength/intensity signature remains available in a compact state chip near the listener or target marker. This helps explain retarget rules without exposing numbers.

If a new event is too weak/equal to retarget:
- the new pulse may reach the listener visually;
- a small `heard but no retarget` lock/priority marker appears briefly;
- the existing investigation target remains emphasized.

This is important for explaining why repeated equal-strength lure spam does not work.

---

## 7. Direct-detection presentation

Acoustic hearing and direct detection are separate systems and must look separate.

Baseline visual grammar:
- hearing: route pulses through passages + ear/attention state;
- direct detection: local line-of-sight/proximity shape around listener, visually different from acoustic routes.

If detection includes a forgiveness hold:
- a short local fill arc may show imminent fail;
- it must not be confused with hearing threshold;
- assist settings may widen timing, never hide acoustic truth.

On fail:
1. freeze or strongly slow for a very short confirmation beat only after fail is mechanically resolved;
2. show listener→player detection line/region;
3. optionally show the last relevant acoustic event separately if it caused the listener to investigate there;
4. display concise reason text such as `Detected while crossing the east room`, not `Too loud` unless sound itself was actually the causal reason for listener location.

---

## 8. Player movement and locomotion noise feedback

### 8.1 WALK vs FAST_MOVE
Movement noise is visible even without preview:
- WALK: small periodic footstep pulse at canonical cadence;
- FAST_MOVE: larger/faster pulse motif.

The player character animation and footprint/pulse rhythm reinforce the difference.

No stamina bar is shown because no stamina system exists.

### 8.2 Upcoming locomotion pulse
When preview is held or a listener is acoustically relevant:
- a subtle ring around the player shows time/distance until the next locomotion event;
- crossing into a new acoustic node updates the predicted source region immediately;
- the indicator must be deterministic and derived from the actual cadence state.

This avoids surprise footsteps near region boundaries.

---

## 9. Source/objective presentation

All usable sound-producing objects need two readable facts before activation:
1. **what interaction is available**;
2. **how strong the sound event will be**.

Canonical object treatment:
- interaction icon tied to action fiction;
- strength-band motif adjacent to it;
- preview route when focused/targeted;
- single-cycle/used state visibly changes the object if applicable.

Required loud objectives should look consequential enough that strength 3–4 does not feel arbitrary.

Moving environmental sources:
- must be visible on their authored route;
- their current source node/pulse originates from current position;
- if they emit periodically, the next emission timing is telegraphed with a world-space rhythm indicator rather than an abstract global timer.

---

## 10. Door mutation UX

Doors are both traversal and acoustic graph mutations; their state change must be unambiguous.

OPEN:
- physical opening readable;
- active route can propagate through it.

CLOSED:
- physical panel visibly seals passage;
- route disappears, not merely dims.

For an interaction that emits sound and mutates a door:
- preview explicitly animates whether the sound travels through pre-change or post-change geometry;
- a brief order glyph may show `sound → close` or `open → sound` using simple before/after pictograms;
- this is used only where the distinction matters, avoiding routine clutter.

No player-facing terminology `BEFORE_MUTATION / AFTER_MUTATION` is required.

---

## 11. HUD philosophy

HUD is intentionally minimal because most information belongs in the world.

Persistent HUD may contain only:
- current objective(s);
- optional encounter/mastery target;
- checkpoint state indicator when useful;
- small control reminder in onboarding/after long inactivity;
- pause/settings affordance.

Not persistent by default:
- minimap;
- node graph;
- sound meter;
- suspicion bar;
- barrier cooldown/mana;
- listener health;
- inventory.

### 11.1 Objective display
Objectives use short action language:
- Reach control room
- Trigger the press
- Retrieve the file
- Exit through north stair

Objective fiction remains light and does not introduce hidden state. Completed objectives receive a concise checkmark/state change.

### 11.2 Mastery display
Mastery conditions are optional and shown before replay/encounter start and in pause screen. In-run display may be compact:
- barrier edits remaining/target;
- time target;
- no-restart intact/broken;
- selective-hearing target.

Mastery UI never changes the baseline rule set.

---

## 12. Controls

Inputs must support equal first-class keyboard/mouse and controller play with no pixel precision.

### 12.1 Keyboard/mouse baseline
- Move: WASD
- Fast Move: Shift / remappable hold or toggle
- Interact / Grab / Confirm: E or left mouse contextually
- Release / Cancel: right mouse or secondary key
- Acoustic Preview: Space / remappable hold or toggle
- Barrier rail move: movement axis while grabbed or mouse drag constrained to rail
- Rotate at station: Q/E or mouse wheel/context button when rotation is legal
- Quick Restart: R hold/confirm-safe configurable
- Pause: Esc

Mouse picking always snaps to valid world interactables/rail handles. No clicking on thin graph edges is required.

### 12.2 Controller baseline
- Move: left stick / d-pad optional
- Fast Move: left trigger or face-button modifier, remappable
- Interact / Grab / Confirm: primary face button
- Release / Cancel: secondary face button
- Acoustic Preview: left bumper/trigger remappable
- Barrier rail move: left stick along constrained rail axis while grabbed
- Rotate at station: shoulder buttons or d-pad when legal
- Quick Restart: dedicated hold chord or menu action; must avoid accidental loss
- Pause: menu button

### 12.3 Focus/selection rules
- contextual focus prioritizes nearest reachable interactable inside a forward/nearby cone;
- if two candidates overlap, d-pad/mouse cycle selects explicitly;
- acoustic preview never changes focus automatically after the player commits to an interaction;
- barrier snap slots are selected by physical movement along rail, not radial menu;
- no essential action requires placing a cursor at sub-character precision.

### 12.4 Remapping
All gameplay actions are independently remappable. Hold/toggle options are available for Preview and Fast Move. Barrier manipulation must work with a single stick and two buttons if needed.

---

## 13. Onboarding and first boot

Onboarding should teach by consequences, not a rule manual.

### 13.1 First boot
1. logo/title;
2. accessibility-first setup shortcut: text size, contrast, motion, subtitles/captions, input device;
3. start demo/campaign with no mandatory lore exposition;
4. optional concise `How sound works` reference becomes available after first acoustic preview, not before play.

### 13.2 D01 onboarding — first 3–4 minutes
- player can move immediately;
- first WALK footstep pulse appears within opening seconds;
- one posted listener visibly receives or does not receive it based on a simple route;
- barrier rail is encountered naturally;
- grab prompt appears once;
- moving barrier between two slots flips the predicted route;
- first independent barrier choice occurs by ~minute 2–3.

No arithmetic, node terminology or stealth textbook.

### 13.3 D02 — alternate route + lure
Teach:
- blocking the visually nearest route may not be enough;
- a deliberate sound can be useful;
- listener investigation target is the event source, not the player magically revealed.

### 13.4 D03 — two listeners + threshold distinction
Teach:
- listeners can differ visibly in hearing threshold;
- stronger objective sound can over-propagate;
- door mutation can alter route.

### 13.5 D04 — selective audibility climax
Must make the thesis undeniable:
- one listener **must hear**;
- another **must not**;
- player physically relocates the barrier before extraction;
- preview and actual route reaction are visible in one coherent world-space shot.

If a player exits the demo describing the game only as `put wall in front of sound so guards cannot hear`, onboarding has failed even if the level was completed.

---

## 14. Pause, settings and restart flow

### 14.1 Pause
Pause menu contains:
- Resume
- Restart from Checkpoint
- Restart Encounter
- Objectives / Mastery
- Controls
- Accessibility
- Audio
- Visual
- Return to Campaign

Pausing stops simulation. Opening Acoustic Preview does not.

### 14.2 Quick restart
Quick restart is designed as a learning tool.
- one short input with accidental-activation protection;
- restoration should feel immediate;
- screen transition ideally <= roughly one second perceived once implementation supports it;
- restart screen does not lecture or hide the cause of the previous fail.

After restart:
- barrier, listener, source, door and objective presentation exactly matches restored canonical snapshot;
- next-action prediction must also match pre-saved state.

### 14.3 Checkpoint communication
Checkpoint activation uses a subtle world/UI confirmation; no giant banner.
- checkpoint appears only at authored safe state;
- pause menu states `Restart from checkpoint` clearly;
- mastery `NO_RESTART` status may be lost as defined, but baseline completion remains unchanged.

---

## 15. Accessibility architecture

Accessibility is part of the core product because acoustic information cannot depend on hearing.

### 15.1 No-audio parity
With master audio at 0:
- all source events remain visually signaled;
- propagation route is visible when relevant;
- sound strength is encoded by count/shape/animation;
- listener threshold is persistent;
- HEARS/DOES_NOT_HEAR is explicit;
- investigation target and state transition are visual;
- moving-source emission timing is visual;
- failure reason remains understandable.

No mechanic uses pitch, stereo direction, loudness judgment or voice recognition.

### 15.2 Color-independent presentation
Every important state uses at least two non-color channels:
- shape/pattern;
- count/notch;
- silhouette;
- animation direction;
- icon state.

Color-blind presets may remap hues, but no preset changes acoustic logic.

### 15.3 Contrast
Options:
- High Contrast World
- High Contrast Acoustic Routes
- Listener Outline Strength
- Barrier/Slot Highlight Strength
- Background Detail Reduction

The accessibility preview mode may dim non-acoustic scenery while preserving physical geometry boundaries.

### 15.4 Reduced motion
Reduced Motion mode may:
- replace expanding pulse rings with stepped/static route fills;
- reduce camera ease/zoom motion;
- remove screen shake;
- shorten decorative snap animation;
- replace listener reaction bounce with static icon swap.

It may not remove timing information. Moving-source timing remains visible through static progress ticks if pulse animation is reduced.

### 15.5 Preview persistence
Options:
- Hold
- Toggle
- Context Automatic + Hold
- Persistent Current-State Preview

All show the same current mechanical facts.

### 15.6 Text/icon scaling
- UI scale presets plus continuous slider;
- objective text wraps safely at handheld resolution;
- listener/source motifs scale independently from decorative UI where possible;
- optional explicit labels `HEARS` / `SAFE FROM SOUND` may accompany icons.

### 15.7 Simulation-speed accessibility
Allowed simulation-speed presets may slow the **entire deterministic gameplay simulation consistently**, including:
- player movement;
- listener movement;
- search/return timers;
- moving environmental sources;
- door/object timed movement where gameplay-relevant;
- locomotion event cadence where defined in simulation time.

This preserves event ordering and solution logic. Acoustic propagation itself is mechanically instantaneous at event resolution; only its visual playback may be slowed independently.

Proposed assist presets for implementation validation: 100%, 85%, 70%, 55% simulation speed.

Rules:
- no listener-only slowdown that creates a different acoustic solution unless implemented later as an explicitly separate assist mode with clear disclosure;
- speed changes cannot alter attenuation, strength, thresholds or update ordering;
- mastery time targets may be disabled or normalized when using reduced simulation speed, but base campaign completion remains valid.

### 15.8 Input accessibility
- full remapping;
- hold/toggle switches;
- generous interaction reach option within the locked legal-variable allowance;
- barrier snap generosity option;
- one-stick barrier manipulation;
- no rapid button mashing;
- restart and pause always available outside deliberately atomic interactions.

---

## 16. Failure explanation system

A major product promise is: **the player can explain why a listener heard or detected them**.

### 16.1 After a hearing outcome
When useful, a short `cause trace` can persist for 1–3 seconds:
- source icon;
- actual physical minimum route(s);
- remaining-strength motif at listener;
- listener threshold motif;
- HEARD / NOT HEARD result.

This is the committed-event version of preview, not a separate post-hoc calculation.

### 16.2 On detection failure
Failure card is concise and specific:
- `Listener B detected you in the control corridor.`
- subline if acoustically relevant: `Your glass break pulled B here through the north route.`

Optional `Show Why` expands the last-cause trace in the frozen failure frame.

### 16.3 Common explanatory cases

**Blocked one route, tied route remained**
- show both equal routes;
- blocked route terminates at barrier;
- surviving route remains highlighted;
- explanation: `A second equally quiet route remained open.`

**Barrier leaked strength-4 event**
- show four-unit pulse reduced by three at barrier, one unit continues;
- listener threshold 1 receives it;
- explanation: `The barrier reduced the sound, but this listener still heard the remaining pulse.`

**Listener did not retarget**
- show incoming event reached listener;
- compare current investigation-causing intensity versus new intensity with motifs;
- explanation: `Heard, but not stronger than the current investigation.`

**Door-ordering case**
- replay tiny before/after pictogram so player sees whether door opened before sound.

No failure explanation should expose hidden simulation state not otherwise available during play.

---

## 17. Audio identity

Audio is important for feel but mechanically redundant.

### 17.1 Functional audio layers
- source impact/footstep sound corresponds to strength band;
- barrier movement has heavy mechanical scrape/roll and decisive snap;
- propagation may use subtle spatialized whoosh/room-tone reinforcement;
- listener hearing reaction has concise confirmation;
- doors/sources retain strong physical foley.

### 17.2 Mechanical redundancy rule
Every functional audio cue has an equivalent visual cue available simultaneously. Audio may make comprehension faster or more satisfying but cannot reveal a route, threshold, state change or timing unavailable visually.

### 17.3 Atmosphere
Use restrained industrial/facility ambience with enough negative space that player-caused sound events feel important. Avoid horror stingers as the primary emotional language; the player should feel clever and causally in control, not helpless before unseen sound rules.

Music should not mask source-class differences. Dynamic music may react broadly to progression but not encode exclusive listener state.

---

## 18. Visual identity

Target identity: **quiet industrial infiltration with visible acoustic geometry**.

### 18.1 World aesthetic
- compact stylized facilities;
- clear architecture silhouettes;
- modular industrial/acoustic surfaces;
- restrained decorative clutter;
- barrier hardware visually iconic across themes;
- listener designs simple enough that threshold/state motifs remain readable.

### 18.2 Acoustic visual signature
The store/trailer-recognizable image should be:
- a physical room/corridor network;
- one large barrier visibly sealing one passage;
- a sound pulse branching through alternative openings;
- one listener highlighted as hearing while another is screened;
- player already moving through the opening created by that difference.

The marketing image should not resemble:
- waveform software;
- a node graph on a black background;
- generic stealth cone screenshot;
- horror microphone gimmick;
- `be completely silent` challenge.

### 18.3 Facility themes
Phase-5 allows 4–6 modular themes. Presentation rule: themes may change materials, lighting and fiction wrappers but must preserve canonical acoustic readability.

Possible non-canonical art directions for implementation exploration:
- records/archive facility;
- mechanical plant;
- research/clean industrial wing;
- broadcast/utility infrastructure;
- secured office/service complex.

Themes cannot introduce unique acoustic materials or hidden rules.

---

## 19. Store capsule and trailer communication

`HUSHLINE` remains provisional and not trademark-cleared. Marketing design should test the concept without depending on the title.

### 19.1 Capsule thesis
A capsule should show:
- infiltrator near a large movable barrier;
- visibly split sound route;
- two listeners with opposite hearing outcomes;
- strong physical environment, not abstract UI.

Avoid a lone crouched silhouette with sound waves; that would market generic sound stealth.

### 19.2 First 10 seconds of trailer
Suggested normal-play communication:
1. player approaches loud objective;
2. preview shows both listeners would hear;
3. player physically slides barrier to another doorway;
4. route flips: Listener A HEARS, Listener B DOES NOT HEAR;
5. player triggers loud action;
6. A investigates; player crosses through the opening.

No narration is required to understand the causal before/after.

### 19.3 Short store description target
Presentation should support a future store sentence structurally equivalent to:
`Move one soundproof barrier through compact facilities, reroute every noise, and decide which guards should hear you.`

This is a communication test, not frozen commercial copy.

---

## 20. Representative presentation paper tests

### PT1 — P1 tied-route posted puzzle
State: one listener, two tied acoustic routes, barrier blocks only one.

Required presentation result:
- both tied routes light equally before barrier move;
- after snapping barrier, blocked route visibly loses pulse at barrier;
- second route remains equally emphasized;
- listener remains HEARS;
- player is never told `blocked` globally.

**PASS on paper.** The tied-route mechanic can be represented without graph UI.

### PT2 — P2 threshold split / selective audibility
State: Listener A threshold 1, Listener B threshold 3; one event produces different remaining strength.

Required result:
- A/B have visibly distinct threshold motifs;
- same source pulse reaches each with different remaining-unit count;
- A HEARS while B DOES NOT HEAR, or vice versa according to actual paper state;
- distinction remains legible in monochrome/high-contrast mode.

**PASS on paper.** Count + threshold + direct outcome avoids arithmetic requirement.

### PT3 — P3 active lure + exposed barrier
State: player intentionally routes sound to A so A leaves rail handle area.

Required result:
- preview clearly shows A will hear and B will not;
- after commit, A's investigation target is the physical lure source;
- route to barrier handle becomes visibly open in world rather than represented as a tactical overlay;
- player reaches and manipulates barrier while world remains live.

**PASS on paper.** Physical fantasy remains intact.

### PT4 — P4 door-ordering
State: one action opens door then emits; another emits then closes.

Required result:
- interaction preview uses tiny order pictogram only while action is targeted;
- route preview matches the correct pre/post door state;
- post-action pulse exactly follows preview.

**PASS on paper**, with implementation requirement that presentation consume canonical `emission_phase` rather than infer order.

### PT5 — P5 moving source
State: environmental cart moves among nodes and emits periodically.

Required result:
- source remains visibly physical;
- next pulse timing appears on source itself;
- route originates from current source region;
- player can read changes without watching a global timeline.

**PASS on paper.** Reduced Motion mode uses static tick/progress motif.

### PT6 — P7 exceptional three-listener state
State: three listeners thresholds 1/2/3, <=10 nodes.

Required result:
- all three distinguishable without color;
- each threshold motif legible;
- preview can show three outcome badges without covering routes;
- only decision-relevant listener traces remain high emphasis.

**CONDITIONAL PASS.** This class must be cut or redesigned if handheld/graybox readability testing shows overlap or visual overload. The presentation does not justify adding a global listener table.

### PT7 — P8 final-style synthesis
State: 12 nodes, two listeners, door mutation, lure, loud objective, three meaningful barrier positions.

Required result:
- preview emphasizes only current target source and its minimum routes;
- inactive acoustic structure remains low emphasis;
- listener current state/target persists locally;
- objective mutation redraws world routes immediately;
- return-path change is understandable without minimap graph.

**PASS on paper** under the rule that only 3–4 simultaneous decision-relevant routes receive high emphasis, matching Phase-5 climax density.

---

## 21. Contradiction audit

No Phase-3/4/5 mechanic was changed for presentation convenience.

Resolved presentation questions:
- barrier between slots remains mechanically inactive; UX explicitly shows old edge reopening before new snap;
- barrier strength-4 leakage is shown, not silently rounded to binary blocking;
- tied minimum routes are all presented;
- listener retarget strength rule is explained by committed event motifs, not a suspicion bar;
- door event ordering is presented only where relevant and uses canonical emission phase;
- simulation speed assist slows the deterministic simulation consistently rather than changing acoustic logic;
- no-audio parity is complete by construction;
- three-listener content remains an exceptional empirical readability gate rather than grounds for abstract global UI.

Potential implementation-phase empirical risks, not design contradictions:
1. whether route VFX remain readable against all 4–6 environment themes;
2. whether barrier manipulation feels satisfying at target frequency ~1.5/minute;
3. whether handheld display can show tied routes + two listeners without clutter;
4. whether explicit HEARS/DOES_NOT_HEAR badges feel too gamey versus necessary clarity;
5. whether 55–70% simulation-speed assist still feels fluid while preserving ordering;
6. whether three-listener exceptional encounters pass readability at all.

These are empirical gates, not reasons to change the locked mechanical model now.

---

## 22. Phase-6 acceptance gates

Phase 6 is complete because:
- camera/framing rules are defined for desktop and handheld targets;
- world architecture and acoustic topology remain visually embedded in physical space;
- source strength 1–4, attenuation 0–2, barrier +3 effect and threshold 1–3 have numeric-free redundant presentation;
- tied minimum routes are all visibly represented;
- HEARS/DOES_NOT_HEAR is explicit and deterministic;
- barrier grab/move/snap/invalid/release UX is fully defined without remote graph control;
- listener POSTED / INVESTIGATE / SEARCH / RETURN / ALERT_FAIL states have distinct presentation;
- hearing is visually separated from direct detection/failure;
- keyboard/mouse and controller maps avoid pixel precision;
- first-boot through four-encounter demo onboarding is defined and reaches first independent barrier decision by ~minute 2–3;
- HUD remains minimal and world-first;
- pause, checkpoint and fast restart presentation are defined;
- complete no-audio decision parity is specified;
- color-independent patterns, contrast, reduced motion, preview persistence, text/icon scaling, remapping and deterministic simulation-speed accessibility are specified;
- failure explanation can show exactly why a listener heard/detected the player without exposing hidden data;
- audio is reinforcement only, never exclusive mechanical information;
- visual identity and trailer/capsule communication emphasize physical selective audibility rather than generic stealth/graph software;
- representative tied-route, two-listener, door-ordering, moving-source, three-listener and final-synthesis states are paper-tested;
- no locked acoustic mechanic or content schema was changed.

**PHASE 6 UX / PRESENTATION ARCHITECTURE = COMPLETE.**

## NEXT DESIGN HANDOFF
Proceed to **Phase 7 — Economy / Retention / Commercial Model**. Create `GAME4_ECONOMY_COMMERCIAL.md`. Use current market research because pricing, Steam demo practice, platform expectations and comparable positioning are time-sensitive. Define premium pricing logic, demo packaging, campaign/progression packaging, replay/mastery incentives, achievements/platform features, retention expectations without live-service mechanics, monetization boundaries, launch/discount assumptions, commercial risk gates and scope/value comparison against current compact premium puzzle/stealth products. Do not add currencies, grind, upgrades or live-service systems merely to increase retention.