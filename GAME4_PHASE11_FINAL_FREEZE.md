# GAME #004 — PHASE 11 FINAL SPECIFICATION FREEZE

Last updated: 2026-08-21
Factory run: **15**
Phase: **11 — Specification Freeze**
Selected concept: **G4C19 physical acoustic-routing infiltration**
Replacement commercial working title: **HEARWALL**
Production implementation: **NOT STARTED**

# DESIGN COMPLETE = YES

This file is the **highest Game #004 design authority**. It integrates the Phase-10 adversarial repairs and resolves all implementation-sensitive ambiguity required to let a fresh implementation session build the game without inventing important gameplay.

`HEARWALL` is a replacement **working commercial title**, selected after basic 2026-08-21 collision screening found no obvious active game/app/service exact-title collision in targeted searches. This is not legal trademark clearance and may be replaced later for legal/branding reasons without changing gameplay canon.

Historical names `Soundproof Smuggler` and `HUSHLINE` are retired from commercial use. They may appear only in historical design files.

---

# 1. Frozen product identity

## 1.1 One-sentence hook
**Move one physical soundproof barrier through a facility so the right listener hears your footsteps, distractions and break-ins while the wrong listener does not — then exploit the reaction to infiltrate.**

## 1.2 Genre / product shape
- Top-down real-time acoustic infiltration puzzle.
- PC / Steam first.
- Single-player.
- Offline-complete baseline.
- Keyboard/mouse and controller first-class.
- Steam Deck / handheld readability is a validation target.
- Premium one-time purchase.
- No progression currency, live-service loop, battle pass, ads, paid power or grind economy.

## 1.3 Core fantasy
The player treats audibility as manipulable physical space. They move through compact facilities, locally reach and reposition one visible acoustic barrier, preview exactly how a near-term sound will propagate, intentionally decide who should hear it, and use the resulting deterministic listener reaction to create traversal or objective windows.

The game is **not** about perfect silence. Useful hearing is mandatory campaign language.

## 1.4 Core loop
1. Read physical space, sources, listeners, doors and visible acoustic passages.
2. Move through the facility.
3. Reach the barrier locally and reposition/rotate it along authored rail slots.
4. Preview the exact consequence of the next relevant sound-producing action.
5. Commit a movement, distraction or loud objective action.
6. Observe the same acoustic result that preview promised.
7. Exploit deterministic listener investigation/return state.
8. Reposition again as source, listener, door or extraction state changes.
9. Complete objective and extract.

---

# 2. Frozen scope ceiling

## 2.1 Campaign
- **34 main encounters: E01–E34.**
- **8 optional remix/mastery encounters: R01–R08 target.**
- Optional remixes are the first content cut if repetition evidence is poor.
- Do not expand above 34 main encounters merely to pad value or justify price.
- First-clear target: roughly **5–8 hours**.
- Normal encounter first-clear target: roughly **6–12 minutes**.
- Natural session target: roughly **20–45 minutes**.

## 2.2 Main-campaign listener ceiling — FINAL
**Maximum two listeners in every main-campaign encounter.**

This supersedes all older Phase-3–9 text describing three-listener E28/E33 or a three-listener main-campaign exception.

Phase-11 decision: **three-listener gameplay is CUT from the 1.0 design entirely**, including optional remixes. It is not an implementation gate and is not a promised experiment. A future post-1.0 design amendment may revisit it only after shipped evidence, but implementation 12A–12H must not build for it as a required feature.

Reason: two listeners fully express selective audibility while preserving handheld/no-audio/world-space readability and reducing route-density complexity.

## 2.3 Density caps
- Normal mature acoustic nodes: **<=12**.
- Main-campaign listeners: **<=2**.
- Meaningful barrier slots in mature content: normally **3–5**.
- Simultaneously decision-relevant acoustic routes on screen: target **<=3–4**.
- One active movable barrier baseline and 1.0 ceiling.
- Sound strengths: **1–4**.
- Base attenuation classes: **0–2**.
- Listener thresholds: **1–3**.
- Barrier attenuation addition: **+3**.

## 2.4 Explicit out-of-scope 1.0
- ray-traced/wave acoustics;
- microphone input;
- audio-only mechanics;
- combat/takedown/weapon pillar;
- suspicion-meter stealth pillar;
- crouch/stamina economy as required systems;
- freeform barrier placement;
- remote/modal whole-building graph editing;
- multiple independently controlled barriers;
- three-listener gameplay;
- large stealth crowds;
- open world;
- procedural endless generation requirement;
- multiplayer/co-op;
- crafting/inventory economy;
- cargo/smuggling economy;
- dialogue-heavy branching narrative;
- arbitrary destructible architecture;
- hidden randomized hearing.

---

# 3. Frozen deterministic acoustic model

## 3.1 Graph
Every encounter has a physical layout plus an acoustic graph embedded in that same world.

Each acoustic node maps to a visible physical region. Each enabled acoustic edge maps to a visible physical passage/opening. There are no hidden acoustic edges.

Every edge has:
- stable ID;
- endpoints/direction;
- base attenuation 0–2;
- optional door binding;
- optional barrier-slot binding;
- enabled state derived from visible world state.

## 3.2 Propagation
For sound event strength `S` from source node:

`I(node) = max(0, S - min_route_cost(node))`

where `min_route_cost` is the minimum total attenuation over currently enabled routes in the event's assigned immutable graph snapshot.

A listener hears iff:

`I(listener_node) >= listener_threshold`.

Barrier on a snapped slot contributes **+3 attenuation** to that edge.

Strength-4 sound may therefore leak through a barrier at intensity 1 if no cheaper alternate route exists. The barrier is strong attenuation, not a magical binary mute wall.

## 3.3 Tied minimum routes
If several routes tie for minimum attenuation:
- all tied minimum routes are mechanically real;
- all are shown with equal outcome emphasis;
- blocking one tied route cannot imply silence if another tied route remains;
- stable ID ordering is presentation/debug ordering only and never changes hearing truth.

## 3.4 No hidden probability
There is no random hearing roll, hidden alertness multiplier, hidden acoustic material modifier or `maybe heard` state in baseline gameplay.

---

# 4. Frozen sound/source vocabulary

Exactly four source families are canonical:
1. **LOCOMOTION** — player footstep/movement events.
2. **DISTRACTION** — deliberate world source triggered by player.
3. **OBJECTIVE** — loud interaction required or strategically meaningful.
4. **MOVING_ENV** — exceptional visible deterministic moving environmental source.

Source instances use fixed strength bands 1–4. Strength is a property of the physical action/object, never a player-selected power slider.

No pitch/frequency puzzle family, microphone classification or audio-only source property exists.

---

# 5. Frozen player movement/noise model

Canonical movement states:
- IDLE;
- WALK;
- FAST_MOVE;
- INTERACTING;
- BARRIER_MANIPULATION;
- FAILED/LOCKED.

Baseline locomotion:
- IDLE: no locomotion sound;
- WALK: strength-1 pulses at deterministic cadence;
- FAST_MOVE: strength-2 pulses at a shorter deterministic cadence;
- barrier manipulation is mechanically silent;
- objective/distraction interactions emit their authored events.

Exact cadence and movement feel are implementation balance knobs, but must be deterministic, preview-compatible and shared by replay/save state.

---

# 6. Frozen barrier contract

## 6.1 Ownership
There is one visible physical barrier per encounter baseline. It moves on an authored rail/track through authored snap slots. A slot maps to exactly one acoustic edge.

The player must be locally within the handle/reach volume to begin manipulation. The world does not pause.

## 6.2 States
RESTING / GRABBED / MOVING / SNAPPING / RELEASED.

## 6.3 Acoustic activation
- Only a fully snapped slot applies +3 attenuation.
- Between slots, the barrier applies **no acoustic attenuation**.
- Leaving the old snap envelope reopens the old edge before the new slot activates.
- On canonical snap, the new slot atomically receives +3.

## 6.4 Release
If released between slots, the barrier returns deterministically to the nearest legal slot; exact midpoint ties return to the last occupied slot. It remains acoustically inactive until re-snapped.

## 6.5 Cost
No mana, cooldown, decay, durability or artificial edit budget is added to force movement. Cost comes from physical travel/exposure and from changing acoustic consequences.

## 6.6 Tactility empirical threshold
Implementation should target a median grab-to-meaningful-snap interaction below roughly **2–3 seconds once in reach**. This is a feel gate, not a simulation rule.

---

# 7. Frozen doors and mutation/event snapshot semantics

Baseline door states: OPEN / CLOSED.
- OPEN: traversal and acoustic edge enabled with authored base attenuation.
- CLOSED: traversal and acoustic edge disabled.

No leaking closed-door archetype is part of the 1.0 frozen grammar.

Every action that both mutates graph state and emits sound has explicit `emission_phase`:
- `BEFORE_MUTATION`, or
- `AFTER_MUTATION`.

## 7.1 BEFORE_MUTATION — FINAL ownership rule
At the canonical mutation point, immediately **before** the relevant barrier/door/object graph mutation commits, capture/reference an immutable pre-mutation graph snapshot/revision. A `BEFORE_MUTATION` event is bound to that snapshot ID and resolves against it later in the tick even though the live world has already advanced to post-mutation state.

The implementation may use copy-on-write/persistent revisions/deltas, but may not reconstruct a BEFORE event later from current mutable state.

## 7.2 AFTER_MUTATION
An `AFTER_MUTATION` event references the immutable post-mutation graph revision after commit.

## 7.3 Prediction parity
Prediction and committed resolution for the same action must bind to the same semantic emission phase and equivalent graph revision.

---

# 8. Frozen listener model

Canonical states:
- POSTED;
- INVESTIGATE;
- ARRIVED/SEARCH;
- RETURN;
- ALERT_FAIL.

Listeners have persistent thresholds 1–3 and deterministic authored navigation.

## 8.1 Heard-event selection
If multiple events are heard on one resolution tick, select investigation target by:
1. highest remaining intensity at listener;
2. if tied, later canonical emission order within tick;
3. if tied, lower stable event ID.

## 8.2 Retargeting
A listener already INVESTIGATING or RETURNING may retarget before ARRIVED/SEARCH only when the newly heard event's received intensity is **strictly greater** than the intensity that caused the current investigation.

Equal-strength lure spam cannot indefinitely reset movement.

Once ARRIVED/SEARCH is reached, a newly valid heard event may establish a new target normally.

## 8.3 Search/return
Search is short, deterministic and bounded, baseline roughly 1–3 seconds. No random wandering.

## 8.4 Hearing is not failure
A listener hearing a sound is often beneficial. Failure comes from direct detection or an explicit obvious environmental fail, not from hearing by itself.

---

# 9. Direct detection — FINAL bounded scope

Direct detection is a **secondary deterministic pressure/failure layer**, not a second stealth mastery system.

Frozen rules:
- explicit visible detection profile;
- no random spotting;
- no hidden suspicion accumulation;
- no pixel-precision LOS threading required for main completion;
- no long cone-cycle memorization as intended puzzle language;
- no frame-perfect crossings;
- a short readable forgiveness hold may be authored;
- whole-simulation speed assists preserve ordering and may scale the real-time window coherently;
- no combat/takedown recovery branch.

Hearing and direct detection use visibly distinct presentation languages.

Empirical fail gate: if representative players fail primarily from vision-cone microtiming rather than acoustic/listener-state decisions, detection is too demanding and must be simplified.

---

# 10. Frozen fixed-step ordering

Authoritative simulation uses fixed domain ticks. Rendering/interpolation never changes rule truth.

Canonical per-tick order:
1. capture semantic input;
2. resolve player movement and acoustic-node ownership;
3. advance barrier manipulation movement excluding snap mutation;
4. advance physical interaction progress and collect pending mutations;
5. immediately before each relevant mutation commit, capture any required immutable BEFORE_MUTATION graph revision references;
6. commit barrier snap/release atomically;
7. commit door/object graph mutations in stable object-ID order;
8. establish post-mutation graph revision used by AFTER_MUTATION events;
9. advance moving environmental sources in stable source-ID order;
10. advance listener movement/state timers and update listener node ownership;
11. generate due sound events and attach their already-defined immutable graph revision IDs;
12. solve propagation for each event using its referenced graph revision;
13. resolve listener hearing/event selection in stable listener-ID order;
14. resolve direct-detection/fail conditions from authoritative post-movement positions;
15. resolve objective/win conditions if no fail occurred;
16. publish deterministic telemetry/presentation events;
17. increment tick.

No engine callback order may substitute for this sequence.

---

# 11. Exact prediction — FINAL contract

Prediction is not an approximation and not a separate solver.

For identical canonical state + candidate action:
- prediction applies the candidate to a prospective state at the same canonical ordering point;
- it invokes the same graph mutation, propagation and hearing functions;
- it binds to the same BEFORE/AFTER emission semantics;
- predicted `HEARS / DOES_NOT_HEAR` booleans must equal committed resolution **100%**.

Prediction exposes the consequence of a candidate action, not an automatic best action or complete future plan.

Forbidden UI/logic:
- global detached node-link acoustic editor;
- all-pairs matrix;
- automatic best-slot recommendation;
- ranked list of safe actions;
- intentionally fuzzy/lying preview.

---

# 12. Content architecture — FINAL

The twelve reasoning families remain canonical:
- F1 Single-route screening;
- F2 Alternate-route denial;
- F3 Selective audibility;
- F4 Deliberate investigation opening;
- F5 Over-propagation tradeoff;
- F6 Barrier travel exposure;
- F7 Door-state reroute;
- F8 Moving-source pressure;
- F9 Threshold split;
- F10 Sequence preservation;
- F11 Return-path inversion;
- F12 Multi-event ordering.

New mechanics/families are not added during implementation merely to create variety.

## 12.1 Campaign identity gates
- By E04, player deliberately creates an investigation opening.
- By E07, player must complete true selective audibility: one listener should hear, one should not.
- Main campaign must repeatedly require useful hearing thereafter.
- E11 is the first encounter where BEFORE/AFTER mutation ordering may be completion-critical.

## 12.2 Revised E28 — FINAL
**E28: two-listener tied-route threshold split.**
- <=10 nodes target;
- exactly two listeners;
- combines tied minimum routes + threshold split + selective audibility;
- no moving environmental source required;
- no completion-critical cyclic patrol timing;
- barrier must have at least three meaningful candidate slots over the solution;
- one static safest-slot solution is forbidden.

## 12.3 Revised E33 — FINAL
**E33: two-listener penultimate acoustic sequence.**
- 10–11 nodes target;
- exactly two listeners;
- combines tied routes + threshold split + sequence preservation;
- at least three completion-critical barrier placements over the encounter;
- no moving-source density spike;
- no three-listener substitute;
- no new mechanic.

## 12.4 E34 — FINAL
Two-listener final synthesis. Must include at least **two distinct moments where a listener should hear** a sound for the intended solution. Combines alternate routes, threshold split, door mutation, deliberate lure, required loud action, exposed barrier travel and extraction inversion while staying <=12 nodes.

---

# 13. Content validators — FINAL additions / repairs

All prior static and authored-solution validators remain unless superseded here.

## V17_SAFE_PREVIEW_ENUMERATION — FINAL
Applies to COMBINE / MATURE / CLIMAX content except explicit early teaching exceptions.

Warn/reject when all strategically relevant barrier slots can be exhaustively previewed from one permanently safe manipulation state and choosing the favorable preview directly resolves the completion-critical acoustic decision **without** meaningful traversal exposure, source choice, listener reaction, sequence dependency, door/source mutation or return-path change.

This validator does **not** hide information. It rejects weak content.

## V18_CONTENT_SIGNATURE_DEDUP — FINAL
Every COMBINE / MATURE / CLIMAX encounter must expose a comparable systemic signature containing at least:
- reasoning-family set;
- source-family combination;
- listener threshold pairing;
- meaningful barrier-slot count;
- door mutation yes/no and phase role;
- moving-source presence;
- extraction inversion yes/no;
- completion-critical barrier-edit sequence length;
- tied-route structure class.

Tooling compares neighboring and campaign-wide signatures. Mechanically near-duplicate encounters must be rewritten or cut even when geometry/art differs.

## Repetition policy
Blind playtests should encounter at least one materially new reasoning responsibility every roughly **2–4 main encounters** without needing a new mechanic.

---

# 14. UX / presentation freeze

## 14.1 World-first
The game must read as physical infiltration first and acoustic routing second.

Acoustic paths are drawn through actual doors/corridors, never on a detached graph screen.

## 14.2 Source strength
Strength 1–4 uses redundant count/shape/pulse motifs. Numbers are optional clarity, never required.

## 14.3 Attenuation
Attenuation 0–2 is visible through physical passage motifs and preview strength loss.

## 14.4 Listener threshold
Threshold 1–3 uses persistent shape/pattern motifs. Listener identity uses more than color.

## 14.5 Tied routes
All tied minimum routes show equal mechanical status. The UI never implies one arbitrary chosen shortest route.

## 14.6 Barrier
Barrier rail, handle, slots and physical seal are visible world objects. Snap is brief and tactile; no long animation blocks control.

## 14.7 Preview
Automatic local preview + hold-to-preview command + optional persistent preview are allowed. Preview never grants hidden future listener-state certainty beyond the current deterministic event/reaction.

## 14.8 Reduced motion
Reduced-motion mode may replace traveling pulses with persistent highlighted segments and discrete state transitions but must preserve route identity and ordering.

## 14.9 No-audio parity
**Every completion-critical decision must remain solvable with audio fully muted.** Audio is atmosphere/reinforcement only.

## 14.10 Handheld
No-audio + reduced-motion + large UI must remain viable at handheld scale for representative mature/final encounters.

---

# 15. Controls / accessibility freeze

Required first-class support:
- keyboard/mouse;
- controller;
- remappable semantic actions;
- UI/text scale;
- high-contrast acoustic motifs;
- reduced-motion acoustic presentation;
- persistent acoustic preview;
- optional explicit numeric acoustic bands;
- whole-simulation speed presets: **100% / 85% / 70% / 55%**.

Simulation-speed assists slow the relationship between wall clock and domain time. They do not alter per-tick acoustic logic, ordering, thresholds, attenuation or source strengths.

Main completion remains valid with assists.

---

# 16. Failure / restart / checkpoint freeze

Canonical fail families:
- direct listener detection/capture;
- explicit obvious lethal environmental hazard when justified;
- immediately legible irreversible objective failure.

Being heard alone is never generic failure.

Quick restart restores a canonical snapshot including player/listener/source states, barrier slot/state, doors, objective flags, timers, event counters and deterministic RNG state if any.

Baseline gameplay requires no RNG.

Normal encounter: usually 0–1 internal checkpoint. Checkpoints only at authored canonical safe states; never mid-barrier move or mid-sound event.

---

# 17. Technical implementation freeze

## 17.1 Engine
Initial implementation target: **Godot 4.7.1-stable**, pinned at bootstrap.

GDScript-first.

Upgrade only after deliberate compatibility testing.

## 17.2 Architecture
Four layers:
A. deterministic Domain Core;
B. runtime/world binding/orchestrator;
C. presentation;
D. platform adapters.

Gameplay truth never lives in rendering/audio/platform callback order.

## 17.3 Determinism
- 60 domain ticks per simulation second target;
- stable authored IDs;
- ordering-sensitive collections sorted deterministically;
- integer acoustic grammar;
- quantized/fixed-point authoritative motion preferred;
- engine free rigid-body outcomes not authoritative;
- deterministic authored navigation;
- semantic input packets with quantized analog axes.

## 17.4 Acoustic solver
Small graphs prioritize correctness and traceability. Stable Dijkstra/all-equivalent shortest-cost method is acceptable if it returns identical minimum attenuation and complete tied-minimum-route presentation data required by content.

## 17.5 Prediction
Same code path on prospective state. No UI-only approximation solver.

---

# 18. Persistence / replay / recovery freeze

Implementation must use explicit schema-versioned save DTOs and stable content IDs/hashes.

Required behaviors:
- local save is authoritative for offline gameplay continuity;
- temp write then atomic replace where supported;
- retained backup generation;
- explicit save migration, never silent incompatible reinterpretation;
- checkpoint fallback when primary current-run state is incompatible/corrupt;
- deterministic state hashing for replay/regression fixtures;
- demo import idempotent;
- demo campaign-completion import only when content identity/hash proves equivalence;
- platform/Cloud sync failures do not block already-valid offline installed play;
- achievement failure does not roll back local campaign completion.

Required automated fixtures before release candidate:
1. process interruption during save write;
2. corrupt primary / valid backup;
3. incompatible content hash;
4. older backup schema migration;
5. Cloud/local chronology conflict behavior;
6. repeated demo import;
7. checkpoint around BEFORE/AFTER mutation-sensitive content;
8. restart from between-slot barrier state;
9. achievement/platform callback failure.

---

# 19. Commercial / package freeze

## 19.1 Model
Buy the complete game once.

No ads, IAP power, currencies, battle pass, energy, paid retries/hints or content required to finish the base campaign.

## 19.2 Price
Final price remains empirical. Current valid test range: **$14.99–$19.99 USD**. `17.99` is a planning anchor only, not design truth.

Do not pad scope to justify price.

## 19.3 Demo
Target **4 curated encounters / ~18–24 minutes**:
- D01 Physical Screen;
- D02 The Other Way Around;
- D03 Make Them Move;
- D04 Selective Audibility.

Demo must end only after the player has successfully made one listener hear while another does not and exploited that reaction physically.

Demo achievements disabled. Settings/accessibility transfer preferred. Campaign progress transfers only when content identity is exact.

## 19.4 Achievements
Target roughly **18–24** full-game achievements without grind-count spam or assist shaming.

---

# 20. Title / capsule freeze

## 20.1 Replacement working title
**HEARWALL**

Basic collision screening performed 2026-08-21:
- targeted exact-name web/game/app/software searches did not surface an obvious active exact-title game/app/service conflict;
- an unrelated academic-search typo/term-like occurrence is not treated as a product collision.

This is **not trademark clearance**. Legal/store/domain checks remain pre-release business work. If the name later fails those checks, rename without altering gameplay.

## 20.2 Naming boundaries
Title/marketing must not imply:
- microphone input;
- horror-first game;
- rhythm/music game;
- cargo/smuggling logistics;
- audio-only accessibility product.

## 20.3 Capsule/trailer
Capsule should show one physical barrier splitting two visible sound routes/listener outcomes.

First trailer seconds should demonstrate:
**barrier moves → route flips → one listener reacts, one does not → player crosses.**

Do not lead with headphones, waveform-only art or generic crouching thief imagery.

---

# 21. Implementation-readiness audit

Fresh Phase-11 audit result: **PASS — 48/48**.

## Product / loop
1. player goal explicit — PASS;
2. repeated signature verb explicit — PASS;
3. traversal/signature-verb relationship explicit — PASS;
4. selective audibility mandatory — PASS;
5. session/demo structure explicit — PASS;
6. scope ceiling explicit — PASS.

## Acoustic mechanics
7. node/edge ownership explicit — PASS;
8. strength grammar explicit — PASS;
9. attenuation grammar explicit — PASS;
10. barrier +3 explicit — PASS;
11. threshold grammar explicit — PASS;
12. hearing inequality explicit — PASS;
13. tied minimum routes explicit — PASS;
14. simultaneous event selection explicit — PASS;
15. retarget rule explicit — PASS;
16. no hidden probability explicit — PASS.

## Ordering / mutations
17. fixed-step order explicit — PASS;
18. barrier activation phase explicit — PASS;
19. door mutation explicit — PASS;
20. BEFORE_MUTATION immutable snapshot ownership explicit — PASS;
21. AFTER_MUTATION ownership explicit — PASS;
22. preview mutation phase parity explicit — PASS.

## Player / listener / detection
23. player movement/noise states explicit — PASS;
24. barrier reach/move/release explicit — PASS;
25. listener state machine explicit — PASS;
26. investigation target ownership explicit — PASS;
27. search/return explicit — PASS;
28. hearing vs fail distinction explicit — PASS;
29. direct detection scope explicit — PASS;
30. no combat recovery explicit — PASS.

## Content
31. 34-main campaign count explicit — PASS;
32. 8-remix target/cut policy explicit — PASS;
33. two-listener main ceiling explicit — PASS;
34. three-listener 1.0 cut explicit — PASS;
35. E28 replacement explicit — PASS;
36. E33 replacement explicit — PASS;
37. E34 final identity explicit — PASS;
38. safe-preview enumeration validator explicit — PASS;
39. signature anti-repetition validator explicit — PASS;
40. content-density ceilings explicit — PASS.

## UX / accessibility
41. no-audio parity explicit — PASS;
42. world-space tied-route presentation explicit — PASS;
43. controller/remap path explicit — PASS;
44. reduced-motion/large-UI/speed assists explicit — PASS.

## Technical / persistence / commercial
45. deterministic architecture/engine boundary explicit — PASS;
46. save/replay/corruption recovery explicit — PASS;
47. offline/platform/demo boundaries explicit — PASS;
48. commercial/title/package boundaries explicit — PASS.

No unresolved gameplay rule requires an implementation session to invent canon.

---

# 22. Legitimate empirical gates carried into implementation

These are **tests of the frozen design**, not missing design decisions.

1. Barrier manipulation feels satisfying rather than chore-like.
2. Representative mature play averages roughly >=1 meaningful barrier edit/minute over long stretches.
3. Median grab→meaningful snap once in reach is roughly <=2–3 seconds.
4. Prediction/committed hearing parity = 100% across deterministic fixtures.
5. Muted/no-audio optimal decisions are identical to audio-enabled play.
6. Reduced-motion + large-UI + handheld remains readable in representative E16/E28/E33/E34-class states.
7. Passive waiting target <15%; >20% warning; >25% across representative mature successes = content redesign territory.
8. Players understand `heard can be useful` by D04/E07.
9. Mature content does not collapse into safe barrier-slot enumeration.
10. 34-main content signatures remain sufficiently varied; optional remixes cut first if not.
11. Direct-detection failures do not dominate acoustic-reasoning failures.
12. 55%/70% simulation-speed assists preserve ordering and acceptable feel.
13. Cross-platform deterministic state/replay hashes pass target builds.
14. Save corruption/backup/checkpoint fallback and idempotent demo import pass automated fixtures.
15. Real Steam demo/full App-ID/Cloud/offline paths pass before release candidate.
16. HEARWALL passes later legal/trademark/store/domain screening or is renamed without gameplay impact.
17. Final price chosen empirically from polished store/demo evidence without scope padding.

Failure of an empirical gate triggers implementation/content/presentation repair within the frozen boundaries or a documented design amendment. It does not grant permission to add unrelated gameplay systems.

---

# 23. Authority order

For Game #004 design/implementation interpretation:

1. **`GAME4_PHASE11_FINAL_FREEZE.md` — highest authority.**
2. `GAME4_PHASE10_AMENDMENTS.md` — historical repair rationale; already integrated. If wording differs, Phase 11 controls.
3. `GAME4_TECHNICAL_SPEC.md` — detailed implementation architecture where not superseded.
4. `GAME4_MECHANICS.md` — detailed mechanics where not superseded.
5. `GAME4_CONTENT.md` — detailed content schema/campaign where not superseded.
6. `GAME4_UX_PRESENTATION.md` — detailed UX/accessibility where not superseded.
7. `GAME4_ECONOMY_COMMERCIAL.md` — detailed commercial/Steam package where not superseded.
8. `GAME4_PRODUCT_THESIS.md` — product rationale where not superseded.
9. `GAME4_WHOLE_GAME_SIMULATION.md` and `GAME4_ADVERSARIAL_REVIEW.md` — validation/rationale; not independent rule authority against the freeze.
10. Tournament/research files — historical evidence only.

Explicit supersessions in this file include:
- `HUSHLINE` -> `HEARWALL` working commercial title;
- all three-listener 1.0 content -> CUT;
- E28/E33 -> two-listener final definitions above;
- V17/V18 -> mandatory validators;
- direct detection -> bounded secondary pressure layer;
- BEFORE_MUTATION -> immutable pre-commit graph revision ownership.

---

# 24. Freeze verdict

The design now has:
- a selected and bounded product identity;
- deterministic rules and ordering;
- complete listener/barrier/door/source semantics;
- exact prediction rules;
- a full 34-encounter campaign architecture;
- revised late-campaign identities after adversarial review;
- bounded accessibility and direct-detection contracts;
- content anti-repetition/oracle validators;
- technical architecture and persistence/recovery rules;
- commercial/demo boundaries;
- a replacement migration working title;
- explicit acceptance criteria;
- only legitimate empirical gates remaining.

A fresh implementation session can begin Phase 12A without inventing important gameplay.

**DESIGN COMPLETE = YES.**

## NEXT ACTION — migration / implementation handoff
1. Prepare factory-side migration package and implementation handoff for dedicated repository `Mikayilzade/hearwall`.
2. Dedicated repo must contain the complete Game #004 authority/history package plus renamed `IMPLEMENTATION_START_HERE.md`, `IMPLEMENTATION_STATUS.md`, `CI_NOTIFICATION_POLICY.md`, `MIGRATION_MANIFEST.md`, and README.
3. Verify final-freeze content/hash identity after migration.
4. Verify authority chain resolves entirely inside the dedicated repo.
5. Update `GAME_INDEX.md` only after migration verification.
6. Only after every migration gate passes, remove `GAME4_*` files from the factory and reset `STATUS.md` for Game #005.
7. Production implementation starts only in the dedicated repository, beginning with Phase 12A technical bootstrap and empirical graybox gates.
