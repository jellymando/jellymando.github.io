---
title: '모듈 순환 참조(Circular Dependency) 개선하기'
categories: [JAVASCRIPT]
tags: [javascript, 순환 참조]
---

{:toc .large-only}

## 모듈 동작 원리

모듈 순환 참조의 문제를 보기에 앞서 브라우저에서 모듈이 어떻게 동작하는지 먼저 알아보자.

```js
// index.js
import './a.js'

// a.js
import { sayHello } from './b.js'
export const NAME = 'mike'
sayHello()

// b.js
import { NAME } from './a.js'
export const sayHello = () => {
  console.log('hello~!', NAME)
}
```

`import`를 통해 모듈을 가져오면 브라우저는 <u>모듈을 평가한 다음</u>, 이를 실행한다.

모든 모듈은 **모듈 객체**를 갖고 있으며, 모듈이 내보내는 변수와 함수는 모듈 객체에 추가된다.

위의 코드에서 `sayHello`는 아래와 같이 표현될 수 있다.

```js
export const sayHello = () => {
  console.log('hello~!', aModuleObject.NAME)
}
```

동일한 모듈을 여러 곳에서 참조해도 모듈은 **최초 호출 시 단 한 번만** 실행된다.

```js
// alert.js
alert("모듈이 평가되었습니다!");

// a.js
import `alert.js`;
// 모듈이 평가되었습니다!
import `b.js`;

// b.js
import `alert.js`;
// 아무 일도 발생하지 않는다.
```

## Circular Dependency (순환 참조)

이제 모듈의 순환 참조가 왜 에러를 발생시키는지 보자.

```js
// index.js
import './a.js'

// a.js
import { NAME } from './b.js'
export const sayHello = () => {
  console.log('hello~!', NAME)
}

// b.js
import { sayHello } from './a.js'
export const NAME = 'mike'
sayHello()
```

1. index.js에서 a 모듈을 평가한다.
1. a 모듈에서 b 모듈을 평가한다.
1. b 모듈에서 a 모듈을 참조하고 있지만 위에서 이미 평가했기 때문에 a 모듈을 평가하지 않는다.
1. b 모듈에서 `sayHello`를 실행하지만 `aModuleObject.sayHello`가 존재하지 않으므로 에러가 발생한다.

## 순환 끊기

### 최하위 모듈 만들기

a와 b 모듈에서 모두 의존하는 최하위 모듈을 만드는 방법도 있다.

```js
// index.js
import './modules.js'

// modules.js
export * from './a.js'
export * from './b.js'

// a.js
import { sayHello } from './modules.js'
export const NAME = 'mike'
sayHello()

// b.js
import { NAME } from './modules.js'
export const sayHello = () => {
  console.log('hello~!', NAME)
}
```

modules.js 파일을 만들어서 a.js와 b.js를 export 한다.

a와 b 모듈을 사용할 때 modules에서 가져온다.

<img src="/assets/img/blog/2022-10-25-Circular-Dependancy_01.png" style="margin:30px 0">

이렇게 하면 a와 b가 서로 직접 의존하지 않으며, modules에서 NAME과 sayHello를 export하는 것과 같은 결과가 된다.

주의할 점은, modules에서 a와 b를 import할 때 평가 순서를 주의해야 한다.

만약 a보다 b를 먼저 export 한다면 NAME 변수가 정의되기 전이므로 에러가 발생한다.

### 의존성 역전시키기

예제 코드에서 의존성의 방향은 index.js -> a.js -> b.js 이다. 즉 모듈간의 순위는 index > a > b 이다.

a는 b보다 순위가 높으므로 b를 참조할 수 있지만, b는 a를 참조해선 안 된다.

에러가 나는 원인은 b가 a를 참조했기 때문이다.

b에서 의존하고 있는 sayHello 함수를 a에서 b로 이동시킨다.

```js
// index.js
import './a.js'

// a.js
import { sayHello } from './b.js'
sayHello()

// b.js
export const NAME = 'mike'
export const sayHello = () => {
  console.log('hello~!', NAME)
}
```

<img src="/assets/img/blog/2022-10-25-Circular-Dependancy_02.png" style="margin:30px 0">

이렇게하면 모듈 평가 순위에 거스르지 않아서 에러가 발생하지 않는다.

## 참고사이트

[JS 모듈 시스템과 순환 참조 문제](https://ljs0705.medium.com/js-%EB%AA%A8%EB%93%88-%EC%8B%9C%EC%8A%A4%ED%85%9C%EA%B3%BC-%EC%88%9C%ED%99%98-%EC%B0%B8%EC%A1%B0-%EB%AC%B8%EC%A0%9C-a9e0c90c07e5)<br/>
[모듈 소개](https://ko.javascript.info/modules-intro)<br/>
[circular-dependency-plugin](https://www.npmjs.com/package/circular-dependency-plugin)
