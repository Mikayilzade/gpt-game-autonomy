# GAME #004 — PRODUCT THESIS LOCK

Last updated: 2026-08-21
Factory run: **7**
Phase: **3 — Product Thesis Lock**
Phase status: **COMPLETE / LOCKED**
Concept: **G4C19 acoustic infiltration / physical sound routing**
Production implementation: **NOT STARTED**

## 1. Product identity

### Working product name
**HUSHLINE** — provisional market-facing working title for design continuity, **not a trademark clearance**. The historical label `Soundproof Smuggler` is retired from active design because cargo/smuggling is not part of the core product.

Title rule: later commercial/title review may replace `HUSHLINE` without changing mechanics, fiction obligations or scope. Do not invent cargo, contraband, delivery economy or a smuggling campaign to justify the old name.

### One-sentence hook
**Move a soundproof barrier through each facility to decide who hears your footsteps, distractions and break-ins — sometimes the right guard must hear you.**

### Genre framing
**Top-down real-time acoustic infiltration puzzle.**

Secondary store-language candidates: stealth puzzle, systemic puzzle, infiltration. Do not frame the game primarily as horror, immersive sim, job simulator or audio game.

### Core fantasy
You are an infiltrator who treats a building's audibility as manipulable physical space. You move through compact facilities while repositioning a visible acoustic barrier so that sounds travel toward useful listeners and away from dangerous ones. Mastery means creating your own openings through **selective audibility**, not crouching indefinitely until patrols happen to line up.

The fiction should support trespass/infiltration/sabotage/retrieval at a light systemic level, but the exact narrative wrapper remains implementation-flexible until later presentation/content phases. It must not require dialogue trees, cargo logistics, economy, combat campaign or large narrative production.

---

## 2. Target player and platform

### Primary player
Players who enjoy compact systemic puzzle games and readable stealth where failure can be understood and retried quickly. The product should reward causal reasoning more than reflex precision or memorizing long patrol schedules.

### Platform
- **PC / Steam first**.
- Keyboard/mouse and controller are equal first-class input targets.
- Steam Deck / handheld-readable UI is a design target, not a promise of certification before implementation validation.
- Single-player and offline-complete baseline.
- No multiplayer/network dependency.

### Session profile
- Normal encounter: roughly **6–12 minutes** on first solution, shorter on replay/mastery.
- Natural play session: **20–45 minutes**, usually 2–5 encounters.
- First-clear campaign target: **5–8 hours**.
- Main content target: **30–36 encounters**, with **8–10 optional advanced/remix/mastery encounters** only if production evidence supports them.
- Fast restart/checkpoint recovery; no long run loss.

---

## 3. Core loop

1. **Read** the physical room layout, visible listeners, current openings and predicted acoustic routes.
2. **Move** through the space toward an objective or next traversal position.
3. **Reposition/rotate the acoustic barrier locally** into an authored physical slot while remaining in the world.
4. **Preview** the exact propagation result for relevant near-term sound-producing actions.
5. **Act** — walk/run, trigger a distraction, open/break/use a noisy object, or cross a risky route.
6. **Exploit the reaction** of listeners who heard the event while those intentionally screened from it remain uninformed.
7. Repeat as doors, player position, listener position and visible sources change the useful acoustic route.
8. Reach the encounter objective/extraction state, then optionally replay for mastery criteria.

The player must spend meaningful time **moving and infiltrating**, not only manipulating a graph. The barrier is the signature verb, but traversal is the carrier that makes each acoustic edit matter.

---

## 4. Barrier manipulation lock

### Decision: LOCAL / DIRECT manipulation is canonical
The player physically approaches a barrier rail/track or its reachable handle zone and directly pushes/slides/rotates the barrier between authored snap slots. The world does not pause. Propagation preview updates continuously as the barrier moves and snaps.

### Explicitly rejected as baseline
- remote whole-building barrier control;
- selecting graph edges from a modal map;
- pausing into a tactical graph editor;
- telekinetic arbitrary-distance dragging;
- freeform placement anywhere in the room.

### Limited exception
A later encounter may use a **clearly physical local mechanism** (e.g. a nearby crank/lever mechanically linked to the same visible barrier) if accessibility/layout needs it, but this cannot turn the product into remote graph control. Phase 4 must define reach/interaction timing and interruption semantics.

Why local/direct is locked: it couples acoustic planning to exposure and traversal, protects the physical fantasy, keeps the 10-second clip understandable and prevents the optimal play surface from becoming an abstract network UI.

---

## 5. Minimum thesis vocabulary

This is the minimum vocabulary needed to describe the product. Phase 4 may formalize values/state machines but must not add families casually.

### Sound sources
1. **Player locomotion** — footsteps/movement noise; source node follows the player.
2. **Deliberate distraction source** — a player-triggered world object/action used to make a chosen listener investigate.
3. **Objective/environment loud action** — e.g. breaking/opening/operating something required by the encounter.
4. **Moving environmental source** — exceptional mature content, used to make routing state evolve without patrol waiting.

No microphone input. No procedural voice recognition. No requirement to identify pitch/frequency by ear.

### Listeners
1. **Stationary/posted listener** — teaches routing without patrol timing.
2. **Investigating listener** — moves to a heard event under deterministic reaction rules.
3. **Patrolling listener** — permitted later, but patrol timing is secondary pressure, not the foundation of every encounter.

Normal mature encounter target: **2 listeners**. Three is exceptional. Large crowds are out of scope.

### Acoustic passages / doors
- Physical openings/passages are the visible acoustic edges.
- A small discrete attenuation vocabulary is used; exact classes belong to Phase 4.
- Doors may visibly open/close and therefore mutate traversal/acoustic connectivity.
- Multiple acoustic routes are allowed and must be previewable; blocking the nearest doorway cannot be assumed to silence a listener.

### Barrier
- One active movable acoustic barrier is the **baseline and product identity**.
- It occupies authored physical slots and adds deterministic attenuation to the affected passage.
- Multiple independently controlled barriers are **not** part of the Phase-3 scope ceiling; Phase 4 must prove the full game with one before any exception can be proposed.

---

## 6. Active-stealth contract

The product is not `wait for patrol cone, then move` stealth.

Locked rules for downstream design:
- at least a substantial portion of main encounters must be solvable with no cyclic patrol timing as the core puzzle;
- deliberate sound that a listener **should hear** must appear in the main campaign, not only optional challenges;
- mature encounter design should repeatedly make `silence everything` inferior or impossible;
- passive waiting target is **<20% of active encounter time**, with a preferred mature target below 10–15%;
- if the player is safe only because they waited through long patrol cycles, content design has failed the thesis even if technically solvable;
- player-triggered investigation windows are preferred over passive schedule windows.

---

## 7. Visual/no-audio parity lock

**Every decision required to complete the game must be possible with game audio muted.** Audio adds atmosphere, timing feel and reinforcement but no exclusive mechanical information.

The visual language must eventually communicate:
- where a sound originates;
- which physical passages it propagates through;
- relative sound-strength band without requiring numbers;
- whether each relevant listener will hear the predicted action;
- what changed when the barrier/door/source/listener state changed;
- why a listener did or did not react after commitment.

Prediction and resolution must use the same deterministic model. A player must not be shown a safe route that resolves as audible because of hidden acoustic simulation.

Accessibility settings may change presentation, contrast, animation speed or simulation speed under rules later defined, but must not secretly change optimal acoustic logic.

---

## 8. Demo promise

Target demo: **15–25 minutes**, with a 20-minute nominal beat.

Required progression:
- first visible sound propagation within the opening minute;
- first independent barrier-placement choice by roughly minute 2–3;
- multiple-route lesson before the midpoint;
- at least two sound strengths/classes demonstrated without numeric homework;
- first deliberate lure where a listener **should hear** the action by roughly minute 10–15;
- demo climax before the end requires **selective audibility**: preserve a useful route to one listener while suppressing another, then actively traverse the created opening.

A demo that ends after teaching only `block sound to sneak past guard` fails the product thesis.

---

## 9. Differentiator / market position

Current sound-stealth precedents such as **Stifled** and **Noise Hunters** reinforce that `sound reveals you / enemies hear noise` is not itself distinctive. 2026 Steam also contains microphone-driven stealth/horror such as **QUIET**, further increasing the need not to market the product as simply `every sound matters`.

The claimable product difference is narrower:

> **The player repeatedly and physically edits deterministic acoustic connectivity so the same action is heard by selected listeners and screened from others.**

The product should visually sell **route flipping + selective listener reaction**, not generic silence, echolocation, microphone gimmicks or realistic acoustics.

Current market evidence also supports keeping the product compact/premium rather than inflating content: comparable experimental/sound-led products occupy a wide price range, while current Steam releases remain crowded. Phase 7 must do the actual pricing analysis; Phase 3 does not freeze price.

---

## 10. Scope ceiling

### In scope
- top-down 2D or 2.5D-readable presentation with discrete physical rooms/passages;
- compact authored encounters backed by reusable data-driven acoustic grammar;
- deterministic graph acoustics;
- one baseline movable barrier;
- small sound-strength/attenuation bands;
- stationary, investigating and limited patrolling listeners;
- doors and a small number of visible moving sound sources;
- objective interactions that generate sound;
- optional mastery/replay criteria if they reuse main systems;
- stylized low-to-moderate asset burden.

### Explicitly out of scope for 1.0 thesis
- ray tracing / wave acoustics / realistic reverberation simulation;
- microphone input or mandatory audio perception;
- combat system as a parallel pillar;
- takedown tree, weapons arsenal or enemy health combat;
- inventory/crafting economy;
- cargo logistics or smuggling economy;
- open world / hub requiring large NPC content;
- procedural endless generation as a requirement;
- multiplayer/co-op;
- dialogue-heavy branching narrative;
- multiple simultaneously free-positioned acoustic barriers;
- remote modal graph editing as core play;
- arbitrary destructible architecture;
- large stealth crowds.

### Content/complexity caps carried into Phase 4
- normal mature encounter: **<=12 acoustic nodes**;
- one barrier baseline;
- <=4 sound-strength bands unless Phase 4 proves fewer are sufficient;
- 2 listeners normal / 3 exceptional;
- <=4 core reusable mature reasoning families must already cover most content before adding another system.

---

## 11. One-week empirical kill gates

The design remains a thesis until graybox evidence exists. A one-week prototype should be able to kill it cheaply.

Required graybox: 8–12 compact encounters, local/direct barrier manipulation, visual prediction, stationary + investigating listeners, at least one door mutation, at least one deliberate lure and at least one multiple-route selective-audibility problem.

### Kill / major-redesign triggers
1. **Prediction mismatch:** any deterministic case where visual preview and actual hearing disagree after bugs are excluded from test setup.
2. **Accessibility divergence:** muted players cannot make the same optimal decisions from visual state alone.
3. **Silence dominance:** mature test encounters are routinely solved by blocking the nearest useful doorway and minimizing all sound.
4. **Waiting dominance:** passive waiting exceeds ~25% of successful run time across representative encounters, or players describe waiting as the primary skill.
5. **Verb scarcity:** meaningful barrier edits average worse than roughly **1 per 60 seconds** for long representative stretches.
6. **Weak physical fantasy:** players describe the main action primarily as `editing a graph/map` rather than moving a barrier to control who hears them.
7. **Selective-audibility failure:** players finish the test set without understanding that intentionally being heard by one listener can be correct.
8. **Tactile friction:** direct barrier manipulation repeatedly feels like a chore between actual stealth decisions rather than the source of those decisions.
9. **Content collapse:** eight or more graybox encounters cannot be built from the frozen vocabulary without bespoke exceptions or hidden rules.

Passing these gates does not prove commercial success or fun; it only allows the design to survive into implementation/content validation.

---

## 12. Phase-3 acceptance checklist

- Target player: **LOCKED**.
- Platform: **PC/Steam-first, single-player/offline — LOCKED**.
- Genre framing: **top-down real-time acoustic infiltration puzzle — LOCKED**.
- One-sentence hook: **LOCKED**.
- Core fantasy: **LOCKED**.
- Session structure / first-clear scope: **LOCKED**.
- Core loop: **LOCKED**.
- Differentiator: **LOCKED**.
- Barrier ownership: **LOCAL/DIRECT — LOCKED**.
- Minimum source/listener/door vocabulary: **LOCKED AT THESIS LEVEL**.
- Active-stealth/no-waiting contract: **LOCKED**.
- Visual/no-audio decision parity: **LOCKED**.
- Demo selective-audibility promise: **LOCKED**.
- Product scope ceiling: **LOCKED**.
- One-week empirical kill gates: **LOCKED**.
- Final commercial title: **NOT LOCKED; `HUSHLINE` is a working product name only**.
- Exact mechanics/state ordering: **intentionally deferred to Phase 4**.

**PHASE 3 PRODUCT THESIS = COMPLETE.**

## NEXT DESIGN HANDOFF
Proceed to **Phase 4 — Mechanical Architecture**. Create `GAME4_MECHANICS.md` and specify deterministic acoustic propagation, barrier interaction state machine, player movement/noise states, listener hearing/reaction states, doors/sources, prediction contract, encounter win/fail/recovery, difficulty/mastery variables, and exact update ordering. Do not expand scope merely to add variety; prove the locked thesis with the minimum vocabulary first.