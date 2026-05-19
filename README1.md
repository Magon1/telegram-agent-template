# 🤖 텔레그램 AI 개인 비서

크립토 BD/Growth/CEO를 위한 24시간 AI 비서. 텔레그램으로 명령하면 
캘린더, 슬랙, Gmail, 텔레그램 DM, PDF/IR덱까지 모두 다룹니다.

## ⚡ 주요 기능

- 📡 **텔레그램 DM/그룹 자동 정리** — 우선순위별 (🔴🟡🟢⚪)
- ☀️ **매일 7시 자동 아침 브리핑** — 캘린더 + 이메일 + 텔레그램 통합
- 🧠 **장기 기억** — 중요 정보 자동/수동 저장 (`/remember`)
- 📚 **문서 검색 (RAG)** — IR덱·딜자료·회의록 자연어 검색
- 💬 **슬랙 통합** — 채널 조회/메시지 발송
- 📅 **캘린더 통합** — 일정 조회/추가, 팀원 캘린더도

## 💰 비용 (1인 기준)

| 항목 | 월 비용 |
|---|---|
| Railway | $5 |
| Anthropic API | $5-10 |
| Pinecone | $0 (Free Tier) |
| Voyage AI | $0 (Free Tier + 카드 등록) |
| **합계** | **약 $10-15/월** |

## 🚀 셋업 방법 (30-60분)

### 추천: Claude.ai와 함께 셋업 ⭐

1. 우상단 **"Use this template"** → 본인 GitHub 계정에 사본 생성
2. [Claude.ai](https://claude.ai) 접속 (Free 플랜 OK)
3. 새 대화 시작
4. 이 레포의 `CLAUDE_PROMPT.md` 내용을 **전부 복사 → Claude.ai에 붙여넣기**
5. Claude가 단계별로 안내해줍니다

설정 도중 막히면 에러 메시지를 Claude에게 보여주면 알아서 해결책 알려줍니다.

## 📂 파일 구조

- `main.py` — 메인 봇 코드
- `requirements.txt` — Python 패키지
- `.env.example` — 환경변수 템플릿 (Railway에 입력할 값)
- `team_context.example.txt` — 팀 정보 템플릿
- `team_context.txt` — **실제 팀 정보 (gitignore됨, 직접 작성)**
- `CLAUDE_PROMPT.md` — Claude.ai 셋업 도우미 프롬프트
- `USAGE_EXAMPLES.md` — 사용 예시

## 🔒 보안

- `.env`, `team_context.txt`는 `.gitignore`에 포함 → GitHub에 안 올라감
- 모든 토큰은 Railway 환경변수로만 관리
- 각자 자기 텔레그램 계정/Google 계정/Slack 토큰 사용

## ❓ 문제 해결

문제 생기면 [Claude.ai](https://claude.ai)에 `CLAUDE_PROMPT.md` 붙여넣고 에러 메시지 보여주세요.
