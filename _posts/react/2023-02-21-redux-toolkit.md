---
title: 'Redux Toolkit + RTK 사용 방법'
categories: [REACT]
tags: [redux, redux toolkit]
---

{:toc .large-only}

## configureStore()

스토어를 구성하는 함수

reducer, middleware 등의 정보를 전달한다.

```js
import { configureStore } from '@reduxjs/toolkit'
import additionalMiddleware from 'additional-middleware'
import logger from 'redux-logger'
// @ts-ignore
import untypedMiddleware from 'untyped-middleware'
import rootReducer from './rootReducer'

export type RootState = ReturnType<typeof rootReducer>
const store = configureStore({
  reducer: rootReducer,
  middleware: (getDefaultMiddleware) =>
    getDefaultMiddleware()
      .prepend(
        // correctly typed middlewares can just be used
        additionalMiddleware,
        // you can also type middlewares manually
        untypedMiddleware as Middleware<
          (action: Action<'specialAction'>) => number,
          RootState
        >
      )
      // prepend and concat calls can be chained
      .concat(logger),
})

export type AppDispatch = typeof store.dispatch

export default store
```

## createApi()

api를 호출하여 데이터를 가져오고 변환하는 방법을 세팅하는 함수

baseUrl에 대하여 여러 endpoints를 세팅할 수 있다.

```js
// Need to use the React-specific entry point to allow generating React hooks
import { createApi, fetchBaseQuery } from '@reduxjs/toolkit/query/react'

// Define a service using a base URL and expected endpoints
export const pokemonApi = createApi({
  reducerPath: 'pokemonApi',
  baseQuery: fetchBaseQuery({ baseUrl: 'https://pokeapi.co/api/v2/' }),
  endpoints: (builder) => ({
    getPokemonByName: builder.query({
      query: (name) => `pokemon/${name}`
    })
  })
})

// Export hooks for usage in function components, which are
// auto-generated based on the defined endpoints
export const { useGetPokemonByNameQuery } = pokemonApi
```

### reducerPath

스토어에 저장될 유니크한 키 값

### baseQuery

endpoints에서 사용되는 기본 쿼리. fetchBaseQuery 유틸리티를 사용한다.

#### fetchBaseQuery

baseUrl, prepareHeaders 등의 매개변수를 받는다.

- baseUrl : api 요청 경로
- prepareHeaders : api 요청 헤더를 설정

```js
const baseQuery = fetchBaseQuery({
  baseUrl: '/',
  prepareHeaders: (headers, { getState }) => {
    const token = (getState() as RootState).auth.token

    // If we have a token set in state, let's assume that we should be passing it.
    if (token) {
      headers.set('authorization', `Bearer ${token}`)
    }

    return headers
  },
})
```

### endpoints

엔드포인트에 대한 설정을 할 수 있다.

```js
import { createApi, fetchBaseQuery } from '@reduxjs/toolkit/query/react'

const api = createApi({
  baseQuery: fetchBaseQuery({ baseUrl: '/' }),
  endpoints: (build) => ({
    //              ResultType  QueryArg
    //                    v       v
    getPost: build.query({
      // inferred as `number` from the `QueryArg` type
      //       v
      query: (id) => `post/${id}`,
      // An explicit type must be provided to the raw result that the query returns
      // when using `transformResponse`
      //                             v
      transformResponse: (rawResult, meta) => {
        //                                                        ^
        // The optional `meta` property is available based on the type for the `baseQuery` used

        // The return value for `transformResponse` must match `ResultType`
        return rawResult.result.post
      }
    })
  })
})
```

## RTK 쿼리 사용하기

### useQuery

api의 endpoint로 만든 쿼리를 rtk 훅을 사용하여 호출할 수 있다.

endpoint에 등록한 쿼리마다 각각 훅이 쿼리의 이름으로 네이밍되어 생성된다.

예를 들어, getPost라는 이름의 쿼리를 만들었다면 useGetPostQuery로 네이밍 된 훅을 사용할 수 있다.

```js
export const PostDetail = ({ id }: { id: string }) => {
  const {
    data: post,
    isFetching,
    isLoading
  } = useGetPostQuery(id, {
    pollingInterval: 3000,
    refetchOnMountOrArgChange: true,
    skip: false
  })

  if (isLoading) return <div>Loading...</div>
  if (!post) return <div>Missing post!</div>

  return (
    <div>
      {post.name} {isFetching ? '...refetching' : ''}
    </div>
  )
}
```

### useLazyQuery

쿼리를 바로 실행하지 않고 수동으로 트리거 할 떄 유용한 훅이다.

```js
const [trigger, result, lastPromiseInfo] = api.useLazyGetPostsQuery(options)
```

`useLazyGetPostsQuery` 에서 제공하는 배열의 첫 번째 인자인 trigger 함수로 쿼리를 호출할 수 있다.

#### 여러 쿼리에서 같은 캐시를 업데이트 하는 경우

만약 여러 쿼리가 같은 캐시를 업데이트하려면, 동일한 태그를 지정해야 한다.

예를 들어, getPrevTodos 쿼리와 getNextTodos 쿼리가 모두 todos 값을 업데이트 한다면, 다음과 같이 providesTags를 설정할 수 있다.

```js
const api = createApi({
  reducerPath: 'todosApi',
  baseQuery: fetchBaseQuery({ baseUrl: 'https://api.example.com' }),
  endpoints: (builder) => ({
    getPrevTodos: builder.query({
      query: () => '/todos/prev',
      providesTags: ['todos']
    }),
    getNextTodos: builder.query({
      query: () => '/todos/next',
      providesTags: ['todos']
    })
  })
})
```

#### 쿼리 데이터를 변형시키려 할 때 에러 발생

쿼리 데이터는 immutable 이기 때문에 속성을 변형시키려고 하면 read only라는 에러가 뜬다.

이때는 `Array.from()` 메서드를 사용하여 원본 배열을 writeable로 복사하여 사용한다.

## 참고사이트

[Redux Toolkit (리덕스 툴킷)은 정말 천덕꾸러기일까?](https://blog.hwahae.co.kr/all/tech/tech-tech/6946)
