---
layout: post
title: "디바이스 감지 Detect Devices"
sitemap: false
---

{:toc .large-only}

### Ipad

```js
(navigator.platform === "MacIntel" && navigator.maxTouchPoints > 1) ||
  navigator.platform === "iPad";
```

### mobile

```js
const toMatch = [
  /Android/i,
  /webOS/i,
  /iPhone/i,
  /iPad/i,
  /iPod/i,
  /BlackBerry/i,
  /Windows Phone/i,
];

return toMatch.some((toMatchItem) => {
  return navigator.userAgent.match(toMatchItem);
});
```

[How to detect iPad Pro as iPad using javascript?](https://stackoverflow.com/questions/57776001/how-to-detect-ipad-pro-as-ipad-using-javascript)
