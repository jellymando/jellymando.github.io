---
layout: post
title: "모바일에서 100vh 값이 100%보다 커서 페이지 밖으로 빠져나갈 때"
sitemap: false
---

{:toc .large-only}

### 모바일에서 100vh 값이 100%보다 클 때

모바일 브라우저는 PC와 달리 `vh` 값에 주소입력창을 포함하기 때문에 컨텐츠를 `100vh`로 지정하면 페이지 안에서 꽉 차는게 아니라 페이지보다 주소입력창 길이만큼 길어져 스크롤바가 생긴다.

<img src="https://jellymando.github.io/assets/img/_posts/2021-06-29-100vh_problem.jpg">

<br/>

`calc()`를 사용해 문제를 해결할 수 있다.

`100vh`에서 `100%`를 뺀 값을 2로 나눠 위로 땡겨준다.

```css
top: calc((100% - 100vh) / 2);
```
