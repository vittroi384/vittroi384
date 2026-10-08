<div align="center">

# 안녕하세요, 개발자 전학수입니다

**실무의 불편에서 출발해, 설계부터 배포·운영까지 끝까지 책임지는 시스템을 만듭니다.**
데이터 파이프라인 · 백엔드(FastAPI · Next.js · Spring) · 클라우드(AWS · GCP)를 넘나들며, 실제로 사용되는 도구를 만드는 것을 좋아합니다.

</div>

---

## About

- **문제 → 시스템**: 수작업으로 굴러가던 업무(강사 정산, 공고 검색, 문서 검색, 행사 부스 체험 확인)를 실사용 시스템으로 바꿔 왔습니다. 지금도 회사와 실사용자들이 쓰고 있습니다.
- **운영을 의식한 엔지니어링**: 멱등 적재(UPSERT) · 트랜잭션 경계 · 데이터 품질 검증 · 금액 스냅샷 · 감사 로그. 재시도·락은 사내 ETL(비공개)에서.
- 설계 결정을 기록합니다: 주요 아키텍처 결정은 ADR로 남기고, 순수 로직은 분리해서 테스트 가능하게 유지합니다. v1 → v2 → v3 점진적 고도화.
- **클라우드**: AWS(EC2 · S3)와 GCP(Cloud Run · Vertex AI · Firestore), Oracle Cloud에 직접 배포·운영합니다.

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
![Next.js](https://img.shields.io/badge/Next.js-000000?style=flat-square&logo=nextdotjs&logoColor=white)
![Spring](https://img.shields.io/badge/Spring-6DB33F?style=flat-square&logo=spring&logoColor=white)

**Infra**

![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white)

---

## 주요 프로젝트

### TutorPay — 강사 배정·급여정산 시스템 *(사내 실사용)*

> 구글 시트로 관리하던 **강사 100여 명·연 수백 건 강의**의 배정·단가 계산·월별 정산·통합보고서를 웹앱으로 이전. **AWS(EC2 + Docker Compose, PostgreSQL 컨테이너 + S3 백업) 배포 구성.**

- **금액 스냅샷 설계** — 단가표가 개정돼도 확정된 강의 금액은 불변. 단가표는 시행일 기반 버전 테이블로 관리
- **급여 규칙의 마이그레이션화** — 요율 개편(차시 구간·지역 특례)을 SQL 마이그레이션으로 추적
- **시트 → DB 이전 파이프라인** — 추출 스크립트가 시트 캐시값과 재계산 값을 대조해 불일치 자동 검증
- **검증**: 시트 558건 재계산 대조 불일치 0, 단위 테스트 43건 + 통합 테스트(단언 68), GitHub Actions에서 빈 DB 생성·재실행 멱등·시드·통합 테스트
- **Stack**: `Next.js 15` `React 19` `TypeScript` `Drizzle ORM` `PostgreSQL` `Docker` `Caddy` `AWS`
- 단독 설계·개발·운영 · 저장소: [`tutor-pay`](https://github.com/vittroi384/tutor-pay)
- **REST 재구현** [`tutorpay-api-nest`](https://github.com/vittroi384/tutorpay-api-nest) — 정산 핵심을 NestJS + TypeORM 으로 다시 짠 API. DTO 검증·오류 봉투·OpenAPI, 정산 잠금과 쓰기를 advisory lock 으로 직렬화(원본의 알려진 한계 해결), 단위 32 + e2e 13(동시성 포함), CI, ADR 3

<br/>

### 부스 QR 스탬프 랠리 — 행사 방문객 앱 + 운영 대시보드 *(배포 완료, 행사 투입 예정)*

> 교육청 주최 수학·과학 축전(**부스 95개**)용 웹앱. 부스에 인력을 두는 대신 **고정 QR + 서버 검증**으로 도장을 찍고, 완주하면 앱 안에서 설문 → 교환권 → 수령까지 이어진다. 운영본부는 15초 갱신 대시보드로 현장을 본다.

- **Auth 없이 anon 키 + RPC 권한 모델** — 개인정보 테이블은 RLS 정책 없이 `security definer` RPC로만 접근
- **치팅 방지는 서버에서** — QR마다 비밀 토큰, 같은 사람 도장 간격 90초. 동시 요청이 간격 검사를 우회하던 경합은 행 잠금으로 수정
- **오프라인 큐** — 통신 실패·타임아웃만 폰에 저장했다가 자동 재전송. 서버 거절과 통신 실패를 구분
- **행사 전 점검** — 영역별로 코드를 다시 읽고 재현 테스트로 42건 수정(치명 4: 설정 동시 저장, 교환권 중복 수령, 잠금 범위, 미저장 부스)
- **검증** — 테스트 스크립트 12벌 · 폭주 800명 동시 에러 0 · **지속 테스트 35,314 요청 에러 0, p95 73ms** (Supabase 무료 플랜)
- **Stack**: `Vanilla JS (단일 HTML)` `Supabase (Postgres · RPC · RLS)` `Vercel` `Playwright` · 운영비 0원
- 단독 설계·개발·테스트·배포 · 저장소: [`wonju-stamp-rally`](https://github.com/vittroi384/wonju-stamp-rally) *(부스·기관명은 더미 데이터)*

<br/>

### GetQRMaker — 무료 QR 코드 생성기 *(10개 언어 공개 서비스, getqrmaker.com 운영 중)*

> URL·Wi-Fi·연락처·결제 등 **17종을 만료 없는 정적 QR**로 만드는 웹서비스. 시장의 "동적 QR + 구독" 모델을 빼고, 수익은 광고·유입은 **10개 언어 × 26종 랜딩 260페이지**로 가져가는 구조. Oracle Cloud 무료 티어 + Cloudflare, 운영비 0원.

- **정적 QR 원칙** — QR에 사용자 내용만 담아 인쇄물이 서버 가동에 종속되지 않음 (ADR)
- **저장 시점에만 기록** — 입력 중 전송 없음. Wi-Fi 비밀번호는 클라이언트·서버 양쪽 마스킹, 전화·이메일은 앞뒤만
- **관리자 3중 잠금** — `/admin`은 일반 404, 비밀 입구 URL + RFC 6238 TOTP 직접 구현 + IP 허용목록
- **공개 API 보호** — 같은 출처·JSON 검사, 종류별 필드 화이트리스트, IP·사이트 전체 분당 상한 (공개 후 보안 점검 6항목 대응)
- **검증** — 단위 177건 + Playwright E2E 40건, GitHub Actions CI(lint·types·tests·build → E2E+Postgres → Docker), ADR 9편
- **Stack**: `Next.js 16` `React 19` `TypeScript` `Drizzle ORM` `PostgreSQL 16` `Docker` `Caddy` `Oracle Cloud` `GitHub Actions`
- 단독 설계·개발·배포 · 저장소: [`qr-web`](https://github.com/vittroi384/qr-web)

<br/>

### 급식 알레르기 자동 판별·알림 시스템 — 학교용 서버리스 웹앱 *(초등학교 1개교 배포)*

> 학생 알레르기 정보와 **NEIS 급식 식단을 매일 자동 대조**해 급식을 못 먹는 학생을 보여주고 담당자·학부모에게 알리는 시스템. Google 스프레드시트 + Apps Script만 사용, 서버·설치 없음, 운영비 0원.

- **NEIS 동기화 → 판별 → 알림** — 알레르기 코드 19종 + 기타 키워드로 판별, 담당자(아침·주간)·학부모(저녁) 알림을 이메일·텔레그램·문자로 발송
- **core / gas / ui 3층 분리** — 파싱·판별·동기화 계획은 Apps Script 의존 없는 순수 로직으로 분리해 `node:test` 78건으로 검증
- **동기화 계획/실행 분리** — 변경 계획을 먼저 만든 뒤 실행. 담당자가 손본 끼니는 자동 동기화가 덮어쓰지 않음
- **접속 잠금** — 비밀번호 해시(SHA-256 + salt)·세션 토큰, 설정 탭만 잠금 / 전체 잠금. 비밀값은 Script Properties에만
- **Stack**: `Google Apps Script` `Google Sheets` `NEIS Open API` `HtmlService` `node:test`
- 단독 설계·개발·배포 · 저장소: [`meal-allergen-checker`](https://github.com/vittroi384/meal-allergen-checker) *(스크린샷은 가상 데이터)*

<br/>

### Drive RAG 챗봇 — 사내 문서 기반 질의응답 *(회사 GCP Cloud Run 운영 중)*

> **사내 Google Drive / GCS 문서를 근거로만 답변하는 RAG 챗봇.** 답변의 근거 여부를 기록하는 검증 단계를 둔 백엔드.

- **검색 백엔드**: Vertex AI Search(공용 문서) + Drive 파일명 검색(로컬 OAuth 한정, 운영은 Vertex 단독)
- **RAG 파이프라인**: 후보 백엔드당 10 → Gemini 재정렬 top-5 → 생성 → **grounded 플래그 기록**
- **검색 백엔드 추상화**: ABC 인터페이스 뒤로 구현 은닉 → 백엔드 교체를 설정 한 줄로
- **엔지니어링**: ADR 12편 · Firestore(대화 저장) · pytest · ruff · mypy · Cloud Run/IAP/Secret Manager 배포
- **검증**: 답변마다 근거 문서 링크 제시. 품질 평가는 골든셋 20문항 초안과 지표(Recall@5·답변 정확도·grounded 일치율) 정의까지(`docs/eval`), 측정은 예정
- **Stack**: `FastAPI` `Python 3.11 (async)` `Vertex AI` `Gemini` `Firestore` `Docker` `Cloud Run`
- 단독 설계·개발 · 저장소: [`drive-chatbot`](https://github.com/vittroi384/drive-chatbot)

<br/>

### 입찰공고 자동화·시각화 ETL 파이프라인 *(사내 운영 중)*

> **6개 정부 부처/기관**(조달청 · 기업마당 · 보조금24 · e나라도움 · K-Startup · KOCCA)의 공고를 자동 수집·정제·시각화. 영업팀 실사용.

- 6개 공공 Open API 6시간 주기 호출, 장애 시 트랙별 격리 + exponential backoff 재시도
- 기관별 상이한 필드·날짜 포맷을 **단일 스키마로 정규화**, 키워드 필터 + 카테고리 자동 태깅
- Batch Insert 일괄 적재 · 자격증명 분리 · Lock 으로 중복 실행 방지 · 90일 자동 정리
- **Stack**: `Google Apps Script` `Google Sheets` `Looker Studio` `REST API` · 단독 기획·개발·운영 · 비공개 *(요청 시 공유)*

<br/>

### KOSHA 작업환경 종합관리 플랫폼 — 공공 SI *(운영 중)*

> **한국산업안전보건공단(KOSHA) 발주** 공공 SI — IoT 기반 화학물질 노출·실내 공기질 모니터링 플랫폼. (주)아이티아이즈 일·학습 병행 사원(2023.08~2024.02)으로 참여해 **4개 모듈을 화면부터 DB까지 풀스택 구현**.

- 담당: 공지사항 · 자료실 · 팝업관리 · **환기수준 모니터링**(IoT 센서 데이터 조회)
- Java MVC + Spring · MyBatis(페이지네이션·검색) · Xframe5 화면 + 반응형 변환 · 폐쇄망(SVN) 환경 7개월
- **Stack**: `Java` `Spring` `MyBatis` `PostgreSQL` `전자정부 표준 프레임워크` · [운영 사이트](https://chemsol.kosha.or.kr/)

<br/>

## 그 외 프로젝트

| 프로젝트 | 설명 |
|---|---|
| [`btc-trading-bot`](https://github.com/vittroi384/btc-trading-bot) | 업비트 시세 수집(UPSERT)→지표→품질검사 파이프라인 + 규칙 매매봇(DRY_RUN) — Python + SQLite 단일 노드, systemd. 학습·실험용 |
| [`fine`](https://github.com/vittroi384/fine) | 벌금형 소셜 습관 챌린지 앱 MVP — Expo(React Native) + Supabase(RLS·Edge Functions·pg_cron), 스펙 문서·SQL 테스트 포함 |
| [`file-auto-sort`](https://github.com/vittroi384/file-auto-sort) | 폴더 실시간 감시 파일 자동 분류 Windows 트레이 유틸 — 연습 모드·되돌리기 등 안전장치 우선 |
| [`oci-arm-grab`](https://github.com/vittroi384/oci-arm-grab) | 클라우드 무료 인스턴스 확보 자동 재시도 GitHub Actions 워크플로 |

---

## Contact

- **Email**: jjook924@gmail.com
- **Portfolio (Notion)**: https://app.notion.com/p/63f54254ed7848c989b11034b3173e96
