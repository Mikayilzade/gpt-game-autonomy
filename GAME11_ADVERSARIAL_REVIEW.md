# GAME #011 — MISSING STEP — PHASE 10 ADVERSARIAL REVIEW

Date: 2026-09-01
Status: **PHASE 10 COMPLETE**
Authority: `START_HERE.md` -> `STATUS.md` -> `GAME_INDEX.md` -> active Game #011 authority through `GAME11_WHOLE_GAME_SIMULATION.md` -> this file for adversarial rulings.

Purpose: attack the frozen design cross-disciplinarily without adding features. Any repair below preserves the four-opcode / one-workpiece / deletion-before-RUN identity.

## 1. Core-fun / repetition attack
The six frozen challenge families remain mechanically distinct only if campaign curation prevents them collapsing into repeated “compare periods until tuple matches.” Shipping content therefore needs **perceptual-family quotas** in addition to solver tags.

Required release mix at the 36-case floor:
- F1 recurrence-forward cases: >=5;
- F2 clamp-window cases: >=5;
- F3 orientation/parity materially decisive: >=4;
- F4 positional-duplicate cases: >=4;
- F5 same-tick A->D cases: >=4;
- F6 two-delete coupled cases: >=7;
- >=10 cases must materially combine >=2 families;
- no run of 4 adjacent campaign cases may share the same dominant solution insight + same target-shape class.

Human curation rejects a certified case if a tester can explain it only as “same thing, bigger numbers.”

## 2. Brute-force dominance attack
Brute force cannot be banned without harming the experimentation thesis. It must instead become unattractive because reasoning is faster and clearer.

Frozen gates:
- tutorials may be brute-forceable; no penalty;
- ordinary late single-delete cases target 6–12 legal edits but should expose a discriminating hypothesis before all candidates are RUN;
- mastery ramps 9 -> roughly 16 -> 20–30 -> max 36 pairs; do not jump from 9 directly to 36;
- no retry cost, cooldown, hidden state or attempt counter may be introduced.

**Empirical gate BF-1:** in moderated tests of Act V/VI representative cases, median successful player should use fewer than 50% of legal candidate RUNs before solving. For 36-pair mastery, median should be <=12 committed RUNs. If not, reject/replace the case; do not add punishment.

**Empirical gate BF-2:** at least 70% of successful testers must be able to state a causal reason for their final deletion(s) beyond “I tried the remaining options.”

## 3. Preview attack: oracle vs clerical burden
The structural DTO separation remains correct: Preview has schedule/anchors/clamp-active markers only, no simulated workpiece future or target result.

Opposite failure is also real: hiding all workpiece consequences may force clerical trace simulation over long horizons.

Frozen compromise:
- Preview continues to show the entire opcode schedule to horizon and CLAMP-active-at-start markers;
- RUN/replay may be paused, stepped, scrubbed and accelerated after commit;
- result/replay may expose the actual committed trace in full;
- planning still never shows predicted lane/orientation/stamp/blocked outcomes.

No solver heatmap, future-state ghost or candidate comparison is added.

## 4. Late horizon / deceptive-prefix fatigue
A mathematically valid 18–24 tick case can be poor if the insight occurs early but verification requires counting to the horizon.

Release curation gates:
- standard target horizon remains 4–18; >18 is exceptional mastery only;
- no launch case >24;
- deceptive prefix >6 ticks is presumptively reject unless the later divergence is visually obvious from recurrence markers rather than manual state bookkeeping;
- if two closest candidates are indistinguishable in schedule-level reasoning for >50% of horizon and differ mainly by manual PUSH/TURN/STAMP accounting, reject one of the case parameters.

**Empirical gate TRACE-1:** after one failed RUN, >=75% of testers should correctly identify the decisive divergence region within two replay/scrub attempts.

**Empirical gate TRACE-2:** median solve time for non-mastery late cases should remain <=8 minutes after the relevant mechanics are learned; repeated >12-minute clerical solves trigger case replacement/reduction, not new hints/mechanics.

## 5. Content exhaustion / near-duplicate attack
The 42 target is subordinate to quality floor 36.

Freeze additional content admission rules:
- automatic similarity threshold from Phase 5 remains a filter, not sole authority;
- campaign neighbors cannot share both successful post-edit period vector and dominant trap;
- across final campaign, no exact successful trace signature may appear twice after harmless token-ID renaming;
- same target tuple/shape may repeat only when different family interaction is materially necessary;
- generated candidates are disposable; the release set is curated and recertified after final ordering.

**Empirical gate CONTENT-1:** blind side-by-side tester presented two nonadjacent cases should distinguish the intended reasoning lesson in >=80% of sampled pairs from the same act. Failure indicates perceptual duplication.

If fewer than 42 survive, ship 36–41. Never pad.

## 6. Scope-creep attack
Explicitly rejected for launch:
- fifth opcode;
- second workpiece;
- insertion/reordering/token movement;
- free programming / variables / conditionals;
- >4 tracks;
- >6 original tokens per track;
- >2 total deletions or two on same track;
- economy/currency/stars/XP;
- narrative branches or large bespoke story volume;
- procedural daily mode / leaderboard / Workshop requirement;
- physics truth or random failure.

These are not “future TODOs” in the launch spec. Any sequel/expansion may revisit them only as a new design decision.

## 7. Controller / 1280x800 / 150% UX attack
Hostile layout checks remain mandatory:
- 4 tracks x 6 tokens + target + timeline + primary controls must fit without horizontal puzzle-state scrolling at 1280x800;
- at 150% text, mechanically essential target clauses, selected deletion slots, track IDs, active tick and primary actions remain visible;
- two-delete selection must expose which track slot is still missing without relying on color;
- duplicate opcode tokens require stable positional focus narration;
- replay step/scrub must be reachable controller-only;
- reduced-motion mode must preserve loop-close, active tick, CLAMP-next-tick and A->D order as discrete cues.

**Empirical gate UX-1:** controller-only completion of an Act-VI representative case at 1280x800/150% text with zero pointer fallback and zero mechanically required clipped text.

## 8. Persistence/cloud attack
Frozen precedence/rulings:
1. local validated save generation is gameplay authority;
2. Steam Cloud is transport/synchronization only;
3. corrupt primary never causes default overwrite before backup check;
4. future-version refusal blocks writers/cloud push for that profile;
5. newly solved completion must be durably saved before ordinary NEXT CASE navigation implies success committed;
6. demo import unions canonical IDs and obeys per-setting provenance;
7. achievement reconciliation is idempotent and never campaign authority.

Cloud conflict implementation gate: when local and cloud generations differ, integration must preserve the newer valid semantic progress set or surface an explicit recoverable conflict; it may not silently replace a newer valid local generation with an older cloud file merely due timestamp quirks.

## 9. Certificate / manifest / rules drift attack
Authority must fail closed.

Release checks:
- every manifest case resolves to exactly one current canonical case payload and matching certificate;
- case hash + rules version + cert format/core semantic identifier match;
- UNIQUE-designated cases remain UNIQUE;
- mandatory onboarding IDs exist;
- act quota <= number of present cases and designated mastery IDs exist;
- demo IDs are a subset of canonical launch IDs;
- achievement case references resolve;
- content reorder cannot alter stable case IDs;
- semantic Rules Core change increments rules version and recertifies affected content; never migrate certificates across changed semantics.

## 10. Implementation ambiguity scan
No implementation session may invent gameplay answers for:
- phase-anchor deletion behavior;
- A->D ordering;
- CLAMP duration;
- PUSH blocked direction;
- STAMP no-op behavior;
- final-tick semantics;
- edit budget;
- target grammar;
- Preview forbidden data;
- failure/Reset semantics;
- progression quotas/skips;
- save/import authority.

Implementation-flexible areas are presentation skin, exact panel proportions, animation durations, sound assets, shader/art style, stable hash algorithm choice before certification, and engine patch/minor upgrade after regression equivalence.

## 11. Remaining empirical gates — explicit pass/fail metrics
- **BF-1:** median candidate RUN usage <50%; max-36 mastery median <=12 committed RUNs.
- **BF-2:** >=70% successful testers articulate causal final-choice reasoning.
- **TRACE-1:** >=75% locate decisive divergence within two replay/scrub attempts after a failure.
- **TRACE-2:** learned non-mastery late cases median <=8 min; recurring >12 min is rejection signal.
- **CONTENT-1:** >=80% sampled same-act pair comparisons are perceived as different reasoning lessons.
- **UX-1:** controller-only 1280x800 + 150% representative Act-VI case with no pointer fallback/clipped mechanic truth.
- **DEMO-1:** at least 70% of first-time demo testers can explain “deletion shortens the loop and changes later alignment” by demo end.
- **PRICE-1:** final price rechecked near launch against certified count, playtime, polish, regional pricing and contemporaneous puzzle comps; working $9.99–12.99 remains non-final.

These are prototype/playtest/business gates. Failure means revise/reorder/reject content or presentation, not invent new gameplay mechanics by default.

## 12. Phase-10 verdict
- repetition: PASS with mix/adjacency gates;
- brute force: PASS with measurable curation gates;
- Preview: PASS; no oracle expansion;
- late-horizon clerical burden: PASS with hard rejection metrics;
- content exhaustion: PASS; 36 floor beats padded 42;
- scope: PASS; expansion explicitly rejected;
- UX/accessibility: PASS with hostile device gate;
- persistence/cloud: PASS with precedence frozen;
- certificates/manifests: PASS fail-closed;
- implementation ambiguity: no material gameplay ambiguity remains.

**PHASE 10 COMPLETE.**

Proceed directly to Phase 11 Specification Freeze.