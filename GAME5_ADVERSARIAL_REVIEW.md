# GAME #005 — ADVERSARIAL REVIEW

Last updated: 2026-08-23
Factory run: **10 — extended pass**
Phase: **10 — Adversarial Review**
Selected concept: **G5C02 — Tension Budget**
Production implementation: **NOT STARTED**

# PHASE 10 REVIEW STATUS = COMPLETE

This review assumes every previous document is wrong until it survives attack. Phase-9 contradictions are treated as real defects, not clerical details. Authoritative repairs are separated into `GAME5_PHASE10_AMENDMENTS.md`.

---

# 1. Review verdict at a glance

The product thesis survives.

No review finding requires:
- a fourth load archetype;
- another carriage;
- combat/enemies;
- precision movement;
- hidden information;
- numeric engineering UI;
- rope simulation authority;
- currency/progression systems;
- longer campaign padding.

The major defects are finite-state authoring contradictions around low-load revisions. They can be repaired by constraining snap count/budget/mutation direction, not by weakening the core model.

---

# 2. Fun / repeated-action attack

## Attack
The repeated verb is always:
- reach carriage;
- grab;
- slide to band;
- watch rig move;
- traverse.

Could this become a slow world-space menu selector by hour 3?

## Evidence for survival
- mature encounters separate decisions by player location and mutation;
- one commit changes several world objects simultaneously;
- three load families have different traversal semantics;
- planned meaningful commit ceiling is low (<=4), reducing repetitive hand motion;
- no animation wait is a puzzle resource;
- campaign ceiling is already modest.

## Required defense
- U03 <=~2–3 s normal intentional carriage move remains empirical gate;
- do not retain an encounter whose primary novelty is only a different room theme;
- optional remixes remain first cut;
- late campaign must include both mutation and non-mutation mastery so the same dramatic trick does not dominate.

Verdict: **SURVIVES / EMPIRICAL FEEL GATE REMAINS EXISTENTIAL.**

---

# 3. Hour-5 repetition / content exhaustion attack

## Attack
18 signatures are metadata. Actual player reasoning could still collapse into:
“try band, cross route, try another band.”

## Risk clusters
- repeated-archetype trio originally E11/E12/E13;
- relays E08/E14/E20/E25;
- mutation/return-inversion cluster in late content;
- 5-band/four-load scenes may feel visually denser without being cognitively different.

## Repair
- interleave repeated-family encounters with S07/S12 content;
- structural fingerprint V14/V15 remains mandatory;
- Phase 10 amendment freezes a revised Band-C order;
- 26 is a working campaign, not a sacred count; 24–28 remains valid and cutting a weak near-duplicate is preferred to adding mechanics.

Verdict: **SURVIVES WITH CONTENT-DENSITY GUARDRAIL.**

---

# 4. Extreme-state heuristic attack

## Attack
Player ignores TAUT and always chooses SLACK/HIGH extremes.

## Defense
- Span only traversable at TAUT;
- three-load compromise can require middle states;
- early E03 establishes this explicitly.

## New adversarial requirement
Late campaign must contain at least two non-tutorial situations where TAUT is useful for reasons involving different load combinations, so “middle matters” is not merely an onboarding gimmick.

Verdict: **SURVIVES.**

---

# 5. All-TAUT heuristic attack

## Attack
After learning middle compromise, player defaults to all-TAUT whenever available.

## Defense
- not every budget/snap path contains an all-TAUT vector;
- Gate/Lift may require HIGH to create a route;
- player-location and future-access value can make all-TAUT locally safe but globally wrong.

Authoring must avoid making `[1,1,...]` a universal “safe state”. V13 permanent-best-band catches the worst form.

Verdict: **SURVIVES.**

---

# 6. Blind band enumeration / brute-force attack

## Attack
Preview is honest and bands are few. Cycle every band, memorize result, select answer.

## Defense
The design intentionally permits local experimentation. Mature depth is not secrecy; it is separated decisions.

A mature encounter is invalid if one safe carriage station acts as the full solution table.

Implementation obligations:
- V11 decision separation;
- V12 static enumeration rejection;
- V13 permanent best band;
- solver reports shortest commit/separation path;
- empirical prototype measures blind full-enumeration frequency.

Do not add move limits, hidden states or slow animations.

Verdict: **SURVIVES / AUTHORING GATE REMAINS CRITICAL.**

---

# 7. Restart brute-force attack

## Attack
Rapid restart makes experimentation nearly free.

## Decision
That is acceptable.

The game is a reasoning puzzle, not an attempt-economy game. Fast restart is a quality feature. If restart makes a puzzle trivial, the puzzle lacks structural depth and should be fixed/cut.

Verdict: **NO REPAIR NEEDED.**

---

# 8. Transition-timing exploit attack

## Attack
Use moving Lift/Gate/Span transient states to bypass intended stable logic.

## Defense
- preview non-authoritative;
- Gate traversal only at required stable clearance;
- Span only stable TAUT;
- Lift can carry rider but legal exits only at stable docks;
- V07 reduced-motion equivalence makes timing dependence mechanically invalid.

Implementation must ensure collision adapters follow semantic contract rather than raw animation position where those diverge.

Verdict: **SURVIVES / INTEGRATION TEST REQUIRED.**

---

# 9. Mutation surprise / unfairness attack

## Attack
Objective mutation changes the same band into a harmful post-revision configuration. Could the player be trapped/crushed or feel the game changed rules arbitrarily?

## Defense
- physical load add/remove must be shown;
- total budget remains conserved;
- anchor physical identity does not move;
- C1 promotes only after stable mutation.

## New defect found
A technically legal alternate route might reach the objective while the carriage is on a band not considered by the intended solution. If that band's post-mutation state is unsafe/softlocked, the objective becomes an exploit trap.

**P10-F01 — NEEDS AUTHORITY.**

Repair: every band from which the objective can legally be activated must resolve to a safe stable post-mutation state and valid C1, or objective access must be physically impossible in that state for an honest world reason. Add explicit mutation-activation safety validator.

Verdict: **SURVIVES AFTER AMENDMENT.**

---

# 10. Finite-state feasibility attack

Phase 9 proved several existing rows impossible.

Root cause: Phase 4 froze local rules but Phase 5 did not explicitly check the cardinality/connectivity of the legal conserved vector space before assigning snap counts to low-load revisions.

This is not a reason to loosen the model.

Repair:
- first-class validator for state-space feasibility;
- explicit low-load mutation templates;
- campaign metadata corrections.

Verdict: **SURVIVES AFTER AMENDMENT.**

---

# 11. E01 fake-tutorial attack

## Attack
Allowing a special one-load tutorial would teach a different game than the real conserved give/take system.

Decision: **REJECT THE EXCEPTION.**

E01 must use at least two active loads. One can be non-completion-critical, but it must visibly receive/give pull so the first action already shows authentic conservation.

Verdict: **AMEND CONTENT, DO NOT AMEND CORE.**

---

# 12. Movement-pillar creep attack

## Attack
Suspended mechanical setting tempts jumping, falling, moving-platform dexterity and timing.

Decision:
- no jump/dash/crouch;
- edges should be authored safe/readable;
- Lift riding is transport, not platforming;
- no completion-critical stepping off in motion.

If environment art makes players repeatedly attempt platforming, presentation is misleading and must be changed.

Verdict: **SURVIVES.**

---

# 13. Rope-physics creep attack

## Attack
Visual team/implementation may want dynamic ropes and then begin reading simulation output for gameplay.

Decision:
- dynamic secondary rope jiggle is cosmetic only;
- semantic band drives gameplay;
- load pose is deterministic;
- any physics component must reset to semantic pose and cannot alter traversal.

Verdict: **SURVIVES / HARD BOUNDARY.**

---

# 14. Engineering-UI creep attack

## Attack
Internal 0/1/2 quanta and budget B make it easy to expose numeric gauges because they simplify debugging.

Decision:
- developer diagnostics may show numbers;
- retail normal play must not require them;
- accessibility labels may show state words only;
- if empirical testers demand numbers to understand ordinary play, that is a product readability failure, not permission to convert the game into arithmetic.

Verdict: **SURVIVES / EMPIRICAL KILL GATE.**

---

# 15. Camera-information attack

## Attack
2–4 loads may not fit one isometric view; player misses a consequence and blames the game.

Defense:
- causal framing;
- gameplay cables as visual composition lines;
- off-screen edge cue / brief camera emphasis;
- Rig Focus can reinforce semantic state without showing a graph.

Reject levels whose essential consequence is intentionally impossible to inspect.

Verdict: **SURVIVES / U06 TEST.**

---

# 16. Color/audio dependence attack

Grayscale + mute + low vibration.

Required truth remains through:
- cable sag/straightness;
- tension hardware posture;
- load silhouette/position;
- optional state-word labels.

Verdict: **SURVIVES / U01/U08.**

---

# 17. Reduced-motion attack

## Attack
Shortened transitions could change Gate/Span timing or Lift rider behavior.

Decision:
- solution graph must be identical;
- Gate/Span logic queries semantic stable states;
- Lift rider test runs at normal/reduced durations;
- no achievement/timing target depends on transition duration.

Verdict: **SURVIVES / AUTOMATED PARITY TEST.**

---

# 18. Controller disconnect attack

## Attack
Controller disconnects while the carriage is between bands.

Bad outcomes:
- auto-commit nearest band;
- carriage drops into a different state;
- game continues and player is stranded.

Authoritative decision:
- disconnect of the sole active controller triggers pause/device prompt;
- preview remains non-authoritative and frozen for presentation;
- **disconnect never commits**;
- player may reconnect or switch valid input device, then continue preview or explicitly cancel;
- restart remains available from pause/menu.

Verdict: **RESOLVED IN AMENDMENT.**

---

# 19. Save/restart state-corruption attack

## Attack vectors
- quit in preview;
- quit in transition;
- quit in mutation;
- spam restart during transition;
- stale callback after restart;
- corrupted current-run save;
- corrupted profile save;
- content definition version changed between sessions.

Technical spec has credible containment:
- checkpoint-level durability;
- semantic snapshot only;
- transition epochs;
- C1 after stable mutation;
- atomic files + previous known-good profile backup where possible;
- content version fallback.

Additional acceptance decision:
- CurrentRunSave corruption may fall back to C0 without campaign loss;
- ProfileSave corruption may never silently start a new profile; attempt backup, preserve files, show recovery state.

Verdict: **SURVIVES / EXACT ACCEPTANCE ADDED.**

---

# 20. Demo-divergence attack

## Attack
Demo becomes a separate simplified code path that tests well while retail mechanics differ.

Decision:
- one Domain Core;
- same load adapters and validators;
- demo may use separate encounter definitions/progression registry only;
- no demo-specific mechanical exceptions;
- demo save cannot accidentally mark retail progression completed.

Verdict: **SURVIVES.**

---

# 21. Performance attack

Worst baseline encounter:
- 4 loads;
- 5 snap bands;
- modest cable/pulley visuals;
- no AI/rope sim/network.

There is no valid design excuse for low performance.

Risk is presentation overproduction, not simulation complexity. Effects must scale down without reducing mechanical readability.

Verdict: **LOW TECHNICAL RISK.**

---

# 22. Validator false-confidence attack

## Attack
A level passes graph/math validators but is boring or visually confusing.

Decision:
Validators guarantee legality/scope, not fun.

Human/empirical gates remain required for:
- tactile carriage feel;
- world readability;
- causal attribution;
- repetition;
- perceived challenge;
- screenshot/trailer legibility.

Systemic signature dedup is a review trigger, not proof of uniqueness.

Verdict: **SURVIVES WITH CORRECT TOOL ROLE.**

---

# 23. Alternate-solution over-policing attack

## Attack
Validator finds an unintended shorter solution and implementation patches it automatically.

Decision:
- alternate solutions are acceptable when safe, deterministic and consistent with product grammar;
- only patch when alternate collapses intended reasoning family, bypasses tutorial literacy or causes exploit/softlock;
- record meaningful alternates for QA.

Verdict: **SURVIVES.**

---

# 24. Difficulty / hint attack

## Attack
No hint system could make some players stall; adding one late could require design invention.

Decision for freeze:
- full hint system is not mandatory for 1.0 design;
- UX may support observational graduated hints later without altering mechanics;
- if implemented, hints can point out relationships/current consequences, never reveal internal numbers;
- final implementation may ship without hints if playtests show onboarding/readability sufficient.

This is intentionally implementation-flexible, not an unresolved core rule.

Verdict: **NOT A FREEZE BLOCKER.**

---

# 25. Difficulty-mode attack

No separate easy/hard ruleset is required.

Accessibility settings do not alter logic. Optional mastery remixes are the only baseline extra challenge path.

Verdict: **NO SECOND BALANCE MATRIX.**

---

# 26. Commercial-value attack

## Attack
4–6 hours / 26 encounters at working $19.99 could feel short if mechanic repeats.

Decision:
- do not pad;
- free demo must prove quality;
- price remains business band, not gameplay mandate;
- if late playtests prove only 24 excellent encounters, ship 24 rather than retain weak filler;
- if perceived value is insufficient, adjust price/polish/positioning rather than add systems.

Verdict: **SURVIVES / COMMERCIAL PRICE REMAINS EMPIRICAL.**

---

# 27. Store-position attack

`Tension Budget` sounds more like engineering/resource management than physical traversal.

Decision:
- label is internal only;
- final store title may change;
- store copy must show physical simultaneous consequence;
- project/repo slug can remain `tension-budget` after migration even if commercial title changes.

Verdict: **NOT A DESIGN BLOCKER.**

---

# 28. Scope attack

Potential feature requests rejected during review:
- second carriage;
- cutting/reattaching cables;
- breakable ropes;
- hazards/enemies to create urgency;
- moving target/timed doors;
- skill jumps;
- inventory tools;
- procedural rig generation;
- scoring economy;
- campaign hub requiring lots of narrative assets.

None is necessary to repair a current defect.

Verdict: **SCOPE REMAINS CONTROLLED.**

---

# 29. Implementation-ambiguity audit

Questions a fresh implementation session should now be able to answer:
- what owns puzzle truth? **Domain Core semantic state.**
- what are legal bands? **authored 3–5 snap states subject to conservation/feasibility.**
- can preview create traversal? **No.**
- can timing create a solution? **No.**
- can restart lose campaign progress? **No.**
- when is C1 durable? **after mutation stabilizes.**
- can controller disconnect commit? **No.**
- can runtime repair bad content silently? **No.**
- can rope physics decide a route? **No.**
- can accessibility change logical solution? **No.**
- can alternative valid solutions exist? **Yes, if they preserve rules/safety and don't collapse required teaching.**

Remaining gameplay unknowns are empirical feel/readability, explicitly allowed by factory rules.

---

# 30. Freeze-critical repair list

Must be made authoritative before Phase 11:
1. P9-C01 one-load E01 repair.
2. P9-C02 3->2 low-load mutation feasibility.
3. P9-C03 2->3 4-band addition repair.
4. P9-C04 empirical prototype repair.
5. first-class finite-state feasibility validator.
6. mutation-activation safety validator from P10-F01.
7. revised E11–E15 sequencing.
8. exact mutation directions/budgets/snap counts for E16–E20 and late mutation templates.
9. controller disconnect preview policy.
10. corrupt-save acceptance behavior.

All ten are resolved in `GAME5_PHASE10_AMENDMENTS.md`.

# PHASE 10 REVIEW DECISION

The design has no remaining adversarial finding that requires a new gameplay pillar or reopening concept selection.

**PHASE 10 ADVERSARIAL REVIEW = PASS, CONDITIONAL ON THE ACCOMPANYING AUTHORITATIVE AMENDMENTS.**