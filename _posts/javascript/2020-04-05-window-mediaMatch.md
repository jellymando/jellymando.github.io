---
title: 'Window.matchMedia()'
categories: [JAVASCRIPT]
tags: [javascript]
---

{:toc .large-only}

`Window.matchMedia()` 메서드는 주어진 미디어 쿼리 문자열의 분석 결과를 나타내는 MediaQueryList (en-US) 객체를 반환합니다.

`window.matchMedia("(min-width: 400px)")`를 출력하면 아래와 같은 객체를 반환한다.

```js
MediaQueryList {
    matches: true
    media: "(min-width: 400px)"
    onchange: null
}
```

matches 속성은 media 조건에 대한 boolean 값을 포함한다.

이를 이용하여 OS 테마 등을 감지할 수 있다.
<br/>

```js
// OS 다크 모드 감지
const isWindowDark = window.matchMedia('(prefers-color-scheme: dark)').matches;

if (window.matchMedia('(min-width: 400px)').matches) {
  /* 뷰포트 너비가 400 픽셀 이상 */
} else {
  /* 뷰포트 너비가 400 픽셀 미만 */
}
```

<br/>

[Window.matchMedia ()](https://developer.mozilla.org/ko/docs/Web/API/Window/matchMedia)
