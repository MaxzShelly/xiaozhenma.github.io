---
layout: page
title: Projects
permalink: /projects/
description: Research and engineering projects in perception, geometry, and intelligent systems.
nav: true
nav_order: 3
display_categories: [Research, Engineering]
horizontal: false
---

<!-- pages/projects.md -->
<style>
  #research-project-grid {
    display: grid;
    grid-template-columns: minmax(0, 1fr);
    grid-auto-rows: 1fr;
    gap: 1.25rem;
    margin-bottom: 3rem;
  }

  #research-project-grid .research-project-card {
    display: flex;
    flex-direction: column;
    min-width: 0;
    min-height: 10rem;
    padding: 1.75rem 2rem;
    background: var(--global-card-bg-color);
    color: var(--global-text-color);
    border: 1px solid var(--global-divider-color);
    border-radius: 0.375rem;
    text-decoration: none;
  }

  #research-project-grid .research-project-title {
    margin: 0 0 0.75rem;
    color: var(--global-text-color);
  }

  #research-project-grid .research-project-card:hover .research-project-title,
  #research-project-grid .research-project-card:focus-visible .research-project-title {
    color: var(--global-theme-color);
  }

  #research-project-grid .research-project-subtitle {
    margin: 0;
    font-size: 1rem;
    font-weight: 300;
    line-height: 1.65;
    overflow-wrap: break-word;
  }

  #research-project-grid .research-project-card:focus-visible {
    outline: 2px solid var(--global-theme-color);
    outline-offset: 4px;
  }

  @media (max-width: 575.98px) {
    #research-project-grid .research-project-card {
      padding: 1.5rem;
    }
  }
</style>

<div class="projects">
{% if site.enable_project_categories and page.display_categories %}
  <!-- Display categorized projects -->
  {% for category in page.display_categories %}
  <a id="{{ category }}" href=".#{{ category }}">
    <h2 class="category">{{ category }}</h2>
  </a>
  {% assign categorized_projects = site.projects | where: "category", category %}
  {% assign sorted_projects = categorized_projects | sort: "importance" %}
  <!-- Generate cards for each project -->
  {% if category == "Research" %}
  <div id="research-project-grid">
    {% for project in sorted_projects %}
      {% assign card_title = project.title %}
      {% case project.permalink %}
        {% when '/projects/sparse-train-reconstruction/' %}
          {% assign card_title = 'TrainRecon' %}
        {% when '/projects/monocular-depth-railway/' %}
          {% assign card_title = 'SceneRecon' %}
        {% when '/projects/intelligent-cad/' %}
          {% assign card_title = 'Intelligent CAD' %}
        {% when '/projects/pikan-drive/' %}
          {% assign card_title = 'PIKAN-Drive' %}
      {% endcase %}
      <a class="research-project-card card hoverable" href="{{ project.url | relative_url }}">
        <h2 class="card-title research-project-title">{{ card_title | escape }}</h2>
        <p class="research-project-subtitle">{{ project.paper_title | default: project.title | escape }}</p>
      </a>
    {% endfor %}
  </div>
  {% elsif page.horizontal %}
  <div class="container">
    <div class="row row-cols-1 row-cols-md-2">
    {% for project in sorted_projects %}
      {% include projects_horizontal.liquid %}
    {% endfor %}
    </div>
  </div>
  {% else %}
  <div class="row row-cols-1 row-cols-md-2">
    {% for project in sorted_projects %}
      {% include projects.liquid %}
    {% endfor %}
  </div>
  {% endif %}
  {% endfor %}

{% else %}

<!-- Display projects without categories -->

{% assign sorted_projects = site.projects | sort: "importance" %}

  <!-- Generate cards for each project -->

{% if page.horizontal %}

  <div class="container">
    <div class="row row-cols-1 row-cols-md-2">
    {% for project in sorted_projects %}
      {% include projects_horizontal.liquid %}
    {% endfor %}
    </div>
  </div>
  {% else %}
  <div class="row row-cols-1 row-cols-md-2">
    {% for project in sorted_projects %}
      {% include projects.liquid %}
    {% endfor %}
  </div>
  {% endif %}
{% endif %}
</div>
