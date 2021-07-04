---
layout: post
title: "Proxy Middleware 사용하기"
sitemap: false
---

{:toc .large-only}

앱과 db서버의 주소나 port 등이 다른 경우 미들웨어를 통해 db서버에 접근할 수 있다.

`http-proxy-middleware`를 설치한다.

```js
npm install http-proxy-middleware --save
```

<br/>

src 폴더에 `setupProxy.js` 파일을 생성한다.

```js
// setupProxy.js
const { createProxyMiddleware } = require("http-proxy-middleware");

module.exports = function (app) {
  app.use(
    createProxyMiddleware("/api", {
      target: "http://localhost:3001/",
      changeOrigin: true,
    })
  );
};
```

<br/>

웹브라우저에 `http://localhost:3000/api` 를 입력하면 `http://localhost:3001/api` 를 호출한 결과를 보여준다.

<br/>

[React + express 연동설정. 처음부터 따라하기 2](https://hello-bryan.tistory.com/122)
