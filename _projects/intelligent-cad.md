---
layout: default
title: "Intelligent CAD: From Geometric Understanding to Editable Reconstruction"
paper_title: "Intelligent CAD: From Geometric Understanding to Editable Reconstruction"
description: Geometric understanding, executable CAD programs, and editable parametric reconstruction.
importance: 3
category: Research
permalink: /projects/intelligent-cad/
---

<div class="post" id="intelligent-cad-project" lang="en" style="font-family: Roboto, sans-serif; font-size: 1rem; font-weight: 300">

<header class="post-header" style="margin-bottom: 2.75rem">
  <h1 class="post-title" style="font-size: clamp(1.5rem, 2.4vw, 2rem); line-height: 1.4; margin: 0">{{ page.paper_title }}</h1>
  <div class="project-metadata" style="margin-top: 1.5rem; font-size: 1rem; font-weight: 300; line-height: 1.75">
    <p style="margin: 0">Xiaozhen Ma · Institute of Automation, Chinese Academy of Sciences</p>
    <p class="text-muted small" style="margin: 0.25rem 0 0">Intelligent CAD Project · February 2026–Present</p>
  </div>
</header>

<article style="line-height: 1.75">

<section aria-labelledby="cad-abstract">
<h2 id="cad-abstract" style="font-size: 1.5rem; margin-bottom: 1.25rem">Abstract</h2>

<p>This project studies automated CAD modeling and reconstruction from point clouds through reproductions and experiments with CAD-Assistant, ParSeNet, Point2CAD, and CAD-Recode. It examines how geometric priors, boundary supervision, CAD knowledge, and execution feedback affect modeling quality. The study progresses from changes to individual models toward multiple-candidate generation and explicit geometric validation. In an independent confirmation evaluation on 300 objects, the combined candidate-generation and validation configuration reduces median Chamfer Distance by approximately 13.4%, improves mean error and IoU, and retains the same execution and solid-validity success count. The outputs remain editable as CadQuery programs and support B-Rep and STEP export. Ongoing work extends this approach toward a CAD agent that coordinates generation, geometric analysis, and program repair.</p>

</section>

<section aria-labelledby="cad-overview" style="margin-top: 3.5rem">
<h2 id="cad-overview" style="font-size: 1.5rem; margin-bottom: 1.25rem">Overview</h2>

<p>The study connects geometric understanding with executable, editable CAD reconstruction. CAD-Assistant provides a setting for testing geometric priors in automated modeling through the FreeCAD Python API. ParSeNet and Point2CAD provide complementary routes for studying surface segmentation, geometric fitting, and topology recovery from point clouds. CAD-Recode generates parametric programs that can be executed, checked, and exported with CadQuery and OpenCascade.</p>

<p>My work covers system deployment, method reproduction, data-interface adaptation, training, and evaluation. Experiments first examine prompt constraints, boundary supervision, and knowledge-enhanced training, then turn to parameter refinement and program diagnosis. The strongest confirmed result comes from combining a larger candidate pool with execution filtering and dense geometric validation under a frozen generation model.</p>

</section>

<section aria-labelledby="cad-results" style="margin-top: 3.5rem">
<h2 id="cad-results" style="font-size: 1.5rem; margin-bottom: 1.75rem">Results</h2>

<section aria-labelledby="cad-assistant">
<h3 id="cad-assistant" style="font-size: 1.25rem; margin-bottom: 1rem">01 · CAD-Assistant: Geometric Priors for Automated Modeling</h3>

<p>CAD-Assistant uses the FreeCAD Python API as its modeling and execution interface. The reproduced workflow covers modeling plans, code generation, program execution, and output inspection. My experiments adjust prompts and modeling plans to include dimensions, geometric relationships, and modeling constraints, assessing their effects on code executability and geometric correctness.</p>

<p>The reproduction establishes a working automated modeling pipeline and enables comparisons across prompt configurations. Adding geometric priors as text alone does not consistently improve overall modeling quality.</p>

</section>

<section aria-labelledby="cad-parsenet" style="margin-top: 3.5rem">
<h3 id="cad-parsenet" style="font-size: 1.25rem; margin-bottom: 1rem">02 · ParSeNet: Surface Segmentation for CAD Reconstruction</h3>

<p>ParSeNet provides surface-instance segmentation and geometric-type classification for point clouds. My work includes environment setup, data preparation, pretrained-model evaluation, and training from scratch. Experiments investigate three-axis and multi-view projections, boundary supervision, and geometric consistency constraints to address over-segmentation, under-segmentation, and label confusion at surface intersections.</p>

<p>Under a common evaluation protocol on 4,000 test samples, both boundary-enhanced configurations fall below the official baseline in surface-segmentation and geometric-type mIoU. The tested boundary and consistency objectives therefore provide no improvement over the baseline.</p>

<div role="region" aria-labelledby="cad-parsenet-caption" tabindex="0" style="margin-top: 1.75rem; overflow-x: auto; -webkit-overflow-scrolling: touch">
  <table id="cad-parsenet-table" class="table table-sm" style="width: 100%; min-width: 0; margin: 0; color: inherit; font-variant-numeric: tabular-nums">
    <caption id="cad-parsenet-caption" class="text-muted small" style="caption-side: bottom; padding-top: 0.85rem; line-height: 1.6">Table 1. ParSeNet evaluation on 4,000 test samples. Higher mIoU indicates better performance.</caption>
    <thead>
      <tr><th scope="col" style="text-align: left">Configuration</th><th scope="col" style="text-align: right">Surface segmentation mIoU ↑</th><th scope="col" style="text-align: right">Geometric type mIoU ↑</th></tr>
    </thead>
    <tbody>
      <tr><th scope="row" style="text-align: left">Official baseline</th><td style="text-align: right; white-space: nowrap"><strong>81.35%</strong></td><td style="text-align: right; white-space: nowrap"><strong>87.57%</strong></td></tr>
      <tr><th scope="row" style="text-align: left">Boundary</th><td style="text-align: right; white-space: nowrap">64.30%</td><td style="text-align: right; white-space: nowrap">59.88%</td></tr>
      <tr><th scope="row" style="text-align: left">Boundary + Pair</th><td style="text-align: right; white-space: nowrap">63.42%</td><td style="text-align: right; white-space: nowrap">56.58%</td></tr>
    </tbody>
  </table>
</div>

</section>

<section aria-labelledby="cad-point2cad" style="margin-top: 3.5rem">
<h3 id="cad-point2cad" style="font-size: 1.25rem; margin-bottom: 1rem">03 · Point2CAD: From Segmented Points to Structured CAD Geometry</h3>

<p>Point2CAD recovers surfaces, boundaries, and topology from segmented point clouds. My work reproduces the method and adapts its data interfaces, tracing how surface-segmentation outputs enter geometric reconstruction. This route supports the study of how segmentation errors affect surface fitting and topology recovery and serves as a geometric reference for point-cloud-to-CAD reconstruction.</p>

<p>The reproduction and interface adaptation establish a working reconstruction workflow, but the experiments do not yield a consistent quantitative improvement that can be reported separately.</p>

</section>

<section aria-labelledby="cad-recode" style="margin-top: 3.5rem">
<h3 id="cad-recode" style="font-size: 1.25rem; margin-bottom: 1rem">04 · CAD-Recode: Knowledge Enhancement and Geometric Validation</h3>

<p>CAD-Recode generates editable CadQuery programs from point clouds. CadQuery and OpenCascade provide program execution, solid checks, and CAD export. My work establishes the complete generation and evaluation pipeline from input points to programs, B-Rep solids, and STEP files, then examines CAD-knowledge curricula, descriptive-geometry tasks, parameter refinement, and program-structure diagnosis.</p>

<div role="region" aria-labelledby="cad-studies-caption" tabindex="0" style="margin-top: 1.75rem; overflow-x: auto; -webkit-overflow-scrolling: touch">
  <table id="cad-studies-table" class="table table-sm" style="width: 100%; min-width: 0; margin: 0; color: inherit; font-variant-numeric: tabular-nums">
    <caption id="cad-studies-caption" class="text-muted small" style="caption-side: bottom; padding-top: 0.85rem; line-height: 1.6">Table 2. CAD-Recode experiments, from model adaptation to candidate generation and validation.</caption>
    <thead>
      <tr><th scope="col" style="text-align: left; width: 40%">Research direction</th><th scope="col" style="text-align: left">Experimental outcome</th></tr>
    </thead>
    <tbody>
      <tr><th scope="row" style="text-align: left">Projector, LoRA, curriculum training, and Knowledge Head</th><td style="text-align: left">Some auxiliary tasks are learnable, but final reconstruction quality does not improve consistently.</td></tr>
      <tr><th scope="row" style="text-align: left">Descriptive-geometry tasks</th><td style="text-align: left">Some geometric metrics improve, with trade-offs in the original CAD generation capability.</td></tr>
      <tr><th scope="row" style="text-align: left">Continuous parameter refinement and program-structure diagnosis</th><td style="text-align: left">Parameter refinement shows degradation; evidence for effective structural repair remains insufficient.</td></tr>
      <tr><th scope="row" style="text-align: left">Multiple-candidate generation and geometric validation</th><td style="text-align: left">The combined configuration improves overall reconstruction quality on a new confirmation set.</td></tr>
    </tbody>
  </table>
</div>

<p style="margin-top: 1.75rem">With the generation model frozen, the final workflow produces multiple candidates, filters them through execution, and uses dense geometric validation for selection. On an independent confirmation set of 300 objects, S2@100 reduces median Chamfer Distance by approximately 13.4% relative to S0@10. Mean Chamfer Distance and mean IoU also improve, while the execution and valid-solid count remains 298 out of 300 for both configurations.</p>

<div role="region" aria-labelledby="cad-confirmation-caption" tabindex="0" style="margin-top: 1.75rem; overflow-x: auto; -webkit-overflow-scrolling: touch">
  <table id="cad-confirmation-table" class="table table-sm" style="width: 100%; min-width: 0; margin: 0; color: inherit; font-variant-numeric: tabular-nums">
    <caption id="cad-confirmation-caption" class="text-muted small" style="caption-side: bottom; padding-top: 0.85rem; line-height: 1.6">Table 3. Independent confirmation on 300 objects. CD denotes Chamfer Distance. S0@10 uses 10 candidates and S2@100 uses 100; the comparison evaluates the combined effects of candidate expansion, execution filtering, and dense geometric validation.</caption>
    <thead>
      <tr><th scope="col" style="text-align: left">Metric</th><th scope="col" style="text-align: right">Baseline S0@10</th><th scope="col" style="text-align: right">Candidate validation S2@100</th></tr>
    </thead>
    <tbody>
      <tr><th scope="row" style="text-align: left">Median CD × 1000 ↓</th><td style="text-align: right; white-space: nowrap">0.203935</td><td style="text-align: right; white-space: nowrap"><strong>0.176646</strong></td></tr>
      <tr><th scope="row" style="text-align: left">Mean CD × 1000 ↓</th><td style="text-align: right; white-space: nowrap">0.299815</td><td style="text-align: right; white-space: nowrap"><strong>0.208125</strong></td></tr>
      <tr><th scope="row" style="text-align: left">Mean IoU ↑</th><td style="text-align: right; white-space: nowrap">0.974109</td><td style="text-align: right; white-space: nowrap"><strong>0.980866</strong></td></tr>
      <tr><th scope="row" style="text-align: left">Successful execution / valid solid</th><td style="text-align: right; white-space: nowrap">298/300</td><td style="text-align: right; white-space: nowrap">298/300</td></tr>
    </tbody>
  </table>
</div>

<p style="margin-top: 1.75rem">The selected outputs retain editable CadQuery programs rather than only a final surface representation. B-Rep and STEP export preserve access to the resulting CAD geometry for further inspection and editing.</p>

</section>

</section>

<section aria-labelledby="cad-future" style="margin-top: 3.5rem">
<h2 id="cad-future" style="font-size: 1.5rem; margin-bottom: 1.25rem">Future Work</h2>

<h3 id="cad-agent" style="font-size: 1.25rem; margin-bottom: 1rem">05 · A CAD Agent for Parametric Reconstruction</h3>

<p>Ongoing work focuses on a CAD agent that selects tools according to task requirements and execution feedback. The planned system brings together CAD generation models, geometric analysis methods such as Point2CAD, and program-repair models. A large language model handles task planning and tool selection, while CadQuery and OpenCascade provide modeling execution and geometric validation.</p>

<p>My current work develops model interfaces, structured error feedback, and task scheduling around a generation, execution, validation, and correction loop. The aim is to identify reconstruction problems and route them to an appropriate geometric-analysis or program-repair tool, extending the verified candidate-selection workflow toward coordinated parametric CAD reconstruction.</p>

</section>

</article>

</div>
