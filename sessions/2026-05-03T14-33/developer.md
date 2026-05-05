# 💻 Developer — writer와 researcher가 제공한 콘텐츠 초안 및 designer가 설계한 레이아웃을 바탕으로, 실제 블로그에 게시될 수 있는 형태의 '웹 목업(Mockup)'을 HTML/CSS 형태로 구현해 주세요. 이 목업은 정적인 페이지여야 하며, 콘텐츠가 자연스럽게 흐르고, CTA와 퀴즈 부분이 시각적으로 기능하는 것처럼 보여야 합니다. (실제 구글 블로그를 만드는 것이 아닌, 구조와 디자인을 보여주는 결과물이어야 합니다.)

💻 Developer: 작업 시작합니다.

요청하신 대로, Writer, Researcher, Designer가 제공한 모든 요소를 통합하여 실제 블로그 포스팅의 구조와 디자인을 보여주는 정적인 웹 목업(Mockup)을 HTML과 CSS 형태로 구현했습니다.

이 코드는 구글 블로그의 실제 기능은 아니지만, 50~70대 타겟에게 최적화된 '권위적이고 신뢰감 있는 전문가의 안내서' 느낌을 시각적으로 완벽하게 재현합니다.

---

### 📄 Mockup Code (HTML & CSS)

**참고:** 이 코드를 `.html` 파일로 저장하고 브라우저에서 열면 목업 페이지를 확인할 수 있습니다.

```html
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>50대 이후 만성 피로, 단순히 '나이 탓'으로 넘기지 마세요.</title>
    <style>
        /* 🎨 Designer Color Variables */
        :root {
            --color-primary-navy: #2C3E50; /* 딥 네이비 - 전문성 */
            --color-secondary-bg: #FCFCF7; /* 아이보리 화이트 - 배경 */
            --color-text-dark: #333333; /* 차분한 회색 - 본문 텍스트 */
            --color-accent-red: #C0392B; /* Danger Red - 경고 */
            --color-accent-orange: #FF9900; /* Vivid Orange - CTA */
            --color-accent-blue: #A9D0F0; /* 미디엄 블루 - 구분 */
        }

        /* 📝 Global Reset & Typography */
        body {
            font-family: '나눔고딕', 'Noto Sans KR', sans-serif;
            background-color: var(--color-secondary-bg);
            color: var(--color-text-dark);
            line-height: 1.7; /* 본문 가독성 최적화 */
            padding: 20px;
            max-width: 800px; /* 블로그 포스트 최대 너비 제한 */
            margin: 0 auto;
        }
        h1 {
            font-size: 36pt;
            color: var(--color-primary-navy);
            border-bottom: 3px solid var(--color-accent-orange);
            padding-bottom: 10px;
            margin-top: 40px;
            font-weight: 700;
        }
        h2 {
            font-size: 26pt;
            color: var(--color-primary-navy);
            margin-top: 35px;
            padding-bottom: 5px;
            border-left: 5px solid var(--color-accent-orange);
            padding-left: 15px;
            font-weight: 600;
        }
        h3 {
            font-size: 22pt;
            color: var(--color-primary-navy);
            margin-top: 25px;
            font-weight: 600;
        }
        p {
            font-size: 18pt; /* ⭐️ 본문 크기 최우선 적용 */
            margin-bottom: 1.5em;
        }
        .highlight {
            font-weight: bold;
            color: var(--color-accent-red);
        }
        .section-break {
            border-top: 1px dashed #ccc;
            margin: 40px 0;
        }

        /* 🚨 경고/진단 섹션 스타일 */
        .warning-box {
            background-color: #ffebeb; /* 아주 연한 빨강 배경 */
            border: 3px solid var(--color-accent-red);
            padding: 25px;
            margin: 30px 0;
            border-radius: 8px;
        }
        .warning-box h4 {
            color: var(--color-accent-red);
            font-size: 24pt;
            margin-top: 0;
        }

        /* 💡 핵심 정보 박스 (원리 설명) */
        .info-box {
            background-color: var(--color-accent-blue);
            padding: 20px;
            margin: 25px 0;
            border-radius: 6px;
        }
        .info-box strong {
            color: var(--color-primary-navy);
        }

        /* 🎯 CTA 버튼 스타일 */
        .cta-button {
            display: block;
            width: 90%;
            max-width: 400px;
            margin: 30px auto;
            padding: 18px 0;
            background-color: var(--color-accent-orange);
            color: white;
            text-align: center;
            text-decoration: none;
            font-size: 24pt;
            font-weight: bold;
            border-radius: 5px;
            transition: background-color 0.3s;
            cursor: pointer;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }
        .cta-button:hover {
            background-color: #e68a00;
        }

        /* 📝 
