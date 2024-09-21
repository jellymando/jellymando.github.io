---
title: 'CSS cubic-bezier() Function'
categories: [CSS]
tags: [css]
---

{:toc .large-only}

## cubic-bezier(x1, y1, x2, y2)

x1, y1, x2, y2 4개의 점으로 3차원 베지어 곡선을 그리는 css 함수.

```css
div {
  width: 100px;
  height: 100px;
  background: red;
  transition: width 2s;
  transition-timing-function: cubic-bezier(0.1, 0.7, 1, 0.1);
}
```

<img src="/assets/img/blog/2022-06-21-cubic-bezier-curve.png">

위 그림에서 두 검은 점의 위치([x1, y1] 과 [x2, y2])를 옮겨서 애니메이션 곡선을 만들 수 있다.

곡선 만들기는 [이 사이트](https://matthewlein.com/tools/ceaser)에서 테스트 해볼 수 있다.

## 참고사이트

[CSS transition cubic-bezier를 파헤치기.](https://velog.io/@vvsogi/CSS-transition-cubic-bezier%EB%A5%BC-%ED%8C%8C%ED%97%A4%EC%B9%98%EA%B8%B0)<br/>
[CSS cubic-bezier() Function](https://www.w3schools.com/cssref/func_cubic-bezier.asp)
