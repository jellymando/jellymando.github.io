---
title: "Promise를 이용하여 실행 지연시키기 (I hate Promise)"
categories: [JAVASCRIPT]
tags: [javascript, promise, 비동기]
---

{:toc .large-only}

async/await, Promise를 사용하여 일정 시간 뒤에 실행되는 함수를 만들어 보자.

코드 구조는 아래와 같다.

```js
const a = async () => {
  console.log("1");
  await stay();
  console.log("2");
};

a();
```

`stay()` 함수에서 3초 지연된 후 다음 코드(`console.log("2")`)를 실행하게 만들어야 한다.

`stay()` 함수를 아래와 같이 작성하면 어떨까?

```js
const stay = () => {
  return new Promise((resolve, reject) => {
    setTimeout(() => console.log("3초 기다려!"), 3000);
  });
};
```

3초 뒤 `3초 기다려!` 가 콘솔에 찍히지만, 다음 코드가 실행되진 않는다.

Promise 객체가 resolve를 호출하지 않아서이다.

resolve나 reject를 호출하지 않으면 Promise는 Pending 상태에서 다른 상태로 변경되지 않는다.

> 대부분의 코드는 Promise가 나중에 어떤 시점에 해결 또는 거부될 것이라고 예상하고 사용합니다. (그래서 Promise를 우선적으로 사용하게 되는 이유입니다.) 그렇지 않으면 코드는 일반적으로 작업을 끝내지 못할 것입니다.

때문에 setTimeout에서 resolve를 호출해줘야 한다.

```js
const stay = () => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve();
      console.log("3초 기다려!");
    }, 3000);
  });
};
```

혹은 `then()` 후속 처리 메서드를 사용해도 좋다.

```js
const stay = () => {
  return new Promise((resolve, reject) => {
    setTimeout(resolve, 3000);
  }).then(() => {
    console.log("3초 기다려!");
  });
};
```

<br/>

async/await 함수의 목적은 사용하는 여러 promise의 동작을 동기스럽게 사용할 수 있게 하고, 어떠한 동작을 여러 promise의 그룹에서 간단하게 동작하게 하는 것이다.

만약 Promise를 사용하지 않고 바로 setTimeout을 호출하면 await이 먹히지 않는다.

<br/>

[How to wrap setTimeout() method in a promise ?](https://www.geeksforgeeks.org/how-to-wrap-settimeout-method-in-a-promise/)<br/>
[Promise, 가만히 냅두면 어떻게 될까?](https://imch.dev/posts/what-happens-if-do-nothing-with-promise/)<br/>
[async function](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/async_function)
