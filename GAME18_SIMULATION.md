# GAME #018 — PHASE 9 WHOLE-GAME SIMULATION

Date: 2026-09-07
Game: **LOCAL TIME**
Status: PHASE 9 COMPLETE — PHASE 10 ADVERSARIAL REVIEW NEXT
Production implementation: NO

Authority: follows Phases 3–8. Explicit **PHASE-9 CANONICAL REPAIR** clauses supersede conflicting earlier wording.

## 1. End-to-end verdict
Paper simulation covered first boot, LT01–LT06, Cases 07–36, mastery, undo/restart/replay, save/load/crash, demo import, Steam offline/cloud conflicts, mouse/controller/Deck, Resolve spam, socket scanning, warnings and budget waste.

The core survives unchanged: clocks create NOW conditions; Resolve earns DONE milestones or LOCKED OUT consequences; moving clocks never rewinds DONE; carriers use explicit finite handoffs; all logic stays deterministic and public.

Three ambiguities require repair.

### PHASE-9 CANONICAL REPAIR A — finite Resolve ceiling
Every shippable case MUST have a finite public `resolve_limit`, even tutorials. It may be generous, but never absent/infinite. Validator rejects missing/non-finite limits. This preserves a finite reachable graph and prevents indefinite no-change Resolve spam without turning every case into beat optimization.

### PHASE-9 CANONICAL REPAIR B — one-shot dispatch / finite carrier state
Baseline DISPATCH is one-shot: eligibility requires its persistent dispatch milestone to be absent; commit earns that milestone atomically. Carrier route edges are consumed or advance to a new finite carrier state. Repeating the same Snapshot cannot duplicate cargo or enqueue the same departure again. Repeatable service is allowed only via an explicit public finite-state/capacity model.

### PHASE-9 CANONICAL REPAIR C — undo does not rewind persistence lineage
Undo Resolve restores exact pre-Resolve **RunState** and puzzle counters/hash. It does NOT decrement profile-level `save_generation`, cloud sync markers or import lineage. Saving an undone state creates a newer persistence generation that may contain an older-equivalent RunState hash.

## 2. First boot and LT01–LT06
**Boot:** local play/profile must work with Steam unavailable. Settings may be changed before starting. Accessibility/input settings never alter puzzle hashes.

**LT01:** wrong first placement may produce a true no-change Resolve; no hidden progress occurs. Correct sequence proves NOW vs DONE and persistence after clock relocation. Repair A makes exploration finite and visible.

**LT02:** narrow Bakery exposure succeeds; broad Bakery+Flower exposure can bake bread and permanently close the flower in the same Snapshot0. Warning is factual, not "bad move." Numeric labels remain semantic equality states, not elapsed chronology.

**LT03:** Bridge OPEN + Station 08:05 must coexist in Snapshot0. Ambiguous multi-label coverage is illegal unless a site explicitly declares REQUIRES_SET.

**LT04:** PREPARE -> DISPATCH/HANDOFF -> ARRIVE -> later ACCEPT. Arrival and acceptance are separate by default. Repair B prevents re-dispatch/duplicate payload under repeated Resolve.

**LT05:** harmful and beneficial candidates can both occur from one Snapshot0; update order cannot bypass a permanent hazard. Undo is puzzle recovery, never fictionally rewind.

**LT06:** unguided synthesis must require a prior persistent milestone, later clock relocation, and final distinct simultaneous labels. Multiple-solution marketing is allowed only if solver verifies it.

## 3. Canonical proof-shape map — Cases 07–36
Exact geometry remains authored later, but each case must preserve its distinct human proof or be cut.

### Chapter 2 — Finish What You Started
- **07 Commit Before You Move:** earn a persistent step before reusing that clock for final NOW.
- **08 Narrow Before Broad:** narrow useful coverage avoids a broad permanent-risk exposure.
- **09 Middle State Matters:** three-stage chain cannot skip middle state or advance twice in one Resolve.
- **10 Shared Exposure, Different Readiness:** align two processes' readiness before one shared exposure.
- **11 Restore the Present:** persistent work is complete, then final clock must return to a NOW gate.
- **12 Two Chains, One Safe Window:** two chains + one protected site share a constrained safe exposure.

### Chapter 3 — Send It Across Town
- **13 Already There:** ACCEPT requires cargo present at Snapshot0; new arrival is too late.
- **14 Departure Window:** prepared persistent cargo + one NOW gate must coincide.
- **15 One Carrier, Two Payloads:** service order through one finite carrier state, no routing puzzle.
- **16 Prepare, Couple, Receive:** prepare -> two-NOW dispatch -> arrival -> later receiving label.
- **17 Receiving Competes With Preparation:** one clock is needed for acceptance and next preparation; order creates future freedom.
- **18 Coupled Departure Relay:** one-shot two-NOW dispatch frees a clock for later acceptance.

### Chapter 4 — Protect the Morning
- **19 Protect Then Share:** no narrow workaround; protection must precede broad useful exposure.
- **20 Which Protection First?:** two vulnerable sites create a partial order of protection prerequisites.
- **21 Safe Coupling:** coupled-current action becomes safe only after persistent protection.
- **22 Snapshot Trap:** protection earned in the same Resolve cannot retroactively prevent a Snapshot0 hazard.
- **23 Two Valid Protection Routes:** two genuinely different causal routes; not symmetric socket swaps.
- **24 Protected Synthesis:** two risks + ordered process + final coupling identify one necessary safe exposure order.

### Chapter 5 — Two Clocks, One Town
- **25 Two Ends at Once:** pure two-clock/two-endpoint simultaneous NOW alignment.
- **26 Earn, Then Reuse:** one clock earns DONE, then must leave to join final coupled arrangement.
- **27 Alternating Couplings:** same clocks satisfy different coupled needs across beats; milestones make each coupling useful.
- **28 Three-Site Accord:** first three-site coupling, only after earlier milestones sharply reduce placement possibilities.
- **29 Departure Under Coordination:** coupled dispatch plus a negative safety constraint on a third site.
- **30 Move-Budget Synthesis:** one placement must serve two different future purposes before relocation.

### Chapter 6 — The Whole Day at Once
- **31 Forked Workday:** two chains compete for one clock; one threshold must be reached before finishing the other.
- **32 Protected Endpoint Relay:** protect destination before dispatch because later receiving exposure would otherwise lock it out.
- **33 Fixed-Time Anchor:** fixed zone removes freedom; protect -> coupled dispatch -> arrival -> receiving relocation -> final NOW.
- **34 Two Carriers, No Routing Puzzle:** two finite carriers share one dispatch/accept resource; order matters, paths do not.
- **35 Bottleneck Window:** one broad exposure is eventually required but unsafe until two prerequisites exist; reason backward from that bottleneck.
- **36 Dependency Braid:** >=2 persistent prerequisites, one protection constraint, one one-shot relay and a final two-site coupled NOW objective, using only known families.

Case 36 human proof must fit <=6 necessities: reserve final coupled sockets; identify relay prerequisite; identify required protection; earn prerequisite A; earn prerequisite B/protection and relay; reuse freed coverage for final NOW after arrival/acceptance.

## 4. Repetition verdict
30–36 campaign remains plausible, but 36 is not a quota.

Highest collision-risk groups:
- 08 / 19;
- 14 / 16 / 18;
- 25 / 28 / 29;
- 31 / 33 / 36.

They survive only if actual authored geometry/playtests preserve the proof distinctions above. If two collapse to the same one-sentence proof, cut the weaker case before adding new mechanics. Quality floor remains 30 campaign.

Mastery remains **8 baseline + 4 reserve**. M09–M12 ship only if each introduces a distinct proof shape; budget-only remixes do not qualify.

## 5. Save / crash / import / cloud simulation
- Undo Move restores planning placement/move count only.
- Undo Resolve restores exact pre-Resolve RunState, while Repair C keeps persistence generation monotonic.
- Replay is presentation-only.
- Restart resets RunState but preserves already-earned profile completion.
- Core computes complete post-state before animation. Skip snaps to it.
- Crash after successful atomic post-state save reloads post-state; interrupted save falls back to last-known-good.
- Demo import is idempotent/monotonic and never deletes demo saves.
- Older demo state cannot replace newer/completed full-game progress.
- Divergent local/cloud saves are never silently timestamp-merged; preserve both before user choice.
- Safe monotonic profile fields may union through tested merge; in-progress RunState is chosen as a whole checkpoint.
- Corrupt cloud cannot overwrite valid local.

## 6. Input and edge-case simulation
Controller/Deck must reach every clock, socket, site, Resolve, Undo and trace action without pointer emulation. A case fails readability if controller focus is unpredictable or camera hunting is required.

Resolve spam: finite by Repair A; no hidden accumulation.
Socket scanning: preview shows footprint/current predicates/risk facts, never multi-beat outcomes. Cases whose practical solution is cycling every socket fail anti-enumeration.
Risk-warning scanning: warnings expose public triggers but never solver judgement.
Undo abuse: acceptable; cannot duplicate milestones/cargo/achievements.
Double-submit: application command lock prevents two Resolve commits from simultaneous devices.
Budget waste: player may fail deliberately; DEAD language remains limited to authored fatal states, exhausted hard budget or exact solver certification.

## 7. Contradiction check
- NOW vs DONE remains coherent.
- Earlier-looking labels do not reverse state.
- Lockout vs beneficial transition remains deterministic from Snapshot0.
- Protection earned in same Resolve does not protect against a Snapshot0 hazard by default.
- Dispatch duplication is closed by Repair B.
- Arrival and acceptance remain separate by default.
- Carrier moves exactly one finite authored step when enabled.
- Coupled predicates use one Snapshot0.
- Save authority is independent of animation.
- Undo restores gameplay, not persistence lineage.

No unresolved contradiction blocks Phase 10.

## 8. Empirical gates carried forward
Paper design cannot prove NOW-vs-DONE comprehension, anti-rewind perception, socket-scan behavior, 1280x800 overlap readability, 30–36 real-play novelty, Case 36 elegance or $14.99 value perception. These remain prototype/playtest gates.

**PHASE 9 WHOLE-GAME SIMULATION = COMPLETE.**

# NEXT DESIGN STEP — PHASE 10 ADVERSARIAL REVIEW
Run destructive review of:
1. fun/repetition and UI-scanning dominance;
2. proof collisions 08/19, 14/16/18, 25/28/29, 31/33/36;
3. no-change Resolve, warning exploitation and undo abuse;
4. dispatch/carrier idempotency and duplicate state;
5. 30-vs-36 content/art scope;
6. Deck/accessibility density;
7. corruption/import/cloud/undo-generation semantics;
8. implementation ambiguity across all authority;
9. demo weakness and Case-36 over-composition.

Repair canon where necessary. If clean, proceed to Phase 11 Specification Freeze. Do not start production implementation.
