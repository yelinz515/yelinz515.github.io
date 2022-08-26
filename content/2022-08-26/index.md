---
title: "[React] Custom Component"
date: "2022-08-26"
author: 김예린
categories: codestates blog
---

### Component Driven Development (CDD)

> 디자인과 개발 단계에서부터 **재사용**할 수 있는, **레고처럼 조립해 나갈 수 있는** 부품 단위로 UI 컴포넌트를 만들어 나가는 개발


<br>

### CSS-in-JS (ex. Styled-Component)

> 기능적(Functional) 혹은 상태를 가진 컴포넌트들로부터 UI를 완전히 분리해 사용할 수 있는 아주 단순한 패턴을 제공

#### Styled Components 문법

#### 1. 컴포넌트 만들기
---

```js
import styled from "styled-components";

const 컴포넌트이름 = styled.태그종류`
    background: black;
    color: white;
`;
```
```js
import styled from "styled-components";

// const button1 = styled(재활용할 컴포넌트) 가능
const button1 = styled.button`
    background: black;
    color: white;
`;
```

#### 2. Props 활용하기 
---

```js
import styled from "styled-components";

const button1 = styled.button`
    background: ${(props) => props.skyblue ? "skyblue" : props.color};
    color: white;
`;

export default function App() {
  return (
    <>
      <Button1>Button1</Button1>
      <Button1 skyblue>Button1</Button1>
    </>
  );
}
```

###

* Props로 조건부 렌더링하기: `props.skyblue ? "skyblue" : "pink" `

* Props 값으로 렌더링하기: `props.skyblue ? "skyblue" : props.color`

#### 3. 전역 스타일 설정하기
---

#### GlobalStyle.js

```js
import { createGlobalStyle } from "styled-components";

const GlobalStyle = createGlobalStyle`
	button {
		padding : 5px;
    margin : 2px;
    border-radius : 5px;
	}
`
```

 `<GlobalStyle>` 컴포넌트를 최상위 컴포넌트에서 사용해주면 전역에 `<GlobalStyle>`ㄴ 컴포넌트의 스타일이 적용된다.

#### App.js

```js
import GlobalStyle from './GlobalStyle'

export default function App() {
  return (
    <>
        <GlobalStyle />
        <button id="practice">Practice!</button>;
  </>
  )
}
```

<br>

### Storybook

> Component Driven Development를 하기 위한 도구

#### 지원하는 주요 기능

* UI 컴포넌트들을 카탈로그화하기
* 컴포넌트 변화를 Stories로 저장하기
* 핫 모듈 재 로딩과 같은 개발 툴 경험을 제공하기
* 리액트를 포함한 다양한 뷰 레이어 지원하기

#### 튜토리얼

```js
npx storybook init
```

이 명령어는 `package.json` 을 보고 사용 중인 프론트엔드 라이브러리에 맞는 Storybook 사용 환경을 알아서 만들어주기 때문에, 꼭 React가 아니더라도 다양한 프론트엔드 라이브러리에서 사용할 수 있다.

<br>

### useRef

 React로 모든 개발 요구 사항을 충족할 수는 없다. 아래와 같이 **DOM 엘리먼트의 주소값을 활용해야 하는 경우** 특히 그렇다.

* focus
* text selection
* media playback
* 애니메이션 적용
* d3.js, greensock 등 DOM 기반 라이브러리 활용

아래 예시 코드처럼 `useRef` 로 DOM 노드, 엘리먼트, 그리고 React 컴포넌트 주소값을 참조할 수 있다.

```js
function TextInputWithFocusButton() {
    // const 주소값을_담는_그릇 = useRef(참조자료형)
  const inputEl = useRef(null);
  const onButtonClick = () => {
    inputEl.current.focus();
  };
  return (
    <>
    {/* <input ref={주소값을_담는_그릇} type="text" /> */}
      <input ref={inputEl} type="text" />
      <button onClick={onButtonClick}>Focus the input</button>
    </>);
}
```