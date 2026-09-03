# GAME #015 — PHASE 10 ADVERSARIAL REVIEW

Date: 2026-09-03
Status: PHASE 10 COMPLETE / PHASE 11 SPECIFICATION FREEZE NEXT
Working title: **FRESH COAT**
Design complete: NO

## 0. Method and authority
This pass re-read `START_HERE.md`, `STATUS.md`, `GAME_INDEX.md`, and every active Game #015 authority file named by STATUS, including the Phase-9 superseding patches. It attacks the frozen design destructively rather than narrating another playthrough.

Severity scale: `S0` note, `S1` minor, `S2` material, `S3` design-blocking. Verdicts: `KEEP`, `PATCH`, `KILL`.

No production implementation is started here. Market/platform assumptions relevant to commercial/technical scope were already freshly checked on 2026-09-03 in Phases 7–8; this pass does not introduce a new market-dependent decision.

## 1. Executive result
Fresh Coat survives Phase 10. No `S3 KILL` finding remains. The core remains unusually coherent because the same exact rule — directional exposure of self-obligated physical workpieces, persisted across at most two passes — produces tutorials, cross-stage planning, cavities, role reversal and capstones without adding a late subsystem.

Five specification patches are required before freeze:
- preview must expose factual region state without making pose enumeration frictionless;
- atomic-region presentation must have a strict renderer/truth correspondence contract;
- hints must not combine across tiers into an implicit solution script;
- progression prerequisites need a canonical per-case table at freeze rather than only prose predicates;
- cloud/demo/achievement merge needs one explicit post-merge reconciliation order.

All five are specification closures, not new mechanics.

---

## 2. Attack matrix

### A10-01 — Novelty decay across FC01–FC24
**Severity: S2 — KEEP with content gate.**

Attack: normalize each family to what the player actually reasons about. F1–F3 are all one-pass occlusion and could feel like increasingly constrained blocker placement; F4–F5 are exposure scheduling/history; F6 adds self-occlusion topology; F7 role reversal; F8 coupling. The risk is strongest in FC03/FC07 and FC08/FC09, where “masker has own target” can repeat under different chain lengths.

Why it survives: the campaign has three genuine macro transitions: direct masking -> constrained mask dependency -> two-stage persistent history -> topology/role reversal. Late difficulty is not object-count inflation.

Required freeze gate: Phase 11 must preserve the Phase-5 repetition signature and additionally require a one-line `new deduction pressure` for every FC01–FC24 entry. FC03 vs FC07 and FC08 vs FC09 receive explicit pairwise non-isomorphism review. If an authored pair cannot state a different elimination step, replace the later case rather than add geometry.

### A10-02 — Exposure preview as brute-force accelerator
**Severity: S2 — PATCH.**

Attack: current preview is exact and always available. Because placement is discrete, a player could cycle every pose while watching exposed/protected badges, turning spatial prediction into search even without a Check button.

Killing preview is rejected: it is also the core readability/accessibility tool and E1 requires players to understand exposure.

**Patch P10-P1 — Preview transaction discipline**
1. Preview remains exact, factual and freely available; no cooldown, resource or penalty.
2. During rapid pose cycling/placement animation, preview updates only after the semantic arrangement has settled/been accepted, never for transient hover/intermediate transforms.
3. Preview shows exposure for the selected/current arrangement but never target-relative correctness, difference-from-previous, “number correct”, aggregate score, or auto-highlighting of changed target obligations.
4. Target cards do not change success/error styling in response to preview before Spray.
5. Object/region inspection may answer `EXPOSED NOW / PROTECTED NOW`; it may not enumerate which blocker causes the state unless that blocker is directly visually evident from ordinary scene geometry.
6. E3 remains the empirical defense: if players still systematically cycle states, revise the affected case/socket domains rather than weaken factual inspection.

This keeps experimentation humane without creating a high-bandwidth oracle.

### A10-03 — Four-object cognitive/visual load
**Severity: S2 — KEEP.**

Phase-9 object-grouped target cards repair bookkeeping. The remaining danger is simultaneous region count and blocker silhouettes. Phase-5 already caps meaningful visible/inspectable atomic regions around 16 and FC24 at four objects. Five objects remain exceptional and are not required by the canonical final capstone.

Hard review rule: FC21–FC24 fail content acceptance if the canonical camera plus selection/isolation cannot let a tester verbally identify each current blocker relation without free-camera hunting. Do not solve overload with x-ray, solver overlays, fifth object, or smaller regions.

### A10-04 — Renderer vs certified truth / partial regions
**Severity: S2 — PATCH.**

The technical spec correctly makes certification authoritative, but a remaining ambiguity exists when a semantic region is fully classified while decorative bevels/material boundaries make it appear partly visible/hidden.

**Patch P10-P2 — Visual-semantic correspondence**
1. Every gameplay atomic region has a dedicated render-selection mask/material mapping derived from the same authored region boundary used by certification.
2. Decorative bevels may exist only outside target-bearing semantic area or must inherit an unambiguous owner region; they cannot visually split a gameplay region.
3. A shipping legal arrangement is rejected if canonical presentation suggests a positive-area exposure state contrary to certified truth, even when exact gameplay geometry is technically correct.
4. Region-boundary overlay in Inspect mode must trace certified semantic boundaries, not artist UV/material seams.
5. Any `PARTIAL_INVALID` certification result is build-failing and cannot be hidden by rendering.

### A10-05 — Eight-family freshness signatures
**Severity: S2 — KEEP.**

The normalized signature is sufficient only if future-transition equivalence is included. Phase 8 already prevents stage-A over-collapse by requiring identical target-relevant B reachability. Preserve that rule in repetition comparison. Mesh/color/title changes never waive similarity.

Pairwise watch list for Phase 11: FC03/FC07, FC08/FC09, FC10/FC12, FC13/FC14, FC16/FC18, FC19/FC20. Each pair must differ in proof topology, not merely constraint count.

### A10-06 — 2-of-3 progression, gates, demo import, Continue
**Severity: S2 — PATCH.**

P9-P1/P2 resolve semantics but leave implementation room to encode slightly different prerequisite logic in UI and runtime.

**Patch P10-P3 — Canonical prerequisite table**
Phase 11 must publish one machine-transcribable table for FC01–FC24 containing `family_visibility_predicate`, `case_prerequisite_ids`, and `concept_requirement_tags`. This table is the sole progression authority. UI locks, Continue, demo import reconciliation and tests derive from it; no separate hard-coded family/gate logic is allowed.

Imported later completions remain visible and count as completion evidence but do not cause prerequisite predicates for unrelated incomplete cases to be skipped.

### A10-07 — Hint tiers leaking the solution cumulatively
**Severity: S2 — PATCH.**

Individually the three hint tiers are safe, but sequential tier 1 + tier 2 + tier 3 can identify both the critical region and necessary relation, effectively leaving only one legal pose in small cases.

**Patch P10-P4 — Hint cumulative-information budget**
- Hints are authored/reviewed as a cumulative set, not independently.
- Tier 3 may state one necessary elimination fact only if tiers 1–2 plus that fact still leave at least two materially distinct player actions/configuration classes whenever the case naturally has them.
- If the puzzle is too small to preserve two classes, tier 3 may instead explain a rule interaction already visible in the failed attempt; it must not name the remaining configuration.
- No hint sequence may identify both the required blocker identity and its socket/pose when either is the central deduction.
- Certifier proof metadata may seed authoring but never generate shipping hint text automatically.

### A10-08 — Controller/keyboard/accessibility parity and modal races
**Severity: S1 — KEEP.**

Abstract actions, two-step placement, modal input consumption and mixed-device focus are sufficiently specified. Acceptance tests must include full campaign navigation with controller only and keyboard only, not just puzzle manipulation. Exposure preview, target cards, conflict dialogs, corrupt-save recovery and demo CTA all need non-pointer focus paths.

### A10-09 — Spray/Undo/reset idempotency and corrupt recovery
**Severity: S1 — KEEP.**

The transaction model is strong: construct next state, durable atomic checkpoint, semantic advance, presentation; transaction IDs prevent double coat application. Reset is disabled during semantic transaction and animation callbacks cannot mutate stale attempts. Corrupt editable snapshots fall back independently from durable spray checkpoints.

Required implementation test remains crash/fault injection at every transaction boundary, but no design rule is unresolved.

### A10-10 — Cloud divergent attempts / Dynamic Cloud Sync / demo duplication
**Severity: S2 — PATCH.**

Existing merge classes are sound, but the order among import, completion union, progression recomputation and achievement reconciliation should be frozen to avoid duplicate/temporarily contradictory states.

**Patch P10-P5 — Post-merge reconciliation order**
For any cloud merge or demo import:
1. validate/migrate all candidate documents;
2. resolve profile identity and import fingerprint/attempt lineage;
3. union monotonic completion/tutorial facts;
4. select exactly one in-progress attempt branch without splicing;
5. persist the merged semantic profile atomically;
6. recompute case/family availability from the canonical prerequisite table;
7. recompute achievement eligibility from merged completion facts;
8. compare against achievement ledger/platform state and issue each missing unlock idempotently;
9. choose Continue target from P9-P2;
10. only then expose the reconciled UI.

Platform achievement failure is retryable platform state and cannot roll back local completion.

### A10-11 — Achievements / FINAL_CASE_CLEARED vs CAMPAIGN_COMPLETE
**Severity: S1 — KEEP.**

P9-P4 cleanly separates ending from 24/24. Family achievements are 3/3. The commercial draft's optional alternate-solution achievement remains risky because it can create completion pressure around undisclosed solution classes. Recommendation for Phase 11: omit it from the frozen baseline unless detection is already mechanically meaningful; target 11 achievements (8 family + first two-pass + first A->B + 24/24) is coherent and filler-free.

### A10-12 — Authored source / certified package / runtime / renderer ambiguity
**Severity: S1 — KEEP after P10-P2.**

The six-layer authority chain in Phase 8 is clear. Shipping builds consume certified packages only; source hash mismatch fails build. Renderer never performs gameplay raycasts. P10-P2 closes the remaining presentation-boundary ambiguity.

### A10-13 — Scope creep pressures
**Severity: S3 if introduced — KEEP current exclusions.**

Attack candidates: third coat, second rearrangement, free spray, tape/stickers, cleaning, paint economy, fifth-object norm, more booth directions, procedural endless mode. Every one either changes the mental timeline, adds a parallel masking system, creates dexterity/simulation burden, or hides content exhaustion.

Verdict: all remain forbidden for 1.0. If 24 cases cannot stay fresh under current grammar, cut/replace cases or kill/reopen the design; do not rescue it with these features.

### A10-14 — Commercial value / price / demo without padding
**Severity: S2 — KEEP as empirical commercial gate.**

A 24-case 3–6h target can support the planning range only if polish/reveal satisfaction and case density validate it. No rule can prove price. C1/C2 remain legitimate release gates. Do not add filler to hit playtime. The seven-case demo is unusually generous relative to 24 total cases, but that is acceptable only if it converts by demonstrating F1/F3/F4/F5 depth rather than exhausting novelty. C2 must measure both duration and whether players perceive meaningful unexplored mechanics after the finale.

### A10-15 — Empirical gates E1–E5 / C1–C6
**Severity: S1 — KEEP, with classification.**

None is an unresolved game-design rule.

Implementation/playtest blockers for release:
- E1 spatial predictability;
- E2 four-object readability;
- E3 reasoning vs blind permutation;
- E4 24-case freshness;
- E5 reveal satisfaction;
- C2 demo pacing/novelty remainder;
- C6 title clearance before public store identity.

Commercial decisions, not design-freeze blockers:
- C1 final price;
- C3 conversion telemetry;
- C4 localization breadth;
- C5 Trading Cards eligibility.

The rules needed to build tests for E1–E5 are already specified. Therefore they may remain empirical gates after design freeze.

---

## 3. Cross-system exploit review

### Preview + target rail
No target-relative preview styling. A player may manually compare factual exposure with targets — that is legitimate reasoning. The game must not perform the comparison before Spray.

### Undo + achievements
Unlimited Undo cannot invalidate achievements. No achievement records failure count, attempt count or “clean solve.” This prevents save/undo manipulation from becoming an economy.

### Demo import + family milestones
Imported FC01/02/03 etc. count exactly as real case completions. A family 3/3 achievement unlocks if the union truly contains all three stable IDs; skipped cases remain absent. No demo-only achievement ledger exists.

### Cloud + ending
If FC24 completion arrives from cloud, `FINAL_CASE_CLEARED` becomes true. Main-ending presentation may be marked seen separately so it is not forced repeatedly on every device. `CAMPAIGN_COMPLETE` still derives only from 24 IDs.

### Case content updates
If a certified case changes after release, stable case ID may remain only when success semantics remain equivalent. A materially redesigned puzzle should receive a content revision and invalidate only incompatible in-progress arrangement snapshots, never completed-case evidence without an explicit migration reason.

---

## 4. Phase-10 superseding patches

The following are later authority than conflicting earlier wording:
- **P10-P1:** exposure preview transaction discipline / no target-relative preview feedback;
- **P10-P2:** strict visual-semantic atomic-region correspondence;
- **P10-P3:** Phase 11 must freeze one canonical machine-transcribable prerequisite table;
- **P10-P4:** hint tiers reviewed under a cumulative-information budget;
- **P10-P5:** deterministic post-cloud/demo merge reconciliation order.

Phase 11 should consolidate P9-P1..P9-P5 and P10-P1..P10-P5 into final authority rather than leaving implementation to reconcile scattered prose.

---

## 5. Kill criteria rechecked
The design would be killed/reopened before production if any of these becomes necessary:
- human play requires exposure matrices/x-ray solver overlays rather than spatial reading;
- four-object capstones require tiny semantic regions or free camera hunting;
- late cases need third coat/second rearrangement/new masking subsystem for freshness;
- E3 playtests show systematic pose enumeration as dominant strategy across representative cases and bounded-domain redesign cannot fix it;
- E4 cannot produce 24 cognitively distinct certified cases under the frozen grammar;
- renderer cannot visually correspond to exact certified exposure without misleading gaps/partial-looking regions.

None is currently proven true; each has a buildable empirical test.

---

## 6. Phase-10 conclusion
**PHASE 10 = COMPLETE.**

Findings: 15 attack areas; 5 explicit specification patches; 0 unresolved S3 design blockers; core concept survives.

`DESIGN COMPLETE = NO` because Phase 11 has not yet consolidated the authority and passed the freeze checklist.

## NEXT ACTION — PHASE 11 SPECIFICATION FREEZE
Re-read all active authority including this file. Produce `GAME15_FINAL_FREEZE.md` as the implementation-facing canonical authority index and acceptance contract. It must:
1. consolidate all Phase-9 and Phase-10 patches without contradiction;
2. freeze the exact FC01–FC24 prerequisite table required by P10-P3;
3. freeze baseline achievement set or explicitly omit the alternate-solution achievement;
4. classify E1–E5/C1–C6 as implementation/release gates vs non-blocking commercial decisions;
5. state authority order and which earlier files remain supporting authority;
6. enumerate production acceptance criteria, test obligations and forbidden drift;
7. verify that no important gameplay decision remains for implementation to invent.

If the checklist passes, set `DESIGN COMPLETE = YES`, attempt migration to the dedicated Fresh Coat repository if it exists, and follow the factory continuity rule exactly if it does not.