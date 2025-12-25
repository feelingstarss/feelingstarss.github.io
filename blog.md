---
layout: page
title: Blog
permalink: /blog/
---

<style>
  /* Container tổng */
  .post-list-container {
    max-width: 850px;
    margin: 0 auto;
    padding: 20px 0;
  }

  /* Khung bài viết biến thành liên kết */
  .post-card-link {
    text-decoration: none !important;
    color: inherit !important;
    display: block;
    margin-bottom: 25px;
  }

  .post-card {
    background: #ffffff;
    border: 1px solid #e1e4e8;
    border-radius: 12px;
    padding: 25px;
    box-shadow: 0 4px 12px rgba(0,0,0,0.05);
    transition: all 0.3s cubic-bezier(0.25, 0.8, 0.25, 1);
    position: relative;
    overflow: hidden;
  }

  /* Hiệu ứng khi di chuột vào bất kỳ đâu trong khung */
  .post-card-link:hover .post-card {
    transform: translateY(-5px);
    box-shadow: 0 12px 24px rgba(0,0,0,0.12);
    border-color: #007bff;
  }

  /* Tiêu đề: Nhỏ lại, cực đậm, 1 dòng duy nhất */
  .post-title {
    font-size: 1.1rem;
    font-weight: 800; /* In đậm theo yêu cầu */
    color: #24292e;
    margin: 0 0 12px 0;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis; /* Hiện dấu ... nếu tiêu đề dài */
    display: block;
  }

  .post-card-link:hover .post-title {
    color: #007bff;
  }

  /* Nội dung mô tả ngắn */
  .post-description {
    color: #586069;
    font-size: 0.95rem;
    line-height: 1.6;
    margin: 0;
    /* Giới hạn hiển thị 2 dòng nội dung */
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
    overflow: hidden;
  }

  /* Trang trí thêm một đường gạch màu nhỏ khi hover */
  .post-card::before {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    width: 4px;
    height: 100%;
    background-color: transparent;
    transition: background-color 0.3s;
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