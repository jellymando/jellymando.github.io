---
layout: post
title: "[npm-run-all] npm scripts 여러개 실행하기"
sitemap: false
---

{:toc .large-only}

### 설치

`package.json`에 있는 여러 npm scripts를 한번에 실행하기 위해 `npm-run-all` 모듈을 설치했다.

```js
yarn add npm-run-all --dev
```

### run-p / run-s

npm-scripts를 동시에 실행하는지, 순서를 보장하여 실행할지 결정할 수 있다.

- `run-p`

  - `npm-run-all -p` 의 약어
  - 주어진 npm-scripts를 <u>병렬로</u> 실행

- `run-s`
  - `npm-run-all -s` 의 약어
  - 주어진 npm-scripts를 <u>순차적으로</u> 실행

### 사용

```js
 "scripts": {
    "start": "npm-run-all -p start:server start:app",
    "start:app": "react-scripts start",
    "start:server": "node ./src/server/index.js",
 }
```

<br/>

혹은

```js
 "scripts": {
    "start": "run-p start:server start:app",
    "start:app": "react-scripts start",
    "start:server": "node ./src/server/index.js",
 }
```

<br/>

`yarn start` 하면 `start:app` 과 `start:server` 가 같이 실행된다.

<br/>

[React or javacript npm-run-all 으로 npm 스크립트 여러개 실행하는 방법](https://xxxxersuy.com/2)
