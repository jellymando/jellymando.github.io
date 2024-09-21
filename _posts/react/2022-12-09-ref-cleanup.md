---
title: '언마운트 시 Ref.current 이벤트 clean-up 하기'
categories: [React]
tags: [react]
---

{:toc .large-only}

### 에러 발생

아래와 같이 컴포넌트에서 ref.current를 클린업하면 에러가 발생한다.

```js
useEffect(() => {
  if (containerRef.current) {
    containerRef.current.addEventListener(() => {
      console.log('event')
    })
  }

  return () => {
    if (containerRef.current) {
      containerRef.current.removeEventListener(() => {
        console.log('event')
      })
    }
  }
}, [containerRef])
```

> The ref value 'containerRef.current' will likely have changed by the time this effect cleanup function runs. If this ref points to a node rendered by React, copy 'containerRef.current' to a variable inside the effect, and use that variable in the cleanup function

`containerRef.current`가 클린업이 실행될 때까지 변경되었을 수 있기 때문에 발생하는 에러이다.

## 해결방법

`containerRef.current`를 변수에 저장하여 사용하면 에러가 나지 않는다.

```js
useEffect(() => {
  const container = containerRef.current
  if (container) {
    container.addEventListener(() => {
      console.log('event')
    })
  }

  return () => {
    if (container) {
      container.removeEventListener(() => {
        console.log('event')
      })
    }
  }
}, [containerRef])
```

## 참고사이트

[Cleanup ref issues in React](https://stackoverflow.com/questions/67069827/cleanup-ref-issues-in-react)
