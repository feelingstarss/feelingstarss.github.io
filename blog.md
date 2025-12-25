---
layout: page
title: Blog
permalink: /blog/
---

<style>
  /* Bố cục lưới cho danh sách bài viết */
  .post-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 25px;
    margin-top: 30px;
  }

  /* Hiệu ứng thẻ Card */
  .post-card {
    background: #fff;
    border-radius: 12px;
    overflow: hidden;
    box-shadow: 0 4px 15px rgba(0,0,0,0.08);
    transition: transform 0.3s ease, box-shadow 0.3s ease;
    border: 1px solid #f0f0f0;
    display: flex;
    flex-direction: column;
    height: 100%;
  }

  .post-card:hover {
    transform: translateY(-8px);
    box-shadow: 0 12px 25px rgba(0,0,0,0.15);
  }

  .post-content {
    padding: 20px;
    display: flex;
    flex-direction: column;
    flex-grow: 1;
  }

  /* Tiêu đề bài viết */
  .post-title {
    font-size: 1.25rem;
    margin: 0 0 12px 0;
    color: #2c3e50;
    line-height: 1.4;
    font-weight: 700;
  }

  .post-title a {
    text-decoration: none;
    color: inherit;
    transition: color 0.2s;
  }

  .post-card:hover .post-title a {
    color: #3498db;
  }

  /* Đoạn giới thiệu ngắn */
  .post-excerpt {
    color: #5d6d7e;
    font-size: 0.95rem;
    line-height: 1.6;
    margin-bottom: 20px;
  }

  /* Nút đọc tiếp */
  .read-more {
    margin-top: auto;
    font-weight: 600;
    color: #3498db;
    text-decoration: none;
    display: flex;
    align-items: center;
    font-size: 0.9rem;
  }

  .read-more::after {
    content: ' →';
    transition: margin-left 0.2s;
  }

  .post-card:hover .read-more::after {
    margin-left: 5px;
  }

  /* Tag trang trí (Java/JS) */
  .post-tag {
    display: inline-block;
    background: #ebf5ff;
    color: #3498db;
    padding: 4px 12px;
    border-radius: 20px;
    font-size: 0.75rem;
    font-weight: 700;
    text-transform: uppercase;
    margin-bottom: 10px;
  }
</style>

# Các bài viết chia sẻ kinh nghiệm

<div class="post-grid">
  {% for post in site.posts %}
    <article class="post-card">
      <div class="post-content">
        <span class="post-tag">Lập trình mạng</span>
        <h2 class="post-title">
          <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
        </h2>
        <div class="post-excerpt">
          {{ post.excerpt | strip_html | truncatewords: 25 }}
        </div>
        <a href="{{ post.url | relative_url }}" class="read-more">Đọc tiếp bài viết</a>
      </div>
    </article>
  {% endfor %}
</div>