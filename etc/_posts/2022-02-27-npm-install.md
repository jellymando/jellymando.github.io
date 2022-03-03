---
layout: post
title: "[npm install] dependencies와 devDependencies"
sitemap: false
---

{:toc .large-only}

## npm install

`npm install`의 동작은 크게 패키지 설치/의존성 설치로 나뉜다.

```js
npm install [package명]
```

패키지명을 명시해 특정 패키지를 설치

```js
npm install
```

`package.json` 파일의 의존성을 설치

## 패키지 설치 플래그

`npm install` 뒤에 `-D`와 같은 접미어(플래그)를 붙이면 프로젝트의 devDependencies 목록에 패키지가 추가된다.

`-P`는 `npm install [package명]`과 동일하기 때문에 보통 생략한다.

| 플래그        | 설명                                                       |
| :------------ | :--------------------------------------------------------- |
| -P (생략가능) | 패키지를 설치하고 프로젝트의 dependencies 목록에 추가      |
| -D            | 패키지를 설치하고 프로젝트의 devDependencies 목록에 추가   |
| -g (—global)  | 패키지를 프로젝트가 아닌 시스템의 node_modules 폴더에 설치 |

## dependencies와 devDependencies

```js
// package.json
{
  "devDependencies": {
    "concurrently": "^5.3.0"
  },
  "dependencies": {
    "express": "^4.17.1"
  }
}
```

- dependencies : express 패키지처럼 실제 코드에도 포함되며 앱 구동을 위해 필요한 의존성 파일들
- devDependencies : concurrently 패키지처럼 실제 코드에 포함되지 않으며 <u>개발 단계에만 필요한</u> 의존성 파일들

dependencies와 devDependencies로 의존성 목록을 구분하면 개발용과 실제 서비스용을 구분하기 쉬워진다.

`npm install -production`을 실행하면 devDependencies를 제외한 의존성만 내려받는다.

## -g

`-g` 플래그를 통해 패키지를 설치하면 시스템 폴더에 설치된다.

(Win10 기준으로는 (사용자명)\AppData\Roaming\npm\node_modules)

시스템의 node_modules 폴더 경로는 `npm root -g` 를 통해 찾을 수 있으며, 프로젝트의 package.json 의존성 목록에 기록되지 않는다.

## 참고사이트

[[Node.js] - npm install, 이제는 알고 쓰자](https://c17an.netlify.app/blog/node.js/npm-install-%EC%A0%95%EB%A6%AC/article/)
