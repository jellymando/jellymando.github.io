---
title: "Node Express 설치 및 html 라우팅하기🔥"
categories: [Node]
tags: [node, express]
---

{:toc .large-only}

## Express 설치

```js
npm install express --save
```

> [Express를 임시로 설치하고 종속 항목 목록에 추가하지 않으려면, 다음과 같이 --save 옵션을 생략하십시오.](https://expressjs.com/ko/starter/installing.html)

## Express 서버 생성

```js
// server.js
var express = require("express");
var app = express();
var server = app.listen(3000, function () {
  console.log("Express server has started on port 3000");
});
```

## Router 생성

라우팅은 애플리케이션 엔드 포인트(URI)의 정의, 그리고 URI가 클라이언트 요청에 응답하는 방식을 말합니다.

#### 기본적인 라우트의 모습

```js
app.get("/", function (req, res) {
  res.send("Hello World!");
});
```

<br/>
라우팅할 html 파일을 생성합니다.

```js
<!DOCTYPE html>
<html>
<head>
<title>Page Title</title>
</head>
<body>

<h1>This is a Heading</h1>
<p>This is a paragraph.</p>

</body>
</html>
```

<br/>
router 폴더를 만들고 그 안에 main.js를 생성합니다.

```js
module.exports = function (app) {
  app.get("/", function (req, res) {
    res.render("index.html");
  });
};
```

## body-parser 설치

```js
npm install body-parser
```

```js
const bodyParser = require("body-parser");
app.use(bodyParser.urlencoded({ extended: true }));
app.use(bodyParser.json());
```

## ejs 설치

```js
npm install ejs
```

## server.js 업데이트

```js
// 라우터 모듈인 main.js를 불러와서 app 에 전달해줍니다.
var router = require("./router/main")(app);

// 서버가 읽을 수 있도록 html 파일의 위치를 정의해줍니다.
app.set("views", __dirname + "/");

// 서버가 html을 렌더링 할 때, ejs 엔진을 사용하도록 설정합니다.
app.set("view engine", "ejs");
app.engine("html", require("ejs").renderFile);
```

#### 최종 server.js

```js
var express = require("express");
var app = express();
var router = require("./router/main")(app);

const bodyParser = require("body-parser");
app.use(bodyParser.urlencoded({ extended: true }));
app.use(bodyParser.json());

app.set("views", __dirname + "/views");
app.set("view engine", "ejs");
app.engine("html", require("ejs").renderFile);

var server = app.listen(3000, function () {
  console.log("Express server has started on port 3000");
});
```
