---
layout: post
title: "Domain Sharding이란?"
sitemap: false
---

{:toc .large-only}

## Domain Sharding

- 한 도메인이 아닌 여러 도메인에 나눠서 요청을 보내 리소스들을 동시에 다운로드 받는 기술
- 예를 들어 CSS, img 등의 파일을 분할하여 일부는 static1.domain.com에서 다운로드하고 나머지는 static2.domain.com에서 받을 수 있다.
- 도메인 샤딩을 적용하는 이유는 대부분의 브라우저가 각 도메인에 허용되는 동시 다운로드 수를 6개 정도로 제한하기 때문
- 브라우저가 6개의 리소스를 병렬로 다운로드할 수 있고 웹 사이트에 6개의 리소스만 필요한 경우에는 필요하지 않다.

### 장점

- 여러 리소스를 동시에 다운 받을 수 있다.
- 페이지 로딩이 빠르다.

### 단점

- DNS 조회 시간 증가
- TCP 오버헤드 증가

## 정리

- HTTP1.1에서 다운받아야 할 리소스가 많은 경우에는 도메인 샤딩 기법을 사용하면 성능을 개선시킬 수 있다.
- 45개의 리소스를 사용하는 사이트를 대상으로 도메인 샤딩 기법을 사용한 결과 페이지 로딩 시간이 약 33% 단축되었다.
- 최신 브라우저를 사용하는 경우 HTTP2나 SPDY 프로토콜을 사용하면 도메인 샤딩 기법을 쓰지 않고도 충분히 성능을 개선할 수 있다.
- 하지만 위 프로토콜을 지원하지 않는 익스플로러 등의 구형 브라우저에서는 도메인 샤딩이 효과적일 수 있다.

## 참고사이트

[Domain Sharding](https://www.keycdn.com/support/domain-sharding)<br/>
[[web network] Domain Sharding 이란?](https://aroundck.tistory.com/5153)
