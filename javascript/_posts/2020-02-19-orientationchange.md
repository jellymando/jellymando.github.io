---
layout: post
title: "디바이스 방향 바뀌는 것 감지 🔁"
sitemap: false
---

{:toc .large-only}

## orientationchange

```js
screen.addEventListener("orientationchange", function () {
  alert("the orientation of the device is now " + window.orientation);
});
```

`screen.orientation` 이 아닌 `window.orientation` 사용

<br/>
[orientationchange](https://developer.mozilla.org/ko/docs/Web/API/Window/orientationchange_event)
