# GAME #012 — PHASE 10 ADVERSARIAL REVIEW

Date: 2026-09-01
Status: **PHASE 10 COMPLETE — PASS WITH REPAIRS / PHASE 11 NEXT**
Product: **OPENWORK** *(provisional working title)*
Authority: destructive review and post-simulation repairs. Where this file explicitly amends earlier progression, content, persistence, input, achievement, or curation wording, this later decision controls until `GAME12_FINAL_FREEZE.md` consolidates the full authority chain in Phase 11.

No production implementation is created here.

---

## 1. Review verdict
OPENWORK survives Phase 10. No discovered flaw requires killing the product, expanding the mechanical vocabulary, enlarging the board ceiling, adding friction to retries, or adding solver-directed hints.

The review did find **four specification hazards that must be repaired before freeze**:
1. Phase-9 repairs existed only as later supersessions while older progression/persistence text still stated contradictory behavior;
2. the 30-case quality floor did not define deterministic progression if a reduced release manifest contains five rather than six cases in an act;
3. post-release removal/replacement of cases did not fully define 100% and achievement behavior;
4. held-reposition / reset / cycling semantics were not exact enough for a fresh implementer under rapid input.

All four are repaired below. Remaining uncertainty is empirical content/device/commercial validation, not missing core game design.

**Phase-10 recommendation: PASS to Phase 11 Specification Freeze.**

---

# 2. Attack A — fun / repetition / articulation collapse

## Attack
The campaign says only 4/36 cases have principal family F1, but F3/F6/F7 cases can still secretly reduce to the same player action: inspect the initial open field, spot one-cell articulation points, occupy one, then clean up secondary predicates. Family labels alone therefore do not prove experiential variety.

## Result
The design is not killed, because F2/F4/F5/F8 and the intended F6 cases have deductions that can be decisive without initial articulation closure. However, the existing quota is insufficient by itself.

## **REPAIR P10-01 — reasoning-skeleton curation gate**
Each accepted case must store a human-authored `reasoning_skeleton` containing 1–4 ordered abstract steps chosen from a controlled taxonomy:
- `CUTSET / ARTICULATION`;
- `ENCLOSURE / RING`;
- `MARKER PARTITION`;
- `BOUNDARY ALLOCATION`;
- `AREA ALLOCATION`;
- `PIECE ROLE / ORIENTATION`;
- `INVERSION / PRESERVE ROUTE`.

This metadata is authoring/curation evidence only and is never visible pre-solve.

Campaign gates:
- no more than 25% of shipping cases may be `ARTICULATION_DOMINANT`, defined as a case whose unique witness can be isolated principally from initial-state articulation/cutset reasoning before another predicate class materially narrows candidates;
- in Acts III–VI, at least **60%** of cases must have their first decisive step be something other than initial-state articulation spotting;
- no three consecutive campaign cases may share the same first two reasoning-skeleton steps;
- every act after Act I must contain at least one accepted case whose strongest visually obvious initial neck is legal to occupy but leads to a non-solution;
- a family quota never overrides this experiential gate.

### Kill condition
If a 30-case accepted manifest cannot meet these gates without adding new mechanics, **kill/redesign OPENWORK rather than pad it**.

Verdict: **PASS with measurable anti-repetition repair.**

---

# 3. Attack B — blind brute force

## Attack
Unlimited instant undo + live predicate truth makes empirical search deliberately pleasant. A strong player can use predicate cards as a feedback vector and systematically test complete placements. Search-space counts alone do not stop this; even 100 complete assignments may be tractable if each attempt is fast and piece changes are cheap.

## Existing defenses retained
- no artificial retry delay, attempt limit or fail modal;
- P9 thresholds: MID normally >=40 canonical assignments, LATE >=100, MASTERY >=500, finale >=1000 preferred;
- content must have intended 2–4 invariant chains;
- current-state feedback remains allowed and must not be weakened merely to obstruct brute force.

## **REPAIR P10-02 — anti-enumeration acceptance test**
For representative Acts III–VI content, curation records both:
1. `canonical_complete_assignments`; and
2. a human solve trace showing how the intended invariant chain eliminates *classes* of placements before complete-state testing.

Reject/rework a case when either is true:
- a competent puzzle tester can enumerate plausible complete states faster than they can articulate/use the intended invariants; or
- solving consists mainly of testing one candidate cell after another and reading card truth changes, even if the raw assignment count is numerically large.

A below-threshold exception must name why complete-state enumeration is still unattractive. A high-count case does **not** automatically pass.

No runtime anti-brute feature is allowed as a substitute.

Verdict: **PASS / empirical content gate remains P9-E02.**

---

# 4. Attack C — decorative predicate piles

## Attack
Late cases permit 4–6 predicates. A unique witness can still carry decorative predicates that happen to be true but contribute nothing. This would create visual load without deduction depth.

## **REPAIR P10-03 — leave-one-out necessity report**
The offline analysis report for every LATE/MASTERY candidate must calculate, for each atomic predicate `p`:
- satisfying assignment count for the full conjunction;
- satisfying assignment count for `all predicates except p`;
- the assignments newly admitted when `p` is removed.

For a default unique-solution campaign case:
- if removing `p` still leaves exactly the same single canonical solution, `p` is **logically redundant** and the case is rejected until the predicate is removed or the case is redesigned;
- if a 5–6 predicate case has an atom whose removal admits only cosmetically/permutationally equivalent evidence already quotiented by canonicalization, treat it as redundant;
- six predicates are allowed only when **every atom is individually necessary** and at least three predicate classes are materially represented.

Additionally report class-level ablation: removing an entire predicate class from a LATE/MASTERY target must expand the candidate set or materially alter the intended proof. Otherwise that class is decorative.

This does not require every predicate to be equally strong; it requires every visible requirement to earn its UI cost.

Verdict: **PASS with exact redundancy test.**

---

# 5. Attack D — topology readability on 9x9

## Attack
Hole semantics are formally clean but cognitively unusual: a hole is itself one of the remaining-open components. A target can therefore simultaneously say “3 open spaces” and “1 enclosed pocket.” On a dense 9x9 state, area numbers, component patterns, markers and boundary signatures can overload handheld presentation.

## Repair / clarification
The existing visual grammar survives, but Phase 11 must freeze these curation rules:
- when `COMPONENT_COUNT` and `HOLE_COUNT` coexist, objective detail explicitly states that enclosed pockets are included in the total open-space count; no topology jargon is required;
- focusing a hole card highlights the same component outline used by component inspection plus the enclosure halo, preventing the UI from implying a second overlapping object;
- six objective cards remain an exception ceiling; 4–5 is the mastery target;
- reject a case if intended reasoning depends on distinguishing tiny component/hole outlines that are ambiguous at the 40-logical-px cell floor;
- reject a case if the *intended or common near-solution states* require the player to track more simultaneously labeled regions than can be read without overlap; do not solve this by adding a second minimap or zoom/pan system.

P9-E01 (worst-case 1280x800) and P9-E03 (handheld fatigue) remain empirical release gates.

Verdict: **PASS / device gate, no mechanical redesign.**

---

# 6. Attack E — controller/focus abuse and rapid input

## Attack cases
- hold a piece, then cycle pieces;
- hold a piece, press undo;
- hold reset while in reposition mode;
- pause while holding;
- spam rotate/place during topology animation;
- solve and press undo/reset during success transition;
- open objective/inspect while a provisional reposition ghost differs from committed truth.

P9-07 establishes that domain truth commits before presentation animation, but a few command priorities remained implementation-ambiguous.

## **REPAIR P10-04 — held-state command matrix**
While `REPOSITION_HELD` is active:
- cursor move changes only the provisional ghost;
- rotate changes only provisional orientation and never commits by itself;
- `A/Confirm` attempts one legal atomic REPOSITION commit;
- `B/Cancel` **always cancels held mode and restores the old committed placement**; it does not also perform global Undo;
- LB/RB piece cycling is disabled until held mode is committed/cancelled;
- reset-hold accumulation is disabled while held; player must cancel/commit first, preventing one press sequence from meaning both cancel and reset;
- pause is allowed and preserves the temporary held UI state in memory, but quitting/reloading restores the last committed placement, never the provisional ghost;
- objective detail / topology inspect, if opened while held, displays **committed-state topology only** and must visually mark the held ghost as provisional; it never evaluates the ghost.

Outside held mode:
- a legal command commits/evaluates immediately; stale animations cancel/retarget to the newest snapshot;
- Undo always acts on the newest committed history transaction, never on animation state;
- on solve, solved progress commits atomically before success navigation; destructive board commands are ignored during the short success lock and are never replayed afterward.

Verdict: **PASS after exact command matrix.**

---

# 7. Attack F — persistence / Cloud / import corruption

## Attack matrix
1. crash before temp-file rename;
2. crash after backup rotation but before new primary visible;
3. corrupt primary + valid backup;
4. corrupt primary + corrupt backup + valid Cloud;
5. both local corrupt + Cloud offline;
6. local compatible + Cloud future-version;
7. future-version local opened by older build;
8. repeated demo import after crash before provenance write;
9. Cloud upload fails after local solve;
10. imported compatible solved set is smaller than existing full solved set.

## Result
P8 atomic-write + P9-05 quarantine + monotonic union handles the attacks, provided the older Phase-8 “start safe empty local profile” sentence is not implemented literally.

## **REPAIR P10-05 — authoritative recovery ordering**
This is the consolidated behavior that overrides conflicting older wording:
1. valid supported primary -> use;
2. invalid primary + valid supported backup -> restore backup atomically;
3. both local copies invalid -> preserve them and enter **UNCOMMITTED_RECOVERY**; do not write/upload blank progress;
4. initialize platform defensively and attempt compatible Cloud recovery;
5. valid compatible Cloud -> atomically restore locally, then resume ordinary semantic sync;
6. unavailable/invalid Cloud -> user may explicitly create a new profile; only that deliberate commit authorizes later Cloud upload;
7. any future-version profile on either side is preserved and blocks destructive older-version merge/upload for that profile;
8. demo import is set-union/idempotent; a repeated import after crash cannot duplicate or erase progress;
9. platform failure after local solve never rolls local progress back.

Phase 11 must copy this rule verbatim into final freeze authority so an implementer does not have to reconcile P8 vs P9 manually.

Verdict: **PASS after consolidation.**

---

# 8. Attack G — progress monotonicity, revised/removed cases, achievements, 100%

## Attack
P9-06 covers a revised case retaining the same stable ID, but not all lifecycle cases:
- a solved case is removed from the shipping manifest;
- an unsolved case is removed;
- a case is replaced under a new ID;
- a removed case was the curated trigger for an achievement;
- 100% was earned before the manifest changed.

## **REPAIR P10-06 — content lifecycle semantics**
- Solved facts are append-only historical profile facts unless the save itself is explicitly reset by the player.
- **Current 100% denominator = current active shipping campaign case IDs**, not all historical IDs ever seen.
- A revised case with the same stable ID is grandfathered solved exactly as P9-06 states.
- A removed case ID remains in historical solved facts but is excluded from the current denominator and current progression gates.
- A replacement that is materially a new puzzle receives a new ID and is unsolved until solved; old removed ID remains historical only.
- If 100% was previously earned, its achievement/platform unlock is never revoked. The current profile may separately show `Current set: X/Y` if later content changes require new solves.
- Steam/platform achievements are monotonic once unlocked.
- Every achievement that is not already globally unlocked must remain attainable from the **current active manifest**. Therefore removing the sole trigger case for an achievement requires remapping that achievement to another appropriate current case/tag before release of the content update.
- Progression/unlocks are always re-derived from current active case IDs intersected with historical solved facts; removed IDs cannot satisfy current gates.

This preserves player trust while allowing honest current-completion accounting.

Verdict: **PASS after lifecycle rule.**

---

# 9. Attack H — progression exploit enumeration

## 36-case canonical target
After P9-01:
- Act I requires C1–C4 = 4 solves; C5/C6 optional.
- Acts II–V each require any 4/6 to unlock the next act.
- Minimal path after Act V gate = 20 total solves.
- Act VI additionally requires >=24 total, forcing **four backfills** from the ten skipped slots available across Acts I–V.
- Finale then requires any 4 of the other 5 Act-VI cases.

For the 36-case structure, the combinatorial route count is intentionally huge but semantically equivalent:
- Acts II–V 4-of-6 choices: `15^4 = 50,625`;
- after those gates there are exactly ten skipped prior cases; choose any four backfills: `C(10,4)=210`;
- choose four of five pre-finale Act-VI cases: `5`.

That yields up to **53,156,250 minimal choice combinations** before the finale, but none bypasses the mandatory four foundation semantics or the 24-total mastery gate. This is branch freedom, not an exploit.

## Reduced 30–35 case manifest ambiguity found
The phrase “30-case floor” previously allowed cutting weak cases without defining what happens if an act has only five cases while progression text still says “4/6.”

## **REPAIR P10-07 — reduced-manifest progression rule**
The launch manifest must keep **six acts**, each containing **5 or 6 active cases**. It may not simply delete cases without re-running progression/content gates.

For any 30–36 case shipping manifest:
- Act I's first four foundation cases remain mandatory sequential;
- for Acts II–V, next-act gate is **4 solved cases from that act**, whether the act contains 5 or 6;
- Act VI still requires the Act-V gate **and >=24 total active campaign cases solved**;
- Act VI must contain at least 5 cases so the finale rule is defined;
- finale unlocks after 4 of the other active Act-VI cases;
- if a reduced manifest makes the >=24 gate feel excessively restrictive in playtest, the solution is to restore/replace quality content or explicitly reopen the progression design in Phase 11—not silently lower the gate during implementation.

Thus 30 is a quality floor with deterministic structure, not permission for arbitrary pruning.

Verdict: **PASS after reduced-manifest rule.**

---

# 10. Attack I — oracle leakage

## Surfaces inspected
- legal footprint ghost;
- topology inspect overlay;
- predicate cards and current truth;
- component/hole area display;
- marker grouping;
- boundary highlighting;
- reasoning primers;
- resume state;
- achievement/family metadata;
- certifier certificates/search counts;
- platform/Cloud state.

## Verdict
No frozen feature needs solution-set access. The largest risk is accidental convenience code that ships certifier diagnostics or chooses primer content based on current solution viability.

## **REPAIR P10-08 — release oracle firewall**
Runtime shipping paths may consume only:
- case data;
- current committed placements;
- deterministic current evaluation snapshot;
- non-solution-authored metadata explicitly whitelisted for UI/progression.

They may **not** consume:
- canonical witness solution;
- satisfying assignment set;
- assignment counts;
- predicate ablation survivor tables;
- candidate rankings;
- articulation/critical-zone analysis generated by authoring tools;
- partial-state extendability;
- reasoning skeleton before solve.

Certificate integrity metadata may ship for diagnostics, but witness/search-analysis fields should be excluded from the ordinary runtime content package unless a test build explicitly needs them. Post-solve retrospective family icons may use curated family metadata; they are not available as a pre-solve solver aid.

Verdict: **PASS with packaging firewall.**

---

# 11. Attack J — scope creep

## Temptations rejected
The following do **not** solve any Phase-10 problem and remain outside launch canon:
- L/T/free polyomino shapes;
- diagonal connectivity;
- portals, switches, doors or movable walls;
- perimeter/path-length/symmetry predicates;
- OR/NOT/nested boolean grammar;
- procedural/endless filler;
- player-facing level editor / Workshop requirement;
- narrative campaign wrapper requiring bespoke scenes/dialogue;
- randomized daily mode, streaks or leaderboards;
- consumable/case-specific solver hints;
- online account/server dependency;
- a second topology minimap/zoom navigation system used to rescue unreadable content.

If content cannot reach the 30-case floor under the existing grammar and readability gates, the product is killed/redesigned rather than rescued by this list.

Verdict: **PASS / scope ceiling remains intact.**

---

# 12. Attack K — commercial honesty

## 30 vs 36
Store copy must use the final accepted manifest count, never the 36 target before curation. The 30-case floor is internal design policy, not a marketing promise.

## Demo
Six-case demo remains valid only if it contains the inversion/coupling aha. It may reuse early full-game cases and carry compatible solved facts, but the demo must not consume the only strong example of a late reasoning family.

## Price
$8.99 remains provisional. If the accepted campaign is 30 and median blind first completion is under three hours, Phase-7 rule still pushes reassessment toward $7.99 rather than padding.

## Platform claims
Controller/Cloud/Achievements are release targets, not claims until implemented. Deck Verified may never be claimed before Valve verification. Shipping-language count is not promised before translation/UI QA.

## **REPAIR P10-09 — launch-claim checklist**
Phase 11 final freeze must separate:
- **design commitments** (finite handcrafted campaign, no timers/reflex, unlimited undo, deterministic remaining-space objectives);
- **implementation release gates** (controller regression, Cloud, achievements, demo import, target-device readability);
- **business variables** (final list price/launch discount/languages/exact case count after curation).

Verdict: **PASS. No commercial feature requires mechanics creep.**

---

# 13. Attack L — fresh-implementer ambiguity

A hypothetical fresh implementation session was asked what it would still have to invent.

## Gameplay truth — sufficiently specified
It does **not** need to invent:
- board/cell/exterior semantics;
- cardinal connectivity;
- hole semantics;
- piece shapes/orientation/placement legality;
- marker protection;
- predicate grammar/AND semantics;
- final solution equivalence/canonicalization;
- partial vs complete win behavior;
- current-state feedback vs oracle boundary;
- undo/reposition/reset conceptual behavior;
- progression after P10-07;
- solved-progress monotonicity after P10-06;
- recovery/Cloud ordering after P10-05;
- rapid held-state behavior after P10-04.

## Intentionally implementation-flexible, not game-design holes
A fresh implementation may choose without reopening game design:
- exact scene/node names;
- exact internal data structures and optimization strategy;
- visual shaders/material palette within accessibility grammar;
- exact easing curves and non-semantic animation timing within frozen ranges;
- exact file format/container around the required save semantics;
- exact maintained Steam binding version compatible with the chosen stable Godot patch;
- exact localization vendor/workflow;
- diagnostics/logging framework;
- whether reset itself is undoable, provided reset recovery/confirmation and history semantics remain coherent and tested.

## Remaining freeze dependencies
The only non-empirical consolidation task is to turn Phases 3–10 plus P10 repairs into one final authority document and acceptance checklist. The only unresolved product facts are deliberately empirical gates.

Verdict: **PASS to specification freeze.**

---

# 14. Kill/redesign decision

## Product kill: NO
No Phase-10 attack presently justifies killing OPENWORK.

## Conditional future kill gates retained
Kill/materially redesign before release if any of these fail despite curation:
1. fewer than 30 high-quality certified cases survive without new mechanics;
2. anti-repetition reasoning-skeleton gates cannot be met;
3. representative mid/late playtests show systematic enumeration dominates deduction;
4. topology/hole state cannot be made legible at the 1280x800 / 40-logical-px floor without pan/zoom or a second visualization;
5. six-case demo cannot teach the hook + inversion/coupling within acceptable comprehension burden;
6. product value at 30-case floor cannot support at least the low end of the price band without padding.

These are falsifiable gates, not invitations to add scope.

---

# 15. Phase-10 repair register

- **P10-01** reasoning-skeleton anti-repetition gate.
- **P10-02** anti-enumeration human acceptance test.
- **P10-03** predicate leave-one-out/class-ablation necessity report.
- **P10-04** exact held-reposition/controller command matrix.
- **P10-05** consolidated local/Cloud recovery ordering.
- **P10-06** revised/removed/replaced case + 100% + achievement lifecycle semantics.
- **P10-07** deterministic progression for any 30–36 case six-act manifest.
- **P10-08** runtime oracle firewall / diagnostic packaging boundary.
- **P10-09** launch-claim separation.

Phase-9 repairs P9-01 through P9-07 remain active unless explicitly refined above.

---

# 16. Phase-11 exact checklist

Phase 11 must create `GAME12_FINAL_FREEZE.md` as the single implementation-facing design authority and may set `DESIGN COMPLETE = YES` only if every item below is explicitly answered.

1. Consolidate exact mechanics and authority order, including holes-as-components and solution canonicalization.
2. Consolidate campaign schema, 30–36 reduced-manifest rule, mandatory Act-I C1–C4, >=24 Act-VI gate and finale gate.
3. Consolidate content certification: unique campaign solution default, assignment thresholds, reasoning skeleton, leave-one-out/class ablation, similarity/repetition gates.
4. Consolidate UX: controller/mouse/keyboard, live current-state feedback, 40px floor, held-state command matrix, success transaction ordering.
5. Consolidate anti-oracle runtime packaging firewall and primer rule.
6. Consolidate persistence: atomic writes, backup, P10-05 quarantine/Cloud ordering, future-version refusal, demo-import idempotency.
7. Consolidate progress lifecycle: stable solved facts, revised/removed/replaced cases, current denominator, monotonic achievements.
8. Consolidate commercial boundaries: provisional price band, demo, no live service, release-target vs claim distinction.
9. List explicit implementation-flexible choices so they are not mistaken for missing design.
10. List empirical gates P9-E01/P9-E02/P9-E03 plus demo comprehension and price-value validation with pass/fail consequences.
11. Produce implementation acceptance tests covering rules fixtures, content certificates, progression routes, save corruption, Cloud conflict, demo import, controller rapid-input races, localization overflow and oracle leakage.
12. Freeze out-of-scope list and define change control: any new shape/predicate/simulation noun reopens design.
13. Decide final working/shipping-name status; a provisional name may remain if naming is explicitly a business variable, but implementation repository naming must be deterministic for migration.
14. Confirm no important gameplay behavior remains only in historical supersession prose.
15. Set `DESIGN COMPLETE = YES` only after the final freeze document can stand alone for a fresh implementation session.

If Phase 11 passes, attempt migration according to `START_HERE.md` and the continuity rule. If a dedicated repository does not exist, retain all Game #012 files as a frozen **NON-ACTIVE** safety archive, mark migration pending in `GAME_INDEX.md`, and immediately advance `STATUS.md` to Game #013 rather than blocking the factory.

**PHASE 10 = COMPLETE.**
