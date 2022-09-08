---
emoji: 💻
title: "[프로그래머스] 1주차 스터디 회고"
date: "2022-09-07"
author: 김예린
tags: 블로그 react
categories: algorithm blog study
---

스터디에서 다른 사람의 코드를 참고하면서 좋았던 부분에 대해 이야기하고자 한다.

<br>

### 하샤드 수
---

```js
function solution(x) {
    return x % (x + '').split('').map(el => +el).
    reduce((acc,cur) => acc+cur) === 0;
}
```

처음 설명듣기 전에 이게 무슨 코드지? 라는 생각이 들었다. `+el` ? `x + ''` ? 

<br>

**자바스크립트는 타입 강제 변환이 일어나기 때문에 연산자를 통해 형변환을 일으킬 수 있다는 것이다.**

```js
console.log(10 + '') // '10'
console.log(+'12') // 12
console.log(-true) // -1
console.log(+'') // 0
}
```

다시 코드를 보면 , x가 12이라고 했을 때 '12'으로 만들어 여러 개의 문자열로 나누면 [ '1', '2' ]이 된다. 이후 map함수를 이용해 `+el => +'1' = 1`이 되면서 [ 1, 2 ]가 되고, reduce함수를 통해 더해서 3이 된다.

정리하면, 12 % 3 === 0이기 때문에 true를 반환하게 된다.

다시 봐도 정말 신기한 코드이다.

<br>

### 최대공약수와 최소공배수
---

```js
function solution(a, b) {
  return [gcd(a, b), lcm(a, b)];
}

function lcm(a, b) {
  return (a * b) / gcd(a, b);
}

function gcd(a, b) {
  // base
  if (b === 0) return a;
  //recursive
  return a > b ? gcd(b, a % b) : gcd(a, b % a);
}
```

gcd함수에서 a가 b보다 크면 작은 수인 b로 나눈 나머지 값을 리턴하고, 아니면 그 반대의 경우로 자기 자신을 호출하였다. 
