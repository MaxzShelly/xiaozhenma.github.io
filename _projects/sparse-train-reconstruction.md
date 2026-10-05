---
layout: default
title: Sparse Point Cloud Reconstruction of High-Speed Train Head Geometry
paper_title: A Three-Dimensional Reverse-Projection Method for Sparse Point Cloud Completion and Its Application to High-Speed Train Nose Reconstruction
description: Three-axis reverse completion for missing glass-window regions in LiDAR scans.
importance: 1
category: Research
permalink: /projects/sparse-train-reconstruction/
---

<div class="post" id="train-reconstruction-project" markdown="1">

<header class="post-header" style="margin-bottom: 2.75rem">
  <h1 class="post-title" style="font-size: clamp(1.5rem, 2.4vw, 2rem); line-height: 1.4; margin: 0">{{ page.paper_title }}</h1>
</header>

<article style="line-height: 1.75" markdown="1">

<section aria-labelledby="train-abstract" markdown="1">
<h2 id="train-abstract" style="font-size: 1.5rem; margin-bottom: 1.25rem">Abstract</h2>

Holes in LiDAR scans of environments with glass windows remain an unresolved problem in three-dimensional reconstruction. This study presents a pipeline for point cloud acquisition, filtering, completion, and surface reconstruction to address sparse sampling and missing window regions in scans of a high-speed train nose. FAST-LIVO2 provides the initial point cloud through multisensor odometry and mapping, and moving least squares (MLS) smooths the observations. We then introduce three-axis projection-based subdivision and interpolation with reverse hole boundary identification, referred to as three-axis reverse completion. The method interpolates missing regions from observations around each hole. Greedy projection triangulation, Poisson surface reconstruction, and a Marching Cubes-based pipeline generate meshes from the completed point cloud. Experiments on a proportionally scaled display model of a high-speed train nose show that the proposed method fills missing point cloud regions around the glass windows. Under the evaluation setting used in this study, greedy projection triangulation yields lower geometric distance errors than the other two reconstruction pipelines. The pipeline supports non-contact digital modeling of train nose geometry and provides a practical approach to reconstructing objects with glass windows.

<p class="text-muted small" style="margin-top: 1.5rem"><strong>Keywords:</strong> high-speed train nose; point cloud completion; three-axis projection; hole boundary identification; moving least squares; greedy projection triangulation.</p>

</section>

<section aria-labelledby="train-overview" style="margin-top: 3.5rem" markdown="1">
<h2 id="train-overview" style="font-size: 1.5rem; margin-bottom: 1.25rem">Overview</h2>

Three-axis reverse completion identifies missing regions through complementary orthogonal projections. Unoccupied grid locations become candidate hole points, which are clustered and linked back to observed boundaries. Surface-layer separation and multidirectional inverse-distance interpolation constrain new points to the appropriate surface. The recovered points are then fused in 3D and passed to surface reconstruction.

<figure id="figure-1" style="margin: 1.75rem 0 0">
  <a href="{{ '/assets/img/train-reconstruction/manuscript/figure-1-pipeline.png' | relative_url }}" target="_blank" rel="noopener" aria-label="Open Figure 1 at full resolution">
    <img class="img-fluid rounded border d-block mx-auto" style="width: 100%; height: auto; background: white" src="{{ '/assets/img/train-reconstruction/manuscript/figure-1-pipeline.png' | relative_url }}" width="5064" height="2122" alt="Pipeline from multisensor acquisition through FAST-LIVO2, MLS, reverse completion and surface reconstruction; detail of projection, hole candidates, reverse boundary search, layer-aware interpolation and 3D fusion">
  </a>
  <figcaption class="text-muted small" style="margin-top: 0.85rem; line-height: 1.6"><strong>Figure 1.</strong> Acquisition, completion, and surface reconstruction pipeline. Select a figure to view it at full resolution.</figcaption>
</figure>

<h3 style="font-size: 1.25rem; margin-top: 2rem; margin-bottom: 1rem">Main Contributions</h3>

- **Reverse hole identification:** locate missing regions from unoccupied projection grids and retrieve surrounding boundary support.
- **Layer-aware completion:** interpolate from the same surface layer in multiple directions, then merge and deduplicate the completed points.
- **Experimental validation:** evaluate window completion on a scaled train-nose model and compare three surface-reconstruction pipelines.

</section>

<section aria-labelledby="train-results" style="margin-top: 3.5rem" markdown="1">
<h2 id="train-results" style="font-size: 1.5rem; margin-bottom: 1.75rem">Results</h2>

<section aria-labelledby="train-acquisition" markdown="1">
<h3 id="train-acquisition" style="font-size: 1.25rem; margin-bottom: 1rem">Capturing the Train Nose</h3>

Handheld multisensor scanning and FAST-LIVO2 mapping produce **9.71 million points** from a proportionally scaled train-nose display model. The main exterior is captured, while glass-window regions retain substantial gaps.

<figure id="figure-2" style="margin: 1.75rem 0 0">
  <a href="{{ '/assets/img/train-reconstruction/manuscript/figure-2-acquisition.png' | relative_url }}" target="_blank" rel="noopener" aria-label="Open Figure 2 at full resolution">
    <img class="img-fluid rounded border d-block mx-auto" style="width: 100%; height: auto; background: white" src="{{ '/assets/img/train-reconstruction/manuscript/figure-2-acquisition.png' | relative_url }}" width="3074" height="2098" loading="lazy" alt="Four panels showing front-left and front-right photographs of the display model alongside the corresponding scanned point cloud views">
  </a>
  <figcaption class="text-muted small" style="margin-top: 0.85rem; line-height: 1.6"><strong>Figure 2.</strong> The scaled train-nose display model and its scanned point cloud, shown from two sides.</figcaption>
</figure>

</section>

<section aria-labelledby="train-filtering" style="margin-top: 3.5rem" markdown="1">
<h3 id="train-filtering" style="font-size: 1.25rem; margin-bottom: 1rem">Preserving Geometry with Fewer Points</h3>

MLS smoothing reduces the point count by **88.47%**, retaining approximately 1.12 million points. It achieves lower Hausdorff and Chamfer distances than random downsampling in this experiment, preserving the observed geometry with a more uniform point distribution.

<figure id="figure-3" style="margin: 1.75rem 0 0">
  <a href="{{ '/assets/img/train-reconstruction/manuscript/figure-3-filtering.png' | relative_url }}" target="_blank" rel="noopener" aria-label="Open Figure 3 at full resolution">
    <img class="img-fluid rounded border d-block mx-auto" style="width: 100%; height: auto; background: white" src="{{ '/assets/img/train-reconstruction/manuscript/figure-3-filtering.png' | relative_url }}" width="3250" height="890" loading="lazy" alt="Side-by-side point cloud results of random downsampling and MLS smoothing">
  </a>
  <figcaption class="text-muted small" style="margin-top: 0.85rem; line-height: 1.6"><strong>Figure 3.</strong> Random downsampling (left) and MLS smoothing (right).</figcaption>
</figure>

</section>

<section aria-labelledby="train-completion" style="margin-top: 3.5rem" markdown="1">
<h3 id="train-completion" style="font-size: 1.25rem; margin-bottom: 1rem">Recovering Missing Window Regions</h3>

Three orthogonal projections expose complementary views of the missing regions. Reverse completion fills the main window gaps and yields approximately **7.68 million points**, with a reported **RMSE of 0.118 cm**, compared with 146.907 cm for nearest-neighbor interpolation under the study's evaluation setting.

<figure id="figure-4" style="margin: 1.75rem 0 0">
  <a href="{{ '/assets/img/train-reconstruction/manuscript/figure-4-projections.png' | relative_url }}" target="_blank" rel="noopener" aria-label="Open Figure 4 at full resolution">
    <img class="img-fluid rounded border d-block mx-auto" style="width: 100%; max-width: 40rem; height: auto; background: white" src="{{ '/assets/img/train-reconstruction/manuscript/figure-4-projections.png' | relative_url }}" width="1810" height="869" loading="lazy" alt="Three orthogonal projected point sets: green YZ plane at X equals zero, red XZ plane at Y equals zero, and blue XY plane at Z equals zero">
  </a>
  <figcaption class="text-muted small" style="margin-top: 0.85rem; line-height: 1.6"><strong>Figure 4.</strong> Orthogonal projections onto the YZ, XZ, and XY planes.</figcaption>
</figure>

<figure id="figure-5" style="margin: 1.75rem 0 0">
  <a href="{{ '/assets/img/train-reconstruction/manuscript/figure-5-completion.png' | relative_url }}" target="_blank" rel="noopener" aria-label="Open Figure 5 at full resolution">
    <img class="img-fluid rounded border d-block mx-auto" style="width: 100%; height: auto; background: white" src="{{ '/assets/img/train-reconstruction/manuscript/figure-5-completion.png' | relative_url }}" width="3250" height="1778" loading="lazy" alt="Top and side point cloud views before and after three-axis reverse completion, with orange boxes marking the window regions">
  </a>
  <figcaption class="text-muted small" style="margin-top: 0.85rem; line-height: 1.6"><strong>Figure 5.</strong> Top and side views before (left) and after (right) completion. Orange boxes highlight window regions.</figcaption>
</figure>

</section>

<section aria-labelledby="train-surfaces" style="margin-top: 3.5rem" markdown="1">
<h3 id="train-surfaces" style="font-size: 1.25rem; margin-bottom: 1rem">Reconstructing the Surface</h3>

Using the completed cloud, greedy projection triangulation follows the train-nose contour more closely than the Poisson and Marching Cubes pipelines in this comparison. It achieves the lowest geometric distance errors, including a **Hausdorff distance of 0.0086 cm** and an **RMSE of 0.0040 cm**.

<figure id="figure-6" style="margin: 1.75rem 0 0">
  <a href="{{ '/assets/img/train-reconstruction/manuscript/figure-6-surfaces.png' | relative_url }}" target="_blank" rel="noopener" aria-label="Open Figure 6 at full resolution">
    <img class="img-fluid rounded border d-block mx-auto" style="width: 100%; height: auto; background: white" src="{{ '/assets/img/train-reconstruction/manuscript/figure-6-surfaces.png' | relative_url }}" width="3250" height="2040" loading="lazy" alt="Display model compared with greedy projection triangulation, Marching Cubes-based reconstruction, and Poisson surface reconstruction">
  </a>
  <figcaption class="text-muted small" style="margin-top: 0.85rem; line-height: 1.6"><strong>Figure 6.</strong> Display model (a), greedy projection triangulation (b), Marching Cubes (c), and Poisson reconstruction (d).</figcaption>
</figure>

</section>


</section>

</article>

</div>
