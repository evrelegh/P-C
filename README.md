# Computational Actuarial Representation Benchmark
Computational actuarial experiments on representation geometry, latent segmentation and FFT-based aggregate risk modelling using the freMTPL2 motor insurance benchmark.

## Overview
This project investigates how representation engineering propagates through the actuarial pipeline:
- pricing discrimination,
- latent segmentation,
- aggregate portfolio behaviour,
- capital metrics,
- and reinsurance sensitivity.

The benchmark combines:
- Tweedie GLMs,
- Gaussian Mixture Models,
- Burt latent representations,
- and FFT-based aggregate risk analytics.

## Main Findings
- Soft GMM segmentation on an actuarially enriched feature space improves pricing discrimination by approximately 5.5 Gini points over the plain GLM baseline. Hard K-means on the same geometry falls below the baseline in at least one configuration — soft probabilistic assignment is essential.
- The best-calibrated Burt experiment (B5, GMM enriched k=8) achieves a top-decile ratio of 1.032 against the best classical experiment (A5) at 1.139, and produces a TVaR 99% approximately €85,000 lower. The Gini gap of 4.5 points is specific to the Tweedie GLM and is expected to narrow under non-linear models.
- The Burt-augmented C-series produces results identical to the Burt-replacing B-series to four decimal places of Gini, confirming informational completeness. The canonical comparison is therefore A-series (classical) versus B-series (Burt-replacing).
- Segment-level severity CVs estimated empirically from observed claims range from 1.1 to 1.8 — roughly double a conventional fixed assumption — with a material impact on TVaR (approximately €500,000).
- Coverage-layer analysis reveals a reinsurance-dependent reversal: under a deductible, B5 produces a lower TVaR 99% by €550,000; under a per-claim limit, the ranking reverses in favour of A5 by €478,000.
- Burr XII and log-logistic distributions fit the claim severity substantially better than lognormal by AIC, but their fitted parameters imply near-infinite higher moments, making them incompatible with FFT aggregation. Lognormal with empirical CV is retained for tractability.

## Technologies
Python · pandas · scikit-learn · glum · aggregate · FFT convolution

## Status
Research / experimental.
