---
layout: post
title: "[URLSearchParams] url parameters 추출하기"
sitemap: false
---

{:toc .large-only}

## location.search

URL 뒤의 `?`를 포함한 문자열 쿼리이다.

최신 브라우저에서는 쿼리 문자열에서 파라미터 값을 쉽게 찾을 수 있도록 `URLSearchParams` 및 `URL.searchParams`를 제공한다.

## URLSearchParams(location.search)

`location.search`를 구문 분석하여 key-value 형태의 객체를 만드는 메서드이다.

아래와 같이 변수에 담을 수 있다.

```js
const params = new URLSearchParams(location.search);
// 혹은
const url = new URL("https://example.com?foo=1&bar=2");
const params = new URLSearchParams(url.search);
```

### urlSearchParams.get("name")

해당 name으로 조회되는 첫 번째 파라미터 값을 리턴한다.

```js
const url = new URL("https://example.com/?name=Jonathan&age=18");
const params = new URLSearchParams(url.search);
const name = params.get("name");
console.log(name); // "Jonathan"
const age = parseInt(params.get("age"), 10);
console.log(age); // 숫자 18
const address = params.get("address");
console.log(address); // null
```

### urlSearchParams.getAll("name")

해당 name으로 조회되는 모든 파라미터 값을 배열로 리턴한다.

```js
const url = new URL("https://example.com?foo=1&foo=2");
const params = new URLSearchParams(url.search);
const foos = params.getAll("foo");
console.log(foos); // ["1", "2"]
```

## 참고사이트

[[javaScript] URL Parameter 값 다루기](https://velog.io/@gillog/javaScript-URL-Parameter-%EA%B0%92-%EB%8B%A4%EB%A3%A8%EA%B8%B0#urlsearchparams)<br/>
[URLSearchParams.get()](https://developer.mozilla.org/ko/docs/Web/API/URLSearchParams/get)<br/>
[URLSearchParams.getAll()](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams/getAll)<br/>
[location.search](https://developer.mozilla.org/en-US/docs/Web/API/Location/search)
