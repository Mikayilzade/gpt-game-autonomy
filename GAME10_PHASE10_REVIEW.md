# GAME #010 — PHASE 10 ADVERSARIAL REVIEW

Date: 2026-08-31
Status: **PHASE 10 COMPLETE — two bounded repairs frozen**
Game: Luggage Carousel Zero *(working title)*

Authority: all prior active Game #010 authorities -> `GAME10_PHASE9_CLOSURE.md` -> this file. This file is authoritative over conflicting earlier statements about **when player-facing DEAD is entered** and **how best-tick mastery survives content/rules changes**. No production implementation is authorized.

---

# 1. Review frame

This pass attacks the product on the factory's required axes:
1. fun / repetition;
2. scope / production burden;
3. technical risk;
4. dominant strategies / solver leakage;
5. progression / commercial incentives;
6. UX ambiguity / accessibility;
7. persistence / corruption / update compatibility;
8. implementation ambiguity;
9. current market/storefront differentiation.

No rescue mechanic is allowed. A defect is repaired only by tightening an existing system or removing an unsafe promise.

---

# 2. Fun and repetition attack

## Attack A — does the game become “move required color toward S0”?
Adjacent-only swaps prevent the original unrestricted-swap collapse. Strong cases additionally require bag-consumption choice and queue coupling. F6 alone is not enough: a late case accepted only because a label walks several edges is repetitive.

**Frozen protection:** the existing content admission pipeline remains authoritative. Mid/late accepted cases must prove causal families, not merely longer label distance, larger N, tighter ticks or wider predicates. F10 still requires >=3 independently proven counted families.

## Attack B — do intentional misses become the same trick repeatedly?
They can. “Do not serve the first valid bag” is memorable once but predictable if overused.

**Protection:** F5 minimum/target remains 6 / 8–12 over the accepted campaign, not a requirement that every late case use intentional miss. F5 instances must differ in *why* immediate service loses: scarcity, substitution class, label staging/displacement, or later queue matching. Trace dedupe after trait/value renaming remains mandatory.

## Attack C — is Act D fake depth after F7 demotion?
Act D survives only as consequence/empty-rhythm presentation. Every D slot must earn itself through F3/F4/F5/F6/F8 proofs. If population cannot produce strong representatives, target 42 may shrink toward the >=36 strong-case floor rather than retain filler.

## Attack D — do K2 cases become “same puzzle, two moves instead of one”?
F9 already requires K2 significance against the identical K1 state/budget. Maximum three base-campaign K2 slots remains correct. No K3 escalation is allowed.

**Fun/repetition verdict:** no redesign required. The decisive release gate is still empirical content population: **>=36 strong non-duplicate cases or the content package is incomplete.**

---

# 3. Scope / production burden attack

Current frozen scope is unusually disciplined:
- one deterministic ring screen;
- N<=8;
- one pickup;
- three predicate dimensions total;
- no direct bag manipulation;
- no economy/live service/networking;
- 36–48 curated cases;
- stylized 2D/2.5D;
- controller-first;
- 12 achievements;
- seven-case demo.

### Main scope traps rejected again
- animated airport NPC crowds;
- voice narrative / bespoke passenger stories as required content;
- conveyor construction;
- luggage inspection/contraband;
- procedural endless mode;
- level editor / Workshop;
- multiple pickups;
- K3+;
- extra bag trait dimensions;
- OR/NOT/history predicates;
- per-case scripting;
- online leaderboards;
- cosmetics progression.

The solver/certification toolchain is the largest non-visual engineering burden, but it directly protects content quality and exact DEAD semantics. It is justified.

**Scope verdict:** PASS. Do not add a meta-game to “increase value.” Product value must come from strong cases/presentation.

---

# 4. Technical-risk attack

## 4.1 Exact solver
The state space remains bounded and authoring envelopes are conservative. Certification can run offline. Runtime exact DEAD remains the main latency risk.

The correction in §5 below reduces runtime pressure because player-facing DEAD no longer needs to be entered after every SWAP. Exact feasibility is still required for certification and after resolved ADVANCE boundaries; implementations may cache/precompute more aggressively.

## 4.2 Deterministic presentation split
Rules Core / Presentation separation remains mandatory. Animation never decides pickup outcome. Reduced-motion uses the same resolved transition.

## 4.3 Save/Undo
State size is tiny; exact snapshot Undo is safe. Saves occur only at committed logical boundaries. An animation is never persisted halfway.

## 4.4 K2
N<=6/ticks<=8 remains a safe authored envelope until benchmarked. No larger K2 case is entitled to ship merely because certification eventually succeeds offline; runtime/readability gates still apply.

**Technical verdict:** PASS after DEAD timing repair below.

---

# 5. Dominant strategy / solver-oracle attack — AUTHORITATIVE REPAIR

## 5.1 Defect
Earlier Phase-4/6/8 canon entered player-facing `DEAD` after **every committed SWAP or ADVANCE** when exact feasibility became false.

With unlimited Undo and at most N adjacent edges, this gives the player a perfect binary oracle:
1. try edge A;
2. if DEAD, Undo;
3. try edge B;
4. repeat until a swap is not declared DEAD.

The oracle does not provide a full solution, but it can collapse a meaningful part of local staging reasoning by certifying safe/unsafe swap branches before the carousel advances. The earlier claim that hard-stop “limits oracle play” is therefore rejected.

## 5.2 Canonical repair — DEAD is entered only after ADVANCE resolution
Player-facing DEAD timing is now:
- **after initial case load:** canonical campaign cases are certified solvable, so initial state is PLAYING;
- **after SWAP:** remain PLAYING regardless of hidden exact-feasibility result; no DEAD banner/hard-stop is exposed;
- **after first or second K2 SWAP:** same; player may Undo, make remaining legal swap, Preview or Advance;
- **after ADVANCE:** after movement/pickup/tick ordering and if not WON/BUDGET_FAILED, exact feasibility is evaluated; if no winning continuation remains, enter DEAD;
- **after compatible active-case resume:** restore the saved terminal state; do not run a new player-visible oracle check merely because the save boundary is after a SWAP;
- Restart returns certified initial PLAYING state.

This is not an approximate DEAD rule. The verdict after Advance remains exact.

## 5.3 Consequences
- `SWAP -> DEAD -> Undo` tests from older authority are superseded.
- SWAP still decrements bandwidth and remains individually Undoable.
- Preview remains one-step visual/predicate preview and never reports future feasibility.
- A player can still experiment consequence-free, but must commit an Advance before receiving a global unsolvability verdict.
- K2 can be explored naturally without a solver judgment after its first micro-edit.
- A save made after an ultimately doomed SWAP may resume as PLAYING; after the next ADVANCE the exact DEAD boundary appears. This is intentional.

## 5.4 Runtime state model amendment
`terminal_status` after SWAP remains PLAYING. An implementation may maintain a private feasibility cache for tooling/performance, but presentation and action legality may not expose it before ADVANCE.

`ADVANCE` ordering becomes:
1. rotate occupancy;
2. evaluate at most one pickup;
3. decrement ticks;
4. if all passengers served -> WON;
5. else if ticks == 0 -> BUDGET_FAILED;
6. else reset swaps to K;
7. exact feasibility check;
8. infeasible -> DEAD, otherwise PLAYING.

This matches the existing Advance ordering; the correction removes post-SWAP terminalization only.

**Oracle verdict:** REPAIRED without adding mechanics.

---

# 6. Other dominant-strategy attacks

## Pickup-only swapping
Defeated by `STAGING_SIGNIFICANT` cases and adjacent locality.

## Always serve immediately
Defeated by F4/F5 exact counterfactuals.

## Always preserve the rarest-looking bag
Not sufficient because bag usefulness is passenger-predicate/phase dependent; cosmetic rarity is non-mechanical and should not imply priority.

## Always move next required label toward S0 via shortest path
Not sufficient because local displacement can damage later label needs, duplicated labels create alternatives, and current pickup label may need preservation.

## Restart/Undo abuse
No economy or score makes save-scumming meaningful. Unlimited Undo is intended.

## Solver-as-hint through Efficient Route
Minimum tick target is hidden before first completion and says nothing about exact swaps. Safe.

**Dominant-strategy verdict:** PASS after DEAD timing repair.

---

# 7. Progression / commercial incentive attack

## Skip system
Worst-case five unresolved skipped cases at ending is coherent. It may look surprising that “campaign complete” occurs before all cases complete, but achievement/state naming already separates `CAMPAIGN_REACHED_ENDING` from `ALL_CASES_COMPLETE`.

UX requirement for Phase 11 consolidation: ending panel must not imply 100% completion when skipped cases remain; show campaign ending reached plus remaining unsolved count where appropriate.

## Efficient Route and intentional waiting
Minimum **Advances**, not minimum “successful pickups,” preserves intentional misses. Delayed surfacing after first F5 lesson remains correct.

## Price
Working $9.99–12.99 remains a hypothesis, not a design dependency. Do not freeze exact price in Phase 11.

## Current market check — 2026-08-31
Fresh search found `Luggage Loop` (June 2026), a casual airport luggage/passenger matching game, and `Luggage Collect Game` (April 2026), another casual baggage sorting puzzle. `Airport Baggage Simulator` released 2026-05-28 and uses inspection/sorting/automation rather than this fixed-gantry permutation system.

Sources:
- https://playgama.com/game/luggage-loop
- https://playgama.com/game/luggage-collect-game
- https://store.steampowered.com/app/3887090/Airport_Baggage_Simulator/

Implication: airport-baggage visuals themselves are **not** differentiated. Storefront/trailer must foreground the fixed gantry labels + adjacent swap + intentional pass rule. `Luggage Carousel Zero` remains a working title only; no final-name promise is frozen.

**Commercial verdict:** PASS, with naming/storefront differentiation retained as empirical release work.

---

# 8. UX ambiguity / accessibility attack

## N=8 at 150% text
Still an empirical risk. The responsive contract already prioritizes front passenger clauses and allows queue scrolling/selected-row expansion while preserving ring/pickup. Phase 11 must keep this as a prototype acceptance gate, not pretend it is proven on paper.

## Seam adjacency
Visual connector only during selection remains sufficient. No text tutorial should be required after initial interaction.

## Miss language
Neutral `MISSED`/clause feedback is necessary because deliberate non-service is core strategy. Red alarm/failure animation for an ordinary miss remains forbidden.

## DEAD after correction
Because DEAD occurs after ADVANCE only, its causal timing is easier to explain: “after this carousel step, no completion remains.” Undo still returns to pre-Advance, from which the player may also Undo earlier swaps. This is clearer than declaring a label edit globally losing before any belt motion.

## Color / audio / motion
Redundant symbols/text, no audio-required information and instant/reduced-motion presentation remain mandatory.

**UX/accessibility verdict:** PASS with empirical N=8/150%/controller gates carried forward.

---

# 9. Persistence / update compatibility — AUTHORITATIVE REPAIR

## 9.1 Defect
Earlier save authority stored `best_ticks_by_case` as an integer and recomputed Efficient Route against the **current** certificate minimum. This is safe only if the best record was earned on compatible case content/rules.

If case content changes while stable `case_id` remains, raw tick numbers are not comparable evidence.

## 9.2 Canonical mastery-record provenance
Replace the logical sole-truth shape:
`best_ticks_by_case[case_id] = integer`

with a provenance-bearing logical record equivalent to:

```text
best_tick_records[case_id] = {
  ticks,
  case_content_hash,
  rules_semantics_version,
  certificate_id_or_version_when_useful
}
```

Serialization may differ, but those first three semantic facts must be recoverable.

## 9.3 Efficient Route compatibility rule
A historical record qualifies for the current Efficient Route only if:
- its case ID matches;
- its `case_content_hash` matches current normalized case content, **or** a future explicit certificate-compatibility table declares the two versions performance-equivalent;
- its rules semantics version is compatible;
- `ticks <= current valid certificate.minimum_ticks` (normally equality because a valid certificate is minimal).

An incompatible historical record may be retained in a history/orphan area but does not light the current mastery marker.

## 9.4 Basic completion remains monotonic
A stable case ID that survives a content patch does not automatically revoke basic completion/progression. This avoids breaking campaign saves after balance/readability edits. If a future update truly replaces a case with a different design, it should use a new stable case ID rather than abuse compatibility.

## 9.5 Demo import / cloud merge
For compatible current records, choose minimum ticks. If two records have different incompatible provenance, do not compare numeric ticks as if equivalent; retain the current-compatible record and archive/ignore incompatible history for mastery.

## 9.6 Migration from older integer-only saves
If the historical `content_manifest_version` deterministically maps to an archived case hash/rules version, migration may attach that provenance. Otherwise mark the record `UNVERIFIED_LEGACY` and do not use it for current Efficient Route until the case is replayed. Basic completion is preserved.

## 9.7 Achievements
Already granted platform achievements are never revoked. New `FIRST_EFFICIENT_ROUTE` / `TEN_EFFICIENT_ROUTES` reconciliation only counts current-compatible mastery records.

**Persistence verdict:** REPAIRED.

---

# 10. Corruption / recovery attack

Frozen requirements:
- atomic temp -> replace writes;
- previous-good local backup where practical;
- validate before trusting newest local/cloud candidate;
- active-case corruption cannot erase profile progression;
- profile corruption tries previous-good backup;
- if all profile candidates are invalid, preserve/quarantine them where practical before creating a safe new profile;
- unknown future schema is never rewritten destructively;
- cloud timestamp alone is not authority;
- stable unknown/removed case IDs are never reassigned.

No player save may repair shipped case/certificate content.

**Recovery verdict:** PASS.

---

# 11. Implementation ambiguity attack

A fresh implementation session must not have to invent answers to these questions:

- What can be swapped? **Adjacent gantry labels only, ring seam included.**
- When do labels move? **Only on player SWAP, never on ADVANCE.**
- What moves on ADVANCE? **Every occupancy exactly one socket clockwise simultaneously.**
- Does pickup compress? **No. Consumed bag becomes persistent GAP occupancy.**
- How many passengers per tick? **At most one, front only.**
- Predicate operators? **1–3 positive equality clauses, one per LABEL/SHAPE/MARK dimension.**
- Can the player wait? **Yes: Advance with zero/unused swaps.**
- When is DEAD player-facing? **Only after nonterminal ADVANCE resolution, exact solver verdict.**
- Can a SWAP be doomed without banner? **Yes; remains PLAYING until Advance.**
- Can terminal states Undo? **Yes.**
- K2 Undo? **One atomic swap per Undo.**
- What is mastery truth? **Provenance-compatible best tick record vs current certificate minimum.**
- Does demo import copy act frontier/skips? **No.**
- Does changing content revoke basic completion? **Not when stable ID is preserved; mastery provenance may invalidate only optimization marker.**
- Is working title final? **No.**

Remaining unknowns are empirical/implementation-flexible rather than gameplay invention: final art, exact launch price, final commercial name, runtime solver backend per case, exact localization list and measured usability/performance results.

---

# 12. Phase-10 adversarial gate summary

| Axis | Result | Required carry |
|---|---|---|
| Fun/repetition | PASS WITH EMPIRICAL GATE | >=36 strong trace-distinct cases; no filler |
| Scope | PASS | no meta-game/rule-zoo expansion |
| Technical | PASS | exact certification; runtime benchmark |
| Dominant strategy | **REPAIRED** | DEAD only after ADVANCE |
| Progression | PASS | ending != all-cases-complete |
| Commercial | PASS WITH MARKET RISK | mechanics-first positioning; title remains working |
| UX/accessibility | PASS WITH EMPIRICAL GATE | N8/150%/controller/reduced-motion tests |
| Persistence | **REPAIRED** | provenance-bearing best-tick records |
| Corruption/recovery | PASS | validate/backup/quarantine rules |
| Implementation ambiguity | PASS | consolidate authority in Phase 11 |

No adversarial finding requires a new mechanic or broader product.

---

# 13. Phase-10 acceptance

- [x] fun/repetition attacked;
- [x] scope attacked;
- [x] technical/solver risk attacked;
- [x] dominant strategies attacked;
- [x] player-facing DEAD oracle defect found and repaired;
- [x] progression/commercial incentives attacked;
- [x] fresh 2026 baggage-market collision check performed;
- [x] UX/accessibility attacked;
- [x] persistence/content-update corruption attacked;
- [x] best-tick provenance defect found and repaired;
- [x] implementation ambiguity enumerated;
- [x] no production implementation started.

**PHASE 10 COMPLETE. DESIGN COMPLETE = NO.**

## NEXT — PHASE 11 SPECIFICATION FREEZE
Create a consolidated final authority that folds all amendments into one implementable specification. Mandatory freeze work:
1. consolidate adjacent-only swap canon and the new **DEAD-after-ADVANCE-only** timing;
2. consolidate exact case/state/action ordering and Undo/terminal rules;
3. consolidate 42-slot/36-strong-floor content architecture with F7 retired;
4. consolidate UX/controller/accessibility/progression/demo/commercial boundaries;
5. consolidate provenance-bearing mastery records, certificate/content-manifest/save migration contracts;
6. write a complete acceptance-test matrix and explicit authority order;
7. classify every remaining unknown as either implementation-flexible or empirical gate; no important gameplay unknown may remain;
8. run one final contradiction scan against earlier active authority;
9. only if the resulting handoff lets a fresh implementation session build without gameplay invention, set `DESIGN COMPLETE = YES` and attempt dedicated-repository migration per factory continuity rules.
