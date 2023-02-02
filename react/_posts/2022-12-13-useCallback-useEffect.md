---
layout: post
title: 'React hook 의존성 배열에 useCallback 함수를 넣을 때 주의하기'
sitemap: false
---

{:toc .large-only}

## useEffect 의존성 배열에 useCallback 함수를 넣으면 어떻게 될까?

useEffect 안에서 useCallback 함수를 사용하는 경우, 의존성 배열에 함수를 넣지 않으면 eslint가 노란색 밑줄을 표시한다.

밑줄에 마우스를 갖다대면 'Either include it or remove the dependency array.'

이런 문구가 나오는데, 함수를 의존성 배열에 추가하거나 제거하라는 내용이다. 즉, 추가가 필수는 아니라는거다.

하지만 괜히 노란 줄이 쳐져 있으면 찜찜해서 useCallback 함수를 의존성 배열에 추가하곤 하는데..

이렇게 하면 useEffect가 의도와는 다르게 동작하게 될 수 있다.

## 직접 확인해보기 위해 컴포넌트를 만들어보았다.

```js
import React, { useState, useCallback, useEffect } from 'react'

function App() {
  const [count1, setCount1] = useState(0)
  const [count2, setCount2] = useState(0)

  const callback = useCallback(() => {
    console.log('-----------콜백 실행-----------', count1)
  }, [count1])

  useEffect(() => {
    console.log('-----------useEffect-----------')
    callback()
  }, [count2, callback])

  return (
    <>
      <button onClick={() => setCount1((count1) => count1 + 1)}>버튼1</button>
      <button onClick={() => setCount2((count2) => count2 + 1)}>버튼2</button>
    </>
  )
}

export default App
```

버튼1을 클릭하면 state1이 변경되고, state1이 변경되면 callback 함수가 업데이트 된다.

useEffect 의존성 배열에는 state2, callback을 넣었다.

의도대로라면 버튼1을 클릭했을 때는 state1만 변화하므로, useEffect와는 관계가 없어야 한다.

하지만 버튼1을 클릭해보면 callback이 업데이트 되면서 아래와 같이 useEffect가 실행되어 callback 함수가 실행된다.

<img src="/assets/img/blog/2022-12-13-useCallback-useEffect_01.gif" style="margin-top:20px" />

## 의도대로 동작하게 하려면

노락색 밑줄이 찜찜해도 useEffect가 본래의 목적대로 실행되려면 의존성 배열에서 callback을 제거해야 한다.

```js
useEffect(() => {
  console.log('-----------useEffect-----------')
  callback()
}, [state2])
```

하지만 걱정인 것은 callback을 실행했을 때 state1 값이 잘 업데이트 될까?

이번엔 버튼1과 버튼2를 번갈아 누르면서 테스트해보자.

<img src="/assets/img/blog/2022-12-13-useCallback-useEffect_02.gif" style="margin:20px 0" />

짝짝짝!🤗 버튼1을 눌렀을 때 state1이 바뀌면서 컴포넌트가 리렌더링 되어 callback이 업데이트 되고,

버튼2를 눌렀을 때 count2가 업데이트되어 useEffect가 실행되면서 위에서 업데이트된 callback이 실행된다.

노란줄 표시됐다고 무조건 넣지 말고, 의도를 생각해보며 작성해야 할 것 같다!

## 이벤트 사용 시 주의사항!

useEffect로 이벤트 핸들러를 추가하는 경우에는 의존성 배열에 함수를 추가해야 한다.

```js
const callback3 = useCallback(() => {
  console.log('-----------콜백 실행-----------', count1)
}, [count1])

useEffect(() => {
  document.addEventListener('click', callback3)
}, []) // callback3을 넣지 않으면 count1 값이 업데이트 되지 않는다.
```

위 코드처럼 의존성 배열을 넣지 않으면 count1 값이 변경되도 document 클릭 시 상태값이 업데이트 되지 않는다.

이벤트 핸들러가 상태값을 참조하는 경우 의존성 배열에 핸들러 함수를 추가해야 한다.

혹은 이벤트 핸들러를 굳이 useCallback으로 감싸지 않고 의존성 배열에도 추가하지 않는 것도 방법이 될 수 있다.

## useCallback에는 의존성 배열을 넣어줘야 한다.

useCallback에도 의존성 배열이 있는데, 이것 때문에 useEffect를 사용할 때와 헷갈리는 것 같다.

useEffect에는 함수를 의존성 배열에 넣지 않아도 상태가 바뀌면 리렌더링 되면서 함수가 업데이트 되지만,

useCallback에는 함수를 의존성 배열에 넣어줘야 한다.

```js
const callback1 = useCallback(() => {
  return `Count : ${count1}`
}, [count1])

const callback2 = useCallback(() => {
  console.log('-----------콜백 실행-----------', callback1())
}, [callback1]) // 참조하는 함수를 의존성 배열에 넣어줘야 한다!

useEffect(() => {
  console.log('-----------useEffect-----------')
  callback2()
}, [count2])
```

위 코드에서 callback2의 의존성 배열에 callback1을 넣지 않으면, callback1을 실행하더라도 count1 값이 업데이트 되지 않는다.

[코드샌드박스](https://codesandbox.io/s/usecallback-dependency-d5h06s?file=/src/App.jsx)에서 직접 실행해볼 수 있다.
