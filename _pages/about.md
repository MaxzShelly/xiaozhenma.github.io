---
layout: default
title: About
permalink: /
subtitle: Multi-View Geometric Methods · Multimodal Perception · Spatial Reasoning · 3D Spatial Understanding
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

{% capture about_body %}

<style id="about-page-style">
  /* About-only visual system. No shared theme or other page is changed. */
  .post:has(#about-page-style) {
    --about-ink: #1d1d1f;
    --about-body: #424245;
    --about-muted: #626269;
    --about-surface: #f5f5f7;
    --about-line: #e5e5ea;
    --about-accent: #b509ac;
    font-family: Roboto, sans-serif;
    font-size: 17px;
    font-weight: 400;
    line-height: 1.75;
    color: var(--about-body);
    padding: 16px 0 32px;
  }
  html[data-theme="dark"] .post:has(#about-page-style) {
    --about-ink: #f5f5f7;
    --about-body: #d2d2d7;
    --about-muted: #b0b0b8;
    --about-surface: #252527;
    --about-line: #3b3b40;
    --about-accent: #d88ad6;
  }
  .post:has(#about-page-style) :is(h1, h2, h3, h4, p, blockquote, td, th) {
    font-family: inherit;
  }
  .post:has(#about-page-style) > .post-header {
    margin-bottom: 32px;
  }
  .post:has(#about-page-style) .post-title {
    margin: 0 0 12px;
    color: var(--global-text-color);
    font-size: clamp(42px, 5vw, 56px);
    font-weight: 300;
    line-height: 1.2;
    letter-spacing: normal;
  }
  .post:has(#about-page-style) .desc {
    max-width: none;
    margin: 0;
    color: var(--global-text-color);
    font-size: 16px;
    font-weight: 300;
    line-height: 1.5;
  }
  .post:has(#about-page-style) .about-research-heading {
    max-width: none;
    margin: 0 0 16px;
    color: var(--global-text-color);
    font-size: clamp(26px, 3vw, 32px);
    font-weight: 300;
    line-height: 1.2;
    letter-spacing: normal;
    text-wrap: wrap;
  }
  .post:has(#about-page-style) .clearfix > p {
    max-width: 760px;
    margin: 0 0 24px;
    color: var(--about-body);
    font-size: 17px;
    font-weight: 400;
    line-height: 1.8;
  }
  .post:has(#about-page-style) .clearfix > .lead {
    margin-bottom: 36px;
    color: var(--about-muted);
    font-size: 17px;
    font-weight: 500;
    line-height: 1.7;
  }
  .post:has(#about-page-style) .clearfix > h2 {
    margin: 76px 0 28px !important;
    color: var(--about-ink);
    font-size: clamp(27px, 3vw, 34px);
    font-weight: 600;
    line-height: 1.25;
    letter-spacing: -0.03em;
    text-wrap: balance;
  }
  .post:has(#about-page-style) blockquote {
    max-width: 760px;
    margin: 40px 0 0;
    padding: 24px 28px;
    border: 1px solid var(--about-line);
    border-left: 3px solid var(--about-accent);
    border-radius: 0 16px 16px 0;
    background: var(--about-surface);
  }
  .post:has(#about-page-style) blockquote :is(p, strong) {
    margin: 0;
    color: var(--about-ink);
    font-size: 21px;
    font-weight: 500;
    line-height: 1.5;
    letter-spacing: -0.015em;
  }
  .post:has(#about-page-style) .clearfix > .row {
    display: grid;
    gap: 24px;
    margin: 0 !important;
  }
  .post:has(#about-page-style) .row-cols-md-2 {
    grid-template-columns: repeat(2, minmax(0, 1fr));
  }
  .post:has(#about-page-style) .row-cols-md-3 {
    grid-template-columns: repeat(3, minmax(0, 1fr));
  }
  .post:has(#about-page-style) .clearfix > .row > .col {
    width: auto;
    max-width: none;
    min-width: 0;
    padding: 0;
    margin: 0;
  }
  .post:has(#about-page-style) .card {
    height: 100%;
    transform: none !important;
    overflow: hidden;
    border: 1px solid var(--about-line);
    border-radius: 20px;
    background: var(--about-surface);
    box-shadow: none !important;
  }
  .post:has(#about-page-style) .card-body {
    padding: 28px !important;
  }
  .post:has(#about-page-style) .card-title {
    margin: 0 0 16px !important;
    color: var(--about-ink);
    font-size: 21px;
    font-weight: 600;
    line-height: 1.35;
    letter-spacing: -0.025em;
  }
  .post:has(#about-page-style) .card-subtitle {
    margin: 0 0 18px !important;
    color: var(--about-ink);
    font-size: 16px;
    font-weight: 500;
    line-height: 1.5;
    letter-spacing: -0.01em;
  }
  .post:has(#about-page-style) .card-text {
    margin: 0 !important;
    color: var(--about-body);
    font-size: 16px;
    font-weight: 400;
    line-height: 1.7;
  }
  .post:has(#about-page-style) .row-cols-md-3 .card-body {
    padding: 26px 24px !important;
  }
  .post:has(#about-page-style) a {
    color: var(--about-accent);
    text-decoration: none;
    text-underline-offset: 0.2em;
  }
  .post:has(#about-page-style) .card-title a {
    color: var(--about-ink);
    transition: color 160ms ease;
  }
  .post:has(#about-page-style) a:hover {
    color: var(--about-accent);
    text-decoration: underline;
  }
  .post:has(#about-page-style) .card-title a:hover {
    text-decoration: none;
  }
  .post:has(#about-page-style) .row-cols-md-3 .card {
    position: relative;
  }
  .post:has(#about-page-style) .row-cols-md-3 :is(.card-body, .card-title, .card-title a) {
    position: static;
  }
  .post:has(#about-page-style) .row-cols-md-3 .card-title a::after {
    content: "";
    position: absolute;
    inset: 0;
    z-index: 1;
    border-radius: 20px;
    cursor: pointer;
  }
  .post:has(#about-page-style) .row-cols-md-3 .card:has(a:focus-visible) {
    outline: 2px solid var(--about-accent);
    outline-offset: 4px;
  }
  .post:has(#about-page-style) a:focus-visible {
    outline: 2px solid var(--about-accent);
    outline-offset: 4px;
    border-radius: 2px;
  }
  .post:has(#about-page-style) .row-cols-md-3 .card-title a:focus-visible {
    outline: none;
  }
  .post:has(#about-page-style) .clearfix > p.about-projects-link {
    margin: 28px 0 0 !important;
    font-size: 16px;
    font-weight: 500;
  }
  .post:has(#about-page-style) .news .table-responsive {
    max-height: none !important;
  }
  .post:has(#about-page-style) .news table {
    margin: 0;
  }
  .post:has(#about-page-style) .news :is(th, td) {
    padding: 20px 0;
    border-top: 1px solid var(--about-line);
    color: var(--about-body);
    font-size: 16px;
    font-weight: 400;
    line-height: 1.7;
    vertical-align: top;
  }
  .post:has(#about-page-style) .news th {
    padding-right: 24px;
    color: var(--about-muted);
    font-size: 14px;
    font-weight: 500;
    white-space: nowrap;
  }
  .post:has(#about-page-style) .social {
    margin-top: 64px;
    padding-top: 32px;
    border-top: 1px solid var(--about-line);
  }
  .post:has(#about-page-style) .contact-icons {
    font-size: 32px;
    line-height: 1.5;
  }
  .post:has(#about-page-style) .contact-icons a {
    display: inline-block;
    margin: 0 8px;
    color: var(--about-ink);
  }
  .post:has(#about-page-style) .contact-icons a:hover {
    color: var(--about-accent);
  }
  .post:has(#about-page-style) .contact-note {
    max-width: 760px;
    margin: 20px auto 0;
    color: var(--about-muted);
    font-size: 14px;
    font-weight: 400;
    line-height: 1.7;
  }
  @media (max-width: 899px) {
    .post:has(#about-page-style) .row-cols-md-3 {
      grid-template-columns: 1fr;
    }
  }
  @media (max-width: 575px) {
    .post:has(#about-page-style) {
      padding-top: 0;
    }
    .post:has(#about-page-style) .clearfix > h2 {
      margin-top: 56px !important;
      margin-bottom: 22px !important;
    }
    .post:has(#about-page-style) .row-cols-md-2 {
      grid-template-columns: 1fr;
    }
    .post:has(#about-page-style) .clearfix > .row {
      gap: 20px;
    }
    .post:has(#about-page-style) .card-body {
      padding: 24px !important;
    }
    .post:has(#about-page-style) blockquote {
      padding: 22px;
    }
    .post:has(#about-page-style) blockquote :is(p, strong) {
      font-size: 19px;
    }
    .post:has(#about-page-style) .news th {
      padding-right: 16px;
      font-size: 13px;
    }
    .post:has(#about-page-style) .news td {
      font-size: 15px;
    }
  }
  @media (prefers-reduced-motion: reduce) {
    .post:has(#about-page-style) .card-title a {
      transition: none;
    }
  }
</style>

<p class="lead">Undergraduate Student in Electronic and Electrical Engineering<br>Southwest Jiaotong University × University of Leeds</p>

I am currently enrolled in the joint undergraduate programme in Electronic and Electrical Engineering at Southwest Jiaotong University and the University of Leeds. My research interests focus on 3D spatial understanding: how to enable large models to understand geometric shapes, object structures, and spatial relationships in the physical world.

I am interested in combining multi-view geometric methods, multi-view and multisensor observations, and semantic information from AI. I hope to connect the information models recognise in images and language with measurable spatial properties of real 3D objects and scenes.

My research experience includes SLAM, sparse point-cloud completion, dense scene reconstruction, intelligent CAD, and learning models for autonomous driving. These experiences have given me a foundation in 3D data acquisition, geometric reconstruction, and structured representations of physical objects. They have also prompted me to consider how models can progress from recognising objects and recovering shapes to understanding object structures and spatial relationships.

Building on this foundation, I hope to explore how large models can use 3D representations and geometric tools for spatial reasoning and 3D spatial understanding, with applications in robotics, autonomous driving, and computer-aided design.

> **How can large models connect what they see and describe with the 3D geometry of the real world?**

## Research Interests

<div class="row row-cols-1 row-cols-md-2">
  <div class="col"><div class="card h-100"><div class="card-body"><h4 class="card-title">3D Reconstruction and Representation</h4><p class="card-text small mb-0">Combining images, point clouds, and multisensor observations to reconstruct objects and scenes and represent their geometric shapes, boundaries, and structures.</p></div></div></div>
  <div class="col"><div class="card h-100"><div class="card-body"><h4 class="card-title">Spatial Understanding Supported by Multi-View Geometry and End-to-End Integration</h4><p class="card-text small mb-0">Combining multi-view geometric measurements, classification and recognition, and world knowledge acquired through machine learning and large AI models to understand object dimensions, positions, orientations, and relationships.</p></div></div></div>
  <div class="col"><div class="card h-100"><div class="card-body"><h4 class="card-title">3D Spatial Reasoning with Large Models</h4><p class="card-text small mb-0">Exploring how large language and multimodal models can use structured 3D information to answer spatial questions and reason about relationships between objects and scenes.</p></div></div></div>
  <div class="col"><div class="card h-100"><div class="card-body"><h4 class="card-title">Spatial Agents and Applications</h4><p class="card-text small mb-0">Exploring agents that connect perception models, geometric tools, and structured representations to support scene analysis, CAD modelling, and robotic applications.</p></div></div></div>
</div>

<h2 class="about-selected-heading">Selected Research</h2>

<div class="row row-cols-1 row-cols-md-3">
  <div class="col"><div class="card h-100 hoverable"><div class="card-body"><h3 class="card-title"><a href="{{ '/projects/sparse-train-reconstruction/' | relative_url }}">Sparse 3D Reconstruction</a></h3><h4 class="card-subtitle">High-Speed Train Point Cloud Completion and Surface Reconstruction</h4><p class="card-text">Reconstructing complex train-nose geometry from incomplete LiDAR observations through multi-view projection, missing-region modelling, and three-dimensional reverse projection. The project focuses on recovering missing glass-window regions and supporting surface reconstruction from sparse point clouds.</p></div></div></div>
  <div class="col"><div class="card h-100 hoverable"><div class="card-body"><h3 class="card-title"><a href="{{ '/projects/monocular-depth-railway/' | relative_url }}">Learning + Geometry</a></h3><h4 class="card-subtitle">Pixel-Level 3D Reconstruction and Object Extraction</h4><p class="card-text">Combining dense monocular depth with sparse LiDAR measurements and semantic boundary constraints for transportation-scene reconstruction. The project explores pixel-level geometry recovery and physical object extraction, connecting learned depth estimation with geometric information from measured point clouds.</p></div></div></div>
  <div class="col"><div class="card h-100 hoverable"><div class="card-body"><h3 class="card-title"><a href="{{ '/projects/intelligent-cad/' | relative_url }}">Spatial Intelligence</a></h3><h4 class="card-subtitle">Intelligent CAD and Editable Reconstruction</h4><p class="card-text">Exploring geometric understanding and editable CAD reconstruction through point-cloud segmentation, parametric program generation, and execution-based verification. The project investigates how candidate generation and explicit geometric validation improve reconstruction quality, with ongoing work towards a CAD agent that coordinates modelling and verification tools.</p></div></div></div>
</div>

<p class="about-projects-link"><a href="{{ '/projects/' | relative_url }}">View all projects →</a></p>

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
{% endcapture %}

<div class="post">
  <header class="post-header">
    <h1 class="post-title">Xiaozhen Ma</h1>
    <h2 class="about-research-heading">3D Spatial Understanding</h2>
    <p class="desc">{{ page.subtitle }}</p>
  </header>
  <article>
    <div class="clearfix">{{ about_body | markdownify }}</div>
    {% if page.social %}
      <div class="social">
        <div class="contact-icons">{% social_links %}</div>
        <div class="contact-note">{{ site.contact_note }}</div>
      </div>
    {% endif %}
  </article>
</div>
