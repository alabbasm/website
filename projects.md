---
layout: page  
title: "Projects"  
permalink: /projects/  
---

<div class="projects-grid">
  {% for p in site.projects %}
    <a class="project-card" href="{{ p.url }}">
      <h3>{{ p.title }}</h3>
      {% if p.description %}<p>{{ p.description }}</p>{% endif %}
    </a>
  {% endfor %}
</div>

