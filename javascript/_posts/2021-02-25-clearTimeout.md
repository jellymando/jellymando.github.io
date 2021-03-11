---
layout: post
title: 'clearTimeout을 빠뜨리면 외않돼지?'
sitemap: false
---

{:toc .large-only}

스크롤하면 알림창이 뜨는 함수를 만든다.

그런데 스크롤 할 때마다 무수히 많은 setTimeout이 생성되어 무수히 많은 알림창이 뜬다.

때문에 앞에 setTimeout이 실행 중일때는 다른 setTimeout이 생기지 않도록 clearTimeout을 해주어야 한다.

```js
var handleAlert = function () {
  if (throttleTimeout) {
    clearTimeout(throttleTimeout);
  }

  throttleTimeout = setTimeout(function () {
    alert('1초뒤');
  }, 1000);
};

window.addEventListener('scroll', handleAlert);
```
