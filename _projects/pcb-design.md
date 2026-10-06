---
layout: default
title: PCB Design
description: From schematic and layout to measurement and debugging.
importance: 3
category: Engineering
permalink: /projects/pcb-design/
---

<div class="post" id="pcb-design-project" lang="en" style="font-family: Roboto, sans-serif; font-size: 1rem; font-weight: 300">

<header class="post-header" style="margin-bottom: 2.75rem">
  <h1 class="post-title" style="font-size: clamp(1.5rem, 2.4vw, 2rem); line-height: 1.4; margin: 0">PCB Design</h1>
  <p class="text-muted" style="margin: 1rem 0 1.5rem; line-height: 1.6">Audio-Visualisation PCB Design and Fabrication</p>
  <div class="project-metadata" style="margin-top: 1.5rem; font-size: 1rem; font-weight: 300; line-height: 1.75">
    <p style="margin: 0">Xiaozhen Ma</p>
    <p class="text-muted small" style="margin: 0.25rem 0 0">KiCad · Analogue Circuits · PCB Layout · Soldering &amp; Testing</p>
  </div>
</header>

<article style="line-height: 1.75">

<section aria-labelledby="pcb-overview">
<h2 id="pcb-overview" style="font-size: 1.5rem; margin-bottom: 1.25rem">Overview</h2>

<p>This project develops an audio-visualisation circuit from KiCad schematic capture and PCB layout to component soldering and hardware testing. Low-pass, band-pass, and high-pass filter branches process the audio signal and drive red, green, and blue LEDs, respectively, making the responses of different frequency bands visible.</p>

<p>My work covers schematic and PCB design, component assembly and soldering, electrical measurements, and troubleshooting, taking the circuit from a design to a testable hardware board.</p>

</section>

<section aria-labelledby="pcb-schematic" style="margin-top: 3.5rem">
<h2 id="pcb-schematic" style="font-size: 1.5rem; margin-bottom: 1.25rem">01 · Circuit Schematic</h2>

<p>The complete KiCad schematic brings together the power supply, adjustable-gain amplifier, three filter branches, and LED drivers. Test points provide access to key circuit nodes for PCB development and hardware debugging.</p>

<div role="region" aria-labelledby="pcb-circuit-caption" tabindex="0" style="margin: 1.75rem 0; overflow-x: auto; -webkit-overflow-scrolling: touch">
  <table class="table table-sm" style="width: 100%; min-width: 0; margin: 0; color: inherit">
    <caption id="pcb-circuit-caption" class="text-muted small" style="caption-side: bottom; padding-top: 0.85rem; line-height: 1.6">Circuit modules and their functions.</caption>
    <thead>
      <tr><th scope="col" style="text-align: left">Circuit module</th><th scope="col" style="text-align: left">Function</th></tr>
    </thead>
    <tbody>
      <tr><th scope="row" style="text-align: left">Power supply</th><td>Rectify and filter the input to provide ±12 V supply rails.</td></tr>
      <tr><th scope="row" style="text-align: left">Adjustable-gain amplifier</th><td>Adjust the amplitude of the input audio signal.</td></tr>
      <tr><th scope="row" style="text-align: left">Low-pass filter</th><td>Extract low-frequency components to drive the red LED.</td></tr>
      <tr><th scope="row" style="text-align: left">Band-pass filter</th><td>Extract mid-frequency components to drive the green LED.</td></tr>
      <tr><th scope="row" style="text-align: left">High-pass filter</th><td>Extract high-frequency components to drive the blue LED.</td></tr>
      <tr><th scope="row" style="text-align: left">Test points</th><td>Provide measurement access to power, signal, and LED-driver nodes.</td></tr>
    </tbody>
  </table>
</div>

<figure style="margin: 0">
  <a href="{{ '/assets/img/pcb-design/circuit-schematic.png' | relative_url }}" target="_blank" rel="noopener" aria-label="Open the full-resolution circuit schematic in a new tab" style="display: block; cursor: zoom-in">
    <img src="{{ '/assets/img/pcb-design/circuit-schematic.png' | relative_url }}" alt="Complete KiCad schematic showing the ±12 V supply, adjustable-gain amplifier, low-pass, band-pass, and high-pass filters, LED drivers, and test points." width="1750" height="1240" loading="lazy" decoding="async" style="display: block; width: 100%; height: auto; border-radius: 0.375rem">
  </a>
  <figcaption class="text-muted small" style="margin-top: 0.85rem; line-height: 1.6">Audio-visualisation circuit schematic designed in KiCad. Click the schematic to view the full-resolution image.</figcaption>
</figure>

</section>

<section aria-labelledby="pcb-layout" style="margin-top: 3.5rem">
<h2 id="pcb-layout" style="font-size: 1.5rem; margin-bottom: 1.25rem">02 · PCB Layout</h2>

<p>Component placement and routing translate the schematic into a board layout, arranging the power connectors, audio input, filter branches, and LED outputs. Test points and silkscreen labels support assembly, node identification, and subsequent measurements.</p>

<figure style="max-width: 45rem; margin: 1.75rem auto 0">
  <img src="{{ '/assets/img/pcb-design/pcb-layout.png' | relative_url }}" alt="KiCad PCB layout showing component footprints, routed connections, power and audio connectors, and labelled test points." width="1306" height="1049" loading="lazy" decoding="async" style="display: block; width: 100%; height: auto; border-radius: 0.375rem">
  <figcaption class="text-muted small" style="margin-top: 0.85rem; line-height: 1.6">Component placement and routing of the audio-visualisation PCB.</figcaption>
</figure>

<!-- Reserved: a responsive two-column figure for separate top and bottom PCB views, once supplied. -->
<template id="pcb-layer-views-slot">
  <figure style="margin: 2rem 0 0">
    <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(min(100%, 18rem), 1fr)); gap: 1.5rem">
      <!-- Insert the supplied top-layer image here. -->
      <!-- Insert the supplied bottom-layer image here. -->
    </div>
    <figcaption class="text-muted small" style="margin-top: 0.85rem; line-height: 1.6">Top and bottom views of the PCB design.</figcaption>
  </figure>
</template>

<figure style="margin: 2rem 0 0">
  <img src="{{ '/assets/img/pcb-design/pcb-3d-preview.png' | relative_url }}" alt="KiCad 3D Viewer preview of the populated audio-visualisation board, showing components, connectors, and LED outputs." width="3600" height="1841" loading="lazy" decoding="async" style="display: block; width: 100%; height: auto; border-radius: 0.375rem">
  <figcaption class="text-muted small" style="margin-top: 0.85rem; line-height: 1.6">Board assembly preview in KiCad 3D Viewer.</figcaption>
</figure>

</section>

<section aria-labelledby="pcb-assembly" style="margin-top: 3.5rem">
<h2 id="pcb-assembly" style="font-size: 1.5rem; margin-bottom: 1.25rem">03 · Fabrication &amp; Assembly</h2>

<p>I assemble and solder the operational amplifiers, resistors, capacitors, diodes, transistors, LEDs, and terminal connectors onto the PCB. Component references and the schematic guide checks of orientation and connectivity before powered measurements and debugging.</p>

<figure style="max-width: 28rem; margin: 1.75rem auto 0">
  <img src="{{ '/assets/img/pcb-design/assembled-board.jpg' | relative_url }}" alt="Assembled blue audio-visualisation PCB with red, green, and blue LEDs, soldered components, test points, and terminal connectors." width="2820" height="3992" loading="lazy" decoding="async" style="display: block; width: 100%; height: auto; border-radius: 0.375rem">
  <figcaption class="text-muted small" style="margin-top: 0.85rem; line-height: 1.6">Assembled audio-visualisation PCB with three LED output channels.</figcaption>
</figure>

<!-- Reserved: a rear-board or solder-joint detail photograph, once supplied. No empty placeholder is rendered. -->

</section>

<section aria-labelledby="pcb-results" style="margin-top: 3.5rem">
<h2 id="pcb-results" style="font-size: 1.5rem; margin-bottom: 1.25rem">Results</h2>

<ul>
  <li>Complete KiCad schematic capture, component placement, and routing for the audio-visualisation circuit.</li>
  <li>Assembled and soldered hardware with low-, mid-, and high-frequency LED output branches.</li>
  <li>Multimeter-based measurements and troubleshooting, with practical experience in circuit design, PCB implementation, and hardware debugging.</li>
</ul>

<figure style="margin: 1.75rem 0 0">
  <video id="pcb-demo-video" controls autoplay muted loop playsinline preload="metadata" aria-label="Silent looping demonstration of audio input and PCB LED responses" style="display: block; width: 100%; max-height: 38rem; aspect-ratio: 1366 / 904; object-fit: contain; background: #000; border-radius: 0.375rem">
    <source src="{{ '/assets/video/pcb-audio-visualisation.mp4' | relative_url }}" type="video/mp4">
    Your browser does not support embedded video. <a href="{{ '/assets/video/pcb-audio-visualisation.mp4' | relative_url }}">Open the LED response demonstration.</a>
  </video>
  <figcaption class="text-muted small" style="margin-top: 0.85rem; line-height: 1.6">Audio input and LED response demonstration.</figcaption>
</figure>

</section>

<section aria-labelledby="pcb-skills" style="margin-top: 3.5rem">
<h2 id="pcb-skills" style="font-size: 1.5rem; margin-bottom: 1.25rem">Skills</h2>

<p>KiCad · Schematic Capture · PCB Layout &amp; Routing · Analogue Filtering · Component Soldering · Multimeter Measurement · Hardware Troubleshooting</p>

</section>

</article>
</div>
