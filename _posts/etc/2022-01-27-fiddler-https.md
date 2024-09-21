---
title: 'Fiddler 켜면 https 페이지 안열리는 이슈'
categories: [기타]
tags: [fiddler]
---

{:toc .large-only}

## 문제

Fiddler를 켜면 https 페이지가 아래와 같이 연결되지 않았다.

<img src="/assets/img/blog/2022-01-27-fiddler-https_01.png">

## 해결

Fiddler에서 https 인증서를 새로 발급받는다.

(Tools - Options - HTTPS - Actions - Reset All Certificates)

<img src="/assets/img/blog/2022-01-27-fiddler-https_02.png">

## 참고사이트

[연결이 비공개로 설정되어 있지 않습니다. (https 연결장애)](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=best798&logNo=221036498833)
