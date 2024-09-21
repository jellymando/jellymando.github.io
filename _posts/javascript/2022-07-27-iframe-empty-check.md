---
title: 'iframe이 제대로 마운트되지 않은 경우 체크'
categories: [Javascript]
tags: [javascript, iframe]
---

{:toc .large-only}

## onLoad 이벤트 핸들러 추가

리액트에서 onLoad를 통해 iframe이 로드되었을 때 이벤트를 실행할 수 있다.

참고로 iframe 내부에서 서버 에러가 발생해도 로드 되었다는 이벤트가 발생한다.

```html
<iframe onLoad="{handleOnLoadIframe}" />
```

## iframe 내부 root 체크

`contentDocument`로 iframe 안의 document값을 얻을 수 있다.

꼼수를 발휘하여 iframe의 document에 root에 엘리먼트가 마운트 되었는지를 체크했다.

root 엘리먼트가 없거나 비어있는 경우 iframe이 정상적으로 마운트되지 않은 것으로 간주한다.

```js
cosnt handleOnLoadIframe = () => {
    const iframeRoot = e.target.contentDocument.getElementById('root')
    if (!iframeRoot || !iframeRoot.children.length > 0) {
    // iframe is empty
    }
}
```

## 참고사이트

[HTMLIFrameElement.contentDocument](https://developer.mozilla.org/en-US/docs/Web/API/HTMLIFrameElement/contentDocument)
