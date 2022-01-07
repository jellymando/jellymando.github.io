---
layout: post
title: "무한 스크롤 구현하기 : scrollTop, scrollHeight"
sitemap: false
---

{:toc .large-only}

## 무한 스크롤 구현하기

scroll 이벤트를 통해서 페이지의 스크롤 위치를 감지할 수 있다.

### Element.scrollTop

**요소의 상단에서 맨 위에 보이는 콘텐츠까지의 거리**를 측정 한 값

요소의 콘텐츠가 수직 스크롤바를 생성하지 않는 경우 해당 scrollTop값은 0이다.

### Element.clientHeight

요소의 내부 높이(px)

패딩은 포함되지만 테두리, 여백 및 가로 스크롤 막대는 제외된다.

### Element.scrollHeight

화면에 보이지 않는 내용을 포함하는 요소의 내용의 높이

<img src="https://developer.mozilla.org/en-US/docs/Web/API/Element/scrollHeight/scrollheight.png">

### Document.scrollingElement

scrollingElement 속성은 HTML body 요소가 있고 스크롤 가능한 경우 HTML 요소를 반환하고, 그렇지 않으면 null을 반환

페이지를 끝까지 스크롤 했을 때, `scrollTop + clientHeight === scrollHeight`가 된다.

이것을 자바스크립트로 표현하면 아래와 같다.

```js
const onScroll = (e) => {
  const { scrollTop, clientHeight, scrollHeight } = e.target.scrollingElement;
  if (scrollTop + clientHeight >= scrollHeight) {
    console.log("끝까지 스크롤 했습니다.");
  }
};

document.addEventListener("scroll", onScroll);
```

But, 이유는 모르겠지만 끝까지 내려도 scrollTop 더하기 clientHeight가 scrollHeight가 되지 않는 경우도 가끔 있는데..

`Meth.ceil(scrollTop)` 으로 scrollTop을 반올림 해주면 응급처치가 될 것 같다.

scroll 이벤트를 걸면 스크롤 할 때마다 무수히 많은 쿼리가 발생한다.

이는 성능 저하를 일으키기 때문에 debounce나 throttle을 사용하여 해결하는 것이 좋다.

## 참고사이트

[요소가 완전히 스크롤되었는지 확인](https://developer.mozilla.org/en-US/docs/Web/API/Element/scrollHeight#problems_and_solutions)
