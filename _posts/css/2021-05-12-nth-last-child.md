---
title: "끝에서 n개까지의 요소에 css 적용하기"
categories: [CSS]
tags: [css]
---

{:toc .large-only}

#### 끝에서 4개까지 적용한다고 했을 때

```html
<style>
  li {
    list-style: none;
    width: 50px;
    height: 50px;
    margin: 2%;
    background-color: orange;
    float: left;
  }
  li:nth-last-child(-n + 4) {
    background-color: green;
  }
</style>
<ul>
  <li>1</li>
  <li>2</li>
  <li>3</li>
  <li>4</li>
  <li>5</li>
  <li>6</li>
  <li>7</li>
  <li>8</li>
  <li>9</li>
  <li>10</li>
</ul>
```

<img src="/assets/img/blog/2021-05-12-nth-last-child.png">
