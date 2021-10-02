---
layout: post
title: "[React Testing Library] Target container is not a DOM element 에러"
sitemap: false
---

{:toc .large-only}

ModalPortal을 사용하는 컴포넌트에서 테스팅 진행 시 아래와 같은 에러가 발생했다.

```js
// Target container is not a DOM element.

      3 | const ModalPortal = ({ children }: { children: JSX.Element }) => {
      4 |   const modalRoot = document.getElementById("modal")!;
    > 5 |   return ReactDOM.createPortal(children, modalRoot);
        |                   ^
      6 | };
      7 |
      8 | export default ModalPortal;
```

테스트 환경에서 DOM 엘리먼트에 id를 제공하지 않기 때문에 modalRoot를 못 찾아서라고 한다.

<<<<<<< HEAD
index.html 에서 modal 엘리먼트를 제거하고 아래와 같이 수동으로 엘리먼트를 추가해준다.

이렇게 하면 test의 가상 DOM에도 modal 엘리먼트가 생성된다.

```js
const modalRoot = document.createElement("div");
modalRoot.setAttribute("id", "modal");
document.body.appendChild(modalRoot);

const ModalPortal = ({ children }: { children: JSX.Element }) => {
  return ReactDOM.createPortal(children, modalRoot);
=======
아래와 같이 div를 추가해주면 된다.

```js
const ModalPortal = ({ children }: { children: JSX.Element }) => {
  const modalRoot = document.getElementById("modal")!;
  return ReactDOM.createPortal(
    children,
    modalRoot || document.createElement("div")
  );
>>>>>>> e4c9dbf157a00e9130c98d064f9f8c4a5bb341e0
};
```

<br/>

<<<<<<< HEAD
[Modals](https://testing-library.com/docs/example-react-modal/)
=======
[Testing React: Target Container is not a DOM element](https://stackoverflow.com/a/52125891)
>>>>>>> e4c9dbf157a00e9130c98d064f9f8c4a5bb341e0
