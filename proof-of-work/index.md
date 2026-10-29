---
layout: page
title: Proof of Work
permalink: /proof-of-work/
---

<section class="post-list">
  {% assign pow_posts = site.categories["proof-of-work"] | default: empty %}
  {% if pow_posts.size > 0 %}
    {% for post in pow_posts %}
      {% include post-preview.html %}
    {% endfor %}
  {% else %}
    <p>No posts yet. Check back soon.</p>
  {% endif %}
</section>
