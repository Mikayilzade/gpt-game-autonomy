# GAME #008 — PRODUCT THESIS

Last updated: 2026-08-30
Phase: **3 — Product Thesis Lock**
Selected concept: **G8C02 Locksmith's Margin**
Working title: **Locksmith's Margin**
Production implementation started: **NO**

## Product identity
**Target player:** players who enjoy compact systemic puzzle games, tactile mechanical objects, deduction through visible causality, and irreversible decisions that can be understood rather than guessed. No prior locksmith knowledge required.

**Platform:** PC/Steam-first premium single-player, keyboard+mouse and controller from design baseline; Steam Deck target. Offline core game.

**Genre framing:** tactile systemic puzzle / mechanical deduction game. Not a realistic locksmith simulator, burglary game, lockpicking dexterity game, roguelite, management sim or crafting economy.

**One-sentence hook:**
> File a few persistent keys to open many different locks — every cut can gain one fit while permanently destroying another, and failed tests are information you may need before committing.

**Core fantasy:** become a careful bench locksmith who understands not just how to make a key fit one cylinder, but how much metal and compatibility to preserve across a whole job.

## Core loop
1. inspect the current finite job: locks, blanks, known access/order constraints;
2. choose a key and lock to test where allowed;
3. physically insert/turn it and read deterministic pin/impression feedback;
4. decide whether the information justifies an irreversible one-step file cut, or preserve the key's current margin;
5. retest this or another lock;
6. partition locks across the few persistent keys and exploit overlapping accepted depth sets;
7. complete the job when every required lock has been opened under its case constraints;
8. review the resulting scarred keys and causal solution, then move to the next authored case.

The interesting decision is frequently **not to cut yet**.

## Session structure
- authored self-contained cases, generally 5–15 minutes once rules are learned;
- early tutorial cases shorter;
- mature cases can reach ~20–25 minutes but should not require repetitive filing busywork;
- campaign target roughly 28–34 strong cases, final count decided by content validation rather than quota;
- demo target 5–6 cases / ~20–30 minutes ending on first clear multi-lock compatibility `aha`;
- immediate restart and bounded undo policy to be specified in Phase 4; irreversible means within committed puzzle state, not punishment through lost real-world time.

## Differentiator
The strategic object is **one destructively edited physical key that remains useful across several locks**. Partial/imperfect compatibility is valuable. A failed insertion is deterministic information. This distinguishes the game from lockpicking, key-copying simulation, generic crafting and abstract resource allocation.

## Scope ceiling
Core campaign authority is deliberately discrete:
- normally 4–6 cut columns per key;
- normally 4–6 depth steps;
- finite accepted depth sets/intervals per lock column;
- one-step filing only;
- master behavior represented only as multiple accepted depths/intervals;
- wear represented only as widened accepted tolerance;
- deterministic first-blocking feedback;
- small authored sets of locks/blanks per case;
- no authoritative continuous geometry or floating-point fit.

Presentation may look tactile and physical, but visuals never override discrete domain state.

## Explicit non-goals
- no real-world lock-bypass instruction or simulation of picking techniques;
- no burglary/crime progression;
- no freehand/continuous filing skill requirement;
- no random jams, spring failures or hidden `realism` exceptions;
- no hundreds of key blank types;
- no shop economy, customer queue, crafting grind or business management layer as core progression;
- no procedural campaign used to substitute for authored puzzle quality;
- no timed pressure in main puzzle reasoning;
- no multiplayer/network dependency;
- no roguelite/meta-stat progression;
- no inventory-grid optimization;
- no requirement to memorize numeric bitting codes;
- no bespoke tool introduced merely to rescue a weak late puzzle.

## Product promise / fairness contract
If a key opens or fails, the same authoritative rules explain it every time. The player can inspect enough state to understand a failure. Impression feedback never lies. Preview/animation cannot imply a different fit than the domain state. A case may hide information until tested, but it may not hide rules.

## Phase-3 lock decision
**PRODUCT THESIS LOCKED.** Phase 4 may refine exact mechanics, ordering, undo, progression and balance, but it may not turn the game into lockpicking, business simulation, continuous dexterity filing or generic blank-budget optimization without reopening concept selection.

## Phase 4 required work
Specify the complete mechanical architecture: exact cut/fit/feedback semantics; lock acceptance model; test access; knowledge model; committed-state and undo/restart boundaries; multi-key/multi-lock ordering; win/fail/softlock rules; progression/difficulty; hint authority; solver state and validation; anti-greedy constraints; balance knobs; edge cases; and >=50 mechanical acceptance tests. Mature depth must continue using the fixed primitive vocabulary rather than locksmith exception trivia.
