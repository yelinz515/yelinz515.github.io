---
title: "TypeScript 기본 문법(수정)"
date: "2022-08-29"
author: 김예린
categories: blog study
---

### enum

```js
enum os {
  window = 3,
  ios,
  Android
}
```

`window = 3, ios = 4, Android = 5`가 출력된다. 문자열도 가능하다.

```js
enum osList {
  window = ' win',
  ios = 'ios',
  Android = 'And'
}

let myOs = osList.window
console.log(myOs)  // 'win'
```

<br>

### interface

```js
type score = 'A' | 'B'

interface User {
  name: string
  age: number
  gender?: string // gender?는 적지 않아도 오류가 나지 않는다.
  readonly birthYear: number // readonly는 수정 불가능
  [grade: number]: score// 'string'
}

let i: User = {
  name: 'yerin',
  age: 18,
  gender: 'male',
  birthYear: 2005,
  1: 'A'
}

i.gender = 'female' // 'male'에서 'female'로 변경
```

아래와 같이 interface로 함수를 정의할 수 있다.

```js
interface Add {
  (age: number): boolean; // age를 number로 받고, 반환 값은 boolean이다.
}

const myAge: Add = (age) => {
  return age > 20
}
console.log(myAge(18)) // false
```

<br>

### function