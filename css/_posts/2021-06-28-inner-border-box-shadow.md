---
layout: post
title: "inner border 적용하기"
sitemap: false
---

{:toc .large-only}

css로 border 값을 넣으면 테두리가 엘리먼트의 바깥으로 생긴다.

안쪽에 테두리를 만들려면 `box-shadow`를 사용한다.

```css
box-shadow: 0 0 0 3px #000 inset;
```

네번째 값을 `border-width` 라고 생각하면 된다.

<br/>

[[publishing] css inner border 만들기](https://jintrue.tistory.com/entry/publishing-css-inner-border-%EB%A7%8C%EB%93%A4%EA%B8%B0)
