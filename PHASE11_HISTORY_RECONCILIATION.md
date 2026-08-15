# ORGANISM CARGO — PHASE 11 VALIDATION-HISTORY RECONCILIATION

Status: **IN PROGRESS — PHASE 9/10 AUTHORITY DEMOTED, STALE SEMANTICS IDENTIFIED**
Last updated: 2026-08-15

`WHOLE_GAME_SIMULATION.md` and `ADVERSARIAL_REVIEW.md` are validation history. They may explain why a rule exists, but they are no longer independent gameplay authorities when a Phase-11 canonical source contains the final rule.

Until direct wording cleanup is complete, this file records known stale phrases that must not be implemented literally.

## 1. Whole-game simulation stale blocked-growth narrative

Representative Contract B currently narrates:
- one blocked growth event;
- then `repeated pressure pushes Grazer...`.

This must **not** be interpreted as repeated unchanged every-tick blocked-growth stress/damage. Canonical rule is `MECHANICS.md` + `PHASE11_FREEZE.md`:
- unchanged illegal deterministic growth begins one `GROWTH_BLOCKED` episode;
- the episode consequence fires once;
- no repeated same-obstruction punishment occurs until a relevant legality/occupancy/orientation/growth-trigger/retry-boundary condition changes.

The representative story remains valid only if later stress derives from independent continuing causes or a genuinely new blocked-growth episode.

## 2. Challenge gate terminology

Any Phase-7/9 phrase such as `after Tier 2`, `roughly the first 16 contracts`, or `after enough rules are documented` is normalized to:

`Challenge mode unlocked iff Bronze(C16) == true`.

Documented rule families may gate individual challenge templates after the mode is unlocked; they cannot unlock the mode before C16.

## 3. Demo mapping terminology

Any older demo wording is normalized to:
- 10 demo species total = 9 documented + 1 bounded discovery;
- D01–D08 may map to C01–C08 Bronze;
- D09–D10 never auto-clear C09+;
- settings/knowledge may transfer through validated version mappings;
- imported knowledge never bypasses C16 Challenge gate;
- no mechanical power transfers.

## 4. Empty-space terminology

Any generic language implying that more unused cells is globally better is superseded. There is no global empty-space score or normal optimization axis. `EMPTY_CELLS` is legal only as an explicit contract-specific predicate where density itself creates a demonstrated dynamic transit tradeoff.

## 5. Resume terminology

Any history wording suggesting that a platform/runtime snapshot itself is authoritative is superseded by `PHASE11_TECH_PERSISTENCE.md`:
- immutable committed input + versions/checksums is the authority;
- resume reconstructs transit deterministically;
- playback cursor may be stored but is presentation state;
- checksum mismatch follows explicit recovery logic.

## 6. Duplicate completion/progression terminology

Any phrase `Results writes progression` is shorthand only. The final semantic contract is idempotent completion application using stable run/completion identity. Entering Results is not itself an award event.

## 7. Phase-10 repairs already folded into canonical sources

The following major Phase-10 repairs now have canonical homes and Phase-10 text is evidence/history only:
- dynamic-transit significance quotas -> `CONTENT_ARCHITECTURE.md` / `PHASE11_FREEZE.md`;
- max-spacing and repeated role-template counterexamples -> content/freeze sources;
- Cooler+Filter <=8 C17–C48 primary Bronze cap -> content/freeze sources;
- living-vs-powered support role distinction -> content/freeze sources;
- sleep explicit trait gates -> `MECHANICS.md` / `DECISION_ARCHITECTURE.md` / freeze;
- no global empty-space optimization -> `MECHANICS.md` / freeze;
- finite T10 reactive pulses -> `MECHANICS.md` / freeze;
- simultaneous material causes preserve multi-parent ancestry -> `MECHANICS.md` / freeze;
- Brownout Phase-A authority -> `MECHANICS.md` / freeze;
- species redundancy clusters and >=70% cut/merge gate -> `CONTENT_ARCHITECTURE.md` / freeze;
- exact campaign graph -> `CONTENT_ARCHITECTURE.md` / freeze;
- exactly-once launch/idempotent Results/reconstruction/cloud/migration/demo import -> `PHASE11_TECH_PERSISTENCE.md`;
- complete keyboard/controller/Deck/no-audio/non-color/reduced-motion/reduced-flash paths -> `PHASE11_UX_ACCESSIBILITY.md`;
- C16 Challenge gate and exact demo progression boundary -> `PHASE11_PROGRESSION.md`.

## 8. Prototype gates remain valid but are not undefined design

Phase-10 empirical gates remain obligations:
- >=70% representative failures produce a specific causal explanation + intended revision rather than blind shuffle;
- at least half of memorable validation outcomes depend on post-launch change;
- ordinary non-mastery planning median should not exceed 8 minutes after rule familiarity;
- helper/protector redundancy clusters are cut/merged if decisions overlap >=70%;
- demo testers predominantly describe planning for transit behavior, not static packing;
- Causal Review surfaces an actionable first cause without raw-log reading.

These gates can fail the prototype and force simplification/cuts. They do not authorize implementation to invent new mechanics before testing.

## 9. Remaining history work

Direct cleanup of `WHOLE_GAME_SIMULATION.md` and `ADVERSARIAL_REVIEW.md` is still required before final repository freeze so future readers do not encounter stale phrases without this reconciliation layer. The final whole-repository sweep must search for: `repeated`, `growth blocked`, `empty`, `Challenge`, `Tier 2`, `demo`, `8 documented`, `2 discovery`, `resume`, `snapshot`, `Results writes`, `controller optional`, `TBD`, `TODO`, `future work`, `to be decided`, `exact dependencies are content data`.