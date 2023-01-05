---
layout: post
title: '[Redux-Saga] 이펙트를 사용하여 비동기 처리 saga 만들기'
sitemap: false
---

{:toc .large-only}

## redux-saga의 이펙트

Saga는 명령을 만들어주기만 하고, 이 명령에 따른 직접적인 처리는 미들웨어가 한다.

이펙트는 Saga의 미들웨어가 실행할 수 있는 명령들이다.

### take

take를 호출하면 해당 액션이 디스패치 될 때까지 기다렸다가, 디스패치되면 다음 코드를 실행한다.

```js
function* watchLogIn() {
  yield take('LOG_IN', logIn) // LOG_IN 액션이 디스패치되면 logIn 함수 실행
}
```

### call

call을 호출하면 비동기 함수를 동기적으로 실행할 수 있다.

미들웨어는 call에 전달된 Promise가 완료될 때까지 Saga를 일시중단하고 Promise가 해결되면 다음 코드를 실행한다.

### fork

fork을 호출하면 비동기 함수를 실행한다.

미들웨어는 fork에 전달된 Promise가 완료될 때까지 Saga를 일시중단하지 않고 다음 코드를 실행한다.

### takeEvery

takeEvery를 사용하면 특정 액션이 디스패치될 때 함수를 실행한다.

```js
import { put, takeEvery } from 'redux-saga/effects'

function* incrementSaga() {
  yield delay(1000)
  yield put({ type: 'INCREMENT' })
}

function* watchIncrementSaga() {
  yield takeEvery('INCREMENT_ASYNC', incrementSaga) //INCREMENT_ASYNC 액션이 디스패치되면 incrementSaga 실행
}
```

### takeLastest

takeEvery와 마찬가지로 특정 액션이 디스패치되면 함수를 실행한다.

대신 takeLastest를 사용하면 기존에 실행중인 작업이 있다면 취소하고 가장 마지막 작업만 실행한다.

```js
import { takeLatest } from 'redux-saga/effects'

function* watchFetchDataSaga() {
  yield takeLatest('FETCH_REQUESTED', fetchData) //FETCH_REQUESTED 액션에 대해서 기존에 진행 중이던 작업이 있다면 취소하고 가장 마지막으로 실행된 작업에 대해서만 fetchData를 실행
}
```

### all

제너레이터 함수를 배열의 형태로 인자로 넣어주면 제너레이터 함수들이 병행적으로 동시에 실행되고, 전부 resolve 될 때까지 기다린다.

```js
import { takeEvery } from 'redux-saga/effects'

export default function* rootSaga() {
  yield all([helloSaga(), watchIncrementSaga(), watchFetchDataSaga()])
}
```

## 비동기 처리 saga 만들기

```js
function asyncIncrement() {
  return async (dispatch) => {
    await delay(1000)
    dispatch({ type: 'INCREMENT' })
  }
}
```

이펙트를 사용하여 위 비동기 함수를 Saga로 만들면 아래와 같다.

```js
import { delay } from 'redux-saga'
import { put } from 'redux-saga/effects'

export function* incrementSaga() {
  yield call(delay, 1000)
  yield put({ type: 'INCREMENT' })
}
```

## 참고사이트

[Making Asynchronous calls](https://redux-saga.js.org/docs/introduction/BeginnerTutorial/#making-asynchronous-calls)<br/>
[Redux-Saga: 제너레이터와 이펙트](https://meetup.toast.com/posts/140)<br/>
[API Reference](https://redux-saga.js.org/docs/api/#forkfn-args)<br/>
[Using Saga Helpers](https://redux-saga.js.org/docs/basics/UsingSagaHelpers/)<br/>
[all([...effects]) - parallel effects​](https://redux-saga.js.org/docs/api/#alleffects---parallel-effects)<br/>
[redux-saga의 주요함수(delay, call, put, all, takeEvery, takeLatest)](https://sustainable-dev.tistory.com/94)
