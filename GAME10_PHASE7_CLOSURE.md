# GAME #010 — PHASE 7 ECONOMY / RETENTION / COMMERCIAL CLOSURE

Date: 2026-08-31
Status: **PHASE 7 COMPLETE**
Game: Luggage Carousel Zero *(working title)*

Authority: all prior active Game #010 authorities -> `GAME10_COMMERCIAL.md` -> this file. This file resolves progression, mastery, achievement and save-visible commercial fields where earlier wording was incomplete.

---

## 1. Campaign progression simulation exposed and repaired one ambiguity

The earlier phrase "completing a case unlocks the next case" could not actually support a blocker skip: if case N blocked the player, case N+1 would never become reachable. The intended one-skip philosophy therefore needs an explicit, bounded progression action.

### Canonical act progression
- Five acts A–E use their frozen campaign order/counts.
- A01 -> A02 -> A03 are **strict mandatory tutorial prerequisites**. No skip is available for those three.
- From A04 onward, and throughout Acts B–E, cases begin sequentially: the first not-yet-reached case is the current frontier.
- Completing the frontier case unlocks the next case normally.
- **Once per act**, when the player is blocked on the current frontier, they may choose `Skip for now`. This unlocks the next case, marks the frontier case `SKIPPED_OPEN`, and consumes that act's single skip allowance. It does not mark the case complete.
- After the single skip is used, later frontier advancement in that act is strict until completion; there is no second skip token, recharge, currency or timer.
- The skipped case remains playable at any time forever.
- The next act unlocks when the current act has **all but one** of its cases basically completed and all hard tutorial prerequisites relevant to that act are satisfied.
- Entering the next act does not erase the unresolved skipped case.
- Basic ending access requires completing the final required frontier in Act E under the same rule; perfect mastery is never required.
- `All Cases Complete` is tracked separately from reaching the ending.

This is a progression affordance, not a consumable economy.

---

## 2. A–E hostile progression walkthrough

Assume target architecture A7/B8/C8/D9/E10.

### Fresh full-game start
1. A01 only is unlocked.
2. A01 completion unlocks A02; A02 completion unlocks A03.
3. A03 completion enables normal act frontier/skip behavior starting A04.
4. Player completes A04, then becomes stuck on A05.
5. `Skip for now` on A05 unlocks A06 and records `A.skip_used=true`, `A05=SKIPPED_OPEN`.
6. Completing A06 unlocks A07. Completing A07 yields 6/7 A cases complete, so Act B unlocks while A05 remains visible/open.
7. No second A skip is possible.

### Replay / clear the blocker
- Player may return from B at any time and solve A05.
- A05 becomes COMPLETE; A becomes 7/7.
- Clearing A05 changes no already-unlocked content backward and grants no currency.

### Middle acts
- B–D follow the identical once-per-act skip rule.
- A player can therefore reach the next act with exactly one unresolved case from the prior act, but cannot chain two unresolved blockers inside one act.
- Because every skipped case stays open, the system avoids a permanent content-loss path.

### Act E / ending
- One E blocker may likewise be skipped for now.
- Reaching the final frontier and meeting E's all-but-one completion threshold permits the ending/campaign-complete state.
- `ALL_CASES_COMPLETE` remains false until every skipped case across A–E is later cleared.

### Failure/reinstall/cloud
- Skip state is durable progression data, not case-session state.
- Reinstall/cloud restore must reproduce the same unlocked acts, frontier, skip-used flags and skipped-open cases from save data or deterministic recomputation.

**Walkthrough verdict:** one blocker can be bypassed without converting progression into a free case-select or grind economy.

---

## 3. Demo import simulation

The seven-case demo may reference campaign cases from several acts because it is a curated teaching path, not the full campaign gate order.

### Import contract
- Demo and full game use stable canonical `case_id` values.
- Demo records completion, best ticks, settings and tutorial acknowledgements in the same logical save schema subset as the full game.
- On first full-game load, demo data is merged **idempotently**: completion can only advance, best-tick records can only improve, settings import only on first migration unless user has already changed full-game settings.
- Demo does **not** import act unlocks, frontier positions or skip-used flags.
- Full-game progression is then deterministically recomputed from imported case completions plus strict A01–A03 prerequisites.

Example: if demo already completed A01, A07, B01 and C01-like canonical cases, full game still requires A02 and A03 before normal progression opens. Once a later act legitimately unlocks, an already-completed imported case within that act counts as complete and the frontier skips over it automatically.

### Achievements on import
- Demo never grants platform achievements.
- Full game evaluates achievement predicates after successful import and grants any qualifying achievements exactly once.
- Repeated imports are safe and cannot duplicate progress or regress records.

This matches current Steamworks guidance that demos may share cloud save data with the full game and that achievements are better granted from the full game after loading demo progress.

---

## 4. Efficient Route adversarial review

### Risk 1 — "efficiency" could teach that any miss is waste
A core insight is that an intentional miss can be part of the **minimum-tick** solution. Therefore a marker based on minimum ticks does not mathematically punish intentional waiting; in some cases it positively certifies that the apparently wasteful miss was optimal.

Repair: the marker is never introduced before the first intentional-miss lesson. The win panel first explains it in/after Act C: `Efficient Route means minimum total carousel Advances for this case. A deliberate miss can still be part of the Efficient Route.`

### Risk 2 — premature optimization can distort first solves
Repair:
- minimum tick target is hidden before first completion;
- first win always celebrates `Solved` before optional mastery information;
- no live par counter, red delta, countdown-to-medal or star loss appears during a first attempt;
- replay is optional.

### Risk 3 — equal minimum ticks but wildly different swap effort
This is acceptable. The product has one surfaced mastery dimension only. Minimum swaps remain solver/internal analytics, not a second medal.

### Risk 4 — solver change invalidates old marker
Certification version is saved with case content, not the player record. On content update, current solver certificate defines the target. If a best historical tick count still meets the new minimum, marker remains; otherwise the marker is recomputed from retained `best_ticks`, never silently from a stale boolean.

**Verdict: KEEP `Efficient Route` with the delayed/explanatory surfacing above.** Phase 10 may still remove the visible label if playtesting shows the wording itself creates anti-wait bias, but minimum-tick records remain safe internal data.

---

## 5. Exact base achievement list — 12

Achievement IDs are stable semantic identifiers; storefront names may be localized/renamed without changing triggers.

1. `ACT_A_COMPLETE` — basically complete every Act A case.
2. `ACT_B_COMPLETE` — basically complete every Act B case.
3. `ACT_C_COMPLETE` — basically complete every Act C case.
4. `ACT_D_COMPLETE` — basically complete every Act D case.
5. `ACT_E_COMPLETE` — basically complete every Act E case.
6. `CAMPAIGN_REACHED_ENDING` — reach the campaign ending under the all-but-one act progression rule.
7. `ALL_CASES_COMPLETE` — basic completion on every shipped base-campaign case; no Efficient Route requirement.
8. `FIRST_EFFICIENT_ROUTE` — earn Efficient Route on any eligible case after mastery surfacing is enabled.
9. `TEN_EFFICIENT_ROUTES` — Efficient Route on any ten distinct base-campaign cases; no repeated farming.
10. `INTENTIONAL_MISS_LESSON` — complete canonical C01 / designated first exact intentional-miss teaching case.
11. `K2_MASTERY` — complete any certified K=2 mastery case.
12. `RETURNED_TO_BLOCKER` — use `Skip for now` on a case and later basically complete that same case.

Rejected: no-Undo, no-hint, speed-input, daily, repeated-action, accessibility-setting, hidden joke, huge-count or all-Efficient achievements.

Achievements never gate content.

---

## 6. Save-visible progression fields handed to Phase 8

Logical profile progression must preserve at minimum:
- `save_schema_version`;
- `content_manifest_version`;
- `completed_case_ids` set;
- `best_ticks_by_case` map (positive integer; absent if never solved);
- `act_unlocks` or enough canonical source data to recompute them;
- per-act `skip_used` boolean;
- per-act optional `skipped_open_case_id` (null or exactly one);
- `campaign_ending_seen` boolean;
- `demo_import_version` / migration marker;
- `tutorial_acknowledgements` for one-time callouts;
- `achievement_local_flags` / reconciliation state where platform integration needs idempotency;
- global settings/accessibility/input binding references as specified by UX authority.

Do **not** persist Efficient Route as sole truth. Derive it from `best_ticks_by_case <= current certified minimum_ticks` so certificate changes remain reconcilable.

Case-in-progress persistence is separate runtime state and is defined in Phase 8.

---

## 7. Commercial boundaries / explicit non-promises

Frozen:
- premium one-time purchase;
- working US launch band $9.99–12.99, not a frozen storefront price;
- seven-case free demo target;
- progress transfer target;
- 12 base achievements;
- once-per-act blocker skip;
- optional Efficient Route replay mastery;
- hints free and consequence-free;
- base game must stand alone.

Explicitly not promised:
- live service, roadmap cadence, DLC, cosmetics economy, Workshop, leaderboards, daily challenges, procedural endless, multiplayer, cloud account system, cross-platform account, mobile/console release, user level editor, speedrun timing features or exact launch price.

---

## 8. Phase-7 acceptance

- [x] A–E progression simulated including blocker skip and replay.
- [x] one-skip ambiguity repaired into an exact implementable rule.
- [x] demo import path simulated and made idempotent.
- [x] Efficient Route attacked for anti-wait/perverse incentives and retained with guardrails.
- [x] exact 12-achievement base list frozen.
- [x] save-visible progression fields frozen.
- [x] commercial boundaries/non-promises frozen.
- [x] implementation no longer needs to invent progression/economy rules.

**PHASE 7 COMPLETE. DESIGN COMPLETE = NO.**

Next authority: `GAME10_TECHNICAL.md`.