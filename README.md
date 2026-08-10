<div align="center">

# 기억의 궁전 · MIND PALACE

### 자료의 의미 구조를, 걸어다닐 수 있는 3D 공간으로. Azure AI 기반 공간 기억 학습 서비스 「회랑」

![Azure](https://img.shields.io/badge/Azure-AI%20Service-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white)
![Azure OpenAI](https://img.shields.io/badge/Azure%20OpenAI-412991?style=for-the-badge)
![GraphRAG](https://img.shields.io/badge/GraphRAG-Microsoft-2088FF?style=for-the-badge)
![Three.js](https://img.shields.io/badge/Three.js-3D%20Engine-000000?style=for-the-badge&logo=threedotjs&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-Backend-009688?style=for-the-badge&logo=fastapi&logoColor=white)
![Vite](https://img.shields.io/badge/Vite-Frontend-646CFF?style=for-the-badge&logo=vite&logoColor=white)

🔗 **[라이브 데모](https://3d-mindpalace-ai-fxf8dyfqega3hvbp.canadacentral-01.azurewebsites.net/)** &nbsp;·&nbsp; **[GraphRAG 파이프라인 repo](https://github.com/liminal-cipher/mind-palace-graphrag)** &nbsp;·&nbsp; `MS AI School 9기 · 3차 프로젝트` &nbsp;·&nbsp; 팀 **고민중독**

</div>

## Overview

기억의 궁전(회랑)은 학습 자료(PDF·노트)를 **걸어다닐 수 있는 3D 기억의 궁전**으로 자동 변환하는 Azure AI 기반 공간 기억 학습 서비스입니다.

사용자가 자료를 올리면, AI가 개념과 관계를 추출해 **GraphRAG 지식그래프**로 구조화하고, 의미가 가까운 개념끼리 '방'으로 묶습니다. 그 방들은 VWorld 3D 지도 위 명소로 떠오르고, 입장하면 가구마다 학습 개념이 배치된 방 내부로 들어갑니다. 사용자는 공간을 **1인칭으로 걸으며 외우고**, 간격 반복으로 복습하며, 챗봇·퀴즈로 근거 기반 확인을 합니다.

핵심은 "AI가 궁전을 만든다"가 아니라 **"공간 구조 자체가 개념의 의미 구조에서 나온다"** 는 데 있습니다. PDF 전처리 → GraphRAG → 3D 공간 생성 → 학습·복습까지 하나의 흐름으로 이어지며, 모든 단계는 책임 있는 AI 6원칙으로 점검했습니다.

## Motivation

사람의 뇌는 '목록'을 그대로 기억하도록 설계되지 않았습니다. 여러 번 읽어도 금세 잊는 이유는 기억이 사라져서가 아니라, **다시 꺼낼 '인출 단서'가 없는 상태**이기 때문입니다. "분명히 봤는데 안 떠오른다"가 그 상태입니다.

`제32조 제1항`, `임진왜란 1592`, `영단어 37개`처럼 평면적인 목록에는 위치 정보가 없어 인출 단서가 빈약합니다. 방대한 분량을 통째로 외워야 하는 학습(수험·자격증·전문 용어)일수록 단순 반복은 비효율적이고, 이것은 **의지의 문제가 아니라 방법의 문제**입니다.

**기억의 궁전(method of loci)** 은 정보에 '위치'를 부여해 경로를 따라 회상하는 고전 기억술입니다. 효과는 신경과학으로 입증됐지만 정작 쓰기 어렵습니다. 효과를 보려면 **분류 → 단서화 → 배치 → 반복**을 사용자가 직접 설계해야 하고, 이 설계 자체가 또 하나의 공부이기 때문입니다. 설계 부담, 진입 장벽, 위치 정보가 없는 평면 자료, 복습 관리의 어려움이 겹쳐 있습니다.

> **회랑의 약속:** 암기를 대신 해주지는 않습니다. 대신 **궁전 설계의 부담을 AI가 집니다.** 사용자는 외우고 복습하는 데만 집중합니다.

### Why Spatial Memory Works

| 근거 | 내용 |
| --- | --- |
| 공간 기억의 신경 기반 | 2014 노벨 생리의학상(O'Keefe·Moser). 장소·격자 세포로 '어디에 있었나'가 오래 남음이 정립 |
| 단서의존 인출 | Tulving & Thomson 1973. 기억은 사라진 게 아니라 인출 '단서'가 있어야 떠오른다 |
| 일반인도 6주 만에 2배 | Dresler et al., *Neuron*(2017). 하루 30분·6주 훈련으로 무작위 단어 회상 **26 → 62개(+138%)**, 4개월 뒤에도 유지 |
| 간격 반복의 효과 | Cepeda et al. 2006 메타분석(184편·317실험). 분산 학습이 몰아치기보다 장기 기억에 일관되게 유리 |

사업 확장 구상(시장·타깃·수익 모델)은 [docs/BUSINESS.md](docs/BUSINESS.md)에 분리해 두었습니다.

## What it does

| 기능 | 설명 | 역할 |
| --- | --- | --- |
| 자료 → 개념·관계 분석 | 텍스트·PDF를 넣으면 AI가 개념·타입·관계(경량 온톨로지)를 추출하고 임베딩 | 입력 이해 |
| 공간 자동 생성 | GraphRAG 구조로 방·복도를 잡고, 클러스터링이 검증·정제, 차원 축소로 배치. 각 개념을 시각 단서로 | 핵심 가치 |
| 사용자 편집 (HITL) | 방·개념을 드래그로 옮기고 단서를 고침. 그 수정은 모델 제약으로 환류 | 신뢰성·책임성 |
| 탐험 + 복습 | 궁전을 1인칭으로 걸으며 외우고, 간격 반복으로 회상 테스트·복습 | 학습·인출 |
| 학습 챗봇 | 근거 있을 때만 답하는 RAG 챗봇 (출처 표시·근거 없으면 거절) | 보조 학습 |
| 퀴즈 | GraphRAG 근거로 출제 → LLM 생성 → 근거 일치 2단 검증 | 인출 강화 |

업로드 한 번이면 2D 설계도 → 3D 워크스루 → 간격 복습 → 챗봇·퀴즈가 하나의 흐름으로 연결됩니다.

| Step | 화면 | 핵심 기능 |
| --- | --- | --- |
| 01 | 메인·창구 챗봇 | 서비스 설명, PDF 제출 유도, 처리 과정 표시 |
| 02 | 도시 3D 지도 | VWorld 위 명소 마커 선택 → 입장 |
| 03 | 2D 설계도 | 방·개념 전체 구조 한눈에 |
| 04 | 3D 워크스루 | 1인칭 WASD로 방을 걸으며 마커 학습 |
| 05 | 간격 복습 | 잊을 때쯤 다시 회상 테스트 |
| 06 | 챗봇·퀴즈 | 근거 기반 질의응답·출제 |

### 대표 화면

**3D 지도**: 위성 지형 위 명소 마커. 마커 클릭 → 건물 줌인 → 입장으로 공간 감각을 유지합니다.
![3D 지도](docs/ui/04-vworld_map.png)

**1인칭 워크스루**: 제품의 심장. 가구마다 번호 핫스팟이 입장 시점 부채꼴 시야 기준으로 매겨집니다.
![1인칭 워크스루](docs/ui/06-memory-walk.png)

**챗봇 RAG 답변**: 한국사 근거로 답하고, 근거가 없으면 거절합니다.
![챗봇 답변](docs/ui/33-assistant-answer.png)

전체 화면 33장(상호작용 상태 포함)과 화면별 의도는 **[docs/GALLERY.md](docs/GALLERY.md)** 에 있습니다.
인터랙티브 기술 설명: [`/legacy/bounding-box-visual.html`](frontend/public/legacy/bounding-box-visual.html)(3D 워크스루 10스텝) · [`/legacy/how-it-all-works.html`](frontend/public/legacy/how-it-all-works.html)(글) · [`/legacy/pipeline-overview.html`](frontend/public/legacy/pipeline-overview.html)(한 장 요약)

## Architecture

업로드 → **전처리 → GraphRAG → 3D 공간 → 복습**, 한 흐름.

### 1. PDF 전처리: 성격에 맞춰 경로 분기

| 갈래 | 처리 | 비고 |
| --- | --- | --- |
| 디지털 PDF | `PyMuPDF`로 텍스트·이미지 객체 로컬 추출 | 빠름·무료, 구조 분리·후처리 생략 |
| 스캔 PDF | `PaddleOCR + Ko-pii` PII 마스킹 → **Azure Content Understanding**(텍스트·레이아웃 마크다운) → `<figure>` 분리 → **DocLayout-YOLO** 미탐 이미지 재검출 | 면적비 게이트로 잡동사니 제외 |
| 공통 | 개인정보 후처리(ko-pii 재검사) → LLM 정제·캡션·목차 | 목차가 방 배치의 기반 |

- *트러블슈팅:* OCR 후보(Docling·MinerU·PyMuPDF)를 직접 비교해 한국어·구조 정확도로 **Content Understanding**을 채택했습니다. 스캔본의 **한글→특수기호 오인식**(한글 특화 OCR 검토), **페이지 전체가 1개 이미지로 잡히는** 오인식(DocLayout-YOLO 재분리)이 핵심 난관이었습니다.

### 2. GraphRAG: 개념·관계 구조화

- 일반 RAG의 약점(흩어진 정보·전체 흐름)을 **개체·관계 지식그래프**로 보완합니다.
- 인덱싱 4단계: 청킹(TextUnit) → 엔티티·관계 추출 → **Leiden 군집화** → community report. 산출물 6개 `.parquet`.
- 목차로 방 경계 고정 → 개념을 첫 등장 위치의 방에 배치 → 루브릭 keep/demote → **방 개수(K) 자동화**(작은 방은 옆 방에 합침) → 이미지를 캡션 임베딩 유사도로 매칭.
- 학습 챗봇 **RAG 라우팅**: **BGE-M3 쿼리 라우터**(`method=auto`)가 질문을 local/global 검색으로 분류, 근거 없으면 거절. 운영에선 답변 질 기준으로 **global 우선 채택(약 7~8초)**. 퀴즈 **2단 검증**(생성→검증 LLM이 근거 확인).

### 3. 3D 엔진: 공간

- **VWorld 국가 3D 지도** 위 명소 마커 → '입장' → 방 내부 전환. (84개 도시 좌표를 카카오맵 재지오코딩 + '이름 일치·도심 거리' 거름망으로 정밀화)
- 방 내부: GLB 방을 받아 **가구 인식 → AABB 중심 3D 좌표 → 걷는 동선 번호 → 학습 개념 배치(장소법)**.
- 상세 알고리즘: **[ARCHITECTURE.md](ARCHITECTURE.md)** (좌표계 정규화·검출 게이트·세그멘테이션·삼각측량·동선·카메라).

<img src="https://3d-mindpalace-ai-fxf8dyfqega3hvbp.canadacentral-01.azurewebsites.net/legacy/shots/naming-result.png" alt="자동 명명 결과. 번호·이름·시점 라벨" width="640" />

### 4. UI/UX · 복습

- **2D 설계도 · 3D 워크스루 · 간격 복습 · 챗봇·퀴즈**를 한 흐름으로.
- 접근성: Azure 음성 + **공간음향(HRTF)**, 읽기 속도·글자 크기·테마, 저사양 모드.

## Tech Stack

| 영역 | 기술 |
| --- | --- |
| **AI · LLM** | Azure OpenAI (**gpt-4.1-mini** 인덱싱·질의 / **GPT-4.1** 비전 사물 명명) · text-embedding-3-small · Microsoft **GraphRAG** (Leiden community report) · **BGE-M3** 쿼리 라우팅 |
| **문서 전처리** | PyMuPDF · Azure Content Understanding · PaddleOCR + Ko-pii(PII) · DocLayout-YOLO |
| **3D 엔진** | Three.js (GLTFLoader+DRACO) · VWorld 3D 지도 · 카카오맵 Geocoding · Azure AI Vision(스캐너) |
| **음성·접근성** | Azure Speech(TTS/STT) · 공간음향(HRTF) |
| **백엔드** | FastAPI BFF: 계정(Cosmos NoSQL)·서재 저장·퀴즈 기록·토큰 사용량 집계 ※ GraphRAG 인덱싱·오케스트레이터·Palace 생성은 별도 repo [mind-palace-graphrag](https://github.com/liminal-cipher/mind-palace-graphrag) |
| **프론트엔드** | Vite · Vanilla JS / legacy HTML |
| **인프라** | Azure App Service · Azure Safety Filter |

## Folder Structure

```
mind-palace/  (팀 정본: PhrenO0/Mindpalace_Microsoft9ai_Thirdprj-)
├─ backend/         FastAPI BFF: 계정(Cosmos)·서재 저장·퀴즈 기록·토큰 집계 (app/, main.py, USER_DB.md)
├─ frontend/        Vite + src/
│  └─ public/legacy/  설명 페이지·3D 워크스루(bounding-box-visual)·방 스캐너·memory-walk
├─ tools/           fetch_city_photos.py (도시 사진 수집)
├─ docs/            GALLERY.md(전체 화면 33장) · BUSINESS.md(사업 구상 원문) · ui/(캡처 원본)
├─ ARCHITECTURE.md  3D 공간 마커 시스템 전체 아키텍처
├─ 3D-PIPELINE-TECHNICAL-SHARE.md · 3D-RECOGNITION-DEEPDIVE.md · HOTSPOT-3D-PIPELINE.md
├─ CONTRIBUTORS.md  팀 역할·사람별 히스토리
└─ deploy-build.ps1 / startup.sh / requirements.txt
```

> **GraphRAG 인덱싱·라이브 오케스트레이터·Palace 생성 파이프라인**은 별도 저장소 [mind-palace-graphrag](https://github.com/liminal-cipher/mind-palace-graphrag)에 있습니다. 이 저장소의 `backend/`는 계정·저장을 담당하는 BFF입니다.

```bash
# 백엔드
pip install -r requirements.txt   # Azure OpenAI/Vision 등은 환경변수 주입 → startup.sh
# 프론트
cd frontend && npm install && npm run dev
# 배포: Azure App Service (deploy-build.ps1)
```

## Results & Limitations

| 항목 | 값 |
| --- | --- |
| 검증 완료 과목 | 한국사 · AI 교안 · 경제 · 회계 감사 (그 외는 GraphRAG 자동 산정) |
| RAG 응답 시간 | global 서치 채택 기준 약 **7~8초** (실측) |
| 처리 용량 | 현재 10MB · 50p 이내 |
| 전처리 정제 예시 | 스캔 1페이지 → figure 19 재크롭 + 6 분리 = 25개 정제 |
| 기억 효과 근거 | 6주 훈련 시 무작위 단어 회상 +138% (Dresler 2017, 외부 문헌) |

**한계를 명시합니다.** 학습 효과(회상률 개선)의 자체 정량 평가는 미측정입니다. 위 기억 효과 수치는 외부 문헌이지 이 서비스의 실측이 아닙니다. 검색 품질은 관련성·근거 충실성 점검 수준이며 벤치마크 수치는 없습니다.

## Team

**고민중독** (MS AI School 9기), 7인이 데이터 전처리부터 책임 있는 AI까지 전 과정을 분담.

| 이름 | 역할 |
| --- | --- |
| **오준상** | 3D 엔진 & UI/UX |
| **오효석** | 3D 엔진 및 보안 |
| **김시언** | UI 및 데이터 전처리 |
| **지경민** | 이미지 및 데이터 전처리 |
| **조윤재** | GraphRAG 및 백엔드 |
| **김인준** | GraphRAG |
| **이재모** | GraphRAG (초기 이미지 전처리) |

## Contributions

| 이름 | 주요 기여 |
| --- | --- |
| 오준상 | VWorld 지도·방 입장, GLB 가구 인식·3D 좌표·동선·카메라(memory-walk), 기술 설명 페이지·통일 내비, 데모 흐름 |
| 오효석 | 프리셋·랜드마크 마커 적용, memory-walk 엔진, 보안(Stored XSS 방어) |
| 김시언 | 홈·챗봇·퀴즈 UI, TTS 공간음향(HRTF), 지도 UX, RAG 챗봇 연동 |
| 지경민 | MinerU 이미지·캡션 추출, 스캔 PDF 정제, "서기" 창구 챗봇, 전처리 파이프라인 |
| 조윤재 | 기획·아키텍처 설계, GraphRAG 백엔드(FastAPI)·라이브 오케스트레이터 구축, 방(K) 자동화·이미지 매칭, Azure Cosmos DB / Blob 기반 상태 영속성 |
| 김인준 | AI 교안 테스트, GraphRAG 인덱싱·검색·요약, 퀴즈 근거 검증 |
| 이재모 | OpenCV 이미지 분리·캡션(초기) → GraphRAG 인덱싱·퀴즈 |

> 사람별 여정·Git 커밋·소감·타임라인 전체는 **[CONTRIBUTORS.md](CONTRIBUTORS.md)** 참조.

## My Role (조윤재)

이 저장소는 팀 정본의 fork이며, 포트폴리오 관점에서 본인 몫을 검증 가능한 증거와 함께 적어 둡니다.

| 영역 | 산출물 | 증거 |
| --- | --- | --- |
| GraphRAG 파이프라인·백엔드 | 인덱싱 실험·최종 구성 채택, 라이브 오케스트레이터, Room 자동화·이미지 매칭, 상태 영속성, 비용 추적 | 별도 저장소 [mind-palace-graphrag](https://github.com/liminal-cipher/mind-palace-graphrag) (259커밋 중 242 본인) |
| 앱 BFF 영속성 레이어 | 사용자 DB(Cosmos NoSQL) `backend/app/cosmos.py`, 서재 Blob 하이브리드 `backend/app/storage.py`, 퀴즈 결과·연상 장면 저장, 토큰 사용량 집계 | 커밋 `bb48f71`·`4e81e84`·`8574dc3`, 설계 문서 [backend/USER_DB.md](backend/USER_DB.md) |
| 저장소 통합 관리 | 팀 PR 24건 리뷰·머지, 데모 모드 온오프, 지역 간 데이터 누수·memory-walk 상태 버그 수정 | PR #1~#24 머지 이력 |

※ 3D 엔진·UI 본체는 오준상의 작업입니다. 전체 분담은 위 Team·Contributions 표를 따릅니다.

## Responsible AI

AI가 핵심인 서비스인 만큼 6대 원칙을 모두 점검했습니다.

| 원칙 | 적용 |
| --- | --- |
| 투명성 | 진행 로그·토큰 사용량 공개 · 근거 없으면 챗봇 거절 · 퀴즈 근거 표시 |
| 개인정보·보안 | ko-pii 이중 차단 · 이미지 마스킹 · 사용자별 DB 파티션 · Zip Bomb/Slip·SSRF 방어 · HTML 이스케이프 |
| 신뢰성·안전성 | 퀴즈 근거 재검증 · 결과 저장(재접속 동일) · 청크 스트리밍 업로드 · 레이트리밋 |
| 공정성 | 전국 랜드마크 · Azure Safety Filter · RAG 품질 정량 평가(관련성·근거 충실성) |
| 책임성 | AI 한계 고지 · 노드명/배치 직접 수정 · 학습 항목 직접 결정 |
| 포용성 | 음성·공간음향 · 스크린리더 접근성 · 글자 크기 · 저사양 모드 |

## Retrospective

- **라이브 인덱싱은 무겁습니다** (GraphRAG 특성). 상태 게이팅과 로딩바로 체감을 눌렀지만, 다시 한다면 사전 인덱싱 캐시와 증분 인덱싱을 먼저 설계할 것입니다.
- **공간 개인화는 후퇴했습니다.** AR 방 스캔·자연어 방 생성은 라이선스·로그인 동선·품질 문제로 보류하고 프리셋 방 + Sketchfab 임포트로 좁혔습니다. 확장한다면 이미 구현된 임포트 경로를 다듬는 쪽이 빠릅니다.
- **스캔 PDF에서 명도·채도가 비슷한 이미지는 분리에 실패합니다.** 전용 분리 모델이 필요합니다.
- **학습 효과를 자체 수치로 재지 못했습니다.** 회상률 전후 비교 같은 최소 실험이 다음 단계입니다.
- 처리 용량(10MB·50p), 플랫폼 확장(앱·DOCX·HWP), 기업 교육 등 확장 구상은 [docs/BUSINESS.md](docs/BUSINESS.md)에 있습니다.

## Status

완료. 팀 개발 2026-05~06, 문서 정리 2026-07~08. 라이브 데모는 Azure 구독이 유지되는 동안 접속 가능합니다.

---

<div align="center">

**자료의 의미 구조를, 걸을 수 있는 공간으로.**

</div>
