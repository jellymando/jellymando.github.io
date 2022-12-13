---
layout: post
title: 'useEffect 의존성 배열에 useCallback 함수를 넣을 때 주의하기'
sitemap: false
---

{:toc .large-only}

## useEffect 의존성 배열에 useCallback 함수를 넣으면 어떻게 될까?

useEffect 안에서 useCallback 함수를 사용하는 경우, 의존성 배열에 함수를 넣지 않으면 eslint가 노란색 밑줄을 표시한다.

밑줄에 마우스를 갖다대면 'Either include it or remove the dependency array.'

이런 문구가 나오는데, 함수를 의존성 배열에 추가하거나 제거하라는 내용이다. 즉, 추가가 필수는 아니라는거다.

하지만 괜히 노란 줄이 쳐져 있으면 찜찜해서 useCallback 함수를 의존성 배열에 추가하곤 하는데..

이렇게 하면 useEffect가 의도와는 다르게 동작하게 될 수 있다.

## 직접 확인해보기 위해 Test 컴포넌트를 만들어보았다.

```js
import React, { useState, useCallback, useEffect } from 'react'

function Test() {
  const [state1, setState1] = useState(0)
  const [state2, setState2] = useState(0)

  const callback = useCallback(() => {
    console.log('-----------콜백 실행-----------', state1)
  }, [state1])

  useEffect(() => {
    console.log('-----------useEffect-----------')
    callback()
  }, [state2, callback])

  return (
    <>
      <button onClick={() => setState1((state1) => state1 + 1)}>버튼1</button>
      <button onClick={() => setState2((state2) => state2 + 1)}>버튼2</button>
    </>
  )
}

export default Test
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

짞짞짞!! 버튼1을 눌렀을 때 state1이 바뀌면서 callback도 업데이트 되고,

버튼2를 눌렀을 때 useEffect가 실행되고 callback 안의 state1 값도 잘 업데이트 되었다!

노란줄 표시됐다고 무조건 넣지 말고, 의도를 생각해보며 작성해야 할 것 같다!
