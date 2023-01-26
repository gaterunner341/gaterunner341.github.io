---
layout: default
title: Blog Posts
permalink: /blogview/
sitemap: false
---

{% assign sorted_posts = site.posts | sort: 'title' %}
        {% for post in sorted_posts %}
            {%if post.categories contains category[0]%}
                <h2><a href="{{ site.url }}{{ site.baseurl }}{{ post.url }}" title="{{ post.title }}">{{ post.title }}, {{ post.date | date: "%B %e, %Y" }}<p class="date"></h2></p></a>
            {%endif%}
        {% endfor %}
