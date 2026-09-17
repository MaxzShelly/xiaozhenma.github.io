---
layout: page
title: Research
permalink: /research/
description: 3D reconstruction, geometric reasoning, and reliable spatial perception.
nav: true
nav_order: 2
---

## Sparse Point Cloud Reconstruction of High-Speed Train Head Geometry

My research explores how machines can recover reliable 3D structure when observations are sparse, incomplete, or uncertain. A central project in this direction is the reconstruction of streamlined high-speed train head geometry from sparse LiDAR observations.

The work used a portable sensing system combining LiDAR, cameras, and an IMU, with FAST-LIVO2 as the multi-sensor SLAM backbone. The goal was to recover a sufficiently continuous geometric representation for surface reconstruction, rather than merely collecting a point cloud.

<div class="row row-cols-1 row-cols-md-2 g-4 my-4">
  <div class="col"><figure class="mb-0 border rounded p-2 h-100"><img class="img-fluid rounded" src="{{ '/assets/img/train-reconstruction/01_train_head_photo.png' | relative_url }}" alt="Physical high-speed train head"><figcaption class="text-muted small mt-2">Physical high-speed train head.</figcaption></figure></div>
  <div class="col"><figure class="mb-0 border rounded p-2 h-100"><img class="img-fluid rounded" src="{{ '/assets/img/train-reconstruction/02_sparse_lidar_scan.png' | relative_url }}" alt="Sparse LiDAR scan of the high-speed train head"><figcaption class="text-muted small mt-2">Sparse LiDAR scan. Window regions contain particularly significant missing returns.</figcaption></figure></div>
</div>

## The Research Question

Glass surfaces often produce large regions with few or no valid LiDAR returns. Direct interpolation becomes unreliable because the missing region has little local geometric support; directly meshing the sparse cloud can also create surfaces that do not correspond to the actual train geometry.

> **How can we identify the geometry of a missing region when the region itself contains almost no observations?**

## Missing-Region Reasoning

Instead of detecting boundaries only among existing points, I represented the problem through explicit missing regions. The point cloud was projected onto three orthogonal planes, where holes that were difficult to recognise directly in 3D became visible from complementary 2D views.

```text
Sparse point cloud → tri-axial projection → hole-point generation
→ missing-region clustering → reverse hole-boundary extraction
→ multi-directional interpolation → fusion → surface reconstruction
```

This changes the question from _“Where does the observed surface end?”_ to _“Where should points exist but do not, and what observed geometry surrounds that empty region?”_

<figure class="my-4 border rounded p-2">
  <img class="img-fluid rounded" src="{{ '/assets/img/train-reconstruction/03_triaxial_projection.png' | relative_url }}" alt="Tri-axial projection diagram of the train point cloud">
  <figcaption class="text-muted small mt-2">Tri-axial projection. Different orthogonal views expose missing regions that are difficult to identify directly in the original 3D point cloud.</figcaption>
</figure>

## Results and Perspective

The original scan covered approximately 90% of the train-head geometry, while the largest holes were concentrated around glass surfaces. Explicit missing-region detection and multi-directional interpolation substantially recovered the side-window regions; one rear area remained incomplete because surrounding boundary observations were insufficient.

After point-cloud completion, Greedy Triangulation, Poisson Reconstruction, and Marching Cubes were compared. Greedy Triangulation best preserved the completed curved train-head geometry in the project experiments and was selected for the final pipeline.

<div class="row row-cols-1 row-cols-md-2 g-4 my-4">
  <div class="col"><figure class="mb-0 border rounded p-2 h-100"><img class="img-fluid rounded" src="{{ '/assets/img/train-reconstruction/04_hole_before_top.png' | relative_url }}" alt="Top view before missing-region completion"><figcaption class="text-muted small mt-2">Before completion — top view.</figcaption></figure></div>
  <div class="col"><figure class="mb-0 border rounded p-2 h-100"><img class="img-fluid rounded" src="{{ '/assets/img/train-reconstruction/05_hole_after_top.png' | relative_url }}" alt="Top view after missing-region completion"><figcaption class="text-muted small mt-2">After completion — top view.</figcaption></figure></div>
  <div class="col"><figure class="mb-0 border rounded p-2 h-100"><img class="img-fluid rounded" src="{{ '/assets/img/train-reconstruction/06_hole_before_side.png' | relative_url }}" alt="Side view before missing-region completion"><figcaption class="text-muted small mt-2">Before completion — side view.</figcaption></figure></div>
  <div class="col"><figure class="mb-0 border rounded p-2 h-100"><img class="img-fluid rounded" src="{{ '/assets/img/train-reconstruction/07_hole_after_side.png' | relative_url }}" alt="Side view after missing-region completion"><figcaption class="text-muted small mt-2">After completion — side view.</figcaption></figure></div>
</div>

## Current Direction

This project shaped my broader interest in **3D perception and spatial intelligence**: combining learned priors, explicit geometry, sensor observations, and uncertainty to build 3D representations that are reliable and useful for real-world reasoning and action.

<p class="mt-4"><a href="{{ '/projects/sparse-train-reconstruction/' | relative_url }}">Read the full project case study →</a></p>
