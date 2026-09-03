# GAME #015 — PHASE 9 AUTHORITY PATCHES

Date: 2026-09-03
Status: ACTIVE SUPERSEDING PATCHES FROM WHOLE-GAME SIMULATION

This file explicitly patches narrow ambiguities discovered by `GAME15_WHOLE_GAME_SIMULATION.md`. For the clauses below, this file has later authority than the corresponding Phase 6–8 wording. All unmentioned rules in the original files remain unchanged.

## P9-P1 — Progression / unlock graph
Supersedes any interpretation of `GAME15_COMMERCIAL_MODEL.md` Section 4 that treats 2-of-3 family completion as sufficient to bypass a concept prerequisite.

- The 2-of-3 rule controls normal family flow/visibility.
- Individual case playability is authoritative and is evaluated from stable `prerequisite_case_ids` and/or frozen concept requirement tags.
- FC03 is required before any case whose intended proof assumes self-obligated masking as established knowledge, including F3's core chain content.
- FC10 is required before any later case whose proof assumes established two-pass manipulation.
- FC13 is required before FC14–FC15 and every later case containing A_THEN_B target history.
- FC16 is required before FC17–FC18 and every later case whose proof depends on cavity semantics.
- Imported demo completion satisfies the same gate by stable case ID even when intervening campaign cases are incomplete.
- Imported completion never marks skipped cases complete and never fabricates a family 3/3 completion.
- Case-level prerequisite predicates override family UI state whenever the two disagree.

## P9-P2 — Continue after demo import / nonlinear progress
Supersedes any implementation that derives Continue from the numerically highest completed case.

Continue order is:
1. resume a valid in-progress case if one exists;
2. otherwise choose the lowest-display-order unlocked incomplete primary case;
3. if progression is blocked only by a mandatory concept gate, choose that gate case;
4. if all 24 are complete, enter campaign-complete/replay surface.

Case Select must display legitimate imported completions even if surrounding skipped cases are incomplete.

## P9-P3 — Editable arrangement persistence
Clarifies `GAME15_TECHNICAL_SPECIFICATION.md` persistence contracts.

For explicit exit from a puzzle, application suspension, and Dynamic Cloud Sync hand-off, persistence must include:
- the latest durable spray checkpoint; and
- the current valid editable arrangement snapshot for `EDIT_A` or `EDIT_B` when it differs from that checkpoint.

The editable snapshot is semantic stable-ID data, never interpolated transforms. It may be discarded independently if corrupt, falling back to the last committed spray checkpoint without damaging profile progress. Presentation animation state is never persisted.

## P9-P4 — Completion states
Clarifies `GAME15_COMMERCIAL_MODEL.md` campaign semantics.

Two distinct states exist:
- `FINAL_CASE_CLEARED`: FC24 has been completed at least once;
- `CAMPAIGN_COMPLETE`: all stable case IDs FC01–FC24 are complete.

First FC24 clear may trigger the main ending/credits celebration. The canonical campaign-completion achievement and 24/24 completion state require `CAMPAIGN_COMPLETE`. A player who advanced via 2-of-3 can therefore see the ending before completing skipped cases without the game falsely claiming 24/24.

## P9-P5 — Late target-rail readability
Clarifies `GAME15_UX_PRESENTATION_ARCHITECTURE.md` for FC21–FC24 and other high-target-count cases.

- Target requirements default to object-grouped collapsible cards rather than one flat list.
- Selecting a workpiece automatically scopes/highlights its target card.
- Selecting a target row focuses/highlights that exact semantic region in 3D.
- Collapsing cards never hides whether an object has unresolved target obligations; the collapsed header shows a neutral count/history-class summary, not correctness against the current arrangement.
- No grouping may expose blocker identity, intended pose, nearest solution, or counterfactual correctness.

## Authority note
These are specification repairs, not new mechanics. Phase 10 must attack them together with the original UX/Commercial/Technical files. At Phase 11 freeze, either fold them into final consolidated authority or retain this file explicitly in the authority chain.