---
title: "ctx.drawImage : 비디오를 캔버스로 가져오기"
categories: [webRTC]
tags: [webrtc, cavnas]
---

{:toc .large-only}

### 비디오를 캔버스로 가져오기

```js
const canvas = canvasRef.current;
const ctx = canvas.getContext("2d");
ctx.drawImage(videoRef.current, 0, 0, canvas.width, canvas.height);
```

ctx.drawImage 메서드를 사용하면 비디오를 이미지처럼 캔버스 위에 올릴 수 있다.

ctx.drawImage는 첫 번째 인자로 이미지 소스를 가져오고 각각 x, y 좌표, 이미지 너비, 높이를 설정한다.

[CanvasRenderingContext2D.drawImage()](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/drawImage)<br/>

[w3s drawImage 직접해보기](https://www.w3schools.com/tags/playcanvas.asp?filename=playcanvas_drawimagewidth&preval=img,10,10,220,277)

<br/>

이미지 사이즈와 캔버스 사이즈가 다른 경우 ratio를 맞춰줘야 한다.

```js
var hRatio = canvas.width / img.width;
var vRatio = canvas.height / img.height;
var ratio = Math.min(hRatio, vRatio);
ctx.drawImage(
  img,
  0,
  0,
  img.width,
  img.height,
  0,
  0,
  img.width * ratio,
  img.height * ratio
);
```

[Scaling an image to fit on canvas](https://stackoverflow.com/questions/23104582/scaling-an-image-to-fit-on-canvas)
