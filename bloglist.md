---
layout: default
title: Blog Posts
permalink: /blogview/
sitemap: false
---

 {% for post in site.posts %}
  <article>
    <h2>
      <a href="{{ post.url }}, {{ post.date | date: "%Y-%m-%d" }}">
        {{ post.title }}
      </a>
    </h2>
  </article>
{% endfor %}
