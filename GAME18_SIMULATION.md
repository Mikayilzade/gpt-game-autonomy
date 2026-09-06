# GAME #018 — PHASE 9 WHOLE-GAME SIMULATION

Date: 2026-09-06
Game: LOCAL TIME
Status: PHASE 9 COMPLETE — PHASE 10 ADVERSARIAL REVIEW NEXT
Production implementation: NO

## Verdict
Paper execution preserves the core loop: moving clock-zones changes current predicates; Resolve turns some valid current conditions into persistent consequences; later relocation reuses clock coverage without reversing completed history.

Phase 9 found and repairs three specification hazards.

## Canonical repairs
1. Every shippable campaign/mastery case must have a finite public resolve_limit. No-change Resolve remains legal and consumes one Resolve, but never accumulates hidden duration. This removes the prior contradiction between incrementing beat_index and the promised finite solver graph.
2. Every carrier handoff is a finite state-qualified edge. A persistent DISPATCH milestone cannot repeatedly execute the same carrier edge after the carrier leaves its source state. Multi-step routes require separate public edges. Arrival and ACCEPT remain separate Resolves by default.
3. Undo Resolve restores exact pre-Resolve puzzle state, but persistence/save generation metadata remains monotonic. If an undone state is persisted, it is written as a new atomic save generation.

## LT01–LT06 run
LT01 proves NOW vs DONE: Bakery 08:00 makes RAW->RISEN; moving the zone to Bridge leaves RISEN persistent. Repeated Resolve cannot advance the same state twice.
LT02 proves permanent risk and no rewind: narrow 08:05 bakes safely; broad exposure may also permanently close an unprotected flower.
LT03 proves simultaneous current predicates in Snapshot0 and one-shot dispatch.
LT04 proves prepare -> handoff -> arrival -> later acceptance; no accidental same-Resolve cascade.
LT05 proves Snapshot0 hazard precedence; warning is factual, not prohibition.
LT06 proves unguided synthesis with two movable plus one fixed zone. Any promise of multiple solutions must be solver-verified.

## Cases 07–36 proof-shape obligations
Chapter 2: 07 competing milestones; 08 narrow-before-broad; 09 irreversible three-stage chain; 10 two chains sharing risk; 11 earn then restore final NOW; 12 two-chain/protection/final-current synthesis.
Chapter 3: 13 prepare-before-dispatch; 14 persistent prerequisite + current gate; 15 two payloads/one finite-state carrier; 16 coupled dispatch -> arrival -> later accept; 17 receiver vs source clock reuse; 18 coupled-departure synthesis.
Chapter 4: 19 protect before broad exposure; 20 two protections in dependency order; 21 coupling safe only after protection; 22 same-Resolve protection too late by default; 23 two genuinely distinct protection routes; 24 two risks + process + final coupling.
Chapter 5: 25 two clocks/two endpoints; 26 earn then redeploy; 27 repeated couplings across beats; 28 first three-site coupling; 29 carrier departure under two-clock coordination; 30 move-budget synthesis that must not become socket scanning.
Chapter 6: 31 dual-chain shared-clock bottleneck; 32 relay into protected endpoint; 33 fixed + two movable with protect/dispatch/receive; 34 two carriers without routing complexity; 35 tight but explainable scarcity; 36 dependency braid with >=2 persistent prerequisites, one protection, one relay and final two-site coupling, human proof <=6 necessity statements.

Phase 10 must compare likely duplicate clusters: 08/19, 14/18/29, 26/27/31, 32/33/36.

## Mastery
M01 alternate-solution pressure; M02 three-site coupling + prerequisite; M03 two-hazard protection order; M04 two payloads/one carrier; M05 dual chains/shared clock; M06 relay + later accept + final current; M07 two movable + one fixed with larger reachable graph; M08 full-family synthesis. M09–M12 remain reserve and ship only for genuinely new proof topology.

## Persistence and hostile behavior
Quit/crash during Resolve animation reloads computed post-state, never half-animation. Corrupt latest checkpoint falls back to known-good backup. Repeat demo import is idempotent; older demo progress cannot overwrite newer full progress. Divergent cloud checkpoints are chosen whole, never field-merged.

Resolve spam cannot create infinite solver state because resolve_limit is finite. Socket/warning scanning stays public but no multi-beat oracle is added; cases solved mainly by cycling sockets fail human-proof review. Unlimited ordinary Undo is acceptable because there is no hidden-information or economy exploit.

## Cross-rule check
Current vs persistent, hazards vs benefits, carrier arrival vs acceptance, coupled-current overlap rules, save-vs-animation and Undo-vs-cloud are internally consistent after the repairs above.

Open empirical gates remain: first-time comprehension, 25–35 minute demo timing, real Deck readability, warning-vs-oracle behavior, final 30–36 authored-board diversity, 6–8 hour completion time and whether clock-zones feel embodied rather than abstract switches.

PHASE 9 WHOLE-GAME SIMULATION = COMPLETE.

# NEXT DESIGN STEP — PHASE 10 ADVERSARIAL REVIEW
Attack repetition, duplicate clusters, dominant strategies, socket scanning, Resolve-limit annoyance, carrier ambiguity, warning-oracle behavior, art/content burden, solver feasibility, save/import/cloud recovery, controller/Deck readability, localization precision, commercial value and remaining implementation ambiguity. Decide whether 36 campaign and 8+4 mastery remain justified. Cut/repair rather than add semantic families.