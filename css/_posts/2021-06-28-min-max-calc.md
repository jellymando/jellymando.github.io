---
layout: post
title: "min/max() + calc() = Incompatible units: 'px' and 'vw'"
sitemap: false
---

{:toc .large-only}

css `min()` / `max()` 안에서 vw / vh 단위 혹은 산술연산자를 사용한 경우 `Incompatible units: 'px' and 'vw'` 에러 발생

`min()` / `max()`를 `calc()`로 감싸주면 해결된다.

<br/>

[SASS: Incompatible units: 'vw' and 'px'](https://stackoverflow.com/questions/54090345/sass-incompatible-units-vw-and-px)
