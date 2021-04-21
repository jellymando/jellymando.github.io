---
layout: post
title: "html element의 data에 접근하기"
sitemap: false
---

{:toc .large-only}

엘리멘트에 `data-` 속성을 추가하고 javascript를 이용하여 속성 값을 가져올 때 dataset을 사용한다.

```html
<article
  id="electriccars"
  data-columns="3"
  data-index-number="12314"
  data-parent="cars"
>
  ...
</article>
```

<br/>

```js
var article = document.getElementById("electriccars");

article.dataset.columns; // "3"
article.dataset.indexNumber; // "12314"
article.dataset.parent; // "cars"
```

<br/>

[데이터 속성 사용하기](developer.mozilla.org/ko/docs/Learn/HTML/Howto/Use_data_attributes)
