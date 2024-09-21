---
title: "이미지가 빌드되지 않는 이슈"
categories: [WEBPACK]
tags: [webpack, file-loader]
---

{:toc .large-only}

Painter 라이브러리 만들며 javascript로 마우스 포인터에 이미지를 넣는 작업을 했다.

but 웹팩 빌드를 돌려도 이미지 파일이 로드되지 않았다.

file-loader를 사용해도 마찬가지.

이유는 javascript에서 `style.curser = url(경로, auto)` 이 부분에 경로를 바로 집어넣어서, 이미지를 로드하지 않은 것 같다.

이미지를 import 한 뒤 경로를 수정하자 정상적으로 빌드되었다.

```js
import paintBrush from "../images/paint-brush.png";

if (this.paintBrush) this.canvas.style.cursor = `url(${paintBrush}), auto`;
```
