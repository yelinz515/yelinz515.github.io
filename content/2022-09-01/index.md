---
title: "Redux"
date: "2022-09-01"
author: 김예린
categories: codestates blog
---

Redux에 들어가기에 앞서, mutate state가 무엇인지 알아보자. 

## mutate state

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

## Cmarket Redux(1)
