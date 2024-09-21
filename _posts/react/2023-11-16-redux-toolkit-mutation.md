---
title: '[Redux-toolkit] Matation 사용하기'
categories: [REACT]
tags: [redux, redux toolkit]
---

{:toc .large-only}

## Matation

Matation은 일반 Query와 달리 쿼리의 캐시 데이터를 변경시킬 수 있는 기능이다.

단순한 get 요청이 아니라 서버의 데이터를 변형해야 하는 경우 사용한다.

endpoints에서 `build.mutation()` 메서드로 정의한다.

```js
updatePost: build.mutation({
  query: ({ id, ...patch }) => ({
    url: `post/${id}`,
    method: 'PATCH',
    body: patch
  })
})
```

## invalidatesTags

Redux-toolkit에서는 엔드포인트마다 태그를 지정할 수 있다.

일반적으로 put, delete 등의 메서드를 호출하여 서버의 데이터를 업데이트 한 경우, get 메서드를 호출하여 변경된 데이터를 가져와서 화면에 보여줘야 한다.

`invalidatesTags`를 사용하면 해당 태그의 캐시를 삭제하고 이 태그를 구독하고 있는 쿼리를 자동으로 호출한다.

```js
 getPosts: build.query({
    query: () => '/posts',
    providesTags: ['Post']
}),
addPost: build.mutation({
    query: (body) => ({
        url: 'post',
        method: 'POST',
        body
    }),
    invalidatesTags: ['Post']
}),
```

위 예제에서는 addPost Mutation을 호출하면 Post 태그의 캐시를 삭제하고, Post 태그를 구독하고 있는 getPosts 쿼리가 실행되어 새로운 posts 데이터를 불러온다.

## invalidatesTags 사용 시 주의사항

주의할 점은 Mutation 호출이 실패해도 태그의 캐시는 삭제되고, 구독 쿼리가 실행된다는 것이다.

invalidatesTags의 매개변수로 Mutaion 호출이 성공했을 때만 태그의 캐시를 삭제하도록 조건을 걸 수 있다.

result 값이 있으면, 즉 호출에 성공하면 태그를 삭제하고, 아닌 경우 삭제하지 않도록 처리해준다.

이 때, 결과값은 반드시 배열(`[]`)이어야 하며, 아닌 경우 에러나 난다.

```js
updatePost: build.mutation({
  query: ({ gameGroup }) => ({
    url: `/posts`,
    method: 'PUT'
  }),
  invalidatesTags: (result) => (result ? ['POSTS'] : [])
})
```

## 참고사이트

[Mutations](https://redux-toolkit.js.org/rtk-query/usage/mutations)<br/>
[Invalidating cache data](https://redux-toolkit.js.org/rtk-query/usage/automated-refetching#invalidating-cache-data)
