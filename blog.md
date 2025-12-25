---
layout: page
title: Blog
permalink: /blog/
---
# Các bài viết đã chia sẻ

<ul>
  {% for post in site.posts %}
    <li style="margin-bottom: 20px;">
      <h2><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h2>
      <p>{{ post.excerpt | strip_html | truncatewords: 30 }}</p>
      <a href="{{ post.url | relative_url }}">Đọc tiếp...</a>
    </li>
  {% endfor %}
</ul>