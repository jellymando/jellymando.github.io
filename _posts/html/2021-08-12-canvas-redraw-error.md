---
title: "Canvas redraw 안되는 이슈"
categories: [HTML]
tags: [canvas]
---

{:toc .large-only}

### 이슈

- storage에 저장된 figure로 `redraw()` 메서드 실행하는데 그려지지 않음

- setTimeout 걸고 redraw 하면 잘 됨

- videoSize가 바뀌면서 canvas의 width, height가 바뀌어서 그리기 내역 초기화 된 듯함

### 해결방법

- canvas 엘리먼트의 width, height는 고정된 값으로 전달하고, 변하는 크기는 style로 전달한다.

```js
const { canvasSize } = "대충 고정된 값";
const [{ width, height }, setCanvasSize] = useState({ width: 0, height: 0 });
<canvas
  width={canvasSize.width}
  height={canvasSize.height}
  style={{ width, height }}
/>;
```
