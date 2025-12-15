# MiniProject-01

## 개요

<details>
<summary>요구사항 명세</summary>

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

</details>

<details>
<summary>styles</summary>

# styles
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

</details>

## 작업 로그 

<details>
<summary>2025.12.10</summary>

# HTML 구조 설계 및 시멘틱 마크업 개선

* `header / main / footer` 기본 레이아웃 구성.
* Hero, Input, Output 세 영역을 시안 기준으로 `section`으로 분리.
* Hero 섹션은 `hero__title`, `hero__catchphrase`, `hero__description` 세 개의 요소로 구성.
* 페이지 내 시각적 타이틀 이미지를 보완하기 위해 `h1.visually-hidden` 추가(SEO 및 접근성 고려).

### 주요 결정 이슈

* h1을 어디 둘지 고민 → 시각적으로 감추고 main 최상단에 두는 방식으로 해결.
* `<article>`, `<figure>` 사용 여부 검토 → Hero 영역에서는 과한 시멘틱 요소라 판단하여 `div` 유지.
* Hero 내부 텍스트 계층 구조를 BEM 기반으로 재정리.



## BEM 네이밍 규칙 정비

### 이슈

여러 Element를 어떻게 네이밍할지, `__`, `--`, Element depth 문제 등 혼란이 있었음.

### 해결 및 결정 기준

* BEM은 `Block__Element--Modifier` 구조를 유지해야 하며 Element 중첩(`Block__Element__Element`)은 비권장.
* Input 영역 초기 네이밍(`input__enter__goal`) 구조가 BEM 규칙 위반 → `input__goal-row`, `input__time-row` 형태로 단일 depth Element로 수정.
* Output 영역 역시 `wrap`, `row` 등 혼재되던 네이밍을 `output__goal-text`, `output__goal-value` 등 얕은 구조로 통일.



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



## 버튼 + 이미지 배치 이슈

### 고민

버튼 옆의 click 이미지가 button 안에 있어야 하나?
→ 시안 기준으로 버튼 *바깥에* 위치하는 것이 맞으므로 구조 유지.

### 결정

* 이미지는 장식 요소이므로 alt="" 처리.
* 클릭 이벤트는 버튼에만 적용 (이미지 클릭 동작이 필요하면 JS로 보조 처리).



## form 태그 사용 여부

* Input 영역을 form으로 묶을지 고민.
* 하지만 시안 상 submit 동작은 JS 로직에서만 처리할 것이며, 실제 form 제출이 필요하지 않음.
* 문장 중간에 input이 자연스럽게 포함되어 있어 form 구조가 오히려 복잡해짐.
* **form 미사용** 결정.



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



## 엔티티 코드 관련

### 정리한 내용

* 소괄호 ( ) 는 엔티티 코드 불필요. 그대로 써도 됨.
* 필요할 때는 `&#40;` `&#41;`
* ※ 기호 → `&#8251;`
* 마지막 output 문장에 불필요한 `:&#41;` 괄호 엔티티 제거 필요.



## 최종 구축한 HTML 구조 개요

(요약)

* Hero
* Input (`input__enter`, `input__goal-row`, `input__time-row`, `section--input__submit`)
* Output (`output__goal-text`, `output__goal-value`, `output__days-text`, `output__days-value`, `output__actions`)
* Footer (`footer__branding`, `footer__notice`)

모든 구조가 시안과 BEM 규칙에 맞도록 확정됨.

끝.

</details>

<details>
<summary>2025.12.11</summary>

---

### 프로젝트 구조 설계 및 마크업 정비 단계

페이지 전체 구조를 page-wrapper 기준으로 정리
header / main / footer를 grid 레이아웃으로 분리
main 내부를 hero / input / output 섹션으로 명확히 구획

```html
<div class="page-wrapper">
    <header></header>
    <main>
        <h1 class="visually-hidden">1만 시간의 법칙</h1>

        <section class="hero"></section>
        <section class="section--input"></section>
        <section class="section--output"></section>
    </main>
    <footer></footer>
</div>
```

```css
.page-wrapper{
    display: grid;
    grid-template-columns: 1fr;
    grid-template-rows: auto auto auto;
    grid-template-areas:
        "header"
        "main"
        "footer";
    gap: 32px;
    margin: 0 auto;
    padding: 0 32px;
}

header { grid-area: header; }
main   { grid-area: main; }
footer { grid-area: footer; }
```

### 접근성과 SEO 고려
시각적 타이틀과 별도로 visually-hidden h1 추가
메인 콘텐츠 최상단에 배치하여 문서 구조 명확화

```html
<h1 class="visually-hidden">1만 시간의 법칙</h1>
```

```css
.visually-hidden {
    position: absolute;
    width: 1px;
    height: 1px;
    margin: -1px;
    clip: rect(0 0 0 0);
    overflow: hidden;
    white-space: nowrap;
}
```

### Hero 영역 구조 확정
hero__title / hero__catchphrase / hero__description 구성
BEM 네이밍 규칙에 따라 클래스 체계 정리

```html
<section class="hero">
    <div class="hero__title">
        <img src="./img/title.png" alt="일만 시간의 법칙 타이틀">
        <img src="./img/clock.png" alt="">
    </div>

    <div class="hero__catchphrase">
        <h2 class="hero__catchphrase-text">
            “연습은 어제의 당신보다 당신을 더 낫게 만든다.”
        </h2>

        <div class="hero__description">
            <img src="./img/quotes.png" alt="">
            <p class="hero__description-text">
                <span>1만 시간의 법칙</span>은<br>
                어떤 분야의 전문가가 되기 위해서는<br>
                최소한 1만 시간의 훈련이 필요하다는 법칙이다.
            </p>
        </div>
    </div>
</section>
```

### Hero 타이틀 레이아웃 구현
부모 요소에 position: relative 적용
title 이미지와 clock 이미지를 absolute로 겹치게 배치
중앙 정렬 및 z-index 조정으로 시안과 동일한 레이어 구성

```css
.hero__title{
    position: relative;
    height: 265px;
    margin-bottom: 56px;
}

.hero__title img{
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}

.hero__title img:nth-child(1){
    width: 564px;
    z-index: 10;
}

.hero__title img:nth-child(2){
    width: 260px;
    z-index: 1;
}
```

### CSS 아키텍처 분리
reset / base / layout / main 파일 역할 분리

```html
<link rel="stylesheet" href="./styles/reset.css">
<link rel="stylesheet" href="./styles/base.css">
<link rel="stylesheet" href="./styles/layout.css">
<link rel="stylesheet" href="./styles/main.css">
```


</details>

<details>
<summary>2025.12.12</summary>

---

### Hero 설명 영역 정렬 개선
quotes 이미지와 설명 텍스트의 시각적 겹침 처리
부모 기준 absolute 배치로 중앙 정렬 기준 통일

```css
.hero__description{
    display: flex;
    justify-content: center;
    position: relative;
}

.hero__description > img{
    position: absolute;
}
```

### Input 영역 UX 및 정렬 조정
label 내부 텍스트와 input을 inline-flex로 배치
align-items로 수직 정렬, gap으로 간격 제어

```html
<label>
    나는
    <input type="text" name="goal">
    전문가가 될 것이다.
</label>
```

```css
.input__enter label{
    display: inline-flex;
    align-items: center;
    gap: 1em;
}
```

### 버튼과 클릭 유도 이미지 정렬
section--input__submit을 기준 컨테이너로 설정
click 이미지를 absolute로 배치

```html
<div class="section--input__submit">
    <button class="btn-submit">
        나는 며칠 동안 훈련을 해야 1만 시간이 될까?
    </button>
    <img class="img-click" src="./img/click.png" alt="">
</div>
```

```css
.section--input__submit{
    position: relative;
}

.section--input__submit .img-click{
    position: absolute;
    width: 64px;
    height: 72px;
}
```

### 타이포그래피 기준 정리
font-weight 숫자 스케일 사용
line-height 배수 단위 적용
문단 간 간격은 margin 기준 관리

```css
body{
    font-family: 'GmarketSansMedium';
    font-weight: 400;
    font-size: 18px;
    line-height: 1.5;
}
```


</details>

<details>
<summary>2025.12.13</summary>

---

### 스타일 마감 및 시안 반영

전역 스타일 확정
배경색, 기본 폰트, 자간·행간 고정

```css
body{
    background-color: #5B2386;
    color: #FFFFFF;
    letter-spacing: 0%;
}
```

### 버튼 컴포넌트 마감
높이, 패딩, 라운드 값 및 타이포 스펙 고정

```css
.btn-submit{
    width: 567px;
    height: 64px;
    border-radius: 12px;
    background-color: #F5DF4D;
    padding: 20px 50px;
    font-family: 'GmarketSansBold';
    font-size: 24px;
    color: #5B2386;
}
```

### Output 섹션 정리
강조 숫자 span을 inline-block으로 처리
액션 버튼 영역을 inline-flex + gap으로 배치

```css
.section--output span{
    display: inline-block;
    font-size: 72px;
    margin: 0 1rem;
}

.output__actions{
    display: inline-flex;
    gap: 12px;
}
```

### Footer 마감
Noto Sans KR 적용
폰트 속성 오탈자 점검 대상 인지

```css
.footer__branding .footer__notice{
    font-family: 'Noto Sans KR';
    font-weight: 400px;
    font-size: 12pxs;
}
```

### 퍼블리싱 1차 완성 상태
레이아웃, 정렬, 타이포 이슈 해소
시안 기준 퍼블리싱 1차 완료
README 및 커밋 로그 정리 가능한 안정 단계 진입

---

</details>

<details>
<summary>2025.12.13 기준 리빌드</summary>

## 리빌드 배경

기존 구현은 기능적으로는 정상 동작했으나,  
텍스트와 input 요소를 시각적으로 문장처럼 구성하기 위해 구조가 과도하게 얽혀 있었다.  
이로 인해 줄바꿈, 간격, 정렬 문제가 CSS가 아닌 br, span, div 등의 마크업 요소에 의존하는 상태였다.

특히 정렬을 위해 inline 요소를 혼합하거나 임시 여백을 추가하는 방식이 반복되면서,  
레이아웃 기준이 일관되지 않고 유지보수가 어려운 구조로 이어졌다.

부분 수정만으로는 이러한 구조적 문제를 해결하기 어렵다고 판단했다.

---

### 리빌드 판단 기준

이번 리빌드는 디자인 변경이나 기능 추가로 인한 것이 아니다.  
레이아웃 정렬 방식을 명확히 정의하고, 마크업과 스타일의 책임을 분리하기 위한 구조적 판단이었다.

- 콘텐츠 의미 구조와 레이아웃 제어가 HTML 단계에서 혼재됨
- 정렬을 위해 마크업 요소가 증가하며 구조 복잡도 상승
- 줄바꿈·간격·정렬을 flex 기반으로 통합 제어할 필요성 확인
- 부분 수정 시 정렬 기준 붕괴 및 기술 부채 누적 가능성 존재

이에 따라 부분 리팩터링이 아닌 구조 단위 리빌드를 선택했다.

---

### 리빌드 목표

- 문장 단위를 label 중심의 의미 구조로 재정의
- flex 레이아웃을 기준으로 정렬, 간격, 줄바꿈 방식 통합
- 정렬 목적의 마크업 요소 제거 및 CSS 중심 레이아웃 제어
- DOM 구조 단순화를 통한 가독성 및 유지보수성 향상
- page-wrapper 레이아웃을 확장 가능 구조로 재설계
- 섹션별 스타일링 이전에 안정적인 구조 기준 확립

---

### 리빌드 결과

- flex 기반 정렬 구조 확립으로 레이아웃 일관성 확보
- 줄바꿈과 간격 제어의 CSS 일원화
- HTML 의미 구조 명확화 및 접근성 개선
- 섹션 단위 스타일링이 가능한 안정적인 기반 확보




</details>

---



<details>
<summary>2025.12.14</summary>

### HTML 구조 정비 및 입력 영역 재설계
- 이슈: `span + input`으로 문장을 이어붙여 구조가 불명확했고, br/span/div 혼재로 DOM이 복잡. 접근성·JS 확장·반응형 대응 모두 불리.
- 판단: 문장은 시각적 문제이고, 구조는 label 단위로 묶는 게 맞음. 줄바꿈은 CSS 책임으로 이관.
- 조치: 문장 단위를 `label`로 재구성, 불필요한 br/span 제거, 모바일 줄바꿈을 미디어쿼리+display 제어로 전환, aria-label/alt 점검.
- 결과: 입력 영역 단순화, 접근성·바인딩·반응형 대응 개선 → “보이는 수준”에서 “확장 가능한 구조”로 전환.
- 코드 전후 (`index.html`):
  - before:
    ```html
    <div class="line">
      <span>연 { </span><input type="number" /> <span>% }</span>
    </div>
    ```
  - after:
    ```html
    <label class="form-row">
      <span class="form-label">연도 (%)</span>
      <input type="number" aria-label="연도 입력" />
    </label>
    ```

### Hero 섹션 레이아웃 시범 구현
- 이슈: 타이틀/시계 이미지 겹침 필요. position 기준 혼란, 섹션 height 필요 여부 불명확.
- 판단: 내부는 `relative + absolute` 조합이 명확. 높이는 콘텐츠 기반 자연 확장이 유지보수에 유리.
- 조치: `.hero__img`에 `position: relative`, 타이틀/시계 이미지를 absolute+transform 중앙 정렬, z-index로 레이어 명확화. 섹션 height 미지정.
- 결과: 시안 동일 겹침 구현, 기준 명확 → margin/gap 조정 용이.
- 코드 전후 (`styles/layout.css`):
  - before:
    ```css
    .hero__img img { position: absolute; }
    ```
  - after:
    ```css
    .hero__img { position: relative; }
    .hero__title { position: absolute; left: 50%; top: 50%; transform: translate(-50%, -50%); z-index: 2; }
    .hero__clock { position: absolute; left: 50%; top: 50%; transform: translate(-50%, -50%); z-index: 1; }
    ```

</details>

<details>
<summary>2025.12.15</summary>

### page-wrapper 및 레이아웃 확장 대비
- 이슈: `.page-wrapper`에 `width: 36rem` 고정 → PC/태블릿 확장 시 재작업 필수. 임시 border·주석 스타일 잔존.
- 판단: 지금 고정폭 제거하지 않으면 전체 구조 재수정 위험. 뼈대를 일찍 확장 가능 상태로.
- 조치: 고정 `width` 제거, margin/padding 중심 레이아웃 전환, 임시 스타일 정리.
- 결과: 모바일 퍼스트 유지하면서 PC 확장 여지 확보, 레이아웃 파일을 실사용 상태로 정리.
- 코드 전후 (`styles/layout.css`):
  - before:
    ```css
    .page-wrapper {
      width: 36rem;
      border: 1px dashed red;
    }
    ```
  - after:
    ```css
    .page-wrapper {
      margin: 0 auto;
      padding: 0 16px;
      max-width: 1200px;
    }
    ```

### CSS 간격(gap/margin) 및 정렬 이슈 정리
- 이슈: flex 줄바꿈은 되나 `row-gap` 기대값 불일치, 텍스트 baseline 들뜸, input-텍스트 간격을 gap으로 제어할 수 있는지 혼란.
- 판단: gap은 flex/grid 직계 자식만 적용; inline 혼합 구조에서는 효과 없음. baseline은 폰트 메트릭 영향 가능.
- 조치: 필요한 영역만 flex 컨테이너로 분리, gap은 레이아웃 단위에서만 사용, 텍스트 정렬은 line-height/padding 조정, input+텍스트 영역은 `label + inline-flex` 유지.
- 결과: 간격 제어 기준 명확, 원인 파악으로 재발 방지.
- 코드 전후 (`styles/layout.css`):
  - before:
    ```css
    .form-row { display: inline-flex; gap: 4px; flex-wrap: wrap; }
    ```
  - after:
    ```css
    .form-row {
      display: flex;
      flex-direction: column;
      align-items: flex-start;
      gap: 6px;
    }
    @media (min-width: 768px) {
      .form-row { flex-direction: row; align-items: center; }
    }
    ```

### 마크업 신뢰도 개선
- 이슈: `spans` 오타, 불필요 공백/깨진 태그, 의미 없는 alt 값 등 신뢰도 저하 요소.
- 판단: 퍼블리싱 단계에서 마크업 신뢰도는 기능만큼 중요; 향후 JS 붙을 때 리스크.
- 조치: 오타 수정, 불필요 공백/깨진 태그 정리, 의미 없는 이미지는 `alt=""`로 명시.
- 결과: HTML 유효성·가독성 개선 → “돌아가는 코드”에서 “관리 가능한 코드”로 전환.
- 코드 전후 (`index.html`):
  - before:
    ```html
    <spans class="desc">...</spans>
    ```
  - after:
    ```html
    <span class="desc">...</span>
    ```

### 시점 기준 상태 정리
- 현재: HTML 섹션/클래스 체계 정비 완료. Hero 스타일 시범 구현, 나머지 섹션은 구조 준비. 모바일 기준 안정화, PC 확장 가능 상태.
- 의도: HTML 구조를 먼저 확정 후 섹션별 스타일을 독립 완성하는 단계적 접근. 본 시점 커밋은 “구조 확정 커밋”.

</details>