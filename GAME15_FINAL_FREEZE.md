# GAME #015 — FINAL SPECIFICATION FREEZE

Date: 2026-09-03
Status: **DESIGN COMPLETE = YES / MIGRATION PENDING**
Working title: **FRESH COAT**

## 0. Freeze verdict
Game #015 passes Phase 11. A fresh implementation session can build the game without inventing important gameplay, progression, persistence, UX, commercial, or technical rules.

This file is the implementation-facing final authority index and acceptance contract. It consolidates all narrow Phase-9 and Phase-10 repairs. Earlier files remain supporting authority unless explicitly superseded here.

No production implementation has started inside the factory.

---

## 1. Frozen product identity
**Hook:** stack ordinary objects so they mask one another, spray the pile in one or two fixed passes, optionally rearrange once, then unpack the objects to prove that every semantic region received exactly the required ordered coat history.

Frozen product form:
- finite premium PC/Steam-first spatial deduction game;
- 24 handcrafted cases, FC01–FC24, grouped F1–F8;
- controller-complete and Steam-Deck-readable baseline;
- 2–5 objects per case, 4 normal late ceiling, 5 exceptional only;
- maximum two fixed spray passes and one rearrangement boundary;
- coat histories RAW, A_ONLY, B_ONLY, A_THEN_B;
- discrete sockets and orthogonal authored poses only;
- exact semantic region exposure/history truth;
- unlimited undo/reset; no punishment for experimentation;
- no binary arrangement Check oracle;
- factual current exposure inspection only;
- no free-aim spraying, fluid physics, tape/stickers, paint economy, cleaning loop, timers, lives, third coat, second rearrangement, procedural filler, multiplayer, leaderboard pressure, paid hints, grind, FOMO, or service-game layer.

The differentiator remains: **the workpieces themselves are reusable masks, those mask objects also carry their own final paint obligations, and persistent exposure history across two stages creates the late-game reasoning.**

---

## 2. Gameplay truth and state contract
Authoritative case truth is the Phase-4/8 semantic model:
`Case = Objects + atomic semantic Regions + discrete Sockets/Poses + legal Compatibility + BoothStages + RearrangementContract + Targets + SymmetryMetadata`.

Runtime never derives puzzle truth from camera pixels, renderer visibility, physics contacts, raster depth, antialiasing, material appearance, or freeform raycasts.

Each spray stage is an atomic semantic transaction:
1. current arrangement must be certified/legal;
2. obtain the certified exposure set for that arrangement/stage;
3. append that stage's coat ID exactly once to each exposed atomic region;
4. durably checkpoint the complete semantic next state;
5. only then advance presentation/state-machine stage;
6. presentation animation can be skipped/interrupted without changing truth.

Main campaign ceiling is universally frozen at:
`arrange A -> SPRAY A -> optional one rearrangement -> SPRAY B -> reveal`.
One-pass cases omit B. There is no third spray or second rearrangement in 1.0.

Atomic regions are binary EXPOSED/OCCLUDED per legal arrangement. Any positive-area partial exposure is `PARTIAL_INVALID` and content/build failing until the region is subdivided or the pose is removed.

---

## 3. Consolidated Phase-9 / Phase-10 patches

### FZ-P1 — progression authority
2-of-3 family completion controls normal family visibility only. Individual case playability additionally uses the canonical prerequisite table in Section 4. Case predicates override family UI state. Demo-imported case completion satisfies its stable-ID prerequisite but never fabricates skipped completions or 3/3 family completion.

### FZ-P2 — Continue authority
Continue resolution order is exactly:
1. resume one valid in-progress attempt if present;
2. otherwise choose the lowest-display-order unlocked incomplete primary case;
3. if blocked only by a mandatory concept-introduction case, choose that gate case;
4. if all 24 are complete, enter campaign-complete/replay surface.

Never derive Continue from highest completed numeric case.

### FZ-P3 — editable arrangement persistence
Explicit exit, application suspension, and Dynamic Cloud Sync hand-off persist both the latest durable spray checkpoint and the current valid semantic editable arrangement snapshot for EDIT_A/EDIT_B. A corrupt editable snapshot may be discarded independently while preserving the last committed checkpoint.

### FZ-P4 — completion states
`FINAL_CASE_CLEARED = FC24 completed at least once`.
`CAMPAIGN_COMPLETE = every stable case ID FC01–FC24 completed`.
The ending/credits may trigger on first FC24 clear. The canonical campaign-complete achievement requires 24/24.

### FZ-P5 — late target readability
High-target-count cases use object-grouped collapsible target cards. Selecting a workpiece scopes its target card; selecting a target row focuses the exact semantic region. Collapsed headers may summarize neutral target facts but never current correctness or intended blocker/pose information.

### FZ-P6 — preview transaction discipline
Exposure preview is exact, factual, free, and non-punitive, but updates only for accepted settled semantic arrangements, never transient hover/interpolated transforms. It cannot display target-relative correctness, number-correct, deltas, solution heatmaps, intended blockers, or aggregate score. Target cards do not turn success/error-colored from preview state before Spray.

### FZ-P7 — visual/semantic correspondence
Every gameplay atomic region has render-selection/boundary mapping derived from the same authored semantic boundary used by certification. Decorative bevels/material seams cannot make a gameplay region appear meaningfully split or contradictory. A legal scene whose canonical visual presentation contradicts certified exposure is rejected by content QA even if semantic geometry is technically correct.

### FZ-P8 — hint cumulative-information budget
Three hint tiers are authored and reviewed cumulatively. Combined hints may identify a relevant obligation and one necessary elimination fact, but must not collapse the central deduction to a named blocker+socket/pose. Where a small puzzle cannot retain two materially distinct actions after tier 3, tier 3 explains a rule interaction visible in the player's failed attempt instead of naming the remaining configuration. Certifier proof metadata never auto-generates shipping hint text.

### FZ-P9 — cloud/demo reconciliation order
For cloud merge or demo import, execute exactly:
1. validate/migrate candidates;
2. resolve profile identity and import fingerprint / attempt lineage;
3. union monotonic completion/tutorial facts;
4. choose exactly one in-progress branch without splicing;
5. atomically persist merged semantic profile;
6. recompute case/family availability from Section 4 table;
7. recompute achievement eligibility;
8. compare local ledger/platform state and issue missing achievement unlocks idempotently;
9. select Continue target by FZ-P2;
10. expose reconciled UI.
Platform achievement API failure never rolls back local completion.

---

## 4. Canonical FC01–FC24 prerequisite table
This table is the **sole machine-transcribable progression authority**. UI locks, runtime playability, Continue, demo import reconciliation, and tests derive from the same data. No parallel hard-coded gate logic is allowed.

Definitions used below:
- `COMPLETE_2(Fn)` = any 2 of the 3 cases in family Fn are complete.
- Concept tags are declarative proof assumptions; they are not separate unlock systems.
- For families F2–F8, all three member cases become visible when the family predicate passes, but a case may still be individually locked by `case_prerequisite_ids`.

| Case | Family visibility predicate | case_prerequisite_ids | concept_requirement_tags |
|---|---|---|---|
| FC01 | TRUE | — | direct_occlusion_intro |
| FC02 | TRUE | FC01 | pose_orientation |
| FC03 | TRUE | FC01 | self_obligated_mask_intro |
| FC04 | COMPLETE_2(F1) | — | adjacent_region_differential |
| FC05 | COMPLETE_2(F1) | — | blocker_footprint_comparison |
| FC06 | COMPLETE_2(F1) | — | future_access, two_stage_foreshadow |
| FC07 | COMPLETE_2(F2) | FC03 | self_obligated_mask, dependency_edge |
| FC08 | COMPLETE_2(F2) | FC03 | self_obligated_mask, dependency_chain |
| FC09 | COMPLETE_2(F2) | FC03 | self_obligated_mask, backward_dependency_chain |
| FC10 | COMPLETE_2(F3) | — | two_pass_intro |
| FC11 | COMPLETE_2(F3) | FC10 | two_pass, persistent_raw |
| FC12 | COMPLETE_2(F3) | FC10 | two_pass, intentional_deferral |
| FC13 | COMPLETE_2(F4) AND FC10 | — | ordered_history_intro |
| FC14 | COMPLETE_2(F4) AND FC10 | FC13 | ordered_history, adjacent_history_differential, self_obligated_mask |
| FC15 | COMPLETE_2(F4) AND FC10 | FC13 | ordered_history, persistent_raw |
| FC16 | COMPLETE_2(F5) AND FC13 | — | cavity_semantics_intro, ordered_history |
| FC17 | COMPLETE_2(F5) AND FC13 | FC16 | cavity_semantics, raw_rim_protection |
| FC18 | COMPLETE_2(F5) AND FC13 | FC16 | cavity_semantics, fixed_target_pose, blocker_rearrangement |
| FC19 | COMPLETE_2(F6) | FC10 | two_pass, mask_role_reversal |
| FC20 | COMPLETE_2(F6) | FC10 | two_pass, self_obligated_role_reversal |
| FC21 | COMPLETE_2(F6) | FC10, FC13 | two_pass, ordered_history, role_reversal_chain |
| FC22 | COMPLETE_2(F7) | FC10, FC13 | coupled_mask_dependency, ordered_history |
| FC23 | COMPLETE_2(F7) | FC10, FC13 | cross_pass_shared_masker, ordered_history |
| FC24 | COMPLETE_2(F7) | FC10, FC13, FC16 | ordered_history, cavity_semantics, role_reversal, coupled_capstone |

Additional invariant:
- any future content revision that introduces A_THEN_B into a case must add FC13 prerequisite unless that case is FC13 itself;
- any future content revision whose intended proof depends on cavity semantics must add FC16 prerequisite unless that case is FC16 itself;
- any future case assuming established two-pass manipulation must add FC10 prerequisite unless it is FC10 itself;
- any future case assuming self-obligated masking as established knowledge must add FC03 prerequisite unless it is FC03 itself.

Demo sequence remains real campaign content:
`FC01 -> FC02 -> FC03 -> FC05 -> FC10 -> FC13 -> FC14` (or the previously authorized smaller mechanically identical FC14-family finale only if C2 pacing validation requires it). Imported completions remain visible even when campaign families around them are not yet naturally reached.

---

## 5. Frozen baseline achievements
Baseline is **11 achievements**; the alternate-solution achievement is intentionally omitted.

1. F1 3/3 complete
2. F2 3/3 complete
3. F3 3/3 complete
4. F4 3/3 complete
5. F5 3/3 complete
6. F6 3/3 complete
7. F7 3/3 complete
8. F8 3/3 complete
9. first successful two-pass case
10. first successful A_THEN_B case
11. CAMPAIGN_COMPLETE (24/24)

No achievement may depend on no-hint, no-undo, speed, minimum moves, failure counts, daily play, control device, accessibility settings, or exhaustive pose/socket cycling.

Demo does not unlock platform achievements. Full build grants any achievement made eligible by imported legitimate completion exactly once after FZ-P9 reconciliation.

---

## 6. Campaign/content acceptance contract
The 24-case family plan from `GAME15_CONTENT_ARCHITECTURE.md` remains canonical:
- F1 FC01–03 direct occlusion / first self-obligation;
- F2 FC04–06 neighboring differential / future access;
- F3 FC07–09 constrained mask dependencies;
- F4 FC10–12 pass-specific exposure;
- F5 FC13–15 ordered history;
- F6 FC16–18 cavity reveal;
- F7 FC19–21 role reversal;
- F8 FC22–24 coupled capstones.

Every shipping case must carry a documented `new_deduction_pressure` line in authoring metadata. Pairwise mandatory review watchlist:
- FC03 vs FC07;
- FC08 vs FC09;
- FC10 vs FC12;
- FC13 vs FC14;
- FC16 vs FC18;
- FC19 vs FC20.

If a pair is isomorphic under the normalized exposure/dependency/rearrangement/future-transition signature and cannot name a different elimination step, the later case is replaced. New geometry, extra sockets, extra objects, or cosmetic differences do not count as freshness.

FC21–FC24 fail content acceptance if the canonical camera + selection/isolation cannot let representative testers verbally identify current blocker relationships without free-camera hunting or solver-like x-ray assistance.

Five objects remain exceptional and are **not required** by FC24; the canonical final capstone is four objects.

---

## 7. UX / accessibility acceptance
Required:
- full campaign, menus, pause, targets, conflict dialogs, recovery prompts, demo CTA operable controller-only;
- same for keyboard-only; mouse adds no exclusive capability;
- active-device glyph switching does not reset semantic focus/state;
- coat and object identity never color-only;
- scalable readable UI at 1280x800 handheld target;
- stable canonical camera; bounded comfort orbit cannot be required to discover truth;
- semantic region browser provides complete factual access to hidden/cavity target regions;
- exposure preview obeys FZ-P6;
- target rail obeys FZ-P5;
- reduced motion preserves all information;
- no audio-only puzzle truth and no timed execution.

Failure/reveal may report required history, actual history, and actual stages of exposure. It may never name intended blocker, correct socket, correct pose, closest solution, or target-relative pre-Spray correctness.

---

## 8. Persistence / cloud / demo acceptance
Required automated/fault tests:
- crash before durable Spray write -> previous checkpoint resumes;
- crash after durable semantic write but before/during animation -> complete new checkpoint resumes, never half paint;
- duplicate Spray callback/import/retry -> coat appended once only;
- Undo from post-A and post-B returns exact previously specified semantic checkpoints;
- explicit exit/suspend while editing preserves valid editable arrangement snapshot;
- corrupt editable snapshot falls back to spray checkpoint without losing profile completion;
- corrupt primary save recovers known-good backup where valid;
- unknown arrangement IDs never map to nearest geometry;
- demo import is idempotent by fingerprint;
- imported later cases do not fabricate skipped completion;
- cloud monotonic completion/tutorial sets union safely;
- divergent in-progress attempts never splice A from one branch with B from another;
- rare branch conflict uses factual case/stage/arrangement summary, never solution closeness;
- FZ-P9 ordering is covered by integration tests;
- platform achievement API failure retries without rolling back local completion.

---

## 9. Technical/build acceptance
Frozen initial implementation target remains **Godot 4.7.x stable, GDScript-first**, with gameplay data/solver/persistence boundaries independent of SceneTree identity.

Shipping build consumes certified immutable case packages only. Each package carries source-content hash and certifier version. Source/certified hash mismatch fails build.

Certifier must:
- enumerate legal discrete arrangements/transitions;
- compute exact atomic exposure;
- reject PARTIAL_INVALID;
- apply exact coat histories;
- enumerate/collapse solution classes with future-transition-safe symmetry handling;
- reject unreachable targets;
- emit repetition signatures;
- flag excessive/trivial solution classes and content-budget violations;
- retain proof metadata for designer review while preventing player-facing solver leakage.

Renderer/certified truth correspondence tests enforce FZ-P7. Decorative mesh/material drift cannot silently alter perceived masking.

Steam/platform calls remain behind a `PlatformServices` adapter; gameplay/persistence does not depend on one community Steam binding.

---

## 10. Commercial freeze vs empirical gates
The product is frozen as finite premium, no ads/paid hints/consumables/FOMO/grind. Planning price remains **US$9.99–14.99 with $12.99 center**, but exact launch price is not a design-freeze fact.

### Release-blocking empirical implementation/playtest gates
- **E1 spatial predictability:** after onboarding, fresh players correctly predict the large majority of meaningful current semantic exposure before Spray without solver overlays/camera hunting.
- **E2 four-object readability:** representative late scenes remain understandable with stable camera + selection/isolation.
- **E3 reasoning vs blind permutation:** representative players eliminate arrangement classes using masking/history reasoning rather than systematic pose enumeration; failing cases must reduce/restructure socket domains/content rather than remove factual preview.
- **E4 24-case freshness:** normalized repetition review + human testing confirms cognitive distinctness; no padding via object/socket count.
- **E5 reveal satisfaction:** unpack feels like confirmation/proof of prediction rather than opaque delayed grading.
- **C2 demo pacing/novelty remainder:** seven-case demo lands around the intended 20–30 minutes and still communicates that meaningful later reasoning remains.
- **C6 title clearance:** required before public store identity freeze.

These gates may fail content/release and force revision/reopen, but their testable rules are fully specified; they are not missing design.

### Non-blocking commercial decisions
- **C1 final price** after measured playtime, polish and launch-quarter comparables;
- **C3 conversion telemetry** for marketing decisions only;
- **C4 localization breadth** based on quality/budget;
- **C5 Trading Cards/profile items** only if platform eligibility and asset value justify them.

Telemetry must never create grind, alter puzzle truth, gate assistance, or be required for offline play.

---

## 11. Forbidden implementation drift
Implementation may not silently add or reinterpret:
- third coat / third spray;
- second rearrangement;
- free spray aiming;
- continuous object placement/rotation/physics stacking;
- masking tape/stickers as parallel system;
- paint quantity, mixing, drying, overspray, cleaning economy;
- fifth-object norm;
- diagonal/perspective-dependent booth truth;
- renderer/pixel-based exposure truth;
- target-relative exposure preview;
- Check score/nearest-solution feedback;
- paid or consumable hints;
- lives, move limits, par times, stars/XP/currency gating;
- leaderboards that reward speed/minimum moves;
- procedural endless mode used to compensate for content weakness;
- UGC/workshop/editor scope;
- multiplayer/network play;
- service-game/FOMO monetization.

If the shipped 24-case design cannot pass E1–E5 under the frozen grammar, reopen/replace affected content or the design itself. Do not rescue it through scope creep.

---

## 12. Final authority order
For Game #015 implementation, resolve authority in this order:
1. `GAME15_FINAL_FREEZE.md` — final consolidated contract and all superseding Phase-9/10 clauses;
2. `GAME15_ADVERSARIAL_REVIEW.md` — supporting attack rationale where not superseded;
3. `GAME15_PHASE9_PATCHES.md` — supporting history; consolidated clauses here supersede it;
4. `GAME15_TECHNICAL_SPECIFICATION.md`;
5. `GAME15_COMMERCIAL_MODEL.md`;
6. `GAME15_UX_PRESENTATION_ARCHITECTURE.md`;
7. `GAME15_CONTENT_ARCHITECTURE.md`;
8. `GAME15_MECHANICAL_ARCHITECTURE.md`;
9. `GAME15_PRODUCT_THESIS.md`;
10. `GAME15_ROUND_C.md`;
11. `GAME15_ROUND_B.md`;
12. `GAME15_ROUND_A.md`;
13. `GAME15_RESEARCH.md`.

Tournament/research files explain why this game was selected; they do not reopen rules frozen later.

If two supporting files conflict, the higher item above wins. If any supporting wording conflicts with this file, this file wins.

---

## 13. Final ambiguity audit
A fresh implementation session does **not** need to invent:
- core fantasy or loop;
- object/region/socket/pose truth;
- exposure definition;
- paint histories;
- stage count/order;
- rearrangement ceiling;
- targets/success/failure;
- undo/reset/checkpoint semantics;
- exposure preview boundary;
- controller/keyboard semantic actions;
- target/hint information limits;
- progression and exact case prerequisites;
- demo import behavior;
- Continue behavior;
- ending vs 24/24 completion semantics;
- baseline achievements;
- persistence/crash/cloud branch rules;
- deterministic certification requirements;
- renderer-vs-truth boundary;
- campaign families/content counts;
- commercial model boundaries;
- empirical release gates;
- forbidden scope drift.

Implementation-flexible choices remain appropriately non-game-design choices: exact art palette/materials within readability rules, exact physical button mapping subject to remapping/action parity, exact maintained Steam binding behind the adapter, exact final price/localization set/title after their empirical/commercial gates, and low-level code/module naming.

**PHASE 11 = COMPLETE.**
**DESIGN COMPLETE = YES.**

## Migration result
Dedicated target checked on 2026-09-03: `Mikayilzade/fresh-coat` does not currently exist / is unavailable through the connected GitHub repository set.

Per factory continuity rule:
- all `GAME15_*` files remain in this factory as a frozen **NON-ACTIVE safety archive**;
- migration is **PENDING**;
- no source safety file may be deleted until a dedicated repository exists and migration integrity is verified;
- pending migration does not block the factory;
- Game #016 becomes the active sequential design slot immediately.
