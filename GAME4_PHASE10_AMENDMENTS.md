# GAME #004 — PHASE 10 NORMATIVE AMENDMENTS

Last updated: 2026-08-21
Authority: **Phase-10 repair layer pending Phase-11 integration**
Purpose: record only normative corrections discovered by `GAME4_ADVERSARIAL_REVIEW.md`. Where this file conflicts with Phase-3–9 wording, this file controls until Phase 11 reconciles the final freeze.

## A10-01 — Main-campaign listener ceiling
Owning upstream: `GAME4_CONTENT.md`, with corresponding presentation/simulation consequences in `GAME4_UX_PRESENTATION.md` and `GAME4_WHOLE_GAME_SIMULATION.md`.

Replace the prior assumption that E28 and E33 are exceptional three-listener main-campaign encounters.

Canonical Phase-10 repair:
- Main campaign E01–E34 has **maximum two listeners per encounter**.
- E28 becomes a two-listener mature encounter centered on tied-route + threshold/selective-audibility pressure.
- E33 becomes a two-listener climax combining tied routes + threshold split + sequence preservation without moving-source density.
- E34 remains a two-listener final synthesis and retains the contract of at least two useful-heard moments.
- Three-listener gameplay is not required for main completion and is not a 1.0 promise.
- A three-listener optional/remix experiment may exist only if handheld + no-audio + reduced-motion tests prove it remains clear and worthwhile. It may be cut entirely without replacement mechanic or campaign-count change.

Reason: the third listener increases world-space route/outcome/detection density much faster than it increases reasoning depth. The core selective-audibility identity is already fully expressible with two listeners.

## A10-02 — Safe preview enumeration validator
Owning upstream: `GAME4_CONTENT.md`.

Add validator concept `V17_SAFE_PREVIEW_ENUMERATION`:
- Applies to COMBINE/MATURE/CLIMAX content, excluding explicit early teaching exceptions.
- Warning/reject when all strategically relevant barrier slots can be exhaustively previewed from one permanently safe manipulation state and choosing the favorable preview directly resolves the completion-critical acoustic decision without meaningful traversal exposure, source choice, listener reaction, sequence dependency, door/source mutation or return-path change.
- The repair does **not** hide prediction or make preview uncertain. It rejects weak content that turns exact prediction into a slot oracle.

## A10-03 — Direct detection scope bound
Owning upstream: `GAME4_MECHANICS.md` and `GAME4_UX_PRESENTATION.md`.

Canonical clarification:
- Direct detection is a deterministic pressure/failure layer, not a second stealth mastery pillar.
- Main completion may not require pixel-precision line-of-sight threading, random spotting, hidden suspicion, long cone-cycle memorization or frame-perfect crossings.
- Detection profiles must be visually explicit, deterministic and compatible with whole-simulation speed assists.
- A short readable forgiveness hold is allowed where needed.
- Hearing remains distinct from direct detection.
- No combat/takedown branch is introduced as recovery.

## A10-04 — Content-signature anti-repetition audit
Owning upstream: `GAME4_CONTENT.md`.

Before Phase-11/final content lock, every COMBINE/MATURE/CLIMAX encounter must expose a comparable signature containing at least:
- reasoning-family set;
- source-family combination;
- listener threshold pairing;
- meaningful barrier-slot count;
- door mutation yes/no and phase role;
- moving-source presence;
- extraction inversion yes/no;
- completion-critical barrier-edit sequence length;
- tied-route structure class.

Neighboring/campaign-wide signatures must be compared. Encounters that are mechanically near-duplicates must be rewritten or cut even if geometry/art differs.

The target remains 34 main encounters. Do not expand above 34 to pad value. The 8 optional remixes remain optional and are the first content cut if repetition evidence is poor.

## A10-05 — BEFORE_MUTATION graph snapshot capture
Owning upstream: `GAME4_MECHANICS.md` and `GAME4_TECHNICAL_SPEC.md`.

Canonical clarification for any action that both mutates graph state and emits a sound:
- `BEFORE_MUTATION`: capture/reference an immutable graph snapshot/version **immediately before** the relevant mutation commit at the canonical ordering point; the emitted event resolves against that immutable snapshot even though general event generation/hearing occurs later in the tick.
- `AFTER_MUTATION`: event references the post-mutation graph snapshot/version after the mutation commit.
- Presentation, prediction and committed resolution must use the same snapshot ID/semantic phase.
- Implementations may optimize storage via persistent graph revision/delta structures, but may not reconstruct a BEFORE event later from the current mutable door/barrier state.

Reason: this removes an implementation ambiguity between Phase-4 fixed-step ordering and Phase-8 event generation while preserving all existing gameplay semantics.

## A10-06 — Commercial title retirement
Owning upstream: product/commercial metadata only; no gameplay spec change.

`HUSHLINE` is **retired from commercial-title consideration** because current search shows multiple active software/app/service uses and a 2026 interactive experiment with the same/near-identical name. It may remain in historical headings as a continuity codename until Phase 11 selects a replacement.

Phase 11 must choose a replacement working commercial title before migration after basic web/store collision screening. This screening is not legal trademark clearance.

## Acceptance impact
These amendments do not change:
- selected G4C19 concept;
- strength 1–4;
- attenuation 0–2;
- listener thresholds 1–3;
- barrier +3 attenuation;
- one local/direct barrier baseline;
- deterministic tied-minimum-route hearing;
- retarget logic;
- 34-main campaign count;
- 8 optional remix target;
- premium/no-currency model;
- exact prediction/resolution parity;
- PC/Steam-first single-player/offline scope;
- Godot 4.7.1-stable / GDScript-first technical direction.

Phase 11 must integrate A10-01 through A10-06 into the final freeze rather than leaving this amendment file as a permanent parallel rule source.
