---
layout: post
title: "parameter와 argument"
sitemap: false
---

{:toc .large-only}

### parameter (매개변수)

parameter는 함수 정의에 나열된 이름입니다.

```js
function functionName(parameter1, parameter2, parameter3) {
  // code to be executed
}
```

### argument (전달인자)

argument는 함수에 전달되고 함수에 의해 수신되는 **실제 값**입니다.

multiply 함수를 호출할 때, a와 b는 parameter는, 입력값 5와 2는 argument입니다.

```js
function multiply(a, b) {
  return a * b;
}

multiply(5, 2); // 10
multiply(5); // NaN !
```

<br/>

[기본값 매개변수](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/Default_parameters)<br/>
[JavaScript 함수 매개 변수](https://www.w3schools.com/js/js_function_parameters.asp)<br/>
[argument와 parameter 차이점](http://taewan.kim/tip/argument_parameter/)
