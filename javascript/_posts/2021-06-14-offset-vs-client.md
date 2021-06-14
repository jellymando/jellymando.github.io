---
layout: post
title: "이벤트 좌표 client, offset 차이"
sitemap: false
---

{:toc .large-only}

### clientX, clientY

- clientX : **브라우저 페이지에서의 X좌표 위치**를 반환하나 스크롤은 무시하고 해당 페이지의 상단을 0으로 측정합니다.

- clientY : **브라우저 페이지에서의 Y좌표 위치**를 반환하나 스크롤은 무시하고 해당 페이지의 상단을 0으로 측정합니다.

### offsetX, offset

- offsetX : **이벤트 대상 객체에서의 상대적 마우스 x좌표** 위치를 반환합니다.

- offsetY : **이벤트 대상 객체에서의 상대적 마우스 y좌표** 위치를 반환합니다.

[clientX, offsetX, pageX, screenX의 차이](http://megaton111.cafe24.com/2016/11/29/clientx-offsetx-pagex-screenx%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90/)
