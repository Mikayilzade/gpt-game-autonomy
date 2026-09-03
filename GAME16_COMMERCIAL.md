# GAME #016 — PHASE 7 ECONOMY / RETENTION / COMMERCIAL MODEL

Date: 2026-09-03
Status: PHASE 7 COMPLETE
Working title: **ONE-WAY WORKSHOP**
Authority: `GAME16_UX.md`, `GAME16_CONTENT.md`, `GAME16_MECHANICS.md`, `GAME16_PRODUCT_THESIS.md` and prior active Game #016 authorities.

## 0. Commercial objective
ONE-WAY WORKSHOP is a finite premium puzzle game. Retention comes from wanting to understand the next dependency structure, not from currencies, streaks, daily tasks, grades, grind, random rewards, shop upgrades or artificial scarcity.

Phase 7 does not add puzzle mechanics. It freezes campaign access, demo carryover, hints, achievements, pricing hypothesis, Steam feature assumptions, replay boundaries and monetization exclusions so Phase 8 can specify persistence and implementation contracts deterministically.

---

# 1. September-2026 market/value evidence
Fresh checks are directional, not sales forecasts.

- **A Little Perspective** (released 2026-04-03) is $14.99 on Steam, has a demo, Steam Cloud/achievements/Deck support and advertises 200+ puzzles. This demonstrates that a polished single-idea puzzle can occupy $14.99, while also creating a very high raw-content-count comparison ONE-WAY WORKSHOP should not try to match.
- **Outpacked** (released 2026-04-01) is $7.99, has a demo, 61 levels, achievements, editor and Workshop. It anchors the low end for a compact authored logic product with substantially more nominal levels.
- **Walk The Frog** (released 2026-05-21) is $12.99 and has a demo; although structurally different, it supports the existence of a $12.99 indie puzzle/casual price point.
- Current demos vary greatly in size: e.g. Outpour's May-2026 demo advertises 30+ puzzles / ~1.5 hours, while other puzzle demos expose one area. Therefore demo value is not judged by case count alone, but ONE-WAY WORKSHOP's proposed 20–30 minute slice must produce a complete causal aha rather than feel like a tutorial stub.
- Steamworks currently recommends optional launch discounts around 10–15%, lasting 7–14 days. A 20%+ discount can trigger wishlist notifications, but that is not a reason to distort launch pricing.
- Demo-to-full transfer is common enough to be a player expectation when promised, but 2026 examples also show that separate demo/full save plumbing can fail or require manual work. ONE-WAY WORKSHOP therefore treats import as a tested product contract, not marketing copy added late.

**Implication:** compete on density, tactile presentation and unusually strong multi-step authored reasoning, not on “200 puzzles” or Workshop-generated volume.

---

# 2. Price and value hypothesis

## 2.1 MSRP
**Frozen working MSRP for validation: USD $12.99.**

Allowed pre-release adjustment band: **$9.99–14.99** without reopening mechanics.

$12.99 is preferred because:
- 24 canonical cases target roughly 5–20 minutes each and are designed as dense multi-step authored jobs rather than micro-levels;
- the tactile 3D workbench, controller/Deck path, certifier, lineage visualization and polished physical feedback carry production/value beyond a minimal abstract puzzle;
- $14.99 would place the product directly beside puzzle games advertising much larger raw counts and therefore requires unusually strong playtest length/presentation evidence;
- $9.99 remains a fallback if median full-campaign playtime/value perception is materially below target.

This is a positioning hypothesis, not a revenue guarantee.

## 2.2 Launch discount
Baseline: **10% launch discount for 7 days**, configurable to 10–15% if release marketing context justifies it. Do not exceed 15% at launch absent a concrete commercial reason. This matches current Steamworks guidance and preserves price credibility.

## 2.3 Value gate
Before store price is finalized, blind playtest evidence should support:
- median first-clear campaign time **>=4.5 hours**, target **5–7 hours**;
- no more than 4 of 24 cases independently described as filler/redundant by a material share of testers;
- late families OW17–OW24 still produce new reasoning sentences rather than longer versions of OW01;
- demo players can identify the byproduct-as-tool hook without being told the marketing sentence.

If median campaign time is <4.5h but quality is strong, prefer $9.99–11.99 or strengthen/rewrite weak cases inside frozen mechanics. Do **not** add grind/filler to defend $12.99. If campaign time exceeds ~8h because of confusion/restart friction rather than reasoning pleasure, fix UX/hints rather than raising price.

---

# 3. Campaign progression contract

## 3.1 Structure
The canonical campaign is six visible work-order trays, one per reasoning family:
- Tray I: OW01–OW04 Immediate Byproduct
- Tray II: OW05–OW08 Property Choice
- Tray III: OW09–OW12 Delayed Lineage
- Tray IV: OW13–OW16 Cross-Blank Ancestry
- Tray V: OW17–OW20 Dual-Use Conflict
- Tray VI: OW21–OW24 Derived Witness Relay

This is **tiered with bounded branching**, not fully linear and not an open hub.

## 3.2 Exact unlock rules
- New campaign: only OW01 unlocked.
- Clearing OW01 unlocks OW02 and OW03.
- Clearing **either** OW02 or OW03 unlocks OW04; both remain available.
- Clearing OW04 unlocks OW05 and Tray II.
- Within each later tray, case `A` (05/09/13/17/21) unlocks first.
- Clearing tray case A unlocks B and C in parallel.
- Clearing **both B and C** unlocks D.
- Clearing D unlocks the next tray's A.
- OW24 is the final canonical certification and campaign-complete gate.

Thus exact later pattern is:
`05 -> {06,07} -> 08 -> 09 -> {10,11} -> 12 -> 13 -> {14,15} -> 16 -> 17 -> {18,19} -> 20 -> 21 -> {22,23} -> 24`.

Reason: players receive limited choice when stuck, but cannot skip prerequisite concepts such as `EDGE`, diagonal witnesses, cross-root dependency, consumption conflict or derived qualification.

## 3.3 Completion semantics
A case clear is permanent profile progress. Replaying or restarting never removes it. Campaign completion means all prerequisite chain gates through OW24 are cleared; because D requires B+C in each tray and later trays depend on D, this necessarily means **all 24 canonical cases cleared**.

No stars, grades, par moves, medals or completion percentages beyond simple `X/24 cleared`.

---

# 4. Demo contract and exact full-game import

## 4.1 Demo content/state
Demo contains only:
- OW01
- OW03
- OW05
- D1 demo capstone (reduced OW13-derived configuration, not campaign case #25)

Demo progression is linear: `OW01 -> OW03 -> OW05 -> D1`.

Demo profile stores:
- schema version;
- stable anonymous profile/save id;
- clear flags for OW01/OW03/OW05;
- `demo_capstone_cleared`;
- accessibility/control/settings;
- optional tutorial-prompt completion flags;
- no achievement grants;
- no in-progress attempt imported into retail.

## 4.2 First full-game import
On full-game launch, if compatible demo data exists, show once:
**Demo progress found — carry your completed work orders and settings into the full game?** `Import` / `Start fresh` / `Decide later`.

Import is **non-destructive and idempotent**. Demo data remains untouched.

Exact merge into an empty retail profile:
- OW01 clear -> retail OW01 cleared;
- OW03 clear -> retail OW03 cleared;
- OW05 clear -> retail OW05 cleared **only as a clear record**, but it does not bypass campaign prerequisites;
- D1 clear -> profile `demo_capstone_seen=true`; D1 never marks OW13 clear;
- settings/tutorial preferences copy where supported;
- retail unlocks are recomputed from retail prerequisite rules, never copied from demo menu state.

Therefore a player who cleared the entire demo starts retail with OW01, OW03 and OW05 recorded as cleared, **OW02 and OW04 available according to prerequisites**, and must clear OW04 before normal Tray-II progression can advance. When OW05 later becomes reachable it is already cleared, so its downstream B/C unlock fires immediately. The player never has to replay demo cases, but also never skips OW02/04 teaching gates.

## 4.3 Merge into existing retail progress
If the player chooses import after starting retail:
- clear flags merge by logical OR;
- accessibility/settings use an explicit choice: `Keep full-game settings` (default) or `Use demo settings`;
- tutorial-completion flags merge by OR;
- no retail clear flag, achievement, setting or save slot is deleted;
- unlock graph is recomputed after merge;
- importing the same demo repeatedly produces no further state change.

## 4.4 Import failure/recovery
A corrupt/incompatible demo save must never block retail boot. Offer `Could not import demo progress` + Retry / Continue without import. Keep a local pre-import retail backup until one successful retail save occurs after merge.

Phase 8 must define app/save paths and Steam Cloud conflict handling. The product promise is **automatic in-game detection/import on supported same-device/account installs; no player file-copy procedure may be the designed path**. If reliable Steam/Deck transfer cannot be validated before release, remove the carryover marketing promise rather than ship a fragile manual procedure.

---

# 5. Hint system — reasoning support, never move solver

## 5.1 Unlock timing
Hints become available after the player has:
- spent **3 minutes** in the current attempt after its first fabrication commit, **or**
- restarted the same uncleared case twice,
whichever occurs first.

A global accessibility option `Hints always available` removes this wait with no penalty.

## 5.2 Three escalation levels
Hints are authored per canonical case and reveal only contradiction/proof structure.

**H1 — Goal focus:** restates one important future requirement in causal language. Example: `The brace will eventually need a Diagonal A guide.`

**H2 — Conflict class:** identifies the planning relationship, not a move. Example: `The piece that can guide that operation may be created before the brace itself.`

**H3 — Proof boundary:** identifies a necessary property/resource class that must survive a stage, but never names an exact cut socket, exact stock-first move or complete sequence. Example: `Before making the rail, make sure some available child can still provide a Short span after the next commit.`

Strict rule: **no hint may name the correct current cut socket or provide a sequence of commits.** If an authored H3 would uniquely identify a move solely because only one legal action exists, rewrite the hint to explain the contradiction the player should inspect instead.

Hints have no currency, cooldown, score penalty or achievement penalty. They are reviewable after reveal. Certifier/dead-state diagnostics remain separate and do not automatically consume/reveal hints.

## 5.3 Hint empirical gate
Blind tests must show H1/H2 usually restore productive reasoning without solving the case. If >25% of testers report H3 as equivalent to “the answer,” rewrite case hint text/structure before launch.

---

# 6. Difficulty, assists and accessibility
There are **no difficulty modes that alter puzzle truth** at baseline. Every player solves the same deterministic jobs.

Allowed assists are information/interaction assists only:
- Hints always available;
- Persistent Guidance;
- high-information capability overlay;
- stronger compatible-target emphasis;
- longer/shorter/no-hold commit confirmation alternatives already frozen in UX;
- text/UI scaling, reduced motion, remapping and other Phase-6 accessibility options.

No assist:
- changes cut outputs;
- adds stock;
- removes a mandatory operation;
- reverses a committed cut;
- grants a solved case automatically.

Using accessibility or hints never blocks achievements or changes completion labels. If post-launch accessibility testing proves one frozen interaction is unnecessarily exclusionary, input/presentation may be improved without creating a punitive “assist mode” badge.

---

# 7. Replay and optional challenge boundary
Baseline replay consists of:
- replay any cleared case from its tray;
- seek another valid solution family where the case supports one;
- inspect the post-clear causal recap of the player's own solution;
- optional `Reset campaign progress` behind confirmation, never required.

**Rejected:** move par, time par, score, material-efficiency grade, no-hint grade, daily challenge, random jobs, endless mode and leaderboards. These incentives would reward optimization/brute repetition instead of the one-way planning thesis or would require content/generation systems outside scope.

No separate challenge campaign is required for 1.0. If empirical testing shows strong demand for alternate solutions, the cheapest acceptable post-launch addition is authored **variant work orders using existing mechanics/assets**, validated exactly like canonical cases. They do not alter canonical progression.

---

# 8. Achievement baseline
Target: **12 Steam achievements**, all deterministic and accessible. No hidden dexterity, speed, grind or no-hint requirements.

1. **First Cut** — clear OW01.
2. **Useful Waste** — clear OW04 / complete Tray I.
3. **Right Property** — clear OW08 / Tray II.
4. **Keep It Around** — clear OW12 / Tray III.
5. **Across the Bench** — clear OW16 / Tray IV.
6. **Only One to Spare** — clear OW20 / Tray V.
7. **Workshop Certified** — clear OW24 / all 24 canonical cases.
8. **Tool Becomes Part** — clear OW12 with the canonical job requirement that a temporary jig later occupies a final part slot; state-based, any valid solution that realizes the required role transition qualifies.
9. **Crossed Favors** — clear OW14, whose certification requires the two-way cross-root dependency.
10. **Prepared Tool** — clear OW22, where a future jig must carry its derived witness.
11. **Another Way** — on OW16 or OW20, certify using two distinct validator-recognized solution-family signatures across separate clears. No exact move count required.
12. **Trace the Work** — after clearing any case OW09+, open the completed-solution causal recap/Trace View through all commits at least once; educational discovery, not repetitive use.

Achievements 8–10 intentionally overlap meaningful campaign milestones rather than demand artificial side behavior. Achievement 11 is the only replay achievement and requires a case explicitly authored/validated for multiple families. Demo grants no Steam achievements; on import, retail may reconcile milestone achievements only after the player reaches/loads the corresponding retail campaign state. Phase 8 must make reconciliation idempotent.

---

# 9. Steam/platform assumptions
Baseline 1.0 Steam product supports:
- Steam achievements (12 baseline above);
- Steam Cloud for retail profile/progress/settings where technically appropriate;
- full controller support and dynamic glyph/input behavior per Phase 6;
- Steam Deck/1280×800 readability target and target-device QA;
- separate free demo package with in-game import contract above;
- Family Sharing subject to Steam platform behavior;
- localization-ready externalized UI/store strings.

Store/UI localization target for budgeting: **English baseline plus a localization architecture capable of adding FIGS, Brazilian Portuguese, Russian, Simplified Chinese, Japanese and Korean without code/layout redesign.** This is readiness, not a promise that all languages ship day one; actual launch languages depend on localization budget and font/QA validation.

Not baseline: Steam Workshop, level editor, leaderboards, trading-card-driven design, inventory items, community market, remote play/co-op features. These may not be advertised until actually scoped and validated.

Cloud rule: campaign progress is monotonic clear-state plus settings, but in-progress attempts can contain irreversible state. Phase 8 must use versioned atomic saves and conflict-safe merge rules; cloud reconciliation may never silently replace a profile with fewer clear flags without explicit recovery path.

---

# 10. Monetization and post-launch boundary

## 10.1 Frozen exclusions
No:
- ads;
- premium currency;
- consumable hints;
- paid retries;
- lives/energy;
- loot boxes/random paid rewards;
- battle pass/FOMO/dailies;
- cosmetic shop at baseline;
- gameplay microtransactions;
- paid solution packs that sell relief from deliberately frustrating difficulty.

Purchase grants the complete 24-case campaign.

## 10.2 DLC / expansion rule
No DLC is required to make the base game feel complete.

A later paid expansion is allowed only if:
- base 24-case product already satisfies its value gate;
- expansion is a substantial authored pack, target **8+ dense cases**;
- it uses the frozen core verb/capability grammar or introduces at most one separately validated extension whose tutorial/content burden justifies an expansion;
- it does not retroactively gate base achievements/progression;
- it does not turn the game into workshop management/crafting simulation.

Free updates may add accessibility, quality-of-life, translations, fixes and a small number of validated variant cases without changing the commercial promise.

---

# 11. Commercial/demo empirical gates
These can alter packaging, price, demo cut or presentation without reopening the mechanical thesis.

## Gate A — demo comprehension
After D1, >=80% of blind target players should explain that a cut byproduct became a later capability/tool without prompted terminology. If not, revise demo ordering/presentation/tutorial copy before mechanics.

## Gate B — demo length
Cold median target 20–30 min; acceptable 18–35. If longer because OW05/D1 is confusing, simplify presentation or D1 data. If <18 and players report it insubstantial, strengthen D1 presentation/recap before adding another full campaign case.

## Gate C — conversion intent/value
Qualitative/quantitative store tests should compare $9.99/$12.99/$14.99 value perception using the actual demo and campaign description. Price can move within frozen band. Do not infer willingness-to-pay from puzzle count alone.

## Gate D — campaign value
Median first-clear target 5–7h, floor 4.5h for $12.99 hypothesis. Weak duration caused by filler is not value.

## Gate E — hint integrity
Hints must restore reasoning without becoming a move solver; H3 spoiler report threshold above.

## Gate F — Steam Deck/controller
Demo must be fully completable on target handheld/controller without pointer fallback or unreadable secondary state.

## Gate G — import reliability
Test fresh install, demo-first, retail-first-then-import, repeated import, Steam Deck, offline local save, cloud enabled, cloud conflict, old schema and corrupt demo save. Any import failure must preserve retail progress. If this cannot be made robust, withdraw carryover marketing promise before release.

## Gate H — store first-read
A 10-second store/trailer test must produce “cut leftover becomes tool” substantially more often than “woodworking simulator/cozy repair game.” If not, change capsule/trailer copy/art, not mechanics.

---

# 12. Phase-7 lock statement
ONE-WAY WORKSHOP is a **$12.99 working-MSRP finite premium puzzle game** with a 24-case tiered/branching campaign, no progression economy, a four-job 20–30 minute demo with deterministic non-destructive retail import, three-level non-solver hints, 12 accessible achievements, Steam Cloud/controller/Deck baseline, no score/par/leaderboard grind, and no microtransaction/live-service layer.

All price, duration and conversion claims remain empirical hypotheses. The mechanics, case count and puzzle truth must not be inflated merely to defend a price.

NEXT: Phase 8 Technical Implementation Specification — freeze engine/runtime direction, authoritative state/data schemas, deterministic transform/certifier contracts, campaign unlock evaluator, versioned persistence and atomic attempt saves, demo import/merge/cloud-conflict algorithm, achievement reconciliation, input abstraction, localization data, performance budgets, validation/test hooks, and implementation order. Do not write production code in the factory.