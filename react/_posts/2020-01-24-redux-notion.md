---
layout: post
title: "REACT가 REDUX를 만나면..💏"
sitemap: false
---

{:toc .large-only}

## Redux 설치

```js
yarn add @reduxjs/toolkit
yarn add react-redux
```

## action 정의

> 어떤 변화가 일어나야 하는지 설명하는 객체

액션 유형과 타입을 반환하는 함수를 담은 파일을 만든다.

```js
export const INCREASE = "INCREASE";
export const DECREASE = "DECREASE";

export function increase() {
  return { type: "INCREASE" };
}

export function decrease() {
  return { type: "DECREASE" };
}
```

## Reducer 정의

> action 객체를 받았을 때, 데이터를 어떻게 처리할지 정의하는 객체

```js
import { INCREASE, DECREASE } from "../action/count";

export function counterReducer(state = { value: 0 }, action) {
  switch (action.type) {
    case INCREASE:
      return { value: state.value + 1 };
    case DECREASE:
      return { value: state.value - 1 };
    default:
      return state;
  }
}
```

## store 적용

createStore로 store를 생성하고 Provider로 컴포넌트를 감싸 store를 전달한다.

store.subscribe로 state를 구독하여 상태가 변할 때마다 리렌더링한다.

```js
import React from "react";
import ReactDOM from "react-dom";
import { createStore } from "redux";
import { Provider } from "react-redux";
import { counterReducer } from "./reducer/counter";
import App from "./App";

const store = createStore(counterReducer);

const render = () => {
  ReactDOM.render(
    <Provider store={store}>
      <App />
    </Provider>,
    document.getElementById("root")
  );
};

store.subscribe(render);
render();
```

## class형

connect를 통해 값과 함수를 props로 전달한다.

```js
import React from "react";
import { connect } from "react-redux";
import { increase, decrease } from "../action/count";

class Counter extends React.Component {
  render() {
    return (
      <div>
        <h1>{this.props.num}</h1>
        <button onClick={this.props.onIncrease}>+ 1</button>
        <button onClick={this.props.onDecrease}>- 1</button>
      </div>
    );
  }
}

const mapStateToProps = (state) => {
  return {
    num: state.value,
  };
};

const mapDispatchToProps = (dispatch) => {
  return {
    onIncrease: () => dispatch(increase()),
    onDecrease: () => dispatch(decrease()),
  };
};

Counter = connect(mapStateToProps, mapDispatchToProps)(Counter);
export default Counter;
```

## 함수형

useSelector, useDispatch로 값과 함수를 전달한다.

```js
import React, { useCallback } from "react";
import { useSelector, useDispatch } from "react-redux";
import * as actions from "../action/count";

const Counter = () => {
  const dispatch = useDispatch();

  const num = useSelector((state) => state.value);

  const onIncrease = useCallback(() => {
    dispatch(actions.increase());
  }, [dispatch]);

  const onDecrease = useCallback(() => {
    dispatch(actions.decrease());
  }, [dispatch]);

  return (
    <div>
      <h1>{num}</h1>
      <button onClick={onIncrease}>+ 1</button>
      <button onClick={onDecrease}>- 1</button>
    </div>
  );
};

export default Counter;
```

<br/>
[Redux 공식문서](https://redux.js.org/introduction/getting-started)<br/>
[Redux 적용하기 (함수형, Class 형)](https://velog.io/@eomttt/Redux-%EC%A0%81%EC%9A%A9%ED%95%98%EA%B8%B0-%ED%95%A8%EC%88%98%ED%98%95-Class-%ED%98%95)
