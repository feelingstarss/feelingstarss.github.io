---
layout: page
title: Blog
permalink: /blog/
---
## Các bài viết đã chia sẻ
{% for post in site.posts %}
- [{{ post.title }}]({{ post.url }})
{% endfor %}