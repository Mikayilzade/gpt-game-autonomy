# GAME #003 — BORROWED COLLISION — WHOLE-GAME SIMULATION ON PAPER

Last updated: 2026-08-20
Factory run: **13**
Phase: **9 — Whole-Game Simulation on Paper**
Product thesis through technical specification: **LOCKED / COMPLETE ON PAPER**
DESIGN COMPLETE: **NO**

This file pressure-tests the frozen Game #003 design end-to-end as a player experience and as a recoverable deterministic product. It does not add token properties, receiver families, transform families, combat, free-angle physics or production code. Earlier canonical rules remain authoritative unless this file identifies and explicitly resolves a genuine contradiction.

---

# 1. Phase-9 verdict

**PASS WITH ONE NARROW CANONICAL RECONCILIATION AND EXPLICIT PHASE-10 ATTACKS.**

Borrowed Collision can be walked coherently from first boot through DEMO01–DEMO05, C01–C34, mastery/remixes, demo import, crash recovery, Cloud conflict, keyboard/controller/Deck play and hostile input without inventing a missing core mechanic.

The core fantasy remains intact:

> A real collision creates a consequence; that consequence becomes portable; its source lineage remains meaningful; the player transforms/spends it elsewhere; the resulting world state may create another real consequence.

The whole-game walk exposes **nine major adversarial risks**, none of which currently requires a new primitive:
1. detached-arrow bookkeeping can reappear if cases overemphasize direction/magnitude matching;
2. multi-room world pickups can become backtracking chores rather than causal routing;
3. RESETTABLE/CYCLIC_WEAK sources can become ammo dispensers if reset/cycle consequences are weak;
4. self-launch can drift toward dexterity/platforming if authored lane outcomes are not visibly snapped;
5. moving receive windows can feel like timing puzzles even though mechanically step-based;
6. causal ancestry can become a debug log once lineages span several rooms;
7. 3-slot inventory can feel like an upgrade/inventory layer rather than a rare ordering constraint;
8. mastery/remixes can become threshold padding unless they force a different causal insight;
9. Act III/IV can feel cognitively repetitive even when formal reasoning tags differ, especially if many cases reduce to `preserve scarce donor, transform arrow, spend`.

One documentation contradiction is proven and resolved below:
- Phase 5 historical remix packaging says **two packs of five**;
- later Phase 7 canonical commercial/progression design freezes **three packs: 3 + 4 + 3**, still exactly 10 remixes.

**P9-R1 CANONICAL RECONCILIATION:** the later Phase-7 three-pack structure is authoritative for 1.0. The Phase-5 two-pack wording is superseded packaging history only; all Phase-5 remix validity rules (changed causal dependency, source substrate, changed insight, known solution fixture) remain authoritative. Phase 11 must include this reconciliation in final authority notes.

No mechanical Phase-4 rule is reopened.

---

# 2. First boot -> Case Board -> first interactive consequence

## 2.1 First launch

The player starts the game and receives the accessibility/input quick setup before any mandatory play. Defaults are usable immediately. The screen includes UI scale, reduced motion, impact flash/camera-shake reduction, subtitles/text event presentation, controller glyph family and hold/toggle choices.

The product must not frame these as an “easy mode.” They are presentation/input preferences and have no causal-domain effect.

The title screen then exposes `Continue`, `Case Board`, `Settings`, `Accessibility`, `Help / Rules`, `Credits`, and desktop Quit as applicable. On a fresh profile, `Case Board` is primary.

## 2.2 Case Board first impression

The board shows a compact physical/diagrammatic case selection surface, not a hub to walk around. No XP, currency, shop, token-upgrade inventory or “impact rarity” surface appears.

The first playable item is C01 in the full campaign or DEMO01 in the demo app.

**Fantasy check:** PASS. The wrapper does not compete with the consequence-transfer mechanic.

## 2.3 First visual event

Within the first minute of DEMO01/C01, a body visibly collides with a capture-enabled surface. The collision resolves first; only then does a portable impact condense at that location.

The pickup visibly carries:
- one of eight arrow orientations;
- WEAK/MEDIUM/STRONG chevron grammar;
- a source stamp identifying the donor collision;
- no numbers, rarity or ammo count language.

The first player-facing interpretation should be `this is the crash we just saw`, not `the game spawned an arrow pickup`.

**Risk gate:** if naive players call it ammo before understanding provenance, the visual/presentation metaphor is failing even if mechanics are correct.

---

# 3. DEMO01–DEMO05 — 15–25 minute complete marketing proof

The demo must prove the full sentence rather than merely show token matching.

## DEMO01 — The Crash You Keep

Sequence:
1. a STANDARD donor collision happens visibly;
2. one WEAK impact condenses;
3. player collects it through ordinary interaction;
4. a nearby R1 Ordinary Mover receiver shows compatible direction;
5. player commits spend;
6. cart moves and completes a simple objective.

What the player must learn:
- collisions can generate portable consequences;
- collection is not reflex capture;
- spending is a causal action, not firing a projectile.

Failure mode to attack later: the player thinks all collisions automatically produce loot. The capture-source affordance must make harvestability explicit.

## DEMO02 — Turn the Hit

Player gets a direction that cannot directly solve the receiver. A visible quarter-turn transform exists between source and target.

The transform preview shows exact before/after direction while preserving source stamp.

The critical lesson is:
- direction is part of the stored consequence;
- the player cannot freely rotate it;
- physical world machinery changes it.

This prevents `vector editor` interpretation.

## DEMO03 — Too Much

The player encounters a magnitude-window or fragile receiver. STRONG is accepted but harmful; MEDIUM succeeds.

A legal STRONG spend must commit and visibly break/overshoot rather than being rejected as input error. Undo restores the exact checkpoint.

This is the earliest commercial proof that magnitude is **suitability**, not a conventional power tier.

If the demo merely says `STRONG BAD` in text, it fails. The direct family consequence must be visible before/after.

## DEMO04 — Use It on Yourself

Player spends an impact through R6 Self-Launch Receiver on a visible authored launch lane. The player follows a deterministic trajectory presentation toward a canonical landing boundary.

The landing creates a genuine secondary collision. That collision emits a new impact with new lineage descended from the spent launch impact.

This is the demo's most important anti-bookkeeping moment:
- the same grammar moves the player;
- spending changes physical position;
- landing creates a new causal resource;
- the product is not a detached inventory puzzle.

## DEMO05 — Borrowed Consequence

Compact synthesis contains:
- two donor sources;
- one converter;
- one fragile/magnitude-sensitive receiver;
- one self-versus-cargo decision;
- one secondary collision opportunity;
- at least two valid baseline solution characters.

The best demo-ending `aha` is not “I matched all arrows.” It is:

> “I used one crash to move myself, and the landing crash became the safer hit I needed for the fragile mechanism.”

The end card may tease later regeneration, moving windows, multi-room routing and causal compression, but must not imply new elemental impacts or upgrades.

## Demo timing verdict

PASS on paper if:
- DEMO01–02 occupy ~5–7 minutes;
- DEMO03 lands by ~10–12 minutes;
- DEMO04 produces the secondary-lineage realization by ~15–18 minutes;
- DEMO05 closes by ~20–25 minutes for a typical new player.

If the first genuine secondary reuse occurs only after 20+ minutes, demo pacing must compress before release.

---

# 4. First 20 minutes of the full campaign

C01–C05 should feel like one escalating causal sentence rather than five disconnected tutorials.

## C01 — consequence becomes portable
One donor -> one pickup -> one receiver.

The player should be able to point backward from the held impact to the collision that created it.

## C02 — direction identity
Two receivers make direction meaningful without a converter. The player learns orientation is a property of the collision outcome, not a targeting choice.

## C03 — quarter-turn transform
The player changes direction through visible machinery. This is the first proof that a token can be **routed physically** rather than edited from UI.

## C04 — magnitude categories
WEAK/MEDIUM distinction enters before breakage. The goal is consistency, not danger.

## C05 — strong can be wrong
The first STRONG impulse is attractive and visually dramatic but damages/overshoots a fragile/window receiver. MEDIUM is the useful consequence.

### First-20-minute comprehension risks

**P9-R2 — direction/magnitude conflation.** Players may read bigger arrow body/chevrons as farther travel direction rather than strength. Phase 10 must test icon grammar under grayscale/no-audio and at Deck size.

**P9-R3 — capture-source expectation.** Once players see two successful harvests, they may expect every visible collision to emit. Capture-enabled source affordance must be teachable without turning rooms into glowing loot markers.

**P9-R4 — transform-as-UI risk.** If converter interaction feels like selecting `rotate 90°` from a menu instead of routing through machinery, the physical-consequence fantasy weakens. Presentation must retain world-device ownership.

---

# 5. First 60 minutes — complete primitive grammar becomes familiar

The first hour should introduce almost everything the player needs at the primitive level.

## C06 — reverse / mirror
Direction topology broadens. Mirror axis must be visually explicit. A player should never fail because they interpreted an icon's decorative orientation differently.

## C07 — secondary lineage
One spent impact moves R7 Chain-Producing Body, which collides elsewhere and emits a new harvestable impact.

This is the first campaign proof that a consequence can be deliberately converted into another consequence without a special `combine` crafting UI.

## C08 — two-token ordering
Inventory capacity 2 becomes meaningful. The player may leave world pickups behind rather than discard. The question is ordering, not hoarding.

## C09 — exhaustible provenance
An EXHAUSTIBLE donor looks useful early but later state shows why preserving source matters. The case remains recoverable through Undo/Restart.

## C10 — meaningful RESETTABLE donor
The reset action must visibly change route/world state. Example: resetting a compression ram re-arms a donor but closes a passage or repositions cargo.

The reset cannot be a free button beside an impact machine.

## C11 — damper
STRONG -> MEDIUM solves suitability. The damper is a physical route/device, not a generic item upgrade.

## C12 — self-launch
Self-launch becomes normal grammar. It is not introduced as a separate platforming mode.

### First self-launch experience
Player selects impact and a self-launch receiver/stance. Preview shows authored landing family, not a ballistic arc with fine aiming. Commit runs one deterministic transaction.

The action should feel physical and satisfying, but baseline success must not require reaction timing.

**P9-R5 — dexterity drift.** If players begin asking for analog aim, air control, double-jump or momentum skill, the presentation is accidentally promising a platformer. Phase 10 must protect authored-lane identity while preserving impact satisfaction.

## C13 — CYCLIC_WEAK donor
The player sees one renewable WEAK source. Its role is not “infinite ammo”; it is a stable low-strength consequence that contrasts with scarce stronger lineages.

A representative lesson: use renewable weak to reposition an intermediate cart so the scarce medium/strong donor remains available for a final receiver.

**P9-R6 — renewable-ammo perception.** If CYCLIC_WEAK looks like a token dispenser, the source/world-state link is diluted. Its cycling physical process must remain visible and causal.

## C14 — moving receiver window
The receiver has canonical movement-step windows. Pause/Step reveals states; no mid-step command is allowed.

The player should reason:
`receiver accepts at State B; I must launch the moving body so arrival aligns with B`
not:
`I need to press the button at exactly the right frame`.

**P9-R7 — timing illusion.** Even deterministic step logic may look reflex-based when animated. Phase 10 must require state labels/preview/step affordances sufficient for first-try prediction.

### First-hour verdict

PASS on paper. By C14 the player has seen:
- harvest;
- direction;
- all major transform semantics;
- magnitude suitability;
- secondary collisions;
- two-token ordering;
- exhaustible/resettable/cyclic source classes;
- self-launch;
- moving receive windows.

The game must now stop teaching new primitive grammar and earn depth through composition.

---

# 6. Act II source economy — RESETTABLE / CYCLIC_WEAK stress test

This is the first place Borrowed Collision can accidentally turn into an economy/inventory game.

## RESETTABLE healthy case

A resettable donor should have a physically meaningful restoration sequence:
- pull ram back -> donor can fire again;
- pulling ram closes temporary gate or shifts counterweight;
- player must decide whether rearming is worth changing the world state.

The new donor generation is legitimate because the source world has changed through a visible reset contract.

## RESETTABLE unhealthy case

Bad design:
- press button;
- same strong collision repeats;
- collect another identical impact;
- no route/state consequence.

This is an ammo factory and violates the non-negotiable differentiation rule.

## CYCLIC_WEAK healthy case

A visible machine repeatedly produces one WEAK donor state as part of the environment. The renewable consequence is intentionally weak and useful because:
- some receivers prefer WEAK;
- weak can reposition bodies without breaking/overshooting;
- weak can engineer a secondary medium result through a different mass/collision relation;
- using weak may preserve a scarce stronger source.

## CYCLIC_WEAK escalation exploit

Hostile player tries:
`renewable WEAK -> chain body -> collision mass interaction -> MEDIUM/STRONG -> repeat`.

If this creates a net-positive renewable strong factory without a bounded world-state cost, the content fails validation.

Technical bounded exploit search already requires this. Phase 9 confirms it is a player-facing product risk, not only a QA edge case.

---

# 7. Act III — C15–C21 consequence chains

Act III is where the product must prove it has more than a clever tutorial mechanic.

## C15 — source selection + protected state

Player has multiple usable donors. The locally obvious donor causes a protected receiver/world state to become unsafe. A less obvious collision source preserves the invariant.

The case is valid only if the choice is explained through source/aftermath, not hidden designer intent.

## C16 — chain-produced medium replaces obvious strong

The player sees a scarce STRONG donor that could force progress but cause breakage/overshoot later. A weaker source can move a chain body to create a new MEDIUM lineage that is the elegant baseline/alternate solution.

This is a crucial anti-max-force case.

## C17 — self-launch changes future donor geometry

Self-launch moves player into another room/side and landing or subsequent interaction enables a donor configuration unavailable before.

Self-launch here is not a traversal tax; it changes causal access.

## C18 — regeneration economy across two rooms

RESETTABLE donor in Room A can be rearmed only by an action that changes Room B route/state. Player must preserve ability to return or choose another chain.

The important thought is `resetting this source changes the world`, not `I need another token`.

## C19 — moving receiver + magnitude suitability

Player aligns canonical receive window with a MEDIUM/WEAK consequence. Pause/Step remains legitimate and mastery-neutral.

## C20 — inventory ordering with world pickups

Two held slots plus several persistent pickups. The player must spend/leave/retrieve in a meaningful order.

### Backtracking stress test

A bad version forces the player to walk physically through already-solved empty rooms multiple times only to retrieve a known pickup.

Phase-6 Room Overview may index previously seen stable pickups and allow presentation-compressed solved-route traversal only when canonical state is unaffected.

**P9-R8 — pickup backtracking friction.** Phase 10 must distinguish causal routing from traversal tax. Compression may remove empty travel, but it may never teleport an impact across unresolved world-state dependencies.

## C21 — Act III synthesis

Target: at least two materially different baseline solution characters.

Example A: preserve scarce strong donor, engineer medium chain.
Example B: consume strong donor but preserve alternate fragile route through different self-launch allocation.

If every player converges on one hidden sequence despite “multiple solutions” wording, content quality fails even if mechanics permit alternatives.

### Act III verdict

PASS with the largest emerging product risk being **cognitive sameness** rather than missing mechanics.

Formal tags can differ while the lived loop repeats:
`inspect donor -> transform arrow -> preserve scarce thing -> spend -> fetch next pickup`.

Phase 10 must evaluate actual reasoning transformation, not merely metadata tags.

---

# 8. Act IV — C22–C28 causal routing / multi-room pickup economy

## C22 — transform topology + donor preservation

Multi-room converter topology is only interesting when world location matters. If the same result could be achieved by opening a token editor and applying rotate/reverse operations from inventory, the case has failed the physical-routing fantasy.

## C23 — fragile cargo versus self allocation

One suitable impact can move cargo safely or launch the player toward another source. Player must reason about which world consequence creates the better future state.

This is a strong defense against arrow matching because the same token has multiple meaningful physical uses.

## C24 — reset closes another route

Healthy RESETTABLE late case: resetting source is not a cost measured in currency; it changes topology/position so another route disappears or body moves.

## C25 — chain ancestry across three rooms

A source collision in Room A produces impact A1. A1 is transformed/spent in Room B, creating collision B2. B2 emits impact B2-1, carried to Room C and spent on final receiver.

### Causal ribbon stress test

Raw ancestry may contain:
- donor event;
- output emission;
- pickup;
- transform 1;
- transform 2;
- spend;
- body motion;
- collision;
- new emission;
- pickup;
- spend;
- final state.

The default UI must compress bookkeeping and show the shortest material chain attached to the selected requirement/impact. The player can expand for full ancestry.

**P9-R9 — causal-ribbon overload.** Phase 10 must freeze a visible-node/sibling budget similar to prior factory lessons without importing another game's actual canon. The product-specific goal is that a player can explain `where this impact came from and why this receiver changed` without reading an event log.

## C26 — first 3-slot case

This is dangerous commercially and mechanically because three visible impact slots can start to feel like inventory progression.

A valid C26 must prove why two slots are insufficient for the intended ordering problem and why the third slot does not simply make the game easier.

The Case Brief can identify this case's capacity as an authored local constraint. It must not be framed as a permanent `inventory upgrade` reward.

**P9-R10 — 3-slot upgrade drift.** Phase 10 should require a specific 3-slot justification note/validator for every 3-slot case, not only content-count ceilings.

## C27 — moving windows + protected invariant

The player must synchronize a deterministic movement-step state while preserving another world condition. Pause/Step is expected, not shameful.

The case fails if animation speed changes perceived solvability or if the player must watch repeated long loops for the correct state.

## C28 — Act IV synthesis / provenance counterfactual must fail

Internal counterfactual:
> If all needed arrows were simply handed to the player at start, would the core challenge remain?

For C28 the answer must be **NO** because donor states, resets, receiver aftermath, topology or chain creation are essential.

This should be a formal pre-Phase-10 content quality gate.

---

# 9. Act V — C29–C34 mastery without new mechanics

## C29 — exhaustible vs chain-generated source

Player can consume an obvious EXHAUSTIBLE impact or engineer a chain-generated alternative. Both may baseline-clear; preservation/compression mastery favors deeper causal reuse.

## C30 — renewable weak beats scarce strong

The case must demonstrate the product thesis in one sentence:
`The weaker recurring crash is more valuable because of the world chain it enables.`

If players still choose STRONG by default, anti-max-force design has failed.

## C31 — self-launch creates only useful downstream donor

Player uses an impact on self, landing collision produces the needed consequence. This is the strongest late proof that self-launch belongs to the central grammar rather than an auxiliary movement gimmick.

## C32 — protected-state multi-solution case

Three to four rooms, multiple baseline solutions. One might consume more donors but preserve cargo; another might engineer fewer lineages but alter route state. The game accepts any final state satisfying baseline requirements.

## C33 — causal compression

A visible obvious solution uses several donors. A better understanding allows one engineered collision chain to replace multiple sources.

Baseline does not require mastery. The player should be able to finish with the obvious structure, then replay because the cleaner solution is intellectually attractive, not because progression forces it.

## C34 — final synthesis

No boss/new mechanic. It recombines:
- source selection;
- transform topology;
- suitability/fragility;
- regeneration economy;
- chain creation;
- self/world allocation;
- moving state where useful;
- protected invariant;
- bounded 2/3-slot ordering.

The ideal final thought is:

> “I don’t need more force. I need the right consequence to happen once, in the right place, so it becomes useful twice.”

C34 must remain clearable with zero optional mastery and zero remix completion.

### Act V verdict

PASS on paper. The design ends by deepening consequence reuse, not by adding token elements, combat or upgrade trees.

---

# 10. Hour-10 content-exhaustion audit

The core vocabulary is intentionally small, so formal variety is not enough. We test lived cognitive transformations.

## Strong distinct axes

1. **Source choice** — which collision should exist/be preserved?
2. **Direction topology** — where can the physical consequence be rerouted?
3. **Magnitude suitability** — why is weaker/stronger correct in this physical state?
4. **Regeneration economy** — what world state changes when a donor is recreated?
5. **Chain creation** — can one consequence create another useful consequence?
6. **Self/world allocation** — should force move the player or environment/cargo?
7. **Moving window state** — which deterministic step state is useful?
8. **Ordering** — which impact remains in world/held and in what sequence?
9. **Protected-state tradeoff** — what local action harms another requirement?
10. **Causal compression** — can one engineered chain replace several obvious sources?

## Highest-risk cognitively flat patterns

### Flat pattern A — “find correct arrow”
Even with provenance labels, repeated direction/band receiver matching will feel like socket bookkeeping.

Mitigation already in canon: from C15 onward donor/world-state relevance mandatory. Phase 10 must evaluate actual case spines, not only notes.

### Flat pattern B — “preserve scarce source” repeated
Exhaustible donor preservation is powerful but can become the answer to too many cases. Act III/IV should rotate when preservation is central versus chain creation/self-allocation/moving-state.

### Flat pattern C — “walk back for pickup”
Multi-room complexity can falsely inflate thinking time via traversal. Solved-route compression is allowed only when canonical state is unaffected.

### Flat pattern D — “converter chain”
Quarter-turn/reverse/mirror/damper can create visually different chains that are cognitively identical. Content validator should flag required chains >3 transforms unless topology itself is the lesson; Phase 5 already contains this guardrail.

### Flat pattern E — “secondary collision every time”
CHAIN_CREATION is the strongest hook expansion but cannot become a mandatory trick in every mature case. Some late solutions should win through regeneration, allocation, protected state or moving windows without a new lineage being the key.

## Consecutive-window audit

The representative campaign spine passes the **formal** Phase-5 tag diversity rules, but Phase 9 cannot prove lived cognitive diversity without authored final case layouts.

Therefore Phase 10 must add a **reasoning-isomorphism attack**:
- for each consecutive 3-case window from C15 onward, write one-sentence solution logic stripped of theme/nouns;
- for each 5-case window, cluster by actual dependency graph pattern;
- reject/repair windows where metadata tags differ but the same causal skeleton solves most cases.

This is an empirical/content-authoring gate, not a new mechanic.

---

# 11. Baseline completion / mastery replay

## Baseline philosophy

The player can experiment freely. Undo/Restart do not damage completion legitimacy. A legal bad spend commits and can teach.

The completion screen emphasizes final state and causal story, not trial count.

## M1 Causal Compression replay

Representative late case baseline:
- use donor A to open route;
- donor B to move cart;
- donor C to trigger final gate.

Mastery insight:
- use donor A on chain body;
- secondary collision produces lineage that moves cart and sets up final gate;
- one source lineage replaces two obvious sources.

This is valid because the mastery asks for a different causal idea, not merely one fewer button press.

## M2 Preservation replay

Baseline may consume an exhaustible donor. Preservation mastery requires a different source/chain route that keeps it available.

Invalid version: same solution except do one unnecessary step less.

## M3 Resource Discipline replay

A valid case might let STRONG solve baseline but create collateral state. Mastery uses CYCLIC_WEAK or a chain-generated medium consequence and leaves STRONG unspent.

## M4 Stable Causality replay

Only meaningful where moving/temporal state exists. Example: final receiver and protected body remain in required state through a bounded moving sequence. It cannot be an arbitrary wait-N-cycles condition.

### Mastery verdict

PASS if every authored mastery includes `mastery_distinction_note` and Phase 10 compares known baseline versus mastery solution character.

---

# 12. Remix packs — canonical reconciliation + changed insight test

## P9-R1 packaging reconciliation

Final 1.0 remix packaging follows Phase 7:
- **R-A Reclaimed Impacts: R01–R03**, unlock C14;
- **R-B Chain Revisions: R04–R07**, unlock C28;
- **R-C Borrowed Department: R08–R10**, unlock C34.

The earlier Phase-5 `two packs of five` packaging is superseded. The exact total remains **10**.

## Pack A changed-insight examples

R01: source/provenance variant on early substrate where original obvious donor is now exhaustible and alternate source matters.

R02: magnitude/fragility variant where original strong path now creates protected-state failure; weaker chain required.

R03: self-launch/transform topology variant where impact must move player first rather than cargo.

Each must change causal dependency, not simply thresholds.

## Pack B examples

R04–R07 should cover at least three actual transformations among regeneration economy, chain creation, moving window, inventory ordering, protected state, self/world allocation.

A remix fails if source solution transfers after only arrow-direction substitution.

## Pack C examples

Expert remixes may use full grammar but cannot add a fourth slot, new transform or new token property.

At least one supports 3+ materially different baseline solution characters.

### Remix verdict

PASS with P9-R1 reconciliation. Phase 10 must compare each remix dependency graph against its source substrate.

---

# 13. Demo -> full-game import simulation

## Compatible import

Demo profile stores settings and durable demo-node completion records. Full game reads through explicit versioned mapping.

Safe results:
- settings import where compatible;
- mapped tutorial tags/import facts apply monotonically;
- no stronger full-game progress is removed;
- repeating same receipt is idempotent;
- demo achievements are not independently granted in a way that duplicates platform reward semantics.

A demo node does **not** automatically clear a campaign case merely because it teaches the same rule. Equivalence requires explicit mapping.

## Incompatible active demo state

If an unfinished demo session uses incompatible content/rules version:
- do not synthesize it into full game;
- preserve compatible durable facts/settings;
- explain that the unfinished demo case cannot be resumed safely;
- allow full-game canonical case start.

**Verdict:** PASS. No gameplay design gap.

---

# 14. Save interruption / corruption / Cloud simulations

## 14.1 Quit during pre-commit preview

No semantic command committed. Resume from previous durable state. Preview disappears.

## 14.2 Crash during collision chain

Partial chain is not canonical persistence. Recovery loads last completed durable transaction checkpoint.

The player may have visually seen part of animation before crash, but after recovery the command is either fully durable or absent according to the write protocol; no half-consumed impact/half-created lineage state exists.

## 14.3 Crash immediately after durable transaction but before animation completes

Recovery loads the resolved state. Causal ribbon/history can explain the last transaction even if animation was not seen.

## 14.4 Corrupted primary save

Checksum/format validation rejects it. Loader evaluates validated temp/backup generations and chooses newest valid compatible generation. Original corruption evidence is not silently overwritten before recovery.

## 14.5 Profile Cloud merge

Durable progression facts merge monotonically:
- baseline clears union;
- tutorial tags union;
- mastery records union where compatible;
- remix unlocks derive from merged clears;
- demo receipts union.

There is no currency or mutable power state requiring conflict arithmetic.

## 14.6 Active-case descendant

Same session + same versions + one command history is exact prefix of the other + shared checkpoint hashes match -> keep descendant.

## 14.7 Divergent active-case branches

Never synthesize. Preserve/select one according to platform conflict UX where candidates available; profile progress remains separately merged.

Player-facing text uses case name/progress, not hash/generation jargon.

**Persistence verdict:** PASS on paper.

---

# 15. Input-path simulations

## Mouse + keyboard

Complete path exists for:
- traversal/focus;
- collect;
- impact selection;
- receiver/transform selection;
- snap orientation;
- inspect provenance/causal ancestry;
- Undo/Redo;
- Pause/Step;
- Case Board/settings/help;
- room overview/pickup index;
- self-launch.

No free-angle drag is required.

## Keyboard-only

Deterministic authored focus graph moves between world candidates. Focus ordering is independent of camera zoom/UI scale. The player can cycle nearby receiver/transform candidates and select orientations with discrete keys.

Potential risk: a dense room with bodies, pickups, transforms and receivers may make `next focus` cognitively unpredictable even if deterministic.

**P9-R11 — focus graph usability.** Phase 10 must require authored/focus-validation examples for dense multi-room late cases, not only reachability.

## Controller-only

Controller actions map semantically; no virtual mouse. D-pad/stick navigates traversal/focus, buttons collect/confirm/cancel/inspect, bumpers/triggers cycle impacts/receivers/history according to context.

Context-sensitive bindings must always display current glyph/action name so `cycle receiver` cannot unexpectedly become `change room` mid-flow.

## Steam Deck

1280×800 layout preserves world dominance, compact impact belt, slide-over case rail and inspection card. Three-slot cases remain readable without a full-screen inventory.

### Input verdict

PASS on paper, with focus/navigation ambiguity as the primary Phase-10 attack.

---

# 16. Accessibility / presentation invariance simulations

## No audio

All collision eligibility, magnitude, direction, breakage, source class, receive-window and causal results remain visible through shape/text/pattern/state.

## Reduced motion

Body interpolation/camera shake can be reduced. Canonical start/end boundaries and collision consequence remain legible as discrete transitions.

## Slowdown

Slowdown changes presentation speed only. It does not create more movement states, larger receive windows or different collision outputs.

## Pause/Step

Player can reveal canonical movement steps one by one. They cannot issue mid-step commands or alter already-decided collision outcome.

## Broken remap recovery

`Reset Controls` must remain reachable through a guaranteed fallback path. This is a technical/UX acceptance requirement.

## UI scaling

Impact belt, direction arrows, magnitude chevrons, provenance/source stamp and receiver compatibility must remain distinguishable at supported scale and Deck layout.

**Accessibility verdict:** PASS on paper.

---

# 17. Hostile / unusual behavior simulations

## 17.1 Duplicate collect command spam

Semantic command ID + expected pre-state hash/revision prevents duplicate collection. First success changes impact availability; duplicates become already-applied/stale and create no second held item.

## 17.2 Duplicate spend spam

First committed spend consumes impact. Repeated same command cannot consume/create again. No duplicate collision chain.

## 17.3 Repeated RESETTABLE reset attempts

Reset is a semantic command with visible state precondition. Only valid source state increments donor generation. Repeated/stale reset cannot increment generation repeatedly without completing the world reset contract.

## 17.4 Inventory full harvest

Collision still emits one stable world pickup; capacity does not suppress lineage emission. Player can return later. No auto-discard baseline.

This avoids hidden resource loss but increases pickup/backtracking risk P9-R8.

## 17.5 Identical-looking impacts with distinct lineage

Two EAST/MEDIUM impacts may have different sources. Belt must retain provenance stamps. Mechanics only use lineage where source/provenance rules require it; visual sameness cannot silently erase source identity.

## 17.6 Transform loops

Player can route impact through quarter-turn/reverse/mirror repeatedly. This never duplicates and damper never increases magnitude.

Content must not require tedious cycling as solution difficulty. A player may waste time, but no exploit appears.

## 17.7 Intentionally broken receiver

Legal adverse STRONG spend breaks fragile receiver. State commits. Player may continue if alternate completion remains or receive dead-end notice if proven. Undo/Restart restores exact state.

## 17.8 Self-launch to bad node

Legal launch may strand player in a dead-end. No health system. If completion impossible, deterministic dead-end proof may offer Undo/Restart.

## 17.9 Repeated Undo/Redo branching

Undo restores checkpoint. Redo restores exact branch while intact. New accepted command after Undo truncates active redo branch. Old branch cannot coexist canonically and duplicate lineage.

## 17.10 Room hopping

Ordinary traversal does not advance autonomous bodies unless a frozen case rule explicitly creates a movement transaction. Therefore room hopping cannot farm collision outputs or alter receive windows by wall-clock time.

## 17.11 Pause spam / animation replay

No domain mutation. One lineage emission max remains intact.

## 17.12 Save/load around world pickup

World pickup availability and lineage-emitted state are both canonical. Reload cannot cause collision to emit again merely because pickup exists or was collected.

### Hostile-behavior verdict

PASS mechanically. The remaining issues are UX friction and content-exploit validation rather than undefined state semantics.

---

# 18. Product-identity dilution audit

Test each major subsystem against the non-negotiable rule.

- **Collision resolution:** directly creates consequence; PASS.
- **Portable impact:** stores resolved consequence + lineage; PASS.
- **Converters/damper:** physically route/alter consequence without free vector editing; PASS.
- **Receiver aftermath:** consequence changes world; PASS.
- **Self-launch:** spends consequence on player and can create new collision; STRONG PASS.
- **Donor regeneration:** PASS only when world-state recreation matters.
- **World pickups / small inventory:** PASS if they remain consequences in space, not generic ammo inventory.
- **Multi-room routing:** PASS if physical access/provenance matters; FAIL if only fetch distance increases.
- **Moving windows:** PASS if canonical receiver state matters; FAIL if presentation implies twitch timing.
- **Mastery:** PASS when it rewards causal compression/preservation/stable consequence; FAIL if raw counts/times.
- **Remixes:** PASS when causal dependency changes; FAIL when only threshold/direction changes.
- **Case Board/progression:** neutral/supportive.
- **Achievements/commercial layer:** neutral if no grind/currency.
- **Save/Cloud/input/accessibility:** neutral and rule-preserving.

### Identity verdict

**STRONG PASS, but content authoring must repeatedly prove provenance/world-state relevance.**

The biggest existential risk is not that the mechanics contradict the thesis; it is that authored cases may underuse the thesis and become arrows-in-sockets.

---

# 19. Canonical contradiction / repair register

## P9-R1 — Remix pack structure conflict — RESOLVED

Conflict:
- Phase 5 historical section: two packs of five;
- Phase 7 later canonical structure: three packs 3/4/3.

Resolution:
- Phase-7 three-pack structure wins for 1.0;
- exact total remains 10;
- Phase-5 validity/data rules remain;
- Phase 11 must record this explicitly.

No gameplay mechanic changes.

## No other proven contradiction requiring reopen

The following remain Phase-10/implementation empirical attacks, not contradictions:

### P9-R2 — Direction/magnitude visual conflation
Test Deck/grayscale/no-audio comprehension.

### P9-R3 — Capture-source expectation
Ensure harvestable collision affordance is learned without loot-glow clutter.

### P9-R4 — Transform-as-menu drift
Physical converter ownership must remain visually causal.

### P9-R5 — Self-launch dexterity drift
Prevent presentation/input from promising free platforming.

### P9-R6 — CYCLIC_WEAK ammo-dispenser perception
Source process/world context must remain visible.

### P9-R7 — Moving-window timing illusion
State-based reasoning must remain legible independent of animation speed.

### P9-R8 — Multi-room pickup backtracking
Separate causal routing from empty traversal tax; compress only solved state-invariant routes.

### P9-R9 — Causal-ribbon overload
Freeze a product-specific default visible material-chain budget in Phase 10.

### P9-R10 — 3-slot upgrade drift
Every 3-slot case needs explicit justification that it creates ordering rather than convenience/power.

### P9-R11 — Dense focus graph usability
Reachability alone is insufficient; navigation must be predictable to humans.

### P9-R12 — Formal-tag versus lived-reasoning repetition
Run reasoning-isomorphism audit across every consecutive C15+ window and remixes.

### P9-R13 — Mastery distinction
Compare baseline and mastery solution character; reject threshold shaving.

### P9-R14 — Remix dependency distinctness
Compare source/remix causal dependency graphs, not metadata claims alone.

---

# 20. Phase-9 acceptance checklist

- **P9-01** First boot exposes accessibility before mandatory gameplay: **PASS**
- **P9-02** Fresh profile reaches Case Board without hub/cinematic dependency: **PASS**
- **P9-03** First collision visually precedes portable impact creation: **PASS**
- **P9-04** First impact remains attributable to a real source collision: **PASS**
- **P9-05** DEMO01 proves consequence-as-resource rather than ammo: **PASS ON PAPER**
- **P9-06** DEMO02 proves physical direction transformation without free vector editing: **PASS**
- **P9-07** DEMO03 proves stronger-not-always-better through legal adverse consequence: **PASS**
- **P9-08** DEMO04 proves self-launch uses same consequence grammar: **PASS**
- **P9-09** DEMO04 landing can create genuinely new lineage without duplication: **PASS**
- **P9-10** DEMO05 includes secondary reuse before demo end: **PASS ON PAPER**
- **P9-11** Demo target remains 15–25 minutes: **PASS / EMPIRICAL TIMING GATE**
- **P9-12** C01–C05 teach impact, direction and magnitude without numbers: **PASS**
- **P9-13** C06 mirror/reverse can be represented with explicit physical axes: **PASS**
- **P9-14** C07 secondary lineage is coherent and bounded: **PASS**
- **P9-15** C08 two-slot ordering does not require discard inventory: **PASS**
- **P9-16** C09 exhaustible donor provenance matters: **PASS**
- **P9-17** C10 RESETTABLE donor requires meaningful world reset contract: **PASS**
- **P9-18** C11 damper remains physical transform, not upgrade: **PASS**
- **P9-19** C12 self-launch has deterministic authored-lane semantics: **PASS**
- **P9-20** C13 CYCLIC_WEAK can remain non-escalating under validator contract: **PASS / EXPLOIT GATE**
- **P9-21** C14 moving receiver is state-based, not frame-based: **PASS**
- **P9-22** First 60 minutes can teach full primitive grammar without new token properties: **PASS**
- **P9-23** Act III source/provenance reasoning is mechanically available: **PASS**
- **P9-24** Act III can make MEDIUM/WEAK strategically superior to STRONG: **PASS**
- **P9-25** Act III multi-room pickups remain persistent when inventory is full: **PASS**
- **P9-26** Empty solved-route traversal may be presentation-compressed without state teleportation: **PASS WITH UX REVIEW**
- **P9-27** C21 supports target of materially distinct baseline solutions: **PASS AS CONTENT OBLIGATION**
- **P9-28** Act IV transform topology remains physical-world topology: **PASS**
- **P9-29** Self-versus-cargo allocation creates a distinct causal decision: **PASS**
- **P9-30** Reset can close/change routes without creating currency economy: **PASS**
- **P9-31** Three-room lineage ancestry remains mechanically exact: **PASS**
- **P9-32** C26 three-slot capacity is case-local rather than permanent upgrade: **PASS / JUSTIFICATION GATE**
- **P9-33** C27 Pause/Step preserves moving-window deterministic outcome: **PASS**
- **P9-34** C28 provenance counterfactual test is meaningful: **PASS**
- **P9-35** Act V adds no new primitive: **PASS**
- **P9-36** Renewable WEAK can outperform scarce STRONG through existing rules: **PASS**
- **P9-37** Self-launch can be essential to create downstream donor without platformer rules: **PASS**
- **P9-38** C33 causal-compression mastery can reward new insight: **PASS**
- **P9-39** C34 baseline ending requires zero mastery/remix completion: **PASS**
- **P9-40** Hour-10 diversity has ten frozen reasoning axes: **PASS AS ARCHITECTURE**
- **P9-41** Formal metadata alone is insufficient to prove lived diversity: **PHASE-10 ATTACK REQUIRED**
- **P9-42** M1 mastery differs from raw command count: **PASS**
- **P9-43** M2 preservation can require alternate causal route: **PASS**
- **P9-44** M3 discipline does not become spendable currency economy: **PASS**
- **P9-45** M4 stable causality uses real moving state rather than waiting: **PASS**
- **P9-46** Remix total remains exactly 10: **PASS**
- **P9-47** Remix packaging conflict is resolved to Phase-7 3/4/3 packs: **PASS / P9-R1**
- **P9-48** Remix changed-dependency rule survives reconciliation: **PASS**
- **P9-49** Compatible demo import is monotonic/idempotent: **PASS**
- **P9-50** Demo similarity does not auto-clear campaign case: **PASS**
- **P9-51** Incompatible active demo state is not synthesized: **PASS**
- **P9-52** Pre-commit quit cannot mutate domain: **PASS**
- **P9-53** Crash during collision chain restores last durable transaction boundary: **PASS**
- **P9-54** Durable post-transaction state can recover even if animation was incomplete: **PASS**
- **P9-55** Corrupt primary can recover from newest valid compatible generation: **PASS**
- **P9-56** Profile Cloud merge is monotonic: **PASS**
- **P9-57** Active-case descendant selection requires exact command/hash ancestry: **PASS**
- **P9-58** Divergent active-case branches are never synthetically merged: **PASS**
- **P9-59** Mouse+keyboard path is complete: **PASS**
- **P9-60** Keyboard-only path is mechanically complete: **PASS / USABILITY GATE**
- **P9-61** Controller-only path is mechanically complete: **PASS / CONTEXT-GLYPH GATE**
- **P9-62** Steam Deck layout can preserve 2–3 impact identity without inventory screen: **PASS ON PAPER**
- **P9-63** No-audio mode preserves complete causal information: **PASS**
- **P9-64** Reduced-motion mode preserves discrete consequence identity: **PASS**
- **P9-65** Slowdown cannot alter domain result: **PASS**
- **P9-66** Pause/Step cannot introduce mid-step commands: **PASS**
- **P9-67** Duplicate collect/spend commands are idempotent: **PASS**
- **P9-68** Repeated reset cannot increment donor generation without valid reset contract: **PASS**
- **P9-69** Inventory-full collision still emits exactly one persistent world pickup: **PASS**
- **P9-70** Two identical-looking impacts can preserve distinct lineage/provenance: **PASS**
- **P9-71** Transform loops cannot duplicate/increase force: **PASS**
- **P9-72** Legal breakage commits and remains recoverable: **PASS**
- **P9-73** Room hopping does not advance autonomous collisions by wall clock: **PASS**
- **P9-74** Save/load cannot duplicate an emitted lineage: **PASS**
- **P9-75** Product identity remains consequence reuse from demo through C34: **STRONG PASS**
- **P9-76** Production implementation has not started in factory: **PASS**

---

# 21. Phase closure

Phase 9 is **COMPLETE ON PAPER**.

No missing core rule was discovered. The only genuine canonical conflict is the remix-pack packaging mismatch, resolved by making the later Phase-7 three-pack structure authoritative while retaining Phase-5 remix validity/data requirements.

**DESIGN COMPLETE remains NO.**

The next stage must be adversarial rather than additive. It should try to destroy the design under lived-repetition, exploit, UX, persistence and implementation ambiguity lenses and turn the P9-R* risks into either canonical repairs or explicit empirical gates.

## NEXT PHASE

Execute **Phase 10 — Adversarial Review** with at least these destructive lenses:
1. detached-arrow/vector-bookkeeping identity collapse;
2. direction/magnitude/capture-source comprehension at Deck/no-audio/reduced-motion conditions;
3. max-force dominance and renewable-source escalation;
4. donor reset/ammo-factory exploits;
5. transform-loop/converter busywork;
6. multi-room pickup/backtracking friction and solved-route compression safety;
7. self-launch platformer/dexterity drift;
8. moving-window timing illusion;
9. 3-slot inventory/upgrade drift;
10. causal-ribbon ancestry overload;
11. keyboard/controller focus predictability;
12. reasoning-isomorphism/content exhaustion across C15–C34;
13. mastery distinction versus threshold shaving;
14. remix source/dependency distinctness;
15. save/lineage duplication, Cloud divergence and transaction recovery;
16. content-authoring/QA burden and ambiguous simultaneous collisions;
17. demo/commercial promise versus actual 15–25 minute experience;
18. implementation ambiguity under a fresh-session read.

Resolve every P9-R* item or explicitly gate it. Reopen only the smallest canonical phase when a true contradiction is proven.