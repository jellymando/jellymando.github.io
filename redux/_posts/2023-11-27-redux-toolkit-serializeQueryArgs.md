---
layout: post
title: '[Redux-toolkit] serializeQueryArgs/merge 사용하기'
sitemap: false
---

{:toc .large-only}

## merge

Redux Toolkit에서 쿼리를 호출할 때 기존 캐시와 새로 생성된 캐시를 병합할 수 있는 기능이다.

리스트 페이징, 무한 스크롤 등을 구현할 때 사용한다.

## serializeQueryArgs

쿼리의 캐시 키를 정의하는 메서드이다.

인수와 관계없이 키 값이 항상 같아야 하는 경우에는 endpointName를 반환한다.

```js
listItems: build.query({
  query: (pageNumber) => `/listItems?page=${pageNumber}`,
  // Only have one cache entry because the arg always maps to one string
  serializeQueryArgs: ({ endpointName }) => {
    return endpointName
  },
  // Always merge incoming data to the cache entry
  merge: (currentCache, newItems) => {
    currentCache.push(...newItems)
  }
})
```

이렇게 endpointName를 반환하면 키 값이 변하지 않으므로 쿼리를 새로 호출했을 때 생성된 캐시를 예전 캐시와 병합할 수 있다.

혹은 쿼리 인수를 반환하여 쿼리 인수 + 엔드포인트 이름의 조합으로 키를 정의할 수도 있다.

이 때 반환한 인수와 동일한 인수로 엔드포인트를 호출하면 동일한 캐시 키가 생성된다.

```js
getPost: build.query({
  queryFn: async ({ id, client }) => {
    const post = await client.fetchPost(id)
    return { data: post }
  },
  serializeQueryArgs: ({ queryArgs, endpointDefinition, endpointName }) => {
    const { id } = queryArgs
    // This can return a string, an object, a number, or a boolean.
    // If it returns an object, number or boolean, that value
    // will be serialized automatically via `defaultSerializeQueryArgs`
    return { id } // omit `client` from the cache key

    // Alternately, you can use `defaultSerializeQueryArgs` yourself:
    // return defaultSerializeQueryArgs({
    //   endpointName,
    //   queryArgs: { id },
    //   endpointDefinition
    // })
    // Or  create and return a string yourself:
    // return `getPost(${id})`
  }
})
```

위 예시에서는 id 인수를 반환하므로 id 값이 같으면 동일한 캐시를 사용할 수 있으며, id 값이 다르면 새로운 캐시를 생성한다.

또한 client 인수는 캐시 키에서 제외했으므로 client 값을 바꾸고 호출해도 새로운 캐시가 생성되지 않는다.

## 참고사이트

[serializeQueryArgs](https://redux-toolkit.js.org/rtk-query/api/createApi#serializequeryargs-1)
