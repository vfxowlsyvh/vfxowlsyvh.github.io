---
layout: page
title: Art
permalink: /art/
---

<section class="post-list">
  {% assign art_posts = site.categories["art"] | default: empty %}
  {% if art_posts.size > 0 %}
    {% for post in art_posts %}
      {% include post-preview.html %}
    {% endfor %}
  {% else %}
    <p>No posts yet. Check back soon.</p>
  {% endif %}
</section>
