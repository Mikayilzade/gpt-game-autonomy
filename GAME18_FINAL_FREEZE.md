# GAME #018 — FINAL SPECIFICATION FREEZE

Date: 2026-09-06
Game: **LOCAL TIME**
Status: **DESIGN COMPLETE = YES**
Production implementation in factory: **NO**
Migration: pending dedicated repository availability

## 0. Freeze verdict
LOCAL TIME is frozen as a premium single-player deterministic spatial scheduling / causal puzzle. A fresh implementation session can build the game without inventing important gameplay. Remaining uncertainty is empirical polish/content selection, not missing rules.

This file is the single implementation-facing authority. If an earlier Game #018 file conflicts with this freeze, this file wins. Earlier files remain rationale/history.

## 1. Authority order
1. `GAME18_FINAL_FREEZE.md`
2. `GAME18_ADVERSARIAL_REVIEW.md` for destructive-review evidence not restated here
3. `GAME18_WHOLE_GAME_SIM.md` for paper-walk evidence not restated here
4. `GAME18_TECH_SPEC.md`
5. `GAME18_COMMERCIAL.md`
6. `GAME18_UX.md`
7. `GAME18_CONTENT.md`
8. `GAME18_MECHANICS.md`
9. `GAME18_PRODUCT_THESIS.md`
10. `GAME18_TOURNAMENT.md`
11. `GAME18_RESEARCH.md`
12. factory-level `START_HERE.md`, `STATUS.md`, `GAME_INDEX.md` govern workflow/migration only.

Phase-9/10 amendments consolidated below override narrow older clauses without requiring archaeology.

## 2. Product contract
Working/shipping title until separately changed: **LOCAL TIME**.

Genre: deterministic spatial scheduling / causal puzzle in compact miniature towns.

Platform baseline: Windows PC / Steam first; mouse/keyboard and full controller path; Steam Deck 1280x800 target-quality path. No Verified claim before Valve/device validation.

Target player: systemic-puzzle players who enjoy visible cause/effect, planning and causal chains without dexterity, hidden-rule guessing, programming syntax or large simulation management.

Store hook: **Move pockets of local time around a tiny town, lining up bakeries, bridges, flowers and trains that all need different times at once.**

Core fantasy: move clock-zones, not history. Sites under different zones can experience different public semantic times simultaneously. A current condition changes when coverage changes; an earned process milestone remains earned.

Canonical identity phrase: **Different local times. Persistent consequences.**

Explicitly not: rewind/time travel, past-self clones, continuous clocks, real-time execution, hidden NPC schedules, physics placement, open-world simulation, tycoon/economy, dialogue-heavy narrative, procedural-infinite content or bespoke per-prop rule exceptions.

## 3. Canonical state model
Two player-facing truth classes are fundamental:
- **NOW / CURRENT**: derived from the current clock layout at a Resolve boundary and may become true/false freely.
- **DONE / PERSISTENT**: earned state transition/milestone; clock movement never reverses it.
- **LOCKED OUT** is a persistent bad milestone and follows the same irreversibility rule.

Time labels such as 07:55/08:00/08:05 are semantic IDs, not elapsed minutes. Labels never tick. Earlier-looking labels never rewind history.

Canonical mutable puzzle state contains only stable serializable values: case/ruleset/schema identity, beat/move/budgets, clock socket assignments, persistent site/object states, object locations, carrier state/payload, persistent flags and terminal state.

Derived CURRENT truth, coverage, objective truth, legal-placement/focus graphs and dead proofs are recomputed. Presentation/scene/animation/audio state is never puzzle authority.

## 4. Placement contract
Clocks occupy authored discrete legal sockets. Socket+footprint maps to an explicit finite set of covered logical site IDs; world geometry never decides logical coverage.

Preview shows exact legal destination, footprint, effective local labels and NOW predicates. It does **not** automatically reveal future persistent writes, fatal/winning moves or multi-beat solutions.

Two clocks may cover one site only when their time labels are identical. Different labels on one site are an illegal configuration rejected before commitment, consuming no beat/move.

Confirmed relocation to a different legal socket charges its authored move cost, default 1. Inspect/cancel/no-op placement costs 0. Multiple relocations may be planned before Resolve if budget allows.

## 5. Frozen semantic families
Base game uses exactly eight semantic families compiled into the universal transition grammar:
1. CURRENT WINDOW;
2. ONE-SHOT PROCESS;
3. ORDERED PROCESS;
4. EXPOSURE CONSEQUENCE;
5. ACCEPT / SERVICE;
6. DISPATCH / CARRIER;
7. COUPLED CURRENT EVENT;
8. PERSISTENT PUBLIC FLAG.

Art skins may vary fiction but not semantics. No arbitrary case scripts. Any future ninth family requires explicit design reopening/review.

## 6. Frozen Resolve pipeline
One successful Resolve is one deterministic boundary:
1. validate planning legality/conflicts/budgets; illegal action mutates nothing;
2. freeze immutable pre-transition snapshot S0;
3. derive effective local times and CURRENT predicates C0;
4. evaluate ADVANCE, LOCKOUT/HAZARD, ACCEPT, DISPATCH and coupled-event intents using only S0+C0;
5. reject contradictory writes as authoring/runtime assertion failure — never tie-break them;
6. atomically commit compatible persistent writes, max one persistent advance per entity per Resolve in frozen baseline;
7. carrier stage: deterministic max one public hop per carrier; newly arrived cargo cannot be accepted in the same Resolve;
8. recompute derived/current truth under unchanged layout;
9. evaluate explicit hard failure, then success, then budget/dead-state boundary;
10. increment beat and emit complete structured reason trace.

Animation visualizes already-computed results and can be sped/skipped without affecting authority.

## 7. No-placement Resolve / anti-farming amendment
A Resolve with no new placement remains legal because carrier hops, arrival/accept boundaries and objective checks may require a boundary.

However, authored content after early tutorials must not be solvable by repeatedly pressing Resolve under an unchanged clock layout to walk the same useful ordered process through multiple milestones.

Validator requirement: flag any reachable state where two consecutive no-placement Resolves under identical clock layout produce two strategically useful persistent advances on the same ordered chain. Exception requires an explicit justification tag + manual review; none is expected in normal post-Chapter-1 campaign content.

A no-placement Resolve that advances a carrier hop is meaningful. Repeated empty Resolves that change neither persistent nor carrier state never improve score and must not be required by an optimal authored solution.

## 8. Objectives, failure, dead state and recovery
Objectives use public predicates only: MILESTONE, CURRENT, OBJECT_AT, FLAG, ALL, ANY, NOT, AT_MOST_MOVES, AT_MOST_BEATS.

Success is checked at Resolve boundaries after committed transitions/handoffs. Explicit irreversible hard failure may occur only when a public bad state proves a required objective impossible and must name the violated rule/objective. Budget exhaustion checks success first.

`DEAD / No winning continuation` may be shown only when exhaustive deterministic search over the exact remaining finite action graph proves impossibility for the matching content/ruleset hash. Never use heuristic dead-state claims.

Recovery:
- Undo Placement reverses unresolved relocation and refunds its move cost;
- Undo Turn restores the exact **pre-Resolve checkpoint**;
- Restart restores authored initial canonical state;
- Replay Last Resolve is presentation-only.

Important persistence amendment: authoritative **post-Resolve active state** and **pre-Resolve Undo Turn checkpoint** are separate records. Loading after interruption never re-runs Resolve logic.

## 9. Scope ceilings
Normal campaign:
- <=3 player-controlled clocks;
- <=8 logically relevant sites;
- <=2 active carrier channels;
- <=4 semantic time labels normally;
- normally <=6 Resolves in late campaign;
- compact authored socket graphs, never giant permutation spaces.

Mastery ceiling: <=3 clocks, <=12 moves, <=8 Resolves, <=5 labels unless design is explicitly reopened.

Late difficulty must braid dependency types — irreversible prerequisite, boundary staging, persistent freeing/repurposing and final simultaneous CURRENT reservation — rather than raise entity ceilings.

## 10. Content contract and count semantics
Campaign architecture remains six chapters with Cases 01–36 as the target portfolio. Cases 01–06 are the demo/onboarding sequence.

**Shipping semantics:**
- 36 campaign cases = target, not quota;
- 30 campaign cases = minimum quality floor under current product sizing;
- M01–M08 = baseline mastery set;
- M09–M12 = reserve only, admitted only if structurally novel.

Cut weak/repetitive cases rather than invent mechanics or pad count. If 7+ campaign cases fail uniqueness/human-proof gates, reopen product sizing rather than silently shipping below 30.

Duplication watch clusters: 09/28, 17/29, 24/34, 25/27/33, 30/35. They survive only when authored dependency graphs/proof shapes are materially distinct.

Every post-tutorial case stores a 2–6 claim public `human_causal_proof`. From Case 12 onward at least one claim must eliminate a nontrivial class of legal early actions before simulation; Chapter 4+ normally requires two independent causal cuts. Difficulty based mainly on scanning near-identical sockets fails review.

## 11. Materially different route definition
Two winning routes count as materially different only after removing no-op Resolves and normalizing explicitly declared symmetric clock/entity IDs, and only if at least one holds:
- milestone partial-order DAG differs by a non-commuting precedence relation;
- carrier/destination role differs and changes a later prerequisite;
- irreversible hazard is neutralized through a different public prerequisite structure;
- final CURRENT clock-role reservation differs in a way that changes earlier dependencies.

Animation order, equivalent socket choice, interchangeable clock IDs, extra harmless Resolves or mere move-count difference do not create a new route family.

Cases 30 and 35 require solver-supported >=2 materially different route families.

## 12. Case 36 frozen capstone
Canonical structural target: **Dependency Braid**.

Required five-claim shape:
1. Garden/safety milestone must be earned before the dangerous productive footprint;
2. Bakery/process earns persistent cargo while the needed clock is still free;
3. cargo dispatches/arrives before Station acceptance/coupled event; arrival cannot accept same Resolve;
4. persistent Garden/cargo milestones free clocks for repurposing;
5. final Resolve reserves the required clocks for Bridge + Station simultaneous CURRENT event and final NOW objective.

Use one carrier baseline. **Double Hazard + Two Carriers is explicitly rejected** because it mostly scales Case 34 with bookkeeping rather than a new causal relationship.

If Dependency Braid fails empirical playtest, permitted fallback is a public choice-collapse finale using only existing families; this requires explicit design amendment before shipping.

## 13. UX / presentation contract
Player-facing canonical terms: NOW, DONE, LOCKED OUT, Resolve, and `ARRIVED — eligible next Resolve`.

Primary play screen: town diorama, objective strip, selected-detail/rule card, action rail. No timeline scrubber or rewind iconography.

Rule cards expose effective local time, persistent state, relevant public rule, NOW conditions and carrier boundary when relevant. They explain conditions, never recommended moves.

Footprints use perimeter/pattern/text/shape reinforcement, never color alone. Different-time overlap conflict shows both labels and cannot commit.

Resolve presentation follows authoritative trace: local labels/NOW -> persistent writes -> carrier hop -> objectives/terminal boundary. Expanded `What changed?` must expose **every authoritative mutation and terminal cause**, including harmful simultaneous events. Stable trace order is reproducibility, not causal priority.

Controller path uses semantic focus navigation; no pointer precision required. Combined mandatory Deck stress gate: **1280x800 + maximum text + pseudolocalization + controller-only + non-color cues + animation skip/reduced motion**. Failure is an implementation defect, not permission to shrink accessibility text.

## 14. LT01–LT06 demo contract
Free demo target 25–35 minutes, desirable median <45.

LT01: CURRENT vs persistent milestone.
LT02: safe milestone before irreversible exposure.
LT03: simultaneous different local times + conflict preview.
LT04: prepare -> dispatch/hop -> accept on later Resolve.
LT05: first unguided irreversible-shortcut reasoning + causal failure explanation.
LT06: three-clock synthesis with persistence, simultaneity, hazard and final CURRENT truth; no new grammar.

Demo completion line: `Different local times. Persistent consequences.` Demo/full carryover imports compatible LT01–LT06 progress/settings idempotently and never downgrades stronger full-game progress.

## 15. Commercial contract
Premium single-player Steam/Windows-first product. Default MSRP **US$14.99**, reviewable pre-release within $14.99–$19.99 only after polished demo/store/value evidence.

Campaign first-completion target 6–8 hours; baseline mastery adds roughly 2–4 hours depending on admitted content. Count never justifies filler.

No ads, MTX, premium currency, consumable hints, lives/energy, battle pass, daily-login economy, loot boxes, paid undo/accessibility, gameplay pre-order bonus or mandatory external account/launcher.

Steam achievements target 18–24 after content lock. Accessibility never invalidates completion/achievements/records.

Next Fest participation is one-shot strategic exposure: enter only when demo, controller/save quality, store messaging and feedback runway are ready. Do not target an event merely because it is nearest.

Localization architecture supports English plus planned FR/DE/ES-ES/PT-BR/RU/ZH-CN/JA/KO subject to budget and semantic QA. Rule translations must be human/semantic QA'd; never machine-publish unreviewed puzzle conditions.

## 16. Technical contract
Recommended runtime: pinned tested Godot 4.7.x stable, GDScript-first, with engine-light puzzle kernel. Upgrade only behind full deterministic/golden regression.

All shipping case content is declarative/versioned/non-executable. Runtime and exhaustive solver share the exact Resolve semantics. No scene callback, frame delta, physics query, RNG or iteration-order accident influences puzzle result.

Canonical state equality is structural; stable hashing is cache/diagnostic aid only. Symmetry normalization applies only to explicitly declared validated symmetry groups.

Every authoritative mutation emits structured localized `ReasonEvent` facts. Reason trace is not authority.

Content CI validates schemas/references, ceilings, reachable contradictions, solvability, shortest costs, human-proof/anti-enumeration metadata, no-op farming, route-family requirements and campaign variety.

Golden fixtures include LT01–LT06 exact canonical snapshots/traces plus at least one late synthesis/Case-36 fixture.

## 17. Save / cloud / demo-import contract
Profile saves are versioned, validated and atomic/recoverable. Write temp -> validate -> preserve/rotate valid backup -> atomic replace where supported. Corrupt current loads valid backup; if both corrupt, preserve evidence and offer fresh profile. Unsupported future schema must never be destructively downgraded/overwritten.

Machine-local graphics settings remain outside cloud progression.

Demo import is monotonic and idempotent: same/older import is semantic no-op; stronger full progress never regresses; repeated import cannot duplicate achievements; source/pre-import backups remain until validated success.

Cloud monotonic progress records may merge; **divergent active checkpoints are never silently merged**. Preserve recovery candidates and require explicit selection when needed.

## 18. Empirical gates after freeze
These do not reopen gameplay unless they fail; implementation must build the frozen baseline needed to test them.

1. >=80% first-time testers explain NOW vs DONE after LT02 without facilitator correction.
2. <=10% describe clock movement/Undo as in-fiction rewind after LT03.
3. Footprint/conflict identification at 1280x800 succeeds >=95% in targeted trials.
4. Controller-only LT01–LT06 has no focus trap/pointer precision dependency.
5. LT05 reason trace lets testers explain failure without external help.
6. Shipping baseline remains no persistent-consequence hover oracle; an explicit one-beat-preview variant may replace it only if comprehension materially improves without increased socket scanning/lower causal explanation quality, and the change is documented.
7. 36->30 quality cut and 12->8 mastery logic is applied honestly after authored fixture/playtest review.
8. Store/trailer viewers primarily describe different/local times in different places, not rewind/time travel.
9. Demo/full import passes clean install, existing save, older schema, repeated import, corrupt source and cloud-restored cases before carryover is advertised.
10. Combined Deck stress gate passes.
11. Every localized rule condition receives semantic QA against canonical English/data meaning.
12. Price $19.99 is used only if later evidence supports it; otherwise $14.99 remains default.

## 19. Implementation acceptance checklist
A dedicated implementation may not claim implementation complete until, at minimum:
- project boots and all shipping cases load from validated non-executable data;
- deterministic kernel + solver share one authoritative transition implementation;
- every shipping case solver-proves >=1 win and no reachable ambiguous write;
- LT01–LT06 golden states/traces pass;
- Case 30/35 route-family requirement passes if those cases ship;
- no-op farming validator runs on every case;
- Case 36 matches Dependency Braid or has an explicitly reviewed replacement amendment;
- NOW/DONE/LOCKED OUT and arrival-boundary UX are present;
- expanded reason trace exposes every authoritative mutation/terminal cause;
- Undo checkpoint is exact and separate from active post-Resolve state;
- save corruption/future-schema/demo-import/cloud divergence tests pass;
- mouse/keyboard/controller semantic input paths work;
- combined Deck/accessibility/pseudolocalization stress gate passes;
- demo/full upgrade path passes if advertised;
- empirical comprehension/content gates are run and recorded;
- production never adds hidden rules, rewind semantics or presentation authority.

## 20. Contradiction audit
Audit of active Phase 1–10 authority found no fatal contradiction after consolidation.

Resolved/clarified here:
- earlier `36+12` wording is superseded by **36 target / 30 floor / M01–M08 baseline / M09–M12 reserve**;
- no-placement Resolve remains mechanically legal, while unchanged-layout useful-chain farming is now a validator/content failure rule;
- post-Resolve active save and pre-Resolve Undo checkpoint are explicitly distinct;
- alternate-route claims now use normalized dependency structure;
- Case 36 is Dependency Braid, not scaled two-hazard/two-carrier complexity;
- immediate persistent-consequence preview is not shipping baseline;
- Steam/Deck/platform claims remain validation-dependent rather than promises.

No important gameplay decision remains for an implementation session to invent.

# FINAL DESIGN VERDICT
**GAME #018 — LOCAL TIME — DESIGN COMPLETE = YES.**

Migration may occur only in a dedicated repository. Until migration integrity is verified, every `GAME18_*` file in this factory is retained as a frozen **NON-ACTIVE safety archive**. It must not become canon for Game #019 or later games.
