---
title: "TypeScript declarations 파일 절대경로를 상대경로로 변환하기"
categories: [FE Build]
tags: [webpack, 절대경로]
---

{:toc .large-only}

## 문제

앱을 빌드하여 .d.ts 파일을 생성할 때, rootDir로 설정한 절대경로가 변환되지 않고 그대로 생성되어 dist 폴더에서 경로를 찾지 못한다.

```js
import { ColorTheme } from "types";
// types가 아니라 ../../types로 바꿔야 경로를 찾아갈 수 있다.
```

## 해결

### typescript-transform-paths, ttypescript 모듈 설치

```bash
yarn add -D typescript-transform-paths ttypescript
```

### tsconfig.json 수정

```js
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
        "@/*": ["src/*"]
    },
    "plugins": [
      // .js 파일 수정
      { "transform": "typescript-transform-paths" },
      // .d.ts 파일 수정
        { "transform": "typescript-transform-paths", "afterDeclarations": true }
    ]
}
```

### webpack.config.js 수정

tsconfig.json에서만 paths를 수정한 경우 webpack에서 찾지 못하므로 alias를 추가해준다.

```js
resolve: {
    extensions: [".ts", ".tsx", ".js", ".jsx"],
    modules: [resolve(__dirname, "src"), "node_modules"],
    alias: {
      "@": resolve(__dirname, "src")
    }
}
```

### package CLI 수정

```bash
webpack && ttsc -p tsconfig.json
```

ttsc 명령어를 먼저 실행하면 webpack에서 덮어쓰기 때문에 webpack을 먼저 실행했다.

```js
import { ColorTheme } from "../../types";
// 빌드 후 정상적으로 경로가 변환된다.
```

## 참고사이트

[TypeScript declarations 파일에 Webpack Alias 적용하기](https://im-developer.tistory.com/194)<br/>
[typescript-transform-paths](https://www.npmjs.com/package/typescript-transform-paths)<br/>
[Webpack alias in TypeScript declarations](https://medium.com/@joshuaavalon/webpack-alias-in-typescript-declarations-81d2b6c0dcd6)
