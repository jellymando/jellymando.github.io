---
layout: post
title: "fancytree 라이브러리"
sitemap: false
---

{:toc .large-only}

## Fancytree

jQuery 라이브러리인 dynatree.js migrate 하면서 정리

하지만 모르겠다 ㅡㅡ

#### treeNode.rootNode

```js
var treeNode = {};

$("#tree").fancytree({
    // ...
    init: function(event, data){
    treeNode.rootNode = data.tree.rootNode;
```

#### [메서드](https://wwwendt.de/tech/fancytree/doc/jsdoc/FancytreeNode.html)

`treeNode.rootNode.addChildren().setActive()`
