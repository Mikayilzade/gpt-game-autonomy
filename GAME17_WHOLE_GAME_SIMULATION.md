# GAME #017 — THE QUEUE KNOWS — PHASE 9 WHOLE-GAME SIMULATION

Date: 2026-09-06
Status: PHASE 9 COMPLETE
Production implementation: NO
Authority: active Game #017 authority through `GAME17_TECHNICAL_SPEC.md`.

This pass simulates the complete player/product lifecycle on paper and repairs cross-file ambiguity without inventing production code.

---

# 1. Simulation method

The game was walked as a player-facing product through:
- first boot and settings;
- QK01–QK06 demo/onboarding;
- transition into paid/full game;
- Chapters 2–6 through QK36;
- optional mastery;
- ordinary failures, wrong commits and certified dead states;
- checkpoint/restart/save/resume;
- controller-only and 1280x800 handheld use;
- unusual but legal interventions;
- replay/fast-forward/evidence review;
- demo-to-full carryover;
- completion/replay.

The pass asks at every step: what does the player know, what can they legally do, what state changes, what is saved, what can be explained, and can a fresh implementation derive the answer from existing authority?

---

# 2. First boot -> first meaningful decision

## Boot
1. Logo/title.
2. Main menu: Continue disabled on first launch; New Game, Case Select after progress exists, Settings, Accessibility, Quit.
3. First-run accessibility shortcut appears before gameplay, but is skippable. It exposes text scale, reduced motion, contrast/non-color reinforcement, audio levels, remapping and hold/toggle behavior.
4. Input glyphs reflect last meaningful input. No keyboard is required.
5. New Game opens QK01 directly after one short premise card: the goal is to learn from customer choices, not run a business.

No economy, score, staff roster or efficiency KPI appears.

## QK01 paper run
Public state: A/B counters, three Price/Routine candidates, one sign intervention.
Player inspects one customer. Candidate chips state Price and Routine; Routine's familiar A/threshold are public. Type Lens may show separate `IF PRICE` and `IF ROUTINE` rows.

Player drafts B FREE. The draft changes only public counterfactual Type Lens results. It does not preview actual choices.
Player applies setup and resolves.
Logical state resolves immediately in authored arrival order; presentation then animates B/A/B.
Evidence strikes incompatible candidate chips. All three become singleton. Objective completes.

Expected learning: `I changed a public rule -> candidate models predicted different choices -> observed choice eliminated models.`

Failure/unusual path: player leaves ineffective setup where candidate models remain pooled. QK01 may use a tutorial prompt to explain that no proof was created, but must not call the branch impossible unless certified. Restart is instant.

Result: first meaningful intervention occurs before any management habit is established. PASS.

---

# 3. QK02–QK06 demo arc simulation

## QK02 — active diagnostic test
Baseline A/B service1 causes Urgent and Routine to choose A. Player can inspect this publicly through separate candidate rows. Setting A service3 creates the exact equality edge: Urgent chooses B; Routine stays familiar A because disadvantage=2 equals threshold2.

Critical UX check: the game must not highlight `service3` as the recommended action. Hint tier may remind player to seek a state where candidate rows differ. PASS.

## QK03 — congestion confound
Player makes A FREE. Early Price customers queue there. Later Urgent customers evaluate the queue state produced by earlier choices. C5 may choose A even though Price is not its actual type.

The player opens C5 evidence. The evidence card restores the immutable pre-choice A/B completion facts; it does not explain C5 by hidden actual type. The final physical queue therefore cannot be mistaken for the evidence snapshot.

This is the first major product-identity proof: final location is not a type label. PASS.

## QK04 — sequential contingent test
Cohort 1 resolves, one service tick advances, checkpoint is written at the next INTERVENE boundary. The second intervention is chosen from the now-public residual state/evidence.

A fixed blind second action must fail certification; at least two allowed observation branches require different safe/diagnostic responses. The player can reload the checkpoint, but doing so restores the entire branch state and cannot merge evidence from a discarded future.

Content warning: QK04 is a logical contract until exact certified customer/world data is authored. Implementation may not improvise a merely illustrative instance. PASS WITH EMPIRICAL/DATA GATE.

## QK05 — pooling is enough
Player configures Privacy separation. Success is permitted while non-target candidate sets remain >1. The objective rail must explicitly say that identifying everybody is unnecessary.

This prevents a learned-but-wrong meta-rule that every case ends with singleton chips. PASS.

## QK06 — first synthesis
Three counters, eight customers, two cohorts, wait <=4, two interventions. The first observation must partition allowed worlds such that at least two branches require different second-stage safe actions. The solver must prove both the information objective and wait constraint.

The player can inspect exact wait/service premises; animation speed cannot affect the constraint.

Like QK04, exact numeric content remains a certified-data obligation. If authored numbers fail, data changes; mechanics do not. PASS WITH EMPIRICAL/DATA GATE.

## Demo end
After QK06, causal recap states the learned loop: change system -> observe choice -> use evidence. Demo ends cleanly at Chapter 1. It may show later chapter silhouettes and store/wishlist CTA, but no paid-game mechanic is teased as if missing from the demo.

Demo target 25–35 minutes remains plausible only if QK04/QK06 certified instances do not require long manual enumeration. This is an implementation playtest gate.

---

# 4. Demo -> full game carryover

On first full-game launch, platform service checks for a compatible DemoCarryover payload.

If found:
- show one explicit import offer;
- import completed QK01–QK06/progression and compatible settings only;
- do not import an in-progress demo attempt as authoritative paid-game state;
- mark import idempotently so relaunch cannot duplicate progression/achievements;
- full-game achievements are not retroactively spammed for every demo action. Chapter-completion achievement may unlock through an explicit post-import reconciliation policy if Phase 8 achievement contract allows it; otherwise it unlocks on replay/next qualifying full-game event.

If payload is absent/corrupt/incompatible:
- full game remains fully playable;
- no progress is destroyed;
- QK01–QK06 can be replayed.

PASS.

---

# 5. Chapter 2 simulation — TEST, DON'T GUESS

QK07–QK12 widen intervention choice rather than rule vocabulary.

Representative run:
- player sees two candidate types currently pool;
- two or three legal presets are available;
- Type Lens lets player compare candidate models under each drafted public state;
- player chooses a diagnostic state, resolves, and gets exact elimination evidence;
- one case introduces Convenience through visible walk cost;
- one introduces a public cardinality constraint;
- one asks EXCLUDE rather than full IDENTIFY.

Progression feeling: the player is no longer learning evaluator definitions; they are selecting experiments.

Hostile legal behavior: player repeatedly chooses the fastest-looking setup. Some cases produce little/no information but remain legal. The game does not scold with a management score; objective remains unsatisfied and hints point to divergent candidate predictions.

PASS.

---

# 6. Chapter 3 simulation — THE CROWD IS PART OF THE TEST

QK13–QK18 normalize congestion-mediated evidence.

Representative multi-customer run:
1. player predicts early candidates separately;
2. resolves cohort;
3. later arrivals see queues produced by earlier hidden-type choices;
4. evidence snapshots preserve exact historical state;
5. capacity/service-time preset can improve service while reducing information, or worsen service while creating a useful split;
6. first HYBRID case requires both proof and wait/service constraint.

The human-solvability gate is essential here: player must not manually enumerate thousands of worlds. UI exposes class-level comparisons and stored evidence; content proof route must fit 2–6 major deductions.

Potential boredom check: if every case reduces to inspecting a matrix and selecting the only divergent column, content fails despite mechanical correctness. Phase-5 anti-triviality/repetition validator plus Phase-10 fun review must attack this directly.

PASS WITH FUN GATE.

---

# 7. Chapter 4 simulation — ENOUGH TO ACT

QK19–QK24 shift the win condition.

Representative case:
- six customers remain in several candidate worlds;
- target is to guarantee no Privacy customer reaches an exposing counter;
- player need not distinguish Price from Convenience among non-targets;
- public cardinality constraint may remove worlds after evidence;
- Commit checks the required predicate across all remaining worlds.

The objective rail says `Safe in every remaining possibility`, avoiding technical quantifier language as the primary wording.

Wrong commit:
- if submitted diagnosis/claim is false, DIAGNOSIS_FAIL;
- reveal/explanation may show actual hidden world only after terminal commitment according to policy;
- restart/checkpoint is offered immediately.

PASS.

---

# 8. Chapter 5 simulation — DESIGN THE HALL

QK25–QK30 make three-counter mechanism design normal.

Representative contingent run:
- player has three legal levers but budget 2;
- several candidate models predict the same first choice;
- an apparently unattractive counter can be made useful as a diagnostic alternative;
- cohort 1 observation partitions worlds;
- player selects a different second intervention depending on partition;
- at least half the chapter accepts multiple certified policy classes.

Unusual legal path: player spends budget on two changes before first Resolve. If legal under the case's intervention window, the solver treats it normally. If it destroys future identifiability, no special authored failure text is required; exact dead-state certification may later offer checkpoint reload.

Dominant-strategy check: there must be no universal `make the cheapest counter free` or `always slow familiar counter` policy. Validator repetition metrics and Phase-10 adversarial review must explicitly search for cross-case dominant heuristics.

PASS WITH DOMINANT-STRATEGY REVIEW REQUIRED.

---

# 9. Chapter 6 simulation — THE QUEUE KNOWS

QK31–QK36 use the full existing vocabulary: up to 10 customers, three counters, 2–4 cohorts, and upper intervention ceilings only late.

Representative QK36 flow:
1. brief states HYBRID proof/service goal and public constraints;
2. player inspects candidate groups rather than opening every customer one-by-one;
3. intervention 1 creates an informative but operationally costly split;
4. cohort 1 resolves;
5. evidence partitions worlds and changes queues;
6. service ticks advance deterministically;
7. player chooses intervention 2 contingent on observed branch;
8. later cohorts create/resolve another ambiguity;
9. final Commit checks proof and service condition;
10. explanation summarizes causal chain, not every solver node.

The late game must remain readable at 1280x800 by keeping candidate chips in inspector, using fixed queue slots and staged cohort trays, and never requiring more than one secondary panel to understand current state.

No new heuristic, economy, re-choice behavior or real-time mechanic appears in the finale. PASS.

---

# 10. Optional mastery simulation

MQK01–MQK12 unlock in pairs after chapter capstones.

A completionist may alternate campaign/mastery or return later. Mastery:
- uses tighter budgets/constraints;
- may use two public cardinality constraints;
- may expose certified dead branches deliberately;
- may use selected pre-certified hidden-world replay variants;
- never gates campaign;
- never requires disabling accessibility;
- never introduces a sixth heuristic.

A mastery replay can advertise `Alternative policies exist` only when validator proves materially distinct policy classes. It does not reveal them.

PASS.

---

# 11. Failure, recovery and dead-state simulation

## Constraint failure
A public hard constraint is violated at its exact evaluation boundary. Simulation records the event; presentation explains the violating state. Animation timing is irrelevant. Offer checkpoint/restart.

## Wrong diagnosis
Commit is deliberate and irreversible for that attempt. Wrong answer enters DIAGNOSIS_FAIL and can reveal truth post-terminal. No lives/currency penalty.

## Certified information dead state
Only exact solver/certificate may declare it. If runtime cannot cheaply prove one, it remains silent rather than guessing. Player can always restart/reload legal checkpoint.

## Checkpoint misuse attempt
Player resolves, learns evidence, then reloads earlier checkpoint. Authoritative evidence/candidate sets rewind with the branch. Player's own memory cannot be erased, but game state never merges future knowledge. This is acceptable for a single-player puzzle; checkpoints are convenience, not an anti-spoiler system.

## Repeated restart
No penalty, no achievement lockout, no hidden adaptation. Fixed authored campaign world remains the same unless a replay variant explicitly declares otherwise.

PASS.

---

# 12. Save/resume simulation

## Mid-case quit
At a legal persistence point, CurrentSession stores authoritative state, selected fixed world, evidence and checkpoint. Presentation animation state is discarded.

On resume:
- rebuild hall from authoritative state;
- if quit occurred during presentation replay, resume at the already-resolved logical boundary rather than trying to reconstruct tween time;
- evidence remains inspectable;
- next simulation result is identical to uninterrupted play.

## Corrupt primary save
Validate primary; if invalid, preserve it and attempt previous-good backup. Never overwrite readable data with failed migration output.

## Content-version correction
Stable IDs map progress. If current attempt is incompatible, restart that case while preserving completed-case progression where logically possible.

## Cloud divergence
Never silently merge current attempts. Conflict UI shows timestamps/progress. Completed-case union is permitted only under compatible schema and non-destructive progression rules.

PASS.

---

# 13. Controller / Steam Deck paper run

At 1280x800:
- objective rail remains visible;
- hall uses center majority;
- inspector is drawer/overlay rather than permanent width loss;
- 10 customers occupy fixed slots/staging without overlap;
- 12px apparent character-height target is preserved; text scales paginate instead of shrinking;
- candidate chips are icon + word + shape, never color-only;
- LB/RB cycles focus groups; D-pad/stick moves stable spatially; South selects; East backs; contextual Type Lens/evidence shortcuts remain reachable;
- no drag, hover, keyboard or precision pointer is mandatory.

Stress path: player opens evidence history in a 10-customer case at 130% text scale. Hall may be partially covered; this is acceptable because evidence inspection is modal/contextual and logical state is paused at player-control boundary. Closing returns focus to originating object.

PASS, subject to implementation-device playtest.

---

# 14. Unusual legal-choice audit

1. **No intervention / ineffective intervention:** legal only when case schema permits. Outcome may produce no information; objective remains unsatisfied. No fake failure.
2. **Spend all budget early:** allowed if legal. Can create certified dead state; exact recovery only.
3. **Choose closed/infeasible counter via UI:** impossible because player does not directly route customers; evaluators exclude infeasible counters.
4. **All candidate models predict same counter:** Type Lens may show this openly; it is not a hidden leak. Player learns current state is non-diagnostic.
5. **Only one feasible counter:** all types choose it; evidence normally eliminates nothing. Content validator rejects using this as fake diagnostic evidence.
6. **NO_FEASIBLE_COUNTER:** campaign case must explicitly allow it or certification rejects reachable state.
7. **Stable-ID tie:** deterministic but should not be the intended invisible puzzle distinction. Content rejection gate already covers this.
8. **Fast-forward/skip Resolve:** presentation changes only; evidence/event order unchanged.
9. **Replay evidence repeatedly:** no state mutation.
10. **Manual note contradicts mechanics:** allowed; manual note is visually distinct and cannot alter candidate set.
11. **Switch input devices mid-panel:** glyphs/focus update, logical state unchanged.
12. **Quit during animation:** resume from authoritative resolved boundary.
13. **Attempt Commit before proof:** UI may allow only if case contract permits submission; objective proof check prevents lucky success where evidence guarantee is required.
14. **Accessibility changes mid-case:** presentation/input only; no achievement/progression penalty.
15. **Replay a solved case:** no campaign regression; achievements are idempotent.

PASS.

---

# 15. Cross-file contradictions / ambiguity found and repaired

## Repair A — GAME_INDEX lag
`GAME_INDEX.md` still reported Phase 7 while `STATUS.md` correctly reported Phase 8 complete. This run updates the index to Phase 9 complete / Phase 10 next. `STATUS.md` remains live phase authority.

## Repair B — Chapter unlock wording
Phase-5 chapter section says Chapter 1 gate clears QK01–QK06, while later progression/commercial authority allows 4-of-6 local flexibility with foundation prerequisites.

Canonical interpretation locked here:
- **QK01–QK06 are all mandatory foundation/demo cases and must all be cleared before Chapter 2.**
- For Chapters 2–5, local 4-of-6 unlock flexibility may expose the next chapter only when any specifically named foundation prerequisite for that later material is also cleared.
- Final campaign completion requires all 36 campaign cases.
- Mastery never gates campaign.

This preserves the demo as a coherent six-case teaching arc and makes 4-of-6 a temporary anti-hard-stop progression convenience, not permanent campaign omission.

## Repair C — QK04/QK06 exactness
Phase 5 intentionally leaves exact final hidden-world/customer tables for QK04 and QK06 to certified implementation-data authoring while calling their logical obligations final. This is acceptable only as an **empirical/content-data gate**, not implementation freedom to redesign mechanics.

Locked rule:
- dedicated implementation must author exact QK04/QK06 data before vertical-slice/demo acceptance;
- validator must certify the stated contingent-policy and wait constraints;
- if no bounded instance satisfies the contract, return to design review rather than weakening proof silently.

## Repair D — progression completion meaning
4-of-6 chapter advancement and `all 36 required for campaign completion` are not contradictory after Repair B: advancement can be flexible, final completion is exhaustive. UI must distinguish `Next chapter available` from `Chapter complete`.

## Repair E — evidence explanation wording
Older tournament text sometimes describes a direct actual-type `choice trace`. Later mechanics/UX correctly forbid actual-type reason leakage before proof. Later authority wins: pre-proof explanation is public facts + candidate contradictions/counterfactuals only. Actual-type-specific explanation is allowed after singleton proof or terminal reveal.

No mechanical formula change is required.

---

# 16. Whole-product pacing verdict

The designed arc is coherent:
- minutes 0–10: deterministic self-selection and active testing;
- demo: congestion, sequential observation and pooling establish the actual identity;
- early paid game: experiment selection broadens;
- midgame: congestion becomes causal instrument and objectives diversify;
- late midgame: partial identification/all-world guarantees prevent singleton monotony;
- late game: contingent three-counter policies synthesize existing vocabulary;
- mastery tightens proof/service budgets rather than adding systems.

The principal unresolved risk is **fun/repetition**, not specification completeness: Type Lens + deterministic candidate models could make some cases feel like mechanically scanning a comparison matrix. Phase 10 must attack whether the optimal play degenerates into `try drafts until rows differ`, whether one lever family dominates, and whether 36+12 cases overstate the sustainable content volume.

---

# 17. Phase-9 acceptance result

Whole-game simulation covers:
- first boot;
- first decision;
- complete QK01–QK06 demo arc;
- demo carryover;
- Chapters 2–6 progression through QK36;
- mastery;
- wrong commits, constraints, dead states, checkpoint/restart;
- save/resume/cloud/content-version recovery;
- controller/Deck stress path;
- unusual legal player actions;
- replay/fast-forward;
- progression ambiguity and evidence-leak repairs.

No production implementation was started.

**PHASE 9 WHOLE-GAME SIMULATION = COMPLETE.**

# NEXT DESIGN STEP — PHASE 10 ADVERSARIAL REVIEW

Run dedicated destructive passes against the full active authority. At minimum attack:
1. fun and `Type Lens -> scan rows -> pick divergence` trivialization;
2. cross-case dominant strategies and lever dominance;
3. 36+12 content exhaustion/repetition;
4. QK04/QK06 contingent-policy feasibility;
5. scope/asset/authoring burden;
6. solver/world-space/performance ceilings;
7. hidden-truth leakage and oracle surfaces;
8. controller/1280x800 late-case ambiguity;
9. accessibility contradictions;
10. checkpoint/save/cloud/demo-import corruption or exploit paths;
11. objective/world-quantifier ambiguity;
12. implementation ambiguity across mechanics/content/UX/technical spec;
13. commercial/demo failure modes;
14. empirical gates that must survive into implementation handoff.

Repair canonical authority where a contradiction is found. Save `GAME17_ADVERSARIAL_REVIEW.md`. Advance to Phase 11 only if no unresolved design blocker remains.