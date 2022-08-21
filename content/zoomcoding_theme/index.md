---
emoji: 🔮
title: 블로깅 마이그레이션 + 블로그 디자인 수정중
date: '2022-08-21'
author: 김예린
tags: 블로그 github-pages gatsby
categories: codestates blog
---

```js
Cannot read properties of null (reading 'split')

  31 |
  32 |   edges.forEach(({ node }) => {
> 33 |     const postCategories = node.frontmatter.categories.split(' ');
     |                                                        ^
  34 |     postCategories.forEach((category) => categorySet.add(category));
  35 |   });
  36 |

File: gatsby-node.js:33:56
```

`index.md`를 생성하고 바로 이런 오류가 났다.

해결방법:
`frontmatter`에 categories를 추가하면 된다.

<br>

### category

현재 태그는 활용되고 있지 않으며, 카테고리는 블로그 리스트 하단에 보이고, 카테고리로 포스팅을 검색 가능하게 한다.

<br>

### 주의할 점

`gatsby develop`과 `npm run deploy`을 동시에 하면 오류난다.