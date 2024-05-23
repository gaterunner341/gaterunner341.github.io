---
layout: default
title: Blog Posts
permalink: /blogview/
sitemap: false
---

<style>
    .article-container {
        display: flex;
        flex-wrap: wrap;
        gap: 20px;
        margin: 20px;
    }
    .article {
        width: 500px;
        height: 125px;
        position: relative;
        border-radius: 10px;
        overflow: hidden;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        background-color: #191970;
        margin-bottom: 20px;
    }
    .article-info {
        padding: 15px;
        position: absolute;
        bottom: 0;
        width: 100%;
        box-sizing: border-box;
        background-color: #f0f0f0;
        font-size: 12px;
    }
    .article-info p {
        margin: 5px 0;
    }
</style>

{% for post in site.posts %}
 <div class="article-container">
    <div class="article">
        <div class="article-info">
          <a style="font-size: 15px;font-weight: strong;" class="hover-underline-animation" href="{{ post.url }}">{{ post.title | truncate: 50 }} | {{ post.date | date: "%Y-%m-%d" }}</a><br>
          {{ post.content | strip_html | truncatewords: 45 }}
        </div>
    </div>
</div>
{% endfor %}

<i class="fa-solid fa-backward" style="padding-right: 0.3em;margin-left: -0.9em;color: #8B0000;"></i>[Back...](./){: .hover-underline-animation}
<p></p>
<p></p>
<p></p>
<p></p>
<p></p>