# GAME #018 — PHASE 7 COMMERCIAL MODEL

Date: 2026-09-06
Selected concept: **LOCAL TIME**
Status: PHASE 7 COMPLETE — TECHNICAL SPECIFICATION NEXT
Production implementation: NO

## 1. Commercial position
LOCAL TIME is a premium single-player systemic puzzle game for PC/Steam first. It competes on a compact, visually legible rule identity and a strong free demo, not on raw content volume, narrative scale, live-service retention, or cheap price.

Store vocabulary must foreground **different local times in one town**, **move clock-zones**, **NOW vs DONE**, and **persistent consequences**. Avoid leading with generic `time manipulation`, `time travel`, `rewind`, or `time-loop` language.

## 2. Fresh market evidence — 2026-09-06
Current Steam checks support a premium indie puzzle reference band around US$19.99 for highly regarded focused puzzle games: Patrick's Parabox is $19.99 and advertises 350+ handcrafted puzzles; Can of Wormholes is $19.99 and advertises 100+ handcrafted stages; A Monster's Expedition is normally $19.99 and uses a large exploratory puzzle catalog. A much larger high-production puzzle-adventure such as The Talos Principle 2 sits at $29.99. These are positioning references, not promises that content count directly determines value.

Steamworks currently lists the next Steam Next Fest as October 19–26, 2026, followed by February 22–March 1, 2027 and June 14–21, 2027. Valve describes Next Fest as an audience-building/feedback opportunity for unreleased games with playable demos, and a game may participate in only one Next Fest. Therefore LOCAL TIME must not burn its one participation before the six-case demo is polished and store messaging is validated.

Research references used this run:
- Steam store: Patrick's Parabox, current list price $19.99, demo, achievements/cloud, 350+ handcrafted puzzles.
- Steam store: Can of Wormholes, current list price $19.99, 100+ handcrafted stages, achievements/cloud, controller-friendly accessibility.
- Steam store: A Monster's Expedition, normal list price $19.99, large puzzle catalog and broad localization.
- Steam store: The Talos Principle 2, current list price $29.99, much larger production/narrative scope.
- Steamworks Upcoming Events / Next Fest documentation, checked 2026-09-06.

## 3. Launch platform and price
**Launch platform:** Windows PC on Steam. Steam Deck is a target-quality device path, not a promise of Valve Verified status before Valve testing. Linux/macOS native builds are stretch goals only after Phase 8 proves low incremental QA burden; Proton compatibility may be tested but is not a substitute for explicit support claims.

**Target base price:** US$14.99 launch MSRP, with a permitted pre-release review band of **$14.99–$19.99**. Default remains $14.99 unless production quality, external playtest demand, and final non-filler content support $19.99.

Why not lock $19.99 now: the strongest $19.99 systemic-puzzle references currently advertise 100–350+ handcrafted puzzles or a much broader exploratory structure. LOCAL TIME intentionally targets a smaller 6–8 hour first completion and should win on density, presentation and novelty rather than padding to imitate those counts.

Why not price below $14.99: the design requires bespoke authored/solver-validated puzzles, polished diorama presentation, controller/Deck UX, reason traces and a substantial demo; positioning it as a disposable micro-puzzle would weaken perceived product ambition.

Regional pricing should use Steam's current regional-price tooling/recommendations at release review rather than hard-code 2026 conversions in design authority.

## 4. Content count re-test and playtime lock
**Keep 36 campaign + 12 optional mastery as a TARGET, not a shipping quota.** Commercial value does not justify filler.

First-completion target: **6–8 hours** for a median puzzle-experienced player who completes the 36 campaign cases without chasing all efficiency goals. Expected shape:
- LT01–LT06: 25–35 min total;
- Cases 07–18: ~1.5–2 h;
- Cases 19–30: ~2–3 h;
- Cases 31–36: ~1.5–2 h;
- navigation/retries/reading naturally fill the remaining band.

Mastery: **2–4 additional hours** for players who choose all 12, with no requirement for campaign ending.

Hard quality cut gate before content lock: if more than 6 of the 36 campaign cases fail the Phase-5 variety/human-proof gates or playtest as renamed/reordered versions of another case, ship **30 campaign cases** rather than replace them with filler. If more than 4 mastery cases depend mainly on arbitrary move-budget harshness, cut mastery from 12 to **8**. Price review then reopens within $14.99–$19.99; count alone never forces a price reduction.

## 5. Demo product
Free Steam demo = **LT01–LT06**, target **25–35 minutes** first completion, maximum desirable median under 45 minutes. It is a curated causal sequence, not a time-limited slice.

Demo includes full baseline settings/accessibility/controller support, glossary entries introduced by those cases, restart/undo/reason trace, and a compact demo case-select after LT01.

Demo ending: completion tableau + one clear message: `Different local times. Persistent consequences.` Then show 2–3 non-spoiler full-game screenshots/GIF beats from later systems (handoff, three-clock footprint, coupled event) and Wishlist / Full Game actions. No fake countdown, nagging popup loop, or locked menu full of inaccessible case cards.

**Save carryover target:** demo completion/settings and per-demo-case records import into full game. Full game must recognize a compatible demo save and unlock Case 07 while retaining LT01–LT06 replay. Phase 8 must define versioned persistence and idempotent import. If safe cross-app/depot persistence cannot be guaranteed, settings and completion may be imported via shared Steam/user save path only after technical validation; never advertise carryover before it passes upgrade tests.

The demo should remain available after launch unless evidence shows a concrete support/problem reason to remove it.

## 6. Steam / Next Fest strategy
Do not target October 2026 merely because it is the nearest event. Participate in the first Next Fest for which all are true:
1. LT01–LT06 are content-complete and externally tested;
2. store capsule/trailer explain local-time zones in <=10 seconds;
3. demo crash/save/controller regressions are release-quality;
4. wishlist call-to-action and public store page are ready;
5. there is enough runway after the Fest to repair feedback without redesign panic.

Because Steam currently permits one Next Fest participation per title, the event is a one-shot launch funnel, not a routine QA milestone.

Pre-Fest playtests/private demo distribution should validate comprehension first. Public demo can launch before the selected Fest if useful, but Fest participation itself waits for polish.

## 7. Store-message hierarchy
Short description direction:
`Move pockets of local time around a tiny town. Open bridges, bake bread and dispatch trains at different times at once — completed steps stay completed when the clocks move.`

Trailer first 10 seconds must show: 08:00 zone -> bakery changes; clock moves -> bread remains DONE; another zone gives station 08:05 while bridge remains NOW open. Text card: `MOVE LOCAL TIME. KEEP THE CONSEQUENCES.`

Store screenshots should show large readable clock labels and distinct simultaneous times; avoid screenshots dominated by menus or abstract socket overlays.

Tags/description may include Puzzle, Logic, Singleplayer, Relaxing/Thoughtful as appropriate after store testing, but marketing copy must not rely on the generic `time manipulation` phrase.

## 8. Progression, replay and efficiency
Campaign completion is the product goal; replay is voluntary mastery.

No XP, currency, daily tasks, streaks, random drops, login rewards or grind unlocks. Completing a campaign chapter unlocks the next chapter and its mastery pair. No star threshold blocks campaign progress.

Optional efficiency targets use solver-validated thresholds such as `<= X moves` or `<= Y Resolves`; they are displayed after first completion unless a case is explicitly teaching budget pressure. Best records are local/profile records and may support achievements. Multiple solution families remain valid; efficiency never defines the canonical solution.

Mastery cases reward deeper composition, not story endings or essential accessibility options.

## 9. Difficulty versus accessibility
Accessibility settings never make a player ineligible for completion, achievements, or records merely for being enabled. Text size, contrast, remapping, reduced motion, animation skip, audio captions and input choices are not difficulty settings.

Shipping baseline uses one authored campaign difficulty because exact puzzle logic is the product. Optional assistance may include rule glossary, reason trace, unlimited recovery and later a carefully designed hint layer if playtests prove necessary. Do not create an `Easy` mode by silently changing puzzle rules or exposing solver answers.

If a hint system is later approved, it should reveal progressively stronger causal observations, not the next clock placement. It remains outside frozen baseline until Phase 9/10 evidence requires it.

## 10. Achievements
Target **18–24 Steam achievements**, finalized after content lock. Philosophy:
- chapter/demo/full-campaign completion;
- optional mastery milestones;
- a few solver-verified elegant/alternate constraints;
- playful systemic discoveries that cannot be permanently missed;
- no achievements for repetitive restarts, hours idled, thousands of moves, daily play, speedrun reaction time, inaccessible audio/color perception, or mutually exclusive save-state traps.

100% completion should be possible from Case Select without replaying the whole campaign from scratch.

## 11. Steam features and saves
Target features for launch: Single-player, Steam Achievements, Steam Cloud, full controller support where technically accurate, Family Sharing under Steam policy, and Steam Deck compatibility target. Phase 8 must validate exact API/runtime requirements before store promises.

Cloud save conflict behavior must preserve both newest canonical progress and recoverability; never silently overwrite a clearly divergent newer local profile. Persistence must be small, versioned and deterministic.

No mandatory account, telemetry login or external launcher.

## 12. Localization
**Launch target:** English plus interface/text localization for French, German, Spanish (Spain), Brazilian Portuguese, Russian, Simplified Chinese, Japanese and Korean, subject to budget and localization QA. This is intentionally ambitious but feasible because the game is dialogue-light and uses compact rule text.

If budget forces cuts, English is mandatory and the architecture remains localization-ready; prioritize Simplified Chinese, German, French, Spanish and Brazilian Portuguese using wishlist/demo geography before release. Never machine-publish unreviewed puzzle-rule translations: a mistranslated condition changes perceived logic/fairness.

Technical/UI requirements: no text baked into world art except replaceable labels; time labels are data; expandable cards; plural/grammar-safe strings; font fallback for CJK/Cyrillic; controller glyphs independent of prose; localization screenshots at 1280x800.

## 13. Discounts and bundles
No launch discount is required. Permitted launch discount: **0–10%** only if release strategy benefits from it; do not use a deep launch sale to compensate for weak positioning.

Post-launch discount assumptions are deliberately conservative: modest event discounts after the initial launch window, deeper discounts only as the title ages and portfolio strategy justifies them. Exact cadence is release-management policy, not frozen gameplay design.

Curated puzzle bundles are acceptable if partners are thematically/commercially sensible. Soundtrack/artbook may be optional separate products only if those assets genuinely exist; they are not production requirements.

## 14. Hard monetization exclusions
No ads; no microtransactions; no premium currency; no consumable hints; no energy/lives; no battle pass; no daily-login economy; no loot boxes; no paid undo; no paid accessibility; no gameplay-affecting pre-order bonus; no always-online DRM designed by the game; no subscription dependency; no selling individual campaign cases to complete the base arc.

Future expansion is allowed only as a substantial optional puzzle pack with reviewed new content and no removal of base-game functionality.

## 15. Commercial empirical gates before production/release commitment
1. Demo comprehension: >=80% of first-time testers can explain NOW vs DONE after LT02 and the core hook after LT06.
2. Demo completion: median target 25–35 min; investigate >45 min median before adding content.
3. Store comprehension: unprompted viewers of first 10 trailer seconds should describe `different/local times in different places`, not primarily `rewind/time travel`.
4. Content density: no >20% repeated proof shape; trigger 36->30 cut if six+ campaign cases fail uniqueness/quality.
5. Mastery quality: trigger 12->8 cut if four+ depend mainly on arbitrary budget tightness.
6. Price: compare $14.99 vs $19.99 intent/willingness only after polished demo/store assets; default $14.99 until evidence supports higher.
7. Deck: complete controller-only demo at 1280x800 with no focus traps and readable footprints before claiming target quality.
8. Localization: every localized rule condition receives semantic QA against English canonical rule data.
9. Save carryover: demo->full import tested across clean install, existing full save, older demo schema and repeated import before advertising.
10. Next Fest: do not enter until demo/store funnel is strong enough to justify the title's one participation.

## 16. Pre-production scope cuts
If schedule/budget tightens, cut in this order without damaging identity:
1. reduce repetitive mastery 12->8;
2. reduce campaign 36->30 only by removing weak cases while preserving all chapter concepts;
3. reduce launch localization count while retaining localization-ready architecture;
4. defer non-Windows native builds;
5. reduce decorative town variants/animations while preserving state readability.

Do **not** cut: LT01–LT06 demo logic, NOW/DONE readability, deterministic reason trace, undo/restart, controller path, solver/validator obligations, or public rule clarity.

## 17. Phase result
Phase 7 locks Steam/Windows-first premium positioning, $14.99 default MSRP with $14.99–$19.99 review band, 6–8 hour campaign target, 36+12 as quality-gated targets rather than quotas, LT01–LT06 free demo, progression/replay/achievement philosophy, accessibility separation, Steam/Deck/cloud targets subject to technical validation, localization plan, Next Fest discipline, discount assumptions and hard monetization exclusions.

**PHASE 7 COMMERCIAL MODEL = COMPLETE.**

# NEXT DESIGN STEP — PHASE 8 TECHNICAL IMPLEMENTATION SPECIFICATION
Create `GAME18_TECH_SPEC.md`. Define engine/runtime direction and alternatives; canonical immutable/mutable state boundaries; data schemas for case/site/object/clock/carrier/rules/objectives; deterministic Resolve pipeline implementation contract; validator + exhaustive solver architecture; reason-trace/event log; input abstraction and controller focus graph; save/profile schema and versioning; demo/full save import and idempotency; Steam Cloud conflict strategy; localization data/font/layout contracts; rendering/performance assumptions for compact dioramas and Steam Deck; test hooks/property tests/golden cases; content-authoring tooling requirements; implementation dependency order for future dedicated repo; and explicit technical acceptance criteria. Research current engine/Steamworks/tool constraints where choices depend on them. Do not write production implementation code.