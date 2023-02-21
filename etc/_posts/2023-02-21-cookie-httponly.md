---
layout: post
title: '쿠키의 httpOnly 옵션'
sitemap: false
---

{:toc .large-only}

## httpOnly

httpOnly 옵션은 웹서버에서 Set-Cookie 헤더를 이용해 쿠키를 설정할 때 지정할 수 있다.

이 옵션은 **자바스크립트 같은 클라이언트 측 스크립트가 쿠키를 사용할 수 없게** 한다.

httpOnly 옵션이 설정된 쿠키는 document.cookie로 쿠키 정보를 읽을 수 없기 때문에 쿠키를 보호할 수 있다.

자바스크립트로 헤더에 쿠키값을 보내는 게 안된다면 서버에서 쿠키를 세팅할 때 httpOnly 옵션을 사용했을 가능성이 있다.

## 참고사이트

[httpOnly](https://ko.javascript.info/cookie#ref-679)<br/>
[[Web] HTTP Only와 Secure Cookie 이해하기](https://nsinc.tistory.com/121)
