---
layout: default
title: Blog Posts
permalink: /blogview/
sitemap: false
---

 {% for post in site.posts %}
  <article>
    <h2><a class="hover-underline-animation" href="{{ post.url }}">{{ post.title }} | {{ post.date | date: "%Y-%m-%d" }}</a></h2>
    {%- if post.image -%}
      <img src="{{ site.url }}/assets/images/featured-image/{{ post.image }}" style="width:150px;float:left" alt="{{ post.alt}}">
    {%- endif -%}
    {{ post.content | strip_html | truncatewords: 50 }}
  </article>
{% endfor %}

<i class="fa-solid fa-backward" style="padding-right: 0.3em;margin-left: -0.9em;color: #8B0000;"></i>[Back...](./){: .hover-underline-animation}