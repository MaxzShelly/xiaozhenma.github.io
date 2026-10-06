---
layout: default
title: FPGA Digital System Design
description: Hierarchical digital modules, simulation, and FPGA testing.
importance: 2
category: Engineering
permalink: /projects/fpga-digital-systems/
---

<div class="post" id="fpga-traffic-light-project" lang="en" style="font-family: Roboto, sans-serif; font-size: 1rem; font-weight: 300">

<header class="post-header" style="margin-bottom: 2.75rem">
  <h1 class="post-title" style="font-size: clamp(1.5rem, 2.4vw, 2rem); line-height: 1.4; margin: 0">FPGA Digital System Design</h1>
  <p class="text-muted" style="margin: 1rem 0 1.5rem; line-height: 1.6">FPGA-Based Traffic Light Control System</p>
  <p class="text-muted small" style="margin: 0; line-height: 1.75">Quartus · Hardware Description Language · Logic Simulation · FPGA Testing</p>
</header>

<article style="line-height: 1.75">

<figure style="margin: 0 0 3.5rem">
  <img src="{{ '/assets/img/fpga-traffic-light/board-running.jpg' | relative_url }}" alt="FPGA development board running the traffic-light controller, with an illuminated LED and a two-digit countdown display." width="1920" height="1080" decoding="async" style="display: block; width: 100%; height: auto; border-radius: 0.375rem">
  <figcaption class="text-muted small" style="margin-top: 0.85rem; line-height: 1.6">Traffic-light control and countdown display on the FPGA development board.</figcaption>
</figure>

<section aria-labelledby="fpga-overview">
<h2 id="fpga-overview" style="font-size: 1.5rem; margin-bottom: 1.25rem">Overview</h2>

<p>This project develops a hierarchical FPGA traffic-light controller using Quartus and a hardware description language. Clock division, timing control, signal decoding, and seven-segment display modules connect through predefined ports to produce a repeating traffic-light sequence with a countdown display. The system supports normal and accelerated timing, maintenance mode, and reset control. Development covers module implementation, system integration, logic simulation, waveform analysis, and FPGA hardware testing.</p>

</section>

<section aria-labelledby="fpga-architecture" style="margin-top: 3.5rem">
<h2 id="fpga-architecture" style="font-size: 1.5rem; margin-bottom: 1.25rem">01 · System Architecture</h2>

<p>A clock divider derives timing signals from the board's 50 MHz clock. The core logic updates the system state according to the counter and switch inputs, while the decoder and display modules drive the LEDs and two seven-segment digits.</p>

<figure style="margin: 1.75rem 0">
  <img src="{{ '/assets/img/fpga-traffic-light/system-architecture.png' | relative_url }}" alt="Traffic-light system architecture: a 50 MHz clock feeds the clock divider; KEY0 resets the divider and core logic; SW0 selects speed and SW1 selects maintenance mode; the decoder drives the LEDs and seven-segment display." width="1672" height="941" loading="lazy" decoding="async" style="display: block; width: 100%; height: auto; background: #fff; border-radius: 0.375rem">
  <figcaption class="text-muted small" style="margin-top: 0.85rem; line-height: 1.6">System architecture showing clock generation, control logic, decoding, and display interfaces.</figcaption>
</figure>

<div role="region" aria-labelledby="fpga-modules-caption" tabindex="0" style="margin-top: 1.75rem; overflow-x: auto; -webkit-overflow-scrolling: touch">
  <table class="table table-sm" style="width: 100%; min-width: 0; margin: 0; color: inherit">
    <caption id="fpga-modules-caption" class="text-muted small" style="caption-side: bottom; padding-top: 0.85rem; line-height: 1.6">Functional modules and interfaces.</caption>
    <thead>
      <tr><th scope="col" style="text-align: left">Module</th><th scope="col" style="text-align: left">Function</th></tr>
    </thead>
    <tbody>
      <tr><th scope="row" style="text-align: left">Clock Divider</th><td>Convert the board clock into timing signals for the system.</td></tr>
      <tr><th scope="row" style="text-align: left">Core Logic &amp; Counter</th><td>Manage traffic-light states, the countdown, and mode transitions.</td></tr>
      <tr><th scope="row" style="text-align: left">Decoder</th><td>Translate control states into LED and display signals.</td></tr>
      <tr><th scope="row" style="text-align: left">Seven-Segment Display</th><td>Show the count on two seven-segment digits.</td></tr>
      <tr><th scope="row" style="text-align: left">Input Controls</th><td>Use KEY0 for reset, SW0 for speed selection, and SW1 for maintenance control.</td></tr>
    </tbody>
  </table>
</div>

</section>

<section aria-labelledby="fpga-work" style="margin-top: 3.5rem">
<h2 id="fpga-work" style="font-size: 1.5rem; margin-bottom: 1.25rem">02 · My Work</h2>

<ul>
  <li><strong>Module development:</strong> I implement functional modules in a hardware description language and define their inputs, outputs, and control signals.</li>
  <li><strong>Module integration:</strong> I connect modules through predefined ports in Quartus, organizing signal paths for clocking, reset, counting, and display.</li>
  <li><strong>Logic simulation and analysis:</strong> I inspect counter updates, state transitions, and output responses in simulation waveforms to check timing relationships between modules.</li>
  <li><strong>Hardware testing:</strong> I deploy the design to the FPGA and verify its functions using the board's switches, push buttons, LEDs, and seven-segment displays.</li>
</ul>

<!-- Reserved: a Quartus top-level design or HDL screenshot, once supplied. No empty placeholder is rendered. -->
<template id="fpga-integration-image-slot">
  <figure style="margin: 1.75rem 0 0">
    <!-- Insert the supplied Quartus or HDL screenshot here. -->
    <figcaption class="text-muted small" style="margin-top: 0.85rem; line-height: 1.6">Hierarchical module integration and signal connections in Quartus.</figcaption>
  </figure>
</template>

</section>

<section aria-labelledby="fpga-control" style="margin-top: 3.5rem">
<h2 id="fpga-control" style="font-size: 1.5rem; margin-bottom: 1.25rem">03 · Control Logic</h2>

<p>The controller cycles through red, amber, green, and amber while updating the countdown display. The speed switch changes the interval between counter updates, the maintenance switch holds the system in maintenance mode, and the reset button restores the initial state.</p>

<figure style="margin: 1.75rem 0">
  <button type="button" aria-label="Enlarge the traffic-light control flow diagram" aria-haspopup="dialog" aria-controls="fpga-flow-dialog" onclick="const dialog = document.getElementById('fpga-flow-dialog'); dialog.showModal(); const view = dialog.querySelector('[role=region]'); view.scrollLeft = (view.scrollWidth - view.clientWidth) / 2;" style="display: block; width: 100%; padding: 1rem; border: 0; border-radius: 0.375rem; background: #fff; cursor: zoom-in">
    <img src="{{ '/assets/img/fpga-traffic-light/control-flow.png' | relative_url }}" alt="Control flow showing reset, normal and accelerated countdown modes, the red–amber–green–amber cycle, and maintenance mode with a 00 display and all three light outputs on." width="962" height="1000" loading="lazy" decoding="async" style="display: block; width: 100%; height: auto">
  </button>
  <figcaption class="text-muted small" style="margin-top: 0.85rem; line-height: 1.6">Control flow covering the traffic-light cycle, speed selection, maintenance mode, and reset. Click the diagram to enlarge it.</figcaption>
</figure>

<div role="region" aria-labelledby="fpga-behaviour-caption" tabindex="0" style="margin-top: 1.75rem; overflow-x: auto; -webkit-overflow-scrolling: touch">
  <table class="table table-sm" style="width: 100%; min-width: 0; margin: 0; color: inherit">
    <caption id="fpga-behaviour-caption" class="text-muted small" style="caption-side: bottom; padding-top: 0.85rem; line-height: 1.6">Control modes and timing. Accelerated mode shortens the elapsed duration of each phase.</caption>
    <thead>
      <tr><th scope="col" style="text-align: left">Function</th><th scope="col" style="text-align: left">Behaviour</th></tr>
    </thead>
    <tbody>
      <tr><th scope="row" style="text-align: left">Normal cycle</th><td>Red: 10 counts → amber: 3 counts → green: 10 counts → amber: 3 counts.</td></tr>
      <tr><th scope="row" style="text-align: left">Normal speed</th><td>Update the count every 1 second.</td></tr>
      <tr><th scope="row" style="text-align: left">Accelerated mode</th><td>Update the count every 0.5 seconds.</td></tr>
      <tr><th scope="row" style="text-align: left">Maintenance mode</th><td>Hold the display at 00 with all three light outputs continuously on.</td></tr>
      <tr><th scope="row" style="text-align: left">Reset</th><td>Restore the functional modules to their initial states.</td></tr>
    </tbody>
  </table>
</div>

</section>

<section aria-labelledby="fpga-video" style="margin-top: 3.5rem">
<h2 id="fpga-video" style="font-size: 1.5rem; margin-bottom: 1.25rem">04 · Video Demonstration</h2>

<p>The hardware demonstration shows the traffic-light cycle and countdown display, along with speed selection, maintenance control, and reset operations using the board's switches and push buttons.</p>

<figure style="margin: 1.75rem 0 0">
  <video id="fpga-demo-video" controls playsinline preload="metadata" poster="{{ '/assets/img/fpga-traffic-light/board-running.jpg' | relative_url }}" aria-label="Hardware demonstration of the FPGA traffic-light control system" style="display: block; width: 100%; aspect-ratio: 16 / 9; object-fit: contain; background: #000; border-radius: 0.375rem">
    <source src="{{ '/assets/video/fpga-traffic-light.mp4' | relative_url }}" type="video/mp4">
    Your browser does not support embedded video. <a href="{{ '/assets/video/fpga-traffic-light.mp4' | relative_url }}">Open the FPGA demonstration video.</a>
  </video>
  <figcaption class="text-muted small" style="margin-top: 0.85rem; line-height: 1.6">Hardware demonstration of the FPGA-based traffic light control system.</figcaption>
</figure>

</section>

<section aria-labelledby="fpga-skills" style="margin-top: 3.5rem">
<h2 id="fpga-skills" style="font-size: 1.5rem; margin-bottom: 1.25rem">Skills</h2>

<p>Hierarchical Digital Design · HDL Development · Quartus · Module Integration · Waveform Analysis · FPGA Hardware Testing</p>

</section>

</article>

<dialog id="fpga-flow-dialog" aria-label="Full-size traffic-light control flow diagram" style="width: min(96vw, 1100px); max-width: 96vw; max-height: 90vh; box-sizing: border-box; padding: 1rem; border: 1px solid #ddd; border-radius: 0.375rem; background: #fff; color: #111">
  <form method="dialog" style="position: sticky; top: 0; margin: 0 0 1rem; text-align: right; background: #fff">
    <button type="submit" autofocus style="padding: 0.4rem 0.85rem; border: 1px solid #999; border-radius: 0.25rem; background: #fff; color: #111; font: inherit; cursor: pointer">Close</button>
  </form>
  <div tabindex="0" role="region" aria-label="Full-size diagram; scroll to explore on smaller screens" style="overflow: auto">
    <img src="{{ '/assets/img/fpga-traffic-light/control-flow.png' | relative_url }}" alt="Full-size traffic-light control flow diagram." width="962" height="1000" loading="lazy" style="display: block; width: 100%; min-width: 962px; height: auto; background: #fff">
  </div>
</dialog>

</div>
