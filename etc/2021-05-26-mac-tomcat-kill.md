---
layout: post
title: "Mac에서 톰캣 서버 강제 종료하기"
sitemap: false
---

{:toc .large-only}

터미널 실행 후

```js
sudo lsof -i:0000 // (실행되고 있는 port 번호)
// 비밀번호 입력 후 리스트에 나오는 PID 확인
kill -9 1849 // (PID 번호)
```
