---
title: "[tsconfig] 특정 파일 제외하기"
categories: [TYPESCRIPT]
tags: [typescript]
---

{:toc .large-only}

## Webpack 빌드할 때 특정 ts 파일 제외시키기

Webpack을 빌드하면서 jest test를 건너 뛰고 싶었다.

`tsconfig.json`의 `exclude` 속성을 추가하면 된다.

```js
    "include": ["src"],
    "exclude": ["**/*.test.ts", "**/*.test.tsx"]
```

<br/>

다시 빌드하면 `*.test.ts`, `*.test.tsx` 파일은 건너뛰고 빌드한다.

<br/>

[How to exclude files ending in '.spec.ts' in tsconfig.json](https://stackoverflow.com/questions/48449107/how-to-exclude-files-ending-in-spec-ts-in-tsconfig-json)<br/>
[Intro to the TSConfig Reference](https://www.typescriptlang.org/tsconfig#include)
