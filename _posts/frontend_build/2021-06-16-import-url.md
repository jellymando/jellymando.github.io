---
title: "모듈의 절대 경로 설정하기"
categories: [FE Build]
tags: [fe build, 절대경로]
---

{:toc .large-only}

모듈 등을 import 할 때 경로 차이가 많이 나면 `../../../../../Components/` 이런식으로 매우 복잡해진다.

jsconfig.json 혹은 tsconfig.json 파일을 열어 아래 코드를 추가한다.

```js
{
  "compilerOptions": {
    "baseUrl": "src"
  },
  "includes": ["src"]
}
```

<br/>

build를 해야하는 경우 webpack.config.js 파일도 수정해주어야 한다.

```js
resolve: {
    modules: [resolve(__dirname, "src"), "node_modules"],
  }
```

`resolve.modules`는 모듈을 해석 할 때 어떤 디렉토리를 검색해야 하는지 웹팩에 알려준다.

위 코드처럼 디렉토리가 여러개면 src를 먼저 검색한다.

`"src"`가 아닌 `"/src"`로 하면 에러 나니 조심.

<br/>

[리액트 절대 경로 사용하기](https://www.imkh.dev/react-absolute-path/)<br/>
[resolve.modules](https://webpack.js.org/configuration/resolve/#resolvemodules)
