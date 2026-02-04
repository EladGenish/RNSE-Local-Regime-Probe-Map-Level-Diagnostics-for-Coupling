RNSE Local Regime Probe

Map-Level Diagnostics for χ–Λ Coupling

This repository contains a diagnostic probe for the Recursive Null-Seed Engine (RNSE), designed to test local regime separability using map-level measurements rather than global scalars.

The goal is not to characterize engine internals, convergence, or optimization behavior, but to evaluate observer-side validity: whether structured inputs produce distinguishable, localized observable regimes under controlled coupling.

What This Tests (and What It Does Not)

This probe tests:

Whether local burst structure (χ) induces local latency structure (Λ) when coupling κ > 0

Whether regimes collapse when κ = 0

Whether separation is observable using pre-declared, replayable diagnostics

This probe does NOT test:

Global convergence or closure

Engine halt/acceptance behavior

Task performance or optimization

Any specific downstream application

All measurements are external diagnostics.
The engine continues running regardless of regime classification.

Experimental Design (High Level)

A 2D lattice is evolved under RNSE dynamics.

Two event patterns are compared:

Bursty (localized, clustered events)

Diffuse (spatially uniform events)

A sweep over κ ∈ {0.00, 0.05, 0.10, 0.15, 0.20} is performed.

Measurements are taken locally (region-of-interest probes), not via global averages.

Regime classification is based on local Λ separation, not scalar means.

This avoids averaging out structure and preserves spatial signal.

Repository Structure
rnse_probe/
├── config.json          # Full experimental configuration (seeds, grid, ticks, κ sweep)
├── sweep_summary.json   # Aggregate results for all κ values
├── digests.json         # SHA256 digests for scripts and outputs (integrity)
├── kappa_0.000/
│   └── maps.npz         # χ and Λ maps for κ = 0.000
├── kappa_0.050/
│   └── maps.npz
├── kappa_0.100/
│   └── maps.npz
├── kappa_0.150/
│   └── maps.npz
├── kappa_0.200/
│   └── maps.npz
└── README.md


All files required to replay the diagnostic are present.
No engine internals are required.

Decision Rule (Pre-Declared)

A regime is classified as separated iff:

ΔΛ_local = Λ_bursty(ROI) − Λ_diffuse(ROI) > ε


under fixed variance and masking checks defined in config.json.

If κ = 0, collapse is expected and observed.
If κ > 0, local separation is expected and observed.

No post-hoc thresholds are introduced.

Reproducibility & Integrity

All runs are seed-controlled.

All outputs are logged.

Cryptographic digests are provided in digests.json.

A third party can replay the regime call without access to RNSE internals.

This repository is intentionally minimal and diagnostic-only.

Interpretation Scope

The observed regimes describe measurement sensitivity, not engine behavior.

They indicate:

Whether a measurement surface remains informative

Whether local structure survives observer aggregation

They do not imply:

Physical equivalence

Ontological claims

Optimization guarantees

Status

This probe is considered complete for its stated scope.

Future work may include:

Formal boundary logging

Cross-probe consistency checks

Additional diagnostic surfaces

Those extensions are orthogonal to the results presented here.

License / Use

This repository is provided for evaluation, replay, and audit of the diagnostic protocol only.

No permission is granted to infer, reconstruct, or claim access to RNSE engine internals.
