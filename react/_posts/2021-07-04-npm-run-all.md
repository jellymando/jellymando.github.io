---
layout: post
title: "npm scripts 여러개 실행하기"
sitemap: false
---

{:toc .large-only}

`package.json`에 있는 여러 npm scripts를 한번에 실행하기 위해 `npm-run-all` 모듈을 설치했다.

```js
yarn add npm-run-all --dev
```

```js
 "scripts": {
    "start": "npm-run-all -p start:server start:app",
    "start:app": "react-scripts start",
    "start:server": "node ./src/server/index.js",
 }
```

<br/>

`yarn start` 하면 `start:app` 과 `start:server` 가 같이 실행된다.
<br/>

[React or javacript npm-run-all 으로 npm 스크립트 여러개 실행하는 방법](https://xxxxersuy.com/2)
