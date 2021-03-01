---
layout: post
title: 'Event.stopPropagation()'
sitemap: false
---

{:toc .large-only}

## 이벤트 전달 및 DOM 이벤트 흐름

<img src="https://www.w3.org/TR/DOM-Level-3-Events/images/eventflow.svg">

<br/>
이벤트가 통과하는 전파 경로는 문서의 계층적 트리 구조를 반영합니다.

이벤트 단계에는 캡처 단계, 목표 단계 및 버블 단계의 세 가지가 있습니다.

단계가 지원되지 않거나 이벤트 객체의 전파가 중지된 경우 단계를 건너 뜁니다.

> 캡처 단계 : 조상을 통해 이벤트 객체의 대상의 부모까지 순서대로 내려오는 단계. 이 단계를 캡처 단계라고 합니다.

> 대상 단계 : 이벤트 객체의 도착 이벤트 대상. 이벤트 객체는 이 단계의 완료 후 정지합니다.

> 버블 단계 : 대상의 부모에서 시작하여 역순으로 올라가 조상에서 끝나는 단계. 이 단계를 버블링 단계라고 합니다.

## event.stopPropagation();

`event.stopPropagation()` 를 사용하면 이벤트 캡쳐링과 버블링에 있어 현재 이벤트 이후의 전파를 막습니다.

```js
item.addEventListener('click', function (e) {
  e.stopPropagation();
  e.target.classList.toggle('selected');
});
document.body.addEventListener('click', function (e) {
  items.forEach(function (elem) {
    elem.classList.remove('selected');
  });
});
```

위 예제에서 item.addEventListener 안에 `e.stopPropagation()` 을 해주지 않으면 버블링되어 body에서 selected 클래스가 다시 remove 됩니다.

<br/>
[Event.stopPropagation ()](https://developer.mozilla.org/ko/docs/Web/API/Event/stopPropagation)<br/>
[이벤트 전달 및 DOM 이벤트 흐름](https://www.w3.org/TR/DOM-Level-3-Events/#event-flow)<br/>
[event.stopPropagation(), event.preventDefault () 이해하기](https://ismydream.tistory.com/98)
