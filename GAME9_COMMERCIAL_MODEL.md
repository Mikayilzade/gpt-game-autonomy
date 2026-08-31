# GAME #009 — PHASE 7 ECONOMY / RETENTION / COMMERCIAL MODEL

Status: **PHASE 7 COMPLETE / PHASE 8 READY**
Date: 2026-08-31
Selected game: **Binder's Imposition** (working title)
Production implementation: **FORBIDDEN in factory**

Authority: `START_HERE.md` -> `STATUS.md` -> `GAME_INDEX.md` -> Game #009 tournament history -> `GAME9_PRODUCT_THESIS.md` -> `GAME9_MECHANICAL_ARCHITECTURE.md` -> `GAME9_CONTENT_ARCHITECTURE.md` -> `GAME9_UX_PRESENTATION_ARCHITECTURE.md` -> this file.

This phase deliberately avoids adding an economy wrapper to a finite authored puzzle game. “Economy” here means purchase/value proposition and progression pacing, not currencies, grinding, shops, consumable hints, or retention pressure.

---

# 1. Commercial thesis

Binder's Imposition is a **finite premium systemic puzzle game**. The player buys the complete campaign and receives every mechanically relevant case and feature. The commercial model must reinforce trust: no artificial friction is created in order to sell relief from it.

Frozen boundaries:
- premium one-time purchase;
- no MTX;
- no ads;
- no paid hints or consumable hint currency;
- no paid grind bypass;
- no battle pass, daily reward, login streak, rotating shop, FOMO, energy/tickets, or live-service treadmill;
- no progression currency;
- no Early Access requirement in the product thesis;
- soundtrack/artbook or genuinely substantial later expansion may exist only as optional non-mechanical products and are not required for the baseline business case.

The value proposition is **a small, polished rule system with 24–30 genuinely distinct authored deductions**, not raw hour count or hundreds of permutations.

---

# 2. Fresh market snapshot — 2026-08-31

Current Steam evidence was refreshed because price and storefront expectations are time-sensitive.

Useful comparison points:
- `Patrick's Parabox`: $19.99, a highly regarded compact systemic puzzle with a downloadable demo and 350+ handcrafted puzzles. It establishes that a pure elegant puzzle can sustain a $19.99 list price, but its content count is far beyond Game #009 and therefore is not a direct value-count comparison.
  - https://store.steampowered.com/app/1260520/Patricks_Parabox/
- `The Roottrees are Dead`: $19.99, premium deduction/mystery puzzle, released 2025, with very strong user reception. It supports a $19.99 reasoning-game reference point where experience value is not measured by action-system breadth.
  - https://store.steampowered.com/app/2754380/The_Roottrees_are_Dead/
- `Chants of Sennaar`: $19.99, premium puzzle/adventure, Steam Cloud and achievements. It is broader and more asset-heavy than Game #009, so it is an upper-comparison for perceived presentation breadth rather than a direct scope match.
  - https://store.steampowered.com/app/1931770/Chants_of_Sennaar/
- `The Case of the Golden Idol`: currently $17.99 and still offers a demo. It is a useful lower/mid reference for a compact authored deduction product.
  - https://store.steampowered.com/app/1677770/The_Case_of_the_Golden_Idol/
- `Blue Prince`: $29.99 list price and 16 Steam achievements; currently observed at a 40% promotion. It is much larger and broader than Game #009, so $29.99 is explicitly **not** the baseline target.
  - https://store.steampowered.com/app/1569580/Blue_Prince/
- `Paper Trail` occupies the visible “paper + folding + puzzle” language on Steam, but its hook is folding the world itself rather than inverse book-imposition reasoning. Store copy for Game #009 must distinguish these immediately.
  - https://store.steampowered.com/app/1889740/Paper_Trail/
- `Is This Seat Taken?` shows current appetite for approachable placement/constraint logic without timers or leaderboards. Game #009 is mechanically more abstract and should not falsely market itself as a generic cozy organizer.
  - https://store.steampowered.com/app/3035120/Is_this_Seat_Taken/

Steamworks rules observed 2026-08-31:
- launch discounts may run 7–14 days and cannot exceed 40%; normal discounts have a 30-day cooldown, while seasonal-sale handling has specific exceptions;
- discounts of 20%+ may trigger wishlist notifications;
- Steam demos can share cloud storage with the full app so players continue from demo progress;
- Valve recommends disabling achievements inside the demo and granting earned equivalents when the full game loads the transferred save;
- current announced seasonal sales include Autumn Sale 2026 (Oct 1–8) and Winter Sale 2026 (Dec 17–Jan 4).

Sources:
- https://partner.steamgames.com/doc/marketing/discounts
- https://partner.steamgames.com/doc/store/application/demos
- https://partner.steamgames.com/doc/marketing/upcoming_events

Market evidence is a snapshot, not a revenue forecast. Price must be rechecked near release against final campaign quality, length, presentation, reviews of comparable new titles, regional pricing tools and actual demo response.

---

# 3. Price / value recommendation

## 3.1 Recommended band

**Current design-stage list-price band: USD $14.99–$19.99.**

Preferred planning point: **$17.99** if the shipped product has:
- >=24 certified strong campaign cases;
- D01–D06 quality at or above the frozen demo gates;
- polished tactile fold presentation;
- full controller/Deck-quality UX;
- robust Undo/Redo/save/recovery;
- enough late-game synthesis that the campaign feels like mastery rather than an extended tutorial.

A **$14.99** launch list is defensible if the final strong campaign lands near the 24-case floor or average completion time is materially shorter than expected. **$19.99** becomes defensible only if the product reaches roughly 28–30 strong cases, presentation is exceptional, the demo validates broad comprehension/desire, and playtest completion time/value perception supports it.

Do not choose $19.99 merely because strong comparables use it. Do not inflate case count to justify price.

## 3.2 Launch discount stance

Commercial design does not require a launch discount. If used, planning default is **10%**, not a deep launch sale. This preserves premium-value signaling while giving wishlisters a modest release incentive. Final choice belongs to release planning using then-current wishlist, festival and calendar evidence.

Never schedule the release around a sale merely to manufacture a discount. Steam itself notes future sale opportunities are recurring.

## 3.3 Value language

Store value should be expressed as:
- a complete finite campaign;
- 24–30 carefully differentiated cases;
- four visible fold-transform families and layered global constraints;
- no timers, grind or random solutions;
- fast reversible experimentation;
- a free demo teaching the actual core system.

Do **not** promise a fixed number of hours before measured playtest data exists.

---

# 4. Campaign progression / unlock pacing

Progression is **authored chapter-gated with limited local choice**, not currency-based and not a fully open puzzle grid.

Canonical unlock rule:
1. D01–D04 / Chapter I tutorial spine is linear because each teaches prerequisite transform literacy.
2. After the tutorial spine, completing the chapter's designated **keystone case** unlocks the next chapter.
3. Within Chapters II–VI, ordinary cases unlock in small authored clusters of 2–3 where prerequisite metadata permits; the player may choose order inside that cluster.
4. A chapter keystone requires completion of its explicit prerequisite cases, not every optional branch case.
5. No score, badge, move count or speed condition gates the next baseline case.
6. A player may replay any solved case at any time.
7. Accessibility settings never affect unlock eligibility.

This gives stuck players some lateral movement without allowing a new transform to appear before its prerequisite mental model.

Content data therefore needs later technical fields:
- `prerequisite_case_ids[]`;
- `is_keystone`;
- `chapter_id`;
- optional `recommended_after[]` for presentation only.

There is no XP, currency, level, shop, unlock token or collectible needed to progress.

---

# 5. Optional mastery / badges / stats

Badges are **post-completion mastery annotations**, never stars required for progression.

## 5.1 Badge vocabulary

Maximum three reusable badge types are allowed, and a case need not expose all three:

1. **Predicted** — satisfy that case's authored prediction prompt(s) before first resolved Preview. This rewards mental modeling, not speed.
2. **Direct Bind** — after the case's first resolved Preview, reach a successful Commit without another incorrect Commit. Preview count itself is not punished.
3. **Constraint Craft** — case-specific optional challenge using only existing mechanics, e.g. solve with a specified template/signature role when solver-certified as meaningful. This appears only where it creates a genuinely different deduction.

A badge condition must be solver/telemetry-verifiable and known before the attempt. No hidden badge criteria.

Forbidden badge types:
- real-time speedrun target as baseline content;
- “never use Undo”;
- “never use accessibility feature”;
- excessive click/move optimization unless the case was explicitly authored around a meaningful solution distinction;
- arbitrary repeated completion/grind;
- daily/weekly streak.

## 5.2 Stats

Per-case stats may store:
- solved yes/no;
- badges earned;
- first-solve Preview count;
- incorrect Commit count;
- optional elapsed **thinking-session** time for personal information only.

No global leaderboard is baseline. No percentile comparison is baseline. Time is never used to shame a player or gate an achievement.

The UI should default to solved/badges, with detailed stats secondary.

---

# 6. Difficulty, hints and accessibility boundary

There is one canonical puzzle validity model. Accessibility settings do not alter whether a solution is correct.

Assistance is layered and non-punitive:
1. replay the transform/rules explanation;
2. highlight which **final predicate family** is currently impossible/failed after a resolved attempt, without naming a source move;
3. optional authored nudge states a reasoning question (“Which signature can contain both required facing pages?”), not a placement;
4. final explicit hint may identify a global deduction (“Gold stock must be outermost”) but should still leave local arrangement to the player.

Using hints does **not** block campaign progression or Steam achievements tied to completion. A specific optional mastery badge may require solving without the final explicit hint only if this is shown in advance; accessibility settings themselves never invalidate it.

No paid hints, hint currency, cooldown, lives or retry cost.

---

# 7. Steam achievements / platform feature boundaries

Target **14–18 Steam achievements**; planning set = **16**.

Recommended distribution:
- 6 chapter-completion achievements;
- 1 campaign-completion achievement;
- 4 genuine mastery milestones (e.g. earn a defined number of Predicted badges; solve one mature three-signature synthesis challenge; complete a certified alternate Constraint Craft solution);
- 3 discovery/interaction achievements that reward understanding rather than random clicking;
- 2 broad completion/mastery achievements.

Rules:
- no achievement requires a difficulty mode;
- no achievement requires disabling accessibility;
- no achievement requires online multiplayer, leaderboard rank or calendar date;
- no grind achievements such as 1,000 Previews/Undos;
- no achievement requires intentionally corrupting/failing a case repeatedly;
- achievements must be idempotently recomputable from persistent completion/mastery state where practical;
- demo does not fire Steam achievements; transferred demo state may cause equivalent eligible achievements to unlock once in the full game, consistent with Steamworks guidance.

Baseline Steam features:
- Steam Achievements: YES;
- Steam Cloud: YES, strongly recommended for PC/Deck continuity;
- controller/Steam Input-aware glyph support: YES per Phase 6;
- Family Sharing: no gameplay dependency; support if platform/package configuration permits;
- Trading Cards: NOT a design requirement;
- Workshop: NO baseline;
- leaderboards: NO baseline;
- Remote Play Together: NO need;
- online account: NO;
- telemetry: optional, privacy-respecting and non-authoritative; game remains offline playable.

---

# 8. Demo package — D01–D06

The frozen demo is the first **six authored campaign cases**, not a separate simplified rule set.

Demo arc:
- D01: four-face inverse-fold surprise;
- D02: prediction reinforcement;
- D03: duplex/orientation;
- D04: first second-signature/nesting concept;
- D05: facing/global relationship;
- D06: capstone where reading order alone is insufficient and material/signature role decides the solution.

Target playtime remains **20–30 minutes**, empirical rather than guaranteed.

## 8.1 Demo end state

After D06 success:
1. show the completed bound object and the exact deduction just mastered;
2. show a short non-spoiler 10–20 second montage of later vocabulary: T8, trim/blank survival, three-signature synthesis;
3. CTA hierarchy: `Wishlist / Follow Full Game` (pre-release) or `Buy Full Game` (post-release), then `Replay Demo Cases`, then `Exit`;
4. state plainly that demo progress carries into the full game;
5. do not fake urgency, countdowns, limited bonuses or “continue now” pressure.

## 8.2 Demo save transfer

**YES — transfer progress.** Demo and full game use a compatible versioned campaign-save schema. Prefer Steam shared Cloud storage where configuration permits, while retaining local import/recovery behavior.

Transferred state includes:
- D01–D06 solved flags;
- eligible badges/mastery records;
- settings/accessibility/input preferences where safe;
- no transient workbench history is required after the demo capstone.

Full game first launch detects demo progress, validates schema/version, imports idempotently, and places the player at the first newly available full-game case. Player can replay D01–D06 at any time.

Demo achievements remain disabled. On full-game import, any completion achievement whose requirements are genuinely met by imported state is granted once by the full game.

---

# 9. Post-campaign retention

The game is allowed to end.

After campaign completion, retention consists only of:
- replay any case;
- finish optional badges/Constraint Craft variants already authored;
- inspect personal case stats;
- optional compact **Mastery Shelf** containing 4–8 solver-certified variants assembled from existing mechanics, only if they pass the same anti-isomorphism quality floor as campaign cases.

The Mastery Shelf is a stretch within the 34-case soft ceiling, not a promise of infinite content.

Explicitly no:
- dailies/weeklies;
- procedural infinite mode promised for launch;
- rotating challenges;
- streaks;
- seasonal FOMO;
- live-service roadmap obligation;
- grind to fill a meta bar.

If players finish, feel satisfied and uninstall, the product has succeeded.

---

# 10. Working title / storefront positioning

## 10.1 Title decision

**`Binder's Imposition` remains an internal working title, not frozen storefront title.**

Reason: “imposition” precisely names the domain but is specialist vocabulary and does not communicate the mechanic to a general puzzle buyer. “Binder” also risks suggesting cozy bookbinding/crafting simulation, while the product is a deterministic logic puzzle.

No strong current exact-title collision was found in the fresh search, but absence of a search result is not trademark clearance. Legal/storefront title clearance is an implementation/release obligation.

## 10.2 Storefront naming direction

Future title candidates must score well on:
- understandable without print vocabulary;
- suggests pages/book/fold/order rather than shop management;
- searchable and pronounceable;
- visually compatible with the flat-sheet -> booklet GIF;
- no confusion with `Paper Trail` or generic bookbinding simulators;
- no promise of realistic printing training.

Phase 7 does **not** freeze a replacement title merely to manufacture novelty. Working codename stays stable until a later naming/marketing validation pass.

## 10.3 Store short-description direction

Preferred plain-language copy:

> **Arrange pages on flat sheets, then fold and nest them into a tiny book. What looks wrong on the table has to read perfectly when it's bound.**

Supporting bullets should foreground:
- predict surprising folds;
- choose which sheets belong inside each other;
- satisfy facing, orientation, material and trim constraints;
- Undo freely and fold-preview instantly;
- solve a finite handcrafted campaign with no timers or grind.

Do not lead with “imposition,” “signature,” or vocational terminology. Those words may be taught secondarily after the visual hook is understood.

Store tags to test near release: `Puzzle`, `Logic`, `Singleplayer`, `Indie`, `2D`/`Stylized` depending final rendering, `Difficult` only if playtests support it. Do not self-position as `Simulation` or `Cozy` unless the shipped experience actually earns those expectations.

---

# 11. Commercial acceptance tests

C01. A new player can understand the store short description without knowing “imposition” or “signature.”

C02. Store capsule/trailer can demonstrate flat wrong-looking layout -> fold -> correct reading order within 10 seconds.

C03. Base purchase exposes every baseline campaign case without currency, grind or extra payment.

C04. No mechanical action consumes a monetized resource.

C05. Campaign progress is never gated by badges, speed, move count, hints used or accessibility configuration.

C06. Chapter prerequisite graph cannot expose a mechanic before its teaching prerequisite.

C07. At least one alternate case is available in a normal later-chapter cluster when the recommended case is temporarily difficult, where content dependencies allow it.

C08. Keystone completion cannot accidentally require every optional branch case unless explicitly authored as prerequisite.

C09. Solved cases remain replayable permanently.

C10. Badge conditions are visible before attempt and deterministically evaluable.

C11. No badge requires disabling accessibility or avoiding Undo.

C12. Detailed personal stats do not alter solution validity or progression.

C13. Hint use cannot consume currency, trigger cooldown, reduce campaign rewards or block completion.

C14. Full explicit hint still leaves at least one meaningful player reasoning/manipulation step in every case where feasible.

C15. Steam achievement set contains no calendar/FOMO/online/grind requirement.

C16. Demo contains exactly the real D01–D06 rule path rather than demo-only mechanics.

C17. Demo end montage does not reveal solutions to later cases.

C18. Demo can be completed offline after installation.

C19. Demo save import is versioned and idempotent: repeated import cannot duplicate progression or achievements.

C20. A corrupt/incompatible demo save fails safely without harming an existing full-game save.

C21. Imported D01–D06 completion never forces the player to skip them; replay remains available.

C22. Demo itself does not fire Steam achievements.

C23. Full game can grant legitimately earned demo-equivalent achievements once after validated import.

C24. Steam Cloud conflict cannot silently replace a newer valid campaign state with older demo-only progress; merge/recovery rules must be specified in Phase 8.

C25. Post-campaign screen has a clear “campaign complete” state and does not imply endless obligations.

C26. Mastery Shelf, if shipped, contains only certified non-filler cases and stays inside content ceiling unless scope is explicitly reopened.

C27. No daily/weekly/live event is necessary for any achievement or content access.

C28. Price shown in marketing never promises hours not backed by measured data.

C29. Regional prices use then-current Steam pricing tools/recommendations rather than a hand-authored USD conversion table frozen in design.

C30. A launch discount, if chosen, obeys then-current Steam rules and is not required by game logic/content.

C31. Store copy never claims professional bookbinding/printing training.

C32. Store copy distinguishes the game from generic paper-folding adventure: the object is a book and the reasoning is inverse page arrangement/nesting.

C33. `Binder's Imposition` can be replaced globally as title without changing save IDs, case IDs or mechanical data contracts.

C34. Accessibility settings can be changed at any time without achievement/progression penalty.

C35. Offline campaign completion is authoritative; reconnecting to Steam can synchronize achievements/cloud without invalidating local completion.

C36. No server availability is required to launch, solve, save or finish baseline campaign.

C37. Purchase state never affects solver validity or case rules.

C38. Optional soundtrack/artbook cannot contain mechanically required hints unavailable to base-game buyers.

C39. If later paid puzzle expansion is considered, baseline campaign remains complete and no frozen base case is removed to create DLC value.

C40. Release-price choice is re-evaluated against final certified case count, measured completion time, demo conversion/feedback and current comparable pricing before store submission.

---

# 12. Empirical commercial gates

These are intentionally not guessed into truth during design.

E1. **Demo completion:** representative puzzle-interested testers should commonly finish D01–D06 inside the intended 20–30 minute band without tutorial confusion dominating play. If median is much longer because of UI/mental-model failure, repair onboarding rather than advertise a longer demo.

E2. **Demo desire:** after D06, a clear majority of target testers should want at least one of the teased later deductions. Ask what they think later play adds; if answer is “more page numbers,” the commercial hook is failing.

E3. **Price perception:** test $14.99/$17.99/$19.99 positioning against final build quality and measured campaign length without telling testers the desired answer. Final price is not frozen until this evidence exists.

E4. **Campaign breadth:** >=24 cases must pass content certification and human fun/repetition review. Price cannot rescue a campaign below the content-quality floor.

E5. **Badge motivation:** optional badges should encourage prediction/mastery for interested players without making ordinary solvers feel they played “wrong.” Remove or hide them more deeply if they distort baseline behavior.

E6. **Hint dignity:** players who use hints should still report understanding the eventual solution. If explicit hints turn cases into transcription, redesign hint steps.

E7. **Store comprehension:** at least ~80% of target viewers shown the short copy + 10-second clip should correctly describe the core as arranging flat pages so folding/nesting produces the requested book, not as a bookshop/crafting sim.

E8. **Title comprehension:** compare working title against clearer candidates before store lock. Retain `Binder's Imposition` publicly only if it does not materially reduce recall/comprehension and passes collision/legal checks.

E9. **Transfer reliability:** demo -> full save transfer must survive fresh install, same-machine install, Steam Cloud enabled/disabled, interrupted write and pre-existing full-save scenarios before release.

E10. **Post-campaign restraint:** if mastery variants are weak or repetitive, ship none. Retention minutes are not a quality KPI by themselves.

---

# 13. Phase-7 freeze

Frozen unless later adversarial review proves a contradiction:
- one-time premium complete-game model;
- current planning price band $14.99–$19.99, preferred evidence-dependent planning point $17.99;
- no economy/grind wrapper;
- authored chapter-gated prerequisite progression with small local branches;
- badges optional/non-gating;
- hints free and non-punitive;
- accessibility independent of difficulty/mastery punishment;
- 14–18 achievement target, planning set 16;
- Steam Cloud + achievements baseline, no leaderboard/Workshop/account requirement;
- D01–D06 real-campaign demo;
- demo progress transfer recommended and required by current spec;
- demo achievements disabled, eligible state reconciled in full game;
- finite replay/mastery postgame, no FOMO/live service;
- `Binder's Imposition` remains a working/internal title pending storefront validation;
- commercial copy leads with the flat-sheet -> folded-book transformation, never specialist terminology.

DESIGN COMPLETE = **NO**.

## NEXT DESIGN QUESTION

Phase 8 must specify the implementation contract without writing production code: engine/runtime recommendation and decision gate; authoritative state architecture; immutable case data schema; transform/solver/validator interfaces; history transactions; save schema/versioning and atomic recovery; demo/full import merge rules; Steam Cloud conflict policy; achievement reconciliation; input abstraction; deterministic animation boundary; localization-ready content representation; performance budgets; test hooks; content-validation pipeline; build/package boundaries; and implementation order for a fresh dedicated repository.