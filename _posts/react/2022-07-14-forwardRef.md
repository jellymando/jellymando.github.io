---
title: "forwardRef 사용하기"
categories: [React]
tags: [react, forwardRef]
---

{:toc .large-only}

## 오류 나는 경우

리액트에서 ref를 props로 전달하기 위해서는 `forwardRef`를 사용해야 한다.

`forwardRef`를 사용하지 않고 자식에게 ref를 전달하면 아래와 같은 에러가 발생한다.

```js
// App.jsx
const ref = React.createRef();
<FancyButton ref={ref}>Click me!</FancyButton>;

// FancyButton.jsx
const FancyButton = ({ ref }) => {
  <button ref={ref} className="FancyButton">
    {props.children}
  </button>;
};
```

<img src="/assets/img/blog/2022-08-01-forwardRef_01.png" style="margin-top:20px;">

## 올바른 예

JSX를 `forwardRef`로 감싸주고, 두 번째 파라미터로 ref를 전달한다.

```js
// App.jsx
const ref = React.createRef();
<FancyButton ref={ref}>Click me!</FancyButton>;

// FancyButton.jsx
// forwardRef 두 번째 인자로 ref를 받는다.
const FancyButton = React.forwardRef((props, ref) => (
  <button ref={ref} className="FancyButton">
    {props.children}
  </button>
));
```

## 참고사이트

[Forwarding Refs](https://ko.reactjs.org/docs/forwarding-refs.html)
