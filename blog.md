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

  .search-container {
    margin-bottom: 30px;
    position: relative;
  }

  #search-input {
    width: 100%;
    box-sizing: border-box; /* Quan trọng: Để padding không làm vỡ layout */
    padding: 15px 25px; /* Tăng padding chút cho đẹp */
    font-size: 1rem;
    border: 2px solid #e1e4e8;
    border-radius: 50px; /* Bo tròn mềm mại hơn */
    outline: none;
    transition: all 0.3s ease;
    box-shadow: 0 4px 10px rgba(0,0,0,0.05); /* Shadow nhẹ cho nổi */
  }

  #search-input:focus {
    border-color: #007bff;
    box-shadow: 0 4px 12px rgba(0,123,255,0.15);
  }

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
    font-size: 1.05rem !important; /* Đã chỉnh nhỏ lại theo ý bạn */
    font-weight: 800 !important;
    color: #1a1a1a;
    margin: 0 0 8px 0;
    display: block;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    line-height: 1.8 !important; /* Tăng mạnh dòng để hiển thị trọn vẹn chữ */
    padding-bottom: 8px !important; /* Đệm dưới dày hơn cho dấu nặng */
    margin-bottom: 0px !important; /* Trừ margin để layout không bị lệch do padding */
  }

  .post-description {
    color: #586069;
    font-size: 0.9rem;
    line-height: 1.5;
    margin: 0;
  }

  /* Ẩn tiêu đề mặc định 'Blog' của layout Page */
  .post-header h1.post-title {
    display: none !important;
  }

  /* Style cho tiêu đề mới */
  .custom-blog-header {
    text-align: center;
    margin-bottom: 40px;
  }
  .custom-blog-header h1 {
    font-size: 2.5rem;
    color: #2c3e50;
    margin-bottom: 10px;
    font-weight: 700;
  }
  .custom-blog-header p {
    font-size: 1.1rem;
    color: #7f8c8d;
    max-width: 600px;
    margin: 0 auto;
    line-height: 1.6;
  }
</style>




<div class="post-list-container">
  
  <div class="custom-blog-header">
    <h1>Góc Chia Sẻ Kiến Thức</h1>
    <p>Chào mừng bạn đến với không gian học tập của Kiệt. Nơi lưu giữ những bài học tâm đắc về Java, Network và hành trình trở thành Developer chuyên nghiệp.</p>
  </div>

  <div class="search-container">
    <input type="text" id="search-input" placeholder="Nhập tên bài viết để tìm kiếm...">
  </div>

  <div id="post-list">
    {% for post in site.posts %}
      <a href="{{ post.url | relative_url }}" class="post-card-link" data-title="{{ post.title | downcase | escape }}" data-content="{{ post.excerpt | strip_html | downcase | escape }}">
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
    noResults.style.display = hasResults ? 'none' : 'block';
  });
</script>