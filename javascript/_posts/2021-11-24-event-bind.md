---
layout: post
title: "이벤트 핸들러 내부의 this"
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

## 참고사이트

모던 자바스크립트 Deep Dive - 789p
