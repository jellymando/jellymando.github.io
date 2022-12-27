---
layout: post
title: 'react-query 사용하기'
sitemap: false
---

{:toc .large-only}

## 설치하기

```bash
npm i @tanstack/react-query
# or
yarn add @tanstack/react-query
```

> @tanstack/react-query(v4)는 react-query(v3)에서 업그레이드 된 최신 버전으로 React 18을 지원한다. [참고](https://tanstack.com/query/v4/docs/react/guides/migrating-to-react-query-4#new-features-)

## 기본 사용법

먼저 react-query를 사용하기 위해 `QueryClientProvider`로 앱을 감싸야 한다.

```js
import { QueryClientProvider } from '@tanstack/react-query'

// Create a client
const queryClient = new QueryClient()

function App() {
  return (
    // Provide the client to your App
    <QueryClientProvider client={queryClient}>
      <Todos />
    </QueryClientProvider>
  )
}
```

default 옵션을 세팅해야 하면 아래처럼 queryClient에 `defaultOptions` 객체를 전달한다.

```js
const queryClient = new QueryClient({
  defaultOptions: {
    queries: {
      refetchOnWindowFocus: false,
      refetchOnMount: false,
      refetchOnReconnect: false,
      retry: false
    }
  }
})
```

## useQuery

`queryKey`, `queryFn` 그리고 옵션을 세팅한다.

```js
useQuery({
  queryKey: ['todos'],
  queryFn: fetchTodos,
  refetchOnWindowFocus: false
})
```

### queryKey

- react-query는 queryKey를 기준으로 데이터를 캐싱한다.
- **queryKey은 중복되지 않는 고유의 값이어야 한다.**
- 기본적으로 배열 형태이며 계층 구조의 식별이 필요하거나 매개변수가 있는 경우 배열에 추가한다.
- 쿼리 함수가 변수에 의존하는 경우, 변수를 queryKey 배열에 추가해야 한다.

```js
// 항목을 고유하게 식별하기 위해 id 전달
useQuery({ queryKey: ['todo', 5], ... })

// 매개변수 전달
useQuery({ queryKey: ['todos', { type: 'done' }], ... })

// 쿼리 함수가 변수에 의존하는 경우, 변수를 queryKey 배열에 추가해야 한다.
function Todos({ todoId }) {
  const result = useQuery({
    queryKey: ['todos', todoId],
    queryFn: () => fetchTodoById(todoId),
  })
}
```

### queryFn

- queryFn는 resolve나 error를 리턴하는 Promise 함수여야 한다.
- `axios`를 사용하지 않고 `fetch`를 사용하면 HTTP 에러를 throw 하지 않으므로 직접 throw 해줘야 한다.

```js
useQuery({
  queryKey: ['todos', todoId],
  queryFn: async () => {
    const response = await fetch('/todos/' + todoId)
    if (!response.ok) {
      throw new Error('Network response was not ok')
    }
    return response.json()
  }
})
```

### options

데이터를 refetch 해주는 옵션들은 기본적으로 true로 설정되어 있기 때문에(retry는 3) 필요하지 않다면 false로 세팅해야 한다.

| option               | 설명                                                                           |
| :------------------- | :----------------------------------------------------------------------------- |
| refetchOnMount       | 데이터가 stale 상태일 경우 마운트 될 때마다 refetch 실행                       |
| refetchOnWindowFocus | 데이터가 stale 상태일 경우 윈도우 포커싱 될 때마다 refetch 실행                |
| refetchOnReconnect   | 데이터가 stale 상태일 경우 네트워크가 끊어졌다가 다시 연결된 경우 refetch 실행 |
| retry                | 쿼리 호출에 실패한 경우 refetch 실행                                           |
| enabled              | 쿼리 자동 실행 여부                                                            |
| initialData          | 쿼리 받아오기 전 초기 data                                                     |

## query hook 만들기 예시

```js
// usePost.js
import { useQuery } from '@tanstack/react-query'
import axios from 'axios'

const getPostById = async (postId) => {
  const { data } = await axios.get(
    `https://jsonplaceholder.typicode.com/posts/${postId}`
  )
  return data
}

export default function usePost(postId) {
  return useQuery({
    queryKey: ['post', postId],
    queryFn: () => getPostById(postId)
  })
}
```

```js
// App.js
import usePost from './hooks/usePost'

const { status, data, error, isFetching } = usePost(id)

return (
  <div>
    {status === 'loading' ? (
      'Loading...'
    ) : status === 'error' ? (
      <span>Error: {error.message}</span>
    ) : (
      <p>{data && data.title}</p>
    )}
  </div>
)
```

## 참고사이트

[useQuery](https://tanstack.com/query/v4/docs/react/reference/useQuery?from=reactQueryV3&original=https%3A%2F%2Freact-query-v3.tanstack.com%2Freference%2FuseQuery)
[My구독의 React Query 전환기](https://tech.kakao.com/2022/06/13/react-query/)<br/>
[tannerlinsley/react-query](https://codesandbox.io/s/45dqt?file=/src/index.js)<br/>
