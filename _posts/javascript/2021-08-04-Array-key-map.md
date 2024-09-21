---
title: "숫자 범위만큼 map 돌리기"
categories: [JAVASCRIPT]
tags: [javascript]
---

{:toc .large-only}

지정된 숫자 범위만큼 map을 돌리고 싶다면

```js
[...Array(n).keys()].map;
```

<br/>

혹은

```js
Array.from(Array(n).keys());
```

<br/>

숫자만큼 배열을 만들어 map을 돌린다.

<br/>

[How to generate range of numbers from 0 to n in ES2015 only?](https://stackoverflow.com/questions/36947847/how-to-generate-range-of-numbers-from-0-to-n-in-es2015-only)
