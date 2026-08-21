# GAME #004 — PHASE 10 ADVERSARIAL REVIEW

Last updated: 2026-08-21
Factory run: **14**
Phase: **10 — Adversarial Review**
Working continuity name: **HUSHLINE** — RETIRED AS COMMERCIAL CANDIDATE; may remain only as internal historical codename until replacement
Phase status: **COMPLETE WITH REQUIRED REPAIRS / READY FOR PHASE 11 RECONCILIATION**
Production implementation: **NOT STARTED**

This review attacks the complete Phase-3 through Phase-9 design as if trying to prevent a weak, repetitive, overexplained, unreadable or technically ambiguous game from reaching specification freeze. It does not add a second gameplay pillar. Findings are classified as **KEEP**, **CUT**, **REPAIR**, or **EMPIRICAL GATE**. Normative corrections are recorded in `GAME4_PHASE10_AMENDMENTS.md` and override conflicting earlier wording until Phase 11 integrates them into the final freeze.

## 1. External pressure refreshed on 2026-08-21

Fresh checks confirm that neither `sound matters in stealth` nor `visible acoustic propagation` is a marketable novelty claim by itself. Current/durable examples include `Stifled`, audio-centric 2026 releases such as `Peek`, and general sound-occlusion/path tooling. The defensible product identity remains narrower: **physically move one world-space barrier so a chosen listener hears an action while another does not, then exploit the reaction through direct infiltration**.

The commercial working title is now a confirmed avoid rather than merely a soft risk. Current search finds:
- Apple App Store: `Hushline: Chat Story`, an active interactive-story product;
- `hushline.net`, an active audio-generation service;
- a 2026 browser experiment named `Hush line`;
- other current software/services using the same or near-identical name.

This is not legal/trademark clearance, but it is enough to **retire HUSHLINE from commercial consideration**. Phase 11 must select a replacement working title after collision screening; no fiction or mechanic may be bent to preserve this name.

Sources refreshed:
- https://apps.apple.com/us/app/hushline-chat-story/id6758482950
- https://hushline.net/
- https://billiem.uk/choice/experiments/2026-07-11-luna-high-hushline/
- https://store.steampowered.com/app/3575190/Peek/

---

# 2. Fun / verb-frequency attack

## Attack
The game can be intellectually clean while its signature physical verb is a chore. The barrier is large, rail-bound and local/direct. If the player repeatedly walks to a handle, grabs, slides, snaps, walks away, then repeats, the mechanic can become a slow maintenance task wrapped around the actual interesting acoustic decision.

The existing paper traces average roughly 1–2 meaningful barrier edits per minute in dense situations and less in exploratory stretches. This is healthy only if each edit has a tactile decision and immediate consequence.

## Failure modes
1. **Dead travel to the rail** — player already knows the correct slot but must spend several seconds commuting to perform it.
2. **Long drag animation** — physicality becomes latency.
3. **Slot enumeration** — player grabs the barrier and cycles every slot while watching HEARS/DOES_NOT_HEAR until one turns favorable.
4. **Setup separation** — solve acoustics first, then execute infiltration as a second phase.
5. **Exposure frustration** — local manipulation is theoretically active but direct detection punishes experimentation so harshly that players retreat to safe preview loops.

## Verdict
**KEEP the local/direct barrier. DO NOT remote-control it.** Remote control would fix friction by destroying the product fantasy.

**REPAIR:** mature encounter validation must reject safe slot-enumeration rooms. If every strategically relevant slot can be previewed from one permanently safe manipulation position with no traversal/exposure/state change, the encounter is too graph-like unless it is an early teaching case.

**EMPIRICAL GATE:** graybox players should describe barrier handling as part of the infiltration decision, not as travel tax. Target median grab→meaningful snap interaction below roughly 2–3 seconds once in reach; exact feel remains implementation empirical.

---

# 3. `Graph puzzle disguised as stealth` attack

## Attack
The acoustic model is deliberately a small integer graph. Exact preview is strong accessibility and fairness design, but also risks revealing the underlying abstraction so completely that optimal play becomes graph inspection followed by execution.

## What protects the fantasy
- graph edges are physical openings, never hidden lines;
- barrier is a world object, not an edge toggle;
- the player must move through the same space being reasoned about;
- listener reactions create traversal windows;
- objective/door/source state can change during play;
- prediction is action-specific and local, not a global solved-state optimizer.

## Hard boundary
The UI must **never** present a global node-link diagram, all-pairs matrix, automatic best-slot recommendation, or ranked list of safe actions. Exact prediction answers the consequence of a candidate action; it does not solve the sequence.

## Verdict
**KEEP world-first exact prediction.** Fair prediction is central and should not be weakened to manufacture uncertainty.

**CUT any future “tactical overview” that detaches acoustics from the facility.** Accessibility must magnify/deemphasize world-space information rather than replace it with a separate graph editor.

**EMPIRICAL GATE:** after a mature 20-minute test, ask players to describe what they were doing. If the dominant description is `I was changing edges on a graph` rather than `I moved the barrier so the right guard heard me and then crossed`, the presentation/level layout fails even if the rules are correct.

---

# 4. Waiting / parking / silence / brute-force / preview-overautomation

## 4.1 Passive waiting
Paper simulations keep intended waiting well below the 20–25% kill ceiling. However players may discover safer unintended routes.

**KEEP** the existing validator and telemetry thresholds. Do not add anti-wait timers, degrading scores during idle, or arbitrary patrol acceleration.

**EMPIRICAL GATE:** representative successful player runs should target <15% passive waiting; >20% warning; >25% across several mature encounters is a content failure.

## 4.2 Permanent barrier parking
Existing V05 correctly rejects a single slot that solves all completion-critical sound outcomes.

**KEEP.** Do not add barrier decay/cooldown to force movement.

## 4.3 Silence-everything
The campaign already requires deliberate useful hearing by E07 and repeatedly later.

**KEEP.** A main-campaign encounter whose clean solution contains no reason to allow/hear a sound is acceptable occasionally, but mature campaign identity must not regress toward universal silence.

## 4.4 Restart brute force
Fast restart is required for humane puzzle learning. With 3–5 barrier slots, brute-force slot testing is possible.

**KEEP fast restart.** Punishing reset would make the game worse.

Countermeasure is information design: the player should have enough preview to reason before acting, and mature encounters should depend on sequences, listener reactions, route changes and physical position rather than one static slot choice.

## 4.5 Preview-overautomation
Exact preview can become an oracle if the player can stand still and sweep all candidates without cost/state change.

**REPAIR:** add a mature-content validator for `SAFE_PREVIEW_ENUMERATION`. A mature encounter fails if all important barrier choices can be exhaustively previewed from a single permanently safe state and the resulting best choice directly completes the acoustic reasoning without needing a sequence, traversal exposure, source choice, listener reaction or visible graph mutation.

This does **not** hide information. It rejects weak encounter construction.

---

# 5. Tied-route overload / listener-density attack

## Attack
Tied minimum routes are mechanically correct but visually expensive. Three listeners multiply route overlays, threshold motifs, investigation states, direct-detection zones and outcome badges. Phase 9 already found E28 and especially E33 fragile.

The three-listener main-campaign cases provide little new reasoning because the core identity is already fully expressible with two listeners through route and threshold asymmetry.

## Verdict
**CUT mandatory three-listener main-campaign content.**

Required repair:
- E28 becomes a two-listener mature encounter using tied-route + threshold/selective-audibility pressure;
- E33 becomes a two-listener climax combining tied routes + threshold split + sequence preservation without moving-source density;
- E34 remains the final synthesis with two listeners and at least two useful-heard moments;
- three listeners move to **optional empirical/remix territory only** and may be omitted entirely from 1.0 if handheld/no-audio readability is inferior.

This keeps 34 main encounters and 8-remix target intact while reducing the most obvious density failure.

**KEEP** the <=12 acoustic-node ceiling and 3–4 simultaneous decision-relevant route ceiling.

---

# 6. Two-listener repetition / 34+8 exhaustion attack

## Attack
Cutting three-listener escalation increases dependence on the same two-listener grammar. Thirty-four main encounters can still become `route A to guard A, block guard B` with decorative topology changes.

## Existing protection
The 12 reasoning families provide meaningful orthogonal axes: alternate routes, threshold split, deliberate investigation, over-propagation, exposure, door mutation, moving source, sequence preservation, return inversion and multi-event ordering.

## Required content signature
Every mature encounter should compile to a signature including at least:
- reasoning-family set;
- source-family combination;
- threshold pairing;
- barrier meaningful-slot count;
- door mutation state;
- moving-source presence;
- extraction inversion yes/no;
- completion-critical barrier-edit sequence length;
- tied-route structure class.

**REPAIR:** before content lock, compare neighboring and campaign-wide signatures. Reject or rewrite encounters that are mechanically near-duplicates even if room geometry/art differs.

**CUT:** expansion above 34 main encounters is not allowed merely because production can author more. The optional 8 remixes are first-cut content if playtests show exhaustion. Do not inflate to 10 unless shipped-quality playtest evidence proves low repetition and low authoring cost.

**EMPIRICAL GATE:** blind playtesters should encounter at least one materially new reasoning responsibility every 2–4 main encounters without needing a new mechanic.

---

# 7. Direct detection vs deterministic puzzle clarity

## Attack
If direct detection uses tight cones, frame-perfect crossings or complex stealth visibility, the game acquires a second mastery pillar competing with acoustic reasoning. If detection is too soft, infiltration loses tension.

## Verdict
**KEEP direct detection as a pressure/failure layer, not a parallel stealth simulation.**

Normative clarification:
- no completion-critical pixel-precision LOS threading;
- no random spotting;
- no hidden suspicion accumulation;
- no long cone-pattern memorization as the intended puzzle;
- direct detection should use simple visible deterministic profiles and, where timing matters, a short readable forgiveness hold;
- whole-simulation speed assists scale timing coherently and may extend allowed detection forgiveness within authored assist bounds.

**CUT** any future combat/takedown solution to direct detection.

**EMPIRICAL GATE:** if players report failing primarily because they misjudged vision-cone microtiming rather than because they created the wrong acoustic/listener state, detection profiles are too demanding.

---

# 8. Controller / handheld / no-audio / reduced-motion / large-UI attack

## Controller
The rail model is well suited to controller because manipulation is one-dimensional and slot-based. Risk is target selection when several sources/listeners are close.

**KEEP** context selection plus a cycle-target fallback. Never require cursor pixel precision.

## Handheld
The strongest risk is route density, not raw text size. Cutting mandatory 3-listener main content materially improves the handheld case.

**KEEP** route-thickness scaling, optional A/B listener labels and world-space emphasis filtering.

## No-audio
Mechanical parity is well specified. Audio must remain reinforcement only.

**KEEP** as a hard gate, not an accessibility nice-to-have.

## Reduced motion
A reduced-motion pulse cannot remove ordering/route identity. Use persistent highlighted segments plus short discrete state changes rather than continuous traveling waves where needed.

**EMPIRICAL GATE:** no-audio + reduced-motion + 150% UI scale must still permit the same optimal decisions in representative E16/E28-replacement/E33-replacement/E34 tests.

---

# 9. Save / replay / checkpoint corruption attack

The Phase-8 architecture is unusually strong here: explicit DTOs, schema versions, content hashes, tmp→atomic replace, backup generation, checkpoint fallback, replay hashes and presentation exclusion are all appropriate.

## Attack cases
1. process dies during save write;
2. primary valid JSON but incompatible content hash;
3. backup is older schema;
4. Cloud restores older profile while local checkpoint is newer;
5. demo profile imported twice;
6. checkpoint captured around door mutation/event ordering;
7. restart during barrier between-slot return;
8. achievement sync fails after local completion.

## Verdict
**KEEP** atomic save + backup + explicit migration.

**REPAIR / technical clarification:** a sound event with `BEFORE_MUTATION` must carry or reference an immutable **pre-mutation graph snapshot/version captured before the mutation commit**. It must not be reconstructed later from current door state at event-generation step. `AFTER_MUTATION` uses the post-mutation snapshot. This removes a real implementation ambiguity between Phase-4 ordering and Phase-8 event generation.

**KEEP** checkpoints only in canonical safe states; no half-barrier or mid-event saves.

**EMPIRICAL GATE:** automated crash/recovery fixtures must include primary corruption, backup recovery, incompatible checkpoint fallback and idempotent demo import.

---

# 10. Demo/full / Steam-offline / platform failure attack

The build-flavor and NullPlatformAdapter split is sufficient.

## Failure cases
- Steam unavailable at boot;
- Cloud unavailable or conflict unresolved;
- overlay/store CTA fails;
- achievement call fails;
- demo and full share storage but demo content is not identical;
- full ownership check is temporarily unavailable.

## Verdict
**KEEP offline-complete local progress as authoritative gameplay continuity.** Platform sync is additive.

**CUT** any startup dependency that blocks campaign play because Steam services are unavailable after ownership/install is already valid.

**KEEP** demo achievements disabled and import of campaign completion only when content identity/hash proves equivalence.

**EMPIRICAL GATE:** real Steam test must verify App-ID separation, shared Cloud path policy, repeated import idempotency and no demo manifest leakage.

---

# 11. Title / capsule / market-position attack

## Title
**CUT `HUSHLINE` from commercial candidates.** The name is already occupied across current apps/services/experiments and creates avoidable search/discovery confusion. It may remain only in historical file headings until Phase 11 establishes a replacement.

Phase 11 naming criteria:
- not obviously occupied by an active game/app/service in targeted search;
- easy to pronounce and type;
- does not imply microphone input, horror-first play, cargo/smuggling, music/rhythm or audio-only accessibility;
- can support the physical barrier / selective-hearing identity;
- works as a repository/product slug;
- receives basic web/store collision screening before migration. This is not legal trademark clearance.

## Capsule
A static capsule cannot explain graph routing. It should show a **single physical barrier dividing two visible sound paths/listener outcomes**, not headphones, waveform-only art or a generic crouching thief silhouette.

Trailer first 10 seconds should show: barrier moves → acoustic route flips → one listener reacts, one does not → player crosses.

## Price/value
The $14.99–$19.99 test range remains plausible, but $17.99 is not a design truth.

**KEEP range as empirical commercial gate.**

**CUT any scope padding to justify price.** If the polished demo feels like a $14.99 product, lower price rather than adding filler encounters.

---

# 12. Phase-4–8 implementation ambiguity audit

## PASS / sufficiently explicit
- strength 1–4, attenuation 0–2, thresholds 1–3;
- barrier +3 attenuation;
- tied minimum routes mechanically count equally;
- one active local/direct barrier baseline;
- between-slot barrier acoustically inactive;
- equal-intensity lure cannot endlessly retarget active investigation;
- hearing distinct from direct detection;
- fixed-step deterministic ordering;
- exact prediction uses same solver;
- stable IDs and tiny graph shortest-path model;
- deterministic authored navigation;
- save DTO/version/hash/backup recovery;
- build flavors and platform adapters;
- no-audio truth parity;
- premium/no-currency commercial model.

## AMBIGUITY REPAIRED
### A10-01 — BEFORE_MUTATION snapshot ownership
Earlier wording allows the correct intent but does not state exactly when the immutable pre-mutation graph state is captured. Phase-10 amendment now requires capture before mutation commit and event reference to that snapshot/version.

## CONTENT AUTHORITY REPAIRED
### A10-02 — main-campaign 3-listener escalation
E28/E33 no longer require three listeners. Main campaign baseline is now maximum two listeners. Three-listener play is optional empirical/remix only and may be cut entirely.

### A10-03 — safe preview enumeration
Mature content gets an explicit validator against solving the acoustic decision by cycling all barrier slots from one permanently safe state.

### A10-04 — direct detection scope
Direct detection is explicitly a simple deterministic pressure layer and may not become a parallel twitch/vision-cone puzzle pillar.

### A10-05 — content signature repetition
Mature content must be audited by systemic signature, not merely geometry/theme, before 34-main lock is accepted.

No other upstream contradiction found that justifies changing core mechanics in Phase 10.

---

# 13. CUT / KEEP / EMPIRICAL-GATE master list

## CUT
1. `HUSHLINE` as final/commercial title candidate.
2. Mandatory three-listener main-campaign encounters E28/E33.
3. Any detached/global acoustic graph editor or tactical overview.
4. Any automatic best-slot/safe-action recommendation.
5. Any barrier cooldown/mana/decay introduced merely to force movement.
6. Any anti-wait punishment timer.
7. Any combat/takedown pillar.
8. Any main difficulty based on pixel-precision LOS or long patrol memorization.
9. Expansion above 34 main merely to pad value; 8 remixes are first-cut if repetitive.

## KEEP
1. Top-down real-time physical acoustic infiltration identity.
2. Local/direct one-barrier manipulation.
3. Exact deterministic prediction/resolution parity.
4. Strength 1–4 / attenuation 0–2 / threshold 1–3 / barrier +3.
5. Tied-minimum routes as mechanically real.
6. Deliberate useful hearing and selective audibility.
7. Two listeners as mature baseline and now main-campaign ceiling.
8. Door mutation / moving sources / threshold split / sequence / extraction inversion as the existing depth grammar.
9. Fast restart and deterministic checkpoints.
10. Complete no-audio decision parity.
11. Premium one-time purchase / no currency / no grind.
12. 34-main target and 8 optional remixes subject to repetition cut gate.
13. Godot 4.7.1-stable / GDScript-first / deterministic Domain Core direction.

## EMPIRICAL GATES
1. Barrier manipulation must feel satisfying rather than chore-like.
2. Meaningful barrier edits should remain roughly >=1/minute in representative mature play; dense moments can be more frequent.
3. Prediction and committed hearing parity = 100%.
4. Muted/no-audio players make identical optimal acoustic decisions.
5. Reduced-motion + large-UI + handheld remains readable.
6. Passive waiting preferably <15%, warning >20%, redesign territory >25% across representative successful runs.
7. Players learn `heard can be useful` by D04/E07.
8. Safe-preview enumeration validator must reject static graph-puzzle rooms in mature content.
9. Two-listener content signatures must remain sufficiently varied across 34 encounters.
10. Three listeners may appear only if optional empirical test proves superior readability/value; otherwise cut entirely.
11. Direct-detection failures must not dominate acoustic-reasoning failures.
12. 55%/70% simulation-speed assists preserve ordering and acceptable feel.
13. Cross-platform deterministic hashes remain identical on target Windows/Linux builds.
14. Corruption/backup/checkpoint fallback and idempotent demo import pass automated fixtures.
15. Real Steam demo/full Cloud/App-ID/offline paths pass before release candidate.
16. Replacement title passes basic collision screening before migration/commercial freeze.
17. Blind pricing test chooses final price inside or below the current $14.99–$19.99 planning range without scope padding.

---

# 14. Phase-10 decision

**PHASE 10 ADVERSARIAL REVIEW = COMPLETE.**

The product survives. The review did **not** find a reason to abandon G4C19 or reopen the concept tournament. It did find five bounded repairs, none of which add mechanics:
- remove mandatory main-campaign three-listener density;
- prevent mature safe-preview slot enumeration;
- explicitly bound direct detection as a secondary deterministic pressure layer;
- require systemic content-signature de-duplication;
- remove ambiguity from BEFORE_MUTATION snapshot capture.

The title `HUSHLINE` is also retired from commercial consideration based on fresh current collisions.

**DESIGN COMPLETE remains NO.** Phase 11 must reconcile these amendments into the final authority chain, perform a fresh implementation-readiness audit, choose a replacement commercial working title after collision screening, produce the final freeze/acceptance criteria, prepare migration + autonomous implementation handoff, and only then decide whether `DESIGN COMPLETE = YES` is justified.
