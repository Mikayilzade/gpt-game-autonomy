# GAME #015 — PHASE 7 COMMERCIAL MODEL / RETENTION / PLATFORM PACKAGE

Date: 2026-09-03
Status: PHASE 7 COMPLETE
Working title: **FRESH COAT**
Design complete: NO

## 0. Authority and boundary
This file freezes the commercial/player-retention package implied by Phases 3–6. It adds no gameplay mechanics and does not start production implementation. Fresh Coat remains a finite premium spatial-deduction game whose value comes from a dense 24-case authored campaign, tactile presentation, replay/inspection, and a representative free demo—not grind or recurring obligations.

Commercial variables that depend on launch conditions (exact price, launch discount, localization breadth, final title) remain explicitly revisable until release evidence exists. The product structure and anti-monetization boundaries are frozen.

## 1. Fresh market/platform evidence — 2026-09-03
Current evidence used for this phase:
- Steamworks demo documentation supports sharing cloud storage with the full app so demo saves can carry forward, and recommends disabling achievements in demos and granting earned achievements when the full game loads the carried save.
- Steam Cloud supports automatic cross-device persistence and Dynamic Cloud Sync for suspend/resume scenarios such as Steam Deck -> PC -> Deck. This fits the controller/handheld thesis.
- Steam Community profile features such as Trading Cards depend on platform engagement eligibility; they cannot be treated as a launch-value pillar.
- Current 2026 puzzle demos continue to use meaningful chunks of the real campaign. Hexzen's August 2026 demo explicitly contains the first campaign region, some later material, full accessibility/input options, and automatic progress import. Timebound's May 2026 demo contains the entire first area. These support a real-campaign demo rather than a bespoke tutorial branch.
- Current puzzle competition ranges from compact games to products advertising hundreds or 1,000+ puzzles. Fresh Coat must not compete on raw count; it must sell density, physical readability, novelty, and a complete finite arc.

Research URLs (market evidence, not canon):
- https://partner.steamgames.com/doc/store/application/demos
- https://partner.steamgames.com/doc/features/cloud
- https://partner.steamgames.com/doc/marketing/tradingcards
- https://store.steampowered.com/app/4970090/Hexzen/
- https://store.steampowered.com/app/4539960/Timebound_Demo/

## 2. Product/value proposition
The paid promise is **24 deliberately distinct handcrafted spatial proofs with a strong physical reveal**, not “hours of spray painting.”

Expected first-clear campaign value target:
- roughly 3–6 hours for a typical puzzle player;
- faster expert clears are acceptable;
- late puzzles may take 10–15+ minutes without requiring every player to hit a target duration;
- no padding is added to meet an hour count.

Replay value comes from revisiting cases, seeing one's successful A/B arrangements, optional completion achievements, and trying alternate legitimate solution classes where they exist. Replay is secondary; the game is allowed to be finished.

Commercial copy must emphasize:
1. use the workpieces themselves as masks;
2. predict hidden exposure across one/two passes;
3. every masker has its own paint obligations;
4. unpack to prove the hidden paint history;
5. 24 handcrafted cases / no filler.

Do not market the product as a simulator or imply free-aim painting.

## 3. Price hypothesis
### Launch hypothesis
Recommended planning range: **US$9.99–14.99**, with **US$12.99** as the current center hypothesis.

Rationale: this is a compact premium authored puzzle game with bespoke 3D presentation and controller/Deck support, but only 24 primary cases. Pricing it like a sprawling 10–20 hour puzzle adventure would create the wrong value expectation; pricing it as a disposable microgame would undervalue the presentation/authoring burden.

This is **not frozen as the final price**. Before release, reassess against:
- measured median campaign completion time from playtests;
- demo conversion/wishlist response;
- final polish and presentation quality;
- comparable puzzle prices in the launch quarter;
- regional pricing recommendations and exchange-rate conditions.

### Discount posture
- Optional launch discount: 10% maximum if commercially useful; 0% is also acceptable.
- Avoid immediate deep discounting that trains buyers to wait.
- Later seasonal discounts may deepen gradually after meaningful time on market.
- No pre-order-exclusive gameplay, FOMO bonus, founder pack or deluxe gameplay advantage.

## 4. Campaign progression / unlock contract
Campaign remains FC01–FC24 in eight visible families.

Default progression:
- FC01 unlocked initially.
- Completing 2 of the 3 cases in a family unlocks the next family **except mandatory concept-introduction gates below**.
- Mandatory knowledge gates: FC03 (self-obligated masker), FC10 (two-pass flow), FC13 (A_THEN_B), and FC16 (cavity semantics) must be completed before entering content whose proof assumes that concept.
- Case Select always permits replay of every unlocked case.
- Completing all 24 is the canonical campaign completion state.

The 2-of-3 rule gives relief from one temporarily stuck puzzle without allowing tutorial bypass. No currency, XP, stars, move ratings or performance grades unlock cases.

No hidden “perfect” ending is tied to no-hint/no-undo behavior.

## 5. Optional completion layer
Keep it minimal and non-grindy:
- family completion marks for 3/3 cases;
- campaign completion for 24/24;
- optional record that a case has more than one player-discovered successful arrangement class only if the implementation can identify this without revealing undiscovered solutions.

Do **not** add collectibles, daily puzzles, streaks, mastery XP, cosmetic currency, randomized objectives, par times, move limits or completion percentages based on repetitive actions.

## 6. Exact demo package
Canonical demo target: **7 full campaign cases / ~20–30 minutes for the intended first-time player**, with no time limit.

Demo case set:
- FC01 — direct masking;
- FC02 — pose/orientation;
- FC03 — self-obligated masker;
- FC05 — blocker-footprint comparison;
- FC10 — first two-pass A/B case;
- FC13 — A_THEN_B introduction;
- one **demo finale variant of FC14** using the shipping FC14 rules/data family, preferably the actual FC14 if pacing validates it.

The demo may unlock these in a curated sequence that skips FC04/FC06–09/FC11–12. Skipped cases are not marked complete. Full-game knowledge-check cards handle the jump back into campaign order as already specified in Phase 6.

### Demo boundary
- Uses the same mechanics, renderer, controls, accessibility options, target/history language and save schema as full game.
- No demo-exclusive puzzle mechanic, currency, metaprogression or reward.
- No artificial timer or play-count limit.
- At completion: concise end card with `Wishlist / Buy Full Game` where platform permits, plus `Replay Demo Cases`.
- Demo remains useful after launch unless storefront/maintenance evidence gives a concrete reason to retire it.

### Carry-over contract
Progress carry-over is **required** on Steam unless a platform technical blocker is discovered in Phase 8.
Persist/import:
- completed shipping case IDs;
- tutorial-card acknowledgements;
- accessibility/settings where safe;
- most recent valid puzzle checkpoint only if the corresponding case exists unchanged in full build.

On first full-game launch, import is idempotent: merge completion by stable case ID, never duplicate achievements/unlocks, never overwrite newer full-game progress with older demo state.

Steam demo achievements are disabled. If imported completion satisfies a full-game achievement, grant it once after successful import, consistent with Steamworks guidance.

## 7. Achievement philosophy
Target **10–14 achievements**, current design target 12. Achievements celebrate learning/completion, not self-imposed deprivation.

Recommended structure:
- 8 family milestones (complete each family 3/3);
- 1 first successful two-pass case milestone;
- 1 first A_THEN_B success milestone;
- 1 campaign completion (24/24);
- 1 optional whole-campaign completion/readability milestone such as completing every case, already covered, or discovering an authored alternate solution class if robustly detectable.

Final list should avoid redundant double-awards; 10–12 is preferable to filler.

Forbidden achievement conditions:
- no hints;
- no undo/reset;
- speed/par time;
- minimum moves;
- repeated spraying/failure counts;
- launching on consecutive days;
- grinding every pose/socket;
- accessibility settings off;
- controller/keyboard-specific completion.

Hints and accessibility never block achievements.

## 8. Difficulty / hints / accessibility commercial stance
There is one canonical puzzle rule set. Assistance changes explanation/readability, not truth.

- Three-tier hints from Phase 6 are included in base game and demo, unlimited and free.
- Exposure preview remains a normal factual inspection feature, not an “easy mode.”
- Accessibility options are parity features, not unlocks or paid extras.
- Store copy should state: no timers, unlimited undo/reset, optional hints, controller support, non-color coat cues.
- Do not market “brutal difficulty” as the identity; late challenge comes from coupled spatial reasoning.

## 9. Steam feature package
### IN / required target
- Steam Achievements (full game only).
- Steam Cloud for campaign/progress; Phase 8 must define conflict-safe schema.
- Full controller support / Steam Input-compatible action abstraction.
- Steam Deck-friendly default presentation and performance target.
- Family Sharing where platform defaults permit it.
- Demo with shared/importable progress.

### CONDITIONAL / nice-to-have
- Trading Cards / profile items only if Steam eligibility is reached and asset cost is justified. Not promised at launch and never a product pillar.
- Steam Rich Presence may show broad state (`Solving FC14`, `Campaign 15/24`) if cheap; it must not expose solutions.

### OUT
- Leaderboards: no canonical competitive metric exists; adding time/move boards would distort play.
- Steam Workshop: no player level editor is in scope and arbitrary authored geometry would require a separate validation/product system.
- Inventory/market items.
- Multiplayer/Remote Play Together as a product feature.
- user-generated puzzle browser.

## 10. Localization plan
Puzzle truth is mostly visual, so localization burden should remain controlled.

Architecture requirement: all strings externalized from first implementation pass; no text baked into puzzle textures or geometry.

Launch language hypothesis (subject to budget/quality):
- English baseline;
- prioritize Simplified Chinese, Japanese, Korean, German, French, Spanish (Spain/LatAm strategy may be combined only where quality permits), Brazilian Portuguese, and Russian based on storefront demand/cost evidence nearer launch.

Do not promise a language until target cards, hint text, settings, achievements, store copy and tutorial cards have been QA'd at handheld scale. Machine-only shipping localization is not acceptable for proof-step hints where ambiguity can change perceived puzzle logic.

Right-to-left readiness is desirable in UI layout architecture but not a frozen launch-language commitment.

## 11. Store-page communication package
### Short-description thesis
A spatial deduction puzzle about stacking the pieces themselves into masks, spraying in fixed passes, and unpacking the hidden paint history.

### Capsule/trailer rule
Never lead with a static workshop shot. The first communication beat must show transformation:
`targets -> stack -> SPRAY A -> rearrange -> SPRAY B -> explode/unpack -> different hidden histories`.

### Trailer structure (target 45–60 sec)
- 0–5s: one-pass mask/reveal hook, no logos before consequence;
- 5–15s: masker has own target;
- 15–30s: two coats + rearrangement + A->B badge;
- 30–42s: cavity/role reversal/capstone glimpses without solutions;
- final: 24 handcrafted cases, no timers, controller/Deck-friendly, demo CTA.

### Screenshot minimum set
1. clean target + pre-spray stack;
2. spray consequence with exposed/protected readability;
3. unpack reveal showing different face histories;
4. two-pass stage rail and A->B target;
5. cavity/late scene demonstrating depth;
6. controller/handheld-readable UI.

Do not use screenshots dominated by menus, generic booth scenery, or free-aim nozzle imagery.

## 12. Working-title obligation
`FRESH COAT` remains a working title only. Before store-page creation, perform dedicated title clearance:
- Steam exact/near title search;
- major storefront/game database search;
- web/domain/social collision search;
- relevant trademark search in intended sales territories if commercial release proceeds.

A weak/occupied title may change without reopening game design. Marketing must not rely on the title alone to explain the mechanic.

## 13. Launch/update/expansion boundaries
### Launch
Ship as a complete 1.0 premium game when the 24-case campaign, demo, accessibility/controller path, persistence, certification and empirical gates pass. Early Access is not part of the baseline plan; the finite puzzle set benefits from a polished complete first impression.

### Free updates
Appropriate for bug fixes, accessibility, localization, performance, quality-of-life and possibly a very small number of free cases if they are genuinely distinct and already production-feasible. Do not promise a live roadmap.

### Paid expansion
Permitted only after release if demand exists and a new authored case set can preserve the frozen grammar or formally reopen it as a clearly scoped expansion. A paid expansion must offer meaningful new authored reasoning/content, not sell withheld base-campaign cases.

### Permanent exclusions
- ads;
- paid hints;
- consumables;
- energy/lives;
- battle pass;
- daily-login rewards;
- FOMO events;
- loot boxes;
- paid puzzle skips;
- cosmetic currency economy;
- subscription requirement;
- retention grind.

## 14. Commercial acceptance / empirical gates
Phase 7 is design-complete because the implementation/release track now has a coherent package. The following remain empirical release decisions rather than missing game rules:

C1 — **Price validation:** reassess $9.99–14.99 / $12.99 center after measured playtime, polish and launch-quarter comparables.
C2 — **Demo pacing:** 7-case demo should land around 20–30 min for representative first-time players; if FC14 pushes it materially longer, use a mechanically identical smaller FC14-family finale without inventing demo-only rules.
C3 — **Demo conversion:** store/demo telemetry may inform marketing, but never triggers grind or gameplay degradation.
C4 — **Localization breadth:** expand only where professional-quality QA is affordable.
C5 — **Trading Cards:** only if Steam eligibility exists; absence is not a launch blocker.
C6 — **Title clearance:** required before public store identity freeze.

## 15. Phase-7 conclusion
Fresh Coat is commercially framed as a compact, complete, premium puzzle game—not a service. Its campaign, demo and platform package all reinforce the same core promise. No retention system is needed to justify the product.

PHASE 7 = COMPLETE
DESIGN COMPLETE = NO

## NEXT ACTION — PHASE 8 TECHNICAL IMPLEMENTATION SPECIFICATION
Re-read all active Game #015 authority and specify implementation without writing production code. Freeze engine/runtime direction or engine-agnostic contracts where appropriate; exact data/state model; deterministic exposure-precompute pipeline; authoring/certifier architecture; runtime arrangement and spray state machine; save schema/versioning/demo import/cloud conflict/idempotency; input abstraction; UI/state boundaries; localization architecture; performance/Deck assumptions; test hooks; telemetry/privacy boundary if any; build/content validation; and recommended implementation order. Explicitly attack renderer-vs-truth divergence, partial-region geometry, symmetry/equivalence, corrupt saves, cloud/demo duplication, and interrupted Spray/undo transactions.