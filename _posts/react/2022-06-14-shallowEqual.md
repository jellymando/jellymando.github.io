---
title: 'useSelector 최적화, shallowEqual 사용하기'
categories: [React]
tags: [redux, useSelector]
---

{:toc .large-only}

## useSelector와 리렌더링

useSelector를 통해 스토어의 상태를 조회하면 기본적으로는 상태가 바뀌지 않으면 리렌더링하지 않는다.

```js
const todos = useSelector((state) => state.todos)
```

하지만 아래처럼 스토어의 상태를 객체로 가져오면, 상태가 바뀌었는지 체크할 수 없기 때문에 action이 일어날 때마다 리렌더링하게 된다.

```js
const { number, diff } = useSelector((state) => ({
  number: state.counter.number,
  diff: state.counter.diff
}))
```

## 해결방법

useSelector로 가져오는 상태마다 변수를 선언한다.

```js
const number = useSelector((state) => state.counter.number)
const diff = useSelector((state) => state.counter.diff)
```

하지만 비효율적이다.

다른 방법은 shallowEqual를 useSelector의 두번째 인자로 전달해주는 것이다.

```js
import { useSelector, shallowEqual } from 'react-redux'

function CounterContainer() {
  const { number, diff } = useSelector(
    (state) => ({
      number: state.counter.number,
      diff: state.counter.diff
    }),
    shallowEqual
  )
}
```

shallowEqual은 react-redux에 내장되어있는 함수로서, 얕은 비교를 이용하여 객체를 비교한다.

이전 상태와 현재 상태가 같지 않으면 false를 반환하여 리렌더링한다.

이전 상태와 현재 상태가 완전히 같을 때마다 true를 반환하고 리렌더링 하지 않는다.

## 참고사이트

[8. useSelector 최적화](https://react.vlpt.us/redux/08-optimize-useSelector.html)<br/>
[react-redux의 shallowEqual 사용하기](https://2ham-s.tistory.com/342)<br/>
[shallowequal](https://www.npmjs.com/package/shallowequal)
