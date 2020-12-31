---
layout: post
title: "[Express] html에서 로드할 수 있는 파일 경로 설정"
sitemap: false
---

{:toc .large-only}

## express.static

Express에서 이미지, CSS 파일 및 JavaScript 파일과 같은 정적 파일을 제공하려 한다.

public 폴더를 express.static 미들웨어 함수에 전달하면 폴더 속 파일을 제공할 수 있다.

```js
app.use(express.static("public"));
```

<br/>
/public 을 생략한 경로로 파일을 로드할 수 있다.

ex) /public/index.js => /index.js

```js
http://localhost:3000/images/kitten.jpg
http://localhost:3000/css/style.css
http://localhost:3000/js/app.js
http://localhost:3000/images/bg.png
http://localhost:3000/hello.html
```

<br/>
[html 파일에서 외부 js 파일 로드하기](https://infodbbase.tistory.com/41)<br/>
[Express에서 정적 파일 제공](https://expressjs.com/ko/starter/static-files.html)
