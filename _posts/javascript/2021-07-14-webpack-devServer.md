---
title: "Webpack Server IP 설정하기"
categories: [Javascript]
tags: [webpack]
---

{:toc .large-only}

`devServer.host` 설정하면 http 서버로 실행된다.

```js
module.exports = {
  //...
  devServer: {
    host: "0.0.0.0",
  },
};
```

<br/>

[DevServer](https://webpack.js.org/configuration/dev-server/)
