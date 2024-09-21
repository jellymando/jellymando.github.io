---
title: '[Redux-Saga] race 이용하기'
categories: [React]
tags: [redux]
---

{:toc .large-only}

## Racing Effects

redux-saga에서 여러 태스크를 병렬로 실행할 때, 태스크 결과를 전부 기다리지 않고 먼저 들어온 태스크만 처리한다.

```js
import { race, call, put, delay } from 'redux-saga/effects'

function* fetchPostsWithTimeout() {
  const { posts, timeout } = yield race({
    posts: call(fetchApi, '/posts'),
    timeout: delay(1000)
  })

  if (posts) yield put({ type: 'POSTS_RECEIVED', posts })
  else yield put({ type: 'TIMEOUT_ERROR' })
}
```

위 예시에서 posts api가 1초 타임아웃보다 먼저 완료되면 `POSTS_RECEIVED`를, 그렇지 않다면 `TIMEOUT_ERROR`를 디스패치한다.

race의 다른 유용한 기능 중 하나는 경주에서 진 이펙트들을 자동으로 취소시키는 것이다.

```js
import { race, take, call } from 'redux-saga/effects'

function* backgroundTask() {
  while (true) { ... }
}

function* watchStartBackgroundTask() {
  while (true) {
    yield take('START_BACKGROUND_TASK')
    yield race({
      task: call(backgroundTask),
      cancel: take('CANCEL_TASK')
    })
  }
}
```

위 예제에서는 먼저 `START_BACKGROUND_TASK`가 디스패치 되기를 기다린다.

해당 값이 디스패치되면 무한 루프에서 실행되는 `backgroundTask`와 `CANCEL_TASK` 디스패치를 기다리는 경주가 시작된다.

`CANCEL_TASK` 디스패치되기 전까지 `backgroundTask`가 계속 실행된다.

`CANCEL_TASK`이 디스패치되면 race는 자동으로 `backgroundTask`를 취소하고 그 태스크 내부에 취소 에러를 throw 한다.

## 응용

race 기능을 응용하면 api 처리 순서를 비동기적으로 조작할 수 있다.

예를 들어, a, b 두 개의 api를 같이 호출하면 어떤 때는 a가 먼저 서버로부터 값이 넘어오고, 어떤 때는 b가 먼저 넘어오기도 한다.

a를 호출한 뒤 race를 걸어두면, a의 호출이 완료되어 값을 받거나 오류가 생긴 뒤에 b를 호출하도록 순서를 보장할 수 있다.

```js
function* backgroundTask() {
  yield call(a)
  yield race({
    success: take('SUCCESS_A'),
    failure: take('FAILURE_A')
  })
  yield call(b)
}
```

## 참고사이트

[Racing Effects](https://redux-saga.js.org/docs/advanced/RacingEffects/)<br/>
[여러 이펙트의 경주](https://mskims.github.io/redux-saga-in-korean/advanced/RacingEffects.html)
