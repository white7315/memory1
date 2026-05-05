# 💻 Developer — 제공된 이미지/영상 소스(C:\Users\2wow\Desktop\photo)를 활용하여, '경기도 안성시 대덕면 만세로383'에 위치한 '의류매장'의 기본적인 웹사이트 구조(홈페이지 목업)를 1차로 구현할 것.

💻 Developer: 작업 시작합니다.
```html
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>미르상사 | 의류매장 공식 웹사이트 (목업)</title>
    <style>
        /* 1. Global Reset & Fonts */
        body {
            font-family: 'Apple SD Gothic Neo', 'Malgun Gothic', sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f9f9f9;
            color: #333;
            line-height: 1.6;
        }
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 20px;
        }
        /* 2. Navigation Bar */
        header {
            background-color: #ffffff;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.08);
            position: sticky;
            top: 0;
            z-index: 1000;
            padding: 15px 0;
        }
        .nav-content {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .logo h1 {
            margin: 0;
            font-size: 28px;
            color: #A0522D; /* 브라운 계열 - 의류/가게 느낌 */
        }
        .nav-links a {
            text-decoration: none;
            color: #555;
            margin-left: 25px;
            font-weight: 500;
            transition: color 0.2s;
        }
        .nav-links a:hover {
            color: #A0522D;
        }
        /* 3. Hero Section */
        #hero {
            background: url('placeholder_main_image.jpg') center center/cover no-repeat; /* 실제 이미지로 대체 예정 */
            height: 60vh;
            display: flex;
            align-items: center;
            text-align: center;
            color: #fff;
            position: relative;
        }
        #hero::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-color: rgba(0, 0, 0, 0.35); /* 텍스트 가독성을 위한 오버레이 */
            z-index: 1;
        }
        .hero-content {
            position: relative;
            z-index: 2;
            max-width: 800px;
            margin: 0 auto;
        }
        .hero-content h2 {
            font-size: 3.5em;
            margin-bottom: 15px;
            letter-spacing: -2px;
        }
        .hero-content p {
            font-size: 1.3em;
            margin-bottom: 30px;
        }
        .btn-primary {
            display: inline-block;
            background-color: #D2B48C; /* 부드러운 골드/베이지 */
            color: #333;
            padding: 12px 30px;
            text-decoration: none;
            border-radius: 5px;
            font-weight: bold;
            transition: background-color 0.3s;
            border: none;
            cursor: pointer;
        }
        .btn-primary:hover {
            background-color: #C0A07E;
        }
        /* 4. Section Styling */
        section {
            padding: 80px 0;
        }
        .section-title {
            text-align: center;
            font-size: 2.2em;
            color: #A0522D;
            margin-bottom: 50px;
            position: relative;
        }
        .section-title::after {
            content: '';
            display: block;
            width: 60px;
            height: 3px;
            background-color: #D2B48C;
            margin: 10px auto 0;
        }
        /* About Section (가게 소개) */
        #about .content-grid {
            display: flex;
            gap: 40px;
            align-items: center;
        }
        #about .text-content {
            flex: 1;
        }
        #about .image-gallery {
            flex: 1;
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 15px;
        }
        .gallery-item img {
            width: 100%;
            height: 180px;
            object-fit: cover;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.08);
        }
        /* Product/Category Section */
        #products {
            background-color: #fff;
        }
        .product-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 30px;
            text-align: center;
        }
        .product-card {
            border: 1px solid #eee;
            border-radius: 8px;
            padding: 20px;
            transition: transform 0.3s, box-shadow 0.3s;
        }
        .product-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
        }
        .product-card img {
            width: 100%;
            height: 250px;
            object-fit: cover;
            border-radius: 6px;
            margin-bottom: 15px;
        }
        .product-card h3 {
            color: #A0522D;
            margin: 10px 0 5px;
        }
        /* Location/Footer */
        #location {
            background-color: #eee;
            text-align: center;
            padding: 60px 0;
        }
        #location p {
            font-size: 1.1em;
            margin-bottom: 10px;
        }
        .address-box {
            margin-top: 20px;
            padding: 15px;
            background-color: #fff;
            border-radius: 5px;
            display: inline-block;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.05);
        }
        footer {
            background-color: #333;
            color: #ccc;
            padding: 30px 0;
            text-align: center;
        }
        footer p {
            margin: 5px 0;
        }
    </style>
</head>
<body>

    <!-- 1. HEADER & NAVIGATION -->
    <header>
        <div class="container nav-content">
            <div class="logo">
                <h1>미르상사</h1>
                <p style="font-size: 0.9em; margin: -5px 0 0;">의류 전문 매장</p>
            </div>
            <nav class="nav-links">
                <a href="#about">소개</a>
                <a href="#products">상품</a>
                <a href="#location">오시는 길</a>
                <!-- CTA 버튼을 헤더에 배치하여 중요도 높임 -->
                <a href="tel:000-0000-0000" style="background-color: #D2B48C; color: #333; padding: 8px 15px; border-radius: 5px; text-decoration: none;">전화 문의</a>
            </nav>
        </div>
    </header>

    <!-- 2. HERO SECTION (메인 배너) -->
    <section id="hero">
        <
