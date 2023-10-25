---
layout: post
title: '함수형 컴포넌트에서 prevState 구현하기'
sitemap: false
---

{:toc .large-only}

## prevState

함수형 컴포넌트는 생명주기가 없기 때문에 클래스형 컴포넌트의 `componentDidUpdate` 같이 `prevProps, prevState`를 제공하는 메서드가 없다.

함수형 컴포넌트를 만들다 보면, 이전 상태값과 현재 상태값을 특정지어서 비교해야 될 때가 생기는데 (ex. prevState는 false, currentState는 true 여야만 하는 조건을 걸어야 할 때), 어떻게 구현할 수 있을까?

## useRef 사용

useRef에 `prevState` 값을 담아 비교할 수 있다.

```js
const functionComponent = () => {
  const [state, setState] = useState(false)
  const prevState = useRef(state)

  useEffect(() => {
    if (prevState.current !== state && state) {
      // prevState가 false, state가 true인 경우
    }
    // prevState 업데이트
    prevState.current = state
  }, [state])
}
```

## Custom Hook 사용

```js
function usePrevious(value) {
  const ref = useRef()

  useEffect(() => {
    ref.current = value
  }, [value])

  return ref.current
}

function Counter() {
  const [count, setCount] = useState(0)
  // 👇 look here
  const prevCount = usePrevious(count)

  return (
    <h1>
      Now: {count}, before: {prevCount}
    </h1>
  )
}
```

useRef를 좀 더 응용하여 usePrevious 커스텀 훅을 생성하여 사용할 수 있다.

<img src="/assets/img/blog/2022-05-22-prevState_01.png">

usePrevious에 0이 인자로 전달되어 호출된다.

<img src="/assets/img/blog/2022-05-22-prevState_02.png">

useRef 인스턴스인 prevCount가 생성된다. 이 때 useRef() 기본값이 비어있으므로 prevCount.current 값은 undefined이다.

useEffect는 컴포넌트가 렌더링 된 후 실행되는 hook이기 때문에, **useEffect를 실행하지 않고 undefined 값이 반환된다.**

즉, Counter 컴포넌트에서 리턴되는 내용은 'Now: 0, before: undefined' 이다.

<img src="/assets/img/blog/2022-05-22-prevState_03.png">

렌더링이 완료된 후 useEffect가 실행되어 `prevCount.current` 값이 드디어 0으로 업데이트된다!

하지만 ref 값은 state가 아니기 때문에 리렌더링되진 않는다.

Counter의 state 값이 변경되면 다시 usePrevious가 호출되고, 이 때 0을 리턴한다.

이렇게 해서 usePrevious가 prevState 값을 저장하고 리턴할 수 있다.

<img src="/assets/img/blog/2022-05-22-prevState_04.png">

## 참고사이트

[Accessing previous props or state with React Hooks](https://blog.logrocket.com/accessing-previous-props-state-react-hooks/#custom-hook-useprevious-hook)<br/>
[[React]Hook에서 prevState 구현](https://developer-talk.tistory.com/224)
