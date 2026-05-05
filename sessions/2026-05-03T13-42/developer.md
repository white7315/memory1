# 💻 Developer — 다음과 같은 기능을 갖춘 'AI 통합 블로그 플랫폼'의 기술 아키텍처를 설계합니다. 1) 외부 위젯(Weather/Lotto/Fortune 등)에서 클릭 시 블로그로 부드럽게 연결되는 구조, 2) 블로그 내에 임베드되는 실시간 AI 챗봇/챗창 모듈, 3) 주제가 쉽게 변경될 수 있도록 하는 CMS(콘텐츠 관리 시스템) 기반의 데이터 파이프라인을 정의하고, 개발 로드맵을 작성해 주세요.

💻 Developer: 작업 시작합니다.

요청하신 'AI 통합 블로그 플랫폼'은 단순한 블로그를 넘어, **'지식 진단 및 상호작용을 통한 트래픽 유입 및 컨설팅 전환'**을 목적으로 하는 고도화된 마이크로 서비스 아키텍처가 필요합니다.

현행 블로그 플랫폼(네이버, 티스토리)의 정책적 제약을 우회하고, 주제의 유연성과 AI의 실시간 상호작용을 담보하기 위해 **헤드리스(Headless) 아키텍처**를 기반으로 설계했습니다.

---

## 🏛️ 1. AI 통합 블로그 플랫폼 기술 아키텍처 설계 (System Architecture)

이 시스템은 크게 4개의 계층(Layer)으로 구성되며, 모든 요청은 **API Gateway**를 통해 중앙에서 관리됩니다.

### 1.1. 아키텍처 다이어그램 (Conceptual Flow)

```mermaid
graph TD
    A[외부 플랫폼/위젯] -->|1. 유입 요청 (URL Parameter)| B(Landing Page/Micro-Site);
    B -->|2. Context & Data 전송| C{API Gateway};
    C -->|3. 주제/콘텐츠 요청| D[CMS (Headless CMS)];
    C -->|4. AI 컨설팅 요청| E[AI Core Service (LLM API)];
    D -->|5. 콘텐츠 데이터| F(Blog Front-End/SPA);
    E -->|6. 응답 데이터| F;
    F --> G[사용자 브라우저];

    subgraph Back-End Services
        C; D; E;
    end
    subgraph Presentation Layer
        B; F;
    end
```

### 1.2. 핵심 기술 스택 제안 (Tech Stack Recommendation)

| 구성 요소 | 역할 | 추천 기술 | 선택 이유 |
| :--- | :--- | :--- | :--- |
| **프론트엔드 (Blog Front-End)** | 사용자 인터페이스 (SPA) | React / Next.js | SEO 친화적이며, 동적 콘텐츠와 위젯 통합에 최적화되어 있습니다. |
| **백엔드/API Gateway** | 모든 요청의 라우팅 및 인증 | Node.js (Express/NestJS) | 비동기 처리가 뛰어나 여러 외부 API(AI, CMS)를 동시에 관리하기 용이합니다. |
| **CMS (Headless CMS)** | 모든 콘텐츠(블로그 글, 주제, 구조) 관리 | Strapi / Contentful | 콘텐츠와 프레젠테이션을 완전히 분리하여, 주제 변경이 극도로 유연합니다. |
| **AI Core Service** | 실시간 대화 처리, 데이터 분석 | OpenAI API (GPT-4o) / LangChain | 복잡한 프롬프트 엔지니어링 및 RAG(Retrieval-Augmented Generation) 구현에 필수적입니다. |
| **데이터베이스** | 메타데이터, 사용자 세션, 위젯 데이터 | PostgreSQL / Redis | PostgreSQL은 구조적 데이터를, Redis는 실시간 캐싱 및 세션 관리를 담당합니다. |

---

## 🧩 2. 기능별 모듈 상세 설계 및 구현 방안

### 2.1. [모듈 1] 외부 위젯 연동 및 트래픽 유입 구조 (The Funnel Entry)

**문제 해결:** 네이버, 티스토리 등 외부 플랫폼의 정책적 제약은 **'랜딩 페이지(Landing Page)'**라는 중간 브릿지를 통해 우회합니다.

**구현 로직:**
1. **Micro-Site/Landing Page 구축:** 블로그와는 별도의 독립된 URL 구조를 가진 페이지를 구축합니다. (예: `[도메인]/weather-widget`, `[도메인]/lotto-widget`)
2. **위젯 시뮬레이션:** 이 페이지에서 실제 위젯처럼 보이는 **'호기심 기반의 질문/진단 결과'**를 노출합니다.
3. **Context Passing (핵심):** 사용자가 위젯을 클릭할 때, 단순 이동이 아니라 **쿼리 파라미터(Query Parameter)**를 통해 *어떤 위젯을 통해* 들어왔는지, *어떤 데이터*를 봤는지 블로그로 전달합니다.
    *   **예시:** `[도메인]/blog?source=weather&region=seoul&temp=25&emotion=curious`
4. **블로그 전용 로직:** 블로그의 Front-End는 이 `source` 파라미터를 읽어, 일반적인 글 보기 모드가 아닌 **'진단 결과 리포트 모드'**로 자동 전환되어야 합니다.

### 2.2. [모듈 2] 실시간 AI 챗봇/챗창 모듈 (The Core Value)

**역할:** 단순 Q&A를 넘어, 사용자가 제출한 **Context (위젯 데이터)**와 **블로그의 핵심 주제(CMS 데이터)**를 결합하여 답변합니다.

**구현 로직 (RAG 기반):**
1. **챗봇 호출:** 사용자가 질문을 입력하면, 프론트엔드가 이 질문과 함께 현재 페이지의 **Context Data**를 API Gateway로 전송합니다.
2. **검색 증강 생성 (RAG):** AI Core Service는 질문을 받으면, 먼저 CMS에서 **'현재 주제와 관련된 최신 전문 지식'**을 검색합니다.
3. **프롬프트 구성:** (1) 시스템 역할 정의 (당신은 전문 컨설턴트입니다), (
