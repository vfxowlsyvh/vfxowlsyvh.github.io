---
layout: page
title: Watch
permalink: /watch/
---

<section class="post-list">
  {% assign watch_posts = site.categories["watch"] | default: empty %}
  {% if watch_posts.size > 0 %}
    {% for post in watch_posts %}
      {% include post-preview.html %}
    {% endfor %}
  {% else %}
    <p>No posts yet. Check back soon.</p>
  {% endif %}
</section>
