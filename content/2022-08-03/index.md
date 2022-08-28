---
title: "React Twittler State & Props"
date: "2022-08-03T23:41:32.169Z"
author: 김예린
tags: 블로그 react
categories: codestates blog
---

## State

> 컴포넌트의 사용 중 컴포넌트 내부에서 변할 수 있는 값


### useState
---

```js
const [state 저장 변수, state 갱신 함수] = useState(상태 초기 값);
```

useState 를 호출하면 **배열**을 반환하는데, 배열의 `0번째 요소`는 현재 state 변수이고, `1번째 요소`는 이 변수를 갱신할 수 있는 함수이다. 

useState 의 인자로 넘겨주는 값은 state의 초깃값이다

```js
const [isChecked, setIsChecked] = useState(false);
```

useState 를 호출한다는 것은 "state" 라는 변수를 선언하는 것과 같으며, 이 변수의 이름은 아무 이름으로 지어도 된다.

<br>

## Props

> 외부로부터 전달받은 값

함부로 변경될 수 없는 읽기 전용 객체이다.

<br>

## React Twittler State & Props

과제를 하면서 중요했던 내용에 대해 적어보도록 하겠습니다. State와 Props에 대해 더 쉽게 이해할 수 있을 것입니다.

### Tweets.js
---

```js
import React, { useState } from 'react';
import Tweet from '../Components/Tweet';

(...)

const Tweets = () => {

  const [tweets, setTweets] = useState(dummyTweets); 

  const handleDeleteTweet = (deleteId) => {
    if(isFiltered) {
      alert("삭제합니다.");
      const deleted = filteredTweets.filter(tweet => tweet.id !== deleteId);
      setFilteredTweets(deleted)
      const deletedTweets = tweets.filter(tweet => tweet.id !== deleteId);
      setTweets(deletedTweets)
    }else {
      alert("삭제합니다.");
      const deleted = tweets.filter(tweet => tweet.id !==deleteId);
      setTweets(deleted);
    }
  };

  return (

    (...)

    <ul className="tweets">
            {isFiltered ? 
        filteredTweets.map(tweet => {
          return <Tweet tweet={tweet} key={tweet.id} handleDeleteTweet={handleDeleteTweet}/>
        })
        : tweets.map(tweet => {
          return <Tweet tweet={tweet} key={tweet.id} handleDeleteTweet={handleDeleteTweet}/>
        })
        }
    </ul>

    (...)

  );
};  
```

```js
  const [tweets, setTweets] = useState(dummyTweets); 
```

* `tweets` : state를 저장하는 함수
* `setTweets` : state tweets 를 변경하는 함수
* `useState` : state hook
* `dummyTweets` : state 초깃값

```js
<Tweet tweet={tweet} key={tweet.id} handleDeleteTweet={handleDeleteTweet}/>
```

`Tweet`컴포넌트에 `tweet`, `handleDeleteTweet`를 `중괄호 {}`로 감싸 넘겨주고 있다.

### Tweet.js
---

```js
import React from 'react';
import './Tweet.css';

const Tweet = ({ tweet, handleDeleteTweet}) => {
  const parsedDate = new Date(tweet.createdAt).toLocaleDateString('ko-kr');

  return (
    <li className="tweet" id={tweet.id}>
      <div className="tweet__profile">
        <img src={tweet.picture} />
      </div>
      <div className="tweet__content">
        <div className="tweet__userInfo">
          <div className="tweet__userInfo--wrapper">
            {/* TODO : 유져 이름이 있어야 합니다. */}
            <span className='tweet__username'>{tweet.username}</span>
            {/* TODO : 트윗 생성 일자가 있어야 합니다. parsedDate를 이용하세요. */}
            <span className='tweet__createdAt'>{parsedDate}</span>
          </div>
          <div className="tweet__userInfo--buttonWrapper">
            <button className="tweet__deleteButton" onClick={() => handleDeleteTweet(tweet.id)}>
              <i className="far fa-trash-alt"></i>
            </button>
          </div>
        </div>
        <div className="tweet__message">
          {/* TODO : 트윗 메세지가 있어야 합니다. */}
          {tweet.content}
        </div>
      </div>
    </li>
  );
};

export default Tweet;
```

넘겨받은 `tweet, handleDeleteTweet`을 이용하여 필요한 모든 데이터를 가지고 온다. 

props를 전달받았으니, props를 렌더링하자. 마찬가지로 JSX에 중괄호와 함께 `id, username, picture, content, createdAt`를 각 기능에 맞게 작성하면 잘 작동한다.

<br>

## React 데이터 흐름

#### 상향식으로 앱을 만들기
---

기획자나 PM, 또는 UX 디자이너로부터 앱의 디자인을 전달받고 나면, 이를 컴포넌트 계층 구조로 나누는 것이 가장 먼저 해야 할 일이다.

#### 데이터는 위에서 아래로 흐른다
---

데이터를 전달하는 주체는 부모 컴포넌트가 된다. 이는 데이터 흐름이 **하향식(top-down)** 임을 의미한다.

📍 사실 상태는 최소화하는 것이 가장 좋다. 상태가 많아질수록 애플리케이션은 복잡해지기 때문이다.
