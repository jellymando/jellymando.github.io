---
title: 'Intersection Observer API으로 스크롤 감지하기'
categories: [JAVASCRIPT]
tags: [javascript, intersection observer]
---

{:toc .large-only}

## Intersection Observer API

`Intersection Observer API`는 타겟 요소와 와 설정한 요소(Element)의 교차점을 비동기적으로 관찰하는 방법이다.

## scroll 이벤트와 다른점

- scroll 이벤트는 사용자가 스크롤할 때마다 끊임없이 호출된다.
- Intersection Observer는 debounce/throttle을 사용하지 않아도 된다.
- scroll 이벤트를 사용하면 offsetTop 값을 구하기 위해 매번 reflow가 발생하지만 Intersection Observer를 사용하면 reflow가 일어나지 않는다.

## 사용법 (무한스크롤 예시)

```html
<div class="container">
  <div class="item">Item 1</div>
  <div class="item">Item 2</div>
  <div class="item">Item 3</div>
  <div class="item">Item 4</div>
  <div id="scrollArea"></div>
</div>
```

위처럼 목록 맨 아래에 스크롤을 감지할 엘리먼트를 추가해준다.

```js
function setIntersectionObserver() {
  const callback = (entries, observer) => {
    entries.forEach((entry) => {
      if (!entry.isIntersecting) {
        return
      }
    })
  }
  const options = {
    root: null,
    rootMargin: '0px',
    threshold: 1.0
  }
  const observer = new IntersectionObserver(callback, options)
  observer.observe(el)
  return observer
}
```

`IntersectionObserver`를 생성하고 `observe()`로 observer 목록에 감지할 요소를 추가한다.

`callback`은 요소의 가시성이 `threshold` 만큼 변경될 때마다 실행된다.

요소가 `threshold` 만큼 보이는 경우, `entry` 객체 안의 `isIntersecting` 값이 `true`가 된다.

다시 스크롤을 올려 요소가 보이지 않게 되면 `entry` 객체 안의 `isIntersecting` 값이 `false`가 된다.

따라서 `!entry.isIntersecting`인 경우에는 `callback`을 실행하지 않으면 된다.

## Options

- `root` : 감지할 엘리먼트의 가시성을 확인할 때 사용되는 뷰포트 요소. root 값이 null 이거나 지정되지 않을 때 브라우저 뷰포트로 설정된다.
- `rootMargin` : `root`가 가진 margin값
- `threshold` : 감지할 엘리먼트의 가시성 퍼센트를 나타내는 숫자 혹은 배열. 기본값은 `0`이며(요소가 1픽셀이라도 보이면 callback이 실행됨). `1.0`은 요소의 모든 픽셀이 화면에 노출되어야 callback 실행

## 참고사이트

[React 무한 스크롤 구현하기 with Intersection Observer](https://velog.io/@jce1407/React-%EB%AC%B4%ED%95%9C-%EC%8A%A4%ED%81%AC%EB%A1%A4-%EA%B5%AC%ED%98%84%ED%95%98%EA%B8%B0-with-Intersection-Observer)<br/>
[Intersection Observer - 요소의 가시성 관찰](https://heropy.blog/2019/10/27/intersection-observer/)<br/>
[자바스크립트로 IntersectionObserver API 다루기](https://imkh.dev/js-intersection-observer/)<br/>
[Intersection Observer API](https://developer.mozilla.org/ko/docs/Web/API/Intersection_Observer_API)
