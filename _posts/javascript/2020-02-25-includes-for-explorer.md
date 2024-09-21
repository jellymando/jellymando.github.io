---
title: "익스플로러에서 includes 대신 indexOf를 사용하자"
categories: [JAVASCRIPT]
tags: [javascript, cross browsing]
---

{:toc .large-only}

인터넷 익스플로러는 includes를 지원하지 않는다...

변경전

```js
if (str.includes("hi")) {
  alert("HI!!");
}
```

변경후

```js
if (str.indexOf("hi") >= 0) {
  alert("HI!!");
}
```
