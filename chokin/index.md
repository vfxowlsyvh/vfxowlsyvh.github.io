---
layout: page
title: Chokin
permalink: /chokin/
---

<section class="post-list">
  {% assign chokin_posts = site.categories["chokin"] | default: empty %}
  {% if chokin_posts.size > 0 %}
    {% for post in chokin_posts %}
      <article class="post-preview">
        <h2><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h2>
        <p class="post-meta">{{ post.date | date: "%B %d, %Y" }} {% if post.categories.size > 0 %}&middot; {{ post.categories | join: ", " }}{% endif %}</p>
        <p class="post-excerpt">{{ post.excerpt | strip_html | truncatewords: 28 }}</p>
      </article>
    {% endfor %}
  {% else %}
    <p>No posts yet. Check back soon.</p>
  {% endif %}
</section>
