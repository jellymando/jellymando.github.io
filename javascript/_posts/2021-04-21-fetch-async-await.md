---
layout: post
title: "fetch API를 이용한 비동기 통신"
sitemap: false
---

{:toc .large-only}

## fetch()

fetch() 함수는 URL과 options를 인자로 받고 Promise 객체를 반환합니다.

리퀘스트가 성공하든 실패하든 해당 리퀘스트 통신에 대한 Response 객체가 취득됩니다.

response 객체는 json() 메서드를 제공합니다.

```js
fetch("http://example.com/movies.json")
  .then((response) => {
    return response.json();
  })
  .then((myJson) => {
    console.log(JSON.stringify(myJson));
  });
```

## options

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

옵션 인자를 전달하지 않으면 디폴트로 GET 방식으로 요청한다.
