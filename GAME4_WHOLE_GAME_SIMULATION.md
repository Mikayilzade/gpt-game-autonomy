# GAME #004 — WHOLE-GAME SIMULATION ON PAPER

Last updated: 2026-08-21
Factory run: **13**
Phase: **9 — Whole-Game Simulation on Paper**
Working name: **HUSHLINE** (provisional / high-risk for final commercial use)
Phase status: **COMPLETE / LOCKED FOR ADVERSARIAL REVIEW**
Production implementation: **NOT STARTED**

This pass walks the locked Game #004 product from first boot through demo, campaign, climax, failure/recovery, accessibility, persistence, mastery and hostile-player behavior. It does not add a new gameplay pillar. Where a contradiction appeared, the repair is explicitly bounded and preserves the Phase-3–8 authority chain.

---

## 1. Simulation purpose and pass criteria

The paper simulation asks one practical question: **if a fresh player actually plays the currently specified game from boot to completion, do the locked thesis, mechanics, content, UX, commercial and technical layers remain mutually coherent?**

The pass fails if any of the following occurs:
- the player must infer hidden acoustic information;
- prediction and resolution require different rules;
- the campaign teaches `silence everything` more strongly than selective audibility;
- barrier manipulation becomes occasional setup rather than a repeated physical verb;
- long passive patrol waits become a default solution surface;
- late content requires a detached graph UI to stay understandable;
- three-listener content is only readable by violating no-audio/handheld constraints;
- fail/restart/save behavior creates states not representable by the deterministic domain model;
- assists alter acoustic truth or ordering;
- mastery introduces grind, currency or a parallel ruleset;
- mature content requires unapproved bespoke mechanics.

Result of this pass: **no foundational contradiction was found. Phase 9 passes with four bounded clarifications and several empirical gates carried forward to Phase 10/implementation.**

---

# 2. First boot → accessibility setup → immediate control

## 2.1 First launch sequence

Expected first launch:
1. application opens to title/menu without a cinematic that blocks required setup;
2. language is chosen automatically from platform preference but can be changed immediately;
3. first-run accessibility card presents only high-impact options rather than a long mandatory form;
4. player may open full settings before starting;
5. `New Game` enters E01 or demo D01 with direct control in seconds;
6. no lore crawl is required to understand the first objective.

The first-run card should expose:
- UI/text scale;
- high-contrast acoustic motifs;
- reduced-motion acoustic pulses;
- persistent acoustic preview;
- whole-simulation speed: 100% / 85% / 70% / 55%;
- controller remap / input preset entry point;
- optional explicit acoustic numbers.

Audio settings are available but are **not** framed as required mechanical configuration. Muting master volume at first boot must not remove any decision information.

## 2.2 First 60 seconds

The player appears in a compact physical facility with:
- player avatar;
- one posted listener;
- one visible acoustic passage;
- one barrier rail and two meaningful snap positions;
- one simple traversal objective.

Within the opening minute:
- a WALK pulse visibly originates from the player;
- the pulse travels through the physical opening;
- the listener's threshold motif compares against the remaining pulse;
- the listener visibly enters HEARS/INVESTIGATE or remains unaffected depending on the authored tutorial beat;
- the player is allowed to move immediately.

The UI does **not** introduce node IDs, attenuation arithmetic, graph terminology, suspicion meters or a global minimap.

### Paper verdict
The first boot path is coherent with the locked no-audio and world-first contracts. The user can reach meaningful control before understanding the full system, while the first pulse demonstrates that acoustics are deterministic physical state rather than hidden stealth math.

---

# 3. Commercial demo simulation — D01–D04 / ~20 minutes

The demo is treated as a real commercial build slice, not a tutorial checklist.

## D01 — Physical Screen (~3–4 min)

### Starting state
- 3–4 acoustic nodes;
- one posted listener;
- one barrier rail with two useful slots;
- one direct traversal path;
- WALK locomotion only needed to solve.

### Player experience
0:00–0:40 — player walks, sees first footstep pulse and listener hearing response.

0:40–1:30 — barrier handle becomes reachable. Grabbing it constrains movement locally; world remains live. As the barrier leaves its first slot, the previously attenuated route visibly reopens. While between slots, no attenuation is active.

1:30–2:30 — candidate slot preview shows the next footstep as DOES_NOT_HEAR. The player snaps the barrier and immediately uses the opening.

2:30–3:30 — player crosses the facility and exits.

### What the player should learn
- sound travels through visible physical openings;
- barrier movement changes propagation;
- preview is exact;
- moving the barrier is a physical world action, not map editing.

### Failure risk
If D01 teaches `put barrier between you and guard = always safe`, that lesson must be broken immediately by D02.

---

## D02 — The Other Way Around (~4–5 min)

### Starting state
- 4–5 nodes;
- one listener;
- two minimum/near-minimum acoustic routes;
- 3 meaningful barrier slots.

### Player experience
The nearest doorway looks like the obvious block. Preview reveals a second route remains mechanically live. Both tied minimum routes illuminate at equal emphasis when applicable.

The player must reposition the barrier to a slot that changes the true minimum route rather than merely covering the visually nearest opening.

### Critical comprehension test
If the player blocks one route and still sees HEARS, the remaining route must be visually obvious **immediately**, not only after failure. This is the first anti-nearest-door proof.

### Demo pacing
No patrol cycle is needed. The encounter is solved by reading routes and moving.

---

## D03 — Make Them Move (~5–6 min)

### Starting state
- 5–6 nodes;
- one listener posted near a traversal choke;
- one fixed deliberate-distraction source;
- barrier placement can route that source toward the listener while preserving a safe player path.

### Player experience
The objective cannot be reached by simply making the player silent. The posted listener physically occupies the route.

The player previews the distraction:
- listener HEARS;
- investigation target is shown at the source-at-emission position;
- the path cue shows where the listener will move after hearing;
- the world does not claim future certainty beyond the deterministic current reaction.

The player triggers the distraction, sees the same committed propagation, then crosses the created opening while the listener investigates.

### Thesis proof
This is the first explicit lesson that **heard is useful** and **hearing is not failure**.

No hidden text explanation is necessary. A short contextual line may reinforce the lesson but must not carry the rule.

---

## D04 — Selective Audibility (~6–8 min)

### Starting state
- 6–7 nodes;
- two visually distinct listeners A/B;
- different route geometry and/or visible thresholds;
- one required louder action;
- barrier must move at least twice.

### Intended sequence
1. player approaches objective;
2. preview shows loud action would reach A and B;
3. barrier is moved so A still hears while B does not;
4. player commits the action;
5. A investigates to a useful location; B stays posted;
6. player actively traverses the created opening;
7. state changes make the outgoing barrier position wrong for the final route;
8. barrier is repositioned again before extraction.

### Demo-end comprehension test
A player who finishes D04 should be able to explain, without technical terminology:
> “I moved the sound barrier so one guard heard the noise and moved, while the other guard didn’t.”

If players instead explain `I made the room quieter` or `I waited for the guards`, the demo has failed despite completion.

### Demo paper verdict
The four-encounter package proves the differentiator within the target duration and avoids exposing late-system density. No contradiction with Steam demo/full-game separation is introduced.

---

# 4. Early campaign E01–E07 — identity formation

E01–E03 broadly mirror the demo's first principles if full-game progression starts from the same teaching grammar. Whether demo content is identical or curated remains a packaging decision already covered by the commercial/technical import contract.

## E01–E03
- E01 teaches single-route screening.
- E02 introduces WALK versus FAST_MOVE pulse cadence/strength without stamina or crouch complexity.
- E03 proves alternate acoustic routes.

The player should now understand that route geometry matters more than Euclidean distance.

## E04 — first deliberate distraction
The listener starts posted in a way that blocks progress. Player must trigger a visible source and create an investigation window. No cyclic patrol timing is necessary.

## E05 — threshold contrast
Two listeners with different persistent motifs face the same event. Preview directly reports HEARS / DOES_NOT_HEAR, so the threshold difference is learned perceptually rather than by arithmetic.

## E06 — required loud objective
A required interaction emits strength 3–4. The player cannot opt out by walking slowly. The game thereby prevents `perfect stealth = no sound` from becoming the campaign's dominant mental model.

## E07 — first true selective audibility
One listener must hear and one must not. This encounter is the campaign's **identity gate**.

### Phase-9 acceptance gate for E07
Before E07 completion, the player has seen:
- sound propagation;
- alternate routes;
- deliberate investigation;
- threshold contrast;
- unavoidable loud action.

After E07, the player must understand:
- audibility is a controllable resource/state;
- a listener reacting can be beneficial;
- barrier placement is not simply defensive silence.

### Paper verdict
The E01–E07 order is strong. No tutorial-text dependency is necessary if visual prediction and reaction animation carry their intended meaning.

---

# 5. Combination band E08–E16

This band tests whether complexity increases through recombination rather than new rules.

## E08 — alternate route + lure
Player cannot simply route a distraction along the nearest opening; alternate path remains live. Solution combines F2 + F4 with one listener.

## E09 — selective audibility + threshold split
Two listeners hear differently because route cost and thresholds both matter. The UI compares incoming pulse count/pattern against each listener motif and states the result.

## E10 — first exposed barrier manipulation
The correct slot is not reachable from a permanently safe pocket. Player uses a previously created investigation window to reach the rail, manipulates while world simulation continues, then exits before return.

**Verb-frequency check:** barrier manipulation now overlaps infiltration instead of remaining pre-room setup.

## E11 — first door mutation
A player interaction changes a visible door and emits sound. The preview must show whether the event uses BEFORE_MUTATION or AFTER_MUTATION geometry with simple pictograms.

### Clarification P9-C1 — event-order teaching bound
Phase 4 already allows BEFORE_MUTATION / AFTER_MUTATION. Phase 9 clarifies that **E11 is the first campaign encounter where this distinction may be completion-critical**. Earlier encounters should not require the player to reason about event/mutation order. This is a pacing clarification, not a new rule.

## E12 — over-propagation
Two physical sources with different fixed strengths demonstrate that louder is not monotonically better. The stronger source can reach an unwanted listener through a second route.

## E13 — sequence preservation
Barrier solves action A at slot X, then must move to slot Y for action B. The encounter rejects one-slot camping without cooldowns or artificial decay.

## E14 — lure creates access to exposed rail
The player deliberately makes the right listener hear, crosses into the manipulation zone, then changes the barrier while still exposed.

## E15 — door mutation changes selective target
A door creates/removes a route so the identity of the listener who should hear the next action changes after mutation.

## E16 — combination mini-climax
- 7–8 nodes;
- two listeners;
- alternate routes;
- selective audibility;
- two-step barrier sequence.

### Band verdict
The campaign now requires 2-family reasoning without introducing system exceptions. Barrier edit cadence remains credible: most encounters need 2–4 meaningful edits across 6–12 minutes, with traversal and source use between edits.

---

# 6. Mature campaign E17–E29

## E17 — return-path inversion
Entry arrangement is wrong for extraction because objective completion changes one visible state. Player cannot memorize a static `best barrier slot` for the facility.

## E18 — two-event ordering / retarget rule
Listener is already INVESTIGATING from event A. Equal-strength event B can be heard but cannot reset the active investigation unless the listener has reached ARRIVED/SEARCH. A stronger received event may retarget.

Presentation must show:
- B propagates and is heard;
- `heard but no retarget` priority marker;
- current investigation target remains owned by A.

This makes the anti-ping-pong rule learnable rather than appearing as inconsistent AI.

## E19 — threshold split + over-propagation
The player chooses between two world sources rather than selecting a strength from a menu. Stronger sound reaches further but may compromise the wrong listener.

## E20 — exposed rail + selective audibility
The player must first create an investigation opening, traverse to the local rail, then reposition for a second sound. The central verb is now inseparable from physical exposure.

## E21 — door mutation + sequence
Door state changes both navigation and acoustic connectivity. The barrier slot useful before the door opens is insufficient afterward.

## E22 — lure + return inversion
The same listener displaced during entry must be handled differently on extraction because the player's source node and door state differ.

## E23 — first moving environmental source
A clearly visible moving source follows one authored deterministic route. It has a world-space emission rhythm indicator. The player is never asked to infer hidden timing.

The first moving-source encounter stays otherwise simple, preventing the new variable from being confused with a new acoustic rule.

## E24 — moving source + alternate route
The source's changing node makes the minimum route evolve. Barrier edits are still local/direct; the player may need to move along the rail as the source progresses.

## E25 — event ordering, two listeners, no patrol dependence
Two deliberate/required events should be triggered in a readable order. Same-tick ambiguous multi-event exploitation is not required.

## E26 — three required actions / sequence preservation
The barrier occupies at least three meaningful slots over the intended route. Each action has a different useful listener outcome.

## E27 — exposed rail + door + return inversion
This is the mature physical-infiltration test: the correct edit requires entering a manipulation envelope while a listener is displaced by a player-created sound, then objective/door mutation changes extraction logic.

---

## E28 — exceptional three-listener encounter

### Paper state
- <=10 acoustic nodes;
- three listeners with clearly distinct silhouettes/patterns;
- no moving environmental source;
- no completion-critical cyclic patrol timing;
- at most 3–4 simultaneously decision-relevant routes;
- selective audibility groups: e.g. A should hear, B/C should not, or A/B should hear while C does not.

### Handheld/no-audio simulation
At 1280×800-equivalent framing:
- threshold motifs remain visible at enlarged UI scale;
- persistent listener labels A/B/C may be enabled as a clarity option;
- route preview emphasizes only the targeted source and relevant listeners;
- unrelated acoustic structure is deemphasized;
- all three listener outcomes remain world-space and no global graph panel is introduced.

### Result
**E28 remains credible on paper but is not promoted to a guaranteed content requirement beyond the already locked exceptional slot.** It carries an implementation/playtest readability gate. If handheld/no-audio tests fail, E28 should be reduced to two listeners or replaced with another two-listener mature encounter rather than rescued by a global graph UI.

This is consistent with the existing Phase-5/6 cut rule.

---

## E29 — mature synthesis with moving source
Two listeners only. This proves mature depth does not require listener-count escalation after E28.

### Mature-band passive-wait budget
Representative intended mature solution traces show player-created windows dominate. Content validator target remains:
- preferred passive waiting <10–15%;
- hard warning/reject territory approaching 20–25%.

A solution that can be completed safely by parking and waiting through patrols is invalid if it bypasses the intended acoustic decisions.

---

# 7. Climax band E30–E34

## E30 — tied-route climax
10–12 nodes, two listeners, multiple tied minimum routes. Blocking one tied path visually leaves the other active. Player must change route costs rather than assume a single chosen shortest path.

## E31 — door + two-event order
A required loud action and door mutation use explicit event phase ordering. The solution depends on choosing when the door state changes, not on frame timing.

## E32 — moving source + extraction inversion
Barrier moves at least three meaningful times. The moving source creates a useful lure during entry but a dangerous return path after objective completion.

## E33 — exceptional three-listener selective audibility

### Paper density audit
The allowed version uses:
- <=10–11 nodes;
- exactly three listeners;
- no moving environmental source;
- no simultaneous door-order tutorial burden;
- no cyclic patrol timing as the core;
- one primary event at a time;
- <=3 decision-relevant minimum-route groups onscreen.

### Result
E33 is **more fragile than E28** because it occurs in climax content and risks making `more listeners = harder` feel like the difficulty model.

### Clarification P9-C2 — E33 content gate
E33 may remain in the 34-encounter plan only if prototype/handheld/no-audio validation shows three listeners remain readable **without** global graph UI and without reducing the physical world to icons. If it fails, replace E33 with a two-listener dense selective-audibility encounter using tied routes + threshold split. The campaign count remains 34; no new mechanic is needed.

This clarifies the existing exceptional-density rule rather than changing it.

## E34 — final synthesis

Target state:
- <=12 nodes;
- two listeners baseline preferred;
- alternate routes;
- threshold difference;
- visible door mutation;
- deliberate lure;
- required loud objective;
- exposed barrier travel;
- extraction inversion;
- optional moving source only if readability remains within route-density caps.

### Intended high-level sequence
1. preview shows the direct objective sound would reach both listeners;
2. player moves barrier and triggers **useful-heard moment #1**: Listener A hears a deliberate source and investigates away from the rail;
3. player crosses to exposed rail and changes barrier position;
4. door/objective mutation alters graph;
5. required loud action produces **useful-heard moment #2**: Listener B should hear and move while A is screened;
6. player reaches objective/extraction region;
7. return-path inversion makes previous slot unsafe;
8. barrier is repositioned a final time;
9. player extracts with both listener outcomes causally readable.

### Finale requirement
The final encounter must not be solved by `silence all dangerous listeners`. At least two heard events are necessary and useful. If implementation cannot create this cleanly at <=12 nodes, the finale must simplify geometry rather than add new mechanics/listeners.

---

# 8. Fail → cause trace → restart → checkpoint restore

## 8.1 Representative failure
Player deliberately lures A, crosses an opening, then FAST_MOVEs through a region where B now hears footsteps through an alternate route. B investigates and later directly detects player.

### Failure presentation
The game must separate causal layers:
1. B heard the specific locomotion event — show exact acoustic route that reached B;
2. B moved because of that event — show captured source-at-emission target;
3. direct detection caused failure — show the separate listener→player detection line/region.

The fail reason must **not** simplify this to `Too loud` if hearing itself was not the fail predicate.

## 8.2 Quick restart
Restart restores the latest canonical snapshot:
- player authoritative state/node;
- listener positions/state/targets;
- doors;
- barrier snapped slot;
- moving sources;
- objective flags;
- event counters;
- deterministic timers/state revision.

No half-barrier state, half-sound event or animation frame is restored.

Prediction after restart must be identical to the same pre-fail canonical state.

## 8.3 Checkpoint continuity
Checkpoint only activates in authored safe state. A checkpoint cannot capture:
- barrier between slots;
- an unresolved sound event;
- a door mutation halfway through commit;
- half-resolved fail state.

### Paper verdict
Failure/recovery is internally coherent with the domain architecture and supports rapid causal learning rather than run loss.

---

# 9. Save exit/reload, corruption recovery, demo→full and Steam-offline

## 9.1 Save/exit during encounter
Manual or automatic save requests resolve to the nearest allowed persistence contract:
- campaign/profile progress saves immediately when safe;
- encounter checkpoint state is saved only as a canonical deterministic snapshot;
- active transient animation does not become save truth.

Reload recreates domain state first, then presentation binds to it.

## 9.2 Corrupted primary save
Expected behavior:
1. primary save fails validation/hash/schema parse;
2. one-generation backup is tested;
3. valid backup restores;
4. player receives a concise recovery notice;
5. the game does not silently invent missing progression.

If both primary and backup are invalid, preserve settings where independently valid and offer safe profile recovery/new profile rather than loading undefined domain state.

## 9.3 Demo → full import
Mechanics stay identical across FULL/DEMO/DEV.

If demo encounters match campaign content and manifest compatibility is verified, full game may import approved completion fields and offer `Continue after demo`.

If demo is curated/remixed, import only:
- settings/accessibility;
- input mappings when compatible;
- `demo_completed` metadata;
- explicitly approved achievement/progress compatibility fields.

Do not mark campaign encounters complete merely because a similar demo encounter was completed.

## 9.4 Steam offline
Steam/platform adapter failure cannot invalidate local campaign state.

Offline behavior:
- game launches and remains playable;
- local saves remain authoritative;
- achievement/Cloud synchronization queues or reconciles later according to adapter rules;
- store overlay/CTA failure does not block demo play;
- no network check is required for hearing, content, saves or progression.

### Paper verdict
No persistence/platform contradiction appears.

---

# 10. Accessibility path simulations

The same representative E20/E26-style encounter is simulated under all core presentation assists.

## 10.1 No-audio
Master volume = 0.

Player still receives:
- source strength motif;
- passage attenuation motifs;
- all minimum routes;
- listener thresholds;
- HEARS / DOES_NOT_HEAR;
- investigation target/path cue;
- locomotion pulse cadence indicator;
- door/event ordering when relevant;
- fail cause trace.

**Acoustic optimal decisions remain identical. PASS on paper.**

## 10.2 Reduced motion
Pulse travel becomes shorter, less animated and may use static stepped route emphasis. Exact route/intensity/outcome remains visible.

No mechanical timer is inferred from cosmetic pulse duration.

**PASS on paper.**

## 10.3 High contrast / color-independent
Listener A/B/C, route classes, source strength and thresholds remain distinguished by shape/count/pattern rather than hue.

**PASS on paper.**

## 10.4 Large UI/text
World-space symbols scale within bounded layouts. Camera may ease slightly or acoustic line thickness increases. The game must not solve overlap by hiding a listener outcome.

Two-listener normal content remains credible. Three-listener exceptional states remain empirical gates.

## 10.5 Whole-simulation speed 70% / 55%
The domain still runs the same sequence of simulation ticks; wall-clock accumulation slows.

At 55%:
- player movement, listener movement, moving sources, interaction progress, search timers, door motion and locomotion pulse cadence all slow together;
- acoustic event resolution remains canonical at the appropriate domain tick;
- retarget ordering is unchanged;
- intended solution remains valid;
- passive-wait percentage measured in simulation time remains the relevant design metric, not wall-clock seconds.

### Clarification P9-C3 — mastery timing under speed assists
Time-target mastery challenges must record whether a deterministic whole-simulation-speed assist was active. Baseline campaign completion remains valid with assists. A fixed-time mastery predicate may either be unavailable under altered simulation speed or compare normalized simulation time; it must never quietly compare wall-clock time and punish accessibility use.

This clarification implements the existing commercial/UX rule that assist use is not shamed while allowing optional timing-specific mastery to remain meaningful.

---

# 11. Mastery, remix and replay flow

After main encounter completion:
- player sees one or two relevant mastery predicates, not a universal three-star checklist;
- completion unlocks related remixes through progression state, not currency;
- no power upgrade changes barrier attenuation, thresholds or footstep strengths;
- replay starts from deterministic initial/checkpoint state;
- cause trace and preview remain available;
- optional no-restart / max-edits / selective-hearing / wait-budget / fast-move goals encourage alternate understanding of the same rules.

## Replay example
A player first clears E16 with four barrier edits. A mastery target asks for <=3 edits. The player discovers that one deliberate lure can keep a listener displaced long enough to combine two traversal actions under one slot choice.

The reward is mastery/unlock state, not a stronger barrier.

### Paper verdict
Retention is intrinsic and consistent with premium one-time purchase. No currency/grind/live-service pressure appears.

---

# 12. Hostile-player behavior / exploit simulation

## 12.1 Permanent barrier parking
**Attack:** leave barrier at one seemingly safe slot for entire encounter.

Expected defense:
- mature content includes alternate routes, loud objectives, selective-hearing requirements or state mutations;
- Phase-5 V05 rejects permanent all-dangerous-listener silence solutions.

**Result:** no mechanical cooldown needed. Content validator remains sufficient.

## 12.2 Silence-everything
**Attack:** WALK slowly, avoid every optional source, never lure.

Expected defense:
- required loud objectives;
- posted listener blocks progress unless deliberately displaced;
- selective-audibility campaign gates.

**Result:** thesis survives if campaign validator coverage is enforced.

## 12.3 Equal-lure spam
**Attack:** repeatedly trigger equal-strength lure to keep listener away indefinitely.

Mechanical result:
- listener already INVESTIGATING ignores equal-intensity retarget for target replacement until ARRIVED/SEARCH;
- event may be visibly heard but does not reset travel.

**Result:** spam does not produce infinite displacement.

## 12.4 Strongest-sound spam
**Attack:** always choose strength-4 source.

Result:
- stronger event reaches more routes/listeners;
- over-propagation makes strength non-monotonic in safety;
- source strengths are physical choices, not an inventory upgrade.

**Result:** no dominant strongest-sound strategy.

## 12.5 Barrier-midpoint abuse
**Attack:** hold barrier halfway between slots hoping to receive partial attenuation or confuse preview.

Mechanical result:
- between slots = no attenuation;
- release deterministically returns to nearest slot, midpoint tie to last occupied slot;
- preview shows passage reopened.

**Result:** no hidden partial benefit.

## 12.6 Door-order race
**Attack:** attempt to exploit frame timing so a sound sometimes uses pre-door graph and sometimes post-door graph.

Mechanical result:
- authored emission phase selects BEFORE_MUTATION or AFTER_MUTATION;
- fixed-step order resolves identically;
- presentation mirrors authored order.

**Result:** no race surface.

## 12.7 Restart brute force
**Attack:** try every barrier slot/source combination and restart instantly rather than reason.

Fast restart is intentionally allowed; the game must not punish experimentation with friction.

Defense is not slower reset. Instead:
- preview makes causal reasoning faster than blind testing;
- mature rails stay at 3–5 meaningful choices;
- sequence/state changes make brute-force branching grow without becoming huge;
- mastery goals can reward clean solutions but main completion accepts discovery through experimentation.

**Result:** acceptable. Brute force is a content-quality risk, not justification for punitive restart delay.

## 12.8 Content-signature repetition
**Attack:** player recognizes `two guards + 3-slot rail + loud objective` and assumes the same slot pattern each time.

Defense:
- content signature validator V16;
- vary route topology, threshold combinations, source positions, door mutation, rail reach/exposure, objective order and return inversion;
- do not vary by hidden exceptions.

### Clarification P9-C4 — signature sampling requirement
For authoring review, every block of roughly 5 consecutive mature/climax encounters should include at least three materially different solution signatures across: primary reasoning-family combination, number/order of barrier edits, useful-heard target identity and graph-mutation pattern. This is a content-review heuristic, not a gameplay rule or hard runtime validator.

**Result:** repetition risk remains controllable without adding systems.

---

# 13. Barrier verb-frequency audit across full game

The selected concept originally survived tournament pressure partly because meaningful barrier manipulation averaged roughly 1.5 edits/minute in dense mature kernels. The campaign need not sustain that density continuously, but the signature verb cannot disappear.

Recommended authored-solution telemetry bands:
- teaching: ~1 meaningful edit per 45–90 seconds while rules are learned;
- combination: ~1 per 35–60 seconds;
- mature: ~1 per 25–60 seconds depending on traversal burden;
- climax: generally 3–6 meaningful edits across a 6–12 minute encounter, with denser moments near causal transitions.

Hard thesis warning remains: **long representative stretches below roughly one meaningful acoustic edit per 60 seconds require review** unless traversal itself is clearly exploiting an edit already made.

Barrier movement should not be inflated with meaningless moves to hit a metric. Only edits that change a relevant near-term acoustic decision count.

---

# 14. Contradiction ledger and bounded repairs

## P9-C1 — First completion-critical emission-order lesson
**Issue:** Phase 4 permits BEFORE/AFTER mutation from the start, but early tutorial content could become opaque if this distinction appears too early.

**Repair:** E11 is the first planned encounter where emission-order distinction may be completion-critical. Earlier content can contain simple actions whose order is self-evident but should not test the player on the abstract distinction.

**Upstream effect:** pacing clarification only; no mechanical file rewrite required.

## P9-C2 — E33 exceptional density
**Issue:** three listeners + climax complexity could violate handheld/no-audio readability even if mechanically valid.

**Repair:** E33 is conditional on implementation readability validation. If it fails, replace with two-listener dense selective-audibility/tied-route content; campaign count remains 34.

**Upstream effect:** consistent with existing Phase-5/6 empirical cut rule; no mechanic change.

## P9-C3 — timing mastery under simulation-speed assist
**Issue:** wall-clock time targets could penalize a deterministic accessibility setting.

**Repair:** mastery records assist state and uses either normalized simulation time or disables only the optional fixed-time predicate under altered whole-simulation speed. Campaign completion and non-timing mastery remain fully valid.

**Upstream effect:** clarification of existing commercial accessibility boundary; no acoustic rule change.

## P9-C4 — mature content signature sampling
**Issue:** data-driven reuse could still create recognizable templates even when each encounter passes individual validators.

**Repair:** authoring review samples consecutive mature/climax blocks and requires materially varied solution signatures. This is a design-review heuristic, not a runtime mechanic.

**Upstream effect:** content-process clarification only.

No contradiction required changing:
- sound strength 1–4;
- attenuation 0–2;
- threshold 1–3;
- +3 barrier effect;
- one barrier baseline;
- local/direct manipulation;
- listener retarget ordering;
- fixed-step update order;
- 34 main / 8 optional content budget;
- premium/no-currency commercial model;
- no-audio parity;
- deterministic prediction/resolution model.

---

# 15. Empirical gates carried into Phase 10 / implementation

Paper simulation cannot prove feel/readability/performance. The following remain explicit empirical gates rather than unresolved rules:

1. barrier manipulation feels tactile rather than chore-like;
2. preview and committed hearing match 100%;
3. muted players make the same optimal acoustic decisions;
4. no-audio route density remains readable at handheld scale;
5. meaningful barrier edit frequency remains healthy without filler moves;
6. passive waiting remains below campaign targets in real play;
7. players naturally learn `heard can be useful` by E07/D04;
8. E28 three-listener state remains readable or is simplified;
9. E33 three-listener climax remains readable or is replaced by two-listener content;
10. whole-simulation speed assists preserve ordering and feel at 70%/55%;
11. deterministic movement/collision remains comfortable at chosen quantization;
12. save/replay state hashes remain stable across target platforms;
13. demo→full import remains safe under real Steam app/configuration behavior;
14. title `HUSHLINE` is replaced/cleared before commercial freeze if conflict risk remains.

---

# 16. Phase-9 acceptance result

- First boot/accessibility path: **PASS ON PAPER**.
- Immediate first acoustic feedback: **PASS**.
- D01–D04 ~20-minute demo: **PASS**.
- Selective audibility visible by D04/E07: **PASS**.
- E08–E16 recombination pacing: **PASS**.
- E17–E29 mature scaling: **PASS WITH EMPIRICAL DENSITY GATES**.
- E28 three-listener readability: **CONDITIONAL / CUTTABLE**.
- E30–E34 climax: **PASS ON PAPER**.
- E33 three-listener readability: **CONDITIONAL / REPLACEABLE WITHOUT SCOPE GROWTH**.
- E34 two useful-heard moments: **PASS AS REQUIRED FINALE CONTRACT**.
- Failure/cause/restart loop: **PASS**.
- Save/reload/corruption fallback: **PASS ON SPEC**.
- Demo→full continuity: **PASS WITH MANIFEST COMPATIBILITY**.
- Steam-offline behavior: **PASS**.
- No-audio / reduced motion / high contrast / large UI: **PASS ON PAPER**.
- 70%/55% whole-simulation-speed path: **PASS ON RULE ORDERING**.
- Mastery/remix flow: **PASS / NO GRIND OR CURRENCY**.
- Hostile-player exploit set: **NO NEW HARD CONTRADICTION**.
- Production implementation started: **NO**.

**PHASE 9 WHOLE-GAME SIMULATION = COMPLETE.**

## NEXT DESIGN HANDOFF — PHASE 10 ADVERSARIAL REVIEW

Create `GAME4_ADVERSARIAL_REVIEW.md` and attack the entire product as if trying to cancel it before production. At minimum:
1. fun/verb-frequency and tactile barrier risk;
2. `graph puzzle disguised as stealth` risk;
3. waiting/camping/silence dominance;
4. brute-force/restart and preview-overautomation risk;
5. tied-route visual overload;
6. two-listener repetition and three-listener density;
7. content-signature exhaustion across 34+8 encounters;
8. direct-detection/stealth feel versus deterministic puzzle clarity;
9. controller/handheld/no-audio/reduced-motion accessibility conflicts;
10. save/replay/checkpoint corruption and deterministic state recovery;
11. demo/full import, Steam-offline and platform-adapter failure;
12. title/capsule/market-position confusion;
13. $14.99–$19.99 value risk;
14. implementation ambiguity in every Phase-4–8 contract;
15. cut list: identify what should be removed before adding anything.

Do not set `DESIGN COMPLETE = YES` in Phase 10. Only Phase 11 may freeze the specification after adversarial findings are reconciled.