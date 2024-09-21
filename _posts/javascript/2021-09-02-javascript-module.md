---
title: "JavaScript module export & import"
categories: [Javascript]
tags: [javascript, module]
---

{:toc .large-only}

## JavaScript module

- ~~IE를 제외한~~ 최신 브라우저에서 기본적으로 모듈 기능을 지원

## 구조

- `module.js`에서 변수나 함수를 export

- `main.js`에서 module을 import

- `index.html`에서 `main.js`를 module 타입으로 참조

## 예시

### module.js

```js
export default function module(text) {
  return console.log(text);
}
```

### main.js

```js
import module from "./module.js";

module("TEST");
```

### index.html

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Page Title</title>
  </head>
  <body>
    <h1>This is a Heading</h1>
    <p>This is a paragraph.</p>

    <script src="./main.js" type="module"></script>
  </body>
</html>
```

## 에러

#### 1. `index.html` 파일을 열면 CORS 에러가 난다.

`Access to script at '~/main.js' from origin 'null' has been blocked by CORS policy: Cross origin requests are only supported for protocol schemes: http, data, chrome, chrome-extension, chrome-untrusted, https.`

type을 module로 설정한 `<script>` 태그가 포함된 HTML 파일을 로컬에서 로드할 경우 자바스크립트 모듈 보안 요구사항으로 인해 CORS 오류가 발생한다. [(참고)](https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Modules#other_differences_between_modules_and_standard_scripts)
따라서 node나 VSCode Go Live 확장 프로그램으로 html 파일을 로컬 서버에서 실행시켜야 한다.

#### 2. net::ERR_ABORTED 404 (Not Found) 에러

`index.html`에서 `main.js` 파일을 찾지 못한다.

`<script src="./main.js" type="module"></script>`

`index.html` 앞에 `./` 을 붙여 경로를 수정해줘야 한다.

#### 3. **또** net::ERR_ABORTED 404 (Not Found) 에러

이번엔 `index.js`에서 `module.js`를 찾지 못한다.

import 할 때 `.js` 확장자까지 붙여줘야 한다.

```js
import module from "./module.js";
```

## 참고사이트

[JavaScript modules](https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Modules)<br/>
[로컬에서 CORS policy 관련 에러가 발생하는 이유](https://velog.io/@takeknowledge/%EB%A1%9C%EC%BB%AC%EC%97%90%EC%84%9C-CORS-policy-%EA%B4%80%EB%A0%A8-%EC%97%90%EB%9F%AC%EA%B0%80-%EB%B0%9C%EC%83%9D%ED%95%98%EB%8A%94-%EC%9D%B4%EC%9C%A0-3gk4gyhreu)<br/>
[[JS] net::ERR_ABORTED 404 (Not Found) 에러](https://heeyamsec.tistory.com/36)
