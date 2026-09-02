# GAME #013 — PHASE 10 ADVERSARIAL REVIEW

Date: 2026-09-02
Status: PHASE 10 COMPLETE — **PASS-TO-FREEZE WITH FOUR REPAIRS**
Selected concept: **SEAL BREAK** (working title)

Authority: this file is the Phase-10 destructive-review authority. Phase 4 remains authoritative for mechanics, Phase 5 for content, Phase 6 for UX, Phase 7 for commercial packaging, Phase 8 for technical contracts, and Phase 9 for its four integration repairs. Where this file explicitly repairs a contradiction or freezes a missing boundary, the Phase-10 repair wins until older text is normalized.

No production implementation is authorized or started here.

---

## 1. Review method

This pass assumes the design is guilty until proved otherwise. It attacks the game from the perspectives of:
- a strong logic-puzzle player at hour 3 and hour 8;
- a brute-force player willing to submit many legal plans;
- a content author tempted to create difficulty by adding more cards/sockets;
- a controller-only handheld player at 1280x800 with 200% text;
- a localization team dealing with long strings;
- an implementation session trying to build from the spec without inventing rules;
- a save/Cloud updater applying content revisions after release;
- a buyer judging the demo/store promise against the actual late game;
- the existing Games #001–#012 portfolio.

The review ends with KILL / REWORK / PASS-TO-FREEZE. A PASS does not waive empirical implementation/playtest gates.

---

# 2. Fun / novelty attack — does hour 8 become evidence-card bookkeeping?

## Attack
The core equation is simple: every installed witness records the first opening whose traversed seams intersect its covered seams. A bad campaign can therefore become a worksheet: read many trigger sets, compare many numbered cards, eliminate permutations.

This is the biggest durable design risk. It is more serious than implementation complexity.

## Why the game still survives
The frozen campaign contains six distinct *operations on the same witness law* rather than six predicate skins:
1. read direct cause;
2. discriminate overlapping witnesses;
3. reason from survival/complements;
4. choose witnesses that will create a required evidence structure;
5. reconstruct history from a fixed witness network;
6. choose witness network and bounded history together.

The player's object of thought changes from “what happened to this seal?” to “what can this set of witnesses prove?” and finally “which witnesses should exist so a history has the required proof signature?”. That is enough second-order progression to justify a compact 24–30 case product.

## Hard anti-bookkeeping gate frozen by Phase 10
A shipping case is invalid if its main difficulty is caused by any two of the following without a new dependency structure:
- more evidence cards;
- more compartments;
- more candidate sockets;
- larger trigger sets;
- longer history;
- more exact checkpoint numbers.

Every MID/LATE/CAPSTONE case must have a written human solve sketch containing at least **three class eliminations** before residual trial. “Class elimination” means ruling out a family of placements/histories from an invariant, intersection, complement, temporal bound or coupling argument; checking individual submissions does not count.

This strengthens the existing `oracle_free_human_review` requirement without changing mechanics.

**Verdict:** PASS. The campaign is compact enough that the design does not need 8–15 hours of novelty. It needs 24–30 consistently authored deductions. Empirical fatigue remains a playtest gate.

---

# 3. Dominant strategy / repeated-commit brute-force attack

## Attack
There is no penalty for wrong commits. A hostile player can enumerate legal setups manually and use retrospective mismatch traces to learn the result of each submission. Because the game correctly shows deterministic observed evidence after a commit, it cannot completely prevent this without hiding causal feedback or adding punitive friction.

Potential exploit: if mismatch cards are sorted by closeness, number of satisfied predicates, likely culprit, or changed consequence, the UI becomes an oracle-assisted hill-climber.

## Existing defenses that survive
- pre-commit UI never predicts tear results;
- mismatch is retrospective only;
- mismatch order is authored target order, not closeness;
- no score, lives, timer or attempt penalty exists;
- content must support human deductions before guessing;
- certifier can guarantee finite correctness but is not exposed to the player.

## Phase-10 freeze clarification
No runtime surface may expose **submission distance**. This includes:
- count or percentage of satisfied target predicates;
- “almost correct” states;
- sorting mismatches by estimated causal relevance;
- highlighting the edit that would fix a failed predicate;
- retaining green/red target cards while the player returns to edit;
- showing aggregate progress across repeated failed submissions.

After `RETURN TO EDIT`, observed-trace inspection remains available only by explicitly reopening the last committed replay/history view; the edit surface itself returns to neutral target evidence. The player may remember what they learned, but the UI must not turn attempts into a live optimization meter.

Brute force is therefore possible in principle but never made optimal by product feedback. Punishing brute force would damage the intended consequence-reading loop more than it helps.

**Verdict:** PASS.

---

# 4. Content-family repetition / fake difficulty attack

## F1 Direct witness reading
Valid only as onboarding. Any late F1-only case is filler. Existing architecture already confines it to tutorials.

## F2 Witness comparison
Risk: becomes sets-on-cards bookkeeping. Valid only when overlap/divergence yields a short inverse deduction. Cases that require scanning every pair are rejected.

## F3 Survivorship / omission
Risk: “try each omitted compartment”. Valid only if survivor trigger structure eliminates omission *classes*. Optional SB_15 remains cuttable if human review devolves into six-way checking.

## F4 Inverse witness placement
Risk: set cover in costume. Valid only when candidate sockets with equal final broken/intact state are discriminated by break time, overlap or survival structure. Selecting witnesses merely because their individual target time matches is insufficient late-game depth.

## F5 History reconstruction
Risk: permutation CSP. Valid only when delayed break, witness intersection or survival yields precedence/band eliminations before residual arrangement.

## F6 Coupled placement + history
Risk: Cartesian explosion that is hard only because there are two editable dimensions. First coupled cases must remain bounded; unrestricted `choose K of many x N!` is invalid even if certifier handles it.

## Phase-10 anti-inflation acceptance rule
For every authored shipping case, certification report + human review must answer:
1. what is the first non-trivial deduction?
2. what family of submissions does it eliminate?
3. what second deduction depends on the first?
4. why would adding/removing one decoy change reasoning rather than only search count?

If answer 3 is absent, the case is at high risk of flat predicate filtering and must be revised or cut.

**Verdict:** PASS with content-authoring discipline; no new mechanic is required.

---

# 5. Scope attack

## Geometry/art burden
Mechanics require discrete seams, compartments and seal sockets, not physical simulation. Tear animation can be authored/parametric presentation over a finished trace. The major scope trap would be making each case a bespoke animated 3D object.

**Freeze:** gameplay authority does not require bespoke 3D cabinet mechanisms. V1 may reuse a small family of 2D/2.5D workbench shells and data-driven seam/socket layouts. Decorative uniqueness cannot become a case requirement.

## Content burden
24 floor / 30 target is reasonable only if geometry is data-driven and certifier-assisted. A single case needing several days of custom art violates the product thesis.

## Localization burden
Evidence grammar is finite and compositional. Narrative prose is not core. This remains safe if display labels stay short and localization keys are separated from logic.

## Controller/focus burden
Author-reviewable focus graph is viable at 24–30 cases. It becomes expensive only if geometry is freeform; freeform is already excluded.

## Certifier runtime
Phase 8 target <=1,000,000 legal combined submissions per case is sufficient. The product gains nothing from certifying gigantic spaces. Any exception above the hard review threshold requires a complete deterministic pruning proof and should be exceptional.

## QA matrix
Main multiplication axes are input method, scale/layout, reveal speed/motion, save state/version and 24-vs-30 content configuration. This is meaningful but bounded for a small offline game.

**Verdict:** PASS.

---

# 6. Demo truth / marketability attack

## Fresh market recheck — 2026-09-02
Current Steam evidence continues to reward easily stated rule identities but gives no reason to market Seal Break as a detective/narrative puzzle. *Case Solved: The London Files* (released 2026-07-29, $9.99) sells closed deduction cases through detective framing and currently has Mixed overall sentiment; *SusDoku: Clues & Suspects* (2026-07-08) also leans crime/detective and currently has Mostly Negative reviews. Meanwhile mechanically legible authored puzzle products such as *Piece by Piece* (2026-03-13) show that a clear physical rule can carry a handcrafted campaign. This does not prove Seal Break's market success, but it reinforces the frozen choice to lead with the physical witness/tear hook rather than crime-story dressing.

## Demo defect found
Phase 7 says demo beat 6 is a coupled late-loop beat “prefer SB_24/SB_26 lineage”. Phase 9 later establishes **SB_21 as first free reconstruction and SB_26 as first genuine coupled family**. Therefore SB_24 lineage alone cannot truthfully satisfy the commercial promise “seal selection + bounded history choice/reconstruction”.

### Repair P10-01 — demo capstone identity
The sixth demo beat must be either:
- a mechanically identical certified campaign case from **SB_26–SB_29** that is suitable for demo onboarding; or
- a distinct demo case ID derived from SB_26–SB_29 mechanics, independently certified, using both editable seal placement and bounded history choice/arrangement.

`SB_24` may supply tutorial wording or reasoning prerequisites but **cannot by itself be the demo's coupled capstone**.

If no SB_26–SB_29 candidate is readable in the demo after tutorialization, the design may not freeze the demo as “done”; it must create a distinct certified demo coupled case using the same rules, not weaken the store promise.

## Trailer truth
First substantive gameplay beat should show: inspect witness relation -> place/select -> commit -> exact tear checkpoints -> evidence consequence. Avoid presenting freeform destruction, realistic forensics or hidden-story deduction.

**Verdict:** PASS after P10-01.

---

# 7. UX/accessibility hostile review

## 1280x800 / 200% text
The drawer/reflow model is structurally sound. Main risk is evidence density forcing constant rail switching and loss of context.

### Repair P10-02 — density/readability budget
A shipping case may exceed the default evidence-card viewport, but no case may require the player to memorize identities while cards are inaccessible. At 200% text and 1280x800:
- focused evidence card must remain fully readable without horizontal scrolling;
- witness/compartment identity, predicate relation and checkpoint number must remain in one semantic card;
- cross-highlight from evidence card to workbench must remain available while that card is focused;
- scrolling may hide other cards, but opening/closing the Evidence rail must preserve exact semantic focus;
- authoring review must test the case with localized pseudo-long strings before certification is considered release-valid.

This is a release acceptance boundary, not a fixed numeric cap on evidence predicates. A numeric card cap would be arbitrary; the correct gate is whether information remains navigable and whether difficulty comes from logic rather than UI memory.

## Color/pattern/icon density
Seal identity remains pattern/icon/label. High-density cases must never introduce visually near-identical patterns just to expand socket count. Accessibility review owns pattern distinguishability.

## Reduced motion / Instant
Because resolver finishes before reveal, reduced motion and Instant can expose identical semantic checkpoints. No deduction depends on animation timing.

## Keyboard/controller only
Discrete focus nodes and move-mode history arrangement cover all gameplay verbs. Mouse conveniences remain non-authoritative.

**Verdict:** PASS after P10-02.

---

# 8. Progression / hints / achievements attack

## Progression
P9-02 fixes the true 24-case floor; forward progression must use explicit prerequisites and `required_for_floor`, never numeric ID ranges. Optional fifth beats cannot gate floor continuation.

## Hints
Three authored levels are safe because opening them is explicit. A nudge may eliminate a class but may not name an exact full submission.

## Achievement ambiguity found
Phase 7's proposed achievement name `Without a Nudge` is described as solving one case “without opening hints”, which is stricter than its title implies because the hint system has Observation, Deduction and Nudge tiers.

### Repair P10-03 — hint achievement semantics
Achievement logic must use an explicit stable condition, not title interpretation:
- planning default: designated case solved with `max_hint_step_opened == 0`;
- commercial display name/description may be renamed before store freeze to accurately communicate “no hints opened”.

If the product team later wants an achievement specifically for avoiding only tier-3 Nudge, that is a different condition and must be named/documented separately. Do not infer behavior from the placeholder `Without a Nudge` label.

No hint use may reduce campaign completion, Full Casebook completion, or ordinary progression.

**Verdict:** PASS after P10-03.

---

# 9. Persistence / Cloud / demo import / content migration attack

## Already strong
- atomic main + backup;
- incompatible future save protection;
- monotonic compatible Cloud union;
- explicit conflict gate when merge is not deterministic;
- external state queued during committed trace;
- idempotent demo import;
- solved facts bound to mechanics/acceptance compatibility.

## Remaining ambiguity found
P9-04 says a mechanically changed case becomes `REVALIDATION_REQUIRED` and unlocks are recomputed “conservatively according to shipped migration policy”. That leaves a future implementation/release session to invent whether a patch can suddenly relock later cases the player already accessed.

### Repair P10-04 — changed-case progression continuity
Persisted progression must distinguish:
- `historical_completion`: player solved an older compatible revision;
- `current_revision_solved`: player solved the currently authoritative mechanics/acceptance revision;
- `ever_unlocked`: case was legitimately unlocked under a prior compatible progression graph.

On a mechanics-changing case update without an explicit migration table:
1. keep historical completion record;
2. set current revision to `REVALIDATION_REQUIRED` / not currently solved;
3. never revoke an achievement already granted;
4. never relock a downstream case whose `ever_unlocked` flag is true;
5. future locked cases still evaluate prerequisites against current-revision solve facts plus explicit grandfathering migrations;
6. `Full Casebook` / current-completion UI uses current revision solve facts, not historical completion;
7. a deliberate grandfather migration may mark the new revision solved only through an explicit versioned migration rule tested in save fixtures.

This avoids both silent false completion and hostile post-patch loss of already-open content.

## Duplicate/import exploit
Demo import uses compatible solved facts as set/monotonic union. Achievement granting is derived/idempotent. Repeated import cannot generate repeated achievements or overwrite newer full settings.

## Cloud during edit
If a compatible external profile arrives in CASE_EDIT, profile merge may happen at a safe boundary without mutating the current draft. Draft ownership remains local until leaving/reloading the case; any remote draft for the same case is not auto-spliced. This follows the already-frozen principle that puzzle edit state is not a CRDT.

**Verdict:** PASS after P10-04.

---

# 10. Implementation-ambiguity audit Phase 4–9

The following questions are sufficiently answered for freeze:
- what opening a compartment means mechanically;
- how seams/sockets derive trigger compartments;
- exact checkpoint ordering and same-checkpoint atomicity;
- already-broken witness behavior;
- legal placement/history modes;
- complete v1 evidence predicate vocabulary;
- structural commit legality vs puzzle correctness;
- replay/reset/return-to-edit semantics;
- accepted solution classes/equivalence;
- preview/oracle boundary;
- campaign families and 24/30 configuration;
- controller/keyboard/mouse interaction grammar;
- 200% scaling and non-color identity requirements;
- hint isolation;
- premium/demo/achievement boundaries;
- shared resolver/certifier contract;
- hashes/versioning/replay compatibility;
- save recovery, Cloud queueing and demo import;
- mechanics-changing content update behavior after P10-04.

Implementation-flexible items that do **not** require game-design invention:
- exact visual shell/cabinet art style;
- exact animation easing/timing within accessibility limits;
- exact Godot scene hierarchy;
- exact file serialization format if semantic schema/contracts are preserved;
- exact Steamworks binding library;
- final commercial title;
- final localized language list;
- final launch price within later market review;
- exact achievement display names/icons;
- whether 24 or 30 cases ship, decided by certification/playtest gates already specified.

Remaining empirical gates, intentionally not solved by paper design:
- real first-solve times;
- fatigue/repetition at hour 3/hour 8;
- whether SB_26–SB_29 yields a demo-readable coupled capstone;
- whether mismatch explanation feels informative rather than punitive/oracular;
- handheld readability of real art at 1280x800/200% across long localization;
- final 24-vs-30 release scope;
- tear animation/audio satisfaction and reduced-motion equivalence.

None require inventing a new rule to start implementation.

---

# 11. Portfolio collision / differentiation recheck

Against #001–#012, Seal Break still owns a distinct reasoning identity: **irreversible temporal witness evidence over a bounded opening history**.

It does not use:
- living-cargo cascades (#001);
- bureaucracy/reality edits (#002);
- transferable physical properties (#003);
- audio-hidden geometry (#004);
- conserved network tension (#005);
- destructive adjacency rewiring (#006);
- observation/persistent remembered transforms (#007);
- destructive key-vector edits (#008);
- flat-sheet fold/nest/trim imposition (#009);
- conveyor label permutation (#010);
- cyclic-program deletion/phase alignment (#011);
- empty-space topology placement (#012).

The visual language of seals crossing seams also escapes the layered-paper lane that killed Carbon Copy and Blind Staple. The title `SEAL BREAK` remains working-only and may collide lexically with unrelated products later; naming is not mechanics canon.

Fresh 2026 Steam review did not reveal a close analogue built around player-placed tamper witnesses whose irreversible break times certify a chosen/reconstructed opening history. Search is not proof of uniqueness, but no current evidence overturns the differentiation thesis.

---

# 12. Phase-10 repairs summary

**P10-01 — Demo:** coupled capstone must come from/certify against SB_26–SB_29 mechanics; SB_24 alone cannot satisfy the late-loop promise.

**P10-02 — Accessibility density:** 1280x800/200% + pseudo-long localization is a per-case release gate with preserved semantic-card integrity and cross-highlighting; difficulty may not depend on UI memory.

**P10-03 — Hint achievement:** stable condition defaults to `max_hint_step_opened == 0`; display name must match semantics.

**P10-04 — Changed-case saves:** retain historical completion and ever-unlocked access, require current-revision solve for current completion, never revoke granted achievements, use explicit migrations for grandfather solve.

These are integration/specification repairs, not new gameplay mechanics.

---

# 13. Final destructive verdict

## KILL?
No. Core hook remains legible, portfolio-distinct, deterministic and commercially scoped.

## REWORK?
No systemic rework. Four finite integration ambiguities were repaired in this pass.

## PASS-TO-FREEZE?
**YES — PASS-TO-FREEZE.**

The game is ready for Phase 11 Specification Freeze, provided Phase 11:
1. normalizes P9/P10 repairs into a final authority document;
2. creates a single implementation-facing acceptance checklist and authority order;
3. explicitly lists empirical gates that implementation/playtest must validate;
4. sets `DESIGN COMPLETE = YES` only after confirming no important rule is left to invent;
5. then attempts dedicated-repository migration under the factory continuity rules.

No production implementation has begun in the factory.