# GAME #005 — PHASE 10 AUTHORITATIVE AMENDMENTS

Last updated: 2026-08-23
Factory run: **10 — extended pass**
Phase: **10 — Adversarial Review / Repair**
Selected concept: **G5C02 — Tension Budget**
Production implementation: **NOT STARTED**

# AMENDMENT STATUS = AUTHORITATIVE

These amendments repair contradictions discovered in `GAME5_WHOLE_GAME_SIMULATION.md` and `GAME5_ADVERSARIAL_REVIEW.md`.

For the exact subjects below, this file **supersedes conflicting older wording** in:
- `GAME5_PRODUCT_THESIS.md`;
- `GAME5_MECHANICS.md`;
- `GAME5_CONTENT_ARCHITECTURE.md`;
- `GAME5_UX_PRESENTATION.md`;
- `GAME5_TECHNICAL_SPEC.md`.

Rules not explicitly amended remain in force.

---

# A01 — Finite distribution-feasibility is a first-class content rule

For revision `R` with:
- `N` active loads;
- fixed encounter budget `B`;
- declared snap count `K`;

a legal rail requires an ordered sequence of **K distinct vectors** in `{0,1,2}^N` such that:
1. every vector sums exactly to `B`;
2. every adjacent pair differs by exactly one `-1`, one `+1`, all other entries 0;
3. every vector maps to a valid distinguishable world state.

It is not enough that K mathematically possible vectors exist somewhere; the authored bands themselves must form a valid adjacent-transfer path.

## New mandatory validator V19 — Distribution Path Feasibility

Before normal encounter validation:
- enumerate legal vectors for every revision;
- verify declared authored vector count equals snap count;
- verify uniqueness;
- verify conservation/bounds;
- verify every adjacent pair is one legal give/take transfer;
- emit a direct diagnostic if the active-load/budget/snap combination cannot support the requested path.

V19 is a clearer first-class diagnostic for the constraint already implied by V01/V03/V04.

---

# A02 — Low-load state-space bounds

With canonical 0/1/2 bands:

## One active load
For any fixed B, only one vector exists.

**Therefore a shipped 3–5 snap-band rig may never have only one active load in any revision.**

## Two active loads
Maximum distinct legal vectors:
- B=0 ->1;
- B=1 ->2;
- **B=2 ->3**;
- B=3 ->2;
- B=4 ->1.

Therefore:
- any two-load revision with 3 snap bands must use **B=2** and may use the full path `[2,0] -> [1,1] -> [0,2]` or reverse / load-permuted equivalent;
- a two-load revision may **never** support 4 or 5 distinct snap bands under current canon.

This is now explicit mechanical/content canon.

---

# A03 — E01 First Pull repaired

Old row:
- 1 Lift;
- 3 bands.

Old row is invalid and superseded.

## New E01 contract
- **Loads:** Lift + Counterweighted Gate;
- **Snap bands:** 3;
- **Budget:** B=2;
- **Mutation:** none;
- **Primary signature:** S01 Direct redistribution;
- **Completion-critical load:** Lift;
- **Secondary teaching load:** Gate visibly participates in give/take but its passage is not required to finish E01;
- **Canonical vector family:** `[2,0] -> [1,1] -> [0,2]` or mirrored rail equivalent.

Purpose:
The first action teaches the real conserved system. It does not create a fake one-load exception.

E02 may reuse Lift+Gate but must make **both consequences completion-relevant**, turning observation into an actual tradeoff.

---

# A04 — Low-load mutation templates

## 3 loads ->2 loads REMOVE
Legal baseline only when:
- snap count = **3**;
- fixed B = **2**;
- pre- and post-revisions each provide three distinct legal adjacent vectors.

Normative example:

Pre active `[L,G,S]`, B=2:
- P0 `[2,0,0]`
- P1 `[1,1,0]`
- P2 `[1,0,1]`

Remove Gate. Post active `[L,S]`, B=2:
- P0 `[2,0]`
- P1 `[1,1]`
- P2 `[0,2]`

Other load ordering/path variants are legal if V01–V19 pass.

## 2 loads ->3 loads ADD
Legal baseline with:
- snap count = **3**;
- fixed B = **2**.

Normative example:

Pre active `[L,G]`:
- P0 `[2,0]`
- P1 `[1,1]`
- P2 `[0,2]`

Add Span. Post active `[L,G,S]`:
- P0 `[2,0,0]`
- P1 `[1,1,0]`
- P2 `[0,1,1]`

These templates are the teaching forms for load removal/addition.

---

# A05 — High-band mutation templates

For 4–5 snap-band mutation encounters, do **not** pass through a two-load revision.

Approved structural families:

### ADD family
- 3 active loads ->4 active loads;
- central budget normally B=3;
- 4 or 5 bands if V19 passes.

Example 5-band pre path for 3 loads / B=3:
- `[2,1,0]`
- `[1,2,0]`
- `[1,1,1]`
- `[0,2,1]`
- `[0,1,2]`

Example 5-band post path for 4 loads / B=3:
- `[2,1,0,0]`
- `[1,2,0,0]`
- `[1,1,1,0]`
- `[1,1,0,1]`
- `[0,2,0,1]`

### REMOVE family
- 4 active loads ->3 active loads;
- central budget normally B=4;
- 4 or 5 bands if V19 passes.

Example 5-band pre path for 4 loads / B=4:
- `[2,2,0,0]`
- `[2,1,1,0]`
- `[1,2,1,0]`
- `[1,2,0,1]`
- `[1,1,1,1]`

Example 5-band post path for 3 loads / B=4:
- `[2,2,0]`
- `[2,1,1]`
- `[1,2,1]`
- `[1,1,2]`
- `[2,0,2]`

These examples prove feasibility; final encounter blueprints must still choose vectors that satisfy their own traversal reasoning and signature-dedup requirements.

---

# A06 — Band C sequencing repaired

Old content skeleton placed Twin Lifts / Twin Gates / Twin Spans consecutively, creating an avoidable S08 repetition cluster.

Final intended E11–E15 order entering Phase 11:
- **E11 Twin Lifts** — S08 repeated-archetype competition;
- **E12 Three Placement** — S07 relay;
- **E13 Twin Gates** — S08;
- **E14 Commit Pocket** — S12 player-location-dependent value;
- **E15 Twin Spans** — S08/S03.

This is a sequencing change only. No mechanics are added.

---

# A07 — Band D exact mutation metadata repaired

## E16 — Counterweight Gone
- active pre: Lift + Gate + Span;
- active post: Lift + Span;
- mutation: REMOVE Gate;
- **snap count 3**;
- **B=2**;
- use legal A04-family vectors;
- first explicit removal lesson / S09 + S16.

## E17 — New Span Joined
- active pre: Lift + Gate;
- active post: Lift + Gate + Span;
- mutation: ADD Span;
- **snap count 3**;
- **B=2**;
- use legal A04-family vectors;
- first explicit addition lesson / S10 + S16.

## E18 — Return Inversion I
- active pre: **4 loads using only the three archetypes**; recommended repeated Lift or Gate instance;
- active post: 3 loads after visible REMOVE;
- **snap count 4**;
- **B=4** baseline;
- mutation family: 4->3 REMOVE;
- primary S11 return inversion;
- must use V19-clean 4-band paths.

## E19 — Mutation Mid-Route
- active pre: 3 loads;
- active post: 4 loads;
- **snap count 5**;
- **B=3** baseline;
- mutation: ADD only;
- primary S12/S16;
- 3->2 removal is prohibited here.

## E20 — Revision Relay
- active pre: 4 loads;
- active post: 3 loads;
- **snap count 5**;
- **B=4** baseline;
- mutation: REMOVE only;
- primary S17;
- intended solution remains <=4 meaningful commits.

The exact final vector/region blueprint for each is locked in Phase 11; the above structural metadata is already authoritative.

---

# A08 — Late mutation direction constraints

For E21–E26:
- no mutation may create a 1-load revision;
- no 4/5-band mutation may create a 2-load revision;
- **E22 Twin Family Mutation:** use 3->4 ADD / B=3 / 5 bands unless Phase-11 blueprint proves another V19-valid 4->3 structure better;
- **E24 Return Inversion II:** 4->3 REMOVE / B=4 / 5 bands;
- **E25 Final Relay:** 4->3 REMOVE / B=4 / 5 bands;
- **E26 Final Budget:** 3->4 ADD / B=3 / 5 bands to avoid making every late mutation a removal.

Every one must pass V14/V15 so shared mutation family does not become duplicated reasoning.

---

# A09 — Demo D04 repaired

The commercial demo's mutation climax uses the **A04 3->2 REMOVE template**:
- 3 active loads pre;
- 2 active loads post;
- 3 snap bands;
- B=2;
- visible removal;
- same physical band reinterpreted after mutation;
- at least one post-mutation reconfiguration required for extraction.

The demo remains 15–25 minutes and still proves the full differentiator.

No 4-band 3->2 demo mutation is allowed.

---

# A10 — One-week empirical prototype repaired

Older Phase-3 wording suggesting one 4-position 3-load removal rig is superseded.

The mandatory early empirical package contains **three small fixtures**:

### P-A — Give/Take literacy
- 2 loads;
- 3 bands;
- B=2;
- no mutation;
- tests consequence prediction and nonnumeric give/take.

### P-B — Mature traversal
- 3 loads;
- **4 bands**;
- feasible central budget/path validated by V19;
- no mutation;
- at least two meaningful commits separated by traversal;
- tests whether static enumeration dominates.

### P-C — Mutation / return inversion
- 3 loads ->2;
- **3 bands**;
- B=2;
- visible removal;
- C1 checkpoint;
- at least one new post-mutation compromise.

Together these fixtures test all existential questions more honestly than one impossible rig.

Existing empirical thresholds remain unchanged:
- roughly >=75% median post-teaching consequence prediction target;
- most players explain give/take without numbers/graph;
- normal carriage commit roughly <=2–3 seconds once reached;
- blind full enumeration not dominant in mature fixture;
- no realistic rope simulation needed for belief/readability.

---

# A11 — Mutation activation safety

## New mandatory validator V20 — Mutation Activation Safety

For every canonical state from which the objective is legally activatable:
1. apply the authored revision mutation at the current physical snap band;
2. verify resulting distribution is legal;
3. verify transition swept volumes are safe for the player's reachable position;
4. verify a safe C1 spawn exists;
5. verify the resulting C1 state is not an unrecoverable softlock;
6. verify restart from that C1 is deterministic.

If an alternate pre-objective route reaches the objective at another band, that band is included.

Do not hide the objective behind arbitrary band-state UI gating. If an unsafe band must not permit activation, the world traversal/physical access must honestly prevent reaching the objective in that state.

---

# A12 — Controller disconnect during preview

When the sole active controller disconnects during `GRABBED_PREVIEW`:
- game pauses / shows device prompt;
- preview remains non-authoritative;
- **disconnect never commits a snap band**;
- no nearest-band auto-release occurs;
- reconnecting or switching to another valid input device may continue preview;
- player may explicitly cancel back to last committed band;
- restart remains available through pause/menu.

This is an implementation acceptance rule.

---

# A13 — Corrupt-save acceptance behavior

## CurrentRunSave corruption
- preserve ProfileSave;
- quarantine/retain invalid current-run data where practical;
- fall back to current encounter C0 or safe campaign resume point;
- never erase completed encounter progression.

## ProfileSave corruption
- never silently create a fresh profile over corrupted data;
- attempt previous known-good backup where available;
- preserve both failed files during recovery attempts;
- if unrecoverable, show explicit recovery/error state and require user choice before new profile creation.

## Content-version mismatch
- deterministic migration when supported;
- if current C1 cannot migrate safely, fall back to that encounter's C0 while preserving campaign completion state.

---

# A14 — Campaign-count interpretation

The authored target remains **26 main encounters**, but 24–28 remains the frozen acceptable release range.

If empirical repetition review identifies a near-duplicate:
1. cut optional remixes first;
2. then cut the weakest redundant main encounter if needed;
3. do **not** invent a fourth archetype/mechanic merely to preserve count 26.

A 24- or 25-encounter final campaign is preferable to padded 26 if it preserves all reasoning families.

---

# A15 — Phase-11 encounter-lock requirement

Phase 10 confirms that a row-level skeleton alone is not enough for `DESIGN COMPLETE = YES` if implementation would still need to invent the important causal structure of each puzzle.

Before final freeze, Phase 11 must produce or consolidate an implementation-ready encounter lock covering all planned main encounters at least at this level:
- exact active load multiset and stable IDs;
- snap count;
- budget B;
- pre/post mutation direction and load ID if any;
- exact distribution path per revision;
- primary/secondary reasoning signatures;
- intended meaningful commit count/sequence class;
- decision-separating event(s);
- canonical region/traversal-edge blueprint sufficient to reconstruct puzzle logic;
- C0/C1/exit requirements;
- known accepted alternate-solution boundaries;
- V01–V20 pass expectations.

World transforms, final art geometry and cosmetic path shape may remain implementation/content-production flexible, but **the causal puzzle cannot be left for implementation to invent.**

Therefore Phase 11 may not set `DESIGN COMPLETE = YES` until this encounter-level readiness requirement is satisfied or the final campaign count is intentionally reduced and every remaining encounter is covered.

---

# A16 — Authority / no scope reopening

These repairs do **not** reopen:
- concept selection;
- Phase-3 product identity;
- three-state band grammar;
- three load archetype ceiling;
- one local carriage baseline;
- fixed conserved budget per encounter;
- adjacent one-quantum transfer;
- no-numeric/no-graph player-facing thesis;
- no transition timing;
- premium commercial baseline.

They narrow authoring to the subset that is mathematically and experientially valid.

# PHASE 10 AMENDMENT DECISION

All fatal contradictions P9-C01..C04 and adversarial finding P10-F01 are repaired without adding a gameplay pillar.

**PHASE 10 AUTHORITATIVE AMENDMENTS = COMPLETE.**

Phase 11 should now perform a full implementation-readiness audit, create the encounter-level causal lock required by A15, consolidate final authority/acceptance criteria, and freeze only if no important gameplay remains for implementation to invent.