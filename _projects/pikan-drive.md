---
layout: page
title: PIKAN-Drive
description: From PilotNet steering regression to Fast-BEV 3D detection.
importance: 4
category: Research
permalink: /projects/pikan-drive/
---

<!-- TODO: add PilotNet and Fast-BEV experiment figures -->

## Overview

At UC Irvine, I studied KAN and physics-informed learning for autonomous driving, extending work from PilotNet steering regression to Fast-BEV 3D detection. The research direction, PilotNet baseline, and KAN starting point were provided by my supervisor.

## My Contribution

- Proposed physics-informed constraints.
- Extended the study from PilotNet to Fast-BEV.
- Designed Full9 auxiliary losses and targeted V2 ablations.
- Conducted most training, experiments, analysis, and the final presentation.

## PilotNet Steering Regression

| Model        |   MAE |  RMSE |
| ------------ | ----: | ----: |
| MLP baseline | 3.616 | 6.825 |
| KAN baseline | 3.301 | 6.281 |
| Best PI-KAN  | 3.209 | 6.163 |

Compared with the MLP baseline, the best PI-KAN result reduced MAE by **11.3%** and RMSE by **9.7%**.

## Fast-BEV 3D Detection

For classification, regression, and direction, I designed grouped auxiliary constraints. Full9 did not outperform the baseline, so I followed with targeted ablations.

> **More constraints ≠ better models.**

A physically reasonable constraint does not automatically become an effective training objective. Auxiliary objectives must align with the task, evaluation metric, and architecture.
