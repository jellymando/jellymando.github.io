---
title: "클래스형 컴포넌트와 함수형 컴포넌트의 차이"
categories: [REACT]
tags: [react]
---

{:toc .large-only}

## 클래스형 컴포넌트

- state, 라이프 사이클 기능이 있다.

- render 함수를 반드시 사용해야 한다.

## 함수형 컴포넌트

- state, 라이프 사이클 기능이 없다.

- 리액트 16.8부터 hook을 이용해 위 기능을 구현할 수 있다.

- 클래스형 컴포넌트보다 메모리를 적게 사용한다.

## Props

### 클래스형 컴포넌트

`this.props` 객체를 통해 전달받는다.

```js
class MyComponent extends Component {
  render() {
    const { name, number } = this.props;
    return (
      <div>
        <p>name : {name}</p>
        <p>number : {number}</p>
      </div>
    );
  }
}
```

### 함수형 컴포넌트

함수의 인자를 통해 전달받는다.

```js
const MyComponent = ({ name, number }) => {
  return (
    <div>
      <p>name : {name}</p>
      <p>number : {number}</p>
    </div>
  );
};
```

## State

### 클래스형 컴포넌트

constructor(생성자) 내부의 `this.state` 객체를 통해 state를 관리한다.

```js
class MyComponent extends Component {
  constructor(props) {
    super(props);
    this.state = {
      name: "",
      number: 0,
    };
  }
  render() {
    return (
      <div>
        <p>name : {this.state.name}</p>
        <p>number : {this.state.number}</p>
      </div>
    );
  }
}
```

<br/>

> 주의 : state에 props를 복사하면 안 된다.

```js
constructor(props) {
 super(props);
 // 이렇게 하지 마세요!
 this.state = { color: props.color };
}
```

this.props.color를 직접 사용하면 되며, props의 값이 변하더라도 state에 반영되지 않는다.

props의 갱신을 의도적으로 무시해야 할 때만 이와 같은 패턴을 사용한다.

### 함수형 컴포넌트

함수형 컴포넌트에서는 `useState` 훅을 사용하여 state를 관리한다.

```js
const MyComponent = () => {
  const [name, setName] = useState("");
  const [number, setNumber] = useState(0);
  return (
    <div>
      <p>name : {name}</p>
      <p>number : {number}</p>
    </div>
  );
};
```

## Constructor

- 클래스 컴포넌트는 항상 props로 기본 constructor(생성자)를 호출해야 한다.

- constructor 안에서 가장 먼저 `super(props)`를 호출해야 한다.

- React에서 생성자는 보통 아래의 두 가지 목적을 위하여 사용된다.
  - `this.state`에 객체를 할당하여 지역 state를 초기화
  - 인스턴스에 이벤트 처리 메서드를 바인딩

## 참고사이트

[클래스형 컴포넌트, state, props](https://uriu.tistory.com/306)<br/>
[[React] 클래스형 컴포넌트](https://points.tistory.com/88)<br/>
[함수에서 클래스로 변환하기](https://ko.reactjs.org/docs/state-and-lifecycle.html#converting-a-function-to-a-class)<br/>
[React.Component](https://ko.reactjs.org/docs/react-component.html)
