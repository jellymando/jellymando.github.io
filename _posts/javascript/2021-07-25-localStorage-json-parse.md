---
title: "localStorage에 객체, 배열 형식 데이터 저장하기"
categories: [JAVASCRIPT]
tags: [javascript]
---

{:toc .large-only}

localStorage는 value를 문자열로만 저장한다.

객체나 배열 형식의 데이터를 localStorage에 저장하거나 가져오려면 문자열로 파싱해야 한다.

### setItem

```js
localStorage.setItem("selectedMembers", JSON.stringify(selectedMembers));
```

### getItem

```js
const localMembers = localStorage.getItem("selectedMembers");
return localMembers ? JSON.parse(localMembers)
```

<br/>

[LocalStorage and JSON.stringify JSON.parse](https://stackoverflow.com/questions/23728626/localstorage-and-json-stringify-json-parse/23728844)
