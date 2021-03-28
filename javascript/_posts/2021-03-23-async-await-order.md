---
layout: post
title: 'async-await 비동기 함수 실행 순서'
sitemap: false
---

{:toc .large-only}

비동기 함수를 다른 함수에서 호출할 때 async-await을 안 붙이면?

```js
var aw = async () => {
  await fetch(
    'https://oivhcpn8r9.execute-api.ap-northeast-2.amazonaws.com/dev/api/cats/random50'
  )
    .then(function (response) {
      return response.json();
    })
    .then(function (myJson) {
      console.log(JSON.stringify(myJson));
    });
  console.log('after await');
};
var a = (() => {
  aw();
  console.log('?');
})();

// ?
// after await
```

비동기 함수를 호출하는 함수에도 async-await을 붙여야 원하는 순서로 실행된다.

```js
var aw = async () => {
  await fetch(
    'https://oivhcpn8r9.execute-api.ap-northeast-2.amazonaws.com/dev/api/cats/random50'
  )
    .then(function (response) {
      return response.json();
    })
    .then(function (myJson) {
      console.log(JSON.stringify(myJson));
    });
  console.log('after await');
};
var a = (async () => {
  await aw();
  console.log('?');
})();

// after await
// ?
```
