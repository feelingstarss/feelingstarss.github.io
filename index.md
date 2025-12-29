---
layout: default
title: Trang Chủ
---


<style>
  /* CỐ ĐỊNH GIAO DIỆN TRANG CHỦ */
  .home-container {
    background-color: #ffffff !important; /* Đặt lại nền trắng cho sạch sẽ nếu user muốn */
    color: #333333 !important;
    display: flex !important;
    flex-direction: column !important;
    align-items: center !important;
    justify-content: center !important;
    text-align: center !important;
    padding: 60px 20px !important;
    min-height: 60vh !important;
  }

  /* Ảnh đại diện */
  .hero-avatar {
    width: 180px; /* Nhỏ lại theo yêu cầu (cũ 280px) */
    height: 180px;
    border-radius: 50% !important;
    object-fit: cover;
    object-position: top center; /* Giúp hiện rõ phần tóc */
    margin-bottom: 20px;
    box-shadow: 0 4px 10px rgba(0,0,0,0.1);
  }

  /* Tiêu đề chính */
  .hero-branding {
    font-size: 2rem !important; /* Tăng size chút cho oai */
    font-weight: 900 !important; /* In đậm tối đa */
    color: #000000 !important;
    margin-bottom: 10px !important;
  }

  /* Subtitle */
  .hero-subtitle {
    font-size: 1.1rem !important;
    color: #666 !important;
    margin-bottom: 30px !important;
  }

  /* Button Container */
  .hero-buttons {
    display: flex !important;
    gap: 20px !important;
    justify-content: center !important;
    width: 100% !important;
  }

  /* Nút bấm (ĐÓNG KHUNG) */
  .btn-dark-option {
    display: inline-block !important; /* QUAN TRỌNG: Để hiện khung */
    padding: 12px 35px !important;
    background-color: transparent !important;
    color: #333 !important;
    border: 2px solid #333 !important; /* Viền đen rõ ràng */
    border-radius: 8px !important;
    font-weight: bold !important;
    text-decoration: none !important;
    transition: all 0.3s ease !important;
    min-width: 120px !important; /* Độ rộng tối thiểu */
    text-align: center !important;
  }

  .btn-dark-option:hover {
    background-color: #333 !important;
    color: #fff !important;
    transform: translateY(-2px);
  }
</style>

<div class="home-container">
  <!-- Ảnh đại diện -->
  <img src="/assets/images/avatar.png" alt="Kiet Avatar" class="hero-avatar">

  <h1 class="hero-branding">Nguyễn Hứa Tuấn Kiệt</h1>
  
  <p class="hero-subtitle">
    Chào mừng bạn đến với không gian chia sẻ kiến thức của mình.<br>
    Tại đây, mình viết về <b>Java Backend</b>, <b>Network Programming</b>, <b>Security</b> và những kinh nghiệm thực tế trên hành trình trở thành Software Engineer.
  </p>

  <div class="hero-buttons">
     <a href="/profile" class="btn btn-dark-option">Profile</a>
     <a href="/blog" class="btn btn-dark-option">Blog</a>
  </div>
</div>

<div class="content-container">
  <!-- LOGIC PHÂN LOẠI BÀI VIẾT -->
  {% assign featured_posts = "" | split: "" %}
  {% assign other_posts = "" | split: "" %}

  {% for post in site.posts %}
    {% if post.path contains "bai-hoc-java-7" or post.path contains "bai-hoc-java-8" %}
      {% assign featured_posts = featured_posts | push: post %}
    {% else %}
      {% assign other_posts = other_posts | push: post %}
    {% endif %}
  {% endfor %}

  <!-- SECTION 1: BÀI VIẾT NỔI BẬT (FEATURED) -->
  <div class="section-title">
    <h2>Bài viết tiêu biểu</h2>
    <div class="title-underline"></div>
  </div>

  <div class="posts-grid featured-grid">
    {% for post in featured_posts %}
      <div class="post-card featured-card">
        <div class="card-body">
          <span class="post-date text-muted">{{ post.date | date: "%d/%m/%Y" }}</span>
          <h3 class="post-title"><a href="{{ post.url }}">{{ post.title }}</a></h3>
           <p class="post-excerpt">{{ post.excerpt | strip_html | truncatewords: 30 }}</p>
          <a href="{{ post.url }}" class="read-more">Đọc tiếp →</a>
        </div>
      </div>
    {% endfor %}
  </div>

  <!-- SECTION 2: CÁC BÀI VIẾT KHÁC -->
  <div class="section-title" style="margin-top: 60px;">
    <h2>Bài viết khác</h2>
    <div class="title-underline"></div>
  </div>

  <div class="posts-grid other-grid">
    {% for post in other_posts %}
      <div class="post-card">
        <div class="card-body">
          <span class="post-date text-muted">{{ post.date | date: "%d/%m/%Y" }}</span>
          <h4 class="post-title small-title"><a href="{{ post.url }}">{{ post.title }}</a></h4>
          <p class="post-excerpt small-excerpt">{{ post.excerpt | strip_html | truncatewords: 20 }}</p>
        </div>
      </div>
    {% endfor %}
  </div>
</div>

<style>
  /* Container chung cho phần nội dung dưới hero */
  .content-container {
    max-width: 1000px;
    margin: 0 auto;
    padding: 20px;
  }

  /* Tiêu đề section */
  .section-title {
    text-align: center;
    margin-bottom: 40px;
  }
  .section-title h2 {
    font-size: 1.8rem;
    font-weight: 800;
    margin-bottom: 10px;
    text-transform: uppercase;
    letter-spacing: 1px;
  }
  .title-underline {
    width: 60px;
    height: 4px;
    background-color: #007bff; /* Màu xanh nổi bật */
    margin: 0 auto;
    border-radius: 2px;
  }

  /* Grid Layout */
  .posts-grid {
    display: grid;
    gap: 25px;
  }

  /* FEATURED GRID: 2 cột */
  .featured-grid {
    grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  }

  /* OTHER GRID: 3 cột */
  .other-grid {
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  }

  /* KIEU DANG CARD */
  .post-card {
    background: #fff;
    border: 1px solid #eee;
    border-radius: 12px;
    overflow: hidden;
    transition: transform 0.3s ease, box-shadow 0.3s ease;
    padding: 25px;
    box-shadow: 0 5px 15px rgba(0,0,0,0.05);
    display: flex;
    flex-direction: column;
    height: 100%;
  }

  .post-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 10px 25px rgba(0,0,0,0.1);
    border-color: #007bff;
  }

  /* Style cho Featured Card */
  .featured-card {
    border-left: 5px solid #007bff; /* Điểm nhấn xanh bên trái */
    background: linear-gradient(to right bottom, #ffffff, #f9fbfd);
  }

  .post-date {
    font-size: 0.85rem;
    font-weight: 600;
    color: #007bff !important;
    text-transform: uppercase;
    margin-bottom: 10px;
    display: block;
  }

  .post-title {
    margin-top: 0;
    margin-bottom: 15px;
    line-height: 1.4;
  }

  .post-title a {
    color: #333;
    text-decoration: none;
    font-weight: 800;
    transition: color 0.2s;
  }
  .post-title a:hover {
    color: #007bff;
  }

  .post-excerpt {
    color: #666;
    font-size: 0.95rem;
    line-height: 1.6;
    flex-grow: 1; /* Đẩy nút đọc tiếp xuống đáy nếu cần */
  }

  .read-more {
    display: inline-block;
    margin-top: 20px;
    font-weight: 700;
    color: #007bff;
    text-decoration: none;
  }
  .read-more:hover {
    text-decoration: underline;
  }

  /* Style cho Other Cards (nhỏ hơn) */
  .other-grid .post-card {
    padding: 20px;
    border-left: none;
  }
  .small-title {
    font-size: 1.1rem;
    margin-bottom: 10px;
  }
  .small-excerpt {
    font-size: 0.9rem;
  }

  /* Responsive */
  @media (max-width: 768px) {
    .featured-grid, .other-grid {
      grid-template-columns: 1fr; /* Về 1 cột trên mobile */
    }
  }
</style>
