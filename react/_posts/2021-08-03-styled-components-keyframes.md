---
layout: post
title: "styled-components에서 keyframes 작성하기"
sitemap: false
---

{:toc .large-only}

`styled.div` 대신에 `keyframes`을 사용한다.

```js
const pulse = keyframes`
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
`;

const animation = (props) =>
  css`
    ${pulse} ${props.animationLength} infinite alternate;
  `;

const PulseButton = styled.button`
  animation: ${animation};
`;
```

<br/>

또한 `props`로 전달받았을 때는 `css` 를 붙여줘야 한다고 한다.

<br/>

[keyframes](https://styled-components.com/docs/api#keyframes)
