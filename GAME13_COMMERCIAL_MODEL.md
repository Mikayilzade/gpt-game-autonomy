# GAME #013 — PHASE 7 COMMERCIAL / PROGRESSION MODEL

Date: 2026-09-02
Status: PHASE 7 COMPLETE — PASS
Selected concept: **SEAL BREAK** (working title)
Authority: Phase 4 mechanics, Phase 5 content, and Phase 6 UX remain authoritative. This file adds product packaging/progression only; it does not authorize new gameplay systems.

## 1. Commercial thesis
SEAL BREAK is a finite premium authored deduction game. It should be sold on the clarity of its destructive-witness hook and the quality of its certified cases, not on hours, grind, procedural volume, narrative padding, daily retention, or collectible systems.

Recommended launch-price posture: **US$9.99–12.99**, with **$11.99** the current planning anchor if the 30-case target ships at the expected polish/readability level. This is a recommendation to revisit near release, not a frozen store price.

Fresh September-2026 context: compact current puzzle products span roughly the high-single-digit to low-teens range. Steam lists *What's the Password?* (May 28, 2026) at $7.99 with a demo and an advertised ~2-hour/100-puzzle compact experience; *Puzzle Spy International* (Mar 30, 2026) is $12.50 with a demo, 11 substantial puzzles and a 2–7 hour claim. The broader Puzzle Lovers storefront snapshot also shows many logic/puzzle products clustered around $7.99–19.99 before discounts. SEAL BREAK should therefore avoid both bargain-bin signaling and a $15+ posture unsupported by its intentionally compact scope.

Discount philosophy:
- launch discount, if used: modest 10% rather than training buyers to wait;
- ordinary early discounts: infrequent and shallow;
- deeper discounts only after meaningful product age / portfolio growth;
- never design content, achievements or progression around sale events.

## 2. Campaign progression
Progression is **small-branch threshold-based**, not a rigid 30-case line and not a free grid.

Each act contains five cases. The first four are the commercial-floor spine; the fifth is the target extension/capstone. Within an act:
- first case unlocks when the act opens;
- completing a case unlocks its explicit Phase-5 prerequisite successors;
- where two successors depend only on the same prerequisite, both may open together;
- the next act unlocks after completing all four floor cases of the current act;
- the fifth target-extension case is optional for forward progression and unlocks when its own prerequisites are solved.

This preserves the Phase-5 teaching graph while allowing a stuck player limited lateral movement. No XP, currency, stars, score thresholds or daily gates exist.

Completion states:
- `CASE SOLVED` — one case;
- `ACT CORE COMPLETE` — four floor cases in an act solved;
- `ACT MASTERED` — all five target cases in the act solved;
- `CAMPAIGN COMPLETE` — all 24 floor cases solved;
- `FULL CASEBOOK COMPLETE` — all certified shipping cases solved.

If only 24 cases ship, marketing says 24 authored cases and there is no empty capstone slot. If 30 ship, marketing says 30. Never advertise the target count before certification locks shipping content.

## 3. Demo package
The demo is a **six-case curated vertical slice**, not simply cases 1–6 in order. It must prove the real late loop while remaining teachable.

Canonical demo beats:
1. SB_01 — direct tear cause;
2. SB_02 — first-crossed semantics;
3. SB_06 — paired witness discrimination;
4. SB_11 — survivor / omitted-compartment reasoning;
5. SB_17 — inverse witness placement under fixed history;
6. a dedicated demo-safe presentation of the late coupled loop derived from an already-certified campaign case (prefer SB_24/SB_26 lineage) with prerequisites/tutorial prompts embedded, not a mechanically unique demo-only rule.

Target first-play demo duration: roughly **30–60 minutes**, highly skill-dependent. The sixth beat must show seal selection + bounded history choice/reconstruction so the store promise is truthful.

Demo end state:
- show `DEMO COMPLETE` after beat 6;
- allow replay of all six demo cases;
- show a restrained full-game callout: six acts, certified authored campaign, deeper combinations of the same witness rules;
- do not show locked fake levels or grind counters.

Carryover:
- demo save uses the same schema/versioned case IDs as full game;
- full game imports solved status/settings for campaign-identical demo cases;
- the demo-only presentation wrapper for beat 6 does not mark a full-game case solved unless its mechanical case ID and acceptance contract are exactly identical;
- import is one-way/idempotent and must never overwrite newer full-game progress;
- settings/accessibility preferences may carry over independently.

## 4. Hints
Hints exist because a finite premium puzzle game should not strand players, but they are **optional, non-monetized, case-authored, and explicitly requested**.

Three-step maximum per substantive case:
1. **Observation hint** — points to a relevant immutable relation already inspectable, e.g. compare which seams S and T share;
2. **Deduction hint** — states a reasoning principle applicable to the case without naming the exact edit, e.g. if they break at different checkpoints, their shared trigger cannot explain both breaks;
3. **Nudge** — may identify a constrained witness/compartment or eliminate a class of possibilities, but must still leave the player to construct the submission.

No hint appears automatically because of time/failures. No hint currency, cooldown, ads, purchase or penalty exists. Hint use does not alter progression.

Oracle boundary: ordinary edit UI remains exactly Phase-6 non-oracular. Opening the Hint panel is a deliberate request to receive authored assistance; it never activates live correctness coloring, hypothetical simulation, closeness scoring or next-edit auto-completion.

## 5. Replay incentives
Replay comes from understanding and mastery, not repeatable reward systems.

Allowed incentives:
- revisit any solved case and inspect/replay its successful committed trace;
- solve optional fifth cases / optional expert cases;
- after campaign completion, a case may display whether the player has discovered another materially valid certified solution class **only when the content author explicitly marked MULTI_VALID_INTENTIONAL**; no demand to exhaust arbitrary permutations;
- personal self-directed clean solving after hints is allowed, but there is no punitive permanent badge for having used a hint.

Rejected:
- timers/speed medals;
- move counts/stars;
- daily puzzles required for retention;
- streaks;
- random/procedural challenge promise;
- grind currencies;
- global leaderboards.

## 6. Achievements
Keep the set small and robust: planning target **10–12** Steam achievements, all derivable from stable progression/state facts.

Recommended set:
- First Break — solve first case;
- Read the Witnesses — complete Act II core;
- Nothing Happened — complete Act III core;
- Place the Proof — complete Act IV core;
- Reconstruct It — complete Act V core;
- Seal the Case — complete campaign floor;
- Full Casebook — solve every shipping case;
- Six Acts Mastered — solve every fifth/capstone case when 30-case target ships;
- Without a Nudge — solve one designated mid/late case without opening hints (single positive mastery achievement, not a global anti-hint punishment);
- Review the Evidence — use replay/scrub after a successful late case;
- optional 1–2 content-stable mastery achievements only if they can be defined without hidden tricks or fragile exact action sequences.

If 24 cases ship, achievements referencing fifth/capstone cases are removed/reworded before store configuration. No achievement requires speed, perfect input, inaccessible audio/color cues, secrets unrelated to puzzle mastery, or permanently missable actions.

## 7. Steam/platform posture
Required product posture for v1:
- PC/Steam-first;
- complete controller and keyboard paths; Steam Deck/handheld readability is a release gate, not a certification claim;
- Steam Achievements;
- Steam Cloud for progress/settings where implementation is robust;
- save architecture must tolerate Cloud/local conflicts and version migration; Steam's current Cloud documentation includes Dynamic Cloud Sync for Deck suspend/resume scenarios, so Phase 8 must define deterministic merge/reload behavior rather than assuming process-lifetime ownership of the save;
- Family Sharing where platform defaults permit;
- demo/full save relationship as above.

Localization posture:
- architecture must be localization-ready from Phase 8;
- initial commercial target: English plus a practical first localization wave chosen near release from store/wishlist/playtest evidence;
- current design recommendation for budgeting/testing: English source plus French, German, Spanish (Spain/LatAm neutral where feasible), Brazilian Portuguese, Simplified Chinese, Japanese, Korean, and Russian interface/subtitles if resources permit;
- no language is promised until localization QA and font/layout coverage pass, especially at 200% text scaling.

Not v1 requirements:
- Workshop/editor;
- leaderboards;
- trading cards;
- online accounts;
- cross-platform proprietary cloud;
- multiplayer/social systems.

## 8. Monetization boundary
Frozen:
- one premium base game;
- free demo;
- no ads;
- no MTX;
- no paid hints;
- no energy/lives;
- no premium currency;
- no battle pass;
- no subscription requirement;
- no live-service cadence pressure;
- no gameplay-affecting DLC planned into the base design.

A future substantial authored expansion may be sold only as conventional expansion content after the base campaign is complete and only if it uses certified same-vocabulary depth rather than withheld base-game cases. Cosmetic DLC is not part of the product thesis.

## 9. Optional expert cases 31–36
Cases 31–36 are **not a launch promise**. Admission requires all of:
1. existing 30 cases already pass certifier/human anti-repetition review;
2. candidate case uses only frozen v1 mechanics/predicates/modes;
3. it demonstrates a deduction interaction not already represented adequately by a shipping case;
4. human review finds a non-enumerative solve path;
5. handheld evidence/geometry remains readable;
6. it does not delay polishing/certifying the 24-floor/30-target campaign.

If admitted, expert cases are optional post-campaign content unlocked after Campaign Complete; they do not gate the ending or base achievements except an explicitly updated `Full Casebook` count before release freeze.

## 10. Store/trailer truth contract
Store capsule/trailer should communicate:
- finite tamper seals across visible seams;
- choose/read an opening plan;
- commit;
- deterministic seals tear at checkpoints;
- infer or construct the required evidence.

The trailer must show a real coupled late-loop case within its first substantive gameplay sequence, not imply freeform destruction, physics simulation, detective narrative, random cases or procedural infinity.

Store copy may call the game compact/authored/deduction-focused. Duration claims are deferred until external playtest telemetry exists.

## 11. Commercial acceptance gates
Phase 7 passes only because the following are now explicit:
1. premium price posture fits compact contemporary puzzle comparables;
2. progression respects Phase-5 prerequisites and gives limited lateral movement without grind;
3. demo contains all six true-hook beats including coupled late play;
4. demo carryover cannot falsely solve a mechanically different full case;
5. hints are requested, authored, free and isolated from ordinary edit/oracle UI;
6. replay has no timer/star/grind distortion;
7. achievements derive from stable progression/mastery facts;
8. advertised content count equals certified shipping count;
9. 24-case floor remains a complete campaign; 30 is target, 31–36 optional only under strict admission;
10. no retention/monetization feature changes puzzle quality or mechanics;
11. Steam Cloud/Deck behavior is deferred to a deterministic Phase-8 persistence contract rather than hand-waved;
12. no production implementation is authorized here.

## 12. Phase verdict
**PHASE 7 PASS.** No contradiction with frozen mechanics/content/UX was introduced.

Proceed to Phase 8 Technical Implementation Specification. Phase 8 must define runtime/certifier shared rules, data schema, deterministic resolver, state machine, persistence/cloud merge and demo import, input abstraction, localization, performance budgets, test hooks, implementation order and acceptance tests without beginning production implementation.
