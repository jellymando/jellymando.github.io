---
title: "HTTP 모듈 (3: 데이터 추출과 쿠키 추출)"
categories: [Node]
tags: [node]
---

{:toc .large-only}

## 데이터 추출

```js
<!DOCTYPE html>
<html>
<head>
<title>Page Title</title>
</head>
<body>

<h1>Send Data With POST Method</h1>
<form method="post">
    <table>
        <tr>
            <td><label>Data A</label></td>
            <td><input type="text" name="data_a"></td>
        </tr>
        <tr>
            <td><label>Data B</label></td>
            <td><input type="text" name="data_b"></td>
        </tr>
    </table>
    <input type="submit"/>
</form>

</body>
</html>
require('http').createServer(function(request, response) {
   if (request.method == 'GET') {
       //GET 요청
       require('fs').readFile('post.html', function(error, data){
           response.writeHead(200, {'Content-Type': 'text/html'});
           response.end(data);
       });
   }else if (request.method == 'POST') {
       //POST 요청
       request.on('data', function(data){
           response.writeHead(200, {'Content-Type': 'text/html'});
           response.end('<h1>' + data + '</h1>');
       });
   }
}).listen(1016, function(){
    console.log('Server Running at localhost:1016');
});
```

<br/>
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbxBta6%2FbtqGARhr0gu%2FALkcQyxTh9RN5hfxkDAK5K%2Fimg.png">

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FyDB6A%2FbtqGAbgJY9m%2FeEno0qhvrmikz0NBUhHMZk%2Fimg.png">

## 쿠키 추출

```js
require("http")
  .createServer(function (request, response) {
    //쿠키를 추출하고 분해합니다.
    var cookie = request.headers.cookie;
    cookie = cookie.split(";").map(function (el) {
      var el = el.split("=");
      return {
        key: el[0],
        value: el[1],
      };
    });

    //쿠키를 생성합니다.
    response.writeHead(200, {
      "Content-Type": "text/html",
      "Set-Cookie": ["name = dain", "age = 30"],
    });

    //응답합니다.
    response.end("<h1>" + JSON.stringify(cookie) + "</h1>");
  })
  .listen(1016, function () {
    console.log("Server Running at localhost:1016");
  });
```

<br/>
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbvpApm%2FbtqGxmJ0ZQE%2FByGY0BqRnL4JjA4toTw9XK%2Fimg.png">
