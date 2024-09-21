---
title: '[Redux-toolkit] interseptor 적용하기'
categories: [React]
tags: [redux, redux toolkit]
---

{:toc .large-only}

## interseptor

interseptor를 통해 api 응답에 대해 공통으로 처리하는 로직을 적용할 수 있다.

RTK에서 interseptor를 적용하는 방법에는 크게 2가지가 있다.

### baseQuery

커스텀 baseQuery를 생성하여 createApi에 적용한다.

쿼리를 직접 호출하여 응답값을 얻을 수 있다.

```js
import { createApi, fetchBaseQuery } from '@reduxjs/toolkit/query'
import { request, gql, ClientError } from 'graphql-request'
import { tokenReceived, loggedOut } from './authSlice'

const baseQuery = fetchBaseQuery({ baseUrl: '/' })

const baseQueryWithReauth = async (args, api, extraOptions) => {
  let result = await baseQuery(args, api, extraOptions)
  if (result.error && result.error.status === 401) {
    // try to get a new token
    const refreshResult = await baseQuery('/refreshToken', api, extraOptions)
    if (refreshResult.data) {
      // store the new token
      api.dispatch(tokenReceived(refreshResult.data))
      // retry the initial query
      result = await baseQuery(args, api, extraOptions)
    } else {
      api.dispatch(loggedOut())
    }
  }
  return result
}

export const api = createApi({
  baseQuery: baseQueryWithReauth
})
```

### middleware

커스텀 미들웨어를 생성하여 configureStore에 적용한다.

`action.payload`로 응답값을 얻을 수 있다.

```js
import { configureStore, getDefaultMiddleware } from '@reduxjs/toolkit'

const customMiddleware = (store) => (next) => (action) => {
  if (action.type.endsWith('fulfilled')) {
    // Perform common logic on fulfilled actions (API responses)
    const response = action.payload
    // Modify the response if needed
    // For example, handle errors or manipulate data
    if (!response.success) {
      // Handle error response
      console.error('API request failed:', response.error)
      // Dispatch an error action or perform error handling logic
    }
  }
  return next(action)
}

const store = configureStore({
  middleware: (getDefaultMiddleware) =>
    getDefaultMiddleware().concat(customMiddleware)
})
```

## 참고사이트

[Automatic re-authorization by extending fetchBaseQuery](https://redux-toolkit.js.org/rtk-query/usage/customizing-queries#automatic-re-authorization-by-extending-fetchbasequery)</br>
[230118 항해99 73일차 RTK Query Axios interceptor처럼 쓰기](https://velog.io/@heayounchoi/230118-%ED%95%AD%ED%95%B499-73%EC%9D%BC%EC%B0%A8-RTK-Query-Axios-interceptor%EC%B2%98%EB%9F%BC-%EC%93%B0%EA%B8%B0)</br>
[Writing Custom Middleware](https://redux.js.org/usage/writing-custom-middleware)
