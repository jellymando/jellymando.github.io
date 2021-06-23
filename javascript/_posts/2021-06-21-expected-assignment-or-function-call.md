---
layout: post
title: "JavaScript arrow function 주의사항"
sitemap: false
---

{:toc .large-only}

```text
Expected an assignment or function call and instead saw an expression  no-unused-expressions
```

함수 코드를 작성하다가 위와 같은 에러가 난다면 잘못된 화살표 함수 표현을 사용했을 수 있다.

### 화살표 함수에서 소괄호 () 와 중괄호 {} 사용

#### ()

```text
const Button = () => <button>Hello world</button>;

// 위와 아래는 같은 코드

const Button = () => (
    <button>Hello world</button>
);
```

[화살표 함수 - JavaScript | MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/Arrow_functions)에 따르면 화살표 함수의 경우 return문을 작성하지 않아도 소괄호 `()` 로 감싸진 부분이 return 된다.

#### {}

반면에 중괄호 `{}` 로 감싸진 다음과 같은 함수는 return문이 없다면 return 값을 반환하지 않는다.

```js
const Button = () => {
  <button>Hello world</button>;
};

console.log(Button); // undefined
```

<br/>

따라서 중괄호 `{}` 를 사용하여 return 값을 반환하는 함수를 만들려면 다음과 같이 return 문을 사용하여 코드를 작성해야 한다.

```js
const Button = () => {
  return <button>Hello world</button>;
};
```

### 기본 구문

```js
(param1, param2, …, paramN) => { statements }
(param1, param2, …, paramN) => expression
// 다음과 동일함:  => { return expression; }

// 매개변수가 하나뿐인 경우 괄호는 선택사항:
(singleParam) => { statements }
singleParam => { statements }

// 매개변수가 없는 함수는 괄호가 필요:
() => { statements }
```

### 고급 구문

```js
// 객체 리터럴 표현을 반환하기 위해서는 함수 본문(body)을 괄호 속에 넣음:
params => ({foo: bar})

// 나머지 매개변수 및 기본 매개변수를 지원함
(param1, param2, ...rest) => { statements }
(param1 = defaultValue1, param2, …, paramN = defaultValueN) => { statements }

// 매개변수 목록 내 구조분해할당도 지원됨
var f = ([a, b] = [1, 2], {x: c} = {x: a + b}) => a + b + c;
f();  // 6
```

<br/>

[JavaScript - 화살표 함수 사용 시 ()와 {} 사용상 주의할 점](https://velog.io/@bigbrothershin/JavaScript-%ED%99%94%EC%82%B4%ED%91%9C-%ED%95%A8%EC%88%98-%EC%82%AC%EC%9A%A9-%EC%8B%9C-%EC%99%80-%EC%82%AC%EC%9A%A9%EC%83%81-%EC%A3%BC%EC%9D%98%ED%95%A0-%EC%A0%90)<br/>
[[React 99% 에러잡기] Expected an assignment or function call and instead saw an expression no-unused-expressions](https://helicopter55.tistory.com/2)
