---
layout: post
title: 'viewport-fit이란?'
sitemap: false
---

{:toc .large-only}

## viewport-fit

viewport-fit은 스크린에서 viewport를 어떻게 보여줄 지에 대한 속성이다.

```html
<meta
  name="viewport"
  content="width=device-width, initial-scale=1, viewport-fit=cover"
/>
```

메타 태그를 통해 viewport-fit을 지정할 수 있다.

`viewport-fit=cover` 속성을 넣어줘야 하는 이유는 IOS 노치 때문인데,

노치가 있는 IOS 단말에서는 가로모드일 때 아래와 같이 safe area가 생기기 때문에 이를 방지하기 위해서다.

<img src="/assets/img/blog/2022-06-03-viewport-fit.png" style="margin-top:25px">

## 참고사이트

[viewport-fit이란?](https://hannut91.github.io/blogs/viewport-fit)
