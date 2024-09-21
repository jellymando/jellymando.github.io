---
title: "[js+css] 상하좌우 요소 만들기"
categories: [JAVASCRIPT]
tags: [javascript]
---

{:toc .large-only}

css에 `:before`, `:after` 같은 가상선택자는 왜 2개밖에 없을까?

`div` 안에 상하좌우 `absolute`인 요소를 만들어야 하는데, 여러(?) 방법 중 고민하다 그냥 `map` 돌려서 요소 4개를 만들기로..

```js
{
  ["top", "bottom"].map((vertical) => {
    return ["left", "right"].map((horizon) => {
      return <span className={`area-frame ${vertical} ${horizon}`} />;
    });
  });
}
```

<br/>

### 결과물 ⬇️

```html
<span class="area top left"></span>
<span class="area top right"></span>
<span class="area bottom left"></span>
<span class="area bottom right"></span>
```

<br/>

### scss ⬇️

```scss
.area {
  position: absolute;
  width: 10vw;
  height: 10vw;

  &.top {
    top: 0;
    border-top: 4px solid #fff;
  }

  &.bottom {
    bottom: 0;
    border-bottom: 4px solid #fff;
  }

  &.left {
    left: 0;
    border-left: 4px solid #fff;
  }

  &.right {
    right: 0;
    border-right: 4px solid #fff;
  }
}
```
