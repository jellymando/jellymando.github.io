---
title: "[Array] filter()와 find()의 차이점"
categories: [JAVASCRIPT]
tags: [javascript]
---

{:toc .large-only}

`filter()` 메서드는 주어진 함수의 테스트를 통과하는 모든 요소를 모아 **새로운 배열**로 반환합니다.

`find()` 메서드는 주어진 판별 함수를 만족하는 **첫 번째 요소의 값**을 반환합니다. 그런 요소가 없다면 `undefined`를 반환합니다.

만약 배열에서 특정 값을 가진 배열을 <u>새로 만들고 싶다면</u> `filter()`를, <u>특정 값을 가진 요소를 수정하고 싶다면</u> `find()`를 사용하면 되겠다.

<br/>

[Array.prototype.filter()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)<br/>
[Array.prototype.find()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/find)
