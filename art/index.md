---
layout: page
title: Art
permalink: /art/
---

<section class="post-list">
  {% assign art_posts = site.categories["art"] | default: empty %}
  {% if art_posts.size > 0 %}
    {% for post in art_posts %}
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
