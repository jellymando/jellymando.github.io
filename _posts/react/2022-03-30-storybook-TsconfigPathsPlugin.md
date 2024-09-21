---
title: "[Storybook] Typescript 절대경로 적용하기"
categories: [REACT]
tags: [storybook]
---

{:toc .large-only}

## 만약

tsconfig에서 paths를 사용하지 않고 rootDir로 절대경로를 설정한 경우, [.storybook 폴더에 webpack.config.js 파일을 만드는 방법](https://jellymando.github.io/react/2022-02-27-storybook-build-error/)으로 간단히 경로를 설정할 수 있다.

## 하지만

tsconfig에서 paths를 사용하는 경우는 라이브러리를 사용하여 tsconfig의 paths 값을 가져와야 한다.

## tsconfig-paths-webpack-plugin 설치

```bash
yarn add -D tsconfig-paths-webpack-plugin
```

## .storybook/main.js 수정

```js
const TsconfigPathsPlugin = require("tsconfig-paths-webpack-plugin");
module.exports = {
  // ...
  webpackFinal: async (config) => {
    config.resolve.plugins = [
      ...(config.resolve.plugins || []),
      new TsconfigPathsPlugin({
        extensions: config.resolve.extensions
      })
    ];
    return config;
  }
};
```

## 참고사이트

[TypeScript Module Resolution](https://storybook.js.org/docs/react/configure/webpack#typescript-module-resolution)
