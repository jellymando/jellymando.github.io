---
title: "[error] 에러 해결 모음집☠"
categories: [Typescript]
tags: [typescript, error]
---

{:toc .large-only}

### 'never' 형식에 'focus' 속성이 없습니다.

```js
const inputRef = useRef<HTMLInputElement>(null);
if (inputRef.current) inputRef.current!.focus();
```

### 'Timeout' 형식은 'number' 형식에 할당할 수 없습니다.

```js
const timerRef: { current: NodeJS.Timeout | null } = useRef(null);
if (timerRef.current) clearTimeout(timerRef.current);
timerRef.current = setTimeout(() => {}, 300);
```

### 'EventTarget' 형식에 'value' 속성이 없습니다.

```js
{ target }: React.ChangeEvent<HTMLInputElement>
```
