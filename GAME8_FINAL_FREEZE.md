# GAME #008 — FINAL SPECIFICATION FREEZE

Last updated: 2026-08-30
Phase: **11 — Specification Freeze**
Selected concept: **G8C02 Locksmith's Margin**
Working title: **Locksmith's Margin**
DESIGN COMPLETE = **YES**
Production implementation started in factory: **NO**
Migration status: **PENDING — dedicated repository not found at freeze time**

This is the final normalized authority for Game #008. It resolves Phase-9 and Phase-10 repairs into one implementation-ready specification. Earlier Game #008 files remain provenance/history and detail references, but where wording conflicts with this document, **this document governs**.

---

# 1. Frozen product identity

Locksmith's Margin is a PC/Steam-first premium single-player tactile systemic puzzle game about **destructively editing a very small set of persistent keys so those same keys can open several different fictional locks**.

The central product promise is:
> File a few persistent keys to open many different locks — every cut can gain one fit while permanently destroying another, and failed tests are deterministic information.

The product is **not** a realistic locksmith simulator, burglary game, lockpicking game, dexterity filing game, shop-management game, roguelite, crafting economy, or real-world locksmith training product.

Frozen platform/product baseline:
- PC/Steam first;
- Windows primary shipping target;
- Linux/Steam Deck architecture target;
- keyboard+mouse and controller first-class from baseline;
- offline single-player core fully playable without Steam;
- premium finite product;
- working price hypothesis $17.99 USD;
- pre-release empirical review band $14.99–$19.99.

---

# 2. Canonical puzzle authority

A case contains:
- `C` reasoning-critical columns, normally 4–6;
- integer depth states `0..D`, with normal campaign `D in {3,4,5}`;
- 1–3 persistent key blanks;
- 1–6 required locks;
- finite accepted depth sets per lock/column;
- visible access predicates over opened locks;
- optional tutorial/mastery metadata that cannot alter fit.

For each blank `b`, authoritative key state is vector:
`K_b = [k_b[1], ..., k_b[C]]`.

For every lock `l` and column `c`, authoritative fit is a non-empty finite accepted set:
`A[l,c] subset {0..D}`.

A key opens a lock iff every current key-column depth belongs to the corresponding accepted set.

Accepted sets are the **only fit authority**. Exact fits, broad/worn fits, and master-style branches are merely different authored shapes of accepted sets. No mesh, physics collision, animation, audio cue, random jam, hidden tolerance, brand-specific geometry, or floating-point contact may alter fit.

---

# 3. FILE rule

`FILE(blank, column)`:
- is legal only when the selected column is below `D` and the blank is legally available;
- increments exactly one authoritative column by exactly `+1`;
- cannot shallow, refill, repair, or add material;
- commits immediately at semantic/domain level before presentation completes;
- appends one authoritative history record;
- truncates the redo tail if taken after Undo.

At max depth, FILE is a no-op with `MAX DEPTH` feedback and no history/progression effect.

Selection/ghost preview is non-authoritative. A distinct explicit FILE commit input is required after preview.

Forward puzzle state therefore preserves the irreversible grammar even though player-time recovery uses unlimited Undo.

---

# 4. TEST rule and information authority

A legal `TEST(blank, lock)` evaluates columns strictly left-to-right.

If all columns are accepted:
- result is OPEN;
- the lock becomes OPENED if not already open;
- all tested depths become accepted observations for that lock;
- visible access consequences derived from the opened-lock bitset resolve in the same semantic action.

If the first incompatible column is `j`:
- columns `1..j-1` are observed as accepted at their tested depths;
- column `j` reveals exactly one failure relation;
- columns after `j` remain unevaluated/unknown for that test.

Canonical failure relations:
- `TOO_SHALLOW`: current depth below every accepted depth;
- `TOO_DEEP`: current depth above every accepted depth;
- `BETWEEN_BRANCHES`: current depth lies between disjoint valid bands but is not itself accepted.

TOO_SHALLOW may additionally expose `LIGHT` when nearest deeper accepted depth is exactly +1, otherwise `STRONG`. This remains a distance class, never an exact hidden target.

A repeated identical legal TEST:
- returns the same semantic result;
- appends a history/checkpoint record because the player really performed it;
- adds zero new knowledge;
- cannot advance tutorial, hint, reward, mastery, achievement, or access state merely by repetition.

Illegal TEST against an inaccessible lock creates no authoritative history or knowledge.

---

# 5. Exhaustive free-testing normalization

Core campaign TESTs cost no currency, durability, score, timer, or forward key state.

Therefore at any fixed current forward state, performing every currently accessible non-duplicate TEST before the next FILE is a rational baseline behavior.

Frozen consequences:
1. The game may not create fake strategy by expecting players to withhold free currently accessible information.
2. Mature cases must retain a meaningful partition/preservation/commitment decision **after exhaustive currently accessible non-duplicate testing at that state**.
3. Diagnostic sequencing is valid only when relevant information is not yet accessible without an OPEN/FILE commitment or when a later key vector is materially different.
4. Access-order depth must come from irreversible opening/key-state consequences, not from arbitrary refusal to perform free tests.
5. No test cost, patience meter, timer, durability, or punitive economy may be added to manufacture scarcity.
6. Validator policy V5 treats exhaustive-current-state testing as an adversarial harness, not a policy that every mature case must defeat.

C10, C12, C23, C25 and especially C30 must be rejected or rewritten if exhaustive-current-state testing removes their real destructive dilemma.

---

# 6. Opened-lock persistence and access

Default campaign objective is `OPEN_ALL_REQUIRED_ONCE`.

Once a required lock is opened on the current forward timeline:
- it remains completed even if the opening key is later filed into an incompatible vector;
- reopening it cannot duplicate completion/access rewards;
- another key/vector may still TEST against it for legitimate observations.

Visible access predicates are limited to deterministic forms equivalent to:
- ALWAYS;
- AFTER_OPEN(A);
- AFTER_ANY(set);
- AFTER_ALL(set).

Access is derived from opened-lock state and visible case data. No random/customer/timer/narrative permission may decide test legality.

Mandatory access graphs must be reachable and must not hide irreversible prerequisites from the player.

---

# 7. Undo / Redo / Restart

Base campaign supports unlimited exact stepwise Undo and Redo.

Undo reverses exactly one authoritative FILE or TEST action, including knowledge and newly-opened/access effects nested in that TEST.

Human memory surviving Undo is explicitly accepted as an assistance/recovery channel. The game does not pretend counterfactual FILE→TEST→Undo probing can erase what the player learned. It is never punished, blocked, monetized, or used to gate progression.

Because this can reduce hidden-information difficulty, every mature required case must retain a non-trivial omniscient partition/coverage problem after accepted sets are known.

Redo:
- replays exact stored transitions;
- never recomputes against time/random state;
- survives save/load with the complete authoritative action timeline and current cursor;
- is truncated only when a new authoritative forward action is taken after Undo.

Restart restores exact authored initial case state and clears current-attempt knowledge/history. It never erases previously committed campaign completion from an older solved attempt.

---

# 8. Truthful TOO_DEEP tutorial

D02 and C03 use the same frozen authority sequence:
1. authored start is solvable and not already irreparably overcut;
2. tutorial asks player to make one visible FILE that creates an overcut for the training lock;
3. player TESTs and receives TOO_DEEP;
4. tutorial explicitly states that the TEST proved the cut is too deep and that the player must rewind the TEST, then rewind the cut;
5. first Undo removes TEST/history/observations;
6. second Undo restores pre-cut key vector;
7. normal case play resumes;
8. Restart also restores the genuinely solvable authored start.

A single Undo may never be described as repairing the overcut after a TEST, because TEST itself is an authoritative history action.

---

# 9. Knowledge and fairness

Player-visible knowledge is monotonic within forward play and tied to stable blank identity.

Ledger categories:
- OBSERVED;
- DEDUCED from universal rules + observations;
- UNKNOWN.

The ledger may expose tested vector snapshots, accepted-prefix facts, blocker relation, shallow strength, OPEN facts, and visible access predicates. It may not expose hidden accepted depths or unevaluated later columns.

Equal-vector blanks have identical fit but can have different knowledge histories. Player-facing identity therefore remains stable across bench position, history, save/load, and UI.

Information-respecting solver/hint logic must preserve that difference unless a full knowledge-preserving permutation exists.

High-risk authored cases **C08–C12, C15–C16, C22–C26, and C30–C32** may ship only if the validator emits/verifies at least one explicit information-respecting witness trace. Before each irreversible FILE in that witness, the choice must be justified from observations/deductions legitimately available at that point. Omniscient solvability alone is insufficient.

C32 additionally requires at least two materially distinct valid solution traces/partitions.

---

# 10. Solver / validator freeze

Two solver modes are mandatory authoring infrastructure:

**Omniscient solver** knows full accepted sets and proves solvability, partitions, softlocks, action bounds and optional mastery properties.

**Information-respecting solver** may choose only from facts legitimately available to a player at that state and is required for fairness and hint safety.

Validator stages must cover at minimum:
- schema legality;
- access reachability;
- omniscient solvability;
- information-respecting fairness;
- proof-only runtime softlock correctness;
- adversarial policy harnesses;
- solution partition extraction;
- canonical duplicate/isomorphism review;
- pacing/action-count metrics;
- tutorial/family/campaign constraints;
- explicit witness traces for the high-risk set above.

Runtime softlock service is proof-only:
- UNSOLVABLE only after a valid proof;
- SOLVABLE when a completion is found;
- UNKNOWN on budget exhaustion;
- UNKNOWN never becomes a warning;
- stale results tied to an older state/version are discarded.

Softlock warnings are advisory and never auto-rewind.

---

# 11. Content architecture freeze

Planning spine remains C01–C32 and demo D01–D06, but **quality outranks quota**.

Release rules:
- hard strong-content floor: **28 validated main-campaign cases**;
- aspirational target: up to 32;
- if only 28–31 remain causally distinct after validation, ship the smaller set;
- if fewer than 28 strong cases survive, reopen/reduce the product rather than pad.

C01–C06 may be mechanically simple because they teach distinct truths. Every C07+ case must state a one-sentence causal `thought delta` from its nearest neighbor.

Cases are merge/cut candidates when they differ only by labels, column permutation, depth translation, blank/lock renaming, accepted-set widening without a new reasoning consequence, or the same policy-failure signature under an isomorphic matrix.

Frozen content families remain:
- causal literacy;
- overlap preservation;
- coverage partition;
- diagnostic sequencing;
- master-branch accepted sets;
- wear/broad-band bridges;
- access order;
- mixed finales.

No new late-game puzzle verb may be introduced merely to create variety.

---

# 12. Demo freeze

Demo is D01–D06, target 20–30 minutes.

It must establish:
- tactile discrete FILE;
- first-blocker deterministic TEST;
- truthful TOO_DEEP + two-Undo history lesson;
- persistent key across different locks;
- same key opening multiple locks;
- deliberate restraint/preservation;
- first 3-lock/2-key partition payoff.

Demo has no master branch, wear, or access gates. It ends after the multi-lock compatibility payoff rather than teaser overload.

Demo achievements are disabled. Full game may idempotently recognize compatible demo completion/tutorial-understood flags and compatible settings, but never transplant arbitrary demo PuzzleState into campaign cases.

---

# 13. UX / presentation freeze

The game is one compact bench, not a traversable room.

Required semantic zones:
- Key Rack;
- Vice/Filing Stage;
- Lock Rail;
- Inspection/Test Cutaway;
- Ledger.

Required camera/focus states may be implemented flexibly, but all gameplay must remain reachable without avatar locomotion or hidden hotspots.

Physical artifact is primary. Ledger externalizes memory but cannot become a clairvoyant numeric solution matrix.

Every critical semantic fact must have redundant readable channels where practical; color/audio/haptics cannot be sole authority.

Required interaction contracts:
- semantic input actions, not device-specific gameplay code;
- full keyboard+mouse path;
- full default-controller path suitable for Steam Deck;
- remapping where platform permits;
- no mandatory drag, hold, timing, or freehand accuracy;
- explicit preview then FILE commit;
- first blocker physically/visually matches domain result;
- later unevaluated columns remain neutral after a failure;
- inaccessible locks remain visible with prerequisite text/icon;
- stable blank/lock identities;
- inspection zoom and scroll rather than microscopic text at 1280x800;
- reduced motion, high contrast, text/UI scaling, non-color semantics, numeric current-key-depth labels as optional accessibility aids;
- accessibility settings may never reveal hidden lock data.

During critical FILE/TEST presentation, implementation must choose **one global deterministic policy**: either reject new authoritative commands with neutral busy feedback or queue at most one semantic command. Mixed per-animation behavior is forbidden. Exact choice is implementation-flexible.

---

# 14. Persistence and solved-review transaction

Every authoritative FILE/TEST/Undo/Redo/Restart and solved-attempt transition must become a durable save candidate. Presentation animation is downstream from already-committed semantic state.

Crash during animation may skip/replay cosmetics but may never create:
- half-cut depth;
- partial TEST knowledge;
- half-open lock/access state;
- duplicated action.

Active attempt persistence includes:
- complete authoritative ActionRecord timeline;
- current cursor/index;
- valid redo tail;
- current PuzzleState/knowledge or deterministic reconstruction data;
- content identity/signature;
- pending solved-review state when applicable.

Final required OPEN does **not** immediately commit permanent campaign progression. It enters `SOLVED_REVIEW_PENDING_COMMIT`.

While pending review:
- exact Undo/Redo remains available;
- crash/quit reloads the exact pending solved attempt;
- no new permanent solved/unlock/achievement fact exists merely from the result animation.

Leaving solved review through Continue/Case Select equivalent runs one idempotent local solve transaction keyed by a stable solve-commit ID. The local journal contains the solved fact, unlock consequences, best-stat comparison and achievement-event IDs.

Power loss at any write boundary must recover to either:
- exact pending solved review; or
- exact fully committed campaign state.

Never mixed/partial unlock state.

Platform achievements are downstream reconciliation only and can never be the authority that a case was solved.

---

# 15. Local save / Cloud boundary

Local storage is the durability authority. Steam/platform service may be absent.

Requirements:
- versioned explicit save schema;
- atomic local writes with validated temp + backup/recovery strategy;
- settings namespace separable from campaign/attempt corruption;
- stale content signature handled by tested migration or by preserving committed campaign facts and restarting only the incompatible current attempt;
- old action records are never replayed against materially changed accepted sets without an explicit migration.

Cloud behavior:
- committed solved/event facts may merge monotonically where schema/profile identity permits;
- current attempt is selected as one whole validated branch, including cursor and redo tail;
- divergent current attempts are never interleaved action-by-action;
- when automatic safe selection cannot be proven, present a human-readable conflict choice;
- raw timestamp alone cannot silently replace a newer meaningful local attempt.

---

# 16. Commercial / progression boundaries

No gameplay economy exists.

Hard NO:
- currency/XP/energy/lives;
- paid hints/Undo/Restart;
- consumable assistance;
- MTX/ads/gacha/battle pass/FOMO/streaks;
- grind gates;
- star/mastery requirements for main progression;
- mandatory account linking;
- speed/timing pressure in base campaign.

Campaign progression follows tutorial dependencies, with bounded post-C06 choice where dependency permits. Optional mastery never gates required content.

Working Steam achievement target remains ~20 low-maintenance deterministic flags. Demo achievements disabled.

Store differentiation must lead with:
**one persistent key -> several locks -> every cut destroys future options**.

`Key cutting` or `be a locksmith` alone is not acceptable differentiation because 2026 competitors already advertise those verbs.

Blind store/trailer gate: target >=70% of target respondents should describe the multi-lock preservation/key-sharing puzzle before burglary, lockpicking, or generic locksmith simulation.

---

# 17. Safety boundary

All locks/key mechanics are fictional abstract puzzle systems.

Do not include:
- real bitting standards;
- real pin heights/keyways/brand dimensions;
- real tolerances;
- impressioning procedure;
- re-keying procedure;
- lockpick/bypass technique;
- real security weaknesses;
- training claims.

Cutaway art must be stylized and non-diagnostic. Game language uses abstract terms such as column, valid band, too shallow, too deep, accepted set.

Any optional post-solve mechanism reveal may show only the fictional accepted-set matrix already governing the puzzle.

---

# 18. Technical baseline

Initial implementation baseline is **Godot 4.7.2-stable, GDScript-first**.

A later stable Godot 4.x may replace it only after regression proves identical:
- domain tests;
- save migration/recovery;
- controller/focus behavior;
- target-device performance.

Architecture must preserve:
1. deterministic headless **Domain Core**;
2. **Presentation/Application** that submits semantic commands and renders returned state/events;
3. **Platform Services** isolated from puzzle authority.

Domain Core must not depend on scene tree, meshes, physics, audio, Steam callbacks, wall-clock timing, or random source.

The 3D/tactile layer is presentation only. If scope pressure occurs, realistic mechanical fidelity is cut before solver/validator, deterministic state, accessibility, controller, save integrity, or content validation.

---

# 19. Empirical gates intentionally left implementation-flexible

These are not missing gameplay design decisions:
- final release price within the frozen review process/band;
- exact final validated case count 28–32;
- final commercial title/store tags;
- exact release localization set;
- optional Reveal Mechanism survival;
- exact animation timings within pacing/readability ceilings;
- runtime softlock budget values while preserving proof-only semantics;
- whether critical-presentation input rejects or queues one command globally;
- how prominently Undo is surfaced after playtesting;
- later stable engine upgrade if regression-safe.

Empirical reopen/kill gates:
- <28 non-isomorphic strong cases survive;
- high-risk witness validation fails;
- C32 cannot support >=2 materially distinct valid traces;
- mature cases routinely collapse to obvious single FILE decisions after exhaustive current-state testing;
- >=25% fresh target players naturally settle into repetitive counterfactual Undo probing and report it as the clearest/best play pattern, requiring a presentation/emphasis review;
- >=30% blind store/capsule respondents primarily read burglary/lockpicking/generic locksmith simulator;
- physical presentation cannot communicate first-blocker/prefix/cut consequence without a dominant numeric matrix;
- solver/validator/art scope displaces accessibility, controller, content validation, or persistence correctness;
- communicating the game would require real locksmith procedure/dimensions.

Empirical gates may tune/reduce/reposition the product; they may not silently invent new core rules.

---

# 20. Final implementation acceptance checklist

A fresh implementation track may call the frozen design faithfully implemented only when all applicable items pass:

## Domain
- accepted sets are sole fit authority;
- FILE is exact +1 and explicit commit;
- TEST is deterministic left-to-right first blocker;
- failure relation is exactly shallow/deep/between branches;
- later columns never leak on failed TEST;
- repeated identical TEST records history but grants no new puzzle/progression state;
- opened-once semantics persist;
- access predicates are visible deterministic functions of opened locks;
- no random/floating fit authority.

## Recovery/history
- unlimited exact Undo/Redo works through entire active case;
- redo tail survives save/load;
- new action after Undo truncates redo;
- D02/C03 require two exact Undos after the proving TEST;
- human-memory rewind leakage is not punished;
- Restart restores exact authored start.

## Solver/content
- V0+ validator pipeline exists;
- proof-only softlock cannot false-warn;
- exhaustive-current-state TEST adversary is included;
- C08–C12, C15–C16, C22–C26, C30–C32 have information-respecting witness traces;
- C32 has >=2 materially distinct valid traces;
- C07+ thought-delta/isomorphism review is performed;
- release contains >=28 strong non-filler cases.

## UX/accessibility
- full keyboard+mouse and controller paths;
- 1280x800 ceiling is usable with zoom/scroll;
- no required fine-motor/freehand/timed interaction;
- first-blocker/accepted-prefix/readability matches domain state;
- numeric aid exposes current key depth only;
- reduced motion/high contrast/localization do not alter information authority;
- inaccessible lock prerequisites are visible;
- equal-vector blank histories remain distinguishable.

## Persistence/platform
- authoritative state commits before animation completion;
- crash injection cannot create partial FILE/TEST/open state;
- pending solved review remains Undoable before durable commit;
- idempotent solve journal survives power loss;
- local save is authority; platform callbacks are downstream;
- corrupt-primary backup recovery exists;
- content-signature mismatch is safe;
- Cloud chooses/merges safe domains without interleaving attempts;
- demo import is idempotent and cannot regress newer full progress.

## Product/commercial/safety
- no gameplay economy/MTX/test cost introduced;
- store leads with one-key/many-lock destructive overlap;
- demo reaches hook by D05 and partition payoff by D06;
- blind positioning gate is measured;
- fictional mechanism remains non-instructional;
- no real locksmith training claims/procedures/data.

---

# 21. Final authority order

For Game #008 after freeze:
1. `GAME8_FINAL_FREEZE.md` — **primary final game-design authority**;
2. `GAME8_PRODUCT_THESIS.md` — product rationale where non-conflicting;
3. `GAME8_MECHANICAL_ARCHITECTURE.md` — detailed mechanical derivation where non-conflicting;
4. `GAME8_CONTENT_ARCHITECTURE.md` — campaign/content detail where non-conflicting;
5. `GAME8_UX_PRESENTATION.md` — UX detail where non-conflicting;
6. `GAME8_COMMERCIAL_MODEL.md` — commercial/progression detail where non-conflicting;
7. `GAME8_TECHNICAL_SPECIFICATION.md` — implementation-spec detail where non-conflicting;
8. `GAME8_PHASE9_REPAIRS.md` and `GAME8_PHASE10_REPAIRS.md` — provenance of repairs already normalized here;
9. `GAME8_WHOLE_GAME_SIMULATION.md` and `GAME8_ADVERSARIAL_REVIEW.md` — validation history;
10. research/tournament files — concept history only, never implementation authority over the winner.

When conflict exists, higher item governs. `GAME8_FINAL_FREEZE.md` intentionally supersedes older wording such as authored-overcut tutorial ambiguity, immediate solve-commit wording, non-persisted redo ambiguity, or the idea that exhaustive free testing itself should fail.

---

# 22. Freeze verdict

All important gameplay decisions required to build the intended product are defined. Remaining unknowns are explicit empirical/release/implementation-tuning gates rather than missing game design.

**DESIGN COMPLETE = YES.**

Migration should proceed to a dedicated repository when one exists. Until verified migration, the complete `GAME8_*` package must remain in the factory as a **frozen NON-ACTIVE safety archive** and must not contaminate Game #009 canon.