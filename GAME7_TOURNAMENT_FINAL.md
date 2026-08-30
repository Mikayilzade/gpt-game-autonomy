# GAME #007 — CONCEPT TOURNAMENT — FINAL DUEL

Last updated: 2026-08-30
Phase: **2 — Concept Tournament**
Run: **3 / FINAL**
Selected concept: **G7C02 Last Known Shape**
Production implementation started: **NO**

## Decision
Finalists: G7C02 Last Known Shape, G7C03 Command Lag, G7C10 Recurrence Department.

Forced-selection threshold is cleared by **G7C02 Last Known Shape**. It has no unresolved paper-level fatal flaw after replacing free-camera interpretation with authored deterministic Observation Frames, and it leads on (A) ownable hook/market legibility while remaining competitive on (B) systemic depth. Command Lag leads on implementation simplicity, but its world-space readability risk and programming-puzzle perception are larger product risks. Recurrence Department is elegant but temporal-repeat competition makes its hook less ownable.

Fresh search on 2026-08-30 found no obvious title-level exact-match game for these internal labels; this is not trademark clearance. Historical temporal puzzle comparators such as Timelie/Causality reinforce that visible time manipulation is established territory; Last Known Shape's strongest differentiation is persistent remembered-form authority, not generic time control.

# 1. LAST KNOWN SHAPE — six canonical blueprints

## L01 Tutorial — Remembered Bridge
One object, two authored forms: BLOCK and LONG. Player enters Frame A; exact LONG candidate is previewed; OBSERVE commits; after leaving direct observation the object resolves to LONG and bridges a gap. Re-observing from default frame returns BLOCK. Teaches explicit commit and persistence.

## L02 Early — Useful Overwrite
Same object must first be LONG to cross, then COMPACT to enter a lift socket. Two frames, no occlusion. Correct solution is preserve -> exploit -> overwrite -> exploit. Kills the belief that one best form should be kept forever.

## L03 Mature A — Mask Choice
A fixed foreground mask in Frame B yields FORK form; Frame C yields TALL. FORK simultaneously holds two contacts but blocks a corridor; TALL actuates one vertical receiver and leaves corridor open. Player chooses form based on downstream affordance rather than apparent size.

## L04 Mature B — Observation Order
Objects A and B interact only through ordinary physical placement. A in TALL form becomes an authored occluder within B's Observation Frame, changing B's candidate from WIDE to HOOK. B must be observed while A is TALL; then A must be overwritten COMPACT without re-observing B. Order is causal and visible.

## L05 Mature C — Preserve Through State Change
Object O has LONG, TALL, COMPACT. LONG can bridge the final return path but if committed too early physically blocks access to the COMPACT frame. TALL actuates a lift; COMPACT travels in lift; LONG is committed from the far side. This defeats largest-form-first and requires planning several remembered states.

## L06 Late Synthesis — Two Memories, Three Frames
Two objects, three frames, one shared authored occlusion relation. A must be FORK to hold dual contacts while B is observed as HOOK; B then moves a shutter that exposes A's COMPACT frame; A is overwritten and transported; finally B is deliberately overwritten, releasing contacts in the required order. No new primitive is introduced. Late complexity comes from preservation, overwrite timing, observation order and physical affordance composition.

### Primitive growth
Tutorial: 1 object, 1 meaningful frame, 2 form states, OBSERVE + ordinary movement.
Early: 1 object, 2 frames, 2–3 forms.
Mature: 1–2 objects, 2–3 frames, fixed masks/occlusion, max 3 useful forms/object.
Late ceiling: 2 simultaneously reasoning-critical objects normally; 3 only after readability proof; <=4 frames in one case; same single OBSERVE commit verb.

### Compact deterministic state model
Per object: `{object_id, physical_pose_slot, remembered_form_id, observation_status, active_affordance_state}`.
Per frame: `{frame_id, eligible_object_ids, deterministic_transform_id, fixed_mask_state, preview_form_id}`.
Global: player discrete traversal/interaction state, receiver/door/lift states, history revision.
`OBSERVE(frame, object)` is legal only at authored frame conditions and computes candidate form from explicit transform + canonical occluder states. Preview and commit use the same pure function. No pixels, arbitrary camera ray geometry or hidden image classifier are authoritative.

Solver risk: moderate but bounded if physical poses, forms and frames are discrete. Geometry collision may be presentation-derived only where possible; puzzle authority uses authored form affordances.

### Error taxonomy
Explainable: overwrote a useful form too early; chose wrong frame; moved an occluder before observing; blocked own access; preserved a form too long.
Unacceptable/arbitrary: game committed a silhouette different from preview; tiny camera motion changed form; unseen pixel occlusion mattered; player cannot identify which observation overwrote memory. These are specification violations, not intended difficulty.

### Hour-4 repetition attack
Attack: every puzzle becomes `find correct frame -> observe -> carry shape to socket`.
Defense requirements: mature content must rotate dominant causal families: preservation/overwrite, access self-block, mask affordance tradeoff, multi-object observation order, occluder state dependency, destructive re-observation, staged transport, coupled receivers. No three consecutive mature cases may share the same dominant skeleton. New forms alone do not count as variety.

### Burden
Authoring: medium-high; each case needs exact frame/form causality and anti-shortcut validation.
Art: medium; stylized modular objects/forms and authored frames are reusable, but transformations must look intentional.
QA: medium-high; preview/commit identity and occlusion determinism are existential.
Technical: medium, substantially reduced by discrete frame authority.

### Demo conversion thesis
6 cases / 20–30 minutes. The demo must reach preserve->overwrite and one two-object order puzzle; stopping after the magical first transformation would sell a gimmick rather than the full reasoning product. End demo on a visible two-object causal chain and offer immediate full-game continuation.

### Store hook
**Observe an object in one exact form, walk away, and that last remembered shape becomes physically real — until you dare to look again.**

### Six-second silent GIF
0–2s: marked frame previews a block as a long bridge outline.
2–3s: OBSERVE flash locks outline.
3–5s: player steps away; block resolves into bridge and player crosses.
5–6s: second frame previews compact form while bridge remains visibly behind.

# 2. COMMAND LAG — six canonical blueprints
C01: one OPEN command delay 2; movement advances turns.
C02: delays 1 and 3; synchronize carrier with gate.
C03: issue command before sensor becomes occupied; maturity uses later state.
C04: A must mature before B becomes issue-legal while C must be issued before A closes access.
C05: two queued commands on same actuator with intervening rotation changes semantic result.
C06: four bounded pending commands across three machines; player physically moves between issue stations and cannot front-load all commands.

Primitive growth: 1 machine/1 pending -> 3–4 machines/max 4 pending/max delay horizon 5; 5–7 reusable verbs ceiling.
State model: machine states, pending records `{target, verb, maturity_turn, stable_id}`, player location, turn, issue/maturity predicates. Excellent determinism/solver profile.
Errors are explainable when countdown, issue condition and maturity consequence are visible; arbitrary if commands fail because of hidden maturity ordering.
Hour-4 attack: becomes arithmetic countdown scheduling. Defense: future-legality inversion, physical access, queue interference and state-dependent command semantics, but these raise UI load.
Burden: authoring medium-low, art medium, QA medium, technical low-medium. Strongest implementation profile.
Demo: 6 cases / 25–35 min; must prove anti-frontload before ending.
Store hook: **Every machine obeys you later. Issue commands now, move through the facility, and make their delayed consequences collide at exactly the right future state.**
Silent GIF: hit OPEN(3); hit ROTATE(2); ticks advance; ROTATE redirects carrier; OPEN matures as carrier arrives.

Fatal-product risk retained: if 3–4 pending commands require a detached timeline to reason reliably, the physical fantasy collapses into programming UI. This is prototype-only but material.

# 3. RECURRENCE DEPARTMENT — six canonical blueprints
R01: press in Room A; one turn later room repeats press locally.
R02: seed recurrence, move object before repeat so same action affects changed target state.
R03: harmful recurrence must be overwritten/cancelled by a different qualifying local action under one global rule.
R04: two rooms' recurrences overlap; order is stable and architectural cues show pending state.
R05: recurrence in A changes local state that makes B's later recurrence beneficial; waiting blindly fails because A repeats again under bounded persistence rule.
R06: three rooms max, each <=1 semantic token; solve by seeding, redirecting current local targets, and deliberately replacing one dangerous recurrence.

Primitive growth: 1 room/token/action -> 3 relevant rooms, <=1 token each, small qualifying action vocabulary. Determinism excellent.
State model: per-room recurrence token `{semantic_action, due_turn, persistence/overwrite state}`, current local target state, stable room ordering, player/object state.
Errors explainable if every room exposes next semantic recurrence and target mapping; arbitrary if replay target selection is hidden.
Hour-4 attack: seed useful actions then wait. Defense requires persistent/harmful repeats, overwrite and state-mediated target changes; viable but bookkeeping rises quickly.
Burden: authoring medium, art low-medium, QA medium, technical low.
Demo: 6 cases / 20–30 min ending on two-room state-mediated recurrence.
Store hook: **Every room remembers what you did there and does it again later — arrange the building so yesterday's action becomes today's solution.**
Silent GIF: press room switch; leave; room pulses; delayed press fires after crate moved; door opens remotely.

Product risk: temporal echo/replay is already a recognizable puzzle category, so differentiation depends heavily on explaining `room repeats semantic action, no clone/path replay`.

# 4. Head-to-head
Scores /5 after concrete blueprint proof:

| Criterion | Last Known Shape | Command Lag | Recurrence Dept. |
|---|---:|---:|---:|
| Ownable hook / store legibility | **5.0** | 4.0 | 4.0 |
| Silent GIF proof | **5.0** | 4.0 | 4.0 |
| Systemic depth without feature growth | **4.5** | 4.5 | 4.0 |
| Determinism / solver simplicity | 4.0 | **5.0** | **5.0** |
| Content scalability | 4.0 | **4.5** | 4.0 |
| Portfolio differentiation | **5.0** | 4.5 | 4.5 |
| Low implementation/content risk | 3.5 | **4.5** | 4.5 |
| Hour-4 anti-repetition evidence | **4.5** | 4.0 | 3.5 |
| Demo conversion potential | **5.0** | 4.0 | 4.0 |

Decision categories from threshold:
A ownable hook/market legibility: **Last Known Shape wins clearly**.
B systemic depth without bespoke growth: **Last Known Shape / Command Lag near tie**, with LKS having more visually distinct causal families.
C implementation/content risk: **Command Lag wins**.

Last Known Shape therefore leads at least two decision dimensions (A, and B by product-level causal variety) while retaining an acceptable bounded technical architecture. **SELECT G7C02.**

# 5. Explicit empirical gates carried forward
EG7-01: after one tutorial, >=80% target testers predict committed form from preview before OBSERVE.
EG7-02: zero cases where authoritative form differs because of unpreviewed camera/pixel details.
EG7-03: 15-second mute clip is correctly described as `last observed shape becomes real/persistent` by a strong majority without explanation.
EG7-04: mature 30-minute slice demonstrates at least 3 causal families, not frame-to-socket repetition.
EG7-05: two-object observation order remains readable without detached state table.
EG7-06: transformation presentation does not create motion-sickness/flash dependence; reduced-motion path preserves causality.

# Phase-2 result
**G7C02 Last Known Shape selected. Phase 2 COMPLETE.**

Command Lag is the strongest reserve but is not canon. Recurrence Department is rejected for this slot and may not be silently reused later without fresh opportunity research.
