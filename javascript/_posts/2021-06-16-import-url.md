---
layout: post
title: "절대 경로로 import 하기"
sitemap: false
---

{:toc .large-only}

모듈 등을 import 할 때 경로 차이가 많이 나면 `../../../../../Components/` 이런식으로 매우 복잡해진다.

jsconfig.js 혹은 tsconfig.js 파일을 열어 아래 코드를 추가한다.

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

`"src"`가 아닌 `"/src"`로 하면 에러 나니 조심.
