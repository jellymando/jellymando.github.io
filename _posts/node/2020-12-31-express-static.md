---
title: "[Express] html에서 로드할 수 있는 파일 경로 설정"
categories: [Node]
tags: [node, express]
---

{:toc .large-only}

## express.static

Express에서 이미지, CSS 파일 및 JavaScript 파일과 같은 정적 파일을 제공하려 한다.

public 폴더를 express.static 미들웨어 함수에 전달하면 디렉토리의 절대 경로를 사용하여 폴더 속 파일을 제공할 수 있다.

```js
app.use("/static", express.static(__dirname + "/public"));
```

<br/>
이제 /static 경로 접두부를 통해 public 디렉토리에 포함된 파일을 로드할 수 있다.

```js
http://localhost:3000/static/images/kitten.jpg
http://localhost:3000/static/css/style.css
http://localhost:3000/static/js/app.js
http://localhost:3000/static/images/bg.png
http://localhost:3000/static/hello.html
```

```js
<script src="/static/js/script.js"></script>
```

<br/>
[html 파일에서 외부 js 파일 로드하기](https://infodbbase.tistory.com/41)<br/>
[Express에서 정적 파일 제공](https://expressjs.com/ko/starter/static-files.html)
