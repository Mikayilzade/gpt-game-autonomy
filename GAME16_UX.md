# GAME #016 — PHASE 6 UX / PRESENTATION ARCHITECTURE

Date: 2026-09-03
Status: PHASE 6 COMPLETE
Working title: **ONE-WAY WORKSHOP**
Authority: `GAME16_CONTENT.md`, `GAME16_MECHANICS.md`, `GAME16_PRODUCT_THESIS.md` and prior active Game #016 authorities.

## 0. UX objective
The player must be able to understand and operate the hardest canonical case, including OW23/OW24, with mouse or controller/Steam Deck, without cursor hunting, hidden state, tiny labels, color-only coding, a separate genealogy screen, or freeform precision manipulation.

The workbench is a tactile proof surface. Physical objects carry the primary meaning; overlays explain rather than replace them. The interface may expose state and causality, but it must never reveal a winning future sequence.

Fresh 2026 platform/accessibility checks carried into this contract:
- Steam Input guidance expects controller-specific glyphs, action-oriented remapping/configuration, controller/mouse coexistence and couch-readable UI.
- Steam Deck compatibility guidance recommends 1280×800 support and text comfortably readable on the handheld display; design target here is 12 px minimum rendered character height at 1280×800 for dense secondary labels, larger for normal UI.
- Essential information must never be encoded by fixed color alone; controls must be remappable and important audio cues need visual redundancy.

These are product requirements, not implementation details.

---

# 1. Workbench and camera model

## 1.1 Single bounded tabletop scene
Every job is played on one compact workbench with four persistent zones:
1. **Plan Rail** — top/upper-left: final assembly silhouette, mandatory operations and requirements.
2. **Stock Bay** — left/lower-left: initial stock and currently loose children.
3. **Operation Bay** — right: jig stations and guided-operation fixtures.
4. **Assembly Pad** — center/right-center: final part slots and certification mechanism.

No walking avatar, traversable shop, physics clutter, or hidden drawers. All current physical pieces are either visible on the bench or represented by one visible stack/fan in the Stock Bay when overlap avoidance is needed.

The hardest case must fit the complete logical state into one bench scene with <=8 loose children, <=3 roots and <=8 station archetypes.

## 1.2 Camera
Baseline camera is a fixed oblique tabletop view with bounded orbit, pan and zoom:
- orbit: small authored arc only; no free camera inversion puzzle;
- zoom: three useful bands — Overview, Work, Inspect;
- pan: constrained so Plan Rail and Assembly Pad are never simultaneously lost for more than one input action;
- selecting an object may softly frame it, but never forcibly spins the camera during a reasoning step.

No puzzle predicate depends on camera angle. Occluded sockets/stations receive a temporary edge marker and can be focused directly.

### Camera accessibility
Options:
- camera motion speed;
- camera easing on/off;
- auto-frame on/off;
- screen shake off by default for essential operations and independently disableable if decorative shake exists;
- reduce motion mode removes nonessential sweep/zoom transitions and shortens split/certification camera moves.

---

# 2. Input model — mouse, controller and Steam Deck

## 2.1 Semantic actions
Input is action-based, not tied to fixed device buttons. Required remappable actions:
- Navigate Focus
- Select / Pick Up
- Cancel / Put Back
- Inspect
- Toggle Requirement Overlay
- Cycle Compatible Targets
- Rotate Piece Left / Right
- Zoom In / Out
- Camera Orbit / Pan
- Preview Cut
- Confirm Commit
- Restart Job
- Certify
- Pause

Displayed glyphs follow the active controller/device. Mouse and controller may be alternated without mode-reset or stale prompts.

## 2.2 Mouse path
- Hover gives outline + one-line identity/capability summary.
- Left click selects/picks.
- Drag may move a loose piece only between discrete valid bench docking targets; no free placement affects logic.
- Right click or dedicated Cancel returns/cancels.
- Wheel zooms; middle/right drag may camera-pan/orbit according to settings.
- Clicking a cut socket enters Cut Preview; destructive action still requires explicit commit confirmation.

Mouse precision is convenience only. Every target has an equivalent focusable controller action.

## 2.3 Controller / Deck path
The controller path uses **semantic focus navigation**, not a fake analog cursor as the only method.

At top level, d-pad/stick moves among four bench zones. Within a zone:
- left/right cycles siblings or stations;
- up/down cycles logical layers where needed (piece → its cut sockets; station → requirement; assembly slot → requirement);
- shoulder buttons cycle compatible targets for the selected piece;
- Inspect opens the selected object's compact card;
- Select picks/docks/activates;
- Cancel returns one hierarchy level.

Analog stick may also move camera. Trackpad/mouse-style pointer is optional convenience, never required.

## 2.4 Focus graph contract
Focus neighbors are authored/generated from logical relationships, not screen proximity alone. The focus graph must remain stable when pieces animate.

Priority order when a piece is selected:
1. valid part slots;
2. compatible jig stations;
3. legal cut sockets on the piece;
4. other loose children;
5. Plan Rail requirement linked to the selection.

Invalid but educationally relevant targets may be included after valid targets, with a clear rejection reason on inspect; they must never require trial clicks to learn a hidden predicate.

No state may require cycling through more than:
- 8 loose children;
- 5 cut sockets on the focused piece;
- 8 stations/part slots combined in one local cycle.

Long cycles must be partitioned by zone or capability relation.

---

# 3. Selection hierarchy and object handling

## 3.1 Selection states
Every interactable has exactly four visible focus states:
- Idle
- Focused
- Selected / carried
- Targeted preview

Focused and selected must differ by shape treatment + motion/outline, not color alone.

## 3.2 Piece fan / anti-clutter rule
When >5 loose children exist, the Stock Bay uses shallow non-overlapping lanes grouped by root stock. Children are laid out in lineage order within each root lane. This is presentation grouping only; it does not imply required solution order.

If a child is currently in a station or part slot, its root lane shows a small non-interactive silhouette placeholder so ancestry can still be followed without opening another screen.

No physical piece may be hidden behind another piece in Overview camera.

## 3.3 Pick/place
Picking a piece lifts it a small fixed amount and reveals valid destinations through soft physical affordances. The player never drags to arbitrary 3D coordinates for correctness.

Valid target snap:
- compatible station/slot visibly opens/highlights its silhouette;
- incompatible target remains selectable for inspection but does not magnetize;
- release over invalid space returns piece to origin; no accidental state change.

Reversible docking has no confirmation dialog.

---

# 4. Capability language — physical first, overlay second

## 4.1 Shared encoding system
Every capability uses three redundant channels:
1. **physical form** — silhouette, notch, edge orientation, span against cradle;
2. **symbol** — stable icon/pattern;
3. **optional text** — plain-language label in Inspect/Requirement view.

Color is only a fourth reinforcement channel.

## 4.2 `SPAN`
Primary representation: bracket/gauge silhouette showing the minimum/target extent against the piece axis. Named bands use repeated notch counts/patterns rather than hue alone.

UI label examples: `Short span`, `Medium-or-long span`. Do not expose algebraic `M+` notation to players.

When comparing to a station, a ghost bracket aligns directly with the relevant local axis.

## 4.3 `EDGE`
- `STRAIGHT`: continuous ruler/fence symbol plus straight groove silhouette.
- `DIAGONAL_A`: one diagonal hatch direction + keyed triangular seat.
- `DIAGONAL_B`: opposite hatch direction + differently keyed triangular seat.

A/B are never distinguished by color alone and should have visibly different keyed geometry.

## 4.4 `FACE`
- `FLAT`: flat-seat glyph and planar contact preview.
- `NOTCHED`: notch glyph + matching keyed fixture profile.

## 4.5 `PAIR`
Visible paired siblings carry complementary physical marks created at the same cut: matching notch halves / mirrored cut scar plus paired-link symbol. Selecting one can momentarily pulse its sibling. No arbitrary genealogy code is shown.

## 4.6 Witnesses
Witnesses are physical marks on the workpiece plus icon:
- `HOLE`: visible drilled pattern;
- `MARK`: engraved/marked reference line;
- `SPACING`: spacing stamp/notch pattern;
- `ANGLE`: visible guided diagonal mark/feature.

A station requirement never asks the player to remember an invisible witness.

---

# 5. Station compatibility and role state

## 5.1 Compatible fit
When a selected child can dock:
- station shows exact contact silhouette;
- required capability symbols appear adjacent;
- piece ghost-snaps into orientation;
- one short affirmative sound/tactile pulse may occur on hover/focus.

## 5.2 Incompatible fit
An incompatible piece never partially seats as if precision were wrong. It stops cleanly before the fixture, and the compact reason names the missing visible requirement, e.g. `Needs notched face` or `Needs Diagonal A edge`.

No penalty, commit or animation delay.

## 5.3 Role state
A piece may currently be:
- Loose
- Part
- Jig (temporary)
- Jig (will be consumed)
- Spent parent / historical
- Consumed

Current physical roles use location first: part in Assembly Pad, jig in Operation Bay, loose in Stock Bay. Inspect card repeats role with icon and text.

Consume-on-operation stations display an unmistakable **consumption marker** before commit: broken-outline icon + plain language `This piece will be consumed`. Temporary stations show `Released after operation`.

---

# 6. Cut preview and irreversible commit UX

## 6.1 Entering Cut Preview
Select loose cuttable piece → choose one visible cut socket → Preview.

Preview freezes no logical state. The parent remains intact. Both deterministic child ghosts separate by a few centimeters and show:
- child silhouettes;
- inherited/new base capability icons;
- direct compatibility pips for already-visible stations/part slots;
- root/lineage relation back to parent.

It does **not** show future solution correctness, future hidden cuts, or a green/red `good choice` verdict.

## 6.2 Commitment affordance
Irreversible fabrication commits use a consistent two-stage gesture:
1. enter preview/operation-ready state with ordinary Select;
2. **hold Confirm Commit for ~0.45 s** by default, or use accessibility option `Double press` / `Single press after explicit confirmation banner`.

The hold ring is around the actual blade/operation control, not a modal centered dialog. Cancel exits instantly.

The confirm line names the irreversible consequence in plain language:
- `CUT — parent is permanently replaced by these two pieces`
- `DRILL — witness is permanent; jig will be released`
- `MARK — witness is permanent; jig will be consumed`

No ordinary reversible docking uses this gesture.

## 6.3 Anti-tedium rule
After the player has successfully completed OW01, explanatory sentence length may collapse to icon + `Hold to cut`; the physical hold remains. Players may shorten hold duration in accessibility settings, but destructive and reversible actions must remain semantically distinct.

## 6.4 Commit animation
Target 0.7–1.4 s total, skippable/acceleratable after first viewing. During atomic commit input is ignored except pause. Result returns focus to the most recently created/modified relevant child rather than to an arbitrary bench object.

---

# 7. Lineage and causal trace without a genealogy screen

## 7.1 Persistent lineage marks
Every root stock receives a neutral root mark: shape badge + pattern, not just color. Children inherit the root badge and add a compact cut-scar branch mark. The player should distinguish three roots and up to six commit generations without reading IDs.

No full tree is permanently drawn across the bench.

## 7.2 On-demand trace
Hold Inspect on a current piece or requirement to enter **Trace View**:
- unrelated pieces dim slightly;
- parent/child chain is drawn as short luminous connectors across current bench placeholders;
- spent parents appear as translucent historical silhouettes in their root lane;
- consumed pieces appear as crossed historical silhouettes;
- guided-operation witness events appear as small operation nodes.

Trace View answers `How did this piece/requirement get here?`, not `What should I do next?`.

## 7.3 Requirement-backward trace
From an unmet requirement, Trace View may show:
- the current slot/station that needs a capability/witness;
- current pieces that **already satisfy** it;
- if dead-state certainty exists, the spent/consumed branch that eliminated all reachable producers.

It must not enumerate future cuts that would create the requirement or rank legal current cuts.

## 7.4 OW23/OW24 readability ceiling
A six-commit late trace may show at most six commit/event nodes and three root lanes at once. If multiple irrelevant ancestors exist, collapse them into a single spent-parent silhouette; expanding them is optional inspection, never required to understand the current causal path.

This replaces the need for a separate genealogy UI.

---

# 8. Plan, HUD and requirement inspection

## 8.1 Default HUD
Persistent HUD is intentionally small:
- case ID/title;
- Restart;
- Inspect/Overlay prompt;
- Certify button when assembly pad is reachable;
- optional hint entry after unlocked by settings/Phase 7;
- pause/settings.

No score, timer, currency, inventory counter or move grade.

## 8.2 Plan Rail
The Plan Rail presents requirements as physical cards tied to final part silhouettes/operation fixtures. Each mandatory requirement has:
- icon/silhouette;
- short text label;
- state: unmet / physically satisfiable now / completed;
- inspect path to its station/part slot.

`Physically satisfiable now` means a currently available piece matches; it does not imply that using it is strategically correct. Therefore it uses a neutral open-circle affordance, not green approval.

## 8.3 Requirement overlay
Toggle overlays concise requirement badges on relevant stations/slots and capability badges on loose pieces. Overlay is optional and never the only representation.

Overlay has three densities:
- Minimal (default): only focused relations;
- Standard: all current station/slot requirements;
- High information: also capability badges on all loose pieces.

Deck defaults to Minimal with large readable focused cards.

---

# 9. Onboarding and first-session flow

## 9.1 First boot
First boot sequence:
1. logo/title → `Play` prominent;
2. optional accessibility quick settings before gameplay: text scale, motion, hold/double-press commit, controller glyph mode;
3. start directly into OW01; no multi-page lore/menu gate.

## 9.2 Modal tutorial budget
Campaign tutorial uses maximum **four blocking prompts total** across OW01–OW05:
1. Select stock / inspect plan;
2. Preview a cut before committing;
3. Hold to commit irreversible cut;
4. Dock byproduct into matching station and perform guided operation.

Every other lesson is contextual non-blocking callout or physical affordance.

A blocking prompt disappears permanently after demonstrated action and is reviewable in Help.

## 9.3 Prompt fading
First occurrence: full sentence + glyph.
Second: short phrase + glyph.
After successful independent use: glyph/affordance only.
Prompts re-expand after repeated failed input or if `Persistent Guidance` accessibility option is enabled.

## 9.4 OW01 → OW03 → OW05 → D1 demo teaching path
- **OW01:** player learns preview → commit → child → spacer jig → guided operation → certify. Trace View is optional after first cut, not forced.
- **OW03:** no new modal. The plan highlights a keyed small station while the visually large offcut remains tempting; incompatibility feedback teaches that size is not value.
- **OW05:** first `EDGE(STRAIGHT)` icon is introduced beside a physical fence silhouette; selecting the edge-bearing child shows exact contact.
- **D1:** two root lanes appear. A brief non-blocking callout says `A piece from either blank may become a tool for the other.` No arrows tell which one. Cross-root trace becomes available once first cut is committed.

Demo completion replay shows the causal chain of the completed solution as a celebratory summary **after** certification. It may reveal the player's actual winning sequence because the puzzle is already solved.

---

# 10. Certifier, failure, dead-state and restart

## 10.1 Certification success
Player invokes Certify. Camera shifts minimally to Assembly Pad, each final requirement is physically tested in 2–5 second sequence, then result locks as solved.

Success presentation order:
1. part presence/contact;
2. guided witness effects;
3. any pair/ancestry physical interface;
4. final mechanical fit/reveal.

A short lineage recap may highlight the actual solved byproduct→jig→product chain.

## 10.2 Certification soft failure
Failure never ejects to menu. The test stops on the first local unmet predicate and:
- outlines the failing part/station;
- shows requirement icon + plain text;
- offers `Inspect cause`, `Return to bench`, `Restart`.

If still recoverable, it must not say `failed attempt` or imply restart is required.

## 10.3 Optimistic dead-state warning
After a commit, if Phase-4 optimistic analysis proves a mandatory requirement unreachable, show:
- compact bench banner: **Lineage broken**;
- the impossible requirement card pulses using outline/pattern + icon, not color alone;
- optional `Inspect cause` opens backward Trace View;
- `Restart now` is one direct action;
- `Keep inspecting` is allowed so the player can understand the mistake.

The detector may be incomplete. Therefore absence of warning never means the state is solvable.

## 10.4 Restart
Restart must require no menu trip:
- dedicated remappable action or persistent HUD button;
- one confirmation only when the current attempt contains >=1 fabrication commit;
- default confirmation can be quick `Hold Restart 0.35 s` rather than a modal;
- reset transition target <1 s perceived, skipping scene reload presentation.

Settings/help state, accessibility and tutorial completion persist. Attempt-local workpiece state does not.

---

# 11. Pause, settings, persistence boundaries

## 11.1 Pause menu
Pause contains:
- Resume
- Restart Job
- Settings
- Controls
- Help / capability legend
- Return to Case Select
- Quit

No critical puzzle information exists only behind pause.

## 11.2 Settings
Required groups:
- Controls/remapping + glyph override;
- camera sensitivity, invert axes, auto-frame, motion reduction;
- text/UI scale;
- overlay density;
- hold/double-press irreversible confirmation mode and hold duration within safe bounds;
- vibration strength/off;
- master/music/effects/interface volumes;
- high-contrast capability overlay;
- optional pattern reinforcement always on/off (default on for essential capability distinctions).

## 11.3 Save/load boundary
Phase 6 player-facing contract:
- campaign progress, solved cases, tutorials seen, settings and accessibility persist;
- current in-progress attempt may autosave only at **stable atomic states between commits/animations**;
- loading resumes the exact stable bench state, focus may safely reset to Overview;
- no save can capture half a cut or half a guided operation;
- restarting a job discards the attempt state but not solved/tutorial/settings state.

Detailed persistence schema belongs to Phase 8.

## 11.4 Between attempts
Persist:
- solved/available case state;
- tutorial/help discoveries;
- settings/accessibility/remaps;
- optional player-created non-scoring notes/bookmarks only if Phase 7/8 chooses to include them.

Do not persist temporary cut previews, hover/focus state, open Trace View, or a hidden hint penalty.

---

# 12. Accessibility baseline

## 12.1 Input
- full controller-only completion;
- complete remapping for semantic actions;
- simultaneous mouse/controller support;
- no hold action is mandatory without an alternate double-press/single-confirm mode;
- no rapid presses, precision timing, stick-click dependency or motion control requirement.

## 12.2 Text and UI
- 1280×800 handheld layout is a first-class target;
- dense secondary text target >=12 rendered pixel character height at 1280×800; normal labels/cards larger;
- scalable UI/text presets: 100%, 125%, 150%; layout must reflow rather than clip;
- high-contrast backing/outline for text over workbench surfaces;
- concise plain language; no mandatory woodworking jargon.

## 12.3 Color and vision
- every capability/witness/state distinction has symbol + shape/pattern; color never stands alone;
- high-contrast overlay option;
- focused object uses outline/scale/pattern, not hue only;
- small cut sockets enlarge their focus target without changing logical geometry.

## 12.4 Motion
- reduce-motion option removes decorative camera sweeps, strong split recoil, pulsing zoom and shake;
- animations may be accelerated/skipped after the first explanation;
- no flashing/flicker communicates correctness.

## 12.5 Audio/hearing
No rule depends on sound. All important sounds have visible/tactile equivalents. Separate volume controls for music, SFX and interface.

If there is any voiced tutorial flavor later, all speech is subtitled; baseline design does not require voice.

## 12.6 Cognitive support
- inspectable capability legend at any time;
- prompts at player-controlled pace;
- no timer/lives;
- retry friction near zero;
- requirement cards use stable terminology across all 24 cases;
- Trace View externalizes ancestry so players do not need to memorize six commits.

---

# 13. Audio / visual / tactile feedback language

All feedback uses a consistent event grammar.

## 13.1 Cut preview
Visual: parent remains solid, two child ghosts separate; cut scar line pulses once.
Audio: soft dry scrape/measure sound.
Tactile: none or very light focus tick.

## 13.2 Cut commit
Visual: short guided blade motion, clean split, child settle, new lineage scars appear.
Audio: strong but brief cut + two-piece separation sounds.
Tactile: single medium pulse at split.

## 13.3 Dock / compatible fit
Visual: keyed target silhouette closes around contact surfaces.
Audio: soft wood/fixture click.
Tactile: small click pulse.

## 13.4 Fit rejection
Visual: piece stops before seat; missing contact requirement flashes as pattern/outline once.
Audio: muted knock, not error buzzer.
Tactile: two tiny pulses optional.

## 13.5 Guided operation
Visual: jig and target contact points illuminate; result witness appears physically.
Audio: operation-specific short drill/mark/press cue.
Tactile: low continuous tick for hold then completion pulse, if enabled.

## 13.6 Witness creation
Visual: new hole/mark/spacing/angle feature persists on object; icon rises then settles into Inspect card.
Audio: concise confirmation accent.

## 13.7 Consume / release
Release: fixture opens and piece visibly returns to loose/available lane or remains pickable; upward/open icon.
Consume: piece physically leaves play through a clear irreversible mechanism and historical silhouette remains in root lane; broken-outline icon.

## 13.8 Certification
Success is a physical test/reveal, not a giant score screen. Failure freezes exactly at the violated requirement and returns control quickly.

---

# 14. Four mandatory UX walkthroughs

## 14.1 OW01 — Keep the Spacer
**Initial:** one stock in Stock Bay; Plan Rail shows final rail + one spacing/drill operation. One obvious jig cradle exists.

Player controller path:
1. focus Stock Bay → Select stock;
2. down to cut sockets; Preview first socket;
3. children ghost apart; station compatibility markers show which child can seat as spacer;
4. Cancel, preview second socket; compare;
5. Hold Commit on desired cut;
6. focus defaults to byproduct; shoulder Cycle Compatible Targets jumps directly to spacer cradle;
7. dock; perform guided operation with irreversible confirmation;
8. dock rail as part; Certify.

Repair found: without post-cut focus targeting the byproduct, first-time controller flow would require zone cycling immediately after the thesis moment. Frozen fix: after every cut, focus defaults to the child with the strongest currently-visible relation to the focused plan/station; if tied, first child spatially nearest. This is navigation assistance only and never says which child is strategically correct.

## 14.2 OW11 — Wrong Side First
Two stocks, up to five commits, future dependency distance three.

The player can select a future operation card in Plan Rail and Cycle Related Pieces. Trace before any commit shows only **current physical compatibility**, not future producers. Cut previews show exact child properties. After a product-first bad cut, optimistic dead-state may prove future angle/spacer impossible; Lineage Broken highlights the later requirement and the spent parent branch.

Repair found: `physically satisfiable now` could look like endorsement and encourage product-first greed. Frozen fix: neutral open-circle status and wording `Fits now`, never green check or `Ready` until the operation itself is executed/completed.

## 14.3 OW20 — Split Decision
Three stocks, six commits, dual-use scarcity and two valid allocation families.

A scarce child fits two stations. Selecting it shows both targets equally; no target is ranked. Temporary vs consuming station status is visible directly on station rim and Inspect text. If player parks the piece temporarily, its root-lane placeholder remains and the other station shows `Piece currently in [station]` when inspected.

Certification accepts either valid family; solved recap reproduces the player's actual path.

Repair found: direct `Cycle Compatible Targets` could accidentally order consuming station first and bias one family. Frozen fix: compatible target cycle is stable spatial/plan order, never solver-derived or based on eventual success probability.

## 14.4 OW24 — Witness Relay
Three root lanes, six commits, two cross-piece witness dependencies.

Workbench readability sequence:
1. Plan Rail shows final beam/brace requirements and known guided-operation stations.
2. Root badges/patterns separate A/B/C without color dependence.
3. Player inspects a station requiring a marked/holed template; current satisfying pieces may be none.
4. Requirement Trace shows no future recipe; it only explains the needed visible witness and current physical candidates.
5. After first/second commits, historical parent silhouettes remain in root lanes.
6. When a child receives `MARK`, the physical mark persists; later docking requirement visibly matches it.
7. At six commits, selecting the final unmet requirement collapses bench to the relevant <=6-event causal path; unrelated pieces dim, not disappear.
8. If lineage is live but wrong due to competition, no false dead-state warning is allowed; the player may Certify, inspect local failure and restart.

Repair found: a full always-on ancestry tree would cover the Deck screen and leak too much branch importance. Frozen fix: lineage is root-lane grouping + physical scars by default; detailed causal connectors exist only in hold-to-inspect Trace View.

**OW24 controller completion gate:** every operation, requirement, loose child, cut socket, jig and part slot must be reachable through semantic focus in <=6 directional/cycle inputs from the current relevant selection; no analog-cursor precision is required.

---

# 15. Presentation style ceiling

## Visual direction
Stylized miniature workshop / crafted diorama. Materials can evoke wood/composite/metal fixtures, but correctness uses authored discrete geometry rather than realistic physics. Edges, sockets, notches and witness marks are intentionally exaggerated for readability.

Avoid:
- photoreal saw simulation;
- messy background props that resemble interactive stock;
- tiny engraved dimensions as primary information;
- workshop management scenery/UI;
- long character animations between puzzle actions.

## Audio direction
Quiet tactile workshop palette: clicks, cuts, clamps, drill/mark accents, restrained music. No audio-only puzzle information.

## Tactile direction
Controller vibration is short semantic punctuation, independently adjustable/off. Never use vibration to carry capability distinctions.

---

# 16. Phase-6 acceptance criteria
Phase 6 is complete only if the specification satisfies all of the following:
1. mouse and controller/Deck can complete every canonical verb;
2. controller navigation uses a deterministic semantic focus graph, not mandatory cursor emulation;
3. <=8 loose children remain visible/selectable without overlap hunting;
4. every capability/witness has physical + symbol + optional text encoding and never relies on color alone;
5. every destructive commit is visibly distinct from reversible docking and protected from accidental activation;
6. cut preview exposes exact immediate children/capabilities but never judges strategic correctness;
7. lineage through six commits is inspectable on the bench without a separate genealogy screen;
8. certifier/dead-state diagnostics explain current causality without revealing future winning moves;
9. restart is immediate and does not require returning to menu;
10. onboarding uses <=4 blocking prompts and the demo path ends with a cross-blank dependency;
11. 1280×800/Deck readability and scalable text are explicit requirements;
12. OW01, OW11, OW20 and OW24 have complete controller-safe walkthroughs with ambiguities repaired.

All twelve gates are satisfied by this document at design level.

---

# 17. Empirical UX gates carried forward
These require implementation/playtest rather than more paper design:
1. socket selection feels like touching/cutting the piece rather than choosing a menu row;
2. cold controller player reaches the intended cut socket/station without cursor hunting;
3. six-commit Trace View is understandable in <10 seconds after prior tutorialization;
4. players distinguish `Fits now` from strategic endorsement;
5. irreversible hold/double-press confirmation prevents accidental commits without feeling repetitive;
6. capability icons remain readable at Steam Deck scale with color removed;
7. cold demo player can explain the D1 causal chain in ordinary language.

Failure of an empirical gate should first repair presentation/navigation, not add mechanics.

## Phase-6 lock statement
**PHASE 6 UX / PRESENTATION ARCHITECTURE COMPLETE.** ONE-WAY WORKSHOP now has a complete player-facing workbench, camera, mouse/controller/Deck navigation, capability language, commit safety model, lineage/trace presentation, onboarding, certifier/restart UX, persistence boundary, accessibility baseline and feedback grammar. No Phase-4/5 mechanic was added or reopened.

NEXT: Phase 7 Economy / Retention / Commercial Model — fresh-market-check price/value positioning; exact campaign unlock structure; demo/full progression import boundary; hint philosophy and limits; achievements; replay/optional challenge model if any; Steam platform feature assumptions; monetization exclusions; commercial acceptance gates. Do not inflate content or add meta-economy merely to manufacture retention.