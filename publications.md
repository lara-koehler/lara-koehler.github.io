---
layout: default
title: Publications
permalink: /publications/
---

{% assign all_pubs = site.data.publications | sort: 'year' | reverse %}
{% assign published = all_pubs | where_exp: 'p', 'p.type != "preprint"' %}
{% assign preprints = all_pubs | where_exp: 'p', 'p.type == "preprint"' %}

{% if published.size > 0 %}
<h2 class="section-heading">Publications</h2>
<div class="publication-list">
  {% for pub in published %}
  {% include publication-entry.html pub=pub %}
  {% endfor %}
</div>
{% endif %}

{% if preprints.size > 0 %}
<h2 class="section-heading">Preprints</h2>
<div class="publication-list">
  {% for pub in preprints %}
  {% include publication-entry.html pub=pub %}
  {% endfor %}
</div>
{% endif %}
