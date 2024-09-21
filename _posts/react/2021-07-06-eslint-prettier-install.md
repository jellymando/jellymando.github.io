---
title: "React에 ESLint와 Prettier 끼얹기"
categories: [React]
tags: [react, eslint, prettier]
---

{:toc .large-only}

## 하면 편하지만 하기가 번거로운 그 과정.. ESLint와 Prettier 끼얹기

### ESLint 설치

```js
npm i -D eslint
```

### .eslintrc.js 파일 생성

```js
npx eslint --init
```

위 명령어를 실행하면 여러 선택사항이 나온다.

프로젝트의 개발 환경에 맞춰 선택하면 된다.

### Prettier 설치

```js
npm i -D prettier
```

### ESLint와 Prettier가 서로 충돌이 되지 않도록 나머지 모듈 설치

```js
npm i -D eslint-config-prettier eslint-plugin-prettier
```

### .eslintrc.js 파일 설정

처음 eslint를 설치하면 코드에 빨간줄이 생긴다.

빨간줄의 원인에 따라 `.eslintrc.js` 파일의 `rules` 속성에 옵션을 추가한다.

아래는 내가 떴던 오류들(props 유효성 검사, function에서 parameter를 사용하지 않을 때)을 해결하기 위해 추가한 옵션이다.

```js
rules: {
    "react/prop-types": "off",
    "no-unused-vars": 0,
  },
```

### .prettierrc 파일 추가

`.eslintrc.js` 경로에 `.prettierrc` 파일을 추가한 후 내용을 작성한다.

내가 보통 쓰는 설정값은

```js
{
  "trailingComma": "es5",
  "semi": true,
  "singleQuote": true,
  "tabWidth": 4,
  "printWidth": 120
}
```

<br/>

[VSCode에서 ESLint와 Prettier (+ TypeScript) 사용하기](https://velog.io/@das01063/VSCode%EC%97%90%EC%84%9C-ESLint%EC%99%80-Prettier-TypeScript-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0)
