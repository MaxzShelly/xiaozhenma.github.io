---
layout: default
title: Embedded Systems
paper_title: Fisherman Day
description: Sensors, microcontrollers, control logic, and physical system behaviour.
importance: 1
category: Engineering
permalink: /projects/embedded-systems/
---

<div class="post" id="fisherman-day-project" lang="en" style="font-family: Roboto, sans-serif; font-size: 1rem; font-weight: 300">

<header class="post-header" style="margin-bottom: 2.75rem">
  <h1 class="post-title" style="font-size: clamp(1.5rem, 2.4vw, 2rem); line-height: 1.4; margin: 0">{{ page.paper_title }}</h1>
  <p class="text-muted" style="margin: 1rem 0 1.5rem; line-height: 1.6">STM32-Based Embedded Game Development</p>
  <div class="project-metadata" style="margin-top: 1.5rem; font-size: 1rem; font-weight: 300; line-height: 1.75">
    <p style="margin: 0">Xiaozhen Ma</p>
    <p class="text-muted small" style="margin: 0.25rem 0 0">April–June 2026</p>
    <p class="text-muted small" style="margin: 0.25rem 0 0">STM32 · Embedded C · State Machines · Peripheral Integration</p>
  </div>
</header>

<article style="line-height: 1.75">

<section aria-labelledby="fisherman-overview">
<h2 id="fisherman-overview" style="font-size: 1.5rem; margin-bottom: 1.25rem">Overview</h2>

<p>Fisherman Day is an interactive STM32-based embedded game developed by a three-person team. Its Fishing, Cooking, and Selling stages form a complete gameplay sequence from catching fish to preparing and selling dishes. The system combines LCD graphics, physical controls, and audio and visual feedback, integrating game logic and hardware peripherals on a single platform.</p>

<p>My main responsibility is the design and implementation of Game 2: Cooking, including fish-chopping interactions, heat adjustment, timing, and outcome evaluation. I also contribute to peripheral testing, stage integration, GitHub code management, and system testing.</p>

</section>

<section aria-labelledby="fisherman-system" style="margin-top: 3.5rem">
<h2 id="fisherman-system" style="font-size: 1.5rem; margin-bottom: 1.25rem">System Overview</h2>

<figure style="margin: 0">
  <img src="{{ '/assets/img/fisherman-day/system-overview.jpg' | relative_url }}" alt="Fisherman Day system diagram showing the main menu, Fishing, Cooking, and Selling stages, with STM32 inputs, game-state logic, LCD output, RGB LEDs, and buzzer feedback." width="1536" height="1024" loading="lazy" decoding="async" style="display: block; width: 100%; height: auto; border-radius: 0.375rem">
  <figcaption class="text-muted small" style="margin-top: 0.85rem; line-height: 1.6">The complete game consists of Fishing, Cooking, and Selling. My primary responsibility is the middle Cooking stage, alongside contributions to overall system integration.</figcaption>
</figure>

</section>

<section aria-labelledby="fisherman-cooking" style="margin-top: 3.5rem">
<h2 id="fisherman-cooking" style="font-size: 1.5rem; margin-bottom: 1.25rem">Game 2: Cooking Stage</h2>

<p>The Cooking stage connects ingredient preparation, heat control, and dish presentation into a continuous interaction. Players chop fish using a button, adjust the heat with a potentiometer, control cooking time according to the requirements of each fish type, and view the final outcome.</p>

<div role="region" aria-labelledby="fisherman-gameplay-caption" tabindex="0" style="margin-top: 1.75rem; overflow-x: auto; -webkit-overflow-scrolling: touch">
  <table id="fisherman-gameplay-table" class="table table-sm" style="width: 100%; min-width: 0; margin: 0; color: inherit">
    <caption id="fisherman-gameplay-caption" class="text-muted small" style="caption-side: bottom; padding-top: 0.85rem; line-height: 1.6">Cooking-stage interactions and system feedback.</caption>
    <thead>
      <tr><th scope="col" style="text-align: left">Stage</th><th scope="col" style="text-align: left">Player action</th><th scope="col" style="text-align: left">System feedback</th></tr>
    </thead>
    <tbody>
      <tr><th scope="row" style="text-align: left">Ingredient preparation</th><td style="text-align: left">Press the button to chop each fish type in sequence.</td><td style="text-align: left">Display chopping progress and the current state.</td></tr>
      <tr><th scope="row" style="text-align: left">Cooking control</th><td style="text-align: left">Turn the potentiometer to adjust the heat.</td><td style="text-align: left">Update the heat-level display and timing information.</td></tr>
      <tr><th scope="row" style="text-align: left">Outcome evaluation</th><td style="text-align: left">Complete cooking according to heat and timing requirements.</td><td style="text-align: left">Display the result and provide RGB LED and buzzer feedback.</td></tr>
      <tr><th scope="row" style="text-align: left">Dish presentation</th><td style="text-align: left">View the prepared dish.</td><td style="text-align: left">Show the corresponding dish, such as Fish &amp; Chips, Cod Burger, or Cod Soup.</td></tr>
    </tbody>
  </table>
</div>

</section>

<section aria-labelledby="fisherman-contributions" style="margin-top: 3.5rem">
<h2 id="fisherman-contributions" style="font-size: 1.5rem; margin-bottom: 1.25rem">My Contributions</h2>

<ul>
  <li><strong>Complete stage development:</strong> I implement the main Game 2 functionality, organizing chopping, cooking, dish presentation, and the result summary into a complete gameplay sequence.</li>
  <li><strong>Hardware interaction and feedback:</strong> I connect button actions, potentiometer input, LCD animations, RGB LEDs, and buzzer feedback to game states, creating an interactive system with visible and audible responses.</li>
  <li><strong>State management and system integration:</strong> I organize stage transitions and timing logic, synchronize inputs, display updates, and peripheral feedback, and coordinate interfaces and integration tests with the team's other game modules.</li>
  <li><strong>Collaborative development and validation:</strong> I use GitHub for code management, document development progress, and participate in system testing and the final demonstration to check gameplay flow and software–hardware coordination.</li>
</ul>

</section>

<section aria-labelledby="fisherman-video" style="margin-top: 3.5rem">
<h2 id="fisherman-video" style="font-size: 1.5rem; margin-bottom: 1.25rem">Game 2 Video</h2>
<h3 style="font-size: 1.25rem; margin-bottom: 1rem">Cooking Stage: Gameplay and Embedded Interaction</h3>

<figure style="margin: 0">
  <video id="fisherman-cooking-video" controls playsinline preload="metadata" aria-label="Game 2 Cooking stage introduction and demonstration" style="display: block; width: 100%; aspect-ratio: 16 / 9; background: #000; border-radius: 0.375rem">
    <source src="{{ '/assets/video/fisherman-day-cooking.mp4' | relative_url }}" type="video/mp4">
    Your browser does not support embedded video. <a href="{{ '/assets/video/fisherman-day-cooking.mp4' | relative_url }}">Open the Cooking demonstration video.</a>
  </video>
  <figcaption class="text-muted small" style="margin-top: 0.85rem; line-height: 1.6">Introduction and demonstration of the Cooking module, my primary contribution to Fisherman Day.</figcaption>
</figure>

</section>

<section aria-labelledby="fisherman-results" style="margin-top: 3.5rem">
<h2 id="fisherman-results" style="font-size: 1.5rem; margin-bottom: 1.25rem">Results</h2>

<p>The Cooking stage runs and can be demonstrated on STM32 hardware. Integration with the team's Fishing and Selling modules produces the complete three-stage game.</p>

<div role="region" aria-labelledby="fisherman-results-caption" tabindex="0" style="margin-top: 1.75rem; overflow-x: auto; -webkit-overflow-scrolling: touch">
  <table id="fisherman-results-table" class="table table-sm" style="width: 100%; min-width: 0; margin: 0; color: inherit">
    <caption id="fisherman-results-caption" class="text-muted small" style="caption-side: bottom; padding-top: 0.85rem; line-height: 1.6">Completed module, hardware integration, and project deliverables.</caption>
    <thead>
      <tr><th scope="col" style="text-align: left">Outcome</th><th scope="col" style="text-align: left">Completed work</th></tr>
    </thead>
    <tbody>
      <tr><th scope="row" style="text-align: left">Standalone game module</th><td style="text-align: left">Game 2 interaction logic, timing, state transitions, and result presentation.</td></tr>
      <tr><th scope="row" style="text-align: left">Peripheral coordination</th><td style="text-align: left">Integration of buttons, a potentiometer, an LCD, RGB LEDs, and a buzzer.</td></tr>
      <tr><th scope="row" style="text-align: left">Team system integration</th><td style="text-align: left">Connection of the Cooking module to the three-stage gameplay sequence.</td></tr>
      <tr><th scope="row" style="text-align: left">Project delivery</th><td style="text-align: left">Code management, development records, system testing, demonstration, and a Game 2 introduction video.</td></tr>
    </tbody>
  </table>
</div>

</section>

<section aria-labelledby="fisherman-skills" style="margin-top: 3.5rem">
<h2 id="fisherman-skills" style="font-size: 1.5rem; margin-bottom: 1.25rem">Skills</h2>

<p>STM32 · Embedded C · State Machines · Peripheral Integration · LCD Graphics · Hardware Debugging · GitHub Collaboration</p>

</section>

</article>

</div>
