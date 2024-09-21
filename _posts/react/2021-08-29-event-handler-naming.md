---
title: "리액트 이벤트 핸들러 네이밍 (on / handle)"
categories: [REACT]
tags: [react, naming, convention]
---

{:toc .large-only}

## Props의 경우

- 컴포넌트에 전달하는 prop의 이름을 정의할 때는 보통 `onClick`과 같이 `on*` 접두사를 지정한다.
- 이를 통해 컴포넌트에게 <u>이 prop은 이런 이벤트 핸들러 기능을 수행하겠구나..</u> 라는 것을 암시할 수 있다.

## Function Names의 경우

- 실제로 호출되는 함수의 이름을 정해야 하는 경우 `handle`을 붙여 `handleClick`과 같이 사용한다.
- `onClick` 그리고 `handleClick` 과 같이 동일한 on과 handle 뒤에 동일한 Name을 Mapping 함으로써, 의미에 대한 혼란을 줄여주고 식별을 쉽게 만들 수 있다.

## 좀 더 복잡한 네이밍

이벤트와 핸들러가 더 많은 경우 아래 규칙에 따라 네이밍한다.

- 먼저, 명사를 맨 앞에 위치
- 그러고 나서 동사가 위치
- 그 후 이 개념을 중심으로 다른 이벤트가 추가될 경우, 알파벳 순으로 그룹화

```js
<MyComponent
  onAlertClick={this.handleAlertClick}
  onAlertHover={this.handleAlertHover}
  onFormSubmit={this.handleFormSubmit}
/>
```

## 주의

- 기본으로 제공되는 React 이벤트 핸들러 이름을 사용하는 경우 원치 않는 동작이 실행될 수 있다.

- 예를들어 아래 코드처럼 props를 부모 요소에도 Spread operator로 전달했을 경우 이벤트 버블링으로 인해 내부의 button의 onClick 이벤트가 먼저 실행된 후, div의 onClick 이벤트가 실행된다.

```js
function MyComponent(props) {
  return (
    <div {...props}>
      <button onClick={props.onClick}>Button</button>
    </div>
  );
}
```

## 정리

함수를 컴포넌트에 props로 전달하는 경우 prop 명에는 on을 붙이고, 전달해준 부모의 함수에는 handle을 붙인다.

만약 props로 전달하지 않고 컴포넌트 내에서 만든 함수를 바로 사용할 경우에는?

컴포넌트에 전달하는 prop 이름에 on을 붙이는 것처럼, on으로 이름짓는 게 실제 사용할 때 통일성 측면에서 좋을 것 같다.

## 예제

```js
<MyComponent onClickButton={this.handleClickButton} />
```

<br/>

```js
function MyComponent({ onClickButton }) {
  const onSubmitForm = () => {};
  return (
    <div>
      <button onClick={onClickButton}>Button</button>
      <form onSubmit={onSubmitForm}></form>
    </div>
  );
}
```

## 참고사이트

[[번역] React의 이벤트 핸들러 네이밍 (Event handler naming in react)](https://blog.sonim1.com/220)
