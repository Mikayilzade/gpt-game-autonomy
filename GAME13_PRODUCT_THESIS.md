# GAME #013 — PHASE 3 PRODUCT THESIS LOCK

Date: 2026-09-02
Status: PHASE 3 COMPLETE — PRODUCT THESIS LOCKED
Selected concept: **SEAL BREAK** (working title)

## One-sentence hook
Place tamper seals across a compact compartmented object, then choose or reconstruct a bounded opening history so the irreversible pattern of torn and surviving seals matches an evidence record.

## Product identity
PC/Steam-first, single-player, deterministic authored logic puzzle. The fantasy is not running security or doing forensic paperwork; it is physically arranging witnesses before a destructive sequence, then reading what the irreversible evidence proves about what happened and in what order.

The key differentiator is **destructive temporal evidence**. Seals are not keys, locks, hit points, or decoration. Each seal is a visible witness whose tear time is determined by which compartment opening first crosses one of its listed seams. Multiple overlapping witnesses let the player infer causality, survivorship, precedence and omitted events.

## Target player
Primary:
- players who like deduction-heavy compact puzzle games;
- players comfortable reasoning from visible constraints rather than executing dexterity;
- players who value authored cases, deterministic rules, undo/reset and strong causal feedback.

Secondary:
- Steam Deck/controller puzzle players;
- players attracted by tactile workbench/object metaphors but not by simulation complexity.

Not targeted:
- action/physics players expecting freeform destruction;
- mystery players expecting long narrative investigation;
- sandbox players expecting arbitrary cabinet construction or freeform seal placement.

## Lead platform and interaction stance
Lead: PC/Steam, designed from the start for controller and handheld readability.

Input must support:
- socket/compartment navigation without precise pointer dependence;
- finite seal placement/removal;
- bounded opening-order arrangement;
- evidence inspection;
- commit, replay, undo/reset.

Mouse may be supported, but core UX must not require drag precision.

## Genre framing
Premium compact logic puzzle / deduction puzzle with tactile 2D or restrained 2.5D presentation.

Avoid marketing it as:
- detective narrative;
- realistic security simulation;
- escape room;
- physics puzzle;
- automation game;
- paperwork/bureaucracy game.

## Core fantasy
'I can place or read physical witnesses so precisely that the final tear pattern proves exactly what sequence of openings could have happened.'

The satisfying moment is the destructive reveal: a compartment opens, several specific seals tear or survive, and the evidence timeline confirms or contradicts the player's predicted history.

## Core loop
1. Inspect the cabinet/object, seal sockets, crossing sets and target evidence.
2. Place the allowed seals and/or arrange the bounded opening history, depending on case family.
3. Use only non-oracular preview information: visible geometry, seal crossing sets, socket legality and already-fixed constraints.
4. Commit the opening sequence.
5. Watch deterministic checkpoint-by-checkpoint tears and survivals.
6. Compare actual evidence with target.
7. Undo/reset/revise until the case is solved.
8. Advance through increasingly coupled witness logic.

## Session structure
- Individual authored cases: roughly 3–20 minutes early/midgame, longer for late capstones.
- Typical session: 15–60 minutes, several cases.
- Campaign target: 30 certified cases.
- Commercial/content floor: 24 cases.
- Cases 31–36 are optional only if playtest/certification proves additional same-vocabulary deduction diversity rather than denser bookkeeping.

## Campaign reasoning arc
The campaign should escalate through reasoning classes, not by adding many mechanics:
1. direct cause;
2. first-crossed semantics;
3. overlapping witness intersection;
4. paired witness discrimination;
5. survivorship/complement reasoning;
6. delayed-break lower bounds and exclusions;
7. inverse witness placement under fixed history;
8. reconstruct history from fixed witnesses;
9. bounded coupled placement + history choice.

Late cases must combine at least three reasoning classes.

## Core verbs
- inspect;
- place seal;
- remove/move seal before commit;
- arrange/select bounded opening order when allowed;
- commit;
- inspect/replay evidence;
- undo/reset.

No freeform drawing, cutting, tearing or physics manipulation.

## Frozen mechanical identity at thesis level
A case contains:
- a finite compartment set;
- a finite set of legal seal sockets;
- for each socket, a visible crossing set of compartments/seams whose opening would tear that seal;
- a seal budget or fixed installed set;
- a bounded opening history or finite history choices;
- one or more evidence checkpoints;
- target predicates over seal identity, exact break checkpoint, survival-through-checkpoint, final intact/broken state, and possibly opened/unopened compartment identity when explicitly given.

Authoritative tear rule:
- an intact installed seal breaks irreversibly at the first checkpoint whose opened compartment crosses that seal;
- otherwise it remains intact;
- no randomness, durability, partial damage or hidden material properties.

Exact state ordering, equivalence rules, commit semantics and edge cases belong to Phase 4.

## Demo thesis
A demo must reveal the real game, not stop at tutorials. Six-case target:
1. direct tear cause;
2. one seal spanning multiple causes;
3. overlapping witnesses with divergent break times;
4. survivorship + one omitted compartment;
5. choose seal witnesses for a fixed opening sequence;
6. coupled seal subset + bounded history reconstruction capstone.

If case 6 cannot be made readable without solver-like live feedback, that is a design warning to repair in later phases.

## Presentation thesis
Visual language: compact cabinet, case, parcel, evidence box or similarly neutral compartmented object with clearly drawn seams and finite seal sockets. Tamper strips should be physically obvious and have readable identities via pattern/icon/label, never color alone.

Desired trailer beat:
- player places three seals;
- reorders four opening cards;
- presses COMMIT;
- doors open in sequence;
- two seals snap at different checkpoints while one survives;
- evidence card resolves in one glance.

Avoid cluttered crime-board aesthetics, text-heavy reports, realistic legal branding or gore/damage spectacle.

## Scope ceiling
Required:
- single-player offline baseline;
- one core finite witness system;
- 24–30 authored certified cases;
- compact progression;
- controller/keyboard/mouse abstraction;
- deterministic replayable resolution;
- robust undo/reset/recovery;
- accessibility-safe seal identities;
- data-driven case definition and certifier contract later.

Explicitly out of scope:
- multiplayer;
- live service;
- procedural campaign promise;
- random tear physics;
- freeform cabinet construction;
- seal crafting/equipment economy;
- open-world or walkable investigation space;
- NPC simulation;
- dialogue-heavy mystery campaign as core value;
- timers/leaderboards as required play;
- roguelite/deckbuilder wrapper;
- monetized hints, ads, MTX;
- arbitrary seal durability, strength or colors as mechanical alphabet;
- user-generated level editor for v1 unless implementation cost later proves trivial and cannot delay core release.

## Anti-repetition gates carried into design
1. Final-state-only broken/intact cases are tutorial-only.
2. Every substantive case has at least two temporal checkpoints.
3. Midgame+ cases combine at least two deduction classes; late cases at least three.
4. Larger compartment/seal counts do not count as new content families.
5. New predicate types are rejected unless they create a new deduction interaction, not just more bookkeeping.
6. Live UI may explain what a seal crosses and what has already happened, but must not score hypothetical future orders or reveal a correct next action.

## Why this concept won the portfolio slot
Compared with Carbon Copy and Blind Staple, Seal Break retains an equally legible physical hook while avoiding the portfolio's existing flat-layer/source-transform lane represented by Game #009. Its advanced reasoning remains centered on irreversible temporal witness evidence rather than layer permutation or depth maps.

## Phase 3 verdict
**PRODUCT THESIS LOCKED.**

Working title remains **SEAL BREAK** and is not a final commercial naming decision.

Next phase: Phase 4 Mechanical Architecture. It must fully specify the exact case/state model, seal/socket legality, crossing semantics, opening-history representation, checkpoint resolution order, evidence predicates, equivalence/uniqueness, player preview boundaries, win/fail semantics, progression-facing difficulty knobs and certifiability constraints.