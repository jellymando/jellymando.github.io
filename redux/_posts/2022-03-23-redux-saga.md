---
layout: post
title: "[Redux-Saga] 비동기 처리 saga 만들기"
sitemap: false
---

{:toc .large-only}

## 제너레이터 함수와 이펙트

```js
function asyncIncrement() {
  return async (dispatch) => {
    await delay(1000);
    dispatch({ type: "INCREMENT" });
  };
}
```

위 함수를 제너레이터 함수로 표현하면 아래와 같다.

```js
import { delay } from "redux-saga";
import { put } from "redux-saga/effects";

export function* incrementAsync() {
  yield call(delay, 1000);
  yield put({ type: "INCREMENT" });
}
```

`call`과 `put`는 redux-saga의 이펙트다.

**Saga는 yield 객체를 redux-saga 미들웨어에 전달하는 Generator 함수이다.**

Saga는 명령을 만들어주기만 하고, 이 명령에 따른 직접적인 처리는 미들웨어가 한다.

Saga가 이펙트를 yield 하면 미들웨어는 Promise가 완료될 때까지 Saga를 일시 중단한다.

**Promise가 해결되면 미들웨어는 Saga를 재개하여 다음 yield까지 코드를 실행한다.**

### take

특정 액션이 디스패치 될 때까지 기다린다.

```js
function* watchLogIn() {
  yield take("LOG_IN", logIn); // 'LOG_IN'이 디스패치되면 logIn 함수 실행
}
```

## 헬퍼 함수 사용하기

여러 개의 Saga를 한 번에 실행하기 위해 redux-saga의 헬퍼 함수를 사용한다.

```js
import { put, takeEvery, all } from "redux-saga/effects";

const delay = (ms) => new Promise((res) => setTimeout(res, ms));

function* helloSaga() {
  console.log("Hello Sagas!");
}

function* incrementAsync() {
  yield delay(1000);
  yield put({ type: "INCREMENT" });
}

function* watchIncrementAsync() {
  yield takeEvery("INCREMENT_ASYNC", incrementAsync);
}

function* watchFetchData() {
  yield takeLatest("FETCH_REQUESTED", fetchData);
}

// 이제 루트 사가만 내보내는 것에 주목하십시오.
// 모든 Sagas를 한 번에 시작하는 단일 진입점
export default function* rootSaga() {
  yield all([helloSaga(), watchIncrementAsync(), watchFetchData()]);
}
```

### takeEvery

`takeEvery` 헬퍼 함수를 사용하면 특정 액션이 dispatch 될 때마다 Saga를 실행한다.

만약 `watchIncrementAsync` Saga에서 액션이 여러번 dispatch 되면 `incrementAsync` 인스턴스가 여러개 실행된다.

### takeLastest

`takeLastest` 헬퍼 함수를 사용하면 `incrementAsync` 작업이 실행 중이면 이전 작업을 취소하고 새 작업을 시작한다.

즉, 최신 요청에 대한 응답만 가져올 수 있다.

### all

여러 이펙트를 병렬로 실행하고 모든 이펙트가 완료될 때까지 기다리도록 미들웨어에 지시한다.

## 참고사이트

[Making Asynchronous calls](https://redux-saga.js.org/docs/introduction/BeginnerTutorial/#making-asynchronous-calls)<br/>
[Redux-Saga: 제너레이터와 이펙트](https://meetup.toast.com/posts/140)<br/>
[Using Saga Helpers](https://redux-saga.js.org/docs/basics/UsingSagaHelpers/)<br/>
[all([...effects]) - parallel effects​](https://redux-saga.js.org/docs/api/#alleffects---parallel-effects)
