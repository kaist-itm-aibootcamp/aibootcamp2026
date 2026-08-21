---
name: kaist-bootcamp-html-builder
description: Build self-contained HTML teaching pages (intro decks, hands-on workshop pages, and the per-week index page) for the KAIST I&TM "에이전틱 AI 부트캠프" course. Use whenever creating or editing a Week N intro/concept page, a Week N hands-on workshop page, or a Week N index page for this bootcamp, so every week shares the same visual design system, topbar, sidebar-TOC layout, progress/checkbox/celebration mechanics, back-to-index navigation, cross-page narrative flow, and file-naming convention established in Week 1–2.
---

# KAIST I&TM AI 부트캠프 — HTML 교재 제작 스킬

Week 1~2에서 확립한 디자인 시스템·네비게이션·흐름 점검 방식을 정리한 스킬입니다. Week 3~4 교재를 만들 때 이 패턴을 그대로 재사용하세요.

## 산출물 세 종류

1. **인트로/개념 설명 덱** (예: `week1-01-intro-agentic-ai.html`) — 개념을 애니메이션·다이어그램으로 설명하는 문서형 페이지.
2. **실습 워크숍 페이지** (예: `week2-06-embedding-search-engine.html`) — Part별 단계를 따라가며 실습하는 페이지 (workshop-step 카드, 프롬프트 빌더 등 포함).
3. **주차 진입 페이지** (`week{N}/index.html`) — 그 주차 자료를 순서대로 나열하는 목록 페이지. 강의 페이지들과는 **다른 레이아웃**(랜딩형)을 씁니다 — 아래 "주차 index.html" 절 참고.

강의 페이지(1·2)는 모두 **단일 HTML 파일**(인라인 CSS+JS, 외부 의존성 없음)로 만듭니다.

## 파일·폴더 이름 (저장소 `CONVENTIONS.md`가 최종 권위)

GitHub Pages 배포 서버가 대소문자를 구분하고 한글 파일명은 URL 인코딩으로 깨지므로 **영문 소문자 kebab-case**만 씁니다. `Week{N}_` 같은 접두어나 한글 파일명은 쓰지 마세요.

| 종류 | 형식 | 예시 |
|---|---|---|
| 주차 진입 페이지 | `week{N}/index.html` | `week2/index.html` |
| 강의자료 | `week{N}-{순번 2자리}-{주제}.html` | `week2-05-keyword-vs-embedding-search.html` |
| 예시·데모 사이트 | `week{N}-example-{주제}.html` | `week2-example-workplace-harassment-report.html` |

- `{순번}`은 강의에서 **다루는 순서**와 일치. 같은 주차 폴더 안에서는 **파일명만으로 상대 링크**(`href="week2-03-....html"`).
- 초안 파일명이 한글이면 저장소에 넣으면서 개명하고, **`CONVENTIONS.md`의 "Week N 적용 결과" 표에 변경 이력을 추가**합니다.

## 공통 CSS 디자인 토큰 (`:root`)

```css
:root{
  --bg:#f3f6f2; --surface:#ffffff; --ink:#22201d; --muted:#626a64; --line:#d5ddd3;
  --brand:#2e9bdb; --brand-dark:#1b6fa6; --green:#2f765b; --amber:#b8792e; --red:#b0483f;
  --blue:#375f8f; --sky-light:#e3f1fb;
  --shadow:0 16px 45px rgba(54,42,31,.12); --radius:14px; --sidebar-width:250px;
}
```
모든 강의 페이지에서 동일한 변수명을 사용해 색상·간격을 통일합니다.

## 통일된 상단 배너 (topbar) — 반드시 이 구조 그대로 사용

왼쪽 그룹(로고 + WEEK 태그 + **목록으로 돌아가기 칩**) / 오른쪽(진행률 바), 2블록.

```html
<header class="topbar">
  <div class="topbar-left">
    <a href="#top" class="brand">
      <span class="brand-mark">AI</span>
      <span class="brand-text"><strong>KAIST I&amp;TM</strong><small>AI 부트캠프</small></span>
    </a>
    <div class="week-tag"><span class="week-num">WEEK {N}</span><span class="week-title">{페이지별 제목}</span></div>
    <a class="back-week" href="index.html">← {N}주차 목록</a>
  </div>
  <div class="progress-wrap" aria-label="진행률">
    <span class="progress-label"><b id="progressCount">0</b>/<span id="progressTotal">0</span> 완료</span>
    <div class="progress-track"><div class="progress-bar" id="progressBar"></div></div>
  </div>
</header>
```

```css
.topbar{
  position:sticky;top:0;z-index:20;display:flex;align-items:center;justify-content:space-between;gap:18px;
  padding:12px clamp(16px,4vw,32px);border-bottom:1px solid var(--line);
  background:rgba(255,255,255,.92);backdrop-filter:blur(12px);
}
.topbar-left{display:flex;align-items:center;gap:18px;}
.brand{display:inline-flex;align-items:center;gap:12px;text-decoration:none;color:var(--ink);}
.brand-mark{display:grid;width:38px;height:38px;place-items:center;border-radius:9px;color:#fff;background:var(--brand);font-size:15px;font-weight:800;}
.brand-text{display:block;line-height:1.25;}
.brand-text strong{display:block;font-size:14.5px;}
.brand-text small{display:block;margin-top:1px;color:var(--muted);font-size:11.5px;font-weight:600;}
.week-tag{display:flex;align-items:center;gap:8px;}
.week-num{font-size:11px;font-weight:900;letter-spacing:.04em;color:#fff;background:var(--brand-dark);padding:4px 10px;border-radius:999px;white-space:nowrap;}
.week-title{font-size:14px;font-weight:800;color:var(--ink);white-space:nowrap;}
.progress-wrap{width:min(220px,32vw);flex:0 0 auto;}
.progress-label{display:block;margin-bottom:5px;color:var(--muted);font-size:12px;text-align:right;}
.progress-track{overflow:hidden;height:7px;border-radius:999px;background:#e1e8df;}
.progress-bar{width:0;height:100%;border-radius:inherit;background:linear-gradient(90deg,var(--brand),var(--sky-light));transition:width 220ms ease;}
```

모바일 대응(권장):
```css
@media (max-width:900px){ .layout{display:block;} .sidebar{position:static;width:auto;height:auto;border-right:none;border-bottom:1px solid var(--line);} }
@media (max-width:640px){ .topbar{flex-wrap:wrap;row-gap:10px;} .topbar-left{flex-wrap:wrap;row-gap:8px;} .progress-wrap{width:100%;} }
```

브랜드 로고 텍스트("AI"), "KAIST I&TM", 작은 글씨 "AI 부트캠프"는 모든 페이지에서 고정입니다. 바뀌는 건 `WEEK {N}` 숫자와 `week-title`(그 페이지의 제목)뿐입니다. 제목은 짧은 명사구로(예: "Agentic AI 소개", "임베딩 검색엔진 구축"). "도입", "인트로부" 같은 모호한 단어는 피하세요.

## 목록으로 돌아가기 — 모든 강의 페이지에 두 군데 (필수)

주차 폴더의 강의 페이지는 **반드시** 아래 두 개의 귀환 동선을 갖습니다. 하나라도 빠지면 학습자가 목록으로 돌아갈 길이 없습니다.

1. topbar 안의 칩 `<a class="back-week" href="index.html">← {N}주차 목록</a>` (위 topbar 마크업 참고)
2. 본문 맨 끝(`</main>` 직전)의 카드

```html
      <a class="back-home" href="index.html">
        <span class="bh-ic">←</span>
        <span><strong>{N}주차 강의자료 목록으로 돌아가기</strong><small>다음 자료로 이어가려면 목록에서 골라보세요</small></span>
      </a>
```

```css
.back-week{display:inline-flex;align-items:center;gap:6px;padding:5px 12px;border:1px solid var(--line);border-radius:999px;background:#fff;color:var(--muted);font-size:12px;font-weight:700;text-decoration:none;white-space:nowrap;transition:color .15s ease,border-color .15s ease,background .15s ease;}
.back-week:hover{color:var(--brand-dark);border-color:var(--brand);background:var(--sky-light);}
.back-home{display:flex;align-items:center;gap:15px;max-width:840px;margin:34px 0 10px;padding:20px 24px;border:1px solid var(--line);border-radius:var(--radius);background:var(--surface);box-shadow:var(--shadow);text-decoration:none;color:var(--ink);transition:transform .18s ease,border-color .18s ease;}
.back-home:hover{transform:translateY(-2px);border-color:var(--brand);}
.back-home .bh-ic{display:grid;place-items:center;flex:0 0 auto;width:42px;height:42px;border-radius:11px;background:var(--sky-light);color:var(--brand-dark);font-size:19px;font-weight:900;}
.back-home strong{display:block;font-size:15.5px;font-weight:800;}
.back-home small{display:block;margin-top:3px;color:var(--muted);font-size:12.5px;font-weight:600;}
@media (max-width:640px){.back-home{padding:18px;gap:12px;}}
```

## 전체 레이아웃 (topbar 아래)

`.layout`(flex) → `.sidebar`(sticky TOC) + `.content`(main, max-width ~900~920px). 콘텐츠는 `.section`/`.doc-section` 단위로 나뉘고 각 섹션 끝에 `.completion-row` 체크박스를 둡니다. 사이드바는 scroll-spy로 active 링크가 바뀌게 합니다(IntersectionObserver 또는 scroll 리스너).

## 글쓰기 원칙 (강의자 지침 — 초안 검토 시 반드시 적용)

**1. 반드시 필요한 것이 아니면 비유를 쓰지 않는다.** 낯선 개념을 처음 설명할 때만 비유가 값을 합니다. 이미 설명한 것을 다시 비유로 부르거나, 사실을 그대로 쓰면 되는 자리에 비유를 얹으면 정확도만 떨어집니다.

| 쓰지 말 것 | 고쳐 쓸 것 |
|---|---|
| "어느 동네 사건인지가 곧 승률이다" | "클러스터가 소송 결과와 함께 나뉘었다" |
| "재료는 zip 파일 하나, 요청은 문장 하나" | "연동 폴더에 저장된 임베딩 JSON을 쓴다" |
| "텍스트를 '읽는' 대신 '재는' 방법" | "텍스트를 의미의 좌표(임베딩)로 바꾼다" |
| "판별법 10초 테스트" | "확인 방법" |

수사적 제목(`— zip 하나, 문장 하나`)도 같은 기준으로 걷어내고, 그 절이 실제로 무엇을 하는지로 바꿉니다.

**2. 전문 용어가 처음 나오면 그 자리에서 설명한다.** 뒤에서 설명하지 말고, 처음 쓰는 문단 바로 앞·뒤에 `.callout`으로 넣습니다. 제목은 용어 그 자체(`실루엣 계수`, `API 키`)로 답니다. 비개발자 수강생 기준으로 **계산 방법보다 "값을 읽고 무엇을 판단하는지"**를 앞세우세요.

**3. 예시 프롬프트는 기술적으로 쓰지 않는다.** 수강생이 복사해 쓸 프롬프트에 알고리즘 이름·하이퍼파라미터·라이브러리를 지정하지 마세요. **원하는 결과만 서술하고, 계획을 먼저 세우게 하고, 기술적 결정은 AI가 선택지와 함께 물어보게** 하는 형태가 이 부트캠프의 표준입니다.

**3-1. 예시 프롬프트는 짧게 — 실제로 쓰는 것처럼.** (3주차 강의 후 확립) 긴 요구사항 목록이 달린 프롬프트는 수강생에게 장벽이 됩니다. **하고 싶은 것만 2~4줄로 간단히 서술**하고, 구체적 구현·세부 결정은 **AI와의 대화 왕복으로 발전**시키는 흐름을 보여주세요. 항목이 6~7개씩 붙은 "완성 프롬프트"는 만들지 않습니다 — 실제 사용 기록(질문 → 답변 → 재지시)을 보여주는 편이 낫습니다.

```
연동 폴더의 임베딩 JSON 파일들로 클러스터링을 하고,
결과를 지도처럼 한눈에 볼 수 있게 시각화해줘.

바로 실행하지 말고 계획부터 세워서 보여줘. 기술적으로 결정해야 할 것이
있으면 선택지와 함께 알려주고, 내가 고르게 해줘.
```

**4. 실습 데이터는 앞 강의의 산출물을 가리킨다.** "첨부 zip을 올려라" 같은 지시 대신, **앞 강의에서 연동 폴더에 이미 저장해 둔 파일**을 쓰게 합니다. 주차 전체가 폴더 하나를 공유하는 구조이므로, 파일을 다시 올리게 하면 그 구조가 무너집니다.

**5. 자명한 문장은 넣지 않는다.** "폴더를 나눠 두면 파일이 섞이지 않습니다" 같은 문장은 지면만 차지합니다. 수강생이 모를 만한 것, 틀리기 쉬운 것만 씁니다.

## 재사용 컴포넌트 (workshop 페이지)

- `.concept-grid` / `.concept` — 3열 개념 카드
- `.workshop` / `.workshop-step` / `.ws-num` — 번호 붙은 실습 단계 카드
- `.definition-list` — 용어 정의 목록
- `.tip-card` — 왼쪽 파란 테두리 팁 박스
- `.callout`, `.callout.caution`, `.callout.ok` — 안내/주의/확인 박스 (`<b class="cap">제목</b>` 포함)
- `.doc-table` — 비교표
- `.next-card-grid` / `.next-card` — 마무리 다음 단계 안내 카드 (**2열 그리드이므로 카드는 정확히 2개**)
- `.prompt-card` / `.design-field` — 프롬프트 빌더 입력 폼. **드롭다운(select)보다 라디오 버튼 그룹을 기본으로** 사용:
  ```css
  .radio-group{display:flex;flex-direction:column;gap:6px;}
  .radio-option{display:flex;align-items:center;gap:9px;padding:8px 11px;border:1px solid var(--line);border-radius:8px;background:#fafcf9;font-size:13.5px;font-weight:600;cursor:pointer;}
  .radio-option:has(input:checked){border-color:var(--brand);background:var(--sky-light);color:var(--brand-dark);font-weight:800;}
  ```
  자유 서술 항목만 `<input type=text>`로 남기고 나머지는 라디오로 통일합니다.
- `.copy-block` + 복사 버튼 + `.toast` — 프롬프트를 클립보드로 복사 (`navigator.clipboard.writeText`, 실패 시 `document.execCommand('copy')` 폴백)

## 진행률 바 + 완료 체크박스 + 축하 컨페티 (모든 강의 페이지 공통)

- 각 섹션 끝에 `<div class="completion-row"><label class="check"><input type="checkbox" data-progress="{id}" /><span>...</span></label></div>`
- **상태는 메모리(JS 변수)에만 저장** — `localStorage`/`sessionStorage` 절대 사용 금지.
- 체크박스 개수를 세어 topbar의 `progressCount`/`progressTotal`/`progressBar`를 갱신.
- 전부 체크되면 1회 한정 축하 이벤트: 인트로 덱은 `.content` 상단 배너, 워크숍 페이지는 `<canvas>` 컨페티 + 모달. Week 2 방식은 `<body data-celebrate="...">`에 축하 문구를 담아 공통 스크립트가 읽어 쓰는 형태 — **이 문구도 페이지 흐름의 일부**이므로 다음 강의 예고와 어긋나지 않게 씁니다.

## 예시/참고 사이트를 페이지에 내장하는 방법 (라이트박스 패턴)

외부에서 만든 완성된 예시 HTML 파일을 워크숍 페이지 안에 실제로 "내장"하려면:

1. 각 예시 HTML 파일을 `base64 -w0 file.html`로 인코딩해 JS 상수로 넣습니다.
2. `.example-card`에 작은 미리보기 iframe을 넣되, **실제 크기로 렌더링한 뒤 CSS로 축소**합니다:
   ```css
   .example-thumb{position:relative;height:170px;overflow:hidden;background:#111;}
   .example-thumb iframe{position:absolute;top:0;left:0;width:400%;height:400%;transform:scale(.25);transform-origin:top left;border:none;pointer-events:none;}
   ```
   `src="data:text/html;base64,{인코딩값}"` 형태면 외부 파일 없이 자기완결형으로 내장됩니다.
3. 카드를 클릭(또는 Enter/Space)하면 `.example-lightbox` 모달을 열고 같은 data URL을 큰 iframe의 `src`로 설정. 닫을 때 `src`를 `about:blank`로 되돌려 리소스를 해제합니다.
4. 내장한 원본 파일은 `week{N}-example-{주제}.html`로 저장소에도 함께 두되, 주차 `index.html` 목록에는 넣지 않습니다.

---

# 주차 index.html (강의 목록 페이지)

강의 페이지와 **다른 디자인 시스템**을 씁니다 — 어두운 hero가 있는 랜딩형이며, `week1/index.html`을 그대로 복사해 내용만 바꾸는 것이 가장 안전합니다. 사이드바·진행률 바·체크박스는 **없습니다**.

구성 순서:

1. `header.topbar` — 좌측 브랜드(`href="../index.html"`), 중앙 nav-links(`#materials`, `../index.html#curriculum`), 우측 Zoom `nav-cta`.
2. `section.hero` (어두운 navy 그라디언트) — `← 부트캠프 홈으로` 링크, `WEEK {N}` 배지 + 날짜, h1, 리드 문단, `meta-chip` 2~3개(강의자료 개수 / 예제 데이터 / 산출물).
3. `section#materials` — `.section-head` + `.material-list` 안에 `a.material` 카드(`.num` 2자리 번호 + 제목 + `.kind` 배지 + 1~2문장 설명 + `.go` 화살표).
   - 배지: `kind-concept`(개념) / `kind-practice`(실습) / `kind-reading`(읽을거리·체험) / `kind-optional`(선택). 성격이 둘이면 배지 2개를 나란히 답니다.
   - **자료가 6개를 넘으면** `.part-head`(PART 배지 + 소제목 + 부연)로 3~4개씩 묶고, 목록 위에 `.flow-strip`(번호 칩을 화살표로 연결한 한 줄 흐름도)을 둡니다. Week 2가 이 형태입니다.
4. (선택) `section#prep` — 강의 전 준비물 `.prep-grid` 3열. 설치·계정·환경 확인이 필요한 주차에 둡니다.
5. `section` "다음 주차" — 다음 주 예고 + `.note`(이번 주 과제).
6. `footer.site-footer`.

만들고 나면 **루트 `index.html`의 해당 주차 카드**에서 `<span class="material-soon">…추가 예정</span>`을 `<a class="material-link" href="week{N}/index.html">📘 {N}주차 강의자료 보러가기 <span class="arrow">→</span></a>`로 바꾸고, **직전 주차 index의 "다음 주차" 안내문**도 "공개 예정" → 실제 링크로 갱신합니다.

---

# 여러 페이지로 이루어진 한 주차의 흐름 점검 (Week 2에서 확립)

한 주차가 5개 이상의 페이지로 나뉘면 페이지 사이의 **서사 연속성**이 가장 자주 깨집니다. 초안을 받거나 새로 만들 때 아래를 순서대로 점검하세요.

1. **hero-kicker 번호 체계를 하나로.** 페이지마다 `STEP 1`, `데이터 분석 ③`, 아무 번호 없음이 섞이면 학습자가 위치를 잃습니다. `WEEK {N} · STEP {i} — {주제}` 한 형식으로 통일하고 `i`는 파일 순번과 일치시킵니다.
2. **"다음 강의 예고"가 실제 다음 파일을 가리키는가.** 마지막 `.next-card-grid`의 예고 카드, 본문 중간의 "다음 실습은…", `data-celebrate` 문구 세 곳을 모두 확인합니다. 중간 파일이 두 칸 뒤를 가리키거나(그 사이 파일이 없는 것처럼 읽힘), 마지막이 아닌 파일이 "다음 주차 예고"를 달고 있는 경우가 흔한 실수입니다.
3. **다음 주차 예고는 그 주차의 마지막 파일에만.** 중간 파일에는 같은 주차의 다음 강의를 예고합니다.
4. **첫 파일을 제외한 모든 페이지가 앞 강의를 한 문장으로 받는가.** hero 문단에서 "앞 강의에서 만든 …를 재료로" 식의 연결을 답니다.
5. **숫자·고유명사가 페이지를 건너뛰며 일관된가.** 데이터 건수(예: 수집 895건 → 분석 대상 347건), 파일명(예: `openrouterkey.txt`), 모델명, 폴더명은 전 페이지에서 같아야 합니다. 값이 달라지는 지점이 있다면 **왜 달라지는지 설명하는 문단을 넣습니다** — 설명 없이 숫자가 바뀌면 학습자는 자료 오류로 읽습니다.
6. **모든 페이지가 마무리 구조를 갖췄는가.** `final-list`(체크리스트) → `next-card-grid`(다음 강의 예고 + 과제/직접 해보기) → `completion-row` → `back-home`. 한 페이지만 이 중 일부가 빠져 있는 경우가 잦습니다.
7. **주차 index의 그룹 구분이 실제 흐름과 맞는가.** PART 구분선이 내용의 전환점(예: 도구가 Cowork → Claude Code로 바뀌는 지점)과 일치해야 합니다.

## 흐름을 확인하는 빠른 방법

큰 HTML을 통째로 읽지 말고, 각 파일에서 텍스트만 뽑아 비교하세요:

```bash
python3 - <<'EOF'
import re,glob,os
for f in sorted(glob.glob("*.html")):
    s=open(f,encoding='utf-8').read()
    s=re.sub(r'<(script|style|svg).*?</\1>','',s,flags=re.S)
    s=re.sub(r'<(h1|h2|h3|p|div|li|tr|br)[^>]*>','\n',s)
    s=re.sub(r'<[^>]+>','',s)
    open("txt/"+os.path.basename(f)+".txt","w",encoding='utf-8').write(re.sub(r'\n\s*\n+','\n',s))
EOF
```
그리고 `grep -oh 'class="hero-kicker">[^<]*' *.html`, `grep -n "다음 강의\|다음 주차\|예고" *.html`로 예고 문구만 모아 한눈에 대조합니다.

---

## 작업 검증 워크플로 (커밋 전 필수)

Playwright(`/opt/pw-browsers/chromium`)로 모든 페이지를 일괄 확인합니다. 페이지가 많으므로 스크립트 하나로 돌리세요:

```js
import { chromium } from '/opt/node22/lib/node_modules/playwright/index.mjs';
const b = await chromium.launch({ executablePath: '/opt/pw-browsers/chromium' });
for (const f of process.argv.slice(2)) {
  const p = await b.newPage(); const errs = [];
  p.on('pageerror', e => errs.push(e.message));
  p.on('console', m => { if (m.type()==='error') errs.push(m.text()); });
  await p.goto('file://' + process.cwd() + '/' + f); await p.waitForTimeout(700);
  const r = await p.evaluate(() => {
    const cbs=[...document.querySelectorAll('input[data-progress]')];
    cbs.forEach(c=>{c.checked=true;c.dispatchEvent(new Event('change',{bubbles:true}));});
    return { n:cbs.length, backWeek:!!document.querySelector('a.back-week'), backHome:!!document.querySelector('a.back-home') };
  });
  await p.waitForTimeout(400);
  const bar = await p.evaluate(() => document.getElementById('progressBar')?.style.width);
  console.log(f, JSON.stringify(r), bar, errs.join('|')||'no-errors');
  await p.close();
}
await b.close();
```

확인 항목:
- 콘솔 에러 0건
- 체크박스를 모두 켰을 때 `progressCount === progressTotal`, 진행률 바 100%
- `a.back-week` / `a.back-home`이 존재하고 `href="index.html"`
- 폼(라디오/입력) 변경 시 프롬프트 미리보기가 갱신되는지
- 라이트박스 등 모달이 열리고 닫히는지 (`hidden` 속성 토글)
- 사이드바 TOC의 active 링크가 스크롤에 따라 바뀌는지 (순간 이동이 아니라 `mouse.wheel`로 점진적 스크롤 — 순간 이동은 false negative를 만듦)
- index 페이지: 데스크톱·모바일(390px) 모두에서 가로 스크롤이 생기지 않는지, 카드 개수와 `href`가 실제 파일과 일치하는지
- 스크린샷을 찍어 육안 확인

**링크 전수 검사**(주차가 늘수록 중요):

```bash
python3 - <<'EOF'
import re,os,glob,urllib.parse
for f in ['index.html']+glob.glob('week*/*.html'):
    d=os.path.dirname(f) or '.'
    for h in set(re.findall(r'href="([^"#][^"]*)"', open(f,encoding='utf-8').read())):
        if h.startswith(('http','mailto:','data:','javascript:')): continue
        t=os.path.normpath(os.path.join(d,urllib.parse.unquote(h.split('#')[0])))
        if not os.path.exists(t): print("BROKEN", f, "->", h)
EOF
```

## 산출물 전달 및 저장 규칙

- 저장소(`kaist-itm-aibootcamp/aibootcamp2026`)에 `week{N}/` 폴더로 커밋하는 것이 정본입니다. `CONVENTIONS.md`의 이름 규칙과 이름 변경 이력도 같은 커밋에서 갱신합니다.
- 사용자에게 직접 파일을 보여줄 때는 `SendUserFile`을 씁니다.
- `.docx` 바이너리는 프로젝트 업로드가 실패하는(HTTP 400) 알려진 제약이 있으므로 `SendUserFile`로만 전달합니다. Word 문서가 필요하면 `docx` npm 패키지로 처음부터 빌드하는 방식이 안정적입니다.

## 다음 주차 작업 시 체크리스트

1. 초안 파일을 `week{N}/`에 **kebab-case로 개명**해 복사하고 `CONVENTIONS.md`에 이력 추가.
2. 모든 강의 페이지에 `back-week`(topbar) + `back-home`(본문 끝) + 관련 CSS 삽입.
3. hero-kicker를 `WEEK {N} · STEP {i} — {주제}`로 통일, topbar `week-title`도 페이지 성격에 맞게 정리.
4. 위 "여러 페이지로 이루어진 한 주차의 흐름 점검" 7항목을 순서대로 적용.
5. `week{N}/index.html`을 `week1/index.html` 복사본에서 만들고(자료 6개 초과면 PART 그룹 + flow-strip 추가), 루트 `index.html`과 직전 주차 index의 링크를 갱신.
6. Playwright 일괄 검증 + 링크 전수 검사 → 스크린샷 확인 → 커밋·푸시.
