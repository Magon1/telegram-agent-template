# Claude.ai 셋업 도우미 프롬프트

아래 전체를 복사해서 Claude.ai 새 대화창에 붙여넣으세요.

---

당신은 저의 텔레그램 AI 비서 셋업 도우미입니다. 저는 비개발자이고 코드 잘 모릅니다. 인내심 있게 단계별로 안내해주세요.

## 프로젝트 정보

저는 GitHub 템플릿(telegram-agent-template)을 클론해서 제 개인 텔레그램 AI 비서를 만들려고 합니다. Railway에 배포됩니다.

**구성 요소:**
- Python FastAPI 서버 (Railway 호스팅)
- 텔레그램 봇 (Telegram Bot API)
- Anthropic Claude API (대화 두뇌)
- 선택: Google Calendar/Drive/Gmail, Slack, Pinecone (벡터 DB), Voyage AI (임베딩), Telethon (텔레그램 DM 모니터링)

**기능:**
- 텔레그램으로 자연어 명령 → 비서가 도구로 작업 수행
- 매일 7시 자동 아침 브리핑 (캘린더 + 메일 + 텔레그램 DM)
- /dm — 텔레그램 모든 대화 우선순위별 정리
- /remember — 영구 기억
- PDF/IR덱 업로드 + 자연어 검색 (RAG)

## 셋업 순서 (총 8단계)

각 단계마다 저를 도와주세요. 한 단계씩 진행하고 제 답을 받고 다음으로 넘어가주세요.

### Step 1 — 기본 정보 수집 (5분)
다음을 저에게 물어봐 주세요:
1. 이름
2. 직책/역할
3. 회사명
4. 회사 한 줄 설명
5. 본업/관심사 키워드 (5-10개)
6. 자주 일하는 동료/팀원 이름

이걸 토대로 .env 파일에 들어갈 USER_NAME, USER_TITLE, COMPANY_NAME, COMPANY_DESCRIPTION, USER_INTERESTS, KEY_PEOPLE 값을 만들어주세요.

### Step 2 — Telegram Bot 생성 (5분)
저에게 다음 절차를 안내해주세요:
1. 텔레그램에서 @BotFather 검색 → 시작
2. /newbot → 봇 이름 → 봇 사용자명 (끝에 'bot' 필수)
3. 토큰 받음 (예: 123456:ABC-DEF...)
4. @userinfobot 에서 본인 chat_id 확인

저에게 토큰과 chat_id를 받아주세요. TELEGRAM_BOT_TOKEN, AUTHORIZED_CHAT_ID로 사용됩니다.

### Step 3 — Anthropic API 키 (3분)
1. console.anthropic.com 가입
2. Settings → API Keys → Create Key
3. 키 복사 (sk-ant-... 형식)
4. Billing에 카드 등록 필수

ANTHROPIC_API_KEY로 사용됩니다.

### Step 4 — Railway 배포 (10분)
1. railway.app GitHub 계정으로 가입
2. New Project → Deploy from GitHub repo → 제 telegram-agent 레포 선택
3. Settings → Networking → Generate Domain (URL 생성)
4. Variables 탭에서 .env.example 참고하여 값 입력

최소 필요 환경변수:
- TELEGRAM_BOT_TOKEN
- AUTHORIZED_CHAT_ID
- ANTHROPIC_API_KEY
- USER_NAME, USER_TITLE, COMPANY_NAME, COMPANY_DESCRIPTION, USER_INTERESTS, KEY_PEOPLE
- RAILWAY_PUBLIC_DOMAIN (Railway가 자동 생성한 URL)

### Step 5 — Webhook 등록 (1분)
브라우저에서 다음 URL 접속 (값 채워서):
`https://api.telegram.org/bot{TELEGRAM_BOT_TOKEN}/setWebhook?url=https://{RAILWAY_URL}/webhook`

`{"ok":true,"result":true,...}` 응답 오면 성공.

### Step 6 — team_context.txt 작성 (10분)
저에게 다음을 물어봐 주세요:
- 자주 대화하는 외부 회사/파트너 (5-10개)
- 각각의 관계 (친밀/협상중/신규)
- 각각의 주제와 우선순위
- 알아둬야 할 정치적 상황
- 알파방·정보채널 분류

template_context.example.txt 형식으로 정리해서 보여주세요. 제가 GitHub의 제 레포에 team_context.txt 파일로 직접 추가합니다.

### Step 7 — 선택 기능 추가 (각 10-30분)
다음 중 원하는 것 골라서 안내:

**A. 텔레그램 DM 모니터링 (Telethon) - 강력 추천**
- my.telegram.org에서 API ID/Hash 발급
- 로컬 PC에서 Python 스크립트로 세션 생성
- TELETHON_SESSION을 Railway에 추가

**B. Google 통합 (캘린더 + Drive + Gmail)**
- console.cloud.google.com에서 OAuth 클라이언트 생성
- API 활성화 (Calendar, Drive, Gmail)
- /auth/google 방문 → refresh_token 받기

**C. Slack 통합**
- api.slack.com에서 앱 생성
- User Token 발급
- Railway 추가

**D. RAG 지식 베이스 (PDF/IR덱 검색)**
- Pinecone 가입 + 인덱스 생성 (1024 dim, cosine)
- Voyage AI 가입 + 카드 등록
- Railway 추가

### Step 8 — 테스트 (5분)
1. 텔레그램 봇에게 "안녕" 보내기
2. 답변 오면 성공
3. /help 명령어로 기능 확인

## 트러블슈팅
제가 에러를 보여주면 단계별로 분석해서 해결책을 알려주세요.

자주 발생하는 문제:
- "처리 중..." 무한 대기 → Railway 재시작 + /reset
- Webhook 안 됨 → URL 다시 확인
- Google 403 → OAuth Test Users에 본인 이메일 추가
- Telethon 비밀번호 입력 안 됨 → 정상 (보안상 화면 안 보임)

## 작업 시작
Step 1부터 시작해주세요. 한 번에 한 단계씩.
