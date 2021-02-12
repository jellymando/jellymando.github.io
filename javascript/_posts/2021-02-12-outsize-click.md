---
layout: post
title: 'Vanilla JS 외부 영역 클릭 감지하기'
sitemap: false
---

{:toc .large-only}

## e.target과 contains

e.target과 Node.contains를 이용하여 외부 영역을 클릭했는지 감지한다.

```js
  handleClickOutside(e) {
    const $contentWrapper = document.getElementById('modal');
    if ($contentWrapper && !$contentWrapper.contains(e.target)) {
      this.handleClose();
    }
  }
```

contains를 사용할 때는 Node가 명확해야한다.
`const $contentWrapper = document.getElementsByClassName('modal')`로 했을 때 contains is not a function 에러가 났었다.
if문에서 `$contentWrapper &&` 를 넣은 이유는 그럴 일은 거의 없겠지만 `$contentWrapper` 요소가 없을 때는 실행되지 않도록 하기 위해서다.

<br/>

[클릭 외부 영역 감지](https://www.javaer101.com/ko/article/2655964.html)
