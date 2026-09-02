<div align="center">

# 안녕하세요, 개발자 전학수입니다 👋

**실무의 불편에서 출발해, 설계부터 배포·운영까지 끝까지 책임지는 시스템을 만듭니다.**
데이터 파이프라인 · 백엔드(FastAPI · Next.js · Spring) · 클라우드(AWS · GCP)를 넘나들며, 실제로 사용되는 도구를 만드는 것을 좋아합니다.

<br/>

![Full-Stack](https://img.shields.io/badge/Focus-Full--Stack%20%2B%20Data-4285F4?style=flat-square)
![Cloud](https://img.shields.io/badge/Cloud-AWS%20·%20GCP-FF9900?style=flat-square)
![Backend](https://img.shields.io/badge/Backend-FastAPI·Next.js·Spring-009688?style=flat-square)
![ETL Pipeline](https://img.shields.io/badge/ETL-Extract·Transform·Load-2088FF?style=flat-square)

</div>

---

## 🧭 About

- 🔧 **문제 → 시스템**: 수작업으로 굴러가던 업무(강사 정산, 공고 검색, 문서 검색)를 실사용 시스템으로 바꿔 왔습니다. 지금도 회사와 실사용자들이 쓰고 있습니다.
- 🛡 **운영을 의식한 엔지니어링**: 멱등성(UPSERT) · 재시도(exponential backoff) · 동시성 제어(Lock) · 데이터 품질 검증 · 금액 스냅샷 · 감사 로그.
- 🧪 **테스트와 문서로 말합니다**: 순수 로직 분리 + 단위 테스트, ADR(Architecture Decision Record)로 설계 결정 기록, v1 → v2 → v3 점진적 고도화.
- ☁️ **클라우드 네이티브**: AWS(EC2 · RDS · S3) 배포 구성과 GCP(Cloud Run · Vertex AI · BigQuery · Firestore) 서버리스 백엔드를 직접 설계·운영합니다.

---

## 🧱 Tech Stack

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
![Google Cloud](https://img.shields.io/badge/GCP-Cloud%20Run·Vertex%20AI·BigQuery-4285F4?style=flat-square&logo=googlecloud&logoColor=white)
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

## 🚀 주요 프로젝트

### 1. 💰 TutorPay — 강사 배정·급여정산 시스템 *(사내 실사용)*

> 구글 시트로 관리하던 **강사 100여 명·연 수백 건 강의**의 배정·단가 계산·월별 정산·통합보고서를 웹앱으로 이전. **AWS(EC2 + Docker Compose + RDS 옵션) 배포 구성.**

- **금액 스냅샷 설계** — 단가표가 개정돼도 확정된 강의 금액은 불변. 단가표는 시행일 기반 버전 테이블로 관리
- **급여 규칙의 마이그레이션화** — 요율 개편(차시 구간·지역 특례)을 멱등 SQL 마이그레이션으로 추적
- **시트 → DB 이전 파이프라인** — 추출 스크립트가 시트 캐시값과 재계산 값을 대조해 불일치 자동 검증
- **Stack**: `Next.js 15` `React 19` `TypeScript` `Drizzle ORM` `PostgreSQL` `Docker` `Caddy` `AWS`
- 👤 단독 설계·개발·운영 · 🔗 [`tutor-pay`](https://github.com/vittroi384/tutor-pay)

<br/>

### 2. 🤖 Drive RAG 챗봇 — 사내 문서 기반 질의응답 *(GCP)*

> **사내 Google Drive / GCS 문서를 근거로만 답변하는 RAG 챗봇.** 환각을 줄이는 검증 파이프라인에 초점을 둔 클라우드 네이티브 백엔드.

- **하이브리드 검색**: 공용 문서(Vertex AI Search) + 개인 문서(OAuth Drive) 동시 검색
- **RAG 파이프라인**: 후보 top-20 → Gemini re-rank top-5 → 생성 → **답변 검증 레이어**
- **검색 백엔드 추상화**: ABC 인터페이스 뒤로 구현 은닉 → 백엔드 교체를 설정 한 줄로
- **엔지니어링**: ADR 13편 · Firestore(대화)/BigQuery(분석) 분리 · pytest · ruff · mypy(strict) · Cloud Run/IAP 배포
- **Stack**: `FastAPI` `Python 3.11 (async)` `Vertex AI` `Gemini` `Firestore` `BigQuery` `Docker` `Cloud Run`
- 👤 단독 설계·개발 · 🔗 [`drive-chatbot`](https://github.com/vittroi384/drive-chatbot)

<br/>

### 3. 🏛 입찰공고 자동화·시각화 ETL 파이프라인 *(사내 운영 중)*

> **6개 정부 부처/기관**(조달청 · 기업마당 · 보조금24 · e나라도움 · K-Startup · KOCCA)의 공고를 자동 수집·정제·시각화. 영업팀 실사용 — 수동 검색 **일 1~2시간 → 0시간**.

- 6개 공공 Open API 6시간 주기 호출, 장애 시 트랙별 격리 + exponential backoff 재시도
- 기관별 상이한 필드·날짜 포맷을 **단일 스키마로 정규화**, 키워드 필터 + 카테고리 자동 태깅
- Batch Insert 일괄 적재 · 자격증명 분리 · Lock 으로 중복 실행 방지 · 90일 자동 정리
- **Stack**: `Google Apps Script` `Google Sheets` `Looker Studio` `REST API` · 👤 단독 기획·개발·운영 · 🔒 *비공개 (요청 시 공유)*

<br/>

### 4. 📊 실시간 암호화폐 데이터 파이프라인 + 자동매매 봇

> 업비트 시세를 **수집 → 저장 → 가공 → 품질검사 → 시각화**하는 ETL 파이프라인. 인프라 없이 Python + SQLite 단일 노드, 24시간 무중단 운영.

- 멱등 수집(UPSERT) · 지표 변환(MA·RSI·볼린저·일목) · 품질검사(결측·신선도) 이상 시 텔레그램 알림
- 각 단계를 실무 도구와 1:1 매핑 설계 — 오케스트레이터↔Airflow, 변환↔dbt, 품질검사↔Great Expectations
- 웹 대시보드(Flask) · systemd · GitHub Actions CI
- **Stack**: `Python` `SQLite` `pandas` `matplotlib` `Flask` · 👤 단독 설계·개발 · 🔗 [`btc-trading-bot`](https://github.com/vittroi384/btc-trading-bot)

<br/>

### 5. 🏭 KOSHA 작업환경 종합관리 플랫폼 — 공공 SI *(운영 중)*

> **한국산업안전보건공단(KOSHA) 발주** 공공 SI — IoT 기반 화학물질 노출·실내 공기질 모니터링 플랫폼. SI 기업 소속으로 참여해 **4개 모듈을 화면부터 DB까지 풀스택 구현**.

- 담당: 공지사항 · 자료실 · 팝업관리 · **환기수준 모니터링**(IoT 센서 데이터 조회)
- Java MVC + Spring · MyBatis(페이지네이션·검색) · Xframe5 화면 + 반응형 변환 · 폐쇄망(SVN) 환경 7개월
- **Stack**: `Java` `Spring` `MyBatis` `PostgreSQL` `전자정부 표준 프레임워크` · 🔗 [운영 사이트](https://chemsol.kosha.or.kr/)

---

## 🧰 그 외 프로젝트

| 프로젝트 | 설명 |
|---|---|
| [`fine`](https://github.com/vittroi384/fine) | 벌금형 소셜 습관 챌린지 앱 MVP — Expo(React Native) + Supabase(RLS·Edge Functions·pg_cron), 스펙 문서·SQL 테스트 포함 |
| [`meal-allergen-checker`](https://github.com/vittroi384/meal-allergen-checker) | 학교 급식 알레르기 자동 판별·알림 시스템 — NEIS 연동, 서버리스(Apps Script), node:test 76건 |
| [`file-auto-sort`](https://github.com/vittroi384/file-auto-sort) | 폴더 실시간 감시 파일 자동 분류 Windows 트레이 유틸 — 연습 모드·되돌리기 등 안전장치 우선 |
| [`script-to-speech`](https://github.com/vittroi384/script-to-speech) | 대본 txt → 순서대로 mp3 변환 데스크톱 TTS (edge-tts/ElevenLabs 2종) |
| [`oci-arm-grab`](https://github.com/vittroi384/oci-arm-grab) | 클라우드 무료 인스턴스 확보 자동 재시도 GitHub Actions 워크플로 |

---

## 📊 GitHub Stats

<div align="center">

<img height="165" src="https://github-readme-stats.vercel.app/api?username=vittroi384&show_icons=true&count_private=true&hide_border=true&include_all_commits=true" alt="GitHub Stats" />
<img height="165" src="https://github-readme-stats.vercel.app/api/top-langs/?username=vittroi384&layout=compact&hide_border=true&langs_count=8&hide=css,html" alt="Top Languages" />

</div>

---

## 📫 Contact

- 📧 **Email**: jjook924@gmail.com
- 📝 **Portfolio (Notion)**: https://app.notion.com/p/63f54254ed7848c989b11034b3173e96

<div align="center">
<sub>문제를 발견하고, 시스템으로 만들고, 끝까지 운영합니다.</sub>
</div>
