---
layout: page
title: projects
permalink: /projects/
description: A growing collection of your cool projects.
nav: true
nav_order: 2
display_categories: all
horizontal: false
min_importance: 5
---

<!-- pages/projects.md -->
<div class="projects">
{% if site.enable_project_categories and page.display_categories %}
  <!-- Display categorized projects -->
  {% if page.display_categories == "all" %}
    {% assign display_categories = site.projects | sort: "importance" | map: "category" | compact | uniq %}
  {% else %}
    {% assign display_categories = page.display_categories %}
  {% endif %}
  {% for category in display_categories %}
  <a id="{{ category }}" href=".#{{ category }}">
    <h2 class="category">{{ category }}</h2>
  </a>
  {% assign categorized_projects = site.projects | where: "category", category %}
  {% assign sorted_projects = categorized_projects | sort: "importance" %}
  <!-- Generate cards for each project -->
  {% if page.horizontal %}
  <div class="container">
    <div class="row row-cols-1 row-cols-md-2">
    {% for project in sorted_projects %}
      {% if project.importance < page.min_importance %}
      {% include projects_horizontal.liquid %}
      {% endif %}
    {% endfor %}
    </div>
  </div>
  {% else %}
  <div class="row row-cols-1 row-cols-md-3">
    {% for project in sorted_projects %}
      {% if project.importance < page.min_importance %}
      {% include projects.liquid %}
      {% endif %}
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
      {% if project.importance < page.min_importance %}
      {% include projects_horizontal.liquid %}
      {% endif %}
    {% endfor %}
    </div>
  </div>
  {% else %}
  <div class="row row-cols-1 row-cols-md-3">
    {% for project in sorted_projects %}
      {% if project.importance < page.min_importance %}
      {% include projects.liquid %}
      {% endif %}
    {% endfor %}
  </div>
  {% endif %}
{% endif %}
</div>
