---
layout: post
title: '[match.params] 라우터 path를 통해 parameter 전달하기'
sitemap: false
---

{:toc .large-only}

## match.params

리액트에서 Router를 통해 설정한 path 값을 해당 페이지(컴포넌트)에서 불러오기 위해 `props.match.params` 을 사용한다.

## 라우트 path 설정하기

```js
<Switch>
  <Route exact path="/post/:postId" component={Post} />
</Switch>
```

`/:` 뒤가 parameter로 전달되는 props 이름이다.

## props 사용하기

`/post/34238` 이라는 url로 접속하면 Post 페이지의 props 객체 내부의 postId 값이 34238로 전달된다.

```js
const { match } = this.props
const { postId } = match.params
console.log(postId) // 34238
```

## Query String

url에서 `?` 뒤에 오는 부분을 query string이라고 한다.

query string은 `props.match.params`으로 뽑아낼 수 없고 `location.search`의 string 형식의 값을 파싱하여 parameter 값을 얻을 수 있다.

## 참고사이트

[React-Router로 props 전달하기 (props.match.params)](https://wiki.jjagu.com/?p=280)<br/>
[1. Route 와 파라미터, 쿼리](https://pro-self-studier.tistory.com/76)
