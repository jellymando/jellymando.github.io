---
layout: post
title: "for문과 for...of문, let과 const"
sitemap: false
---

{:toc .large-only}

## 의문의 시작

보통 for문에서는 변수를 선언할 때 let을, for...of문에서는 const를 사용하는데,

왜 그랬는지 까먹었다.

```js
for (const item of [1, 2, 3]) {
  console.log(item);
}
// 1, 2, 3
```

새삼 신기한 for...of문

MDN 문서를 보면 `블록 내부 변수를 수정하지 않는 경우` const를 사용할 수 있다고 한다.

## for문

### var

```js
for (var i = 0; i < 2; i++) {
  console.log(i);
}
// 0
// 1

// i
// 2
```

var 키워드를 이용해 변수 i를 선언하면 루프 외부에서도 i를 호출할 수 있다.

for문 루프를 다 돌고 i를 찍으면 2가 된다.

### let

```js
for (let i = 0; i < 2; i++) {
  console.log(i);
}
// 0
// 1

// i
// Uncaught ReferenceError: i is not defined
```

let 키워드를 이용해 변수 i를 선언하면 루프 외부에서 i를 호출할 수 없다.

let으로 선언된 변수는 for문 루프 안에서만 접근할 수 있다.

### const

```js
for (const i = 0; i < 2; i++) {
  console.log(i);
}
// 0
// Uncaught TypeError: Assignment to constant variable.
```

const 키워드를 이용해 변수 i를 선언하면 i의 값을 변경할 수 없으므로 에러가 발생한다.

즉, for문을 사용할 때는 let 키워드를 사용하는 것이 가장 효율적이다.

## for...of

### const

```js
for (const i of [1, 2, 3]) {
  console.log(i);
}
// 1
// 2
// 3
```

for문과는 달리 에러가 나지 않는다.

즉, **for...of문은 각 반복마다 새로운 블록 범위를 생성한다**는 것을 의미한다.

각각의 i가 새 블록의 새 변수로 선언되어 상수가 재할당되지 않음을 알 수 있다.

그러나 MDN 문서에서 참조한대로 블록 범위 내에서 i의 값을 수정하는 것은 되지 않는다.

```js
for (const i of [1, 2, 3]) {
  i *= 2;
  console.log(i);
}
// Uncaught TypeError: Assignment to constant variable.
```

### let

```js
for (const i of [1, 2, 3]) {
  i *= 2;
  console.log(i);
}
// 2
// 4
// 6
```

블록 범위 내에서 변수를 수정해야 할 때는 let 키워드를 사용해야 한다.

## 참고사이트

[ES6 Variable Declaration & For Loops — Why ‘const’ works in a ‘for…in’ loop but not in a normal ‘for’ loop](https://medium.com/@mautayro/es6-variable-declaration-for-loops-why-const-works-in-a-for-in-loop-but-not-in-a-normal-a200cc5467c2)
