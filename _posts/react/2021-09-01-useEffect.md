---
title: "useEffect 동작 원리, 사용하기"
categories: [React]
tags: [react, useEffect]
---

{:toc .large-only}

## useEffect()

`useEffect()`를 사용하여 side effect를 수행할 수 있습니다.

useEffect Hook을 componentDidMount와 componentDidUpdate, componentWillUnmount가 합쳐진 것으로 생각해도 좋습니다.

## useEffect가 하는 일은 무엇일까요?

- useEffect Hook을 이용하여 우리는 리액트에게 컴포넌트가 렌더링 이후에 어떤 일을 수행해야 하는지를 말합니다.

- 리액트는 우리가 넘긴 함수를 기억했다가(이 함수를 ‘effect’라고 부릅니다) **DOM 업데이트를 수행한 이후에** 불러낼 것입니다.

## useEffect를 컴포넌트 안에서 불러내는 이유는 무엇일까요?

- useEffect를 컴포넌트 내부에 둠으로써 클로저를 이용하여 effect를 통해 count state 변수(또는 그 어떤 prop에도)에 접근할 수 있게 됩니다.

## useEffect는 렌더링 이후에 매번 수행되는 걸까요?

- 네, 기본적으로 **첫번째 렌더링과 이후의 모든 업데이트에서 수행**됩니다.

- **리액트는 effect가 수행되는 시점에 이미 DOM이 업데이트되었음을 보장합니다.**

## 정리(clean-up)를 이용하는 Effects

외부 데이터에 구독(subscription)을 설정해야 하는 경우를 생각해보겠습니다.

이런 경우에 메모리 누수가 발생하지 않도록 정리(clean-up)하는 것은 매우 중요합니다.

effect가 함수를 반환하면 리액트는 컴포넌트가 마운트 해제되는 때에 정리(clean-up)를 실행합니다.

```js
useEffect(() => {
  ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
  // effect 이후에 어떻게 정리(clean-up)할 것인지 표시합니다.
  return function cleanup() {
    ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
  };
});
```

## Effect를 건너뛰어 성능 최적화하기

`useEffect()`에 두 번째 인자로 배열을 전달하지 않으면 effect는 매 렌더링마다 실행됩니다.

```js
useEffect(() => {
  document.title = `You clicked ${count} times`;
}, [count]); // count가 바뀔 때만 effect를 재실행합니다.
```

<br/>

위의 예시에서 우리는 [count]를 두 번째 인수로 넘깁니다.

만약 count가 5이고 컴포넌트가 리렌더링된 이후에도 여전히 count는 변함없이 5라면 리액트는 effect를 건너뛰게 됩니다.

이런 식으로 **최적화가 가능**합니다.

effect를 실행하고 이를 정리(clean-up)하는 과정을 마운트와 마운트 해제 시에 딱 한 번씩만 실행하고 싶다면, 빈 배열([])을 두 번째 인수로 넘기면 됩니다.

이렇게 함으로써 effect는 한 번만 실행되며 effect 안의 prop과 state는 초깃값을 유지하게 됩니다.

## 참고사이트

[Using the Effect Hook](https://ko.reactjs.org/docs/hooks-effect.html)<br/>
[[React] useEffect의 동작 원리](https://jungpaeng.tistory.com/92)
