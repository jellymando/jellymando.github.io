---
title: '[matchPath] 라우터 path 체크하기'
categories: [React]
tags: [react, react router]
---

{:toc .large-only}

## matchPath

정규식을 통해 url을 체크하듯이 현재 라우터의 path가 매치되는지 체크할 수 있다.

```js
import { matchPath } from 'react-router'

const match = matchPath(window.location.pathname, {
  path: '/users/:id',
  exact: true,
  strict: false
})
```

pathname이 prop(url)과 일치하면 객체를 반환한다.

```js
{
  isExact: true
  params: {
    id: '2'
  }
  path: '/users/:id'
  url: '/users/2'
}
```

일치하지 않으면 null을 반환한다.

## 참고사이트

[matchPath](https://v5.reactrouter.com/web/api/matchPath)
