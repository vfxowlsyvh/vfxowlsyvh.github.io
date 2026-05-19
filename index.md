---
layout: home
title: Proof of Work Daily
---

Welcome to **Proof of Work Daily** — a focused exploration of proof-of-work cryptocurrencies.

Here you'll find:
- Daily deep dives into one PoW coin at a time
- Mining economics, network health, and industry shifts
- Bilingual posts in English and Chinese

## Latest Posts

{% for post in site.posts limit:10 %}
### [{{ post.title }}]({{ post.url | relative_url }})
*{{ post.date | date: "%B %d, %Y" }}* · {{ post.categories | join: ", " }}

{{ post.excerpt }}

---
{% endfor %}

[View all posts](/posts/)
