---
title: '자바스크립트 함수의 구성, 매개변수(parameter)와 인수(argument)'
categories: [JAVASCRIPT]
tags: [javascript, parameter, argument]
---

{:toc .large-only}

<img src="/assets/img/blog/2022-04-04-javascript-parameter-argument.png">

### 함수 이름

- 식별자
- 이름이 있는 함수를 기명 함수, 없는 함수를 무명/익명 함수라 한다.

### 매개변수 (parameter)

- = 인자
- 0개 이상의 매개변수를 소괄호로 감싸고 쉼표로 구분한다.
- 각 매개변수에는 함수를 호출할 때 지정한 인수가 <u>순서대로</u> 할당된다.
- 함수를 정의할 때 선언하며, 함수 내부에서 변수와 동일하게 취급된다.
- 함수가 호출될 때 값을 전달받으면 매개변수에 값이 정의된다.

### 인수 (argument)

- 값으로 평가할 수 있는 표현식이어야 한다.
- 함수를 호출할 때 지정하며, 개수와 타입에 제한이 없다.
- 인수로 전달한 값은 매개변수를 통해 사용 가능하게 된다.

<br/>

```js
// 함수 선언문
function add(x, y) {
  // x, y => 매개변수
  return x + y
}

// 함수 호출
// 인수 1과 2가 매개변수 x, y에 순서대로 할당되고 함수 몸체의 문들이 실행된다.
var result = add(1, 2) // 1, 2 => 인수
```

<br/>

모던 자바스크립트 Deep Dive - 157p, 168p<br/>
[인수(Argument)와 인자(Parameter, 매개변수)의 차이](https://amagrammer91.tistory.com/9)
