---
layout: post
title: "fetch API를 이용한 비동기 통신"
sitemap: false
---

{:toc .large-only}

## fetch API

`fetch()` 함수는 url과 options 객체를 인자로 받아 Request를 보내고, Response로 Promise 객체를 반환한다.

브라우저에서 내장된 `fetch()` 함수를 이용하면 axios, jQuery.ajax와 같은 라이브러리를 사용하는 것보다 자원의 낭비를 줄일 수 있다.

## 사용법

options 객체에 HTTP 메서드, HTTP 요청 헤더, HTTP 요청 전문(body) 등을 설정해줄 수 있다.

Response 객체로부터는 HTTP 응답 상태(status), HTTP 응답 헤더, HTTP 응답 전문(body) 등을 읽어올 수 있다.

## Options

```js
fetch(url, {
  method: "POST", // *GET, POST, PUT, DELETE, etc.
  mode: "cors", // no-cors, cors, *same-origin
  cache: "no-cache", // *default, no-cache, reload, force-cache, only-if-cached
  credentials: "same-origin", // include, *same-origin, omit
  headers: {
    "Content-Type": "application/json",
    // 'Content-Type': 'application/x-www-form-urlencoded',
  },
  redirect: "follow", // manual, *follow, error
  referrer: "no-referrer", // no-referrer, *client
  body: JSON.stringify(data), // body data type must match "Content-Type" header
}).then((response) => response.json());
```

## GET

`fetch()` 함수는 디폴트로 GET 방식으로 작동하고, GET 방식은 요청 전문을 받지 않기 때문에 보통은 옵션 인자가 필요없다.

<br/>

```js
fetch("http://example.com/movies.json").then((response) => {
  return response.json();
});
```

## POST

`method` 옵션을 POST로 지정해주고, `headers` 옵션을 통해 JSON 포맷을 사용한다고 알려줘야 하며, `body` 옵션에 요청 전문을 json 형식으로 설정한다.

<br/>

```js
fetch("https://jsonplaceholder.typicode.com/posts", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify({
    title: "Test",
    body: "I am testing!",
    userId: 1,
  }),
}).then((response) => console.log(response));
```

## 에러 처리

axios와는 달리 `fetch()`**로 부터 반환되는 Promise 객체는 HTTP error 상태를 reject하지 않으므로 catch로 떨어지지 않는다.**

대신 ok 상태가 false인 resolve가 반환되며, 네트워크 장애나 요청이 완료되지 못한 상태에는 reject가 반환된다.

HTTP 에러가 발생했을 때 또는 CORS가 서버단에서 잘못 설정되어 있을 때 에러가 catch문으로 떨어지지 않으므로 **response의 ok를 체크**해야 한다.

<br/>

```js
fetch("http://example.com/movies.json")
  .then((response) => {
    if (!response.ok) throw new Error("HTTP 에러");
    return response.json();
  })
  .catch((e) => {
    throw new Error(e.message);
  });
```

<br/>

```js
try {
  await fetch("http://example.com/movies.json").then((response) => {
    if(!response.ok) throw new Error("HTTP 에러");
    return response.json();
  }
} catch (e) {
  throw new Error(`fetch 작업 오류 : ${e.message}`);
}
```

## api 별도 처리 예제

```js
// api.js
const request = async (nodeid) => {
  try {
    const result = await fetch(
      `https://zl3m4qq0l9.execute-api.ap-northeast-2.amazonaws.com/dev/${
        nodeid ? `:${nodeid}` : ""
      }`
    ).then((response) => {
      if (!response.ok) throw new Error("HTTP 에러");
      return response.json();
    });
  } catch (e) {
    throw new Error(`fetch 작업 오류 : ${e.message}`);
  }
};

// app.js
const init = async () => {
  const rootNodes = await request();
};
```

## 참고사이트

[fetch API를 이용한 비동기 통신](https://jellymando.github.io/javascript/2021-04-21-fetch-async-await/)<br/>
[Using Fetch](https://developer.mozilla.org/ko/docs/Web/API/Fetch_API/Using_Fetch)<br/>
['2021 Dev-Matching: 웹 프론트엔드 개발자(상반기)' 기출 문제 해설](https://prgms.tistory.com/53)<br/>
[Axios - Handling Errors](https://axios-http.com/docs/handling_errors)
