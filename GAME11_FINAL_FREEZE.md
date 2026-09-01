# GAME #011 — MISSING STEP — FINAL SPECIFICATION FREEZE

Date: 2026-09-01
Status: **DESIGN COMPLETE = YES**
Working title: **Missing Step** — commercial title not cleared.

## 1. Final authority order
For Game #011, implementation must read in this order:
1. `GAME11_FINAL_FREEZE.md` — freeze gate, authority map, acceptance matrix and conflict rulings;
2. `GAME11_MECHANICAL_ARCHITECTURE.md` — exact gameplay truth;
3. `GAME11_CONTENT_ARCHITECTURE.md` — campaign/case/certification truth;
4. `GAME11_UX_PRESENTATION_ARCHITECTURE.md` — player-facing interaction/accessibility truth;
5. `GAME11_COMMERCIAL_RETENTION_MODEL.md` — progression/demo/commercial boundaries;
6. `GAME11_TECHNICAL_SPECIFICATION.md` + `GAME11_TECHNICAL_HOSTILE_CLOSURE.md` — implementation/persistence/contracts;
7. `GAME11_WHOLE_GAME_SIMULATION.md` + `GAME11_ADVERSARIAL_REVIEW.md` — lifecycle repairs and measurable empirical gates;
8. `GAME11_PRODUCT_THESIS.md` — product identity/scope intent;
9. Phase-2 tournament and Phase-1 research — history/evidence only, never override later frozen rules.

If prose conflicts, later phase/freeze rulings above prevail. Rejected tournament concepts are not Game #011 canon.

## 2. Frozen product
Compact PC/Steam-first single-player deterministic puzzle game about subtractive programming.

Hook: **cross out one step in a repeating machine program; shortening the loop re-phases all later operations against the other loops.**

Core player loop: READ -> HYPOTHESIZE -> DELETE -> PREVIEW -> RUN -> EXPLAIN -> REVISE.

One workpiece. 1–4 cyclic tracks. Four opcodes only: `PUSH`, `TURN`, `STAMP`, `CLAMP`. Finite public horizon. Standard exactly-one deletion; late mastery exactly one deletion on each of two named tracks. No editing during RUN.

## 3. Exact gameplay rules — frozen
- Workpiece: lane 0|1, orientation N|E, successful-stamp count, blocked-push count.
- Tracks execute one token each global tick in public fixed A -> B -> C -> D order.
- Deletion shortens the edited loop and preserves stable token identity.
- If authored start token is deleted, first execution resolves to next surviving clockwise token in original cycle.
- `PUSH`: toggles lane; destination lane1 is blocked only when clamp is active that tick; lane1->0 is never blocked; each blocked attempt increments count.
- `TURN`: toggles N/E.
- `STAMP`: increments successful stamps iff lane==1 at its execution instant; lane0 STAMP is visible no-op.
- `CLAMP`: schedules lane1 clamp for the next tick only; multiple same-tick clamps coalesce; a clamp on final tick has no beyond-horizon effect.
- At tick start prior scheduled clamp is promoted, new schedule cleared, tracks execute A->D, cursors advance, trace records.
- Target is evaluated after final tick unless an allowed monotone max/equality has already been exceeded.
- Target grammar: conjunction only of final lane, final orientation, stamp count exact/range, blocked-push count exact/range.
- No hidden state/randomness/physics truth.

## 4. Edit and Preview rules — frozen
Standard case: exactly one deletion total from explicit eligible token IDs.

Mastery: exactly one deletion on each of two named tracks, max launch search space 6x6=36 pairs.

Deletion cannot leave a track with <2 tokens.

Preview may show surviving loops, resolved anchors, full opcode alignment to public horizon, cycle markers and clamp-active-at-start schedule. Before RUN it may **not** expose future lane/orientation/counts, target pass/fail, dead status, solution count, ranking, alternate candidate traces or recommendations.

RUN is the experiment boundary. After RUN, full committed trace/result may be replayed, scrubbed, stepped and accelerated.

## 5. Content/campaign freeze
Target 42 certified cases; **quality floor 36**. Never pad weak/near-duplicate content to reach 42.

Six acts:
1. THE GAP
2. WINDOWS
3. WHICH ONE?
4. SAME TICK
5. FALSE FRIENDS
6. TWO ABSENCES

Required reasoning families: recurrence contraction, clamp windows, orientation parity, positional duplicate deletion, same-tick A->D choreography, coupled two-delete beat frequency.

At 36-case floor preserve minimum family/act coverage specified in Content Architecture and Phase-10 perceptual mix gates. Generated candidates are never authority until exhaustively certified and human-curated.

Normal campaign expects UNIQUE solutions; UNSAT/EQUIVALENT_MULTI rejected; TRACE_MULTI excluded from normal launch campaign unless explicitly admitted later without affecting required progression.

Demo: 8 canonical full-game cases exposing recurrence, second track, CLAMP, deceptive deletion, duplicate position, same-tick order and a compact two-delete teaser.

## 6. Progression/commercial freeze
Premium one-time purchase. No ads, consumable hints/lives, premium currency, battle pass, gacha, grind/streak economy or live-service dependency.

Working launch-price band: $9.99–12.99, final price empirical near launch.

Mandatory onboarding: first three Act-I cases. Afterward act progression uses quotas, not strict linear locks. 42-case default: 5/6 Act I, 5/7 Acts II–V, 6/8 Act VI. 36-case campaign scales approximately 75–80% per act while preserving onboarding.

Ending eligibility, all-cases completion and mastery completion are distinct derived states. Skipped cases remain revisitable.

Hints explain rules/concepts only; no solver oracle. Preview/accessibility/retries never affect achievements/progression.

## 7. UX/accessibility freeze
PC/Steam first; Steam Deck/1280x800 first-class; full controller plus mouse/keyboard and keyboard-only paths.

Primary puzzle truth must fit without mechanically relevant scrolling under standard <=4-track cases. At 150% text, target clauses, selected deletion slots, track IDs, active tick and primary actions remain usable.

Required launch accessibility: enlarged text, high contrast, non-color redundancy, reduced motion, flash restraint, volume controls, complete non-pointer paths, visible focus, optional opcode legend, adjustable playback speed, first-attempt step-through accessibility option.

Duplicate tokens remain positionally distinguishable. A->D order and CLAMP-next-tick behavior require redundant visual communication.

## 8. Technical/persistence freeze
Preferred baseline: Godot 4.7.2 stable + GDScript, upgradeable only after deterministic regression equivalence.

One pure Rules Core is shared by runtime and certifier. Animation/UI never owns gameplay truth. Every shipping case must have matching canonical certificate keyed by normalized case hash + rules version + certificate/core semantic version.

Runtime/campaign truth derives from canonical case IDs and completed-case IDs. Act unlock/ending/mastery booleans are derived, not authoritative persisted flags.

Persistence requires versioned atomic primary + previous-valid backup, explicit migrations, corrupt-primary recovery before default creation, future-version refusal without downgrade rewrite, and writer/cloud blocking while incompatible future save is refused.

Newly solved completion must be durably saved before ordinary navigation implies it is committed.

Steam Cloud is synchronization only; local validated save generation is gameplay authority. Achievements reconcile idempotently from local canonical progress.

Demo import unions canonical completed IDs, ignores unknown IDs, preserves stronger full progress and uses per-setting user-modified provenance for settings precedence.

## 9. Scope exclusions — frozen
Launch does not include:
- fifth opcode;
- second workpiece;
- insertion/reordering/token movement;
- free programming, variables or conditionals;
- >4 tracks or >6 original tokens/track;
- >2 deletions or two deletions on same track;
- factory building/belts/resource extraction;
- physics/random failures/reflex timing;
- multiplayer/network dependency;
- large branching narrative;
- launch Workshop/editor requirement;
- leaderboards/dailies/streaks/economy/live service.

These are exclusions, not unimplemented required features.

## 10. Implementation-flexible decisions
A dedicated implementation team/session may choose without reopening game design:
- exact machine/art style, shaders, decorative theme and audio assets;
- exact panel proportions while meeting layout/accessibility contracts;
- animation duration/easing and default playback speeds;
- exact stable cryptographic hash algorithm before first authoritative certification, provided it is versioned/canonical;
- exact internal class/module names;
- later stable Godot patch/minor after golden-trace/regression equivalence;
- optional soundtrack/artbook;
- final commercial title;
- final launch price after required empirical recheck.

These choices may not alter rules, information boundaries, progression or scope.

## 11. Empirical implementation/playtest gates
Design freeze does not pretend these can be answered on paper. They are measurable release gates:
- **BF-1:** Act V/VI median committed candidate RUNs <50% of legal space; max-36 mastery median <=12 RUNs.
- **BF-2:** >=70% successful testers articulate causal reasoning for final edit(s), not pure enumeration.
- **TRACE-1:** >=75% identify decisive divergence region within two replay/scrub attempts after one failure.
- **TRACE-2:** learned non-mastery late-case median solve <=8 min; recurring >12 min signals replacement/reduction.
- **CONTENT-1:** >=80% sampled same-act case pairs perceived as different reasoning lessons.
- **UX-1:** representative Act-VI case completes controller-only at 1280x800 + 150% text with no pointer fallback and no clipped mechanical truth.
- **DEMO-1:** >=70% first-time demo testers can explain that deletion shortens the loop and changes later alignment by demo end.
- **PRICE-1:** price rechecked near launch against final case count/playtime/polish/current market/regional guidance.

Failing an empirical gate defaults to revising/replacing content or presentation. It does not authorize new mechanics automatically.

## 12. Acceptance matrix
| Area | Freeze acceptance |
|---|---|
| Product hook / target player | PASS |
| Mechanical state / tick order | PASS |
| Four opcode semantics | PASS |
| Start-anchor/deletion semantics | PASS |
| Single + two-track edit contracts | PASS |
| Target grammar / win-fail | PASS |
| Preview non-oracle boundary | PASS |
| Solver/certificate authority | PASS |
| >=6 reasoning families | PASS |
| Campaign structure / 36 floor / 42 target | PASS |
| Duplicate/near-duplicate curation | PASS |
| Controller / 1280x800 / 150% | PASS |
| Reduced motion / non-color redundancy | PASS |
| Progression quota / skip behavior | PASS |
| Ending vs completion/mastery | PASS |
| Demo/carry-over/achievements | PASS |
| Premium monetization boundary | PASS |
| Rules Core / runtime separation | PASS |
| Save migrations / backup recovery | PASS |
| Future-version refusal | PASS |
| Demo settings provenance | PASS |
| Cloud/platform authority | PASS |
| Certificate/manifest drift | PASS |
| Whole-game lifecycle | PASS |
| Repetition / brute-force adversarial pass | PASS with measurable empirical gates |
| Scope exclusions | PASS |
| Production implementation in factory | NOT STARTED / correctly out of scope |

## 13. Contradiction scan
Final scan finds no unresolved gameplay contradiction among product, mechanics, content, UX, commercial, technical, lifecycle and adversarial documents.

Resolved historical ambiguities include:
- CLAMP next-tick vs current-tick semantics;
- deleted start-anchor cursor resolution;
- duplicate opcode identity;
- same-tick A->D ordering;
- Preview oracle boundary;
- demo settings precedence through provenance;
- derived progression vs stale saved booleans;
- save-success-before-navigation;
- future-version refusal blocking writers/cloud push;
- 42 target vs 36 quality floor;
- brute-force/fatigue handled by measurable curation rather than punishment/new mechanics.

No fresh implementation session should need to invent important gameplay design.

# FREEZE VERDICT
**GAME #011 MISSING STEP — DESIGN COMPLETE = YES.**

Migration target preference: `Mikayilzade/missing-step` unless a later explicit naming decision changes repository naming. On 2026-09-01 the repository did not exist (GitHub returned Not Found). Therefore migration is pending and this full Game #011 package must remain a frozen NON-ACTIVE safety archive until a destination exists and migration integrity is verified.