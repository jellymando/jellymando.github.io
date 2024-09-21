---
title: "[lodash] 리액트에서 debounce나 throttle 사용하기"
categories: [React]
tags: [react, lodash, debounce, throttle]
---

{:toc .large-only}

리액트에서 `useRef`를 사용하여 debounce를 구현하려 했지만 잘 안되었다..

```js
const debounce = () => {
  if (timerRef.current) clearTimeout(timerRef.current);
  timerRef.current = setTimeout(() => {
    console.log("debounce");
  }, 200);
};

document.addEventListner("mousemove", (e) => debounce(e));
```

<br/>

위 코드로 동작했을 때 콘솔이 한 번만 찍혀야 하는데 이벤트가 발생하는 족족 찍혔다.

그래서 `lodash` 라이브러리를 설치하였다.

`lodash.debounce` 나 `lodash.throttle` 만 설치해도 사용할 수 있다.

```js
npm i --save lodash
//혹은
npm i --save lodash.debounce
```

<br/>

라이브러리 설치 후 아래와 같이 사용하면 된다.

```js
import debounce from "lodash.debounce";

const debounceSomethingFunc = debounce(() => {
  console.log("called debounceSomethingFunc");
}, 200);
```

<br/>

[[React/lodash] React에서 debounce 간단 사용방법](https://ithub.tistory.com/319)
