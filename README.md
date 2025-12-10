# 요구사항 명세
1. 디자인/레이아웃 요구사항

   1. 피그마 시안을 기준으로 전체 페이지 레이아웃, 컴포넌트 스타일, 타이포그래피, 컬러 등을 최대한 동일하게 구현한다.
   2. 데스크톱과 모바일(소형 화면) 모두에서 깨지지 않도록 반응형 레이아웃으로 구현한다.
   3. 브레이크포인트는 피그마 구조를 우선으로 하되, 필요 시 320px 이상 모바일 환경에서 기본 사용성을 확보한다.

2. 마크업 및 CSS 구현 기준

   1. 시멘틱 마크업

      * header, main, section, article, nav, footer 등 시멘틱 태그를 사용해 구조를 잡는다.
      * 버튼, 링크, 리스트 등은 역할에 맞는 태그(button, a, ul/li 등)를 사용한다.
   2. 반응형 웹

      * 모바일 퍼스트 또는 데스크톱 퍼스트 중 하나의 전략으로 일관되게 media query를 설계한다.
      * 폰트, 이미지, 카드, 버튼 등이 뷰포트에 맞게 유연하게 줄어들도록 한다(폭 고정 지양).
   3. 접근성

      * 주요 인터랙션 요소에 키보드 포커스 가능하도록 tabindex와 outline을 보존한다.
      * 이미지에 대체 텍스트(alt), 아이콘 버튼에 aria-label 등을 적용한다.
      * 명도 대비는 WCAG 기준에 최대한 부합하도록 색상을 선택한다.
   4. SEO

      * 페이지당 h1을 1개만 사용하고, h2–h3 등으로 계층 구조를 만든다.
      * title, meta description, lang 속성 등 기본 SEO 메타를 포함한다.
   5. CSS 네이밍 방법론

      * BEM 등 일관된 네이밍 방법론을 적용한다. (예: .section-title, .card__title, .card__button 등)
      * id 사용은 최소화하고, 재사용 가능한 컴포넌트는 class 기반으로 설계한다.

3. 모달 관련 퍼블리싱 요구사항

   1. “훈련하기 GO! GO!” 버튼과 연동될 모달 레이아웃, 스타일을 HTML/CSS로 우선 완전히 퍼블리싱한다.
   2. 초기 상태에서는 화면에 보이지 않도록 CSS로 숨김 처리한다.

      * 예: display: none; 또는 visibility/opacity와 aria-hidden 조합 등.
   3. 접근성을 고려해 모달 구조를 설계한다.

      * 모달 컨테이너에 role="dialog" 또는 aria-modal="true" 설계.
      * 제목 요소에 aria-labelledby 연결 가능하도록 id 부여.

4. 자바스크립트로 추후 구현할 기능 목록(지금은 마크업/스타일만)

   1. “훈련하기 GO! GO!” 버튼 클릭 시 해당 모달이 열리도록 하는 동작.
   2. 모달 닫기 버튼(또는 배경 클릭 등)으로 모달을 닫는 동작.
   3. 모달 오픈 시 포커스를 모달 내부로 이동하고, 닫을 때 이전 포커스로 반환하는 접근성 로직은 추후 JS 단계에서 구현 예정.



---
# CSS
    - reset.css
        브라우저 기본 스타일 제거.

    - base.css
        프로젝트의 가장 기초가 되는 전역 스타일.
        타이포그래피 설정(font-family, font-size, line-height)
        <!-- color palette(전역 색상 변수) -->
        <!-- spacing scale(마진·패딩 단위 정의) -->
        <!-- 전역 box-sizing, body 기본 스타일 -->
        <!-- 링크/버튼 기본 리셋 수준의 전역 룰 -->
        

    - layout.css
        페이지 골격(그리드, flex 레이아웃, 레이아웃 wrapper)을 관리.

    - components.css
        버튼, 카드, 모달 등 반복되는 UI 컴포넌트 스타일.

    - main.css
        페이지 단위 스타일을 의미한다.
        예: index.html에만 필요한 스타일
        특정 섹션 배치를 위한 스타일
        특정 페이지에서만 쓰는 테마나 구조

---

# 작업 로그 (2025-12-10)

## HTML 구조 설계 및 시멘틱 마크업 개선

* `header / main / footer` 기본 레이아웃 구성.
* Hero, Input, Output 세 영역을 시안 기준으로 `section`으로 분리.
* Hero 섹션은 `hero__title`, `hero__catchphrase`, `hero__description` 세 개의 요소로 구성.
* 페이지 내 시각적 타이틀 이미지를 보완하기 위해 `h1.visually-hidden` 추가(SEO 및 접근성 고려).

### 주요 결정 이슈

* h1을 어디 둘지 고민 → 시각적으로 감추고 main 최상단에 두는 방식으로 해결.
* `<article>`, `<figure>` 사용 여부 검토 → Hero 영역에서는 과한 시멘틱 요소라 판단하여 `div` 유지.
* Hero 내부 텍스트 계층 구조를 BEM 기반으로 재정리.

---

## BEM 네이밍 규칙 정비

### 이슈

여러 Element를 어떻게 네이밍할지, `__`, `--`, Element depth 문제 등 혼란이 있었음.

### 해결 및 결정 기준

* BEM은 `Block__Element--Modifier` 구조를 유지해야 하며 Element 중첩(`Block__Element__Element`)은 비권장.
* Input 영역 초기 네이밍(`input__enter__goal`) 구조가 BEM 규칙 위반 → `input__goal-row`, `input__time-row` 형태로 단일 depth Element로 수정.
* Output 영역 역시 `wrap`, `row` 등 혼재되던 네이밍을 `output__goal-text`, `output__goal-value` 등 얕은 구조로 통일.

---

## Input 영역 구조 설계

### 주요 결정

* 입력 문장 “나는 ( ) 전문가가 될 것이다”, “그래서 하루에 ( ) 시간” 문장을 `<label>` 내부에서 구성.
* `<label for>`와 `id` 사용 여부 고민 → input을 label 내부에 포함시키는 방식으로 결정하여 `for / id` 불필요.
* `type="number"` 사용 시 브라우저 기본 스핀 버튼 등장 → 제거 방법을 CSS에서 처리하는 방향으로 결정.

### 최종 구조

```
<div class="input__enter">
    <div class="input__goal-row">...</div>
    <div class="input__time-row">...</div>
</div>
```

---

## Output 영역 구조 설계

### 이슈

Output도 label을 사용해야 하나? → NO. label은 input 설명용.
결과 출력은 `p` + `span` 조합이 시멘틱하게 맞음.

### 결정

* 결과 문장 구조를 다음과 같이 명확하게 설계:

  * `output__goal-text`
  * `output__goal-value`
  * `output__days-text`
  * `output__days-value`

### 버튼 그룹

* "훈련하러 가기", "공유하기" 두 버튼을 하나의 action group으로 묶음.
* 그룹 네이밍: `output__actions`
* 개별 버튼: `output__action-go`, `output__action-share` 로 확정.

---

## 버튼 + 이미지 배치 이슈

### 고민

버튼 옆의 click 이미지가 button 안에 있어야 하나?
→ 시안 기준으로 버튼 *바깥에* 위치하는 것이 맞으므로 구조 유지.

### 결정

* 이미지는 장식 요소이므로 alt="" 처리.
* 클릭 이벤트는 버튼에만 적용 (이미지 클릭 동작이 필요하면 JS로 보조 처리).

---

## form 태그 사용 여부

* Input 영역을 form으로 묶을지 고민.
* 하지만 시안 상 submit 동작은 JS 로직에서만 처리할 것이며, 실제 form 제출이 필요하지 않음.
* 문장 중간에 input이 자연스럽게 포함되어 있어 form 구조가 오히려 복잡해짐.
* **form 미사용** 결정.

---

## Footer 구조 설계

### 이슈

* 저작권 문구를 일반 p로 넣어도 되는지?
* 보험약관처럼 작은 글씨이므로 별도 클래스를 부여하는 것이 실무적으로 적절.

### 결정

```html
<footer>
    <div class="footer__branding">
        <img ...>
        <p class="footer__notice">...</p>
    </div>
</footer>
```

---

## 엔티티 코드 관련

### 정리한 내용

* 소괄호 ( ) 는 엔티티 코드 불필요. 그대로 써도 됨.
* 필요할 때는 `&#40;` `&#41;`
* ※ 기호 → `&#8251;`
* 마지막 output 문장에 불필요한 `:&#41;` 괄호 엔티티 제거 필요.

---

## 최종 구축한 HTML 구조 개요

(요약)

* Hero
* Input (`input__enter`, `input__goal-row`, `input__time-row`, `section--input__submit`)
* Output (`output__goal-text`, `output__goal-value`, `output__days-text`, `output__days-value`, `output__actions`)
* Footer (`footer__branding`, `footer__notice`)

모든 구조가 시안과 BEM 규칙에 맞도록 확정됨.

끝.
---
