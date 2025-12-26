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
    width: 160px;
    height: 160px;
    border-radius: 50% !important;
    object-fit: cover;
    margin-bottom: 20px;
    box-shadow: 0 4px 10px rgba(0,0,0,0.1);
  }

  /* Tiêu đề chính */
  .hero-branding {
    font-size: 1.8rem !important;
    font-weight: bold !important;
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

  <h1 class="hero-branding">Xin chào mình là Nguyễn Hứa Tuấn Kiệt</h1>
  
  <p class="hero-subtitle">
    Chào mừng bạn đến với blog của mình
  </p>

  <div class="hero-buttons">
     <a href="/profile" class="btn btn-dark-option">Profile</a>
     <a href="/blog" class="btn btn-dark-option">Blog</a>
  </div>
</div>
