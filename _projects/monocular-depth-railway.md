---
layout: page
title: Monocular Depth-Driven 3D Railway Scene Reconstruction
description: Combining learned depth, LiDAR anchors, and semantic boundary constraints.
importance: 2
category: Research
permalink: /projects/monocular-depth-railway/
---

<!-- TODO: add railway reconstruction and LiDAR/depth fusion images -->

## Overview

After the first project, I expected pretrained visual models to provide a stronger route to dense reconstruction and wanted to test that assumption. This project integrated multi-frame LiDAR, frustum-based point aggregation, monocular depth estimation, LiDAR-based metric correction, semantic segmentation, and boundary constraints.

## Problem and Failure

Depth predictions appeared dense and visually coherent in image space. However, after back-projecting them into 3D, some long-range structures showed inaccurate relative distances.

> **Visual completeness did not guarantee metric correctness.**

## System Design

The system gives each component a distinct role:

- **Depth** provides dense structural information.
- **LiDAR** provides sparse but metrically reliable anchors.
- **Segmentation** provides object-boundary constraints that prevent incorrect cross-object interpolation.

## My Contribution

- Proposed multi-frame frustum LiDAR fusion.
- Proposed LiDAR-based correction of monocular depth.
- Worked on the integration of pretrained segmentation as boundary constraints.

## Takeaway

Learning and geometry should not be treated as competing alternatives. Learned models provide rich priors and dense information; geometry and sensor measurements provide reliability constraints.

### Project Report

_Sparse Point Cloud 3D Railway Scene Reconstruction Driven by Monocular Metric Depth Estimation_ — Project Final Technical Report.
