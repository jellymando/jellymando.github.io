---
layout: post
title: 'bind / call / apply 사용법, 차이점'
sitemap: false
---

{:toc .large-only}

## bind

`bind()` 메서드가 호출되면 **새로운 함수를 생성**한다.

바인딩으로 감싼(wrapped) 원본 함수 객체이다.

```js
const handleClick = this.handleClick.bind(this)
```

## call

`call()` 메서드는 주어진 this 값 및 각각 전달된 인수와 함께 **함수를 호출**한다.

```js
const openDocument = document.open

// openDocument()로 호출하면 에러가 나기 때문에 call을 이용한다.
openDocument.call(document)
```

## apply

`apply()` 메서드는 주어진 this 값과 배열 (또는 유사 배열 객체)로 제공되는 인수로 **함수를 호출**한다.

## 정리

bind는 함수를 바인딩하여 새로운 함수를 만들고, call, apply는 함수를 실행한다.

세 메서드 모두 this를 인수로 전달하여 바라보게 한다는 점은 같다.

## 참고사이트

[binding의 개념과 call, apply, bind의 차이점](https://wooooooak.github.io/javascript/2018/12/08/call,apply,bind/)<br/>
[Function.prototype.call()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Function/call)<br/>
[Function.prototype.bind()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)
