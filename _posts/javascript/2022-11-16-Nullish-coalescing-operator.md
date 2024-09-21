---
title: '?? 연산자와 || 연산자'
categories: [Javascript]
tags: [javascript, 연산자]
---

{:toc .large-only}

## ??

`??`는 null 병합 연산자이다.

왼쪽 피연산자가 `null`이거나 u`ndefined`일 때 오른쪽 피연산자를 반환하고, 그렇지 않으면 왼쪽 피연산자를 반환한다.

```js
const foo = null ?? 'default string'
console.log(foo)
// 'default string'
```

## ||

`||`는 왼쪽 피연산자가 참(true)이면 왼쪽 피연산자를 반환하고, 그렇지 않으면 오른쪽 피연산자를 반환한다.

피연산자가 false인 경우는 아래와 같다.

- null
- NaN
- 0
- ''
- undefined

## ?? 와 || 의 차이

`||` 연산자는 왼쪽 피연산자 값이 `0`, `''` 일 때 오른쪽 피연산자를 반환하지만

`??` 연산자는 왼쪽 피연산자 값이 `0`, `''` 일 때 왼쪽 피연산자를 반환한다!

```js
const baz = 0 ?? 42
console.log(baz)
// 0

const qty = 0 || 42
console.log(qty)
// 42
```

## 참고사이트

[Nullish coalescing operator](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing)<br/>
[Logical OR (||)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_OR)
