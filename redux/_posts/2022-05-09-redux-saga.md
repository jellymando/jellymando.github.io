---
layout: post
title: "[Redux-Saga] 리액트 hook과 함께 사용하기"
sitemap: false
---

{:toc .large-only}

## Using Hooks in a React Redux App

클래스형 컴포넌트에서 `connect()`로 감싼 것처럼, 함수형 컴포넌트에서는 먼저 App을 `<Provider>`로 감싸주어야 한다.

```js
const store = createStore(rootReducer);

// As of React 18
const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  <Provider store={store}>
    <App />
  </Provider>
);
```

## React Redux hooks APIs

React Redux hooks API를 가져와서 함수형 컴포넌트 안에서 사용한다.

### useSelector()

Redux 저장소에서 상태 데이터를 가져온다.

```js
import React from "react";
import { useSelector } from "react-redux";

export const CounterComponent = () => {
  const counter = useSelector((state) => state.counter);
  return <div>{counter}</div>;
};
```

`useSelector`를 사용하면 구성 요소가 렌더링될 때마다 셀렉터의 새 인스턴스가 생성된다.

### createSelector()

`createSelector()`는 **셀렉터 메모이징** 기능이 있는 API이다.

`reselect` 패키지를 설치하여 사용한다.

```bash
npm install reselect

yarn add reselect
```

상태값을 추출하는 <u>input 셀렉터(여러개 가능)와, 추출된 값을 인자로 받아 값을 반환하는 output 셀렉터</u>를 인자로 전달하여 사용한다.

생성된 셀렉터가 여러번 호출되어도 추출된 값이 변경된 경우에만 출력한다.

```js
import React from "react";
import { useSelector } from "react-redux";
import { createSelector } from "reselect";

const selectNumCompletedTodos = createSelector(
  (state) => state.todos, // input 셀렉터
  (todos) => todos.filter((todo) => todo.completed).length // output 셀렉터
);

export const CompletedTodosCounter = () => {
  const numCompletedTodos = useSelector(selectNumCompletedTodos);
  return <div>{numCompletedTodos}</div>;
};

export const App = () => {
  return (
    <>
      <span>Number of completed todos:</span>
      <CompletedTodosCounter />
    </>
  );
};
```

복수의 input 셀렉터를 전달하는 경우,

```js
import { createSelector } from "reselect";

const selectShopItems = (state) => state.shop.items;
const selectTaxPercent = (state) => state.shop.taxPercent;

const selectSubtotal = createSelector(selectShopItems, (items) =>
  items.reduce((subtotal, item) => subtotal + item.value, 0)
);

const selectTax = createSelector(
  selectSubtotal,
  selectTaxPercent,
  (subtotal, taxPercent) => subtotal * (taxPercent / 100) // input 셀렉터에서 추출한 state를 인자로 사용
);

const selectTotal = createSelector(
  selectSubtotal,
  selectTax,
  (subtotal, tax) => ({ total: subtotal + tax }) // input 셀렉터에서 추출한 state를 인자로 사용
);
```

## useDispatch()

Redux 스토어에서 `dispatch` 함수에 대한 참조를 반환한다.

```js
import React from "react";
import { useDispatch } from "react-redux";

export const CounterComponent = ({ value }) => {
  const dispatch = useDispatch();

  return (
    <div>
      <span>{value}</span>
      <button onClick={() => dispatch({ type: "increment-counter" })}>
        Increment counter
      </button>
    </div>
  );
};
```

하위 요소에 `dispatch`를 사용하여 콜백을 전달할 때 `useCallback`을 사용하면 콜백을 메모할 수 있다.

```js
import React, { useCallback } from "react";
import { useDispatch } from "react-redux";

export const CounterComponent = ({ value }) => {
  const dispatch = useDispatch();
  const incrementCounter = useCallback(
    () => dispatch({ type: "increment-counter" }),
    [dispatch]
  );

  return (
    <div>
      <span>{value}</span>
      <MyIncrementButton onIncrement={incrementCounter} />
    </div>
  );
};

export const MyIncrementButton = React.memo(({ onIncrement }) => (
  <button onClick={onIncrement}>Increment counter</button>
));
```

일반적으로 `store` 인스턴스는 앱에서 변경되지 않는다.

따라서 동일한 `store` 인스턴스가 `<Provider>`에게 전달되는 한 `dispatch` 값은 안정적이다.

하지만 React hooks의 lint 규칙에서 `dispatch`를 `useEffect`, `useCallback`의 종속성 배열에 추가해야 한다고 경고하므로 의존성 배열에 `dispatch`를 추가해주는 것이 좋다.

## 참고사이트

[React Redux​](https://react-redux.js.org/api/hooks#using-hooks-in-a-react-redux-app)<br/>
[Reselect​](https://github.com/reduxjs/reselect)<br/>
[React(61) React Toolkit - createSelector 사용하기](https://devbirdfeet.tistory.com/189)<br/>
[how to use redux-sagas with react-hooks](https://stackoverflow.com/questions/57781631/how-to-use-redux-sagas-with-react-hooks/57781632#57781632)
