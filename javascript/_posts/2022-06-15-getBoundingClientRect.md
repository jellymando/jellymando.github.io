---
layout: post
title: '엘리먼트의 크기 구하기 : clientWidth/clientHeight vs getBoundingClientRect()'
sitemap: false
---

{:toc .large-only}

## clientWidth/clientHeight

엘리먼트의 내부 너비/높이 픽셀값

padding은 포함하지만 border, margin, 스크롤바는 포함하지 않는다.

<img src="/assets/img/blog/2022-06-16-getBoundingClientRect_01.png">

## getBoundingClientRect()

엘리먼트의 크기와 뷰포트에 상대적인 위치 정보를 제공하는 DOMRect 객체를 반환한다.

<img src="/assets/img/blog/2022-06-16-getBoundingClientRect_02.png">

## 차이점

clientWidth/clientHeight는 엘리먼트의 실제 크기만을 나타낸다.

만약 엘리먼트에 `transform: scale(0.5);` 같은 스타일을 적용시켜도 clientWidth/clientHeight 값은 변하지 않는다.

`getBoundingClientRect().width`/`getBoundingClientRect().height`는 렌더링된 엘리먼트의 크기를 반환하기 때문에 스타일이 적용된 크기를 가져올 수 있다.

## 참고사이트

[엘리먼트의 크기 가져오기 (offsetWidth, clientWidth, scrollWidth)](https://ohgyun.com/571)
