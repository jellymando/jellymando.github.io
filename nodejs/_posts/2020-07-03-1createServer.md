---
layout: post
title: "HTTP 모듈 (1: createServer)"
sitemap: false
---

{:toc .large-only}

## Node.js

비동기 이벤트 기반 JavaScript 런타임인 ​​Node.js는 확장 가능한 네트워크 애플리케이션을 빌드하도록 설계되었습니다.<br/>
HTTP는 TCP/IP를 기반으로 하는 프로토콜입니다.<br/>
Node.js에는 HTTP라는 내장 모듈이있어 Node.js가 HTTP (Hyper Text Transfer Protocol)를 통해 데이터를 전송할 수 있습니다.

```js
const http = require("http");

const hostname = "127.0.0.1";
const port = 3000;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader("Content-Type", "text/plain");
  res.end("Hello World");
});

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});
```

## server 객체

- http 모듈의 createServer() 메서드를 사용하면 server 객체를 생성할 수 있습니다.

| server 객체의 메서드      | 설명               |
| :------------------------ | :----------------- |
| listen(port[, callback])) | 서버를 실행합니다. |
| close()                   | 서버를 종료합니다. |

- server 객체는 EventEmitter 객체를 기반으로 만들어졌으므로 이벤트를 연결할 수 있습니다.

| server 객체의 이벤트 | 설명                                                             |
| :------------------- | :--------------------------------------------------------------- |
| request              | 클라이언트가 요청할 때 발생하는 이벤트입니다.                    |
| connection           | 클라이언트가 접속할 때 발생하는 이벤트입니다.                    |
| close                | 서버가 종료될 때 발생하는 이벤트입니다.                          |
| checkContinue        | 클라이언트가 지속적인 연결을 하고 있을 때 발생하는 이벤트입니다. |
| upgrade              | 클라이언트가 HTTP 업그레이드를 요청할 때 발생하는 이벤트입니다.  |
| clientError          | 클라이언트에서 오류가 발생할 때 발생하는 이벤트입니다.           |

```js
//모듈을 추출합니다.
var http = require("http");

//server 객체를 생성합니다.
var server = http.createServer();

//server 객체에 이벤트를 연결합니다.
server.on("request", function () {
  console.log("Request On");
});
server.on("connection", function () {
  console.log("Connection On");
});
server.on("close", function () {
  console.log("Close On");
});

//listen() 메서드를 실행합니다.
server.listen(1016);
```

## response 객체

- 클라이언트에 웹 페이지를 제공하기 위해 response 객체를 사용합니다.

response 객체는 request 이벤트 리스너의 두 번째 매개 변수로 전달되는 객체입니다.<br/>
HTTP 모듈을 포함하려면 다음 require() 메소드를 사용하십시오.

| response 객체의 메서드        | 설명                    |
| :---------------------------- | :---------------------- |
| writeHead(statusCode, object) | 응답 헤더를 작성합니다. |
| end([data], [encoding])       | 응답 본문을 작성합니다. |

```js
require("http")
  .createServer(function (request, response) {
    //웹 서버를 생성하고 모듈을 추출합니다.
    response.setHeader("Content-Type", "text/html");
    response.writeHead(200, { "Content-Type": "text/html" });
    //writeHead는 한 번만 호출되어야 하며 end()가 호출되기 전에 호출되어야 함. 상태 코드는 404와 같은 3자리 HTTP 상태 코드입니다.
    response.write();
    //이것은 응답 본문의 청크를 보냅니다. 이 방법은 신체의 연속적인 부분을 제공하기 위해 여러 번 호출 될 수 있습니다.
    response.end("<h1>Hello Web Server with Node.js</h1>");
    //데이터가 로드되었음을 서버에 알림
  })
  .listen(1016, function () {
    //웹 서버를 실행합니다.
    console.log("Server Running at localhost:1016");
  });
```

헤더가 setHeader로 설정되면 헤더는 writeHead로 전달된 모든 헤더와 병합되며, 헤더는 writeHead로 우선 순위가 지정됩니다.
writeHead가 호출되고 setHeader가 호출되지 않은 경우, 내부적으로 캐싱하지 않고 제공된 헤더 값을 네트워크 채널에 직접 쓰며, 헤더의 getHeader는 예상 결과를 산출하지 못합니다.
향후 검색 및 수정 가능성이 있는 경우 response.setHeader()를 사용합니다.
{:.note}

### 참고사이트

[https://www.w3schools.com/nodejs/nodejs_http.asp](https://www.w3schools.com/nodejs/nodejs_http.asp)
[http://zetcode.com/javascript/http/](http://zetcode.com/javascript/http/)
