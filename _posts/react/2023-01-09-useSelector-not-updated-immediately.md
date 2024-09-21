---
title: "react-redux 상태가 동기적으로 업데이트되지 않음"
categories: [React]
tags: [redux, useSelector]
---

{:toc .large-only}

## redux 상태 업데이트 전/후 콘솔 찍기

```js
const handleClick = () => {
  console.log("before count", count);
  dispatch(increment());
  console.log("after count", count);
};

return <button onClick={handleClick}>디스패치!</button>;
```

increment는 count 상태를 1씩 증가시키는 액션 함수이다.

버튼을 클릭하여 콘솔을 찍어보면 before count에 0이 찍히고, dispatch를 하고 난 후에 after count에도 0이 찍힌다.

버튼을 다시 한번 누르면 count는 before, after 모두 1로 찍힌다.

dispatch가 상태를 업데이트 한 후 동기적으로 다음 코드로 넘어가는 것이 아니라 비동기적으로 상태를 업데이트하는 것처럼 보인다.

## 원인

```js
const handleClick = () => {
  console.log("before count", count);
  dispatch(increment());
  console.log("after count", count);
};

useEffect(() => {
  console.log("useEffect count", count);
}, [count]);

return <button onClick={handleClick}>디스패치!</button>;
```

count 상태에 의존하는 useEffect를 추가해보았다.

버튼을 눌러보니 아래 순서로 콘솔이 찍힌다.

```bash
before count 0
useEffect count 1
after count 0
```

dispatch 한 후 count 값이 업데이트 되어서 useEffect가 실행된다.

redux는 동기적으로 상태를 잘 업데이트하고 있었던 것이다;;

그렇다면 왜 after count는 업데이트된 count 값을 바라보지 못하는 걸까?

처음 컴포넌트가 마운트되어 handleClick 함수가 만들어진 시점에 handleClick 안의 count 값은 0이다.

count가 바뀌어서 컴포넌트가 리렌더링 되어도 handleClick 함수는 실행중인 상태기 때문에 useSelector와 함께 클로저가 되는 것 같다..

<img src="/assets/img/blog/2023-01-10-useSelector-not-updated-immediately_01" style="margin-top: 50px;">

### 해결방법?

꼭 한 함수 안에서 dispatch하고 업데이트된 값을 사용해야 한다면 ref를 사용하는 방법이 있다.

```js
const handleClick = () => {
  console.log("stateRef.current", stateRef.current);
  dispatch(increment());
  stateRef.current = count + 1;
  console.log("stateRef.current", stateRef.current);
};
```

이렇게 하면 ref에 업데이트된 값을 저장하여 바로 사용할 수 있다.

다른 방법으로는 useEffect를 사용하여 상태가 업데이트될 때 원하는 동작을 취하는 것이다.

클래스형 컴포넌트에서는 좀 더 쉽게 해결할 수 있다.

dispatch에 async-await을 붙이면 된다.

```js
  handleClick = async () => {
    console.log("before count", this.props.count);
    await this.props.onIncrease();
    console.log("after count", this.props.count);
  };

  render() {
    return <button onClick={this.handleClick}>디스패치!</button>;
  }
```

이렇게 하면 before은 0, after는 1로 상태가 잘 업데이트 되는 것을 확인할 수 있다.

하지만 함수형 컴포넌트에서는 async-await을 붙여도 해결이 되지 않는다.

## 참고사이트

[Redux state doesn't update immediately](https://stackoverflow.com/a/69139701)
