---
layout: post
title: "띄어쓰기 파라마터가 %20으로 바뀔 때, 디코딩. decodeURI()"
sitemap: false
---

{:toc .large-only}

input에 띄어쓰기 입력 후 submit하면 %20으로 인코딩 되어 에러가 나는 현상 수정

```js
console.log(decodeURI("123%20456")).replace(/\D/g, "");
//123456
```
