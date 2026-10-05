---
layout: page
title: A Three-Dimensional Reverse-Projection Method for Sparse Point Cloud Completion and Its Application to High-Speed Train Nose Reconstruction
description: Three-axis reverse completion for missing glass-window regions in LiDAR scans.
importance: 1
category: Research
permalink: /projects/sparse-train-reconstruction/
---

Zhao Tang, Xiaozhen Ma, Hanbin Lai, Ruiqi Chen, Jin Jin

## Abstract

Holes in LiDAR scans of environments with glass windows remain an unresolved problem in three-dimensional reconstruction. This study presents a pipeline for point cloud acquisition, filtering, completion, and surface reconstruction to address sparse sampling and missing window regions in scans of a high-speed train nose. FAST-LIVO2 provides the initial point cloud through multisensor odometry and mapping, and moving least squares (MLS) smooths the observations. We then introduce three-axis projection-based subdivision and interpolation with reverse hole boundary identification, referred to as three-axis reverse completion. The method interpolates missing regions from observations around each hole. Greedy projection triangulation, Poisson surface reconstruction, and a Marching Cubes-based pipeline generate meshes from the completed point cloud. Experiments on a proportionally scaled display model of a high-speed train nose show that the proposed method fills missing point cloud regions around the glass windows. Under the evaluation setting used in this study, greedy projection triangulation yields lower geometric distance errors than the other two reconstruction pipelines. The pipeline supports non-contact digital modeling of train nose geometry and provides a practical approach to reconstructing objects with glass windows.

**Keywords:** high-speed train nose; point cloud completion; three-axis projection; hole boundary identification; moving least squares; greedy projection triangulation.

## Three-Axis Reverse Completion

We propose three-axis projection-based subdivision and interpolation with reverse hole boundary identification, hereafter referred to as three-axis reverse completion. Projections along three orthogonal directions reduce the dependence of hole identification on a single viewing direction. Unoccupied locations in each projection domain become candidate hole points, allowing regions without observations to participate in clustering. The method then separates overlapping surface layers, retrieves observations from the same layer in multiple directions around each hole, and applies inverse distance weighting to reduce cross-layer mixing and one-sided neighborhood support. Combined with FAST-LIVO2 acquisition, MLS preprocessing, and surface reconstruction, the method forms the train nose reconstruction pipeline shown in Figure 1.

<figure id="figure-1" class="my-4">
  <a href="{{ '/assets/img/train-reconstruction/manuscript/figure-1-pipeline.png' | relative_url }}" target="_blank" rel="noopener" aria-label="Open Figure 1 at full resolution">
    <img class="img-fluid rounded border d-block mx-auto" style="width: 100%; height: auto; background: white" src="{{ '/assets/img/train-reconstruction/manuscript/figure-1-pipeline.png' | relative_url }}" width="5064" height="2122" alt="Pipeline from multisensor acquisition through FAST-LIVO2, MLS, reverse completion and surface reconstruction; detail of projection, hole candidates, reverse boundary search, layer-aware interpolation and 3D fusion">
  </a>
  <figcaption class="text-muted small mt-2"><strong>Figure 1.</strong> Overall pipeline for three-axis reverse completion and train nose reconstruction. Select any figure to view it at full resolution.</figcaption>
</figure>

### Main Contributions

The main contributions of this study are as follows:

1. We propose three-axis reverse completion. The method converts unoccupied grid locations within valid projection domains into candidate hole points, identifies missing regions through clustering, and establishes their correspondence with surrounding observed boundaries to support the completion of regional holes.
2. We develop a multidirectional interpolation strategy using observations from the same surface layer. To address overlapping projections and uneven sampling along hole boundaries, the strategy combines surface layer separation with multidirectional boundary searches to constrain new points to the appropriate layer. The completed points from each projection direction are then recovered in three-dimensional space.
3. We validate the method on a point cloud of a proportionally scaled train nose display model acquired by our research team. We integrate the method into a multisensor point cloud reconstruction pipeline, compare it with nearest-neighbor interpolation, and compare the results of greedy projection triangulation, Poisson surface reconstruction, and Marching Cubes to examine window completion and differences in surface reconstruction.

The completion procedure uses concave projection domains and coarse-to-fine subdivision to identify candidate holes. DBSCAN groups these candidates, and a concave hull for each cluster guides the search for observed boundary support. The projection plane is divided into six 60-degree sectors around each interpolation location. Support from the same surface layer is filtered for outliers and weighted by inverse squared distance to interpolate the perpendicular coordinate and RGB values. The recovered three-dimensional point sets are merged with the original cloud and deduplicated; iterative refinement addresses persistent holes.

## Experimental Results and Analysis

### Point Cloud Acquisition Results

The experiments use a proportionally scaled display model of a high-speed train nose. Its streamlined geometry includes cab windows, flow-guiding grooves, and lower skirt structures. The research team acquires the data through handheld mobile scanning with the custom multisensor device.

FAST-LIVO2 registers the acquired multisensor data to produce an initial point cloud of 9,706,530 points. The cloud covers the main exterior of the display model, while local gaps remain around the windows, as shown in Figure 2.

<figure id="figure-2" class="my-4">
  <a href="{{ '/assets/img/train-reconstruction/manuscript/figure-2-acquisition.png' | relative_url }}" target="_blank" rel="noopener" aria-label="Open Figure 2 at full resolution">
    <img class="img-fluid rounded border d-block mx-auto" style="width: 100%; height: auto; background: white" src="{{ '/assets/img/train-reconstruction/manuscript/figure-2-acquisition.png' | relative_url }}" width="3074" height="2098" loading="lazy" alt="Four panels showing front-left and front-right photographs of the display model alongside the corresponding scanned point cloud views">
  </a>
  <figcaption class="text-muted small mt-2"><strong>Figure 2.</strong> The proportionally scaled high-speed train nose display model and its scanned point cloud. Panels (a) and (c) show photographs from different viewing directions; panels (b) and (d) show the corresponding side views of the point cloud.</figcaption>
</figure>

### Comparison of Filtering Results

We compare random downsampling with MLS smoothing, as shown in Figure 3. MLS combines local surface fitting with smooth sampling. Table 1 reports the results for the acquired display model point cloud.

<figure id="figure-3" class="my-4">
  <a href="{{ '/assets/img/train-reconstruction/manuscript/figure-3-filtering.png' | relative_url }}" target="_blank" rel="noopener" aria-label="Open Figure 3 at full resolution">
    <img class="img-fluid rounded border d-block mx-auto" style="width: 100%; height: auto; background: white" src="{{ '/assets/img/train-reconstruction/manuscript/figure-3-filtering.png' | relative_url }}" width="3250" height="890" loading="lazy" alt="Side-by-side point cloud results of random downsampling and MLS smoothing">
  </a>
  <figcaption class="text-muted small mt-2"><strong>Figure 3.</strong> Results of random downsampling and MLS smoothing. Each panel shows the processed point cloud using the original display colors. Table 1 provides the quantitative comparison.</figcaption>
</figure>

<div class="table-responsive my-4" role="region" aria-label="Filtering results table; scroll horizontally if needed" tabindex="0">
  <table id="table-1" class="table table-sm" style="min-width: 34rem; font-variant-numeric: tabular-nums; color: inherit">
    <caption style="caption-side: top; color: inherit"><strong>Table 1.</strong> Comparison of filtering results.</caption>
    <thead>
      <tr><th scope="col">Metric</th><th scope="col" class="text-right">MLS smoothing</th><th scope="col" class="text-right">Random downsampling</th></tr>
    </thead>
    <tbody>
      <tr><th scope="row">Input points</th><td class="text-right">9,706,530</td><td class="text-right">9,706,530</td></tr>
      <tr><th scope="row">Output points</th><td class="text-right">1,118,817</td><td class="text-right">970,653</td></tr>
      <tr><th scope="row">Point count reduction (%)</th><td class="text-right">88.473564</td><td class="text-right">90.000000</td></tr>
      <tr><th scope="row">Density change (%)</th><td class="text-right">88.470909</td><td class="text-right">89.575424</td></tr>
      <tr><th scope="row">Uniformity change</th><td class="text-right">5.454283</td><td class="text-right">2.464060</td></tr>
      <tr><th scope="row">Hausdorff distance (cm)</th><td class="text-right">1.7564</td><td class="text-right">99.1275</td></tr>
      <tr><th scope="row">Chamfer distance (cm)</th><td class="text-right">0.6927</td><td class="text-right">0.7447</td></tr>
    </tbody>
  </table>
</div>

Table 1 shows that MLS reduces the point count from 9,706,530 to 1,118,817, a reduction of 88.47%. The density change is also 88.47%, consistent with the change in point count. The uniformity change metric is 5.454 for MLS and 2.464 for random downsampling, indicating a larger improvement in point distribution uniformity for MLS in this experiment.

MLS yields a Hausdorff distance of 1.7564 cm and a Chamfer distance of 0.6927 cm, both lower than those of random downsampling. The difference is particularly large for the Hausdorff distance, which is 99.1275 cm for random downsampling. These results indicate that MLS reduces the number of points while preserving the spatial distribution and geometry more closely under the evaluation used here.

### Analysis of Sparse Point Cloud Densification by Interpolation

We compare three-axis reverse completion with nearest-neighbor interpolation. Figure 4 shows the three orthogonal projection directions, and Figure 5 presents top and side views before and after completion. The proposed method fills missing points around the windows. Some gaps remain near the rear of the display model because boundary support is insufficient.

<figure id="figure-4" class="my-4">
  <a href="{{ '/assets/img/train-reconstruction/manuscript/figure-4-projections.png' | relative_url }}" target="_blank" rel="noopener" aria-label="Open Figure 4 at full resolution">
    <img class="img-fluid rounded border d-block mx-auto" style="width: 100%; max-width: 40rem; height: auto; background: white" src="{{ '/assets/img/train-reconstruction/manuscript/figure-4-projections.png' | relative_url }}" width="1810" height="869" loading="lazy" alt="Three orthogonal projected point sets: green YZ plane at X equals zero, red XZ plane at Y equals zero, and blue XY plane at Z equals zero">
  </a>
  <figcaption class="text-muted small mt-2"><strong>Figure 4.</strong> Spatial arrangement of the three orthogonal projected point sets. Green, red, and blue indicate the YZ (X = 0), XZ (Y = 0), and XY (Z = 0) projection planes, respectively.</figcaption>
</figure>

<figure id="figure-5" class="my-4">
  <a href="{{ '/assets/img/train-reconstruction/manuscript/figure-5-completion.png' | relative_url }}" target="_blank" rel="noopener" aria-label="Open Figure 5 at full resolution">
    <img class="img-fluid rounded border d-block mx-auto" style="width: 100%; height: auto; background: white" src="{{ '/assets/img/train-reconstruction/manuscript/figure-5-completion.png' | relative_url }}" width="3250" height="1778" loading="lazy" alt="Top and side point cloud views before and after three-axis reverse completion, with orange boxes marking the window regions">
  </a>
  <figcaption class="text-muted small mt-2"><strong>Figure 5.</strong> Point clouds before and after three-axis reverse completion. Panels (a) and (b) show top views, and panels (c) and (d) show side views. The left and right columns show the results before and after completion, respectively. Orange boxes mark the window regions used for comparison.</figcaption>
</figure>

<div class="table-responsive my-4" role="region" aria-label="Completion results table; scroll horizontally if needed" tabindex="0">
  <table id="table-2" class="table table-sm" style="min-width: 36rem; font-variant-numeric: tabular-nums; color: inherit">
    <caption style="caption-side: top; color: inherit"><strong>Table 2.</strong> Comparison of point cloud completion results. Three-axis reverse completion denotes the complete procedure described above.</caption>
    <thead>
      <tr><th scope="col">Method</th><th scope="col" class="text-right">Point count</th><th scope="col" class="text-right">Coefficient of determination R<sup>2</sup></th><th scope="col" class="text-right">RMSE (cm)</th></tr>
    </thead>
    <tbody>
      <tr><th scope="row">Three-axis reverse completion</th><td class="text-right">7,679,247</td><td class="text-right">1</td><td class="text-right">0.118</td></tr>
      <tr><th scope="row">Nearest-neighbor interpolation</th><td class="text-right">7,994,022</td><td class="text-right">0.9879</td><td class="text-right">146.907</td></tr>
    </tbody>
  </table>
</div>

Table 2 compares the completion results. Three-axis reverse completion increases the point count to 7,679,247, with a coefficient of determination R² of 1 and a root mean square error (RMSE) of approximately 0.118 cm. Nearest-neighbor interpolation produces 7,994,022 points, with R² = 0.9879 and RMSE = 146.907 cm.

### Comparison of Surface Reconstruction Results

Greedy projection triangulation, Poisson surface reconstruction, and the MC-based pipeline use the completed point cloud as input. Figure 6 shows their outputs. In this experiment, greedy projection triangulation follows the input point cloud contour more closely, whereas the other two pipelines show deviations in the overall reconstructed shape.

<figure id="figure-6" class="my-4">
  <a href="{{ '/assets/img/train-reconstruction/manuscript/figure-6-surfaces.png' | relative_url }}" target="_blank" rel="noopener" aria-label="Open Figure 6 at full resolution">
    <img class="img-fluid rounded border d-block mx-auto" style="width: 100%; height: auto; background: white" src="{{ '/assets/img/train-reconstruction/manuscript/figure-6-surfaces.png' | relative_url }}" width="3250" height="2040" loading="lazy" alt="Display model compared with greedy projection triangulation, Marching Cubes-based reconstruction, and Poisson surface reconstruction">
  </a>
  <figcaption class="text-muted small mt-2"><strong>Figure 6.</strong> Outputs of the three surface reconstruction pipelines. Panel (a) shows the display model; panels (b), (c), and (d) show greedy projection triangulation, the MC-based pipeline, and Poisson surface reconstruction, respectively.</figcaption>
</figure>

<div class="table-responsive my-4" role="region" aria-label="Surface reconstruction results table; scroll horizontally if needed" tabindex="0">
  <table id="table-3" class="table table-sm" style="min-width: 40rem; font-variant-numeric: tabular-nums; color: inherit">
    <caption style="caption-side: top; color: inherit"><strong>Table 3.</strong> Comparison of surface reconstruction results.</caption>
    <thead>
      <tr><th scope="col">Metric</th><th scope="col" class="text-right">Greedy projection triangulation</th><th scope="col" class="text-right">Poisson surface reconstruction</th><th scope="col" class="text-right">MC-based reconstruction</th></tr>
    </thead>
    <tbody>
      <tr><th scope="row">Hausdorff distance (cm)</th><td class="text-right">0.0086</td><td class="text-right">53.0692</td><td class="text-right">481.0731</td></tr>
      <tr><th scope="row">Maximum deviation distance (cm)</th><td class="text-right">0.0086</td><td class="text-right">54.1552</td><td class="text-right">46.2680</td></tr>
      <tr><th scope="row">Mean deviation distance (cm)</th><td class="text-right">0.0036</td><td class="text-right">2.2900</td><td class="text-right">6.3177</td></tr>
      <tr><th scope="row">Standard deviation (cm)</th><td class="text-right">0.0016</td><td class="text-right">1.4693</td><td class="text-right">3.1728</td></tr>
      <tr><th scope="row">RMSE (cm)</th><td class="text-right">0.0040</td><td class="text-right">2.7209</td><td class="text-right">7.0697</td></tr>
      <tr><th scope="row">Surface smoothness</th><td class="text-right">0.876081</td><td class="text-right">0.873940</td><td class="text-right">0.000000</td></tr>
      <tr><th scope="row">Face count</th><td class="text-right">12,182,654</td><td class="text-right">111,600</td><td class="text-right">50,597</td></tr>
    </tbody>
  </table>
</div>

Table 3 summarizes the evaluation of the three reconstruction pipelines.

Greedy projection triangulation yields a Hausdorff distance of 0.0086 cm, compared with 53.0692 cm for Poisson reconstruction and 481.0731 cm for the MC-based pipeline. The maximum deviation distances are 0.0086 cm, 54.1552 cm, and 46.2680 cm, respectively. Greedy projection triangulation also has the lowest mean deviation, standard deviation, and RMSE, at 0.0036 cm, 0.0016 cm, and 0.0040 cm. It therefore produces the lowest geometric distance errors among the three pipelines under the evaluation setting used in this study.

The surface smoothness metrics of greedy projection triangulation and Poisson reconstruction are similar, at 0.876081 and 0.873940, respectively. The MC-based pipeline has a value of 0 for this metric. Greedy projection triangulation generates 12,182,654 faces, more than either alternative, providing a finer subdivision of local surfaces.

Considering geometric distance errors, surface smoothness, and contour preservation in this experiment, we use greedy projection triangulation to reconstruct the surface from the completed point cloud.

## Conclusion

By linking sparse point cloud completion with surface reconstruction, this study establishes a pipeline for non-contact digital modeling of a train nose display model. Three-axis reverse completion uses the geometry around holes to identify and fill missing regions, improving data completeness near the glass windows and providing more continuous point cloud input for subsequent surface reconstruction. This workflow offers a practical basis for representing and analyzing train nose geometry.

This study primarily validates the pipeline on a proportionally scaled display model and does not yet cover the range of acquisition conditions found in complex industrial environments. Three-axis reverse completion depends on valid boundary information around each hole. Insufficient boundary support leaves some regions near the rear of the model incomplete.
