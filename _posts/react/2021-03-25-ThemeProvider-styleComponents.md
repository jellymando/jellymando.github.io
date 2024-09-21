---
title: "ThemeProvider로 공통 스타일 속성 관리하기"
categories: [REACT]
tags: [react, ThemeProvider]
---

{:toc .large-only}

1. ThemeProvider를 import 한다.

```js
import { ThemeProvider } from "styled-components";
```

2. theme 객체를 만들어 적용하고 싶은 속성을 넣어준다.

```js
const theme = {
  black: "#000000",
  white: "#ffffff",
};
```

3. Theme을 적용할 범위를 `<ThemeProvider>`로 감싸고 theme 값을 넣어준다.

```js
<ThemeProvider theme={theme}>
    <App>
</ThemeProvider>
```

4. ThemeProvider로 감싸진 컴포넌트의 style-components에서 theme 속성을 사용할 수 있다.

```js
${({ theme }) => theme.black};
```
