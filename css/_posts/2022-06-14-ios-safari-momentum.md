---
layout: post
title: 'IOS Safari에서 스크롤 이벤트 모멘텀 해결하기'
sitemap: false
---

{:toc .large-only}

## 모멘텀?

IOS 사파리에서 페이지 화면을 쓕 쓸어내리면 스크롤이 된다.

안드로이드에서와는 달리 스크롤 되는 속도에 가속도가 붙었다가 천천히 느리게 멈춘다.

이렇게 화면에서 touchend가 된 후에도 스크롤이 멈추지 않는 것을 모멘텀이라고 한다.

문제는 모멘텀이 일어나는 동안 다른 스크롤 이벤트를 발생시키면 먹히지 않는다는 것이다.

아래로 버튼을 눌렀을 때, 모멘텀을 무시하고 맨 밑으로 내려가야 하는데 내려가지 않거나 내려갔다가 모멘텀으로 인해 다시 위로 스크롤되는 현상이 있었다.

## 해결방법

예전에는 `-webkit-overflow-scrolling: auto;`로 해결할 수 있었던 것 같다.

하지만 지금은 위 방법으로도 모멘텀 발생을 막을 수 없다.

당연히 안 될 줄 알았던 방법인데, `overflow-y: scroll;` 스타일이 적용되어 있는 엘리먼트에 `style.overflowY = 'hidden'`를 적용하고 원하는 곳으로 스크롤을 이동시킨 다음에, `style.overflowY = 'scroll'` 을 적용해주니 정상적으로 이동한다!

```js
scrollElement.style.overflowY = 'hidden'
scrollElement.scrollTop = somewhere
scrollElement.style.overflowY = 'scroll'
```

overflowY가 hidden이 되면 scroll 이벤트가 아예 발생되지 않는다! 스크롤이 있어야 scroll 이벤트가 발생되는 것이었다..

## 참고사이트

[Momentum Scrolling on iOS Overflow Elements](https://css-tricks.com/snippets/css/momentum-scrolling-on-ios-overflow-elements/)<br/>
[모바일 사파리에서 스크롤 구현과 관련된 문제](https://blog.outsider.ne.kr/971)<br/>
[[Javascript] ios Momentum Scrolling Issue(탄력스크롤)](https://steadev.tistory.com/69)
