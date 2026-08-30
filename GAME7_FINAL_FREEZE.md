# GAME #007 — LAST KNOWN SHAPE — PHASE 11 SPECIFICATION FREEZE

Last updated: 2026-08-30
Phase: **11 — Specification Freeze**
Selected concept: **G7C02 Last Known Shape**
Production implementation started: **NO**
DESIGN COMPLETE: **YES**
Migration complete: **NO**

This file is the final design authority for Last Known Shape. Older files retain rationale and detail; where this file or `GAME7_ADVERSARIAL_REVIEW.md` explicitly narrows an older allowance, the narrower rule wins.

---

# 1. Frozen product identity

**Working title:** Last Known Shape.

**Platform/product:** PC / Steam first, premium, single-player, offline-capable, controller + keyboard/mouse, Steam Deck-friendly.

**Genre:** systemic observation / transformation puzzle.

**Hook:** Observe an object in one exact authored form, commit that memory, then leave observation; the last remembered form becomes physically real until deliberately overwritten by another observation.

**Core fantasy:** observation is a physical write operation. The player chooses what reality remembers, preserves useful memories through world changes, and overwrites them at the right moment.

**Primary repeated verb:** `COMMIT_OBSERVATION(frame_id, object_id)` from an authored Observation Frame after exact preview.

The game is not free-camera perspective manipulation, pixel/image recognition, physics sandbox, portal/topology game, time-clone game, programming game, combat game, live service or progression economy.

---

# 2. Frozen gameplay vocabulary

Canonical primitive families:
1. stable transformable object identity;
2. discrete authored forms with global affordance tags;
3. discrete pose slots and deterministic movement;
4. authored Observation Frames;
5. exact deterministic Candidate computation;
6. persistent Remembered form;
7. Physical form resolved from Remembered form after observation ends;
8. fixed masks and at most one declared dynamic input per Frame in the main campaign;
9. deterministic receivers/mechanisms consuming form/pose affordances;
10. free exact Undo/Redo and Restart.

Main campaign/demo ceiling: **at most two reasoning-critical remembered objects**. A third critical memory is outside 1.0 campaign canon.

Ordinary object: 2–3 useful forms. Ordinary case: <=4 relevant Frames, normally <=5 pose slots/object. Main campaign Frame: 0–1 dynamic input. No recursive candidate dependency.

---

# 3. Frozen observation semantics

Pure function:

`CANDIDATE(frame_id, object_id, canonical_state) -> form_id | rejection_reason`

Allowed inputs are only explicit authored canonical facts: selected Frame rule, object identity/pose, fixed mask, declared dynamic input object's physical form/pose, and named mechanism state where the global transform family permits it.

Forbidden authority:
- camera transform;
- screen pixels/depth buffer;
- arbitrary ray visibility;
- resolution/antialiasing;
- animation progress;
- wall-clock/frame delta;
- audio;
- hidden physics callback order;
- pointer precision.

Preview and commit query the same Candidate function against the same canonical revision.

Canonical lifecycle:
1. player reaches/activates authored Frame;
2. semantically selects eligible object;
3. Preview shows exact Candidate + current Remembered + neutral overwrite fact;
4. Preview mutates nothing;
5. Confirm atomically overwrites `remembered_form_id` and records committed-observed state;
6. while direct observation remains active, the object's Physical form does not yet adopt the new memory;
7. player leaves/ends observation through an ordinary semantic action;
8. at that canonical boundary `physical_form_id := remembered_form_id`;
9. receiver/mechanism/access consequences resolve deterministically to the next stable command boundary.

Re-entering or previewing never automatically writes memory. Only explicit Confirm commits.

---

# 4. Frozen physical affordance contract

Gameplay never infers authority from arbitrary transformed mesh geometry.

Forms expose finite global tags such as bridge/span, step, blocker, narrow-fit, reach-high, contact, movable/carry eligibility and declared occluder contribution.

Object movement is discrete slot-to-slot and uses current **Physical** form for legality. Remembered form persists through ordinary movement.

Dynamic input/occluder behavior must obey one reusable player-learnable transform-family invariant. Equivalent visible/canonical relations may not map to unrelated outcomes solely to create difficulty.

Every dynamic input relationship must have a visible/inspectable world-space causal bridge at the Frame; UI naming supplements but cannot replace physical evidence.

---

# 5. Frozen deterministic ordering

Domain authority is discrete. Renderer, physics callbacks, scene-tree order and animation timing never decide puzzle state.

For each accepted semantic transaction:
1. validate against immutable pre-state and expected revision;
2. apply direct semantic delta;
3. collect/recompute object affordance claims;
4. resolve receivers by stable priority then ID;
5. resolve mechanism consequences by declared priority then ID;
6. recompute affected access predicates;
7. assert invariants;
8. finalize exact child state/hash/revision/history;
9. emit presentation events.

Mutually incompatible simultaneous mechanism demands require one global deterministic resolution rule or invalidate the authored case.

---

# 6. Frozen Undo / Redo / idempotency

Every accepted semantic command plus all deterministic immediate consequences before the next command opportunity is one history transaction.

Required:
- effectively unlimited active-case Undo/Redo;
- exact parent/child semantic restoration;
- branch-after-Undo truncates old Redo descendants;
- Preview/Cancel never create history entries;
- same command ID + identical payload returns recorded result with no second mutation;
- same command ID + different payload hard-rejects;
- stale expected revision rejects before mutation.

Internal checkpoint/delta/history compaction is allowed only after property tests prove exact hash restoration through long traces, branching and save/reload. No silent player-visible shallow history cap.

Undo/hints/accessibility never invalidate baseline completion or achievements.

---

# 7. Frozen campaign/content architecture

Main target: **C01–C34**.

Strong-release target/floor review: target >=28 strong main cases, but 28 is never permission to ship filler. If 24–27 exceptional cases survive while measured value remains commercially viable, Phase 12G may request explicit scope/price review; otherwise delay/resize/kill rather than add unrelated mechanics.

Demo: **DEMO01–DEMO06**, target ~20–30 minutes and must reach one readable two-object/order dependency.

Optional remixes: **R01–R06 maximum, zero minimum**, admitted only after causal-distinction validation.

Teaching bands remain:
- C01–C05 observation/write/overwrite literacy;
- C06–C10 affordance conflict and preservation;
- C11–C15 state-dependent authored input;
- C16–C22 two memories/order;
- C23–C28 mature preservation chains;
- C29–C34 synthesis with no new magical primitive.

Canonical dominant families F1–F8 remain:
`PRESERVE_OVERWRITE`, `ACCESS_SELF_BLOCK`, `AFFORDANCE_TRADEOFF`, `RELOCATION`, `OCCLUDER_DEPENDENCY`, `DESTRUCTIVE_REOBSERVATION`, `TWO_OBJECT_ORDER`, `STATE_DEPENDENT_REUSE`.

Hard mature diversity rules remain: no three consecutive same dominant family; every five-case mature window >=3 families; C23–C34 >=6 families; no family >30% of C11–C34; occluder family <=25%; two-object order appears >=5 and <=9 main cases; anti-isomorphism causal vectors are mandatory.

P10 addition: every C11+ representative solution requires at least two distinct causal decisions; felt diversity must be validated empirically, not inferred from metadata.

---

# 8. Frozen anti-dominant / anti-enumeration defenses

Mature content must falsify cheap policies across the campaign, including:
- always commit visible Candidate;
- keep largest form;
- keep current form forever;
- observe every Frame before moving;
- solve A completely then B;
- move object directly to receiver then find form;
- try all candidates until goal.

From C16 onward, the campaign target is that >=75% of mature validated cases defeat both a greedy-visible candidate policy and a shallow local-enumeration policy because preservation or physical/world state change is causally necessary.

Free Undo remains. Anti-bruteforce design comes from state dependence, not punishment, hidden costs, limited lives or candidate-count inflation.

Preview may show exact current Candidate and immediately knowable deltas, but never `best`, `required`, dead-state, future-solution, shortest-path or global candidate-atlas information.

---

# 9. Frozen solver / validator contract

Solver consumes only canonical Domain state and uses the same transition semantics as runtime.

V1–V8 remain mandatory:
1. schema/ID/private-callback lint;
2. reachability;
3. Candidate determinism;
4. complete solver termination/instrumentation;
5. shortcut-policy checks;
6. causal diversity/anti-isomorphism;
7. accessibility-data lint;
8. presentation-dependency lint.

Required metrics include states visited, transitions expanded, duplicates pruned, shortest semantic command length, bounded solution count, termination reason, peak frontier/approximate memory and diagnostic wall time.

Ordinary authoring target: <=150k semantic states, <=1.5m transitions; named late profile only after instrumentation. Over-budget ladder: remove irrelevant states -> reduce branching -> simplify dependencies -> cut case. No bespoke incomplete pruning.

Validator may prove structural properties, never `fun`, `fair`, `readable`, `good value` or felt variety.

Runtime exposes no default dead-state oracle.

---

# 10. Frozen UX / presentation contract

Five facts remain recoverable:
1. Physical now;
2. Remembered;
3. exact Candidate;
4. whether memory will be overwritten;
5. when remembered state becomes Physical.

Canonical visual sequence is `Preview -> Confirm memory write -> perceptible committed-but-not-yet-resolved beat -> leave/end observation -> Physical resolution -> world consequences`.

Physical/Remembered/Candidate use redundant shape/pattern/icon/text cues; color and audio are supplemental only.

The world remains primary puzzle surface. No global Frame/form matrix, detached form-management screen or full future-state table.

Only targeted object's Candidate expands during two-object play; other object keeps compact identity + Physical/Remembered facts. Stable object identity token survives all form changes.

Dynamic inputs must remain physically visible/inspectable in Frame context. UI panels may never cover target object, named input relation and old->new comparison simultaneously on target display.

Hints are authored causal facts H0–H3; after tutorial they cannot reveal next command, correct Frame/form, dead-state truth or solver-derived move.

---

# 11. Frozen input / accessibility / Deck contract

Complete required paths:
- controller only;
- keyboard only;
- mouse + keyboard;
- Steam Deck built-in controls at 1280×800.

Frame target choice uses authored semantic focus order, never precision aiming. Camera is presentation only.

Remapping preserves recoverable Confirm, Cancel/Back, navigation and Pause. A visible non-timing modifier layer may expose Undo/Redo/Inspect.

Before bulk content population, a representative demo slice must be completed through all four input paths including remap/recovery tests.

Accessibility baseline:
- reduced motion;
- high contrast/redundant patterns;
- complete audio-off play;
- text scaling/localization expansion;
- flash/shake reduction;
- camera sensitivity/inversion;
- remapping;
- unlimited Undo/Redo;
- replayable tutorial facts.

Commit and resolution remain distinguishable when animation is minimized, audio is muted and color is ignored. No accessibility setting changes Candidate semantics.

---

# 12. Frozen pacing / traversal contract

Mature difficulty comes from causal decisions, not route length.

For C20+, representative first clears where >~33% of active puzzle time is repeated already-understood safe traversal with no new observation, movement, receiver or preservation decision trigger redesign: shorten route, open a rule-consistent solved-state shortcut, or cut case.

No global fast-travel puzzle mechanic is added.

---

# 13. Frozen persistence / content compatibility

Only stable committed gameplay boundaries are durable.

Persistence uses verified generation-based writes with prior verified backup and fault injection. Recovery chooses exact newest verified compatible generation or prior exact committed generation, never a hybrid.

Case win, unlock/profile mutation and branch transition share one durable logical transaction/journal boundary.

Durable saves record schema version, content version and global rule-schema version. Publicly referenced IDs become compatibility surface. IDs may not be reused for materially different semantics.

Migration is explicit/versioned. Unsupported incompatible active-case state may fall back to transparent safe case restart only after preserving valid profile progress; no heuristic state surgery.

---

# 14. Frozen Cloud / demo-import contract

Offline local correctness outranks Cloud convenience.

Cloud never structurally merges divergent active puzzle branches. Explicit monotonic profile facts may merge under documented commutative rules. Divergent active branches must preserve both and use non-spoiler conflict choice metadata; wall-clock newest-wins is insufficient.

**Cloud is cut from release if branch-integrity fixtures fail.**

Demo -> full import is versioned/idempotent and limited to whitelisted language/settings/accessibility, recognized semantic remaps, tutorial acknowledgements and monotonic demo facts. No active demo puzzle state, remembered forms or guessed campaign completion imports into campaign.

---

# 15. Frozen commercial model

Premium single purchase. No ads, MTX, paid hints, currencies, dailies, streaks, FOMO, battle pass, mandatory account or always-online requirement.

Working US list target: **$17.99**.
Release-review band: **$14.99–$19.99**.

This is explicitly an empirical hypothesis. Final pricing/value claims require measured non-expert duration, surviving case count, perceived causal variety, polish and demo intent. Optional remixes count as zero promised value until built and validated.

Campaign unlock structure from Phase 7 remains. Hints are free. Mastery is causal/optional and never speed/no-Undo grind. Target achievements 14–20, bounded and non-grindy.

Store framing must foreground authored persistent observation/memory, not generic perspective manipulation. A representative trailer/demo must show consequential overwrite, not only spectacle.

---

# 16. Frozen technical direction

Initial implementation baseline checked 2026-08-30: **Godot 4.7.2-stable, GDScript-first**. Official archive listed 4.8-dev4 as development-only at freeze time.

This engine version is a bootstrap baseline, not gameplay canon. A newer stable may be evaluated at implementation start only with rollback point plus full domain/save/input/Deck regression.

Architecture is strict:
- Domain Core = canonical state, commands, Candidate, legality, solver semantics, history, serialization/hash;
- Presentation = world/UI/camera/audio/animation only;
- Platform Adapter = Steam/Cloud/achievements/device metadata only.

Domain runs headlessly and imports no Presentation/Platform authority.

No production implementation begins inside the factory.

---

# 17. Frozen scope / cut ladder

If reality contradicts paper assumptions, repairs occur in this order:
1. simplify presentation while preserving causal sequence;
2. simplify individual cases/poses/branching;
3. cut weak/near-isomorphic cases;
4. cut optional remixes;
5. cut Cloud if integrity is not proven;
6. adjust final price/value claims to measured package;
7. reduce product scope through explicit review;
8. kill product if mature felt variety or core comprehension fails.

Forbidden repair: invent unrelated mechanics, free-camera authority, third critical memory, additional dynamic-input complexity, grind, procedural filler, combat, precision platforming or private per-case rules to rescue content count.

---

# 18. Empirical gates retained — explicitly NOT paper-PASS

Implementation/playtest must resolve at minimum:
- exact Candidate/form prediction after tutorial;
- zero unpreviewed camera/pixel authority;
- mute-clip comprehension of persistent remembered-form rule and authored Frame authority;
- >=3 felt mature planning families in representative slice;
- two-object readability without detached table;
- reduced-motion/non-audio causal comprehension;
- keyboard-only comfort;
- controller/keyboard/mouse+keyboard/Deck full-path proof;
- mature anti-enumeration behavior;
- transformation/art production cost under reusable-asset ceiling;
- solver production cost/frontier profile;
- final strong-case count/diversity;
- measured non-expert first-clear duration;
- DEMO06 readability and full-game interest;
- final price/value perception;
- Cloud branch integrity if Cloud is to ship.

Failed empirical gates trigger the cut ladder or kill condition; they do not authorize silent redesign of the core rule.

---

# 19. Canonical authority order after freeze

1. `GAME7_FINAL_FREEZE.md` — final frozen authority and explicit narrowing.
2. `GAME7_ADVERSARIAL_REVIEW.md` — P10 repairs/kill gates where not repeated here.
3. `GAME7_WHOLE_GAME_SIMULATION.md` — P9-R1..P9-R27 where consistent with P10/freeze.
4. `GAME7_PRODUCT_THESIS.md` — product identity detail.
5. `GAME7_MECHANICAL_ARCHITECTURE.md` — exact domain detail.
6. `GAME7_CONTENT_ARCHITECTURE.md` — campaign/data/validation detail.
7. `GAME7_UX_PRESENTATION_ARCHITECTURE.md` — presentation/input/accessibility detail.
8. `GAME7_ECONOMY_COMMERCIAL.md` — commercial/progression detail.
9. `GAME7_TECHNICAL_SPEC.md` — implementation architecture detail.
10. Tournament/research files — rationale/history only, never active gameplay authority.

Where documents conflict, higher authority wins. No lower file may silently broaden a narrowed ceiling.

---

# 20. Freeze acceptance

A fresh implementation session can determine without inventing important gameplay:
- what the player does and why;
- exact observation/overwrite/resolution lifecycle;
- Candidate authority inputs and forbidden inputs;
- object/form/pose/receiver semantics;
- multi-object order and hard ceilings;
- deterministic transaction ordering;
- Undo/Redo/idempotency;
- campaign progression/families/diversity;
- anti-dominant/anti-enumeration requirements;
- UX/input/accessibility behavior;
- persistence/Cloud/demo import boundaries;
- commercial boundaries;
- technical architecture and validation;
- empirical gates and kill responses.

No fatal paper contradiction remains.

**PHASE 11 — SPECIFICATION FREEZE: COMPLETE.**
**DESIGN COMPLETE = YES.**
**PRODUCTION IMPLEMENTATION STARTED = NO.**

## NEXT ACTION
Attempt migration to preferred dedicated repository `Mikayilzade/last-known-shape`. If it exists, copy the full frozen Game #007 package, add/verify `IMPLEMENTATION_START_HERE.md`, `IMPLEMENTATION_STATUS.md`, CI/email-noise policy, verify migration integrity, then remove only the Game #007 factory safety copy and advance to Game #008. If the repository does not exist or creation is unavailable, record migration pending, retain all `GAME7_*` files as a frozen NON-ACTIVE safety archive, update `GAME_INDEX.md`, and immediately advance `STATUS.md` to Game #008 Phase 1. Pending migration must not block the factory.