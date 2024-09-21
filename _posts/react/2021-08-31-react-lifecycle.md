---
title: "✅리액트 컴포넌트의 생명주기"
categories: [REACT]
tags: [react]
---

{:toc .large-only}

## 클래스형 컴포넌트의 생명주기

<img src="/assets/img/blog/2021-08-31-react-lifecycle_01.png">

<br/>

### `constructor()`

- React 컴포넌트의 생성자는 해당 컴포넌트가 마운트되기 전에 호출됩니다.
- React에서 생성자는 보통 아래의 두 가지 목적을 위하여 사용됩니다:
  - this.state에 객체를 할당하여 지역 state를 초기화
  - 인스턴스에 이벤트 처리 메서드를 바인딩

### `render()`

- render() 메서드는 클래스 컴포넌트에서 반드시 구현돼야 하는 유일한 메서드입니다.
- 보통 JSX를 사용하여 React 엘리먼트를 생성합니다. 예를 들어, `<div />`와 `<MyComponent />`는 React가 DOM 노드 또는 사용자가 정의한 컴포넌트를 만들도록 지시하는 React 엘리먼트입니다.

### `componentDidMount()`

- 컴포넌트가 마운트된 직후, 즉 DOM에 삽입된 직후에 호출됩니다.
- 네트워크 요청, 데이터 구독 설정에 적절한 위치입니다.
- `componentDidMount()`에서 즉시 `setState()`를 호출하는 경우 `render()`가 두 번 호출되는 <u>추가적인 렌더링이 발생하지만, 브라우저가 화면을 갱신하기 전에 이루어질 것입니다.</u> 이 경우 사용자는 그 중간 과정을 볼 수 없을 것입니다.
- 모달(Modal) 또는 툴팁과 같이 **렌더링에 앞서 DOM 노드의 크기나 위치를 먼저 측정해야 하는 경우** 이러한 방식이 필요할 수 있습니다.

### `shouldComponentUpdate()`

- `shouldComponentUpdate()`를 사용하면 현재 state 또는 props의 변화가 컴포넌트의 출력 결과에 영향을 미치는지 여부를 React가 알 수 있습니다.
- props 또는 state가 새로운 값으로 갱신되어서 렌더링이 발생하기 직전에 호출됩니다. 기본값은 true입니다.
- `shouldComponentUpdate()`가 false를 반환할 경우 `render()`, `componentDidUpdate()`는 호출되지 않습니다.

### `componentDidUpdate()`

- 이 메서드는 최초 렌더링에서는 호출되지 않으며 갱신이 일어난 직후에 호출됩니다.
- **컴포넌트가 갱신되었을 때 DOM을 조작하기 위하여 이 메서드를 활용**하면 좋습니다.

### `componentWillUnmount()`

- 컴포넌트가 DOM 상에서 제거(마운트 해제)될 때에 호출됩니다.
- 이 메서드 내에서 타이머 제거, 네트워크 요청 취소, **componentDidMount() 내에서 생성된 구독 해제** 등 필요한 모든 정리 작업을 수행하세요.

<br/>

> [주의] <br/> 아래 메서드는 기존에 사용되었지만 이제는 사용하면 안 됩니다. <br/> `UNSAFE_componentWillUpdate()`, `UNSAFE_componentWillReceiveProps()`

<br/>

<img src="/assets/img/blog/2021-08-31-react-lifecycle_02.png">

## 참고사이트

[React.Component](https://ko.reactjs.org/docs/react-component.html)
