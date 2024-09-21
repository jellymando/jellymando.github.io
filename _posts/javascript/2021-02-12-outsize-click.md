---
title: '[contains] 외부 영역 감지하기'
categories: [JAVASCRIPT]
tags: [javascript, 외부 영역 감지]
---

{:toc .large-only}

## contains

contains를 이용하여 이벤트 타겟이 엘리먼트 외부 영역에 있는지 감지할 수 있다.

```js
  handleClickOutside(e) {
    const $contentWrapper = document.getElementById('modal');
    if ($contentWrapper && !$contentWrapper.contains(e.target)) {
      this.handleClose();
    }
  }
```

contains를 사용할 때는 엘리먼트가 명확해야 한다.

`const $contentWrapper = document.getElementsByClassName('modal')`로 했을 때 contains is not a function 에러가 났었다.

## svg 주의

엘리먼트 안의 svg를 클릭했을 때는 contains가 false로 나오기 때문에 svg에 `pointer-events: none` 스타일을 추가해줘야 한다.

## 참고사이트

[클릭 외부 영역 감지](https://www.javaer101.com/ko/article/2655964.html)
