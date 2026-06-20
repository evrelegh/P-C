# Computational Actuarial Representation Benchmark

How does *representation geometry* — the way categorical rating factors are encoded —
propagate through the actuarial pipeline? Not only into pricing discrimination, but into
latent segmentation, aggregate portfolio behaviour, capital metrics, and reinsurance
sensitivity. This project investigates that question on the freMTPL2 motor insurance
benchmark (678,013 policy-years), combining Tweedie pricing, Gaussian-mixture
segmentation, Burt latent representations, and FFT-based analytic aggregate risk.

The work is in two stages: a linear (GLM) study, and a non-linear extension that tests
which of its findings survive a gradient-boosted learner.

---

## Stage 1 — The GLM study

Tweedie GLM pricing across three representation families (classical one-hot, Burt-replacing,
Burt-augmented), with soft GMM segmentation and analytic compound-Poisson aggregation
replacing Monte Carlo simulation.

**Headline findings**
- Soft GMM segmentation on an enriched feature space improves discrimination by ~5.5 Gini
  points over the plain GLM baseline; hard K-means on the same geometry does not — soft
  probabilistic assignment is essential.
- The Burt representation trades ~4.5 Gini points for better top-decile calibration and a
  lower aggregate tail (TVaR 99% ~€85k below the classical model, ground-up).
- A reinsurance-dependent **coverage-layer reversal**: Burt wins ground-up and under a
  deductible; the classical geometry wins under a per-claim limit.
- Segment-level severity CVs estimated empirically (≈1.1–1.8, roughly double the
  conventional fixed assumption) materially affect the tail (~€500k on TVaR 99%).

→ `technical_note.pdf` · `executive_summary.pdf`

## Stage 2 — The gradient boosting extension

The Tweedie GLM is replaced by a gradient-boosted Tweedie learner, holding the dataset,
the Burt geometry, and the GMM segmentation fixed, with discrimination measured
out-of-fold. The single question: which Stage 1 findings are properties of the *linear
model*, and which are properties of the *representation geometry*?

**Headline findings** *(stable across two fold partitions)*
- The discrimination gap **narrows by ~23% but does not collapse** — about four fifths
  survives. It is partly, not wholly, an artefact of the linear model.
- Informational completeness of the Burt coordinates **persists** under a tree free to
  exploit both encodings.
- The aggregate capital findings — lower ground-up tail and the coverage-layer reversal —
  are **reproduced almost unchanged**, suggesting they are properties of the segmentation
  geometry rather than the pricing model.
- One caveat: top-decile *calibration* of the Burt representation is partition-sensitive
  and should be read as a distribution, not a point estimate.

→ `gradient_boosting_extension.pdf`

---

## Repository

| File | Contents |
|------|----------|
| `motor_burt_benchmark.ipynb` | Full notebook — 11 sections, GLM study (1–10) and GBM extension (11) |
| `technical_note.pdf` | Stage 1 technical note |
| `executive_summary.pdf` | Stage 1 executive summary |
| `gradient_boosting_extension.pdf` | Stage 2 extension note |

## Stack
Python · pandas · scikit-learn · glum · LightGBM · [aggregate](https://github.com/mynl/aggregate) (FFT compound-Poisson convolution) · out-of-fold cross-fitting

## Data
freMTPL2 (French motor third-party liability), available via the `CASdatasets` R package
and OpenML. Not redistributed here; the notebook expects a local cache (see Cell 1.1).

## Status
Research / experimental.

*Idem mutatus resurgo.*
