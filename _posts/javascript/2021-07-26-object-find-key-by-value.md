---
title: "[Object] value 값으로 key 찾기"
categories: [JAVASCRIPT]
tags: [javascript]
---

{:toc .large-only}

key 값으로 value를 찾는건 쉽지만, value를 가진 key를 찾는 건 좀 헷갈린다.

객체의 키를 배열로 만든 후 순환하며 value와 비교하여 key를 찾을 수 있다.

```js
const object = {
  a: 0,
  b: 1,
  c: 2,
};

const getKey = (value) => {
  const result = Object.keys(object).find((key) => object[key] === value);
  console.log(result);
};

getKey(value);
```

<br/>

[[JS] value값으로 key값 찾기!](https://velog.io/@try_catch/JS-value%EA%B0%92%EC%9C%BC%EB%A1%9C-key%EA%B0%92-%EC%B0%BE%EA%B8%B0)
