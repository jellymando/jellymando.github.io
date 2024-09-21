---
title: "url 프로토콜 체크하여 http ➡️ https로 변경"
categories: [Javascript]
tags: [javascript]
---

{:toc .large-only}

## http 체크하여 https로 변경

- window.location.href

현재 페이지의 href (URL)를 반환합니다.

- window.location.hostname

웹 호스트의 도메인 이름을 반환합니다.

- window.location.pathname

현재 페이지의 경로와 파일 이름을 반환합니다.

- window.location.protocol

사용 된 웹 프로토콜 (http : 또는 https :)을 반환합니다.

```js
if (document.location.protocol == "http:") {
  window.location.href = window.location.href.replace("http", "https");
}
```

<br/>

[JavaScript Window Location](https://www.w3schools.com/js/js_window_location.asp)<br/>
[[javascript] https 체크](http://blog.naver.com/PostView.nhn?blogId=zgabriel&logNo=221362570040&parentCategoryNo=&categoryNo=7&viewDate=&isShowPopularPosts=false&from=postView)
