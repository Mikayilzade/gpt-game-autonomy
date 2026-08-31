# GAME #010 — PHASE 7 ECONOMY / RETENTION / COMMERCIAL MODEL

Date: 2026-08-31
Status: **PHASE 7 ACTIVE — CORE COMMERCIAL CONTRACT ESTABLISHED**
Game: Luggage Carousel Zero *(working title)*

Authority: all prior active Game #010 authorities -> `GAME10_PHASE6_CLOSURE.md` -> this file.

## 1. Fresh market/platform evidence
Research checked 2026-08-31.

Current 2026 Steam examples show a broad compact-puzzle price band rather than one mandatory price: `What's the Password?` is $7.99 and describes ~2 hours/100 puzzles; `Piece by Piece` is $12.99 with 100 handcrafted levels; `A Little Perspective` is $14.99 with 200+ puzzles; `Puzzle Loot` launched 2026-08-21 at $8.99. These are scope anchors, not direct comparables.

Official Steamworks documentation also confirms that a demo can share cloud storage with the full app so progress carries forward, and recommends disabling achievements in the demo then granting earned achievements when the full game loads shared progress. Steamworks API integration is optional to ship but supports expected platform features such as achievements.

Sources checked:
- https://store.steampowered.com/app/4095490/Whats_the_Password/
- https://store.steampowered.com/app/3249380/Piece_by_Piece/
- https://store.steampowered.com/app/3485300/A_Little_Perspective/
- https://store.steampowered.com/app/4960710/Puzzle_Loot/
- https://partner.steamgames.com/doc?q=cloud
- https://partner.steamgames.com/doc/sdk/api

## 2. Product model
**Premium single-purchase game.** No ads, consumable currency, energy, battle pass, gacha, paid hints, subscription, login requirement or live-service obligation.

Working launch-price hypothesis: **US $9.99–12.99**, with $11.99 as an internal planning center only. Final price is an empirical/storefront decision after real campaign count, playtime, production quality and demo conversion are known. Phase 11 must not falsely freeze an exact price before those facts exist.

Rationale: 36–48 curated cases are intentionally below 100–200-puzzle volume competitors, but the game aims for denser systemic cases and replayable optimization. $14.99 should require demonstrated length/polish stronger than currently proven; <$7.99 risks communicating a disposable micro-puzzle product unless final scope shrinks.

## 3. Campaign progression
The campaign is not an economy.

Frozen progression rule:
- Acts A–E contain the architecture counts already specified.
- Act A starts with A01 unlocked.
- Within an act, completing a case unlocks the next case.
- Completing **all but one** cases in the current act unlocks the next act. This gives one skip for a blocker while preserving teaching order.
- Once the next act unlocks, the skipped case remains available forever.
- Act E completion requires no perfect/mastery performance; basic completion is enough.
- Completed cases can always be replayed.
- No stars are required to unlock anything.

Early tutorial dependency exception: A01→A02→A03 are strictly sequential before the one-skip rule can matter; the player must demonstrate ownership/adjacency basics before broader choice.

## 4. Mastery and replay
A single optional **Efficient Route** marker survives commercial review.

A completed case earns Efficient Route if the player wins using the solver-certified minimum tick count. It is informational/prestige only:
- does not gate acts, ending, achievements requiring all basic content, hints or settings;
- case tile may show one compact marker;
- win panel shows `Solved` and, when earned, `Efficient Route`;
- minimum swap count is not exposed as a second medal to avoid optimization clutter;
- players may replay to earn it.

This creates a clear replay target without converting the game into a score economy. If playtests show minimum-tick optimization undermines intentional waiting comprehension, Phase 10 may remove the surfaced marker while retaining solver metrics internally.

## 5. Difficulty and assistance
No Easy/Normal/Hard ruleset variants: changing budgets would invalidate authored reasoning/certification.

Assistance instead uses optional hints from Phase 6:
1. Rule Reminder;
2. Reasoning Nudge;
3. Structural Hint.

Hints are unlimited and consequence-free. Using a hint does **not** invalidate basic completion or progression. Efficient Route is based only on actual tick count, not hint use. Full solution reveal is out of base canon unless accessibility testing later proves necessary; if added, it must be explicit and consequence-free rather than monetized.

## 6. Demo strategy
Canonical demo = seven-case path already frozen, approximately 15–25 minute target, ending with exact Demo 07. It demonstrates ownership, trait binding, local staging, preservation, intentional miss, visible persistent gap semantics and a compact multi-passenger finale. It excludes K2 and dense three-clause mastery.

Demo principles:
- free Steam demo;
- no timer or artificial session limit;
- completion screen clearly states that the full game expands the same rule set into deeper queue/local-permutation problems rather than promising a mechanic zoo;
- full game progress transfer is a target using shared save/cloud where practical;
- if Steam Cloud sharing is implemented, full game imports demo completion and settings idempotently;
- achievements should not pop in the demo; any qualifying demo progress can grant them after full-game import, consistent with Steamworks guidance;
- no demo-exclusive mechanics/content needed.

## 7. Achievements
Target **12–18 achievements**, low implementation burden and no grind.

Categories:
- act completion (5);
- campaign completion (1);
- first Efficient Route (1);
- Efficient Route across a bounded set / all cases only if solver certification is stable (1–2);
- first intentional-miss lesson completion (1);
- complete a K2 mastery case (1);
- optional accessibility-positive/non-punitive milestones such as completing a case in Reduced Motion are **rejected** because accessibility settings should not be gamified.

No achievements for huge Undo counts, daily play, speed input, no-hint runs, repetitive farming or hidden arbitrary behavior.

## 8. Retention philosophy
Retention comes from:
- curiosity about the next authored relationship;
- short case cadence;
- one-skip act progression reducing hard stalls;
- replay for Efficient Route;
- late synthesis cases recombining proven families;
- consequence-free Undo encouraging experimentation.

Explicitly rejected retention machinery: daily challenges, streaks, XP, cosmetics grind, randomized loot, procedural endless mode, leaderboards requiring comparable speed execution, Workshop promise, live events and FOMO.

A future free content update may add certified cases using the frozen grammar, but no update cadence is promised and base value must stand alone.

## 9. Storefront positioning assumptions
Store description should lead with the mechanical sentence, not `airport simulator` language:

**Swap the labels, not the luggage. Plan a moving carousel, let the wrong bag pass when you must, and get every passenger the right case.**

First trailer/GIF target: select adjacent gantries -> label slides locally -> belt advances -> a tempting bag deliberately misses -> later scarce bag is preserved/claimed. The product should be tagged/positioned primarily as Puzzle / Logic / Strategy / Singleplayer / Controller-friendly rather than Management or Simulation.

Working title remains non-commercial; naming/brand search is a later storefront task and cannot redefine mechanics.

## 10. Phase-7 remaining closure work
Before Phase 7 closes:
1. run a campaign progression simulation across A–E including one skipped blocker, replay and demo-import path;
2. decide exact base achievement list/rules without grind;
3. specify save-visible progression fields handed to Phase 8;
4. attack Efficient Route for perverse incentives, especially cases whose insight is intentional delay;
5. freeze commercial boundaries and explicit non-promises;
6. if clean, close Phase 7 and continue directly to Phase 8 Technical Implementation Specification.

**PHASE 7 ACTIVE. DESIGN COMPLETE = NO.**