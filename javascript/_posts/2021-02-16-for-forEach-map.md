---
layout: post
title: "for, forEach, map의 차이점"
sitemap: false
---

{:toc .large-only}

## for()

조건문은 조건을 검사합니다.

만약 조건문이 참이라면, 그 반복문은 실행됩니다.

만약 조건문이 거짓이라면, 그 for문은 종결됩니다.

```js
var step;
for (step = 0; step < 5; step++) {
  // Runs 5 times, with values of step 0 through 4.
  console.log("Walking east one step");
}
```

## forEach()

배열의 각 요소에 대해 callback을 실행합니다.

중간에 return 할 수 없음

```js
const array1 = ["a", "b", "c"];

array1.forEach((element) => console.log(element));

// expected output: "a"
// expected output: "b"
// expected output: "c"
```

#### for 반복문을 forEach()로 바꾸기

```js
const items = ["item1", "item2", "item3"];
const copy = [];

// 이전
for (let i = 0; i < items.length; i++) {
  copy.push(items[i]);
}

// 이후
items.forEach(function (item) {
  copy.push(item);
});
```

## map()

배열의 각 요소에 대해 callback을 실행하고 실행결과를 모은 새 배열을 리턴합니다.

중간에 return 할 수 없음

```js
const animals = ["lion", "tiger"];
rr = animals.map((animal) => {
  console.log(animal);
});
console.log(rr); // [undefined, undefined]
// [콘솔 출력 결과]
// lion
// tiger
// [undefined, undefined]
```
