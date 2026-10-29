---
layout: page
title: Thangka
permalink: /thangka/
---

<section class="post-list">
  {% assign thangka_posts = site.categories["thangka"] | default: empty %}
  {% if thangka_posts.size > 0 %}
    {% for post in thangka_posts %}
      {% include post-preview.html %}
    {% endfor %}
  {% else %}
    <p>No posts yet. Check back soon.</p>
  {% endif %}
</section>
