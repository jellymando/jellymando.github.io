---
title: "[Storybook] 빌드 시 You may need to refresh the browser 에러"
categories: [React]
tags: [storybook]
---

{:toc .large-only}

## 원인

storybook 실행 시 빌드 단계에서 컴포넌트의 절대경로를 찾지 못해 발생하는 에러

## 해결

`.storybook` 폴더에 `webpack.config.js` 파일을 만들고 아래 코드를 입력하여 절대경로를 잘 찾아가도록 설정한다.

```js
const path = require("path");

module.exports = ({ config }) => {
  config.resolve.modules.push(path.resolve(__dirname, "../src"));
  return config;
};
```

## 참고사이트

[I can not import with absolute path in Storybook](https://github.com/storybookjs/storybook/issues/3916#issuecomment-490287662)
