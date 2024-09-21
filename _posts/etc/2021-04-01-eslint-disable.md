---
title: "eslint 에러 비활성화하기 (array-callback-return)"
categories: [..etc]
tags: [eslint]
---

{:toc .large-only}

Line 49:44: Expected to return a value in arrow function array-callback-return

위 에러는 콜백에서 return을 하지 않아 나타나는 에러로 해당 옵션을 비활성화 함으로 해결했다.

```js
/* eslint-disable array-callback-return */
```

<br/>

[배열 메서드의 콜백에서 return 문을 적용합니다 (array-callback-return)](https://eslint.org/docs/rules/array-callback-return)
