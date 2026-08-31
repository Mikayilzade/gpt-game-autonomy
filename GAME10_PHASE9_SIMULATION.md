# GAME #010 — PHASE 9 WHOLE-GAME SIMULATION ON PAPER

Date: 2026-08-31
Status: **PHASE 9 ACTIVE — FIRST FULL PRODUCT WALKTHROUGH COMPLETE**
Game: Luggage Carousel Zero *(working title)*

Authority: all prior active Game #010 authorities -> `GAME10_PHASE8_CLOSURE.md` -> this file.

This pass simulates the shipped experience as a coherent product. It may expose contradictions and request repairs, but does not add mechanics or begin implementation.

## 1. First boot — full game
1. Launch reaches Main Menu without account/login/platform dependency.
2. New profile has A01 unlocked only. Five act chapters are visible; later acts show locked progress state.
3. Settings/accessibility are reachable before play. Controller-only path is complete.
4. Selecting A01 loads its validated case definition and matching certificate. No active-case save exists yet.
5. First callout teaches only: bags move, gantry labels stay.
6. K=0 keeps labels inspectable while swap mode is unavailable.
7. Preview shows exactly one movement. Advance resolves; successful pickup wins on one tick.
8. A01 completion is written to profile save; A02 unlock is recomputed; achievement reconciliation remains separate/platform-optional.

No contradiction found.

## 2. First 20 minutes — canonical teaching arc
### A01
Player learns fixed label ownership through observation.

### A02 / Demo-02 equivalent
Player makes first adjacent S0 swap and combines socket label with immutable bag shape. Only neighboring target highlights, teaching local swap legality through interaction.

### A03/A07-style staging
A required label cannot teleport from distance two. Player must make a non-pickup swap before it is needed. If they attempt only pickup-adjacent swaps, exact DEAD may appear; Undo returns them one action at a time. The optional contextual nudge may say labels can be moved before needed, but does not name the edge.

### Preservation case
A broad passenger can consume a bag required by a later narrow passenger. Player sees that successful service is not automatically good strategy.

### First intentional miss
The tempting scarce bag arrives. Player changes S0 label so it deliberately fails, then later serves another candidate and preserves the scarce bag. Match/miss language remains neutral.

### GAP teaching
A successful pickup leaves an empty occupancy that keeps circulating. Tutorial says belt does not compress and does not claim the gap shifts other luggage.

### Demo finale
Player combines scarce-bag preservation, intentional miss and required non-pickup staging. This ends the demo/full first-session hook with same-vocabulary depth rather than a new mechanic.

Walkthrough finding: the teaching arc remains coherent after F7 demotion. GAP is visual state consequence, not falsely sold as a new strategic subsystem.

## 3. First hour — Act A into early Act B
By the first hour, the player should have stopped asking how movement works and instead compare candidate bags and future label distances.

Expected reasoning evolution:
- predict next incoming bag;
- identify all bags satisfying bag-trait clauses;
- compare label distance to S0 under adjacent swaps;
- preserve scarce candidate classes;
- occasionally use both sides of ring/seam for staging;
- understand Undo as experimentation, not penalty recovery.

Hostile check: repeated exact DEAD after every speculative swap could become oracle play. The hard-stop rule limits this because the player cannot continue forward from a dead state; they must Undo/Restart. However they can still test candidate swaps one by one. This is accepted as consequence-free puzzle experimentation, not a contradiction. Phase 10 must attack whether DEAD should be delayed for UX reasons, but semantics may not become approximate.

## 4. Early mastery — Acts B/C
The player now sees passenger queues as a matching problem coupled to a moving label permutation.

A representative C-state:
- current front passenger can consume either of two dot bags;
- one is the only square needed by P3;
- G label is two edges from S0;
- current R must remain for this tick;
- winning line stages G away from pickup while allowing/forcing a deliberate miss or alternate service.

The mental model has three simultaneous objects without new rules:
1. which bag survives;
2. which label reaches S0 on each future tick;
3. which passenger advances the queue.

No mechanics contradiction found.

## 5. Midgame — Act D / empty rhythm
Act D must not pretend gaps are a separate causal family. On paper, returning GAPs do two useful product things:
- visually memorialize earlier consumption;
- create recognizable guaranteed non-service beats in longer second-circuit traces.

But acceptance still comes from F3/F4/F5/F6/F8 proofs. A D-case that remains interesting only because a blank slot is visible but has no causal substitution/staging relationship is rejected as filler.

This reinforces Phase-5 closure rather than reopening it.

## 6. Late game — Act E
Late mastery remains bounded:
- N up to 8 for K1;
- three-clause predicates only when the third clause splits candidate competition;
- exactly 2–3 K2 campaign cases targeted, N<=6/ticks<=8;
- no new trait dimension, pickup, rule, currency or bag verb.

### K2 paper walkthrough
A needed G label starts two edges from S0. K1 cannot make G active this tick; K2 can stage G across two adjacent edges. First swap is individually undoable and may itself make state DEAD. If alive, second swap reaches target. The player may also Advance after only one swap; unused second bandwidth expires. This remains understandable because top UI shows 2 -> 1 -> 0 swaps.

### 3-clause case
Passenger asks LABEL=R + SHAPE=square + MARK=dot. This is accepted only because two square candidates differ in mark; otherwise the third clause is redundant and content is rejected. Predicate card still fits the fixed LABEL/SHAPE/MARK grammar.

No late-game rule-zoo pressure is required on paper.

## 7. Replay / Efficient Route
After first completion, case tile may reveal Efficient Route if mastery surfacing is active for that progression point. Minimum tick target is not shown before first solve.

For intentional-miss cases, the certified minimum route may still contain one or more deliberate misses. Therefore `minimum ticks` does not mean `serve whenever possible`; it means minimum total Advances under the real rules.

Replay does not alter progression negatively. Best ticks update monotonically downward. Efficient Route derives from current valid certificate, not a persisted stale boolean.

Potential UX risk remains wording: some players may read “Efficient” as anti-wait even with explanation. This is explicitly carried to Phase 10 adversarial review; removal of the visible badge is permitted without changing saved best-tick data or game mechanics.

## 8. Blocker skip / recovery
Simulated Act B blocker:
1. player completes B01–B04;
2. B05 blocks them;
3. `Skip for now` opens B06 and records one act skip used + B05 skipped-open;
4. B06/B07/B08 can proceed strictly; once all but B05 are complete, Act C unlocks;
5. B05 remains visible/open forever;
6. later completion clears skipped-open and may trigger RETURNED_TO_BLOCKER achievement;
7. no second B skip exists.

No progression deadlock found. Imported demo completion of a later canonical case counts only when normal progression reaches/unlocks that act; demo never imports skip/frontier flags.

## 9. Demo -> full-game path
A demo player completes the seven demo cases, changes text to 125%, enables Reduced Motion, and earns best tick records. They buy/install full game.

First full-game load:
- stable demo case completions merge by set union;
- best ticks merge by min;
- settings import if the full profile has no explicit newer preference;
- tutorial acknowledgements merge safely;
- act unlock/frontier/skip state is recomputed from full progression rules, not copied from demo;
- A01 completion may be recognized, but A02/A03 remain mandatory if not already completed in demo under their canonical IDs;
- eligible achievements are granted only now through platform adapter;
- repeating the import produces no duplicate progression or grants.

No contradiction found.

## 10. Save/quit/resume during a case
Player has made SWAP, ADVANCE, SWAP and quits from pause.

At a committed boundary the active-case save stores current state plus enough Undo history. Relaunch:
- content manifest/case/certificate compatibility checked;
- logical state restored exactly;
- UI rebuilt in neutral inspectable state, not halfway through animation;
- last pickup result may restore if saved;
- Undo once returns to the exact previous committed boundary.

If a patch changes the case incompatibly, profile progression remains; active case restarts with one-time notice. No guessed mid-case migration.

## 11. Reinstall / cloud restore
Profile/cloud restore contains progression/settings but active-case file may be older or absent.

Expected behavior:
- profile schema migrates through explicit version chain;
- current content manifest validates known case IDs;
- completion/best ticks are retained for surviving stable IDs;
- unlocks/frontiers recompute;
- Efficient Route recalculates against current certificates;
- platform achievements reconcile idempotently;
- if active-case manifest mismatch exists, discard only active case and keep profile progress.

Corrupted newest local profile attempts previous-good backup before defaulting. Content/certificates themselves are immutable shipped resources and are never repaired from player save data.

## 12. Hostile player behavior
### Spam Undo
Safe: one action per committed boundary; optional hold-repeat requires delay. No resource exploit exists.

### Equal-value swaps
User may insist after no-change warning; it spends bandwidth and can lead to DEAD. Solver does not branch on it. Undo restores bandwidth.

### Advance with unused swaps
Always legal while PLAYING. This is canonical waiting; no separate wait action needed.

### Queue inspection abuse
Free and non-stateful. All remaining predicates are public, so no information exploit exists.

### Repeated DEAD probing
Possible but bounded by Undo and no forward continuation. No economy or leaderboard makes it profitable beyond ordinary puzzle experimentation.

### Save-scumming
Irrelevant by design: Undo/Restart already provide consequence-free experimentation.

### Offline / Steam unavailable
Game, local progression and local achievement predicates continue. Steam sync/grants reconcile later.

### Changed controller/device mid-case
InputRouter switches glyphs/mappings; logical state unchanged. No physical button ID is part of puzzle save.

## 13. Whole-game contradiction audit
Resolved/confirmed:
- adjacent-only swap remains necessary and legible;
- F7/GAP demotion remains correct across midgame;
- intentional misses coexist with Efficient Route mathematically;
- final-tick win ordering is coherent;
- once-per-act skip has no deadlock;
- demo import cannot bypass tutorial prerequisites via imported frontier flags;
- active-case incompatibility does not threaten profile progress;
- exact DEAD remains implementation-heavy but semantically complete.

Open for Phase 10 attack, not unresolved design ambiguity:
1. whether visible Efficient Route wording creates anti-wait bias in real players;
2. whether immediate DEAD after every committed swap encourages excessive oracle probing;
3. whether N=8 + 150% text/controller distance stays readable empirically;
4. whether 36+ strong cases survive final content population without normalized repetition;
5. whether exact DEAD p95 target needs precomputed artifacts for most late cases;
6. whether working title has acceptable storefront/name differentiation — commercial naming only, not mechanics.

These are empirical/adversarial gates, not reasons to reopen Phases 3–8 now.

## 14. Phase-9 state
The complete experience from first boot through late mastery, replay, skip recovery, demo import, save/resume and reinstall/cloud restore has been walked without finding a mechanics/progression/persistence contradiction requiring redesign.

**PHASE 9 ACTIVE but major whole-game walkthrough complete. DESIGN COMPLETE = NO.**

NEXT: Phase 9 closure should run a second hostile whole-game pass focused on worst-case campaign paths (multiple skipped blockers across acts, ending with unresolved cases, content update after Efficient Route, DEAD on every action class, certificate/content version mismatch). If clean, close Phase 9 and immediately begin Phase 10 Adversarial Review.