---
layout: post
title: "[Redux] 기초 배우기"
sitemap: false
---

{:toc .large-only}

## 구성

### Action

상태를 변경시킬 때 객체 타입의 액션을 발생시킨다.

액션 객체는 type 필드를 필수적으로 포함해야 하며, type은 작업을 설명하는 이름을 제공하는 문자열이어야 한다. ex) `todos/todoAdded`

일반적으로 슬래시 기준 첫 번째 값은 이 작업이 속한 기능 또는 범주이고 두 번째 부분은 발생한 특정 일이다.

이 외에 작업에 대한 추가 정보를 payload 등의 추가 필드에 입력하기도 한다.

```js
const addTodoAction = {
  type: "todos/todoAdded",
  payload: "Buy milk",
};
```

### Action Creator

파라미터를 받아와서 액션 객체를 반환하는 함수

```js
const addTodo = (text) => {
  return {
    type: "todos/todoAdded",
    payload: text,
  };
};
```

### Reducer

**state와 action을 인자로 받아 상태를 업데이트하고 새로운 상태를 반환**하는 함수이다.

수신된 액션 type에 따라 이벤트를 처리하는 이벤트 리스너로 생각할 수 있다.

```js
function counter(state, action) {
  switch (action.type) {
    case "INCREASE":
      return state + 1;
    case "DECREASE":
      return state - 1;
    default:
      return state;
  }
}
```

### Store

리덕스에서는 애플리케이션당 하나의 store 객체를 만들게 된다.

스토어는 `configureStore()` 메서드에 리듀서를 전달하여 생성한다.

스토어 안에는 상태와 리듀서가 들어있고, 추가적으로 몇가지 내장 함수들이 있다.

```js
import { configureStore } from "@reduxjs/toolkit";

const store = configureStore({ reducer: counterReducer });

console.log(store.getState());
// {value: 0}
```

### Dispatch

스토어의 내장 메서드로 **상태를 업데이트하는 유일한 방법**

**`store.dispatch()` 메서드에 액션을 전달하면 리듀서 함수를 통해 상태를 업데이트한다.**

```js
store.dispatch({ type: "counter/increment" });

console.log(store.getState());
// {value: 1}

const increment = () => {
  return {
    type: "counter/increment",
  };
};

store.dispatch(increment());

console.log(store.getState());
// {value: 2}
```

## 참고사이트

[Redux Essentials, Part 1: Redux Overview and Concepts](https://redux.js.org/tutorials/essentials/part-1-overview-concepts)<br/>
[1. 리덕스에서 사용되는 키워드 숙지하기](https://react.vlpt.us/redux/01-keywords.html)
