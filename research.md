---
layout: default
title: Research
permalink: /research/
---

<div class="project-list">
  {% assign projects = site.projects | sort: 'order' %}
  {% for project in projects %}
  {% include project-card.html project=project %}
  {% endfor %}
</div>
