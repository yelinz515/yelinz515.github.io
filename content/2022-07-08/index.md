---
title: "객체 코플릿 (ft. 20번 21번)"
date: "2022-07-08T23:41:32.169Z"
author: 김예린
tags: 블로그 react
categories: codestates blog
---

### MDN

MDN가서 메소드나 함수를 참고하면 좋을 것 같다 😊 실제로 자바스크립트와 메서드를 함께 검색하면 MDN이 먼저 검색되는 것을 볼 수 있다.

<br>

### 객체 코플릿 오답노트(수정)

#### #20
---

```js
function countAllCharacters(str) {
  // TODO: 여기에 코드를 작성합니다.
  obj = {}; // 빈 객체 생성
  for(let el in str){
    if(obj[str[el]] === undefined){ // 처음 시작할 때 obj는 아무런 값이 없으니까
      obj[str[el]] = 0;  // 빈 객체에 각 요소의 값을 0으로 리턴한다, ''도 가능!
    }
    obj[str[el]]++; // 0으로 초기화 했으니 이제 개수를 세서 값으로 넣어주면 된다
  }
  return obj;

  console.log(obj)
}
countAllCharacters('banana') 
```

#### #21
---

```js
function mostFrequentCharacter(str) {
  // TODO: 여기에 코드를 작성합니다.
  // 문자열을 띄어쓰기 없이 합치고
  // 개수를 세서
  // 가장 큰 값 출력
 let arr = str.split(' ') // [ 'bad', 'apple' ]
 let newStr = arr.join('') // 'badapple'
 let obj = {}
 let max = 0
 let result = ''
 
 for(let i of newStr){
   if(obj[i]){ // i 값이 있으면 그 i값에 1을 더한다.
     obj[i] += 1
   }
   else {
     obj[i] = 1 // i 값이 없으면 1로 초기화
   }
   
   if(max < obj[i]){
     max = obj[i]
     result = i
   }
 }
 return result
}

mostFrequentCharacter('bad apple')
```

<br>

### 마무리

코드스테이츠에서 자바스크립트를 처음부터 배울 수 있어서 좋은 기회라고 생각한다.

자바, c언어 등 다양한 언어를 배워왔지만, 프론트엔드에 관심을 두고 있기 때문에 누군가의 도움이 필요했다. 대학교 1학년 때 html과 css 개념 정도로만 간단하게 배워서 전문가로서 다룰 실력이 안됐다.😭  

며칠 간 코플릿으로 배열, 객체의 기본을 이해하고, 로직을 짜니까 생각외로 너무 잘하고 있다는 생각에 자신감이 올라갔다.
데헷😊 

#### 클린 코드를 써야한다

만약 쉬운 문제를 풀고 있다면, 읽기 쉬운 코드로 작성하여 가독성을 높일 수 있다. 어렵다고 생각되는 문제 어떻게든 스파게티 코드라도 작성해서 정답을 도출하려고 했다.🔥 이후 레퍼런스를 보며, 클린 코드로 작성하려고 노력했다.

쨌든, 오늘은 나도 할 수 있다는 자신감을 얻어서 좋다ㅎ💜
