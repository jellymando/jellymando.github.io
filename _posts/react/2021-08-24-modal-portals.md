---
title: "Portal을 사용하여 Modal 띄우기"
categories: [React]
tags: [react, modal]
---

{:toc .large-only}

`ReactDOM`에서 제공하는 `createPortal`을 사용하여 `#root` 외부에서 모달을 띄울 수 있다.

### DOM에 modal 요소 생성

`#root` 형제 요소로 `#modal`을 추가한다.

```html
<body>
  <div id="root"></div>
  <div id="modal"></div>
</body>
```

### ModalPortal 컴포넌트 생성

```js
import ReactDOM from "react-dom";

const ModalPortal = ({ children }: { children: JSX.Element }) => {
    const modalRoot = document.getElementById("modal")!;
    return ReactDOM.createPortal(children, modalRoot);
};

export default ModalPortal;
```

### Modal 컴포넌트 생성

실제로 띄울 모달 컴포넌트를 생성한다.

```js
import React, { useRef, useEffect } from "react";
import {
  Container,
  ModalWrap,
  Content,
  Title,
  ButtonWrap,
  Button,
} from "./styled";

const Modal = ({ title, contents, handleClickCloseButton }) => {
  const modalRef = useRef(null);

  return (
    <Container ref={modalRef}>
      <ModalWrap>
        <Content>
          {title && <Title>{title}</Title>}
          {contents && contents}
        </Content>
        <ButtonWrap>
          <Button onClick={handleClickCloseButton}>닫기</Button>
        </ButtonWrap>
      </ModalWrap>
    </Container>
  );
};

export default Modal;
```

### 모달 사용하기

모달을 사용할 컴포넌트에서 `ModalPortal`안에 `Modal`을 넣어 사용한다.

```js
{
  isOpenModal && (
    <ModalPortal>
      <Modal
        title="제목"
        contents="내용"
        handleClickCloseButton={() => setIsOpenModal(false)}
      />
    </ModalPortal>
  );
}
```

<br/>

[https://velog.io/@velopert/react-portals](리액트 - Portals 를 통한 부모 컴포넌트의 외부 DOM 에 컴포넌트 렌더링하기)<br/>
[Portals](https://ko.reactjs.org/docs/portals.html)
