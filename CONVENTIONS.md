# 파일·폴더 이름 규칙 (2026 에이전틱 AI 부트캠프)

이 저장소는 GitHub Pages로 정적 배포된다. 배포 서버(Linux)는 **대소문자를 구분**하고 한글 파일명은 URL에서 퍼센트 인코딩(`%EC%98%88...`)되어 링크가 깨지기 쉬우므로, 아래 규칙을 따른다.

## 기본 원칙

1. **영문 소문자 ASCII만** 사용한다. 한글·공백·대문자·언더스코어(`_`) 금지.
2. 단어 구분은 **하이픈(`-`)** — kebab-case.
3. 확장자는 `.html` 소문자.
4. 각 주차 폴더는 `week1/`, `week2/` … 형식이며, 폴더 진입점은 반드시 `index.html`.

## 이름 형식

| 종류 | 형식 | 예시 |
|---|---|---|
| 주차 진입 페이지 | `index.html` | `week1/index.html` |
| 강의자료 | `week{N}-{순번 2자리}-{주제}.html` | `week1-03-js-financial-planner.html` |
| 예시·데모 사이트 | `week{N}-example-{주제}.html` | `week1-example-litigation-dashboard.html` |
| 자율 실습 안내 | `week{N}-assignment.html` | `week2-assignment.html` (주차당 1개, 순번 없음) |

> 자율 실습은 **제출·필수 개념이 없는 선택 활동**이다. 각 주차 `index.html`의 강의 목록 맨 아래에 `[선택]` 뱃지 카드로 링크하고, 하단 💡 노트에서 한 줄로 안내한다. 페이지 안에서도 "제출/과제" 표현 대신 "직접 해보기/자율 실습" 표현을 쓴다.

- `{순번}`은 `01`부터 시작하는 두 자리 숫자. 강의에서 **다루는 순서**와 일치시킨다. (파일 목록이 자연 정렬되도록 두 자리 고정)
- `{주제}`는 내용을 알아볼 수 있는 영문 명사구, 2~4단어 권장. 한국어 제목의 음차(`apdo-jeok-hyogwaseong`)가 아니라 **의미 번역**(`html-effectiveness`)을 쓴다.
- 순번을 나중에 끼워 넣어야 하면 뒤 파일들을 모두 다시 번호 매기고, **다른 파일에서 링크한 경로도 함께 수정**한다.

## 링크 규칙

- 같은 주차 폴더 안에서는 **상대 경로 파일명만** 사용한다: `href="week1-04-html-effectiveness.html"`
- 루트 `index.html` → 주차 페이지도 상대 경로: `href="week1/index.html"` (절대 URL을 쓰면 로컬에서 열 때 깨진다)
- 본문에 파일명을 그대로 노출하지 않는다. 사람이 읽는 제목(예: "HTML의 압도적 효과성")으로 링크한다.

## Week 1 적용 결과 (이름 변경 이력)

| 이전 | 변경 후 |
|---|---|
| `Week1_1_intro_agentic_ai.html` | `week1-01-intro-agentic-ai.html` |
| `Week1_2_personalbrandingworkshop.html` | `week1-02-personal-branding-workshop.html` |
| `Week1_3_JS_financial_planner.html` | `week1-03-js-financial-planner.html` |
| `Week1_4_HTML의_압도적_효과성.html` | `week1-04-html-effectiveness.html` |
| `Week1_5_Cloudflare_도메인연결.html` | `week1-05-cloudflare-custom-domain.html` |
| `예시_소송사건_대시보드.html` | `week1-example-litigation-dashboard.html` |
| `예시_PT_운동관리.html` | `week1-example-pt-workout-tracker.html` |
| `예시_가족여행_플래너.html` | `week1-example-family-trip-planner.html` |

> 참고: 이름 변경 전 `week1-03-...`은 존재하지 않는 `Week1_HTML의_압도적_효과성.html` / `Week1_JS_financial_planner.html`을 링크하고 있었다(번호 접두어가 나중에 붙으면서 링크가 갱신되지 않음). 이번 정리에서 함께 수정했다.

## Week 2 적용 결과 (이름 변경 이력)

| 이전 (초안) | 변경 후 |
|---|---|
| `01_Week2_Cowork_웹스크래핑.html` | `week2-03-cowork-web-scraping.html` |
| `02_Week2_임베딩_추출.html` | `week2-04-embedding-extraction.html` |
| `03_Week2_판결문지도_클러스터링.html` | `week2-05-judgment-map-clustering.html` |
| `04_Week2_Chat_Cowork_Code.html` | `week2-01-chat-cowork-code.html` |
| `05_Week2_검색엔진_키워드vs임베딩.html` | 3주차로 이관 → `week3/week3-02-keyword-vs-embedding-search.html` |
| `06_Week2_임베딩_검색엔진.html` | 3주차로 이관 → `week3/week3-03-embedding-search-engine.html` |
| `07_Week2_RAG_LongContext.html` | 3주차로 이관 → `week3/week3-04-rag-long-context.html` |
| `08_Week2_스킬_제작.html` | `week2-06-building-skills.html` (4주차→3주차를 거쳐 최종 2주차 ⑥으로 — RAG 의존 서술은 제거하고 3주차 예고로 대체) |
| `09_Week2_논문계보도_문헌리서치.html` | `week2-07-citation-genealogy-research.html` (선택 자료) |
| (신규 — `week2-03` §1·§2·§4의 이론부 분리) | `week2-02-web-crawling-theory.html` |
| `자료/Week2_예시_판례분석보고서.html` | `week2-example-workplace-harassment-report.html` |
| `자료/Week2_자료_계보도_AI노동.html` | `week2-example-citation-genealogy-ai-labor.html` |

> 이후 강의 순서를 바꾸면서 `04`(Chat·Cowork·Code — 도구 설명과 설치)를 맨 앞으로 옮기고 기존 `01`~`03`을 한 칸씩 뒤로 밀었다. 순번은 강의에서 다루는 순서를 따르므로, 순서가 바뀌면 파일명·`index.html` 링크·각 페이지의 `STEP N` 표기를 함께 고친다.

> 2026-08 주차 재편성: 검색(키워드 vs 임베딩·검색엔진)과 RAG는 3주차로 이관했다. Week 2는 "수집 → 임베딩 → 지도 → 스킬"(①~⑥ 본편 + ⑦ 선택)이며, 크롤링 이론은 `week2-02-web-crawling-theory.html`로 분리해 신설했다.

> 예시 파일 2개는 각각 `week2-03`·`week2-07`에 base64 data URL로 내장되어 있어 강의 페이지만 열어도 보인다. 저장소에는 단독으로 열어볼 수 있는 원본으로 함께 두되, 주차 `index.html`의 자료 목록에는 넣지 않는다(Week 1의 `week1-example-*` 파일과 같은 취급).

## Week 3 적용 결과 (이름 변경 이력)

| 이전 | 변경 후 |
|---|---|
| (신규 — 옛 `인증·접근 통제·데이터 보안`의 이론부 분리) | `week3-01-privacy-security-auth.html` (이론 오프너) → **강의에서 제외, `drafts/`로 백업** (인증 부분은 추후 ⑥에 통합 예정) |
| (신규 — 2026-08-17) | `week3-01-claude-code-onboarding.html` — STEP 1을 Claude Code 온보딩으로 교체 (git·gh 설치, gh 브라우저 로그인, 폴더 연동, 깃헙 레포 생성, 승인 권한 기준) |
| (2주차에서 이관) `week2-05-keyword-vs-embedding-search.html` | `week3-02-keyword-vs-embedding-search.html` |
| (2주차에서 이관) `week2-06-embedding-search-engine.html` | `week3-03-embedding-search-engine.html` |
| (2주차에서 이관) `week2-07-rag-long-context.html` | `week3-04-rag-long-context.html` |
| (옛 초안) `판례 검색기 Vercel 배포` + `판결문 챗봇을 Vercel로` | `week3-05-vercel-deploy.html` (두 편 통합 — 구글시트 기록부는 4주차 예고로 조정) |
| (옛 초안) `인증·접근 통제·데이터 보안` 실습부 | `week3-06-auth-email-code.html` (대상을 ⑤의 배포 챗봇으로 재서술, §6에 비밀번호 해시 지름길 추가) → 2026-08-17 ⑥ 신설로 `week3-07-auth-email-code.html`로 한 칸 이동 |
| (분리 — 2026-08-17) `week3-04-rag-long-context.html`의 §5~§7 | `week3-06-long-context-hybrid.html` — Long Context·모델 비교·하이브리드는 쟁점이 달라 별도 강의(⑥)로 분리 |
| `week3-04-rag-long-context.html` | `week3-04-rag-chatbot.html` (Long Context 분리 후 RAG 챗봇 실습 중심으로 개명) |
| (신규 — 2026-08-17) | `week3-08-service-logging.html` — 서비스 로그 강의 신설(STEP 8): Supabase 문답 기록, 톱니바퀴 관리자 화면, 해시 하드코딩 |
| (옛 초안) `MCP 커넥터` · `포트폴리오 시트 읽기 전용` · `구글 시트 읽기/쓰기` · `팀 현황판` · `CLI 도구` · `총정리` | 4주차로 이관 (Week 4 표 참조) |

> 2026-08 주차 재편성: 새 Week 3 = "검색엔진과 RAG — 서비스로 만들어 세상에 내놓기" (Claude Code 주간, 자료 8개, STEP 1~8). 스킬 만들기는 4주차→3주차를 거쳐 최종적으로 **2주차 ⑥**에 안착했다(주차별 분량 균형). ③(검색엔진 구축)에 문서화 절(PLAN·DECISIONS·README·CLAUDE.md)을 추가했다.

## Week 4 적용 결과 (이름 변경 이력)

| 이전 | 변경 후 |
|---|---|
| (옛 3주차) `MCP(커넥터) 소개` | `week4-02-mcp-connectors.html` — WEEK 4 STEP 2. 한때 CLI를 §6으로 흡수했다가(`-cli` 접미사), CLI를 별도 강의로 분리하며 파일명에서 접미사 제거 |
| (옛 3주차) `CLI 도구 — 레거시 연결` | `week4-03-cli-tools.html` — 별도 강의로 재신설(STEP 3). 기성 CLI 사용 예시 4종(Google Cloud CLI·ffmpeg·pandoc·ImageMagick)과 레거시 어댑터(결정적 정리 로직 + AI 요약 분업) 3단계 추가 |
| (옛 3주차) `구글 시트 읽기/쓰기 — 서비스 계정` | `week4-04-google-sheets-integration.html` — `tmp-sheets-readonly.html`(웹에 게시 읽기 전용)과 `tmp-team-dashboard.html`(팀 현황판 활용사례)을 흡수해 한 편으로 |
| (옛 3주차) `총정리 — 연동 방식 판단 기준` | `week4-07-integration-decision-guide.html` — 자율 에이전트/루틴 갈래(Q6)와 부트캠프 4주 수료 마무리 추가 |
| (신규) | `week4-01-autonomous-execution-risks.html` (이론 오프너 — 치명적 3요소·인젝션·샌드박스·HITL) |
| (신규) | `week4-05-hermes-agent-setup.html` (에르메스 ① — Hostinger VPS 원클릭 설치·도메인·텔레그램·OpenRouter) |
| (신규) | `week4-06-hermes-agent-routines.html` (에르메스 ② cron 루틴·대시보드) |
| (신규) | `week4/index.html` · `week4-assignment.html` |
| `tmp-cli-tools.html` · `tmp-sheets-readonly.html` · `tmp-team-dashboard.html` | 흡수 후 삭제 |

> 2026-08 주차 재편성: 새 Week 4 = "연동과 자율 에이전트 — AI에게 일을 맡기는 법" (마지막 주차, 자료 7개, STEP 1~7). 스킬 만들기가 2주차로 옮겨갔고, CLI가 ③ 별도 강의로 분리되면서 시트 연동·에르메스·총정리가 ④~⑦로 밀렸다.

## 콘텐츠 규칙

각 강의자료 HTML은 단일 파일(인라인 CSS+JS, 외부 의존성 없음)로 만들고, topbar/사이드바 TOC/진행률 바/완료 체크박스 등 디자인 시스템은 `kaist-bootcamp-html-builder` 스킬 문서를 따른다.
