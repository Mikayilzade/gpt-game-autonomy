# ORGANISM CARGO — CONTENT ARCHITECTURE

Status: **CANONICAL PHASE 5 — CONTENT ARCHITECTURE LOCKED**
Last updated: 2026-08-15

This file defines the launch-facing content architecture for **Organism Cargo**. It composes only mechanics already frozen in `MECHANICS.md`, `DECISION_ARCHITECTURE.md`, and `PHASE4_CLOSURE.md`. Content may tune numeric parameters and combine existing rules; it may not quietly invent new authoritative simulation systems.

---

# 1. Phase-5 content contract

The content layer must achieve four goals at once:

1. teach the rule vocabulary gradually;
2. create enough distinct decisions for a premium campaign without hundreds of bespoke assets;
3. provide a deterministic generator/recombination layer for long-tail mastery;
4. remain readable enough that every species can be understood from body silhouette + 1–3 significant traits.

Any proposed content item is rejected if it requires one-off runtime code, adds a hidden target-selection rule, exceeds the trait/body-plan limits without an authored exception, or creates difficulty mainly through information clutter.

---

# 2. Exact content targets

## 2.1 MVP vertical slice

The smallest version that proves the game:
- body plans: **4** (B01 Dot, B02 Domino, B03 Corner, B04 Bar);
- significant trait families: **10** foundation families T01–T10;
- playable species: **9** representative species from `PHASE4_CLOSURE.md`;
- supports: **6** foundation supports;
- hold families/layouts: **3**;
- route hazard families: **5**;
- authored contracts: **12**;
- tutorial/milestone contracts inside those 12: **6**;
- generated challenge templates: **6**;
- flavor variants: **0 required**;
- discovery contracts: **2**.

## 2.2 Public demo target

The demo must prove the differentiator without exposing most advanced combinations:
- body plans: **4**;
- species: **10** total, of which 8 are fully documented and 2 appear in bounded discovery form;
- supports: **4** available (Cooler, Filter, Baffle, Feed Cartridge); Nest Pad and Monitor Beacon remain outside the demo;
- holds: **3 layouts** from two families;
- route hazard families: **3**;
- authored contracts: **10**;
- generated/recombined challenge templates: **3**;
- discovery contracts: **1**;
- campaign playtime target: roughly **60–90 minutes** for a normal first clear, longer for Gold optimization.

The demo ends immediately after the first contract that combines growth timing with a route hazard and support tradeoff. It should leave the player understanding that later species/hazards will deepen the same system rather than merely increase quantity.

## 2.3 Launch target

Launch content target:
- body plans: **4** foundation body plans; no fifth body plan required;
- significant trait families: **10** foundation families, expressed through parameter/state-gated variants rather than new systems;
- launch species: **22** mechanically distinct compositions;
- supports: **6**;
- hold families: **5**;
- authored hold layouts: **12**;
- route hazard families: **7**;
- authored route profiles/timelines: **18**;
- authored campaign contracts: **48**;
- tutorial/milestone contracts within the 48: **14**;
- discovery contracts within the 48: **8**;
- generated/recombined challenge templates: **24**;
- hand-authored final mastery contracts: **6** included in the 48;
- cosmetic/flavor variants: up to **2 presentation variants per species**, never mechanically distinct and not required for all species;
- codex/discovery entries: **22 species + 10 trait-family entries + 7 route-hazard entries + 6 support entries**.

Target campaign first-clear length: approximately **8–12 hours**, depending on retries and optional medals. Gold/mastery plus generated challenges should support materially longer play without requiring grind.

---

# 3. Numeric parameter bands

Species may choose values only from these launch bands unless later balance testing changes the bands globally. This prevents arbitrary per-species arithmetic.

## 3.1 Stress thresholds

Three threshold profiles:

### Hardy
- agitated enter: 8
- agitated exit: 4
- panic enter: 14
- panic exit: 9

### Standard
- agitated enter: 6
- agitated exit: 3
- panic enter: 11
- panic exit: 7

### Sensitive
- agitated enter: 5
- agitated exit: 2
- panic enter: 9
- panic exit: 6

All preserve canonical hysteresis ordering.

## 3.2 Contamination profiles

### Resistant
- intake multiplier: 0.5 fixed-point equivalent
- contaminated enter: 11
- contaminated exit: 5

### Standard
- intake multiplier: 1.0
- contaminated enter: 8
- contaminated exit: 4

### Vulnerable
- intake multiplier: 1.5 fixed-point equivalent
- contaminated enter: 7
- contaminated exit: 3

## 3.3 Satiety bands

- low reserve start: 3–4
- normal reserve start: 5–7
- high reserve start: 8–9
- ordinary metabolism: -1 every 2 ticks
- high metabolism: -1 every tick
- feed intake cap: 1, 2, or 3 units/tick

## 3.4 Source/sink magnitude bands

Environmental source output per authoritative tick:
- weak: 2
- standard: 3
- strong: 4
- pulse: 4–6 once per legal state-entry event

Sink/mitigation capacity:
- weak: 2
- standard: 3
- strong: 4

Social direct stress modification:
- weak: 1
- standard: 2
- strong: 3

No launch species exceeds `strong` continuous output. Larger numbers belong to route hazards or rare one-time pulses.

## 3.5 Range bands

- adjacency: distance 1
- near: Manhattan distance <=2
- directed: cardinal ray range 2 or 3

No launch organism uses an always-on whole-hold aura.

## 3.6 Lifecycle timing bands

Growth/sleep prerequisite duration:
- quick: 1 completed qualifying tick
- standard: 2 consecutive qualifying ticks
- slow: 3 consecutive qualifying ticks

Delayed reactive output:
- next tick
- +2 ticks maximum for normal launch content

Longer hidden timers are prohibited because they become memory tests rather than spatial prediction.

---

# 4. Canonical launch species roster — 22 species

The first nine preserve the Phase-4 validation identities. Values below are launch-band identities, not final balance numbers.

## O01 Ember Pod
- body/stage: B01 Dot, fixed stage;
- profile: Standard stress, Standard contamination;
- traits: T01 Heat Emitter + T03 Alarm Emitter;
- role: unstable heat/social source;
- useful partners: Hushling, Ash Sponge;
- dangerous partners: Pulse Mite, other sensitive emitters;
- lifecycle: none;
- readability hook: ember-orange sac that brightens and trembles with stress;
- tiers: 1–6;
- generator exclusions: never pair more than 3 in generated manifests below Tier 4.

## O02 Hushling
- body/stage: B01 Dot;
- profile: Sensitive stress, Standard contamination;
- traits: T04 Soother;
- role: narrow social stabilizer;
- useful partners: Ember Pod, Pulse Mite, Glass Larva;
- dangerous partners: stress sources that can disable its CALM-only function;
- lifecycle: none;
- readability hook: soft folded antennae open only while soothing;
- tiers: 1–6;
- exclusions: no generated contract may rely on one Hushling soothing more targets than its capacity.

## O03 Silt Grazer
- body/stage: B01 Dot -> B02 Domino;
- profile: Standard stress, Resistant contamination;
- traits: T06 Filter Feeder + T08 Growth Trigger;
- role: contamination sink whose success changes topology;
- useful partners: Spore Bell, contamination routes;
- dangerous partners: tight holds, Feed Cartridge when early growth is undesirable;
- lifecycle: grows after sustained satiety threshold;
- readability hook: squat mouth-ring sprouts a forward tail segment before growth;
- tiers: 2–6;
- exclusions: generator must prove at least one legal growth path unless blocked growth is an explicitly visible intended pressure.

## O04 Spore Bell
- body/stage: B01 Dot;
- profile: Hardy stress, Standard contamination;
- traits: T05 Spore Shedder + T10 Reactive Pulse;
- role: persistent contamination cascade seed;
- useful partners: Silt Grazer, Filter;
- dangerous partners: contamination-vulnerable species;
- lifecycle: state-gated by CONTAMINATED;
- readability hook: translucent bell fills with visible dark motes before shedding;
- tiers: 2–6;
- exclusions: no first-contact discovery contract may combine it with another undocumented contamination rule.

## O05 Warmback
- body/stage: B02 Domino;
- profile: Hardy stress, Resistant contamination;
- traits: T01 Heat Emitter + T09 Symbiotic Buffer;
- role: harmful thermal body / narrow protector;
- useful partners: FRAGILE-tag organisms vulnerable to contamination;
- dangerous partners: heat-sensitive clusters;
- lifecycle: none;
- readability hook: hot dorsal plates; shielded neighbor gets visible amber link;
- tiers: 2–6;
- exclusions: at most one protected target per Warmback.

## O06 Cradle Moss
- body/stage: B01 Dot;
- profile: Sensitive stress, Resistant contamination;
- traits: T04 Soother + T07 FEEDING producer form;
- role: beneficial cluster anchor with double loss when asleep/panicked;
- useful partners: grazers and alarm-prone species;
- dangerous partners: hazards that disable CALM/awake benefits;
- lifecycle: awake/asleep strongly changes role;
- readability hook: fronds open while producing food/soothing, fold shut during sleep;
- tiers: 2–6;
- exclusions: generator must not count both benefits as independent supports when one state disables both.

## O07 Pulse Mite
- body/stage: B01 Dot;
- profile: Sensitive stress, Standard contamination;
- traits: T03 Alarm Emitter + T10 heat Reactive Pulse;
- role: converts social failure into heat failure;
- useful partners: Hushling, Baffle;
- dangerous partners: Ember Pod, heat-sensitive species;
- lifecycle: one-time pulse on PANICKED entry;
- readability hook: small bright thorax flashes once on panic transition;
- tiers: 2–6;
- exclusions: no recursive same-tick pulse chain accepted by validator.

## O08 Glass Larva
- body/stage: B01 Dot -> B03 Corner;
- profile: Sensitive stress, Vulnerable contamination;
- traits: T07 Grazer + T08 Growth Trigger;
- role: future-space lifecycle puzzle;
- useful partners: Cradle Moss, Feed Cartridge, Warmback protection;
- dangerous partners: blocked corners, contamination sources;
- lifecycle: matures after sustained satiety;
- readability hook: transparent body shows three budding lobes matching future footprint;
- tiers: 2–6;
- exclusions: generated contracts must overlay/validate legal mature footprint.

## O09 Ash Sponge
- body/stage: B02 Domino;
- profile: Hardy stress, Resistant contamination;
- traits: T02 Heat Sink + T06 Filter Feeder + T10 delayed stress Reactive output;
- role: powerful two-channel helper with self-generated social cost;
- useful partners: heat/contamination sources;
- dangerous partners: sensitive social clusters;
- lifecycle: delayed stress output after high heat absorption;
- readability hook: dark porous body swells red, then exhales visible agitation wave;
- tiers: 4–6;
- exclusions: authored or high-tier generated only; never introduced before player understands all three component families.

## O10 Frost Finch
- body/stage: B01 Dot;
- profile: Sensitive stress, Standard contamination;
- traits: T02 Heat Sink;
- role: simple local thermal sink;
- useful partners: Ember Pod, Warmback;
- dangerous partners: none intrinsic, but low capacity makes over-clustering fail;
- lifecycle: none;
- readability hook: pale feather-crystal mantle frosts adjacent cells when active;
- tiers: 1–6;
- exclusions: none beyond capacity validation.

## O11 Rattle Reed
- body/stage: B04 Bar;
- profile: Standard stress, Resistant contamination;
- traits: T03 Alarm Emitter, directed orientation variant;
- role: directional social hazard and separator;
- useful partners: Baffle, distant positioning;
- dangerous partners: targets in its facing ray;
- lifecycle: alarm activates while AGITATED/PANICKED;
- readability hook: three reed chambers visibly point toward emission direction;
- tiers: 3–6;
- exclusions: never place in tutorial before directed overlays are taught.

## O12 Velvet Nurse
- body/stage: B02 Domino;
- profile: Standard stress, Standard contamination;
- traits: T04 Soother + T09 Symbiotic Buffer;
- role: one-target welfare specialist with positioning cost;
- useful partners: FRAGILE or sensitive species;
- dangerous partners: its value collapses if forced asleep/panicked;
- lifecycle: none;
- readability hook: one side glows soft blue toward selected eligible neighbor;
- tiers: 3–6;
- exclusions: generated manifests may contain at most 2 to prevent blanket buffering.

## O13 Cinder Snail
- body/stage: B02 Domino;
- profile: Hardy stress, Resistant contamination;
- traits: T01 Heat Emitter + T08 Growth Trigger;
- role: slow thermal source that becomes a larger spatial obstacle;
- useful partners: Frost Finch, Cooler;
- dangerous partners: tight future-space layouts;
- lifecycle: B02 Domino -> B04 Bar after sustained high heat exposure;
- readability hook: shell extends one visible segment in facing direction;
- tiers: 3–6;
- exclusions: growth path must be validated; not combined with hidden route timing on first use.

## O14 Mire Sipper
- body/stage: B01 Dot;
- profile: Standard stress, Resistant contamination;
- traits: T06 Filter Feeder;
- role: simple contamination sink without growth complication;
- useful partners: Spore Bell, contamination leak routes;
- dangerous partners: none intrinsic, but capacity-limited;
- lifecycle: none;
- readability hook: visible siphon animation only when contamination is actually consumed;
- tiers: 1–6;
- exclusions: none.

## O15 Lantern Tick
- body/stage: B01 Dot;
- profile: Sensitive stress, Standard contamination;
- traits: T10 Reactive Pulse producing temporary food on CALM recovery after AGITATED;
- role: recovery timing resource source;
- useful partners: grazers that need a timed feed window;
- dangerous partners: constant stress that prevents recovery pulse;
- lifecycle: pulse once per distinct legal recovery event, bounded by cooldown/event guard;
- readability hook: abdomen lights only on recovery boundary;
- tiers: 4–6;
- exclusions: generated validator caps recover-pulse count and rejects self-sustaining food loops.

## O16 Moth Cushion
- body/stage: B03 Corner;
- profile: Sensitive stress, Vulnerable contamination;
- traits: T04 Soother + sleep-gated lifecycle rule using existing sleep grammar;
- role: broad footprint that is useful awake but easy to disable;
- useful partners: clustered sensitive species;
- dangerous partners: vibration timing, contamination sources;
- lifecycle: enters sleep quickly on Nest Pad; soothing disabled asleep;
- readability hook: wing-corner folds visibly closed during sleep;
- tiers: 3–6;
- exclusions: no contract may require its soothing and mandatory sleep simultaneously without making timing solvable.

## O17 Coal Urchin
- body/stage: B01 Dot;
- profile: Hardy stress, Resistant contamination;
- traits: T02 Heat Sink + T03 Alarm Emitter;
- role: thermal helper that becomes a social liability under stress;
- useful partners: hot but emotionally stable cargo;
- dangerous partners: panic-prone clusters;
- lifecycle: none;
- readability hook: spines cool from red to black while calm, flare on agitation;
- tiers: 4–6;
- exclusions: generator rejects cases where its sink and alarm are both irrelevant.

## O18 Spindle Bloom
- body/stage: B01 Dot -> B04 Bar;
- profile: Standard stress, Standard contamination;
- traits: T05 Spore Shedder + T08 Growth Trigger;
- role: contamination source whose emission footprint expands over time;
- useful partners: filters/grazers;
- dangerous partners: vulnerable species and narrow lanes;
- lifecycle: matures under sustained contamination exposure;
- readability hook: folded bud unfurls into a line of spore cups;
- tiers: 4–6;
- exclusions: advanced-only; generator must ensure causal explanation remains <=5 meaningful links for Bronze path.

## O19 Amber Leech
- body/stage: B01 Dot;
- profile: Standard stress, Resistant contamination;
- traits: T07 Grazer + T09 Symbiotic Buffer;
- role: consumes food while protecting the same compatible neighbor, creating dependency;
- useful partners: food-producing FRAGILE species;
- dangerous partners: Feed Cartridge competition and starvation;
- lifecycle: none;
- readability hook: visible feeding tether doubles as protection link;
- tiers: 3–6;
- exclusions: source cost must remain conserved; no free infinite feed/protection cycle.

## O20 Whistle Crab
- body/stage: B03 Corner;
- profile: Hardy stress, Standard contamination;
- traits: T03 Alarm Emitter + T09 Symbiotic Buffer;
- role: protector that becomes dangerous when its own stress rises;
- useful partners: one compatible fragile target;
- dangerous partners: route vibration/heat sources;
- lifecycle: none;
- readability hook: one claw shelters a neighbor while shell vents whistle rings when agitated;
- tiers: 4–6;
- exclusions: cannot protect from stress; otherwise it could negate its own primary downside.

## O21 Pale Drifter
- body/stage: B02 Domino;
- profile: Standard stress, Vulnerable contamination;
- traits: T10 cleansing Reactive Pulse on waking + sleep lifecycle rule;
- role: timed contamination relief tied to wake events;
- useful partners: Nest Pad, bounded contamination spikes;
- dangerous partners: wrong vibration timing or unnecessary sleep;
- lifecycle: wake produces one cleansing pulse using T10; no continuous sink;
- readability hook: dormant body clouds over; wake produces one bright clearing ring;
- tiers: 5–6 / discovery first;
- exclusions: only one pulse per sleep episode; generated use only after documented.

## O22 Splitcap
- body/stage: B02 Domino -> 4-cell authored growth footprint derived from B03-style extension, no new body-plan family;
- profile: Sensitive stress, Standard contamination;
- traits: T06 Filter Feeder + T08 Growth Trigger + T03 Alarm Emitter;
- role: mastery species that turns successful filtering into future size and possible social instability;
- useful partners: bounded contamination sources, Hushling/Baffle;
- dangerous partners: tight holds and uncontrolled feed/filter loops;
- lifecycle: grows after sustained contamination consumption/satiety; alarm only while agitated/panicked;
- readability hook: cap visibly separates into four lobes before growth;
- tiers: 6 / authored mastery and validated generation only;
- exclusions: excluded from discovery and low-tier generation; solver must verify future footprint and post-growth adjacency.

---

# 5. Hold families and layout grammar

Launch uses five hold families. Families alter topology/fixtures only; none adds a new simulation subsystem.

## HF1 Open Crate
Purpose: teach relationships clearly.
- mostly rectangular usable grid;
- 5x5 to 6x5;
- 1–2 utility fixtures;
- optional single bed fixture;
- broad zones.

Launch layouts: H01 Training Crate, H02 Long Crate, H03 Twin-Fixture Crate.

## HF2 Split Hold
Purpose: create separation/bridge decisions.
- partial wall/blocked-cell spine;
- baffle-compatible boundary;
- port/starboard zones;
- 2 utility fixtures;
- 5x6 to 6x6.

Layouts: H04 Split Hold, H05 Offset Split, H06 Narrow Gate.

## HF3 Bent Hold
Purpose: challenge template reuse and directed/growth planning.
- irregular L/bent usable area;
- 2–3 utility fixtures;
- uneven zone sizes;
- some edge cells unavailable.

Layouts: H07 Bent Hold, H08 Hook Hold.

## HF4 Service Bay
Purpose: make fixture competition central.
- moderate cargo area but dense utility/bed fixture topology;
- route power capacity is comparatively tight;
- no special runtime rule beyond existing fixtures/power.

Layouts: H09 Service Bay, H10 Cross-Fixture Bay.

## HF5 Constricted Vault
Purpose: mastery spatial pressure.
- 7x6 to 9x7 bounding area but with 20–35% blocked cells;
- pockets connected by 1–2-cell necks;
- directional species and future growth become important;
- larger visual footprint without higher organism count.

Layouts: H11 Three-Pocket Vault, H12 S-Corridor Vault.

### Hold-generation limits
Generated contracts use authored layouts only at launch. The generator may select, rotate/mirror where symmetry rules permit, choose zone/hazard assignments, and choose fixture availability; it does **not** procedurally invent arbitrary grid topology at launch. This preserves readability and solver reliability.

---

# 6. Route hazard families

Seven launch hazard families, all expressible through existing route/hold inputs.

## RH1 Thermal Surge
Adds bounded heat to named zones for a known tick window.
Teaching use: simplest route-to-organism causal link.

## RH2 Contamination Leak
Adds contamination to named source cells/zones for a known window.
Teaching use: persistence, filters, filter feeders.

## RH3 Vibration Burst
Adds a short stress-field event and wakes ASLEEP organisms according to existing wake rules.
Teaching use: sleep timing and social cascades.

## RH4 Brownout
Reduces available powered-support capacity for a known window.
Teaching use: support priority and loss of mitigation.

## RH5 Vent Cycle
Applies existing contamination decay/vent modifier for a known window and may also apply a small heat-removal modifier if the route profile declares it through existing channel input.
Teaching use: timing beneficial route events; no new channel.

## RH6 Thermal Gradient
Applies different heat input to two declared zones during the same window.
Teaching use: orientation/zone tradeoff and anti-template pressure.

## RH7 Maintenance Oscillation
A deterministic sequence composed only of existing inputs, e.g. short brownout followed several ticks later by vibration or vice versa. It is stored as a route profile, not a new effect type.
Teaching use: multi-event temporal planning.

### Hazard sequencing limits
- Tier 0–1: 0–1 active family;
- Tier 2: max 1 family, optionally two non-overlapping events;
- Tier 3: max 2 families;
- Tier 4–5: max 3 families, with no more than 2 simultaneously active;
- Tier 6: max 4 families, still no more than 2 simultaneous unless an authored final contract explicitly demonstrates readability;
- no normal route exceeds 24 ticks;
- first exposure to a family uses exact timing and intensity;
- hidden/bounded uncertainty is reserved for discovery content and never overlaps two unknown hazard dimensions.

---

# 7. Campaign architecture — 48 authored contracts

The campaign is divided into six chapters of eight contracts. Chapter boundaries are mechanical teaching boundaries, not large narrative episodes.

## Chapter 1 — Read the Hold (C01–C08)
Goal: learn placement, orientation, one source/sink, first route consequence.

Introductions:
- C01 placement and launch with Dot species;
- C02 Hushling soothing relationship;
- C03 Ember Pod heat/alarm;
- C04 Frost Finch heat sink;
- C05 first Thermal Surge;
- C06 first Domino orientation;
- C07 first Silver/Gold welfare objective;
- C08 milestone: one route hazard creates a state change that activates a second trait.

Available supports: none until C06; Cooler first appears C07.

## Chapter 2 — Useful Neighbors (C09–C16)
Goal: cluster/separate tradeoffs and contamination.

Introductions:
- Mire Sipper;
- Spore Bell;
- Contamination Leak;
- Filter;
- Silt Grazer;
- Baffle;
- first growth planning;
- first generated-style recombination contract at C15;
- C16 milestone combines contamination feeding + future footprint.

## Chapter 3 — Plan for Later (C17–C24)
Goal: lifecycle timing, feeding, sleep/wake.

Introductions:
- Cradle Moss;
- Glass Larva;
- Feed Cartridge;
- Nest Pad;
- Vibration Burst;
- Cinder Snail;
- Moth Cushion;
- Warmback;
- C24 milestone: wake window + growth window + one support tradeoff.

## Chapter 4 — Protect the Weak Link (C25–C32)
Goal: cascades and scarce mitigation.

Introductions:
- Pulse Mite;
- Velvet Nurse;
- Rattle Reed / directed overlay;
- Brownout;
- Service Bay hold family;
- power priority;
- Coal Urchin;
- Whistle Crab;
- C32 milestone: 4-step deterministic cascade that can be interrupted in at least two distinct ways.

## Chapter 5 — Discover, Don’t Guess (C33–C40)
Goal: bounded uncertainty and codex discovery.

Discovery sequence:
- C33 first Monitor Beacon observation contract;
- C34 Lantern Tick undocumented recovery-pulse family clue;
- C35 exact documentation and normal use;
- C36 Pale Drifter discovery with bounded wake clue;
- C37 exact documentation;
- C38 Spindle Bloom advanced lifecycle;
- C39 Amber Leech dependency relationship;
- C40 milestone: unknown route detail where Monitor competes with mitigation but Bronze remains conservatively solvable.

Rule: every discovery contract unlocks exact documentation after unique causal observation; failure carries no persistent loss.

## Chapter 6 — No Familiar Template (C41–C48)
Goal: mastery recombination, irregular holds, strict optional medals.

Introductions:
- Ash Sponge as advanced composite if not already shown in optional content;
- Splitcap mastery species;
- Constricted Vault family;
- Thermal Gradient;
- Maintenance Oscillation;
- contracts intentionally vary which familiar helper is a liability.

C43–C47 are six-system recombination tests but still keep causal chains for Bronze explainable.

### C48 Final campaign test — “Living Manifest”
Requirements:
- irregular authored vault;
- 7–9 organisms drawn from at least five learned role families;
- one lifecycle species;
- one beneficial-dangerous composite species;
- three known route hazard families in non-chaotic sequence;
- power/fixture pressure;
- at least two valid Bronze strategy families confirmed by solver;
- Gold requires efficient support use plus welfare stability, never intentional harm;
- no new rule, species behavior, or hidden fact appears here.

The final contract proves model-building and recombination rather than memorization.

---

# 8. Authored vs generated content split

## Authored
Always authored:
- the 48 campaign contracts;
- all first introductions of species, supports, holds, hazards, and trait families;
- all discovery contracts;
- the final six mastery contracts;
- tutorial text/cues;
- flavor framing of milestone shipments;
- hold layouts at launch.

## Generated/recombined
Generator may vary:
- manifest from unlocked/documented species pools;
- starting meters within validated bands;
- orientation choices;
- authored hold selection plus permitted mirror/rotation variant;
- support allowance from validated pools;
- route profile/timing from validated hazard templates;
- mandatory/medal predicate templates;
- deterministic seed.

Generator does not create new trait definitions, new species compositions, arbitrary dialogue, arbitrary hold topology, or hidden mechanics.

---

# 9. Generated challenge pipeline

Every generated challenge passes all stages before exposure to the player.

## Stage 1 — Seeded assembly
Input:
- generator version;
- deterministic seed;
- difficulty tier;
- unlocked/documented content set;
- requested challenge family.

Select hold, route template, manifest, starting states, support allowance, predicates.

## Stage 2 — Structural validation
Reject if:
- manifest cannot physically fit at t=0;
- required support fixtures do not exist;
- mandatory target is impossible by definition;
- a growth species has no legal future configuration when the challenge does not explicitly allow blocked growth as pressure;
- trait composition violates species/exclusion rules.

## Stage 3 — Candidate solution construction
Use one or both:
1. construct from known-valid heuristic layout families;
2. bounded search over placements/orientations/support assignments using the authoritative deterministic simulator.

A launch challenge must have at least one proven Bronze solution.

Tier 4+ generated challenges should target at least **two materially distinct Bronze solution families** where tractable, defined as differing in at least one of support loadout, zone allocation, or key adjacency/growth reservation—not merely symmetric cell swaps.

## Stage 4 — Medal validation
- prove Bronze;
- prove Silver if offered;
- prove Gold if offered;
- reject a Gold predicate set if no valid solution found within the certified search budget;
- reject medals whose only solution causes worse mandatory welfare than a simpler Bronze route unless the objective itself is a transparent tradeoff that remains ethically/product-consistent.

## Stage 5 — Causal-opacity rejection
For at least one canonical Bronze solution and one plausible near-miss:
- generate causal graph from event log;
- identify mandatory-failure path;
- reject if the shortest useful explanation exceeds **6 major causal links** below Tier 6;
- Tier 6 allows up to **8** only if the UI groups repeated channel propagation into one understandable event family;
- reject if more than two unseen-by-player state changes must be remembered simultaneously to explain failure.

## Stage 6 — Transit significance test
Reject if:
- success can be predicted entirely from t=0 legal fit/static adjacency and route adds no meaningful state change;
- changing transit length/hazard timing within template-safe bounds has no strategic effect;
- no organism state/footprint/environmental relationship changes after launch.

Tutorial generator is exempt because tutorials remain authored anyway.

## Stage 7 — Anti-template diversity
Compare candidate against recent generated challenges and a library of dominant strategy fingerprints.

Fingerprint dimensions:
- hold family;
- manifest role histogram;
- key pressure channels;
- lifecycle present yes/no;
- required cluster/separate relation count;
- powered-support optimal set;
- major route hazard sequence;
- canonical solution zone allocation.

Reject or down-rank if similarity score exceeds **0.80** against any of the last 5 surfaced challenges, or if the same powered-support pair is optimal in more than 3 consecutive surfaced challenges.

## Stage 8 — Difficulty calibration
A challenge must fit its tier envelope for organism count, pressure families, hazards, support complexity, and discovery information.

Difficulty is not inferred solely from solver node count. Solver effort is a secondary signal because human difficulty depends on explanation structure.

## Stage 9 — Freeze record
Persist:
- generator version;
- content-definition version;
- seed;
- all selected IDs and numeric starting parameters;
- medal predicate version;
- validation result hash;
- at least one certified solution fingerprint for QA, hidden from normal player UI.

This ensures exact reproduction after bug reports and save/reload.

---

# 10. Narrative and flavor framing

The fiction must make species memorable without becoming dialogue-heavy.

## 10.1 Player role
The player is a specialist cargo ecologist/containment planner working for an inter-habitat transport service. The organization exists mainly to justify manifests, safety rules, route conditions, and increasingly unusual living cargo.

## 10.2 Contract framing
Each authored contract uses at most:
- a shipment title;
- one-sentence client/context line;
- manifest notes;
- one optional arrival note after completion.

No branching dialogue is required.

## 10.3 Species memory aids
Every species has:
- common name;
- silhouette/icon;
- 1–2 sentence ecological note;
- exact mechanical trait summary once documented;
- one memorable handling sentence.

Example handling voice: “Warmbacks protect delicate neighbors from residue, but their plates run hot. Give the protected passenger room to breathe.”

## 10.4 Tone
Curious, competent, lightly strange, not grim body horror. Organisms can look odd but should be readable as living cargo with welfare worth preserving. Failure presentation emphasizes stress/unsafe delivery rather than gore.

## 10.5 Environmental storytelling
Flavor comes from:
- destination/source tags;
- shipping labels;
- habitat stamps;
- prior-handler notes;
- species nicknames;
- visual wear on crates/supports.

None is mechanically authoritative unless mirrored in explicit rule UI.

---

# 11. Content data schemas

These are conceptual implementation schemas. Exact serialization syntax belongs to Phase 8.

## 11.1 SpeciesDefinition
- `species_id`
- `display_name_key`
- `body_plan_id`
- `starting_stage`
- `stage_definitions[]`
- `legal_orientations[]`
- `stress_profile_id`
- `contamination_profile_id`
- `satiety_profile`
- `trait_instances[]`
- `compatibility_tags[]`
- `passive_readability_tags[]`
- `generator_tier_min`
- `generator_tier_max`
- `generator_exclusions[]`
- `discovery_definition_id?`
- `presentation_profile_id`
- `content_version`

## 11.2 TraitInstance
- `trait_family_id`
- `parameter_band_id`
- `state_gate`
- `target_selector`
- `range_model`
- `effect_parameters`
- `delay_ticks?`
- `capacity?`
- `compatibility_tags[]`
- `ui_summary_key`
- `causal_log_key`

No arbitrary executable callback field is allowed in content data.

## 11.3 HoldDefinition
- `hold_id`
- `family_id`
- `width`, `height`
- `usable_cells[]`
- `blocked_cells[]`
- `utility_fixtures[]`
- `bed_fixtures[]`
- `zones[]`
- `baffle_boundaries[]`
- `power_capacity`
- `legal_symmetry_transforms[]`
- `tier_range`
- `content_version`

## 11.4 RouteDefinition
- `route_id`
- `tick_count`
- `hazard_events[]`
- `known_information_policy`
- `uncertainty_bounds?`
- `base_power_available`
- `zone_modifiers[]`
- `tier_range`
- `content_version`

Each hazard event has type, tick start/end, intensity band/value, target zone/cells, and reveal policy.

## 11.5 ContractDefinition
- `contract_id`
- `chapter_index`
- `difficulty_tier`
- `hold_id`
- `route_id`
- `manifest_instances[]`
- `starting_meter_overrides[]`
- `support_allowance`
- `mandatory_predicates[]`
- `silver_predicates[]`
- `gold_predicates[]`
- `knowledge_overrides[]`
- `tutorial_steps[]?`
- `unlock_rewards[]`
- `flavor_id`
- `certified_solution_fingerprints[]` (dev/QA only)
- `content_version`

## 11.6 FlavorVariant
- `flavor_variant_id`
- `species_id`
- `palette/material variant`
- `pattern/accessory set`
- `display-only tags`
- `mechanical_equivalence_group`

Invariant: two flavor variants in one equivalence group serialize identical mechanics.

## 11.7 DocumentationState
Per profile:
- documented species IDs;
- documented trait-family facts;
- observed-but-not-documented clue IDs;
- support codex unlocks;
- route-hazard codex unlocks;
- campaign chapter/contract completion;
- best medal per authored contract;
- generated challenge history seeds/fingerprints.

---

# 12. Demo specification

Demo content is fixed and intentionally not a random slice of the campaign.

## Included species
O01 Ember Pod, O02 Hushling, O03 Silt Grazer, O04 Spore Bell, O06 Cradle Moss, O07 Pulse Mite, O08 Glass Larva, O10 Frost Finch, O14 Mire Sipper, plus O13 Cinder Snail as the single bounded discovery species.

## Included supports
- Cooler;
- Filter;
- Baffle;
- Feed Cartridge.

## Included hazards
- Thermal Surge;
- Contamination Leak;
- Vibration Burst.

## Included holds
- Training Crate;
- Long Crate;
- Split Hold.

## Contract arc
D01 placement/orientation;
D02 Hushling + Ember Pod;
D03 Thermal Surge;
D04 Frost Finch capacity limit;
D05 contamination leak + Mire Sipper;
D06 Spore Bell persistence;
D07 Silt Grazer future growth;
D08 support choice: Filter vs no-powered Gold path;
D09 bounded Cinder Snail discovery;
D10 finale: growth timing + thermal route event + competing proximity.

## Explicitly outside demo
- Nest Pad;
- Monitor Beacon;
- Brownout/power-priority interaction;
- Service Bay/Constricted Vault;
- Ash Sponge and other 3-trait mastery species;
- Pale Drifter wake-cleansing discovery;
- advanced generated challenges;
- Chapter 5–6 content;
- final campaign mastery contract.

The demo save may carry only a small cosmetic acknowledgment into the full game; no mechanical power bonus is required.

---

# 13. Phase-5 acceptance checklist

Phase 5 passes only if all are true:

- [x] exact MVP/demo/launch counts defined;
- [x] launch species roster contains 18–24 compositions — final count 22;
- [x] every species uses only B01–B04 and T01–T10 plus already-frozen state/feeding variants;
- [x] no normal species exceeds 3 significant traits;
- [x] numeric parameter bands are systematic;
- [x] every species has a role, readable hook, useful/dangerous relationships, tier limits, and generator exclusions where needed;
- [x] hold families/layout target defined without procedural topology scope creep;
- [x] route hazard families are compositions of existing channel/state/power inputs;
- [x] hazard sequencing limits defined;
- [x] 48-contract campaign teaching order defined;
- [x] discovery placement and safety rules preserved;
- [x] final campaign test contains no new mechanic;
- [x] authored/generated boundary explicit;
- [x] generation pipeline proves Bronze and medals before surfacing content;
- [x] causal-opacity rejection explicit;
- [x] anti-template diversity metric explicit;
- [x] deterministic seed/version/freeze record explicit;
- [x] narrative framing adds memory without dialogue burden;
- [x] data schemas defined for required content families;
- [x] demo content and exclusions explicit;
- [x] no content item requires reopening the Phase-4 global tick architecture.

**Result: PASS. Phase 5 content architecture is closed.**

---

# 14. Frozen Phase-5 decisions and forward obligations

Frozen for subsequent design unless a contradiction is discovered:
- launch target is 22 mechanically distinct species;
- 4 body plans remain sufficient;
- 10 trait families remain sufficient;
- 6 supports remain sufficient;
- 5 hold families / 12 authored launch layouts;
- 7 route-hazard families;
- 48 authored campaign contracts in 6 chapters;
- 24 generated challenge templates;
- generator selects/composes validated content but does not invent traits/species/topology;
- first-clear campaign target 8–12 hours;
- demo target 10 authored contracts and 60–90 minutes;
- no new rule in final campaign test.

Forward phases must now specify **how the player perceives and operates this content** (Phase 6), then progression/commercial structure (Phase 7), technical implementation contracts (Phase 8), and whole-game/adversarial freeze passes.
