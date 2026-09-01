# GAME #011 — MISSING STEP — PHASE 9 WHOLE-GAME SIMULATION

Date: 2026-09-01
Status: **PHASE 9 SUBSTANTIAL PASS COMPLETE — whole product lifecycle simulated**
Authority: active Game #011 design files through `GAME11_TECHNICAL_HOSTILE_CLOSURE.md` -> this file for cross-phase walkthrough findings.

Purpose: simulate the complete player/product lifecycle on paper and attack contradictions that do not appear inside isolated mechanic, UX, commercial or technical documents. No production implementation is started here.

---

## 1. First boot -> first case

Expected path:
1. title screen loads local primary save; if absent, checks backup state then creates fresh profile only after both locations are genuinely absent/invalid;
2. platform adapter may initialize Steam, but campaign does not wait for it;
3. settings are available before gameplay;
4. fresh player enters Act I with C01–C03 mandatory onboarding path;
5. case screen shows one workpiece, target, visible loop, eligible deletion positions and RUN;
6. C01 teaches that removing a token closes the loop; Preview shows the contracted schedule but not future lane/stamp result;
7. player commits RUN and sees causal A->D playback;
8. result compares actual vs target; success auto-saves completion; failure has no resource consequence.

Cross-contract result: PASS. Product thesis, UX and technical facade agree on planning -> Preview -> RUN -> Result.

Potential failure attacked: Steam unavailable at boot. Null platform path still permits title, save load, settings, campaign and local achievement eligibility. Platform reconciliation can happen later.

---

## 2. First 10 minutes

Likely player experience:
- C01: understands deletion closes loop;
- C02: realizes recurrence count changed, not merely one event removed;
- C03 / next teaching case: sees a second track and fixed A->D order;
- early failure is diagnostic rather than punitive;
- Preview reduces clerical alignment work while leaving physical state prediction to player.

Adversarial behavior: player tries each legal deletion by brute-force RUN without reasoning.
- This is possible in tiny tutorials by design and is not prevented artificially.
- Retry friction remains low.
- Campaign depth must therefore come from growing hypothesis space / trace interpretation, not from hiding outcomes or imposing retry penalties.
- Later ordinary cases expose roughly 5–12 legal single deletions; mastery exposes 9–36 pairs. Brute force remains physically possible but becomes less attractive if RUN/diagnosis teaches causality and curated cases produce meaningful deceptive prefixes.

Result: PASS. No anti-bruteforce punishment should be introduced.

---

## 3. First hour / Act I -> Act II

42-case target progression:
- Act I contains 6 cases;
- C01–C03 mandatory;
- next-act quota = 5/6.

Walkthrough:
- player solves mandatory 3;
- solves any 2 of remaining 3;
- one difficult case may remain unsolved;
- Act II unlocks from completed canonical IDs + manifest, not a stored boolean;
- skipped Act-I case remains selectable and may be solved later.

Hostile path: player solves C01,C02,C03,C04,C05, leaves C06. Act II unlocks. Later content update reorders C04/C05. Unlock remains correct because completion identity is by stable `case_id`, not ordinal.

Result: PASS.

---

## 4. Act II — CLAMP misunderstanding

Likely confusion: player reads CLAMP as “blocks lane 1 now” rather than “arms next tick.”

Required recovery loop already exists:
- CLAMP animation arms now;
- arrow points to next tick;
- next tick header shows active clamp marker;
- Preview may reveal the active-clamp schedule because that is deterministic from opcodes;
- failure says blocked push count/tick, not solution.

Adversarial path: player accelerates playback to 4× and misses the cue. Result screen + replay/step makes diagnosis recoverable. Accessibility step-through can be enabled from first attempt.

Result: PASS.

---

## 5. Act III — duplicate token identity

Hostile case: A loop contains two PUSH tokens. Player says “I deleted PUSH, why is the other PUSH solution different?”

Required explanation:
- each token has stable slot/token identity;
- deletion ghost preserves original slot;
- loop closure visibly changes neighboring sequence;
- result never labels the solution merely by opcode name;
- accessibility focus can narrate slot/track identity.

Certificate layer treats token IDs as distinct edits and rejects normal-campaign EQUIVALENT_MULTI successes.

Result: PASS.

---

## 6. Act IV — same-tick A->D choreography

Whole-game risk: player learns to reason only by columns/periods and overlooks within-column order.

Simulation:
- Act III has already established positional reasoning;
- Act IV introduces cases where A STAMP then B PUSH differs from A PUSH then B STAMP;
- track order is never authored per case; always A->D;
- persistent ribbon and sequential playback communicate order;
- target/failure traces expose the actual physical consequence.

No new opcode is needed. Result: PASS.

---

## 7. Act V — late deceptive prefixes

Late cases may share useful first 4–6 ticks between correct and near-correct edits.

Hostile player behavior:
- watches only first cycle;
- sees machine “working” and skips playback;
- final target fails after later recurrence drift.

Recovery:
- exact horizon remains public;
- Preview shows full schedule to horizon;
- result shows final deltas;
- replay can scrub late divergence;
- no solver ranking is surfaced.

Risk retained for playtest: if many Act-V cases are solved primarily by tedious manual full-horizon simulation, they fail content curation even when mathematically valid. This is an empirical content-quality gate, not a missing mechanic.

Result: mechanically PASS; playtest gate retained.

---

## 8. Act VI — first two-delete mastery

First mastery case should use 3×3=9 pairs, not jump directly to 36.

Player path:
- UI shows `Remove 1 from A` and `Remove 1 from B` independently;
- RUN disabled until both selected;
- Preview displays the two contracted loops aligned on shared ticks;
- candidate pair is reasoned about as coupled periods;
- no third deletion ever appears.

Late mastery C09-style case has 16 pairs and exact unique certificate. A maximum launch case may have 36 pairs, still exhaustively certifiable.

Hostile behavior: player changes A selection repeatedly while leaving B fixed. Preview updates only current pair, never ranks A alternatives. PASS.

---

## 9. Ending vs all-cases vs mastery

Scenario at end of Act VI:
- player reaches quota (e.g. 6/8 in 42-case target);
- some optional ordinary/mastery cases remain unsolved;
- ending sequence becomes eligible;
- UI state says ending reached/available while separately showing remaining campaign cases;
- all-cases completion achievement remains locked;
- mastery achievement remains independently derived from designated mastery IDs.

Technical correction from Phase 8 means these are derived states, not stale save booleans.

Hostile path: after ending, player solves remaining cases offline. Local completed IDs update; all-cases/mastery flags derive correctly even before Steam reconnect. PASS.

---

## 10. Demo -> purchase -> full import

Demo player solves 6/8 canonical cases, modifies text scale and reduced motion, then buys full game.

Full-game boot possibilities:
### Fresh full profile
- import demo progress offered;
- canonical completed IDs union into empty full set;
- supported settings imported;
- tutorial flags imported;
- quotas derived;
- corresponding achievements reconciled when platform is available.

### Existing partial full profile
Use Phase-8 hostile example: union progress, full user-modified setting keys win, untouched defaults may inherit demo preferences.

### Repeated import
Same export hash/state produces semantic no-op. No duplicate achievement/progression side effects.

### Demo missing/corrupt
Full game remains fully playable; import failure is not purchase blocker.

Result: PASS.

---

## 11. Offline play -> Steam reconnect

Scenario:
1. Steam unavailable;
2. player solves multiple cases locally, maybe reaches ending;
3. save writes locally and remains authority;
4. Steam returns later;
5. platform adapter initializes;
6. achievement reconciliation derives earned achievements from local canonical progress and sets missing platform achievements;
7. campaign never waits on callback.

Cloud conflict rule is intentionally not treated as gameplay truth. Implementation must use Steam Cloud carefully around local atomic files; if platform cloud integration cannot preserve primary+backup recovery semantics reliably, local persistence wins and Cloud may be disabled/reconfigured rather than weakening saves.

Result: PASS with implementation integration test required.

---

## 12. Save corruption during long campaign

State: primary corrupt after Act V; previous valid backup exists from shortly earlier.

Load:
- primary rejected without write;
- backup loaded/migrated;
- user informed of recovery;
- at worst progress since previous valid generation may be lost, but empty profile is never written before recovery attempt;
- next legitimate save preserves recovered generation until replacement validates.

Hostile variant: both primary and backup corrupt.
- application may offer fresh-profile path only after both fail;
- corrupted files should be preserved/renamed where practical for support rather than immediately destroyed;
- no fake restoration claim.

Result: PASS.

---

## 13. Future-version save / downgrade

Player opens save with older executable after testing newer build.

Required:
- future version refused read-only;
- no downgrade rewrite;
- no empty save overwrite;
- user can exit/update executable;
- platform reconnect must not upload an older blank save over the newer incompatible one merely because load failed.

New integration requirement: **a refused future-version save is a persistence-blocked state, not “no save found.” Cloud/local save writers must remain disabled for that profile until compatible runtime loads it or user explicitly chooses a separate new profile/path.**

This closes a lifecycle hole not explicit enough in the earlier architecture.

---

## 14. Content update invalidates certificate

Development/release verification encounters a case whose case hash changed without recertification.

Correct behavior:
- verification fails closed;
- case is not silently admitted;
- author regenerates certificate under exact current Rules Core;
- if rules semantic version changed, all affected golden traces/certificates rerun.

Player-facing shipped build should never discover routine certificate mismatches if release gate works. If a malformed external/content package somehow reaches runtime, show recoverable content error rather than invent semantics.

Result: PASS.

---

## 15. Unusual player behavior

### Repeatedly toggling edits during planning
Safe; no gameplay state mutation except selection save. Preview remains pure schedule derivation.

### Quit during RUN
No mid-RUN persistence required. Resume returns to planning with selected edits; deterministic RUN restarts from tick 1.

### Quit immediately after success
Completion checkpoint must be persisted before navigation can safely imply success is committed. UI should not advance to next case until save transaction has either succeeded or produced a visible persistence error/retry path.

### Rapid input while playback animates
Input can pause/speed/skip where allowed but cannot mutate Rules Core state. Presentation consumes immutable trace.

### Controller disconnect
Game pauses or switches to another available semantic input path; no puzzle-state loss.

### Change accessibility settings mid-case
Presentation/layout/playback changes only; selected edits/case truth stay intact.

### Change locale mid-case
Semantic enums/IDs stay stable; UI relocalizes strings; no save/content identity change.

### Revisit solved case and choose a losing edit
Solved completion remains solved; replay failure does not revoke canonical completion or achievements.

All PASS by existing contracts.

---

## 16. Whole-game contradictions / repairs

### Repair P9-1 — save-success navigation ordering
New explicit persistence rule:
- when a case is newly solved, update in-memory completion -> attempt atomic save -> only after success may UI present the completion as durably committed and navigate without warning;
- if save fails, keep result visible and offer Retry Save / continue only with explicit risk messaging if implementation chooses to allow it;
- Steam achievement callback never substitutes for local save success.

Reason: otherwise a player can see NEXT CASE, quit, and lose newly earned progress.

### Repair P9-2 — future-version refusal blocks writers/cloud push
A future-version save is not equivalent to empty profile. No local/default overwrite or cloud notification may occur while profile is in incompatible-read refusal state.

### Repair P9-3 — `ending_sequence_seen` is presentation state only
If needed to avoid replaying ending automatically every boot, persist `ending_sequence_seen` separately. Ending eligibility itself remains derived from completion IDs/manifests.

No mechanical contradiction required changing opcodes, targets, deletion budgets or campaign structure.

---

## 17. Phase-9 verdict

Coverage:
- first boot: PASS;
- first 10 minutes: PASS;
- first hour: PASS;
- act transitions / quota skip behavior: PASS;
- CLAMP misunderstanding/recovery: PASS;
- duplicate identity: PASS;
- same-tick order: PASS;
- late deceptive prefixes: PASS with empirical curation gate;
- mastery ramp: PASS;
- ending vs all-cases/mastery: PASS;
- demo purchase/import: PASS;
- offline/Steam reconnect: PASS;
- save corruption recovery: PASS;
- future-version downgrade: PASS after writer/cloud blocking repair;
- certificate mismatch: PASS;
- unusual player behavior: PASS;
- durable save before success navigation: repaired.

**PHASE 9 COMPLETE.**

## NEXT ACTION
Proceed to **Phase 10 Adversarial Review**. Attack fun/repetition, brute-force dominance, content exhaustion, preview-oracle leakage, late-horizon clerical burden, scope creep, accessibility/readability, save/cloud conflict, certificate/manifest drift and implementation ambiguity. Any remaining unknown that is empirical rather than design-specifiable must be named as a measurable implementation/playtest gate. If Phase 10 closes cleanly, continue to Phase 11 Specification Freeze in the same run when safely connected.