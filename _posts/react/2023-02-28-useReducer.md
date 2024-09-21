---
title: 'useReducer를 사용하여 useState 대체하기'
categories: [Javascript]
tags: [react, useReducer]
---

{:toc .large-only}

```js
const [startDate, setStartDate] = useState()
const [endDate, setEndDate] = useState()
const [title, setTitle] = useState('')
const [description, setDescription] = useState('')
const [location, setLocation] = useState()
const [attendees, setAttendees] = useState([])
```

useState로 관리하는 상태가 많고 복잡할 때 useReducer로 대체할 수 있다.

```js
const [event, updateEvent] = useReducer(
  (prev, next) => {
    return { ...prev, ...next }
  },
  { title: '', description: '', attendees: [] }
)
```

불변성을 유지하기 위해 use-immer 라이브러리를 사용할 수도 있다.

```js
import { useImmerReducer } from 'use-immer'

function reducer(draft, action) {
  switch (action.type) {
    case 'increment':
      draft.count++
      break
    case 'decrement':
      draft.count--
      break
  }
}

function Counter() {
  const [state, dispatch] = useImmerReducer(reducer, initialState)
  return (
    <>
      Count: {state.count}
      <button onClick={() => dispatch({ type: 'increment' })}>+</button>
      <button onClick={() => dispatch({ type: 'decrement' })}>-</button>
    </>
  )
}
```

## 참고사이트

[A Cure for React useState Hell?](https://www.builder.io/blog/use-reducer)<br/>
[[번역] useState 지옥에서 벗어나기](https://velog.io/@eunbinn/a-cure-for-react-useState-hell#usestate%EB%A5%BC-%EC%82%AC%EC%9A%A9%ED%95%98%EB%8A%94-%EA%B1%B0%EC%9D%98-%EB%AA%A8%EB%93%A0-%EA%B3%B3%EC%97%90%EC%84%9C-usereducer%EB%A5%BC-%EC%82%AC%EC%9A%A9%ED%95%A0-%EC%88%98-%EC%9E%88%EC%8A%B5%EB%8B%88%EB%8B%A4)
