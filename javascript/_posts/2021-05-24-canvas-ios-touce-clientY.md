---
layout: post
title: "IOS에서 Canvas에 그릴 때 좌표 안맞는 문제"
sitemap: false
---

{:toc .large-only}

#### IOS에서 캔버스에 그릴 때, 터치한 좌표와 실제로 그려지는 좌표에 차이가 나는 이슈

터치이벤트로 발생하는 x, y좌표는 `e.touches[0].clientX`, `e.touches[0].clientY` 이다.

`Element.getBoundingClientRect()`는 윈도우(window)룰 기준으로 엘리먼트의 위치를 구하는 메서드이다.

mouse/touch event대로 그리면 이 위치 좌표가 더해져서 그려지기 때문에 위치값을 빼주어야 한다.

<img src="https://developer.mozilla.org/en-US/docs/Web/API/Element/getBoundingClientRect/element-box-diagram.png">

```js
const rect = this.canvas!.getBoundingClientRect();

const x = e.touches[0].clientX - rect.left;
const y = e.touches[0].clientY - rect.top;
```

[Using Touch Events with the HTML5 Canvas](https://bencentra.com/code/2014/12/05/html5-canvas-touch-events.html)
