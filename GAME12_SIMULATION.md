# GAME #012 — PHASE 9 WHOLE-GAME SIMULATION

Date: 2026-09-01
Status: **PHASE 9 COMPLETE**
Product: **OPENWORK** *(provisional working title)*
Authority: whole-product journey simulation and repairs discovered after Phases 3–8. Where this file explicitly amends an earlier progression/persistence/input clause, this later Phase-9 decision controls until Phase 11 consolidates the final specification.

No production implementation is created here.

---

## 1. Simulation method

The paper simulation attacks the frozen product as a complete player journey rather than as isolated systems. Each scenario traces:
- player state before the event;
- actions available under frozen mechanics/UX;
- rules/progression/persistence effects;
- failure or ambiguity discovered;
- repair, if required;
- remaining empirical gate, if the answer depends on real-device/playtest evidence.

The evaluator remains the Phase-4 authority: 4-neighbour remaining-open topology, holes are zero-boundary-contact remaining-open components, pieces have no placement-order semantics, runtime never enumerates solutions.

---

# 2. Scenario matrix

## S01 — Fresh keyboard/mouse first boot through first six onboarding cases

### Trace
1. Fresh profile starts at title screen.
2. Accessibility quick-start is visible before campaign start; default mouse/keyboard path needs no controller assumptions.
3. C1 teaches that the open field is the scored object and shows component change after the first committed placement.
4. C2 introduces markers and SAME/DIFFERENT.
5. C3 introduces an enclosed pocket with ordinary-language copy.
6. C4 introduces edge/boundary contact.
7. C5 provides the first explicit inversion: the obvious neck is wrong.
8. C6 combines two already-visible predicate classes and exposes inspect overlay if unused.

### Contradiction found — mandatory teaching vs 4/6 skip gate
Phase 7 allowed Act I C1–C3 sequential, then free order. Under that rule a player could solve C5 as the fourth Act-I case, unlock Act II, and never see C4 — the first boundary-contact teaching case — before Act II contains boundary predicates. Phase 8 already identified this as a hostile skip risk but did not fully repair the manifest rule.

### **REPAIR P9-01 — Act-I foundation lock**
Act I **C1–C4 are sequential mandatory foundation cases**. After C4, C5 and C6 are freely selectable and may be left unsolved. Act II unlocks once C1–C4 are solved; this is the Act-I interpretation of the 4/6 gate.

This preserves two-case skip tolerance without allowing component/marker/hole/boundary semantics to be skipped before later acts. C5/C6 remain valuable inversion/coupling cases and remain protected in the demo mini-arc, but are not required for campaign progression.

### Result
PASS after P9-01. No tutorial panel needs more than two short sentences. The first six still form the preferred onboarding/demo arc even though campaign progression can move forward after C4.

---

## S02 — Controller/Deck first boot at 1280x800, text scaling, high contrast, reduced motion

### Trace
- D-pad/stick moves a cell cursor independent of board obstacles.
- LB/RB cycles pieces; LT/RT rotates only rotatable pieces; A commits; B undoes/cancels; Y inspects current topology.
- High contrast preserves marker identity via labels/shapes, fixed-vs-placed solid via texture/seams, and components via outline pattern rather than tint alone.
- Reduced motion replaces topology redraw travel with short crossfade while predicate state changes remain visible.
- 9x9 board remains the maximum; ordinary target is >=48 logical px/cell, absolute floor 40.

### Risk found
Six predicate cards + 9x9 board + enlarged text at 1280x800 is the tightest presentation combination. Phase 6 correctly prioritizes board size over chrome, but the actual maximum supported UI scale has not been rendered on target hardware.

### Empirical gate P9-E01
Before release candidate, test at 1280x800 with:
- a 9x9 case;
- six objective cards;
- maximum supported text/UI scale;
- high contrast;
- controller glyphs;
- both normal and reduced motion.

Pass if the board remains >=40 logical px/cell, all six compact objective states are simultaneously identifiable without horizontal/vertical scrolling, focused objective detail is readable without hiding the currently selected board cell, and no marker/invalid-placement symbol becomes ambiguous.

If the first implementation misses this gate, compact chrome/detail-panel layout changes are allowed; shrinking below 40 px or requiring board pan is not.

### Result
DESIGN PASS / EMPIRICAL DEVICE GATE.

---

## S03 — Player repeatedly skips the two hardest cases and attempts to reach Act VI/finale

### Trace under repaired progression
- Act I: C1–C4 mandatory foundation solved = 4 total; C5/C6 may remain unsolved.
- Act II: solve any 4/6 -> 8 total.
- Act III: solve any 4/6 -> 12 total.
- Act IV: solve any 4/6 -> 16 total.
- Act V: solve any 4/6 -> 20 total.
- Act VI has the additional >=24 total campaign-solved gate. Therefore the pure two-skip-per-act path **cannot enter Act VI**. Player must backfill four previously skipped cases from Acts I–V.
- Once Act VI opens, finale requires 4 of the other 5 Act-VI cases.

### Teaching audit
Mandatory Act-I C1–C4 establishes the four semantics that later cases assume: scored open regions, marker grouping, enclosed pockets and edge contact. Area predicates introduced later are quantitatively self-describing and also receive first-seen UI explanation; they are not a hidden simulation noun. No later act may assume a new mechanical predicate family before its card/detail language has appeared.

### Amendment P9-02 — manifest lint
The campaign validator must fail if any case in act N uses a predicate family whose first-ever occurrence is only in a skippable case of an earlier act and whose meaning is not fully self-describing through existing predicate-card grammar. This is a static content lint, not a new player-facing lock system.

### Result
PASS. Skip tolerance relieves blind spots but does not create a straight 20-solve tunnel to late mastery.

---

## S04 — Strong player brute-tests placements rather than reasoning

### Early game
Brute experimentation is intentionally viable in tutorials; banning it would punish learning. A 1-piece C1 with 10–20 legal cells is supposed to reveal the causal law quickly.

### Mid/late game
The risk becomes meaningful when complete assignment count is small enough that rapid undo/reposition beats deduction. Runtime cannot slow retries artificially and may not hide feedback.

### Repair P9-03 — anti-brute content thresholds
Carry these curation thresholds into Phase 10/11:
- INTRO/EARLY may be small by teaching intent.
- MID cases should normally have **>=40 canonical complete assignments**, with >=100 preferred when more than one piece is used.
- LATE cases should normally have **>=100 canonical complete assignments**.
- MASTERY cases should normally have **>=500 canonical complete assignments**, with >=1000 preferred for the finale.
- A case below its band may survive only if human curation proves the decision structure is still non-enumerative (for example a large number of visually equivalent local outcomes is not required). The exception must be recorded.
- No runtime delay, limited undo, attempt penalty or animation lock may be introduced as an anti-brute patch.

Counts alone do not prove deduction quality, so representative playtests must also check whether the player can articulate reusable invariants and whether repeated complete-state testing becomes the dominant solve method.

### Empirical gate P9-E02
For representative Acts III–VI cases, observe first-time strong puzzle players. Reject/rework a case if systematic complete-assignment enumeration is consistently easier/faster than applying the intended 2–4 invariant chain. This is a content gate, not a player restriction.

### Result
PASS with strengthened curation gate.

---

## S05 — Struggling player uses unlimited undo, inspect and reasoning primers

### Trace
- Any legal committed state can be undone/repositioned/reset without losing campaign progress.
- Inspect shows only facts about the current committed topology.
- A generic reasoning primer may explain a reusable already-taught fact, never coordinates/candidate zones/solution counts/extendability.
- Complete-but-unsolved states do not trigger a fail modal.

### Oracle audit
A dangerous implementation shortcut would be to choose a primer based on which predicate is "blocking" the current solution or by asking the certifier whether the partial state is extendable. That would cross the frozen boundary.

### Repair P9-04 — primer eligibility source
Primer availability may be triggered by non-solution metadata such as elapsed engagement, number of complete-unsolved submissions, or explicit player request, but the **primer content selection is case-authored/general-family metadata only**. Runtime may not inspect solution sets, candidate rankings or partial-state extendability to choose a primer.

A primer remains optional and has no achievement penalty.

### Result
PASS.

---

## S06 — Demo partial/full progression -> full install -> import -> achievements/unlocks

### Trace
1. Demo stores solved facts with source product, versions and stable case identity.
2. Full install detects eligible demo profile and offers explicit import.
3. Compatible solved facts union into full solved set.
4. Shared whitelisted settings import only when chosen according to the frozen settings policy.
5. Unlocks are re-derived from full solved set; achievements are reconstructed rather than copied from demo flags.
6. Import provenance prevents duplicate side effects on repeated boot/import.

### Compatibility rule clarified
A demo solve is compatible only when the full-game mapping declares the demo case equivalent. Minimum identity is stable case ID plus compatible rules/content identity; a canonical content hash should be used by the import manifest when practical.

### Crash trace
If crash occurs after merged profile is written but before import provenance is marked, the next import repeats the same union. Because solved-set union and achievement reconstruction are idempotent, progress does not duplicate or shrink. Provenance then closes the transaction.

### Result
PASS. Demo can carry progress without becoming authority over full saves.

---

## S07 — Existing full progress plus older/newer/incompatible demo imports

### Existing full progress
Demo import never replaces a full profile. `full_solved ∪ compatible_demo_solved` is monotonic.

### Older compatible demo
Compatible solved facts add; already-solved IDs remain one fact.

### Incompatible revised demo case
Its solved flag is not imported. Other compatible solved facts still merge. The UI reports that this puzzle changed rather than silently claiming a replay is required for the entire demo.

### Newer/future schema demo
Older full runtime does not destructively parse/overwrite it. Import is refused or deferred while the current full profile remains intact.

### Settings
Current full settings win by default. Explicit `Use Demo Settings` applies only whitelisted compatible keys and never touches solved progress.

### Result
PASS. No path shrinks existing full solved progress.

---

## S08 — Two-device Cloud conflict with disjoint solved sets + conflicting resume/settings

### Example
Device A local solves `{1,2,3,4,7}`; Device B Cloud contains `{1,2,3,4,8,9}`. Same supported schema/rules/content mapping.

### Merge
- solved -> `{1,2,3,4,7,8,9}`;
- tutorials/glossary -> union;
- unlocks/completion/achievements -> recomputed;
- resume -> choose one compatible resume as convenience, never merge placements;
- settings -> device-local by default, unless a separately tested Cloud-settings policy is later chosen.

A clock skew can change last-selected/resume convenience only; it cannot erase a solved fact.

### Result
PASS.

---

## S09 — Offline solves -> Steam returns -> achievement/Cloud reconciliation

### Trace
1. Steam unavailable: local rules, saves, progression and controller input continue.
2. Case solve commits to local progress atomically before any platform action.
3. Achievement eligibility is reconstructed locally.
4. Steam returns: adapter retries eligible achievement unlocks and Cloud sync.
5. Cloud semantic merge occurs before upload.
6. Platform failure cannot roll back local solve.

### Result
PASS. Steam is optional transport/integration, not puzzle authority.

---

## S10 — Corrupt primary + valid backup; both corrupt; future-version save on older build

### A. Corrupt primary + valid backup
Backup restores authoritative local profile, corruption is quarantined/non-blockingly reported, then Cloud reconciliation runs.

### B. Both local primary and backup corrupt
A hidden hazard exists if the app immediately commits an empty replacement before Steam Cloud is checked; that empty profile could later be uploaded over recoverable Cloud data.

### **REPAIR P9-05 — unrecoverable-local quarantine state**
When both local primary and backup are invalid:
1. preserve corrupt files;
2. create an **in-memory recovery candidate**, not a committed empty authoritative profile;
3. attempt platform/Cloud initialization when available;
4. if a valid compatible Cloud profile exists, restore/merge it and atomically commit locally;
5. if Cloud is unavailable or invalid, show explicit recovery warning and allow the player to start a new local profile only through a deliberate action;
6. until a valid profile is chosen/committed, Cloud upload is disabled.

This supersedes any reading of Phase 8 that would immediately persist a blank profile after both local copies fail.

### C. Future-version save opened by older build
Do not migrate downward, do not overwrite, do not Cloud-upload from that profile. The safest baseline is guarded refusal to mutate the profile; optional ephemeral play must use a separate non-authoritative session if implemented.

### Result
PASS after P9-05. This is a major persistence repair.

---

## S11 — Content update changes a previously solved case

### Contradiction found
Phase 7 correctly rejects incompatible *demo import* solves. Applying the same rule to an already-solved full-game profile after a patch could silently unsolve a case and potentially revoke 100% completion, violating the monotonic-progress principle.

### **REPAIR P9-06 — post-release solved grandfathering**
For the full game after public release:
- a material puzzle edit increments `content_version` and invalidates certificate/resume state;
- an already-recorded full-game solved fact for that stable case remains **grandfathered solved for progression, completion and achievements**;
- its in-case resume placements are discarded on content mismatch;
- replay opens the revised case normally and may show it as `Solved (updated)` until replayed, but replay is never required to preserve prior completion;
- if a revision is so fundamental that grandfathering would be misleading, ship it under a new case ID and treat replacement/removal as an explicit product migration, never silent unsolving.

Pre-release demo import remains stricter: an incompatible demo solve need not become a full-game solve because it has not yet been authoritative full-game progression.

### Result
PASS after P9-06; solved progress remains monotonic across ordinary content patches.

---

## S12 — Late 9x9 / 4-piece / 5–6-predicate case on handheld

### Interaction trace
- Player cycles only four pieces; no inventory scrolling burden.
- Cursor grid means no precision drag.
- Six compact cards fit in the hard layout target; details are focus-expanded.
- Current-state inspect can show component patterns, areas and boundary contacts without hypothetical previews.
- Reposition is one user-visible transaction; cancel restores exact prior placement.

### Fatigue risks
1. Four-piece states can require frequent piece selection/reposition.
2. Six predicates can turn inspect into visual clutter.
3. Fine region outlines can become visually dense when multiple tiny components exist.

### Phase-9 curation constraints
- Six predicates remain a **hard exception ceiling**, not a mastery target; prefer 4–5.
- A late case with six cards must fail curation if any predicate is decorative/redundant.
- Tiny-component clutter is a readability rejection reason even when mechanically valid.
- Difficulty must come from coupling, not forcing repeated tray management.

### Empirical gate P9-E03
On target handheld hardware, a representative 9x9/4-piece/6-card case must support ten minutes of repeated inspect/reposition/undo without focus loss, mistaken piece identity or unreadable region/hole state. If it fails, cut/re-author the case before expanding UI complexity.

### Result
DESIGN PASS / EMPIRICAL FATIGUE GATE.

---

## S13 — 30-case floor vs 36-target campaign value/session shape

### 36-case path
At ordinary 2–8 minute puzzle solves with some 8–15 minute mastery cases, the game naturally supports multiple 15–40 minute sessions and a finite authored arc.

### 30-case floor
The product remains coherent if six weak cases are cut, provided:
- all six acts retain a readable arc;
- F2–F8 credibility and anti-repetition gates survive;
- demo does not consume the only good examples of late families;
- 30 accepted cases still contain a finale and sufficient coupled late-game density.

Commercial gate remains authoritative: if the final campaign is 30 and median blind first-play completion is <3 hours, reassess list price toward $7.99 instead of padding.

### Result
PASS. Quantity is subordinate to curation.

---

## S14 — 100% completion / replay / postgame without grind

### Trace
- Finale solve marks campaign complete.
- 100% means all shipping cases solved, reconstructed from solved facts.
- Case select shows remaining unsolved cases.
- Replaying solved cases never clears solved records.
- `Clear Placement and Replay` resets only current board state.
- Postgame hardest-case filter is navigation only, not new progression.
- No timers, move medals, streaks, grind currencies, procedural filler or leaderboards are required.

### Content-update interaction
P9-06 prevents an ordinary patch from silently removing 100% from a player who already earned it.

### Result
PASS.

---

## S15 — Rapid input during animation, reposition, undo, reset-hold and success transition

### Hazard
Phase 6 says placement animations are skippable/accelerated by subsequent input, but without an exact transaction boundary a fast sequence could render stale topology, double-commit a reposition, undo a state whose animation has not settled, or trigger reset after success.

### **REPAIR P9-07 — command/animation transaction rule**
Puzzle truth never waits for presentation animation.

For every board command:
1. input resolves against the latest **committed** session state;
2. legal command commits atomically and immediately computes the new evaluation snapshot;
3. presentation tween reads `old_snapshot -> new_snapshot` but is disposable;
4. a later legal command may cancel/fast-forward stale tweening and starts presentation from the latest committed truth;
5. no second command may mutate a temporary held/reposition state ambiguously: `B` while held cancels/restores old placement; `A` on a legal new footprint commits one REPOSITION; ordinary Undo is available again only after that held transaction resolves;
6. reset-hold completion resolves against the latest committed state at the instant the hold completes; cancellation before threshold has no effect;
7. when a solved snapshot is reached, the solved progress transaction commits **before** success presentation/navigation;
8. after solved commit, destructive board commands for that completed session are ignored during the <=450 ms success lock; navigation commands may buffer only to the completion panel, never mutate the solved board underneath it.

No input queue may replay obsolete board mutations after a newer navigation/state transition.

### Result
PASS after P9-07. Animation becomes a projection of truth, never a lock around truth.

---

# 3. Cross-scenario invariant checks

## Progression / teaching
PASS after P9-01/P9-02.
- Component, marker, hole and boundary semantics cannot be skipped before Act II.
- Repeated 4/6 skipping cannot reach Act VI without four backfills.
- Finale still requires four other Act-VI solves.
- No new currency or punitive lock was introduced.

## No-silent-progress-shrink
PASS after P9-05/P9-06.
- local/Cloud compatible solved facts union;
- demo import only adds compatible facts;
- existing full progress wins over incompatible demo data;
- both-local-corrupt state cannot auto-upload a blank profile before Cloud recovery attempt;
- future-version saves are protected from old-build overwrite;
- ordinary post-release case edits grandfather prior full-game solves.

## Anti-oracle boundary
PASS.
- ghosts show footprint legality only;
- current committed topology can be inspected;
- predicate truth can be shown for current state;
- no hypothetical topology, articulation highlight, candidate ranking, solution count or extendability check;
- primer selection cannot query certifier/solution state.

## Experimentation usability
PASS by design, empirical confirmation still required.
- unlimited undo/reposition/reset;
- no fail modal;
- animation is cancellable and does not throttle attempts;
- no anti-brute penalties;
- difficult cases must earn difficulty through curation/search-space/deduction structure.

---

# 4. Canonical Phase-9 amendments

These amendments are binding for later phases and must be consolidated into the final freeze:

1. **P9-01 Act-I foundation lock:** C1–C4 sequential mandatory; C5/C6 free. Act II can unlock after C1–C4.
2. **P9-02 teaching lint:** content manifest rejects skippable-only prerequisite semantics that a later act assumes without established/self-describing UI grammar.
3. **P9-03 anti-brute thresholds:** MID normally >=40 canonical complete assignments; LATE >=100; MASTERY >=500, finale >=1000 preferred; exceptions require explicit human curation.
4. **P9-04 primer boundary:** primer eligibility may use engagement/retry metadata, but primer selection/content may never query solution/candidate/extendability state.
5. **P9-05 unrecoverable-local quarantine:** both-local-corrupt state remains uncommitted until Cloud recovery attempt or explicit new-profile choice; upload disabled meanwhile.
6. **P9-06 solved grandfathering:** post-release full-game solved facts are monotonic across ordinary content revisions; revised resume may be invalidated, solved completion is not silently revoked.
7. **P9-07 rapid-input transaction rule:** domain commits/evaluation precede and outlive disposable animations; solved progress commits before success transition; held reposition/reset/undo have unambiguous serialization.

---

# 5. Empirical gates carried to Phase 10/implementation

- **P9-E01 Handheld max-layout:** 9x9 + six objectives + max supported text scale/high contrast at 1280x800, board >=40 logical px/cell, no board pan.
- **P9-E02 Anti-brute playtest:** representative Acts III–VI must reward intended invariant reasoning over systematic complete-state enumeration.
- **P9-E03 Handheld fatigue:** ten-minute repeated inspect/reposition/undo on a 9x9/4-piece/6-card case without focus/readability/piece-identity failure.
- **P9-E04 Demo comprehension:** first-time players can explain after six demo cases that objectives judge remaining open space and can distinguish component vs enclosed pocket vs boundary contact without formal topology vocabulary.
- **P9-E05 Price-value:** retain Phase-7 30-case/<3h reassessment toward $7.99.

None of these gates requires a new mechanic. Failure should first cut/re-author content or simplify presentation.

---

# 6. Phase-9 conclusion

All 15 required journeys have been simulated. The product survives as a coherent compact puzzle game, but Phase 9 repaired four consequential specification hazards: skippable boundary teaching, blank-save-over-Cloud recovery risk, post-update silent unsolving, and rapid-input/presentation race ambiguity. It also tightened brute-force curation and primer boundaries.

**PHASE 9 = COMPLETE.**

## NEXT — PHASE 10 ADVERSARIAL REVIEW
Run destructive review passes against the now-repaired whole-game specification. Minimum attack list:
1. **Fun/repetition:** does 30–36 authored content still collapse to articulation spotting despite family quotas?
2. **Blind brute force:** attack representative MID/LATE/MASTERY cases against P9-03/P9-E02 without adding friction.
3. **Predicate redundancy:** prove late 4–6-predicate cases are not decorative constraint piles.
4. **Topology readability:** holes-as-components, boundary signatures, area multisets and marker partitions under worst-case 9x9 visual density.
5. **Controller/focus abuse:** rapid piece cycling, held reposition, panel focus, reset-hold, pause, success and reduced-motion transitions.
6. **Persistence corruption:** interrupted atomic writes, corrupt primary/backup, future-version refusal, Cloud conflict, offline return, demo import replay/idempotency and P9-05 quarantine.
7. **Progress monotonicity:** content revisions/removals, achievement reconstruction, 100% status, demo/full compatibility and grandfathered solves.
8. **Progression exploits:** every legal 4/6 + 24-total + finale route after P9-01; verify no required reasoning vocabulary is bypassed.
9. **Oracle leakage:** inspect, legality ghost, primers, predicate cards, resume state and platform metadata must reveal no future-solution information.
10. **Scope creep:** attack any pressure for extra shapes, OR/NOT predicates, editor, procedural filler, narrative wrapper, telemetry or live-service retention.
11. **Commercial honesty:** 30 vs 36 cases, demo content, price band, Deck/locale/controller claims and actual launch feature gates.
12. **Implementation ambiguity:** attempt to build the rules/session/save/platform contracts from documents and list every place a fresh implementer would still need to invent gameplay behavior.

Phase 10 must repair contradictions in authority files (or explicitly supersede them) and produce a go/no-go recommendation for Phase 11 Specification Freeze.