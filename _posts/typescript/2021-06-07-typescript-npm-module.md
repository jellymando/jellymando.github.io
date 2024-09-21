---
title: "Typescript NPM 모듈 만들기"
categories: [TYPESCRIPT]
tags: [typescript]
---

{:toc .large-only}

### tsconfig 설정

```js
{
  "compilerOptions": {
    "target": "es5",
    "module": "commonjs",
    "declaration": true,
    "outDir": "./dist",
    "strict": true
  }
}
```

기존 tsconfig 설정에 `"declaration": true` 와 `"outDir": "./dist"` 를 추가하였다.

> `"declaration": true` : 상응하는 ‘d.ts’ 파일 생성
> `"outDir": "./dist"` : 결과물을 저장 할 디렉토리 설정

### webpack.config 설정

기존 설정에서 html 파일을 빌드하는 코드를 삭제하였다.

### package.json 설정

```js
"main": "dist/index.js",
"types": "dist/index.d.ts",
```

기존 설정에서 main이 index.js를 바라보게 수정하였고, types를 추가하였다.

<br/>

```js
output: {
    path: resolve(__dirname, "dist"),
    filename: "index.js",
    libraryTarget: "umd",
  },
```

output에 `libraryTarget: "umd"`를 추가하였다.

> libraryTarget을 umd로 설정하면 모듈은 `<script>` 로드 뿐만 아니라 모든 방식의 로더에서 사용할 수 있다.
> 위 설정을 추가하지 않았을 때 해당 모듈을 사용하면 class가 빈 객체로 들어온다. (~ is not a constructor 에러)

### npm 로그인

```js
npm login
```

로그인이 정상적으로 되었는지 확인은 아래 명령어로 확인 할 수 있다.

```js
npm whoami
```

### npm 배포하기

배포하기 전 package.json 에서 패키지 명 등을 마지막으로 체크해보자!

```js
npm publish
```

정상적으로 배포가 된다면 NPM Packages에 패키지가 업로드 되었을 것이다.

> 배포된 패키지는 72시간이 지나면 삭제할 수 없으니 불필요한 패키지라면 미리 삭제하자.
> npm unpublish PACKAGE_NAME -f

[빠르게 배우는 NPM 패키지 생성부터 배포까지 완벽 가이드](https://kdydesign.github.io/2020/08/28/npm-tutorial/)<br/>
[[번역] TypeScript로 NPM 모듈을 만들어 배포하기](https://blog.ull.im/engineering/2018/12/23/how-to-create-and-publish-npm-module-in-typescript.html)
