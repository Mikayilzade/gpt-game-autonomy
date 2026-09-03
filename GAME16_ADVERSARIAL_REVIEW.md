# GAME #016 — PHASE 10 ADVERSARIAL REVIEW

Date: 2026-09-03
Status: PHASE 10 COMPLETE — no unresolved design-blocking issue after patches
Working title: **ONE-WAY WORKSHOP**
Authority attacked: all active Game #016 files through `GAME16_SIMULATION.md`.

## 0. Review result
ONE-WAY WORKSHOP survives destructive review. The core thesis remains worth freezing: irreversible cuts create children whose future usefulness is a capability/ancestry planning problem, not a material-yield problem.

No new mechanic is required. No scope ceiling needs expansion. The 24-case campaign remains viable as an authored premium puzzle product provided Phase 11 freezes the clarifications below as binding acceptance criteria.

The review found **four specification ambiguities that must be treated as patched authority from this file onward**:
1. `reset_generation` must be an explicit persisted monotonic profile field used to distinguish deliberate campaign reset from stale cloud resurrection.
2. Baseline 1.0 cloud policy is now **profile cloud-sync + active attempt local-only**; the alternative opaque attempt-cloud path in Phase 8 is rejected for 1.0.
3. Runtime dead-state silence must never be presented as evidence that a state is live; only positive `Lineage broken` is a proof claim.
4. H3 hints must pass a per-state leakage test: if a hint plus current visible state leaves one legal fabrication commit, H3 must be rewritten to describe a contradiction/requirement relation without shrinking the move set to one.

These are clarifications of already-frozen systems, not added gameplay.

---

# 1. Core fun / tactility attack

## Attack: discrete cut sockets may feel like choosing menu options
**Severity before mitigation: HIGH.** If the player selects a row labeled Cut A/B/C and watches an animation, the differentiator collapses into an abstract dependency puzzle wearing a workshop skin.

**Why the design still survives:** the UX already requires embodied sockets on the physical workpiece, exact two-child ghost preview, physical manipulation of resulting children and direct docking into fixtures. The mechanic is only acceptable if the input path is object-first.

**Binding Phase-11 gate:** a vertical-slice cold test must show the player can point to the workpiece and describe where they cut it, rather than describing that they “picked option B.” Controller play may use focus navigation, but focus must land on visible cut marks on the piece.

## Attack: irreversible commits could feel punitive
**Severity: MEDIUM.** The puzzle asks the player to forecast future dependencies, so irreversible mistakes are expected.

**Survival condition:** restart remains sub-1.5-second-to-interactive target, no menu reload, rich immediate child preview, no lives/score/material penalty. A wrong cut is a reasoning experiment, not lost progress.

## Attack: tactile fantasy may imply woodworking simulation
**Severity: MEDIUM.** Current September 2026 market context reinforces this risk: Woodo is launching September 16 with a highly polished tactile wooden-diorama presentation and a demo, while other workshop/crafting products train players to expect broader manipulation. ONE-WAY WORKSHOP must therefore market the causal event — cut -> two children -> waste becomes jig — rather than generic cozy woodworking.

**Patch:** trailer/store screenshots may show saw/drill presentation, but store copy must explicitly communicate discrete deterministic puzzle fabrication and avoid claims of freeform woodworking.

---

# 2. Repetition / hour-5 freshness attack

## Attack: every case could reduce to “inspect future station, preserve matching offcut”
**Severity: HIGH.** This is the principal content risk.

The six families remain distinct only if their proof sentences remain observably different:
- I Immediate: next-step byproduct necessity;
- II Property: preserve the right physical property, not size;
- III Delayed: preserve capability across unrelated commits;
- IV Cross-blank: another root determines the current root’s cut;
- V Dual-use: allocate/sequence a scarce compatible child;
- VI Relay: create a future tool by adding one derived witness.

**Binding validator/playtest gate:** after blind solve, testers must be able to explain each family with a different causal sentence. If two adjacent families repeatedly receive the same explanation, rewrite cases inside frozen mechanics before ship. Do not add a seventh capability or verb.

## Filler audit
OW01–OW04 are justified as tutorial/thesis establishment; OW03 specifically destroys “largest is best,” and OW04 destroys “first compatible station is correct.” OW05–OW08 introduce genuinely different physical compatibility. OW09–OW12 change temporal planning distance. OW13–OW16 change root coupling. OW17–OW20 change resource allocation through occupation/consumption. OW21–OW24 introduce one-step derived qualification.

No family is currently pure count inflation. The highest filler risk is **OW02 vs OW01** and **OW18 vs OW17**. Phase 11 should freeze an empirical replacement rule: if either case is solved by the same proof sentence with no additional planning burden in blind tests, rewrite that case rather than keeping it for 24-count symmetry.

---

# 3. Dominant strategy / brute-force attack

## “Preserve biggest child”
Defeated by keyed FACE/EDGE/SPAN needs and explicitly taught failure in OW03.

## “Make final product pieces first”
Defeated by OW11 and later dependency graphs.

## “Never consume anything until forced”
Defeated by cases whose mandatory progress requires a consuming operation and whose substitute allocation must be planned.

## “Dock every compatible piece and see what lights up”
Reversible docking is intentionally cheap rehearsal, so this behavior cannot be punished. The anti-bruteforce defense is that docking compatibility does not reveal strategic correctness, and later states require irreversible upstream cuts before relevant pieces exist.

**Patch:** `Fits now` / compatibility affordances may never be ranked, colored as recommended, or ordered by solver desirability. Controller `Cycle Compatible Targets` must use stable semantic ordering, not heuristic ordering.

## “Enumerate every cut preview”
This is allowed. Hiding immediate outcomes would make the game unfair. The puzzle must remain nontrivial even after every current cut has been previewed.

**Authoring gate:** any canonical case that becomes trivial solely by previewing all <=5 current sockets fails content validation. The human proof must depend on future requirement relationships, not discovering which preview contains a green-compatible child.

## Exhaustive restart search
With <=6 commits, a determined player can brute-force some jobs. The product does not need cryptographic search resistance. The requirement is that reasoning be noticeably faster and more comprehensible than enumeration. Do not inflate branching merely to defeat solvers.

---

# 4. Mechanical redundancy / rule inflation

The four base capability families plus witnesses remain sufficient. No review finding justifies another base property.

`FACE` is the weakest primitive because it can become arbitrary key-lock content. Keep it only where fixture shape is physically obvious. Any FACE predicate that cannot be understood from silhouette/contact without text should be rewritten using existing geometry or removed.

`PAIR` remains acceptable only as a visible sibling interface; secret genealogy checks remain forbidden.

Derived witnesses remain capped at one upgrade step on the same piece. Relaxing this cap would create “level up the universal tool” behavior and turn lineage into state bookkeeping.

---

# 5. Scope / production-ratio attack

## Geometry tokens
Target <=45 child silhouettes is viable only with stretchable/reused stock archetypes. Do not author each case as a bespoke wooden object. Logical geometry token reuse is mandatory production strategy, not optional optimization.

## Station kit
Eight reusable station archetypes remain enough. Case-specific presentation may reskin them, but no new logical station family may be added solely for visual novelty.

## Animation expectation
The product needs excellent split/snap/contact feedback, but correctness never uses animation/physics. Minimum polish priority: cut result separation, jig seating, consume/release distinction, certification reveal. Background workshop animation is lower priority.

## Trace View
Trace View is justified because delayed/cross-root reasoning otherwise becomes opaque. It must remain a projection of semantic trace data, not a separate editable genealogy UI. No manual tree layout feature.

## Validator cost
The validator is a real production cost but also the strongest scope protector. Given <=3 roots, <=6 commits and authored finite sockets, exhaustive per-job search is acceptable as an offline requirement. If a job’s state space becomes impractical to exhaust, that is evidence the job violated intended boundedness and should be simplified before weakening validation.

## Deck/controller
Semantic focus is production overhead but necessary for the chosen Steam-first promise. No feature currently requires cursor-only precision. Keep focus graph authoring/testing in scope.

## Localization/platform plumbing
Externalized strings, scalable UI, cloud profile, achievements and demo import are bounded. Do not promise the full target-language list until budget/QA exists; architecture readiness is enough.

---

# 6. UX ambiguity attack

## `Fits now`
Potential misread: “this is the correct strategic use.”

**Patch:** wording/visual semantics must mean only **physically compatible in the current state**. Preferred player-facing phrase: `Fits this fixture` / `Compatible now`, accompanied by neutral iconography. Never use green checkmarks that imply the future remains solvable.

## Temporary release vs consume
This must be visible before commit through shape/icon + plain text. If a consume-on-operation fixture can be mistaken for temporary use in a blind test, the fixture fails UX acceptance.

## Witness vs base capability
A witnessed child must show both its base physical property and the new physical mark. A requirement that needs a witness cannot accept an otherwise identical unwitnessed piece. Inspect copy must state the missing mark, not generic incompatibility.

## PAIR
Selecting a paired child may pulse its sibling and matched scar. No family code or hidden ID is required.

## Trace View spoiler leakage
Pre-clear Trace View may show only past/current causal facts and current pieces already satisfying a requirement. It may not enumerate hypothetical future producers, rank current cuts or display an unreachable future branch. Post-clear recap may show the player’s actual winning path.

## Competition deaths
A key ambiguity is now resolved: **absence of `Lineage broken` means only “the conservative detector has not proved death.” It never means “this state is still solvable.”** UX copy/help must state this if players can reasonably infer the opposite. Certification failure and manual restart remain valid when competition-based death was not detected.

## Controller focus cycles
Stable semantic ordering must not leak solver preference. Root lanes -> visible relation -> stable ID is acceptable; “most useful” is not.

---

# 7. Accessibility attack

Color independence survives: form + symbol + text are primary channels.

Text scaling must be tested not merely on menus but on requirement cards, incompatibility reasons, commit consequence text, hints and cloud/import recovery dialogs at 1280x800.

Reduced motion may shorten/replace animations but may never remove the visible before/after distinction of a destructive commit.

Commit alternatives (hold, double-press, explicit single-confirm) are equivalent interaction safety methods. None changes puzzle truth.

High-information overlay is acceptable because all shown capabilities/requirements are already inspectable facts. It may not add future-reachability information or distinguish strategically safe from unsafe choices.

**Cognitive-load gate:** OW24 with High Information must not become a wall of icons. The overlay may spatially filter/group existing facts, but cannot hide mandatory information available in Minimal mode.

---

# 8. Certifier / dead-state / solution-family attack

## Certifier
State-based AND requirements remain correct. No canonical move-string comparison is allowed.

## Zero false positives
This is non-negotiable. Offline exhaustive oracle must prove `runtime_dead => oracle_dead` for every enumerated reachable state of every canonical job and D1.

If exhaustive search is not feasible for a proposed case under final content data, simplify that case; do not ship an unproven positive dead-state detector for it.

## Optimistic closure
Ignoring competition is safe only because it creates a superset of possibilities. Any implementation optimization that prunes possible producer chains must itself be proven conservative. Performance is secondary to the no-false-positive contract.

## Alternate-family signatures
`Another Way` may use only validator-authored coarse semantic facts (e.g. which root supplied which scarce role), never exact order/count. Each recognized signature must correspond to at least one golden certifying trace and signatures must be mutually distinguishable from final semantic trace/state facts.

---

# 9. Hint leakage attack

The existing H1/H2/H3 philosophy survives, but the “do not name the socket” rule is insufficient in a small state space: a sentence can uniquely force a move without naming it.

**Binding patch — H3 leakage test:** for every authored H3 and every state in which it may be revealed, evaluate the set of currently legal irreversible fabrication commits. If combining H3 with already-visible facts reduces a multi-action choice to exactly one specific commit, rewrite H3 to point at a contradiction class, future requirement relationship, or comparison task instead. It may tell the player **what must remain true**, but not which current commit makes it true.

If only one legal irreversible commit exists before revealing H3, H3 may explain why that commit is relevant because no choice remains to spoil; however it still may not disclose subsequent sequence.

Empirical gate remains: if >25% of blind testers call H3 “the answer,” rewrite it.

---

# 10. Persistence / import / cloud / reset attack

## Reset generation — authoritative clarification
Add persisted profile field:

`reset_generation: integer >= 0`

Fresh profile = 0. Explicit `Reset Campaign Progress` increments generation and creates a new empty campaign-clear/hint/tutorial-progress generation while preserving settings/profile identity as designed. Cloud/profile merge compares generation **before** monotonic set union:
- higher generation represents the later deliberate reset lineage;
- stale lower-generation clear flags must not resurrect progress automatically;
- equal generation merges monotonic progress normally;
- irreconcilable/corrupt generation data must preserve both backups and request recovery rather than guess.

The reset action requires explicit confirmation explaining that older cloud progress will not be automatically restored into the new reset generation.

## Active attempt — authoritative 1.0 decision
The Phase-8 alternative of clouding an opaque active attempt is rejected for baseline 1.0. **`attempt` is local-only.** Cloud sync includes profile/backups + merge-safe portable settings only.

Cross-device behavior is therefore explicit: campaign progress/settings travel; an unfinished work order does not. On another device the player starts that work order from its authored initial state. This is preferable to semantic merging or timestamp conflicts over irreversible state.

## Demo import
Existing idempotent receipt + prerequisite reachability logic survives. D1 never maps to OW13. In-progress demo attempts never import.

## Crash boundary
Domain transaction -> durable complete state -> presentation remains correct. No half-cut save state permitted.

---

# 11. Commercial / demo promise attack

Fresh September-3 checks still support the positioning logic rather than forcing a redesign. Woodo is scheduled for September 16, 2026 with a free demo and tactile wooden-diorama positioning; it increases the presentation bar but not the mechanical collision. Outpacked remains $7.99 with 61 levels, a demo and Workshop, demonstrating why ONE-WAY WORKSHOP should not compete on raw level count.

**$12.99 remains a working MSRP, not a freeze-level guarantee.** Keep the $9.99–14.99 adjustment band until blind value testing.

The 4.5-hour median first-clear floor remains the commercial gate. If the game is shorter, lower price or rewrite weak cases; do not add filler.

The 20–30 minute demo remains credible only if D1 survives the time budget. If median exceeds 30 minutes, simplify D1 presentation/content before removing the cross-blank capstone, because that capstone proves the second-order hook.

Marketing rule survives: never imply freeform woodworking, crafting grind, shop management or realistic fabrication simulation.

---

# 12. Fresh-implementation ambiguity audit

A new implementation session must not invent answers to the following; Phase 11 must include them in authority/acceptance freeze:
1. exact `reset_generation` semantics and merge precedence;
2. active attempt local-only in 1.0;
3. dead-state silence is non-assertive;
4. compatibility indicators mean present physical fit only, not strategic safety;
5. stable controller target ordering may not use solver heuristics;
6. H3 per-state leakage rule;
7. FACE predicates require physically obvious fixture geometry;
8. exhaustive oracle is required for every shipped canonical job/D1 positive-death fixture; simplify content rather than weaken it;
9. alternate-family signatures are semantic allocation facts backed by golden traces;
10. campaign-case rewrite is allowed inside frozen mechanics when filler/proof-distinctness gates fail; adding mechanics is not;
11. exact launch localization set is budget-flexible; localization-ready architecture is mandatory;
12. exact final MSRP is empirical inside $9.99–14.99; mechanics/content cannot be padded to defend price.

Everything else needed for implementation is already specified in Phase 3–9 authorities.

---

# 13. Rejected attacks / non-issues

- **Need procedural levels for value:** rejected. Would weaken validation and scope; authored density is the product.
- **Need undo after committed cut:** rejected. Removes the one-way thesis; instant restart is the recovery mechanism.
- **Need score/par to motivate replay:** rejected. Would distort play toward optimization and brute repetition.
- **Need full dead-state completeness:** rejected. Zero false positives matters more; competition deaths may remain silent.
- **Need realistic woodworking physics:** rejected. Deterministic tokens are core correctness.
- **Need more than 24 cases because competitors advertise more:** rejected pending value tests; raw count is not the design target.
- **Need new late-game mechanic:** rejected. Existing relay/allocation/cross-root composition is sufficient if content proofs remain distinct.

---

# 14. Remaining empirical gates — not design blockers

1. Socketed cuts feel object-direct, not menu-like.
2. Six-commit / <=8-child lineage remains readable on desktop and Deck.
3. Cold players infer jig compatibility primarily from physical form.
4. Restart friction is low enough that irreversible commits feel tense rather than punitive.
5. Family proof sentences remain distinct in blind play.
6. OW02 and OW18 specifically survive filler/duplication checks.
7. Demo median is 20–30 minutes and communicates the hook unaided.
8. Full campaign median first-clear is >=4.5h, target 5–7h.
9. H3 is not perceived as answer leakage by a material share of players.
10. Marketing art communicates deterministic byproduct-as-tool puzzle before generic woodworking expectations.

These are implementation/playtest gates. They do not require inventing gameplay during implementation.

---

# 15. Phase-10 verdict

**PASS.** No unresolved design-blocking contradiction remains after the authoritative clarifications above. The product thesis, mechanic grammar, 24-case architecture, UX approach, commercial model and technical architecture remain coherent under destructive review.

Proceed to **Phase 11 Specification Freeze** next. Phase 11 must consolidate authority order, explicit acceptance criteria, implementation-flexible vs design-fixed decisions, empirical gates, exact reset/cloud/dead-state/hint clarifications, and decide `DESIGN COMPLETE = YES` only after confirming a fresh implementation session would not need to invent important gameplay.