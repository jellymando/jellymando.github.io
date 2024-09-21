---
title: "[error] eslint ts 적용되지 않음, prettier/prettier 에러"
categories: [REACT]
tags: [react, error, eslint, prettier]
---

{:toc .large-only}

<img src="/assets/img/blog/2021-08-08-prettier-error.png">

<br/>

prettier/prettier 에러가 뜨거나 .ts 파일을 lint하지 못할 때 `setting.json` 파일을 아래 코드를 추가해준다.

```js
"typescript.format.enable": false,
"eslint.alwaysShowStatus": true,
"eslint.autoFixOnSave": true,
```

<br/>

[ESLint 를 이용한 코드 규격화](https://7stocks.tistory.com/101)
