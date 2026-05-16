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

- Soft probabilistic segmentation materially improves discrimination over the plain GLM baseline.
- Burt-based latent representations trade some discrimination for improved calibration and more moderate aggregate tail behaviour.
- The Burt-augmented representation adds almost no lift beyond the Burt-only representation, suggesting strong informational redundancy.
- Coverage-layer analysis shows that the preferred representation can change under deductible versus per-claim-limit structures.
- Heavy-tailed severity distributions create numerical instability within FFT aggregation frameworks despite superior local fit.

## Technologies

Python · pandas · scikit-learn · glum · aggregate · FFT convolution

## Status

Research / experimental.
