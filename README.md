<div align="center">

# 안녕하세요, 개발자 전학수입니다

**실무의 불편에서 출발해, 설계부터 배포·운영까지 끝까지 책임지는 시스템을 만듭니다.**
데이터 파이프라인 · 백엔드(FastAPI · Next.js · Spring) · 클라우드(AWS · GCP)를 넘나들며, 실제로 사용되는 도구를 만드는 것을 좋아합니다.

<br/>

![Full-Stack](https://img.shields.io/badge/Focus-Full--Stack%20%2B%20Data-4285F4?style=flat-square)
![Cloud](https://img.shields.io/badge/Cloud-AWS%20·%20GCP%20·%20Supabase-FF9900?style=flat-square)
![Backend](https://img.shields.io/badge/Backend-FastAPI·Next.js·Spring-009688?style=flat-square)
![ETL Pipeline](https://img.shields.io/badge/ETL-Extract·Transform·Load-2088FF?style=flat-square)

</div>

---

## About

- 🔧 **문제 → 시스템**: 수작업으로 굴러가던 업무(강사 정산, 공고 검색, 문서 검색, 행사 부스 체험 확인)를 실사용 시스템으로 바꿔 왔습니다. 지금도 회사와 실사용자들이 쓰고 있습니다.
- 🛡 **운영을 의식한 엔지니어링**: 멱등성(UPSERT) · 재시도(exponential backoff) · 동시성 제어(Lock) · 데이터 품질 검증 · 금액 스냅샷 · 감사 로그.
- 🧪 설계 결정을 기록합니다: 주요 아키텍처 결정은 ADR로 남기고, 순수 로직은 분리해서 테스트 가능하게 유지합니다. v1 → v2 → v3 점진적 고도화.
- ☁️ **클라우드 네이티브**: AWS(EC2 · RDS · S3) 배포 구성과 GCP(Cloud Run · Vertex AI · Firestore) 서버리스 백엔드를 직접 설계·운영합니다.

---

## Tech Stack

**Languages**

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)
![Java](https://img.shields.io/badge/Java-ED8B00?style=flat-square&logo=openjdk&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)
![SQL](https://img.shields.io/badge/SQL-025E8C?style=flat-square&logo=postgresql&logoColor=white)

**Backend & Frontend**

![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)
![Next.js](https://img.shields.io/badge/Next.js%2015-000000?style=flat-square&logo=nextdotjs&logoColor=white)
![React](https://img.shields.io/badge/React%2019-61DAFB?style=flat-square&logo=react&logoColor=black)
![Spring](https://img.shields.io/badge/Spring-6DB33F?style=flat-square&logo=spring&logoColor=white)
![Drizzle ORM](https://img.shields.io/badge/Drizzle%20ORM-C5F74F?style=flat-square&logo=drizzle&logoColor=black)

**Cloud & Infra**

![AWS](https://img.shields.io/badge/AWS-EC2·RDS·S3-FF9900?style=flat-square&logo=amazonwebservices&logoColor=white)
![Google Cloud](https://img.shields.io/badge/GCP-Cloud%20Run·Vertex%20AI·Firestore-4285F4?style=flat-square&logo=googlecloud&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat-square&logo=linux&logoColor=black)
![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white)

**Data & AI**

![ETL](https://img.shields.io/badge/ETL%20Pipeline-2088FF?style=flat-square)
![pandas](https://img.shields.io/badge/pandas-150458?style=flat-square&logo=pandas&logoColor=white)
![RAG](https://img.shields.io/badge/RAG-Vertex%20AI%20Search·Gemini-673AB7?style=flat-square)
![Data Quality](https://img.shields.io/badge/Data%20Quality-00897B?style=flat-square)

---

## 주요 프로젝트

### 1. TutorPay — 강사 배정·급여정산 시스템 *(사내 실사용)*

> 구글 시트로 관리하던 **강사 100여 명·연 수백 건 강의**의 배정·단가 계산·월별 정산·통합보고서를 웹앱으로 이전. **AWS(EC2 + Docker Compose + RDS 옵션) 배포 구성.**

- **금액 스냅샷 설계** — 단가표가 개정돼도 확정된 강의 금액은 불변. 단가표는 시행일 기반 버전 테이블로 관리
- **급여 규칙의 마이그레이션화** — 요율 개편(차시 구간·지역 특례)을 멱등 SQL 마이그레이션으로 추적
- **시트 → DB 이전 파이프라인** — 추출 스크립트가 시트 캐시값과 재계산 값을 대조해 불일치 자동 검증
- **성과**: 월말마다 시트에서 하던 수작업 정산 마감(강사별 단가 대조·명세서 개별 작성, **반나절 이상**) → **자동 계산 + 원클릭 명세서·엑셀 출력**으로 단축, 수기 대조 오류 0건
- **Stack**: `Next.js 15` `React 19` `TypeScript` `Drizzle ORM` `PostgreSQL` `Docker` `Caddy` `AWS`
- 👤 단독 설계·개발·운영 · 🔗 [`tutor-pay`](https://github.com/vittroi384/tutor-pay)

<br/>

### 2. 부스 QR 스탬프 랠리 — 행사 방문객 앱 + 운영 대시보드 *(배포 완료, 행사 투입 예정)*

> 교육청 주최 수학·과학 축전(**부스 95개 · 하루 최대 5만 명**)용 웹앱. 부스마다 인력을 두는 대신 **고정 QR + 서버 검증(토큰·시간 간격)** 으로 도장을 찍고, 완주하면 앱 안에서 설문 → 교환권 → 운영본부 수령까지 한 흐름. 운영본부는 15초 갱신 대시보드로 현장을 본다.

- **Auth 없이 anon 키 하나 + RPC 권한 모델** — 개인정보 테이블은 RLS 정책 없이 `security definer` RPC 로만 접근, 관리자는 비밀번호 해시 검사 뒤에서만
- **치팅 방지는 서버에서** — QR 마다 비밀 토큰, 같은 사람 도장 간격 90초. 링크를 공유받아도 이득이 없게
- **오프라인 큐** — 운동장 통신 불안정 대비, 전송 실패·타임아웃 시 폰에 저장 후 자동 재전송. 서버 거절과 통신 실패를 구분
- **행사 전 점검** — 방문객·관리자·지도·대시보드·SQL·보안으로 나눠 코드를 다시 읽고 재현 테스트로 43건 수정. 라우터 복귀 주소, 관리자 잠금 범위(틀린 비밀번호만), 설정 동시 저장 병합, 교환권 중복 수령 차단
- **검증**: Playwright 테스트 12벌 · 폭주 테스트 800명 동시 에러 0 · **지속 테스트 2회(초당 6명 × 15분 = 35,314 요청) 에러 0, p95 73ms** (Supabase 무료 플랜)
- **Stack**: `Vanilla JS (단일 HTML)` `Supabase (Postgres · PostgREST · RPC · RLS)` `Vercel` `Playwright` · 운영비 0원
- 👤 단독 설계·개발·테스트·배포 · 🔗 [`wonju-stamp-rally`](https://github.com/vittroi384/wonju-stamp-rally) *(부스·기관명은 더미 데이터)*

<br/>

### 3. GetQRMaker — 무엇이든 QR 코드로 바꾸는 무료 생성기 *(10개 언어 공개 서비스, getqrmaker.com 운영 중)*

> URL·SNS·WhatsApp·Wi-Fi·연락처·결제 링크 등 **17종(Pix·UPI·EPC 결제 포함)을 정적 QR**로 만드는 웹서비스. 시장의 "동적 QR + 구독" 모델을 의도적으로 배제하고, 수익은 AdSense·유입은 **10개 언어 × 26종 SEO 랜딩 260페이지**(영어 기본, 한·스페인·포르투갈·독일·프랑스·일본·힌디·인도네시아·중국어(간체)는 언어별로 새로 쓴 본문)로 가져가는 구조. Oracle Cloud 무료 티어 + Cloudflare 프록시, 운영비 0원.

- **정적 QR 원칙** — QR에 사용자 내용만 담아 인쇄물이 서버 가동에 종속되지 않음. 리다이렉트·추적·단축 URL 없음 (ADR로 기록)
- **저장 시점에만 기록** — 입력 중 전송 없이 PNG/SVG/복사/인쇄/ZIP 클릭에서만 1건. Wi-Fi 비밀번호는 클라이언트·서버 양쪽에서 `****` 고정 마스킹
- **관리자 3중 잠금** — `/admin`은 일반 404와 동일 응답, 비밀 입구 URL(서명 게이트 쿠키) + RFC 6238 TOTP 직접 구현(재사용 차단) + IP 허용목록, `__Host-` 세션·UA 지문
- **일괄 생성·인쇄** — 엑셀 붙여 넣기 → PNG ZIP(의존성 없는 ZIP 작성기), A4 인쇄 안내판. QR 비트맵은 모듈당 정수 픽셀로 보정
- **분석·운영** — 관리자 통계(언어·페이지·종류별 저장, 선택→미리보기→저장 퍼널; 개인정보 없는 카운터), 입력 기록 자동 분류(도메인·플랫폼·방문자 언어)·요약, **Umami 자체 호스팅**(쿠키 없음 → 동의 배너 불필요, 대시보드는 SSH 터널로만·공개 경로는 추적 스크립트 2개뿐), 브라우저 오류 수집, 로그 로테이션
- **검증** — 코드 리뷰 8차(지적 → 수정 → 통과) + 공개 후 보안 점검 6항목 대응, 단위 테스트 166건 + Playwright E2E 38건(a11y 포함), Lighthouse 98/100/100/100, GitHub Actions CI(lint·types·tests·build → E2E+Postgres → Docker), ADR 9편
- **Stack**: `Next.js 16` `React 19` `TypeScript` `Drizzle ORM` `PostgreSQL 16` `Umami` `Docker` `Caddy` `Oracle Cloud` `GitHub Actions`
- 👤 단독 설계·개발·배포 · 🔗 [`qr-web`](https://github.com/vittroi384/qr-web)

<br/>

### 4. Drive RAG 챗봇 — 사내 문서 기반 질의응답 *(회사 GCP Cloud Run 운영 중)*

> **사내 Google Drive / GCS 문서를 근거로만 답변하는 RAG 챗봇.** 환각을 줄이는 검증 파이프라인에 초점을 둔 클라우드 네이티브 백엔드.

- **하이브리드 검색**: 공용 문서(Vertex AI Search) + 개인 문서(OAuth Drive) 동시 검색
- **RAG 파이프라인**: 후보 top-20 → Gemini re-rank top-5 → 생성 → **답변 검증 레이어**
- **검색 백엔드 추상화**: ABC 인터페이스 뒤로 구현 은닉 → 백엔드 교체를 설정 한 줄로
- **엔지니어링**: ADR 9편 · Firestore(대화 저장) · pytest · ruff · mypy · Cloud Run/IAP/Secret Manager 배포
- **성과**: 규정·지침 확인을 위해 드라이브 폴더를 뒤지던 시간(**건당 수 분~수십 분**)을 **질문 한 번으로 단축**, 답변마다 근거 문서 링크를 제시해 반복 문의·재확인 비용 절감
- **Stack**: `FastAPI` `Python 3.11 (async)` `Vertex AI` `Gemini` `Firestore` `Docker` `Cloud Run`
- 👤 단독 설계·개발 · 🔗 [`drive-chatbot`](https://github.com/vittroi384/drive-chatbot)

<br/>

### 5. 입찰공고 자동화·시각화 ETL 파이프라인 *(사내 운영 중)*

> **6개 정부 부처/기관**(조달청 · 기업마당 · 보조금24 · e나라도움 · K-Startup · KOCCA)의 공고를 자동 수집·정제·시각화. 영업팀 실사용 — 수동 검색 **일 1~2시간 → 0시간**.

- 6개 공공 Open API 6시간 주기 호출, 장애 시 트랙별 격리 + exponential backoff 재시도
- 기관별 상이한 필드·날짜 포맷을 **단일 스키마로 정규화**, 키워드 필터 + 카테고리 자동 태깅
- Batch Insert 일괄 적재 · 자격증명 분리 · Lock 으로 중복 실행 방지 · 90일 자동 정리
- **Stack**: `Google Apps Script` `Google Sheets` `Looker Studio` `REST API` · 👤 단독 기획·개발·운영 · 🔒 *비공개 (요청 시 공유)*

<br/>

### 6. 실시간 암호화폐 데이터 파이프라인 + 자동매매 봇

> 업비트 시세를 **수집 → 저장 → 가공 → 품질검사 → 시각화**하는 ETL 파이프라인. 인프라 없이 Python + SQLite 단일 노드, 24시간 무중단 운영.

- 멱등 수집(UPSERT) · 지표 변환(MA·RSI·볼린저·일목) · 품질검사(결측·신선도) 이상 시 텔레그램 알림
- 각 단계를 실무 도구와 1:1 매핑 설계 — 오케스트레이터↔Airflow, 변환↔dbt, 품질검사↔Great Expectations
- 웹 대시보드(Flask) · systemd · GitHub Actions CI
- **Stack**: `Python` `SQLite` `pandas` `matplotlib` `Flask` · 👤 단독 설계·개발 · 🔗 [`btc-trading-bot`](https://github.com/vittroi384/btc-trading-bot)

<br/>

### 7. KOSHA 작업환경 종합관리 플랫폼 — 공공 SI *(운영 중)*

> **한국산업안전보건공단(KOSHA) 발주** 공공 SI — IoT 기반 화학물질 노출·실내 공기질 모니터링 플랫폼. SI 기업 소속으로 참여해 **4개 모듈을 화면부터 DB까지 풀스택 구현**.

- 담당: 공지사항 · 자료실 · 팝업관리 · **환기수준 모니터링**(IoT 센서 데이터 조회)
- Java MVC + Spring · MyBatis(페이지네이션·검색) · Xframe5 화면 + 반응형 변환 · 폐쇄망(SVN) 환경 7개월
- **Stack**: `Java` `Spring` `MyBatis` `PostgreSQL` `전자정부 표준 프레임워크` · 🔗 [운영 사이트](https://chemsol.kosha.or.kr/)

---

## 그 외 프로젝트

| 프로젝트 | 설명 |
|---|---|
| [`fine`](https://github.com/vittroi384/fine) | 벌금형 소셜 습관 챌린지 앱 MVP — Expo(React Native) + Supabase(RLS·Edge Functions·pg_cron), 스펙 문서·SQL 테스트 포함 |
| [`meal-allergen-checker`](https://github.com/vittroi384/meal-allergen-checker) | 학교 급식 알레르기 자동 판별·알림 시스템 — NEIS 연동, 서버리스(Apps Script), node:test 77건 |
| [`file-auto-sort`](https://github.com/vittroi384/file-auto-sort) | 폴더 실시간 감시 파일 자동 분류 Windows 트레이 유틸 — 연습 모드·되돌리기 등 안전장치 우선 |
| [`script-to-speech`](https://github.com/vittroi384/script-to-speech) | 대본 txt → 순서대로 mp3 변환 데스크톱 TTS (edge-tts/ElevenLabs 2종) |
| [`oci-arm-grab`](https://github.com/vittroi384/oci-arm-grab) | 클라우드 무료 인스턴스 확보 자동 재시도 GitHub Actions 워크플로 |

---

## Contact

- 📧 **Email**: jjook924@gmail.com
- 📝 **Portfolio (Notion)**: https://app.notion.com/p/63f54254ed7848c989b11034b3173e96

<div align="center">
<sub>문제를 발견하고, 시스템으로 만들고, 끝까지 운영합니다.</sub>
</div>
