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
  color: white;
  font-size: 12px;
  margin-bottom: 20px;
  padding-left: 20px; /* Add padding to the left */
  box-sizing: border-box;
}

.article-title {
  margin-left: -20px; /* Negative margin to counteract the padding */
  padding-left: 20px; /* Re-add padding to the title */
  display: inline-block; /* Ensure the margin does not affect block-level elements */
}

.article-info {
  padding: 15px;
  position: absolute;
  bottom: 0;
  width: 100%;
  box-sizing: border-box;
  background-color: #f0f0f0;
  color: black;
  font-size: 12px;
}

.article-info p {
  margin: 5px 0;
}
</style>

{% for post in site.posts %}
  <div class="article-container">
    <div class="article">
      <span class="article-title">{{ post.title | truncate: 50 }} | {{ post.date | date: "%Y-%m-%d" }}</span>
      <div class="article-info">
        {{ post.content | strip_html | truncate: 200 }}<br>
        <a style="font-size: 12px; font-weight: bold;" class="hover-underline-animation" href="{{ post.url }}">Continue Reading...</a>
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