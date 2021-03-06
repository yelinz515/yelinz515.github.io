---
title:  "[5주차] [JavaScript] 고차 함수 - 4일차"
excerpt: "Section2의 시작"

categories:
  - Blog
tags:
  - [Blog, jekyll, Github, Git]

toc: true
toc_sticky: true
 
date: 2022-07-21
last_modified_at: 2022-07-21
---

# ☑️ 고차 함수

* 오늘 공부한 내용
* 어려웠던 내용
* 궁금한 내용과 부족한 내용 
* 느낀점

#

# ✨  오늘 공부한 내용

## ✅ 고차 함수
> **함수를 리턴하는 함수, 함수를 전달인자로 받는 함수(=커링 함수)**

이때 
다른 함수의 전달인자로 전달되는 함수 : **콜백 함수(callback function)**

* 콜백 함수를 전달받은 고차 함수는, 함수 내부에서 이 콜백 함수를 호출할 수 있다.
* 아예 호출하지 않을 수도 있고, 여러 번 실행할 수 있다.

**📍 for...of vs for...in**
* for...of : 반복가능한 객체 (Array, Map, Set, String, TypedArray, arguments 객체 등을 포함)에 대해서 반복

```js
for(let i =0; i<arr.length; i++){
}    
```

위처럼 쓰지 않아도 아래 코드로 쓰면 대입받은 변수를 이용하면 루프 안에서 객체의 열거할 수 있는 프로퍼티에 순차적으로 접근할 수 있습니다.

```js
for (variable of iterable) {
  statement
}  
```

###

* for...in :  객체에서 문자열로 키가 지정된 모든 열거 가능한 속성에 대해 반복

자세한 내용은 아래 링크를 눌러주세요!
출처: https://yjshin.tistory.com/entry/JavaScript-자바스크립트-for-문-for-in-문-for-of-문 [YJUN IT BLOG:티스토리] 

#

## ✅ 내장 고차 함수

### filter
> **주어진 함수의 테스트를 통과하는 모든 요소를 모아 새로운 배열로 반환합니다.**

### map
> **배열 내의 모든 요소 각각에 대하여 주어진 함수를 호출한 결과를 모아 새로운 배열을 반환합니다**

### reduce
> **배열의 각 요소에 대해 주어진 리듀서(reducer) 함수를 실행하고, 하나의 결과값을 반환합니다.**

리듀서 함수는 네 개의 인자를 가집니다.

1. 누산기 (acc)
2. 현재 값 (cur)
3. 현재 인덱스 (idx)
4. 원본 배열 (src)

리듀서 함수의 반환 값은 **누산기에 할당**되고, 누산기는 순회 중 유지되므로 결국 최종 결과는 **하나의 값**이 됩니다

#

# ✨  어려웠던 내용

고차 함수 코플릿 몇 문제가 어려웠다.

### ✅ 오답노트
(주말에 스스로 풀어서 오답노트 작성하기!)

#

# ✨  부족한 내용

내장 고차 함수 대표 3가지인 filter, map, reduce를 자주 연습해야겠다.
하다보면 익숙해질 것이다.

(종합퀴즈 4,8번 오답노트 작성하기!)

✅ 4.

#

> ## 마무리 👀

section2의 첫 시작이었는데, section1보다 살짝 난이도가 어려워졌고, 학습 이후 처음으로 시간이 부족하다고 느꼈다.

❤️진짜 정신차리고 열심히 하자!!❤️

**꾸준히 자기주도적 학습을 하고 새롭게 알게 된 내용을 바탕으로 TIL를 작성하겠습니다.** 😊