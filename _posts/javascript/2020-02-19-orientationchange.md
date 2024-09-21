---
title: "[orientationchange] 디바이스 방향 바뀌는 것 감지 🔁"
categories: [Javascript]
tags: [javascript, orientationchange]
---

{:toc .large-only}

## orientationchange

```js
screen.addEventListener("orientationchange", function () {
  alert("the orientation of the device is now " + window.orientation);
});
```

`screen.orientation` 이 아닌 `window.orientation` 사용

**세로모드** : `window.orientation = 0`
**가로모드** : `window.orientation = 90 || -90`

<br/>
[orientationchange](https://developer.mozilla.org/ko/docs/Web/API/Window/orientationchange_event)
