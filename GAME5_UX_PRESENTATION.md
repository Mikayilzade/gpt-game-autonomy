# GAME #005 — UX / PRESENTATION ARCHITECTURE

Last updated: 2026-08-23
Factory run: **9 — extended pass**
Phase: **6 — UX / Presentation Architecture**
Selected concept: **G5C02 — Tension Budget**
Commercial title: **TBD**
Production implementation: **NOT STARTED**

# PHASE 6 STATUS = COMPLETE

This file freezes how the already-defined mechanics are controlled, read, learned, explained and recovered from. Presentation must make deterministic redistribution legible without turning the game into a numeric engineering interface.

---

# 1. UX north star

The player should be able to understand the important mechanical truth by looking at the world:

> **I moved the carriage here; this cable gave, that one took, these mechanisms changed, and now this route exists while that one does not.**

HUD and text may reinforce that truth. They may not become the primary place where the truth lives.

---

# 2. Camera and framing

## 2.1 Baseline camera
- elevated top-down / isometric-style perspective;
- stable readable gameplay framing rather than cinematic free camera;
- soft authored camera zones may pan/zoom to keep the carriage plus affected loads legible;
- player remains visible during ordinary traversal;
- camera never requires manual precision rotation to solve a puzzle.

## 2.2 Causal framing rule
When the player grabs a carriage, framing should prioritize:
1. carriage;
2. connected cable runs;
3. the 2–4 affected loads where practical;
4. player's immediate route context.

If all loads cannot fit at once, world-space causal highlighting and short guided camera emphasis may reveal off-screen consequences without removing player control for long periods.

## 2.3 No information hiding by camera
An encounter may not be made difficult because a relevant load is intentionally impossible to inspect. The player can always regain a readable view before committing.

---

# 3. Input architecture

## 3.1 Core controls
### Keyboard/mouse
- Move: WASD / remappable equivalent.
- Interact/Grab: one primary action.
- Release/Commit: release same action or explicit confirm depending implementation feel; only one consistent model ships.
- Restart from checkpoint: dedicated remappable action / pause-menu command.
- Pause/Menu: standard.

### Controller
- Move: left stick / D-pad where practical.
- Interact/Grab: face/shoulder button.
- Carriage slide while grabbed: left stick projected to rail axis, with strong snap attraction.
- Restart: remappable/menu-safe command.

No cursor precision is required.

## 3.2 Interaction priority
- nearest valid carriage/objective in the player's interaction cone is highlighted;
- carriage dominates ordinary nearby decorative interactables;
- no generic physics-pickup system exists, avoiding ambiguous grabs.

## 3.3 Grab state
On successful grab:
- locomotion becomes locally constrained to the interaction stance if needed for clarity;
- carriage receives strong focus state;
- connected rig receives one consistent world-space emphasis;
- snap bands become visible/tactile;
- the player can cancel back to committed state before release if implementation testing supports this cleanly.

Cancel behavior must never create a new mechanical state.

---

# 4. Carriage presentation

## 4.1 Physical object
The carriage must read as a large hand-operated machine element, not a UI slider pasted into the world.

Required characteristics:
- visible handle/grip;
- short rail;
- 3–5 mechanically authored detents/snap bands;
- large travel language so movement is readable from gameplay camera;
- connected cable hardware visibly responding during preview.

## 4.2 Snap-band communication
Snap bands use redundant cues:
- physical notches/detents;
- carriage alignment marks;
- brief world-space emphasis when crossed;
- controller haptic tick where supported;
- subtle sound tick where enabled.

None of these replace the visible load consequence.

## 4.3 Preview versus commit
During GRABBED_PREVIEW:
- destination postures may ghost/animate toward preview states;
- current authoritative traversal state remains visually distinguishable;
- a consistent preview treatment prevents the player from mistaking in-between poses for legal traversal states.

Recommended presentation distinction:
- committed mechanisms: fully solid normal rendering;
- preview destination: restrained outline/ghost posture or mechanical indicator movement;
- no neon graph overlays connecting every node.

---

# 5. SLACK / TAUT / HIGH visual language

The three states are world grammar, not merely labels.

## SLACK
At minimum:
- obvious cable sag;
- relaxed/low tensioner posture;
- load in its SLACK stable pose;
- optional icon language: curved loose-line motif.

## TAUT
At minimum:
- cable straight under ordinary working pull;
- mechanical tab/collar in centered position;
- load in TAUT pose;
- optional icon: straight line with centered marker.

## HIGH
At minimum:
- cable straight but visibly strained through hardware posture, not dangerous breakage;
- tensioner/collar at clear extreme;
- load in HIGH pose;
- optional icon: straight line with extreme marker / doubled brace.

### Critical accessibility rule
A player must distinguish states without relying on:
- hue alone;
- sound alone;
- controller vibration;
- tiny text;
- numeric values.

Optional labels `SLACK`, `TAUT`, `HIGH` may be enabled as accessibility reinforcement.

---

# 6. Load-specific presentation

## 6.1 Lift
- three stable docks have unmistakable authored landing heights;
- travel path and target dock are visible;
- valid landing alignment uses strong geometry/silhouette rather than tiny indicator lights;
- deck remains visibly safe/solid.

## 6.2 Counterweighted Gate
- clearance tiers use major physical positions;
- passage requirement is readable by player/body scale;
- partial motion cannot suggest a timing squeeze is intended;
- if a tier is unusable, geometry clearly blocks ordinary passage.

## 6.3 Flexible Span
- SLACK = visibly deep sag;
- TAUT = walkable level/comfortable slope;
- HIGH = visibly over-lifted / too steep, with route entrance geometry clearly refusing normal traversal;
- TAUT should become one of the game's strongest visual teaching motifs that “middle can be right.”

---

# 7. Causal feedback sequence

Every committed change should communicate causality in the same perceptual order:

**carriage snap → cable give/take → load response → traversal consequence**

Recommended timing philosophy:
- fast enough that ordinary play never feels like waiting;
- slow enough that two or more simultaneous consequences can be followed;
- affected cables receive a short directional pulse/physical travel cue;
- loads begin motion in a slight readable cascade if needed, but authoritative result is deterministic and not timing-sensitive.

For off-screen affected loads:
- edge-of-screen indicator may briefly identify direction;
- optional short camera nudge/peek may show major change;
- after first teaching, player should increasingly rely on the physical cable network and known world layout rather than repeated forced cameras.

---

# 8. HUD

## 8.1 Baseline HUD — minimal
Normal play should require little persistent HUD.

Allowed baseline elements:
- small current objective prompt when needed;
- contextual interact prompt;
- restart/checkpoint prompt in pause/help;
- optional accessibility labels for currently focused cable/load states.

Not allowed as default mechanical authority:
- numeric tension bars;
- percentage allocation;
- detached node graph;
- minimap showing hidden rig logic;
- inventory/toolbelt;
- score/combo/timer pressure.

## 8.2 Focus inspection aid
Optional hold/toggle `Rig Focus` may:
- emphasize the currently relevant carriage/cables/loads;
- label load archetype and SLACK/TAUT/HIGH state if accessibility labels are enabled;
- highlight currently open/closed traversal edges in world-space.

It may not:
- solve the puzzle by ranking bands;
- expose internal quanta/B values;
- show future solution sequences.

---

# 9. Onboarding architecture

Onboarding must teach by interaction, not engineering exposition.

## E01 teaching sequence
1. Player walks to one obvious carriage.
2. Interaction prompt shows grab.
3. Moving carriage visibly moves one Lift through stable docks.
4. No fail state; player learns direct cause/effect.

## E02
- second load appears on same rig;
- one carriage move helps Lift while Gate changes oppositely;
- no text saying “conservation law” is required.

## E03
- Flexible Span introduced;
- HIGH visibly over-lifts it;
- TAUT creates usable bridge;
- this is the explicit conceptual proof that extremes are not automatically correct.

### First rule-explanation text, if needed
At most a short plain-language line such as:
**“One rig shares one pull. Give more here, and something else gives.”**

No formulas or engineering tutorial panel.

---

# 10. First-session flow

Target first 20–30 minutes:
1. title/start with minimal menu friction;
2. immediate movement in-world;
3. first carriage interaction within roughly 60–90 seconds;
4. visible two-load tradeoff within first 5–8 minutes;
5. TAUT middle-state reasoning soon after;
6. first traversal-separated reconfiguration before session feels like a row of switches;
7. first mutation/return-inversion either late in first session or by demo climax.

The game should reveal its true differentiator early enough that a Steam demo/store clip is honest.

---

# 11. Objective presentation

Objectives are simple physical actions: latch, coupling, inspection point, counterweight release, clutch engagement, etc.

Rules:
- objective location is world-readable;
- objective does not introduce a minigame;
- the resulting load add/remove mutation is physically shown;
- mutation causal chain is not skipped by a fade/cutscene;
- after mutation, camera/feedback gives enough context to see that the same rig has changed meaning.

---

# 12. Restart, checkpoint and recovery UX

## 12.1 Checkpoints
- C0 at encounter entry.
- C1 immediately after a valid completion-relevant mutation once rig stabilizes.

Restart should be fast and deterministic.

## 12.2 Restart behavior
- no lives;
- no currency/score penalty;
- no long reload;
- restores exact canonical authoritative state;
- optional confirmation only if accidental restart testing shows it is needed.

## 12.3 Failure philosophy
Most wrong decisions should create an obviously unhelpful but recoverable state, not death.

A hard failure/softlock should be rare because validators reject it. If player becomes stranded in a state from which no legal carriage route is reachable, offer immediate checkpoint restart and record the layout as QA-critical.

## 12.4 Explainable failure
When a chosen configuration blocks progress, the world itself should show why:
- gate closed;
- span sagged/over-lifted;
- lift at wrong dock;
- player on wrong side of a commitment.

Avoid generic “incorrect” banners.

---

# 13. Pause and settings

Required baseline settings architecture:
- master/music/SFX volume;
- subtitle/caption controls for any narrative/audio cues;
- input remapping;
- controller vibration toggle/intensity where supported;
- camera shake toggle/intensity;
- reduced-motion mode;
- UI/text scale;
- color/accessibility options;
- optional explicit SLACK/TAUT/HIGH labels;
- window/display/performance settings appropriate to PC.

Pause freezes gameplay state. No rig simulation continues while paused.

---

# 14. Accessibility contracts

## 14.1 Low dexterity burden
- generous carriage interaction radius;
- snap attraction removes precision;
- ordinary traversal speeds;
- no reaction-time gates;
- no jump/catch timing.

## 14.2 Reduced motion
Reduced-motion mode may:
- shorten load transitions;
- reduce camera pans/shake;
- reduce cable oscillation flourish;
- replace some continuous animation with clearer snap-to-stable transitions after causal cue.

It may not change solution logic.

## 14.3 Color-independent readability
State grammar must survive grayscale/major color-vision deficiencies through cable curvature, hardware position, silhouette and labels where enabled.

## 14.4 Audio independence
Every completion-relevant fact is visually available. Audio/haptics reinforce cause and snap feel only.

## 14.5 Cognitive clarity
Optional assistance may label focused loads and current state words, but should not reveal recommended next band. A future hint system, if added, must provide graduated observational nudges rather than direct solution sequences; hints are not required for initial freeze.

---

# 15. Presentation style

Preferred art direction:
- stylized exposed civic/industrial suspended infrastructure;
- large readable mechanisms;
- modest material palette and strong silhouettes;
- low visual clutter around active rigs;
- cables are composition lines that help the player understand relationships.

Avoid:
- photorealistic dense factory clutter;
- dozens of decorative cables indistinguishable from gameplay cables;
- tiny realistic hardware requiring close zoom;
- glowing sci-fi graph language that makes the rig feel virtual rather than physical.

Gameplay cables and decorative cables must be immediately distinguishable, ideally by routing grammar/attachment hardware, not only color.

---

# 16. Commercial screenshot / trailer readability requirements

A strong representative screenshot should show:
- player near carriage;
- at least two connected loads visible or compositionally implied;
- obvious exposed cable relationships;
- one route created and another compromised.

A strong 8–10 second mute clip should show:
1. carriage pulled;
2. two or three cables respond;
3. Lift/Gate/Span change together;
4. player immediately moves through the resulting route.

No trailer clip should need a numeric overlay to explain the hook.

---

# 17. UX validation gates

## U01 — State recognition
Unfamiliar players distinguish SLACK/TAUT/HIGH at normal gameplay camera after onboarding without numbers.

## U02 — Causal attribution
After one carriage move, players can identify at least two resulting load changes and attribute them to the same rig action.

## U03 — Interaction speed
Once in range, normal intentional carriage move targets roughly <=2–3 seconds from grab to committed snap.

## U04 — No false timing affordance
Players do not repeatedly attempt to run through moving Gates or use transient Span/Lift poses as intended solutions.

## U05 — Preview distinction
Players understand preview is prospective and that traversal state commits only on release/snap.

## U06 — Off-screen consequence comprehension
When not all loads fit in one frame, players can still discover/understand the result without opening a detached diagram.

## U07 — Controller parity
Every main encounter is fully solvable on controller without cursor precision.

## U08 — Muted parity
A muted playtest retains all completion-critical information.

## U09 — Reduced-motion parity
Reduced-motion mode yields identical logical solutions and traversal permissions.

## U10 — Restart trust
Players use restart freely without fear of losing campaign progress or replaying pre-mutation sections unnecessarily.

---

# 18. Explicit UX cuts

Not part of the baseline product:
- diegetic numeric gauges required for solution;
- graph/minimap puzzle screen;
- radial tool inventory;
- precision analog rope aiming;
- manual camera rotation as a requirement;
- QTEs;
- timed escape sequences as puzzle authority;
- health/lives/combat HUD;
- resource counters;
- score stars tied to move limits in the main campaign.

---

# 19. Phase 6 acceptance checklist

- [x] Camera/framing contract defined.
- [x] Keyboard/mouse and controller interaction model defined.
- [x] Carriage/snap/preview presentation defined.
- [x] SLACK/TAUT/HIGH world grammar defined redundantly.
- [x] Load-specific presentation rules defined.
- [x] Causal feedback ordering defined.
- [x] HUD remains minimal and nonnumeric.
- [x] Onboarding and first-session flow defined.
- [x] Objective mutation presentation defined.
- [x] Restart/checkpoint/failure explanation defined.
- [x] Settings and accessibility baseline defined.
- [x] Trailer/screenshot readability requirements defined.
- [x] UX empirical gates defined.
- [x] No new gameplay pillar introduced.
- [x] Production implementation remains outside factory.

# PHASE 6 DECISION

**PHASE 6 UX / PRESENTATION ARCHITECTURE = COMPLETE.**

The product can now move to Phase 7 Economy / Retention / Commercial Model. Phase 7 must preserve the compact premium thesis and should not invent progression currencies, live-service systems or padding to justify price.

## NEXT ACTION — PHASE 7 ECONOMY / RETENTION / COMMERCIAL MODEL
Research current comparable premium puzzle positioning where useful, then freeze pricing strategy/range, demo/release funnel, progression/unlock model, achievements, replay incentives, optional content boundaries and monetization cuts without changing the core campaign.