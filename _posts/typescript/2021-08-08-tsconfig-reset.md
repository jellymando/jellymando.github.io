---
title: "[error] 앱 실행 시 tsconfig.json 자동 수정됨"
categories: [Typescript]
tags: [typescript, error]
---

{:toc .large-only}

타입스크립트로 리팩토링 하던 도중, `yarn start`로 앱을 실행하면 `tsconfig.json` 파일이 자동으로 수정되어버림;

타입스크립트 사용 버전을 workspace로 바꿔도 동일 현상 지속.

가장 바깥 경로에 `.env` 파일을 생성하고 아래 코드 추가 후 저장해도 똑같음.

```js
DISABLE_NEW_JSX_TRANSFORM: true;
```

<br/>

결국 `tsconfig.json` 바뀌게 냅두고 `@types/react` 인스톨.

```js
npm i --save-dev @types/react
```

<br/>

[tsconfig.json gets overwritten the moment the CRA typescript project is closed and opened in VSCode](https://github.com/facebook/create-react-app/issues/10178#issuecomment-737346917)<br/>
[Cannot use JSX unless the '--jsx' flag is provided.ts(17004)](https://chinsun9.github.io/tags/tsconfig/)
