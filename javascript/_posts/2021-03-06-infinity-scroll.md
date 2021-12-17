---
layout: post
title: '무한 스크롤 구현하기 : scrollTop, scrollHeight, throttle, debounce'
sitemap: false
---

{:toc .large-only}

## 무한 스크롤 구현하기

### 1. 페이지의 맨 아래로 스크롤 했는지 감지

- Element.scrollTop

**요소의 상단에서 맨 위에 보이는 콘텐츠까지의 거리**를 측정 한 것입니다.

요소의 콘텐츠가 수직 스크롤바를 생성하지 않는 경우 해당 scrollTop값은 0입니다.
<br/>

- Element.clientHeight

요소의 내부 높이 (픽셀 단위)입니다.

패딩은 포함되지만 테두리, 여백 및 가로 스크롤 막대 (있는 경우)는 제외됩니다.
<br/>

- Element.scrollHeight

화면에 보이지 않는 내용을 포함하는 요소의 내용의 높이를 측정합니다.

<img src="https://developer.mozilla.org/en-US/docs/Web/API/Element/scrollHeight/scrollheight.png">
<br/>

- Document.scrollingElement

scrollingElement 속성은 HTML body 요소가 있고 스크롤 가능한 경우 HTML 요소를 반환하고, 그렇지 않으면 null을 반환합니다.

<br/>

페이지를 끝까지 스크롤 했을 때, `scrollTop + clientHeight === scrollHeight` 가 됩니다.

이것을 자바스크립트로 표현하면 아래와 같습니다.

```js
const onScroll = (e) => {
  const { scrollTop, clientHeight, scrollHeight } = e.target.scrollingElement
  if (scrollTop + clientHeight >= scrollHeight) {
    console.log('끝까지 스크롤 했습니다.')
  }
}

document.addEventListener('scroll', onScroll)
```

But, 이유는 모르겠지만 끝까지 내려도 scrollTop 더하기 clientHeight가 scrollHeight가 되지 않는 경우도 가끔 있는데..

`Meth.ceil(scrollTop)` 으로 scrollTop을 반올림 해주면 응급처치가 될 것 같습니다.

<br/>
[요소가 완전히 스크롤되었는지 확인](https://developer.mozilla.org/en-US/docs/Web/API/Element/scrollHeight#problems_and_solutions)

### 2. 성능 향상 - debounce / throttle

scroll 이벤트를 걸면 스크롤 할 때마다 무수히 많은 쿼리가 발생합니다.

이는 성능 저하를 일으키기 때문에 debounce나 throttle을 사용하여 해결하는 것이 좋습니다.

- debounce

발생한 이벤트에 대해 마지막 한 번만 실행합니다.

```js
const debounce = (func, delay) => {
  let timeoutId = null
  return function (...args) {
    clearTimeout(timeoutId)
    timeoutId = setTimeout(() => {
      func(...args)
    }, delay)
  }
}
```

이벤트가 계속 발생해도 앞에서 발생한 setTimeout 값을 clearTimeout 하기 때문에 결국 맨 마지막에 발생한 이벤트만 실행하게 됩니다.
<br/>

- throttle

일정한 시간 간격을 두고 한 번씩만 실행합니다.

```js
const throttle = (func, delay) => {
  let timeoutId = null
  return function (...args) {
    if (!timeoutId) {
      timeoutId = setTimeout(() => {
        timeoutId = null
        func(...args)
      }, delay)
    }
  }
}
```

[쓰로틀링과 디바운싱](https://www.zerocho.com/category/JavaScript/post/59a8e9cb15ac0000182794fa)<br/>
[Debouce, Throttle (디바운스, 쓰로틀)](https://jinminkim-50502.medium.com/javascript-debouce-throttle-3f6618c13fb6)

#### 이벤트 리스너 핸들러로 바로 사용하기

`addEventListener`에 debounce나 throttle 함수를 바로 전달하면 먹히지 않는데, 이벤트가 발생할 때마다 `timeoutId`가 `null`로 초기화되기 때문이다!

`let timeoutId = null`을 `addEventListener` 바깥으로 빼주어야 한다.

```js
let timeoutId = null
document.addEventListener('mousemove', ({ target }) => {
  if (!timeoutId) {
    timeoutId = setTimeout(() => {
      console.log('mousemove target', target)
      timeoutId = null
    }, 300)
  }
})
```

#### 에러 노트

setTimeout 함수 안에 함수를 실행시키는 방법

```js
setTimeout(func.bind(null, ...args), delay)
```

혹은

```js
setTimeout(() => {
  func(...args)
}, delay)
```
