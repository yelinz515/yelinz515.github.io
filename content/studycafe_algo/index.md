---
emoji: 💻
title: "알고리즘 학습 소모임 시작"
date: "2022-08-23"
author: 김예린
tags: 블로그 react
categories: algorithm blog study
---

### 시작은 달라도 결국 동일선상에 서 있다

6주동안 알고리즘 소모임이 시작된다. 오늘 OT에서 가장 인상깊었던 말이다. 남들보다 늦게 출발했어도 알고리즘 문제를 열심히 풀다보면 결국 빨리 시작한 사람들과 같은 곳에 있을 것이라는 말이다.

<br>

### 1주차 OT

나는 백준 사이트를 처음 사용해보는 것은 아니다. 백준에서는 자바스크립트 언어를 사용하기 위해 node.js 입출력(fs모듈)으로 문제를 풀었었다.

#### 소모임을 참여하게 된 이유

일단 다른 사람들과 함께 알고리즘 문제에 대해 소통할 수 있어서 좋았다. 항상 여러가지 풀이 방법이 존재하는데 다른 사람들은 어떻게 풀었는지, 내 답이 베스트인지 등 생각하지 못했던 방법을 발견할 수 있다.

###

> **fs모듈을 이용하는 방법**

1) 한 줄로 입력을 받을 때

```js
let fs = require('fs');
let input = fs.readFileSync('/dev/stdin').toString().split(' ');
```

###

2) 여러 줄로 입력을 받을 때

```js
let fs = require('fs');
let input = fs.readFileSync('/dev/stdin').toString().split('\n');
```

<br>

> **fs모듈을 이용하는 방법(vscode)**

```js
let input = require('fs').readFileSync('예제.txt').toString().split('\n');
```

`예제.txt`파일을 만들고 문제에서 주어진 예제 입력을 그대로 복사해서 저장한다.

텍스트 파일의 이름은 항상 달라지기 때문에 더 편리한 방법으로 풀 수 있었다.

```js
const input = require("fs")
.readFileSync(
process.platform === "linux"
? "/dev/stdin"
: __filename.split("/").pop().slice(0, -3) + ".txt"
)
```

파일의 이름을 `slice()` 함수로 추출한다. 이렇게 작성하면, 나중에 `txt` 파일을 만들더라도 fs모듈을 수정하지 않고 사용할 수 있다.

<br>

### 마무리
***

1주차에서는 `단계부터 차근차근 문제를 풀어나가며 node.js 입출력 방법을 익히는 것이 중요할 것 같다. 소모임 스터디를 통해 다른 동기들의 코드를 참고해서 더 클린한 코드를 작성하는 방법을 알고 도움될 만한 알고리즘 블로그를 작성해야 겠다!!!😆😆😆

현재 `BackjoonHub`라는 크롬 익스텐션을 추가했기 때문에 백준에서 문제를 제출하면 자동으로 깃허브에 자신이 지정한 레퍼지토리로 커밋된다. ~(아주 편리하다)~