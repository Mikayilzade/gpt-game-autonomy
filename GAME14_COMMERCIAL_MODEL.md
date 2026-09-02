# GAME #014 — PHASE 7 ECONOMY, RETENTION & COMMERCIAL MODEL

Date: 2026-09-02
Status: COMPLETE — finite-premium package frozen; Technical Implementation Specification next.
Working title: **NEGATIVE CASTING**
Authority: `START_HERE.md` -> `STATUS.md` -> `GAME_INDEX.md` -> Game #014 tournament record -> `GAME14_PRODUCT_THESIS.md` -> `GAME14_MECHANICAL_ARCHITECTURE.md` -> `GAME14_CONTENT_ARCHITECTURE.md` -> `GAME14_UX_PRESENTATION.md` -> this file.

## 1. Phase-7 verdict
**PASS.** Negative Casting remains coherent as a 3–5 hour finite premium puzzle product without content inflation, live-service retention, currencies, score chasing or paid assistance. The 24-case floor is enough to define the product; NC25–NC30 remain optional quality-gated bonus cases rather than a commercial obligation.

Commercial identity: **buy once, solve at your pace, keep the complete game.** Retention means returning to unfinished authored cases or replaying a favorite deduction, not manufacturing daily engagement.

No production implementation begins here.

---

## 2. Fresh market / platform check — 2026-09-02
Current evidence used for this phase:
- `Is This Seat Taken?` remains a useful closest-scale commercial benchmark: $9.99, roughly 5–6 hour completion estimates in current price/history coverage, no-pressure puzzle framing, and discounts observed around 30% after launch maturity.
- `Railbound` remains $12.99 with a much larger 240+ puzzle content promise. Negative Casting should not price as if it offers that volume.
- `A Little to the Left` remains a $14.99 premium puzzle benchmark with 75–100+ puzzle/mess content and mature discounts reaching 60%; again, its content-volume proposition is materially larger.
- `The Roottrees are Dead` is $19.99, but carries substantially greater narrative/art/content scope and is not a sensible direct price anchor for Negative Casting.
- `Blue Prince` is $29.99 and currently discounted 40% to $17.99 through 2026-09-06; its scale, systemic breadth and production history place it outside the intended product tier.
- Current Steamworks discount rules: launch discounts are 10–40% for 7–14 days; a product release creates a 30-day discount cooldown, while Steam-wide seasonal-sale treatment has specific exceptions. Commercial planning must obey the current Steamworks rules at release rather than hard-coding old cooldown assumptions.

Conclusion: the credible shelf is **$9.99–$14.99 USD**, with Negative Casting best positioned around the lower-middle of that band unless final production value materially exceeds the frozen scope. Price should sell the strength of the idea, not pretend that 24 carefully authored cases equal hundreds of levels.

---

## 3. Launch price and discount policy

### 3.1 Price
**Target US base price: $11.99.**

Acceptable pre-release decision band: **$9.99–$12.99** without reopening product design. `$14.99` requires implementation-stage evidence of exceptional presentation polish and/or a shipping count near 30 with no quality dilution; it is not the default.

Regional prices should use current Steam pricing guidance / sensible purchasing-power adjustments at release. The design does not assume one global currency conversion formula.

### 3.2 Launch discount
Preferred default: **10% launch discount for 7–14 days** if commercially useful at release. No launch discount is also acceptable if wishlist/press strategy argues for it. Do not exceed 15% at launch merely to manufacture urgency.

### 3.3 Post-launch discount boundaries
Product policy, separate from Steam's platform minimum/maximum rules:
- first ordinary custom discount: target **15–20%**, only after platform cooldown permits it;
- avoid >25% in the first ~6 months absent a major strategic reason;
- 30–40% becomes reasonable only after the game is mature or for major events/bundles;
- deeper mature discounts are allowed later, but must not be part of the launch value proposition.

The implementation/release owner must re-check Steamworks discount rules at the actual release date.

---

## 4. Demo -> full game contract

### 4.1 Demo content
Frozen demo is **NC01–NC08** from Content Architecture, targeting roughly 20–30 minutes. It uses the same canonical mechanics, data schema, target semantics, controls, accessibility and renderer truth contract as the full game.

The demo is **not**:
- a special simplified ruleset;
- a timed trial;
- a random subset;
- a teaser that ends before a complete solve;
- a separate progression economy.

NC07 must reveal the second surface and NC08 must provide a satisfying synthesis solve before the purchase call-to-action.

### 4.2 Progress transfer
Preferred/frozen product expectation: if the platform/account environment permits reliable identification of compatible demo progress, full game should import:
- NC01–NC08 completion;
- current/resumable demo case state where schema-compatible;
- tutorial-seen flags;
- accessibility/control preferences where safe and appropriate.

Import is **one-way demo -> full**. The full game never depends on the demo remaining installed. If transfer data is absent, corrupt or version-incompatible, the full game starts normally with no loss beyond demo progress.

The technical mechanism and version/migration contract belong to Phase 8.

### 4.3 Demo end screen
After NC08 completion:
- celebrate the completed demo arc first;
- show a restrained preview of later two-/three-surface casting tables;
- state that the full game contains at least 24 authored cases if that count is still true at release;
- provide platform-native purchase/wishlist navigation where permitted;
- do not use countdowns, artificial scarcity or FOMO copy.

---

## 5. Campaign completion / 100% semantics

The floor campaign is **NC01–NC24**, arranged in 8 groups of 3. Completing any 2/3 unlocks the next group, as already frozen.

Canonical completion states:
- **Reached Final Group** — progression state only; not campaign completion.
- **Campaign Complete** — all 24 `required_for_floor` cases solved. This is the main ending/completion badge and the expected first-completion target.
- **All Shipped Cases** — every case included in the installed base game solved, including any quality-approved NC25–NC30. This is optional completionist status, not required to see the ending or main completion acknowledgment.
- **100% achievements** — means all platform achievements earned. Achievement design below intentionally avoids grind, speed, no-hint purity or mandatory optional-case perfection unless the optional cases demonstrably meet the same accessibility/difficulty contract.

NC25–NC30 never become required retroactively to claim `Campaign Complete` for the 24-case floor.

If post-launch free cases are added, they receive their own completion collection and do not revoke an existing campaign-complete state.

---

## 6. Hint / assist policy

### 6.1 Principle
There is **no hint currency, cooldown, penalty, score impact, achievement penalty or paid hint**. Assistance exists to prevent a player from abandoning a finite deduction game, while preserving the act of deduction.

Contribution Inspection from Phase 6 is a standard legibility tool and is **not** counted as a hint.

### 6.2 Hint ladder
Each shipping case may define up to three authored optional hint tiers. They are requested explicitly; none appear automatically.

1. **Re-orient attention** — names a semantic observation without naming a blocker/state. Example class: “A target that must stay fully lit can rule out possibilities before you try to create the shadows.”
2. **Name the relevant relationship** — identifies a surface/region or deduction family in player language, still without identifying the correct pose. Example class: “Compare the two poses that look the same on Surface A with what they do on Surface B.”
3. **Expose one deduction premise** — identifies one currently useful constraint or candidate class to compare, but does not state the final blocker pose or solve subsequent steps. Example class: “Only one remaining sculpture can block Light 2 at this sample.”

Tier 3 is the maximum standard assist. There is no `Solve`, auto-move, full route playback, remaining-solution count or correct-pose highlight in the frozen product.

### 6.3 Hint state and accessibility
Hints can be revisited after opening. Using hints never changes completion marks or achievements. The game may remember which hint tiers were opened only to restore UI state; it must not shame/rank the player.

If implementation playtesting shows that some users still become permanently blocked, adding a clearly labelled **solution reveal** would require reopening this policy because it changes the completion/achievement semantics; it is not silently assumed.

---

## 7. Achievements

Target: **10–14 Steam achievements**, with 12 as the preferred planning count. They should describe natural milestones, not impose a second metagame.

Recommended structure:
- 1: complete NC01 / first cast;
- 3–4: reach selected campaign groups / major progression beats;
- 1: complete NC08 / demo arc;
- 1: solve first 3-surface case;
- 1: Campaign Complete (all 24 floor cases);
- 1: complete a group 3/3 after only 2/3 was required to advance;
- 1–2: benign interaction/discovery achievements that cannot be permanently missed and do not require repetitive input;
- optional 1: All Shipped Cases only if NC25–NC30 ship and their accessibility/difficulty is not deliberately punitive.

Forbidden achievement conditions:
- solve without hints;
- solve under a timer or move count;
- never undo/reset/check incorrectly;
- complete repeated arbitrary actions;
- replay already-solved cases solely for a counter;
- use a specific input device;
- disable accessibility settings;
- color-dependent recognition;
- hidden one-shot missables;
- procedural/daily streaks.

Achievements must be earnable offline where Steam/platform behavior permits and synchronize when the platform reconnects.

---

## 8. Replay and challenge incentives

Replay is deliberately light:
- any solved case can be reopened immediately;
- player can reset to initial state and solve again;
- completed final casts may be viewed in a compact gallery/case browser thumbnail if implementation cost is low;
- cases with multiple accepted physical solutions may invite informal experimentation after completion, but the game does not score alternate solutions;
- NC25–NC30, if shipped, are the only planned “extra challenge” layer.

There are **no**:
- scores;
- par moves;
- speed medals;
- leaderboards;
- daily puzzles;
- procedural challenge runs;
- streaks;
- randomized retention quests;
- unlock grind.

A future level editor is not part of launch scope. Adding one is a separate product decision because moderation/distribution/UX burden is much larger than the core game.

---

## 9. Steam / Deck / cloud / offline assumptions

Product-level requirements:
- PC/Steam lead platform;
- single-player gameplay must work offline after normal platform installation/entitlement handling;
- complete default-controller path and correct active-device glyph behavior;
- handheld baseline remains 1280x800 with 1280x720/1080p/aspect validation from Phase 6;
- Steam Cloud is desired for campaign progress, case completion, achievements-supporting local state and resumable case state;
- device-specific presentation settings that can create bad cross-device behavior should remain local where practical; accessibility preferences that are safe to roam may sync;
- cloud conflict/corrupt-save behavior must prefer recoverability over silently replacing the only good progress copy;
- achievements must not be the authoritative save: local/cloud campaign state is authoritative and achievements reconcile from it where platform APIs allow;
- no always-online account, telemetry dependency or server-side puzzle validation is required.

Exact save slots/files, cloud paths, conflict strategy and schema migration belong to Phase 8.

---

## 10. DLC / expansion boundary

### 10.1 Safe content expansion
A paid or free case pack may use only the frozen canonical grammar:
- two fixed logical lights;
- geometry-derived opaque blockers;
- discrete socketed states;
- 1–3 projection surfaces within readability ceilings;
- the same four target classes;
- the same player verbs and validation semantics.

A content pack must pass the same human-route, repetition, accessibility and geometry-clearance gates as the base campaign. New cosmetic studio/table themes and new blocker **shapes** are allowed only when they obey existing opacity/state rules.

### 10.2 Design-reopening expansion
The following are **not** “just DLC content” and require reopening design/mechanics before commitment:
- third logical light channel;
- transparent/refractive/colored blockers;
- moving lights;
- free blocker translation;
- continuous rotation;
- mirrors/reflection;
- timed/moving surfaces;
- blocker powers;
- cooperative play;
- procedural generation presented as a new mode;
- editor/workshop ecosystem.

Do not sell a mechanically altered sequel-sized ruleset as if Phase 4 already specifies it.

### 10.3 Base-game integrity
No case required to understand or complete the base campaign may be DLC. DLC must not add a stronger hint system available only to purchasers. No cosmetic purchase system is planned.

---

## 11. Monetization exclusions

Frozen exclusions:
- no ads;
- no consumables;
- no premium currency or soft currency;
- no paid hints/solutions;
- no battle pass;
- no subscription;
- no loot boxes;
- no gacha/random paid rewards;
- no energy/lives;
- no FOMO rotations;
- no daily login rewards;
- no paid skip;
- no booster/XP economy;
- no gameplay grind;
- no cosmetic microtransaction store;
- no required external account for single-player progression.

A soundtrack/artbook sold separately is commercially compatible because it does not affect gameplay. A conventional substantial case-pack expansion is compatible only under Section 10.

---

## 12. Store positioning

Primary store promise should lead with the physical hook, not genre taxonomy:
**“Arrange strange sculptures between two lights. Every pose changes several walls at once; make each point receive exactly the right kind of light and shadow.”**

Store/trailer sequence should show:
1. one blocker rotates;
2. both channel-marked shadows visibly change;
3. second surface changes simultaneously;
4. target/current glyphs make the deduction legible;
5. a late 3-surface beauty shot demonstrates depth without explaining new rules.

Avoid selling on raw level count, “relaxing/cozy” alone, or claims of infinite replayability. The credible value is a compact, polished sequence of authored deductions with an unusual physical presentation.

---

## 13. Commercial acceptance gates

Phase 7 remains valid only if all are true at freeze/release review:
1. 24 floor cases independently pass content quality gates; price is not used to justify filler.
2. Median first completion remains plausibly ~3–5 hours after implementation playtest; if materially shorter, price/positioning is reconsidered before content is inflated.
3. Demo reaches NC07 second-surface reveal and ends with NC08 satisfying synthesis.
4. Demo/full rules and case truth are identical.
5. No purchase/retention system changes deduction mechanics.
6. Hints are free, optional and non-punitive.
7. Achievement completion is accessibility-safe and no-grind.
8. Campaign Complete remains all 24 floor cases even if optional launch/post-launch cases exist.
9. Offline single-player does not depend on servers.
10. Cloud loss/conflict cannot be allowed to redefine puzzle truth or silently destroy the only recoverable campaign record.
11. Store screenshots/trailer can communicate two lights + blocker + target + multi-surface consequence without solver-like UI.
12. Any future new puzzle rule triggers explicit design review instead of being smuggled into DLC/content production.

---

## 14. Phase-7 result
**PASS -> proceed to Phase 8 Technical Implementation Specification.** The finite premium product works at the 24-case floor and does not need a retention economy, extra mechanics or inflated content count.

### NEXT ACTION — PHASE 8
Create `GAME14_TECHNICAL_SPEC.md` and specify enough for a fresh implementation session to build the frozen game without inventing mechanics:
1. choose/freeze engine/runtime direction and supported desktop baseline;
2. define canonical rational geometry representation and exact segment-vs-polygon-interior algorithm/tie behavior;
3. define authored case/archetype schemas, stable ids, validation and derived-cache hashing/invalidation;
4. define runtime state machine, input abstraction, undo/redo/check and surface/inspection state boundaries;
5. define deterministic certifier + observational-equivalence + human-route verification contracts;
6. define renderer/logical-truth separation and semantic-overlay contract;
7. define persistence schema, atomic save/recovery, content revision handling, demo->full import and Steam Cloud boundaries;
8. define accessibility/settings persistence and localization-ready text/data boundaries;
9. define performance budgets for handheld baseline and maximum frozen case size;
10. define automated tests/test hooks, malformed-content rejection and implementation order through vertical slice;
11. explicitly preserve all Phase 3–7 exclusions and do not start production implementation inside this factory.
