---
title: "Redux"
date: "2022-09-01"
author: 김예린
categories: codestates blog
---

Redux에 들어가기에 앞서, mutate state가 무엇인지 알아보자. 

## mutate state
---

```js
const reducer = (state = [], action) => {
    switch (action.type) { //action.text가 필요해보이는데?
        case add_todo:
            return [];
        case delete_todo:
            return [];
        default:
            return state;
    }
};
```

<br>

state를 수정하려고 할 때, 아래처럼 작성하였다.

```js
        case add_todo:
            return state.push(action.text);
```

### state 값을 바꿀 땐, mutate를 할 수 없다!

**mutate**

> 파생변수를 생성할 때 사용하는 함수.

쉽게 말하자면 array의 값을 바꾸는 메서드는 사용할 수 없다는 이야기다. `state.push` 이런 것들 말이다. 

```js
        case add_todo:
            return [...state, {text: action.text}];
```

state를 바꿀때는 위 코드처럼 새롭게 정의해주어야 한다. 즉 state가 배열이라면, **배열을 새롭게 정의**해야한다.

Redux에서 저장소나 리듀서에서 상태 불변성을 지키자. NEVER! MUTATE STATE!!

<br>

## Redux
---

![github-blog-1.png](redux-data-flow.gif) [Redux 구조]


<details>
<summary>Redux는 다음과 같은 순서로 상태를 관리한다.</summary>
<div markdown="1">       
<br>

1. 상태가 변경되어야 하는 이벤트가 발생하면, 변경될 상태에 대한 정보가 담긴 `Action` 객체가 생성된다.

2. 이 Action 객체는 `Dispatch` 함수의 인자로 전달된다.

3. Dispatch 함수는 Action 객체를 `Reducer` 함수로 전달한다.

4. Reducer 함수는 Action 객체의 값을 확인하고, 그 값에 따라 전역 상태 저장소 `Store`의 상태를 변경한다.

5. 상태가 변경되면, React는 화면을 다시 **렌더링** 한다.

<br>
</div>
</details>

정리하면, Redux에서는 Action → Dispatch → Reducer → Store
순서로 데이터가 **단방향**으로 흐르게 된다.

<br>

## Cmarket Redux 예고
---

내일까지 진행되는 과제인 Cmarket Redux는 다음 포스팅에서 뵙겠습니다.
