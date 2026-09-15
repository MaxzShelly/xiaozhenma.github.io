---
layout: page
title: Sparse Point Cloud Reconstruction of High-Speed Train Head Shapes
description: Rethinking missing-region reconstruction from sparse LiDAR observations.
importance: 1
category: Research
permalink: /projects/sparse-train-reconstruction/
---

<!-- TODO: add high-speed train sparse point cloud image -->
<!-- TODO: add missing-window and before/after completion images -->

## Overview

This project investigated high-precision reconstruction of streamlined high-speed train geometry from sparse LiDAR observations. The sensing system combined LiDAR, cameras, and IMUs, with FAST-LIVO2 used for multi-sensor point-cloud acquisition.

## Problem

Glass windows caused severe LiDAR return loss. In several regions, almost no valid points existed inside the missing area, while the surrounding observations were also extremely sparse. Direct interpolation lacked reliable support, while direct surface reconstruction could connect noise and sparse points into incorrect surfaces.

## Approach

I changed the representation of the problem. Instead of detecting hole boundaries only from existing points, I projected the 3D point cloud onto multiple orthogonal planes so that missing regions on differently oriented surfaces could be exposed in 2D.

> Tri-axial projection → hole-point generation → missing-region clustering → reverse boundary extraction → multi-directional interpolation → 3D fusion

## My Contribution

- Designed the tri-axial projection strategy and implemented the projection pipeline.
- Designed explicit hole-point generation and reverse hole-boundary reasoning.
- Designed and implemented multi-directional interpolation.
- Participated in sensor acquisition and reconstruction experiments.
- Independently wrote the final technical report.

FAST-LIVO2, moving least squares, DBSCAN, Greedy Triangulation, Poisson reconstruction, and Marching Cubes were existing methods or tools used in the broader pipeline; they are not presented here as my algorithmic inventions.

## Results

Model completeness improved from approximately **75% to 98%**.

### Research Report

_Three-Dimensional Surface Reconstruction of High-Speed Train Heads from Sparse Point Clouds_ — Technical Research Report.

## What I Learned

> The most important lesson from this project was that the representation of a problem can itself be part of the solution. When an existing approach repeatedly fails, changing how the problem is formulated may be more effective than continuing to optimise the same method.
