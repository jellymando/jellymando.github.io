---
layout: post
title: "ForwardRef 사용할 때 발생하는 에러 (형식에 'current' 속성이 없습니다.)"
sitemap: false
---

{:toc .large-only}

## 에러

React에서 ref를 props로 전달하기 위해 forwardRef를 사용하면 "형식에 'current' 속성이 없습니다." 라는 에러가 발생했다.

```js
const Nav = forwardRef<HTMLVideoElement | null>((props, ref) => {
  const handleScreenShare = useCallback(() => {
        if (videoRef!.current) startScreenShare(videoRef!.current);
  }, []);
...
```

current 속성을 넣으면 해결될까 했지만 이걸로도 해결되지 않았다.

```js
const Nav = forwardRef<{current: HTMLVideoElement | null}>((props, ref) => {
  const handleScreenShare = useCallback(() => {
        if (videoRef!.current) startScreenShare(videoRef!.current);
  }, []);
...
```

## 해결

에러가 발생하는 원인은 ref의 타입이 무조건 current 속성이 있는 객체가 아니라 함수일수도 있기 떄문이다.

따라서 아래처럼 함수인 경우에 예외처리를 해주면 정상적으로 해결된다.

```js
const Nav = forwardRef<HTMLVideoElement | null>((props, ref) => {
  const handleScreenShare = useCallback(() => {
        if (typeof ref !== 'function') return

        if (videoRef!.current) startScreenShare(videoRef!.current);
  }, []);
...
```

## 참고사이트

[using ref.current in React.forwardRef](https://stackoverflow.com/a/62238917)
