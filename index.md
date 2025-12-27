---
layout: default
title: Trang Chủ
---


<style>
  .home-container {
    background-color: #ffffff !important;
    color: #333333 !important;
    display: flex !important;
    flex-direction: column !important;
    align-items: center !important;
    justify-content: center !important;
    text-align: center !important;
    padding: 60px 20px !important;
    min-height: 60vh !important;
  }

  .hero-avatar {
    width: 180px;
    height: 180px;
    border-radius: 50% !important;
    object-fit: cover;
    object-position: top center;
    margin-bottom: 20px;
    box-shadow: 0 4px 10px rgba(0,0,0,0.1);
  }

  .hero-branding {
    font-size: 2rem !important;
    font-weight: 900 !important;
    color: #000000 !important;
    margin-bottom: 10px !important;
  }

  .hero-subtitle {
    font-size: 1.1rem !important;
    color: #666 !important;
    margin-bottom: 30px !important;
  }

  .hero-buttons {
    display: flex !important;
    gap: 20px !important;
    justify-content: center !important;
    width: 100% !important;
  }

  .btn-dark-option {
    display: inline-block !important;
    padding: 12px 35px !important;
    background-color: transparent !important;
    color: #333 !important;
    border: 2px solid #333 !important;
    border-radius: 8px !important;
    font-weight: bold !important;
    text-decoration: none !important;
    transition: all 0.3s ease !important;
    min-width: 120px !important;
    text-align: center !important;
  }

  .btn-dark-option:hover {
    background-color: #333 !important;
    color: #fff !important;
    transform: translateY(-2px);
  }
</style>

<div class="home-container">
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
