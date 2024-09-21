---
title: "[Error] can't resolve 'fs'"
categories: [NEXTJS]
tags: [nextjs, error]
---

{:toc .large-only}

## mongoose 스키마의 다양한 속성

dotenv 모듈을 import 하는 중에 can't resolve 'fs' 에러가 발생했다.

webpack에서 node 모듈에 대한 폴리파일을 포함하지 않아서 발생하는 에러라고 한다.

next.config.js에 아래 코드를 추가하여 해결했다.

```js
webpack(config) {
    config.resolve.fallback = {
      ...config.resolve.fallback,
      fs: false,
    };

    return config;
  }
```

<br/>

[Module not found: Can't resolve 'fs' - NextJS](https://stackoverflow.com/a/67478653)
