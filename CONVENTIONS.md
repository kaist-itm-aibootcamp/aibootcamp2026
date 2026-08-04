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

## 콘텐츠 규칙

각 강의자료 HTML은 단일 파일(인라인 CSS+JS, 외부 의존성 없음)로 만들고, topbar/사이드바 TOC/진행률 바/완료 체크박스 등 디자인 시스템은 `kaist-bootcamp-html-builder` 스킬 문서를 따른다.
