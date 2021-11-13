---
layout: post
title: "console.log()와 console.dir()의 차이점"
sitemap: false
---

{:toc .large-only}

## 차이

- `console.log()`는 여러개의 인자를 받고, `console.dir()`는 인자를 하나만 받는다.

- dom element를 `console.log()`와 `console.dir()`로 찍어보면 `console.log()`는 **HTML** 형식으로 출력되고, `console.dir()`는 **JSON**과 같은 트리 구조로 출력된다.

<img src="/assets/img/blog/2021-11-10-console-dir.png" style="margin-top:30px;">

## 참고사이트

[Console.log()](https://developer.mozilla.org/ko/docs/Web/API/Console/log)<br/>
[console.dir()](https://developer.mozilla.org/en-US/docs/Web/API/console/dir)<br/>
[Console API reference](https://developer.chrome.com/docs/devtools/console/api/#dir)