---
layout: page
title: Blog
permalink: /blog/
---

<style>
  .post-list-container {
    max-width: 800px;
    margin: 0 auto;
    padding: 20px 10px;
  }

  .post-card-link {
    text-decoration: none !important;
    color: inherit !important;
    display: block;
    margin-bottom: 20px;
  }

  .post-card {
    background: #ffffff;
    border: 1px solid #e1e4e8;
    border-radius: 12px;
    /* Tăng padding để chữ không bị sát mép */
    padding: 22px 25px; 
    box-shadow: 0 4px 12px rgba(0,0,0,0.05);
    transition: all 0.3s ease;
    position: relative;
    overflow: hidden;
  }

  .post-card-link:hover .post-card {
    transform: translateY(-3px);
    box-shadow: 0 8px 20px rgba(0,0,0,0.12);
    border-color: #007bff;
  }

  /* TỰA ĐỀ: Điều chỉnh kích thước nhỏ lại để không bị mất chữ */
  .post-title {
    font-size: 1.2rem;   /* Giảm nhẹ kích thước để rõ chữ hơn */
    font-weight: 800;    /* Giữ độ đậm chuyên nghiệp */
    color: #1a1a1a;
    margin: 0 0 10px 0;
    line-height: 1.3;    /* Tăng khoảng cách dòng để không bị dính chữ */
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    display: block;
  }

  .post-card-link:hover .post-title {
    color: #007bff;
  }

  .post-description {
    color: #586069;
    font-size: 0.95rem;
    line-height: 1.6;
    margin: 0;
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
    overflow: hidden;
  }

  /* Đường trang trí bên trái khi hover */
  .post-card::before {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    width: 5px;
    height: 100%;
    background-color: transparent;
    transition: 0.3s;
  }

  .post-card-link:hover .post-card::before {
    background-color: #007bff;
  }
</style>

<div class="post-list-container">
  {% for post in site.posts %}
    <a href="{{ post.url | relative_url }}" class="post-card-link">
      <article class="post-card">
        <h2 class="post-title">
          {{ post.title }}
        </h2>
        <div class="post-description">
          {{ post.excerpt | strip_html }}
        </div>
      </article>
    </a>
  {% endfor %}
</div>