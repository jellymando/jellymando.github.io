---
title: 'useEffect 의존성 배열에 ref 사용'
categories: [REACT]
tags: [react, useEffect]
---

{:toc .large-only}

## 자꾸 까먹어서 메모

`useRef`는 내용이 변경될 때 그것을 알려주지는 않는다는 것을 유념하세요.

`.current` 프로퍼티를 변형하는 것이 **리렌더링을 발생시키지는 않습니다.**

React가 DOM 노드에 ref를 attach하거나 detach할 때 어떤 코드를 실행하고 싶다면 대신 콜백 ref를 사용하세요.

## 콜백 ref

DOM 노드의 위치나 크기를 측정하는 기본적인 방법의 하나는 콜백 ref를 사용하는 것입니다.

React는 ref가 다른 노드에 연결될 때마다 해당 콜백을 호출합니다.

```js
function MeasureExample() {
  const [height, setHeight] = useState(0)

  const measuredRef = useCallback((node) => {
    if (node !== null) {
      setHeight(node.getBoundingClientRect().height)
    }
  }, [])

  return (
    <>
      <h1 ref={measuredRef}>Hello, world</h1>
      <h2>The above header is {Math.round(height)}px tall</h2>
    </>
  )
}
```

## 참고사이트

[useRef](https://ko.reactjs.org/docs/hooks-reference.html#useref)<br/>
[콜백 ref](https://ko.reactjs.org/docs/hooks-faq.html#how-can-i-measure-a-dom-node)
