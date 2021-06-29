---
layout: post
title: "[React 스터디] 1 : 주요 개념 (1)"
sitemap: false
---

{:toc .large-only}

## React란?

React 컴포넌트는 render()라는 메서드를 이용하여 데이터를 입력받아 화면에 표시할 내용을 반환합니다.

```js
ReactDOM.render(<h1>Hello, world!</h1>, document.getElementById("root"));
```

[React 소개 및 작동 원리](https://blex.me/@yoyounn18/react-%EC%86%8C%EA%B0%9C-%EB%B0%8F-%EC%9E%91%EB%8F%99-%EC%9B%90%EB%A6%AC-react%EB%8A%94-%EC%99%9C-%EB%B9%A0%EB%A5%B4%EB%A9%B0-%EA%B0%81%EA%B4%91%EB%B0%9B%EB%8A%94-%EA%B8%B0%EC%88%A0%EC%9D%B8%EA%B0%80)<br/>
[React 공식 문서 - Hello World](https://reactjs.org/docs/hello-world.html)

## JSX는 객체를 나타냅니다.

```js
const element = <h1 className="greeting">Hello, world!</h1>;
```

Babel은 JSX를 컴파일하여 React.createElement()를 호출합니다.

```js
const element = {
  type: "h1",
  props: {
    className: "greeting",
    children: "Hello, world!",
  },
};
```

```js
const element = React.createElement(
  "h1",
  { className: "greeting" },
  "Hello, world!"
);
```

## 필요한 것만 업데이트하는 반응

React DOM은 요소와 하위 요소를 이전 요소와 비교하고 DOM을 원하는 상태로 가져 오는 데 필요한 DOM 업데이트 만 적용합니다.

```js
function tick() {
  const element = (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {new Date().toLocaleTimeString()}.</h2>
    </div>
  );
  ReactDOM.render(element, document.getElementById("root"));
}

setInterval(tick, 1000);
```

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdDXVEZ%2FbtqGFbHXnvQ%2Frpo47jO9UdyJh8MNYg44E1%2Fimg.gif">

## 구성 요소 작성

React를 기존 앱에 통합하면 상향식으로 시작하여 점차적으로 뷰 계층 구조의 맨 위로 올라갈 수 있습니다.

```js
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

function App() {
  return (
    <div>
      <Welcome name="Sara" />
      <Welcome name="Cahal" />
      <Welcome name="Edite" />
    </div>
  );
}

ReactDOM.render(<App />, document.getElementById("root"));
```

<img src="/assets/img/blog/2020-12-25-react-01.png">

## 이벤트 처리

preventDefault () 메서드는 취소 가능한 경우 이벤트를 취소합니다. 즉, 이벤트에 속한 기본 작업이 발생하지 않습니다.
예를 들어 다음과 같은 경우에 유용 할 수 있습니다.

- "제출"버튼을 클릭하면 양식이 제출되지 않습니다.
- 링크를 클릭하면 링크가 URL을 따라 가지 못하도록 합니다.

```js
function ActionLink() {
  function handleClick(e) {
    e.preventDefault();
    console.log("The link was clicked.");
  }

  return (
    <a href="#" onClick={handleClick}>
      Click me
    </a>
  );
}
```

JavaScript에서 클래스 메서드는 기본적으로 [바인딩](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_objects/Function/bind) 되지 않습니다. ()와 같이 뒤에 없는 메서드를 참조하는 경우 onClick={this.handleClick} 해당 메서드를 바인딩 해야 합니다.

```js
class Toggle extends React.Component {
  constructor(props) {
    super(props);
    this.state = { isToggleOn: true };

    // This binding is necessary to make `this` work in the callback
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    this.setState((state) => ({
      isToggleOn: !state.isToggleOn,
    }));
  }

  render() {
    return (
      <button onClick={this.handleClick}>
        {this.state.isToggleOn ? "ON" : "OFF"}
      </button>
    );
  }
}

ReactDOM.render(<Toggle />, document.getElementById("root"));
```

## 조건부 렌더링

사용자가 로그인했는지 여부에 따라 이러한 구성 요소 중 하나를 표시 하는 구성 요소를 만듭니다.
현재 상태에 따라 `<LoginButton />` 또는 `<LogoutButton />`이 렌더링 됩니다. 또한 Greeting 컴포넌트에서 `<UserGreeting />` 또는 `<GuestGreeting />` 을 렌더링합니다.

```js
function Greeting(props) {
  const isLoggedIn = props.isLoggedIn;
  if (isLoggedIn) {
    return <UserGreeting />;
  }
  return <GuestGreeting />;
}

ReactDOM.render(
  // Try changing to isLoggedIn={true}:
  <Greeting isLoggedIn={false} />,
  document.getElementById("root")
);
class LoginControl extends React.Component {
  constructor(props) {
    super(props);
    this.handleLoginClick = this.handleLoginClick.bind(this);
    this.handleLogoutClick = this.handleLogoutClick.bind(this);
    this.state = { isLoggedIn: false };
  }

  handleLoginClick() {
    this.setState({ isLoggedIn: true });
  }

  handleLogoutClick() {
    this.setState({ isLoggedIn: false });
  }

  render() {
    const isLoggedIn = this.state.isLoggedIn;
    let button;
    if (isLoggedIn) {
      button = <LogoutButton onClick={this.handleLogoutClick} />;
    } else {
      button = <LoginButton onClick={this.handleLoginClick} />;
    }

    return (
      <div>
        <Greeting isLoggedIn={isLoggedIn} />
        {button}
      </div>
    );
  }
}

ReactDOM.render(<LoginControl />, document.getElementById("root"));
```

[Element Variable Example](https://codepen.io/gaearon/pen/QKzAgB?editors=0010)

## Map 과 Key

key는 요소 목록을 만들 때 포함해야하는 특수 문자열 속성입니다.
key는 주변 배열의 컨텍스트에서만 의미가 있습니다. `<li>`요소가 아닌 배열 ListItem의 `<ListItem />`요소에 키를 유지해야 합니다.

```js
function ListItem(props) {
  // Correct! There is no need to specify the key here:
  return <li>{props.value}</li>;
}

function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) => (
    // Correct! Key should be specified inside the array.
    <ListItem key={number.toString()} value={number} />
  ));
  return <ul>{listItems}</ul>;
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById("root")
);
```
