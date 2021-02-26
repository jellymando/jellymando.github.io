---
layout: post
title: "Ref.current가 null로 나와요!"
sitemap: false
---

{:toc .large-only}

```js
useEffect(() => {
  if (Ref && Ref.current) {
    console.log("ref", Ref.current);
  }
}, [Ref]);
```

원래 위와 같이 하는 게 맞다.

그런데 Ref.current가 null로 나오는 것은 Ref가 제대로 업데이트 되지 않아서이다.

현재 문제에서는 Ref.current를 호출하는 컴포넌트가 부모, 실제 Ref Elment가 있는 컴포넌트가 자식이었다.

Ref.current를 호출하는 useEffect를 자식 컴포넌트로 옮기니 잘 돌아갔다.

<br/>
[참고사이트](https://stackoverflow.com/questions/56541342/react-hooks-why-is-current-null-for-useref-hook)
