---
layout: about
title: About
permalink: /
subtitle: 3D Perception · Spatial Intelligence · Geometric Learning
nav: true
nav_order: 1

selected_papers: false
social: true # includes social icons at the bottom of the page

announcements:
  enabled: false # News is rendered below with About-only corrections; shared news pages remain unchanged.
  scrollable: true # adds a vertical scroll bar if there are more than 3 news items
  limit: 5 # leave blank to include all the news in the `_news` folder

latest_posts:
  enabled: false
  scrollable: true # adds a vertical scroll bar if there are more than 3 new posts items
  limit: 3 # leave blank to include all the blog posts
---

<h1>Xiaozhen Ma</h1>

<p class="lead">Undergraduate Student in Electronic and Electrical Engineering<br>Southwest Jiaotong University × University of Leeds</p>

I am an undergraduate student in Electronic and Electrical Engineering at Southwest Jiaotong University and the University of Leeds.

My research focuses on how intelligent systems perceive, reconstruct, and reason about the 3D world, particularly under sparse, incomplete, or uncertain observations.

My work spans sparse point-cloud reconstruction, monocular depth estimation, multimodal perception, intelligent CAD, and autonomous-driving perception. Across these projects, I have repeatedly encountered the same question: how can a model distinguish between a result that merely looks plausible and one that is geometrically reliable?

I am particularly interested in combining learned semantic and structural priors with explicit geometry, real-world sensor observations, and validation mechanisms to build more reliable 3D representations.

> **How can machines build reliable 3D understanding when what they see is incomplete?**

## Research Interests

<div class="row row-cols-1 row-cols-md-2 g-5 mb-5">
  <div class="col"><div class="card h-100"><div class="card-body p-3"><h4 class="card-title mb-2">3D Perception</h4><p class="card-text small mb-0">Reliable 3D representation from images, depth, point clouds, and multimodal sensor observations, especially under sparse, occluded, or incomplete conditions.</p></div></div></div>
  <div class="col"><div class="card h-100"><div class="card-body p-3"><h4 class="card-title mb-2">Spatial Intelligence</h4><p class="card-text small mb-0">Understanding distance, orientation, visibility, connectivity, containment, contact, and topology rather than relying only on visual similarity.</p></div></div></div>
  <div class="col"><div class="card h-100" style="transform: translateY(0.5cm)"><div class="card-body p-3"><h4 class="card-title mb-2">Geometry-Aware Learning</h4><p class="card-text small mb-0">Combining learned semantic and structural priors with explicit geometry, sensor measurements, topology, and deterministic constraints.</p></div></div></div>
  <div class="col"><div class="card h-100" style="transform: translateY(0.5cm)"><div class="card-body p-3"><h4 class="card-title mb-2">Robotic Perception</h4><p class="card-text small mb-0">Connecting reliable spatial understanding with downstream reasoning, planning, and action in robotic and autonomous systems.</p></div></div></div>
</div>

<h2 class="mt-5">Selected Research</h2>

<div class="row row-cols-1 row-cols-md-3 g-4" style="row-gap: 1.5rem">
  <div class="col"><div class="card h-100 hoverable"><div class="card-body"><h3 class="card-title"><a href="{{ '/projects/sparse-train-reconstruction/' | relative_url }}">Sparse 3D Reconstruction</a></h3><h4 class="card-subtitle mb-3">High-Speed Train Point Cloud Completion and Surface Reconstruction</h4><p class="card-text">Reconstructing complex train-nose geometry from incomplete LiDAR observations through multi-view projection, missing-region modelling, and three-dimensional reverse projection. The project focuses on recovering missing glass-window regions and supporting surface reconstruction from sparse point clouds.</p></div></div></div>
  <div class="col"><div class="card h-100 hoverable"><div class="card-body"><h3 class="card-title"><a href="{{ '/projects/monocular-depth-railway/' | relative_url }}">Learning + Geometry</a></h3><h4 class="card-subtitle mb-3">Pixel-Level 3D Reconstruction and Object Extraction</h4><p class="card-text">Combining dense monocular depth with sparse LiDAR measurements and semantic boundary constraints for transportation-scene reconstruction. The project explores pixel-level geometry recovery and physical object extraction, connecting learned depth estimation with geometric information from measured point clouds.</p></div></div></div>
  <div class="col"><div class="card h-100 hoverable"><div class="card-body"><h3 class="card-title"><a href="{{ '/projects/intelligent-cad/' | relative_url }}">Spatial Intelligence</a></h3><h4 class="card-subtitle mb-3">Intelligent CAD and Editable Reconstruction</h4><p class="card-text">Exploring geometric understanding and editable CAD reconstruction through point-cloud segmentation, parametric program generation, and execution-based verification. The project investigates how candidate generation and explicit geometric validation improve reconstruction quality, with ongoing work towards a CAD agent that coordinates modelling and verification tools.</p></div></div></div>
</div>

<p class="mt-4"><a href="{{ '/projects/' | relative_url }}">View all projects →</a></p>

## Leadership and International Collaboration

Outside research, I serve as President of the Academic Innovation Base at SWJTU–Leeds Joint School, coordinating research, competition, and academic activities across a 30+ member student organisation. Studying in the SWJTU–Leeds joint programme and conducting research at UC Irvine have strengthened my ability to read, discuss, and present technical work in English across international research environments.

## Contact

I am interested in graduate research opportunities and collaborations related to 3D perception, spatial intelligence, geometric learning, robotic perception, and intelligent autonomous systems. You can reach me at <a href="mailto:shellyma626@163.com">shellyma626@163.com</a>.

<!-- Keep the following news corrections local to About, without changing the shared News collection. -->
<h2><a href="{{ '/news/' | relative_url }}" style="color: inherit">news</a></h2>
<div class="news">
  {% assign about_news = site.news | reverse %}
  {% assign railway_project = site.projects | where: 'permalink', '/projects/monocular-depth-railway/' | first %}
  <div class="table-responsive"{% if page.announcements.scrollable and about_news.size > 3 %} style="max-height: 60vw"{% endif %}>
    <table class="table table-sm table-borderless">
      {% for item in about_news limit: page.announcements.limit %}
        {% assign news_date = item.date %}
        {% assign news_content = item.content %}
        {% case item.path %}
          {% when '_news/2025-01-ai-competition.md' %}
            {% assign news_date = '2025-08-01' %}
          {% when '_news/2026-05-railway-reconstruction.md' %}
            {% capture news_content %}Completed the project “{{ railway_project.paper_title }}.”{% endcapture %}
          {% when '_news/2026-02-cas.md' %}
            {% assign news_content = 'Joined the Institute of Automation, Chinese Academy of Sciences, conducting research in geometric understanding and editable CAD reconstruction.' %}
        {% endcase %}
        <tr>
          <th scope="row" style="width: 20%">{{ news_date | date: '%b %d, %Y' }}</th>
          <td>
            {% if item.inline %}
              {{ news_content | remove: '<p>' | remove: '</p>' | emojify }}
            {% else %}
              <a class="news-title" href="{{ item.url | relative_url }}">{{ item.title }}</a>
            {% endif %}
          </td>
        </tr>
      {% endfor %}
    </table>
  </div>
</div>
