---
layout: default
title: Blog Posts
permalink: /blogview/
sitemap: false
---

 {% for post in site.posts %}
  <article>
    <h2><a class="hover-underline-animation" href="{{ post.url }}">{{ post.title }}, {{ post.date | date: "%Y-%m-%d" }}</a></h2>
    {%- if post.image -%}
      <img src="{{ site.url }}/{{ post.image }}">
    {%- endif -%}
    <br>{{ post.content | strip_html | truncatewords: 50 }}
  </article>
{% endfor %}
