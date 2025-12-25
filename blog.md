---
layout: page
title: Blog
permalink: /blog/
---
# Các bài viết đã chia sẻ
{% for post in site.posts %}
  <div style="margin-bottom: 20px; border-bottom: 1px solid #ccc;">
    <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
    <p>{{ post.excerpt | strip_html | truncatewords: 25 }}</p>
    <a href="{{ post.url }}">Đọc tiếp...</a>
  </div>
{% endfor %}