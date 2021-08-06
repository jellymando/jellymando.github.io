---
layout: post
title: "position: absolute 자식을 부모 요소의 정가운데에 배치하기"
sitemap: false
---

{:toc .large-only}

툴팁 등을 만들 때 부모 요소의 가운데에 배치시키려면 아래처럼 작성한다.

```css
position: absolute;
left: 50%;
transform: translateX(-50%);
```

<br/>

`left: 50%`은 **부모 크기의** 50%만큼 이동하고, `transform: translateX(-50%)`은 **요소 크기의** 50% 만큼 이동한다.

둘을 함께 사용해야 부모와 자식 요소 크기의 평균대로 가운대 배치할 수 있다.

<br/>

<img src="/assets/img/blog/2021-08-06-position-left-translateX.jpeg">

<br/>

[레이어 위치를 가운데 정렬 할때 유용한 CSS transform](https://sonsoo.tistory.com/6)
