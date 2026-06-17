<div align="center">

# 안녕하세요, 데이터 엔지니어 전학수입니다 👋

**흩어진 데이터를 수집·정제·적재해 "바로 쓸 수 있는 형태"로 만드는 파이프라인을 설계하고 운영합니다.**
백엔드(FastAPI · Spring)까지 직접 구현하며, 데이터가 흐르는 **처음부터 끝까지** 책임지는 일을 좋아합니다.

<br/>

![Data Engineering](https://img.shields.io/badge/Focus-Data%20Engineering-4285F4?style=flat-square)
![ETL Pipeline](https://img.shields.io/badge/ETL-Extract·Transform·Load-2088FF?style=flat-square)
![Cloud Native](https://img.shields.io/badge/Cloud-GCP-34A853?style=flat-square)
![Backend](https://img.shields.io/badge/Backend-FastAPI·Spring-009688?style=flat-square)

</div>

---

## 🧭 About

- 🔧 **데이터 파이프라인 설계·운영**에 집중합니다 — 수집(Extract) → 정제(Transform) → 적재(Load) → 품질검사 → 서빙/시각화의 전 과정.
- 🛡 **운영을 의식한 엔지니어링**을 지향합니다: 멱등성(UPSERT) · 재시도(exponential backoff) · 동시성 제어(Lock) · 데이터 품질 검증 · 모니터링/로깅.
- ☁️ **GCP 기반 클라우드 네이티브** 전환에 관심이 많습니다: Cloud Run · BigQuery · Vertex AI · Firestore · Cloud Scheduler.
- 🤝 데이터의 **소비처(REST API · RAG)까지** 백엔드(FastAPI / Java·Spring)로 직접 구현해, 데이터 흐름을 한 줄기로 다룹니다.
- 📝 주요 설계 결정은 **ADR(Architecture Decision Record)** 로 남기고, 레거시도 **점진적으로 고도화(v1 → v2 → v3)** 합니다.

---

## 🧱 Tech Stack

**Languages**

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![Java](https://img.shields.io/badge/Java-ED8B00?style=flat-square&logo=openjdk&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)
![SQL](https://img.shields.io/badge/SQL-025E8C?style=flat-square&logo=postgresql&logoColor=white)

**Data & ETL**

![ETL](https://img.shields.io/badge/ETL%20Pipeline-2088FF?style=flat-square)
![pandas](https://img.shields.io/badge/pandas-150458?style=flat-square&logo=pandas&logoColor=white)
![Apps Script](https://img.shields.io/badge/Google%20Apps%20Script-4285F4?style=flat-square&logo=googleappsscript&logoColor=white)
![Looker Studio](https://img.shields.io/badge/Looker%20Studio-4285F4?style=flat-square&logo=looker&logoColor=white)
![Data Quality](https://img.shields.io/badge/Data%20Quality-00897B?style=flat-square)

**Cloud — Google Cloud Platform**

![Google Cloud](https://img.shields.io/badge/Google%20Cloud-4285F4?style=flat-square&logo=googlecloud&logoColor=white)
![Cloud Run](https://img.shields.io/badge/Cloud%20Run-4285F4?style=flat-square&logo=googlecloud&logoColor=white)
![BigQuery](https://img.shields.io/badge/BigQuery-669DF6?style=flat-square&logo=googlebigquery&logoColor=white)
![Vertex AI](https://img.shields.io/badge/Vertex%20AI-4285F4?style=flat-square&logo=googlecloud&logoColor=white)
![Firestore](https://img.shields.io/badge/Firestore-FFCA28?style=flat-square&logo=firebase&logoColor=black)

**Backend**

![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)
![Spring](https://img.shields.io/badge/Spring-6DB33F?style=flat-square&logo=spring&logoColor=white)
![MyBatis](https://img.shields.io/badge/MyBatis-DC382D?style=flat-square)
![eGovFrame](https://img.shields.io/badge/전자정부%20표준%20프레임워크-003876?style=flat-square)

**Database & Infra**

![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![SQLite](https://img.shields.io/badge/SQLite-003B57?style=flat-square&logo=sqlite&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat-square&logo=linux&logoColor=black)
![Git](https://img.shields.io/badge/Git-F05032?style=flat-square&logo=git&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white)

> 🌱 **학습/관심**: Airflow · dbt · Great Expectations · Terraform — 직접 만든 파이프라인의 각 단계를 실무 표준 도구로 옮기는 중입니다.

---

## 🚀 주요 프로젝트

데이터 파이프라인을 중심으로, 그 데이터를 소비하는 백엔드/AI 까지 다룹니다.

### 1. 📊 실시간 암호화폐 데이터 파이프라인 + 자동매매 봇

> **업비트 시세를 수집 → 저장 → 가공 → 품질검사 → 분석/시각화하는 ETL 파이프라인.** 별도 인프라 없이 Python + SQLite 단일 노드로 동작하도록 설계.

- **핵심 엔지니어링**
  - **멱등 수집**: UPSERT 로 캔들 적재 → 재실행해도 중복 없음
  - **변환**: 원본 시세에서 지표 계산(이동평균 · RSI · 볼린저 · 일목) 후 별도 테이블 적재
  - **데이터 품질검사**: 빠진 봉 · 결측치 · 신선도 점검 → 이상 시 텔레그램 알림
  - **오케스트레이션**: 수집→가공→품질을 순서대로(DAG 형태) 주기 실행 + 실패 처리·로깅
  - **서빙/운영**: matplotlib 리포트(PNG) · Flask 대시보드 · systemd 24시간 무중단 · GitHub Actions CI
- **설계 관점**: 각 단계를 실무 도구와 **1:1로 매핑**해 설계 — SQLite↔TimescaleDB, 오케스트레이터↔Airflow, 변환↔dbt, 품질검사↔Great Expectations, 리포트↔Grafana
- **Stack**: `Python` `SQLite` `pandas` `matplotlib` `Flask` `systemd` `Oracle Cloud VM` `GitHub Actions`
- 👤 **역할**: 단독 설계·개발 · 🔗 [`btc-trading-bot`](https://github.com/vittroi384/btc-trading-bot)

> ⚠️ 이 프로젝트의 핵심은 *매매 수익*이 아니라 **데이터 파이프라인 설계·운영**입니다.

<br/>

### 2. 🏛 입찰공고 자동화·시각화 ETL 파이프라인 *(사내 운영 중)*

> **6개 정부 부처/기관**(조달청 · 기업마당 · 보조금24 · e나라도움 · K-Startup · KOCCA)의 입찰/지원사업 공고를 자동 수집·정제·시각화하는 **사내 ETL 파이프라인(v2.0)**. 현재 영업팀이 실사용 중.

- **핵심 엔지니어링**
  - **Extract**: 6개 공공 Open API 를 6시간 주기로 호출, API 장애 시 트랙별 격리(try-catch) + exponential backoff 재시도(3회)
  - **Transform**: 기관별 제각각인 필드명·날짜 포맷을 **단일 스키마로 정규화**, 키워드 필터링 + 카테고리 자동 태깅, **Set 기반 중복 제거**
  - **Load**: Google Sheets **Batch Insert(setValues)** 로 일괄 적재 → 반복 쓰기 대비 실행 시간 단축
  - **운영 안정화**: 자격증명 분리(`PropertiesService`) · 트리거 중복 실행 방지(`LockService`) · 90일 경과 데이터 자동 정리 · 실행 로그 시트로 모니터링
- **성과**: 영업팀 수동 검색 시간 **일 1~2시간 → 0시간**, 누락 공고 차단으로 신규 수주 기회 확대
- **진화**: v1.0 → v1.5 → v2.0 점진적 고도화 / **v3.0 계획** — Cloud Run(FastAPI) · Cloud Scheduler · BigQuery 로 클라우드 네이티브 이전
- **Stack**: `Google Apps Script` `Google Sheets` `Looker Studio` `REST API` `JSON`
- 👤 **역할**: 단독 기획·개발·운영 · 🔒 *비공개 저장소 (요청 시 공유)*

<br/>

### 3. 🤖 Drive RAG 챗봇 — 사내 문서 기반 질의응답

> **사내 Google Drive / GCS 문서를 근거로만 답변하는 RAG 챗봇.** "없는 내용 지어내기(환각)"를 줄이는 데 초점을 둔 클라우드 네이티브 백엔드.

- **핵심 엔지니어링**
  - **하이브리드 검색**: 공용 문서(Vertex AI Search) + 개인 문서(OAuth Drive)를 함께 검색
  - **검색 백엔드 추상화**: `DocumentSearchService` ABC 뒤로 구현을 은닉 → 백엔드 교체를 **설정 한 줄(`SEARCH_MODE`)** 로 처리
  - **RAG 파이프라인**: 후보 top-20 → Gemini re-rank top-5 → 생성 → **답변 검증 레이어**
  - **데이터 분리**: Firestore(실시간 대화) + BigQuery(분석) / **ADR 기반 설계** · slowapi rate limit · OAuth 2.0 · pytest · ruff · mypy · CI
- **Stack**: `FastAPI` `Python 3.11 (async)` `Vertex AI` `Gemini` `Firestore` `BigQuery` `Docker` `Cloud Run` `GCP`
- 👤 **역할**: 단독 설계·개발 *(개발 진행 중)* · 🔒 *비공개 저장소 (요청 시 공유)*

<br/>

### 4. 🏭 KOSHA 작업환경 종합관리 플랫폼 — 공공 SI *(운영 중)*

> **한국산업안전보건공단(KOSHA) 발주, 계약금액 13.95억** 규모 공공 SI 사업. IoT 기반 화학물질 노출·실내 공기질 실시간 모니터링 플랫폼. (주)아이티아이즈(코스닥 372800) **인턴**으로 참여해 4개 모듈을 풀스택 구현.

- **담당 모듈** (화면~DB 풀 사이클): 공지사항 · 자료실 · 팝업관리 · **환기수준 모니터링**(사업장별 IoT 센서 데이터 조회)
- **작업 범위**: Java MVC + Spring(Controller/Service/VO/DTO) · MyBatis 쿼리(페이지네이션·검색) · Xframe5 화면 + 반응형 변환 · 첨부파일 처리
- **트러블슈팅**: 문서가 부족한 Xframe5 HTML 에디터의 저장 방식을 디버깅으로 규명, XSS 위험을 인지해 **관리자 권한 분리로 완화**
- **환경**: 정보누출금지대상 사업(폐쇄망 · SVN · 인터넷 차단 노트북 · 보안서약)에서 7개월 수행
- **Stack**: `Java` `Spring` `MyBatis` `PostgreSQL` `Xframe5` `전자정부 표준 프레임워크` `SVN`
- 👤 **역할**: 인턴 / 풀스택(4개 모듈) · 🔗 [운영 사이트](https://chemsol.kosha.or.kr/)

---

## 📊 GitHub Stats

<div align="center">

<img height="165" src="https://github-readme-stats.vercel.app/api?username=vittroi384&show_icons=true&count_private=true&hide_border=true&include_all_commits=true" alt="GitHub Stats" />
<img height="165" src="https://github-readme-stats.vercel.app/api/top-langs/?username=vittroi384&layout=compact&hide_border=true&langs_count=8" alt="Top Languages" />

<br/>

<img src="https://streak-stats.demolab.com/?user=vittroi384&hide_border=true" alt="GitHub Streak" />

</div>

---

## 📫 Contact

- 📧 **Email**: jjook924@gmail.com
- 📝 **Portfolio (Notion)**: https://app.notion.com/p/63f54254ed7848c989b11034b3173e96
- 🌐 **운영 사이트(KOSHA)**: https://chemsol.kosha.or.kr/

<div align="center">
<sub>데이터의 처음부터 끝까지 — 수집하고, 정제하고, 흐르게 만듭니다.</sub>
</div>
