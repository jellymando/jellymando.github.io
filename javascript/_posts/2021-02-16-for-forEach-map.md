---
layout: post
title: "for, forEach, map의 차이점"
sitemap: false
---

{:toc .large-only}

## for()

for문은 조건을 검사하는 조건문이다.

만약 조건문이 참이라면, 그 반복문은 실행된다.

만약 조건문이 거짓이라면, 그 for문은 종결된다.

```js
var step;
for (step = 0; step < 5; step++) {
  // Runs 5 times, with values of step 0 through 4.
  console.log("Walking east one step");
}
```

## forEach()

배열의 각 요소에 대해 callback 함수를 실행한다.

**값을 return 할 수 없다.**

```js
let arr = [1, 2, 3, 4, 5];
let a = arr.forEach(function (value) {
  return value;
});
console.log(a); //undefined
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

forEach와 같이 배열의 각 요소에 대해 callback 함수를 실행한다.

하지만, 다른 점은 callback 함수의 실행 결과인 **return 값으로 새로운 배열을 생성**한다는 점이다.

```js
const animals = ["lion", "tiger"];
const newAnimals = animals.map((animal) => {
  console.log(animal);
});
console.log(newAnimals); // [undefined, undefined]
// [콘솔 출력 결과]
// lion
// tiger
// [undefined, undefined]
```

위 코드에서 newAnimals를 콘솔창에 찍어보면 `[undefined, undefined]`로 출력된다.

값을 return 하지 않았기 때문에 순회했던 개수만큼의 undefined 원소가 출력된 것이다.

따라서 아래와 같이 값을 return 시켜야만 새로운 배열에 값이 추가된다.

```js
const animals = ["lion", "tiger"];
newAnimals = animals.map((animal) => {
  console.log(animal);
  return "mammal " + animal;
});
console.log(newAnimals); // ["mammal lion", "mammal tiger"]
// [콘솔 출력 결과]
// lion
// tiger
// ["mammal lion", "mammal tiger"]
```

<br/>

[[JavaScript] for vs. forEach vs. map](https://m.blog.naver.com/wideeyed/221877912230)<br/>
[Array.prototype.map()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)<br/>
[forEach()와 map()의 차이점](https://dream-frontend.tistory.com/341)
