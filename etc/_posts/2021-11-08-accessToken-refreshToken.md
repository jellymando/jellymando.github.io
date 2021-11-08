---
layout: post
title: "Access Token과 Sliding Sessions, Refresh Token"
sitemap: false
---

{:toc .large-only}

## 토근 기반 인증

HTTP의 Connectionless, Stateless 특성 때문에 세션을 이용한 서버 인증 방식을 주로 사용된다.

하지만 서버를 통한 인증 방식은 저장해야 하는 세션의 수가 많아지면 서버에 과부하가 발생될 수 있다.

토큰을 사용한 인증 방식은 서버측에 데이터를 담아두지 않는다.

서버에서 발급받은 AccessToken을 클라이언트측에 저장하고, 서버로 보내는 HTTP의 요청 헤더의 Authorization 값에 토큰을 포함시켜 전달한다.

ex) [아임포트 Access Token 사용법](https://docs.iamport.kr/tech/access-token)

## JWT

- JWT은 Json Web Token의 약자로 웹표준 방식이다.

- 자가수용적(self-contained) 방식으로 필요한 정보를 자체적으로 지니고 있다.

- 두 개체에서 JSON 객체를 사용하여 데이터를 전달한다.

- HTTP 요청 헤더나 URL 파라미터로 전달할 수 있다.

- 토큰이 검증되었다는 것을 증명해주는 signature를 포함한다.

## AccessToken의 만료 기한

JWT는 토큰의 만료 기한을 설정할 수 있다.

만료 기한을 짧게 설정하면 토큰이 탈취되더라도 빠르게 만료되어 보안성은 높아지지만, 자주 로그인해야 하며 글을 작성하는 등의 사용자 행위 중에 토큰이 만료될 수 있다.

반면 만료 기한을 길게 설정하면 토큰이 탈취되었을 때 만료되기 전까지 기한 제약이 없어 보안성이 떨어진다.

## Access Token과 Sliding Sessions

세션을 지속적으로 이용하는 유저에게 자동으로 만료 기한을 연장시켜주는 방법이다.

주로 유효한 AccessToken을 가진 클라이언트의 요청에 대해 서버가 새로운 AccessToken을 발급하는 방식을 사용한다.

글쓰기, 장바구니, 결제 등의 서비스를 이용할 때 중간에 토큰이 만료되지 않도록 특정 페이지에 접속할 때 또는 클라이언트가 토큰의 iat(토큰 발급 시간)를 참조해 새로운 토큰을 받아올 수 있다.

슬라이딩 세션을 활용하면 AccessToken 방식의 만료 기한과 관련된 단점을 보완할 수 있다.

## Access Token과 Refresh Token

AccessToken과 RefreshToken을 함께 발급하는 방법이다.

주로 AccessToken은 1시간 내외, RefreshToken은 2주에서 한달 정도의 만료 기간을 부여한다.

AccessToken이 만료되면 RefreshToken을 이용하여 AccessToken 재발급을 요청한다.

AccessToken은 서버에 따로 저장해 둘 필요가 없지만, RefreshToken의 경우 서버에 저장해야 한다.

RefreshToken를 사용하면 I/O 작업이 필요하며, 이는 I/O 작업이 필요없는 JWT의 장점에 상반된다.

## 참고사이트

[Refresh Token과 Sliding Sessions를 활용한 JWT의 보안 전략](https://blog.ull.im/engineering/2019/02/07/jwt-strategy.html)<br/>
[Secure JWT and Slinding Sessions](https://www.hahwul.com/2021/05/05/sliding-sessions/)<br/>
[[JWT] 토큰(Token) 기반 인증에 대한 소개](https://velopert.com/2350)<br/>
[[Node.js / JWT] Express.js 서버에서 JWT 기반 회원인증 시스템 구현하기](https://velopert.com/2448)
