---
title: "여러개의 DOM에 useRef 사용하기"
categories: [REACT]
tags: [react, useRef]
---

{:toc .large-only}

```js
tree.map(branch => <Branch name={branch.name} ref={??} />);
```

위 코드처럼 map으로 여러 DOM 요소를 생성할 때나 재귀 컴포넌트의 경우, Ref를 어떻게 생성해야 할까?

우선 useRef 변수를 생성하고 초기값을 빈 배열로 만든다.

```js
const elementRefs = useRef([] as HTMLDivElement[] | null[]);
```

그리고 요소에서 콜백 함수를 통해 배열에 ref를 추가한다.

```js
tree.map((branch, i) => (
  <Branch name={branch.name} ref={(el) => (elementRefs.current[i] = el)} />
));
```

이렇게 하면 배열의 인덱스에 각 요소의 ref가 들어간다.

요소는 배열 Ref의 current를 통해 접근할 수 있다.

ex) elementRefs.current[0];

```js
elementRefs.current.forEach((element) => console.log(element));
```

<br/>

[useRef로 여러개의 DOM제어하기](https://velog.io/@chaerin00/useRef%EB%A1%9C-%EC%97%AC%EB%9F%AC%EA%B0%9C%EC%9D%98-DOM%EC%A0%9C%EC%96%B4%ED%95%98%EA%B8%B0)
