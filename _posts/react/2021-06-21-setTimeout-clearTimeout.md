---
title: "리액트에서 setTimeout, clearTimeout 사용하기"
categories: [REACT]
tags: [react]
---

{:toc .large-only}

일반 함수에서는 var, let 등의 변수를 선언 후 `setTimeout` 값을 넣어 사용한다.

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

<br/>

리액트에서는 `useRef` hook을 이용하여 `setTimeout`을 사용할 수 있다.

```js
const timerRef = useRef(0);

useEffect(() => {
  if (timerRef.current) clearTimeout(timerRef.current);
  timerRef.current = setTimeout(() => {
    setIsOpen(!isOpen);
  }, 3000);
}, []);
```

`Ref` 생성 후 `.current` 에 `setTimeout` 값을 넣어 사용한다.

<br/>

[[React] setTimeout, clearTimeout](https://j3sung.tistory.com/647)
