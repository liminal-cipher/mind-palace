# Team History & Contributors

> Microsoft AI School 9기 3차 프로젝트 · 팀 고민중독 (7인)  
> 참여자: 조윤재 · 지경민 · 김인준 · 이재모 · 김시언 · 오준상 · 오효석  
> 프로젝트 기간: 2026.05.20 ~ 2026.06.25

## Role Overview

| 이름 | GitHub | 담당 | 주요 기여 |
|---|---|---|---|
| **조윤재** | [@liminal-cipher](https://github.com/liminal-cipher) | AI 아키텍처 · 백엔드 총괄 | 기획 및 전체 아키텍처 총괄, GraphRAG 백엔드(FastAPI) 및 라이브 오케스트레이터 구축, 방(K) 자동화·이미지 매칭, Azure Cosmos DB / Blob 영속성 |
| **지경민** | [@jen282](https://github.com/jen282) | 퀴즈 시스템 · PDF 전처리 파이프라인 | 퀴즈 생성기·서버 채점·근거 드로어 전담 개발, 스캔 PDF 정제 및 도표/이미지·캡션 분리 파이프라인 구축, 지도 챗봇 RAG 연동 |
| **김인준** | [@JunK98](https://github.com/JunK98) | BGE 쿼리 라우팅 · GraphRAG 실험 | BGE-M3 쿼리 라우터(Global vs Local 검색 분기) 모듈 개발, Azure Speech 토큰 API 구축, GraphRAG 인덱싱/청킹(overlap200) 및 룸 설계 실험 |
| **이재모** | [@imjml](https://github.com/imjml) | 전처리 프로토타입 · 연상 프롬프트 | 초기 OpenCV 기반 이미지 분리 프로토타이핑, GraphRAG 인덱싱 실험 및 시각 단서 기반 연상 장면 생성 프롬프트 설계 |
| **김시언** | [@happybluebird](https://github.com/happybluebird) | UI/UX · 3D 공간음향 | 초기 전처리/목차 추출 설계, 홈/랜딩 인터랙션, 인룸 퀴즈/챗봇 UI, HRTF 3D 공간음향 시스템 구축 |
| **오준상** | [@PhrenO0](https://github.com/PhrenO0) | 3D 공간 엔진 · UI/UX | 3D 공간 엔진(memory-walk), VWorld 지도·방 입장, GLB 가구 인식·동선·카메라 알고리즘, 기술 설명 페이지 일습 |
| **오효석** | [@ohyoseok92](https://github.com/ohyoseok92) | 3D 에셋 · 시스템 보안 | 3D 방 에셋/프리셋 확보 및 렌더링 성능 최적화, 파일 업로드 보안 전수 방어(Zip Bomb, SSRF, XSS) |

## Individual Contributions

### 조윤재 ([@liminal-cipher](https://github.com/liminal-cipher)) · AI 아키텍처 및 백엔드 총괄

- **역할 및 여정**: 프로젝트 핵심 아이디어('기억의 궁전') 제안 및 AI/백엔드 통합 파이프라인 전체 아키텍처 설계. 한국사 및 AI 교안 데이터셋 검증, 방 개수(K) 자동화 및 임베딩 코사인 유사도 기반 노드-이미지 매칭 알고리즘 구현. FastAPI 기반 라이브 오케스트레이션 서버와 Azure Cosmos DB / Blob 분리 영속성 레이어 구축, Microsoft Entra ID 인증 전환 및 토큰 비용 트래킹 총괄.
- **대표 작업** ([백엔드 리포 242커밋](https://github.com/liminal-cipher/graphrag) / 프론트엔드 리포 58커밋):
  | 영역 | 내용 |
  |---|---|
  | 기획 및 아키텍처 | 핵심 아이디어 제안 및 AI/백엔드 통합 파이프라인 전체 아키텍처 설계 |
  | AI / GraphRAG | 방 개수(K) 자동화 알고리즘, 임베딩(`text-embedding-3-small`) 코사인 유사도 기반 캡션-노드 매칭 |
  | 백엔드 및 인프라 | 비동기 라이브 인제스트 오케스트레이터, Azure Cosmos DB / Blob 분리 저장소 구축, Microsoft Entra 인증 전환 |
  | 서비스 통합 및 UX | 내 서재 실시간 영속화, AI 토큰/비용 사용량 추적 API, 지역 간 데이터 누수 방어, 데모 모드 오버레이 |

### 지경민 ([@jen282](https://github.com/jen282)) · 퀴즈 시스템 및 PDF 전처리 파이프라인

- **역할 및 여정**: 스캔 PDF 텍스트/도표 정제 파이프라인(MinerU, Azure Content Understanding, DocLayout-YOLO) 구축 및 이미지-캡션 분리 로직 고도화. GraphRAG 스냅샷 기반 퀴즈 생성기(`quiz_generator.py`), 서버 사이드 채점 및 정답 은닉 API(`quiz_page.py`), 우측 슬라이드 근거 드로어(Evidence Drawer), 퀴즈 프론트 위젯 연동 전담 개발 및 메인 지도 뷰 챗봇 RAG 연동.
- **대표 작업**:
  | 영역 | 내용 |
  |---|---|
  | 퀴즈 시스템 | `quiz_generator.py`, `quiz_page.py`, 서버 사이드 채점(OX/객관식/주관식), 근거 드로어(Evidence Drawer) 구현 |
  | PDF 전처리 | 스캔 PDF 정제, 이미지-캡션 분리 로직 고도화, 전처리 파이프라인 통합 |
  | 서비스 연동 | 지도 뷰 챗봇 GraphRAG 연동, 퀴즈 위젯 이벤트 핸들링 및 UI 버그 수정 |

### 김인준 ([@JunK98](https://github.com/JunK98)) · BGE 쿼리 라우팅 및 GraphRAG 실험

- **역할 및 여정**: 사용자 질의 유형(요약/비교 질문 vs 특정 개념 질문)을 분류하여 Global Search와 Local Search로 분기하는 BGE-M3 쿼리 라우팅 모듈(`routing_bge.py`, `graphrag_search_client.py`) 개발. 프론트엔드 TTS 연동을 위한 Azure Speech 인증 토큰 발급 API(`/api/speech-token`) 구축. `overlap200` 청킹, 프롬프트 엔지니어링, 커뮤니티 병합(`merge_communities.py`) 등 GraphRAG 인덱싱 대규모 실험 및 검증 수행.
- **대표 작업**:
  | 영역 | 내용 |
  |---|---|
  | 쿼리 라우팅 | BGE-M3 쿼리 라우터(Global vs Local 검색 지능형 분기) 모듈 개발 |
  | API 인프라 | Azure Speech 인증 토큰 발급 엔드포인트(`/api/speech-token`) 구축 |
  | GraphRAG 실험 | `overlap200` 청킹, 프롬프트 튜닝, 커뮤니티 병합 및 룸 디자인 실험 |

### 이재모 ([@imjml](https://github.com/imjml)) · 전처리 프로토타입 및 연상 프롬프트

- **역할 및 여정**: 프로젝트 초기에 OpenCV 기반 겹친 이미지 분리 및 캡션 추출 프로토타이핑(`crop_scan_images.py`) 수행. 이후 GraphRAG 인덱싱 실험 및 퀴즈 초기 프로토타이핑에 참여하였으며, 3D 방 속 가구/오브젝트의 시각적 특징과 학습 개념을 엮어주는 시각 단서 기반 연상 장면 생성 프롬프트(Mnemonic Prompt) 설계.
- **대표 작업**:
  | 영역 | 내용 |
  |---|---|
  | 전처리 PoC | OpenCV 기반 스캔 PDF 이미지 분리 및 캡션 추출 프로토타입 |
  | 연상 프롬프트 | 3D 오브젝트 시각 단서-학습 개념 매핑 연상 장면 생성 프롬프트 설계 |
  | 파이프라인 실험 | GraphRAG 인덱싱 및 퀴즈 생성 구조 초기 검증 |

### 김시언 ([@happybluebird](https://github.com/happybluebird)) · UI/UX 및 3D 공간음향

- **역할 및 여정**: 프로젝트 초기 데이터 전처리 및 목차 추출 파이프라인 초안(DI + GPT) 설계. 이후 프론트엔드/UI 전담으로 전환하여 홈/랜딩 인터랙션(히어로, 시네마틱 입장 영상, FAQ, 체험 순서), 인룸 퀴즈 설정 UI 및 `quiz-widget.js` 연동, 3D 공간 내 입장점 기준 HRTF 3D 공간음향 시스템 구축.
- **대표 작업**:
  | 영역 | 내용 |
  |---|---|
  | 홈/랜딩 UI | 시네마틱 입장 영상, 체험 순서 가이드, 히어로 및 랜딩 인터랙션 |
  | 퀴즈/챗봇 UI | 인룸 퀴즈 설정 UI 및 위젯 연동, 챗봇 인터페이스 개선 |
  | 오디오 시스템 | HRTF 3D 공간음향 및 엔티티 카드 오디오 내레이션 연동 |

### 오준상 ([@PhrenO0](https://github.com/PhrenO0)) · 3D 공간 엔진 및 UI/UX

- **역할 및 여정**: 기억의 궁전 1인칭 워크스루 엔진(memory-walk) 구축. 겹친 마커의 황금각 나선 배치 및 세로 층 분리, VWorld 지도와 3D 방 전환 연동, GLB 방 가구 인식·AABB 좌표·1인칭 동선 및 카메라 알고리즘 개발. 랜딩 설득 골격 설계 및 기술 설명 인터랙티브 페이지 일습(3D 워크스루 10스텝, `how-it-all-works`, `pipeline-overview`) 제작.
- **대표 작업**:
  | 영역 | 내용 |
  |---|---|
  | 3D 공간 엔진 | 황금각 나선 마커 분산, GLB 가구 인식 및 AABB 중심 좌표·동선 생성 |
  | 3D 워크스루 | 1인칭 카메라 워크스루, VWorld 지도 ↔ 3D 룸 전환 인터랙션 |
  | 기술 문서화 | 인터랙티브 3D 기술 설명 페이지 4종 및 통합 내비게이션 구축 |

### 오효석 ([@ohyoseok92](https://github.com/ohyoseok92)) · 3D 에셋 및 시스템 보안

- **역할 및 여정**: 3D 방 에셋 및 프리셋 대량 확보/최적화, 종로 및 전국 랜드마크 마커 적용, `memory-walk` 렌더링 성능 최적화(그림자맵 정적화, 조작 시 렌더링). 외부 에셋 임포트 시 발생 가능한 Zip Bomb, SSRF, 이미지 디컴프레션 폭탄 방어, Stored XSS 출력 인코딩 및 GitHub Actions 보안 CI 파이프라인 구축.
- **대표 작업**:
  | 영역 | 내용 |
  |---|---|
  | 3D 에셋/최적화 | 방/프리셋 에셋 파이프라인 구축, 3D 렌더링 부하 최적화 |
  | 시스템 보안 | Zip Bomb(1026:1 차단), SSRF, Pillow 이미지 폭탄 차단 |
  | 웹 보안 및 CI | Stored XSS 방어, bandit/pip-audit/gitleaks/OWASP ZAP 보안 CI 구축 |

## Key Decisions & Architecture Pivots

1. **도메인 특화 및 신뢰성 검증 중심 전환 (05-27 멘토링)**:
   - 클러스터링 기반 RAG 배치의 신뢰성을 확보하기 위해 한국사 및 AI 교안으로 도메인을 좁혀 검증하고, 책임 있는 AI 6원칙(투명성, 공정성, 신뢰성 등)을 전수 수립.
2. **방 구성 3계층 구조 확정 (05-28)**:
   - 무한 확장성과 동선 직관성을 절충하기 위해 `1분류(오픈공간) → 2분류(건물 랜드마크) → 3분류(방/가구 오브젝트)` 3단계 계층 구조 채택.
3. **파이프라인 아키텍처의 GraphRAG 네이티브 전환**:
   - 직접 조립형 파이프라인(DI + 클러스터링)에서 Microsoft GraphRAG(엔티티-관계 지식그래프 + 커뮤니티 리포트)를 코어 엔진으로 채택하고, 목차 기반 방 경계 고정 및 위치 기반 배치로 결정론적 안정성 확보.
4. **한옥 프리셋에서 실제 GPS 랜드마크 마커로 전환 (06-09)**:
   - 도로변 한옥 배치 대신 VWorld 실제 건물 GPS 좌표를 활용한 명소 마커로 전환하여 장소법의 실재감과 현실 학습 시나리오 강화.
5. **RAG Global 검색 채택 및 정직한 거절 원칙 수립**:
   - 답변 품질 및 거시적 맥락 연결을 위해 Global Search를 우선 채택(응답 7~8초)하고, 지식그래프에 근거가 없는 질문에는 환각 없이 한국어로 솔직하게 거절하는 책임성 로직 적용.

## Project Timeline

- **1주차 (05-20 ~ 05-22)**: 아이데이션 및 '기억의 궁전' 프로젝트 주제 확정, 아키텍처 초안 수립.
- **2주차 (05-26 ~ 05-29)**: 멘토 피드백 반영, GraphRAG 및 Three.js 도입 확정, 역할 분담 및 데이터셋 선정.
- **3주차 (06-01 ~ 06-05)**: VWorld 지도 경량화, 3D 에셋 가구 인식 테스트, GraphRAG 샘플 인덱싱 및 텍스트 추출 도구 비교.
- **4주차 (06-08 ~ 06-12)**: 1인칭 워크스루(황금각 나선 마커) 구현, LLM 기반 목차 추출 전환, 방 개수(K) 자동화, 이미지 분리 PoC.
- **5주차 (06-15 ~ 06-19)**: Global RAG 채택, 백엔드 라이브 오케스트레이터 구축, PDF 전처리 파이프라인 통합, 퀴즈 생성기 개발, 보안 전수 방어, 책임 있는 AI 점검.
- **6주차 (06-22 ~ 06-25)**: Azure Cosmos DB / Blob 영속성 및 Entra ID 인증 전환, HRTF 3D 공간음향 구축, 기술 설명 인터랙티브 페이지 완성, 배포 및 발표.
