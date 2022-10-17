---
layout: post
title: '[styled-components] StyleSheetManager 사용하기'
sitemap: false
---

{:toc .large-only}

## StyleSheetManager

하위 컴포넌트의 스타일 처리 방식을 설정하기 위한 모듈이다.

iframe 안에 `createPortal`로 컴포넌트를 집어넣을 때, 컴포넌트와 관련된 스타일이 iframe 내부에 생기지 않아 페이지가 깨지는 현상 때문에 사용하였다.

스타일 적용할 컴포넌트를 `StyleSheetManager`로 감싸고 `target`에 iframe의 head 노드를 전달하면 된다.

```js
const iframeHead =
  ref.current && ref.current.contentDocument && ref.current.contentDocument.head

return (
  <StyleSheetManager target={iframeHead}>
    <iframe ref={ref}>
      {iframeBody && createPortal(children, iframeBody)}
    </iframe>
  </StyleSheetManager>
)
```

이렇게 해주면 iframe의 head에 스타일이 삽입된다.

## 참고사이트

[StyleSheetManager](https://styled-components.com/docs/api)
