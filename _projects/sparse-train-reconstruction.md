---
layout: page
title: Sparse Point Cloud Reconstruction of High-Speed Train Head Geometry
description: Recovering missing surfaces by reasoning about empty regions, not only observed points.
importance: 1
category: Research
permalink: /projects/sparse-train-reconstruction/
---

This project investigated 3D reconstruction of streamlined high-speed train head geometry from sparse LiDAR observations. A portable sensing system combining LiDAR, cameras, and an IMU was used for data acquisition, with FAST-LIVO2 serving as the multi-sensor SLAM backbone. The objective was not simply to obtain a point cloud, but to recover a sufficiently continuous geometric representation for subsequent surface reconstruction.

<div class="row row-cols-1 row-cols-md-2 g-4 my-4">
  <div class="col"><figure class="mb-0 border rounded p-2 h-100"><div class="d-flex align-items-center" style="aspect-ratio: 832 / 357"><img class="img-fluid rounded" style="width: 100%; height: 100%; object-fit: contain" src="{{ '/assets/img/train-reconstruction/01_train_head_photo.png' | relative_url }}" alt="Physical high-speed train head"></div><figcaption class="text-muted small mt-2">Physical high-speed train head.</figcaption></figure></div>
  <div class="col"><figure class="mb-0 border rounded p-2 h-100"><img class="img-fluid rounded" src="{{ '/assets/img/train-reconstruction/02_sparse_lidar_scan.png' | relative_url }}" alt="Sparse LiDAR scan of the high-speed train head"><figcaption class="text-muted small mt-2">Sparse LiDAR reconstruction; missing returns are especially visible around glass-window regions.</figcaption></figure></div>
</div>

## Problem: Missing Regions Are Not Ordinary Noise

Sparse sensing errors were not uniformly distributed. Glass surfaces produced large regions with few or no valid LiDAR returns, while nearby observations also remained sparse. This created two linked difficulties:

- **Interpolation lacked geometric support.** With very few neighbouring points, directly estimating a missing surface from local observations became unreliable.
- **Surface reconstruction could create incorrect geometry.** Meshing the sparse point cloud directly could connect unrelated points or noise into surfaces that did not correspond to the actual train geometry.

The core question became:

> **How can we identify the geometry of a missing region when the region itself contains almost no observations?**

## Reframing the Task as Missing-Region Reasoning

<div class="row align-items-center g-4 my-4">
  <div class="col-12 col-md-6">
    <p>Instead of searching only for boundaries among observed 3D points, the method changes the representation of the problem. The point cloud is projected onto three orthogonal planes, where a missing surface that is difficult to identify directly in 3D can become more visible from one projected view.</p>
    <p class="mb-0">The method explicitly represents empty regions as <strong>hole points</strong>. Rather than asking where a boundary lies among already observed points, it asks where points should exist but do not, and what observed geometry surrounds that empty region.</p>
  </div>
  <div class="col-12 col-md-6 text-center">
    <img class="img-fluid rounded d-block mx-auto" src="{{ '/assets/img/train-reconstruction/reconstruction-pipeline.svg' | relative_url }}" alt="Sparse point cloud reconstruction pipeline">
  </div>
</div>

<figure class="my-4 border rounded p-2">
  <img class="img-fluid rounded w-50 d-block mx-auto" src="{{ '/assets/img/train-reconstruction/03_triaxial_projection.png' | relative_url }}" alt="Tri-axial projection of the train point cloud">
  <figcaption class="text-muted small mt-2">Tri-axial projection. Complementary orthogonal views expose missing regions that are difficult to identify directly in the original 3D point cloud.</figcaption>
</figure>

## Reverse Hole-Boundary Reasoning

A conventional boundary detector starts from existing observations and attempts to identify where an observed surface ends. That assumption becomes fragile when observations are extremely sparse.

The proposed approach reverses this reasoning:

> **empty region → hole cluster → hole boundary → observed boundary support**

After projection and spatial subdivision, regions without sufficient observations are explicitly represented as hole points. These points are clustered into individual missing regions. The boundary of each missing region is then used to search back into the original point cloud for surrounding geometric support. This formulation enables reasoning about missing surfaces even when almost no LiDAR points exist inside them.

## Multi-Directional Completion

Once the surrounding boundary support was identified, missing geometry was estimated with distance-weighted interpolation from multiple directions. Using observations from at least six directions reduced dependence on any single sparse neighbourhood and helped the reconstructed region transition smoothly into the surrounding train surface. Results from the three orthogonal projections were fused back into the original 3D coordinate system to form the completed point cloud.

### Project Contributions

- Designed and implemented the tri-axial projection strategy for exposing missing regions from complementary views.
- Designed explicit hole-point representation and reverse hole-boundary reasoning.
- Designed and implemented multi-directional interpolation for missing-surface completion.
- Participated in multi-sensor data acquisition and reconstruction experiments.
- Conducted comparative surface-reconstruction experiments.
- Independently organised and wrote the final technical report.

FAST-LIVO2, Moving Least Squares, DBSCAN, Greedy Triangulation, Poisson Reconstruction, and Marching Cubes were existing methods or open-source components used within the broader pipeline; they are not presented as my algorithmic inventions.

## Results

The original scan covered approximately 90% of the train-head geometry, with the most significant missing regions concentrated around glass surfaces. After missing-region detection and interpolation, the large window holes were substantially recovered. In the reported experiment, the side-window regions were completed, while one rear area remained incomplete because insufficient surrounding boundary observations were available.

<div class="row row-cols-1 row-cols-md-2 g-4 my-4">
  <div class="col"><figure class="mb-0 border rounded p-2 h-100"><img class="img-fluid rounded" src="{{ '/assets/img/train-reconstruction/04_hole_before_top.png' | relative_url }}" alt="Top view before missing-region completion"><figcaption class="text-muted small mt-2">Before completion — top view.</figcaption></figure></div>
  <div class="col"><figure class="mb-0 border rounded p-2 h-100"><img class="img-fluid rounded" src="{{ '/assets/img/train-reconstruction/05_hole_after_top.png' | relative_url }}" alt="Top view after missing-region completion"><figcaption class="text-muted small mt-2">After completion — top view.</figcaption></figure></div>
  <div class="col"><figure class="mb-0 border rounded p-2 h-100"><img class="img-fluid rounded" src="{{ '/assets/img/train-reconstruction/06_hole_before_side.png' | relative_url }}" alt="Side view before missing-region completion"><figcaption class="text-muted small mt-2">Before completion — side view.</figcaption></figure></div>
  <div class="col"><figure class="mb-0 border rounded p-2 h-100"><img class="img-fluid rounded" src="{{ '/assets/img/train-reconstruction/07_hole_after_side.png' | relative_url }}" alt="Side view after missing-region completion"><figcaption class="text-muted small mt-2">After completion — side view.</figcaption></figure></div>
</div>

<p class="text-muted small">Before and after missing-region completion. Large LiDAR holes around the train windows become recoverable after explicit missing-region detection and multi-directional interpolation.</p>

## Surface Reconstruction Comparison

After point-cloud completion, three classical reconstruction methods were evaluated: **Greedy Triangulation**, **Poisson Reconstruction**, and **Marching Cubes**. In the project evaluation, Greedy Triangulation produced the surface most consistent with the completed point cloud and better preserved the curved train-head geometry. It was therefore selected for the final reconstruction pipeline.

<div class="row row-cols-1 row-cols-md-3 g-4 my-4">
  <div class="col"><figure class="mb-0 border rounded p-2 h-100"><img class="img-fluid rounded" src="{{ '/assets/img/train-reconstruction/08_greedy_triangulation.png' | relative_url }}" alt="Greedy Triangulation reconstruction"><figcaption class="text-muted small mt-2">Greedy Triangulation.</figcaption></figure></div>
  <div class="col"><figure class="mb-0 border rounded p-2 h-100"><img class="img-fluid rounded" src="{{ '/assets/img/train-reconstruction/09_marching_cubes.png' | relative_url }}" alt="Marching Cubes reconstruction"><figcaption class="text-muted small mt-2">Marching Cubes.</figcaption></figure></div>
  <div class="col"><figure class="mb-0 border rounded p-2 h-100"><img class="img-fluid rounded" src="{{ '/assets/img/train-reconstruction/10_poisson.png' | relative_url }}" alt="Poisson Reconstruction result"><figcaption class="text-muted small mt-2">Poisson Reconstruction.</figcaption></figure></div>
</div>

<p class="text-muted small">Surface reconstruction comparison. Greedy Triangulation preserved the reconstructed train-head geometry more faithfully in the project experiments than Poisson Reconstruction and Marching Cubes.</p>
