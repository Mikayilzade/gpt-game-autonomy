# GAME #006 — STITCHSPACE — WHOLE-GAME SIMULATION ON PAPER

Last updated: 2026-08-29
Factory run: **9**
Phase: **9 — Whole-Game Simulation on Paper**
Selected concept: **G6C01 Stitchspace**
Production implementation started: **NO**
DESIGN COMPLETE: **NO**

Purpose: walk the frozen Phase-3..8 design as a real player/product instead of as separate specifications, expose contradictions/repetition/value failures, and make only the smallest repairs needed before adversarial review.

---

# 1. First boot / first 20 minutes

First launch presents accessibility/input setup, then immediate access to the first case/demo path. No cinematic delays the verb.

C01 establishes a seam as an already-existing physical relationship. The player crosses it before editing it. C02 then forces the first endpoint move and makes the old route disappearing necessary. This is critical: if C02 can be solved while mentally treating the seam as “placing a second portal,” onboarding has failed.

C03–C05 establish the commercial hook sequence:
- scarce seam reused for different destinations;
- orientation visible in physical room frames;
- useful disconnection creates safety/access rather than merely being a penalty.

Expected first-session language after C05: “I move one end of the connection, so the old connection vanishes.” If players instead say “I make portals between rooms,” the vertical slice must improve physical seam persistence/OLD→NEW feedback before bulk content.

No contradiction found with Phase 6 onboarding.

---

# 2. First hour — C01–C10

The campaign moves from replacement literacy into lost-return-route, object-before-player ordering, isolation and orientation+cut.

Healthy rhythm:
1. inspect physical room state;
2. form a topology hypothesis;
3. edit one endpoint;
4. physically traverse/move an entity;
5. state changes;
6. seam value changes;
7. edit again.

Primary failure mode: consecutive cases could collapse into `connect current room to destination, cross, reconnect`. Phase-5 lost-adjacency requirements already protect mature content, but C07–C10 need explicit review that the *destroyed* connection changes the solution, not merely prevents backtracking.

**P9-R1 repair:** require C07–C10 authoring review to record one sentence: `Why is the lost adjacency materially useful or constraining after the edit?` This is a content-validation clarification, not a new mechanic.

---

# 3. Hours 1–3 — C11–C20

C11 changes seam value after entity movement. C12 introduces occupancy locking without reflex timing. C13–C14 add seam #2 only after one-seam reasoning is established.

Two-seam simulation reveals a readability risk: a player may track seam endpoints but forget which relationship will be destroyed when moving one of four endpoints.

Phase-6 OLD→NEW preview handles the immediate edit, but the idle world also needs persistent pair identity.

**P9-R2 repair:** with >=2 seams, both endpoints of each seam must retain redundant persistent identity (shape/pattern/icon; color optional) even when not selected. This restates Phase 6 as mandatory rather than decorative.

C15–C20 produce the first mature alternation between topology and entity state. The solver must not become player-facing oracle; known dead-end detection remains tooling-only by default.

No new mechanic required.

---

# 4. Midgame — C21–C31

The strongest expected “aha” pattern is `cut before connect`: intentionally reduce current reachability to create a later useful topology. This differentiates Stitchspace from portal routing.

Dominant-strategy attack on paper:
- prefer endpoint nearest current player;
- always preserve one seam as lifeline;
- brute-force all target sockets;
- minimize number of seam edits.

Repairs already present:
- state-dependent rewiring defeats static nearest-target logic;
- C26 inverts the stable-lifeline assumption;
- legal bad moves + free Undo make blind enumeration possible but not rewarding;
- mastery does not universally reward move count.

Remaining risk: brute-force target cycling can become viable if candidate socket counts become too high.

**P9-R3 repair:** runtime UX may list all structurally legal targets, but mature authored cases should normally keep *currently relevant exposed legal targets per selected endpoint* <=6. Cases above 6 require readability justification even if total case sockets remain <=10/12. This narrows presentation/content density without changing structural legality.

Three-seam C30 is simulated as a stress case. It remains valid only if the third seam simultaneously preserves two relations while a third relation is rewritten. If it reads as “more portals to track,” remove it rather than adding UI complexity.

---

# 5. Finale — C32–C34

C34 must feel like compression of learned topology reasoning, not graph size escalation.

Preferred capstone state:
- 4–5 rooms;
- 2 seams default;
- one ordinary loop;
- player + at most one material mover/object;
- useful cut;
- state-dependent reuse;
- orientation or loop dependency;
- at least two solution skeletons where solver tractability permits.

**P9-R4 repair:** C34 defaults to **2 seams**. A third seam is allowed only if Phase-5 three-seam proof passes *and* naive readability playtest evidence later shows the capstone remains easier to explain than the strongest two-seam alternative. Paper design alone may not promote 3 seams for spectacle.

This protects the finale from complexity inflation.

---

# 6. Undo / hostile legal states

Legal but bad endpoint moves can strand the player or isolate needed objects. Simulation confirms this is acceptable only because exact Undo is immediate and history restores the whole transaction including mover consequences.

Hostile sequence tested conceptually:
1. move endpoint;
2. automatic mover crosses;
3. player Undoes;
4. Redoes;
5. Undoes again;
6. makes a different endpoint move.

Expected: exact prior state restores each time; new move truncates Redo; no mover remains in a hybrid destination.

A player may create an unsolvable state. UI does not automatically announce “dead end,” because that would become solver assistance. Restart/Undo always remain available.

No repair needed.

---

# 7. Pause / Step / moving entities

Occupancy cases remain puzzle/order challenges rather than reaction tests.

Simulation confirms Pause/Step must operate at canonical movement boundaries, and using them cannot invalidate baseline/mastery. A case whose challenge disappears when stepping one deterministic mover is invalid content, not a reason to restrict accessibility.

**P9-R5 repair:** every main case using automatic mover occupancy must include a known baseline fixture replayed entirely through Step-compatible canonical boundaries; validator/review records that no wall-clock timing predicate exists.

---

# 8. Save crash / recovery

Crash scenarios simulated:
- before endpoint transaction commit;
- after new canonical state exists but before durable primary promotion;
- during backup rotation;
- after save write but before UX save indicator;
- after Undo branch change;
- during mover chain presentation.

Phase-8 temp/primary/backup protocol is coherent: resume can only yield exact prior committed generation or exact later committed generation. No half seam/crossing state is persisted.

Important presentation rule: animation may resume/reconstruct from canonical state after load, but must never be treated as proof that an intermediate gameplay state existed.

No repair needed.

---

# 9. Cloud divergence

Device A clears C18 and has active C19 branch. Device B clears C20 and has a divergent C19 branch.

Expected:
- profile clear facts union safely;
- active C19 branches do not merge;
- one verified branch is selected explicitly when needed;
- losing branch remains recoverable where practical;
- offline local play remains available.

No contradiction found.

---

# 10. Demo → full

DEMO01–05 commercial sequence must prove:
1. physical persistent seam;
2. endpoint replacement destroys old adjacency;
3. orientation matters;
4. useful disconnection matters;
5. state-dependent reuse after physical traversal.

The demo must not end after only impossible-space spectacle.

On full install, explicit mapping imports compatible progress/settings monotonically and idempotently. Active demo case state is not guessed equivalent to campaign state.

**P9-R6 repair:** store/demo CTA must appear only outside active puzzle decision flow (completion/title/case-board surfaces), never as an overlay interrupting DEMO05’s final causal reveal.

---

# 11. Controller / Deck / localization simulation

At 1280×800, physical world must remain primary. A two-seam mature room cannot require reading all topology from tiny labels.

Controller loop:
select seam -> select endpoint -> cycle/focus candidate socket -> OLD/NEW preview -> confirm -> traverse.

Keyboard-only uses the same semantic focus graph. Pointer direct selection resolves to the same semantic target.

Pseudolocalization expansion primarily pressures Case Rail, invalid-reason text and objective rows. Topology identity remains icon/shape-based.

**P9-R7 repair:** invalid-edit reasons must use a bounded reason-code + localized template system, not arbitrary generated sentences. This improves localization, tests and support reproduction without changing UX meaning.

---

# 12. Commercial-value pacing

At $17.99 design target, the game cannot rely on 34 nominal levels alone. Value depends on distinct causal skeletons and a satisfying final third.

Paper pacing target:
- first 15–25 min: full hook visible;
- first hour: replacement + useful disconnection fully understood;
- hour 2: two-seam grammar arrives;
- hours 3–5+: increasingly compressed/state-dependent applications rather than new verbs;
- post-clear: 8 remixes only if changed-causal-dependency audits pass.

Commercial risk remains empirical: puzzle experts may clear far faster than 5 hours. Price stays a release-review decision inside $14.99–$19.99.

**P9-R8 repair:** Phase 12G must measure first-clear time separately for experienced systemic-puzzle players and broader target players; do not use one blended average to justify price/value.

---

# 13. Repetition / anti-isomorphism pass

Most dangerous repetition skeleton:
`move endpoint to route object -> object crosses -> move endpoint to route player -> exit`.

Phase-5 anti-isomorphism rules catch consecutive repeated dominant skeletons, but paper simulation strengthens the review requirement:

**P9-R9 repair:** C15–C34 each stores a compact dominant causal skeleton with at least these dimensions where relevant:
- useful cut/isolation;
- orientation dependency;
- seam preservation/inversion;
- entity ordering;
- loop creation/destruction;
- state-dependent target value;
- occupancy/mover sequencing;
- multi-seam role swap.

No consecutive 3-case window may share one dominant skeleton, and every 5-case window must contain >=3 materially distinct dominant skeleton families. This is a clarification of Phase-5 anti-isomorphism authority.

---

# 14. Whole-game empirical gates retained

The following cannot be honestly closed on paper:
- players spontaneously understand replacement rather than portals;
- OLD→NEW preview is fast enough for repeated use;
- two-seam identity remains readable on Deck/grayscale;
- orientation is intuitive without compass arithmetic;
- useful disconnection feels clever rather than punitive;
- C15–C34 feel materially non-isomorphic;
- controller target selection remains predictable in dense rooms;
- three-seam content, if any, remains readable;
- 5–8 hour perceived-value target is plausible;
- demo communicates the full product thesis and creates interest in full game.

These become explicit Phase-10/11 retained empirical gates for Phase 12G.

---

# 15. Phase-9 acceptance checks

- **S9-01** C01–C05 communicate persistent seam + atomic replacement + useful lost adjacency.
- **S9-02** C07–C10 each document why lost adjacency matters materially.
- **S9-03** >=2 seams retain persistent redundant pair identity outside selection state.
- **S9-04** Mature selected-endpoint target density normally stays <=6 or has readability justification.
- **S9-05** C30 third seam remains removable if it fails genuine simultaneous-topology proof.
- **S9-06** C34 defaults to 2 seams absent exceptional proof + later readability evidence.
- **S9-07** Undo/Redo hostile branch simulation restores exact state and truncates correctly.
- **S9-08** Every mover/occupancy case has Step-compatible baseline replay with no wall-clock predicate.
- **S9-09** Save fault simulation never yields hybrid topology/history.
- **S9-10** Divergent Cloud active branches never merge structurally.
- **S9-11** Demo proves state-dependent reuse before CTA interrupts the experience.
- **S9-12** Invalid edit messages use bounded reason codes/localized templates.
- **S9-13** Phase 12G separates expert and broader-target first-clear timing.
- **S9-14** C15–C34 store causal skeleton dimensions sufficient for anti-isomorphism review.
- **S9-15** No three-case mature window shares one dominant skeleton; each five-case window has >=3 families.
- **S9-16** All unresolved player-understanding/value/readability questions remain empirical rather than being claimed solved.

---

# 16. Phase-9 closure

Whole-game path simulated: **YES**
First boot/demo/first hour/midgame/finale simulated: **YES**
Legal-bad/Undo/Redo states simulated: **YES**
Mover/Pause/Step simulated: **YES**
Persistence/Cloud/demo import simulated: **YES**
Controller/Deck/localization pressure simulated: **YES**
Commercial/repetition pressure simulated: **YES**
Canonical repairs added: **P9-R1..P9-R9**
Production implementation started: **NO**
Phase 9 complete on paper: **YES**
DESIGN COMPLETE: **NO**

## NEXT PHASE

**Phase 10 — Adversarial Review.**

Attack fun/repetition, portal misread, dominant seam strategies, brute-force target cycling, alternate-solution explosion, three-seam readability, simultaneous intents, Undo/persistence/Cloud corruption, controller/focus ambiguity, accessibility, demo/value, scope creep and implementation ambiguity. Reconcile P9-R1..R9 into the final authority and produce concrete adversarial acceptance gates before Phase 11 freeze.
