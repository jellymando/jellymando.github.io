---
title: 'CustomEvent()로 이벤트 커스텀하기'
categories: [Javascript]
tags: [javascript, custom event]
---

{:toc .large-only}

1. CustomEvent()

`CustomEvent()`를 사용하여 이벤트를 만들고, 임의로 발생시킬 수 있다.

```js
CustomEvent(typeArg)
CustomEvent(typeArg, options)
```

- typeArg : 이벤트 이름
- options : 이벤트 관련 정보를 나타내는 객체. `{"detail": {[key]: value}}` 구조

```js
// CustomEvent 생성
const catFound = new CustomEvent('animalfound', {
  detail: {
    name: 'cat'
  }
})
const dogFound = new CustomEvent('animalfound', {
  detail: {
    name: 'dog'
  }
})
```

1. 이벤트 등록

이벤트를 발생시킬 타겟에 EventListener를 등록한다.

```js
// 적합한 이벤트 수신기 부착
obj.addEventListener('animalfound', (e) => console.log(e.detail.name))
```

1. dispatchEvent()

EventTarget 객체로 Event를 발송하여 해당 이벤트에 대해 등록된 EventListener를 호출한다.

```js
// 이벤트 발송
obj.dispatchEvent(catFound)
obj.dispatchEvent(dogFound)
```

## 참고사이트

[CustomEvent()](https://developer.mozilla.org/ko/docs/Web/API/CustomEvent/CustomEvent)<br/>
[EventTarget.dispatchEvent()](https://developer.mozilla.org/ko/docs/Web/API/EventTarget/dispatchEvent)
