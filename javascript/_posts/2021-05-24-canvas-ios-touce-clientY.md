---
layout: post
title: "IOS에서 Canvas에 그릴 때 y좌표 안맞는 문제"
sitemap: false
---

{:toc .large-only}

#### IOS에서 캔버스에 그릴 때, 터치한 y좌표와 실제로 그려지는 y좌표에 차이가 나는 이슈

터치이벤트로 발생하는 y좌표는 `e.touches[0].clientY` 이다.

여기서 캔버스의 ClientRect를 빼주어야 한다.

```js
const rect = this.canvas!.getBoundingClientRect();

const drawY = e.clientY - rect.top;
```

[Using Touch Events with the HTML5 Canvas](https://bencentra.com/code/2014/12/05/html5-canvas-touch-events.html)
