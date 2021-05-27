---
layout: post
title: "비동기로 브라우저 새 창 띄우기"
sitemap: false
---

{:toc .large-only}

링크를 통하지 않고 페이지에서 브라우저 새 창을 띄우기

```js
var window = window.open(url, windowName, [windowFeatures]);
```

Window 인터페이스인 open() 메서드는 명시된 리소스를 명시된 이름으로 브라우징 컨텍스트(윈도우, `<iframe>` 또는 탭)에 로드한다.

이름이 없다면 새 윈도우가 열리고 이 윈도우의 브라우징 컨텍스트에 명시된 리소스가 열린다.

[Window.open()](https://developer.mozilla.org/ko/docs/Web/API/Window/open)

<br/>

빈 페이지를 띄우고 싶다면 아래와 같은 방식으로 하면 된다.

```js
window.open("about:blank", "_blank");

// 혹은 그냥..
window.open("");
```

비동기로 받은 데이터를 새 창에 적용해야 할 때는,

```js
$.ajax({
  url: "url",
  ...
  success: function (data) {
    window.open("about:blank", "_blank").document.write(data);
  },
});
```

위 코드는 비동기로 dom을 받아와야 할 때 새 창을 띄우고, data를 새 창의 document에 write 하도록 했다.

새 창을 변수로 선언하고, 나중에 url이나 데이터를 넣어줄 수도 있다.

```js
var newTap = window.open("about:blank", "_blank");

$.ajax({
  url: "url",
  ...
  success: function (data) {
    newTap.location = 'url';
  },
});
```
