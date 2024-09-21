---
title: "context로 storage 값을 사용하는데 값이 초기화되지 않을 때"
categories: [React]
tags: [react]
---

{:toc .large-only}

context를 사용해서 상태 관리를 할 때 storage에서 상태 값을 가져오는 경우, 맨 처음 storage에서 가져온 값은 새로고침 할 때까지 바뀌지 않는다.

Provider 부분에서 state를 수정해야 한다.

```js
const getStateName = () => {
  return storage.get("");
};

const [state, dispatch] = useReducer( , {
  ...state,
  stateName: getStateName(),
});
```
