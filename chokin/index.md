---
layout: page
title: Chokin
permalink: /chokin/
---

<section class="post-list">
  {% assign chokin_posts = site.categories["chokin"] | default: empty %}
  {% if chokin_posts.size > 0 %}
    {% for post in chokin_posts %}
      {% include post-preview.html %}
    {% endfor %}
  {% else %}
    <p>No posts yet. Check back soon.</p>
  {% endif %}
</section>
