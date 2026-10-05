---
layout: default
title: Pixel-Level 3D Reconstruction and Physical Object Extraction from Sparse Point Clouds in Transportation Scenes
paper_title: Pixel-Level 3D Reconstruction and Physical Object Extraction from Sparse Point Clouds in Transportation Scenes
description: Combining learned depth, LiDAR anchors, and semantic boundary constraints.
importance: 2
category: Research
permalink: /projects/monocular-depth-railway/
---

<div class="post" id="railway-reconstruction-project" lang="en" style="font-family: Roboto, sans-serif; font-size: 1rem; font-weight: 300">

<header class="post-header" style="margin-bottom: 2.75rem">
  <h1 class="post-title" style="font-size: clamp(1.5rem, 2.4vw, 2rem); line-height: 1.4; margin: 0">{{ page.paper_title }}</h1>
  <div class="project-metadata" style="margin-top: 1.5rem; font-size: 1rem; font-weight: 300; line-height: 1.75">
    <p style="margin: 0">Xiaozhen Ma · University of California, Irvine</p>
    <p class="text-muted small" style="margin: 0.25rem 0 0">UCInspire 2026 · July–September 2026</p>
    <p class="text-muted small" style="margin: 0.25rem 0 0">Faculty Mentor: Prof. Fadi Kurdahi</p>
  </div>
</header>

<article style="line-height: 1.75">

<section aria-labelledby="railway-abstract">
<h2 id="railway-abstract" style="font-size: 1.5rem; margin-bottom: 1.25rem">Abstract</h2>

<p>Sparse LiDAR sampling, local errors in monocular depth, and ambiguous object associations in occluded regions complicate the reconstruction of transportation scenes. This study presents a method for pixel-level 3D reconstruction and physical object extraction that combines multi-frame frustum aggregation, object boundaries, and depth correction. Poses and point clouds from FAST-LIVO2 define a common metric coordinate system. Co-visible measurements from an offline sequence are projected into each keyframe to provide geometric support for local reconstruction.</p>

<p>SAM 3 masks define the regions for depth correction. Within each object, a piecewise moving least squares (MLS) model fits the residuals between LiDAR measurements and monocular depth predictions. Back-projecting valid pixels with the corrected depth produces a colored 3D point cloud constrained by measured geometry and object boundaries.</p>

<p>Depth-consistency screening and class-aware radius filtering organize observations across frames, while frame-based visualization supports scene browsing and asset extraction. Results from urban mapping and railway bridge reconstruction show the transition from sparse observations to locally continuous surface representations and demonstrate the extraction of track regions and crossbeams.</p>

</section>

<section aria-labelledby="railway-overview" style="margin-top: 3.5rem">
<h2 id="railway-overview" style="font-size: 1.5rem; margin-bottom: 1.25rem">Overview</h2>

<p>The method uses LiDAR measurements to constrain image-based depth estimates in a common metric coordinate system while restricting correction to individual objects. Keyframe frusta select co-visible observations from multiple frames. Object masks define the regions for local residual fitting, and LiDAR anchors guide depth correction within these regions. Consistency screening, distance-dependent class-aware filtering, and frame-based organization connect reconstruction with scene browsing and asset extraction.</p>

<p>The pipeline operates offline on scenes dominated by static transportation infrastructure. Co-visible observations can precede or follow the keyframe. Measured geometry, depth priors, and object boundaries jointly guide the conversion of sparse observations into pixel-level 3D samples within valid object regions.</p>

<figure id="railway-figure-1" style="margin: 1.75rem 0 0">
  <div class="rounded" style="position: relative; aspect-ratio: 1442 / 262; overflow: hidden; background: white">
    <img class="d-block" style="width: 100%; height: auto" src="{{ '/assets/img/railway-reconstruction/results/pipeline.png' | relative_url }}" width="1442" height="642" loading="lazy" alt="Pipeline overview: FAST-LIVO2 mapping, multi-frame aggregation, object-constrained reconstruction, and pixel-level 3D output">
  </div>
  <figcaption class="text-muted small" style="margin-top: 0.85rem; line-height: 1.6"><strong>Figure 1.</strong> Overview of the reconstruction pipeline, from FAST-LIVO2 mapping and multi-frame aggregation to object-constrained reconstruction and pixel-level 3D output.</figcaption>
</figure>

<h3 style="font-size: 1.25rem; margin-top: 2rem; margin-bottom: 1rem">Main Contributions</h3>

<ul>
  <li>The method establishes geometric correspondences between co-visible point clouds and keyframe pixels to support object-level depth correction.</li>
  <li>It combines object boundaries with piecewise MLS residual fitting to generate pixel-level 3D samples from sparse metric anchors and monocular depth.</li>
  <li>Distance-dependent class-aware filtering and frame-based organization support object association across frames, scene visualization, and transportation asset extraction.</li>
</ul>

</section>

<section aria-labelledby="railway-results" style="margin-top: 3.5rem">
<h2 id="railway-results" style="font-size: 1.5rem; margin-bottom: 1.75rem">Results</h2>

<section aria-labelledby="railway-mapping">
<h3 id="railway-mapping" style="font-size: 1.25rem; margin-bottom: 1rem">Scene Mapping and Multi-Frame Aggregation</h3>

<p>The base point clouds capture building facades, roadside structures, bridge columns, crossbeams, and track alignment. Multi-frame frustum aggregation combines observations of the bridge, while object-boundary filtering selects the relevant points. These measurements provide geometric support for depth correction and surface reconstruction within the bridge region.</p>

<figure id="railway-figure-2" style="margin: 1.75rem 0 0">
  <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(min(100%, 20rem), 1fr)); gap: 1.5rem; align-items: start">
<div style="min-width: 0">
    <div class="d-block rounded" style="position: relative; aspect-ratio: 16 / 10; overflow: hidden; border: 1px solid var(--global-divider-color, #e0e0e0); background: #191919; isolation: isolate">
      <img class="d-block" style="position: absolute; max-width: none; width: 115.39352%; height: auto; left: -10.41667%; top: -4.81481%" src="{{ '/assets/img/railway-reconstruction/results/urban-map.png' | relative_url }}" width="997" height="568" loading="lazy" alt="Urban point cloud from FAST-LIVO2 mapping">
    </div>
    <p class="text-muted small" style="margin: 0.65rem 0 0; line-height: 1.6">(a) Urban scene</p>
  </div>
<div style="min-width: 0">
    <div class="d-block rounded" style="position: relative; aspect-ratio: 16 / 10; overflow: hidden; border: 1px solid var(--global-divider-color, #e0e0e0); background: #191919; isolation: isolate">
      <img class="d-block" style="position: absolute; max-width: none; width: 115.39352%; height: auto; left: -7.52315%; top: -1.48148%" src="{{ '/assets/img/railway-reconstruction/results/railway-map.png' | relative_url }}" width="997" height="558" loading="lazy" alt="Railway bridge point cloud from FAST-LIVO2 mapping">
    </div>
    <p class="text-muted small" style="margin: 0.65rem 0 0; line-height: 1.6">(b) Railway bridge</p>
  </div>
  </div>
  <figcaption class="text-muted small" style="margin-top: 0.85rem; line-height: 1.6"><strong>Figure 2.</strong> Urban and railway bridge point clouds from FAST-LIVO2 mapping.</figcaption>
</figure>

<figure id="railway-figure-3" style="margin: 1.75rem 0 0">
  <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(min(100%, 20rem), 1fr)); gap: 1.5rem; align-items: start">
<div style="min-width: 0">
    <div class="d-block rounded" style="position: relative; aspect-ratio: 16 / 10; overflow: hidden; border: 1px solid var(--global-divider-color, #e0e0e0); background: #191919; isolation: isolate">
      <img class="d-block" style="position: absolute; max-width: none; width: 122.5%; height: auto; left: -6.25%; top: -3.33333%" src="{{ '/assets/img/railway-reconstruction/results/single-frame.png' | relative_url }}" width="588" height="320" loading="lazy" alt="Sparse railway bridge point cloud from a single frame">
    </div>
    <p class="text-muted small" style="margin: 0.65rem 0 0; line-height: 1.6">(a) Single-frame sparse observations</p>
  </div>
<div style="min-width: 0">
    <div class="d-block rounded" style="position: relative; aspect-ratio: 16 / 10; overflow: hidden; border: 1px solid var(--global-divider-color, #e0e0e0); background: #191919; isolation: isolate">
      <img class="d-block" style="position: absolute; max-width: none; width: 103.01724%; height: auto; left: -0.64655%; top: -3.10345%" src="{{ '/assets/img/railway-reconstruction/results/object-candidates.png' | relative_url }}" width="478" height="309" loading="lazy" alt="Bridge points selected by multi-frame aggregation, keyframe frustum projection, and object masks">
    </div>
    <p class="text-muted small" style="margin: 0.65rem 0 0; line-height: 1.6">(b) Object-constrained multi-frame points</p>
  </div>
  </div>
  <figcaption class="text-muted small" style="margin-top: 0.85rem; line-height: 1.6"><strong>Figure 3.</strong> Single-frame sparse observations and the bridge point cloud after multi-frame aggregation and object-boundary filtering.</figcaption>
</figure>

</section>

<section aria-labelledby="railway-fusion" style="margin-top: 3.5rem">
<h3 id="railway-fusion" style="font-size: 1.25rem; margin-bottom: 1rem">Object-Constrained Depth Fusion and Reconstruction</h3>

<p>Combining monocular depth, LiDAR measurements, and SAM 3 object boundaries yields locally continuous representations of bridge columns and crossbeams. The reconstructed cloud also shows the spatial relationship between the track and the bridge structure. Piecewise residual correction and pixel back-projection convert sparse measurements and image information into colored 3D surface samples.</p>

<figure id="railway-figure-4" style="margin: 1.75rem 0 0">
  <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(min(100%, 20rem), 1fr)); gap: 1.5rem; align-items: start">
<div style="min-width: 0">
    <div class="d-block rounded" style="position: relative; aspect-ratio: 16 / 10; overflow: hidden; border: 1px solid var(--global-divider-color, #e0e0e0); background: #191919; isolation: isolate">
      <img class="d-block" style="position: absolute; max-width: none; width: 150.70755%; height: auto; left: -25.23585%; top: -0.37736%" src="{{ '/assets/img/railway-reconstruction/results/rgb.png' | relative_url }}" width="1278" height="537" loading="lazy" alt="RGB image of the railway bridge">
    </div>
    <p class="text-muted small" style="margin: 0.65rem 0 0; line-height: 1.6">(a) RGB image</p>
  </div>
<div style="min-width: 0">
    <div class="d-block rounded" style="position: relative; aspect-ratio: 16 / 10; overflow: hidden; border: 1px solid var(--global-divider-color, #e0e0e0); background: #191919; isolation: isolate">
      <img class="d-block" style="position: absolute; max-width: none; width: 150.70755%; height: auto; left: -25.23585%; top: -0.37736%" src="{{ '/assets/img/railway-reconstruction/results/monocular-depth.png' | relative_url }}" width="1278" height="533" loading="lazy" alt="Monocular depth visualization of the railway bridge">
    </div>
    <p class="text-muted small" style="margin: 0.65rem 0 0; line-height: 1.6">(b) Monocular depth</p>
  </div>
<div style="min-width: 0">
    <div class="d-block rounded" style="position: relative; aspect-ratio: 16 / 10; overflow: hidden; border: 1px solid var(--global-divider-color, #e0e0e0); background: #191919; isolation: isolate">
      <img class="d-block" style="position: absolute; max-width: none; width: 147.47596%; height: auto; left: -23.79808%; top: -2.69231%" src="{{ '/assets/img/railway-reconstruction/results/object-mask.png' | relative_url }}" width="1227" height="538" loading="lazy" alt="Bridge segmentation mask overlaid on the RGB image">
    </div>
    <p class="text-muted small" style="margin: 0.65rem 0 0; line-height: 1.6">(c) Object segmentation</p>
  </div>
<div style="min-width: 0">
    <div class="d-block rounded" style="position: relative; aspect-ratio: 16 / 10; overflow: hidden; border: 1px solid var(--global-divider-color, #e0e0e0); background: #191919; isolation: isolate">
      <img class="d-block" style="position: absolute; max-width: none; width: 148.64865%; height: auto; left: -22.80405%; top: -6.21622%" src="{{ '/assets/img/railway-reconstruction/results/fused-cloud.png' | relative_url }}" width="880" height="403" loading="lazy" alt="Point cloud from the fusion of monocular depth and LiDAR measurements">
    </div>
    <p class="text-muted small" style="margin: 0.65rem 0 0; line-height: 1.6">(d) Depth and LiDAR fusion</p>
  </div>
  </div>
  <figcaption class="text-muted small" style="margin-top: 0.85rem; line-height: 1.6"><strong>Figure 4.</strong> RGB input, monocular depth, object segmentation, and the fused 3D point cloud.</figcaption>
</figure>

<figure id="railway-figure-5" style="max-width: 40rem; margin: 1.75rem auto 0">
<div style="min-width: 0">
    <div class="d-block rounded" style="position: relative; aspect-ratio: 16 / 10; overflow: hidden; border: 1px solid var(--global-divider-color, #e0e0e0); background: #191919; isolation: isolate">
      <img class="d-block" style="position: absolute; max-width: none; width: 166.12903%; height: auto; left: -18.14516%; top: -16.12903%" src="{{ '/assets/img/railway-reconstruction/results/boundary-reconstruction.png' | relative_url }}" width="824" height="364" loading="lazy" alt="Reconstructed bridge columns, crossbeams, track, and nearby vegetation">
    </div>
  </div>
  <figcaption class="text-muted small" style="margin-top: 0.85rem; line-height: 1.6"><strong>Figure 5.</strong> Object-constrained reconstruction of bridge columns, crossbeams, and the track region.</figcaption>
</figure>

</section>

<section aria-labelledby="railway-views" style="margin-top: 3.5rem">
<h3 id="railway-views" style="font-size: 1.25rem; margin-bottom: 1rem">Multi-View Scene Visualization</h3>

<p>Views from above and from the side reveal the bridge geometry and its surrounding environment. The elevated front view shows the track extending through the bridge and the arrangement of crossbeams. The side view reveals the spatial relationships among columns, crossbeams, and the ground.</p>

<figure id="railway-figure-6" style="margin: 1.75rem 0 0">
  <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(min(100%, 20rem), 1fr)); gap: 1.5rem; align-items: start">
<div style="min-width: 0">
    <div class="d-block rounded" style="position: relative; aspect-ratio: 16 / 10; overflow: hidden; border: 1px solid var(--global-divider-color, #e0e0e0); background: #191919; isolation: isolate">
      <img class="d-block" style="position: absolute; max-width: none; width: 148.39286%; height: auto; left: -27.85714%; top: -29.14286%" src="{{ '/assets/img/railway-reconstruction/results/front-view.png' | relative_url }}" width="831" height="462" loading="lazy" alt="Elevated front view of the reconstructed railway bridge">
    </div>
    <p class="text-muted small" style="margin: 0.65rem 0 0; line-height: 1.6">(a) Elevated front view</p>
  </div>
<div style="min-width: 0">
    <div class="d-block rounded" style="position: relative; aspect-ratio: 16 / 10; overflow: hidden; border: 1px solid var(--global-divider-color, #e0e0e0); background: #191919; isolation: isolate">
      <img class="d-block" style="position: absolute; max-width: none; width: 116.66667%; height: auto; left: -0.86806%; top: -31.11111%" src="{{ '/assets/img/railway-reconstruction/results/side-view.png' | relative_url }}" width="672" height="474" loading="lazy" alt="Side view of the reconstructed railway bridge">
    </div>
    <p class="text-muted small" style="margin: 0.65rem 0 0; line-height: 1.6">(b) Side view</p>
  </div>
  </div>
  <figcaption class="text-muted small" style="margin-top: 0.85rem; line-height: 1.6"><strong>Figure 6.</strong> Elevated front and side views of the reconstructed railway bridge.</figcaption>
</figure>

</section>

<section aria-labelledby="railway-assets" style="margin-top: 3.5rem">
<h3 id="railway-assets" style="font-size: 1.25rem; margin-bottom: 1rem">Transportation Asset Extraction</h3>

<p>Class-based selection extracts track regions and crossbeams from the reconstructed scene for separate display. The extracted track cloud retains its longitudinal shape, while the crossbeams appear as a set of distinct structural elements. These results connect scene reconstruction with the retrieval and visualization of transportation assets.</p>

<figure id="railway-figure-7" style="margin: 1.75rem 0 0">
  <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(min(100%, 20rem), 1fr)); gap: 1.5rem; align-items: start">
<div style="min-width: 0">
    <div class="d-block rounded" style="position: relative; aspect-ratio: 16 / 10; overflow: hidden; border: 1px solid var(--global-divider-color, #e0e0e0); background: #191919; isolation: isolate">
      <img class="d-block" style="position: absolute; max-width: none; width: 203.47222%; height: auto; left: -61.63194%; top: -23.05556%" src="{{ '/assets/img/railway-reconstruction/results/rail-extraction.png' | relative_url }}" width="1172" height="453" loading="lazy" alt="Track region extracted from the full scene">
    </div>
    <p class="text-muted small" style="margin: 0.65rem 0 0; line-height: 1.6">(a) Track extraction</p>
  </div>
<div style="min-width: 0">
    <div class="d-block rounded" style="position: relative; aspect-ratio: 16 / 10; overflow: hidden; border: 1px solid var(--global-divider-color, #e0e0e0); background: #191919; isolation: isolate">
      <img class="d-block" style="position: absolute; max-width: none; width: 333.52273%; height: auto; left: -166.76136%; top: -89.09091%" src="{{ '/assets/img/railway-reconstruction/results/crossbeam-extraction.png' | relative_url }}" width="1174" height="478" loading="lazy" alt="Crossbeams extracted by object class">
    </div>
    <p class="text-muted small" style="margin: 0.65rem 0 0; line-height: 1.6">(b) Crossbeam extraction</p>
  </div>
  </div>
  <figcaption class="text-muted small" style="margin-top: 0.85rem; line-height: 1.6"><strong>Figure 7.</strong> Track regions and crossbeams extracted from the reconstructed scene.</figcaption>
</figure>

</section>

</section>

</article>

</div>
