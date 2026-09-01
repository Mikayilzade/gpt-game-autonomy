# GAME #011 — MISSING STEP — PHASE 7 COMMERCIAL / RETENTION MODEL

Date: 2026-09-01
Status: **PHASE 7 COMPLETE**
Authority: `START_HERE.md` -> `STATUS.md` -> `GAME_INDEX.md` -> `GAME11_PRODUCT_THESIS.md` -> `GAME11_MECHANICAL_ARCHITECTURE.md` -> `GAME11_CONTENT_ARCHITECTURE.md` -> `GAME11_UX_PRESENTATION_ARCHITECTURE.md` -> this file for commercial/progression decisions.

This phase changes no puzzle mechanics.

## 1. Fresh 2026 market context
Fresh Steam checks on 2026-09-01 show a wide current premium-puzzle range rather than one universal price point:
- The Grid. (2026) — $7.99;
- Piece by Piece (2026) — $12.99, 100 handcrafted levels;
- A Little Perspective — $14.99, 200+ puzzles;
- Isles of Sea and Sky — $19.99;
- The Roottrees are Dead — $19.99.

Sources:
- https://store.steampowered.com/app/2481060/The_Grid/
- https://store.steampowered.com/app/3249380
- https://store.steampowered.com/app/3485300/A_Little_Perspective/
- https://store.steampowered.com/app/1233070/Isles_of_Sea_and_Sky/
- https://store.steampowered.com/app/2754380/The_Roottrees_are_Dead/

Interpretation: Missing Step should not compete on raw level count against 100–200-level products or on adventure/narrative volume against $19.99 titles. Its value case is compact certified depth, unusually low friction, a complete 36–42 case campaign, mastery content, strong controller/Deck fit and a demo that exposes the real hook.

## 2. Monetization boundary
**FROZEN:** premium one-time purchase.

Not allowed:
- ads;
- consumable hints;
- paid retries/lives;
- battle pass;
- gacha/loot boxes;
- premium currency;
- subscription dependency;
- grind accelerators;
- live-service retention obligations;
- content gating by engagement streak.

Optional soundtrack/artbook is implementation/business-flexible and must not contain mechanical content.

## 3. Working launch-price band
Design working band: **USD $9.99–$12.99**.

This is not a final pricing decision. Price must be empirically rechecked near launch against:
- final certified case count and measured median playtime;
- demo conversion/wishlist data;
- presentation polish;
- contemporaneous comparable releases;
- regional pricing and Steam recommendations.

Decision logic:
- $9.99 is the conservative anchor if launch settles near the 36-case floor or presentation is intentionally very minimal;
- $12.99 is justified if 42 strong cases ship, mastery/replay quality survives playtest, and presentation/audio feel materially polished;
- do not push to $14.99+ merely because some larger puzzle games do; Missing Step lacks their 100–200 puzzle volume/open-world/narrative breadth.

## 4. Campaign progression and gates
Campaign remains six acts and target 42 / quality floor 36.

Progress contract:
- Act I cases 1–3 are mandatory onboarding.
- After those, each act unlocks through a **completion quota**, not strict linear completion.
- Default target for a 42-case campaign: complete **5 of 6** in Act I, **5 of 7** in Acts II–V, and **6 of 8** in Act VI to unlock the next act / ending gate.
- If launch contracts to 36, act quotas scale so that roughly 75–80% of available cases in an act are enough to progress, while preserving all mandatory onboarding cases.
- The player may revisit skipped cases at any time.
- No stars, currency, XP or score gates.

Reason: a single logic puzzle should never permanently block access to the rest of a premium campaign.

## 5. Ending vs completion
**Ending:** earned by reaching the end of Act VI and satisfying its act quota. All cases are not required.

**Campaign Complete:** all launch cases solved.

**Mastery Complete:** all designated Band-4/mastery cases solved; this is optional and not required for ending.

The UI must distinguish these states. Do not imply the player “failed to finish the game” because optional hard cases remain.

## 6. Skip policy
No consumable skip token exists.

After mandatory onboarding, unsolved cases may simply be left and another unlocked case selected. The quota model is the skip system.

For a case currently blocking a quota, the UI may say “Solve any 5 of 7 cases in this act to continue,” never “use skip.” This avoids turning skips into a resource or shame mechanic.

## 7. Demo contract
Demo uses the eight-case curriculum already frozen in Phase 5.

Rules:
- demo cases are canonical full-game cases, not simplified demo-only mechanics;
- demo exposes CLAMP, duplicate-position reasoning, same-tick A->D and a small two-delete teaser;
- demo completion does not alter full-game difficulty or grant mechanical bonuses;
- demo remains replayable after completion;
- store messaging should foreground `delete one step -> loop contracts -> rows re-phase`, not generic factory automation.

### Demo -> full carry-over
The demo and full game may have separate Steam app IDs, so carry-over is an explicit game-level import contract rather than assumed platform magic.

On first full-game boot:
1. search for a compatible local demo progress payload;
2. show `Import demo progress` if found;
3. import completed canonical case IDs, accessibility/settings and relevant tutorial-seen flags;
4. never import solver/certificate internals or arbitrary executable data;
5. keep import idempotent: re-import cannot revoke full-game progress or duplicate achievements;
6. if demo data version is older, migrate through explicit version rules or safely ignore incompatible fields.

If import is unavailable, the first eight cases are still short and replayable; purchase never depends on import succeeding.

## 8. Hint/help boundary
Normal help can explain **rules**, not solutions.

Always-free help:
- opcode definitions;
- start-anchor/deletion semantics;
- A->D execution order;
- CLAMP next-tick behavior;
- target predicate meanings;
- Preview controls;
- playback stepping/speed/accessibility.

Optional per-case `Nudge` may exist only if playtesting proves necessary. Frozen maximum scope:
- one authored conceptual hint per case;
- it may point to a relationship/family, e.g. “Watch what repeats on ticks 4–8,” or “These two PUSH tokens close different gaps”;
- it may not name a token ID, correct opcode, deletion pair, solution period vector or pass/fail prediction;
- using Nudge never changes progression, achievements or completion status.

No solver-generated “hot/cold”, partial correctness, recommended deletion or oracle mode in normal play.

## 9. Achievements
Target launch set: **12 achievements**, all compatible with retries, Preview, accessibility and hints.

Progress achievements:
1. **The First Gap** — solve first canonical case.
2. **Read the Loop** — complete Act I.
3. **Through the Window** — complete Act II.
4. **Which One?** — complete Act III.
5. **Same Tick** — complete Act IV.
6. **False Friends** — complete Act V.
7. **Two Absences** — reach the ending through Act VI quota.

Mastery/completion achievements:
8. **Nothing Missing but the Step** — solve every launch campaign case.
9. **Coupled Rhythm** — solve every designated Act-VI mastery case.
10. **Position Matters** — solve a certified positional-duplicate F4 case.
11. **In Order** — solve a certified same-tick F5 case.
12. **Clean Run** — solve a designated certified case whose target includes `BLOCKED_PUSH_COUNT == 0`.

Achievement rules:
- no achievement for no-retry / first-try / speedrun / no-Preview / no-hint / high playback speed;
- no achievements that accessibility settings can invalidate;
- achievements unlock from canonical case-completion/progression events, not fragile animation events;
- imported demo completion may retroactively satisfy corresponding full-game achievements once full-game ownership/runtime initializes, using idempotent reconciliation.

Steamworks currently supports persistent achievements/stats associated with the user's Steam account and offline caching; implementation may use that platform layer, but local campaign save remains authority for game progression.

Source: https://partner.steamgames.com/doc/features/achievements

## 10. Replay incentives
Replay is understanding-focused rather than score-grind.

Allowed:
- replay any solved case instantly;
- inspect prior selected deletion(s);
- compare one's own alternate successful routes only if a late TRACE_MULTI case intentionally exists;
- optional personal `Solved` / `All Cases` / `Mastery` summaries;
- optional case-family filters after campaign completion.

Not allowed at launch:
- global leaderboards;
- time pressure medals;
- move-count medals (the edit budget is already fixed);
- daily generated puzzles;
- streak rewards;
- XP levels;
- randomized loot;
- completion percentages that count settings/tutorial actions as grind.

## 11. Steam platform baseline
Launch baseline:
- Steam achievements;
- Steam Cloud for versioned local save files where integration proves reliable;
- full controller support / correct active-input glyphs;
- Steam Deck-compatible UI/performance targets already frozen in Phase 6;
- offline single-player remains fully playable; platform outage cannot block campaign.

Steam Cloud is synchronization, not the only persistence layer. Local atomic/versioned saves remain required. Steam's current documentation supports Cloud synchronization and roaming files; achievements also cache offline.

Sources:
- https://partner.steamgames.com/doc/features/cloud
- https://partner.steamgames.com/doc/features/achievements
- https://partner.steamgames.com/doc/steamhardware/compat

No Steam leaderboards, inventory, workshop or networking are required for launch.

## 12. Adversarial commercial/retention review
### Grind
PASS: no XP/currency/streaks; progress is case understanding only.

### One puzzle blocks purchase value
PASS: act quotas allow several unresolved cases after onboarding.

### Skip destroys curriculum
PASS: mandatory first three + act-local quotas preserve exposure, while later gates assume already introduced rules only.

### Demo is misleadingly easier than full game
PASS by contract: eight canonical cases reach same-tick and coupled-edit teaser rather than ending after tutorials.

### Demo gives away too much
PASS: it gives the full *verb*, not the full combinatorial campaign. The product sells depth from recombination, so hiding the real mechanic would hurt conversion more than help.

### Price/value mismatch
MITIGATED, empirical gate retained: $9.99–12.99 only; final price waits for certified count/playtime/polish and launch-market recheck.

### Achievement exploit through re-import
PASS by contract: achievement reconciliation is idempotent and based on union of completed canonical case IDs.

### Punishing accessibility/help
PASS: no achievements/progression depend on Preview, Nudge, playback mode, retry count, control method or accessibility settings.

### Solver leakage becomes default play
PASS: Nudge is authored conceptual help only; solver remains certification infrastructure.

## 13. Phase-7 acceptance gates
- premium boundary: PASS;
- working launch-price band + empirical gate: PASS;
- campaign pacing/unlocks: PASS;
- non-blocking skip model: PASS;
- ending vs all-cases completion: PASS;
- demo subset/carry-over/replay: PASS;
- achievements/mastery/replay: PASS;
- hint/help non-oracle rule: PASS;
- Steam baseline without live-service dependency: PASS;
- grind/demo/price/exploit hostile review: PASS.

**PHASE 7 COMPLETE.**

## Phase 8 handoff
Define implementation architecture without writing production code: engine/runtime direction, pure deterministic Rules Core, exact data/certificate schemas, runtime/campaign/UI boundaries, save schema and migrations, demo-import contract, Steam abstraction, localization/input architecture, performance budgets, validation/test hooks and implementation order. Preserve the mechanical authority exactly.