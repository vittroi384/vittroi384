<div align="center">

# 안녕하세요, 개발자 전학수입니다

**실무의 불편에서 출발해, 설계부터 배포·운영까지 이어지는 시스템을 만듭니다.**
백엔드(FastAPI · NestJS · Next.js) · 데이터 파이프라인 · 클라우드(AWS · GCP · Oracle Cloud)

</div>

---

## Highlights

| | |
|---|---|
| **실사용 시스템** | 사내: 강사 정산(TutorPay) · 입찰공고 ETL · 문서 RAG 챗봇 / 학교: 급식 알레르기 판별(1개교) |
| **행사 운영** | 교육청 축전 스탬프 랠리 — 참여 약 6,100~8,100명(추정) · 도장 6,250건 · 장애 없이 운영 |
| **공개 서비스** | GetQRMaker([getqrmaker.com](https://getqrmaker.com)) · LocalConvert([convert.getqrmaker.com](https://convert.getqrmaker.com)) — 10개 언어 |
| **검증 습관** | 시트 558건 재계산 대조 불일치 0 · 지속 테스트 35,314 요청 에러 0 · 설계 결정은 ADR로 기록 |

---

## Tech Stack

| | |
|---|---|
| **Languages** | ![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white) ![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white) ![Java](https://img.shields.io/badge/Java-ED8B00?style=flat-square&logo=openjdk&logoColor=white) ![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black) ![SQL](https://img.shields.io/badge/SQL-025E8C?style=flat-square&logo=postgresql&logoColor=white) |
| **Backend & Frontend** | ![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white) ![NestJS](https://img.shields.io/badge/NestJS-E0234E?style=flat-square&logo=nestjs&logoColor=white) ![Next.js](https://img.shields.io/badge/Next.js-000000?style=flat-square&logo=nextdotjs&logoColor=white) ![React](https://img.shields.io/badge/React-61DAFB?style=flat-square&logo=react&logoColor=black) ![Spring](https://img.shields.io/badge/Spring-6DB33F?style=flat-square&logo=spring&logoColor=white) |
| **Infra** | ![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white) ![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white) ![Supabase](https://img.shields.io/badge/Supabase-3FCF8E?style=flat-square&logo=supabase&logoColor=white) ![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white) |

---

## 주요 프로젝트

### TutorPay — 강사 배정·급여 정산 시스템 · `사내 실사용`

구글 시트로 관리하던 강사 100여 명, 연 수백 건 강의의 배정·단가 계산·월별 정산을 웹앱으로 옮겼습니다.

- **금액 스냅샷**: 단가표가 바뀌어도 확정된 강의 금액은 그대로. 단가표는 시행일 기준 버전 테이블로 관리
- **시트 → DB 이전 검증**: 시트 값과 재계산 값을 대조하는 추출 스크립트, 558건 불일치 0
- **NestJS 재구현**: 정산 핵심을 REST API로 다시 작성. 월 정산 잠금은 advisory lock으로 직렬화, 감사 로그는 같은 트랜잭션에 기록 (단위 32 · e2e 13 · ADR 3)
- **Stack**: `Next.js 15` `TypeScript` `Drizzle ORM` `PostgreSQL` `NestJS` `TypeORM` `Docker` `AWS`
- 저장소: [`tutor-pay`](https://github.com/vittroi384/tutor-pay) · [`tutorpay-api-nest`](https://github.com/vittroi384/tutorpay-api-nest)

### 부스 QR 스탬프 랠리 — 행사 방문객 앱 + 운영 대시보드 · `2026.10 행사 운영`

교육청 주최 수학·과학 축전(부스 95개)용 웹앱. 부스마다 사람을 두는 대신 고정 QR과 서버 검증으로 도장을 찍고, 완주하면 설문 → 교환권 → 수령까지 앱 안에서 이어집니다.

- **권한 모델**: 로그인 없이 anon 키 하나. 개인정보 테이블은 RLS로 막고 security definer RPC로만 접근
- **치팅 방지는 서버에서**: QR마다 비밀 토큰, 같은 사람 도장 간격 90초
- **결과**: 참여 약 6,100~8,100명(추정) · 도장 6,250건 · 피크 분당 49건을 장애 없이 처리 · 운영 만족도 96%
- **검증**: 행사 전 재현 테스트로 42건 수정 · 지속 테스트 35,314 요청 에러 0, p95 73ms
- **Stack**: `Vanilla JS` `Supabase (Postgres · RPC · RLS)` `Vercel` `Playwright`
- 저장소: [`wonju-stamp-rally`](https://github.com/vittroi384/wonju-stamp-rally)

### GetQRMaker — 무료 QR 코드 생성기 · `공개 서비스` [getqrmaker.com](https://getqrmaker.com)

URL·Wi-Fi·연락처·결제 링크 등 17종을 정적 QR로 만드는 10개 언어 웹서비스. Oracle Cloud 무료 티어 + Cloudflare, 운영비 0원.

- **정적 QR 원칙**: QR에 사용자 내용만 담아 서버가 멈춰도 인쇄물은 계속 동작 (ADR로 기록)
- **관리자 3중 잠금**: 비밀 입구 URL + TOTP 직접 구현 + IP 허용목록
- **검증**: 단위 194 · Playwright E2E 44 · GitHub Actions CI · ADR 9
- **Stack**: `Next.js 16` `TypeScript` `Drizzle ORM` `PostgreSQL` `Docker` `Caddy` `Oracle Cloud`
- 저장소: [`qr-web`](https://github.com/vittroi384/qr-web)

### Drive RAG 챗봇 — 사내 문서 기반 질의응답 · `회사 GCP 운영`

사내 Google Drive / GCS 문서를 근거로만 답하는 RAG 챗봇.

- **파이프라인**: 후보 검색 → Gemini 재정렬 top-5 → 생성 → 근거 여부(grounded) 기록, 답변마다 근거 문서 링크
- **검색 백엔드 추상화**: 인터페이스 뒤로 구현을 숨겨 백엔드 교체를 설정 한 줄로
- **엔지니어링**: ADR 12 · pytest · mypy · Cloud Run / IAP / Secret Manager 배포
- **Stack**: `FastAPI` `Python` `Vertex AI` `Gemini` `Firestore` `Cloud Run`
- 저장소: [`drive-chatbot`](https://github.com/vittroi384/drive-chatbot)

---

## 실무

- **입찰공고 자동화 ETL** · `사내 운영` — 6개 공공기관 Open API를 6시간마다 수집해 단일 스키마로 정규화, 영업팀이 사용. 기관별 장애 격리 + 재시도, 중복 실행 잠금. `Apps Script` `Sheets` `Looker Studio` · 비공개
- **KOSHA 작업환경 종합관리 플랫폼** · `공공 SI` — (주)아이티아이즈 일·학습 병행(2023.08~2024.02). 공지·자료실·팝업·환기수준 모니터링 4개 모듈을 화면부터 DB까지 구현. `Java` `Spring` `MyBatis` `PostgreSQL`

---

## 그 외 프로젝트

| 프로젝트 | 설명 |
|---|---|
| [`file-converter`](https://github.com/vittroi384/file-converter) | LocalConvert([convert.getqrmaker.com](https://convert.getqrmaker.com)) — 파일을 업로드하지 않고 브라우저 안(WebAssembly)에서 변환하는 10개 언어 공개 서비스. 워커 풀·스마트 압축·관측성 구성 |
| [`meal-allergen-checker`](https://github.com/vittroi384/meal-allergen-checker) | 급식 알레르기 자동 판별·알림 — NEIS 식단 자동 대조, 초등학교 1개교 배포, 순수 로직 테스트 78건 |
| [`btc-trading-bot`](https://github.com/vittroi384/btc-trading-bot) | 업비트 시세 수집 → 가공 → 품질검사 데이터 파이프라인 + 모의매매 봇 |
| [`fine`](https://github.com/vittroi384/fine) | 벌금형 소셜 습관 챌린지 앱 MVP — Expo + Supabase(RLS·Edge Functions) |
| [`script-to-speech`](https://github.com/vittroi384/script-to-speech) | 대본 각 줄을 mp3로 만드는 데스크톱 TTS 도구 |
| [`file-auto-sort`](https://github.com/vittroi384/file-auto-sort) | 이름 기반 파일 자동 분류 Windows 트레이 유틸 |
| [`oci-arm-grab`](https://github.com/vittroi384/oci-arm-grab) | 클라우드 무료 인스턴스 확보 자동 재시도 GitHub Actions 워크플로 |

---

## Contact

- **Email**: jjook924@gmail.com
- **Portfolio (Notion)**: https://app.notion.com/p/63f54254ed7848c989b11034b3173e96
