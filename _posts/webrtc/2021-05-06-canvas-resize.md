---
title: "canvas의 크기를 수정하면 내용이 지워지고 까맣게 변하는 이슈"
categories: [WEBRTC]
tags: [webrtc, canvas]
---

{:toc .large-only}

canvas를 사용할 때는 태그에 width, height 값을 꼭 넣어주어야 한다.

(속성을 정의하지 않을 경우 기본으로 300, 150 크기를 가진다.)

canvas의 width, height를 직접 변경할 때는 setState 등을 통해 상태를 변경하거나 javascript property를 이용한다.

```js
canvas.width = 800;
canvas.height = 600;
```

<br/>

그러나 canvas 크기를 직접 수정하면 canvas의 내용물이 초기화 되어버린다.

이런 경우 크기 변경 후 표시하려는 콘텐츠를 다시 그려주어야 한다.

**해결법**: css를 사용하여 canvas 크기를 임의로 설정할 수 있으며 width와 height를 고정시키고 style로 size를 변경하면 내용물이 지워지지 않는다.

> CSS 크기 지정이 초기 캔버스의 비율을 고려하지 않으면 왜곡되어 나타납니다. 만약 렌더링이 왜곡된 것처럼 보이는 경우 CSS를 사용하지 않고 `<canvas>` 속성에서 width 및 height 속성을 명시적으로 지정하십시오.

```js
canvas.style.width = "800px";
canvas.style.height = "600px";
```

<br/>

[캔버스 리사이즈 시 주의할 점](https://ohgyun.com/323)<br/>
[캔버스(Canvas) 기본 사용법](https://developer.mozilla.org/ko/docs/Web/API/Canvas_API/Tutorial/Basic_usage)
