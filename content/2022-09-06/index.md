---
title: "웹 표준 & 접근성"
date: "2022-09-06"
author: 김예린
categories: codestates blog
---

## Summury

* `<head>` 요소의 자식 요소로 `<title>` 요소, `<meta>` 요소를 작성해주는 것이 일반적이다.

    ### `<meta>` 요소

    <details>
    <summary>주요 속성값</summary>
    <div markdown="1">       
    <br>

    |name 속성값|설명||
    |------|---|---|
    |description|콘텐츠에 대한 간략한 설명. 검색 결과에서 제목 밑에 뜨는 내용.|
    |keywords|웹 페이지의 관련 키워드들을 나열할 때 사용.|
    |author|콘텐츠의 제작자를 표시.|

    <br>
    </div>
    </details>

    SEO가 목적이라면 위 표처럼 name 속성을 사용하는 <meta> 요소에 더 중점을 두되, 오픈 그래프(ex. property="og:title")도 잘 작성해주는 것이 좋다.

* 콘텐츠를 작성할 때 `<hgroup>` 요소에 넣어주는 것도 SEO에 도움이 되지만, 똑같은 키워드만 반복해서 넣는 것은 역효과를 불러 올 수 있어 비슷한 키워드로 대체해서 사용하거나, 핵심 키워드의 관련 키워드들을 쭉 포함시키는 것이 좋다.

<br>

## 웹 접근성
---

> 장애인, 고령자 등이 웹 사이트에서 제공하는 정보에 비장애인과 동등하게 접근하고 이해할 수 있도록 보장하는 것

<br>

## WAI-ARIA
---

> 웹 표준을 정하는 W3C에서 웹 접근성을 담당하는 기관에서 발표한 RIA 환경에서의 웹 접근성 기술 규격

<details>
<summary>RIA (Rich Internet Applications)</summary>
<div markdown="1">       
<br>

따로 프로그램을 설치하지 않아도 웹 브라우저를 통해 사용할 수 있는 편리성 + 프로그램을 직접 설치해서 사용하는 것처럼 빠른 반응의 사용자 인터페이스를 동시에 가지는 웹 애플리케이션. SPA를 의미하는 경우가 많다.

<br>
</div>
</details>

<br>

## WAI-ARIA 사용법

 HTML 태그 내부에 속성(attribute)을 추가

* 역할(role) : HTML 요소의 역할을 정의하는 속성

```js
<div role="button">div이지만 button으로 사용할꺼야</div>
```
<br>

* 상태(state) : 요소의 현재 상태를 나타내는 속성

```js
<div role="tabList">
  <li role="tab" aria-selected="true">Tab1</li>
  <li role="tab" aria-selected="false">Tab2</li>
</div>
```
<br>

* 속성(property) : 요소의 특징을 정의하는 속성(attribute)

```js
<button> <img src="X.png" /> </button>
```

음... 이거 무슨 버튼이지? 라는 생각이 들 수 있다. 다음과 같이 버튼에 라벨을 붙일 수 있다. 

```js
<button aria-label="닫기"> <img src="X.png" /> </button>
```

