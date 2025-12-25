---
layout: page
title: Blog
permalink: /blog/
---

<style>
  /* Container tổng */
  .post-list-container {
    max-width: 900px;
    margin: 0 auto;
    padding: 20px 0;
  }

  /* Khung của mỗi bài viết (Card) */
  .post-card {
    background: #ffffff;
    border: 1px solid #e1e4e8;
    border-radius: 10px;
    padding: 20px;
    margin-bottom: 25px;
    box-shadow: 0 2px 8px rgba(0,0,0,0.05);
    transition: all 0.3s ease;
    display: flex;
    flex-direction: column;
  }

  /* Hiệu ứng khi di chuột vào khung */
  .post-card:hover {
    transform: translateY(-3px);
    box-shadow: 0 8px 20px rgba(0,0,0,0.1);
    border-color: #3498db;
  }

  /* Tiêu đề: Nhỏ lại, in đậm, giới hạn 1 dòng */
  .post-title-link {
    font-size: 1.15rem; /* Chữ nhỏ vừa phải */
    font-weight: 800;   /* Siêu đậm */
    color: #1a1a1a;
    text-decoration: none;
    display: block;
    white-space: nowrap;      /* Không cho xuống dòng */
    overflow: hidden;         /* Ẩn phần thừa */
    text-overflow: ellipsis;  /* Hiện dấu ... nếu quá dài */
    margin-bottom: 10px;
  }

  .post-card:hover .post-title-link {
    color: #3498db;
  }

  /* Đoạn giới thiệu ngắn */
  .post-description {
    color: #586069;
    font-size: 0.95rem;
    line-height: 1.5;
    margin-bottom: 15px;
    /* Giới hạn hiển thị 2 dòng mô tả cho gọn */
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
    overflow: hidden;
  }

  /* Nút Đọc tiếp */
  .btn-readmore {
    font-size: 0.85rem;
    font-weight: 600;
    color: #3498db;
    text-decoration: none;
    align-self: flex-start;
  }

  .btn-readmore:hover {
    text-decoration: underline;
  }
</style>

<div class="post-list-container">
  {% for post in site.posts %}
    <article class="post-card">
      <a href="{{ post.url | relative_url }}" class="post-title-link">
        {{ post.title }}
      </a>
      
      <div class="post-description">
        {{ post.excerpt | strip_html }}
      </div>
      
      <a href="{{ post.url | relative_url }}" class="btn-readmore">
        Đọc tiếp...
      </a>
    </article>
  {% endfor %}
</div>