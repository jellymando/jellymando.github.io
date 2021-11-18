---
layout: post
title: "서버 실행 시 자동으로 브라우저 창 띄우기"
sitemap: false
---

{:toc .large-only}

## webpack.config.js

```js
module.exports = {
  //...
  devServer: {
    open: true,
  },
};
```

## 참고사이트

[devServer.open](https://webpack.js.org/configuration/dev-server/#devserveropen)
