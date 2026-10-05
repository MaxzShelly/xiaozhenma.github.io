---
layout: default
title: PIKAN-Drive
paper_title: "PIKAN-Drive: KAN and Physics-Informed Learning for Autonomous Driving"
description: From PilotNet steering regression to Fast-BEV 3D detection.
importance: 4
category: Research
permalink: /projects/pikan-drive/
---

<div class="post" id="pikan-drive-project" lang="en">

<header class="post-header" style="margin-bottom: 2.75rem">
  <h1 class="post-title" style="font-size: clamp(1.5rem, 2.4vw, 2rem); line-height: 1.4; margin: 0">{{ page.paper_title }}</h1>
  <p class="text-muted" style="margin: 1rem 0 1.5rem; line-height: 1.6">From Steering Prediction to Multi-Camera 3D Object Detection</p>
  <p style="margin: 0; line-height: 1.75">Xiaozhen Ma · University of California, Irvine</p>
  <p class="text-muted small" style="margin: 0.25rem 0 0; line-height: 1.75">UCInspire 2026 · July–September 2026</p>
  <p class="text-muted small" style="margin: 0.25rem 0 0; line-height: 1.75">Faculty Mentor: Prof. Fadi Kurdahi</p>
</header>

<article style="line-height: 1.75">

<section aria-labelledby="pikan-abstract">
<h2 id="pikan-abstract" style="font-size: 1.5rem; margin-bottom: 1.25rem">Abstract</h2>

<p>This project explores Kolmogorov-Arnold networks (KANs) and physics-informed learning for autonomous driving through steering-angle prediction and multi-camera 3D object detection. Experiments with PilotNet and Fast-BEV compare prediction-head architectures and evaluate the effects of physical priors and task-specific auxiliary objectives. In PilotNet, the optimized PI-KAN configuration reduces MAE by 11.3% and RMSE by 9.7% relative to the MLP baseline. In Fast-BEV, the KAN detection head achieves higher mAP and NDS, while additional auxiliary losses provide no clear further improvement. The results show the potential of KAN prediction heads across both tasks and indicate that the effects of constraints depend on the task and architecture.</p>

</section>

<section aria-labelledby="pikan-overview" style="margin-top: 3.5rem">
<h2 id="pikan-overview" style="font-size: 1.5rem; margin-bottom: 1.25rem">Overview</h2>

<p>The study asks whether replacing a conventional multilayer perceptron (MLP) prediction head with a KAN improves performance, and whether physical priors and task-specific constraints provide additional gains. The experiments begin with steering regression in PilotNet and extend to multi-camera 3D detection in Fast-BEV M0. The two stages are evaluated separately. Each retains its base feature-extraction pipeline so that the comparison focuses on the prediction head and training objectives.</p>

<div role="region" aria-labelledby="pikan-study-design-caption" tabindex="0" style="margin-top: 1.75rem; overflow-x: auto; -webkit-overflow-scrolling: touch">
  <table id="pikan-study-design" class="table table-sm" style="width: 100%; min-width: 0; margin: 0; color: inherit; font-variant-numeric: tabular-nums">
    <caption id="pikan-study-design-caption" class="text-muted small" style="caption-side: bottom; padding-top: 0.85rem; line-height: 1.6">Table 1. Task-specific study design.</caption>
    <thead>
      <tr><th scope="col" style="text-align: left">Study component</th><th scope="col" style="text-align: left">Steering prediction</th><th scope="col" style="text-align: left">3D object detection</th></tr>
    </thead>
    <tbody>
      <tr><th scope="row" style="text-align: left">Base model</th><td style="text-align: left">PilotNet</td><td style="text-align: left">Fast-BEV M0</td></tr>
      <tr><th scope="row" style="text-align: left">Input and output</th><td style="text-align: left">Front-view image to steering angle</td><td style="text-align: left">Multi-camera images to 3D bounding boxes</td></tr>
      <tr><th scope="row" style="text-align: left">Architecture comparison</th><td style="text-align: left">MLP and KAN prediction heads</td><td style="text-align: left">MLP and KAN detection heads</td></tr>
      <tr><th scope="row" style="text-align: left">Constraint study</th><td style="text-align: left">Smoothness, output range, and sparsity regularization</td><td style="text-align: left">Classification, regression, and direction-related auxiliary losses</td></tr>
      <tr><th scope="row" style="text-align: left">Evaluation metrics</th><td style="text-align: left">MAE and RMSE</td><td style="text-align: left">mAP and NDS</td></tr>
    </tbody>
  </table>
</div>

<h3 id="pikan-my-work" style="font-size: 1.25rem; margin-top: 2rem; margin-bottom: 1rem">My Work</h3>

<p>Building on the research direction, PilotNet baseline, and initial KAN implementation provided by the faculty mentor, my work focuses on model comparison, constraint design, training, and experimental analysis.</p>

<ul>
  <li><strong>Model comparison and evaluation:</strong> the PilotNet study compares MLP, PI-MLP, KAN, and PI-KAN through model training, parameter tuning, and test-result analysis.</li>
  <li><strong>Constraints for steering prediction:</strong> experiments assess smoothness and output-range constraints together with KAN sparsity regularization, testing different combinations and weights.</li>
  <li><strong>Extension to 3D perception:</strong> the Fast-BEV study compares MLP and KAN detection heads to evaluate the effect of the prediction-head architecture on 3D detection.</li>
  <li><strong>Grouped and individual ablations:</strong> experiments progress from combinations of nine auxiliary losses to targeted tests of confidence, size, velocity, and direction terms, separating architecture gains from auxiliary-loss effects.</li>
</ul>

</section>

<section aria-labelledby="pikan-results" style="margin-top: 3.5rem">
<h2 id="pikan-results" style="font-size: 1.5rem; margin-bottom: 1.75rem">Results</h2>

<section aria-labelledby="pikan-steering">
<h3 id="pikan-steering" style="font-size: 1.25rem; margin-bottom: 1rem">Reducing Steering Error with PilotNet</h3>

<p>The KAN baseline outperforms the MLP baseline, and the optimized PI-KAN configuration reduces the errors further. Relative to MLP, it lowers MAE by 11.3% and RMSE by 9.7%. Its MAE is also approximately 2.8% lower than that of the KAN baseline. The different constraint combinations yield different results, showing that both the choice of constraints and their weights affect performance.</p>

<div role="region" aria-labelledby="pikan-pilotnet-table-caption" tabindex="0" style="margin-top: 1.75rem; overflow-x: auto; -webkit-overflow-scrolling: touch">
  <table id="pikan-pilotnet-table" class="table table-sm" style="width: 100%; min-width: 0; margin: 0; color: inherit; font-variant-numeric: tabular-nums">
    <caption id="pikan-pilotnet-table-caption" class="text-muted small" style="caption-side: bottom; padding-top: 0.85rem; line-height: 1.6">Table 2. PilotNet steering prediction. Lower MAE and RMSE indicate better performance.</caption>
    <thead>
      <tr><th scope="col" style="text-align: left">Model / configuration</th><th scope="col" style="text-align: right; white-space: nowrap">MAE ↓</th><th scope="col" style="text-align: right; white-space: nowrap">RMSE ↓</th></tr>
    </thead>
    <tbody>
      <tr><th scope="row" style="text-align: left">MLP baseline</th><td style="text-align: right; white-space: nowrap">3.616</td><td style="text-align: right; white-space: nowrap">6.825</td></tr>
      <tr><th scope="row" style="text-align: left">KAN baseline</th><td style="text-align: right; white-space: nowrap">3.301</td><td style="text-align: right; white-space: nowrap">6.281</td></tr>
      <tr><th scope="row" style="text-align: left">PI-KAN: range constraint</th><td style="text-align: right; white-space: nowrap">3.293</td><td style="text-align: right; white-space: nowrap">6.284</td></tr>
      <tr><th scope="row" style="text-align: left">PI-KAN: smoothness + range</th><td style="text-align: right; white-space: nowrap">3.290</td><td style="text-align: right; white-space: nowrap">6.270</td></tr>
      <tr><th scope="row" style="text-align: left">PI-KAN: full constraint combination</th><td style="text-align: right; white-space: nowrap">3.299</td><td style="text-align: right; white-space: nowrap">6.212</td></tr>
      <tr><th scope="row" style="text-align: left"><strong>PI-KAN: optimized configuration</strong></th><td style="text-align: right; white-space: nowrap"><strong>3.209</strong></td><td style="text-align: right; white-space: nowrap"><strong>6.163</strong></td></tr>
    </tbody>
  </table>
</div>

</section>

<section aria-labelledby="pikan-detection" style="margin-top: 3.5rem">
<h3 id="pikan-detection" style="font-size: 1.25rem; margin-bottom: 1rem">Improving 3D Detection with a KAN Head</h3>

<p>In Fast-BEV M0, replacing the MLP detection head with a KAN raises mAP from 0.2559 to 0.2720 and NDS from 0.3950 to 0.4046. These gains correspond to 1.61 and 0.96 percentage points, respectively, when the metrics are expressed on a 100-point scale. The improvement in both metrics supports further study of KAN detection heads.</p>

<div role="region" aria-labelledby="pikan-fastbev-table-caption" tabindex="0" style="margin-top: 1.75rem; overflow-x: auto; -webkit-overflow-scrolling: touch">
  <table id="pikan-fastbev-table" class="table table-sm" style="width: 100%; min-width: 0; margin: 0; color: inherit; font-variant-numeric: tabular-nums">
    <caption id="pikan-fastbev-table-caption" class="text-muted small" style="caption-side: bottom; padding-top: 0.85rem; line-height: 1.6">Table 3. Fast-BEV M0 detection-head comparison. Higher mAP and NDS indicate better performance.</caption>
    <thead>
      <tr><th scope="col" style="text-align: left">Detection head</th><th scope="col" style="text-align: right; white-space: nowrap">mAP ↑</th><th scope="col" style="text-align: right; white-space: nowrap">NDS ↑</th></tr>
    </thead>
    <tbody>
      <tr><th scope="row" style="text-align: left">MLP baseline</th><td style="text-align: right; white-space: nowrap">0.2559</td><td style="text-align: right; white-space: nowrap">0.3950</td></tr>
      <tr><th scope="row" style="text-align: left"><strong>KAN baseline</strong></th><td style="text-align: right; white-space: nowrap"><strong>0.2720</strong></td><td style="text-align: right; white-space: nowrap"><strong>0.4046</strong></td></tr>
      <tr><th scope="row" style="text-align: left">Absolute gain</th><td style="text-align: right; white-space: nowrap">+0.0161</td><td style="text-align: right; white-space: nowrap">+0.0096</td></tr>
    </tbody>
  </table>
</div>

</section>

<section aria-labelledby="pikan-ablations" style="margin-top: 3.5rem">
<h3 id="pikan-ablations" style="font-size: 1.25rem; margin-bottom: 1rem">Evaluating Auxiliary Losses</h3>

<p>Adding all nine auxiliary losses lowers both metrics for MLP and KAN heads. Targeted configurations remain close to their respective baselines: the Scale constraint slightly improves the MLP results, and Dir3 slightly improves the KAN results. These small differences do not establish a consistent benefit from auxiliary losses.</p>

<div role="region" aria-labelledby="pikan-ablation-table-caption" tabindex="0" style="margin-top: 1.75rem; overflow-x: auto; -webkit-overflow-scrolling: touch">
  <table id="pikan-ablation-table" class="table table-sm" style="width: 100%; min-width: 0; margin: 0; color: inherit; font-variant-numeric: tabular-nums">
    <caption id="pikan-ablation-table-caption" class="text-muted small" style="caption-side: bottom; padding-top: 0.85rem; line-height: 1.6">Table 4. Grouped and targeted auxiliary-loss ablations for MLP and KAN detection heads.</caption>
    <thead>
      <tr><th scope="col" style="text-align: left">Head</th><th scope="col" style="text-align: left">Auxiliary-loss configuration</th><th scope="col" style="text-align: right; white-space: nowrap">mAP ↑</th><th scope="col" style="text-align: right; white-space: nowrap">NDS ↑</th></tr>
    </thead>
    <tbody>
      <tr><th scope="row" style="text-align: left">MLP</th><td style="text-align: left">Baseline</td><td style="text-align: right; white-space: nowrap">0.2559</td><td style="text-align: right; white-space: nowrap">0.3950</td></tr>
      <tr><th scope="row" style="text-align: left">MLP</th><td style="text-align: left">Full9: nine-loss combination</td><td style="text-align: right; white-space: nowrap">0.2547</td><td style="text-align: right; white-space: nowrap">0.3947</td></tr>
      <tr><th scope="row" style="text-align: left">MLP</th><td style="text-align: left">Scale: size-related constraint</td><td style="text-align: right; white-space: nowrap">0.2560</td><td style="text-align: right; white-space: nowrap">0.3953</td></tr>
      <tr><th scope="row" style="text-align: left">KAN</th><td style="text-align: left">Baseline</td><td style="text-align: right; white-space: nowrap">0.2720</td><td style="text-align: right; white-space: nowrap">0.4046</td></tr>
      <tr><th scope="row" style="text-align: left">KAN</th><td style="text-align: left">Full9: nine-loss combination</td><td style="text-align: right; white-space: nowrap">0.2703</td><td style="text-align: right; white-space: nowrap">0.4027</td></tr>
      <tr><th scope="row" style="text-align: left">KAN</th><td style="text-align: left">Dir3: direction-loss combination</td><td style="text-align: right; white-space: nowrap">0.2721</td><td style="text-align: right; white-space: nowrap">0.4047</td></tr>
    </tbody>
  </table>
</div>

</section>

</section>

<section aria-labelledby="pikan-findings" style="margin-top: 3.5rem">
<h2 id="pikan-findings" style="font-size: 1.5rem; margin-bottom: 1.25rem">Key Findings</h2>

<p>The gain from replacing the prediction head is more evident than the gain from adding auxiliary losses in Fast-BEV. PI-KAN achieves the best steering-prediction results among the tested configurations, while additional constraints have a more limited effect on 3D detection. The results distinguish the contribution of the head architecture from that of the training objectives and show why constraint design requires task-specific evaluation.</p>

</section>

</article>

</div>
