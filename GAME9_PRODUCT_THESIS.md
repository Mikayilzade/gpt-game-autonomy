# GAME #009 — PHASE 3 PRODUCT THESIS LOCK

Status: **PHASE 3 COMPLETE / PRODUCT THESIS LOCKED**
Date: 2026-08-31
Selected concept: **G9C02 Binder's Imposition**
Working title: **Binder's Imposition**
Production implementation: **FORBIDDEN in factory**

## Product thesis

### Target player
Players who enjoy compact systemic deduction puzzles, physical transformation puzzles, constraint satisfaction, and learning a small rule language deeply. Primary target is PC players comfortable with mouse/controller interaction and 20–60 minute focused sessions; no prior bookbinding or print-production knowledge is assumed or required.

### Platform baseline
PC / Steam first. Single-player, offline-first premium game. Keyboard+mouse baseline with controller path required during UX phase. Steam Deck compatibility is a target, not yet a frozen certification claim.

### Genre framing
Tactile systemic permutation / constraint puzzle presented through abstracted book imposition, folding, nesting, trimming, and binding.

### One-sentence hook
**Arrange pages on flat sheets so that after they fold, flip, nest and trim, the finished book reads exactly right.**

### Core fantasy
You are not decorating books or running a shop. You are mastering the strange logic by which an apparently wrong flat sheet becomes a correct physical book. The satisfaction is predicting the transformation, choosing signature roles, and watching a compact mockup fold into proof that the reasoning was correct.

### Core loop
1. Read the requested finished-book constraints.
2. Inspect available sheets/signatures and fold templates.
3. Assign/swaps page faces and choose bounded sheet roles/orientation/nesting.
4. Use physical Fold Preview to inspect deterministic consequences.
5. Revise until all final constraints are satisfied.
6. Commit Bind/Trim and receive an exact success/failure explanation.

Preview reveals consequences; it does not auto-solve constraints.

### Session structure
Cases are discrete authored puzzles with a clear start and solved state. Expected ordinary session: 20–60 minutes, often 2–6 cases depending on difficulty. Campaign progression introduces one transformation primitive at a time, then recombines them. No run-based roguelite wrapper is planned.

### Primary differentiator
The game is not generic bookbinding. Its identity is **physical permutation reasoning**: the player works backward from the desired bound object to an unintuitive flat-sheet arrangement. Late depth comes from signature roles, nesting, facing spreads, orientation, inserts/material restrictions, blanks/trim survival, and alternative fold templates intersecting over the same final book.

### Store/GIF promise
A page layout looks absurd on a flat duplex sheet; the player folds it; the page numbers suddenly become 1-2-3-4 in order. A second sheet is inserted, changing which faces become adjacent. The visual transformation itself explains the hook.

## Scope ceiling
- One compact workbench / abstract production scene; no walkable shop/world required.
- Deterministic discrete authority; presentation animation may be rich but cannot determine gameplay state.
- Main campaign planning target: approximately **30 strong cases**, subject to later content-quality floor rather than a filler quota.
- Logical page-face scale normally 4–20 faces; larger sizes require explicit proof that they add reasoning rather than clerical swapping.
- Small finite catalog of fold/signature templates; each must materially change reasoning.
- Minimal readable page-face assets: numbers, icons, colors, motifs, orientation marks; no large prose-layout burden.
- No need to reproduce real commercial imposition standards exactly. Fictionalized/abstract transformations are allowed whenever they improve clarity and avoid vocational-training expectations.

## Explicit non-goals
- no generic cozy shop management;
- no customer queue/economy simulation as core play;
- no freeform cover decoration or book-crafting sandbox as core identity;
- no realistic print-shop calibration, paper grain science, ink systems, press operation, binding adhesives, machine setup, or professional production training;
- no avatar locomotion requirement;
- no procedural infinite puzzle promise unless later validated as genuinely high-quality;
- no multiplayer/networking baseline;
- no deckbuilding, roguelite metaprogression, grind, FOMO, MTX, or live-service treadmill;
- no giant page counts used merely to inflate difficulty;
- no hidden-information trick where the fold transform is withheld from the player.

## Difficulty philosophy
Difficulty must come from interacting constraints over understandable transforms, not from remembering obscure terminology or mentally tracking dozens of page numbers. Learned local imposition patterns may become reusable skills; mature cases must then ask a higher-order question such as which signature is outer/inner, which stock can occupy which role, which fold template is viable, or how facing/orientation constraints intersect.

## Demo thesis
Target 20–30 minutes:
1. 4-face single-sheet surprise;
2. duplex orientation;
3. second signature and nesting;
4. facing-spread requirement;
5. capstone where two layouts satisfy reading order but only one satisfies a material/signature-role constraint.

A successful demo ends with the player able to predict at least some folded adjacencies before preview and able to explain why a wrong sheet role cannot be repaired by local swapping.

## Empirical gates retained for later phases / prototype
1. After tutorial case 4, at least 70% of representative testers should predict two final adjacencies before preview; otherwise onboarding/mental model is failing.
2. Mature play must not devolve into blind Fold Preview -> swap -> preview loops. A majority of observed actions in representative later cases should be explainable by a stated hypothesis.
3. Orientation must remain readable without real printing jargon. If binary orientation markers still cause dominant clerical errors, simplify further.
4. 12–20 face cases must be tested for interaction cost; if manipulation time dominates reasoning time, add structured swap/group operations without automating the puzzle.
5. At least ~30 distinct strong cases must be supportable from the eventual mechanical/content vocabulary without filler or near-isomorphic repetition.

## Working title direction
**Binder's Imposition** remains the internal/working title because it names the central transformation but may be too technical for a storefront. Phase 6/7 may test clearer commercial names. Store copy should never require the player to know what "imposition" means; the hook sentence must explain it visually and verbally.

## Phase-3 freeze
The following are now canon unless a later adversarial phase finds a contradiction severe enough to reopen them explicitly: selected concept, PC/Steam-first single-player premium baseline, physical-permutation puzzle identity, deterministic flat-sheet -> folded-book transform, reversible layout/nesting decisions, no real-industry simulation requirement, compact workbench scope, and depth through intersecting final-book constraints.

## NEXT DESIGN QUESTION
Phase 4 must turn this thesis into exact mechanical architecture: canonical state model; allowed verbs; fold/nest/trim ordering; orientation semantics; signature templates; constraint language; preview/commit behavior; win/fail states; Undo/Redo/Restart; difficulty knobs; solver/validator contract; anti-bookkeeping operations; and minimum acceptance tests.