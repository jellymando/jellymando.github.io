---
title: "debounce와 throttle 사용하기"
categories: [JAVASCRIPT]
tags: [javascript, debounce, throttle]
---

{:toc .large-only}

## 들어가기에 앞서

debounce와 throttle은 주로 mousemove, scroll 등의 이벤트 쿼리 성능 향상에 사용한다.

이벤트 핸들러를 콜백함수로 전달하여 클로저를 이용해 일정시간 혹은 한번만 핸들러를 실행한다.

## debounce

발생한 이벤트에 대해 마지막 한 번만 실행

```js
const debounce = (func, delay) => {
  let timeoutId = null;
  return function (...args) {
    clearTimeout(timeoutId);
    timeoutId = setTimeout(() => {
      func(...args);
    }, delay);
  };
};
```

이벤트가 계속 발생해도 앞에서 발생한 setTimeout 값을 clearTimeout 하기 때문에 결국 맨 마지막에 발생한 이벤트만 실행된다.

## throttle

일정한 시간 간격을 두고 한 번씩만 실행

```js
const throttle = (func, delay) => {
  let timeoutId = null;
  return (...args) => {
    if (!timeoutId) {
      timeoutId = setTimeout(() => {
        timeoutId = null;
        func(...args);
      }, delay);
    }
  };
};
```

## 이벤트 리스너 핸들러로 바로 사용하기

`addEventListener`에 debounce나 throttle 함수를 바로 전달하면 먹히지 않는데, 이벤트가 발생할 때마다 `timeoutId`가 `null`로 초기화되기 때문이다!

`let timeoutId = null`을 `addEventListener` 바깥으로 빼주어야 한다.

```js
let timeoutId = null;
document.addEventListener("mousemove", ({ target }) => {
  if (!timeoutId) {
    timeoutId = setTimeout(() => {
      console.log("mousemove target", target);
      timeoutId = null;
    }, 300);
  }
});
```

## 에러 노트

setTimeout 함수 안에 함수를 실행시키는 방법

```js
setTimeout(func.bind(null, ...args), delay);
```

혹은

```js
setTimeout(() => {
  func(...args);
}, delay);
```

### args 파라미터 넣는 이유

```js
window.addEventListener(
  "resize",
  throttle(() => {
    console.log("resize");
  }, 500)
);
```

이벤트 핸들러는 이벤트 파라미터를 전달받아 실행되므로 아래 코드와 같다.

```js
window.addEventListener("resize", (event) =>
  throttle(() => {
    console.log("resize");
  }, 500)(event)
);
```

throttle은 클로저기 때문에 결국 아래와 같이 된다.

```js
window.addEventListener("resize", (event) => {
  (...args) => {
    if (!timeoutId) {
      timeoutId = setTimeout(() => {
        timeoutId = null;
        func(...args);
      }, delay);
    }
  }(event);
});
```

이벤트 핸들러로부터 이벤트 객체가 전달되므로 args는 이벤트 객체이다.

## 참고사이트

[쓰로틀링과 디바운싱](https://www.zerocho.com/category/JavaScript/post/59a8e9cb15ac0000182794fa)<br/>
[Debouce, Throttle (디바운스, 쓰로틀)](https://jinminkim-50502.medium.com/javascript-debouce-throttle-3f6618c13fb6)
