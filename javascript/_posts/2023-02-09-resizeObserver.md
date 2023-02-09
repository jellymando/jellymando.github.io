---
layout: post
title: "ResizeObserver API : 엘리먼트 크기 변화 감지하기"
sitemap: false
---

{:toc .large-only}

## ResizeObserver

HTML 엘리먼트의 크기 변화를 감지할 수 있는 API다. (브라우저 창의 크기가 변경됨을 감지하려면 `window.addEventListener('resize')`)

```js
const resizeObserver = new ResizeObserver((entries) => {
  for (const entry of entries) {
    if (entry.contentBoxSize) {
      const contentBoxSize = entry.contentBoxSize[0];
      h1Elem.style.fontSize = `${Math.max(
        1.5,
        contentBoxSize.inlineSize / 200
      )}rem`;
      pElem.style.fontSize = `${Math.max(
        1,
        contentBoxSize.inlineSize / 600
      )}rem`;
    } else {
      h1Elem.style.fontSize = `${Math.max(
        1.5,
        entry.contentRect.width / 200
      )}rem`;
      pElem.style.fontSize = `${Math.max(1, entry.contentRect.width / 600)}rem`;
    }
  }
});

checkbox.addEventListener("change", () => {
  if (checkbox.checked) {
    resizeObserver.observe(divElem);
  } else {
    resizeObserver.unobserve(divElem);
  }
});
```

ResizeObserver 객체를 생성한 후 observe(), unobserve() 메서드로 엘리먼의 크기 변화를 지켜보거나 취소한다.

### entry

resize가 발생하면 ResizeObserver 콜백 함수가 실행되며 entries가 전달된다.

각 entry는 지켜보고 있는 엘리먼트의 크기값을 가지고 있다.

- entry.borderBoxSize : 테두리를 포함한 크기
- entry.contentBoxSize : 테두리를 제외한 크기

위의 boxSize는 contentBoxSize {blockSize, inlineSize} 객체를 담은 배열이다.

## 참고사이트

[ResizeObserver](https://developer.mozilla.org/en-US/docs/Web/API/ResizeObserver)
