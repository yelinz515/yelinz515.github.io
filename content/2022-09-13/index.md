---
title: "[Backend] 인증 / 보안"
date: "2022-09-13"
author: 김예린
categories: codestates blog
---

## Cookie
---

> 서버에서 클라이언트에 영속성있는 데이터를 저장하는 방법

서버는 쿠키를 이용하여 데이터를 저장하고 이 데이터를 다시 불러와 사용할 수 있지만, 데이터를 저장한 이후 특정 조건들이 만족되어야 다시 가져올 수 있다.

```js
'Set-Cookie':[
            'cookie=yummy', 
            'Secure=Secure; Secure',
            'HttpOnly=HttpOnly; HttpOnly',
            'Path=Path; Path=/cookie',
            'Doamin=Domain; Domain=yelinz515.com'
        ]
```

### Axios

> 브라우저, Node.js를 위한 Promise API를 활용하는 HTTP 비동기 통신 라이브러리

axios는 자동으로 JSON데이터 형식으로 변환하기 때문에 `.json()` 은 필요없다.

<br>

## Session
---

사용자가 인증에 성공한 상태는 세션이라고 부른다. 웹사이트에서 로그인을 유지하기 위한 수단으로 쿠키를 사용하는데, 쿠키에는 서버에서 발급한 세션 아이디를 저장합니다.

<br>

## 마무리

다음 시간에는 토큰 개념에 대해 알아보고, 과제를 통해서 JWT와 Oauth의 작동원리에 대해 실습해보겠습니다. 
