---
title: 'styled-components에서 keyframes 작성하기'
categories: [REACT]
tags: [react, styled components]
---

{:toc .large-only}

`styled.div` 대신에 `keyframes`을 사용한다.

```js
import styled, { keyframes } from 'styled-components'

const fadeIn = keyframes`
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
`

const FadeInButton = styled.button`
  animation: 1s ${fadeIn} ease-out;
`
```

<br/>

스타일 규칙을 부분적으로 작성하는 경우 `css`를 붙여 사용해야 한다.

```js
import styled, { css, keyframes } from 'styled-components'

const pulse = keyframes`
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
`

const animation = (props) =>
  css`
    ${pulse} ${props.animationLength} infinite alternate;
  `

const PulseButton = styled.button`
  animation: ${animation};
`
```

<br/>

[keyframes](https://styled-components.com/docs/api#keyframes)
