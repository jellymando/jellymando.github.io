---
title: "MiniCssExtractPlugin - css 파일 따로 분리하기"
categories: [WEBPACK]
tags: [webpack]
---

{:toc .large-only}

## MiniCssExtractPlugin

번들링 할 때 css를 js 파일에 포함시키지 않고 따로 파일을 분리할 때 사용하는 플러그인이다.

dist 폴더에 js 파일과 css 파일이 각각 따로 생성된다.

linkType, filename 등의 옵션을 설정할 수 있다.

## Install

```js
npm install --save-dev mini-css-extract-plugin
```

## webpack.config.js

```js
const MiniCssExtractPlugin = require("mini-css-extract-plugin");

module.exports = {
  plugins: [new MiniCssExtractPlugin()],
  module: {
    rules: [
      {
        test: /\.css$/i,
        use: [MiniCssExtractPlugin.loader, "css-loader"],
      },
    ],
  },
};
```

## 참고사이트

[MiniCssExtractPlugin](https://webpack.js.org/plugins/mini-css-extract-plugin/)
