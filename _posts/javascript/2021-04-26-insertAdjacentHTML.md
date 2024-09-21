---
title: "element 안에 html 집어넣기 : insertAdjacentHTML()"
categories: [JAVASCRIPT]
tags: [javascript]
---

{:toc .large-only}

```js
element.insertAdjacentHTML(position, text);
```

- position
  - 'beforebegin' : element 앞에
  - 'afterbegin' : element 안에 가장 첫번째 child
  - 'beforeend' : element 안에 가장 마지막 child
  - 'afterend' : element 뒤에

```html
<!-- beforebegin -->
<p>
  <!-- afterbegin -->
  foo
  <!-- beforeend -->
</p>
<!-- afterend -->
```

> beforebegin , afterend position은 element의 부모가 존재해야 하고, node가 tree 안에 있어야 한다.

```js
var d1 = document.getElementById("one");
d1.insertAdjacentHTML("afterend", '<div id="two">two</div>');
```
