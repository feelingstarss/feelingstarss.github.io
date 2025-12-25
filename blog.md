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

  /* KHU VỰC THANH TÌM KIẾM */
  .search-container {
    margin-bottom: 30px;
    position: relative;
  }

  #search-input {
    width: 100%;
    padding: 12px 20px;
    font-size: 1rem;
    border: 2px solid #e1e4e8;
    border-radius: 25px; /* Bo tròn hiện đại */
    outline: none;
    transition: all 0.3s ease;
    box-shadow: 0 2px 6px rgba(0,0,0,0.05);
  }

  #search-input:focus {
    border-color: #007bff;
    box-shadow: 0 4px 12px rgba(0,123,255,0.15);
  }

  /* CSS CHO CÁC THẺ BÀI VIẾT */
  .post-card-link {
    text-decoration: none !important;
    color: inherit !important;
    display: block;
    margin-bottom: 20px;
    transition: transform 0.3s;
  }

  .post-card {
    background: #ffffff;
    border: 1px solid #e1e4e8;
    border-radius: 12px;
    padding: 20px 25px; 
    box-shadow: 0 4px 12px rgba(0,0,0,0.05);
    position: relative;
    overflow: hidden;
  }

  .post-card-link:hover {
    transform: translateY(-3px);
  }

  .post-title {
    font-size: 1.2rem !important;
    font-weight: 800 !important;
    color: #1a1a1a;
    margin: 0 0 8px 0;
    display: block;
  }

  .post-description {
    color: #586069;
    font-size: 0.9rem;
    line-height: 1.5;
    margin: 0;
  }

  /* CSS CHO PHẦN CODE TRONG BÀI VIẾT (Dùng cho trang chi tiết) */
  pre, code, .highlight {
    background: #1e1e1e !important;
    color: #d1d1d1 !important;
    border-radius: 8px;
    padding: 15px;
    display: block;
    white-space: pre !important;
    overflow-x: auto;
    margin: 15px 0;
  }
</style>

<div class="post-list-container">
  <div class="search-container">
    <input type="text" id="search-input" placeholder="Nhập tên bài viết để tìm kiếm...">
  </div>

  <div id="post-list">
    {% for post in site.posts %}
      <a href="{{ post.url | relative_url }}" class="post-card-link" data-title="{{ post.title | downcase }}" data-content="{{ post.excerpt | strip_html | downcase }}">
        <article class="post-card">
          <h2 class="post-title">{{ post.title }}</h2>
          <p class="post-description">{{ post.excerpt | strip_html | truncate: 150 }}</p>
        </article>
      </a>
    {% endfor %}
  </div>

  <p id="no-results" style="display: none; text-align: center; color: #888; margin-top: 20px;">
    Không tìm thấy bài viết nào phù hợp...
  </p>
</div>

<script>
  const searchInput = document.getElementById('search-input');
  const postCards = document.querySelectorAll('.post-card-link');
  const noResults = document.getElementById('no-results');

  searchInput.addEventListener('input', function() {
    const searchTerm = this.value.toLowerCase().trim();
    let hasResults = false;

    postCards.forEach(card => {
      const title = card.getAttribute('data-title');
      const content = card.getAttribute('data-content');

      if (title.includes(searchTerm) || content.includes(searchTerm)) {
        card.style.display = 'block';
        hasResults = true;
      } else {
        card.style.display = 'none';
      }
    });

    // Hiện thông báo nếu không có kết quả
    noResults.style.display = hasResults ? 'none' : 'block';
  });
</script>