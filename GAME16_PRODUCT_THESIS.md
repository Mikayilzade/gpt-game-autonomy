# GAME #016 — PHASE 3 PRODUCT THESIS LOCK

Date: 2026-09-03
Status: PHASE 3 COMPLETE
Working title: **ONE-WAY WORKSHOP**

## Product identity
**One-sentence hook:** Every irreversible cut creates both a product piece and a byproduct that may be the only tool/jig capable of making a later operation possible.

**Genre framing:** single-player deterministic tabletop fabrication puzzle; finite authored jobs; physical manipulation with proof-oriented logic, not simulation.

**Core fantasy:** feel clever for planning a fabrication ancestry where apparent waste becomes capability. You are not optimizing material yield or running a shop; you are reading a plan, committing irreversible cuts, and discovering how the children of those cuts become the means to finish the object.

**Target player:** PC puzzle players who enjoy compact systemic reasoning, tactile assembly, explainable consequences and multi-step planning. Accessible to players without woodworking/engineering knowledge. No arithmetic or craft expertise is prerequisite.

**Platform:** PC/Steam first; full controller path and Steam Deck/handheld readability are product requirements. Mouse supported. No touch/mobile baseline, VR, console certification or multiplayer in initial scope.

## Session shape
- Individual authored job: target ~5–15 minutes after tutorials; late cases may reach ~20 minutes.
- Natural session: 2–4 jobs / ~20–45 minutes.
- Campaign baseline: 24 canonical cases across six reasoning families.
- No timer, lives, score chase or grind required for completion.
- Immediate retry is expected; pre-commit inspection is generous, post-commit geometry is irreversible within the attempt.

## Core loop
1. **Read** the product plan, required operations and visible jig stations.
2. **Inspect** stock pieces and every legal cut socket, including deterministic child preview.
3. **Plan** which children become final parts and which must preserve typed capability for later operations.
4. **Commit** a cut; the parent ceases to exist and exactly two deterministic children become physical objects.
5. **Assign/use** children as product pieces or physical jigs/templates/spacers at compatible stations.
6. **Perform** jig-gated operations that may modify a part or create a typed witness/capability.
7. Repeat until the assembly can be **certified** or the player identifies a dead lineage and restarts.
8. Certification physically demonstrates why the finished object works and, on failure, identifies the broken requirement/ancestry without revealing the solution sequence.

## Frozen differentiator
The defining resource is **fabrication ancestry as capability**. Material subtraction is not merely cost/waste: the geometry/property of a child created by one irreversible action determines which future actions remain possible. The game must repeatedly make the player value the “wrong” side of a cut.

This differentiates the product from:
- freeform woodworking/craft simulation: no continuous sawing, skill accuracy, sanding, economy or workshop management;
- ordinary assembly puzzles: assembly order alone is insufficient; upstream cut ancestry creates downstream tools;
- optimization/factory games: no throughput automation, production line scaling or scoreboards as core;
- generic cozy repair/workshop games: narrative/shop decoration is not the product loop.

## Canonical verbs / representation ceiling
Player-facing primitive verbs remain: **inspect plan; inspect stock/children; choose a legal socket; preview split; commit cut; pick/place child; dock child in compatible jig/part station; perform guided operation; assemble; certify; restart.** Camera/navigation and UI are not puzzle verbs.

Allowed fabrication primitive families at thesis level: straight cut, diagonal cut, guided drill/mark, spacing/positioning operation, final assembly/certification. Phase 4 may formalize these but may not introduce freehand fabrication.

Typed capability vocabulary must stay small and physically motivated. Current permitted thesis-level families: dimension/length band, spacer width, straight reference edge, angle template, hole-pattern witness, availability/consumption/occupation. Phase 4 must reduce/normalize rather than proliferate them casually.

## Scope ceiling
Initial full game targets:
- exactly 24 canonical authored cases as baseline;
- 6 reasoning families × 4 cases from Round C, subject to Phase-5 validation without changing product identity;
- <=3 stock pieces per canonical late case;
- <=6 committed fabrication operations per canonical case;
- <=8 simultaneously loose child pieces;
- no continuous cut coordinates: all destructive cuts use authored, visibly embodied legal sockets;
- no real-world structural/physics simulation required for correctness;
- one compact tabletop/workbench presentation vocabulary, not a traversable workshop;
- modest reusable stock/product/jig visual kit; no huge bespoke prop catalogue;
- no procedural campaign dependency; authored certifiable jobs are baseline.

If a proposed puzzle requires violating these ceilings to be interesting, redesign the puzzle before expanding scope.

## Demo promise
A standalone ~20–30 minute demo should teach the causal thesis and end with one cross-blank capstone. Provisional content: cases 01–06 plus a curated later-style capstone, tuned after Phase 5. The player must leave the demo able to say, in ordinary language, “I had to cut that piece that way because the leftover became the tool I needed later.”

The store/trailer must lead with cut → two children → rotate apparent waste → snap into jig → finish product. Never lead with “cozy woodworking,” shop management, or generic crafting.

## Difficulty philosophy
Difficulty comes from dependency structure, not dexterity, hidden rules, tiny geometry or arithmetic. Every legal cut and its immediate deterministic children are inspectable before commitment. The challenge is forecasting future capability. Later cases add longer dependency chains, cross-blank ancestry, dual-use conflicts and derived witnesses while keeping the same verbs.

Human reasoning must outperform blind enumeration: authored jobs should expose enough plan/jig constraints to eliminate branches deductively. Phase 4 must specify certifier/proof traces and anti-bruteforce authoring rules.

## Failure / restart thesis
A committed cut is irreversible inside the current attempt because permanence is essential to the fantasy. The product must not punish experimentation with reload friction: restart/reset is near-instant, and inspection before commitment is rich. Failure explanation names the unmet operation/certification predicate and relevant lineage, but never gives the winning first move.

## Presentation thesis
Small stylized tabletop workshop, readable materials, satisfying split/snap/contact animation and sound. Physical shape/fit should carry meaning before text. Property overlays are secondary explanatory tools. Avoid photorealism because it invites freeform woodworking/physics expectations the rules intentionally do not model.

## Commercial thesis (provisional until Phase 7)
Premium finite puzzle game, no ads, energy, consumable hints, FOMO, paid retries or live-service dependence. Round-C value hypothesis: $9.99–14.99, $12.99 center, to be re-researched after mechanics/content scope is known. Demo is strategically important.

## Explicit out of scope
- multiplayer/co-op;
- freehand or continuous cutting/drilling;
- physics-based precision, structural stress, real material simulation;
- factory automation/throughput;
- shop economy, customers, crafting grind, resource harvesting;
- open world/traversable workshop;
- procedural level generation as required content;
- level editor/Workshop at baseline;
- narrative campaign requiring large dialogue/cinematic burden;
- tool durability, currencies, inventory meta, crafting recipes outside a job;
- leaderboard optimization as primary replay motivation;
- VR baseline.

## Empirical gates (implementation-stage validation, not design ambiguity)
1. Socketed cutting feels tactile/direct rather than menu-driven.
2. Six-operation ancestry remains visually readable with <=8 loose children.
3. Cold players infer most jig compatibility from physical form/feedback rather than reading abstract labels.
4. Irreversible commits create useful tension while instant restart prevents punishment.
5. Trailer/store art communicates byproduct-as-tool before generic workshop genre cues.

## Phase-3 lock statement
**ONE-WAY WORKSHOP is the canonical Game #016 concept.** Round-C losers are exclusion history and must not leak their mechanics into the selected game. Product identity, scope ceiling, target player/platform, session shape, core loop, differentiator, demo promise and out-of-scope boundaries are now explicit.

NEXT: Phase 4 Mechanical Architecture — formalize exact stock/child/cut/jig/operation state model, property grammar, legality/order, irreversible commit and restart semantics, certification/proof traces, win/dead-state logic, progression/difficulty variables, authoring constraints and adversarial anti-bruteforce rules.