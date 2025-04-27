---
title: "[Error] Minified React error #321"
categories: [FE Build]
tags: [webpack, error]
---

{:toc .large-only}

npm 라이브러리를 사용하는 프로젝트에서 라이브러리의 리액트 컴포넌트를 import 하면 `Minified React error #321` 에러 발생

라이브러리의 `webpack.config.js` 파일에 `externals` 속성 추가

```js
  externals: ["react", "react-dom"],
```
