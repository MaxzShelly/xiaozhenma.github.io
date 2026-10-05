---
layout: page
title: Sparse Point Cloud Reconstruction of High-Speed Train Head Geometry
description: Three-axis reverse completion for missing glass-window regions in sparse LiDAR scans.
importance: 1
category: Research
permalink: /projects/sparse-train-reconstruction/
---

This study develops a complete pipeline for reconstructing the geometry of a high-speed train nose from sparse and incomplete LiDAR observations. A portable sensing device combining LiDAR, cameras, and an inertial measurement unit (IMU) acquires the data, while FAST-LIVO2 performs multisensor odometry and mapping. Moving least squares (MLS) then smooths the observations before the proposed **three-axis reverse completion** method identifies and fills missing regions. Finally, three surface-reconstruction pipelines are compared on the completed point cloud.

The experiments use a proportionally scaled display model of a high-speed train nose. FAST-LIVO2 produces an initial point cloud containing **9,706,530 points**, but substantial local gaps remain around the glass windows.

<div class="row row-cols-1 row-cols-md-2 g-4 my-4">
  <div class="col"><figure class="mb-0 border rounded p-2 h-100"><div class="d-flex align-items-center" style="aspect-ratio: 1672 / 941"><img class="img-fluid rounded" style="width: 100%; height: 100%; object-fit: contain" src="{{ '/assets/img/train-reconstruction/01_train_head_photo.png' | relative_url }}" alt="High-speed train nose display model"></div><figcaption class="text-muted small mt-2">High-speed train nose display model.</figcaption></figure></div>
  <div class="col"><figure class="mb-0 border rounded p-2 h-100"><div class="d-flex align-items-center" style="aspect-ratio: 1672 / 941"><img class="img-fluid rounded" style="width: 100%; height: 100%; object-fit: contain" src="{{ '/assets/img/train-reconstruction/02_sparse_lidar_scan.png' | relative_url }}" alt="Sparse point cloud of the high-speed train nose"><figcaption class="text-muted small mt-2">FAST-LIVO2 point cloud; missing returns are concentrated around the glass-window regions.</figcaption></figure></div>
</div>

## Research Problem

A large total point count does not guarantee complete surface coverage. Glass produces few or no valid LiDAR returns, leaving extended holes even when the surrounding streamlined shell is densely sampled. These holes create two linked difficulties:

- The absence of observations makes the extent of a missing region difficult to determine directly.
- Points near a hole may belong to opposite sides or different surface layers, so unconstrained interpolation can mix unrelated geometry.

Rather than relying on a pretrained complete-shape model, this study uses the geometry surrounding each hole to locate missing regions and constrain the generation of new points.

## Reconstruction Pipeline

<div class="row align-items-center g-4 my-4">
  <div class="col-12 col-md-6">
    <p>The full pipeline comprises multisensor acquisition, FAST-LIVO2 mapping, MLS preprocessing, three-axis reverse completion, and surface reconstruction.</p>
    <p>The central method projects the point cloud along three orthogonal directions. Unoccupied grid locations inside valid projection domains become candidate hole points. Clustering identifies individual missing regions, and reverse boundary searches retrieve observed samples from the correct surface layer around each hole.</p>
    <p class="mb-0">The new points recovered from the three projection directions are transformed back into three-dimensional space, merged with the original cloud, and deduplicated to produce the completed point cloud.</p>
  </div>
  <div class="col-12 col-md-6 text-center">
    <img class="img-fluid rounded d-block mx-auto" src="{{ '/assets/img/train-reconstruction/reconstruction-pipeline.png' | relative_url }}" alt="Three-axis reverse point cloud completion pipeline">
  </div>
</div>

## Acquisition and MLS Preprocessing

FAST-LIVO2 combines LiDAR, camera, and IMU measurements through sequential LiDAR-inertial and visual-inertial updates. The resulting point cloud is processed using MLS, which fits a local quadratic surface with Gaussian distance weights and projects the samples onto the fitted surface along their normal directions.

Compared with random downsampling, MLS reduces the point count while preserving the spatial distribution and local geometry more closely under the evaluation used in the study.

<div class="table-responsive my-4">
  <table class="table table-sm table-bordered align-middle">
    <thead>
      <tr>
        <th>Method</th>
        <th>Output points</th>
        <th>Reduction</th>
        <th>Uniformity change</th>
        <th>Hausdorff distance</th>
        <th>Chamfer distance</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>MLS smoothing</td>
        <td>1,118,817</td>
        <td>88.47%</td>
        <td>5.454283</td>
        <td>1.7564 cm</td>
        <td>0.6927 cm</td>
      </tr>
      <tr>
        <td>Random downsampling</td>
        <td>970,653</td>
        <td>90.00%</td>
        <td>2.464060</td>
        <td>99.1275 cm</td>
        <td>0.7447 cm</td>
      </tr>
    </tbody>
  </table>
</div>

## Three-Axis Reverse Completion

### 1. Orthogonal projection and subdivision

The three-dimensional point cloud is projected onto the planes normal to the X, Y, and Z axes. A two-dimensional concave hull defines the valid domain of each projection, and coarse-to-fine spatial subdivision identifies unoccupied grid locations inside that domain as candidate hole points.

<figure class="my-4 border rounded p-2">
  <img class="img-fluid rounded w-50 d-block mx-auto" src="{{ '/assets/img/train-reconstruction/03_triaxial_projection.png' | relative_url }}" alt="Three orthogonal projections of the train point cloud">
  <figcaption class="text-muted small mt-2">Three orthogonal projection directions. Complementary views reduce dependence on a single viewing direction when locating missing regions.</figcaption>
</figure>

### 2. Surface-layer separation

Opposite surfaces may overlap after projection even though their perpendicular coordinates remain different. The method uses extrema of the perpendicular coordinate and a layer-thickness threshold to separate upper and lower surface layers. This prevents interpolation from combining observations that belong to different sides of the object.

### 3. Reverse hole-boundary identification

DBSCAN clusters the candidate hole points into distinct missing regions. A concave hull is constructed for each cluster, after which a reverse search in the original point cloud retrieves the surrounding observed boundary samples. This establishes a correspondence from an empty region back to the geometric observations that constrain it.

### 4. Multidirectional inverse-distance interpolation

Around each interpolation location, the projection plane is divided into six sectors of 60 degrees. The nearest valid point in each sector provides multidirectional support. Coordinates and RGB values are interpolated using inverse squared distance weights:

\[
w*i = \frac{1}{d_i^2}, \qquad
q = \frac{\sum*{i=1}^{m} w*i q_i}{\sum*{i=1}^{m} w_i}.
\]

Samples whose perpendicular coordinates do not satisfy \(\lvert q_i - \mu \rvert \leq 2\sigma\) are rejected as outliers. This combination of layer-aware selection, six-direction support, and outlier filtering reduces cross-layer mixing and one-sided neighborhood bias.

### 5. Three-dimensional fusion

The completed point sets recovered from the X, Y, and Z projection directions are combined, merged with the original point cloud, and deduplicated. Iterative refinement is applied to persistent holes.

## Point Cloud Completion Results

Three-axis reverse completion is compared with nearest-neighbor interpolation. The method fills the principal window gaps, although some regions near the rear of the display model remain incomplete because the available boundary support is insufficient.

<div class="row row-cols-1 row-cols-md-2 g-4 my-4">
  <div class="col"><figure class="mb-0 border rounded p-2 h-100"><img class="img-fluid rounded" src="{{ '/assets/img/train-reconstruction/04_hole_before_top.png' | relative_url }}" alt="Top view before point cloud completion"><figcaption class="text-muted small mt-2">Top view before completion.</figcaption></figure></div>
  <div class="col"><figure class="mb-0 border rounded p-2 h-100"><img class="img-fluid rounded" src="{{ '/assets/img/train-reconstruction/05_hole_after_top.png' | relative_url }}" alt="Top view after point cloud completion"><figcaption class="text-muted small mt-2">Top view after three-axis reverse completion.</figcaption></figure></div>
  <div class="col"><figure class="mb-0 border rounded p-2 h-100"><img class="img-fluid rounded" src="{{ '/assets/img/train-reconstruction/06_hole_before_side.png' | relative_url }}" alt="Side view before point cloud completion"><figcaption class="text-muted small mt-2">Side view before completion.</figcaption></figure></div>
  <div class="col"><figure class="mb-0 border rounded p-2 h-100"><img class="img-fluid rounded" src="{{ '/assets/img/train-reconstruction/07_hole_after_side.png' | relative_url }}" alt="Side view after point cloud completion"><figcaption class="text-muted small mt-2">Side view after three-axis reverse completion.</figcaption></figure></div>
</div>

<div class="table-responsive my-4">
  <table class="table table-sm table-bordered align-middle">
    <thead>
      <tr>
        <th>Method</th>
        <th>Point count</th>
        <th>Coefficient of determination (R²)</th>
        <th>RMSE</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>Three-axis reverse completion</td>
        <td>7,679,247</td>
        <td>1</td>
        <td>0.118 cm</td>
      </tr>
      <tr>
        <td>Nearest-neighbor interpolation</td>
        <td>7,994,022</td>
        <td>0.9879</td>
        <td>146.907 cm</td>
      </tr>
    </tbody>
  </table>
</div>

## Surface Reconstruction Comparison

Greedy projection triangulation, Poisson surface reconstruction, and a Marching Cubes-based pipeline are evaluated using the completed point cloud. Under the study's evaluation setting, greedy projection triangulation follows the input contour most closely and yields the lowest geometric distance errors.

<div class="row row-cols-1 row-cols-md-3 g-4 my-4">
  <div class="col"><figure class="mb-0 border rounded p-2 h-100"><img class="img-fluid rounded" src="{{ '/assets/img/train-reconstruction/08_greedy_triangulation.png' | relative_url }}" alt="Greedy projection triangulation result"><figcaption class="text-muted small mt-2">Greedy projection triangulation.</figcaption></figure></div>
  <div class="col"><figure class="mb-0 border rounded p-2 h-100"><img class="img-fluid rounded" src="{{ '/assets/img/train-reconstruction/09_marching_cubes.png' | relative_url }}" alt="Marching Cubes reconstruction result"><figcaption class="text-muted small mt-2">Marching Cubes-based reconstruction.</figcaption></figure></div>
  <div class="col"><figure class="mb-0 border rounded p-2 h-100"><img class="img-fluid rounded" src="{{ '/assets/img/train-reconstruction/10_poisson.png' | relative_url }}" alt="Poisson surface reconstruction result"><figcaption class="text-muted small mt-2">Poisson surface reconstruction.</figcaption></figure></div>
</div>

<div class="table-responsive my-4">
  <table class="table table-sm table-bordered align-middle">
    <thead>
      <tr>
        <th>Method</th>
        <th>Hausdorff distance</th>
        <th>Mean deviation</th>
        <th>Standard deviation</th>
        <th>RMSE</th>
        <th>Surface smoothness</th>
        <th>Face count</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>Greedy projection triangulation</td>
        <td>0.0086 cm</td>
        <td>0.0036 cm</td>
        <td>0.0016 cm</td>
        <td>0.0040 cm</td>
        <td>0.876081</td>
        <td>12,182,654</td>
      </tr>
      <tr>
        <td>Poisson surface reconstruction</td>
        <td>53.0692 cm</td>
        <td>2.2900 cm</td>
        <td>1.4693 cm</td>
        <td>2.7209 cm</td>
        <td>0.873940</td>
        <td>111,600</td>
      </tr>
      <tr>
        <td>Marching Cubes-based reconstruction</td>
        <td>481.0731 cm</td>
        <td>6.3177 cm</td>
        <td>3.1728 cm</td>
        <td>7.0697 cm</td>
        <td>0.000000</td>
        <td>50,597</td>
      </tr>
    </tbody>
  </table>
</div>

## Conclusions and Limitations

The study demonstrates that combining FAST-LIVO2 mapping, MLS preprocessing, three-axis reverse completion, and geometric surface reconstruction can recover major missing glass-window regions in a sparse train-nose point cloud. MLS reduces the point count by 88.47% while preserving geometry more closely than random downsampling. Three-axis reverse completion achieves an RMSE of 0.118 cm in the reported comparison, and greedy projection triangulation provides the lowest geometric distance errors among the three evaluated surface-reconstruction pipelines.

The current validation is limited to a proportionally scaled display model. The method also depends on valid observations around each hole; when the surrounding boundary is insufficient, some regions cannot be fully completed. Further evaluation is therefore required under the wider range of acquisition conditions found in industrial environments.

<p class="text-muted small mt-4"><strong>Manuscript:</strong> <em>A Three-Dimensional Reverse-Projection Method for Sparse Point Cloud Completion and Its Application to High-Speed Train Nose Reconstruction</em>. Zhao Tang, Xiaozhen Ma, Hanbin Lai, Ruiqi Chen, and Jin Jin.</p>
