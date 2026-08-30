# GAME #007 — LAST KNOWN SHAPE — WHOLE-GAME SIMULATION ON PAPER

Last updated: 2026-08-30
Phase: **9 — Whole-Game Simulation on Paper**
Selected concept: **G7C02 Last Known Shape**
Production implementation started: **NO**
DESIGN COMPLETE: **NO**

Authority order remains: Product Thesis -> Mechanical Architecture -> Content Architecture -> UX/Presentation -> Economy/Commercial -> Technical Specification. This Phase-9 file records end-to-end simulation failures and repairs; it may narrow ambiguous behavior but may not invent unrelated mechanics.

---

# 1. Simulation goal

Run the paper game as if it already existed, from first boot through campaign completion and hostile recovery/platform states. The purpose is not to prove fun on paper. It is to expose contradictions, hidden state, tutorial gaps, dominant behaviors, save/history corruption risks, input dead ends and content pacing problems before adversarial review.

Simulation assumptions:
- canonical mechanics from Phase 4 are exact;
- C01–C34 structure/families from Phase 5 exists at blueprint level;
- UX from Phase 6 is available;
- commercial progression from Phase 7 is active;
- technical architecture from Phase 8 is followed exactly;
- empirical gates remain unpassed until prototype/playtest.

---

# 2. First boot -> C01 -> first 10 minutes

## Walkthrough
1. Player launches offline with controller connected.
2. Accessibility-safe first boot exposes language/display/input before any required cinematic.
3. New Game opens C01 quickly.
4. Player sees one transformable object and one clearly authored Observation Frame.
5. Frame focus selects the one eligible object.
6. Preview shows Candidate plus current Remembered state.
7. Confirm writes memory; object remains physically unchanged while directly observed.
8. Tutorial says/depicts leave Frame to resolve.
9. Player steps away; object becomes remembered form and creates traversal affordance.
10. Player uses it and completes C01.
11. C02 demonstrates Preview/Cancel does nothing.
12. C03 creates first consequential overwrite.

## Failure found: commit/resolve can feel like one action
If animation begins immediately on Confirm while player still stands in the Frame, player may infer that Confirm itself physically transforms the object, erasing the product's important remembered-vs-physical distinction.

### P9-R1 — mandatory perceptible committed-observed beat
After the first successful commit in C01–C03, Presentation must preserve a perceptible stable beat where:
- memory token clearly changed;
- physical object clearly has not yet resolved;
- leave/end-observation cue is visible;
- player remains in control.

This beat may be very short after literacy is proven, but tutorial cases may not visually collapse commit and leave-resolution into one undifferentiated morph.

---

# 3. C02–C05 overwrite literacy / strategic mistakes

## Walkthrough
Player previews second form, cancels, sees no mutation. Later the player commits a new form, destroying prior memory. C05 permits a legal but poor overwrite; Undo restores the earlier memory/state.

## Failure found: `OVERWRITE` may be read as destructive confirmation warning
A modal warning every time remembered form changes would train players to treat overwrite as exceptional/dangerous and slow the central repeated verb.

### P9-R2 — overwrite is neutral, not modal
`OVERWRITE` remains an always-visible factual state comparison, never a default extra confirmation dialog. Confirm remains the one deliberate commit action. Only destructive non-puzzle actions such as abandoning a profile may use modal confirmation.

## Failure found: immediate Undo can hide why the bad state is bad
If C05 tells player to Undo as soon as a legal poor choice happens, the game becomes correctness policing.

### P9-R3 — bad-state pedagogy waits for causal evidence
C05 and later cases must allow the player to experience the downstream consequence before any generic Undo reminder. The system must not label a legal choice `wrong` at commit time.

---

# 4. C06–C10 affordance conflict

## Walkthrough
Forms begin to differ by bridge/fit/block/reach/contact affordances. C10 requires preserve -> exploit -> relocate -> overwrite -> exploit.

## Failure found: form icons can become a detached lookup table
If Expanded Inspect exposes every possible affordance of every possible form, the player can solve by menu comparison rather than physical experimentation.

### P9-R4 — inspect shows current-known facts, not universal form catalog
Expanded Inspect may show affordances already observed/taught for the current Physical/Remembered forms. It must not reveal unencountered form outcomes or compile a complete future-state matrix. Frame Preview may show only immediately knowable deltas for the exact candidate.

---

# 5. C11–C15 dynamic input / authored occluder simulation

## C11 first state-dependent candidate
Player uses Frame B on Object O. Candidate changes because a named physical input object is in a qualifying pose/form state.

## Failure found: candidate change may appear arbitrary if input is merely listed in UI
A label `Input: Object A` is insufficient if the physical relationship cannot be seen.

### P9-R5 — dynamic input requires world-space causal bridge
Every dynamic occluder/input case must visually connect the named input to the Frame's authored observation volume/mask through world geometry, framing rails/light-plane/inspection outline or equivalent redundant presentation. UI naming supplements this; it cannot be the sole explanation.

## C15 preserve after restoring occluder
Player changes A, observes B under A, then changes A back while B's remembered form persists.

Simulation succeeds under Phase-4 rule that B reads A only at B's commit transaction and never updates retroactively.

## Failure found: re-entering B's Frame could be mistaken for automatic re-observation

### P9-R6 — frame entry never visually resembles an automatic write
On re-entry, Candidate may appear immediately, but Remembered remains visually separate and no write pulse/sound/memory-token replacement occurs until explicit Confirm. This is especially mandatory from C11 onward where candidate may differ because inputs changed.

---

# 6. C16–C19 two-object teaching

## C16
Two objects exist, no cross-dependency. Quick Inspect shows two stable object identities.

## C17
A's physical form changes access to B's Frame.

## C18
A becomes explicit candidate input for B.

## C19
Observe B under A, then overwrite A; B must remain unchanged.

## Failure found: object identity can be lost when two objects share similar forms

### P9-R7 — persistent object identity outranks form identity
Each reasoning-critical object receives a stable non-color identity token (shape badge/pattern/letter-like icon independent of localized name). Physical, Remembered and Candidate displays always carry this object token. Transforming A into a form visually similar to B may not erase which memory belongs to which object.

## Failure found: controller focus may switch target after A changes legality
If target cycling list is filtered live and focused target disappears, arbitrary focus migration can cause accidental B commit.

### P9-R8 — legality invalidation cancels commit context safely
If the currently previewed target becomes illegal before Confirm due to a canonical state change, Preview invalidates, no commit occurs, and semantic focus returns to a deterministic safe target or Frame root. The game never silently retargets Confirm to a different object.

This matches Phase-4 stale/mismatch rejection while giving it exact UX behavior.

---

# 7. C20–C22 coupled order / transition to mature shelves

Simulation uses two objects, relocation and receiver consequences. Player can solve C20 or C21 in either order after C19, then C22.

## Failure found: unlock flexibility could produce a perceived difficulty spike
If C20 and C21 emphasize different causal families and one is much harder, player may mistake the shelf for mandatory linear difficulty.

### P9-R9 — parallel cases display neutral recommended ordering without gating
Case Select may mark one newly unlocked parallel case as `Suggested next` based on authored pacing, while both remain available. It must not use stars/levels or imply the other is optional filler. This is presentation/progression metadata only.

---

# 8. C23–C28 mature preservation chains

Simulation of representative case:
- A remembered bridge state is preserved rather than overwritten at visible Frame;
- A is relocated;
- B changes mechanism access;
- later the skipped candidate becomes useful only after mechanism state changes;
- player returns and deliberately overwrites.

This passes anti-enumeration structurally.

## Blind-enumeration player simulation
Player visits every accessible Frame and commits every distinct candidate immediately.

Expected result: mature cases repeatedly destroy a needed remembered state or close later access. Free Undo permits experimentation without making enumeration optimal.

## Failure found: candidate browsing itself could expose all options at zero cost and reduce planning to memorizing a menu

### P9-R10 — target/candidate discovery remains embodied
The player may inspect any currently accessible Frame candidate freely, but the game does not provide a global list of all Frames/candidates in the case. Candidate knowledge is local to physically/semantically reaching that Frame; Quick/Expanded Inspect stores current memory facts, not a global candidate atlas.

---

# 9. C29–C33 late synthesis

No new primitive enters. Each case rotates dominant causal family. Mature cases require at least one later target whose value depends on earlier physical/world state.

## Failure found: late cases could become long because of traversal repetition, not reasoning depth
A correct multi-stage solution may require returning through already-solved physical routes several times.

### P9-R11 — traversal-tax content rejection rule
During later content validation/playtest, any mature case where more than roughly one third of first-clear active time is repeated already-understood traversal with no new decision must be shortened, add a rule-consistent shortcut activated by solved state, or be redesigned/cut. This is a content pacing gate, not fast travel as a new puzzle mechanic.

Tooling may record semantic movement count separately from observation/object decisions to flag candidates for review.

---

# 10. C34 capstone simulation

Frozen ceiling: two reasoning-critical objects, <=4 Frames, <=3 useful forms/object, at least two preserve/overwrite decisions separated by physical exploitation.

Paper route:
1. establish A form to gain B observation access;
2. use A as declared input to commit B form;
3. preserve B while deliberately overwriting A;
4. relocate/use A to alter mechanism state;
5. return through newly available route;
6. deliberately skip a tempting B candidate;
7. exploit preserved B;
8. later overwrite B for final receiver state;
9. reach goal with all consequences resolved.

No third object, timing, free camera, hidden candidate dependency or new receiver law is needed.

## Failure found: capstone temptation could be indistinguishable from ordinary irrelevant preview

### P9-R12 — late preserve decisions require visible consequence context
When C29+ asks the player to skip a legal candidate, the currently preserved form must have an already-readable downstream affordance/access relationship. The case cannot rely on `remember that this might matter later` without environmental evidence. Difficulty comes from planning among known consequences, not clairvoyance.

---

# 11. Excessive Undo/Redo simulation

Sequence: 200+ accepted moves/observations, repeated Undo to root, Redo forward, branch at midpoint, save/reload, further Undo.

Mechanical contract succeeds if immutable snapshots/hash are correct.

## Failure found: unlimited history + durable full snapshots may exceed practical memory/save size in pathological experimentation

### P9-R13 — implementation may compact history without changing player contract
Phase 8 may implement checkpoint + deterministic delta/history compaction internally once thresholds are profiled, provided:
- player-visible ordinary Undo remains effectively unlimited within active case;
- exact semantic hashes restore;
- save/load retains current branch history according to final persistence policy;
- compaction never crosses a boundary in a way that makes a previously available active-case Undo disappear without explicit product decision.

No numeric history cap is paper-frozen before profiling.

---

# 12. Duplicate / stale command simulation

Scenario A: same commit command arrives twice because input/platform retry occurs.
- first commits;
- second same ID/payload returns recorded result;
- no second overwrite/history node.

Scenario B: duplicate ID with changed payload.
- hard reject.

Scenario C: Preview computed at revision 18, object/world changes to revision 19, stale Confirm arrives.
- reject stale revision;
- refresh/cancel Preview;
- never commit a different candidate under old intent.

No contradiction found after P9-R8.

---

# 13. Crash matrix simulation

Crash points:
1. before temp save write;
2. mid-payload;
3. after complete write before verify;
4. after verify before promotion;
5. after promotion before manifest update;
6. during manifest update;
7. after preferred update before prior cleanup.

Expected recovery from Phase 8: newest fully verified compatible generation; otherwise prior verified generation.

## Failure found: campaign-completion fact and current branch could be persisted in different generations if profile and branch files commit independently

### P9-R14 — cross-file progression transaction boundary
Case completion, unlock/profile mutation and current-case branch transition must share one durable logical generation/manifest commit, or use a transactional journal that proves the set belongs together. Recovery may not produce `C34 animation seen but C34 clear missing`, nor `case clear recorded but required committed win state absent` if both facts are intended to become durable together.

Settings that are independent may persist separately.

---

# 14. Corrupt newest generation

Newest file has valid syntax but wrong hash: reject, use prior verified generation and show recovery notice.

Newest has valid checksum but object references nonexistent form due to content mismatch: schema/content compatibility validation rejects before activation.

## Failure found: a game patch can remove/rename content IDs that old saves use

### P9-R15 — shipped content IDs become durable compatibility surface
After public/demo save compatibility matters, gameplay IDs referenced by durable saves cannot be casually renamed/reused. Content migrations must map old IDs explicitly. Removed case content may remain migration-readable even if not directly selectable.

---

# 15. Steam Cloud divergent devices

Device A: player branches C25 state X.
Device B offline: same earlier ancestor branches C25 state Y and clears C26.
Cloud later sees both.

Profile clear facts may union where explicitly monotonic. Active C25 branch X/Y must not structurally merge.

## Failure found: silently choosing newest timestamp is unsafe under clock skew and can discard meaningful branch

### P9-R16 — Cloud active-branch conflict is explicit when ancestry diverges
When two verified active branches for the same case have divergent branch IDs/ancestry and neither is an exact ancestor with safely comparable generation provenance, do not choose by wall-clock timestamp alone. Preserve both conflict copies and ask the player to choose using non-spoiler metadata (device label where available, committed progress timestamp as advisory, case ID, command/history depth). If robust conflict UX/platform integration is not implemented, Cloud remains disabled for release.

---

# 16. Demo -> full import and re-import

Player completes DEMO01–06, customizes accessibility/remaps, buys full game.

Full game imports whitelisted settings/tutorial acknowledgements + demo_veteran. C01 remains uncleared. Second import attempt is idempotent.

## Failure found: importing a controller remap from demo may be invalid in full build if action vocabulary changed

### P9-R17 — remap import is semantic-action/version aware
Demo import maps bindings only for recognized semantic action IDs. Missing/new mandatory actions receive safe defaults and remap validation runs before acceptance. Imported config can never strand Confirm/Cancel/Pause/navigation.

---

# 17. Controller-only simulation

Flow C18:
- enter Frame;
- semantic focus selects legal A/B target deterministically;
- shoulders cycle target;
- Inspect Memory reachable;
- Confirm commits;
- Cancel exits preview;
- movement leaves Frame;
- Undo available.

## Failure found: one dedicated action each for Undo/Redo plus Inspect may pressure ordinary gamepads

### P9-R18 — binding layout may use a non-timing modifier layer
A semantic action layer/menu modifier is permitted for Undo/Redo/Inspect provided:
- no timing chord is required;
- state of modifier is visible;
- Confirm/Cancel remain unambiguous;
- all actions are reachable on standard gamepad and Deck;
- remapping can change it.

This is input ergonomics only; no gameplay semantic changes.

---

# 18. Keyboard-only simulation

Keyboard-only requires camera-turn bindings because mouse cannot be assumed. Core Frame target acquisition is semantic, so play remains possible.

## Failure found: ordinary 3D traversal with keyboard-only camera may be uncomfortable even if technically complete

### P9-R19 — empirical keyboard-only comfort gate
Vertical slice must test a complete keyboard-only path for an entire representative demo segment. If free-look traversal is needlessly cumbersome, camera/layout may use authored snap-turn/auto-alignment assistance. Such assistance may never alter Candidate authority.

---

# 19. Deck 1280x800 + text expansion

Two-object C19 with +40% localized text expansion, one-step increased text scale, candidate/remembered cards visible.

## Failure found: expanded panel can cover physical input relation even while satisfying percentage limits

### P9-R20 — panel occlusion is evaluated against causal subjects, not screen percentage alone
At Frame Preview, UI layout must avoid covering:
- target object;
- named dynamic input object/relationship cue;
- old->new form comparison.

If no fixed screen region satisfies this at 1280x800 + required scale, panel must reflow/collapse/move rather than obscure a causal subject. The prior ~30%/34% size targets are necessary but not sufficient.

---

# 20. Reduced-motion / non-audio simulation

All transformation audio muted. Reduced motion replaces morph with before/after outline + snap/dissolve. Memory commit and leave-resolution remain distinguishable via persistent visual state.

## Failure found: if commit and resolve both use similar outline flashes, reduced-motion path can blur them

### P9-R21 — reduced-motion has two distinct static causal markers
Memory commit and physical resolution must use different redundant icon/pattern/text transitions even with animation duration near zero. Audio may reinforce but is never required.

---

# 21. Localization expansion simulation

Long labels, invalid-command templates and Tutorial Facts expanded by +40%.

## Failure found: localized shape nouns can become too long for compact form comparison

### P9-R22 — form identity does not depend on noun fit
Compact UI prioritizes stable silhouette/icon token plus shortened localized display label with full localized name available in accessible expanded text. No truncation may make two forms indistinguishable. Translator notes define glossary semantics.

---

# 22. Solver-budget exceedance simulation

A late two-object case reaches 400k states under ordinary profile; a tempting author fix is bespoke pruning using intended solution knowledge.

Rejected.

### P9-R23 — budget failure has fixed escalation ladder
When a case exceeds target:
1. inspect accidental state dimensions / derived-state duplication;
2. remove irrelevant slots/frames/forms;
3. simplify causal structure while preserving dominant family;
4. use named capstone budget profile only if readability/content value justifies it;
5. cut case.

No case-specific semantic pruning, hidden solver-only rule or intended-solution oracle may enter Domain Core.

---

# 23. Save during preview / case win transition

Player previews candidate, then application exits. Since preview is non-canonical, Continue returns to latest committed boundary with no remembered-form mutation. Acceptable.

Player clears case, application exits during completion animation. P9-R14 requires win + unlock facts already durable before completion screen transition.

### P9-R24 — completion UI waits on verified logical save commit
The case-won semantic state resolves immediately, but transition that invites `Continue` to newly unlocked content occurs only after the small logical completion generation is successfully queued/verified according to persistence policy. UX must avoid a long blocking spinner; failure retains retry/recovery-safe state and does not pretend unlock was durable when it was not.

---

# 24. Hostile legal play / unusual interaction sequence

Player repeatedly:
- enters/leaves Frame without commit;
- commits same remembered form repeatedly;
- moves object away/back;
- inspects both objects rapidly;
- Undo during presentation animation;
- opens Pause mid-animation;
- switches device.

## Repair: semantic state always wins

### P9-R25 — presentation cancellation/snap contract
Undo/Redo/Restart/Load during non-authoritative animation first cancels/snaps Presentation to a canonical boundary, then applies the requested semantic/history operation. No input queue may replay a stale Confirm after the snap. Device switching preserves semantic focus ID where still legal, otherwise applies deterministic safe-focus rule.

---

# 25. Post-clear / replay simulation

C34 clear records Campaign Complete. Player has 31–33 other clears due to bounded bypass. Case Select exposes remaining main cases. All Main Cases is separate. Optional Insights/remixes do not gate campaign.

## Failure found: `Campaign Complete` at C34 while skipped cases remain can look like those cases are disposable side content

### P9-R26 — completion copy distinguishes ending from full main-case completion
C34 completion messaging: campaign arc complete, with remaining authored main cases clearly listed as unresolved main cases rather than `bonus`. `All Main Cases` is a separate completion state. No percentage/grade is used to shame bypass.

---

# 26. Commercial/demo simulation

Mute 15–30s store clip shows preview -> commit -> leave -> physical form -> use -> second candidate threatening overwrite. DEMO06 demonstrates two-object order.

Paper simulation cannot PASS EV7 hook/value gates.

### P9-R27 — store/demo claims wait for empirical proof
Until EG7/EV7 tests run, store copy may state the literal mechanic but must not claim hours, broad replayability, Steam Deck verification, Cloud availability, or validated causal variety beyond what implementation/testing confirms.

---

# 27. Whole-game contradiction summary

No fatal paper contradiction found. The central mechanic remains coherent through C34 and technical/recovery flows.

Repairs retained as canonical Phase-9 constraints:
- **P9-R1** perceptible commit-before-resolution beat;
- **P9-R2** neutral non-modal overwrite;
- **P9-R3** bad-state pedagogy waits for consequence;
- **P9-R4** no universal future-form lookup table;
- **P9-R5** dynamic input needs world-space causal bridge;
- **P9-R6** frame entry never resembles automatic write;
- **P9-R7** persistent object identity independent of form;
- **P9-R8** target invalidation safely cancels, never silent retarget;
- **P9-R9** suggested order for parallel cases without gating;
- **P9-R10** candidate discovery remains embodied/local;
- **P9-R11** reject traversal-tax mature cases;
- **P9-R12** preserve decisions require visible consequence context;
- **P9-R13** internal history compaction allowed only with exactness/player-contract preserved;
- **P9-R14** case win/unlock/branch transition share durable logical transaction;
- **P9-R15** shipped content IDs are save-compatibility surface;
- **P9-R16** divergent Cloud branch conflict explicit; timestamp alone insufficient;
- **P9-R17** demo remap import action/version aware;
- **P9-R18** visible non-timing input modifier layer allowed;
- **P9-R19** keyboard-only comfort empirical gate;
- **P9-R20** Deck panel cannot obscure causal subjects;
- **P9-R21** reduced-motion commit/resolve markers remain distinct;
- **P9-R22** form identity survives localization length;
- **P9-R23** fixed solver-budget failure ladder;
- **P9-R24** completion transition follows verified logical save;
- **P9-R25** presentation snap/cancel before history/load operations;
- **P9-R26** campaign-vs-all-main completion wording;
- **P9-R27** commercial/platform claims wait for empirical proof.

---

# 28. Phase-9 result

**PHASE 9 — WHOLE-GAME SIMULATION ON PAPER: COMPLETE.**

Simulation covered first boot/first 10 minutes, overwrite literacy, C11 dynamic input, C16–C19 two-object teaching, mature preservation chains, C34, blind enumeration, excessive Undo/Redo, stale/duplicate commands, save-crash/corruption, divergent Cloud devices, demo import/re-import, controller/keyboard, Deck + text expansion, reduced-motion/non-audio, localization, solver budget failure, hostile legal interaction and post-clear state.

27 explicit repairs were found and reconciled without adding a new gameplay primitive. No fatal paper blocker remains, but empirical gates remain genuinely open.

## NEXT ACTION
Phase 10 — Adversarial Review. Attack Last Known Shape destructively across at least: one-gimmick/repetition risk; perspective-game misread; observation-frame/menu detachment; dominant strategies; blind candidate cycling; form/object visual ambiguity; two-object bookkeeping; dynamic-input arbitrariness; content authoring burden; solver/state explosion; traversal tax; Undo/history memory; persistence/content migrations; Cloud conflicts; demo/full import; controller/keyboard/Deck; reduced-motion/non-audio/localization; tutorial/hint oracle risk; value/price/demo conversion; engine/platform assumptions; cross-spec contradictions. For every surviving issue, create an explicit repair or kill condition. Then determine whether Phase 11 freeze is justified.