---
title: "배열에서 중복을 제거하는 3가지 방법"
categories: [JAVASCRIPT]
tags: [javascript]
---

{:toc .large-only}

## Set

배열을 Set 인스턴스로 만들어 중복 제거 후, 스프레드 연산자로 배열로 반환

```js
const dupArr = [1, 2, 3, 1, 2];

const set = new Set(dupArr);

const uniqueArr = [...set];
```

## filter(), indexOf()

`filter()`와 `indexOf()`로 <u>특정값이 처음으로 나타나는 index를 필터링</u>하여 새로운 배열로 반환

```js
const dupArr = [1, 2, 3, 1, 2];

const uniqueArr = dupArr.filter((element, index) => {
  return dupArr.indexOf(element) === index;
});
```

## forEach(), includes()

`forEach()`와 `includes()`를 사용하여 배열을 순회하며 새로운 배열에 중복되지 않는 요소를 담는다.

```js
const dupArr = [1, 2, 3, 1, 2];

let uniqueArr = [];
dupArr.forEach((element) => {
  if (!uniqueArr.includes(element)) {
    uniqueArr.push(element);
  }
});
```

## 참고사이트

[[Javascript] 배열 중복 제거하는 3가지 방법](https://hianna.tistory.com/422)
