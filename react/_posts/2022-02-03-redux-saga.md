---
layout: post
title: "[Redux-Saga] 미들웨어 만들고 스토어에 연결하기"
sitemap: false
---

{:toc .large-only}

## Redux-Saga

액션을 모니터링하고 있다가, 특정 액션이 발생하면 이에 따라 특정 작업을 하는 Redux 미들웨어.

Generator 문법을 사용하여 비동기 흐름을 쉽게(?) 읽고, 쓰고, 테스트할 수 있다.

Saga를 실행하려면 아래 작업이 필요하다.

- Saga 만들기
- Saga 미들웨어 만들기
- Saga 미들웨어를 Redux 스토어에 연결하기

## Saga 만들기

제너레이터를 이용하여 Saga를 만든다.

```js
// sagas.js
export function* helloSaga() {
  console.log("Hello Sagas!");
}
```

## Saga 미들웨어를 Redux 스토어에 연결하기

```js
// main.js
import { createStore, applyMiddleware } from "redux";
import createSagaMiddleware from "redux-saga";

// ...
import { helloSaga } from "./sagas";

const sagaMiddleware = createSagaMiddleware();
const store = createStore(reducer, applyMiddleware(sagaMiddleware));
sagaMiddleware.run(helloSaga);

const action = (type) => store.dispatch({ type });
```

- 앞에서 만든 Saga를 import 한다.
- `createSagaMiddleware()`를 사용하여 Saga 미들웨어를 만든다.
- `applyMiddleware`를 사용하여 미들웨어를 스토어에 연결한다.
- `sagaMiddleware.run(helloSaga)`로 Saga를 시작한다.

## 참고사이트

[튜토리얼](https://mskims.github.io/redux-saga-in-korean/introduction/BeginnerTutorial.html)
