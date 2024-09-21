---
title: "[react-use] useUpdateEffect Hook"
categories: [React]
tags: [react, useUpdateEffect]
---

{:toc .large-only}

### `useUpdateEffect`

첫 번째 호출은 무시하고 이후에 실행, 나머지는 `useEffect`와 동일

두 번째 인자로 상태값을 넣어봤다.

첫 렌더링 시에는 아예 호출되지 않는다.

이후 이벤트나 함수를 통해 상태값을 변경한 후에야 실행된다.

원래 사용 목적은 처음에 context의 상태값을 가져올 때 초기값인 `0`이 넘어오는 것을 건너뛰려는 목적이었지만, 이러한 용도에는 걸맞지 않다는 걸 깨달았다.

`drawOn` 같은 이벤트 관련 상태에 사용하기 좋을 것 같다.

<br/>

[useUpdateEffect](https://github.com/streamich/react-use/blob/master/docs/useUpdateEffect.md)
