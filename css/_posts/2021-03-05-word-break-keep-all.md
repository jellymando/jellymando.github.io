---
layout: post
title: "일본어/중국어 word-break: keep-all; 단어길이가 길 경우 줄바꿈"
sitemap: false
---

{:toc .large-only}

word-break: keep-all 로 단어 사이에서 줄바꿈

하지만 일본어와 같이 단어 사이에 띄어쓰기가 없는 경우 줄이 바뀌지 않고 영역을 넘어 쭉 이어진다..

word-wrap: break-word를 추가해도 변함 없음....

설마 했는데 width값을 설정하니 해결되었다.

```js
width: 100%;
word-break: keep-all;
word-wrap: break-word;
```

[word-break 속성과 word-wrap 속성 알아보기](wit.nts-corp.com/2017/07/25/4675)
