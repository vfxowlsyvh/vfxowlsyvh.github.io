---
layout: page
title: All Posts
permalink: /posts/
---

<section class="post-list">
  {% for post in site.posts %}
    <article class="post-preview">
      <h2><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h2>
      <p class="post-meta">{{ post.date | date: "%B %d, %Y" }} {% if post.categories.size > 0 %}&middot; {{ post.categories | join: ", " }}{% endif %}</p>
      <p class="post-excerpt">{{ post.excerpt | strip_html | truncatewords: 24 }}</p>
    </article>
  {% endfor %}
</section>
