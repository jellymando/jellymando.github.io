---
layout: post
title: "CRA 없이 리액트 환경 만들기"
sitemap: false
---

{:toc .large-only}

### 폴더 생성 및 초기화

프로젝트 폴더를 만들고 yarn을 초기화하여 package.json 파일을 생성해준다.

```js
yarn init -y
```

### public 폴더 생성

정적 파일들을 담을 public 폴더를 생성한다.

public 폴더 안에 index.html 파일을 만들고 html 코드를 넣어준다.

```html
<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>Title</title>
  </head>
  <body>
    <div id="root"></div>
  </body>
</html>
```

### react 설치

```js
yarn add react react-dom
```

### typescript 설치

```js
yarn add --dev typescript

npm install -D ts-node

yarn run tsc --init
```

tsconfig.json 설정

```js
{
  "compilerOptions": {
    "sourceMap": true,  // 소스맵(*.map) 파일 생성 여부
    "jsx": "react", // Resolve: Cannot use JSX unless '--jsx' flag is provided
    "esModuleInterop": true, // import * as => import
    "declaration": true, // .d.ts 파일 생성
    "outDir": "./build", // 결과물을 저장할 디렉토리 설정
    "baseUrl": "src" // 절대경로 설정
  },
  "includes": ["src"] // 절대경로 설정
}
```

[1 : 타입스크립트란? & 기본 설치](https://jellymando.github.io/typescript/2020-12-24-typscript-notion/)

### babel 설치

```js
yarn add @babel/core --dev
```

### webpack 설치

```js
yarn add -D webpack webpack-cli webpack-dev-server
```

### loader 설치

웹팩의 번들링에 필요한 로더 설치

```js
yarn add -D babel-loader css-loader style-loader file-loader ts-loader
```

### 플러그인 설치

웹팩으로 번들링을 한 후에 적용할 플러그인들을 설치

```js
yarn add -D html-webpack-plugin clean-webpack-plugin
```

### src 경로에 index.tsx, App.tsx 생성

#### index.tsx

```js
import React from "react";
import ReactDOM from "react-dom";
import App from "./App";

ReactDOM.render(<App />, document.getElementById("root"));
```

#### App.tsx

```js
import React from "react";

const App = () => {
  return <div></div>;
};

export default App;
```

### 웹팩 설정

루트 경로에 webpack.config.js 파일을 만들고 설정

- **entry** : 모듈의 의존성이 시작되는 부분으로 웹팩은 이 Entry 속성에 명시된 파일을 기준으로 의존성 트리를 만들어 하나의 번들 파일을 만든다.

```js
module.exports = {
  entry: {
    main: "./src/index.tsx",
  },
};
```

- **resolve** : 웹팩이 모듈을 처리하는 방식 정의하는 것으로 확장자를 생략하고도 인식하게 만든다.

```js
resolve: {
  extensions: [".ts", ".tsx", ".js", ".jsx"],
    modules: [resolve(__dirname, "src"), "node_modules"], // 절대경로로 모듈을 불러왔을 때 어떤 디렉토리를 검색해야 하는지 설정
}
```

[Webpack + React + TypeScript: Module not found … in … node_modules/react/](https://stackoverflow.com/questions/47721962/webpack-react-typescript-module-not-found-in-node-modules-react)

- **output** : 웹팩의 번들링 결과물에 대한 옵션. 번들링 결과를 path 경로에 filename으로 묶어낸다. entry 설정은 항상 프로젝트 디렉터리 내부이기 때문에 상대 경로로 하는 반면에, output 설정은 항상 프로젝트 디렉터리 내부라는 보장이 없으므로 절대 경로로 한다. path 모듈을 사용하기 위해서 설정 파일의 module.exports 위에 선언해주자.

```js
const { resolve } = require('path');

output: {
  path: resolve(__dirname, 'build'),
  filename: 'js/build.js',
}
```

> 참고로 \_\_dirname은 NodeJS에서 현재 프로젝트 디렉터리를 의미합니다. npx webpack을 실행하면 프로젝트 최상위 디렉터리에 build.js 파일이 생성되었음을 확인할 수 있습니다.

- **externals** : 특정 import 패키지의 번들링을 방지하고 대신 런타임에 이러한 외부 종속성을 검색

npm 라이브러리를 사용하는 프로젝트에서 라이브러리의 react 컴포넌트를 import하지 못하는 에러 때문에 추가하였다.

```js
  externals: ["react", "react-dom"],
```

- **module.rules** : Loader 추가

```js
module: {
  rules: [
    {
      test: /\.(js|jsx)$/,
      exclude: '/node_modules/',
      loader: 'babel-loader'
    },
    {
      test: /\.css$/,
      use: [
        { loader: 'style-loader' },
        { loader: 'css-loader' }
      ]
    },
    {
      test: /\.(png|jpg|jpeg|gif)$/,
      loader: 'file-loader',
      options: {
        // 파일명 앞에 img/ 처럼 경로를 붙이면 그 경로에 생성된다.
        name: 'img/[name].[ext]'
      }
    },
    { test: /\.tsx?$/, loader: "ts-loader" }
  ]
},
```

- **plugins** : 웹팩을 실행할 때 마다 기존에 있던 번들 파일을 먼저 깔끔히 지우고 싶은 경우에는 clean-webpack-plugin 플러그인을 사용

```js
const HtmlWebpackPlugin = require("html-webpack-plugin");
const { CleanWebpackPlugin } = require("clean-webpack-plugin");

plugins: [
    new CleanWebpackPlugin(),
    new HtmlWebpackPlugin({
      template: "./public/index.html",
      minify: false, // index.html minify 여부
    }),
  ],
```

> `HtmlWebpackPlugin` template을 설정하지 않으면 `webpack serve`를 해도 리액트 코드가 `$root`에 들어가지 않는다!!

- **mode** : production - 빌드 / development - dev <u>(생략..)</u>

### package.json에 스크립트 입력

```js
{
  "scripts": {
    "dev": "webpack serve --progress --mode development",
    "build": "webpack --progress --mode production"
  }
}
```

webpack-cli가 3.x 버전이라면 webpack-dev-server, 4.x 버전이라면 webpack serve 이다!!

webpack-dev-server로 하면 not found module 에러가 계속 나서 찾다가 해결..

[Cannot find module 'webpack/bin/config-yargs'](https://stackoverflow.com/questions/40379139/cannot-find-module-webpack-bin-config-yargs/41182205)

<br/>

[[React] CRA 없이 리액트 환경 만들기](https://baeharam.netlify.app/posts/react/React-CRA-%EC%97%86%EC%9D%B4-%EB%A6%AC%EC%95%A1%ED%8A%B8-%ED%99%98%EA%B2%BD-%EB%A7%8C%EB%93%A4%EA%B8%B0) <br/>
[웹팩(Webpack) 기본 설정법 (Entry/Output/Loader/Plugins)](https://www.daleseo.com/webpack-config/)

### 에러 체크

- `index.html`에 js library 참조하니 build 에러. `index.js`에서 import or require.

- css 파일에서 `@import` 사용하면 build 에러. `index.html`에서 직접 폰트 참조.

- build 폴더에 img, js, html 한꺼번에 들어옴 ➡️ `webpack.config.js`에서 파일명 앞에 경로

```js
options: {
        // 파일명 앞에 img/ 처럼 경로를 붙이면 그 경로에 생성된다.
        name: 'img/[name].[ext]'
      }
      ~~~
```

- build 후 license.txt 파일이 생성된다면

```js
npm install --save-dev terser-webpack-plugin
```

```js
const TerserPlugin = require('terser-webpack-plugin');

    optimization: {
        minimizer: [new TerserPlugin({ extractComments: false })],
    },
```

[How to prevent the creation of a LICENSE.txt file?](https://github.com/webpack-contrib/terser-webpack-plugin/issues/229#issuecomment-761294644)
