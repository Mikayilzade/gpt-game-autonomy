# GAME #005 — PHASE 11 ENCOUNTER BLUEPRINT LOCK

Last updated: 2026-08-24
Factory run: **11 — extended pass**
Phase: **11 — Specification Freeze / Encounter Lock**
Selected concept: **G5C02 — Tension Budget**
Production implementation: **NOT STARTED**

# ENCOUNTER LOCK STATUS = COMPLETE / SUBJECT TO FINAL READINESS AUDIT

This file is the causal implementation lock required by Phase-10 Amendment A15. Final art transforms, corridor shape, decorative routing and exact metric dimensions remain production-flexible; the causal puzzle graphs below do not.

## Blueprint notation
- Load quantum `0/1/2` = SLACK/TAUT/HIGH.
- Gate condition `>=TAUT` means clearance tier 1 or 2.
- Lift conditions refer to stable authored dock semantics; implementation may choose physical heights but may not alter which semantic band opens the named graph edge.
- Span traversal exists only at stable TAUT.
- `rail` in multiple regions means the same physical carriage can be reached from multiple authored sides/approaches, not multiple carriages.
- All edges are stable-state edges; transition timing never creates an edge.
- Named vectors below are complete authoritative paths, not suggestions.

# Path catalog (exact, authoritative)

All vectors are ordered by the load order declared by the encounter. `P0..Pn` are physical rail bands from one end to the other. Every adjacent pair has exactly one -1/+1 transfer and every vector conserves B.

- `P2`: `[2,0] -> [1,1] -> [0,2]`.
- `P3A`: `[2,1,0] -> [1,2,0] -> [1,1,1] -> [0,2,1]`.
- `P3B`: `[0,1,2] -> [0,2,1] -> [1,1,1] -> [2,0,1]`.
- `P3C`: `[2,0,1] -> [1,1,1] -> [0,2,1] -> [0,1,2]`.
- `P3D`: `[1,0,2] -> [1,1,1] -> [2,0,1] -> [2,1,0]`.
- `P3E`: `[2,1,0] -> [1,2,0] -> [1,1,1] -> [0,2,1] -> [0,1,2]`.
- `P4B4`: `[2,2,0,0] -> [2,1,1,0] -> [1,2,1,0] -> [1,2,0,1] -> [1,1,1,1]`.

Mutation families:
- `M32A` pre `[L,G,S]`: `[2,0,0] -> [1,1,0] -> [1,0,1]`; post `[L,S]`: `[2,0] -> [1,1] -> [0,2]`.
- `M23A` pre `[L,G]`: `[2,0] -> [1,1] -> [0,2]`; post `[L,G,S]`: `[2,0,0] -> [1,1,0] -> [0,1,1]`.
- `M43A4` pre 4-load/B4: `[2,2,0,0] -> [2,1,1,0] -> [1,2,1,0] -> [1,1,1,1]`; post 3-load/B4: `[2,2,0] -> [2,1,1] -> [1,2,1] -> [1,1,2]`.
- `M34A5` pre 3-load/B3: `[2,1,0] -> [1,2,0] -> [1,1,1] -> [0,2,1] -> [0,1,2]`; post 4-load/B3: `[2,1,0,0] -> [1,2,0,0] -> [1,1,1,0] -> [1,1,0,1] -> [0,2,0,1]`.
- `M43A5/M43B5/M43C5` pre 4-load/B4: `[2,2,0,0] -> [2,1,1,0] -> [1,2,1,0] -> [1,2,0,1] -> [1,1,1,1]`; post 3-load/B4: `[2,2,0] -> [2,1,1] -> [1,2,1] -> [1,1,2] -> [2,0,2]`.
- `M34B5` pre `[G1,G2,S]`: `[0,1,2] -> [0,2,1] -> [1,1,1] -> [2,0,1] -> [2,1,0]`; post `[G1,G2,S,L1]`: `[0,1,2,0] -> [0,2,1,0] -> [1,1,1,0] -> [1,1,0,1] -> [1,0,1,1]`.
- `M34C5` pre `[L1,G1,S1]`: `[2,1,0] -> [1,2,0] -> [1,1,1] -> [0,2,1] -> [0,1,2]`; post `[L1,G1,S1,L2]`: `[2,1,0,0] -> [1,2,0,0] -> [1,1,1,0] -> [1,1,0,1] -> [0,1,1,1]`.

The path names are shorthand only; an encounter's declared load order plus named path uniquely determines every revision vector.

# Main campaign blueprints

## E01 — First Pull
- **Loads/order:** `L1:LIFT,G1:GATE`.
- **Snap/B/path:** `3` bands, `B=2`, `P2`.
- **Mutation:** none.
- **Reasoning:** S01.
- **Meaningful commit class:** 1; intended canonical sequence `P2→P0`.
- **Decision separation:** commit.
- **Regions:** R0 rail/start; X exit.
- **Canonical traversal edges:** R0->X iff L1=HIGH; G1 visible only.
- **Checkpoint/exit:** C0:R0/P2; exit X.
- **Alternate boundary:** safe deterministic alternates are accepted only if they retain the primary reasoning family, do not remove every decision-separating event, and do not reduce the encounter to one permanent best band/static enumeration.
- **Expected validation:** V01–V10, V19 PASS by exact vectors; V11–V15 required from E06 onward (tutorial exceptions E01–E05 are explicit); V16–V18 PASS by scope; V20 required iff mutation exists.

## E02 — Give / Take
- **Loads/order:** `L1:LIFT,G1:GATE`.
- **Snap/B/path:** `3` bands, `B=2`, `P2`.
- **Mutation:** none.
- **Reasoning:** S02.
- **Meaningful commit class:** 1; intended canonical sequence `P2→P1`.
- **Decision separation:** both consequences completion-relevant.
- **Regions:** R0 rail/start; R1; X.
- **Canonical traversal edges:** R0->R1 iff G1>=TAUT; R1->X iff L1>=TAUT.
- **Checkpoint/exit:** C0:R0/P2; exit X.
- **Alternate boundary:** safe deterministic alternates are accepted only if they retain the primary reasoning family, do not remove every decision-separating event, and do not reduce the encounter to one permanent best band/static enumeration.
- **Expected validation:** V01–V10, V19 PASS by exact vectors; V11–V15 required from E06 onward (tutorial exceptions E01–E05 are explicit); V16–V18 PASS by scope; V20 required iff mutation exists.

## E03 — Middle Holds
- **Loads/order:** `L1:LIFT,S1:SPAN`.
- **Snap/B/path:** `3` bands, `B=2`, `P2`.
- **Mutation:** none.
- **Reasoning:** S03.
- **Meaningful commit class:** 1; intended canonical sequence `P0→P1`.
- **Decision separation:** TAUT proves middle.
- **Regions:** R0 rail/start; R1; X.
- **Canonical traversal edges:** R0->R1 iff S1=TAUT; R1->X iff L1=TAUT.
- **Checkpoint/exit:** C0:R0/P0; exit X.
- **Alternate boundary:** safe deterministic alternates are accepted only if they retain the primary reasoning family, do not remove every decision-separating event, and do not reduce the encounter to one permanent best band/static enumeration.
- **Expected validation:** V01–V10, V19 PASS by exact vectors; V11–V15 required from E06 onward (tutorial exceptions E01–E05 are explicit); V16–V18 PASS by scope; V20 required iff mutation exists.

## E04 — Gate Then Lift
- **Loads/order:** `L1:LIFT,G1:GATE`.
- **Snap/B/path:** `3` bands, `B=2`, `P2`.
- **Mutation:** none.
- **Reasoning:** S05.
- **Meaningful commit class:** 2; intended canonical sequence `P0→P2; traverse R1; P2→P0`.
- **Decision separation:** traversal separates decisions.
- **Regions:** R0 rail; R1 rail-access; X.
- **Canonical traversal edges:** R0->R1 iff G1>=TAUT; R1->X iff L1=HIGH.
- **Checkpoint/exit:** C0:R0/P0; exit X.
- **Alternate boundary:** safe deterministic alternates are accepted only if they retain the primary reasoning family, do not remove every decision-separating event, and do not reduce the encounter to one permanent best band/static enumeration.
- **Expected validation:** V01–V10, V19 PASS by exact vectors; V11–V15 required from E06 onward (tutorial exceptions E01–E05 are explicit); V16–V18 PASS by scope; V20 required iff mutation exists.

## E05 — Span Commitment
- **Loads/order:** `G1:GATE,S1:SPAN`.
- **Snap/B/path:** `3` bands, `B=2`, `P2`.
- **Mutation:** none.
- **Reasoning:** S06.
- **Meaningful commit class:** 2; intended canonical sequence `P0→P1; cross Span; P1→P0`.
- **Decision separation:** crossing destroys return route.
- **Regions:** R0 rail; R1 rail-access; X.
- **Canonical traversal edges:** R0->R1 iff S1=TAUT; R1->X iff G1=HIGH.
- **Checkpoint/exit:** C0:R0/P0; exit X.
- **Alternate boundary:** safe deterministic alternates are accepted only if they retain the primary reasoning family, do not remove every decision-separating event, and do not reduce the encounter to one permanent best band/static enumeration.
- **Expected validation:** V01–V10, V19 PASS by exact vectors; V11–V15 required from E06 onward (tutorial exceptions E01–E05 are explicit); V16–V18 PASS by scope; V20 required iff mutation exists.

## E06 — Three-Load Middle
- **Loads/order:** `L1:LIFT,G1:GATE,S1:SPAN`.
- **Snap/B/path:** `4` bands, `B=3`, `P3A`.
- **Mutation:** none.
- **Reasoning:** S03/S02.
- **Meaningful commit class:** 2; intended canonical sequence `P0→P2; traverse R2; P2→P0`.
- **Decision separation:** middle then extreme in new context.
- **Regions:** R0 rail; R1; R2 rail-access; X.
- **Canonical traversal edges:** R0->R1 iff S1=TAUT; R1->R2 iff G1>=TAUT; R2->X iff L1=HIGH.
- **Checkpoint/exit:** C0:R0/P0; exit X.
- **Alternate boundary:** safe deterministic alternates are accepted only if they retain the primary reasoning family, do not remove every decision-separating event, and do not reduce the encounter to one permanent best band/static enumeration.
- **Expected validation:** V01–V10, V19 PASS by exact vectors; V11–V15 required from E06 onward (tutorial exceptions E01–E05 are explicit); V16–V18 PASS by scope; V20 required iff mutation exists.

## E07 — Same Door, Different Future
- **Loads/order:** `L1:LIFT,G1:GATE,S1:SPAN`.
- **Snap/B/path:** `4` bands, `B=3`, `P3B`.
- **Mutation:** none.
- **Reasoning:** S04.
- **Meaningful commit class:** 2; intended canonical sequence `P0→P1; traverse; P1→P3`.
- **Decision separation:** P1 chosen over locally equivalent P2 because future lift.
- **Regions:** R0 rail; R1; R2 rail-access; X.
- **Canonical traversal edges:** R0->R1 iff G1=HIGH; R1->R2 iff S1=TAUT; R2->X iff L1=HIGH.
- **Checkpoint/exit:** C0:R0/P0; exit X.
- **Alternate boundary:** safe deterministic alternates are accepted only if they retain the primary reasoning family, do not remove every decision-separating event, and do not reduce the encounter to one permanent best band/static enumeration.
- **Expected validation:** V01–V10, V19 PASS by exact vectors; V11–V15 required from E06 onward (tutorial exceptions E01–E05 are explicit); V16–V18 PASS by scope; V20 required iff mutation exists.

## E08 — Balcony Relay
- **Loads/order:** `L1:LIFT,G1:GATE,S1:SPAN`.
- **Snap/B/path:** `4` bands, `B=3`, `P3C`.
- **Mutation:** none.
- **Reasoning:** S07.
- **Meaningful commit class:** 3; intended canonical sequence `P3→P0; R1; P0→P1; R2; P1→P2`.
- **Decision separation:** three-step relay.
- **Regions:** R0 rail; R1 rail; R2 rail; X.
- **Canonical traversal edges:** R0->R1 iff L1=HIGH; R1->R2 iff S1=TAUT; R2->X iff G1>=TAUT.
- **Checkpoint/exit:** C0:R0/P3; exit X.
- **Alternate boundary:** safe deterministic alternates are accepted only if they retain the primary reasoning family, do not remove every decision-separating event, and do not reduce the encounter to one permanent best band/static enumeration.
- **Expected validation:** V01–V10, V19 PASS by exact vectors; V11–V15 required from E06 onward (tutorial exceptions E01–E05 are explicit); V16–V18 PASS by scope; V20 required iff mutation exists.

## E09 — High Is Wrong
- **Loads/order:** `L1:LIFT,G1:GATE,S1:SPAN`.
- **Snap/B/path:** `4` bands, `B=3`, `P3D`.
- **Mutation:** none.
- **Reasoning:** S03.
- **Meaningful commit class:** 2; intended canonical sequence `P0→P1; traverse; P1→P3`.
- **Decision separation:** late non-tutorial TAUT use.
- **Regions:** R0 rail; R1; R2 rail; X.
- **Canonical traversal edges:** R0->R1 iff S1=TAUT; R1->R2 iff L1=TAUT; R2->X iff G1>=TAUT.
- **Checkpoint/exit:** C0:R0/P0; exit X.
- **Alternate boundary:** safe deterministic alternates are accepted only if they retain the primary reasoning family, do not remove every decision-separating event, and do not reduce the encounter to one permanent best band/static enumeration.
- **Expected validation:** V01–V10, V19 PASS by exact vectors; V11–V15 required from E06 onward (tutorial exceptions E01–E05 are explicit); V16–V18 PASS by scope; V20 required iff mutation exists.

## E10 — Far-Side Choice
- **Loads/order:** `L1:LIFT,G1:GATE,S1:SPAN`.
- **Snap/B/path:** `4` bands, `B=3`, `P3A`.
- **Mutation:** none.
- **Reasoning:** S13.
- **Meaningful commit class:** 2; intended canonical sequence `P0→P1; traverse to R2; P1→P2`.
- **Decision separation:** P1 and P3 both solve local Gate; only P1 preserves Lift access to R2.
- **Regions:** R0 rail; R1; R2 rail access only via correct branch; X.
- **Canonical traversal edges:** R0->R1 iff G1=HIGH; R1->R2 iff L1>=TAUT; R2->X iff S1=TAUT.
- **Checkpoint/exit:** C0:R0/P0; exit X.
- **Alternate boundary:** safe deterministic alternates are accepted only if they retain the primary reasoning family, do not remove every decision-separating event, and do not reduce the encounter to one permanent best band/static enumeration.
- **Expected validation:** V01–V10, V19 PASS by exact vectors; V11–V15 required from E06 onward (tutorial exceptions E01–E05 are explicit); V16–V18 PASS by scope; V20 required iff mutation exists.

## E11 — Twin Lifts
- **Loads/order:** `L1:LIFT,L2:LIFT,G1:GATE`.
- **Snap/B/path:** `4` bands, `B=3`, `P3B`.
- **Mutation:** none.
- **Reasoning:** S08.
- **Meaningful commit class:** 2; intended canonical sequence `P0→P3; traverse; P3→P1`.
- **Decision separation:** same-family competition across space.
- **Regions:** R0 rail; R1; R2 rail; X.
- **Canonical traversal edges:** R0->R1 iff L1=HIGH; R1->R2 iff G1>=TAUT; R2->X iff L2=HIGH.
- **Checkpoint/exit:** C0:R0/P0; exit X.
- **Alternate boundary:** safe deterministic alternates are accepted only if they retain the primary reasoning family, do not remove every decision-separating event, and do not reduce the encounter to one permanent best band/static enumeration.
- **Expected validation:** V01–V10, V19 PASS by exact vectors; V11–V15 required from E06 onward (tutorial exceptions E01–E05 are explicit); V16–V18 PASS by scope; V20 required iff mutation exists.

## E12 — Three Placement
- **Loads/order:** `L1:LIFT,G1:GATE,S1:SPAN`.
- **Snap/B/path:** `5` bands, `B=3`, `P3E`.
- **Mutation:** none.
- **Reasoning:** S07.
- **Meaningful commit class:** 3; intended canonical sequence `P4→P0; R1; P0→P2; R2; P2→P1`.
- **Decision separation:** three meaningful commits.
- **Regions:** R0 rail; R1 rail; R2 rail; R3; X.
- **Canonical traversal edges:** R0->R1 iff L1=HIGH; R1->R2 iff S1=TAUT; R2->R3 iff G1=HIGH; R3->X iff L1=TAUT.
- **Checkpoint/exit:** C0:R0/P4; exit X.
- **Alternate boundary:** safe deterministic alternates are accepted only if they retain the primary reasoning family, do not remove every decision-separating event, and do not reduce the encounter to one permanent best band/static enumeration.
- **Expected validation:** V01–V10, V19 PASS by exact vectors; V11–V15 required from E06 onward (tutorial exceptions E01–E05 are explicit); V16–V18 PASS by scope; V20 required iff mutation exists.

## E13 — Twin Gates
- **Loads/order:** `G1:GATE,G2:GATE,S1:SPAN`.
- **Snap/B/path:** `4` bands, `B=3`, `P3C`.
- **Mutation:** none.
- **Reasoning:** S08.
- **Meaningful commit class:** 2; intended canonical sequence `P3→P0; traverse; P0→P3`.
- **Decision separation:** mirrored gate values differ by location.
- **Regions:** R0 rail; R1; R2 rail; X.
- **Canonical traversal edges:** R0->R1 iff G1=HIGH; R1->R2 iff S1=TAUT; R2->X iff G2>=TAUT.
- **Checkpoint/exit:** C0:R0/P3; exit X.
- **Alternate boundary:** safe deterministic alternates are accepted only if they retain the primary reasoning family, do not remove every decision-separating event, and do not reduce the encounter to one permanent best band/static enumeration.
- **Expected validation:** V01–V10, V19 PASS by exact vectors; V11–V15 required from E06 onward (tutorial exceptions E01–E05 are explicit); V16–V18 PASS by scope; V20 required iff mutation exists.

## E14 — Commit Pocket
- **Loads/order:** `L1:LIFT,G1:GATE,S1:SPAN`.
- **Snap/B/path:** `4` bands, `B=3`, `P3A`.
- **Mutation:** none.
- **Reasoning:** S12.
- **Meaningful commit class:** 3; intended canonical sequence `P3→P0; enter pocket; P0→P2; leave pocket; P2→P1`.
- **Decision separation:** same vector changes value after pocket commitment.
- **Regions:** R0 rail; P pocket with rail; R2; X.
- **Canonical traversal edges:** R0->P iff L1=HIGH; P->R2 iff S1=TAUT; R2->X iff G1=HIGH.
- **Checkpoint/exit:** C0:R0/P3; exit X.
- **Alternate boundary:** safe deterministic alternates are accepted only if they retain the primary reasoning family, do not remove every decision-separating event, and do not reduce the encounter to one permanent best band/static enumeration.
- **Expected validation:** V01–V10, V19 PASS by exact vectors; V11–V15 required from E06 onward (tutorial exceptions E01–E05 are explicit); V16–V18 PASS by scope; V20 required iff mutation exists.

## E15 — Twin Spans
- **Loads/order:** `S1:SPAN,S2:SPAN,L1:LIFT`.
- **Snap/B/path:** `4` bands, `B=3`, `P3B`.
- **Mutation:** none.
- **Reasoning:** S08/S03.
- **Meaningful commit class:** 2; intended canonical sequence `P3→P2; cross S1; P2→P0`.
- **Decision separation:** second non-tutorial middle-state family.
- **Regions:** R0 rail; R1; R2 rail; X.
- **Canonical traversal edges:** R0->R1 iff S1=TAUT; R1->R2 iff L1>=TAUT; R2->X iff S2=TAUT.
- **Checkpoint/exit:** C0:R0/P3; exit X.
- **Alternate boundary:** safe deterministic alternates are accepted only if they retain the primary reasoning family, do not remove every decision-separating event, and do not reduce the encounter to one permanent best band/static enumeration.
- **Expected validation:** V01–V10, V19 PASS by exact vectors; V11–V15 required from E06 onward (tutorial exceptions E01–E05 are explicit); V16–V18 PASS by scope; V20 required iff mutation exists.

## E16 — Counterweight Gone
- **Loads/order:** `L1:LIFT,G1:GATE,S1:SPAN -> L1,S1`.
- **Snap/B/path:** `3` bands, `B=2`, `M32A`.
- **Mutation:** REMOVE G1.
- **Reasoning:** S09/S16.
- **Meaningful commit class:** 3; intended canonical sequence `pre P2→P1→P0; mutate at P0; post P0→P1`.
- **Decision separation:** first removal lesson; same band reinterprets.
- **Regions:** R0 rail; R1; O objective; R2 rail; X.
- **Canonical traversal edges:** pre R0->R1 iff G1=TAUT; R1->O iff L1=HIGH; post O->R2 iff S1=TAUT; R2->X iff L1>=TAUT.
- **Checkpoint/exit:** C0:R0/P2; C1:O/P0; exit X.
- **Alternate boundary:** safe deterministic alternates are accepted only if they retain the primary reasoning family, do not remove every decision-separating event, and do not reduce the encounter to one permanent best band/static enumeration.
- **Expected validation:** V01–V10, V19 PASS by exact vectors; V11–V15 required from E06 onward; V16–V18 PASS by scope; V20 PASS across every objectively reachable activation band.

## E17 — New Span Joined
- **Loads/order:** `L1:LIFT,G1:GATE -> L1,G1,S1`.
- **Snap/B/path:** `3` bands, `B=2`, `M23A`.
- **Mutation:** ADD S1.
- **Reasoning:** S10/S16.
- **Meaningful commit class:** 3; intended canonical sequence `pre P0→P1; traverse R1; P1→P0; mutate P0; post P0→P2`.
- **Decision separation:** first addition lesson.
- **Regions:** R0 rail; R1; O; R2 rail; X.
- **Canonical traversal edges:** pre R0->R1 iff G1=TAUT; R1->O iff L1=HIGH; post O->R2 iff S1=TAUT; R2->X iff G1=TAUT.
- **Checkpoint/exit:** C0:R0/P0; C1:O/P0; exit X.
- **Alternate boundary:** safe deterministic alternates are accepted only if they retain the primary reasoning family, do not remove every decision-separating event, and do not reduce the encounter to one permanent best band/static enumeration.
- **Expected validation:** V01–V10, V19 PASS by exact vectors; V11–V15 required; V16–V18 PASS by scope; V20 PASS across every objectively reachable activation band.

## E18 — Return Inversion I
- **Loads/order:** `L1:LIFT,L2:LIFT,G1:GATE,S1:SPAN -> L1,G1,S1`.
- **Snap/B/path:** `4` bands, `B=4`, `M43A4`.
- **Mutation:** REMOVE L2.
- **Reasoning:** S11.
- **Meaningful commit class:** 3; intended canonical sequence `pre P3→P0→P1; mutate P1; post P1→P3`.
- **Decision separation:** entry band becomes wrong after removal.
- **Regions:** R0 rail; R1; O; R2 rail; X.
- **Canonical traversal edges:** pre R0->R1 iff L2=HIGH; R1->O iff G1>=TAUT; post O->R2 iff S1=TAUT; R2->X iff L1>=TAUT.
- **Checkpoint/exit:** C0:R0/P3; C1:O/P1; exit X.
- **Alternate boundary:** safe deterministic alternates are accepted only if they retain the primary reasoning family and return inversion.
- **Expected validation:** V01–V20 PASS; V20 explicitly enumerates all objective-reachable pre bands.

## E19 — Mutation Mid-Route
- **Loads/order:** `L1:LIFT,G1:GATE,S1:SPAN -> +G2:GATE`.
- **Snap/B/path:** `5` bands, `B=3`, `M34A5`.
- **Mutation:** ADD G2.
- **Reasoning:** S12/S16.
- **Meaningful commit class:** 3; intended canonical sequence `pre P4→P0→P2; mutate P2; post P2→P3`.
- **Decision separation:** mutation after spatial commitment.
- **Regions:** R0 rail; R1; O; R2 rail; R3; X.
- **Canonical traversal edges:** pre R0->R1 iff L1=HIGH; R1->O iff S1=TAUT; post O->R2 iff G2>=TAUT; R2->R3 iff G1>=TAUT; R3->X iff L1=TAUT.
- **Checkpoint/exit:** C0:R0/P4; C1:O/P2; exit X.
- **Alternate boundary:** safe deterministic alternates are accepted only if they preserve the post-addition reinterpretation.
- **Expected validation:** V01–V20 PASS.

## E20 — Revision Relay
- **Loads/order:** `L1:LIFT,L2:LIFT,G1:GATE,S1:SPAN -> L1,G1,S1`.
- **Snap/B/path:** `5` bands, `B=4`, `M43A5`.
- **Mutation:** REMOVE L2.
- **Reasoning:** S17.
- **Meaningful commit class:** 4; intended canonical sequence `pre P4→P0→P1; mutate P1; post P1→P2→P3`.
- **Decision separation:** post-objective relay not simple reversal.
- **Regions:** R0 rail; R1; O; R2 rail; R3 rail; X.
- **Canonical traversal edges:** pre R0->R1 iff L2=HIGH; R1->O iff G1>=TAUT; post O->R2 iff S1=TAUT; R2->R3 iff G1=HIGH; R3->X iff L1>=TAUT.
- **Checkpoint/exit:** C0:R0/P4; C1:O/P1; exit X.
- **Alternate boundary:** alternates may shorten one local traverse but may not collapse the extraction relay to a single post-mutation commit.
- **Expected validation:** V01–V20 PASS.

## E21 — Four Loads
- **Loads/order:** `L1:LIFT,G1:GATE,S1:SPAN,G2:GATE`.
- **Snap/B/path:** `5` bands, `B=4`, `P4B4`.
- **Mutation:** none.
- **Reasoning:** S15.
- **Meaningful commit class:** 3; intended canonical sequence `P4→P0; R1; P0→P2; R2; P2→P4`.
- **Decision separation:** four-load compromise without mutation.
- **Regions:** R0 rail; R1; R2 rail; R3; X.
- **Canonical traversal edges:** R0->R1 iff G1=HIGH; R1->R2 iff S1=TAUT; R2->R3 iff G2>=TAUT; R3->X iff L1=TAUT.
- **Checkpoint/exit:** C0:R0/P4; exit X.
- **Alternate boundary:** safe deterministic alternates accepted only if they preserve a four-load global compromise and at least two separated decisions.
- **Expected validation:** V01–V19 PASS; V20 N/A.

## E22 — Twin Family Mutation
- **Loads/order:** `G1:GATE,G2:GATE,S1:SPAN -> +L1:LIFT`.
- **Snap/B/path:** `5` bands, `B=3`, `M34B5`.
- **Mutation:** ADD L1.
- **Reasoning:** S14.
- **Meaningful commit class:** 4; intended canonical sequence `pre P0→P4→P2; mutate P2; post P2→P4→P1`.
- **Decision separation:** repeated family redistributes asymmetrically.
- **Regions:** R0 rail; R1; O; R2 rail; X.
- **Canonical traversal edges:** pre R0->R1 iff G1=HIGH; R1->O iff S1=TAUT; post O->R2 iff L1>=TAUT; R2->X iff G2=HIGH.
- **Checkpoint/exit:** C0:R0/P0; C1:O/P2; exit X.
- **Alternate boundary:** alternate must preserve same-family competition plus mutation; no one-band post solution.
- **Expected validation:** V01–V20 PASS.

## E23 — Local Decoy
- **Loads/order:** `L1:LIFT,G1:GATE,G2:GATE,S1:SPAN`.
- **Snap/B/path:** `5` bands, `B=4`, `P4B4`.
- **Mutation:** none.
- **Reasoning:** S04/S13.
- **Meaningful commit class:** 3; intended canonical sequence `P0→P2; traverse; P2→P4; traverse; P4→P0`.
- **Decision separation:** P2 and P3 both solve the local G1=HIGH problem; only P2 preserves G2 for the next decision.
- **Regions:** R0 rail; R1; R2 rail only via preserved edge; X.
- **Canonical traversal edges:** R0->R1 iff G1=HIGH; R1->R2 iff S1=TAUT AND G2>=TAUT; R2->X iff L1=HIGH.
- **Checkpoint/exit:** C0:R0/P0; exit X.
- **Alternate boundary:** a shorter alternate is rejected if it turns the local-decoy lesson into direct single-band selection.
- **Expected validation:** V01–V19 PASS; V20 N/A.

## E24 — Return Inversion II
- **Loads/order:** `L1:LIFT,G1:GATE,G2:GATE,S1:SPAN -> L1,G1,S1`.
- **Snap/B/path:** `5` bands, `B=4`, `M43B5`.
- **Mutation:** REMOVE G2.
- **Reasoning:** S11/S17.
- **Meaningful commit class:** 4; intended canonical sequence `pre P4→P2; mutate P2; post P2→P3→P1` plus separated traversal.
- **Decision separation:** different return relay from E20 via Span requirement.
- **Regions:** R0 rail; R1; O; R2 rail; R3; X.
- **Canonical traversal edges:** pre R0->R1 iff G2>=TAUT; R1->O iff G1=HIGH; post O->R2 iff G1=HIGH; R2->R3 iff L1>=TAUT; R3->X iff S1=TAUT.
- **Checkpoint/exit:** C0:R0/P4; C1:O/P2; exit X.
- **Alternate boundary:** alternates must retain return inversion and at least two materially distinct post-objective decisions.
- **Expected validation:** V01–V20 PASS.

## E25 — Final Relay
- **Loads/order:** `L1:LIFT,L2:LIFT,G1:GATE,S1:SPAN -> L1,G1,S1`.
- **Snap/B/path:** `5` bands, `B=4`, `M43C5`.
- **Mutation:** REMOVE L2.
- **Reasoning:** S07/S15/S17.
- **Meaningful commit class:** 4; intended canonical sequence `pre P4→P0→P1; mutate P1; post P1→P2→P4`.
- **Decision separation:** synthesis relay; no timing.
- **Regions:** R0 rail; R1; O; R2 rail; R3 rail; X.
- **Canonical traversal edges:** pre R0->R1 iff L2=HIGH; R1->O iff G1>=TAUT; post O->R2 iff S1=TAUT; R2->R3 iff G1=HIGH; R3->X iff L1=HIGH.
- **Checkpoint/exit:** C0:R0/P4; C1:O/P1; exit X.
- **Alternate boundary:** alternate must preserve four-load pre-read, mutation, and multi-step extraction.
- **Expected validation:** V01–V20 PASS.

## E26 — Final Budget
- **Loads/order:** `L1:LIFT,G1:GATE,S1:SPAN -> +L2:LIFT`.
- **Snap/B/path:** `5` bands, `B=3`, `M34C5`.
- **Mutation:** ADD L2.
- **Reasoning:** S18.
- **Meaningful commit class:** 4; intended canonical sequence `pre P4→P0→P2; mutate P2; post P2→P3→P4`.
- **Decision separation:** final synthesis: tradeoff+TAUT+mutation+return.
- **Regions:** R0 rail; R1; O; R2 rail; R3 rail; X.
- **Canonical traversal edges:** pre R0->R1 iff L1=HIGH; R1->O iff S1=TAUT; post O->R2 iff L2>=TAUT; R2->R3 iff G1>=TAUT; R3->X iff S1=TAUT.
- **Checkpoint/exit:** C0:R0/P4; C1:O/P2; exit X.
- **Alternate boundary:** alternates may vary order only if the full S18 synthesis remains; no bypass of the new L2 consequence.
- **Expected validation:** V01–V20 PASS.

# Campaign-level lock checks

1. **Count:** 26 retained main encounters, inside the frozen 24–28 range.
2. **Vocabulary:** only Lift/Gate/Span; one carriage; 2–4 active loads; 3–5 bands.
3. **Math:** every listed revision path conserves B, stays in 0/1/2, has unique vectors and exact adjacent one-quantum transfer.
4. **Low-load bounds:** every two-load revision is exactly 3 bands/B=2.
5. **Mutation families:** E16/E17 use the A04 low-load templates; all 4/5-band mutations stay in 3↔4-load families.
6. **TAUT defense:** E03, E06, E09, E15, E21+ use non-tutorial middle-state reasoning across different compositions.
7. **No transition timing:** every graph edge is stable-state semantic.
8. **Anti-enumeration:** E06+ contain at least two meaningful decisions separated by traversal, rail-access change, location value or mutation. Validator/solver remains authoritative for actual scene data.
9. **Commit ceiling:** every intended solution is <=4 meaningful commits after mutation is counted as an event, not a carriage commit.
10. **Mutation safety:** every mutation encounter must enumerate all objectively reachable activation bands under V20; objective geometry must physically exclude any unsafe activation state rather than UI-gating it.
11. **Alternate solutions:** allowed when they preserve safety/grammar; rejected when they collapse the declared primary signature or tutorial literacy.
12. **Repetition:** repeated-family lessons are interleaved (E11/E13/E15) and late mutation families use different causal region graphs; V14/V15 still compare compiled scene fingerprints before release.
13. **Checkpoints:** C0 always; C1 only after stable mutation and before extraction.
14. **Exit:** completion only in a stable authoritative state.
15. **Implementation boundary:** implementation may tune geometry, transforms and presentation but may not invent alternate causal graphs to make a blueprint work; a blueprint that fails in scene construction must return to design review/cut rather than receive a new mechanic.

# Phase-11 encounter decision

All 26 retained main encounters now have implementation-ready causal blueprints with exact load sets, snap/B paths, mutation structure, reasoning family, intended commit/separation class, region graph and checkpoint/exit contracts.

The final freeze still requires a cross-document readiness audit and authority/acceptance manifest. `DESIGN COMPLETE = YES` is not asserted by this file alone.
