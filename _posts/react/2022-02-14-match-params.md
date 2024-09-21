---
title: '[React Router] URL path를 통해 parameter 전달하기'
categories: [React]
tags: [react, react router]
---

{:toc .large-only}

## params

리액트에서 Router를 통해 설정한 path 값을 해당 페이지(컴포넌트)에서 불러오기 위해 `params`를 사용한다.

## 라우트 path 설정하기

```js
<Switch>
  <Route exact path="/blog/:categoryId/:postId" component={Post} />
</Switch>
```

`/:` 뒤가 parameter로 전달되는 props 이름이다.

## props 사용하기

`/blog/abc/12345` url로 접속했다고 가정했을 때, 클래스형/함수형 컴포넌트에서 params 값을 가져오는 방법이 있다.

### 함수형 컴포넌트

`react-router-dom`의 `useParams()` 훅을 사용하여 params 값을 얻을 수 있다.

```js
import { useParams } from 'react-router-dom'
const params = useParams()
const { categoryId, postId } = params

console.log(categoryId, postId) // abc, 12345
```

### 클래스형 컴포넌트

`this.props`로 전달되는 `match.params` 객체를 통해 categoryId, postId 값을 얻을 수 있다.

```js
const { match } = this.props
const { categoryId, postId } = match.params

console.log(categoryId, postId) // abc, 12345
```

### 일반 함수

일반 함수에서 리액트 라우터의 path 값을 가져오고 싶으면 `matchPath`를 사용한다.

```js
import { matchPath } from 'react-router-dom'

const match = matchPath(window.location.pathname, {
  path: '/users/:id',
  exact: true,
  strict: true
})

console.log(match?.params)
```

`matchPath`는 현재 URL과 라우터의 path가 일치하면 params 객체를 반환한다.

## Query String

url에서 `?` 뒤에 오는 부분을 query string이라고 한다.

query string은 `props.match.params`으로 뽑아낼 수 없고 `location.search`의 string 형식의 값을 파싱하여 parameter 값을 얻을 수 있다.

## 참고사이트

[React-Router로 props 전달하기 (props.match.params)](https://wiki.jjagu.com/?p=280)<br/>
[1. Route 와 파라미터, 쿼리](https://pro-self-studier.tistory.com/76)
