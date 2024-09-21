---
title: "local ip로 node server 구동하기 (맥북)"
categories: [ETC]
tags: [node]
---

{:toc .large-only}

### 문제점

네트워크 환경설정에 나오는 IP(IPv4 주소)로 server를 구동하면 페이지가 뜨지 않는다.

### 해결법

gateway 주소로 서버를 돌려야 한다.

터미널에 아래 코드를 치면 gateway 주소를 얻을 수 있다.

```js
ifconfig | grep inet
```

```js
app.listen(3000, "10.0.0.0");
```

<br/>

[외부 ip에서 local 서버 접속](https://10000sukk.tistory.com/23)
