---
layout: post
title: "Storybook을 사용한 design-system 만들기"
sitemap: false
---

{:toc .large-only}

## Storybook 설치

```bash
npm i @storybook/react @storybook/cli sb init
```

`sb init` 명령어를 실행하면 `package.json`에 아래와 같은 CLI가 생기며, `.storybook` 폴더가 생성된다.

```js
  "scripts": {
    // ...
    "storybook": "start-storybook -p 6006 -s public",
    "build-storybook": "build-storybook -s public"
  }
```

## Webpack 설정

Storybook에서 컴포넌트를 import할 때 절대경로를 사용한다면 웹팩을 설정해주어야 한다.

.storybook 폴더에 webpack.config.js 파일을 생성하고 아래 코드를 저장한다.

```js
const path = require("path");

module.exports = ({ config }) => {
  config.resolve.modules.push(path.resolve(__dirname, "../src"));
  return config;
};
```
