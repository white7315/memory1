# 💻 Developer — 가장 최근에 완성된 웹사이트 프로토타입(풍선 아치 애니메이션 포함)을 로드하여 사용자에게 시각적으로 보여주고, 상호작용이 가능한 상태로 유지할 것.

💻 Developer: 작업 시작합니다.

```html
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>미르상사 - 따뜻하고 신뢰감 있는 공간</title>
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@300;400;700&display=swap" rel="stylesheet">
    <style>
        /* 전역 스타일 및 톤앤매너 설정 */
        :root {
            --primary-color: #3a6b4b; /* 신뢰감 있는 녹색 계열 */
            --secondary-color: #f5c16d; /* 따뜻한 포인트 오렌지/골드 */
            --text-dark: #333;
            --background-light: #f9f7f4;
            --danger-red: #d9534f;
        }
        body {
            font-family: 'Noto Sans KR', sans-serif;
            background-color: var(--background-light);
            color: var(--text-dark);
            margin: 0;
            padding: 0;
            line-height: 1.6;
        }
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }
        /* 헤더 및 로고 */
        header {
            background-color: #fff;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.08);
            padding: 15px 0;
            position: sticky;
            top: 0;
            z-index: 100;
        }
        .header-content {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .logo {
            font-size: 1.8em;
            font-weight: 700;
            color: var(--primary-color);
        }
        nav a {
            margin-left: 25px;
            text-decoration: none;
            color: var(--text-dark);
            font-weight: 500;
            transition: color 0.2s;
        }
        nav a:hover {
            color: var(--primary-color);
        }

        /* 메인 배너 (풍선 아치 애니메이션 영역) */
        #hero-section {
            text-align: center;
            padding: 80px 20px;
            background-color: #fff;
            position: relative;
            overflow: hidden; /* 애니메이션을 담기 위함 */
            margin-bottom: 40px;
        }
        .hero-title {
            font-size: 3em;
            font-weight: 700;
            color: var(--primary-color);
            margin-bottom: 15px;
        }
        .hero-subtitle {
            font-size: 1.2em;
            color: #666;
            margin-bottom: 30px;
        }

        /* 🎈 풍선 아치 컨테이너 (애니메이션 대상) */
        #balloon-arch-container {
            position: absolute;
            top: 0;
            left: 50%;
            transform: translateX(-50%);
            /* 이 컨테이너 내부에 SVG/애니메이션이 위치함 */
            width: 80%; 
            max-width: 800px;
            height: 200px; /* 시각적 높이 설정 */
            z-index: 1;
            pointer-events: none; /* 클릭 방해 최소화 */
        }

        /* 풍선 아치 애니메이션 (SVG 또는 Pseudo-element 기반으로 가정) */
        .balloon-arch {
            position: absolute;
            width: 100%;
            height: 100%;
            top: 0;
            left: 0;
            /* 실제로는 SVG나 복잡한 CSS로 구현되지만, 여기서는 시각적 효과만 줍니다. */
            background: linear-gradient(to bottom, rgba(255,255,255,0.7) 0%, transparent 100%);
            opacity: 0.9;
            z-index: 2;
        }

        /* 📌 주소 안내 시 포커스 마커 (실제 애니메이션의 '출력' 역할) */
        #address-focus {
            position: absolute;
            width: 10px;
            height: 10px;
            background-color: var(--secondary-color);
            border-radius: 50%;
            box-shadow: 0 0 10px rgba(245, 193, 109, 0.8);
            transition: all 0.5s cubic-bezier(0.25, 1, 0.5, 1); /* 부드러운 이동 효과 */
            z-index: 3;
            /* 초기 위치는 중앙에 배치하고 JS로 이동시킵니다. */
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
        }
        
        /* 내용물 섹션 스타일 */
        section {
            padding: 60px 0;
            border-bottom: 1px solid #eee;
        }
        .section-title {
            text-align: center;
            font-size: 2em;
            color: var(--primary-color);
            margin-bottom: 40px;
        }
        .card-container {
            display: flex;
            gap: 30px;
            justify-content: center;
            margin-top: 30px;
        }
        .card {
            background: #fff;
            padding: 25px;
            border-radius: 8px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.05);
            flex: 1;
            max-width: 350px;
        }
        .card h3 {
            color: var(--primary-color);
            margin-top: 0;
        }

        /* CTA 및 리드 마그넷 */
        #cta-section {
            background-color: var(--primary-color);
            color: white;
            text-align: center;
            padding: 60px 20px;
        }
        .cta-button {
            display: inline-block;
            background-color: var(--secondary-color);
            color: var(--text-dark);
            padding: 15px 30px;
            text-decoration: none;
            font-size: 1.1em;
            font-weight: 700;
            border-radius: 50px;
            margin-top: 20px;
            transition: background-color 0.3s, transform 0.3s;
            border: none;
            cursor: pointer;
        }
        .cta-button:hover {
            background-color: #e0b44e;
            transform: translateY(-2px);
        }

        /* 경고/강조 섹션 */
        .warning-box {
            background-color: #fdebeb;
            border-left: 5px solid var(--danger-red);
            padding: 20px;
            margin: 30px 0;
            border-radius: 4px;
        }
        .warning-box p {
            margin: 0;
            font-weight: 500;
        }
        .warning-box strong {
            color: var(--danger-red);
        }

        /* Footer */
        footer {
            text-align: center;
            padding: 30px 0;
            background-color: #e9ecef;
            color: #6c757d;
        }
    </style>
</head>
<body>
    <header>
        <div class="container header-content">
            <div class="logo">미르상사</div>
            <nav>
                <a href="#hero-section">HOME</a>
                <a href="#about-section">스토어 소개</a>
                <a href="#service-section">서비스</a>
                <a href="#contact-section">오시는
