---
layout: post
title: 'height를 width와 똑같은 비율로 만들기'
sitemap: false
---

{:toc .large-only}

부모의 padding-bottom 값을 원하는 비율로 설정하고

자식에게 absolute를 주면 된다.

```js
.wrapper {
  position: relative;
  width: 100%;
  padding-bottom: 100%;
}

.player {
  position: absolute;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
}
```
