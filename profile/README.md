# [FinMate] 초보 투자자를 위한 AI 기반 투자 도우미

"삼성전자 요즘 많이 올랐는데 사도 괜찮으려나"     
초보 투자자의 고민에 대해 뉴스, 재무제표를 분석하고 인사이트를 제공하는 AI 에이전트 서비스입니다.

---

## 팀원 소개

| 이름 | 역할 | GitHub |
|------|------|--------|
| **[김남호]** | AI Agent Logic (LangGraph) | [namho](https://github.com/namho1029) |
| **[신재호]** | AI Agent Logic (LangGraph) | [sjho0210](https://github.com/sjho0210) |
| **[안동우]** | Frontend, UI/UX Design| [DongwooAn00](https://github.com/DongwooAn00) |
| **[장성우]** | Backend, Docker | [woo1016](https://github.com/woo1016) |
| **[최형윤]** | Backend, DataBase | [kestrel01360](https://github.com/kestrel01360) |

## 프로젝트 개요

초보 투자자들이 직면하는 '정보의 과잉'과 '분석의 어려움'을 해결하기 위해 기획되었습니다.  
사용자가 특정 종목에 대해 질문하면, AI 에이전트가 실시간 데이터를 수집하고 전설적인 투자자들의 철학을 투영하여 입체적인 분석 결과를 제공합니다.

### 주요 기능
- **🔍 실시간 정보 수집**: 뉴스 및 최신 재무제표 데이터를 에이전트가 자동 탐색
- **⚠️ 리스크 평가**: 단순 추천이 아닌 데이터 기반의 잠재적 리스크 분석
- **💬 인터랙티브 리포트**: 복잡한 지표를 사용자 눈높이에 맞춘 대화형 인터페이스로 제공

## 기술 스택

### Backend
- **Python 3.12+**
- **FastAPI**
- **LangGraph** (Multi-Agent Orchestration)

### Frontend
- **React (Vite)**
- **Figma** (UI/UX Design)

### AI/ML
- **Upstage Solar LLM**
- **LangChain**
- **ChromaDB** (Vector Database)

### Infrastructure
- **Docker**
- **Kubernetes (k3s)**
- **AWS EC2**

## 프로젝트 구조
```
FinMate - Upstage_Project/
├── backend/
│       |
│      app/
│       ├── agents/              # AI 에이전트 로직
│       │   └── subgraphs/      # 에이전트 서브그래프
│       ├── api/                # API 라우터
│       │   └── route/          # API 엔드포인트
│       ├── core/               # 핵심 설정 (DB, LLM, Logger 등)
│       ├── models/             # 데이터 모델
│       │   ├── entities/       # 도메인 엔티티
│       │   └── schemas/        # API 스키마 (Pydantic)
│       ├── repository/         # 데이터 액세스 계층
│       │   ├── client/         # 외부 클라이언트
│       │   └── vector/         # 벡터 DB 레포지토리
│       └── service/            # 비즈니스 로직
│           └── agents/         # 에이전트별 서비스
│
└── frontend/ 
       |
      src/
       ├── api/               # API 
       ├── components/        # 버튼, 입력창같은 작은 컴포넌트
       └── pages/             # 화면단위의 페이지
```




## 아키텍처

저희 서비스는 `Orchestrator`를 중심으로 한 **Multi-Agent** 구조로 설계되었습니다.
<img width="1454" height="834" alt="Image" src="https://github.com/user-attachments/assets/969ca038-f266-42bc-8869-b1808b369ff5" />


## 설치 및 설정

### 1. Python 패키지 설치

```bash
# pyproject.toml 기반 설치
pip install -e .

# 또는 requirements.txt 사용
pip install -r requirements.txt
```

### 2. 환경 변수 설정

`.env.example` 파일을 복사하여 `.env` 파일을 생성하고 필요한 API 키를 입력하세요.

```bash
cp .env.example .env
```

필수 환경 변수:
- `UPSTAGE_API_KEY`: Upstage Solar LLM API 키
- `DART_API_KEY`: 금융감독원 DART API 키
- `NAVER_CLIENT_ID`: 네이버 뉴스 검색 API 클라이언트 ID
- `NAVER_CLIENT_SECRET`: 네이버 뉴스 검색 API 시크릿
- `DATABASE_URL`: PostgreSQL 연결 문자열

### 3. Firebase Admin SDK 설정

`secrets/` 폴더를 생성하고 Firebase Admin SDK JSON 키 파일을 넣어주세요.

```bash
mkdir secrets
# Firebase Console에서 다운로드한 서비스 계정 키를 secrets/ 폴더에 복사
cp /path/to/your-firebase-adminsdk.json secrets/
```

### 4. 데이터베이스 설정

PostgreSQL 데이터베이스를 준비하고 마이그레이션을 실행하세요.

```bash
# Docker로 PostgreSQL 실행 (선택사항)
docker-compose up -d

# 마이그레이션 실행
alembic upgrade head
```

### 5. 서버 실행

```bash
# 개발 서버
uvicorn main:app --reload

# 또는 start.sh 사용 (Linux/Mac)
./start.sh
```

## API 키 발급 안내

- **Upstage Solar API**: https://console.upstage.ai/
- **DART API**: https://opendart.fss.or.kr/
- **네이버 검색 API**: https://developers.naver.com/
- **Firebase**: https://console.firebase.google.com/
