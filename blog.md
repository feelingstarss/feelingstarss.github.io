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

  /* TỰA ĐỀ: Nhỏ lại (1.05rem) và in đậm cực mạnh (800) */
  .post-title {
    font-size: 1.05rem !important; 
    font-weight: 800 !important;
    color: #1a1a1a;
    margin: 0 0 10px 0;
    line-height: 1.2;
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
    font-size: 0.92rem;
    line-height: 1.5;
    margin: 0;
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
    overflow: hidden;
  }

  /* ĐƯỜNG TRANG TRÍ BÊN TRÁI KHI HOVER */
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

  /* FIX LỖI CODE BÀI 4-9: Tự động đóng khung và xuống hàng cho mọi khối code */
  pre, code, .highlight {
    background: #1e1e1e !important; /* Nền tối như ảnh mẫu */
    color: #d1d1d1 !important;
    border-radius: 8px;
    padding: 15px;
    display: block;
    overflow-x: auto;
    white-space: pre !important; /* Giữ nguyên định dạng xuống hàng */
    font-family: 'Consolas', 'Monaco', monospace;
    font-size: 0.85rem;
    margin: 15px 0;
    border: 1px solid #333;
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