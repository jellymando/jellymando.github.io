---
title: "CRA에서 build 시 .d.ts 파일 생성 안됨"
categories: [Typescript]
tags: [typescript]
---

{:toc .large-only}

CRA에서 build를 진행하는데 `.d.ts` 파일이 생성되지 않았다.

`tsconfig.json`에서 declaration, emitDeclarationOnly, outDir 설정해도 마찬가지..

`tsconfig.json`에 있는 baseUrl이나 include 다 잘 적용되는데..

build 할 때 tsconfig.json을 컴파일해주니 `.d.ts` 파일이 정상적으로 생성됐다.

```js
"build": "react-app-rewired build && tsc --project tsconfig.json"
```

## 참고사이트

[Creating .d.ts Files from .js files](https://www.typescriptlang.org/docs/handbook/declaration-files/dts-from-js.html)<br/>
[tsc CLI Options](https://www.typescriptlang.org/docs/handbook/compiler-options.html#handbook-content)<br/>
[error TS6231: Could not resolve the path '' with the extensions: '.ts', '.tsx', '.d.ts'](https://stackoverflow.com/a/71362909)
