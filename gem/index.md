---
layout: page
title: Gem
permalink: /gem/
---

<section class="post-list">
  {% assign gem_posts = site.categories["gem"] | default: empty %}
  {% if gem_posts.size > 0 %}
    {% for post in gem_posts %}
      {% include post-preview.html %}
    {% endfor %}
  {% else %}
    <p>No posts yet. Check back soon.</p>
  {% endif %}
</section>
