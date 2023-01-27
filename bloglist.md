---
layout: default
title: Blog Posts
permalink: /blogview/
sitemap: false
---

 {% for post in site.posts %}
  <article>
    <h2><a href="{{ post.url }}">{{ post.title }}, {{ post.date | date: "%Y-%m-%d" }}</a></h2>
  </article>
{% endfor %}
