---
title: '리액트 합성 이벤트 throttle 적용 안되는 이슈'
categories: [REACT]
tags: [react, throttle]
---

{:toc .large-only}

```js
onChange={throttle(handleKeyChange, 250)}
```

이런 식으로 컴포넌트에 리액트 이벤트를 등록하면 `throttle`이 적용되지 않는다.

하지만 `handleKeyChange`를 아래와 같이 수정하면 정상 동작한다.

```js
const handleKeyChange = throttle(() => {}, 250)
```

클로저가 생성되지 않아서 `throttle`에서 timer 변수가 계속 새로 선언되기 때문이다.
신기...
