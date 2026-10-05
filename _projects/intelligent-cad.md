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
    <p style="margin: 0">Xiaozhen Ma · National Laboratory of Pattern Recognition, Institute of Automation, Chinese Academy of Sciences</p>
    <p class="text-muted small" style="margin: 0.25rem 0 0">Research Assistant · February 2026–Present</p>
    <p class="text-muted small" style="margin: 0.25rem 0 0">Faculty Mentors: Prof. Dong-Ming Yan and Prof. Mingyang Zhao</p>
  </div>
</header>

<article style="line-height: 1.75">

<p>This project studies automated CAD modeling and reconstruction from point clouds through reproductions and experiments with CAD-Assistant, ParSeNet, Point2CAD, and CAD-Recode. It examines how geometric priors, boundary supervision, knowledge enhancement, and execution feedback affect modeling quality. The research progresses from changes to individual models toward multiple-candidate generation and explicit geometric validation, and further explores the coordination of multiple models for editable parametric CAD reconstruction.</p>

<section aria-labelledby="cad-assistant" style="margin-top: 3.5rem">
<h2 id="cad-assistant" style="font-size: 1.5rem; margin-bottom: 1.25rem">01 · CAD-Assistant</h2>
<p class="text-muted">Geometric Priors for Automated CAD Modeling</p>

<h3 style="font-size: 1.25rem; margin-top: 2rem; margin-bottom: 1rem">Model</h3>
<p>CAD-Assistant, with the FreeCAD Python API as the modeling and execution interface.</p>

<h3 style="font-size: 1.25rem; margin-top: 2rem; margin-bottom: 1rem">My Work</h3>
<p>My work covers system deployment and evaluation, establishing a workflow for modeling plans, code generation, program execution, and output inspection. Building on this workflow, I adjust prompts and modeling plans to include dimensions, geometric relationships, and modeling constraints, and assess their effects on code executability and geometric correctness.</p>

<h3 style="font-size: 1.25rem; margin-top: 2rem; margin-bottom: 1rem">Experimental Results</h3>
<p>The reproduction establishes a working automated modeling pipeline and enables experiments with multiple prompt configurations. Adding geometric priors as text alone does not consistently improve overall modeling quality.</p>

</section>

<section aria-labelledby="cad-parsenet" style="margin-top: 3.5rem">
<h2 id="cad-parsenet" style="font-size: 1.5rem; margin-bottom: 1.25rem">02 · ParSeNet</h2>
<p class="text-muted">Point Cloud Surface Segmentation for CAD Reconstruction</p>

<h3 style="font-size: 1.25rem; margin-top: 2rem; margin-bottom: 1rem">Model</h3>
<p>ParSeNet, for surface-instance segmentation and geometric-type classification of point clouds.</p>

<h3 style="font-size: 1.25rem; margin-top: 2rem; margin-bottom: 1rem">My Work</h3>
<p>My work includes environment setup, data preparation, pretrained-model evaluation, and training from scratch. To address surface over-segmentation, under-segmentation, and label confusion at intersections, I investigate three-axis and multi-view projections, boundary supervision, and geometric consistency constraints under a common evaluation protocol.</p>

<h3 style="font-size: 1.25rem; margin-top: 2rem; margin-bottom: 1rem">Experimental Results</h3>
<p>On 4,000 test samples, the boundary-enhanced configurations do not outperform the official baseline.</p>

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

<p style="margin-top: 1.75rem">The tested boundary and consistency supervision does not provide an improvement over the baseline.</p>

</section>

<section aria-labelledby="cad-point2cad" style="margin-top: 3.5rem">
<h2 id="cad-point2cad" style="font-size: 1.5rem; margin-bottom: 1.25rem">03 · Point2CAD</h2>
<p class="text-muted">From Segmented Point Clouds to Structured CAD Geometry</p>

<h3 style="font-size: 1.25rem; margin-top: 2rem; margin-bottom: 1rem">Model</h3>
<p>Point2CAD, for recovering surfaces, boundaries, and topology from segmented point clouds.</p>

<h3 style="font-size: 1.25rem; margin-top: 2rem; margin-bottom: 1rem">My Work</h3>
<p>My work reproduces the method and adapts its data interfaces, tracing how surface-segmentation outputs enter subsequent geometric reconstruction. I study how segmentation errors affect surface fitting and topology recovery and use this route as a geometric reference for point-cloud-to-CAD reconstruction.</p>

<h3 style="font-size: 1.25rem; margin-top: 2rem; margin-bottom: 1rem">Experimental Results</h3>
<p>The reproduction and interface adaptation establish a working reconstruction workflow, but the experiments do not yield a consistent quantitative improvement that can be reported separately.</p>

</section>

<section aria-labelledby="cad-recode" style="margin-top: 3.5rem">
<h2 id="cad-recode" style="font-size: 1.5rem; margin-bottom: 1.25rem">04 · CAD-Recode</h2>
<p class="text-muted">Knowledge Enhancement and Geometric Validation for Editable CAD</p>

<h3 style="font-size: 1.25rem; margin-top: 2rem; margin-bottom: 1rem">Model</h3>
<p>CAD-Recode, with CadQuery and OpenCascade for program execution, solid checks, and CAD export.</p>

<h3 style="font-size: 1.25rem; margin-top: 2rem; margin-bottom: 1rem">My Work</h3>
<p>My work establishes a complete generation and evaluation pipeline from point clouds to CadQuery programs, B-Rep solids, and STEP files. Experiments examine CAD-knowledge curricula, descriptive-geometry tasks, parameter refinement, and program-structure diagnosis in sequence. The subsequent workflow combines multiple-candidate generation, execution filtering, and dense geometric validation with a frozen model.</p>

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

<h3 style="font-size: 1.25rem; margin-top: 2rem; margin-bottom: 1rem">Main Results</h3>
<p>In an independent confirmation evaluation on 300 objects, the multiple-candidate and geometric-validation configuration reduces median Chamfer Distance by approximately 13.4%, while also improving mean error and IoU.</p>

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

<p style="margin-top: 1.75rem">The final outputs retain editable CadQuery programs and support B-Rep and STEP export.</p>

</section>

<section aria-labelledby="cad-future" style="margin-top: 3.5rem">
<h2 id="cad-future" style="font-size: 1.5rem; margin-bottom: 1.25rem">05 · Future Work</h2>
<p class="text-muted">Building an Agent for Parametric CAD Reconstruction</p>

<h3 style="font-size: 1.25rem; margin-top: 2rem; margin-bottom: 1rem">Models and Tools</h3>
<p>The planned system integrates CAD generation models, geometric analysis models such as Point2CAD, and program-repair models. CadQuery and OpenCascade provide modeling execution and geometric validation, while a large language model handles task planning and tool selection.</p>

<h3 style="font-size: 1.25rem; margin-top: 2rem; margin-bottom: 1rem">My Work</h3>
<p>My ongoing work focuses on a CAD agent that selects tools according to task requirements and execution feedback. I design model interfaces, structured error feedback, and task-scheduling mechanisms around a generation, execution, validation, and correction loop. The aim is to identify problems in the current reconstruction and select an appropriate geometric-analysis or program-repair tool.</p>

</section>

</article>

</div>
