---
layout: post
title: "node로 .ts 파일 실행시키기"
sitemap: false
---

{:toc .large-only}

node로 .ts 파일을 실행시키면 "syntaxerror: unexpected identifier" 가 발생하였다.

babel-node도 설치해보고 tsconfig도 수정해봤지만 소용x

ts 파일을 node로 실행하려면 ts-node 모듈을 설치해야 한다.

ts-node는 메모리 상에서 티입스크립트를 transpile 하여 바로 실행할 수 있게 해준다.

```js
npm install -D ts-node
```

그리고 package.json에서 스크립트로 등록해주면 ts-node를 바로 사용할 수 있다.

```js
"scripts": {
    "start": "ts-node src/index.ts",
}
```

[Nodejs 에서 타입스크립트(Typescript) 사용하기](http://cosmiclatte.co.kr/nodejs-%EC%97%90%EC%84%9C-%ED%83%80%EC%9E%85%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8typescript-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0/)<br/>
[ts-node](https://www.npmjs.com/package/ts-node)
