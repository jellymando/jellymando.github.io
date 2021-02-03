---
layout: post
title: "$(window).on("load", fn) 순서"
sitemap: false
---

{:toc .large-only}

## $(window).on("load", fn) 순서

jquery 3 이상부터 `$(window).on("load", fn)` 순서가 바뀐 듯하다.

기존 jquery에서는 `$(function () {` -> `$(window).on("load", fn)` 순서로 실행되는데,

`$(window).on("load", fn)`가 먼저 실행된다.

`$.ready.then(function () {` 로 안에서 한번 더 감싸주어 순서를 다시 바꾸었다.

```js
$(function () {
  console.log("jquery");
});

$(window).on("load", function () {
  $.ready.then(function () {
    console.log("window");
  });
});
```
