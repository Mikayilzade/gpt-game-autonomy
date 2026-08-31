# GAME #010 — FINAL SPECIFICATION FREEZE

Date: 2026-09-01
Status: **DESIGN COMPLETE = YES / MIGRATION PENDING**
Game: **Luggage Carousel Zero** *(working title only; not storefront commitment)*

Authority: this file consolidates all prior active Game #010 authority. Where earlier files conflict, this file plus explicit Phase-10 corrections are authoritative. Earlier Game #010 files remain frozen supporting history/safety archive until successful migration.

---

## 1. Product thesis
PC/Steam-first premium single-player offline deterministic systemic puzzle game.

**Hook:** Swap the labels, not the luggage: shape a moving baggage carousel so every passenger gets the right bag — sometimes by making them wait.

Core fantasy: the player does not move bags directly. Bags circulate one socket per Advance under fixed gantry labels. The player locally swaps adjacent gantry labels to control which label a bag has when it reaches the single pickup. Passenger predicates are public. Strategic depth comes from three coupled questions: which bag should be consumed, when should it reach pickup, and which local label permutation must exist then.

Not canon: airport management, real-time sorting, direct bag manipulation, multiple pickups, hidden preferences, queue impatience, compression, conveyor building, physics handling, roguelike/meta economy, multiplayer, live service, procedural endless, Workshop, new rule families introduced for late game.

Target campaign: 42 planned slots, but **>=36 certified strong trace-distinct cases is the release floor**. Weak filler is rejected. Demo target: seven curated cases.

---

## 2. Canonical state and case limits
A case defines:
- `N` ring sockets, canonical 3..8;
- exactly one fixed pickup socket, normally S0;
- one socket-owned label value per socket, duplicates allowed;
- bag set with immutable `shape` and `mark` values;
- occupancy vector of bag IDs and GAPs, length N;
- ordered passenger queue;
- finite `tick_limit`;
- case-static `swaps_per_tick` K in {0,1,2};
- optional early tutorial-only swappable-socket mask.

Player-visible predicate grammar is exactly:
`1..3 positive equality clauses ANDed together`, at most one clause per dimension from exactly:
- LABEL = value
- BAG_SHAPE = value
- BAG_MARK = value

No OR, NOT, XOR, history, adjacency predicates, numeric comparisons, hidden conditions, scripts or extra trait dimensions.

Authoring envelopes:
- standard campaign: N<=8, K=1, exact certification mandatory;
- K=2 mastery: N<=6 and tick_limit<=8 until implementation benchmark proves safe; base campaign target 2–3 strong K2 cases, maximum 3;
- K=0: short observation/teaching only, N<=5, tick_limit<=4.

---

## 3. Player verbs and adjacency
The only gameplay edit verb is `SWAP` of two **adjacent** gantry labels.

Ring adjacency includes seam S(N-1)<->S0. Long-distance label teleportation is illegal. Equal-value adjacent swaps are mechanically legal no-ops but UI warns and solver omits them.

`SWAP(a,b)` is legal only while PLAYING, with remaining swap bandwidth, with adjacent sockets, and within any tutorial-only mask. It exchanges label values and decrements current-tick swap bandwidth by one.

Labels never move on Advance. Bags/GAPs move; gantry labels stay fixed in socket space.

K=2 means two separately committed adjacent swaps before one Advance. Undo reverses one committed swap at a time.

---

## 4. Exact Advance ordering
While PLAYING, Advance is always legal even if swaps remain unused. This is the canonical wait/non-service action.

On `ADVANCE`:
1. snapshot the committed pre-Advance state for Undo;
2. rotate every occupancy exactly one socket clockwise simultaneously: `O_after[(i+1) mod N] = O_before[i]`;
3. labels remain unchanged;
4. inspect occupancy at pickup S0;
5. if GAP, no passenger is served;
6. if a bag exists and passengers remain, evaluate the **front passenger only** using bag shape/mark + current S0 label;
7. if all displayed clauses match, replace that bag at S0 with GAP and increment passenger index exactly once;
8. if any clause misses, bag remains and queue does not advance;
9. decrement ticks by exactly one;
10. if all passengers are served -> WON;
11. else if ticks == 0 -> BUDGET_FAILED;
12. else reset swaps remaining to case K;
13. run exact feasibility; infeasible -> DEAD, feasible -> PLAYING.

At most one passenger can be served per tick. There is no compression, chained pickup, passenger impatience, collision rule or movement reaction.

Final-tick success beats budget failure.

---

## 5. GAP semantics
Successful pickup replaces the consumed bag with a persistent GAP occupancy. Ring slot count never changes and surviving bags never shift relative to each other.

A GAP:
- moves one socket per Advance like any occupancy;
- guarantees no service when it reaches pickup;
- visually records that a bag was consumed.

A GAP does **not** accelerate, delay, compress, reindex or otherwise phase-shift surviving bags and grants no special action.

Historical F7 is retired as an independent reasoning family. Canonical descriptive tag is `BLANK_RETURN` only.

---

## 6. Preview, DEAD, Undo and Restart
Preview is one-step only. It may show ghost destinations for all occupancies, the next pickup occupancy, current pickup label, and clause-level prospective match/miss for the current front passenger. It may not reveal solver-selected swaps, multi-tick outcomes, optimality, future passenger outcomes or global feasibility.

### DEAD — final corrected timing
Player-facing DEAD occurs **only after a nonterminal Advance**. A SWAP may produce an internally infeasible state but remains PLAYING; no DEAD banner or forward hard-stop is exposed until the player commits an Advance.

After Advance, if exact search proves no winning continuation within remaining budget, state becomes DEAD. DEAD disables forward Swap/Advance and leaves Undo/Restart available.

This rule prevents using the game as a perfect binary solver oracle by probing swaps.

### Undo
Unlimited within a case. One Undo reverses exactly one committed atomic action:
- after Swap: restores exact label vector and swap bandwidth;
- after Advance: restores occupancy, consumed bag/passenger, passenger index, ticks, bandwidth, result and terminal state atomically.

Undo remains available from WON/BUDGET_FAILED/DEAD.

### Restart
Restores exact certified initial state. No penalty, currency or campaign loss.

---

## 7. Content architecture and admission
Planning architecture remains 42 slots: A7 + B8 + C8 + D9 + E10. Shipping count may be lower only down to the >=36 strong-case floor; never pad weak content.

Counted reasoning families:
- F1 Alignment
- F2 Trait binding
- F3 Substitution
- F4 Scarcity preservation
- F5 Intentional miss
- F6 Label staging
- F8 Duplicate-label flexibility
- F9 K2 bandwidth
- F10 Synthesis

F7 is retired; `BLANK_RETURN` is descriptive only.

Coverage floors over accepted campaign pool:
- F1 >=7
- F2 >=6
- F3 >=8
- F4 >=8
- F5 >=6
- F6 >=14
- F8 >=5
- F9 >=2, max 3 base campaign
- F10 >=6

Required proof standards:
- F3: plausible early candidate choices differ in later feasible service family;
- F4: consuming scarce class early fails or materially worsens intended budget;
- F5: all relevant immediate-service lines fail while a delayed line wins;
- F6: forbidding swaps not incident to S0 makes case unsolvable or destroys intended certified family;
- F8: collapsing duplicate-label spatial position to free-choice/multiset changes solvability/minimum ticks/service family;
- F9: identical state/budget at K=1 is unsolvable or loses intended certified family;
- F10: at least three independently proven counted families.

Trace dedupe ignores cosmetic renaming and compares service ticks, served trait-class sequence, pickup-label sequence, gap-at-pickup sequence, effective pre-Advance label states and counterfactual tags.

No accepted case may earn its slot only by larger N, tighter tick budget or wider predicate.

---

## 8. Demo path
Canonical seven-case teaching sequence:
1. fixed gantry label vs moving bag;
2. label + immutable bag trait;
3. required away-from-pickup adjacent staging;
4. preserve the only future-needed bag (canonical tick budget 5);
5. exact intentional miss lesson;
6. persistent GAP/no-compression visual semantics only;
7. exact N5/K1/T7 finale combining scarce-bag preservation, intentional miss and required non-pickup staging.

Demo excludes K2 and dense three-clause mastery. Target 15–25 minutes. No timer/session cap.

---

## 9. UX and presentation
One dominant puzzle screen, no camera pan for N<=8.

Primary hierarchy:
1. moving bag/GAP occupancy;
2. fixed gantry label;
3. pickup socket;
4. front passenger predicate;
5. legal adjacent swap relation;
6. queue/tick/swaps status.

Baseline layout at 1280x800: status top, actions bottom, passenger rail right, carousel center-left. 16:9 preserves anchors. Ultrawide width-caps gameplay composition; extra width is ambience.

Controller-first semantic actions cover all gameplay; no mouse/touchpad fallback is required. Selecting a gantry illuminates exactly the two adjacent legal targets, including seam adjacency.

Text scale presets 100/125/150%. At 150%, front passenger stays fully expanded; queue becomes compact/focusable; clauses never truncate. Color is never the sole carrier: labels use text abbreviation + unique symbol/pattern; shapes/marks use icons/silhouettes + text.

Reduced Motion / Instant presentation preserves all predictive information. Gameplay never requires audio or dexterity/time pressure.

Permanent event log is removed. Keep transient pickup/miss feedback and one `Last result` line.

Normal miss is neutral feedback, not failure language.

Required screens/states: main menu, case select, neutral puzzle, swap select, Preview, Advance transition normal/reduced-motion, match/miss, DEAD, out-of-ticks, win, pause, settings/accessibility/input, passenger detail/queue focus, onboarding callouts.

---

## 10. Campaign progression
A01 -> A02 -> A03 are mandatory sequential tutorial prerequisites.

From A04 onward and in Acts B–E:
- frontier cases unlock sequentially;
- once per act, player may choose `Skip for now` on current blocker;
- this opens the next case, marks exactly one `SKIPPED_OPEN`, and permanently consumes that act's one skip allowance;
- skipped case remains playable forever;
- next act unlocks when all but one cases of current act are basically complete;
- later cleanup does not relock anything.

Ending may be reached with up to one unresolved skipped case per act. `CAMPAIGN_REACHED_ENDING` is distinct from `ALL_CASES_COMPLETE`. Ending UI must not imply 100% completion when unresolved cases remain.

No stars, XP, currency, grind or mastery requirement gates content.

---

## 11. Mastery and achievements
Optional surfaced mastery: **Efficient Route** = win at current solver-certified minimum number of Advances. Minimum target is hidden before first completion and surfaced only after the first intentional-miss lesson so players do not infer that every miss is waste.

Efficient Route never gates progression. Minimum swaps are not a second medal.

Base achievement semantics — 12:
1. ACT_A_COMPLETE
2. ACT_B_COMPLETE
3. ACT_C_COMPLETE
4. ACT_D_COMPLETE
5. ACT_E_COMPLETE
6. CAMPAIGN_REACHED_ENDING
7. ALL_CASES_COMPLETE
8. FIRST_EFFICIENT_ROUTE
9. TEN_EFFICIENT_ROUTES
10. INTENTIONAL_MISS_LESSON
11. K2_MASTERY
12. RETURNED_TO_BLOCKER

No achievement for no-Undo, no-hint, speed input, daily play, accessibility settings or farming.

---

## 12. Commercial model
Premium single purchase. No ads, paid hints, consumable currency, energy, battle pass, gacha, subscription, required account, live-service obligation or FOMO.

Working launch-price hypothesis: US $9.99–12.99; **not frozen storefront price**.

Working title is not final. Storefront/trailer must foreground the mechanic, not generic airport baggage visuals: fixed gantry labels + local adjacent swaps + deliberate non-service.

Not promised: DLC cadence, Workshop, leaderboards, daily challenges, endless mode, multiplayer, mobile/console release, cross-platform account, user level editor, exact launch price.

---

## 13. Technical implementation authority
Preferred direction: Godot 4.7.2 stable + GDScript, PC/Steam-first. Engine is implementation direction, not gameplay canon; later stable engine versions may be used after regression.

Required conceptual layers:
1. immutable Case Data;
2. pure deterministic Rules Core;
3. exact Solver/Certification using same semantics;
4. Presentation/Platform/Persistence adapters.

Presentation objects never own gameplay truth. Animation visualizes a resolved logical transition and never decides pickup outcome.

Core pure operations must exist semantically: validate case, build initial state, legal adjacent swaps, apply swap, preview advance, apply advance, evaluate predicate, exact feasibility, restart.

Action log is deterministic `SWAP(edge)` / `ADVANCE` plus case/content version.

---

## 14. Certification and release content authority
Every shipped campaign case requires a matching certificate with at least:
- certificate schema/version/id;
- case ID;
- normalized case content hash;
- rules semantics version;
- solver version;
- content manifest version;
- solvable=true;
- minimum ticks;
- minimum effective swaps at minimum ticks when computed;
- viable opening metric/set/hash;
- required family-counterfactual results;
- optional exact-feasibility artifact hash.

Release packaging fails on mismatched case hash, rules semantics or required artifact hash. Heuristics may prune search but may never directly declare DEAD.

Runtime exact DEAD backend may be precomputed lookup or exact memoized search. Target <=100 ms p95 on Steam-Deck-class target for shipped cases; otherwise ship precomputed support or simplify/reject case.

Content manifest identifies ordered base campaign, demo path, exact case/certificate hashes, rules semantics version and schema requirements.

---

## 15. Persistence, save migration and cloud/demo merge
Profile save is versioned, atomic temp->replace, with previous-good backup where practical.

Profile preserves at minimum:
- save schema/content manifest versions;
- completed case IDs;
- per-act skip state and skipped-open case;
- campaign ending state;
- tutorial acknowledgements;
- demo import version;
- achievement reconciliation history;
- global settings/accessibility/input;
- provenance-bearing mastery records.

Active-case save stores case/manifest identity, full committed PlayState and enough snapshot/action history for continued stepwise Undo. Saves occur only at committed boundaries, never mid-animation.

Incompatible active puzzle state after content update is discarded/restarted with one-time notice while profile progress survives.

Save migrations are explicit chained `vN -> vN+1`, deterministic and tested. Unknown future schema is preserved/fails safe, never destructively reinterpreted.

Cloud/local merging validates candidates; timestamp alone is not authority. Completion merges monotonically; non-mergeable progression is recomputed from canonical source fields.

Demo import:
- stable case IDs;
- completion set union;
- compatible best mastery record chosen by minimum ticks;
- settings import only when full profile does not already supersede;
- never import act frontier or skip flags;
- recompute progression under full-game rules;
- idempotent; no duplicate achievement grant.

---

## 16. Mastery provenance — corrected sole truth
Do **not** store integer-only `best_ticks_by_case` as the authoritative mastery truth.

Canonical logical record per case must recover:
- `ticks`;
- `case_content_hash`;
- `rules_semantics_version`;
- certificate/version identifier when useful.

A record qualifies for current Efficient Route only if case ID matches and its content/rules provenance is compatible with the current certified case (normally same content hash and compatible rules semantics, unless an explicit future equivalence mapping says otherwise) and its ticks meet current minimum.

Basic completion remains monotonic for a stable case ID across compatible product updates. Incompatible historical mastery may be retained as history but does not light current mastery until replay.

Legacy integer-only records may gain provenance only if historical manifest deterministically maps them; otherwise mark unverified and exclude from current Efficient Route while preserving completion.

Already granted platform achievements are never revoked.

---

## 17. Acceptance-test matrix
Implementation cannot claim frozen-design compliance until these pass.

### Rules / mechanics
- exact ring adjacency including seam;
- unrestricted long-distance swap rejected;
- equal-value swap no-op handling;
- K0/K1/K2 bandwidth and reset;
- every occupancy rotates exactly one clockwise;
- labels remain fixed on Advance;
- GAP pass and pickup-created GAP persistence;
- one front passenger max per tick;
- predicate grammar/ordering and duplicate-dimension rejection;
- final-tick win before budget failure;
- Advance with unused swaps;
- no compression.

### DEAD / Preview / Undo
- Preview is one-step and non-oracular;
- Swap never raises player-facing DEAD;
- first/second K2 swap never raises player-facing DEAD;
- exact DEAD may arise only after nonterminal Advance;
- DEAD after miss and after successful nonfinal pickup both restore correctly with Undo;
- terminal Undo works from WON/BUDGET_FAILED/DEAD;
- repeated Undo restores one atomic committed action per press.

### Regression content
Automate Phase-4 M1–M12 where still non-conflicting, adjacency correction R1–R8, Demo-03 staging proof, Demo-05 intentional-miss proof and exact Demo-07 finale.

Any older test expecting DEAD immediately after SWAP is explicitly removed/superseded.

### Content/certification
- every release case validates schema/invariants;
- matching certificate/hash required;
- family tags pass exact counterfactuals;
- F7 cannot count as family;
- >=36 strong non-duplicate cases before release claim;
- K2 cases obey envelope unless separately benchmarked/amended before release.

### UX/accessibility
- controller-only demo completion;
- 1280x800 N3..8 layout;
- seam target visibly adjacent;
- 150% text keeps front predicate complete;
- reduced motion preserves Preview/Advance information;
- color-independent labels and match/miss;
- queue fully inspectable without state cost;
- miss feedback neutral;
- no permanent event log dependency.

### Progression/commercial
- mandatory A01–A03;
- once-per-act skip exact behavior;
- five unresolved blockers can coexist at ending;
- later cleanup produces ALL_CASES_COMPLETE only at true full completion;
- Efficient Route hidden before first solve and does not gate;
- all 12 achievements trigger idempotently under their frozen semantics;
- no demo achievements before full-game reconciliation.

### Persistence/update
- atomic save + previous-good recovery;
- corrupted active case cannot erase profile;
- corrupted newest profile falls back safely;
- unknown future schema preserved/fails safe;
- active-case manifest mismatch restarts only active case;
- repeated demo import idempotent;
- cloud/local monotonic merge;
- provenance-compatible mastery record merging;
- incompatible old record does not qualify for current Efficient Route;
- basic completion preserved for stable case ID;
- release build fails on certificate/content mismatch.

### Performance / packaging
- target 60 fps at 1280x800 Steam-Deck-class hardware;
- exact DEAD verdict <=100 ms p95 or precomputed support used;
- release package has no missing mandatory case/certificate artifact;
- offline gameplay/progression works without Steam API.

---

## 18. Empirical gates vs implementation-flexible details
### Empirical gates — must be tested, not invented around
- >=36 strong non-duplicate certified cases survive population;
- first-time players understand bags move / labels stay by case 2;
- adjacent seam is understood without repeated explanation;
- intentional miss feels clever rather than arbitrary;
- N=8 remains readable at 1280x800/controller distance;
- 150% text and reduced motion preserve all essential information;
- controller-only demo path is comfortable;
- exact runtime DEAD performance meets target or precompute is used;
- storefront name/visual differentiation is sufficient;
- final price follows actual playtime/polish/conversion evidence.

Failure of an empirical gate may justify simplifying/rejecting content or changing presentation/branding. It may **not silently change frozen mechanics** without reopening design authority.

### Implementation-flexible
- exact art style within stylized 2D/2.5D readability contract;
- animation timings inside frozen causal ordering;
- solver algorithm choice if exact semantics match;
- precompute vs runtime DEAD backend per case;
- serialization syntax/file organization;
- exact stable Godot 4.x version after regression;
- final localization list;
- audio assets;
- final working-title replacement and exact price.

No gameplay rule remains undefined.

---

## 19. Final contradiction scan
Resolved supersessions:
- unrestricted swap -> **adjacent-only swap**;
- GAP as phase-shifter/F7 strategy family -> **no compression, BLANK_RETURN only**;
- player-facing DEAD after Swap -> **DEAD only after nonterminal Advance**;
- integer-only best ticks -> **provenance-bearing mastery record**;
- Demo-04 ticks 4 -> **canonical 5**;
- permanent event log -> **removed**;
- vague blocker skip -> **explicit once-per-act Skip for now**.

No remaining active authority requires a fresh implementation session to invent an important mechanic, progression rule, content admission rule, UX state, commercial boundary, persistence semantic or solver truth condition.

**DESIGN COMPLETE = YES.**

---

## 20. Migration state
Preferred dedicated repository: `Mikayilzade/luggage-carousel-zero` *(working repo slug only)*.

Repository check on 2026-09-01 returned **not found**, and this factory runtime has no repository-creation capability. Therefore migration is **PENDING / NON-BLOCKING**.

All `GAME10_*` files, including this final freeze, must remain in `gpt-game-autonomy` as a frozen **NON-ACTIVE safety archive** until a dedicated repository exists, migration is verified, and only then may Game #010 safety files be removed.

Factory continuity requires immediate advance to Game #011. Game #010 must never remain active canon merely because migration is pending.
