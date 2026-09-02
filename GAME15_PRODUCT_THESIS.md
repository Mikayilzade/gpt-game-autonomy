# GAME #015 — PHASE 3 PRODUCT THESIS LOCK

Date: 2026-09-03
Status: PHASE 3 COMPLETE / PRODUCT THESIS LOCKED
Working title: **FRESH COAT**
Design complete: NO

## 1. Product identity

### One-sentence hook
**Stack ordinary objects so they mask one another, spray the pile in a few fixed passes, rearrange it once, then unpack the objects to reveal whether every hidden face received exactly the right paint history.**

### Genre framing
Finite premium spatial deduction puzzle game. It is not a spray-paint simulator, restoration simulator, physics stacker, packing game, decorating sandbox, real-time dexterity game or factory optimizer.

### Core fantasy
You are not an artist aiming a nozzle. You are a clever paint-shop jig designer: the satisfaction comes from using the workpieces themselves as temporary masks and predicting what the booth will and will not reach before committing a pass.

### Player promise
Every solve should create the feeling:
> “I can see why this arrangement protects exactly those faces — and when I unpack it, the hidden result proves my prediction.”

The reveal is confirmation of reasoning, not a random surprise.

## 2. Target player
Primary: players who enjoy compact visual/spatial deduction, tactile object manipulation, clean deterministic rules, short handcrafted puzzle sessions and explainable failures.

Useful adjacent audiences: thinky puzzle players, cozy/low-pressure puzzle players, Steam Deck/controller users, and people attracted by satisfying physical transformations even if they do not identify as hardcore puzzle players.

Not targeted: players seeking freeform painting, narrative-heavy adventure, realistic workshop simulation, physics chaos, competitive speedrunning as the main game, or endlessly procedural content.

## 3. Platform and input thesis
- PC / Steam first.
- Full controller support is a product requirement, not a stretch goal.
- Steam Deck/handheld readability is a default design constraint.
- Mouse/keyboard may offer faster selection but no exclusive capability.
- No precision pointer aiming is part of the core loop.
- Single-player only for the initial product.

## 4. Core loop
1. Read the final paint-history requirements on 2–5 objects.
2. Inspect object shapes, semantic faces, legal sockets/poses and booth direction(s).
3. Arrange objects so current occlusion produces the intended exposure set.
4. Inspect factual current exposure if desired.
5. Commit a spray pass.
6. If the case allows it, perform the single bounded rearrangement stage.
7. Commit the next pass.
8. Unpack/reveal final per-face histories.
9. Read exact success/failure feedback, undo or reset, and iterate.

The loop must remain understandable without a solver table.

## 5. Session structure
- Typical puzzle: ~2–8 minutes after onboarding, with late capstones allowed to run ~10–15 minutes.
- Typical session: 15–40 minutes / 3–8 puzzles.
- Campaign target: 24 primary cases in 8 groups x 3, as established by Round C.
- Campaign should feel deliberately finite and finishable rather than retention-driven.
- No daily tasks, energy, battle pass, streaks, rotating FOMO content or mandatory grind.

## 6. Differentiator
The differentiator is the combination of:
1. **3D workpieces are the masks** — not flat stencil cards or user-placed masking tape;
2. **mask objects have their own final paint obligations** — they are constrained resources, not disposable blockers;
3. **paint history persists across passes** — raw/A-only/B-only/A->B create temporal meaning without a timer;
4. **one bounded rearrangement can reverse masking roles** — the spatial relationship, not a new subsystem, creates later depth;
5. **final unpack reveal is directly readable** — hidden state becomes visible and explainable.

Any design drift that removes self-obligated masking, persistent history or spatial occlusion risks collapsing the product into flat set partitioning.

## 7. Presentation thesis
Visual style should emphasize clarity and satisfying material response over realism:
- chunky stylized solids;
- stable booth/tabletop framing;
- clearly segmented semantic faces;
- paint represented by both color and pattern/texture identity;
- strong before/after spray wipe;
- satisfying explode/unpack reveal;
- no reliance on tiny texture details, reflections or physically realistic overspray.

The scene should read like a miniature industrial puzzle toy rather than a full workshop simulator.

## 8. Scope ceiling
Initial product ceiling:
- 24 primary handcrafted cases;
- 6–8 reusable core solids plus minor variants only when mechanically justified;
- 2 canonical coat identities in the main campaign unless later mechanical proof demonstrates a third is necessary;
- 2–3 fixed booth directions total across the product vocabulary;
- 2–5 objects per case, with 4 the normal late-game ceiling and 5 exceptional;
- at most one authored rearrangement stage between primary passes unless Phase 4 proves a bounded later variant necessary;
- no continuous physics stacking;
- no freeform geometry authoring required from the player;
- no online multiplayer, workshop economy, NPC job simulation or open hub required.

If later phases need large asset growth or many bespoke mechanics to keep 24 cases fresh, reopen the concept rather than silently expanding scope.

## 9. Explicit non-goals / forbidden drift
The following are out of scope unless design is formally reopened:
- free-aim spray gun gameplay;
- painting percentages / “cover 98% of surface” objectives;
- realistic overspray, viscosity, drip, drying or fluid simulation;
- masking tape/sticker placement as a parallel puzzle system;
- consumable paint/resource economy;
- cleaning/repair/restoration chores;
- physics balance/tower stacking;
- arbitrary mesh rotation/continuous placement;
- hidden-object camera hunting;
- timers, lives, punitive Check limits;
- procedural endless mode used to compensate for weak handcrafted depth;
- story/dialogue production that dominates puzzle production;
- cosmetics or monetization that alter puzzle state.

## 10. Demo promise
Target demo: ~20–30 minutes, using only final-game rules.

Demo arc should teach:
1. one object masks another;
2. adjacent protected faces;
3. masker with own paint obligation;
4. second paint identity;
5. one rearrangement;
6. A-only/B-only/raw distinctions;
7. finale introducing A->B and a self-obligated mask.

The demo must end with a strong stack -> two-pass -> unpack reveal that is representative of the full game, and progress should be structured so carry-over is straightforward if commercial/platform decisions retain that plan.

## 11. Failure and experimentation philosophy
The game should support experimentation without making brute-force attractive.
- Unlimited undo/reset.
- No punishment for a failed attempt.
- No rapid binary Check oracle during arrangement.
- Current exposure preview may show factual booth visibility for the current arrangement only.
- After a spray, the player sees exact actual paint consequences.
- Final reveal says which face-history requirements failed, but never identifies the move that would solve them.

Failure should answer “what happened?” while leaving “what should I arrange differently?” to the player.

## 12. Accessibility/product requirements
- No rule depends on color alone: every coat has distinct pattern/texture/badge identity.
- Semantic face requirements must remain legible at handheld scale.
- Stable camera and discrete navigation; camera movement cannot be required to discover hidden truth.
- Reduced-motion mode replaces animated spray/unpack with concise transitions.
- Full remapping target for production.
- Text is supplemental; the primary rule should be learnable visually.
- No timed execution requirement.

## 13. Content thesis
The campaign is authored around **reasoning families**, not merely more objects:
F1 direct occlusion; F2 differential neighboring-face protection; F3 self-obligated mask chains; F4 pass-specific exposure; F5 ordered history; F6 cavity reveal; F7 mask-role reversal; F8 coupled capstones.

Each family receives three cases. A normalized repetition gate must reject cases that differ only by mesh/color relabeling while preserving the same exposure/dependency structure.

## 14. Commercial thesis boundary
Exact price is Phase 7 work, not locked now. Product form is nevertheless locked as:
- finite premium game;
- no ads;
- no paid hints;
- no consumable monetization;
- no FOMO retention layer;
- demo should represent the real product rather than a separate mode.

## 15. Technical philosophy boundary
Phase 4/8 will define exact mechanics and runtime, but Product Thesis requires:
- authoritative puzzle truth must be deterministic and semantic, not pixel/renderer threshold based;
- object placement/rotation must be discrete;
- exposure must resolve exactly against authored face-regions;
- solver/certifier enumeration is allowed for authoring and QA but is not surfaced to players;
- rendering cannot become the source of gameplay truth.

## 16. Empirical gates carried forward
These are implementation/prototype validation obligations, not unresolved rules:

### E1 — spatial predictability
After onboarding, fresh players should correctly predict the large majority of current semantic face exposure before spray. If they need x-ray/solver overlays or constant camera hunting, readability has failed.

### E2 — four-object readability
Late 4-object scenes must remain understandable using selection outlines/isolation and stable camera without turning inspection into an oracle.

### E3 — reasoning vs blind permutation
Observed players should eliminate arrangement classes using exposure/history reasoning rather than systematically cycling sockets/poses.

### E4 — 24-case freshness
The full authored ladder must pass normalized repetition review and human playtest for cognitive distinctness; difficulty cannot come mainly from adding objects or sockets.

### E5 — reveal satisfaction
The unpack/result moment must feel like proof of the player's prediction, not delayed opaque validation.

## 17. Product-thesis acceptance test
Phase 3 passes because a fresh implementation/design session can now state without invention:
- who the game is for;
- what the player does minute to minute;
- what the game is and is not;
- why it differs from adjacent paint/masking games;
- what the full campaign scale is;
- what the demo promises;
- what scope may not silently expand;
- which empirical risks remain.

PHASE 3 = COMPLETE
DESIGN COMPLETE = NO

## NEXT ACTION — PHASE 4 MECHANICAL ARCHITECTURE
Fully specify the exact mechanical system: object/face/socket model; legal pose and compatibility rules; semantic exposure computation; booth/pass ordering; coat-history state machine; rearrangement contract; final target predicates; success/failure; current-state inspection; undo/reset; progression/difficulty knobs; canonical edge cases; equivalence/certifier model; and at least several fully worked puzzles including a late mask-role-reversal case. Resolve whether two coats and one rearrangement are universal ceilings or campaign-local parameters without adding optional mechanics merely for variety.