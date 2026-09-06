# GAME #018 — PHASE 7 COMMERCIAL MODEL

Date: 2026-09-06
Game: **LOCAL TIME**
Status: PHASE 7 COMPLETE — PHASE 8 TECHNICAL SPECIFICATION NEXT
Production implementation: NO

Authority: prior active Game #018 files. This file locks product/commercial boundaries; it does not add gameplay grammar.

## 1. Commercial thesis
LOCAL TIME is a compact premium single-player systemic puzzle game for PC/Steam. It competes on clarity, novelty and authored causal quality rather than raw puzzle count. No ads, MTX, currencies, consumable hints, battle pass, daily systems or live-service retention.

## 2. Fresh September 2026 market anchors
Fresh Steam checks on 2026-09-06 show three strong systemic puzzle references at **$19.99 USD**: Patrick's Parabox, Can of Wormholes and A Monster's Expedition. Patrick's Parabox advertises 350+ handcrafted puzzles; Can of Wormholes advertises 100+ and explicitly emphasizes no filler. Both expose Steam achievements/cloud; Patrick's Parabox supports 10 interface languages, while Can of Wormholes currently lists English/French/Simplified Chinese. These are quality/positioning anchors, not direct scope matches: LOCAL TIME targets fewer, larger authored causal cases and therefore should enter below their current $19.99 anchor unless playtest scope expands materially.

Steam Next Fest documentation checked 2026-09-06 confirms a title may appear in only one Next Fest. October 2026 registration already closed August 31; future documented editions include Feb 22–Mar 1 2027 and Jun 14–21 2027. The factory must not commit the game's single Next Fest opportunity before a polished representative demo and store page exist.

## 3. Price lock
**Base launch MSRP: $14.99 USD.**

Review band before store setup: **$14.99–$19.99**. Raise to $19.99 only if production validation demonstrates substantially more than the quality floor, excellent presentation, and first-completion value near/above the 6–8 hour target. Do not reduce below $14.99 merely because the puzzle count is lower than abstract/grid competitors; each LOCAL TIME case is a larger diorama causal composition.

Regional pricing should use Steam's current recommended regional-pricing tooling at release review rather than hard-coding 2026 currency tables into design canon.

## 4. Content count and duration decision
The old 36 campaign + 12 mastery number remains a **target, not a quota**.

Locked ship gates:
- campaign target: 36; **quality floor 30**;
- mastery baseline: **8**;
- mastery reserve: M09–M12, ship only if each adds a distinct proof shape;
- expected first campaign completion: **6–8 hours** for target package;
- acceptable high-quality floor package: roughly **5–7 hours** if 30 campaign cases survive and later cases are stronger for the cuts;
- mastery adds optional challenge, not promised mandatory hours.

Never inflate duration with repeated proof shapes, slow animations, forced traversal, collectibles or budget variants. If Cases 31–36 or M09–M12 fail novelty gates, cut them and adjust store claims rather than add bespoke mechanics.

## 5. Demo lock
Free Steam demo: **LT01–LT06**, target **25–35 minutes** for a first-time puzzle player.

Demo must prove the complete product identity by its end: NOW vs DONE, distinct simultaneous local times, permanent risk, carrier/later acceptance, and unguided synthesis. It must end on a satisfying solved-town tableau plus wishlist/full-game CTA, not on a cliffhanger.

Demo uses the same canonical case data/runtime as full game. Completion/settings/accessibility state and compatible checkpoint/profile data carry into full game. Full game recognizes completed LT01–LT06 and lets the player continue without replay, while always permitting replay from case select. Import is idempotent and never overwrites newer full-game progress.

No demo-exclusive progression, account requirement or telemetry dependency is required.

## 6. Next Fest / launch timing principle
Do **not** target October 2026; its registration deadline has passed and the design is not implementation-ready. Because Steam permits one Next Fest appearance, select a later edition only when:
- LT01–LT06 are polished and externally playtested;
- store capsule/trailer communicate local-time zones rather than generic time travel;
- controller/Deck path is functional;
- demo save/import is tested;
- no major mechanic rewrite is expected;
- release is close enough that festival attention can plausibly carry toward launch.

February/June 2027 are current documented opportunities, not promises. Re-check Steamworks dates/eligibility when implementation reaches marketing readiness.

## 7. Steam/platform baseline
Launch baseline:
- Windows/Steam first;
- full mouse/keyboard and controller support;
- Steam Deck readability/performance is a product requirement; pursue Verified/Playable compatibility as implementation evidence permits, never promise certification before Valve testing;
- Steam Cloud for profile/checkpoint/settings data where appropriate;
- Steam achievements;
- Family Sharing compatibility unless later platform constraints intervene;
- no mandatory online connection for puzzle play.

Native macOS/Linux are stretch targets only after Windows stability unless implementation cost proves trivial. Do not delay the core release merely to claim platform count.

## 8. Achievements
Target **18–24 achievements**, mostly milestone/insight based:
- chapter completion;
- campaign completion;
- mastery completion bands;
- a few explicit optional challenge conditions already represented by authored case objectives;
- accessibility-neutral discovery/skill achievements.

No daily/streak achievements, no huge grind counters, no achievements requiring intentionally corrupting progress, and no requirement for globally shortest solutions.

## 9. Localization
Architecture must be localization-ready from first implementation. English is source language.

Commercial target after text lock: localize UI/rules/store-critical text into a practical first wave such as Simplified Chinese, French, German, Spanish, Brazilian Portuguese, Russian, Japanese and Korean, subject to budget and market review. Because rules are compact but precision-sensitive, machine-only untranslated QA is unacceptable; each language needs terminology consistency and layout testing.

If budget cannot support the full target, ship fewer professionally reviewed languages rather than low-quality broad coverage. Critical clock labels remain numeric/semantic and are not allowed to carry meaning through English-only art.

## 10. Discount boundaries
Suggested launch discount: **10%**, with 0% also acceptable if wishlist/launch strategy favors price stability. Do not exceed 15% at launch.

Post-launch discounts may deepen gradually during meaningful Steam events after the launch window; avoid rapid steep discounting that trains players to wait. No fake permanent sale cadence. Exact discount calendar is a release-stage marketing decision, not frozen design.

## 11. Replay / mastery without grind
Replay value comes from:
- optional mastery cases;
- alternate valid solutions;
- optional authored efficiency goals only where they create a new reasoning question;
- case replay after completion;
- achievement challenges that use existing rules.

No XP, currencies, randomized loot, procedural filler, daily puzzle obligation, consumable hint economy or forced collectible hunt. Normal campaign solutions are not graded against a global shortest path.

## 12. Commercial risks and gates
1. **Perceived low content for $14.99:** test store/demo audiences; answer with strong case density and presentation, not filler count.
2. **Generic 'time puzzle' positioning:** trailer/store copy must show multiple local times simultaneously and avoid rewind vocabulary.
3. **Demo too tutorial-heavy:** LT06 must be genuinely unguided and satisfying; median first-session target 25–35 min.
4. **36-case target creates repetition:** content gate outranks count; ship 30 strong campaign cases if necessary.
5. **Diorama production cost exceeds puzzle scope:** reuse bounded landmark/object/carrier kit from Phase 5; no unique art set per case.
6. **Next Fest used too early:** single-participation rule makes readiness a hard marketing gate.
7. **Localization precision:** rule mistranslation is gameplay breakage; terminology QA required.
8. **Deck promise outruns implementation:** readability/controller are required design targets; certification claims wait for real validation.

## 13. Phase acceptance
Locked: premium Steam-first model; $14.99 launch MSRP and $14.99–19.99 review band; 30–36 campaign quality gate, 8 mastery baseline + 4 reserve; 6–8h target / 5–7h acceptable quality-floor package; LT01–LT06 25–35 minute free demo with idempotent carryover; one-shot Next Fest readiness principle; Steam/controller/Deck/Cloud/achievement/localization expectations; conservative discount boundaries; replay without grind; explicit commercial empirical gates.

**PHASE 7 COMMERCIAL MODEL = COMPLETE.**

# NEXT DESIGN STEP — PHASE 8 TECHNICAL IMPLEMENTATION SPECIFICATION
Define engine/runtime direction, canonical data model mapping from Phase 4, deterministic solver/validator architecture, authored-case schema, state hashing, Resolve/reason-trace contract, persistence and atomic save/import semantics, Steam Cloud conflict policy, input abstraction, localization pipeline, performance/display assumptions, test hooks/golden cases/property tests, content validation tooling, implementation order and technical acceptance criteria. Use fresh research only where current engine/platform/tool facts materially affect the choice. Do not begin production implementation.