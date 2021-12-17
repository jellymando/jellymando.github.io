---
layout: post
title: "이벤트를 등록하는 방식, 이벤트 핸들러 내부의 this"
sitemap: false
---

{:toc .large-only}

## 이벤트 핸들러 attribute 방식

```html
<button onclick="handleClick()">Click me</button>
<script>
  function handleClick() {
    console.log(this); // window
  }
</script>
```

위 예제의 `handleClick` 함수 내부의 `this`는 전역 객체 window를 가리킨다.

일반 함수 내부의 `this`는 전역 객체를 가리키기 때문이다.

단, <u>이벤트 핸들러를 호출할 때 this를 인수로 전달하면 이벤트를 바인딩한 DOM 요소를 가리킨다.</u>

```html
<button onclick="handleClick(this)">Click me</button>
<script>
  function handleClick(button) {
    console.log(button); // 이벤트를 바인딩한 button 요소
    console.log(this); // window
  }
</script>
```

## addEventListener 방식

addEventListener 핸들러 내부의 `this`는 이벤트를 바인딩한 DOM 요소를 가리킨다.

```html
<button id="el">클릭해라</button>
<script>
  const button = document.getElementById("el");

  button.addEventListener("click", function () {
    console.log(this); // 이벤트를 바인딩한 button 요소
  });
</script>
```

arrow function으로 정의한 이벤트 핸들러 내부의 `this`는 상위 스코프의 `this`를 가리킨다.

<u>arrow function은 함수 자체의 this 바인딩을 갖지 않는다.</u>

```html
<button id="el">클릭해라</button>
<script>
  const button = document.getElementById("el");

  button.addEventListener("click", () => {
    console.log(this); // window
  });
</script>
```

이 경우에는 `e.currentTarget`을 통해 button 요소에 접근할 수 있다.

```html
<button id="el">클릭해라</button>
<script>
  const button = document.getElementById("el");

  function handleClick() {
    console.log("handleClick", this);
  }

  button.addEventListener("click", (e) => {
    console.log(e.currentTarget); // button 요소
  });
</script>
```

## 두 방식의 차이점

- addEventListener는 하위 버전의 브라우저에서 지원하지 않는다.

- attribute 방식으로는 하나의 콜백 함수(리스너)만 지정할 수 있지만, addEventListener는 여러 개의 이벤트 리스너를 추가할 수 있다.

```html
<div id="div1">Click me!</div>
<script>
  document.getElementById("div1").onclick = function (e) {
    alert("do process #1");
  };
  document.getElementById("div1").onclick = function (e) {
    alert("do process #2");
  };
</script>
<!-- 위 코드의 경우 클릭을 해보면 #2만 출력된다. -->

<div id="div2">Click me!</div>
<script>
  document.getElementById("div2").addEventListener("click", function (e) {
    alert("do process #1");
  });
  document.getElementById("div2").addEventListener("click", function (e) {
    alert("do process #2");
  });
</script>
<!-- 위 코드의 경우 클릭을 해보면 #1과 #2 모두 출력된다. -->
```

- JavaScript 모듈 또는 다른 라이브러리와 확장이 용이하기 때문에 모질라 등 개발자 포럼에서 addEventListener 사용을 더 추천하고 있다!

## 참고사이트

모던 자바스크립트 Deep Dive - 789p<br/>
[[js] 자바스크립트 onclick · addEventListener 비교 사용법](https://goddino.tistory.com/68)<br/>
[[자바스크립트] 이벤트 핸들러(리스너) 등록과 addEventListener/attachEvent vs onload 차이점](https://unikys.tistory.com/312)
