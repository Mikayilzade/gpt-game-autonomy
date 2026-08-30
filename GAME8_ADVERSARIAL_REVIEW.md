# GAME #008 — PHASE 10 ADVERSARIAL REVIEW

Last updated: 2026-08-30
Phase: **10 — Adversarial Review**
Selected concept: **G8C02 Locksmith's Margin**
Working title: **Locksmith's Margin**
Production implementation started: **NO**

This review attacks the complete Phase 3–9 design without protecting the selected concept. Repairs discovered here are authoritative through `GAME8_PHASE10_REPAIRS.md` until Phase 11 consolidates the final specification.

## Verdict
**SURVIVES PHASE 10, WITH MANDATORY REPAIRS APPLIED.**

The concept still has a coherent product core: destructively editing a tiny set of persistent artifacts to cover overlapping target-acceptance sets, with deterministic partial feedback. However, Phase 10 found one major structural mistake in earlier framing: free non-destructive TEST means exhaustive currently accessible testing is rational baseline behavior, so test-order scarcity cannot be sold as depth unless access/irreversible state actually changes what can be learned. This is repaired rather than papered over.

No new gameplay primitive is required. No economy, timer, durability, random information, lockpick verb, or punitive test cost is added.

---

# 1. Fun / repetition attack

## Attack
The obvious repetitive loop is:
`TEST every accessible lock -> FILE one step -> repeat all useful TESTs -> solve coverage`.
With 4–6 columns and small accepted sets, this can become clerical unless the next FILE decision changes which future multi-lock overlaps remain possible.

## Failure found
Earlier documents overstate `which lock should I test next?` as a strategic question even when all those tests are free and currently accessible.

## Repair
AR1 makes exhaustive-current-state testing the baseline attack policy. Mature cases must remain interesting after all current free information is collected.

## Content survival standard
C07+ should primarily evolve through:
- partition of locks across persistent blanks;
- preserving a vector because future access is not yet available;
- branch choice that changes multiple future overlaps;
- irreversible repurposing after a blank's information role is actually exhausted;
- access unlocks that expose genuinely new information only after an OPEN commitment.

Cases whose only tension is `maybe I shouldn't test that yet` are cut.

**Result: SURVIVES with AR1.**

---

# 2. Cheap-solver / dominant-policy attack

Policies attacked:
- deepest-first;
- shallowest-first;
- finish-current-lock;
- exhaustive-test-first;
- never-repurpose;
- greedy largest known overlap;
- solver-assisted memorization.

## Deepest-first
Still defeatable by overlap preservation / branch sharing. Required C06/C11/C15/C29/C32 counters remain plausible.

## Shallowest-first
Still defeatable where one specialist requires irreversible deeper commitment and postponing it harms future partition/access. Must be validated from real case data, not prose.

## Finish-current-lock
Still defeatable in mature partition/access cases because completing one lock may require a FILE that destroys a future shared vector.

## Exhaustive-test-first
**Cannot honestly be treated as a mistake at a fixed forward state.** A legal free TEST cannot reduce future options. This is the major Phase-10 finding. AR1 changes the design standard accordingly.

## Never-repurpose
Late conversion cases can defeat it because opened-once state persists and repurposing frees scarce blank capacity.

## Greedy largest-known-overlap
Must fail in at least several mature cases through future access / branch structure where present count is not future coverage. C28/C29/C32 are the natural anchors.

## Solver-assisted memorization
Unlimited Undo permits counterfactual data mining by a determined player. This is accepted as an assistance path, not blocked with artificial punishment (AR2). Mature cases must retain a non-trivial omniscient partition problem.

**Result: SURVIVES, but V5 must be normalized in Phase 11 around AR1/AR2.**

---

# 3. Information fairness attack

High-risk sets reviewed conceptually: C08–C12, C15–C16, C22–C26, C30–C32.

## Failure condition
An intended trace is invalid if a required FILE depends on an exact unseen accepted depth merely because the author/omniscient solver knows it.

## Mandatory Phase-11 gate
Each high-risk case must include at least one explicit information-respecting witness trace over observations available before every irreversible FILE. It is insufficient to say V3 exists; the freeze package must require the validator to emit or verify those witnesses.

## Specific pressure points
- C08 Wrong Partition: global failure must be inferable from visible overlap evidence before the decisive cut.
- C10 Probe First: probe value must arise from information available at current vector; no unseen family guess.
- C11 Strong Mark Trap: STRONG is only distance class, never exact depth recommendation.
- C15/C16: branch sharing must not reveal undiscovered exact branch coordinates through cutaway art.
- C22: visible access predicates must be enough to reason about consequence before specialization.
- C23–C25: later conversion cannot assume unseen data that only omniscient validator knows.
- C26: knowledge difference by blank history is legal; fit difference is not.
- C30: exhaustive current testing must still leave a destructive dilemma or the case is cut.
- C31/C32: at least one information-respecting solution plus >=2 strategically distinct valid final traces for C32.

**Result: SURVIVES subject to validator witness requirement.**

---

# 4. Tutorial truthfulness attack — D02/C03

## Failure found
Previous wording could imply a single Undo or Restart repairs a TOO_DEEP state even though TEST itself is an authoritative history action, or could start from an authored overcut that Restart reproduces.

## Mandatory repair
AR3 freezes a truthful sequence: player creates the overcut from a solvable start, TEST proves TOO_DEEP, first Undo removes the TEST, second Undo removes the cut. Restart also returns to the genuinely solvable authored start.

This has an extra benefit: it teaches exact action-history semantics rather than hiding them.

**Result: REPAIRED.**

---

# 5. Undo / Redo / meta-exploit attack

## Attack
Unlimited Undo can turn irreversible discovery into a reversible oracle because human memory survives state rewind.

## Decision
Do **not** charge Undo, limit it, erase tests selectively, or add punishment. Those fixes would violate the product's time-respect promise and create an economy around mistakes.

AR2 explicitly accepts counterfactual rewind as optional player assistance. The normal forward grammar remains irreversible; no-Undo mastery is a post-solve optional challenge.

## Redo persistence
Phase 9 left persistence ambiguous. AR4 freezes full redo-tail persistence with action-log cursor. Losing redo after reload is no longer allowed except when the attempt itself is invalidated by content-version recovery.

**Result: REPAIRED / EMPIRICAL GATE retained for natural abuse rate.**

---

# 6. Solved transaction race attack

Sequence attacked:
`final OPEN -> pending review -> Undo -> Redo -> quit/crash -> Continue -> platform achievement callback -> reconnect`.

AR5 freezes one idempotent local solve-commit journal keyed to case/attempt. Platform achievements are downstream. Power-loss injection at every transaction boundary is mandatory implementation QA.

No state may exist where:
- campaign case solved but prerequisite unlock missing;
- unlock exists while solved fact absent;
- achievement platform grant is the only record of solve;
- pending review has lost its exact Undo history;
- replay Undo erases previously committed completion.

**Result: SURVIVES after AR5.**

---

# 7. Persistence attack

Attacks:
- corrupt primary + valid backup;
- corrupt primary + corrupt backup;
- stale schema;
- stale case content;
- save after Undo with redo tail;
- crash during action animation;
- repeated recovery loop.

Existing Phase-9 R3/R9 are sound. AR4 closes redo-tail persistence. Both-corrupt profile behavior must preserve corrupt artifacts where practical, explain recovery, and offer fresh local profile rather than boot loop. It may not salvage partially trusted puzzle state field-by-field without namespace validation.

**Result: SURVIVES.**

---

# 8. Cloud / platform attack

Offline-first remains coherent. Committed solved-set facts may merge monotonically where schema/profile match; current attempt is one whole branch. Redo tail travels with that branch.

Steam unavailable/reconnect cannot alter puzzle outcomes. Achievement event reconciliation is idempotent.

Conflict chooser must compare human-readable campaign progress + current case/attempt recency, not raw file timestamps alone.

**Result: SURVIVES.**

---

# 9. UX ambiguity attack

## First-blocker / prefix
Risk: animation accidentally reveals later columns. Hard rule remains: later columns stay neutral/unresolved after first blocker.

## Master branches
Risk: cutaway diagram draws exact hidden branch locations. Tutorial may reveal the rule `two valid bands exist`; exact undiscovered coordinates remain hidden until logically established.

## Wear
Risk: players infer a center/real tolerance. UI uses `valid band` semantics only; no realism calibration.

## Access gates
Known inaccessible locks stay visible with prerequisite; no surprise permission.

## Identical-vector blanks
Stable labels/rack position mandatory because history differs while fit does not.

## 6-lock bench / ledger
Physical overview may abbreviate, but focus view must expose full lock identity/access text; ledger scrolls instead of shrinking.

## Rapid input
One globally chosen policy: either reject authoritative input during critical presentation beat or queue at most one semantic command. Mixed per-animation behavior is forbidden.

**Result: SURVIVES.**

---

# 10. Accessibility / localization attack

Settings cannot reveal extra lock information. Numeric labels show key depths only. High contrast may emphasize known blocker/prefix only. Reduced motion jumps to same semantic result.

1280×800 requirement survives by inspection zoom + scrolling, not tiny text. Long localized access predicates require wrapped/focus-expanded text and stable lock IDs/icons.

Controller focus at 3 keys × 6 locks × ledger density requires deterministic semantic navigation graph; pointer-hover may not steal controller focus.

**Result: SURVIVES.**

---

# 11. Content exhaustion / isomorphism attack

## Risk
32 authored cases can easily become matrix permutations wearing different titles.

## Decision
Do not protect the number 32. AR6 keeps 28 as strong floor and makes 32 aspirational.

High-risk similarity clusters:
- C08/C09/C11 around partition + tempting local choice;
- C10/C12/C23/C25 around diagnostic value;
- C13/C14/C15/C16 around branch learning;
- C17/C18/C19 around broad acceptance;
- C20/C21/C22 around access;
- C27–C30 around mixed-policy synthesis.

This does not mean automatic cuts: tutorial cases can differ by the truth taught. But C07+ must provide a distinct thought delta and survive canonical-signature review.

**Minimum strong release set: 28.** If only 28 remain causally distinct after authored data/solver review, ship 28.

**Result: SURVIVES with aggressive content gate.**

---

# 12. Scope / production attack

Potential scope traps:
- realistic lock internals;
- bespoke key meshes per case;
- tactile filing physics;
- detailed hands/avatar;
- unique mechanisms;
- full mechanism reveal;
- Cloud/achievement plumbing before core validator quality.

AR7 cuts these. The production promise is tactile **presentation of discrete domain events**, not realistic lock simulation.

Priority order if schedule pressure occurs:
1. deterministic Domain Core correctness;
2. case validator / fairness / anti-isomorphism;
3. readable physical-first UX + ledger;
4. controller/Deck/accessibility;
5. reusable tactile key/lock visuals;
6. platform extras / optional reveal/polish.

Cloud and achievements are shipping targets, but may never force puzzle authority into platform callbacks.

**Result: SURVIVES with scope cuts.**

---

# 13. Commercial / store attack — fresh 2026 check

Fresh Steam research materially changes the marketing risk:
- **Access Key** released April 8, 2026 and explicitly includes locksmith gameplay with lockpicking, key cutting and re-keying.
- **Locksmith Simulator** remains coming soon and advertises broader locksmith jobs including producing locks and keys.

Therefore `key cutting` itself cannot carry differentiation. The exact strategic grammar still appears meaningfully distinct in current search, but the store surface must lead with **one key / several locks / every cut destroys options**, not generic locksmith simulation. The working title may be retained for now, but commercial naming remains an empirical release task rather than mechanical canon. citeturn421262search2turn421262search0

Blind trailer/capsule target is tightened in AR8.

**Result: SURVIVES, store-positioning risk MEDIUM.**

---

# 14. Safety boundary attack

A realistic cutaway + key-cutting tutorial could accidentally become real locksmith instruction even if lockpicking is absent.

AR9 requires fictionalized non-diagnostic mechanism, no real bitting/tolerance/keyway/brand/procedure data, and no training claims. Post-solve reveal, if any, is abstract accepted-set visualization only.

**Result: SURVIVES with explicit safety boundary.**

---

# 15. Mandatory repairs summary

Mandatory before Phase-11 freeze normalization:
1. normalize exhaustive-current-state TEST as rational baseline policy (AR1);
2. normalize unlimited-Undo human-memory leakage as accepted assistance behavior (AR2);
3. replace ambiguous D02/C03 staging with exact two-Undo truthful tutorial (AR3);
4. persist full redo tail and cursor (AR4);
5. freeze idempotent solved-attempt local commit journal (AR5);
6. protect 28-case quality floor over 32-case quota and require thought-delta/isomorphism review (AR6);
7. keep tactile 3D fictional and reusable, cutting realism scope first (AR7);
8. sharpen current-store differentiation after 2026 key-cutting analogue evidence (AR8);
9. freeze non-instructional fictional locksmith safety boundary (AR9).

---

# 16. Kill gates carried into implementation / empirical validation

The design should be reopened or materially reduced if prototype/playtest shows any of these:
- >=25% fresh target players naturally settle into repetitive exhaustive rewind probing and report it as the best/clearest way to play;
- after exhaustive currently accessible tests, mature cases routinely have an obvious single FILE with no real partition/preservation choice;
- >=30% target players in blind trailer/capsule test primarily describe real lockpicking/burglary/generic locksmith simulator rather than multi-lock preservation puzzle;
- physical presentation cannot make first blocker/prefix/cut consequence readable without a dominant numeric matrix UI;
- strong validated campaign falls below 28 non-isomorphic cases;
- C32 cannot support >=2 materially distinct valid traces;
- information-respecting validator cannot produce witness solutions for high-risk mature cases;
- safety/presentation requires real locksmith dimensions or procedures to remain understandable;
- solver/validator complexity or tactile art cost displaces accessibility/controller/content validation from release scope.

---

# 17. Empirical gates retained intentionally

These are not unresolved rules:
- final release price inside existing review band;
- exact final case count 28–32 according to quality;
- whether optional Reveal Mechanism survives production;
- exact input busy-policy choice (reject vs queue-one), provided it is global and deterministic;
- how strongly Undo is visually emphasized after observing player behavior;
- final commercial title/store tags/localization set;
- animation timings within already frozen pacing ceilings.

---

# 18. Phase-11 readiness verdict

**READY FOR PHASE 11 SPECIFICATION FREEZE.**

Reason:
- no attack requires a new gameplay verb;
- the largest conceptual contradiction (free TEST dominance) has an explicit repair that strengthens content requirements rather than inventing punishment;
- TOO_DEEP tutorial and redo persistence are now exact;
- solved transaction, Cloud, accessibility and safety boundaries are implementable without gameplay invention;
- remaining unknowns are empirical implementation/release gates, not missing core game design.

Do **not** set `DESIGN COMPLETE = YES` yet. Phase 11 must normalize Phase-9 + Phase-10 repair authority, define final authority order and acceptance/freeze checklist, and verify that a fresh implementation session would not need to invent important gameplay.
