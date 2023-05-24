---
layout: post
title: '모듈 순환 참조(Circular Dependency) 에러'
sitemap: false
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

## Circular Dependency

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
1. b 모듈에서 a 모듈을 참조하고 있지만 위에서 이미 실행했기 때문에 a 모듈을 실행하지 않는다.
1. b 모듈에서 `sayHello`를 실행하지만 `aModuleObject.sayHello`가 존재하지 않으므로 에러가 발생한다.

## 참고사이트

[JS 모듈 시스템과 순환 참조 문제](https://ljs0705.medium.com/js-%EB%AA%A8%EB%93%88-%EC%8B%9C%EC%8A%A4%ED%85%9C%EA%B3%BC-%EC%88%9C%ED%99%98-%EC%B0%B8%EC%A1%B0-%EB%AC%B8%EC%A0%9C-a9e0c90c07e5)<br/>
[모듈 소개](https://ko.javascript.info/modules-intro)<br/>
[circular-dependency-plugin](https://www.npmjs.com/package/circular-dependency-plugin)
