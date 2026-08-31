# GAME #011 — MISSING STEP — PHASE 3 PRODUCT THESIS

Date: 2026-09-01
Status: **PHASE 3 PRODUCT THESIS LOCKED**
Working title: **Missing Step** — internal only; commercial title not cleared.
Authority: `START_HERE.md` -> `STATUS.md` -> `GAME_INDEX.md` -> Game #011 Phase-2 history -> this file for product identity.

## One-sentence hook
**Cross out one step in a repeating machine program; because the loop becomes shorter, every later operation re-phases against the other loops, turning one tiny deletion into a completely different machine rhythm.**

## Product identity
A compact single-player deterministic puzzle game about **subtractive programming**. The player is not building a factory, writing code, rewinding time, or routing belts. Each puzzle presents a small already-running machine whose visible cyclic instruction tracks almost work. The player removes a very small number of existing operations before committing to RUN. Removing a token changes both what the machine does and, crucially, **when all remaining operations recur**.

The central pleasure is the moment a seemingly wrong deletion makes several loops drift into the right alignment.

## Target player
Primary:
- players who enjoy compact deterministic logic puzzles;
- players who like understanding a system, predicting consequences, then committing;
- players comfortable with Into-the-Breach-style explainability but not necessarily programming syntax;
- Steam/Steam Deck users seeking short sessions and controller-friendly puzzles.

Not targeted as:
- factory-builder audience expecting free construction;
- coding-game audience expecting functions/variables/loops authored from scratch;
- reflex/rhythm audience;
- narrative-heavy adventure audience.

## Platform / input thesis
- PC / Steam first.
- Steam Deck / 1280x800 is a first-class layout target, not a post-launch port concern.
- Mouse/keyboard and full controller paths.
- Single-player offline baseline.
- No networking requirement.

## Genre framing
Store-facing framing should be approximately **deterministic machine-sequencing puzzle / subtractive programming puzzle**, not “factory automation.” Factory/machine imagery is presentation; deletion-induced re-phasing is the genre hook.

## Core fantasy
“I can fix an impossible machine by removing exactly the right thing.”

The fantasy is elegant sabotage/repair: fewer instructions produce a smarter rhythm.

## Core loop
1. **READ** — inspect 1–4 short cyclic tracks, current phases, workpiece state, horizon and exact target.
2. **HYPOTHESIZE** — identify which operation(s) might be removed and how shortening a loop changes recurrence.
3. **DELETE** — cross out the allowed token(s).
4. **PREVIEW** — inspect the resulting shortened loops and shared tick alignment; preview explains consequences but does not choose for the player.
5. **RUN** — watch deterministic execution with strong causal animation.
6. **EXPLAIN** — success or failure points to exact target mismatch / blocked event.
7. **REVISE** — instant reset/undo-to-planning and try another deletion.

## Session structure
- Individual puzzle: roughly 1–6 minutes after onboarding; mastery cases may run longer.
- Natural session: 10–25 minutes / several cases.
- Campaign should support stop/resume between cases with no punishment.
- No daily obligation, energy timer or live-service cadence.

## The differentiator
The player edits **period**, not merely behavior. Deleting `TURN` does not only mean “TURN no longer happens”; a 4-step loop becomes a 3-step loop, so PUSH/STAMP recur on different global ticks relative to other tracks. This must remain visually and mechanically central throughout the campaign.

If a proposed feature would still be equally interesting if each track ran only once, it is probably not serving the game's identity.

## Frozen mechanic vocabulary ceiling for Phase 4 exploration
The selected concept enters mechanical architecture with the tournament vocabulary as a hard baseline:
- cyclic tracks;
- global deterministic ticks;
- `PUSH`, `TURN`, `STAMP`, `CLAMP`;
- deletion before RUN;
- deletion shortens the loop;
- finite horizon;
- lane/orientation/stamp/blocked-event targets;
- explicit current phase;
- `CLAMP` telegraphs a next-tick lane-1 block.

Phase 4 may refine exact semantics and data representation, but it must **not casually add** insertion, token movement, speed controls, rewind, branching instructions, variables, conditionals, free code editing, conveyor construction, physics simulation, hidden randomness or a large operation catalog. Any expansion requires proof that the frozen vocabulary cannot sustain the target campaign and must be treated as a scope-risk decision, not assumed progression.

## Scope ceiling
Target product is a focused premium indie puzzle game, not an automation sandbox.

Ceilings entering Phase 4:
- <=4 simultaneous tracks on standard campaign screens;
- <=6 visible tokens per track before deletion;
- <=2 authorized deletions in normal mastery content, usually one deletion total and only occasionally one-per-two-tracks;
- one primary workpiece model unless Phase 4 proves a second piece is essential and still readable;
- no more than the four selected operation families without an explicit adversarial gate;
- deterministic authored/data-driven cases with exhaustive solver certification;
- low-to-moderate bespoke art burden; machine motion/state change should carry presentation value.

## Difficulty thesis
Difficulty comes from recombination of:
- post-delete loop length;
- relative periods / recurrence;
- visible starting phase;
- interaction between PUSH movement and next-tick CLAMP cadence;
- STAMP timing at lane 1;
- TURN timing and final orientation;
- exact finite horizon;
- one deletion vs coupled two-track deletions;
- target conjunctions.

Difficulty must **not** come from hidden timing, tiny unreadable icons, long arithmetic, excessive track count, memorizing exception rules, or slow replay.

## Failure / fairness thesis
Every failure must be explainable from public deterministic state. After RUN, the player can identify the first decisive mismatch: blocked push, wrong lane, wrong orientation, wrong stamp count, or horizon ending before target. The game should encourage experimentation; reset is fast and failure carries no resource loss.

Preview is a teaching and accessibility tool, not an oracle. It may show the deterministic schedule resulting from the player's currently selected deletion, because manually transcribing modular alignment is clerical work. It must not rank deletions, reveal “correct” tokens, or silently search alternatives.

## Content thesis
Authored cases should be **solver-certified, not trusted from prose intuition**. Round B already exposed apparently plausible unsatisfiable/non-unique cases. Phase 5 therefore needs a case schema and exact validator that records legal edit sets, solution count, traces and useful difficulty signatures.

Campaign value should come from trace-distinct interactions under the same operation vocabulary, not from introducing a new gimmick every few levels.

## Demo thesis
A demo should reach the complete product identity quickly:
1. deletion changes behavior;
2. deletion changes recurrence;
3. recurrence against a second loop matters;
4. a deceptive case proves “delete the bad-looking step” is not the strategy;
5. ideally end on a compact coupled-period case or teaser of two-track deletion.

A silent 10–20 second clip should be able to show: **cross out token -> loop visibly contracts -> rows drift into a new alignment -> machine succeeds**.

## Presentation thesis
Readable mechanical diorama + timeline, not code editor.
- Tokens are large physical/graphic actions, not source-code text.
- Shared tick columns make re-phasing visible.
- Deletion has a satisfying crossed-out/removal animation and the loop physically closes the gap.
- During RUN, the active column pulses and machine motion mirrors the token.
- Color is redundant with shape/icon/text.
- Reduced-motion mode preserves state transitions without relying on animation timing.

## Commercial boundary entering later research
Premium one-time purchase is the default hypothesis. Exact price, demo length, achievements and commercial title remain Phase 7 decisions requiring fresh market research. No ads, consumable hints, battle pass, gacha, paid lives or grind economy belong in the thesis.

## Explicit out of scope
- production implementation in this factory;
- free-form factory building;
- belt routing/resource extraction;
- programming language syntax;
- random machine failures;
- real-time dexterity timing;
- multiplayer/co-op dependency;
- physics-based collision as puzzle truth;
- narrative branching as core content volume;
- user-generated level editor as launch requirement;
- live service.

## Phase-3 acceptance check
- One-sentence hook: PASS.
- Target player/platform: PASS.
- Core fantasy: PASS.
- Core loop: PASS.
- Differentiator: PASS.
- Session shape: PASS.
- Scope ceiling: PASS.
- Demo thesis: PASS.
- Portfolio separation #001–#010: PASS.
- Important identity ambiguity remaining before mechanics: NONE.

**PHASE 3 COMPLETE.**

## NEXT DESIGN QUESTION
Phase 4 must turn the thesis into a complete mechanical contract: exact tick/order semantics, deletion eligibility, track/workpiece state, target grammar, preview boundary, win/fail/dead-state rules, difficulty knobs, solver/certificate model, case-generation constraints, and adversarial traces. It must prove that the four-operation vocabulary can support a full campaign without quietly becoming a programming mechanic zoo.
