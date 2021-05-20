---
layout: post
title: "스타일 컴포넌트 GlobalStyle 사용하기"
sitemap: false
---

{:toc .large-only}

### 리액트 GlobalStyle 사용하기

GlobalStyle 사용하는 이유 : style component로 컴포넌트들을 스타일링 할 때, `html, body, #root` 등의 엘리먼트를 스타일링 하기 위해서

1. Styled Components 설치

```js
npm install --save styled-components
```

2. `createGlobalStyle`를 import 한다.

```js
import { createGlobalStyle } from "styled-components";
```

3. GlobalStyle 작성

```js
const GlobalStyle = createGlobalStyle`
	body {
		padding: 0;
		margin: 0;
	}
`;
```

4. GlobalStyle 컴포넌트 넣기 **(감싸는 것 아님!!)**

```js
<>
  <GlobalStyle />
  <App />
</>
```

[리액트 Styled Components - 1편](https://velog.io/@taewo/%EB%A6%AC%EC%95%A1%ED%8A%B8-Styled-Components-76jsolbaf8)
