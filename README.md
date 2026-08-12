# 회랑 (Mind Palace)

> 자료의 의미 구조를, 걸어다닐 수 있는 3D 공간으로. Azure AI 기반 공간 기억 학습 서비스.

![Azure](https://img.shields.io/badge/Azure-AI%20Service-0078D4?logo=microsoftazure&logoColor=white)
![Azure OpenAI](https://img.shields.io/badge/Azure%20OpenAI-412991)
![GraphRAG](https://img.shields.io/badge/GraphRAG-Microsoft-2088FF)
![Three.js](https://img.shields.io/badge/Three.js-3D%20Engine-000000?logo=threedotjs&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-Backend-009688?logo=fastapi&logoColor=white)
![Vite](https://img.shields.io/badge/Vite-Frontend-646CFF?logo=vite&logoColor=white)

Microsoft AI School 9기 3차 프로젝트 · 팀 고민중독 (7인) · 2026.05 ~ 06

[라이브 데모](https://3d-mindpalace-ai-fxf8dyfqega3hvbp.canadacentral-01.azurewebsites.net/) · [GraphRAG 파이프라인 repo](https://github.com/liminal-cipher/mind-palace-graphrag)

## Motivation

사람의 뇌는 '목록'을 그대로 기억하도록 설계되지 않았다. 여러 번 읽어도 금세 잊는 이유는 기억이 사라져서가 아니라, **다시 꺼낼 '인출 단서'가 없는 상태**이기 때문이다. "분명히 봤는데 안 떠오른다"가 그 상태다.

`제32조 제1항`, `임진왜란 1592`, `영단어 37개`처럼 평면적인 목록에는 위치 정보가 없어 인출 단서가 빈약하다. 방대한 분량을 통째로 외워야 하는 학습(수험·자격증·전문 용어)일수록 단순 반복은 비효율적이고, 이것은 **의지의 문제가 아니라 방법의 문제**이다.

**기억의 궁전(method of loci)** 은 정보에 '위치'를 부여해 경로를 따라 회상하는 고전 기억술이다. 효과는 신경과학으로 입증됐지만 정작 쓰기 어렵다. 효과를 보려면 **분류 → 단서화 → 배치 → 반복**을 사용자가 직접 설계해야 하고, 이 설계 자체가 또 하나의 공부이기 때문이다. 설계 부담, 진입 장벽, 위치 정보가 없는 평면 자료, 복습 관리의 어려움이 겹쳐 있다.

> **회랑의 약속:** 암기를 대신 해주지는 않는다. 대신 **궁전 설계의 부담을 AI가 진다.** 사용자는 외우고 복습하는 데만 집중한다.

핵심은 "AI가 궁전을 만든다"가 아니라 **"공간 구조 자체가 개념의 의미 구조에서 나온다"** 는 데 있다. 방의 경계도, 개념의 배치도 자료를 읽어 만든 구조에서 파생된다.

### Why Spatial Memory Works

| 근거 | 내용 |
| --- | --- |
| 공간 기억의 신경 기반 | 2014 노벨 생리의학상(O'Keefe·Moser). 장소·격자 세포로 '어디에 있었나'가 오래 남음이 정립 |
| 단서의존 인출 | Tulving & Thomson 1973. 기억은 사라진 게 아니라 인출 '단서'가 있어야 떠오른다 |
| 일반인도 6주 만에 2배 | Dresler et al., *Neuron*(2017). 하루 30분·6주 훈련으로 무작위 단어 회상 **26 → 62개(+138%)**, 4개월 뒤에도 유지 |
| 간격 반복의 효과 | Cepeda et al. 2006 메타분석(184편·317실험). 분산 학습이 몰아치기보다 장기 기억에 일관되게 유리 |

사업 확장 구상(시장·타깃·수익 모델)은 [docs/BUSINESS.md](docs/BUSINESS.md)에 분리해 두었다.

## What It Does

자료를 올리면 AI가 개념과 관계를 추출해 **GraphRAG 지식그래프**로 구조화하고, 의미가 가까운 개념끼리 '방'으로 묶는다. 그 방들은 VWorld 3D 지도 위 명소로 떠오르고, 입장하면 가구마다 학습 개념이 배치된 방 내부로 들어간다. 사용자는 공간을 **1인칭으로 걸으며 외우고**, 간격 반복으로 복습하며, 챗봇·퀴즈로 근거 기반 확인을 한다.

| 기능 | 설명 | 역할 |
| --- | --- | --- |
| 자료 → 개념·관계 분석 | 텍스트·PDF를 넣으면 AI가 개념·타입·관계(경량 온톨로지)를 추출하고 임베딩 | 입력 이해 |
| 공간 자동 생성 | GraphRAG 구조로 방·복도를 잡고, 클러스터링이 검증·정제, 차원 축소로 배치. 각 개념을 시각 단서로 | 핵심 가치 |
| 사용자 편집 (HITL) | 방·개념을 드래그로 옮기고 단서를 고침. 그 수정은 모델 제약으로 환류 | 신뢰성·책임성 |
| 탐험 + 복습 | 궁전을 1인칭으로 걸으며 외우고, 간격 반복으로 회상 테스트·복습 | 학습·인출 |
| 학습 챗봇 | 근거 있을 때만 답하는 RAG 챗봇 (출처 표시·근거 없으면 거절) | 보조 학습 |
| 퀴즈 | GraphRAG 근거로 출제 → LLM 생성 → 근거 일치 2단 검증 | 인출 강화 |

업로드 한 번이면 2D 설계도 → 3D 워크스루 → 간격 복습 → 챗봇·퀴즈가 하나의 흐름으로 연결된다.

| Step | 화면 | 핵심 기능 |
| --- | --- | --- |
| 01 | 메인·창구 챗봇 | 서비스 설명, PDF 제출 유도, 처리 과정 표시 |
| 02 | 도시 3D 지도 | VWorld 위 명소 마커 선택 → 입장 |
| 03 | 2D 설계도 | 방·개념 전체 구조 한눈에 |
| 04 | 3D 워크스루 | 1인칭 WASD로 방을 걸으며 마커 학습 |
| 05 | 간격 복습 | 잊을 때쯤 다시 회상 테스트 |
| 06 | 챗봇·퀴즈 | 근거 기반 질의응답·출제 |

### 대표 화면

**3D 지도**: 위성 지형 위 명소 마커. 마커 클릭 → 건물 줌인 → 입장으로 공간 감각을 유지한다.
![3D 지도](docs/ui/04-vworld_map.png)

**1인칭 워크스루**: 제품의 심장. 가구마다 번호 핫스팟이 입장 시점 부채꼴 시야 기준으로 매겨진다.
![1인칭 워크스루](docs/ui/06-memory-walk.png)

**챗봇 RAG 답변**: 한국사 근거로 답하고, 근거가 없으면 거절한다.
![챗봇 답변](docs/ui/33-assistant-answer.png)

전체 화면 33장(상호작용 상태 포함)과 화면별 의도는 **[docs/GALLERY.md](docs/GALLERY.md)** 에 있다.
인터랙티브 기술 설명: [`/legacy/bounding-box-visual.html`](frontend/public/legacy/bounding-box-visual.html)(3D 워크스루 10스텝) · [`/legacy/how-it-all-works.html`](frontend/public/legacy/how-it-all-works.html)(글) · [`/legacy/pipeline-overview.html`](frontend/public/legacy/pipeline-overview.html)(한 장 요약)

## Architecture

업로드 → **전처리 → GraphRAG → 3D 공간 → 복습**, 한 흐름.

### 1. PDF 전처리: 성격에 맞춰 경로 분기

| 갈래 | 처리 | 비고 |
| --- | --- | --- |
| 디지털 PDF | `PyMuPDF`로 텍스트·이미지 객체 로컬 추출 | 빠름·무료, 구조 분리·후처리 생략 |
| 스캔 PDF | `PaddleOCR + Ko-pii` PII 마스킹 → **Azure Content Understanding**(텍스트·레이아웃 마크다운) → `<figure>` 분리 → **DocLayout-YOLO** 미탐 이미지 재검출 | 면적비 게이트로 잡동사니 제외 |
| 공통 | 개인정보 후처리(ko-pii 재검사) → LLM 정제·캡션·목차 | 목차가 방 배치의 기반 |

- *트러블슈팅:* OCR 후보(Docling·MinerU·PyMuPDF)를 직접 비교해 한국어·구조 정확도로 **Content Understanding**을 채택했다. 스캔본의 **한글→특수기호 오인식**(한글 특화 OCR 검토), **페이지 전체가 1개 이미지로 잡히는** 오인식(DocLayout-YOLO 재분리)이 핵심 난관이었다.

### 2. GraphRAG: 개념·관계 구조화

- 일반 RAG의 약점(흩어진 정보·전체 흐름)을 **개체·관계 지식그래프**로 보완한다.
- 인덱싱 4단계: 청킹(TextUnit) → 엔티티·관계 추출 → **Leiden 군집화** → community report. 산출물 6개 `.parquet`.
- 목차로 방 경계 고정 → 개념을 첫 등장 위치의 방에 배치 → 루브릭 keep/demote → **방 개수(K) 자동화**(작은 방은 옆 방에 합침) → 이미지를 캡션 임베딩 유사도로 매칭.
- 학습 챗봇 **RAG 라우팅**: **BGE-M3 쿼리 라우터**(`method=auto`)가 질문을 local/global 검색으로 분류, 근거 없으면 거절. 운영에선 답변 질 기준으로 **global 우선 채택(약 7~8초)**. 퀴즈 **2단 검증**(생성→검증 LLM이 근거 확인).

### 3. 3D 엔진: 공간

- **VWorld 국가 3D 지도** 위 명소 마커 → '입장' → 방 내부 전환. (84개 도시 좌표를 카카오맵 재지오코딩 + '이름 일치·도심 거리' 거름망으로 정밀화)
- 방 내부: GLB 방을 받아 **가구 인식 → AABB 중심 3D 좌표 → 걷는 동선 번호 → 학습 개념 배치(장소법)**.
- 상세 알고리즘: **[ARCHITECTURE.md](ARCHITECTURE.md)** (좌표계 정규화·검출 게이트·세그멘테이션·삼각측량·동선·카메라).

<img src="frontend/public/legacy/shots/naming-result.png" alt="자동 명명 결과. 번호·이름·시점 라벨" width="640" />

### 4. UI/UX · 복습

- **2D 설계도 · 3D 워크스루 · 간격 복습 · 챗봇·퀴즈**를 한 흐름으로.
- 접근성: Azure 음성 + **공간음향(HRTF)**, 읽기 속도·글자 크기·테마, 저사양 모드.

### 5. 스택

| 계층 | 구성 |
| --- | --- |
| AI·LLM | Azure OpenAI (gpt-4.1-mini 인덱싱·질의 · GPT-4.1 비전 명명) · text-embedding-3-small · Microsoft GraphRAG · BGE-M3 |
| 문서 전처리 | PyMuPDF · Azure Content Understanding · PaddleOCR + Ko-pii(이중 마스킹) · DocLayout-YOLO |
| 3D·프론트 | Three.js (GLTFLoader+DRACO) · VWorld 3D 지도 · 카카오맵 Geocoding · Azure AI Vision(방 스캐너) · Vite |
| 음성·접근성 | Azure Speech (TTS/STT) · 공간음향(HRTF) |
| 백엔드·인프라 | FastAPI BFF · Azure Cosmos DB · Blob Storage · Azure App Service · Azure Safety Filter |

### 6. repo 구조

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

## Tech Decisions

| 영역 | 선택 | 이유 |
| --- | --- | --- |
| 스캔 PDF 텍스트 추출 | **Azure Content Understanding** | Docling·MinerU·PyMuPDF를 같은 스캔 교과서로 직접 비교했다. 한국어 정확도가 가장 높아 지도·사진 속 한자와 고유명사('도산서원')까지 읽어냈고 띄어쓰기가 원문에 가깝게 보존됐다. 응답 JSON의 `content`에 `figcaption`·`pageHeader`·`table` 태그가 담겨 와 본문과 캡션을 섞지 않고 파싱할 수 있는 것이 결정적이었다 |
| 디지털 PDF 추출 | **PyMuPDF** (로컬) | 텍스트 레이어가 이미 있으면 외부 API를 부를 이유가 없다. 로컬·무료·빠르고, 스캔본에 필요한 구조 분리와 이미지 후처리 단계를 통째로 건너뛰어 시간과 비용을 줄인다 |
| 이미지 재검출 | **DocLayout-YOLO** | 스캔본은 레이아웃이 불규칙해 페이지 전체가 이미지 1개로 잡히거나 둘이 붙어 인식된다. 레이아웃 모델로 재검출한 뒤 검출 개수로 분기하고, 면적비 게이트로 머리글 로고 같은 잡동사니를 걸러낸다 |
| 개념·관계 구조화 | **Microsoft GraphRAG** (Leiden) | 일반 RAG는 흩어진 정보를 모으고 전체 흐름을 잡는 데 약하다. 엔티티·관계 그래프와 community report가 있어야 '방'의 경계를 의미 단위로 자를 수 있다 |
| 인덱싱 모델 | **gpt-4.1-mini** | 모델 4종을 같은 자료로 스윕해 산출물과 비용을 비교한 뒤 채택했다. 사물 명명은 비전이 필요해 GPT-4.1을 따로 쓴다 |
| RAG 라우팅 | **BGE-M3 쿼리 라우터** | 요약·비교 질문은 community report(global), 특정 개념 질문은 entities+relationships(local)로 가야 한다. 라우팅이 어긋나면 자료에 있는데도 답을 못 받는다. global↔local 폴백과 '근거 없으면 거절'을 함께 둔다 |
| 3D 지도 | **VWorld 국가 3D 지도** | 국가 단위 실제 건물 타일을 그대로 쓸 수 있어 장소법의 '실재하는 장소' 감각이 살아난다. 다만 지역마다 정밀도가 달라 엔진 기본 최적화를 두면 건물이 사라져, 디테일을 낮추고 안정성을 택했다 |
| 상태 저장 | **Cosmos DB + Blob** | 인덱싱이 수 분 걸리는 파이프라인이라 서버가 재시작되면 결과가 사라지면 안 된다. 계정·서재·퀴즈 기록은 Cosmos, 산출물은 Blob으로 분리했다 |

> 이 repo의 `backend/`는 계정·저장을 담당하는 BFF이다. GraphRAG 인덱싱·오케스트레이터·Palace 생성은 별도 repo [mind-palace-graphrag](https://github.com/liminal-cipher/mind-palace-graphrag)에 있다.

## Results & Limitations

| 항목 | 값 |
| --- | --- |
| 검증 완료 과목 | 한국사 · AI 교안 · 경제 · 회계 감사 (그 외는 GraphRAG 자동 산정) |
| RAG 응답 시간 | global 서치 채택 기준 약 **7~8초** (실측) |
| 처리 용량 | 현재 10MB · 50p 이내 |
| 전처리 정제 예시 | 스캔 1페이지 → figure 19 재크롭 + 6 분리 = 25개 정제 |
| 기억 효과 근거 | 6주 훈련 시 무작위 단어 회상 +138% (Dresler 2017, 외부 문헌) |

**한계를 명시한다.** 학습 효과(회상률 개선)의 자체 정량 평가는 미측정이다. 위 기억 효과 수치는 외부 문헌이지 이 서비스의 실측이 아니다. 검색 품질은 관련성·근거 충실성 점검 수준이며 벤치마크 수치는 없다.

## Getting Started

라이브 데모는 위 헤더 링크로 바로 접속할 수 있다. 아래는 직접 띄울 때다.

**필요한 Azure 리소스**: OpenAI(gpt-4.1-mini, GPT-4.1, text-embedding-3-small), Content Understanding, AI Vision, Speech, Cosmos DB, Blob Storage. 키와 엔드포인트는 환경변수로 주입하며 `startup.sh`가 읽는다.

```bash
# 백엔드 (FastAPI BFF)
pip install -r requirements.txt

# 프론트엔드
cd frontend && npm install && npm run dev

# 배포: Azure App Service (deploy-build.ps1)
```

GraphRAG 인덱싱과 Palace 생성은 이 repo에 없다. [mind-palace-graphrag](https://github.com/liminal-cipher/mind-palace-graphrag)의 실행 방법을 따로 참고하세요.

## Responsible AI

AI가 핵심인 서비스인 만큼 6대 원칙을 모두 점검했다.

| 원칙 | 적용 |
| --- | --- |
| 투명성 | 진행 로그·토큰 사용량 공개 · 근거 없으면 챗봇 거절 · 퀴즈 근거 표시 |
| 개인정보·보안 | ko-pii 이중 차단 · 이미지 마스킹 · 사용자별 DB 파티션 · Zip Bomb/Slip·SSRF 방어 · HTML 이스케이프 |
| 신뢰성·안전성 | 퀴즈 근거 재검증 · 결과 저장(재접속 동일) · 청크 스트리밍 업로드 · 레이트리밋 |
| 공정성 | 전국 랜드마크 · Azure Safety Filter · RAG 품질 정량 평가(관련성·근거 충실성) |
| 책임성 | AI 한계 고지 · 노드명/배치 직접 수정 · 학습 항목 직접 결정 |
| 포용성 | 음성·공간음향 · 스크린리더 접근성 · 글자 크기 · 저사양 모드 |

## Team & Contributions

7인이 데이터 전처리부터 책임 있는 AI까지 전 과정을 분담했다. 파이프라인 순서로 적는다.

| 이름 | GitHub | 담당 | 주요 기여 |
| --- | --- | --- | --- |
| **지경민** | [@jen282](https://github.com/jen282) | 이미지 · 데이터 전처리 | MinerU 이미지·캡션 추출, 스캔 PDF 정제, "서기" 창구 챗봇, 전처리 파이프라인, 인덱싱·라우팅 실험 |
| **이재모** | [@imjml](https://github.com/imjml) | 전처리 · GraphRAG | OpenCV 이미지 분리·캡션(초기), 인덱싱·퀴즈 실험 |
| **조윤재** | [@liminal-cipher](https://github.com/liminal-cipher) | GraphRAG · 백엔드 | 기획·아키텍처 설계, GraphRAG 백엔드(FastAPI)·라이브 오케스트레이터 구축, 방(K) 자동화·이미지 매칭, Azure Cosmos DB / Blob 기반 상태 영속성 |
| **김인준** | [@JunK98](https://github.com/JunK98) | GraphRAG | AI 교안 테스트, GraphRAG 검색·요약·쿼리 라우팅, 퀴즈 근거 검증 |
| **오준상** | [@PhrenO0](https://github.com/PhrenO0) | 3D 엔진 · UI/UX | VWorld 지도·방 입장, GLB 가구 인식·3D 좌표·동선·카메라(memory-walk), 기술 설명 페이지·통일 내비, 데모 흐름 |
| **오효석** | [@ohyoseok92](https://github.com/ohyoseok92) | 3D 엔진 · 보안 | 프리셋·랜드마크 마커 적용, memory-walk 엔진, 보안(Stored XSS 방어) |
| **김시언** | [@happybluebird](https://github.com/happybluebird) | UI · 데이터 전처리 | 홈·챗봇·퀴즈 UI, TTS 공간음향(HRTF), 지도 UX, RAG 챗봇 연동 |

> 사람별 여정·Git 커밋·소감·타임라인 전체는 **[CONTRIBUTORS.md](CONTRIBUTORS.md)** 참조.

## My Role (조윤재)

| 담당 | 산출물 |
| --- | --- |
| GraphRAG 파이프라인·백엔드 | 인덱싱 최종 구성, 라이브 오케스트레이터, 방(K) 자동화·이미지 매칭, 비용 추적. 별도 repo [mind-palace-graphrag](https://github.com/liminal-cipher/mind-palace-graphrag) (259커밋 중 242) |
| 앱 BFF 영속성 레이어 | 사용자 DB [`backend/app/cosmos.py`](backend/app/cosmos.py), 서재 Blob 하이브리드 [`backend/app/storage.py`](backend/app/storage.py), 퀴즈 결과·연상 장면 저장, 토큰 사용량 집계. 설계 문서 [backend/USER_DB.md](backend/USER_DB.md) |
| repo 통합 관리 | 팀 PR 24건 리뷰·머지, 데모 모드 온오프, 지역 간 데이터 누수·memory-walk 상태 버그 수정 |

## Retrospective

- **라이브 인덱싱은 무겁다** (GraphRAG 특성). 상태 게이팅과 로딩바로 체감을 눌렀지만, 다시 한다면 사전 인덱싱 캐시와 증분 인덱싱을 먼저 설계할 것이다.
- **공간 개인화는 후퇴했다.** AR 방 스캔·자연어 방 생성은 라이선스·로그인 동선·품질 문제로 보류하고 프리셋 방 + Sketchfab 임포트로 좁혔다. 확장한다면 이미 구현된 임포트 경로를 다듬는 쪽이 빠르다.
- **스캔 PDF에서 명도·채도가 비슷한 이미지는 분리에 실패한다.** 전용 분리 모델이 필요하다.
- **학습 효과를 자체 수치로 재지 못했다.** 회상률 전후 비교 같은 최소 실험이 다음 단계이다.
- 처리 용량(10MB·50p), 플랫폼 확장(앱·DOCX·HWP), 기업 교육 등 확장 구상은 [docs/BUSINESS.md](docs/BUSINESS.md)에 있다.

## Status

완료. Microsoft AI School 9기 3차 프로젝트로 2026.05 ~ 06 진행. 라이브 데모는 Azure 구독이 유지되는 동안 접속 가능하다. 마지막 갱신 2026-08-11.
